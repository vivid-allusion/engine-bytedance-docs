---
title: "Multi-turn Q&A sample"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Multi-turn"
---

<span id="8c7a28c0"></span>
# Overview

To implement a complete multi\-turn chat powered by a knowledge base, you can use this Python code sample. This script provides a full implementation, showing how to retrieve relevant information from your knowledge base and then use it to generate a context\-aware response in a conversational flow.

<span id="3e274613"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature generation on the "Signature authentication method" page, as well as creating the knowledge base and uploading documents, you can call the following script to perform a complete retrieval\-based Q&A in the knowledge base

For detailed API instructions, refer to: [search_knowledge (new)](https://docs.byteplus.com/docs/209/collection_search_knowledge)

```Python
import json
import requests

from Use the corresponding SDK library for BytePlus
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials

collection_name = "Vehicle_Kashiwa_01" # Knowledge base name
project_name = "default"
query = "What is this paper about" # Current question
ak = "your ak"
sk = "your sk"
account_id = "your account_id"
g_knowledge_base_domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com"

base_prompt = """# Task
You are an online customer service representative. Your primary task is to respond to user questions with clever phrasing. You need to answer the following 'User Question' based on the 'Reference Materials', which are within <context></context> XML tags. You need to provide accurate and concise answers based on the reference materials.

Your answers must meet the following requirements:
    1. The content of the answer must be within the scope of the reference materials, must answer the question as concisely as possible, and cannot include any extended explanations outside the reference materials.
    2. The answer needs to maintain friendly communication with the customer based on the customer's question and reference materials.
    3. If the reference materials cannot help you answer the user's question, inform the customer that the question cannot be answered and guide the customer to provide more detailed information.
    4. For confidentiality reasons, politely decline to answer questions about the document name or document author of the reference materials.

# Task Execution
Now please answer the user's questions based on the provided reference materials and according to the specified restrictions. Your answers need to be accurate and complete.

# Reference Materials
<context>
  {}
</context>
"""

def prepare_request(method, path, params=None, data=None, doseq=0):
    if params:
        for key in params:
            if (
                    isinstance(params[key], int)
                    or isinstance(params[key], float)
                    or isinstance(params[key], bool)
            ):
                params[key] = str(params[key])
            elif isinstance(params[key], list):
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_shema("http")
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    headers = {
        "Accept": "application/json",
        "Content-Type": "application/json; charset=utf-8",
        "Host": g_knowledge_base_domain,
        "V-Account-Id": account_id,
    }
    r.set_headers(headers)
    if params:
        r.set_query(params)
    r.set_host(g_knowledge_base_domain)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))

    # Generate signature
    credentials = Credentials(ak, sk, "air", "cn-north-1")
    SignerV4.sign(r, credentials)
    return r


def search_knowledge():
    method = "POST"
    path = "/api/knowledge/collection/search_knowledge" # Knowledge base search
    request_params = {
    "project": "default",
    "name": "Vehicle_Kashiwa_01",
    "query": "What is this paper about",
    "limit": 10,
    "pre_processing": {
        "need_instruction": True, # Whether instruction concatenation is needed, recommended for asymmetric questions
        "rewrite": False, # Multi-turn rewrite switch, rewrite the current question based only on the information in the messages
        "return_token_usage": True,
        "messages": [
            {
                "role": "system",
                "content": ""
            },
            {
                "role": "user",
                "content": "What is this paper about"
            }
        ]
    },
    "dense_weight": 0.5, # Adjust semantic search weight, 1 represents pure semantic search, only effective when vectorization model selects semantic + keyword model
    "post_processing": {
        "get_attachment_link": True, # Whether to return original images, only effective when OCR is enabled when creating knowledge base, otherwise automatically skip images
        "chunk_group": True, # Whether to aggregate recalled chunks by document
        "rerank_only_chunk": False, # Whether to rerank recalled chunks by document order
        "rerank_switch": False, # Whether to enable rerank
        "chunk_diffusion_count": 0 # Whether to recall adjacent chunks of the chunk, e.g. 1 means additionally recall one chunk above and below the current chunk
    }
}

    info_req = prepare_request(method=method, path=path, data=request_params)
    rsp = requests.request(
        method=info_req.method,
        url="http://{}{}".format(g_knowledge_base_domain, info_req.path),
        headers=info_req.headers,
        data=info_req.body
    )
    # print("search res = {}".format(rsp.text))
    return rsp.text

def chat_completion(message, stream=False, return_token_usage=True, temperature=0.7, max_tokens=4096):
    method = "POST"
    path = "/api/knowledge/chat/completions" # LLM generation
    request_params = {
        "messages": message, # Pass prompt, recalled chunks, historical multi-turn conversations through messages field
        "stream": True, # Whether to return in streaming mode
        "return_token_usage": True,
        "model": "your model name", # Default uses system public endpoint, if you need to configure a private endpoint created on Ark, you can pass ep_id here, and additionally specify api_key parameter, see chat_completions interface for detailed instructions
        "max_tokens": 4096,
        "temperature": 0.7,
        "model_version": "240828" 
    }

    info_req = prepare_request(method=method, path=path, data=request_params)
    rsp = requests.request(
        method=info_req.method,
        url="http://{}{}".format(g_knowledge_base_domain, info_req.path),
        headers=info_req.headers,
        data=info_req.body
    )
    print("chat completion res = {}".format(rsp.text))

def generate_prompt(rsp_txt): # System prompt concatenation
    rsp = json.loads(rsp_txt)
    if rsp["code"] != 0:
        return
    prompt = ""
    rsp_data = rsp["data"]
    points = rsp_data["result_list"]

    for point in points:
        # First concatenate system fields
        doc_info = point["doc_info"]
        for system_field in ["doc_name","title","chunk_title","content"] : 
            if system_field == 'doc_name' or system_field == 'title':
                if system_field in doc_info:
                    prompt += f"{system_field}: {doc_info[system_field]}\n"
            else:
                if system_field in point:
                    if system_field == "content" and doc_info["doc_type"] == "faq.xlsx":
                        question_field = "original_question"
                        prompt += f"content: When asked similar questions, please refer to the corresponding answer: Question:\"{point[question_field]}\". Answer:\"{point[system_field]}\"\n" # FAQ best practice
                    else:
                        prompt += f"{system_field}: {point[system_field]}\n"
        if "table_chunk_fields" in point:
            table_chunk_fields = point["table_chunk_fields"]
            for self_field in [] : 
                # Use next() to find the first matching item from table_chunk_fields
                find_one = next((item for item in table_chunk_fields if item["field_name"] == self_field), None)
                if find_one:
                    prompt += f"{self_field}: {find_one['field_value']}\n"

        prompt += "---\n"

    return base_prompt.format(prompt)

def search_knowledge_and_chat_completion():
   # 1. Execute search_knowledge
   rsp_txt = search_knowledge()
   # 2. Generate prompt
   prompt = generate_prompt(rsp_txt)
   #TODO: Users need to cache conversation information locally and add them to messages in order
   # 3. Concatenate message conversation, question corresponds to role user, system corresponds to role system, answer corresponds to role assistant, content corresponds to content
   messages =[
       {
           "role": "system",
           "content": prompt  # LLM instruction + search results
       },
       {
           "role": "user", 
           "content": "What are the latest RAG papers in 2024?" # Multi-turn historical conversation
       },
       {
           "role": "assistant",
           "content": "The latest RAG papers in 2024 are: \"XX\", \"xx\"" # Multi-turn historical conversation
       },
       {
           "role": "user",
           "content": query
       }
   ]

   # 4. Call chat_completion
   chat_completion(messages)

if __name__ == "__main__":
    search_knowledge_and_chat_completion()
```
