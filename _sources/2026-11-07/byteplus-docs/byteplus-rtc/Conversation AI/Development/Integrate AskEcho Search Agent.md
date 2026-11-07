---
title: "Integrate AskEcho Search Agent"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856161"
---

You can integrate with AskEcho Search Agent, enabling the agent to retrieve information from the internet in real time and provide summarized answers. For example, it can retrieve the latest news, obtain weather information, or query real\-time stock prices.

<span id="bec648a5"></span>
## Restrictions

It is only compatible with BytePlus ModelArk models or third\-party LLMs that support Function Calling. For a comprehensive list of supported ModelArk models, refer to the [Model List-Tool use](https://docs.byteplus.com/en/docs/ModelArk/1330310#f44ceef7).

<span id="73f7e7c6"></span>
## Procedure

<span id="aa635b02"></span>
### Step 1: Set up the AskEcho Search Agent


1. Sign in to the [AskEcho Search Agent console](https://console.byteplus.com/bp-ask-echo/my-agent).

2. Go to **Workspace**, create an Agent as needed and activate it, then copy its ID.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating an agent, it is recommended to set the <strong>Web search</strong> option to <strong>Always search</strong>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a7a5ba322ac44d02a17d5bfebd70307c) </span>

3. Select **Manage \> API Key management**, create an API Key, and copy the API Key value.


<span id="886efb81"></span>
### Step 2: Configure StartVoiceChat

> You do not need to implement the backend logic for the web search tool. Instead, you simply declare the tool by providing a `FunctionName` and `FunctionDescription` when calling `StartVoiceChat`. The system then automatically invokes this built\-in tool.


When calling the `StartVoiceChat` interface, configure the `Config.WebSearchAgentConfig` object as follows:

&nbsp;


|Field |Required |Description |
|---|---|---|
|`Enable` |Yes |Enables the search agent. Must be set to `true`. |
|`APIKey` |Yes |The API Key you obtained in [Step 1: Set up the AskEcho Search Agent](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856161#aa635b02). |
|`ParamsString` |Yes |Pass\-through parameters for the AskEcho service, sent as a compressed and escaped JSON string. For details, see [ParamsString Description](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856161#095e595a). |
|`FunctionName` |Yes |Your custom name for the search agent tool (e.g., `web_search`). This must be unique and not conflict with any tool names defined in Function Calling (`LLMConfig.Tools`). |
|`FunctionDescription` |Yes |A natural language description that helps the LLM decide when to use this tool. This is injected into the prompt to improve accuracy.<br><br>> To avoid logical conflicts, the described purpose of this agent should be distinct from your other Function Calling tools. |
|`ComfortWords` |No |A user\-facing message played via TTS when a search is triggered. This improves the user experience by providing feedback while the user waits.<br><br><br>* The message must end with punctuation.<br><br>* If left blank, no message is played. |


<span id="095e595a"></span>
#### ParamsString Description

The `ParamsString` parameter is a compressed and escaped JSON string that passes configuration and context to the AskEcho service. It represents the entire `ChatCompletionRequest` body for the backend API call.

To generate this value:


1. Build a JSON object based on the `ChatCompletionRequest` parameters from the [AskEcho Search Agent API](https://docs.byteplus.com/en/docs/askecho/Agent_API_Reference).

   * `bot_id`: Required. Set this to the Agent ID from [Step 1: Set up the AskEcho Search Agent](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856161#aa635b02).

   * `stream`: Required. Must be set to `true`.

   * Other parameters (e.g., `messages`, `knowledge`) can be included as needed.

      **Examples**

      Here are some examples of the JSON object before it is compressed and escaped.

   * **Minimal Configuration (Required fields only)** 

      ```JSON
      {
         "bot_id": "7429...747",
         "stream": true
      }
      ```
      

   * **Advanced Configuration** (with contextual `messages` and `knowledge`)

      ```JSON
      {
         "bot_id": "7429...747",
         "stream": true,
         "user_id": "user_123",
         "messages": [
            { "role": "user", "content": "I want to plan a multi-day trip to Xi'an, any recommendations?" },
            { "role": "assistant", "content": "Of course, Xi'an is a historic city with famous sites like the Terracotta Army and Giant Wild Goose Pagoda. When are you planning to go?" }
         ], 
         "knowledge": "The current user is planning a trip to Xi'an."
      }
      ```
      

2. Compress and escape the JSON object into a single\-line string.


<span id="websearchagentconfig-example"></span>
#### WebSearchAgentConfig example

```JSON
"WebSearchAgentConfig": {
  "Enable": true,
  "ParamsString": "{\"bot_id\":\"7429...747\",\"stream\":true}",
  "APIKey": "your_agent_api_key",
  "FunctionName": "web_search",
  "FunctionDescription": "Used to query time-sensitive information, such as today's weather or the latest news events.",
  "ComfortWords": "Searching online for you, please wait a moment."
}
```


<span id="afc705ac"></span>
## Other Methods for Internet Access

In addition to integrating the AskEcho Search Agent, web search can also be implemented using MCP or Function Calling:


* [Integrate MCP](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856160)

* [Function Calling](https://docs.byteplus.com/docs/byteplus-rtc/docs-1554654)
