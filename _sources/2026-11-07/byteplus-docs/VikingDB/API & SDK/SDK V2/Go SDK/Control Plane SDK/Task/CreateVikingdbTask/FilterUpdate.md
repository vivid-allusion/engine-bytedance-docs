---
title: "FilterUpdate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FilterUpdate"
---

<span id="overview"></span>
# Overview

Bulk update data by specific conditions. Updating vector, sparse_vector, and text type fields is not supported.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `CreateVikingdbTask(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a task creation request. The input parameter is of type `vikingdb.CreateVikingdbTaskInput` and contains complete configuration information required for task creation.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |string |No |Project name |
|CollectionName | |string |Either one required |Collection name |
|ResourceId | |string | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|**TaskType** | |string |Yes |filter_update |
|TaskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Specific task configuration |
| |FilterConds |[]interface{} |Yes |Filter conditions. For usage reference: https://www.volcengine.com/docs/84313/1791133 |
| |UpdateFields |interface{} |Yes |Field values to be updated. Must be scalar fields. Updating vector, sparse_vector, and text type fields is not supported. |


<span id="return-parameters"></span>
# Return Parameters


|Parameter |Type |Description |
|---|---|---|
|TaskId |string |Task ID |
|Message |string |Operation result information |


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

    // Create update task
    input := &vikingdb.CreateVikingdbTaskInput{
       TaskType: volcengine.String(vikingdb.EnumOfTaskTypeForCreateVikingdbTaskInputFilterUpdate),
       TaskConfig: &vikingdb.TaskConfigForCreateVikingdbTaskInput{
          FilterConds: []interface{}{
             map[string]interface{}{
                "op":    "must",
                "field": "name",
                "conds": []string{"old value1", "old value2"},
             },
          },
          UpdateFields: map[string]interface{}{
             "name": "new value",
          },
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


<span id="response-example"></span>
## Response Example

```Go
fmt.Println(*resp.TaskId)
fmt.Println(*resp.Message)
```
