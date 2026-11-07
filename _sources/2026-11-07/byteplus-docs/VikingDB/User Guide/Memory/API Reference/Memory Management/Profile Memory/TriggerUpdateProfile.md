---
title: "TriggerUpdateProfile"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/TriggerUpdateProfile"
---

<span id="Overview"></span>
## API Overview

Manually trigger updates to profile memory.

Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/profile/trigger_update` |Endpoint path |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request content type |
| |Authorization: HMAC\-SHA256 \*\*\* |Signature generated using AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |No |Target viking memory name. |
|project_name |String |No |Project that owns the viking memory. |
|resource_id |String |No |Unique resource ID of the viking memory. You can pass `resource_id` directly, or provide both `collection_name` and `project_name` as the unique identifier. |
|update_profile_type |Array of String |No |Profile memory types to update. When omitted, all profile types are updated by default. |
|filters |Object |No | |
|* user_id |String or Array of String |No |Users whose profiles to update. If omitted, all users are updated. Up to 1000 values; for more, use parallel calls. |
|* end_time |Integer |No |Cutoff timestamp for the update window. The event\-memory range for this run is from the last update timestamp up to `end_time`. Set it slightly earlier than the current time to ensure data completeness. |


<span id="Response"></span>
## Response


|**Field** |**Type** |**Description** |
|---|---|---|
|code |Integer |Status code; `0` indicates success, non‑zero indicates error. |
|message |String |Message text; typically `"success"` on success, otherwise the error reason. |
|data |Object |Detailed response payload. |
|request_id |String |Unique request identifier. |


<span id="Python (Request)"></span>
## Sample Request

<span id="f796fc32"></span>
### **Python Request**

```Python
import os
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
    
path = "api/memory/profile/trigger_update"

payload = {
    "collection_name": "my_first_memory_collection",
    "project_name": "default",
    "update_profile_type": ["profile_v1","social network"]  
}

rsp = internal_request("POST", path, payload)
print(rsp.json())
```


<span id="Response Message"></span>
## Response Message

<span id="Successful Response"></span>
### **Successful Response**

```Shell
{
    "code":0,
    "message":"success",
    "request_id":"021695029537650fd001de666660000000000000000000230da93"
}
```
