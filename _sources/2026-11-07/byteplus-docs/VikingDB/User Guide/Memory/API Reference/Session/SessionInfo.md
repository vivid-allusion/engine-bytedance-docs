---
title: "SessionInfo"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/query_session_information"
---

<span id="607dc010"></span>
## API Overview

Query detailed information for a specified session, including generated event memory list, original messages, and token consumption.

<span id="Request Endpoint"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |`/api/memory/session/info` |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |No |Name of the target memory collection. |
|session_id |String |Yes |Session ID for the current conversation or message batch, length requirement: [1, 128]. |


<span id="Response Message"></span>
## Response Message


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |Integer |Status code, 0 indicates success, others indicate errors. |
|message |String |Return message, usually "success" on success. |
|data |Object |Detailed data returned. |
|* usage |Object |Token consumption for this session input. |
|* \-embedding_tokens |Integer |Total token consumption of the embedding model. |
|* \-llm_input_tokens |Integer |Total token consumption of LLM input. |
|* \-llm_output_tokens |Integer |Total token consumption of LLM output. |
|* \-llm_input_tokens_details |Object |Detailed token consumption of LLM input. |
|* \-cached_tokens |Integer |Cached token consumption of LLM input. |
|* event_memory |Array of Object |List of generated event memories. |
|* \-event_id |String |ID of the event memory. |
|* \-event_type |String |Name of the event type. |
|* \-memory_info |Object |Content of the event memory. Contains:<br><br>• Original multi\-turn conversation information.<br><br>• Event attributes: for built\-in event sys_event_v1, only summary; for custom events, display according to custom attribute fields. |
|* \-user_id |Array of String |List of user IDs associated with the event. |
|* \-assitant_id |Array of String |List of assistant IDs associated with the profile. |
|* \-time |Integer |Timestamp (milliseconds) when the memory was created. |
|* messages |Array of Object |List of conversation messages. |
|* \-content |String |Message content. |
|* \-message_id |String |Conversation ID. |
|* \-role |String |Speaker role. |
|* \-role_id |String |Speaker ID. |
|* \-role_name |String |Speaker name. |
|* \-time |Integer |Timestamp (milliseconds) when the message was sent. |
|* session_id |String |Session ID for the current conversation or message batch. |
|* status |String |Processing progress of the current session, enum values: processing, success, failed. |
|* time |Integer |Unified occurrence time of the current session, millisecond\-level timestamp. |
|* user_ids |Array of String |List of users associated with the current session. |
|* assistant_ids |Array of String |List of assistants associated with the current session. |
|request_id |String |Unique ID identifying each request. |


<span id="Sample Code"></span>
## Sample Code

<span id="Curl Request"></span>
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

path = "/api/memory/session/info"

payload = {
    "collection_name": "my_first_memory_collection",
    "session_id": "message0"
}
rsp = internal_request("POST", path, payload)
print(rsp.json())
```
