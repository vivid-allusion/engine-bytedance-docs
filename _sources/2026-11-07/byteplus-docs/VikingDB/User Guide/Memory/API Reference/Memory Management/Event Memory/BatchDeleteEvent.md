---
title: "BatchDeleteEvent"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/batch_delete_event_memories"
---

<span id="79bde839"></span>
## API Overview

Used to batch delete event memories that have been written to the memory collection.

<span id="dea2c9c3"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/event/batch_delete` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |Yes |Name of the target memory collection. |
|filter |Object |Yes |Filter criteria for deleting memories. |
|* user_id |String or Array of String |No |User ID for filtering. Supports a single ID or a list of IDs. At least one of assistant_id or user_id must be provided, and both can be provided together. |
|* assistant_id |String or Array of String |No |Assistant ID for filtering. Supports a single ID or a list of IDs. At least one of assistant_id or user_id must be provided, and both can be provided together. |
|* event_type |String or Array of String |No |Event type for filtering. |
|delete_type |String |Yes |Memory deletion mode. Default is full mode.<br><br>• partial: Only removes memory association for target user or assistant<br><br>• full: Globally deletes the entire memory |


<span id="Response"></span>
## Response


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |Integer |Status code. 0 indicates success, other values indicate errors. |
|message |String |Response message. Usually "success" on success. |
|request_id |String |Unique ID identifying each request. |


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

path = "/api/memory/event/batch_delete"
payload = {
    "collection_name": "my_first_memory_collection",
    "filter": {
        "user_id": ["student_A"],
        "event_type": ["english_study"]
    }
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
