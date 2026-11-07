---
title: "fetchDataInCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetchDataInCollection"
---

<span id="overview"></span>
# Overview

Query single or multiple data entries in a specified Collection by primary key, up to 100 entries per query.

Data can be queried in real\-time after being written to or deleted from the Collection.

<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|CollectionName |string |2 out of 1 |Collection name, either this or ResourceID must be provided. |
|ResourceID |string | |Collection resource ID. |
|IDs |[]interface{} |Yes |* List of primary keys to query, maximum 100 entries. |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Response Body Common Parameters Introduction" below). The `Result` field type is FetchDataInCollectionResult:


* FetchDataInCollectionResult



|Name |Type |Description |
|---|---|---|
|Items |[]DataItem |List of matched data entries, structure shown below. |
|NotFoundIDs |[]string |List of primary keys that were not matched. |



* DataItem



|Name |Type |Description |
|---|---|---|
|ID |interface{} |Primary key of the data entry. |
|Fields |map[string]interface{} |All scalar fields, key is the field name. |


<span id="response-body-common-parameters-introduction"></span>
## Response Body Common Parameters Introduction


|Parameter Name |Type |Description |
|---|---|---|
|RequestID |string |Request ID. |
|Code |string |Operation status code. `Success` on success, otherwise an error code phrase. |
|Message |string |Execution information. `The API call was executed successfully.` on success. |
|Result |FetchDataInCollectionResult |Operation result. If no data needs to be returned, `Result = null`. |


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
    }).Fetch(ctx, model.FetchDataInCollectionRequest{
       IDs: []interface{}{1},
    })
    if err != nil {
       fmt.Println("Fetch failed, err: ", err)
       panic(err)
    }

    fmt.Println(resp.Message)
}
```
