---
title: "Integrating LLM with Memory"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Integrating_LLM_with_Memory"
---

This chapter uses the Bytepus Seed Large Language Model as an example to demonstrate how to integrate a memory store with an LLM to build a conversational AI system with long\-term memory capabilities.

<span id="fba320f1"></span>
## **Step 1: Prerequisites and API Wrapping**

Before you begin, make sure you have completed the following steps:


1. **Install the required libraries:** 


```Plain
pip install volcengine
pip install byteplus-python-sdk-v2
```



2. **Obtain credentials:** 

* Acquire the **AK/SK** (Access Key / Secret Key) from **Byteplus** for memory store authentication.

* Acquire the **API Key** from **Byteplus ModelArk** for LLM authentication.

* Set the AK, SK, and API Key as environment variables in your system.


To simplify API calls, it is recommended to encapsulate the memory store API logic into a dedicated service class.

Below is a complete example implementation. You can save it as **step1_memory_service.py** and import it into your main application:

```Python
import json
import threading

from volcengine.ApiInfo import ApiInfo
from volcengine.Credentials import Credentials
from volcengine.base.Service import Service
from volcengine.ServiceInfo import ServiceInfo
from volcengine.auth.SignerV4 import SignerV4
from volcengine.base.Request import Request

class VikingDBMemoryException(Exception):
    def __init__(self, code, request_id, message=None):
        self.code = code
        self.request_id = request_id
        self.message = "{}, code:{}，request_id:{}".format(message, self.code, self.request_id)

    def __str__(self):
        return self.message

class VikingDBMemoryService(Service):
    _instance_lock = threading.Lock()

    def __new__(cls, *args, **kwargs):
        if not hasattr(VikingDBMemoryService, "_instance"):
            with VikingDBMemoryService._instance_lock:
                if not hasattr(VikingDBMemoryService, "_instance"):
                    VikingDBMemoryService._instance = object.__new__(cls)
        return VikingDBMemoryService._instance

    def __init__(self, host="api-knowledgebase.mlp.cn-hongkong.bytepluses.com", region="cn-hongkong", ak="", sk="", sts_token="", scheme='http',
                 connection_timeout=30, socket_timeout=30):
        self.service_info = VikingDBMemoryService.get_service_info(host, region, scheme, connection_timeout, socket_timeout)
        self.api_info = VikingDBMemoryService.get_api_info()
        super(VikingDBMemoryService, self).__init__(self.service_info, self.api_info)
        if ak:
            self.set_ak(ak)
        if sk:
            self.set_sk(sk)
        if sts_token:
            self.set_session_token(session_token=sts_token)
        try:
            self.get_body("Ping", {}, json.dumps({}))
        except Exception as e:
            raise VikingDBMemoryException(1000028, "missed", "host or region is incorrect".format(str(e))) from None

    def setHeader(self, header):
        api_info = VikingDBMemoryService.get_api_info()
        for key in api_info:
            for item in header:
                api_info[key].header[item] = header[item]
        self.api_info = api_info

    @staticmethod
    def get_service_info(host, region, scheme, connection_timeout, socket_timeout):
        service_info = ServiceInfo(host, {"Host": host},
                                   Credentials('', '', 'air', region), connection_timeout, socket_timeout,
                                   scheme=scheme)
        return service_info

    @staticmethod 
    def get_api_info():
        api_info = {
            "CreateCollection":     ApiInfo("POST", "/api/memory/collection/create", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),
            "GetCollection":        ApiInfo("POST", "/api/memory/collection/info", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),
            "DropCollection":       ApiInfo("POST", "/api/memory/collection/delete", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),
            "UpdateCollection":     ApiInfo("POST", "/api/memory/collection/update", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),            
            "SearchMemory":     ApiInfo("POST", "/api/memory/search", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),
            "AddSession":    ApiInfo("POST", "/api/memory/session/add", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),     
            "Ping":                   ApiInfo("GET", "/api/memory/ping", {}, {},
                                        {'Accept': 'application/json', 'Content-Type': 'application/json'}),
        }
        return api_info

    def get_body(self, api, params, body):
        if not (api in self.api_info):
            raise Exception("no such api")
        api_info = self.api_info[api]
        r = self.prepare_request(api_info, params)
        r.headers['Content-Type'] = 'application/json'
        r.headers['Traffic-Source'] = 'SDK'
        r.body = body

        SignerV4.sign(r, self.service_info.credentials)

        url = r.build()
        resp = self.session.get(url, headers=r.headers, data=r.body,
                                timeout=(self.service_info.connection_timeout, self.service_info.socket_timeout))
        if resp.status_code == 200:
            return json.dumps(resp.json())
        else:
            raise Exception(resp.text.encode("utf-8"))

    def get_body_exception(self, api, params, body):
        try:
            res = self.get_body(api, params, body)
        except Exception as e:
            try:
                res_json = json.loads(e.args[0].decode("utf-8"))
            except:
                raise VikingDBMemoryException(1000028, "missed", "json load res error, res:{}".format(str(e))) from None
            code = res_json.get("code", 1000028)
            request_id = res_json.get("request_id", 1000028)
            message = res_json.get("message", None)
            
            raise VikingDBMemoryException(code, request_id, message)
        
        if res == '':
            raise VikingDBMemoryException(1000028, "missed",
                                    "empty response due to unknown error, please contact customer service") from None
        return res
    
    def get_exception(self, api, params):
        try:
            res = self.get(api, params)
        except Exception as e:
            try:
                res_json = json.loads(e.args[0].decode("utf-8"))
            except:
                raise VikingDBMemoryException(1000028, "missed", "json load res error, res:{}".format(str(e))) from None
            code = res_json.get("code", 1000028)
            request_id = res_json.get("request_id", 1000028)
            message = res_json.get("message", None)
            raise VikingDBMemoryException(code, request_id, message)
        if res == '':
            raise VikingDBMemoryException(1000028, "missed",
                                    "empty response due to unknown error, please contact customer service") from None
        return res
    
    def create_collection(self, collection_name, description="", custom_event_type_schemas=[], custom_profile_type_schemas=[], builtin_event_types=[], builtin_profile_types=[]):
        params = {
            "CollectionName": collection_name, "Description": description, 
            "CustomEventTypeSchemas": custom_event_type_schemas, "CustomProfileTypeSchemas": custom_profile_type_schemas,
            "BuiltinEventTypes": builtin_event_types, "BuiltinProfileTypes": builtin_profile_types,    
        }
        res = self.json("CreateCollection", {}, json.dumps(params))
        return json.loads(res)

    def get_collection(self, collection_name):
        params = {"CollectionName": collection_name}
        res = self.json("GetCollection", {}, json.dumps(params))
        return json.loads(res)

    def drop_collection(self, collection_name):
        params = {"CollectionName": collection_name}
        res = self.json("DropCollection", {}, json.dumps(params))
        return json.loads(res)

    def update_collection(self, collection_name, custom_event_type_schemas=[], custom_profile_type_schemas=[], builtin_event_types=[], builtin_profile_types=[]):
        params = {
            "CollectionName": collection_name, 
            "CustomEventTypeSchemas": custom_event_type_schemas, "CustomProfileTypeSchemas": custom_profile_type_schemas,
            "BuiltinEventTypes": builtin_event_types, "BuiltinProfileTypes": builtin_profile_types,    
        }
        res = self.json("UpdateCollection", {}, json.dumps(params))
        return json.loads(res)
        
    def search_memory(self, collection_name, query, filter, limit=10):
        params = {
            "collection_name": collection_name, 
            "query": query,
            "limit": limit,
            "filter": filter,
        }
        res = self.json("SearchMemory", {}, json.dumps(params))
        return json.loads(res)
    
    def add_session(self, collection_name, session_id, messages, metadata, profiles=None):
        params = {
            "collection_name": collection_name, 
            "session_id": session_id,
            "messages": messages,
            "metadata": metadata,
        }
        if profiles is not None:
            params["profiles"] = profiles
        res = self.json("AddSession", {}, json.dumps(params))
        return json.loads(res)
```


