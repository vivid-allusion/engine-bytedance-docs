---
title: "searchById"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchById"
---

<span id="overview"></span>
# Overview

searchById is used for primary key ID retrieval. Based on the primary key ID, it searches for the limit number of vectors that are closest to it.


* For hybrid indexes using the hnsw\-hybrid algorithm, ID\-based retrieval is temporarily not supported.

* After Collection data is written/deleted, Index data update is expected to take 20s, so it cannot be retrieved immediately in the Index.

* When the request parameter filter is configured, it indicates hybrid search; when the request parameter filter is not configured, it indicates pure vector search.


<span id="prerequisites"></span>
# Prerequisites


* When creating a dataset through the createCollection interface, the defined fields have already added the vector field.

* When writing data through the upsertData interface, the field names and field values of vector type have been written.

* When creating an index through the createIndex interface, the vectorIndex vector index has been created.


<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Parameter Description** |
|---|---|---|---|
|ID |interface{} |Yes |Primary key id. |
|Filter |map[string]interface{} |No |Filter conditions, see **Scalar Filtering**<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and two combinations of query operators: and and or. |
|OutputFields |[]string |No |List of scalar fields to return.<br><br><br>1. If user does not pass output_fields, return all scalar fields<br><br>2. If user passes an empty list, do not return scalar fields<br><br>3. If output_fields format is incorrect, or filter fields are not fields in the collection, the interface returns an error |
|Limit |int |No |Number of retrieval results, maximum 5000. |
|Offset |int |No |Offset. Only used in pagination scenarios. It is not recommended to set a large value, otherwise it will cause deep pagination impact. Default value is 0. Set value must be at least 0, semantics are the same as MySQL's offset. |
|Advance |SearchAdvance |No |Advanced parameters, see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082) |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |Type |**Description** |
|---|---|---|
|Data |[]SearchItem |See below |
|FilterMatchedCount |Int |Number of matched filters |
|TotalReturnCount |Int |Number of returned results |
|RealTextQuery |string | |
|TokenUsage |interface{} |Token usage |



* List



|**Attribute** |Type |**Description** |
|---|---|---|
|ID |interface{} |Primary key id. |
|Fields |map[string]interface{} |Fields in the request response |
|Score |float64 |Similarity |
|AnnScore |float64 |ANN score |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Go
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

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).SearchByID(ctx, model.SearchByIDRequest{
       ID: 1,
    })

    if err != nil {
       fmt.Println("SearchByID failed, err: ", err)
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


 &nbsp;
