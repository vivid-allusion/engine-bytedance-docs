---
title: "Managing model gateway usage"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage"
---

The model gateway allows you to control model call usage from two dimensions: Proxy API Key and model. You can set rate limits and daily/weekly/monthly token and credits quotas for a Proxy API Key, and configure tokens\-per\-minute limits and credits conversion rates for models under a provider. This prevents a single Key or model from consuming excessive resources. This topic describes how to configure model gateway token usage.

## Limits

* If model rate limiting is configured and the limit value is set to **0**, the corresponding Proxy API Key or model no longer accepts new requests.

* When token rate limits or token quotas are not configured, the system does not restrict token usage for the corresponding period or model. When credits quotas are not configured, the system does not restrict credits usage for the corresponding period.

* When token rate limits, token quotas, or credits quotas are configured, requests must satisfy all configured limits simultaneously. When any limit is triggered, the system rejects new requests and returns HTTP 429.

* A credits quota must be greater than 0 and supports up to two decimal places. Leaving it unconfigured means credits usage for the corresponding period is not restricted. Local credits quota rejection does not trigger retry or fallback.

* Concurrent requests already accepted by the system continue running, so the final measured usage may slightly exceed the configured value.

## Manage Proxy API Key token usage

You can set per\-minute rate limits and daily/weekly/monthly token quotas as well as daily/weekly/monthly credits quotas for a single Proxy API Key. A request must satisfy all configured limits simultaneously. Once any limit is triggered, the system rejects new requests.

> **warning**

> **Token quotas and credits quotas take effect independently. When either quota is exhausted, the request is rejected**.

* > **Token quota** is used to control the total number of tokens that a Proxy API Key can consume within a specified period.

* > **Credits quota** is used to control the model invocation quota that a Proxy API Key can consume within a specified period, measured by a unified credits standard.

### Prerequisites

