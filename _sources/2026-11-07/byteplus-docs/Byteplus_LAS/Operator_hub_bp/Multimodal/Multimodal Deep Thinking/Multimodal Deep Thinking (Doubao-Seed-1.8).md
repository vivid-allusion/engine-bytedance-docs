---
title: "Multimodal Deep Thinking (Doubao-Seed-1.8)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-1-8"
---

<span id="1ae3b7b7"></span>
# Operator introduction

<span id="2e76a426"></span>
## Description

Provides deep thinking capabilities of large models in multimodal scenarios.

Use models with deep thinking capabilities to analyze and understand images, videos or texts, and return structured text output. The operator will automatically build a message structure that conforms to the specifications of multimodal models, and users only need to provide image / video / text data as agreed to complete the inference.

<span id="da8ba1ea"></span>
## Core Features


* Deep thinking mechanism: The model automatically performs problem decomposition and logical reasoning before answering questions, and generates a chain of thought (reasoning_content)

* Multimodal scenario support: Supports image / video / text input at the same time, and automatically completes multimodal message assembly

* Input simplification mechanism: Supports multiple data sources such as local files, HTTP/HTTPS URLs, TOS/S3 object storage, etc., and visual understanding capabilities can be realized through simple configuration

* Flexible thinking mode: Supports controlling the deep thinking mode (enabled / disabled / auto) through the thinking_type parameter, to flexibly balance between answer quality and performance


<span id="e98ac5df"></span>
## Input and Output Specifications


* Input format:

* Images (images): Supports string or list format

* Supported data source types:

* url: Network resource address, supports http/https/tos/s3, pre\-signed URLs will be automatically generated for TOS/S3

* base64: Base64 encoded data

* binary: Binary data (will be converted to Base64 encoding internally)

* Videos (videos): Supports string or list format, with the same data source types as images

* Texts (texts): Supports string or list format, used as user prompt input

   ```Plain Text
   (Mixing string and list types in the same field is not allowed)
   ```
   

* Output format:

* Default mode: Returns struct type, containing the following fields:

* llm_result: Final answer content of the model

* reasoning_content: Chain of thought / reasoning process of the model

* When the environment variable LAS_LLM_FINISH_REASON_CHECK=true is set, the struct will additionally include:

* finish_reason: Reason for the end of the model result, the value range includes:

* stop: Normal termination

* length: Exceeded token limit

* content_filter: Hit content filtering policy

* When the environment variable LAS_LLM_BOTS_REFERENCES=true is set, the struct will additionally include:

* references: Retrieval results or external knowledge information cited by the model, which is convenient for downstream transparent transmission and parsing


<span id="28297262"></span>
## Model Capability Enhancement


* Chain of thought visualization: Outputs the reasoning process of the model through the reasoning_content field, which is convenient for observation and review

* Result reliability control: Identifies abnormal termination situations such as length truncation or content filtering through the finish_reason field

* Multimodal understanding: Supports mixed input parsing of images / videos / texts, which is suitable for complex multimodal scenarios


<span id="baa0b57e"></span>
# Rest API Call

<span id="500b97b0"></span>
## Chat

<span id="bff307d1"></span>
### API Description

Call the seed\-1.8 model through the Chat interface for multimodal understanding.

Supported model and version: `seed-1-8-251228`.

<span id="a481f416"></span>
### Request Parameters


