---
title: "aggregate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/aggregate"
---

<span id="overview"></span>
# Overview

Aggregate statistics are used for group statistics on scalar fields in the index and can be used with filter conditions to quickly understand data distribution.

The index must have at least one scalar index field of type string, int64, or bool that can be used for aggregation or filtering.

<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|ResourceID |string |Either/Or |Resource ID. Either this or `CollectionName` is used to locate the collection. |
|CollectionName |string |Either/Or |Collection name. When accessing the index by name, can be used with `ProjectName`. |
|ProjectName |string |No |Project name. When used in combination with `CollectionName`, can further restrict the scope. |
|IndexName |string |Yes |Index name. |
|Filter |map[string]interface{} |No |General filter condition for vector retrieval, syntax is consistent with the search interface. No filtering is applied if not specified. |
|Partition |string |No |Specifies the partition name to aggregate. |
|Op |string |Yes |Aggregation operator, currently only supports `count`. |
|Field |string |No |Scalar field to be aggregated by group. Supports string, int64, or bool types and must be indexed. |
|Cond |map[string]interface{} |No |Secondary filter condition after aggregation, similar to SQL `HAVING`. Currently count only supports `gt` comparison syntax. |
|Order |string |No |Sort direction for aggregation results, e.g., `desc`. |


<span id="response-parameters"></span>
## Response Parameters


|Field |Type |Description |
|---|---|---|
|Request_id |string |Request trace ID, can be used for troubleshooting. |
|Code |string |Error code, empty when successful. |
|Message |string |Error message. |
|Api |string |Name of the API actually called. |
|Result |AggResult |Aggregation result, may be `nil` on failure or when there are no results. |


AggResult Structure


|Field |Type |Description |
|---|---|---|
|Agg |map[string]interface{} |Aggregation result dictionary. Returns counts by field value, includes `_total` if `Field` is not specified. |
|Op |string |Aggregation operator name. |
|Field |string |Field name involved in aggregation. |


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
       field = "type"
    )

    // SELECT type, COUNT(*) FROM index WHERE score >= 0.3 AND score <= 0.46 GROUP BY type HAVING COUNT(*) > 4
    resp, err := client.Index(model.IndexLocator{
       CollectionLocator: model.CollectionLocator{
          CollectionName: "Your Collection Name",
       },
       IndexName: "Your Index Name",
    }).Aggregate(ctx, model.AggRequest{
       RecallBase: model.RecallBase{
          Filter: map[string]any{
             "op": "range", "field": "score", "gte": 0.3, "lte": 0.46,
          },
       },
       Op:    "count",
       Field: &field,
       Cond:  map[string]any{"gt": 4},
    })

    if err != nil {
       fmt.Println("Aggregate failed, err: ", err)
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
