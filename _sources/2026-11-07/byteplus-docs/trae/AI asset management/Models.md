---
title: "Models"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/model-settings"
---

You can configure model settings that work for the entire enterprise.

<span id="bac641d2"></span>
## System built\-in models

<span id="d03e3823"></span>
### Available system built\-in models

The following built\-in system models are provided by TRAE Enterprise:


* GPT\-5.4 (default model)

* GPT\-5.2

* Gemini\-3.1\-Pro\-Preview

* Gemini\-3\-Flash\-Preview

* GLM\-4.7

* MiniMax\-M2.7

* Kimi\-K2.5

* DeepSeek\-V3.2


<span id="7edeb00c"></span>
### Manage system built\-in models

You can enable or disable system built\-in models. The default model cannot be disabled.


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Setup** \> **Models**.

3. In the **System Built\-in Models** section, enable or disable models.


<span id="eba117e4"></span>
## Enterprise built\-in models

<span id="9c71f120"></span>
### Add enterprise built\-in models

After you add and enable an enterprise built\-in model, all members can use this model within TRAE clients.

Follow these steps to add an enterprise built\-in model:


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Setup** \> **Models**.

3. In the upper\-right corner of the **Enterprise Built\-in Models** section, click the **Add model** button.

4. In the **Add model** window, complete the following steps:

   1. Select a model provider. The currently available providers include: AWS, Anthropic, OpenAI, Gemini, OpenRouter, Kimi\-CN, Kimi\-Global, DeepSeek, Volcano Engine, Alibaba Cloud, Tencent Cloud, Model Ark, SiliconFlow, PPIO, Novita, BytePlus, and Custom.

   2. If you select **Custom** as the model provider, enter the model name and URL.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The URL must comply with OpenAI's Chat Completions protocol specification and be entered as the API base path. The base path refers to the unified prefix of the interface and does not include specific function endpoints (such as <code>/chat/completions</code>).      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For example, if the full request URL for the model is <code>https://example.com/v1/ai/chat/completion</code>, then the URL you should enter is <code>https://example.com/v1/ai/</code>.      </div>
      

   3. Enter the API Key for authentication with this model.

   4. (Optional) In **Advanced Settings**, configure the following fields as needed:

      
      |**Field** |**Description** |
      |---|---|
      |Custom request address |If requests to this model provider need to go through other services, you can enter a custom request address here; if left blank, the system will use the official request address of the model provider by default.<br><br>***Note***: The custom request address must also comply with the above URL requirements. |
      |Context window \- Input |Set the maximum number of tokens the model can receive per request. |
      |Context window \- Output |Set the maximum number of tokens the model can generate per response. |
      |Tool call round |Set the maximum number of times the model can call tools in a single task. |
      |Support image input |When enabled, users can use images as context for chat. |
      

   5. Click the **Save** button.


<span id="6ff25cc5"></span>
### Verify the availability of Anthropic models

The availability of Anthropic models cannot be verified by sending requests directly from a browser. You need to use `curl` in your local terminal to test the API key. Use the following script:

```Bash
curl 'https://api.anthropic.com/v1/models' \
-H 'x-api-key: {{your_api_key}}' \
-H 'anthropic-version: 2023-06-01'
```


<span id="4d76999b"></span>
## Set the default model

Set the default model used by enterprise members. The default model cannot be disabled or deleted.


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Setup** \> **Models**.

3. In the **Default Model** section, set a system built\-in model as the default model.


<span id="bd043ae0"></span>
## Manage custom model permissions for members

After you enable custom model permissions for enterprise members, they can add and use custom models in TRAE IDE.

Follow these steps to enable or disable custom model permissions for your enterprise members:


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Setup** \> **Models**.

3. In the **Member\-defined Model** section, toggle the **Whether to allow members to add custom models on the TRAE IDE and plugin** switch on or off.


<span id="20923da8"></span>
## View usage

After enabling pay\-as\-you\-go, TRAE will track the number of tokens consumed beyond the quota included in the subscription plan that are subject to additional charges.

In the usage statistics dashboard on BytePlus, you can view the total token usage for models, total input token count, and total output token count.


1. Log in to the [BytePlus TRAE Console](https://console.byteplus.com/trae/overview).

2. From the left navigation bar, select **Usage statistics**.

3. Set filter conditions as needed, including model, period, and time dimension.

   The dashboard will display the corresponding data.


<span id="24a49079"></span>
## Max mode

Max mode is designed for users who require a larger context window and more complex tool invocation capabilities. After enabling Max mode, the context window of AI models expands significantly, allowing support for processing larger\-scale input.

In Max mode, the supported context window for each model in a single turn of chat is as follows:


|**Model name** |**Context window in Max mode (measured by tokens)**  |
|---|---|
|GPT\-5.4 |200k |
|GPT\-5.2 |200k |
|Gemini\-3.1\-Pro\-Preview |200k |
|Gemini\-3\-Flash\-Preview |200k |
|GLM\-4.7 |200k |
|MiniMax\-M2.7 |200k |
|Kimi\-K2.5 |200k |
|DeepSeek\-V3.2 |200k |


**Enable Max mode:** 

In the lower\-right corner of the AI chat input box, click the model name, then toggle the **Max Mode** switch on in the menu.
