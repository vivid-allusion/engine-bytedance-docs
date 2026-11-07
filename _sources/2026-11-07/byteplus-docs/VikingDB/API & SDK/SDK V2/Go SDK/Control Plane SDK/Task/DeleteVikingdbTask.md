---
title: "DeleteVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DeleteVikingdbTask"
---

<span id="overview"></span>
# Overview

Deletes the specified task. The task will be terminated after deletion.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `DeleteVikingdbTask(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a task deletion request. The input parameter type is `vikingdb.DeleteVikingdbTaskInput`, which contains the parameter information required for task deletion.

<span id="request-parameters"></span>
# Request Parameters


|Field Name |Type |Required |Description |
|---|---|---|---|
|TaskId |string |Yes |Task ID, returned when the task is created |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |string |success |Operation result information |


<span id="example"></span>
# Example

```go
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

    input := &vikingdb.DeleteVikingdbTaskInput{
       TaskId: volcengine.String("your-task-id"),
    }

    resp, err := svc.DeleteVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.Message)
}
```
