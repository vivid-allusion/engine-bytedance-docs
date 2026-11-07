---
title: "Model usage"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Model_usage"
---

AIDAP provides AI models access capabilities (AI\-Gateway) for workspaces using the Supabase engine, allowing users to call ByteDance Doubao series models through OpenAI\-compatible interfaces. This topic explains how to view available models, test model performance online in the Console, and call models through the SDK.

<span id="lGAdKQAt"></span>
## Function introduction

AIDAP offers an all\-in\-one AI models access AI\-Gateway feature aimed at APP/Agent users. Compared with traditional AI\-Gateway, AIDAP’s AI\-Gateway has the following advantages:


|Core advantages |Function details |developer benefits |
|---|---|---|
|**API Key\-free security management** |**Deep integrated authentication system**:<br><br><br>* Seamlessly integrates with Supabase Auth, supports unified authentication with access_token and service_role_key.<br><br>* Supports [Third-party Auth (custom JWKS)](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_third-party_login) and trusted system JWT tokens. |* **Security upgrade**: avoid key leakage risk from the root by not distributing API keys to end users.<br><br>* **Quick access**: existing Supabase apps can quickly add AI models access capabilities.<br><br>* **Rrchitecture simplification**: supports "pure frontend" development mode, eliminating backend relay service development costs. |
|**Fully compatible with mainstream ecosystems** |**Standard protocol native support**:<br><br><br>* Compatible with major vendors’ SDKs such as OpenAI (GPT), Anthropic (Claude), Google (Gemini).<br><br>* deeply adapt to Vercel AI SDK and other modern AI development toolchains |* **Seamless migration**: Developers can continue using their existing development habits and tool chains with zero learning cost.<br><br>* **Reduce burden**: No need to manage or maintain underlying model protocol conversion, greatly easing R&D pressure. |
|**one\-stop operation and maintenance management suite** |**Full\-link user and traffic governance**:<br><br><br>* Built\-in quota management, multi\-level rate limiting strategy, and model fallback.<br><br>* Provides metering and billing, observation and auditing, long\-term memory, and hooks callback. |* **shorten delivery cycles**: eliminate repetitive development of operation and maintenance management functions, allowing the team to focus more on business innovation<br><br>* **optimize maintenance costs**: significantly reduce the complexity of generated code in AI programming scenarios, improving code maintainability |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For detailed billing information about large models, refer to <a href="https://docs.byteplus.com/en/docs/aidap/Billing_items_and_prices_of_large_model_access">Billing items and prices of large model access</a>.</div>


<span id="Ofawpsi4"></span>
## Precautions

In newly created workspaces, the user’s token quota is 0 by default. Before your first use of the AI\-Gateway, adjust the quota value to avoid the following error:


* `{"error":{"message":"no quota configured for user","type":"quota_exceeded"}}`

* `{"type":"error","error":{"type":"rate_limit_error","message":"no quota configured for user"}}`

* `{"error":{"code":402,"message":"no quota configured for user","status":"RESOURCE_EXHAUSTED"}}`


<span id="blZ2QAi6"></span>
## Function entry


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, select **AI models access** \> **Model usage** tab.


<span id="ljT8S4Co"></span>
## View model list

The left side of the **Model usage** page displays the list of available AI models in the current workspace. Each model shows the following information:


* **Model name**: the full identifier of the model, such as `bytedance/doubao-seed-2.0-pro`.

* **Model type**: the ability type of the model, such as "Text model."

* **Provider**: the provider of the model, such as "ByteDance."


Currently supported models include:


|**Model name** |**Type** |**Provider** |**Service status** |
|---|---|---|---|
|bytedance/doubao\-seed\-2.1\-pro |Text model |ByteDance |Active |
|bytedance/doubao\-seed\-2.1\-turbo |Text model |ByteDance |Deprecated |
|bytedance/doubao\-seed\-2.0\-pro |Text model |ByteDance |Deprecated |
|bytedance/doubao\-seed\-2.0\-code |Text model |ByteDance |Deprecated |
|bytedance/doubao\-seed\-2.0\-lite |Text model |ByteDance |Deprecated |
|bytedance/doubao\-seed\-2.0\-mini |Text model |ByteDance |Active |
|bytedance/doubao\-seedance\-2.0 |Video model |ByteDance |Active |
|bytedance/doubao\-seedance\-2.0\-fast |Video model |ByteDance |Active |
|bytedance/doubao\-seedance\-2.0\-mini |Video model |ByteDance |Active |
|bytedance/doubao\-seedream\-5.0\-pro |Image model |ByteDance |Active |
|bytedance/doubao\-seedream\-5.0\-lite |Image model |ByteDance |Deprecated |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The actual available model list may change with platform updates, refer to the console page for the latest display.</div>


