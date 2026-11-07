---
title: "ArkClaw A2A API integration: basic calls"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_A2A_API_integration_basic_calls"
---

This topic describes how to remotely call **ArkClaw** agent capabilities through the Agent\-to\-Agent (A2A) JSON\-RPC standard API. Three calling modes are supported: **synchronous blocking, streaming push, and asynchronous polling**, which can support various business scenarios such as simple Q&A, real\-time output, and long\-running tasks. Developers can complete integration debugging and business integration using any HTTP client, such as curl, Python, or Postman.

This topic uses `curl` commands and `Python` code as examples to illustrate API calling methods.

<span id="buqLkysY"></span>
## What can the ArkClaw A2A API do?

The ArkClaw A2A API is based on the JSON\-RPC 2.0 protocol and exposes ArkClaw agent capabilities to external systems. Through this API, you can:


* **Integrate intelligent Q&A into business systems**: Connect an agent to the business backend to provide knowledge Q&A, semantic search, and similar capabilities.

* **Process long\-running tasks asynchronously**: Suitable for scenarios such as report generation and complex retrieval, avoiding synchronous waiting.

* **Deliver streaming interaction**: Display agent output in real time on the frontend to improve user experience.

* **Enable multi\-turn contextual conversations**: Support follow\-up questions and contextual reasoning through session persistence.


<span id="ssGRj1wu"></span>
## Request endpoint and common parameters

<span id="a5SNIg4I"></span>
### Enable Webhook and obtain the Webhook request endpoint

After you enable A2A\-protocol\-based external access for an ArkClaw instance, the platform automatically generates an Endpoint URL and an API Key for external business systems to access and call the current ArkClaw instance over the public network.


1. On the details page of the target ArkClaw instance, switch to the "Settings" tab, and click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0726c23cacc938e9916523fd157ae331.png) </span> icon to enable Webhook. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Setting_Webhook)

2. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9351d4db4106b3b7851667cc3c7cf069.png) </span> icon to copy the generated public endpoint for use in subsequent calls. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Setting_Webhook?lang=en#7K7ux20B)


<span id="GIOli0Uy"></span>
### Common parameters


* **Unified API request endpoint**

   All A2A API requests are sent to the following public endpoint. Replace the placeholder parameters in the endpoint with the actual configuration of your ArkClaw instance:

   `https://{GATEWAY_HOST}/a2a/jsonrpc?apikey={API_KEY}&clawId={CLAW_ID}`

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The request endpoint above is the <strong>Webhook</strong> public Endpoint, which can be obtained from the <a href="https://docs.byteplus.com/en/docs/394/114190#a5SNIg4I">Enable Webhook and obtain the Webhook request endpoint</a> section.   </div>
   

   * **Public endpoint parameters**

   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |`{GATEWAY_HOST}` |The public domain name of APIG.<br><br>> You need to use the public domain name. Do not append the `-inner` private network suffix. Private network domain names only support private network access and cannot be resolved over the public network. |xxxxxxxx.apigateway\-cn\-beijing.volceapi.com |
   |`{API_KEY}` |The API authentication key used for server\-side identity verification. It is globally unique. Keep it confidential and do not expose it to prevent security risks such as unauthorized access and API abuse. |9ac252facbad4e519ddd6413ed\*\*\*\* |
   |`{CLAW_ID}` |The unique ID of the ArkClaw instance, used to identify the specific agent instance to call. |ci\-yep7s80hdsrkm4w\*\*\*\* |
   


<span id="GhyBTfxP"></span>
### Public request headers

All API requests use the following fixed request header: `Content-Type: application/json`.

<span id="ivRJ4q02"></span>
## Call the A2A API through `curl` commands

`curl` is suitable for **quick debugging and temporary API verification**. It requires no development environment. Simply copy the command and execute it in a terminal. It is commonly used for testing, troubleshooting, and quickly viewing response structures. You can choose any of the following methods to debug the A2A API as needed.


<Tabs>
<Tab zoneid="H5IwIHDBV2" title="Synchronous blocking call">
<TabTitle>Synchronous blocking call</TabTitle>

