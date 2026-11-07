---
title: "ListCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/list_memory_collection"
---

<span id="API Overview"></span>
# API Overview

This endpoint retrieves a list of all memory collections associated with a user's account and a specified project. It returns basic information for each memory collection, including its name, description, built\-in/custom event and profile types, creation time, and last update time.

<span id="Endpoint"></span>
# Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |/api/memory/collection/list |Uniform Resource Identifier |
|**Method** |POST |The type of operation the client is requesting from the memory collection server. |
|**Headers** |Content\-Type: application/json |The type of the request message. |
| |Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK. |


<span id="Request Parameters"></span>
# Request Parameters


|**Parameter Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ProjectName |String |No |The name of the project. |


<span id="Response"></span>
# Response


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |Object |Metadata about the response. |
|* Region |String |The service region, e.g., "cn\-hongkong". |
|* RequestId |String |A unique identifier for the request. |
|* Service |String |The service name, e.g., "knowledge_base_server". |
|* Version |String |The API version number. |
|Result |Object |Detailed configuration information for the memory collection. |
|* CreateAt |String |The time the memory collection was created, e.g., "2025\-06\-03T06:35:32". |
|* CreatedBy |String |The creator of the memory collection. |
|* DescMsg |String |A description of the memory collection, e.g., "A memory bank for recording and analyzing students' English learning progress." |
|* Name |String |The name of the memory collection, e.g., "english_learning_memory". |
|* PipelineConfig |Object |Pipeline configuration information. |
|* CpuQuota |Int |The resources consumed. |
|* LlmExtractConfig | | |
|* \-BuiltinProfileTypes |Array of String |A list of built\-in profile types. |
|* \-BuiltinEventTypes |Array of String |A list of built\-in event types. |
|* \-CustomProfileTypeSchemas |Array of ProfileTypeSchema |A list of user\-defined profile type schemas. |
|* \-\-AssociatedEventTypes |Array of String |A list of event type names associated with this profile type, e.g., ["english_study"]. |
|* \-\-Description |String |A detailed description of the profile type, e.g., "Used to track a student's learning progress on a specific English knowledge point." |
|* \-\-ProfileType |String |The unique name of the profile type, e.g., "english_knowledge_point". |
|* \-\-EnableAssistantIsolation |Boolean |Whether the profiles are isolated by assistant_id. The default is True, meaning they are isolated. |
|* \-\-Properties |Array of ProfileProperty |A list of properties that make up this profile type. |
|* \-\-\-AggregateExpression |Object |The aggregate expression configuration, defining how this property is aggregated from associated events. |
|* \-\-\-EventPropertyName |String |The name of the property in the event type that participates in the aggregation, e.g., "rating_score". |
|* \-\-\-\-EventType |String |The name of the event type that participates in the aggregation, e.g., "english_study". |
|* \-\-\-\-Op |String |The aggregation operator, e.g., "MAX", "SUM", "COUNT". |
|* \-\-\-Description |String |A detailed description of the property, e.g., "The unique primary key ID of the knowledge point." |
|* \-\-\-IsPrimaryKey |Boolean |Whether this is the primary key of the profile, e.g., true. |
|* \-\-\-PropertyName |String |The name of the property, e.g., "id", "knowledge_point_name". |
|* \-\-\-PropertyValueType |String |The value type of the property, e.g., "int64", "string", "list". |
|* \-\-Role |String |The role type, e.g., "user". |
|* \-\-Version |String |The profile schema version number, e.g., "1". |
|* \-CustomEventTypeSchemas |Array of EventTypeSchema |A list of user\-defined event type schemas. |
|* \-\-Description |String |A detailed description of the event type, e.g., "Records a Q&A and rating between a teaching assistant and a student in an English study session." |
|* \-\-EventType |String |The unique name of the event type, e.g., "english_study". |
|* \-\-HasMultiEvent |Boolean |Whether multiple events are supported, e.g., true. |
|* \-\-OriginalMessagePreserveStrategy |String |The original message preservation strategy, e.g., "ranges". |
|* \-\-Properties |Array of EventProperty |A list of properties that make up this event type. |
|* \-\-\-Description |String |A detailed description of the property, e.g., "The name of the knowledge point involved in the current conversation." |
|* \-\-\-PropertyName |String |The name of the property, e.g., "knowledge_point_name", "question", "answer". |
|* \-\-\-PropertyValueType |String |The value type of the property, e.g., "string", "float32". |
|* \-\-Searchable |Boolean |Whether it is searchable, e.g., true. |
|* \-\-ValidationExpression |String |The validation expression. |
|* \-\-Version |String |The version number, e.g., "1". |
|* Project |String |The project name, e.g., "default". |
|* ResourceId |String |The unique identifier for the resource. |
|* UpdatedAt |String |The last update time, e.g., "2025\-06\-03T06:35:32". |
|* EventCount |Int |The number of memory entries. |
|* ProfileCount |Int |The number of profile entries. |
|TotalNum |Int |The number of memory collections in the project. |


<span id="Sample Code"></span>
# Sample Code

<span id="Python Code"></span>
## Python Code

```Python
import requests
import json
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials
from volcengine.auth.SignerV4 import SignerV4


AK = "Your AK" 
SK = "Your SK" 
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

path = "/api/memory/collection/list"
payload = {
    "project_name": "default"   
}

rsp = internal_request("POST", path, payload)
print(rsp.json())
```
