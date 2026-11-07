---
title: "Mixed text and image output sample"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Mixed_text_and_image_output_sample"
---

<span id="290953f6"></span>
# Overview

To replicate the console's mixed text and image effect in your knowledge base Q&A responses, you can follow this best practice guide. This document provides a complete Python code example that demonstrates how to call the `search_knowledge` and `chat_completions` APIs, process their responses, and render a final answer that seamlessly integrates text with relevant images.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9514f555d83d47ad918ac958da4cb206~tplv-goo7wpa0wc-image.image) </span>


* Related interfaces: [search_knowledge (new)](https://docs.byteplus.com/docs/209/collection_search_knowledge)[chat_completions (new)](https://docs.byteplus.com/docs/209/collection_chat_completions)

* Implementation principle:

   1. Optimize the prompt to enable the large language model (LLM) to output the reference chunk ID for the answer, and specify whether the corresponding image is suitable as an illustration.

   2. Parse the output from the large language model, locate the corresponding reference identifier, download and cache the corresponding image, and implement the appropriate style rendering on the frontend.

* Solution limitations:

   1. It is recommended to use vision\-language models (VLMs); other models may affect the accuracy of image selection.


<span id="799dd514"></span>
# **Prerequisites**

You need to complete account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication and Call Example" page. After creating the knowledge base and uploading documents, you can use the code below for knowledge base Q&A, and the answer content will support mixed text and image output.

<span id="65620365"></span>
# Complete code

```Python
import json
import requests


from volcengine.auth.SignerV4 import SignerV4
from volcengine.base.Request import Request
from volcengine.Credentials import Credentials

name = "your collection name" # Knowledge base name
project_name = "default" # Project to which the knowledge base belongs
query = "What is this paper DLSP: A Document Level Structure Parser for Multi-Page Digital Documents about" # User question
ak = "your ak" # AK obtained through "Prerequisites"
sk = "your sk" # SK obtained through "Prerequisites"
# Your account ID
g_knowledge_base_domain = "api-knowledgebase.mlp.cn-hongkong.bytepluses.com"


base_prompt = """
# Task
You are an online customer service representative. Your primary task is to respond to user questions with clever phrasing. You need to answer the following 'User Question' based on the 'Reference Materials', which are within <context></context> XML tags. You need to provide accurate and concise answers based on the reference materials.

Your answers must meet the following requirements:
    1. The content of the answer must be within the scope of the reference materials, answer the question as concisely as possible, and cannot make any extended explanations outside the reference materials.
    2. The answer needs to maintain friendly communication with the customer based on the customer's question and reference materials.
    3. If the reference materials cannot help you answer the user's question, inform the customer that the question cannot be answered and guide the customer to provide more detailed information.
    4. For confidentiality reasons, politely decline to answer questions about the document name or document author of the reference materials.

# Task Execution
Now please answer the user's questions based on the provided reference materials and follow the restrictions. Your answers need to be accurate and complete.

# Reference Materials
<context>
{documents}
</context>
"""

vision_base_prompt = """
# Task
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
 
{documents}
</context>
Images mentioned in the reference materials are arranged in upload order. Please answer the question by combining image and text information. If there are no images in the reference materials, please answer the question based only on the text information in the reference materials.
 
# Citation Requirements
1. When an answer can be provided, appropriately cite relevant reference materials at the end of sentences. Each reference material citation must use <reference> tag pairs, for example: <reference data-ref="{{point_id}}"></reference>
2. When informing the customer that the question cannot be answered, do not cite any reference materials
3. The 'data-ref' field represents the point_id of the corresponding reference material
 
 
# Illustration Requirements
1. First deeply understand the meaning of each image content in the reference materials, then filter out images directly related to the answer context from all images, and insert them as illustrations at appropriate positions in the answer. The image content must provide a direct visual explanation for the answer. If there are no suitable images in the reference materials, or the images are only indirectly related, omit the illustration.
2. Use <illustration> tag pairs to represent illustrations, for example: <illustration data-ref="{{point_id}}"></illustration>, where the 'point_id' field represents the point_id of the corresponding image. Each illustration tag pair must be on a new line, and the same image can only be used once.
 
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
    r.set_shema("https")
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
    path = "/api/knowledge/collection/search_knowledge"
    request_params = {
    "project": "default",
    "name": name,
    "query": query,
    "limit": 10,
    "pre_processing": {
        "need_instruction": True,
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
        ],
        "rewrite": False
    },
    "dense_weight": 0.5,
    "post_processing": {
        "get_attachment_link": True,
        "rerank_only_chunk": False,
        "rerank_switch": False,
        "chunk_group": True,
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

def is_vision_model(model_name):
    if model_name is None:
        return False
    return "vision" in model_name
    
def get_content_for_prompt(point: dict, image_num: int) -> str:
    content = point["content"]
    original_question = point.get("original_question")
    if original_question:
# In an FAQ recall scenario, because the content only contains the answer, you need to include the original question
        return f'When asked similar questions, please refer to the corresponding answer: Question: "{original_question}". Answer: "{content}"'
    if image_num > 0 and "chunk_attachment" in point and point["chunk_attachment"][0]["link"] : 
        placeholder = f"<img>Image{image_num}</img>"
        return content + placeholder
    return content


def generate_prompt(rsp_txt):
    rsp = json.loads(rsp_txt)
    if rsp["code"] != 0:
        return "", []
    prompt = ""
    image_urls = []
    rsp_data = rsp["data"]
    points = rsp_data["result_list"]
    using_vlm = is_vision_model("your model name")
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
        for system_field in ["doc_name","title","chunk_title","content","point_id"] : 
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


    return base_prompt.format(prompt), image_urls


def chat_completion(message, stream=False, return_token_usage=True, temperature=0.7, max_tokens=4096):
    method = "POST"
    path = "/api/knowledge/chat/completions"
    request_params = {
        "messages": message,
        "stream": False,  # Set to False
        "return_token_usage": True,
        "model": "your model name",
        "max_tokens": 4096,
        "temperature": 0.7,
        "model_version": "250115"
    }


    info_req = prepare_request(method=method, path=path, data=request_params)
    rsp = requests.request(
        method=info_req.method,
        url="http://{}{}".format(g_knowledge_base_domain, info_req.path),
        headers=info_req.headers,
        data=info_req.body
    )
    rsp.encoding = "utf-8"
    return rsp.text  # Return response text


def process_chat_completion_response(response_text, search_result_text):
    """Process chat completion response, extract generated answer and handle citation tags"""
    response_data = json.loads(response_text)


    if response_data["code"] != 0:
        return "Sorry, an error occurred while processing the answer."


    # Check returned data structure
    if "data" not in response_data or not response_data["data"]:
        return "Sorry, the returned data format is incorrect."


    # Get generated answer based on actual data structure
    try:
        generated_answer = None
        if "choices" in response_data["data"]:
            generated_answer = response_data["data"]["choices"][0]["message"]["content"]
        elif "message" in response_data["data"]:
            generated_answer = response_data["data"]["message"]["content"]
        elif "generated_answer" in response_data["data"]:
            generated_answer = response_data["data"]["generated_answer"]
        else:
            return "Sorry, unable to extract answer from returned data."
    except (KeyError, IndexError) as e:
        print("Error extracting answer:", str(e))
        return "Sorry, an error occurred while extracting the answer."


    # Parse citation tags
    import re
    reference_pattern = r'<reference data-ref="([^"]+)" data-img-ref="([^"]+)"></reference>'


    # Parse search results to get all chunk information
    search_result = json.loads(search_result_text)
    points = []
    if search_result["code"] == 0 and "data" in search_result and "result_list" in search_result["data"]:
        points = search_result["data"]["result_list"]


    # Create point_id to chunk mapping for quick lookup
    point_map = {point.get("point_id"): point for point in points if "point_id" in point}


    def replace_reference(match):
        point_id = match.group(1)
        img_ref = match.group(2).lower() == 'true'


        # Only process images when data-img-ref is true
        if img_ref and point_id in point_map:
            point = point_map[point_id]
            if "chunk_attachment" in point and point["chunk_attachment"]:
                for attachment in point["chunk_attachment"]:
                    if "link" in attachment:
                        image_link = attachment["link"]
                        # Convert to Markdown format image link
                        return f'![Image]({image_link})'


        # If conditions are not met or image not found, return empty string
        return ''


    # Replace all citation tags
    processed_answer = re.sub(reference_pattern, replace_reference, generated_answer)


    # Modify generated_answer in original response
    if "generated_answer" in response_data["data"]:
        response_data["data"]["generated_answer"] = processed_answer
    elif "choices" in response_data["data"]:
        response_data["data"]["choices"][0]["message"]["content"] = processed_answer
    elif "message" in response_data["data"]:
        response_data["data"]["message"]["content"] = processed_answer


    # Return modified complete response
    return json.dumps(response_data, ensure_ascii=False, indent=2)


def search_knowledge_and_chat_completion():
    # 1. Execute search_knowledge
    search_result_text = search_knowledge()
    # 2. Generate prompt
    prompt, image_urls = generate_prompt(search_result_text)
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


    # 4. Call chat_completion and get response
    response_text = chat_completion(messages)


    # 5. Process chat_completion response, return answer with image links
    processed_result = process_chat_completion_response(response_text, search_result_text)
    print(processed_result)


if __name__ == "__main__":
    search_knowledge_and_chat_completion()
```


<span id="1e59b5a1"></span>
## Description of search_knowledge interface return value

The search_knowledge interface returns the most similar chunk information after retrieval, as well as the corresponding chunk content. If the chunk contains an image, when you set the get_attachment_link parameter of the search_knowledge interface to True, the returned message will provide a temporary download link for the image in the `link` field of the `chunk_attachment` object. Note that the link is valid for 10 minutes.

```Python
{
    "code": 0,
    "data": {
        "collection_name": "test_pdf_zy",
        "count": 10,
        "token_usage": {
            "embedding_token_usage": {
                "prompt_tokens": 35,
                "completion_tokens": 0,
                "total_tokens": 35
            },
            "rerank_token_usage": 0
        },
        "result_list": [
            {
                "id": "_sys_auto_gen_doc_id-14474546439936949726-0",
                "content": "Seed-Thinking-v1.5: Advancing Superb Reasoning Models with Reinforcement Learning\nByteDance Seed\nFull author list in Contributions\nAbstract\nWe introduce Seed-Thinking-v1.5, capable of reasoning through thinking before responding, resulting in improved performance on a wide range of benchmarks. Seed-Thinking-v1.5 achieves 86.7 on AIME 2024, 55.0 on Codeforces and 77.3 on GPQA, demonstrating excellent reasoning abilities in STEM and coding. Beyond reasoning tasks, the method demonstrates notable generalization across diverse domains. For instance, it surpasses DeepSeek R1 by 8% in win rate on non-reasoning tasks, indicating its broader applicability. Compared to other state-of-the-art reasoning models, Seed-Thinking-v1.5 is a Mixture-of-Experts (MoE) model with a relatively small size, featuring 20B activated and 200B total parameters. As part of our effort to assess generalized reasoning, we develop two internal benchmarks, BeyondAIME and Codeforces, both of which will be publicly released to support future research.\n[Date: April 10, 2025\nFigure 1 Benchmark performance on reasoning tasks]Seed-Thinking-v1.5 DeepSeek R1 Gemini 2.5 pro OpenAI o3-mini-high 100 92.0 87.3 86.7 86.7 86.5 84.0 79.8 79.7 80 77.3 74.0 71.5 67.5 65.0 63.8 63.6 58.8 60 Accuracy (%) 56.3 55.0 49.2 49.3 48.0 47.0 45.0 42.4 39.9 40 27.6 25.8 20 18.3 AIME 2024 AIME 2025 Codeforces SWE-bench GPQA Diamond ARC-AGI Beyond AIME",
                "score": 0.4485875368118286,
                "point_id": "_sys_auto_gen_doc_id-14474546439936949726-0",
                "chunk_title": "Seed-Thinking-v1.5: Advancing Superb Reasoning Models with Reinforcement LearningAbstractDate: April 10, 2025\nFigure 1 Benchmark performance on reasoning tasks",
                "chunk_id": 0,
                "process_time": 1744807812,
                "doc_info": {
                    "doc_id": "_sys_auto_gen_doc_id-14474546439936949726",
                    "doc_name": "seed-thinking-v1.5.pdf",
                    "create_time": 1744807788,
                    "doc_type": "pdf",
                    "doc_meta": "[{\"field_name\":\"doc_id\",\"field_type\":\"string\",\"field_value\":\"_sys_auto_gen_doc_id-14474546439936949726\"}]",
                    "source": "tos_fe",
                    "title": "Seed-Thinking-v1.5: Advancing Superb Reasoning Models with Reinforcement Learning"
                },
                "recall_position": 2,
                "chunk_type": "image",
                "chunk_source": "document",
                "update_time": 1744807812,
                "chunk_attachment": [
                    {
                        "uuid": "c68dede9-c362-4fa9-b254-666893a92b33",
                        "caption": "Date: April 10, 2025\nFigure 1 Benchmark performance on reasoning tasks",
                        "type": "image",
                        "link": "https://knowledgebase-image.tos-cn-hongkong.bytepluses.com/c68dede9-c362-****-b254-666893a92b33?X-Tos-Algorithm=TOS4-HMAC-SHA256\u0026X-Tos-Credential=AKLTYzA0NGUwNTUzMjlhNGZjN2E5ZTQwYjlmZWJiYTMwODM%2F20250424%2Fcn-hongkong%2Ftos%2Frequest\u0026X-Tos-Date=20250424T035401Z\u0026X-Tos-Expires=600\u0026X-Tos-Signature=****a4d950b661cb4dcc2e726146730eb817421bd95891e646de3caf4e0bddbc\u0026X-Tos-SignedHeaders=host"
                    }
                ],
                "FromRecallQueue": "master_recall",
                "original_coordinate": {
                    "page_no": [
                        0,
                        0,
                        0,
                        0,
                        0,
                        0
                    ],
                    "bbox": [
                        [
                            0.1568839869281046,
                            0.13181597727272726,
                            0.8431165032679738,
                            0.17835829545454546
                        ],
                        [
                            0.4337450980392157,
                            0.2216444696969697,
                            0.5670680555555556,
                            0.2342235732323232
                        ],
                        [
                            0.3855555392156863,
                            0.24445758838383838,
                            0.6152536764705883,
                            0.25703661616161616
                        ],
                        [
                            0.4569754901960784,
                            0.303469797979798,
                            0.5430257026143791,
                            0.3185647474747475
                        ],
                        [
                            0.15502287581699345,
                            0.3281949747474748,
                            0.8464071241830066,
                            0.4766287878787879
                        ],
                        [
                            0.12087380652334176,
                            0.5504872485844776,
                            0.8730337105545343,
                            0.89134986954506
                        ]
                    ]
                }
            },

... ...
    },
    "message": "success",
    "request_id": "02174546684150800000000000000000000ffff0a00580c55b970"
}
```


<span id="b1db65a6"></span>
## Description of chat_completions interface return value

In this sample code, the generated_answer section of the original return value from the chat_completions interface identifies the image source referenced in the generated answer by using thetag.


* An example of a completetag is:

* data\-ref="_sys_auto_gen_doc_id\-42676952\*\*\*\*\*885639\-0": This provides the unique identifier (point\-id) of the referenced chunk, which can be used to identify and locate the corresponding chunk.

* data\-img\-ref="true/false": This attribute indicates whether the answer content is related to the image. If true, it means the image in this chunk is relevant to the answer content and needs to be processed and rendered accordingly. If false, it means the model determines that the image in this chunk is not relevant to the answer content and does not need to be processed.


```Plain
{
    "code": 0,
    "data": {
        "generated_answer": "Seed-Thinking-v1.5 is a model capable of reasoning through thinking before responding, with improved performance across a wide range of benchmarks.<reference data-ref=\"_sys_auto_gen_doc_id-14474546439936949726-0\" data-img-ref=\"true\"></reference><reference data-ref=\"_sys_auto_gen_doc_id-14474546439936949726-1\" data-img-ref=\"false\"></reference>.",
        "usage": "{
            \"prompt_tokens\": 5841,
            \"completion_tokens\": 94,
            \"total_tokens\": 5935,
            \"prompt_tokens_details\": {\"cached_tokens\": 0},
            \"completion_tokens_details\": {\"reasoning_tokens\": 0}
        }"
    },
    "message": "success",
    "request_id": "02174531357890000000000000000000000ffff0a0040921bc0f9"
}
```
