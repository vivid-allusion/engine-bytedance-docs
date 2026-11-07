---
title: "DataImport"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DataImport"
---

<span id="overview"></span>
# Overview

Import data into a Collection. The file column names must match the Collection Fields exactly, otherwise parsing will fail.

Please authorize VikingDB for cross\-service access to TOS before use: [Authorize](https://console.volcengine.com/iam/service/attach_role/?ServiceName=vikingdb)

<span id="method-definition"></span>
# Method Definition

The Go SDK uses the client instance created by `vikingdb.New(sess)` to call the `CreateVikingdbTask(input)` method to initiate a task creation request. The input parameter is of type `vikingdb.CreateVikingdbTaskInput`, which contains the complete configuration information required for task creation.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |string |No |Project name |
|CollectionName | |string |1 of 2 required |Collection name |
|ResourceId | |string | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|TaskType | |string |Yes |data_import |
|TaskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Task specific configuration |
| |FileType |string |Yes |File type, json or parquet, required |
| |TosPath |string |Yes |TOS path, format: {bucket name}/{path}, note this is not a domain name. Required |
| |IgnoreError |bool |No |When set to true, parsing continues when encountering erroneous data, default is false |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Description |
|---|---|---|
|TaskId |string |Task ID |
|Message |string |Operation result message |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )

    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := &vikingdb.CreateVikingdbTaskInput{
       TaskType: volcengine.String(vikingdb.EnumOfTaskTypeForCreateVikingdbTaskInputDataImport),
       TaskConfig: &vikingdb.TaskConfigForCreateVikingdbTaskInput{
          FileType: volcengine.String(vikingdb.EnumOfFileTypeForCreateVikingdbTaskInputJson),
          TosPath:  volcengine.String("your-tos-bucket-name/path/data.json"),
       },
       ProjectName:    volcengine.String("default"),
       CollectionName: volcengine.String("Your Collection Name"),
    }

    resp, err := svc.CreateVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.TaskId)
}
```
