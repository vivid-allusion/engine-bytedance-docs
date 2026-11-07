---
title: "updateData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateData"
---

<span id="overview"></span>
# Overview

updateData is used to update partial fields of existing data. Supports updating text, scalar fields, and vector fields.

<span id="request-parameters"></span>
# **Request Parameters**


|Name |Type |Description |Required |
|---|---|---|---|
|CollectionName |string |Collection name, alternative to resource_id. |One of two required |
|ResourceID |string |Collection resource ID. | |
|Data |[]map[string]any |List of data to be updated, maximum 100 items per request, must include primary key fields and fields to be modified. |Yes |
|TTL |int |New TTL (Time To Live) after update, in seconds. |No |
|Async |bool |Asynchronous write switch. Default: false. Asynchronous writing can increase QPS by 10 times, but will increase the latency of data entering the index, suitable for large\-scale offline data ingestion. |No |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Response Body Common Parameters Introduction" below). The `result` field type is UpdateDataResult:


* UpdateDataResult



|Name |Type |Description |
|---|---|---|
|TokenUsage |map[string]interface{} |Token consumption involved in this write operation, fields are related to the metering strategy. |


<span id="response-body-common-parameters-introduction"></span>
## Response Body Common Parameters Introduction


|Parameter Name |Type |Description |
|---|---|---|
|RequestID |string |Request ID. |
|Code |string |Operation status code. `Success` for success, otherwise an error code phrase. |
|Message |string |Execution information. `The API call was executed successfully.` for success, otherwise an error message. |
|Result |map[string]interface{} |Operation result. If no data needs to be returned, `result = null`. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/vikingdb-go-sdk/vector"
    "github.com/volcengine/vikingdb-go-sdk/vector/model"
    "os"
    "time"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       endpoint  = "https://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
       region    = "ap-southeast-1"
    )

    client, err := vector.New(
       vector.AuthIAM(accessKey, secretKey), // IAM auth
       // vector.AuthAPIKey(apiKey),            // APIKey auth
       vector.WithEndpoint(endpoint),
       vector.WithRegion(region),
       vector.WithTimeout(time.Second*30),
       vector.WithMaxRetries(3),
    )
    if err != nil {
       fmt.Println("New client failed, err: ", err)
       panic(err)
    }
    ctx := context.Background()

    resp, err := client.Collection(model.CollectionLocator{
       CollectionName: "Your Collection Name",
    }).Update(ctx, model.UpdateDataRequest{
       WriteDataBase: model.WriteDataBase{
          Data: []model.MapStr{
             {
                "id":      1,
                "type":    "type1",
                "name":    "vikingdb data",
                "content": "vikingdb is a vector database...",
             },
          },
       },
    })
    if err != nil {
       fmt.Println("Update failed, err: ", err)
       panic(err)
    }

    fmt.Println(resp.Message)
}
```
