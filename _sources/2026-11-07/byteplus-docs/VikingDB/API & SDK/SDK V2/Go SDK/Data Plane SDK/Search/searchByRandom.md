---
title: "searchByRandom"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByRandom"
---

<span id="overview"></span>
# Overview

Random search is a retrieval method that randomly returns several records from a dataset when no query content is specified. Random search also supports filtering and post\-processing of search results, and can be used for scenarios such as comparing recall effects and data filtering. searchByRandom randomly returns several records from data that meets the filter conditions.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByRandomRequest`, and its fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Filter |map[string]interface{} |No |Scalar filter conditions, see **Scalar Filtering**.<br><br><br>* If not filled, returns randomly from the full collection data.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|OutputFields |[]string |No |List of scalar fields to return.<br><br><br>1. Returns all scalar fields in the collection when not set.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. The field name must exist in the collection schema, otherwise the request will report an error. |
|Limit |int |No |Limit the number of returned results, maximum 5000. |
|Offset |int |No |Pagination offset, default 0. |
|Partition |string |No |Only search the specified partition, default search all partitions. |
|Advance |SearchAdvance |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082)<br><br>. |


<span id="return-parameters"></span>
# Return Parameters


|Name |Type |Description |
|---|---|---|
|RequestId |string |Request link ID. |
|Code |string |Service return code, Success indicates success. |
|Message |string |Error or prompt information. |
|Api |string |Name of the specific API called. |
|Result |SearchResult |Search result body, structure is shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|Data |[]SearchItemResult |List of recalled results, structure is shown below. |
|FilterMatchedCount |int |Total number of documents that meet the filter conditions. |
|TotalReturnCount |int |Number of results returned this time. |
|RealTextQuery |string |Real query string after possible model correction (returned by some interfaces). |
|TokenUsage |map[string]interface{} |Token measurement information. |



* SearchItemResult



|**Attribute** |Type |**Description** |
|---|---|---|
|ID |interface{} |Primary key id. |
|Fields |map[string]interface{} |fields field in the request return result. |
|Score |float64 |Similarity |
|AnnScore |float64 |ann score |


<span id="request-example"></span>
## Request Example

```go
package main

import (
    "context"
    "encoding/json"
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

    var (
       limit = 10
    )

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).SearchByRandom(ctx, model.SearchByRandomRequest{
       SearchBase: model.SearchBase{
          Limit: &limit,
       },
    })

    if err != nil {
       fmt.Println("SearchByRandom failed, err: ", err)
       panic(err)
    }

    jsonData, err := json.Marshal(resp.Result)
    if err != nil {
       fmt.Println("Marshal result failed, err: ", err)
       panic(err)
    }
    fmt.Println(string(jsonData))
}
```