<span id="5d6b9b09"></span>
## **Step 2: Running the First Complete Conversation**

Once the memory store is ready, we can simulate a **two\-turn conversation** as a complete example.


* After the conversation ends, the **dialogue history** will be written into the memory store.

* Then, we will start a **new topic** and ask a question related to the previous conversation.

* The AI will be able to use the **stored memory** to generate its response.

> **Note:**  The initial write operation requires **3–5 minutes** to build the index. During this time, retrieval requests will return errors.


You can implement this logic in the following file:

**step2_first_conversation.py**

```Python
import json
import os
import time
from dotenv import load_dotenv
from byteplussdkarkruntime import Ark
from step1_memory_service import VikingDBMemoryService

def initialize_services():
    load_dotenv()
    ak = os.environ.get("VOLC_ACCESSKEY")
    sk = os.environ.get("VOLC_SECRETKEY")
    ark_api_key = os.environ.get("ARK_API_KEY")

    if not all([ak, sk, ark_api_key]):
        raise ValueError("VOLC_ACCESSKEY, VOLC_SECRETKEY, and ARK_API_KEY must be set in environment variables.")

    memory_service = VikingDBMemoryService(ak=ak, sk=sk)
    llm_client = Ark(
        api_key=ark_api_key,
    )
    return memory_service, llm_client

def ensure_collection_exists(memory_service, collection_name):
    """Check if memory collection exists, create if not."""
    try:
        memory_service.get_collection(collection_name)
        print(f"Memory collection '{collection_name}' already exists.")
    except Exception as e:
        error_message = str(e)
        if "collection not exist" in error_message:
            print(f"Memory collection '{collection_name}' not found, creating...")
            try:
                memory_service.create_collection(
                    collection_name=collection_name,
                    description="Emotional support scenario test",
                    builtin_event_types=["sys_event_v1"],
                    builtin_profile_types=["sys_profile_v1"]
                )
                print(f"Memory collection '{collection_name}' created successfully.")
                print("Waiting for collection to be ready...")
            except Exception as create_e:
                print(f"Failed to create collection: {create_e}")
                raise
        else:
            print(f"Error checking collection: {e}")
            raise

def search_relevant_memories(memory_service, collection_name, user_id, query):
    """Search for memories relevant to user query, with retry during index building."""
    print(f"Searching for memories related to '{query}'...")
    retry_attempt = 0
    while True:
        try:
            filter_params = {
                "user_id": [user_id],
                "memory_type": ["sys_event_v1", "sys_profile_v1"]
            }
            response = memory_service.search_memory(
                collection_name=collection_name,
                query=query,
                filter=filter_params,
                limit=3
            )

            memories = []
            if response.get('data', {}).get('count', 0) > 0:
                for result in response['data']['result_list']:
                    if 'memory_info' in result and result['memory_info']:
                        memories.append({
                            'memory_info': result['memory_info'],
                            'score': result['score']
                        })

            if memories:
                if retry_attempt > 0:
                    print("Search successful after retry.")
                print(f"Found {len(memories)} relevant memories:")
                for i, memory in enumerate(memories, 1):
                    print(f"  {i}. (Relevance: {memory['score']:.3f}): {json.dumps(memory['memory_info'], ensure_ascii=False, indent=2)}")
            else:
                print("No relevant memories found.")
            return memories

        except Exception as e:
            error_message = str(e)
            if "1000023" in error_message:
                retry_attempt += 1
                print(f"Memory index is being built. Retrying in 60 seconds... (Attempt {retry_attempt})")
                time.sleep(60)
            else:
                print(f"Error searching memories (non-retryable): {e}")
                return []

def handle_conversation_turn(memory_service, llm_client, collection_name, user_id, user_message, conversation_history):
    """Handle one conversation turn, including memory search and LLM response."""
    print("\n" + "="*60)
    print(f"User: {user_message}")
    relevant_memories = search_relevant_memories(memory_service, collection_name, user_id, user_message)

    system_prompt = "You are a compassionate, attentive AI companion with long-term memory capabilities. Your goal is to provide emotional support and warm companionship to users."
    if relevant_memories:
        memory_context = "\n".join([f"- {json.dumps(mem['memory_info'], ensure_ascii=False)}" for mem in relevant_memories])
        system_prompt += f"\n\nHere are some of our past conversation memories for reference:\n{memory_context}\n\nPlease use this information to better understand and respond to the user."

    print("AI is thinking...")
    
    try:
        messages = [{"role": "system", "content": system_prompt}] + conversation_history + [{"role": "user", "content": user_message}]
        completion = llm_client.chat.completions.create(
            model="seed-1-6-250615",
            messages=messages
        )
        assistant_reply = completion.choices[0].message.content
    except Exception as e:
        print(f"LLM call failed: {e}")
        assistant_reply = "Sorry, I'm a bit confused right now and can't respond. Can we talk again later?"
    
    print(f"Companion: {assistant_reply}")
    
    conversation_history.extend([
        {"role": "user", "content": user_message},
        {"role": "assistant", "content": assistant_reply}
    ])
    return assistant_reply

def archive_conversation(memory_service, collection_name, user_id, assistant_id, conversation_history, topic_name):
    """Archive conversation history to memory database."""
    if not conversation_history:
        print("No conversation to archive.")
        return False
        
    print(f"\nArchiving conversation about '{topic_name}'...")
    session_id = f"{topic_name}_{int(time.time())}"
    metadata = {
        "default_user_id": user_id,
        "default_assistant_id": assistant_id,
        "time": int(time.time() * 1000)
    }
    
    try:
        memory_service.add_session(
            collection_name=collection_name,
            session_id=session_id,
            messages=conversation_history,
            metadata=metadata
        )
        print(f"Conversation successfully archived, Session ID: {session_id}")
        print("Waiting for memory index update...")
        return True
    except Exception as e:
        print(f"Failed to archive conversation: {e}")
        return False

def main():
    print("Starting end-to-end memory test...")

    try:
        memory_service, llm_client = initialize_services()
        collection_name = "emotional_support"
        user_id = "xiaoming"
        assistant_id = "assistant"
        ensure_collection_exists(memory_service, collection_name)
    except Exception as e:
        print(f"Initialization failed: {e}")
        return

    print("\n--- Phase 1: Initial Conversation ---")
    initial_conversation_history = []
    handle_conversation_turn(
        memory_service, llm_client, collection_name, user_id,
        "Hello, I'm Xiaoming, 18 years old, but under a lot of pressure.",
        initial_conversation_history
    )
    handle_conversation_turn(
        memory_service, llm_client, collection_name, user_id,
        "The college entrance exam is coming soon, and my family's expectations are very high.",
        initial_conversation_history
    )

    print("\n--- Phase 2: Archive Memory ---")
    archive_conversation(
        memory_service, collection_name, user_id, assistant_id,
        initial_conversation_history, "study_stress_discussion"
    )

    print("\n--- Phase 3: Verify Memory ---")
    verification_conversation_history = []
    handle_conversation_turn(
        memory_service, llm_client, collection_name, user_id,
        "I've been very anxious lately and don't know what to do.",
        verification_conversation_history
    )

    print("\nEnd-to-end memory test completed!")

if __name__ == "__main__":
    main()
```
