---
title: "UpdateVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/UpdateVikingdbTask"
---

<span id="overview"></span>
# Overview

Update the specified task. Currently, task update is only used for the manual confirmation step of **deleting a task**.

<span id="method-definition"></span>
# Method Definition

The Go SDK uses the client instance created by `vikingdb.New(sess)` to call the `UpdateVikingdbTask(input)` method to initiate a task update request. The input parameter type is `vikingdb.UpdateVikingdbTaskInput`, which contains the complete configuration information required for task update.

<span id="request-parameters"></span>
# Request Parameters


|Field Name |Type |Required |Description |
|---|---|---|---|
|TaskId |string |Yes |Task ID, returned when the task is created |
|TaskStatus |string |Only the `confirm` status can be updated, and it can only be updated to `confirmed`. Required | |
| | | | |
| | | | |
| | | | |
| | | | |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |string |success |Operation result message |


<span id="example"></span>
# Example

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

    input := &vikingdb.UpdateVikingdbTaskInput{
       TaskId:     volcengine.String("your-task-id"),
       TaskStatus: volcengine.String(vikingdb.EnumOfTaskStatusForUpdateVikingdbTaskInputConfirmed),
    }

    resp, err := svc.UpdateVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.Message)
}
```


<span id="notes"></span>
## Notes

Only supports updating the task status from `confirm` to `confirmed`.