This mode is suitable for short Q&A interactions, lightweight computations, and tasks with short overall processing time. For details, see **Synchronous access to the A2A API** in [ArkClaw A2A API integration: session-based multi-turn conversations](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_A2A_API_integration_session-based_multi-turn_conversations).


</Tab>
<Tab zoneid="Ulk7KnQZuW" title="Asynchronous polling call">
<TabTitle>Asynchronous polling call</TabTitle>

This mode is suitable for long\-text generation calls and tasks with long execution times. For details, see **Asynchronous access to the A2A API** in [ArkClaw A2A API integration: session-based multi-turn conversations](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_A2A_API_integration_session-based_multi-turn_conversations?lang=zh).


</Tab>
<Tab zoneid="djUKOCnC4I" title="Streaming call">
<TabTitle>Streaming call</TabTitle>

This mode is suitable for interactive scenarios that require real\-time result output, long\-text segmented responses, or continuous retrieval of intermediate states during task processing.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This mode uses the SSE protocol to push data continuously. The server returns processing states and generated content event frame by event frame within the same connection, allowing the client to display output results in real time.</div>



1. **Send a streaming request**: Using the question "Who are you?" as an example, execute the following command to send a user conversation message via the streaming API.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You only need to replace the values of the following parameters with your actual business information. All other parameters are fixed and do not require any modifications.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>{URL}</code>: The API call endpoint. This is a <strong>required field</strong>. Replace it with the public Endpoint provided in the ArkClaw console. For details, see the <a href="https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_A2A_API_integration_basic_calls?lang=zh#a5SNIg4I">Enable Webhook and obtain the Webhook request endpoint</a> section.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>id</code>: A unique identifier for a single request. Custom strings or UUIDs are supported. This parameter is used to distinguish each API call.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>messageId</code>: A unique ID for the current conversation message. Custom strings or UUIDs are supported. This parameter is used to distinguish different messages within a session.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>text</code>: The content of the user's question. Replace this value with your actual conversation content customized based on your business needs.   </div>
   

   ```JSON
   curl '{URL}' \
    -H 'content-type: application/json' \
    -d '{
       "jsonrpc": "2.0",
       "id": "unique-request-id",
       "method": "message/stream",
       "params": {
         "message": {
           "parts": [{"kind": "text", "text": "Who are you"}],
           "messageId": "unique-message-id",
           "role": "user"
         }
       }
     }'
   ```
   

2. **View the streaming response**: After the request is sent, the streaming API returns multiple `data:`event frames based on the SSE protocol. There are two types:

   * **working frame**: Pushes only the task running state and the `contextId` session identifier, with no complete response text. This type is used to display the loading state in real time.

   * **completed frame**: Pushed after inference ends. Contains the complete AI response message, conversation context, and output `artifacts`. Indicates that the current conversation turn is complete, and listening to the streaming data is stopped.


</Tab>
</Tabs>


<span id="gIBk8gjP"></span>
## Call the A2A API through `Python` commands

Using Python's requests library to call the A2A API is suitable for integrating ArkClaw's A2A capabilities in server\-side scripts, automated tasks, or backend applications. The supported calling modes include synchronous blocking, streaming, and asynchronous polling.

<span id="oE0K6Lxu"></span>
### Step 1: Install dependencies


1. Execute the following command to install the network request dependency library.

   ```Bash
   pip install requests
   ```
   

2. Open a terminal and execute the following command. If the output displays the Version and Location information, the installation is complete.

   ```Bash
   pip show requests
   ```
   


<span id="Kw9hPFkU"></span>
### Step 2: Configure the API endpoint and encapsulate common request methods

Replace the API endpoint with the public Endpoint provided in the ArkClaw console, and encapsulate the message construction method and common request method. This makes the methods reusable for subsequent synchronous, streaming, and asynchronous calls, and avoids writing repeated request construction code.

