---
title: "DeleteCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/delete_memory_collection"
---

<span id="4dfea90c"></span>
## API Overview

Deletes an existing memory collection. This operation is irreversible and all data in the memory collection will be permanently deleted.

<span id="717cdc89"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/collection/delete` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |String |Yes |Unique name of the memory collection to be deleted. |


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
|Result |String |Success indicator, e.g., "success". |


<span id="Sample Request"></span>
## Sample Request

<span id="cURL Request"></span>
### **Python Request**

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


path = "/api/memory/collection/delete"
payload = {
    "CollectionName": "my_first_memory_collection"
}
rsp = internal_request("POST", path, payload)
print(rsp.json())
if rsp.status_code == 200:
    print(rsp.json())
else:
    print(rsp.status_code, rsp.text)
```
