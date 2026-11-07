---
title: "aggregate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/aggregatev2"
---

<span id="overview"></span>
# Overview

Aggregation statistics are used for group statistics on scalar fields in an index, and can be used with filter conditions to quickly understand data distribution.

The index must have at least one scalar index field of type string, int64, or bool that can be used for aggregation or filtering.

<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|resource_id |Optional[str] |Either/or |Resource ID. Either this or `collection_name` must be provided to locate the collection. |
|collection_name |Optional[str] | |Collection name. If accessing the index by name, can be used together with `project_name`. |
|project_name |Optional[str] |No |Project name. When used in combination with `collection_name`, it can further limit the scope. |
|index_name |str |Yes |Index name. |
|filter |Optional[Dict[str, Any]] |No |General filter condition for vector retrieval, syntax is consistent with the search interface, no filtering when not specified. |
|partition |Optional[str] |No |Specifies the partition name to aggregate. |
|op |str |Yes |Aggregation operator, currently only `count` is supported. |
|field |Optional[str] |No |Scalar field for group aggregation. Supports string, int64, or bool types and must be indexed. |
|cond |Optional[Dict[str, Any]] |No |Secondary filter condition after aggregation, similar to SQL `HAVING`. Currently count only supports `gt` comparison syntax. |
|order |Optional[str] |No |Sorting direction of aggregation results, e.g., `desc`. |


<span id="response-parameters"></span>
## Response Parameters


|Field |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request chain ID, can be used for troubleshooting. |
|code |Optional[str] |Error code, empty when successful. |
|message |Optional[str] |Error message. |
|api |Optional[str] |Actual API name called. |
|result |Optional[AggResult] |Aggregation result, may be `None` on failure or when there are no results. |


AggResult structure:


|Field |Type |Description |
|---|---|---|
|agg |Dict[str, Any] |Aggregation result dictionary. Returns counts by field value, includes `_total` if `field` is not specified. |
|op |Optional[str] |Aggregation operator name. |
|field |Optional[str] |Name of the field participating in aggregation. |


<span id="example"></span>
# Example

Variables required in the example (such as `VIKINGDB_AK`, `VIKINGDB_COLLECTION`, etc.) should be configured as environment variables before running.

```python
import json
import os

from vikingdb import IAM
from vikingdb.vector import AggRequest, VikingVector

auth = IAM(ak=os.environ["VIKINGDB_AK"], sk=os.environ["VIKINGDB_SK"])
client = VikingVector(
    host=os.environ["VIKINGDB_HOST"],
    region=os.environ["VIKINGDB_REGION"],
    auth=auth,
    scheme="https",
)

index = client.index(
    collection_name=os.environ["VIKINGDB_COLLECTION"],
    project_name=os.getenv("VIKINGDB_PROJECT"),
    index_name=os.environ["VIKINGDB_INDEX"],
)

# SELECT category, COUNT(*) FROM index WHERE score >= 60 AND score <= 100 GROUP BY category HAVING COUNT(*) > 5
request = AggRequest(
    op="count",
    filter={"op": "range", "field": "score", "gte": 60, "lte": 100},
    field="category",
    cond={"gt": 5},
)
response = index.aggregate(request)

agg = response.result.agg if response.result else {}
print(f"aggregate request_id={response.request_id} agg={json.dumps(agg, ensure_ascii=False)}")
```
