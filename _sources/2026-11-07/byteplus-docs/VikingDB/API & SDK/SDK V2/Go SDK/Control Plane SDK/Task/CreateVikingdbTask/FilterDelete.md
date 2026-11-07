---
title: "FilterDelete"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FilterDelete"
---

<span id="overview"></span>
# Overview

Batch delete data in a Collection based on specific conditions.

<span id="method-definition"></span>
# Method Definition

The Go SDK uses a client instance created via `vikingdb.New(sess)` to call the `CreateVikingdbTask(input)` method to initiate a task creation request. The input parameter is of type `vikingdb.CreateVikingdbTaskInput`, which contains the complete configuration information required for task creation.

<span id="request-parameters"></span>
# Request Parameters

To back up data to TOS, first authorize VikingDB for cross\-service access to TOS: [Authorize](https://console.volcengine.com/iam/service/attach_role/?ServiceName=vikingdb)


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |string |No |Project name |
|CollectionName | |string |2 out of 1 |Collection name |
|ResourceId | |string | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|**TaskType** | |string |Yes |filter_delete |
|TaskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Task specific configuration |
| |FileType |string |Yes |Backup file type, json or parquet. Required. |
| |NeedConfirm |bool |No |Whether manual confirmation is required, default is true. |
| |FilterConds |[]interface{} |Yes |Filter conditions. Usage reference: https://www.volcengine.com/docs/84313/1791133 |
| |TosPath |string |Yes |TOS path, format: {bucket name}/{path}, note this is not a domain name. Required. |


<span id="return-parameters"></span>
# Return Parameters


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

    // Create filter delete task
    input := &vikingdb.CreateVikingdbTaskInput{
       TaskType: volcengine.String(vikingdb.EnumOfTaskTypeForCreateVikingdbTaskInputFilterDelete),
       TaskConfig: &vikingdb.TaskConfigForCreateVikingdbTaskInput{
          FilterConds: []interface{}{
             map[string]interface{}{
                "op":    "must",
                "field": "name",
                "conds": []string{"old value1", "old value2"},
             },
          },
          NeedConfirm: volcengine.Bool(true),
          TosPath:      volcengine.String("your-bucket/path/to/backup.json"),
          FileType:     volcengine.String("json"),
       },
       CollectionName: volcengine.String("Your Collection Name"),
       ProjectName:    volcengine.String("default"),
    }

    resp, err := svc.CreateVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.TaskId)
}
```


<span id="return-parameters"></span>
## Return Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|TaskId |string | |Task ID |
|Message |string |success |Operation result message |


<span id="follow-up-processing"></span>
## Follow\-up Processing

If NeedConfirm is true and manual confirmation is required, you can perform the **Update Task** operation for confirmation.
