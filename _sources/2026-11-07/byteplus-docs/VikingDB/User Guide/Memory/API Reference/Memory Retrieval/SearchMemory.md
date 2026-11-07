---
title: "SearchMemory"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/search_memory_collection"
---

<span id="29548813"></span>
## API Overview

Retrieve relevant memory events or profile information from a specified memory collection. You can perform semantic similarity searches based on user queries and scope the search using filtering conditions.

<span id="Request Endpoint"></span>
## Request Endpoint


|**Parameter** |**Value** |**Description** |
|---|---|---|
|**URL** |/api/memory/search |Uniform Resource Identifier |
|**Method** |POST |Client request operation type to memory server |
|**Headers** |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Signature information generated based on AK/SK |


<span id="Request Parameters"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collection_name |String |Yes |Name of the memory collection to search. |
|query |String |No |User's search query statement (maximum 4000 characters)<br><br>• When query is provided, semantic matching recall will be performed on memories based on the query content, with the number of recalled memories related to the limit value;<br><br>• When query is not provided, a list of memories matching the filter conditions will be returned, sorted chronologically (most recent first), with the number of recalled memories related to the limit value. |
|filter |Object |Yes |Search filtering conditions and return settings. |
|* user_id |String or Array of String |No |User ID, Can be a single ID or list of IDs. |
|* assistant_id |String or Array of String |No |Assistant ID, Can be a single ID or list of IDs. |
|* primary_key |String or Array of String |No |Profile primary key expression for filtering. Can be single or list, e.g., if profile primary key is kb_id and you want to query data where kb_id is 1, the search condition would be primary_key="kb_id=1" |
|* start_time |Integer |No |Start time for retrieving memories, millisecond\-level timestamp. |
|* end_time |Integer |No |End time for retrieving memories, millisecond\-level timestamp. |
|* memory_type |String or Array of String |Yes |Memory types to retrieve. Can be specific event type (EventType) or profile type (ProfileType) names, or a list of them. |
|* group_id |String or Array of String |No |Group ID for filtering. Can be a single ID or list of IDs. |
|* session_id | | | |
|limit |Integer |No |Number of search results to return, default is 10, range [1, 5000]. |


<span id="b6197f50"></span>
### **Notes**


* **Event/Profile Retrieval**

   * user_id and assistant_id: At least one must be provided.

   * Both can be provided together.


<span id="Response Message"></span>
## Response Message


|**Field** |**Type** |**Description** |
|---|---|---|
|code |Integer |Status code, 0 indicates success, others indicate errors. |
|message |String |Return message. |
|data |Object |Detailed search results. |
|* collection_name |String |Name of the searched memory collection. |
|* count |Integer |Number of search results returned. |
|* result_list |Array of Object |List of search results. |
|* \-id |String |Unique ID of the memory entry (event or profile instance). |
|* \-score |Float |Relevance score to the query. |
|* \-memory_type |String |Memory entry type (EventType or ProfileType) name. |
|* \-user_id |Array of String |List of associated user IDs. |
|* \-assistant_id |Array of String |List of associated assistant IDs. |
|* \-session_id |String |Associated session ID. |
|* \-group_id |String |Associated group ID. |
|* \-time |Integer |Timestamp (milliseconds) when the memory occurred or was last updated. |
|* \-status |String |Status of the memory entry (reserved field). |
|* \-labels |String |Labels of the memory entry (reserved field). |
|* \-memory_info |Object |Additional detailed information. Its structure depends on memory_type.<br><br>For events, includes event attributes plus original multi\-turn conversation information, e.g.:<br><br>`{ "original_messages": "tutor_001(assistant):Okay, let's talk about weather...", "answer": "Today is cloudy but very warm.", "knowledge_point_name": "Weather-related expressions", "question": "How would you say \"今日は曇りだけど暖かい\" in English?", "rating": "good", "rating_reasoning": "Student correctly described weather in English...", "rating_score": 7 }`<br><br>For profiles,it only includes profile attributes, e.g.:<br><br>`{ "answer_bad_count": 0, "answer_good_count": 3, "count": 3, "has_been_taught": 0, "issues": [], "rating_score_max": 1, "rating_score_sum": 3 }` |
|* token_usage |Integer |Number of tokens consumed by this search. |
|request_id |String |Unique ID identifying each request. |


<span id="Sample Code"></span>
## Sample Code

<span id="Curl Request"></span>
### Python Request

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

path = "/api/memory/search"
playload = {
    "collection_name": "my_first_memory_collection",
    "query": "can you guess who win the final game?",
    "limit": 5,
    "filter": {
        "user_id": "user1",
        "memory_type": ["sys_event_v1", "sys_profile_v1"]
    }
}

rsp = internal_request('POST', path, playload)
print(rsp.json())
```
