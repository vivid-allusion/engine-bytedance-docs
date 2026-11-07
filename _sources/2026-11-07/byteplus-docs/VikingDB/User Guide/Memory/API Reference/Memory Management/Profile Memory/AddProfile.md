---
title: "AddProfile"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/add_profile"
---

<span id="API Overview"></span>
# API Overview

This endpoint adds a profile memory.

<span id="Endpoint"></span>
# Endpoint


|**URL** |/api/memory/profile/add |Uniform Resource Identifier |
|---|---|---|
|**Method** |POST |The type of operation the client is requesting from the memory server. |
|**Headers** |Content\-Type: application/json |The type of the request message. |
| |Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK. |


<span id="Request Parameters"></span>
# Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |Yes |The name of the target memory collection. |
|profile_type |String |Yes |The type of the profile. |
|memory_info |Object |Yes |The content of the profile memory. For the built\-in profile `sys_profile_v1`, only `user_profile` is included. For custom profiles, the fields should be written according to the custom attributes. **Note: The format must follow the format already defined in the memory collection.**  |
|user_id |String |Yes |The user ID associated with the profile. |
|assistant_id |String |No |Assistant ID associated with the profile.<br><br><br>* For profiles isolated by assistant: This field is required. It can be set to an empty string `""` or a valid ID.<br><br>* For profiles NOT isolated by assistant: Providing an `assistant_id` will result in an error. |
|group_id |String |No |The group ID, used to isolate different sessions or scenarios. |
|is_upsert |Boolean |No |Whether to update an existing memory with this write. Defaults to `false` (do not update).<br><br><br>* `false`: Checks if a record exists. If it exists, an error is reported. If it does not exist, a new one is added.<br><br>* `true`: Checks if a record exists. If it exists, it is updated. If it does not exist, a new one is added. |


<span id="Response"></span>
# Response


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |Integer |The status code. 0 indicates success, others indicate an error. |
|message |String |The return message, usually "success" on success. |
|data |Object |Detailed data returned. |
|* profile_id |String |The unique ID of the profile. |
|* memory_info |Object |The content of the profile memory. |
|* primary_key |String |The primary key of the profile. |
|* profile_type |String |The type of the profile. |
|usage |Object |The tokens consumed by writing the profile memory. |
|* embedding_tokens |Integer |The embedding tokens consumed. |
|request_id |String |A unique ID for each request. |


<span id="Complete Example"></span>
# Complete Example

<span id="Request"></span>
## Request

<span id="Python Request"></span>
### **Python Request**

```python
import json
import requests
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials
from volcengine.auth.SignerV4 import SignerV4

AK = "your AK"   # Replace with your AK
SK = "your SK"   # Replace with your SK
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

# ===== Add Profile =====
path = "/api/memory/profile/add"
payload = {
    "collection_name": "my_first_memory_collection",
    "profile_type": "sys_profile_v1",
    "memory_info":{
    "user_profile": "### Basic Information: Gender Female/Age 28/Hometown Guangzhou/Occupation Product Manager"
    },
    "user_id": "user001",
}

rsp = internal_request("POST", path, payload)
print(rsp.json())
```


<span id="Response"></span>
## Response

<span id="Successful Response"></span>
### **Successful Response**

```shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json

{
    "code":0,
    "message":"success",
    "data": {
        "profile_id": "68a6xxxxec42",
        "primary_key":"",
        "profile_type": "sys_profile_v1",
        "memory_info":{
            "user_profile": "### Basic Information: Gender Female/Age 28/Hometown Guangzhou/Occupation Product Manager"
        },
        "usage": {
            "embedding_tokens":68
        }
    }
    "request_id":"0216xxxxda93"
}
```


<span id="Failed Response"></span>
### Failed Response

```shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json

{"code":1000003, "message":"invalid request：%s", "request_id": "0216xxxx9b8f"}
```
