---
title: "searchByScalar"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByScalar"
---

<span id="overview"></span>
# Overview

This interface applies to indexes containing scalar index fields of int64/float32 type. Scalar search in a vector database refers to a search method based on scalar values. In a vector database, each vector has one or more scalar values. Scalar search can retrieve data based on these scalar values to find data related to the query, such as author feature retrieval in document retrieval.

SearchByScalar returns results sorted/paginated by scalar field.

<span id="request-parameters"></span>
# Request Parameters

The request parameter is `SearchByScalarRequest`, whose fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Field |string |Yes |Scalar field used for sorting, must be int64/float32 and have a scalar index established. |
|Order |string |No |Sort direction, values `asc`/`desc`, default `desc`. |
|Filter |map[string]interface{} |No |Scalar filter condition, see **Scalar Filtering** for details.<br><br><br>* If not filled, sorting is performed on the full index.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|OutputFields |[]string |No |List of scalar fields to return.<br><br><br>1. When not set, all scalar fields in the collection are returned.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. Field names must exist in the collection schema, otherwise the request will report an error. |
|Limit |int |No |Limit the number of returned items, maximum 5000. |
|Offset |int |No |Pagination offset, default 0, excessive value will cause deep pagination performance overhead. |
|Partition |string |No |Only search the specified partition, search all partitions by default. |
|Advance |SearchAdvance |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082) for details<br><br>. |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|RequestId |string |Request link ID. |
|Code |string |Service return code, Success indicates success. |
|Message |string |Error or prompt message. |
|Api |string |Specific API name called. |
|Result |SearchResult |Search result body, see structure below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|Data |[]SearchItemResult |Recalled result list, see structure below. |
|FilterMatchedCount |int |Total number of documents meeting the filter conditions. |
|TotalReturnCount |int |Number of results returned this time. |
|RealTextQuery |string |Real query string possibly corrected by the model. |
|TokenUsage |map[string]interface{} |Token metering information. |



* SearchItemResult



|**Attribute** |Type |**Description** |
|---|---|---|
|ID |interface{} |Primary key id. |
|Fields |map[string]interface{} |Fields field in the request response. |
|Score |float64 |Similarity. |
|AnnScore |float64 |ANN score. |


<span id="example"></span>
# Example

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
       field = "score"
    )

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).SearchByScalar(ctx, model.SearchByScalarRequest{
       SearchBase: model.SearchBase{
          Limit: &limit,
       },
       Field: &field,
       Order: model.ScalarOrderAsc,
    })

    if err != nil {
       fmt.Println("SearchByScalar failed, err: ", err)
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
