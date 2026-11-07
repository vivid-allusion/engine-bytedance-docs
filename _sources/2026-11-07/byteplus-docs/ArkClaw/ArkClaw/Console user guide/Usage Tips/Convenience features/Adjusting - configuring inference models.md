---
title: "Adjusting/configuring inference models"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_configuring_inference_models"
---

ArkClaw supports subscriptions to either the **Agent Plan or Coding Plan**, as well as models available in the **ModelArk Foundation models**. It also allows custom integration with large model services provided by third\-party vendors such as DeepSeek, fully meeting your personalized inference requirements. You can flexibly adjust and configure the required models as needed based on your current subscription status.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This topic may contain information about third\-party products, which is provided for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.</div>


* <div data-tips="true" data-tips-type="default">If you have created an agent team for ArkClaw, in addition to configuring an inference model for the primary agent, you can also configure independent inference models for other agents in the team. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring_models_for_agents_in_teams">Learn more</a>.</div>



<span id="24p19vup"></span>
## Limits

The range of model sources configurable in ArkClaw varies based on your subscribed large model subscription package (Agent Plan and Coding Plan).

<mark>
|**Subscription status** |**Supported model configuration source** |
|---|---|
|Not subscribed to any package |Agent Plan, Foundation models, Custom model configuration, and Trial token quota |
|Subscribed to the Agent Plan ||
|Subscribed to the Coding Plan |Coding Plan, Foundation models, Custom model configuration, and Trial token quota |
|Subscribed to both packages |Agent Plan, Coding Plan, Foundation models, Custom model configuration, and Trial token quota |
</mark>

<span id="dkWSWjYz"></span>
## Prerequisites

If you need to **integrate a large model service provided by a third\-party vendor**, ensure that you have access to the target model service and have prepared the **model name**, **Base URL**, and **API Key** for authentication in advance.

This topic uses DeepSeek, GLM, Kimi, and Qwen as examples to describe how to obtain the relevant information:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Protocol compatibility limits:</strong> ArkClaw currently only supports integrating API Base URLs that are compatible with the OpenAI standard protocol.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Service and billing declaration:</strong> You need to prepare and maintain the integrated third\-party large model services yourself. ArkClaw only provides a unified call channel. It <strong>does not </strong>provide the API Keys or Token quotas for third\-party models.</div>




