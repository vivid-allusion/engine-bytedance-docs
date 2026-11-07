---
title: "Multimodal Deep Thinking (Doubao-Seed-2.0)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-2-0"
---

# Operator introduction

## Description

Provides deep thinking capabilities of large models in multimodal scenarios.

Use models with deep thinking capabilities to analyze and understand images, videos or texts, and return structured text output. The operator will automatically build a message structure that conforms to the specifications of multimodal models, and users only need to provide image / video / text data as agreed to complete the inference.

## Core Features

* Deep thinking mechanism: The model automatically performs problem disassembly and logical reasoning before answering questions, and generates a chain of thought (reasoning_content)

* Multimodal scenario support: Supports image / video / audio / text input at the same time, and automatically completes multimodal message assembly

* Input simplification mechanism: Supports multiple data sources such as local files, HTTP/HTTPS URLs, TOS/S3 object storage, etc. Visual understanding capabilities can be realized through simple configuration

* Flexible thinking mode: Supports controlling the deep thinking mode (enabled / disabled / auto) through the thinking_type parameter, to make a flexible trade\-off between answer quality and performance

## Input and Output Specifications

* Input format:

* Images: Supports string or list format

* Supported data source types:

* url: Network resource address, supports http/https/tos/s3, pre\-signed URLs will be automatically generated for TOS/S3

* base64: Base64 encoded data

* binary: Binary data (will be converted to Base64 encoding internally)

* Videos: Supports string or list format, and the data source types are consistent with images

* Audios: Supports string or list format, and the data source types are consistent with images

* Texts: Supports string or list format, used as user prompt input

   ```Plain Text
   (Mixing string and list types in the same field is not allowed)
   ```

* Output format:

* Default mode: Returns struct type, including the following fields:

* llm_result: Final answer content of the model

* reasoning_content: Chain of thought / reasoning process of the model

* When the environment variable LAS_LLM_FINISH_REASON_CHECK=true is set, the struct will additionally include:

* finish_reason: Reason for the end of the model result, the value range includes:

* stop: Normal termination

* length: Exceeded token limit

* content_filter: Hit content filtering policy

* When the environment variable LAS_LLM_BOTS_REFERENCES=true is set, the struct will additionally include:

* references: Retrieval results or external knowledge information cited by the model, which is convenient for downstream transparent transmission and parsing

## Model Capability Enhancement

* Chain of thought visualization: Outputs the reasoning process of the model through the reasoning_content field, which is convenient for observation and review

* Result reliability control: Identifies abnormal termination situations such as length truncation or content filtering through the finish_reason field

* Multimodal understanding: Supports mixed input parsing of images / videos / texts, which is suitable for complex multimodal scenarios

# Rest API Call

## Chat

### API Description

Call the seed\-2.0 model through the Chat interface for multimodal understanding.

Supported models and versions: `seed-2-0-pro-260328`.

### Request Parameters

**model** string 必选 `Example value: seed-2-0-pro-260328`

Model name and version, in the format of `model-name-version`. Supported values: seed\-2\-0\-pro\-260328, seed\-2\-0\-lite\-260428, seed\-2\-0\-mini\-260428

**messages** list of chat_message 必选

A list of messages composed of the conversation up to now. Different models support different types of messages, such as text, image, video, etc. For the usage of this field, refer to the `messages` parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384).

**max_tokens** integer `Example value: 10000`

