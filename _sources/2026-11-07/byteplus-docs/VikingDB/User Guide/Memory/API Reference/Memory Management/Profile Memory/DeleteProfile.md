---
title: "DeleteProfile"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/delete_single_entity_memory"
---

<span id="00ab66c3"></span>
## API Overview

Used to delete a single profile memory that has been written to the memory collection.

<span id="6cb1ea68"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/profile/delete` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |Yes |Name of the target memory collection. |
|profile_id |String |Yes |ID of the profile memory to be deleted. |


<span id="Response"></span>
## Response


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |Integer |Status code. 0 indicates success, other values indicate errors. |
|message |String |Response message. Usually "success" on success. Returns error reason on failure. |
|request_id |String |Unique ID identifying each request. |


<span id="Sample Request"></span>
## Sample Request

<span id="Request Message"></span>
### Request Message

<span id="cURL Request"></span>
#### **Python Request**

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
        r.set_body(json.dumps(data, ensure_ascii=False))
    credentials = Credentials(ak, sk, "air", "cn-north-1")
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
    resp = requests.request(
        method=req.method,
        url="{}://{}{}".format(req.schema, req.host, req.path),
        headers=req.headers,  
        data=req.body,
        params=params,
        timeout=30,
    )
    return resp

path = "/api/memory/profile/delete"
payload = {
    "collection_name": "my_first_memory_collection",
    "profile_id": "6879e9d0f2b275b6a4ae2960_2"
}

rsp = internal_request("POST", path, payload)
print(rsp.json())
```


<span id="Response Message"></span>
## Response Message

<span id="Successful Response"></span>
### **Successful Response**

```http
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "data": {
        "resource_id": "kb-8349ef57441ab57"
    },
    "request_id":"021695029537650fd001de666660000000000000000000230da93"
}
```


<span id="Failed Response"></span>
### **Failed Response**

```http
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