* <div data-tips="true" data-tips-type="warning">Image model doubao\-seedream\-5.0\-lite were discontinued on October 12, 2026. It is recommended to switch to doubao\-seedream\-5.0\-pro.</div>


* <div data-tips="true" data-tips-type="warning">The services of text models doubao\-seed\-2.1\-turbo and doubao\-seed\-2.0\-lite were discontinued on October 9, 2026. It is recommended to switch to doubao\-seed\-2.1\-pro.</div>


* <div data-tips="true" data-tips-type="warning">The services of text models doubao\-seed\-2.0\-pro and doubao\-seed\-2.0\-code were discontinued on August 8, 2026. You can use doubao\-seed\-2.1\-pro and doubao\-seed\-2.1\-turbo as replacements.</div>



<span id="MOgUwPqx"></span>
## Online testing model

After selecting the target model in the model list, the test interaction panel for that model appears on the right. You can:


1. Enter the content you want to test in the input box, such as "What is an AI model?".

2. Click the send button to view the model's response in real time.


Through online testing, you can quickly verify the capabilities of different models and choose the one best suited for your business scenario.

If a video or image model (Seedance/Seedream) is selected, the interaction area shows the corresponding multimodal generation parameters to facilitate online experience of different models’ effects and capability differences.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the AI models access console, your session records are not retained (chat history no longer displays after leaving the page), but historically generated video outputs are saved in the Storage of the corresponding Branch, and you can still go to Storage to Download historical outputs.</div>



* <div data-tips="true" data-tips-type="default">Bucket name: <code>_supabase_internal_ai_gateway_output</code></div>


* <div data-tips="true" data-tips-type="default">Video file path: <code>video/<tenant>/<user>/<task_id>/video.mp4</code></div>


* <div data-tips="true" data-tips-type="default">Last frame path: <code>video/<tenant>/<user>/<task_id>/last_frame.<ext></code></div>



<span id="1CqitCv0"></span>
## **View AI Gateway audit logs**


