---
title: "AskEcho Search Agent API Reference"
product: "Byteplus AskEcho"
product_code: "askecho"
source: "https://docs.byteplus.com/en/docs/askecho/Agent_API_Reference"
---

<span id="yJK2xDOj"></span>
# Prerequisites for Access

**Authentication Method**: [AskEcho Search Agent Authentication](https://docs.byteplus.com/en/docs/askecho/AskEcho_Search_Agent_Authentication)

&nbsp;

<span id="jIKlMMKF"></span>
# Interface Details

<span id="ynWkwc5n"></span>
## Agent conversation

<span id="MagFKbFm"></span>
### URL


|Field |Value |
|---|---|
|URL |* API Key Access (Recommended)：https://torchlight.byteintlapi.com/agent_api/agent/chat/completion<br><br>* Byteplus IAM Access：https://mercury.volcengineapi.com?Action=ChatCompletion&Version=2024\-01\-01 |
|Method |POST |
|Content\-Type |application/json |
|Service |volc_torchlight_api |
|Region |ap\-southeast\-1 |


<span id="ia8XaGku"></span>
### Request

**ChatCompletionRequest**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|bot_id |String |Yes |Create on the console on the official website of Byteplus, address: https://console.byteplus.com/bp\-ask\-echo/my\-agent |
|messages<br><br> |Array[Message]<br><br> |Yes<br><br> |1. The conversation message list supports up to 10 rounds. (Note: This refers to the maximum valid array length of "messages" being 10. If there are more than 10, only the last 10 messages will be kept. However, if the first message is "System", it will be retained.)<br><br>2. The larger the context window, the longer the response time. If the window is too long, it may also lead to context deviation.<br><br>3. The "messages" array cannot be empty. One message represents a single round of conversation, while multiple messages represent multiple rounds of conversation. For example (text conversation provided for reference only):<br><br>   1. Single round of conversation:<br><br>      1. "messages": [ {"role": "user","content": "Hello"}]<br><br>   2. Multiple rounds of conversation: The last message represents the current request, while the previous messages represent the historical conversation.<br><br><br>```JSON```<br>```"messages": [ ```<br>```    {"role":"user","content": "Hello"},```<br>```    {"role":"assistant","content":"How can I help you?"},```<br>```    {"role":"user","content":"Introduce yourself"},```<br>```]```<br><br><br><br>4. Explanation of the role order in messages:<br><br>   1. The role of the first message must be either "user" or "system".<br><br>   2. The role of the last message must be "user".<br><br>   3. The valid role sequence for messages is as follows:<br><br>      1. system \-\> user \-\> assistant \-\> user ...<br><br>      2. user \-\> assistant \-\> user ... |
|stream |Boolean |No |Whether to enable streaming response. False by default. |
|user_id |String |No |User ID |
|device_id |String |No |Device ID |
|knowledge |String |No |You can pass the current [ambient music] and [driving vehicle] to enhance the Q&A effect, separated by commas.<br><br>Format example: Playing xxx's "xxx", driving xxx<br><br>```JSON```<br>```    "knowledge":"Currently playing 'Cloudy Day' by Stefanie Sun, driving the AITO M9 MAX five-seater.",```<br> |
|location_info |LocationInfo |No |Current geolocation information<br><br>```JSON```<br>```  "location_info":{ ```<br>```      "province": "New York State",```<br>```      "city": "New York City",```<br>```      "district": "Manhattan",```<br>```      "town": "Broadway",```<br>```      "longitude": -73.990259,```<br>```      "latitude": 40.714216 ```<br>```  },  ```<br> |
|timezone |String |No |The time zone where the user is located complies with the IANA standard. Refer to https://www.iana.org/time\-zones. <ins>The default is Asia/Shanghai</ins>. |
|locale |String |No |User language environment, currently supported:<br><br><br>* en: English environment<br><br>* zh: Chinese environment<br><br><br>Default value: en |


**Message**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|role<br><br> |String |Yes |* user: Indicates the user's input, such as a question or instruction.<br><br>* assistant: Indicates the AI assistant's response<br><br>* system: SystemPrompt |
|content |String/Object<br><br> |Yes<br><br> |Conversation message list<br><br>```JSON```<br>```"content": "You are a helpful assistant."```<br> |


**LocationInfo**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|province |String |No |It is recommended to provide the current province, as this can help improve the performance of the agent's responses. |
|city |String |No |It is recommended to provide the city where the current location is, as this can help improve the performance of the agent's responses. |
|district |String |No |It is recommended to provide the district where the current location is, as this can help improve the performance of the agent's responses. |
|town |String |No |It is recommended to provide the county/subdistrict where the current location is, as this can help improve the performance of the agent's responses. |
|longitude |Number |No |Longitude of the current location |
|latitude |Number |No |Latitude of the current location |


<span id="E23Zd3YA"></span>
### Response

**ChatCompletionResponse**


|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|id |String |Yes |Unique identifier of the response |
|object<br><br> |String |Yes |Type of response object<br><br><br>* Chat<br><br>   * chat.completion.chunk: Streaming chat response<br><br>   * chat.completion: Complete chat response |
|choices |Array[Choice] |Yes |Return item |
|created |Number |Yes |Response creation timestamp (in seconds) |
|references |Array[Reference] |No |References used for completion.<br><br>When streaming responses, this field is present only in the first frame. |
|follow_ups |Array[FollowUp] |No |Related follow\-up question suggestions. |


**Choice**


|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|delta<br><br> |Object |No |Used for **streaming response**, with incremental content updates included.<br><br><br>* role: Role identifier<br><br>* content: Text snippet<br><br>* tool_calls: Plugin invocation, provided in the final frame of the streaming summary.<br><br><br>```JSON```<br>```{```<br>```    "role": "assistant",```<br>```    "content": "Okay, based on your request, the volume needs to be adjusted to 50.",```<br>```    "tool_calls": [```<br>```        {```<br>```            "id": "Request ID",```<br>```            "type": "function",```<br>```            "function": {```<br>```                "name": "control_volume",```<br>```                "arguments": "{\"volume\": \"50\"}"```<br>```            }```<br>```        }```<br>```    ]```<br>```}```<br><br><br> |
|message |Object |No |Used for **non\-streaming responses**, with the complete response included, consistent with the delta structure. |
|finish_reason<br><br> |String |Yes |Reason for generation termination, possible values:<br><br><br>* stop: Complete model output returned by the API<br><br>* tool_calls: Plugin invocation<br><br>* length: Maximum token limit reached<br><br>* content_filter: Content filtered<br><br>* null: Generation not yet complete |
|index |Number |Yes |The currently selected index. It is usually 0 in a single response, but there may be multiple indices in a multi\-choice configuration. |


**Reference**


|**Field name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|id |String |Yes |Unique ID of the referenced content |
|source_type |String |Yes |Content source |
|site_name |String |No |Site name, mapped to SourceType. In enumerated scenarios, SourceType takes priority. |
|title |String |No |Title |
|publish_time<br><br> |Number |No |Publish time, UnixSecond timestamp<br><br>0 in some cases |
|url |String |No |Landing page |
|cover_image<br><br> |Object<br><br> |No |Cover image<br><br>```JSON```<br>```{```<br>```    "url": "https://xxx", // Cover image link```<br>```    "width": 123, // Cover image width, not guaranteed to be provided```<br>```    "height": 123, // Cover image height, not guaranteed to be provided```<br>```}```<br> |


&nbsp;

<span id="agz99iPt"></span>
### Sample request

```JSON
{
  "bot_id": "7429717161499017747",
  "user_id": "108210528",
  "messages": [
      {
          "role": "system", // systemprompt
          "content": "You are an AI assistant called Atlas. Your role is to answer questions clearly and provide useful guidance."
      },
      {
          "role":"user", // Chat History
          "content":"What are some songs by Lady Gaga?"
      },
      {
          "role":"assistant",
          "content":"Some of Jay Chou’s songs include Rice Field, Ye Huimei, East Wind Breaks and Chrysanthemum Terrace."
      },
      {
          "role": "user", // Current Question
          "content": "What is the main idea of the last song?"
      }
  ]
  "knowledge":"Currently playing 'Cloudy Day' by Stefanie Sun, driving the AITO M9 MAX five-seater.",
  "location_info":{ //Current Location
      "province": "New York State",
      "city": "New York City",
      "district": "Manhattan",
      "town": "Broadway",
      "longitude": -73.990259, //Longitude
      "latitude": 40.714216 //Latitude
  },  
  "stream": true // Streaming Output
}
```


&nbsp;

<span id="NOEbuIh9"></span>
### Sample response

<span id="ql2ptavM"></span>
#### Non\-streaming response

```JSON
{
    "id": "202412041530171E9F2E4A5A8B75F4E8A0",
    "object": "chat.completion",
    "choices": [
        {
            "delta": null,
            "message": {
                "role": "assistant",
                "content": "According to a December 2nd report, Honor will hold the global launch event for the Honor 300 series at 7 PM on the same day, officially unveiling the series of smartphones, including the Honor 300 Ultra. Recently, some tipsters have compiled its configuration information: it will feature a downclocked Qualcomm Snapdragon 8 Gen 3 mobile platform (3.0GHz clock speed, released on October 25), a 1.5K OLED eye-protecting display, a rear triple-camera setup (including a 50MP large sensor main camera and a periscope telephoto camera), a 50MP dual front camera, 100W wired and wireless charging support, Honor's Giant Rhino Glass, satellite communication technology, and a plastic mid-frame. Many believe its starting price may be around RMB 4,000."
            },
            "finish_reason": "stop",
            "index": 0
        }
    ],
    "created": 1733297420,
    "references": [
        {
            "id": "7443704254352720423",
            "source_type": "universal_search",
            "site_name": "BBC Weather",
            "title": "London - BBC Weather",
            "publish_time": 1733122470,
            "url": "https://www.bbc.com/weather/2643743",
            "cover_image": {
                "url": "https://www.bbc.com/weather/2643743",
                "width": 600,
                "height": 518
            }
        }
    ],
    "usage": {
        "prompt_tokens": 2276,
        "completion_tokens": 229,
        "total_tokens": 2505
    }
}
```


<span id="M5h258LX"></span>
#### Streaming response


* Streaming text and followup


```JSON
data: {
    "id": "2024120415414954BC859A628D38329176",
    "object": "chat.completion.chunk",
    "choices": [
        {
            "delta": {
                "role": "assistant",
                "content": "According"
            },
            "message": null,
            "finish_reason": "",
            "index": 0
        }
    ],
    "created": 1733298110,
    "references": [
        {
            "id": "7443704254352720423",
            "source_type": "universal_search",
            "site_name": "BBC News",
            "title": "Highlights of the iPhone 16 launch event – starting price confirmed?",
            "publish_time": 1733122470,
            "url": "https://www.bbc.com/news/technology-7443704254352720423",
            "cover_image": {
                "url": "https://ichef.bbci.co.uk/news/600/cpsprodpb/example.jpg",
                "width": 600,
                "height": 518
            }
        }
    ]
}

data: {
    "id": "2024120415414954BC859A628D38329176",
    "object": "chat.completion.chunk",
    "choices": [
        {
            "delta": {
                "role": "assistant",
                "content": " "
            },
            "message": null,
            "finish_reason": "",
            "index": 0
        }
    ],
    "created": 1733298110,
    "references": null
}

data: {
    "id": "2024120415414954BC859A628D38329176",
    "object": "chat.completion.chunk",
    "choices": [
        {
            "delta": {
                "role": "assistant",
                "content": "1"
            },
            "message": null,
            "finish_reason": "",
            "index": 0
        }
    ],
    "created": 1733298110,
    "references": null
}

...

data: {
    "id": "2024120415414954BC859A628D38329176",
    "object": "chat.completion.chunk",
    "choices": [
        {
            "delta": {
                "role": "assistant",
                "content": ""
            },
            "message": null,
            "finish_reason": "stop",
            "index": 0
        }
    ],
    "created": 1733298110,
    "references": null
}

data: {
    "id": "2024120415414954BC859A628D38329176",
    "object": "chat.completion.chunk",
    "choices": null,
    "created": 1733298110,
    "references": null,
    "follow_ups": [
        {"item": "How fast is the iPhone 16 wireless charging?"},
        {"item": "What are the main features of the iPhone 16 satellite communication technology?"},
        {"item": "How effective is the iPhone 16’s 1.5K OLED eye-comfort display?"}
    ]
}

data: {
    "id": "2024120415414954BC859A628D38329176",
    "object": "chat.completion.chunk",
    "choices": null,
    "created": 1733298110,
    "references": null,
    "usage": {
        "prompt_tokens": 2276,
        "completion_tokens": 247,
        "total_tokens": 2523
    }
}

data: [DONE]
```


&nbsp;

<span id="EjjimfYn"></span>
# Advanced Features

<span id="WjBYQRcI"></span>
## Citation badge

**Description:**  Inserts citation markers into the output to indicate which reference material the text comes from.

**Output Format:**  `[ref_x]`, where `x` is the index of the reference item in the `references` array, starting from 1.

**Applicable Scenarios:**  Both streaming and non\-streaming mode.

**How to Enable:**  Toggle the switch in the console.

**Notes:** 


* The client can customize how citation badges are displayed according to its own needs.


&nbsp;

<span id="bnme9My0"></span>
## Output of Key Execution Steps

**Description:**  Outputs key execution steps during processing to enhance the interaction experience.

**Applicable Scenarios:**  Only effective in streaming mode.

**How to Enable:**  See `*Extended Parameters*` * – * `*Other Parameters*`.

**Key Execution Steps:**  


|**Action** |**Description(cn)**  |**Description(en)**  |**Explanation** |
|---|---|---|---|
|planning |正在理解问题 |Understanding |Agent has completed initialization and starts understanding the user’s question. |
|search_begin |正在搜索网页 |Searching the web |Invokes the web search capabilities. |
|search_finish |已阅读X个网页 (X\>0) |Read x web pages (X\>0) |Web search completes. |
||搜索完成 (空搜情况) |Search completed (X=0) ||


**Sample response：** 

```JSON
{
    "id": "202503271640468507AA4C950F0039CEA0",
    "object": "chat.completion.chunk",
    "choices": [
        {
            "delta": {
                "role": "assistant",
                "content": "",
                "tool_calls": null,
                "processing_state": {
                  "action": "planning",
                  "description": "Understanding"
                }
            },
            "message": null,
            "finish_reason": "",
            "index": 0
        }
    ],
    "created": 1743064848,
    "references": null
}
```


&nbsp;

&nbsp;

<span id="MVoeG2Qw"></span>
# Extended Parameters

You can ignore this section when using the basic features. Extended parameters provide additional support for certain special scenarios. These parameters are **not general\-purpose** and are usually enabled only in specific cases upon request.

**Note:**  There is no guarantee of stable responses if extended parameters are provided arbitrarily.

&nbsp;

<span id="ghZmdGqH"></span>
## Other Parameters

**ChatCompletionRequest**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|bot_id |String<br><br> |Yes |Agent ID: Obtained after creating the agent in the console: https://console.byteplus.com/bp\-ask\-echo/my\-agent |
|... |... |... |... |
|extension_options |ExtensionOptions |No |Extended Parameters |


**ExtensionOptions**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|filter_emoji |Boolean |No |When set to `true`, filters out emoji characters from the model’s output. |
|enable_processing_state |Boolean |No |When set to `true`, outputs the agent’s key execution steps.<br><br>Only effective in streaming mode. See **Advanced Features – Output of Key Execution Steps** for details. |
|disable_citation |Boolean |No |When set to `true`, disables citation badge even if they are enabled in the console. |
|disable_follow_up |Boolean |No |When set to `true`, disables follow\-up function even if they are enabled in the console. |
|browsing_mode<br><br> |Number |No |Controls web search behavior. This parameter takes priority over console settings.<br><br>**Parameter values:** <br><br><br>* **1 – Auto search**<br><br>   * Equivalent to the default “Auto Search” setting in the console.<br><br>* **2 – Always search**<br><br>   * Ensures that at least one search source is used for web retrieval and summarization.<br><br>* **3 – Search disabled**<br><br>   * Completely disables web access. No online resources will be used for search or summarization. |


**ChatCompletionResponse**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|id |String |Yes |Unique identifier of the response |
|... |... |... |... |


&nbsp;

&nbsp;

<span id="Yf0hAigG"></span>
# Error Handling

<span id="0185bung"></span>
## Error code

**Gateway errors:** 

This API is published through the BytePlus TOP gateway. If a gateway\-level error occurs (for example, a signature verification error), we will return a BytePlus TOP gateway error. The response format is as follows:

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202210271151020102121450321B8D2A21",
        "Action": "ScanSyncArticles",
        "Version": "2023-01-01",
        "Service": "volc_torchlight_api",
        "Region": "cn-north-1",
        "Error": {
            "CodeN": 100010,
            "Code": "SignatureDoesNotMatch",
            "Message": "The request signature we calculated does not match the signature you provided. Check your Secret Access Key and signing method. Consult the service documentation for details."
        }
    }
}
```


**Product\-specific error codes:** 

```JSON
{
    "error": {
        "log_id": "Error logid",
        "message": "Detailed description of the error",
        "type": "Error type",
        "code": "Error code",
        "param": "Optional. The parameter that caused the error"
    }
}
```


**If an error occurs during streaming mode, the error information will be returned in a data block starting with data:. The fields are explained as follows:** 


|**Parameter** |**Type** |**Description** |**Required** |**More information** |
|---|---|---|---|---|
|type<br><br> |String |Error type<br><br> |Yes |* authentication_error：Authentication\-related error<br><br>* validation_error：Request parameter validation failed<br><br>* permission_error：Permission\-related error<br><br>* model_error：AI model\-related error<br><br>* bot_unavailable_error：The agent is deactivated, pending activation, or has exhausted its trial quota<br><br>* server_error：Internal server error |
|code |String |Specific error code |Yes |* Provides a detailed error code, or may be the same as the type field. |
|message |String |Error description |Yes |* Provides a detailed error code, or may be the same as the type field. |
|param |String |The parameter that caused the error |No |* Returned only when the error is parameter\-related. |


<span id="JaMGLavW"></span>
## Error response

```JSON
// Authentication Error
{
  "error": {
    "code": "invalid_api_key",
    "message": "API key expired or invalid",
    "type": "authentication_error",
    "param": null
  }
}
// Request Parameter Error
{
  "error": {
    "code": "invalid_parameter",
    "message": "stream requires bool type",
    "type": "validation_error",
    "param": "stream"
  }
}
// Rate Limit Exceeded
{
  "error": {
    "code": "llm_rate_limit_exceeded",
    "message": "llm_rate_limit_exceeded",
    "type": "rate_limit_error",
    "param": null
  }
}
```


<span id="AUYj3XJa"></span>
## How to obtain logid

RequestID is the unique identifier for each API request. If an issue arises that cannot be resolved independently, you can provide the RequestID of the request, and we will assist with troubleshooting.


* The RequestID format is: `20241211184452633DBFC9B5FB220BDEBF`.

* Several ways to obtain the RequestID:

   * Response body` ResponseMetadata-RequestID`. Refer to the document for the specific response structure: [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

   * Response header `X-Tt-Logid`
