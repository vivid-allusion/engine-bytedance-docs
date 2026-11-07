---
title: "ListVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/ListVikingdbTask"
---

<span id="overview"></span>
# Overview

Get information for multiple tasks, returning up to 20 items at once.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `ListVikingdbTask(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a task list query request. The input parameter is of type `vikingdb.ListVikingdbTaskInput`, which contains the parameters required for the task list query.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |string |No |Project name |
|CollectionName |string |2 out of 1 |Collection name |
|ResourceId |string | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|TaskStatus |string |Yes |Task status, see below |
|TaskType |string |Yes |Task type, see below |
|PageNumber |int |No |Page number for pagination. Starts at 1. |
|PageSize |int |No |Page size for pagination. |


<span id="response-parameters"></span>
# Response Parameters


|Field |Type |Sub\-field Description |
|---|---|---|
|Tasks |[]TaskForListVikingdbTaskOutput |Task list |
|PageSize |int | |
|PageNumber |int | |
|TotalCount |int | |



* List



|**Attribute** | |**Type** |**Description** |
|---|---|---|---|
|TaskId | |string |Task ID |
|TaskConfig | |TaskConfigForListVikingdbTaskOutput | |
| |CollectionName |string | |
| |ExportAll |bool | |
|TaskType | |string |Task type |
|TaskStatus | |string |Task status |
|UpdatePerson | |string |Task updater |
|UpdateTime | |string |Task information update time |
|CreateTime | |string |Task information creation time |
|TaskProcessInfo | |TaskProcessInfoForListVikingdbTaskOutput |Task processing information, see below |



* TaskType includes



|TaskType<br><br>data_import |Description<br><br>Data import task |
|---|---|
|data_export |Data export task |
|filter_update |Data filter update task |
|filter_delete |Data filter delete task |



* TaskStatus includes



|init |queued |running |done |fail |
|---|---|---|---|---|
|Initializing |Queued |Running |Done |Failed |



* TaskProcessInfoForListVikingdbTaskOutput includes



|**Field** |**Type** |**Description** |
|---|---|---|
|TaskProgress |string |Task progress, e.g. 50% |
|ErrorMessage |string |Task error message |
|SampleData |[]SampleDataForGetVikingdbTaskOutput |Sample 5 data items for display |
|SampleTimestamp |int |Sample timestamp, data written afterward will not be processed |
|ScanDataCount |int |Current scanned data count |
|TotalDataCount |int |Total number of data items in collection (estimated) |
|TotalFilterCount |int |Already filtered data |


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

    input := &vikingdb.ListVikingdbTaskInput{
       ProjectName:    volcengine.String("default"),
       CollectionName: volcengine.String("Your Collection Name"),
    }

    resp, err := svc.ListVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.TotalCount)
    for _, task := range resp.Tasks {
       fmt.Println(*task.TaskId, *task.TaskStatus)
    }
}
```


 &nbsp;