|Third\-party model |Configuration parameters and acquisition methods |
|---|---|
|DeepSeek |* Model name: Visit the official DeepSeek website to obtain it. For details, see [Model list](https://api-docs.deepseek.com/zh-cn/quick_start/pricing).<br><br>* Access address: https://api.deepseek.com<br><br>* API Key: Refer to [DeepSeek API Key guide](https://api-docs.deepseek.com/zh-cn/) or log in to the DeepSeek console to obtain it. |
|GLM (Zhipu AI) |* Model name: Visit the official Zhipu website to obtain it. For more information, see [Model list](https://bigmodel.cn/dev/howuse/model).<br><br>* Access address: https://open.bigmodel.cn/api/paas/v4/<br><br>* API Key: Refer to [Getting started](https://docs.bigmodel.cn/cn/guide/start/quick-start) or log in to the GLM console to obtain it. |
|Kimi (Moonshot AI) |* Model name: Visit the official Moonshot website to obtain it. For details, see [Model list](https://platform.moonshot.cn/docs/introduction#%E6%A8%A1%E5%9E%8B%E5%88%97%E8%A1%A8).<br><br>* Access address: https://api.moonshot.cn/v1<br><br>* API Key: Refer to [Obtaining an API Key ](https://platform.moonshot.cn/docs/introduction#%E8%8E%B7%E5%8F%96-api-%E5%AF%86%E9%92%A5)or log in to the Kimi console to obtain it. |
|Qwen (Tongyi Qianwen) |* Model name: Visit the official Alibaba Cloud website to obtain it. For details, see [Model list](https://help.aliyun.com/zh/model-studio/models).<br><br>* Access address: https://dashscope.aliyuncs.com/compatible\-mode/v1<br><br>* API Key: Refer to [How to Get API Key](https://help.aliyun.com/zh/model-studio/get-api-key) or log in to the Qwen console to obtain it. |


<span id="je1LDg6j"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/management).

2. Go to the target ArkClaw page.

3. Switch or configure models as needed.

   * **Switch models**

      Switch between model services that your current account has subscribed to or is authorized to access for different business scenarios.

      1. In the ArkClaw interaction interface, click the current model name.

      2. Select the source channel for the target model (for example, Agent Plan and "Foundation models"), and click the target model in the corresponding model list to switch to the model.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The model source channel is associated with account subscription permissions. Only subscribed model service channels are displayed.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">To subscribe to or authorize access to other models if the current model does not meet your needs, refer to "Configure the model" in the next step.         </div>
         

   * **Configure the model**

      1. Click the current model name and select the "Settings" button.

      2. In the "Model configuration" pop\-up window, select the target model and refer to the table below to configure the relevant parameters. ArkClaw allows you to select a model from the following five channels: "Agent Plan", "Coding Plan", "Foundation models", "Custom model configuration", and "Trial token quota".

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The Agent Plan is a brand\-new upgraded subscription package built on the basis of the Coding Plan. It is recommended as the preferred option.         </div>
         

         
         |Model source |Operation and description |
         |---|---|
         |Agent Plan |Subscribe to the Agent Plan package to provide ArkClaw with stable large model inference capability.<br><br><br>1. (Optional) Click the "[Go to activate](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=subscribe)" button and select the Agent Plan package you want to subscribe to. For the models supported by Agent Plan and model selection recommendations.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Configuration is required only if you have not subscribed to the Agent Plan package.   </div><br>   <br><br>2. Click the "Agent Plan" card, and select the target model and its corresponding API Key from the drop\-down list.<br><br>3. Click the " Confirm" button to complete the operation. |
         |Coding Plan |Adjust the subscribed Coding Plan package to provide ArkClaw with stable large model inference capability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you are <strong>not subscribed</strong> to the Coding Plan, you will not be able to configure models supported by the Coding Plan.</div><br><br><br><br>1. Click the "Coding Plan" card, and select the target model and its corresponding API Key from the drop\-down list. For the models supported by Coding Plan and model selection recommendations, refer to [Supported models](https://docs.byteplus.com/en/docs/ModelArk/1925114#51b87c17).<br><br>2. Click the " Confirm" button to complete the operation. |
         |Foundation models |Use a large model from the ModelArk [Foundation models](https://console.byteplus.com/ark/region:ark+cn-beijing/model?groupType=ModelGroups&vendor=Bytedance&view=DEFAULT_VIEW) as the inference large model for ArkClaw.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using models from ModelArk "Foundation models" <strong>will not consume</strong> your Coding Plan quota. You will be charged based on token usage.</div><br><br><br><br>1. Click the "Foundation models" card, and select the target model and its corresponding API Key from the drop\-down list.<br><br>2. Click the " Confirm" button to complete the operation. |
         |Custom model configuration |You can customize third\-party large models to be integrated to provide underlying inference services for ArkClaw. In this section, "DeepSeek\-V3.2" is used as an example for integration.<br><br><br>1. Click the "Custom model configuration" card.<br><br>2. Enter the model name, access address, and API Key for authentication.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Ensure that the model name, access address, and API Key are strictly matched and not mixed (e.g., using a DeepSeek access address with a Zhipu AI API Key). Otherwise, authentication failure or call errors occur.   </div><br>   <br><br>   * **Model name**: Enter the target large model name, such as "DeepSeek\-V3.2". For details, refer to [Prerequisites](https://docs.byteplus.com/en/docs/394/103369#dkWSWjYz).<br><br>   * **Access address:**  Enter the API interface call address (Base URL) of the target model service, such as "https://api.deepseek.com". For details, refer to [Prerequisites](https://docs.byteplus.com/en/docs/394/103369#dkWSWjYz).<br><br>   * **API Key:**  Enter the authentication key (API Key) used to call and access the target model service, such as "sk\-j08hbgg5h3\*\*\*\*". For details, refer to [Prerequisites](https://docs.byteplus.com/en/docs/394/103369#dkWSWjYz).<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The API Key will be used as an important credential for configuring ArkClaw's underlying model call service, granting full access permission to the model. Keep it safe and prevent leakage. If the API Key is leaked, it may cause unauthorized use of your model call quota or other security risks.      </div><br>      <br><br>3. Click the " Confirm" button to complete the operation. |
         |Trial token quota |Use the trial token quota to provide underlying inference services for ArkClaw.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After you <a href="https://docs.volcengine.com/docs/87732/2253818">purchase ArkClaw</a>, the platform automatically allocates a free trial token quota of 50M each month. The <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-lite">Doubao\-Seed\-2.0\-lite</a> model from the ModelArk Foundation models is configured by default for your trial use.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Quota consumption and switch rules</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>If you have purchased the large model subscription package (Agent Plan),</strong> the platform will deduct quota from the package first. You can also manually switch to the <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-lite">Doubao\-Seed\-2.0\-lite</a> model as needed to use the free trial quota.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>If you do not have the subscription package,</strong> the platform will consume the free trial quota by default. Once your trial token quota runs out, you may <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&_vtm_=a106466.b106468.0_0.0_0.0.366_7613594367911118351&advancedActiveKey=agentPlan">upgrade to Agent Plan</a> or <a href="https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_configuring_inference_models">modify the model configuration</a> to obtain more exclusive quota and higher configuration.</div><br><br><br>1. Click the "Trial token quota" card.<br><br>2. Confirm that there is still trial token quota available, and click the "Confirm" button to complete the operation. |