Value range: varies by model, see [Model List](https://docs.byteplus.com/en/docs/ModelArk/1330310) for details.

Maximum length of the model's response (unit: token).

* The model response does not include chain\-of\-thought content. `Model response = Model output - Model chain of thought (if any)`.

* The total length of output tokens is also limited by the model's context window length.

**max_completion_tokens** integer `Example value: 10000`

> For models supporting this field and usage instructions, refer to [Documentation](https://docs.byteplus.com/en/docs/ModelArk/1449737).

> Value range: [0, 64k].

> Controls the maximum length of the model output (including the length of model response and model chain\-of\-thought content, unit: token). After configuring this parameter, the model can output ultra\-long content, the `max_tokens` (default value 4k) becomes invalid, and the model outputs content (response and chain of thought) as needed until the value configured for `max_completion_tokens` is reached.

> Cannot be set simultaneously with the `max_tokens` field, otherwise an error will be reported directly.

**stop** list of string

Default value is null.

The model will stop generating further content when it encounters the string specified in the `stop` field, and the string itself will not be output. Up to 4 strings are supported.

> [Deep thinking capability models](https://docs.byteplus.com/en/docs/ModelArk/1330310) do not support this field.

**frequency_penalty** float `Example value: 1.0`

Value range: [\-2.0, 2.0]. Frequency penalty coefficient. If the value is positive, new tokens will be penalized based on their frequency of occurrence in the text, reducing the possibility of the model repeating word for word.

**presence_penalty** float `Example value: 1.0`

Value range: [\-2.0, 2.0]. Presence penalty coefficient. If the value is positive, new tokens will be penalized based on whether they have appeared in the text so far, increasing the possibility of the model talking about new topics.

**temperature** float `Example value: 1`

Value range: [0, 2]. Sampling temperature. Controls the degree of smoothing applied to the probability distribution of each candidate word during text generation. When the value is 0, the model only considers the token with the maximum log probability. Higher values (e.g., 0.8) make the output more random, while lower values (e.g., 0.2) make the output more focused and deterministic. It is generally recommended to adjust only one of `temperature` or `top_p`, not both.

**top_p** float `Example value: 0.5`

Value range: [0, 1]. Nucleus sampling probability threshold. The model considers token results whose probability mass falls within `top_p`. When the value is 0, the model only considers the token with the maximum log probability. A value of 0.1 means only the top 10% of tokens with the highest probability mass are considered. The larger the value, the higher the randomness of generation; the lower the value, the higher the determinism of generation. It is generally recommended to adjust only one of `temperature` or `top_p`, not both.

**thinking** request_thinking

Controls whether the model enables deep thinking mode. Deep thinking mode is enabled by default and can be manually turned off. For the usage of this field, refer to the `thinking` parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384).

**tools** list of chat_tool

List of tools to be called, which can be included in the model's return information. You need to configure this structure when you want the model to return tools to be called. For the usage of this field, refer to the `tools` parameter in the request body of [Chat API](https://docs.byteplus.com/en/docs/ModelArk/1494384).

**tool_choice** string or object

> Only seed\-1\-6\-\*\*\* and later generation models support this field.

> Specifies whether the model's return information for this request contains tools to be called. When no tools are specified, `none` is the default value. If tools exist, `auto` is the default value.

> **Tool selection mode (string)**

> **Tool call (object)**

* `none`: The model's return information must not contain tools to be called.

* `required`: The model's return information must contain tools to be called. When selecting this option, please confirm that suitable tools exist to reduce model hallucinations.

* `auto`: The model independently determines whether to include tools to be called in the return information.

* Specifies the scope of tools to be called. Only the following model information is allowed in the model's return information. When selecting this option, please confirm that the tool meets user needs to reduce model hallucinations. `tool_choice.name` specifies the name of the tool to be called, and `tool_choice.type` specifies the call type.

### Response Data

**id** string `Example value: 0217426318107460cfa43dc3f3683b1de1c09624ff49085a457ac`

Unique identifier of this request.

**model** string

Name and version of the model actually used for this request.

**created** integer

Unix timestamp (in seconds) when this request was created.

**object** string `Example value: chat.completion`

Fixed as `chat.completion`.

**choices** list of choice

Model output content for this request.

**index** integer `Example value: 0`

Index of the current element in the choices list.

**finish_reason** string `Example value: stop`

Reason why the model stopped generating tokens. Value range:

* `stop`: The model output ends naturally, or is truncated because it hits the field specified in the request parameter `stop`.

* `length`: The model output is truncated because it reaches the model output limit, for the following reasons:

* The `max_tokens` limit is triggered (length limit of response content).

* The `max_completion_tokens` limit is triggered (length limit of chain\-of\-thought content + response content)

* The `context_window` limit is triggered (length limit of input content + chain\-of\-thought content + response content).

* `content_filter`: The model output is intercepted by content moderation.

* `tool_calls`: The model has called tools.

**message** message

Content output by the model.

**role** string `Example value: assistant`

Role of the content output, fixed as `assistant` here.

**content** string

Message content generated by the model.

**reasoning_content** string

Chain\-of\-thought content of the model processing the problem. Only deep reasoning models support returning this field.

**tool_calls** list of tool_call

Tool calls generated by the model.

**id** string `Example value: assistant`

Role of the content output, fixed as `assistant` here.

**type** string `Example value: function`

Tool type, currently only `function` is supported.

**function** function `Example value: function`

Function called by the model.

**name** string

Name of the function called by the model.

**arguments** string

Parameters generated by the model for calling the function, in JSON format.

The model does not always generate valid JSON, and may hallucinate parameters not defined in your function parameter specifications. Please validate these parameters in your code before calling the function.

**logprobs** logprobs

Log probability information of the current content.

**content** list of lpb_content

Log probability information of tokens in each content element in the message list.

**token** string

Current token.

**bytes** list of integer

UTF\-8 value of the current token, in the format of an integer list. It can be used for encoding and decoding characters when a character consists of multiple tokens (such as emojis or special characters). It is empty if the token has no UTF\-8 value.

**logprob** float

Log probability of the current token.

**top_logprobs** list of top_logprobs

List of the most likely tokens and their log probabilities at the current token position. In some cases, the number returned may be less than the number specified by the request parameter `top_logprobs`.

**token** string

Current token.

**bytes** list of integer

UTF\-8 value of the current token, in the format of an integer list. It can be used for encoding and decoding characters when a character consists of multiple tokens (such as emojis or special characters). It is empty if the token has no UTF\-8 value.

**logprob** float

Log probability of the current token.

**moderation_hit_type** string

When the text output by the model contains sensitive information, the risk classification tag hit by the model output text will be returned. Return values and meanings:

* `severe_violation`: The text output by the model involves serious violations.

* `violence`: The text output by the model involves radical behavior.

**usage** usage

Token usage for this request.

**total_tokens** integer `Example value: 10000`

Total number of tokens consumed for this request (input + output).

**prompt_tokens** integer `Example value: 1000`

Number of tokens in the content input to the model for processing.

**prompt_tokens_details** prompt_tokens_details

Details of the number of tokens in the content input to the model for processing.

**cached_tokens** integer `Example value: 100`

Token usage of cached input content.

**audio_tokens** integer `Example value: 100`

Token usage of audio input content.

**audio_cached_tokens** integer `Example value: 100`

Token usage of audio cached input content.

**completion_tokens** integer `Example value: 9000`

Tokens consumed by the model's output content.

**completion_tokens_details** completion_tokens_details

Details of tokens consumed by the model's output content.

**reasoning_tokens** integer `Example value: 200`

Number of tokens consumed by the output chain\-of\-thought content.

### Examples

#### Request Example

```BASH
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/chat/completions" \
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
                        "url": "https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/online/operator_cards/0.1.0/video_keyframes/sample.mp4"
                    }
                },
                {
                    "type": "text",
                    "text": "What is in the video"
                }
            ]
        }
    ],
    "model": "seed-2-0-pro-260328"
}'
```

#### Response Example

```JSON
{
  "model": "seed-2-0-pro-260328",
  "usage": {
    "prompt_tokens": 3877,
    "completion_tokens": 493,
    "total_tokens": 4370,
    "prompt_tokens_details": {
      "cached_tokens": 0,
      "audio_tokens": null,
      "audio_cached_tokens": null
    },
    "completion_tokens_details": {
      "reasoning_tokens": 354,
      "provisioned_tokens": null
    }
  },
  "created": 1772692173,
  "id": "0217726921599114f28f9638b6effb5ab036b3eddba1d5642ea3d",
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "logprobs": null,
      "message": {
        "content": "The video shows a pleasant outdoor scene by the sea:\n1. Core content: A lady wearing a light beige wide-brimmed hat and black sunglasses, dressed in a white top and a printed colorful skirt, leans against the corner of a white building, sits on a folding chair and plays the accordion. She hums along while playing, looking very relaxed. A bottle of drinking water is placed at her feet, with the blue sea and the low shoreline in the distance as the background.\n2. Screen changes: During the video, the camera gradually zooms in on the lady, allowing viewers to see the details of her performance and her expression more and more clearly; in the second half of the video, a passerby wearing a green short-sleeved shirt and light-colored long pants passes by her.\nThe overall atmosphere is leisurely, full of the relaxed vibe of a coastal area.",
        "reasoning_content": "\nThe user now needs to describe the content in the video, right? First, sort out the scene: it is outdoors by the sea, with a corner of a white building, right? Then the protagonist is a lady wearing a light-colored wide-brimmed hat, white top, floral skirt, and sunglasses, sitting on a folding chair, playing the accordion, with a bottle of water on the ground next to her, and the sea and distant shore in the background. During the process, she sings while playing, and the camera slowly zooms in on her, right? Then passersby pass by later, such as a person wearing a green short-sleeved shirt and light-colored pants walking by, and other passersby? Oh right, the overall atmosphere is very leisurely, like a street performance by the sea, right?\nWait, sort it out clearly:\nFirst, the overall scene: This is outdoors by the sea, near the corner of a white building, the ground is stone, the background shows the blue sea and low distant land, and the weather is sunny.\nThen the core character: A lady sits on a black folding chair, wearing a light beige wide-brimmed hat, black sunglasses, a white top, a colorful skirt with floral patterns, and black sandals on her feet. She is playing the accordion, humming along while playing, and is in a very relaxed and leisurely state. A bottle of transparent drinking water is placed at her feet, and there is a black case like an accordion case next to her.\nThen the camera changes: During the video, the camera gradually zooms in on the playing lady, and in the second half, you can clearly see the details of her performance and her expression.\nFinally, there are small details: In the second half of the video, passersby walk past the building next to her, such as a lady wearing a mint green short-sleeved shirt and light khaki long pants passing by.\nThe whole atmosphere is very leisurely, full of the comfortable feeling of a seaside town.\nYes, that's clear enough.",
        "role": "assistant"
      }
    }
  ],
  "object": "chat.completion"
}
```

### Error Codes

|HTTP Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |The model name is invalid |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.Invalid |The api key is invalid. |The API key is invalid |

## Responses

### API Description

Call the seed\-2.0 model through the Responses interface for multimodal understanding. Refer to [Response API](https://docs.byteplus.com/en/docs/ModelArk/Create_model_request) for interface definition.

Supported models and versions: `seed-2-0-pro-260328`.

### Examples

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
                    "video_url":  "https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/online/operator_cards/0.1.0/video_keyframes/sample.mp4"
                },
                {
                    "type": "input_text",
                    "text": "What is in the video"
                }
            ]
        }
    ],
    "model": "seed-2-0-pro-260328"
}'
```

#### Response Example

```JSON
{
    "created_at": 1772617764,
    "error": null,
    "id": "resp_021772617762470960a4483e1c6480e5dcf931407efe2bda06a32",
    "incomplete_details": null,
    "max_output_tokens": 32768,
    "model": "seed-2-0-pro-260328",
    "object": "response",
    "output": [
        {
            "type": "reasoning",
            "id": "rs_02177261776458300000000000000000000ffffac1504e228c011",
            "summary": [
                {
                    "type": "summary_text",
                    "text": "The user now needs to analyze the video content. First, look at the footage: A woman wearing a light-colored wide-brimmed hat, sunglasses, a white top and a floral dress sits on a folding chair next to a white building, playing the accordion while singing. The background is the seaside, with blue waters and distant land. There are other elements in the video: there is a water bottle next to her, and later pedestrians (a person in a green top and khaki pants, and another person) walk past her. The whole scene is at the outdoor seaside, the woman is focused on playing the accordion and singing, with movements including pressing the keys of the accordion, pushing and pulling the bellows, and swinging her head along with the music. Now organize these elements and describe them clearly."
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
                    "text": "The content presented in the video is as follows:\n1. Characters and behaviors: A woman wearing a light-colored wide-brimmed sun hat, sunglasses, a white top and a long floral-patterned skirt sits on a folding chair next to a white building, playing the accordion (pressing the keys with her hands, pushing and pulling the bellows) while singing, and her head also moves to the rhythm of the music; later, two pedestrians (one in a lake green top and khaki bottoms, one in a white top) walk past her.\n2. Environment and objects: The scene is an outdoor seaside area, with blue waters and distant land covered with green plants visible in the background; a bottle of mineral water is placed on the ground next to the woman, and there is an open box behind her.",
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
          "cached_tokens": 0,
          "audio_tokens": null,
          "audio_cached_tokens": null
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
