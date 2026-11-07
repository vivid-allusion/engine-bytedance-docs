---
title: "GetVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/GetVikingdbTask"
---

<span id="overview"></span>
# Overview

Query the detailed information and execution progress of a specified Task.

<span id="method-definition"></span>
# Method Definition

The Go SDK uses the client instance created by `vikingdb.New(sess)` to call the `GetVikingdbTask(input)` method to initiate a task query request. The input parameter is of type `vikingdb.GetVikingdbTaskInput`, which contains the parameter information required for the task query.

<span id="request-parameters"></span>
# Request Parameters


|Field Name |Type |Required |Description |
|---|---|---|---|
|TaskId |string |Yes |Task ID, returned when the task is created |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |**Type** |**Description** |
|---|---|---|
|TaskId |string |Task ID |
|TaskType |string |Task Type |
|TaskStatus |string |Task Status |
|UpdatePerson |string |Task updater |
|UpdateTime |string |Task information update time |
|CreateTime |string |Task information creation time |
|TaskProcessInfo |TaskProcessInfoForGetVikingdbTaskOutput |Task processing information, such as progress |



* task_type types include



|data_import |Data import task |
|---|---|
|data_export |Data export task |
|filter_update |Data filter update task |
|filter_delete |Data filter delete task |



* task_status includes



|init |queued |confirm |confirmed |running |done |fail |
|---|---|---|---|---|---|---|
|Initializing |Queued |Requires manual confirmation |Confirmed |Running |Done |Failed |



* TaskProcessInfoForGetVikingdbTaskOutput



|**Field** |**Type** |**Description** |
|---|---|---|
|TaskProgress |string |Task progress, e.g. 50% |
|ErrorMessage |string |Task error message |
|SampleData |[]SampleDataForGetVikingdbTaskOutput |Sample 5 data items for display |
|SampleTimestamp |int |Sampling timestamp, data written later will not be processed |
|ScanDataCount |int |Current scanned data volume |
|TotalDataCount |int |Total number of data items in the collection (estimated) |
|TotalFilterCount |int |Data that has been filtered out |


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

    input := &vikingdb.GetVikingdbTaskInput{
       TaskId: volcengine.String("your-task-id"),
    }

    resp, err := svc.GetVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.TaskStatus)
    fmt.Println(*resp.TaskType)
}
```
