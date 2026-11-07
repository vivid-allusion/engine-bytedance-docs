---
title: "CreateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/create_memory_collection"
---

<span id="7233642f"></span>
## API Overview

Creates a new memory collection for storing and managing memory data specific to a particular scenario. Supports user\-defined event types and profile types for memory collection to match data modeling requirements in specific business contexts. Each memory collection has an independent memory structure; if memory abstraction differs across business scenarios, a new memory collection should be created.

<span id="7ee688ce"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/collection/create` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The original concept of <strong>entity</strong> has been replaced by <strong>profile</strong>. It is recommended to use <strong>profile</strong> consistently. Parameters related to the original <strong>entity</strong> remain supported for backward compatibility.</div>


* <div data-tips="true" data-tips-type="tip">The configuration item <strong>“sys_profile_collect_v1”</strong> is no longer required. When configuring <strong>“sys_profile_v1”</strong>, the platform will automatically perform event extraction and update the related profiles.</div>




|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |String |Yes |Unique name for the memory collection. Can only use English letters, numbers, underscores, and **must start with an English letter**. |
|CollectionType |String |No |Type of memory collection. Defaults to Ultimate Edition.<br><br>• **standard**: Standard edition for small\-scale scenarios. Supports up to 20 million vectors and 30 QPS. Recommended to choose Ultimate edition when exceeding 2.5 million vectors. Standard edition uses resource sharing mode with more affordable pricing.<br><br>• **ultimate**: Ultimate edition for large\-scale scenarios. Unlimited vectors and QPS. Supports high\-end computing resource configuration with better performance. |
|CpuQuota |Integer |No |Required when selecting Ultimate edition. Range: [1, 100]. If not provided, defaults to 1 CU (1 core 8GB), supporting approximately 100 QPS and 4 million vectors. Exceeding CPU will trigger rate limiting; exceeding memory will automatically scale up. |
|Description |String |No |Description information for the memory collection. |
|BuiltinEventTypes |Array of String |No |Select from built\-in event types. Optional values include "sys_event_v1". See end of section for details. Defaults to empty. |
|BuiltinProfileTypes |Array of String |No |Select from built\-in profile types. Optional value is "sys_profile_v1". See end of section for details. |
|CustomEventTypeSchemas |Array of EventTypeSchema |No |List of custom event types based on business requirements. |
|* EventType |String |Yes |Unique name for the event type, e.g., "customer_feedback", "learning_progress". |
|* Description |String |Yes |Detailed description of the event type. |
|* Properties |Array of EventProperty |Yes |List of properties that compose this event type. |
|* \-PropertyName |String |Yes |Property name, e.g., score, total_interactions. |
|* \-PropertyValueType |String |Yes |Type of property value. Optional values: ["int64", "list", "string", "list", "float32", "bool"] |
|* \-Description |String |Yes |Detailed description of the property. |
|* Version |String |No |Schema version number, defaults to "1". |
|* ValidationExpression |String |No |Optional validation expression for validating event content validity, e.g., "field_a == '1'". |
|CustomProfileTypeSchemas |Array of ProfileTypeSchema |No |List of user\-defined profile type schemas. |
|* ProfileType |String |Yes |Unique name for the profile type, e.g., user_profile, product_summary. |
|* Description |String |Yes |Detailed description of the profile type. |
|* EnableAssistantIsolation |Boolean |No |Whether the profiles are isolated by assistant_id. The default is True, meaning they are isolated. |
|* Properties |Array of ProfileProperty |Yes |List of properties that compose this profile type. |
|* \-PropertyName |String |Yes |Property name, e.g., user_id, total_interactions. |
|* \-PropertyValueType |String |Yes |Type of property value. Optional values: ["int64", "list", "string", "list", "float32", "bool"] |
|* \-Description |String |Yes |Detailed description of the property. |
|* \-AggregateExpression |AggregateExpression |No |Aggregation expression defining how this property is calculated from associated events. |
|* \-\-Op |String |No |Aggregation operator, e.g., SUM, MAX, AVG, COUNT, LLM_MERGE. |
|* \-\-EventType |String |No |Name of the event type participating in the aggregation. |
|* \-\-EventPropertyName |String |No |Property name in the event type participating in the aggregation. |
|* \-IsPrimaryKey |Boolean |No |Whether this is the primary key of the profile. Defaults to false. |
|Version |String |No |Profile schema version number, defaults to "1". |


<span id="Response"></span>
## Response


|**Field** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |Object |Response metadata information. |
|* Action |String |Operation type. |
|* Region |String |Service region, e.g., "cn\-hongkong". |
|* RequestId |String |Unique request identifier. |
|* Service |String |Service name, e.g., "knowledge_base_server". |
|* Version |String |API version number. |
|Result |Object |Actual business data. |
|* ResourceId |String |Successfully created memory collection resource ID. |


<span id="Sample Request"></span>
## Sample Request

<span id="cURL Example"></span>
### Python Example

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
                        method = method,
                        path = api,
                        ak = AK,
                        sk = SK,
                        data = payload)

  r = requests.request(method=req.method,
          url="{}://{}{}".format(req.schema, req.host, req.path),
          headers=req.headers,
          data=req.body,
          params=params,
      )
  return r
  
path = '/api/memory/collection/create'
playload = {
    'CollectionName': "my_first_memory_collection",
    'Description': "test description",
    'BuiltinEventTypes': ["sys_event_v1"],
    'BuiltinProfileTypes': ["sys_profile_v1"],
}
rsp = internal_request('POST', path, playload)
print(rsp.json())
```


<span id="Additional Integration Notes"></span>
## Additional Integration Notes

<span id="Built-in Event Types"></span>
### Built\-in Event Types

**sys_event_v1**: System event type for general system\-level events

<span id="Built-in Entity Types"></span>
### Built\-in Profile Types

**sys_profile_v1**: System profile profile type for storing user profile information
