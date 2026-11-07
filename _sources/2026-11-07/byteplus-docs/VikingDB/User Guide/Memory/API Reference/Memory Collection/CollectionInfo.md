---
title: "CollectionInfo"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/get_memory_collection_information"
---

<span id="4bbb1395"></span>
## API Overview

Retrieves detailed configuration information for a specified memory collection.

<span id="0b77fcb7"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/collection/info` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |String |Yes |The unique name of the memory collection to query. |


<span id="Response Message"></span>
## Response Message


|**Field** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |Object |Response metadata information. |
|* Region |String |Service region, e.g., "cn\-hongkong". |
|* RequestId |String |Request unique identifier |
|* Service |String |Service name, e.g., "knowledge_base_server". |
|* Version |String |API version number. |
|Result |Object |Detailed configuration information of the memory collection. |
|* CreatedAt |String |Memory collection creation time, e.g., "2025\-06\-03T06:35:32". |
|* CreatedBy |String |Memory collection creator. |
|* DescMsg |String |Memory collection description information, e.g., "Memory collection for recording and analyzing student English learning processes". |
|* Name |String |Memory collection name, e.g., "english_learning_memory". |
|* PipelineConfig |Object |Pipeline configuration information. |
|* \-CpuQuota |Int |Resource consumption |
|* \-LlmExtractConfig |Object |LLM extraction configuration |
|* \-\-BuiltinProfileTypes |Array of String |List of built\-in profile types. |
|* \-\-BuiltinEventTypes |Array of String |List of built\-in event types. |
|* \-\-CustomProfileTypeSchemas |Array of profileTypeSchema |List of user\-defined profile type schemas. |
|* \-\-\-AssociatedEventTypes |Array of String |List of event type names associated with this profile type, e.g., ["english_study"]. |
|* \-\-\-Description |String |Detailed description of the profile type, e.g., "Used to track student learning progress on specific English knowledge points". |
|* \-\-\-ProfileType |String |Unique name of the profile type, e.g., "english_knowledge_point". |
|* \-\-\-EnableAssistantIsolation |Boolean |Whether the profiles are isolated by assistant_id. The default is True, meaning they are isolated. |
|* \-\-\-Properties |Array of ProfileProperty |List of properties that constitute this profile type. |
|* \-\-\-\-AggregateExpression |Object |Aggregation expression configuration, defining how this property is aggregated and calculated from associated events. |
|* \-\-\-\-\-EventPropertyName |String |Property name in the event type participating in aggregation, e.g., "rating_score". |
|* \-\-\-\-\-EventType |String |Event type name participating in aggregation, e.g., "english_study". |
|* \-\-\-\-\-Op |String |Aggregation operator, e.g., "MAX", "SUM", "COUNT". |
|* \-\-\-\-Description |String |Detailed description of the property, e.g., "Unique primary key ID of the knowledge point". |
|* \-\-\-\-IsPrimaryKey |Boolean |Whether it is the primary key of the profile, e.g., true. |
|* \-\-\-\-PropertyName |String |Property name, e.g., "id", "knowledge_point_name". |
|* \-\-\-\-PropertyValueType |String |Property value type, e.g., "int64", "string", "list". |
|* \-\-\-Role |String |Role type, e.g., "user". |
|* \-\-\-Version |String |Schema version number, e.g., "1". |
|* \-\-CustomEventTypeSchemas |Array of EventTypeSchema |List of user\-defined event type schemas. |
|* \-\-\-Description |String |Detailed description of the event type, e.g., "Records Q&A and scoring between tutor and student in an English learning session". |
|* \-\-\-EventType |String |Unique name of the event type, e.g., "english_study". |
|* \-\-\-HasMultiEvent |Boolean |Whether it supports multiple events, e.g., true. |
|* \-\-\-OriginalMessagePreserveStrategy |String |Original message preservation strategy, e.g., "ranges". |
|* \-\-\-Properties |Array of EventProperty |List of properties that constitute this event type. |
|* \-\-\-\-Description |String |Detailed description of the property, e.g., "Name of the knowledge point involved in the current conversation". |
|* \-\-\-\-PropertyName |String |Property name, e.g., "knowledge_point_name", "question", "answer". |
|* \-\-\-\-PropertyValueType |String |Property value type, e.g., "string", "float32". |
|* \-\-\-Searchable |Boolean |Whether it is searchable, e.g., true. |
|* \-\-\-ValidationExpression |String |Validation expression. |
|* \-\-\-Version |String |Version number, e.g., "1". |
|* Project |String |Project name, e.g., "default". |
|* ResourceId |String |Unique resource identifier. |
|* UpdatedAt |String |Last update time, e.g., "2025\-06\-03T06:35:32". |
|* EventCount |Int |The number of events in this collection. |
|* ProfileCount |Int |The number of profiles in this collection. |
|* CollectionStatus |String |The status of this collection. |


<span id="Sample Code"></span>
## Sample Code

<span id="cURL Request"></span>
### Python Request

```python
import json
import requests
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials
from volcengine.auth.SignerV4 import SignerV4

AK = "your AK"  
SK = "your SK"  
Domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com"

def prepare_request(method, path, ak, sk, data=None):
    r = Request()
    r.set_shema("http")       
    r.set_method(method)
    r.set_host(Domain)
    r.set_path(path)

    if data is not None:
        r.set_body(json.dumps(data))

    credentials = Credentials(ak, sk, 'air', 'cn-north-1')
    SignerV4.sign(r, credentials)
    return r

def internal_request(method, api, payload, params=None):
    req = prepare_request(
        method=method,
        path=api,
        ak=AK,
        sk=SK,
        data=payload
    )

    r = requests.request(
        method=req.method,
        url="{}://{}{}".format(req.schema, req.host, req.path),
        headers=req.headers,
        data=req.body,
        params=params,
    )
    return r


path = '/api/memory/collection/info'
payload = {
    "CollectionName": "my_first_memory_collection"
}
rsp = internal_request("POST", path, payload)
print(rsp.json())
```
