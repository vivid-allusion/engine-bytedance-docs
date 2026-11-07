---
title: "chat_completions (new)"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_chat_completions"
---

This section explains how to generate answers using a large language model using multi\-turn conversation history.

<span id="51091c52"></span>
# Overview

To generate answers from a large language model using multi\-turn conversation history, you can use the `/api/knowledge/chat/completions` endpoint. This API is a key component of the retrieval\-augmented generation (RAG) workflow and is designed to be used with the `search_knowledge` endpoint to create context\-aware, conversational responses.

<span id="9e97936f"></span>
# **Prerequisites**


* The knowledge base has been created.

* Documents have been imported and processed.

* After you complete account registration, identity verification, and obtain your AK/SK keys and signature on the "Integration Guide" page, you can call the API to perform knowledge base retrieval queries and generate integrated answers.

* Assemble and concatenate prompts locally.


<span id="dc543de7"></span>
# **Request endpoint**


|**URI** |/api/knowledge/chat/completions |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |The HTTP method for the request |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="450b7649"></span>
# **Request parameters**


|**Parameters** |**Sub\-parameters** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|model |\-\- |String |Yes |\-\- |**The large language model to use for generating responses**<br><br>Private inference access point IDs are in the following format:<br><br><br>* ep\-202406040\*\*\*\*\*\-\*\*\*\*\*<br><br><br>Caution: When using a private access point, you must provide the API key for authentication.<br><br>> Note: The default value may change with version updates. To ensure stable product performance, users are advised to specify the model version. |
|model_version |\-\- |string |No |\-\- |The range of available conversation models and image understanding models can be found in [Conversation model](https://docs.byteplus.com/docs/209/collection_chat_completions#c435c833) and [Image understanding model](https://docs.byteplus.com/docs/209/collection_chat_completions#d66b802b). |
|thinking |\-\- |json |No |enabled |**Controls whether the model enables deep thinking mode.** <br><br>Value range:<br><br><br>* enabled: Enables thinking mode. The model will always think before answering.<br><br>* disabled: Disables thinking mode. The model answers questions directly without reasoning.<br><br>* auto: Automatic thinking mode. The model determines whether thinking is needed based on the question and answers simple questions directly.<br><br><br>**Example:** <br><br>```Bash```<br>``````<br>```    extra_body={```<br>```        "thinking": {```<br>```            "type": "disabled",  # Do not use deep thinking capability```<br>```            # "type": "enabled", # Use deep thinking capability```<br>```            # "type": "auto", # The model determines whether to use deep thinking capability```<br>```        }```<br>```    }```<br> |
|api_key |\-\- |string |No |\-\- |**API Key for the endpoint**<br><br>To use a private model endpoint, the corresponding API key must be provided for authentication. |
|messages |\-\- |json |Yes |\-\- |The role of the participant sending the message. Available values include:<br><br><br>* system: System message<br><br>* user: User message<br><br>* assistant: Assistant message<br><br><br>**Multi\-turn text Q&A**: For example scripts, refer to [Multi-turn Q&A sample](https://docs.byteplus.com/docs/RAG_Cloud/Multi-turn)<br><br>```JSON```<br>```[```<br>```    {"role": "system", "content": "You are an online customer service representative. Your primary task is to respond to user inquiries with skillful communication. You need to answer the following 'user questions' based on the 'reference materials' provided within the <context></context> XML tags. You should provide accurate and concise answers based on the reference materials."},```<br>```    {"role": "user", "content": "Recommend a toy suitable for a 3-year-old child"},```<br>```    {"role": "assistant", "content": "Hello! 3-year-old children are at a stage of rapid development in physical, intellectual, and emotional aspects. You may want to consider the following types of toys: LEGO building blocks, puzzles, fire station and fire helicopter sets, medical toy sets, children's scooters"},```<br>```    {"role": "user", "content": "Please introduce in detail which LEGO building block series are suitable"}```<br>```]```<br><br><br>**Multi\-turn image and text understanding**: For example scripts, refer to [Multimodal Q&A sample](https://docs.byteplus.com/docs/RAG_Cloud/Multimodal_QA_sample)<br><br>```Plain```<br>```[```<br>```    {```<br>```        "role": "system",```<br>```        "content": "You are an online customer service representative tasked with skillfully responding to user inquiries. Answer the user's questions based on the reference materials provided in the <context> tags. These materials may include images, referenced by <img> tags, which correspond to the order of images uploaded by the user. Provide accurate and concise answers."```<br>```    },```<br>```    {```<br>```        "role": "user",```<br>```        "content": [```<br>```            {```<br>```                "type": "text",```<br>```                "text": "Recommend a toy suitable for a 3-year-old child"```<br>```            },```<br>```            {```<br>```                "type": "image_url",```<br>```                "image_url": {```<br>```                    "url": "https://ark-project.tos-cn-beijing.volces.XXX.jpeg" // Top 1 image URL retrieved from knowledge base```<br>```                }```<br>```            },```<br>```            {```<br>```                "type": "image_url",```<br>```                "image_url": {```<br>```                    "url": "https://ark-project.tos-cn-beijing.volcess.XXX.jpeg" // Top 2 image URL retrieved from knowledge base```<br>```                }```<br>```            }```<br>```        ]```<br>```    }```<br>```]```<br> |
|stream |\-\- |Boolean |No |False |**Whether the response content is returned in streaming mode**<br><br><br>* false: The model returns the result in one batch after generating all content.<br><br>* true: The model returns generated content in chunks according to the SSE protocol, ending with a `data: [DONE]` message. |
|max_tokens |\-\- |Integer |No |4096 |**The maximum number of tokens the model can generate**<br><br>> Caution<br><br>> * **The maximum length of model replies (in tokens) varies by model.** <br><br>> * **The total length of input tokens and output tokens is also limited by the model's context length.**  |
|return_token_usage |\-\- |Boolean |No |False |**Whether to return token usage statistics** |
|temperature |\-\- |Float |No |0.1 |**Sampling temperature**<br><br>Controls the degree of smoothing applied to the probability distribution of candidate words when generating text. The value range is [0, 1]. When set to 0, the model considers only the token with the highest log probability.<br><br>Higher values (such as 0.8) make the output more random, while lower values (such as 0.2) make the output more focused and deterministic. It is generally recommended to adjust only temperature or top_p, not both. |


<span id="c435c833"></span>
## **Conversation model**


|Model name |Model ID |Available versions |
|---|---|---|
|Deepseek\-R1\-64k |Deepseek\-r1 |250528 |


<span id="d66b802b"></span>
## **Image understanding model**


|Model name |Model ID |Available versions |
|---|---|---|
|ByteDance\-Seed\-1.6 |Seed\-1\-6 |250915, 250615 |
|ByteDance\-Seed\-1.6\-flash |Seed\-1\-6\-flash |250715, 250615 |
|Skylark\-vision |Skylark\-vision |250515 |


<span id="33177999"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |
|request_id |Unique identifier for each request |
|data |Model answer and token usage statistics |


Fields in the data object


|Field |Subfield |Field type |Description |
|---|---|---|---|
|reasoning_content |\-\- |string |Content of the reasoning chain used by the model to process the question<br><br>> Models that support returning this field: DeepSeek\-r1 |
|generated_answer |\-\- |string |Final answer from the model |
|usage |\-\- |object |An object containing token usage statistics |


<span id="2edb9989"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |Unauthorized |Missing authentication information |
|1000002 |403 |Permission denied |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |


<span id="59c65fc4"></span>
# Complete example

<span id="f4344f41"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/chat/completions \
  -d '{
        "model": "Seed-1-6",
        "max_tokens": 4096,
        "temperature": 0.1,
        "messages": [
                {
                    "role": "system",
                    "content": "prompt template"
                },
                {
                    "role": "user",
                    "content": "history content"
                },
                {
                    "role": "assistant",
                    "content": "history content"
                },
                {
                    "role": "user",
                    "content": "history content"
                },
                ...
           
                {
                    "role": "assistant",
                    "content": "history content"
                }         
            ],
        "stream":False,
        "return_token_usage": True
}'
```


<span id="79780a41"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 209
Content-Type: text/event-stream

{
    "code": 0,
    "data": {
        "generated_answer": "xxx",
        "usage": "{\"prompt_tokens\":13,\"completion_tokens\":217,\"total_tokens\":230}\n"
    },
    "message": "success",
    "request_id": "02172742276364600000000000000000000ffff0a00406fa14e0d"
    
}
```


Failed execution returns:

```JSON
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
