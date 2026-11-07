---
title: "searchByKeywords"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByKeywords"
---

<span id="overview"></span>
# Overview

SearchByKeywords is used for keyword search, applicable to indexes with text field vectorization configuration (vectorize parameter), and supports multi\-keyword search.

<span id="method-definition"></span>
# Method Definition

```go
resp, err := client.Index(indexLocator).SearchByKeywords(ctx, req)
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByKeywordsRequest`, and its fields are shown in the table below.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Keywords |[]string |Yes |Keyword list, containing 1\-10 elements, and empty strings are not allowed. |
|CaseSensitive |bool |No |Whether case\-sensitive. Default is false. |
|Filter |map[string]interface{} |No |Filter conditions, see **Scalar Filter** for details<br><br><br>* Default is empty, no filtering is applied.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and two combinations of query operators: and and or. |
|OutputFields |[]string |No |List of scalar fields to return.<br><br><br>1. If user does not pass output_fields, all scalar fields are returned<br><br>2. If user passes an empty list, no scalar fields are returned<br><br>3. If output_fields format is incorrect or the filter field is not a field in the collection, the interface returns an error |
|Limit |int |No |Number of search results, maximum 5000. |
|Offset |int |No |Offset. Only used in pagination scenarios. It is not recommended to set too large a value, otherwise there will be deep pagination impact. Default value is 0. The value must be at least 0, with the same semantics as MySQL offset. |
|Advance |SearchAdvance |No |Advanced parameters, see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082) |


<span id="response-parameters"></span>
# Response Parameters


* SearchResult



|**Attribute** |Type |**Description** |
|---|---|---|
|Data |[]SearchItemResult |See below |
|FilterMatchedCount |int |Total number of documents that meet the filter conditions. |
|TotalReturnCount |int |Number of results returned this time. |
|RealTextQuery |string |The actual query string after potential correction by the model. |
|TokenUsage |map[string]interface{} |Token metering information. |



* SearchItemResult



|**Attribute** |Type |**Description** |
|---|---|---|
|ID |interface{} |Primary key id. |
|Fields |map[string]interface{} |The fields field in the response |
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
       limit = 10
    )

    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).SearchByKeywords(ctx, model.SearchByKeywordsRequest{
       SearchBase: model.SearchBase{
          Limit: &limit,
       },
       Keywords:      []string{"viking"},
       CaseSensitive: false,
    })

    if err != nil {
       fmt.Println("SearchByKeywords failed, err: ", err)
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
