---
title: "UpdateEvent"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/update_event_memory"
---

<span id="d2a31530"></span>
## API Overview

Used to update event memories that have been written to the memory collection.

<span id="9aacdb29"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/event/update` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |Yes |Name of the target memory collection. |
|event_id |String |Yes |ID of the event memory to be updated. |
|memory_info |Object |No |Content of the event memory. For built\-in event sys_event_v1, only summary; for built\-in event sys_profile_collect_v1, only user_profile; for custom events, display according to custom property fields. **Note: The format must follow the format already defined in the memory collection.**  |
|user_id |Array of String |No |User ID associated with the event. |
|assistant_id |Array of String |No |Assistant ID associated with the event. |


<span id="Format Examples"></span>
### **Format Examples**

**Built\-in event sys_event_v1:** 

```json
{
  "summary": "Today I celebrated my birthday with my good friends."
}
```


**Custom event:** 

```json
{
  "knowledge_point_name": "Today I celebrated my birthday with my good friends.",
  "rating_score": 9
}
```


<span id="Response"></span>
## Response


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |Integer |Status code. 0 indicates success, other values indicate errors. |
|message |String |Response message. Usually "success" on success. Returns error reason on failure. |
|data |Object |Detailed returned data. Usually empty when message is added successfully. |
|request_id |String |Unique ID identifying each request. |


<span id="Sample Request"></span>
## Sample Request

<span id="cURL Request"></span>
### **Python Request**

```python
import json
import requests
import time
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

path = "/api/memory/event/update"
payload = {
    "collection_name": "my_first_memory_collection",
    "event_id": "6879e9d0f2b275b6a4ae2960_0",
    "memory_info": {
        "original_messages": (
            "Monday, 2025-08-18 02:58 PM\n"
            "user1(user): I really love watching matches, and there's another one tomorrow!\n"
            "user1(user): Xiao A has been training for this match against Xiao B for half a year.\n"
            "assistant1(assistant): So inspiring! That means the win is pretty much guaranteed, right?\n"
            "user1(user): I think so too, since Xiao B hardly prepared at all.\n"
            "assistant1(assistant): Haha, let’s look forward to Xiao A’s performance together!"
        ),
        "summary": (
            "On the afternoon of August 18, 2025, the user expressed a strong interest in watching matches "
            "and mentioned that on August 19 there would be a match between Xiao A and Xiao B. "
            "Xiao A had trained for half a year while Xiao B barely prepared, and the assistant looked forward "
            "to Xiao A’s performance."
        )
    },
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
