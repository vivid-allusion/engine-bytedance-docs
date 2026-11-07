---
title: "Sample calls for text prompts"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts"
---

This topic describes the method for testing an agent using plain text prompts embedded in the URL.

<span id="C9uokv5V"></span>
## Prerequisites

[An agent runtime in the](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) **Running** status is created in the console.

<span id="M9tqhsxA"></span>
## Use the console test feature

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The online test feature is supported only when <strong>Network access</strong> is set to <strong>Public network</strong>.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">For agent runtimes created based on OAuth inbound identity authentication, only the <strong>M2M type client</strong> is supported for online testing. Other client types are not supported for online testing. If no client type is specified when you create the agent runtime, you can go to the <a href="https://docs.byteplus.com/en/docs/identity/Create_a_user_pool">user pool</a> to create an <strong>M2M type client</strong> and then perform online testing.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The ChatUI (intelligent conversation interface) online test method is supported only for specific applications deployed with one click from Agent Gallery. For details, refer to <a href="https://docs.byteplus.com/en/docs/agentkit/Using_scenario-based_templates">Test agent applications</a>.</div>


   Click the "Online test" button in the "Actions" column of the target agent runtime, specify the request method, headers, and body, and then click "Confirm" to verify whether the agent can work as expected.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Request method |The following request methods are supported: GET, POST, PUT, DELETE, PATCH, HEAD, and OPTIONS. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a67b361bc40c0e4ca7f4caeb97020265.png) </span> |
   |URL |The public network access domain name assigned to the agent by the platform, which cannot be modified. ||
   |Headers |The request header. Including:<br><br><br>* Content\-Type: The format of the request body. Default value: application/json.<br><br>* Authorization: Inbound identity authentication. That is, the API Key or OAuth JWT that is configured for inbound identity authentication during the agent runtime creation process. The API Key is used by default.<br><br>* session_id: The custom session identifier request header, used to identify the session of the current user. Default value: defaultSession.<br><br>* user_id: The custom user identifier request header, used to identify the user initiating the request. Default value: defaultUser. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29ed9f955c8f2fd0dc0c16a00a55ee3b.png) </span><br><br> |
   |Body |The request body. The raw, form\-data, and x\-www\-form\-urlencoded formats are supported. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ed34413d93ef12a43ae7ac5d9616cc0.png) </span><br><br> |
   

If the test result returns information similar to the following, the agent is working as expected.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_714a888b6547325d839457ef1349f9b8.png) </span>


<span id="T4IsX7NF"></span>
## Use the `invoke` command

After an agent runtime is created, you can execute the `agentkit invoke` command to send a test request to the agent and verify whether its features work as expected. For detailed parameter description, refer to [agentkit invoke](https://docs.byteplus.com/en/docs/agentkit/agentkit_invoke).


* Usage method

   ```Bash
   agentkit invoke [message content][option]
   ```
   

* Sample value

   ```Bash
   agentkit invoke "What's the weather like in Hangzhou today?"
   ```
   

   If the following output is displayed, the call is successful.

   ```Bash
   
   💬 Calling the agent...
   ✅ Runtime ID: r-xxxxxx
   🌐 Call address: http://xxx.apigateway-ap-southeast-1.volceapi.com
   ✅ Call succeeded!
   📡 Agent response:
   It's sunny in Hangzhou today with a temperature of 22°C, perfect for going out.
   ```
   


<span id="3Y0dFppi"></span>
## Use the `curl` command

After the agent runtime is created, the agent runtime will automatically generate a domain name, as shown in the figure below. You can use the `curl` command to specify the domain name and initiate a POST request to verify whether the agent is working as expected.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_43bcc406c7d0d82dd6fb5fb94d9d5fad.png) </span>

In this example, weather query is used for verification.

```Bash
curl -v -X POST http://sd3rltac7npja1818xxxx.apigateway-xxxx.volceapi.com/invoke \
  -H "Authorization: Bearer 6-CVnQDrvNM4iYRLTsw8mPe4RerrQnOq****" \
  -H "Content-Type: application/json" \
  -H "user_id: 123" \
  -H "session_id: 123" \
  -d '{"prompt": "What is the weather like in Wuhan?"}'
```


The following table describes the parameters. Replace the sample values with actual values.


|Parameter​ |Description |
|---|---|
|\-X POST |Set the HTTP request method to POST. |
|http://sd3rltac7npja1818xxxx.apigateway\-xxxx.volceapi.com/invoke |The domain name of the agent runtime for public network access. |
|\-H "Authorization: Bearer 6\-CVnQDrvNM4iYRLTsw8mPe4RerrQnOq\*\*\*\*" |Inbound identity authentication. That is, the API Key or OAuth JWT that is configured for inbound identity authentication during the agent runtime creation process. In this example, the API Key is used. |
|\-H "Content\-Type: application/json" |The format of the request body. In this example, the JSON format is specified. |
|\-H "user_id: 123" |The custom user identifier request header, used to identify the user initiating the request. |
|\-H "session_id: 123" |The custom session identifier request header, used to identify the session of the current user. |
|\-d '{"prompt": "What is the weather like in Wuhan?"}' |The POST request body, which contains data in JSON format. |


If the following output is displayed, the call is successful.

```JSON
{
  "code": 200,
  "message": "success",
  "data": {
    "city": "Wuhan",
    "date": "2025-10-22",
    "weather": "Overcast turning to light rain",
    "temperature": {
      "min": 16,
      "max": 22,
      "unit": "℃"
    }
```


<span id="B1mpeedn"></span>
###
