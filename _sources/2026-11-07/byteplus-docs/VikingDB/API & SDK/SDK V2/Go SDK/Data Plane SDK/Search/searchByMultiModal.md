---
title: "searchByMultiModal"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByMultiModal"
---

<span id="overview"></span>
# Overview

`searchByMultiModal` is used for multimodal data retrieval. Multimodal data retrieval means that the vector database supports direct retrieval through multimodal data types such as text and images, and supports combinations of modalities, such as text\-to\-image, image\-to\-image, image\-to\-text+image, etc.


* Currently supports unstructured data of text, image, and video types.

* After Collection data is written/deleted, Index data update time is approximately 20s, and cannot be immediately retrieved in the Index.


<span id="prerequisites"></span>
# Prerequisites


* Selected the database type starting from vectorization from the console, and configured vectorization fields when creating the dataset; or configured the Collection's vectorization function by setting the vectorize parameter when creating the dataset through the create_collection interface.

* When writing data through the upsert_data interface, the field names and field values of text or image types have been written.

* When creating an index through create_index, a vector_index vector index has been created.


Applicable when "vectorization required" is selected when creating the vector database: when the imported data is raw data, you can input text, images, etc. through this interface for retrieval.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByMultiModalRequest`, and its fields are shown in the following table.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Text |string |At least 1 required |Input text for retrieval. |
|Image |interface{} | |Input image for retrieval, supports:<br><br><br>* TOS link, in the form `tos://{bucket}/{object_key}`.<br><br>* Base64 encoding, in the form `base64://{Base64 encoding}`. |
|Video |interface{} | |JSON structure, for example:<br><br>{<br><br>"value": "http(s)://..." or "tos://..." (required)<br><br>"fps": 2.0 (0.2\-5, optional)<br><br>} |
|Filter |map[string]interface{} |No |Scalar filtering conditions, see **Scalar Filtering** for details.<br><br><br>* Not filling in means pure multimodal retrieval.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|OutputFields |[]string |No |List of scalar fields to return.<br><br><br>1. Returns all scalar fields in the collection when not set.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. Field names must exist in the collection schema, otherwise the request will report an error. |
|Limit |int |No |Limit the number of returned items, maximum 5000. |
|Offset |int |No |Pagination offset, default 0, excessive value will cause deep pagination performance overhead. |
|Partition |string |No |Specify the partition name for retrieval. |
|Advance |SearchAdvance |No |Advanced parameter collection (post_process_ops, ids_in, etc.), see [Retrieval Common Parameters](https://docs.byteplus.com/docs/84313/1927082)<br><br>for details. |
|NeedInstruction |bool |No |Controls whether to let the model automatically complete instruction, Doubao series defaults to true, other models default to false. |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|RequestId |string |Request link ID. |
|Code |string |Service return code, Success indicates success. |
|Message |string |Error or prompt information. |
|Api |string |Specific API name called. |
|Result |SearchResult |Retrieval result body, structure shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|Data |[]SearchItemResult |List of recalled results, structure shown below. |
|FilterMatchedCount |int |Total number of documents that meet the filter conditions. |
|TotalReturnCount |int |Number of results returned this time. |
|RealTextQuery |string |The real query string possibly corrected by the model. |
|TokenUsage |map[string]interface{} |Token measurement information. |



* SearchItemResult



|**Attribute** |Type |**Description** |
|---|---|---|
|ID |interface{} |Primary key id. |
|Fields |map[string]interface{} |fields field in the request response |
|Score |float64 |Similarity |
|AnnScore |float64 |ANN score |


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
       text            = "viking"
       needInstruction = true // NeedInstruction: improve prompt by auto completing instruction
       limit           = 10
    )

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).SearchByMultiModal(ctx, model.SearchByMultiModalRequest{
       Text:            &text,
       NeedInstruction: &needInstruction,
       SearchBase: model.SearchBase{
          Limit: &limit,
       },
    })

    if err != nil {
       fmt.Println("SearchByMultiModal failed, err: ", err)
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
