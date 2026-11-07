---
title: "UpdateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/update_memory_collection"
---

<span id="61d766fd"></span>
## API Overview

Used to update the configuration information of an existing memory collection, including the collection description, custom event types, custom profile types, and other content. **Please note that this interface adopts a full replacement strategy** \- fields provided in the request will overwrite the original configuration, rather than incrementally modifying on the original configuration. Configuration items not included in the request body will be cleared or reset. The update only targets the memory collection structure; previously added data is not affected and can still be retrieved normally.

<span id="b386329a"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/collection/update` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters

>  **⚠️ Important:**  When updating a memory collection, you must include all configurations; otherwise, they will be overwritten.



|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |String |Yes |Unique name of the memory collection to be updated. |
|BuiltinEventTypes |Array of String |No |New list of built\-in event type names. Providing this field will overwrite existing built\-in event types. |
|BuiltinProfileTypes |Array of String |No |New list of built\-in profile type names. Providing this field will overwrite existing built\-in profile types. |
|CustomEventTypeSchemas |Array of EventTypeSchema |No |New list of custom event type schemas. Providing this field will overwrite existing custom event types. |
|CustomProfileTypeSchemas |Array of ProfileTypeSchema |No |New list of custom profile type schemas. Providing this field will overwrite existing custom profile types. |
|CpuQuota |Integer |No |Defaults to 1 core at creation, supporting 100qps. Range [1, 100]. |


<span id="Response"></span>
## Response

When the operation is successful, the HTTP status code is 200.


|**Field** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |Object |Response metadata information. |
|* Region |String |Service region, e.g., "cn\-hongkong". |
|* RequestId |String |Unique identifier for the request. |
|* Service |String |Service name, such as "knowledge_base_server". |
|* Version |String |API version number. |


<span id="Sample Request"></span>
## Sample Request

<span id="cURL Request"></span>
### **Python Request**

```python
import requests
import json
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

path = "/api/memory/collection/update"
playload = {
  "CollectionName": "my_first_memory_collection",
  "Description": "analyse the conversion in the collection",
  "CustomEventTypeSchemas": [
        {
          "PropertyName": "language",
          "PropertyValueType": "string",
          "Description": "language (zh-CN/en)"
        },
        {
          "PropertyName": "sentiment",
          "PropertyValueType": "stxring",
          "Description": "emotion (positive/neutral/negative)"
        },
        {
          "PropertyName": "topic",
          "PropertyValueType": "string",
          "Description": "topics (used to cluster and retrieve)"
        },
        {
          "PropertyName": "intent",
          "PropertyValueType": "string",
          "Description": "intention tag (info seek / talk)"
        }
      ],
      "Version": "1"
    }
  ]
}
rsp = internal_request('POST', path, playload)
print(rsp.json())
```