```Python
import json
import time
import uuid

import requests

URL = f"https://sd8ojs9tiq5rjni****.apigateway-cn-beijing.volceapi.com/a2a/jsonrpc?apikey=9ac252facbad4e519ddd6****&clawId=ci-yeok2q4dmo3pe****"
HEADERS = {"Content-Type": "application/json"}


def build_message(text):
    return {
        "parts": [{"kind": "text", "text": text}],
        "messageId": str(uuid.uuid4()),
        "role": "user",
    }


def post_jsonrpc(method, params, timeout=120):
    payload = {
        "jsonrpc": "2.0",
        "id": str(uuid.uuid4()),
        "method": method,
        "params": params,
    }
    response = requests.post(URL, headers=HEADERS, json=payload, timeout=timeout)
    response.raise_for_status()
    data = response.json()
    if "error" in data:
        raise RuntimeError(data["error"])
    return data["result"]
```


The following table describes the parameters. Replace the sample values with actual values.


|**Parameter** |**Type** |**Required** |**Description** |Sample value |
|---|---|---|---|---|
|**Basic configuration parameters** |||||
|URL |String |Yes |The API call endpoint. Replace it with the [public Endpoint](https://docs.byteplus.com/en/docs/394/114190#a5SNIg4I) provided in the ArkClaw console. |`https://sd8ojs9tiq5rjni****.apigateway-cn-beijing.volceapi.com/a2a/jsonrpc?apikey=9ac252facbad4e519ddd6****&clawId=ci-yeok2q4dmo3pe****` |
|HEADERS |Dict |Yes |The HTTP request header. Fixed as ` {"Content-Type": "application/json"}`. No modification is required. |Retain the default value |
|**Construct the A2A message body parameters** |||||
|text |String |Yes |The text input by the user, used as the content of this conversation request. You can modify it based on your business requirements. |`Who are you?` |
|parts[].kind |String |Yes |The type of the message part. The value is fixed as `text`, indicating a text message. |Retain the default value |
|messageId |String |Yes |A unique identifier for a message, used to identify a single user message. |Retain the default value |
|role |String |Yes |The message role identifier. The value is fixed as `user`, indicating that the message is a question from the user. |Retain the default value |
|**JSON\-RPC request parameters** |||||
|method |String |Yes |The name of the method called by JSON\-RPC. The value varies by calling mode. Valid values:<br><br><br>* message/send: synchronous blocking call<br><br>* message/stream: streaming call<br><br>* tasks/get: polling for asynchronous task results |`message/send` |
|params |Dict |Yes |The parameter object for the method call. The valid values of the subfields vary by calling mode:<br><br><br>* For synchronous blocking calls (message/send): Pass in `params.message`.<br><br>* For streaming calls (message/stream): Pass in `params.message`.<br><br>* For asynchronous task submission (message/send, where params.configuration.blocking=false): Pass in `params.message` and `params.configuration`.<br><br>* For asynchronous task queries (tasks/get): Pass in `params.id`. | |
|timeout |Integer |No |The timeout for the HTTP request, in seconds. The default value is 120 seconds. If your business involves long\-running inference scenarios, increase this value as needed. Only an integer value is accepted. |Retain the default value |
|jsonrpc |String |Yes |The JSON\-RPC protocol version. The value is fixed as 2.0. No modification is required. |Retain the default value |
|id |String |Yes |A unique identifier for a request, automatically generated, used to match requests with responses. |Retain the default value |


<span id="Xd56qjfZ"></span>
### Step 3: Select a calling mode based on your business scenario

Combine the base encapsulation code with the synchronous blocking, streaming, or asynchronous polling call example into a single Python script. Run the file directly, and the program will automatically output the complete response returned by the agent.


<Tabs>
<Tab zoneid="rpZ6Q34Udv" title="Synchronous blocking call">
<TabTitle>Synchronous blocking call</TabTitle>

Synchronous blocking calls are suitable for general Q&A interactions, short\-text generation, and scenarios where the result can be returned within a single request, such as single\-turn Q&A or lightweight command execution.

Call the common request function `post_jsonrpc`, passing in the method name `message/send` and the constructed conversation message body. The API returns the final result in a single response after the server completes processing.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Replace the text inside the parentheses of <code>send_sync("Who are you?")</code> with your desired question as needed.</div>


```Python
def send_sync(text):
    result = post_jsonrpc(
        "message/send",
        {"message": build_message(text)},
    )
    parts = result.get("status", {}).get("message", {}).get("parts", [])
    return "".join(part.get("text", "") for part in parts if part.get("kind") == "text")


answer = send_sync("Who are you")
print(answer)
```





</Tab>
<Tab zoneid="PdadHkGvYh" title="Streaming call">
<TabTitle>Streaming call</TabTitle>

This mode is suitable for scenarios involving long\-text generation, segmented responses, and real\-time result display.

> `message/stream` returns an event stream based on the **Server\-Sent Events** (**SSE**) protocol. In Python, specify `stream=True` to continuously read the incremental content returned by the server.


Set the method name to `message/stream` and specify `stream=True` to continuously read the SSE event stream and output incremental content frame by frame. When the returned `state` changes to `completed`, `failed`, or `canceled`, the streaming task is complete, and the client should stop reading further events.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace the text inside the parentheses of <code>send_sync("Who are you?")</code> with your desired question as needed.</div>


* <div data-tips="true" data-tips-type="default">If your business involves long\-running inference or generation scenarios, increase the <code>timeout</code> parameter value based on the API response time to avoid requests terminating prematurely due to insufficient wait time.</div>



```Python
def send_stream(text):
    payload = {
        "jsonrpc": "2.0",
        "id": str(uuid.uuid4()),
        "method": "message/stream",
        "params": {"message": build_message(text)},
    }

    with requests.post(URL, headers=HEADERS, json=payload, stream=True, timeout=120) as response:
        response.raise_for_status()
        response.encoding = "utf-8"
        for line in response.iter_lines(decode_unicode=True):
            if not line or not line.startswith("data:"):
                continue

            event = json.loads(line[len("data:"):].strip())
            result = event.get("result", {})
            state = result.get("status", {}).get("state")
            parts = result.get("status", {}).get("message", {}).get("parts", [])
            text_delta = "".join(part.get("text", "") for part in parts if part.get("kind") == "text")

            if text_delta:
                print(text_delta, end="", flush=True)
            if state in {"completed", "failed", "canceled"}:
                break


send_stream("Who are you")
```





</Tab>
<Tab zoneid="USrupvSg4o" title="Asynchronous polling call">
<TabTitle>Asynchronous polling call</TabTitle>

This mode is suitable for scenarios where task execution takes a long time the client does not want to be blocked waiting for the result.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace the text inside the parentheses of <code>send_sync("Who are you?")</code> with your desired question as needed.</div>


* <div data-tips="true" data-tips-type="default">If your business involves long\-running inference or generation scenarios, increase the <code>timeout</code> parameter value based on the API response time to avoid requests terminating prematurely due to insufficient wait time.</div>


1. First, submit an asynchronous task to obtain a `task_id`.

   Call the `start_async_task` function, using the `message/send` API, where `configuration.blocking=False` is specified to instruct the server to enable asynchronous non\-blocking mode.

   * The server returns a `task_id` immediately upon receiving the request, without waiting for model inference.

   * This mode significantly reduces the API response time and prevents the client from being blocked on a long\-lived connection.

   ```Python
   def start_async_task(text):
       result = post_jsonrpc(
           "message/send",
           {
               "message": build_message(text),
               "configuration": {"blocking": False},
           },
       )
       return result["id"]
   ```
   

2. Call the `get_task` function to query the task execution status by `task_id` via `tasks/get`, and set a fixed polling interval.

   * Stop polling when the `state` parameter changes to `completed`, `failed`, or `canceled`.

   * We recommend that you set a reasonable polling interval (for example, 1 to 5 seconds) to avoid resource waste caused by high\-frequency requests.

   ```Python
   def get_task(task_id):
       return post_jsonrpc("tasks/get", {"id": task_id})
   
   def wait_task(task_id, interval=2, timeout=300):
       deadline = time.time() + timeout
       while time.time() < deadline:
           result = get_task(task_id)
           state = result.get("status", {}).get("state")
           if state in {"completed", "failed", "canceled"}:
               return result
           time.sleep(interval)
       raise TimeoutError(f"task timeout: {task_id}")
   
   task_id = start_async_task("Who are you")
   result = wait_task(task_id)
   parts = result.get("status", {}).get("message", {}).get("parts", [])
   print("".join(part.get("text", "") for part in parts if part.get("kind") == "text"))
   ```
   





</Tab>
</Tabs>