The model service and Proxy API Key have been created. For detailed operations, see [Creating model service](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service) and [Managing model service](https://docs.byteplus.com/en/docs/agentkit/Managing_model_service).

### Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Model integration". On the "Proxy API Key management" tab, click "Edit" for the Proxy API Key to be configured.

3. On the edit page, configure Proxy API Key model rate limiting by referring to the following table.

   |Parameter​ |Description |
   |---|---|
   |Term |The name of the current Proxy API Key. It is display\-only and cannot be modified. |
   |Provider model permission |Select the scope of provider models that the Proxy API Key can call.<br><br><br>* **All provider models**: No restrictions. The key can call all models from all provider types under the current model service.<br><br>* **Custom scope**: Precisely restricts the Key to calling only specific models under a specified model provider.<br><br>   * **Provider**: When "Provider model permission" is set to  **"Custom scope"** , select the provider whose models the Proxy API Key can call.<br><br>   * **Specific model configuration**: When the  **"Provider model permission"**  is set to "Custom scope", select the list of specific models that this key is allowed to call under the selected provider.<br><br>      * You can select all target models or manually select some of them.<br><br>      * If you enable "Auto\-authorize new models", the Proxy API Key automatically gains permission to call newly added models under this provider. If you disable it, you must select new models manually. |
   |Model group permission |Configure the model groups that can be used with this key. This permission allows you to call models in the selected group, including its fallback models. The accessible scope updates when the group configuration changes.<br><br><br>* **All model groups**: Allows the key to call models configured in all model groups under the current model service.<br><br>* **Custom scope**: Select specific model groups to restrict the key to calling only the models configured in those groups. |
   |Model rate limit |Whether to set a separate rate limit for each model that the current Proxy API Key can call. The rate limit prevents any single model from being overused.<br><br>After model rate limiting is enabled, configure the **rate limit**, that is, the specific threshold for model rate limiting.<br><br><br>* **0**: Indicates that the per\-minute usable token limit is 0, and the Proxy API Key no longer accepts new requests.<br><br>* **Not configured**: Indicates that the per\-minute usable token limit is not restricted.<br><br>* **Other values**: Indicate the actual per\-minute usable token limit, in millions of TPM (tokens per minute, in units of ×10⁶). For example, entering 100 means that the Key can consume up to 100 million tokens per minute. |
   |Model quotas |Whether to set a usage quota for the models that the current Proxy API Key can call. Each period takes effect independently. The service stops when any quota is exhausted.<br><br><br>* **Token quotas** (unit: million tokens): Set the maximum total tokens this Proxy API Key can consume within a **calendar day**, **calendar week**, or **calendar month**. Quotas are automatically reset at 00:00 daily, 00:00 every Monday, and 00:00 on the 1st of each month (UTC+8).<br><br>   * **Specific value**: The service stops when cumulative consumption in the current period reaches the upper limit.<br><br>   * ****0: If the quota for the current period is 0, no new requests are accepted.<br><br>   * **Leave blank**: Token usage for the corresponding period is not restricted.<br><br>* **Credits quotas** (unit: credits): Set the maximum total credits this Proxy API Key can consume within a **calendar day**, **calendar week**, or **calendar month**. Quotas are automatically reset at 00:00 daily, 00:00 every Monday, and 00:00 on the 1st of each month (UTC+8). Credits are an internal governance unit. Before use, configure the credits conversion rate in the provider model configuration.<br><br>   * A **value greater than 0**: Enables credits quota control for the corresponding period. You can retain up to two decimal places.<br><br>   * **Leave blank**: Credits usage during the corresponding period is not restricted.<br><br>   > **tip**<br>   <br><br>   * > **Credits quota rules**: Daily, weekly, and monthly quotas are independent. After the quota for any period is exhausted, the system rejects new requests. If model quotas are enabled but all three credits quota configurations are left blank, no credits quota limit is enforced for the Proxy API Key. Any usage count already accumulated in the current period is retained.<br>   <br><br>   * > **Authorized model conversion rate:** When credits quota control is enabled, the system verifies whether models within the Proxy API Key authorized scope have a valid credits conversion rate configured. **Only when the authorized model has a valid conversion rate can the credits quota configuration be saved for the Proxy API Key**.<br>    |

4. Click "Confirm". You can then view the quota usage of the current Key in the Proxy API Key list.

5. (Optional) Reset quota. When the periodic quota usage (daily/weekly/monthly) of a key reaches 100%, the administrator can reset the quota for that period.

   1. In the Proxy API Key list, click "Reset quota" in the Actions column for the target Key.

   2. Select the quotas to reset (**Token quota/Credits quota**), select the periods to reset, and click "Confirm" to complete the operation. After the reset, the remaining quota for the corresponding period returns to 100%.

## Manage model rate limits and credits conversion rates

When multiple Proxy API Keys can be used to call the same model under the same provider, you can set a unified tokens\-per\-minute limit for that model, and this limit is shared by all Proxy API Keys that can be used to call the model. To enable credits quota control or collect credits usage statistics, configure a credits conversion rate for each model under the provider. Once configured, the system computes the corresponding credits usage based on the token usage of each actual upstream Attempt and the model rate.

### Prerequisites

A provider has been added to the model service, and model configuration has been completed. For detailed operations, see [Managing model service](https://docs.byteplus.com/en/docs/agentkit/Managing_model_service).

### Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Model integration". On the "Provider and model management" tab, click "... \> Edit" in the upper\-right corner of the card for the model provider to be configured.

3. On the edit page, configure the model information by referring to the following table.

   |Parameter​ |Description |
   |---|---|
   |Provider |The name of the current Proxy API Key. It is display\-only and cannot be modified. |
   |Term |This parameter is required only for **Custom** model providers. Enter the display name of the custom model provider, for example, DeepSeek.<br><br>> **tip**<br><br><br>> A custom\-type provider refers to any provider other than the platform's built\-in **ModelArk \- Foundation models**, **ModelArk \- AgentPlan**, and **ModelArk \- CodingPlan**.<br> |
   |Specific model configuration |Configure the models that can be called under the current provider. You can set **TPM**, **input rate**, **cache rate**, and **output rate** for each model separately. The ** input rate, cache rate, and output rate ** values range from 0 to 1000 and support up to two decimal places.<br><br>> **tip**<br><br><br><br>* > **Credits are a unified unit of measurement**used for internal enterprise usage control and**do not represent billing amounts, account balances, or model pricing.** The unit price of each model varies. Therefore, the administrator needs to configure a **conversion rate** for each model to convert the model's actual token consumption, making it easier to manage usage across models in a unified way.<br><br><br>* > **The rate** indicates the number of credits corresponding to each 1M tokens. You can configure the conversion rate with reference to the model price per million tokens and the enterprise's unified conversion ratio. The formula is: Conversion rate = price per million tokens × custom conversion coefficient of the enterprise.<br><br><br>* **Configuration descriptions**:<br><br>   * **TPM**: The upper limit of tokens\-per\-minute usage for the model, measured in millions.<br><br>   * **Input rate ** (Credits/1M Tokens): The number of credits corresponding to each 1M input tokens consumed. If this parameter is not configured, the default is 0. This means that the model input is not counted toward credits usage.<br><br>   * **Cache rate** (Credits/1M Tokens): The number of credits corresponding to each 1M cache\-hit tokens consumed.<br><br>      * **Not configured**: The cache rate is computed based on the input rate.<br><br>      * **Configured**: The cache portion is deducted from the input rate and computed based on the cache rate.<br><br>   * **Output rate** (Credits/1M Tokens): The number of credits corresponding to each 1M output tokens consumed. If this parameter is not configured, the default is 0. This means that the output for this model is not counted toward credits usage.<br><br>* **Add a model**: Enter the standard model ID that the provider offers (that is, the value of the `model `parameter passed when calling the API), for example, **` deepseek-v4-pro`**, and then click "Add". The system does not automatically retrieve the model list. To add multiple models, repeat the operation. |
   |Provider Base URL |Configure the base URL for the provider's model service. The URL must be consistent with the selected protocol and the provider's requirements.<br><br><br>* This URL is the prefix of the API endpoint for the model service. The system uses this URL to send model call requests to the provider.<br><br>* **Configuration instructions**<br><br>   When you select a built\-in ModelArk provider (**ModelArk \- Foundation models, ModelArk \- Agent Plan, or ModelArk \- Coding Plan**), the system automatically populates the corresponding default URL, **and no modification is typically required**. Manual adjustment is required in the following cases:<br><br>   * Your account uses a **privately deployed** or **dedicated cluster** ModelArk service, whose endpoint differs from the public cloud endpoint.<br><br>   * You want to route requests to a specific **regional node** or a **custom proxy**. |
   |Provider API Key |Configure the actual API Key required to access the provider's model service. This key is used for authentication when call requests are sent to the model provider. The following two methods are supported:<br><br><br>* **Select existing:**  Select from the list of API Keys already hosted under your account. This method is recommended for centralized key management and rotation.<br><br>* **Custom input:**  Manually enter a name and API Key value. This method is suitable for keys being added for the first time or used temporarily. |
   |Fallback model |Configure a fallback model to use when the current model is unavailable. If the current model encounters an access error or runs out of quota, the system will automatically switch to the fallback model. |

4. Click "Confirm". After the configuration is complete, on the "Provider and model management" tab, click the target model provider card to view the model rate limiting information in the details.
