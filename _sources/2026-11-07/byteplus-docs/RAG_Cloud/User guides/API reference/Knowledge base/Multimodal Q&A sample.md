---
title: "Multimodal Q&A sample"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Multimodal_QA_sample"
---

<span id="f05d337c"></span>
# Overview

For Q&A scenarios involving complex multimodal information, the knowledge base product provides a set of best practices for multimodal Q&A based on large multimodal models, improving the accuracy of the knowledge base in image information understanding, extraction, and Q&A tasks.

<span id="4a6474a8"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature generation on the "Signature authentication method" page, as well as creating the knowledge base and uploading documents, you can call the following script to perform a complete knowledge base retrieval and Q&A.

For detailed API interface documentation, refer to:[search_knowledge (new)](https://docs.byteplus.com/docs/RAG_Cloud/90175)[chat_completions (new)](https://docs.byteplus.com/docs/RAG_Cloud/90186)

<span id="10cd34b1"></span>
## Code structure:


1. **Prepare request**: Construct an HTTP request and generate a signature to ensure the legitimacy and security of the request.

2. **Knowledge search**: Send a query request to the knowledge base service to obtain reference materials related to the user's question.

3. **Generate prompt**: Dynamically generate an appropriate text or visual Q&A template based on the knowledge search results.

4. **Chat completion**: Call the multimodal large model API to generate answers based on the user's question and reference materials.

5. **Main process control**: Connect knowledge search, prompt generation, and model response into a complete Q&A process, supporting the combination of text and images.


<span id="f38264de"></span>
## Code sample:

```Python
import json
import requests

from volcengine.auth.SignerV4 import SignerV4
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials

collection_name = "your collection" # Knowledge base name
project_name = "default" # Project to which the knowledge base belongs
query = "What is this paper DLSP: A Document Level Structure Parser for Multi-Page Digital Documents about" # User question
ak = "your ak" # AK obtained through "Prerequisites"
sk = "your sk" # SK obtained through "Prerequisites"
account_id = "your account_id" # Volcano account
g_knowledge_base_domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com"
model_name = "your model name" # Model name to use

base_prompt = """# Task
You are an online customer service representative. Your primary task is to respond to user questions with clever phrasing. You need to answer the following 'User Question' based on the 'Reference Materials', which are within <context></context> XML tags. You need to provide accurate and concise answers based on the reference materials.

Your answers must meet the following requirements:
    1. The content of the answer must be within the scope of the reference materials, answer the question as concisely as possible, and cannot make any extended explanations outside the reference materials.
    2. The answer needs to maintain friendly communication with the customer based on the customer's question and reference materials.
    3. If the reference materials cannot help you answer the user's question, inform the customer that the question cannot be answered and guide the customer to provide more detailed information.
    4. For confidentiality reasons, politely decline to answer questions about the document name or document author of the reference materials.


# Task Execution
Now please answer the user's questions based on the provided reference materials and following the restrictions. Your answers need to be accurate and complete.

# Reference Materials
<context>
{}
</context>
"""
vision_base_prompt = """# Task
You are an online customer service representative. Your primary task is to respond to user questions with clever phrasing. You need to answer the following 'User Question' based on the 'Reference Materials', which are within <context></context> XML tags. You need to provide accurate and concise answers based on the reference materials. The reference materials may contain image information, and image references are described within <img></img> XML tags. The order of images in the reference materials matches the order of images uploaded by the user.

Your answers must meet the following requirements:
    1. The content of the answer must be within the scope of the reference materials, answer the question as concisely as possible, and cannot make any extended explanations outside the reference materials.
    2. The answer needs to maintain friendly communication with the customer based on the customer's question and reference materials.
    3. If the reference materials cannot help you answer the user's question, inform the customer that the question cannot be answered and guide the customer to provide more detailed information.
    4. For confidentiality reasons, politely decline to answer questions about the document name or document author of the reference materials.

# Task Execution
Now please answer the user's questions based on the provided reference materials and following the restrictions. Your answers need to be accurate and complete.

# Reference Materials
<context>
{}
</context>

Images mentioned in the reference materials are arranged in upload order. Please answer the question by combining image and text information. If there are no images in the reference materials, please answer the question based only on the text information in the reference materials.
"""
# Prepare request: Construct HTTP request and generate signature to ensure request legitimacy and security
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

# Knowledge search: Send query request to knowledge base service to obtain reference materials related to user's question
def search_knowledge():
    method = "POST"
    path = "/api/knowledge/collection/search_knowledge"
    request_params = {
    "project": project_name,
    "name": collection_name,
    "query": query,
    "limit": 10,
    "pre_processing": {
        "need_instruction": True,
        "rewrite": False,
        "return_token_usage": True,
        "messages": [
            {
                "role": "system",
                "content": ""
            },
            {
                "role": "user",
                "content": query
            }
        ]
    },
    "dense_weight": 0.5,
    "post_processing": {
        "get_attachment_link": True,
        "chunk_group": True,
        "rerank_only_chunk": False,
        "rerank_switch": False,
        "chunk_diffusion_count": 0
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

# Chat completion: Call multimodal LLM API to generate answers based on user questions and reference materials
def chat_completion(message, stream=False, return_token_usage=True, temperature=0.7, max_tokens=4096):
    method = "POST"
    path = "/api/knowledge/chat/completions"
    request_params = {
        "messages": message,
        "stream": False,
        "return_token_usage": True,
        "model": model_name,
        "max_tokens": 4096,
        "temperature": 0.7,
    }

    info_req = prepare_request(method=method, path=path, data=request_params)
    rsp = requests.request(
        method=info_req.method,
        url="http://{}{}".format(g_knowledge_base_domain, info_req.path),
        headers=info_req.headers,
        data=info_req.body
    )
    print("chat completion res = {}".format(rsp.text))

def is_vision_model(model_name):
    return model_name == "your model name"

def get_content_for_prompt(point: dict, image_num: int) -> str:
    content = point["content"]
    original_question = point.get("original_question")
    if original_question:
        # FAQ recall scenario, content only contains the answer, need to include the original question
        return "When asked similar questions, please refer to the corresponding answer: Question:\"{question}\". Answer:\"{answer}\"".format(
                question=original_question, answer=content)
    if image_num > 0 and "chunk_attachment" in point and point["chunk_attachment"][0]["link"]:
        placeholder = f"<img>Image{image_num}</img>"
        return content + placeholder
    return content
    
# Generate Prompt: Dynamically generate text or visual Q&A template based on knowledge search results
def generate_prompt(rsp_txt):
    rsp = json.loads(rsp_txt)
    if rsp["code"] != 0:
        return "", []
    prompt = ""
    image_urls = []
    rsp_data = rsp["data"]
    points = rsp_data["result_list"]
    using_vlm = is_vision_model(model_name)
    image_cnt = 0

    for point in points:
        # Extract image links
        if using_vlm and "chunk_attachment" in point:
            image_link = point["chunk_attachment"][0]["link"]
            if image_link:
                image_urls.append(image_link)
                image_cnt += 1
        # First concatenate system fields
        doc_info = point["doc_info"]
        for system_field in ["doc_name", "title", "chunk_title", "content"] : 
            if system_field == 'doc_name' or system_field == 'title':
                if system_field in doc_info:
                    prompt += f"{system_field}: {doc_info[system_field]}\n"
            else:
                if system_field in point:
                    if system_field == "content":
                        prompt += f"content: {get_content_for_prompt(point, image_cnt)}\n"
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

    if using_vlm:
        return vision_base_prompt.format(prompt), image_urls
    return base_prompt.format(prompt), image_urls

# Main process control: Connect knowledge search, Prompt generation, and model response into a complete Q&A process, supporting text and image combination
def search_knowledge_and_chat_completion():
    # 1. Execute search_knowledge
    rsp_txt = search_knowledge()
    # 2. Generate prompt
    prompt, image_urls = generate_prompt(rsp_txt)
    #TODO: Users need to cache conversation information locally and add them to messages in order
    # 3. Concatenate message conversation, question corresponds to role user, system corresponds to role system, answer corresponds to role assistant, content corresponds to content
    if image_urls:
        multi_modal_msg = [{"type": "text", "text": query}]
        for image_url in image_urls:
            multi_modal_msg.append({"type": "image_url", "image_url": {"url": image_url}})
        messages =[
            {
                "role": "system",
                "content": prompt
            },
            {
                "role": "user",
                "content": multi_modal_msg
            }
        ]
    else:
        messages =[
            {
                "role": "system",
                "content": prompt
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