1. [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

2. Click **Logs** in the left sidebar of Supabase console to enter the **Logs & Analytics** page.

3. On the **Logs & Analytics** page, click **Collection** \> **AI Gateway** to enter the audit log page of AI Gateway.


On this page, you can view the operation log list generated by the AI Gateway service.

<span id="gF9cteVK"></span>
### **Search and filter**

The following filtering and viewing tools are provided above the log list:


* Search box: supports keyword search for log events.

* Refresh button: manually refresh the log list.

* Last hour: time range selector, default to show logs of the last hour, other time ranges can be selected.

* Severity: filter by log level (e.g., INFO, WARNING, ERROR)

* Module: filter logs by module, supporting Backend and AI Request Trace modules.

* Chart: toggle the chart view to intuitively see the log distribution trend.

* Download button: export the current log data.


<span id="cXIy1V7W"></span>
### **View log details**

Click the tag of any log in the log list (such as **`INFO`**) to expand the log details panel on the right, providing two views: **Details** and **Raw**.


* **Details view**


Display key log fields in a structured way for quick reading:


|**Field** |**Decscription** |
|---|---|
|id |Unique identifier of the log entry. |
|timestamp |Timestamp when the log is generated. |
|event_message |Complete original log message content. |
|metadata |Log metadata includes fields such as level (log level), module (associated module), and msg (brief message), supporting click to Expand and view full content. |



* **Raw view**


Display the full data of logs in raw JSON format, with fields corresponding one\-to\-one with the Details view, suitable for scenarios requiring copying or precise parsing of logs. Example structure as follows:

&nbsp;

```JSON
{
  "event_message": "...",
  "id": "d93da8cc-52d5-4d05-ad10-5e673e06****",
  "metadata": [
    {
      "level": "info",
      "module": "backend",
      "msg": "[BACKEND] HERTZ: HTTP server listening on address=[::]:8916"
    }
  ],
  "timestamp": 1782114218004000
}
```


<span id="SWVaLouQ"></span>
## Call examples

Call code examples are provided at the bottom of the page to help you integrate the model into your application. The following three call methods are currently supported:


* **OpenAI**: Call through OpenAI SDK, suitable for applications integrated with the OpenAI ecosystem.

* **cURL**: Send HTTP requests directly via command line, suitable for quick debugging and testing.

* **Vercel AI**: Call through Vercel AI SDK, suitable for AI applications deployed on Vercel.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The large model interface of AIDAP Supabase is compatible with the OpenAI API format. You can switch between different methods in the <strong>Call method</strong> dropdown menu on the Console and view the corresponding code examples.</div>


<span id="ZgsOrRl9"></span>
### General calling process

No matter which calling method is used, the core process is:


1. Obtain the current user's session (Access Token) through the Supabase client.

2. Use the token as the authentication credential and set the URL of the Supabase instance as the request address.

3. Call the Chat Completions interface to send the request.


<span id="0cKkgprw"></span>
### Text model call examples

<span id="enm0cDI9"></span>
#### Call text model via OpenAI SDK

Call models through the openAI official SDK, suitable for applications integrated with the openAI ecosystem. No need to additionally install a specific SDK.

```JavaScript
const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

const { data: { session }, error } = await supabase.auth.getSession();

const client = new OpenAI({
  apiKey: session.access_token,
  baseURL: '$SUPABASE_URL/v1',
})
  
const stream = await client.chat.completions.create({
  model: 'bytedance/doubao-seed-2.0-pro',
  stream: true,
  messages: [{ role:'user', content: '' }],
});
```


<span id="v3d9Hs2c"></span>
#### Call text model via cURL

Send HTTP requests directly via command line, suitable for quick debugging and testing.

```Bash
curl "$SUPABASE_URL/v1/chat/completions" \
  -H "Authorization: Bearer $session.access_token" \
  -H "Content-Type: application/json" \
  -d '{
    "model":"bytedance/doubao-seed-2.0-pro",
    "stream": true,
    "messages":[{"role":"user","content":""}
   ]
}'
```


<span id="72TxRS6c"></span>
#### Call text model via Vercel AI SDK

Call models through the Vercel AI SDK, suitable for AI applications deployed on Vercel.

```JavaScript
const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

const { data: { session }, error } = await supabase.auth.getSession();

const gateway = createOpenAICompatible({
  name: "ai-gateway",
  apiKey: session.access_token,
  baseURL: '$SUPABASE_URL/v1',
});

const result = streamText({
  model: gateway('bytedance/doubao-seed-2.0-pro'),
  prompt: '',
});
```


<span id="mKyygmmh"></span>
### Video model call examples

<span id="LOmf4Zyg"></span>
#### Call video model via Ark Python SDK

```Python
import os
import time

from arkruntime import Ark
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_video() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = Ark(
        base_url=supabase_url + "/api/v3",
        api_key=session.access_token,
    )

    response = client.content_generation.tasks.create(
        model="bytedance/doubao-seedance-2.0-fast",
        content=[
            {
                "type": "text",
                "text": (
                    "一段 5 秒的产品展示视频：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
                    "镜头缓慢推进，写实摄影风格，高质量细节"
                ),
            }
        ],
        duration=5,
        ratio="16:9",
        resolution="720p",
        watermark=False,
    )

    task = client.content_generation.tasks.get(response.id)
    while str(getattr(task.status, "value", task.status)) not in {
        "succeeded",
        "failed",
        "cancelled",
    }:
        time.sleep(10)
        task = client.content_generation.tasks.get(response.id)

    print("response:", task)

generate_video()
```


<span id="sOy9VIdw"></span>
### Image model call examples

<span id="t1QTxmIM"></span>
#### Call image model via Ark Python SDK

```Python
import os

from arkruntime import Ark
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = Ark(
        base_url=supabase_url + "/v1",
        api_key=session.access_token,
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        watermark=False,
        response_format="url",
        output_format="png",
    )
    print("response:", response)

generate_image()
```


<span id="xTE8yVdw"></span>
#### Call image model via OpenAI Python SDK

```Python
import os

from openai import OpenAI
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = OpenAI(
        base_url=supabase_url + "/v1",
        api_key=session.access_token,
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

generate_image()
```


<span id="5IcxcrPj"></span>
#### Call image model via Vercel Python SDK

```Python
import asyncio
import os

import ai
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

async def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    provider = ai.get_provider(
        "openai",
        base_url=supabase_url + "/v1",
        api_key=session.access_token,
    )

    response = await provider.sdk_client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

asyncio.run(generate_image())
```


<span id="teaTA0e9"></span>
### Key parameters explanation


|**Name** |**Decscription** |
|---|---|
|apiKey / Authorization |Use `session.access_token` from the Supabase authentication system as the authentication credential. |
|baseURL / request address |Set as the URL of the Supabase instance with the suffix `/v1`, for example `https://your-instance.supabase.co/v1`. |
|modelshuo |Specify the model name to call, selected from the model list, for example `bytedance/doubao-seed-2.0-pro`. |
|stream |Set to `true` to enable streaming output, the model returns generated content step by step. |
|messages / prompt |Dialog message content. OpenAI and cURL use `messages` array (including `role` and `content`); Vercel AI uses `prompt` string. |


<span id="ouz3T4vG"></span>
### More samples

For more model usage examples, refer to [APP/Agent accessing AI models through AI-Gateway](https://docs.byteplus.com/en/docs/aidap/Supabase-APP_Agent_accessing_AI_models_through_AI-Gateway).
