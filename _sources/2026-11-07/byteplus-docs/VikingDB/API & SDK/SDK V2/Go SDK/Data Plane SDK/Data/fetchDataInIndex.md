---
title: "fetchDataInIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetchDataInIndex"
---

<span id="overview"></span>
# Overview

FetchDataInIndex is used for Index data queries. It queries one or more data entries in the specified Index based on the primary key ID, with a maximum of 100 entries per query.

After Collection data is written/deleted, there is a synchronization delay in Index data updates, typically around 10 seconds, so the data cannot be queried in the Index immediately.

<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|CollectionName |string |Either this or ResourceID |Collection name, either this or ResourceID must be provided. |
|ResourceID |string | |Collection resource ID. |
|IndexName |string |Yes |Index name. |
|IDs |[]interface{} |Yes |List of primary keys for point query, maximum 100 entries. |
|Partition |string |No |Filter index data by partition. |
|OutputFields |[]string |No |Control the returned scalar fields:<br><br><br>1. When not provided, all scalar fields are returned.<br><br>2. If an empty list is passed, only vectors and IDs are returned.<br><br>3. If a field does not exist or has an incorrect format, an error will be directly reported. |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Common Response Body Parameters" below). The `Result` field type is FetchDataInIndexResult:


* FetchDataInIndexResult



|Name |Type |Description |
|---|---|---|
|Items |[]IndexDataItem |Matched index data. |
|IDsNotExist |[]interface{} |Unmatched primary keys. |



* IndexDataItem



|Name |Type |Description |
|---|---|---|
|ID |interface{} |Data primary key. |
|Fields |map[string]interface{} |Scalar fields. |
|DenseVector |[]float64 |Persisted dense vector. |
|DenseDim |int |Vector dimension. |


<span id="common-response-body-parameters"></span>
## Common Response Body Parameters


|Parameter Name |Type |Description |
|---|---|---|
|RequestID |string |Request ID. |
|Code |string |Operation status code. Success is `Success`, otherwise it is an error code phrase. |
|Message |string |Execution information. On success, it is `The API call was executed successfully.`. |
|Result |map[string]interface{} |Operation result. If no data needs to be returned, `Result = null`. |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

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

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).Fetch(ctx, model.FetchDataInIndexRequest{
       IDs: []interface{}{ 1 },
    })
    if err != nil {
       fmt.Println("Fetch failed, err: ", err)
       panic(err)
    }

    fmt.Println(resp.Message)
}
```
