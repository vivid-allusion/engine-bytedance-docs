---
title: "Integrate Third-Party Model"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1399966"
---

In real\-time conversational AI scenarios, you can integrate self\-developed or third\-party LLMs and agents, such as a Dify agent, in addition to Volcano Ark and Coze models. This lets you adapt Conversation AI to your specific business requirements.

<span id=".5o6l5YWl5pa55rOV"></span>
# Quick Integration

<span id="ebf0f9f2"></span>
## 1. Prepare the Service API

Prepare an HTTP(S) service endpoint URL that complies with the BytePlus interface standard:


* The endpoint must be accessible over the public network. An HTTPS domain is recommended.

* The endpoint must support streaming responses over SSE and end each response with `data: [DONE]`.

* Requests to this URL time out after 10 seconds. Make sure your service can return a response within this timeout.

* The endpoint must strictly follow [API Standards](https://docs.byteplus.com/en/docs/12/47016#cae507df). Before production integration, use the [validation tool](https://docs.byteplus.com/en/docs/12/47016#validate) to verify that the endpoint meets the requirements.


<span id="ad4b213b"></span>
## 2. Configure StartVoiceChat

Call the `StartVoiceChat` API and configure `LLMConfig` using the required parameter structure. The following example shows the minimum `LLMConfig` configuration:

> To send a simple business identifier, such as `session_id` or `source`, with each request, append it directly to the URL as a query string. For example: `https://api.my-custom-agent.com/v1/chat-stream?session_id=12345`. To send more complex custom data, see [Custom Data Transmission](https://docs.byteplus.com/en/docs/12/47016#f7fdb009).


```JSON
{
    "Config": {
        "LLMConfig": {
            "Mode": "CustomLLM",
            "Url": "https://api.my-custom-agent.com/v1/chat-stream",
            "APIKey": "bearer-token-for-my-agent"
        }
    }
}
```


`Mode` is required and must be set to `CustomLLM`. `Url` is required and must be the address of your service endpoint. `APIKey` is optional and is used as the authentication token.

<span id="66be64f3"></span>
# Advanced Configuration

<span id="47c17a66"></span>
## Context Management

Use `SystemMessages`, `UserPrompts`, and `HistoryLength` to inject initial context into the conversation and control how many previous conversation turns are retained. For detailed instructions, see [Context (Short-Term Memory)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1511926).

<span id="862f051c"></span>
## Vision and Image Understanding

If your third\-party model supports vision, configure `VisionConfig` to send real\-time video streams or external image data to the LLM. This enables advanced interactions such as visual question answering and environment perception. For configuration and usage details, see [Video and Image Understanding](https://docs.byteplus.com/docs/byteplus-rtc/docs-1408245).

<span id="47d2550e"></span>
## Configure MCP

With MCP (Model Context Protocol), you can encapsulate external services, such as knowledge base Q&A (RAG), online search, and business API calls, as standardized tools. The LLM can invoke these tools during a conversation to retrieve data or perform actions, and then generate more accurate and professional responses based on the returned results. For implementation details, see [Integrate MCP](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856160).

<span id="d65c3fb5"></span>
## Function Calling

Function calling allows large models to identify user intent and invoke external functions for specific tasks, such as checking the weather, querying order status, retrieving stock information, or obtaining other real\-time data. For implementation details, see [Function calling](https://docs.byteplus.com/docs/byteplus-rtc/docs-1554654).

<span id="2d8e3307"></span>
## Parameter Concatenation

To send non\-sensitive business information, such as `session_id`, with each request, append it directly to `LLMConfig.Url` as a query parameter.


* Format: `https://<third-party model or agent API address>?<custom business parameter name>=<parameter value>`.

* Example: `https://api.my-custom-agent.com/v1/chat-stream?session_id=12345`.


<span id="f7fdb009"></span>
## Custom Data Transmission

<span id="method-1-pass-through-global-configuration"></span>
### Method 1: Pass Through Global Configuration

To send fixed parameters, such as user tags or a business ID, throughout the entire agent task lifecycle, pass them through the following `LLMConfig` fields when calling `StartVoiceChat`:


* `Custom`: A custom JSON string that is passed through to the `custom` field in the LLM request body.

* `ExtraHeader`: A JSON object whose key\-value pairs are passed through as additional HTTP headers in the LLM request.


```JSON
{ 
  "Config": {
        "LLMConfig": {
            "Mode": "CustomLLM",
            "Url": "https://api.example.com/chat", 
            "Custom": "{\"user_level\": \"vip\", \"biz_id\": \"order_123\"}",
            "ExtraHeader": {
                "X-Custom-Source": "mobile_app",
                "X-Client-Version": "1.0.0"
            }
        }
    }
}
```


<span id="method-2-dynamically-pass-through-data-from-the-client"></span>
### Method 2: Dynamically Pass Through Data from the Client

You can send custom data from the client, such as business data or algorithm detection results. The data is cached and passed through to the third\-party LLM as response context in the HTTP request for the next conversation turn. Sending this data does not immediately trigger a request, and the data is not read aloud directly by TTS.

This feature is suitable for scenarios where the client and LLM need to exchange real\-time business data. For example:


* **Game interaction**: The client sends the player's real\-time status, such as health points or location, to the LLM. The LLM returns an appropriate game strategy or dialogue based on the status, and the returned data can trigger specific game events on the client.

* **Emotion synchronization**: The client detects the user's emotion through a camera or sensor and sends a status such as `happy` or `sad` to the LLM. While generating a response, the LLM can return an instruction that tells the client's avatar to display the corresponding expression.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature does not support proactive delivery of business data from the LLM unless the client has requested it. If you only add the <code>X-Biz-Trace-Info</code> field to the LLM response unilaterally, unexpected results might occur. If you only need the LLM to proactively send a simple text instruction to the client, use <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1350596#.6L-H5ruk57uG6IqC5L-h5oGv">Filter Non\-Dialogue Content</a>.</div>



1. **Send data from the client.** 

   On the client, call the RTC SDK API [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage) to send custom data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data sent by the client is not pushed to the LLM service immediately. The data is cached and passed through in the HTTP request body when the next conversation request occurs.   </div>
   

   * `userId`: The AI user ID, which is `AgentConfig.UserId` configured in `StartVoiceChat`.

   * `buffer`: The buffer must use the following TLV binary format:

      
      |Field |Type |Description |
      |---|---|---|
      |magic_number |Binary |Message format identifier. The fixed value is `trac`. |
      |length |Binary |Byte length of `trace_data`, in bytes. The value is stored in big\-endian byte order. |
      |trace_data |Binary |Custom data to pass through, in JSON format. |
      

      trace_data

&nbsp;

      
      |Field |Type |Required |Description |
      |---|---|---|---|
      |EnableModules |JSONMap |Yes |Specifies the AI services that receive the custom data. The key is the module name, and the value is a Boolean value that specifies whether data pass\-through is enabled for the module.<br><br><br>* For LLM pass\-through, use `"EnableModules": { "llm": true }`.<br><br>* For TTS pass\-through, use `"EnableModules": { "tts": true }`. |
      |X\-Biz\-Trace\-Info |String |Yes |Custom business data. The value must be Base64\-encoded. |
      

2. **Receive returned data on the client.** 

   When ASR recognizes user speech and triggers the next LLM request, the system puts the cached custom data in the `X-Biz-Trace-Info` field of the HTTP request body and forwards it to your LLM service. You can return this field in the response. The system broadcasts it to the client as a `trac` message. On the client, listen for the RTC SDK callback [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived-2) to receive data returned from the LLM.

   For message format and parsing method, refer to the parsing example in [Real-time subtitles (conversation records)](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1337284). Change the magic number check to `trac` to obtain the latest business data.


<span id="cae507df"></span>
# API Standards

During a conversation, the system sends a POST request to the endpoint of your configured third\-party LLM or agent in the following format to obtain the model response. The API response must support SSE.

<span id="request"></span>
## Request


* **Method**: POST

* **Headers**:

   * Content\-Type: application/json

   * Authorization: Bearer <your_APIKey\> (when the LLM requires Bearer Token authentication)

* **Request body**:

&nbsp;

   
   |Parameter |Type |Required |Description |
   |---|---|---|---|
   |**messages** |Object[] |Yes |The latest conversation turns. The maximum number of turns is defined by `StartVoiceChat.HistoryLength`. The current ASR result is appended to the end of the array. |
   |└ **role** |String |Yes |Possible values are `user` or `assistant`. |
   |└ **content** |String |No |Conversation content. |
   |**stream** |Boolean |No |Value: `true`. |
   |**temperature** |Float |No |The value from `StartVoiceChat.LLMConfig.temperature`. |
   |**max_tokens** |Int |No |The value from `StartVoiceChat.LLMConfig.MaxTokens`. |
   |**model** |String |Yes |The value from `StartVoiceChat.LLMConfig.ModelName`. |
   |**top_p** |Float |No |The value from `StartVoiceChat.LLMConfig.TopP`. |
   |**custom** |String |No |The value from `StartVoiceChat.LLMConfig.Custom`. |
   |**parallel_tool_calls** |Boolean |No |The value from `StartVoiceChat.LLMConfig.EnableParallelToolCalls`. |
   |**X\-Biz\-Trace\-Info** |String |No |Custom data passed from the client. This field is included only when the client sends data. The content is a Base64\-encoded JSON string. |
   


<span id="response"></span>
## Response

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Protocol</strong>: The response must support SSE (Server\-Sent Events).</div>


* <div data-tips="true" data-tips-type="warning"><strong>Headers</strong>: Content\-Type must be text/event\-stream.</div>


* <div data-tips="true" data-tips-type="warning"><strong>End marker</strong>: The response must include the <code>data: [DONE]</code> end marker to indicate that the model has finished the current response.</div>



<span id="statuscode-200"></span>
### StatusCode==200

&nbsp;


|Parameter |Type |Required |Description |
|---|---|---|---|
|**id** |String |Yes |Request UUID. The ID must remain the same within one streaming request. |
|**object** |String |Yes |Fixed value: `chat.completion.chunk`. |
|**created** |Integer |Yes |Unix timestamp (seconds). |
|**model** |String |Yes |Model name. |
|**choices** |Object[] |Yes |Array of streaming fragments. |
|└ **index** |Integer |Yes |Fragment index, starting from 0. |
|└ **finish_reason** |String |No |Completion status. The value is `null` while generation is in progress, and `stop`, `length`, or another completion reason when generation finishes. |
|└ **delta** |Object |Yes |Content delta object. |
|└─ **role** |String |No |Fixed as `assistant`. |
|└─ **content** |String |No |AI\-generated text fragment. |
|**usage** |Object |No |Token usage statistics. It is recommended to return this field in the last packet. |
|└ **prompt_tokens** |Integer |No |Number of input tokens. |
|└ **completion_tokens** |Integer |No |Number of output tokens. |
|└ **total_tokens** |Integer |Yes |The total number of tokens (prompt + completion). |
|**stream_options** |Object |Yes |Streaming API options. |
|└ **include_usage** |Boolean |Yes |Always `true`, indicating that usage statistics are included in the stream. |
|**X\-Biz\-Trace\-Info** |String |No |Pass\-through custom data, Base64\-encoded. |


Example of a successful request and response:

```bash
curl -v --location 'https://rtc-cloud-rendering.byted.org/voicechat/test-sse' \
--header 'Content-Type: application/json' \
--data '{
    "messages":[{
        "role":"user",
        "content":"What is suitable to do today?"
    }],
    "stream": true,
    "temperature": 0.1,
    "max_tokens": 100,
    "top_p": 0.9,
    "model": "Skylark-32k",
    "stream_options": {"include_usage":true}
}'

> POST /voicechat/test-sse HTTP/1.1
> Host: rtc-cloud-rendering.byted.org
> User-Agent: curl/8.4.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 254
>
< HTTP/1.1 200 OK
< Date: Thu, 15 Aug 2024 09:36:02 GMT
< Content-Type: text/event-stream
< Transfer-Encoding: chunked
< Connection: keep-alive
< Access-Control-Allow-Origin: *
< Cache-Control: no-cache

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"role":"assistant"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":1,"delta":{"content":"It"}},{"finish_reason":null,"index":0,"delta":{"content":"is"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"starting,"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"the"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":1,"delta":{"content":"happy"}},{"finish_reason":null,"index":0,"delta":{"content":"to be a"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"person"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"."}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"Groom horses,"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"Chop wood,"}},{"finish_reason":null,"index":1,"delta":{"content":"Travel"}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":null,"index":0,"delta":{"content":"the world"}},{"finish_reason":null,"index":1,"delta":{"content":"."}}],"model":"Skylark-32k-2024-07-25","created":1723714562}

data: {"id":"c99d67a4-5ae9-11ef-bdf5-b8cef6dcdbe2","object":"chat.completion.chunk","choices":[{"finish_reason":"stop","index":0,"delta":{}}],"model":"Skylark-32k-2024-07-25","created":1723714562,"usage":{"prompt_tokens":1,"completion_tokens":2,"total_tokens":3}}

data: [DONE]
```


<span id="statuscode-4xx、5xx"></span>
### StatusCode==4xx or 5xx

The request is terminated and an error is returned. RTC does not process the response body and only reports the error.

&nbsp;


|Parameter |Type |Required |Description |
|---|---|---|---|
|Error |Object |Yes |Error details. |


Error

&nbsp;


|Parameter |Type |Required |Description |
|---|---|---|---|
|Code |String |Yes |Error code. |
|Message |String |Yes |Error reason. |


**Response example**:

```JSON
{
  "Error": {
    "Code": "AuthenticationError",
    "Message": "The API key or AK/SK in the request is missing or invalid. "
  }
}
```


<span id="statuscode-200、4xx、5xx"></span>
### StatusCode !== 200, 4xx, or 5xx

In this case, RTC does not process the response. It only reports an error and returns the original status code.

<span id="validate"></span>
# Validate the API

Use the validation tool to verify whether the request endpoint of the third\-party LLM or agent complies with the API standards.

> The validation tool only supports Linux and macOS systems.


1. Download and extract the validation toolkit.

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e5da63fd97323952415d0f5161d7e96.zip" name="Archive.zip">Archive.zip</Attachment>
   

2. Run the validation command (Linux/macOS).

   When you use zsh and the URL contains special characters, such as `?`, `=`, or `&`, you must escape those characters.

   ```Bash
   # Syntax: ./app-<os> <API address> <model name> <APIKey> <test question>
   
   # Linux
   ./app-linux <llmAPIUrl> <llmModel> <llmAPIKey> <LLMQuestion>
   
   # macOS
   ./app-mac <llmAPIUrl> <llmModel> <llmAPIKey> <LLMQuestion>
   ```
   


If the validation passes, the output is similar to the following:


* OpenAI

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46d3de0843c5281462b6c7513daf4b50.png) </span>

* Custom URL

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0e2a36d6199b30ba2abd1ef67b09292.png) </span>


<span id="faq"></span>
# FAQ

<span id=".cTHvvJrmmK_lkKbmlK_mjIHlnKjmnKzlnLDnjq_looPosIPnlKjlkozmtYvor5Xpqozor4Hlr7nor53lvI8tYWkt56ys5LiJ5pa55aSn5qih5Z6L5oiWLWFnZW50LeaOpeWPo--8nw=="></span>
## Q1: Can I call or test the third\-party LLM or agent endpoint in a local environment?

Yes.

<span id=".cTLvvJrkvb_nlKjnrKzkuInmlrnlpKfmqKHlnovml7bvvIzorr7nva7nmoTlpJrova7ljoblj7Llr7nor50taGlzdG9yeWxlbmd0aC3mnKrnlJ_mlYjvvIzmr4_mrKHor7fmsYLlj6rkvKDpgJLkuobmnIDmlrDkuIDmnaHlr7nor53lhoXlrrnmgI7kuYjlip7vvJ8="></span>
## Q2: Why does `HistoryLength` not take effect for multi\-turn conversations, and why is only the latest conversation entry sent with each request?

You can try the following troubleshooting steps:


1. Check whether your LLM endpoint supports multi\-turn conversation history.

2. Check whether the endpoint response includes the standard `data: [DONE]` terminator. If this terminator is missing, the system might not be able to identify the end of a conversation turn, which can cause context storage to fail.
