---
title: "searchByVector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByVector"
---

<span id="overview"></span>
# Overview

searchByVector is used for vector search. It searches for the limit number of vectors closest to the query vector.


* After Collection data is written/deleted, Index data update takes approximately 20s, so it cannot be retrieved in the Index immediately.

* When the request parameter filter is configured, it indicates hybrid search; when the request parameter filter is not configured, it indicates pure vector search.


<span id="prerequisites"></span>
# Prerequisites


* When creating a dataset through the CreateVikingdbCollection interface, the defined fields have added the vector field.

* When writing data through the UpsertData interface, the field names and field values of vector type have been written.

* When creating an index through CreateVikingdbIndex, the vector_index vector index has been created.


Applicable when selecting "Existing vector data" when creating a vector database: When the imported data is a vector, this interface can be used to input vectors for retrieval.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByVectorRequest`, and its fields are shown in the following table.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|DenseVector |[]float64 |Yes |Dense vector for retrieval, length must be consistent with the index dimension. |
|SparseVector |map[string]float64 |No |Sparse vector representation (such as BOW), used for hybrid retrieval with DenseVector. |
|Filter |map[string]interface{} |No |Scalar filter conditions, see **Scalar Filtering**<br><br><br>* If not filled, it indicates pure vector retrieval.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|OutputFields |[]string |No |List of scalar fields to return.<br><br><br>1. If not set, returns all scalar fields in the collection.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. The field name must exist in the collection schema, otherwise the request will report an error. |
|Limit |int |No |Limit the number of returned items, maximum 5000. |
|Offset |int |No |Pagination offset, default 0, deep pagination performance overhead occurs when it is too large. |
|Partition |string |No |Only retrieve the specified partition, by default search all partition data. |
| | | | |
|Advance |SearchAdvance |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Search Common Parameters](https://docs.byteplus.com/docs/84313/1927082). |


<span id="return-parameters"></span>
# Return Parameters


|Name |Type |Description |
|---|---|---|
|RequestId |string |Request link ID. |
|Code |string |Service return code, Success indicates success. |
|Message |string |Error or prompt message. |
|Api |string |The specific API name called. |
|Result |SearchResult |Retrieval result body, structure as shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|Data |[]SearchItemResult |List of retrieved results, structure as shown below. |
|FilterMatchedCount |int |Total number of documents that meet the filter conditions. |
|TotalReturnCount |int |Number of results returned this time. |
|RealTextQuery |string |The real query string after possible model correction. |
|TokenUsage |map[string]interface{} |Token measurement information. |



* SearchItemResult



|**Attribute** |Type |**Description** |
|---|---|---|
|ID |interface{} |Primary key id. |
|Fields |map[string]interface{} |The fields field in the request response. |
|Score |float64 |Similarity score. |
|AnnScore |float64 |ANN score. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

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
       limit       = 10
       denseVector = make([]float64, 0, 4096) // 4096 is the dimension of the vector
    )
    for i := 0; i < 4096; i++ {
       denseVector = append(denseVector, 0.5)
    }

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).SearchByVector(ctx, model.SearchByVectorRequest{
       SearchBase: model.SearchBase{
          Limit: &limit,
       },
       DenseVector: denseVector,
    })

    if err != nil {
       fmt.Println("SearchByVector failed, err: ", err)
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
