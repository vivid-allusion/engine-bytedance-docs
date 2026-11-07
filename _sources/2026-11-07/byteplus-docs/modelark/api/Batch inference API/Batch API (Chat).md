---
title: "Batch API (Chat)"
product: "ModelArk"
product_code: "modelark"
source: "https://docs.byteplus.com/en/docs/modelark/batch-chat-api"
---

`POST https://ark.ap-southeast.bytepluses.com/api/v3/context/chat/completions` [Try](https://api.byteplus.com/api-explorer/?action=BatchChatCompletions&version=2024-01-01)

This topic describes the input and output parameters of the API for calling model services through batch inference, so you can understand parameter meanings when using the API. By using batch inference, you can benefit from higher rate limit quotas and more affordable pricing, making it suitable for large\-scale data processing.

> For the recommended calling method, see [code sample](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/batch-inference#075b8a07).

> **Tip**

* > **The Batch Chat API has been marked for deprecation.** We recommend that you use the [Chat API](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/chat-api) directly and set `service_tier=flex` in the request to complete batch data processing through [Online inference (Flex)](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/online-inference-flex). The API parameters are consistent, so the migration effort is low.

* > For latency\-insensitive workloads involving dynamically generated data, background tasks, or other scenarios that need to keep using synchronous calls, you can migrate to [Online inference (flex)](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/online-inference-flex). After migration, use a provisioned inference endpoint or custom inference endpoint for standard online inference, and set `service_tier=flex` in the request.

* > Online inference (flex) supports the [Chat API](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/chat-api), [Responses API](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/create-model-responses-api), and [Messages API](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/messages-api). Choose the interface to migrate to based on the API protocol currently used by your business and the capabilities you need.

* > **Note: Seed 2.1 and later models no longer support calling the Batch Chat API.**

**Quick access**

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2abecd05ca2779567c6d32f0ddc7874d.png) [Model list](https://ai.byteplus.com/ark/docs/model-list) ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5fdd3028d35cc512a10bd71b982b6eb.png) [Pricing](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-pricing) ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_afbcf38bdec05c05089d5de5c3fd8fc8.png) [API key](https://ai.byteplus.com/ark/region:ap-southeast-1/apiKey) ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bef4bc3de3535ee19d0c5d6c37b0ffdd.png) [Activate model](https://ai.byteplus.com/ark/region:ap-southeast-1/openManagement)

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57d0bca8e0d122ab1191b40101b5df75.png) [Tutorial](https://docs.byteplus.com/en/docs/ModelArk/1399517) ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1609c71a747f84df24be1e6421ce58f0.png) [FAQ](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/modelark-faq)

**Authentication**

This API supports API key and access key authentication. For more information, see [Authentication methods](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/base-url-and-authentication).

**Try Now**

[去调试](https://api.byteplus.com/api-explorer/?action=BatchChatCompletions&data=%7B%7D&groupName=%E6%89%B9%E9%87%8F%E6%8E%A8%E7%90%86&query=%7B%7D&serviceCode=ark&version=2024-01-01)

---

## Request parameters

> Go to [Response parameters](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/batch-chat-api#PM1q4ttH)

### Request body

---

**model** `string` `Required`

Call the model by using the endpoint ID. For more information, see [Get endpoint ID](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/online-inference-standard).

---

**messages** `object[]` `Required`

A list of messages that make up the conversation so far. Different models support different types of messages, such as text, image, video, etc.

Message type \-\-\- \*\*System message\*\* `object` Instructions provided by developers. The model should follow these instructions. For example, the role or goal that the model should play.
Attributes \-\-\- messages.\*\*role\*\* `string` `Required` Role of the message sender. In this case, set it to `system`. \-\-\- messages.\*\*content\*\* `string / object[]` `Required` System message content.
Attributes \-\-\- \*\*Plain text message content\*\* `string` Plain text message content. Large language models support this type. \-\-\- \*\*Multimodal message content\*\* `object[]` Text, image, video, and other types are supported. Multimodal models such as visual understanding models, and some large language models support this parameter.
Message parts for each modality \-\-\- \*\*Text message\*\* `object` In a multimodal message, this is the text content input. [Models with visual understanding capabilities](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/model\-list#76df97c8){target="_self"}, and some large language models support this message type.
Attributes \-\-\- messages.content.\*\*text\*\* `string` `Required` Content of the text message. \-\-\- messages.content.\*\*type\*\* `string` `Required` Text message type. In this case, set it to `text`.

---

**Image message** `object`

In a multimodal message, this is the image content part. [Models with visual understanding capabilities](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-list#76df97c8) support this message type.

Attributes \-\-\- messages.content.\*\*image_url\*\* `object` `Required` Content of the image message.
Attributes \-\-\- messages.content.image_url.\*\*url \*\* `string` `Required` The parameter supports an image URL or a Base64\-encoded image. For instructions, see [Instructions](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/image\-understanding#7a123cd1){target="_self"}. \-\-\- messages.content.image_url.\*\*detail\*\* `string` `Default value: auto` You can manually set the image quality. Valid values are `high`, `low`, and `auto`. \* `high`: High\-detail mode. It is suitable for scenarios that require understanding image details, such as extracting multiple local details or features from an image and understanding complex images or images with rich details. It provides more comprehensive understanding. \* `low`: Low\-detail mode. It is suitable for simple image classification or recognition, and overall content understanding or description. It provides faster understanding. \* `auto`: Default mode. The mode selected varies slightly by model. For details, see [Depth control for image understanding](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/image\-understanding#bf4d9224){target="_self"}.

---

messages.content.**type** `string` `Required`

Image message type. In this case, set it to `image_url`.

---

**Video message**

> For video understanding models, see [Video understanding](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-list#76df97c8).

> In a multimodal message, this is the video content part.

Attributes \-\-\- messages.content.\*\*type\*\* `string` `Required` Video message type. In this case, set it to `video_url`. \-\-\- messages.content.\*\*video_url\*\* `object` `Required` Content of the video message.
Attributes \-\-\- messages.content.video_url.\*\*url \*\* `string` `Required` You can pass a video URL or a Base64\-encoded video. For specific usage, see [Video understanding](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/video\-understanding){target="_self"}. \-\-\- messages.content.video_url.\*\*fps\*\* `float/ null` `Default value: 1` Value range: `[0.2, 5]`. The number of frames to be extracted from the video per second. The higher the value, the more sensitive it is to frame changes in the video. The lower the value, the less sensitive it is to frame changes in the video, but it consumes fewer tokens and runs faster. For details, see [Usage notes](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/image\-understanding#57188ace){target="_self"}.

---

**User message** `object`

A message sent by the user, including prompts or additional context information. Different models support different parameter types. At most, text, image, and video messages are supported.

Attributes \-\-\- messages.\*\*role\*\* `string` `Required` Role of the message sender. In this case, set it to `user`. \-\-\- messages.\*\*content\*\* `string / object[]` `Required` Content of the user message.
Content type \-\-\- \*\*Plain text message content\*\* `string` Plain text message content. Large language models support this type. \-\-\- \*\*Multimodal message content\*\* `object[]` Text, image, video, and other types are supported. Multimodal models such as visual understanding models, and some large language models support this parameter.
Content type \-\-\- \*\*Text message\*\* `object` In a multimodal message, this is the text content input. Vision understanding models and some large language models support this type of message.
Attributes \-\-\- messages.content.\*\*text\*\* `string` `Required` Content of the text message. \-\-\- messages.content.\*\*type\*\* `string` `Required` Text message type. In this case, set it to `text`.

---

**Image message** `object`

In a multimodal message, this is the image content part. Vision understanding models support this type of message.

\*\*Attributes\*\* \-\-\- messages.content.\*\*type\*\* `string` `Required` Image message type. In this case, set it to `image_url`. \-\-\- messages.content.\*\*image_url\*\* `object` `Required` Content of the image message.
\*\*Attributes\*\* \-\-\- messages.content.image_url.\*\*url \*\* `string` `Required` You can pass an image URL or a Base64\-encoded image. Supported image sizes vary slightly by model. For details, see [Instructions](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/image\-understanding#7a123cd1){target="_self"}. \-\-\- messages.content.image_url.\*\*detail\*\* `string / null` `Default value: low` Valid values: `high`, `low`, `auto`. You can manually set the image quality. \* `high`: High\-detail mode. It is suitable for scenarios that require understanding image details, such as extracting multiple local details or features from an image and understanding complex images or images with rich details. It provides more comprehensive understanding. In this case, \*\*min_pixels\*\* is `3136` and \*\*max_pixels\*\* is `4014080`. \* `low`: Low\-detail mode. It is suitable for simple image classification or recognition, and overall content understanding or description. It provides faster understanding. In this case, \*\*min_pixels\*\* is `3136` and \*\*max_pixels\*\* is `1048576`. \* `auto`: Default mode. The mode selected varies slightly by model. For details, see [Depth control for image understanding](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/image\-understanding#bf4d9224){target="_self"}. \-\-\- messages.content.image_url.\*\*image_pixel_limit\*\* `object / null` `Default value null` You can set image pixel count limits. If an image is outside this range, it will be scaled up or down proportionally to fit within the range. Priority: It has higher priority than \*\*detail\*\*. That is, when both \*\*detail\*\* and \*\*image_pixel_limit\*\* are configured, \*\*image_pixel_limit\*\* takes effect. If the \*\*min_pixels\*\* / \*\*max_pixels\*\* parameters are not set, the corresponding \*\*min_pixels\*\* / \*\*max_pixels\*\* values configured by \*\*detail\*\* are used. Subparameter value logic: `3136` ≤ \*\*min_pixels\*\* ≤ \*\*max_pixels\*\* ≤ `4014080` \-\-\- \* messages.content.image_url.image_pixel_limit.\*\*max_pixels\*\* `integer` Value range: (\*\*min_pixels\*\*, `4014080`]. Maximum pixel limit for uploaded images. If the image pixel count exceeds this value, it will be scaled down proportionally to below the value of the \*\*max_pixels\*\*. If not set, the value will be the \*\*max_pixels\*\* value corresponding to the configured \*\*detail\*\* value. \-\-\- \* messages.content.image_url.image_pixel_limit.\*\*min_pixels\*\* Value range: [`3136`, \*\*max_pixels\*\*). Minimum pixel limit for uploaded images. If the image pixel count is lower than this value, it will be scaled up proportionally to above the value of the \*\*min_pixels\*\*. If not set, the value will be the \*\*min_pixels\*\* value (`3136`) corresponding to the configured \*\*detail\*\* value.

---

**Video message** `object`

> For video understanding models, see [Video understanding](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-list#76df97c8).

> In a multimodal message, this is the video content part.

Attributes \-\-\- messages.content.\*\*type\*\* `string` `Required` Video message type. In this case, set it to `video_url`. \-\-\- messages.content.\*\*video_url\*\* `object` `Required` Content of the video message.
Attributes \-\-\- messages.content.video_url.\*\*url \*\* `string` `Required` You can pass a video URL or a Base64\-encoded video. For specific usage, see [Video understanding](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/video\-understanding){target="_self"}. \-\-\- messages.content.video_url.\*\*fps\*\* `float/ null` `Default value: 1` Value range: `[0.2, 5]`. The number of frames to be extracted from the video per second. The higher the value, the more sensitive it is to frame changes in the video. The lower the value, the less sensitive it is to frame changes in the video, but it consumes fewer tokens and runs faster. For details, see [Usage notes](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/image\-understanding#57188ace){target="_self"}.

---

**Model message** `object`

Messages returned by the model in historical conversations. This is often used to pass historical conversation records in multi\-turn conversations, or to let the model continue from preset response content when using [Prefill response](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/continuation-mode).

Attributes

> **Tip**

> You must specify at least one of messages.**content** and messages.**tool_calls**.

---

## messages.**role** `string` `Required`

## Role of the message sender. In this case, set it to `assistant`.

## messages.**content** `string / array`

## The message returned by the model.

messages.**tool_calls** `object[]`

Tool call information returned by the model in historical conversations.

Show subparameters \-\-\- messages.tool_calls.\*\*function\*\* `object` `Required` Information about the function corresponding to the tool called by the model.
Show subparameters \-\-\- messages.tool_calls.function.\*\*name\*\* `string` `Required` Name of the function called by the model. \-\-\- messages.tool_calls.function.\*\*arguments\*\* `string` `Required` Parameters generated by the model for calling the function in JSON format.

> **Tip**

> The model does not always generate valid JSON, and may fabricate some parameters that are not defined in your function parameter specifications. Before calling the function, please verify the validity of these parameters in your code.

---

## messages.tool_calls.**id** `string` `Required`

## ID of the called tool.

messages.tool_calls.**type** `string` `Required`

Tool type. Currently only `function` is supported.

---

**thinking** `object` `Default value: {"type":"enabled"}`

Whether deep reasoning is enabled for the model. Deep reasoning is enabled by default, but you can manually disable it.

> For models that support this parameter and usage examples, see [the documentation](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/deep-thinking#fa3f44fa).

Attributes \-\-\- thinking.\*\*type\*\* `string` `Required` Value range: \* `enabled`: Enables reasoning mode. The model always reasons before answering. \* `disabled`: Disables reasoning mode. The model answers the question directly without reasoning.

---

**max_tokens** `integer / null` `Default value: 4096`

The maximum length of the model response, in tokens. The value range varies by model. For details, see [Model list](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-list).

The total length of input and output tokens is also limited by the model's context length.

---

**max_completion_tokens** `integer / null`

> Model that supports this parameter: `deepseek-r1-250528`.

Value range: `[0, 64k]`.

For usage examples, see [the documentation](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/deep-thinking#cfc7c5a8). Controls the maximum length of the model's output (including the length of the model's answer and model chain\-of\-thought content, unit: token). After this parameter is configured, the model can output very long content. **max_tokens** (default value: 4k) and the maximum chain\-of\-thought length no longer take effect. The model outputs content as needed until it reaches the value configured for **max_completion_tokens**.

Cannot be set while **max_tokens** parameter is set, or an error will be reported.

---

**stop** `string / string[] / null` `Default value: null`

When the model encounters the string specified by the stop parameter, it will stop generating further content, and the string itself will not be output.

* By default, up to `4` stop words are supported.

* `deepseek-v4-pro-ga-260813` and `deepseek-v4-flash-ga-260731` support up to `16` stop words.

> [Deep reasoning models](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-list#32e9e053) do not support this parameter by default, except for DeepSeek V4 models mentioned above.

Example: `["hello", "weather"]`

---

**frequency_penalty** `float / null` `Default value: 0`

Value range: [\-2.0, 2.0].

Frequency penalty coefficient. If the value is positive, new tokens are penalized based on their frequency of occurrence in the text, reducing the possibility of the model repeating word for word.

---

**presence_penalty** `float / null` `Default value: 0`

Value range: [\-2.0, 2.0].

Presence penalty coefficient. If the value is positive, new tokens are penalized based on whether they have appeared in the text so far, increasing the possibility of the model discussing new topics.

---

**temperature** `float / null` `Default value: 1`

Value range: [0, 2].

Sampling temperature. Controls the degree of smoothing applied to the probability distribution of each candidate word when generating text. When the value is 0, the model only considers the token with the highest log probability.

Higher values (e.g., 0.8) make the output more random, while lower values (e.g., 0.2) make the output more focused and deterministic.

It is generally recommended to adjust either temperature or top_p, while modifying both is not advised.

---

**top_p** `float / null` `Default value: 0.7`

Value range: [0, 1].

Nucleus sampling probability threshold. The model considers token results whose cumulative probability mass falls within the top_p threshold. When the value is 0, the model only considers the token with the highest log probability.

A value of 0.1 means only the top 10% of tokens with the highest probability mass are considered. The higher the value, the higher the randomness of generation; the lower the value, the higher the determinism of generation. It is generally recommended to adjust either temperature or top_p, while modifying both is not advised.

---

**logprobs** `boolean / null` `Default value: false`

Whether to return the log probabilities of output tokens.

* `false`: Does not return log probability information.

* `true`: Returns the log probability of each output token in the message content.

---

**top_logprobs** `integer / null` `Default value: 0`

Value range: [0, 20].

Specifies the most probable number of tokens to return for each output token position, each with an associated log probability. The **top_logprobs** parameter can only be set when **logprobs** is `true`.

---

**logit_bias** `map / null` `Default value: null`

Adjusts the probability of specified tokens appearing in the model's output, making the generated content better align with specific preferences. The **logit_bias** parameter accepts a map value, where each key is a token ID in the vocabulary (obtained via the tokenization interface), and each value is the bias for that token, with a value range of [\-100, 100].

A value of \-1 reduces the probability of the token being selected, while a value of 1 increases the selection probability; \-100 completely bans the selection of this token, and 100 forces only this token to be selected. The actual effect of this parameter may vary by model.

`{"<Token_ID>": -100}`

---

**tools** `object[] / null` `Default value: null`

List of tools available for calling, which may be included in the model's response. This structure needs to be configured when you require the model to return tools to be called. For models that support this parameter, see [Tool use](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/model-list#f44ceef7).

Attributes \-\-\- tools.\*\*type\*\* `string` `Required` Type of the tool. In this case, set it to `function`. \-\-\- tools.\*\*function\*\* `object` `Required` The model's response may include tools to be called.
Attributes \-\-\- tools.function.\*\*name\*\* `string` `Required` Name of the called function. \-\-\- tools.function.\*\*description\*\* `string` Description of the function to be called. The LLM uses it to determine whether to call this function. \-\-\- tools.function.\*\*parameters\*\* `object` Function request parameters, described in JSON Schema format. For the specific format, see the [JSON Schema](https://json\-schema.org/understanding\-json\-schema) documentation. The format is as follows: ```json { "type": "object", "properties": { "location": { "type": "string", "description": "City name, e.g. Beijing" } }, "required": ["location"] } ``` Where: \* All parameter names are case\-sensitive. \* \*\*parameters\*\* must be a valid JSON Schema object. \* We recommend using English parameter names and putting other languages in the \*\*description\*\* parameter.

---

## Response parameters

> Go to [Request parameters](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/batch-chat-api#B2fc2CRV)

### Non\-streaming output

---

**id** `string`

Unique identifier of the request.

---

**model** `string`

The name and version of the model actually used for this request.

---

**service_tier** `string`

Whether this request used a TPM guarantee package.

* `default`: This request did not use the TPM guarantee package quota.

---

**created** `integer`

Unix timestamp (in seconds) of the request creation time.

---

**object** `string`

Fixed as `chat.completion`.

---

**choices** `object[]`

Model output content of this request.

Attributes \-\-\- choices.\*\*index\*\* `integer` The index of the current element in the \*\*choices\*\* list. \-\-\- choices.\*\*finish_reason\*\* `string` The reason why the model stopped generating tokens. Value range: \* `stop`: The model output ends naturally, or is truncated because it hits the parameter specified in the request parameter stop. \* `length`: The model output is truncated because it reaches the model output limit, for the following reasons: \* The `max_token` limit is triggered (length limit of the answer content). \* \* The `max_completion_tokens` limit is triggered (length limit of chain\-of\-thought content + answer content). \* \* The `context_window` limit is triggered (length limit of input content + chain\-of\-thought content + answer content). \* `content_filter`: The model output is intercepted by content moderation. \* `tool_calls`: The model called tools. \-\-\- choices.\*\*message\*\* `object` Content output by the model.
Attributes \-\-\- choices.message.\*\*role\*\* `string` Role of the output information. It is always `assistant`. \-\-\- choices.message.\*\*content\*\* `string` Message content generated by the model. \-\-\- choices.message.\*\*reasoning_content\*\* `string / null` Chain\-of\-thought content of the model processing the problem. Only deep reasoning models support returning this parameter. For deep reasoning models, see [Pass encrypted thinking content back](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/deep\-thinking#8cfd447b){target="_self"}. In batch inference scenarios, for models that have thinking summary enabled by default, this parameter (thinking content summary) is not returned; only the answer content is returned. \-\-\- choices.message.\*\*tool_calls\*\* `object[] / null` Tool calls generated by the model.
Attributes \-\-\- choices.message.tool_calls.\*\*id\*\* `string` ID of the called tool. \-\-\- choices.message.tool_calls.\*\*type\*\* `string` Tool type. Currently only `function` is supported. \-\-\- choices.message.tool_calls.\*\*function\*\* `object` The function called by the model.
Attributes \-\-\- choices.message.tool_calls.function.\*\*name\*\* `string` Name of the called function. \-\-\- choices.message.tool_calls.function.\*\*arguments\*\* `string` Parameters generated by the model for calling the function in JSON format. The model does not always generate valid JSON, and may fabricate some parameters that are not defined in your function parameter specifications. Before calling the function, please verify the validity of these parameters in your code.

---

choices.**logprobs** `object / null`

Log probability information of the current content.

Attributes \-\-\- choices.logprobs.\*\*content\*\* `object[] / null` Log probability information of tokens in each content element in the message list.
Attributes \-\-\- choices.logprobs.content.\*\*token\*\* `string` Current token. \-\-\- choices.logprobs.content.\*\*bytes\*\* `integer[] / null` UTF\-8 value of the current token, in the format of an integer list. It can be used for character encoding and decoding when a character consists of multiple tokens (such as emojis or special characters). It is empty if the token has no UTF\-8 value. \-\-\- choices.logprobs.content.\*\*logprob\*\* `float` Log probability of the current token. \-\-\- choices.logprobs.content.\*\*top_logprobs\*\* `object[]` A list of the most probable tokens and their log probabilities at the current token position. In some cases, the number of returned results may be less than the number specified by the request parameter top_logprobs.
\*\*Attributes\*\* \-\-\- choices.logprobs.content.top_logprobs.\*\*token\*\* `string` Current token. \-\-\- choices.logprobs.content.top_logprobs.\*\*bytes\*\* `integer[] / null` UTF\-8 value of the current token, in the format of an integer list. It can be used for character encoding and decoding when a character consists of multiple tokens (such as emojis or special characters). It is empty if the token has no UTF\-8 value. \-\-\- choices.logprobs.content.top_logprobs.\*\*logprob\*\* `float` Log probability of the current token.

---

choices.**moderation_hit_type** `string / null`

When the model output text contains sensitive information, the risk classification tag hit by the model output text will be returned.

Return values and meanings:

* `severe_violation`: The model output text involves serious violations.

* `violence`: The model output text involves radical behavior.

   Note: Currently only [visual understanding models](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/image-understanding#f8d6cc48) support returning this parameter. The risk classification tag will only be returned when ModerationStrategy is set to Basic in the [endpoint creation page](https://ai.byteplus.com/ark/region:ap-southeast-1/endpoint/create) of the ModelArk console or the [CreateEndpoint](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/create-endpoint-api) API.

---

**usage** `object`

Token usage of this request.

Attributes \-\-\- usage.\*\*prompt_tokens\*\* `integer` Number of input prompt tokens. \-\-\- usage.\*\*completion_tokens\*\* `integer` Number of tokens generated by the model. \-\-\- usage.\*\*total_tokens\*\* `integer` Total number of tokens consumed by this request (input + output). \-\-\- usage.\*\*prompt_tokens_details\*\* `object` This API does not currently support this parameter. Details about tokens that hit the context cache.
Attributes \-\-\- usage.prompt_tokens_details.\*\*cached_tokens\*\* `integer` This API does not currently support this parameter. This should be `0`.

---

usage.**completion_tokens_details** `object`

Details about the tokens consumed by this request.

Attributes \-\-\- usage.completion_tokens_details.\*\*reasoning_tokens\*\* `integer` Number of tokens consumed by the output chain\-of\-thought content. For models that support chain\-of\-thought output, see [documentation](https://ai.byteplus.com/ark/region:ap\-southeast\-1/docs/deep\-thinking#14b5c6db){target="_self"}.