|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|model |string |Yes |seed\-1\-8\-251228 |Model name and version, in the format of `model-name-version`. seed\-1\-8\-251228 is supported. |
|messages |list of chat_message |Yes | |A list of messages composed of the conversation up to now. Different models support different types of messages, such as text, image, video, etc. For the usage of this field, refer to the messages parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384). |
|max_tokens |integer |No |10000 |Value range: varies by model, see [Model List](https://docs.byteplus.com/en/docs/ModelArk/1330310) for details.<br><br>Maximum length of the model's response (unit: token).<br><br><br>* The model's response does not include chain\-of\-thought content. `Model response = Model output - Model chain-of-thought (if any)`.<br><br>* The total length of output tokens is also limited by the model's context length. |
|max_completion_tokens |integer |No |10000 |> For models supporting this field and usage instructions, refer to [Documentation](https://docs.byteplus.com/en/docs/ModelArk/1449737).<br><br><br>Value range: [0, 64k].<br><br>Controls the maximum length of the model output (including the length of model response and model chain\-of\-thought content, unit: token). After configuring this parameter, the model can output super long content, the max_tokens (default value 4k) becomes invalid, and the model outputs content (response and chain\-of\-thought) on demand until it reaches the value configured for max_completion_tokens.<br><br>Cannot be set simultaneously with the max_tokens field, otherwise an error will be reported directly. |
|stop |list of string |No | |Default value is null.<br><br>The model will stop generating when it encounters the string specified in the stop field, and the string itself will not be output. Up to 4 strings are supported.<br><br>> [Deep thinking capability model](https://docs.byteplus.com/en/docs/ModelArk/1330310) does not support this field. |
|frequency_penalty |float |No |1.0 |Value range is [\-2.0, 2.0]. Frequency penalty coefficient. If the value is positive, new tokens will be penalized based on their frequency of occurrence in the text, reducing the possibility of the model repeating word for word. |
|presence_penalty |float |No |1.0 |Value range is [\-2.0, 2.0]. Presence penalty coefficient. If the value is positive, new tokens will be penalized based on whether they have appeared in the text so far, increasing the possibility of the model talking about new topics. |
|temperature |float |No |1 |Value range is [0, 2]. Sampling temperature. Controls the degree of smoothing applied to the probability distribution of each candidate word when generating text. When the value is 0, the model only considers the token with the highest log probability. Higher values (e.g. 0.8) make the output more random, while lower values (e.g. 0.2) make the output more focused and deterministic. It is generally recommended to adjust only one of temperature or top_p, not both. |
|top_p |float |No |0.5 |Value range is [0, 1]. Nucleus sampling probability threshold. The model considers token results whose probability mass is within top_p. When the value is 0, the model only considers the token with the highest log probability. 0.1 means only the top 10% of tokens with the highest probability mass are considered. The larger the value, the higher the randomness of generation, and the lower the value, the higher the certainty of generation. It is generally recommended to adjust only one of temperature or top_p, not both. |
|thinking |request_thinking |No | |Controls whether the model enables deep thinking mode. Deep thinking mode is enabled by default and can be turned off manually. For the usage of this field, refer to the thinking parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384). |
|response_format |request_response_format |No | |The model output content must follow the format specified here. For the usage of this field, refer to the response_format parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384). |
|tools |list of chat_tool |No | |List of tools to be called, which can be included in the model's return information. When you need the model to return the tools to be called, you need to configure this structure. For the usage of this field, refer to the tools parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384). |
|tool_choice |string or object |No | |> Only seed\-1\-6\-\*\*\* and later generation models support this field.<br><br><br>Indicates whether there are tools to be called in the model's return information for this request. When no tools are specified, none is the default value. If tools exist, auto is the default value.<br><br>**Tool selection mode (string)** <br><br><br>* none: The model's return information cannot contain tools to be called.<br><br>* required: The model's return information must contain tools to be called. When selecting this option, please confirm that suitable tools exist to reduce the occurrence of model hallucinations.<br><br>* auto: The model determines on its own whether there are tools to be called in the return information.<br><br><br>**Tool call (object)** <br><br><br>* Specifies the scope of tools to be called. Only the following model information is allowed in the model's return information. When selecting this option, please confirm that the tool is suitable for user needs to reduce the occurrence of model hallucinations. tool_choice.name specifies the name of the tool to be called, and tool_choice.type specifies the type of call. |


<span id="3f55f8a5"></span>
### Response Data

```mixin-react
const properties = ({
  "columns": [
    {
      "title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
      "title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
      "title": "Example",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 150
    },
    {
      "title": "Description",
      "dataIndex": "column_3",
      "key": "column_3"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "id",
      "column_1": "string",
      "column_2": "0217426318107460cfa43dc3f3683b1de1c09624ff49085a456ac",
      "column_3": "Unique identifier of this request."
    },
    {
      "key": "2",
      "column_0": "model",
      "column_1": "string",
      "column_2": "",
      "column_3": "Name and version of the model actually used for this request."
    },
    {
      "key": "3",
      "column_0": "created",
      "column_1": "integer",
      "column_2": "",
      "column_3": "Unix timestamp (in seconds) of the creation time of this request."
    },
    {
      "key": "4",
      "column_0": "object",
      "column_1": "string",
      "column_2": "chat.completion",
      "column_3": "Fixed to `chat.completion`."
    },
    {
      "key": "5",
      "column_0": "choices",
      "column_1": "list of choice",
      "column_2": "",
      "column_3": "Model output content of this request.",
      "children": [
        {
          "key": "5-1",
          "column_0": "index",
          "column_1": "integer",
          "column_2": "0",
          "column_3": "Index of the current element in the choices list."
        },
        {
          "key": "5-2",
          "column_0": "finish_reason",
          "column_1": "string",
          "column_2": "stop",
          "column_3": <div>Reason why the model stops generating tokens. Value range:<ul><li>`stop`: The model output ends naturally, or is truncated because it hits the field specified in the request parameter stop.</li><li>`length`: The model output is truncated because it reaches the model output limit, for the following reasons:</li><li>Triggers the `max_tokens` limit (length limit of response content).</li><li>Triggers the `max_completion_tokens` limit (length limit of chain-of-thought content + response content)</li><li>Triggers the `context_window` limit (length limit of input content + chain-of-thought content + response content).</li><li>`content_filter`: The model output is intercepted by content moderation.</li><li>`tool_calls`: The model called a tool.</li></ul></div>
        },
        {
          "key": "5-3",
          "column_0": "message",
          "column_1": "message",
          "column_2": "",
          "column_3": "Content output by the model.",
          "children": [
            {
              "key": "5-3-1",
              "column_0": "role",
              "column_1": "string",
              "column_2": "assistant",
              "column_3": "Role of the content output, fixed to `assistant` here."
            },
            {
              "key": "5-3-2",
              "column_0": "content",
              "column_1": "string",
              "column_2": "",
              "column_3": "Message content generated by the model."
            },
            {
              "key": "5-3-3",
              "column_0": "reasoning_content",
              "column_1": "string",
              "column_2": "",
              "column_3": "Chain-of-thought content of the model processing the problem. Only deep reasoning models support returning this field."
            },
            {
              "key": "5-3-4",
              "column_0": "tool_calls",
              "column_1": "list of tool_call",
              "column_2": "",
              "column_3": "Tool calls generated by the model.",
              "children": [
                {
                  "key": "5-3-4-1",
                  "column_0": "id",
                  "column_1": "string",
                  "column_2": "assistant",
                  "column_3": "Role of the content output, fixed to `assistant` here."
                },
                {
                  "key": "5-3-4-2",
                  "column_0": "type",
                  "column_1": "string",
                  "column_2": "function",
                  "column_3": "Tool type, currently only `function` is supported."
                },
                {
                  "key": "5-3-4-3",
                  "column_0": "function",
                  "column_1": "function",
                  "column_2": "function",
                  "column_3": "Function called by the model.",
                  "children": [
                    {
                      "key": "5-3-4-3-1",
                      "column_0": "name",
                      "column_1": "string",
                      "column_2": "",
                      "column_3": "Name of the function called by the model."
                    },
                    {
                      "key": "5-3-4-3-2",
                      "column_0": "arguments",
                      "column_1": "string",
                      "column_2": "",
                      "column_3": "Parameters generated by the model for calling the function, in JSON format.<br/> The model does not always generate valid JSON, and may hallucinate some parameters that are not defined in your function parameter specification. Before calling the function, please verify the validity of these parameters in your code."
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "key": "5-4",
          "column_0": "logprobs",
          "column_1": "logprobs",
          "column_2": "",
          "column_3": "Log probability information of the current content.",
          "children": [
            {
              "key": "5-4-1",
              "column_0": "content",
              "column_1": "list of lpb_content",
              "column_2": "",
              "column_3": "Log probability information of tokens in each content element in the message list.",
              "children": [
                {
                  "key": "5-4-1-1",
                  "column_0": "token",
                  "column_1": "string",
                  "column_2": "",
                  "column_3": "Current token."
                },
                {
                  "key": "5-4-1-2",
                  "column_0": "bytes",
                  "column_1": "list of integer",
                  "column_2": "",
                  "column_3": "UTF-8 value of the current token, in the format of an integer list. It can be used for character encoding and decoding when a character is composed of multiple tokens (such as emojis or special characters). It is empty if the token has no UTF-8 value."
                },
                {
                  "key": "5-4-1-3",
                  "column_0": "logprob",
                  "column_1": "float",
                  "column_2": "",
                  "column_3": "Log probability of the current token."
                },
                {
                  "key": "5-4-1-4",
                  "column_0": "top_logprobs",
                  "column_1": "list of top_logprobs",
                  "column_2": "",
                  "column_3": "List of the most likely tokens and their log probabilities at the current token position. In some cases, the number returned may be less than the number specified by the request parameter top_logprobs.",
                  "children": [
                    {
                      "key": "5-4-1-4-1",
                      "column_0": "token",
                      "column_1": "string",
                      "column_2": "",
                      "column_3": "Current token."
                    },
                    {
                      "key": "5-4-1-4-2",
                      "column_0": "bytes",
                      "column_1": "list of integer",
                      "column_2": "",
                      "column_3": "UTF-8 value of the current token, in the format of an integer list. It can be used for character encoding and decoding when a character is composed of multiple tokens (such as emojis or special characters). It is empty if the token has no UTF-8 value."
                    },
                    {
                      "key": "5-4-1-4-3",
                      "column_0": "logprob",
                      "column_1": "float",
                      "column_2": "",
                      "column_3": "Log probability of the current token."
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "key": "5-5",
          "column_0": "moderation_hit_type",
          "column_1": "string",
          "column_2": "",
          "column_3": <div>When the text output by the model contains sensitive information, the risk classification tag hit by the model output text will be returned. Return values and meanings:<ul><li>`severe_violation`: The text output by the model involves serious violations.</li><li>`violence`: The text output by the model involves radical behavior.</li></ul></div>
        }
      ]
    },
    {
      "key": "6",
      "column_0": "usage",
      "column_1": "usage",
      "column_2": "",
      "column_3": "Token usage of this request.",
      "children": [
        {
          "key": "6-1",
          "column_0": "total_tokens",
          "column_1": "integer",
          "column_2": "10000",
          "column_3": "Total number of tokens consumed by this request (input + output)."
        },
        {
          "key": "6-2",
          "column_0": "prompt_tokens",
          "column_1": "integer",
          "column_2": "1000",
          "column_3": "Number of tokens of the content input to the model for processing."
        },
        {
          "key": "6-3",
          "column_0": "prompt_tokens_details",
          "column_1": "prompt_tokens_details",
          "column_2": "",
          "column_3": "Details of the number of tokens of the content input to the model for processing.",
          "children": [
            {
              "key": "6-3-1",
              "column_0": "cached_tokens",
              "column_1": "integer",
              "column_2": "100",
              "column_3": "Token usage of cached input content, should be `0` here."
            }
          ]
        },
        {
          "key": "6-4",
          "column_0": "completion_tokens",
          "column_1": "integer",
          "column_2": "9000",
          "column_3": "Tokens spent on the model output content."
        },
        {
          "key": "6-5",
          "column_0": "completion_tokens_details",
          "column_1": "completion_tokens_details",
          "column_2": "",
          "column_3": "Details of the tokens spent on the model output content.",
          "children": [
            {
              "key": "6-5-1",
              "column_0": "reasoning_tokens",
              "column_1": "integer",
              "column_2": "200",
              "column_3": "Number of tokens spent on outputting chain-of-thought content."
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```



|Parameter name |Type |Example |Description |
|---|---|---|---|
|id |string |0217426318107460cfa43dc3f3683b1de1c09624ff49085a456ac |Unique identifier of this request. |
|model |string | |Name and version of the model actually used for this request. |
|created |integer | |Unix timestamp (in seconds) of the creation time of this request. |
|object |string |chat.completion |Fixed to `chat.completion`. |
|choices |list of choice | |Model output content of this request. |
|usage |usage | |Token usage of this request. |


<span id="873ae795"></span>
### Examples

<span id="fb8791a9"></span>
#### Request Example

```BASH
curl --location "${LAS_ENDPOINT}/api/v1/chat/completions" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $$LAS_API_KEY" \
--data '{
    "messages": [
        {
            "role": "user",
            "content": [
                {
                    "type": "video_url",
                    "video_url": {
                        "url": "https://las-ai-cn-beijing.tos-cn-beijing.volces.com/qa/operator_cards/0.1.0/video_keyframes/sample.mp4"
                    }
                },
                {
                    "type": "text",
                    "text": "What is in the video"
                }
            ]
        }
    ],
    "model": "seed-1-8-251228"
}'
```


<span id="f3fac88a"></span>
#### Response Example

```JSON
{
    "id": "021768911071736e97fe2f517eced7c4391200710ba13b1ae8bec",
    "object": "chat.completion",
    "created": 1768911086,
    "model": "seed-1-8-251228",
    "serviceTier": "default",
    "choices": [
      {
        "index": 0,
        "message": {
          "role": "assistant",
          "content": "The video presents the following content:\nA lady wearing a light-colored wide-brimmed sun hat, sunglasses, a white top and a floral long skirt sits on a black folding chair next to a white mottled building, playing the accordion while singing devotedly. There is a bottle of water on the ground beside her. The background is the open blue water, and land covered with green plants can be seen in the distance. The scene is located in a coastal area. The camera moves and zooms in during the video to show the details of the performance, and later a pedestrian wearing a green top and khaki bottoms passes by from the right side of the frame.",
          "name": null,
          "reasoning_content": "The user now needs to summarize the content in the video. First look at the video: A lady wearing a light-colored wide-brimmed hat, sunglasses, a white top and a floral skirt sits on a folding chair next to a white building, playing the accordion while singing. The background is the seaside, with blue water and distant land. The camera moves, and later a pedestrian (green top, khaki pants, etc.) walks by. These elements need to be sorted out:\n\nIn the video, a lady wearing a light-colored wide-brimmed sun hat, sunglasses, a white top and a floral long skirt sits on a black folding chair next to a white building (with mottled traces on the wall), playing the accordion while singing. There is a bottle of water beside her. The background is the open blue water and distant land covered with green plants, and the environment is a coastal area. During the process, the camera is adjusted to zoom in to show the details of the performance, and a pedestrian (person wearing a green top and khaki bottoms) passes by from the right side of the frame.",
          "function_call": null,
          "tool_calls": null,
          "tool_call_id": null
        },
        "finish_reason": "stop",
        "moderation_hit_type": null,
        "logprobs": null
      }
    ],
    "usage": {
      "prompt_tokens": 3930,
      "completion_tokens": 294,
      "total_tokens": 4224,
      "prompt_tokens_details": {
        "cached_tokens": 0,
        "provisioned_tokens": null
      },
      "completion_tokens_details": {
        "reasoning_tokens": 189,
        "provisioned_tokens": null
      }
    }
}
```


<span id="af974cdd"></span>
### Error Codes


|HTTP Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |Invalid model name |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API key |


<span id="dab2148a"></span>
## Responses

<span id="5602ebbf"></span>
### API Description

Call the seed\-1.8 model for multimodal understanding through the Responses interface. For interface definition, refer to [Response API](https://docs.byteplus.com/en/docs/ModelArk/Create_model_request).

Supported model and version: `seed-1-8-251228`.

<span id="8c037896"></span>
### Examples

<span id="6fadd64a"></span>
#### Request Example

```BASH
curl --location "${LAS_ENDPOINT}/api/v1/responses" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $$LAS_API_KEY" \
--data '{
    "input": [
        {
            "role": "user",
            "content": [
                {
                    "type": "input_video",
                    "video_url":  "https://las-ai-cn-beijing.tos-cn-beijing.volces.com/qa/operator_cards/0.1.0/video_keyframes/sample.mp4"
                },
                {
                    "type": "input_text",
                    "text": "What is in the video"
                }
            ]
        }
    ],
    "model": "seed-1-8-251228"
}'
```


<span id="16231fb2"></span>
#### Response Example

```JSON
{
    "created_at": 1772617764,
    "error": null,
    "id": "resp_021772617762470960a4483e1c6480e5dcf931407efe2bda06a32",
    "incomplete_details": null,
    "max_output_tokens": 32768,
    "model": "seed-1-8-251228",
    "object": "response",
    "output": [
        {
            "type": "reasoning",
            "id": "rs_02177261776458300000000000000000000ffffac1504e228c011",
            "summary": [
                {
                    "type": "summary_text",
                    "text": "The user now needs to analyze the video content. First look at the picture: a lady wearing a light wide-brimmed hat, sunglasses, a white top and a floral skirt sits on a folding chair next to a white building, playing the accordion while singing. The background is the seaside, with blue waters and distant land. There are other elements in the video: there is a water bottle next to her, and later pedestrians (a person in a green top and khaki pants, and another person) walk past her. The whole scene is the outdoor seaside. The lady concentrates on playing the accordion and singing, with movements including pressing the keys of the accordion, pushing and pulling the bellows, and swinging her head with the music. Now sort out these elements and describe them clearly."
                }
            ],
            "status": "completed"
        },
        {
            "type": "message",
            "id": "msg_02177261776828500000000000000000000ffffac1504e2a4e276",
            "role": "assistant",
            "content": [
                {
                    "type": "output_text",
                    "text": "The content presented in the video:\n1. Characters and behaviors: A lady wearing a light wide-brimmed sun hat, sunglasses, a white top and a long dress with floral patterns sits on a folding chair next to a white building, playing the accordion (pressing the keys with her hands, pushing and pulling the bellows) while singing, and her head also moves to the rhythm of the music; later two pedestrians (one in lake green top and khaki bottoms, one in white top) pass by her.\n2. Environment and items: The scene is an outdoor seaside area, with blue waters and distant green land visible in the background; a bottle of mineral water is placed on the ground next to the lady, and there is an open box behind her.",
                    "annotations": null
                }
            ],
            "status": "completed",
            "partial": null
        }
    ],
    "previous_response_id": null,
    "thinking": null,
    "reasoning": null,
    "service_tier": "default",
    "status": "completed",
    "temperature": null,
    "tools": null,
    "top_p": null,
    "usage": {
        "input_tokens": 3930,
        "output_tokens": 276,
        "total_tokens": 4206,
        "input_tokens_details": {
            "cached_tokens": 0
        },
        "output_tokens_details": {
            "reasoning_tokens": 137
        },
        "tool_usage": null,
        "tool_usage_details": null
    },
    "caching": {
        "type": "disabled",
        "prefix": null
    },
    "text": null,
    "instructions": null,
    "store": true,
    "expire_at": 1772876962,
    "tool_choice": null,
    "parallel_tool_calls": null,
    "max_tool_calls": null
}
```
