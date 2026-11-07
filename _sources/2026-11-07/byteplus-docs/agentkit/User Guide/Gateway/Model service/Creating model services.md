---
title: "Creating model services"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Creating_model_service"
---

The model service provides centralized management of configurations, including model providers, provider API Keys, model IDs, Proxy API Keys, model access scopes, retry policies, and fallback models. If you need to centrally manage multiple model providers, isolate call credentials by application, or assign different model access scopes to different applications, you can create the model service. This allows your applications to call authorized models through a unified endpoint and Proxy API Keys, without maintaining the actual credentials of multiple providers directly on the application side. This topic describes how to create and manage the model service, including creating the model service, adding providers and models, configuring Proxy API Keys, and setting model access scopes and rate limits.

## Instructions

In multi\-model, multi\-provider scenarios, applications typically need to maintain separate endpoints, model IDs, and API Keys for each provider. As the number of integrated models grows, credential management, access control, rate limit configuration, and call log troubleshooting all become increasingly complex.

**The model service** provides a unified model call entry point. In the console, you can integrate model providers, host provider API Keys, create Proxy API Keys, and configure model access scopes and rate\-limiting policies for different applications or scenarios. **The model service** uses provider API Keys to call upstream model services. When an application calls the model service, it only needs to use the endpoint and Proxy API Keys provided by the model service, without storing provider API Keys directly.

## Prerequisites

Before managing the model service, make sure your account, gateway, and provider and model information are ready. If any of the following conditions are not met, you may not be able to complete the creation.

* You have[ created a gateway instance](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en). When creating the model service, you must specify a gateway instance as the traffic entry point for model requests. **The model service itself does not incur fees, but the gateway instance associated with the model service incurs fees**. For details, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

* (Optional) A Proxy API Key authorization policy has been confirmed. Create separate Proxy API Keys for different applications or scenarios to control the model access scope for different callers and achieve access isolation.

* (Optional) Model\-related information has been obtained in advance. If you are integrating a model service not provided by ModelArk (such as OpenAI, Anthropic, or a self\-hosted model), prepare the following information:

   * **Provider information**: provider name, base URL, protocol type, and API Key.

   * **Model ID**: The standard model ID provided by the provider. The model service routes requests to the upstream model based on this ID. Using a non\-standard ID may cause model calls to fail.

## Create a model service

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation tree, select "Gateway \> Model integration" and click the "Create model service" button.

3. On the "Create model service" page, complete the gateway configuration, model configuration, and Proxy API Key configuration.

   > **tip**

   > When adding a model, you can select the following provider types: **ModelArk \- Foundation models**, **ModelArk \- Agent Plan**, **ModelArk \- Coding Plan**, or **Custom**. The "Custom" type requires you to manually enter the provider name, base URL, protocol, and API Key. Its parameters differ from those of the other three types. Configure the parameters as described in the following table.

   * **Model provider: ModelArk \- Foundation models**, **ModelArk \- Agent Plan**, or **ModelArk \- Coding Plan**

      |Parameter​ |Description |
      |---|---|
      |**Gateway configuration** ||
      |Gateway instances |Select the dedicated gateway instance used by the model service. |
      |**Model configuration** ||
      |Provider |Select a model provider. The provider is **ModelArk \- Foundation models**, **ModelArk \- Agent Plan**, or **ModelArk \- Coding Plan**.<br><br><br>* **Type description**<br><br>   * **ModelArk \- Foundation models**: Uses public models available in the  "Foundation models". After selecting this option, you can directly select the required models from the model list.<br><br>   * **ModelArk \- Agent Plan**: Uses model resources under the  Agent Plan. This option is suitable for agent scenarios. After selecting this option, you can directly select the required models from the corresponding model list.<br><br>   * **ModelArk \- Coding Plan**: Uses model resources under the  Coding Plan. This option is suitable for programming scenarios such as code generation and code understanding. After selecting this option, select the required models from the corresponding model list.<br><br>* **How to choose**:<br><br>   * To integrate models already available on ModelArk, such as Doubao or DeepSeek, select **ModelArk \- Foundation models**.<br><br>   * If you have purchased an Agent Plan or Coding Plan resource package, select **ModelArk \- Agent Plan or ModelArk \- Coding Plan**. |
      |Specific model configuration |Select the specific models to integrate with the model service. By default, all models are selected. You can modify the tokens\-per\-minute (TPM) limit for a model after you create the model service. For details, see [Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage). |
      |Provider Base URL |Configure the base URL for the provider's model service. The URL must be consistent with the selected protocol and the provider's requirements.<br><br><br>* This URL is the prefix of the API endpoint for the model service. The system uses this URL to send model call requests to the provider.<br><br>* **Configuration instructions**<br><br>   When you select a built\-in ModelArk provider (**ModelArk \- Foundation models, ModelArk \- Agent Plan, or ModelArk \- Coding Plan**), the system automatically populates the corresponding default URL, **and no modification is typically required**. Manual adjustment is required in the following cases:<br><br>   * Your account uses a **privately deployed** or **dedicated cluster** ModelArk service, whose endpoint differs from the public cloud endpoint.<br><br>   * You want to route requests to a specific **regional node** or a **custom proxy**. |
      |API Key |Configure the actual API Key required to access the provider's model service. This key is used for authentication when call requests are sent to the model provider. The following two methods are supported:<br><br><br>* **Select existing:**  Select from the list of API Keys already hosted under your account. This method is recommended for centralized key management and rotation.<br><br>* **Custom input:**  Manually enter a name and API Key value. This method is suitable for keys being added for the first time or used temporarily. |
      |Fallback model |Configure a fallback model to use when the current model is unavailable. If the current model encounters an access error or runs out of quota, the system will automatically switch to the fallback model. **You can skip this parameter for now and configure it after you create the model service**. |
      |**Proxy API Key configuration** ||
      |Term |Enter a name for the Proxy API Key to distinguish and manage different keys on the "Proxy API Key management" page.<br><br><br>* A Proxy API Key is the unified access credential exposed by the model service. Callers (such as agents or third\-party applications) use this key to send requests to the model service, which proxies and forwards the requests to the actual provider model. Callers do not need to hold the provider's original API Key directly, achieving key isolation and centralized control.<br><br>* After you enter a name, the system automatically generates the corresponding key value. Once the model service is created, you can view and manage the Proxy API Key on the "Proxy API Key management" tab. |
      |Available models |Set the scope of models that the Proxy API Key is allowed to call. The default scope is **All models**, which means all models configured under the model service can be called. You can modify the Proxy API Key usage limit after you create the model service. For details, see [Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage). |
      |**Other** ||
      |Failure retry count |Configure the number of retries after a model call fails. If a model call fails, the model service will automatically retry the specified number of times. |

   * **Model provider**: ** Custom**

      |Parameter​ |Description |
      |---|---|
      |**Gateway configuration** ||
      |Gateway instances |Select the gateway instance used by the model service. |
      |**Model configuration** ||
      |Provider |Select a model provider. The "Provider" parameter is set to **Custom**.<br><br><br>* Manually enter the provider name, base URL, protocol, and API Key to integrate a third\-party model service or a privately deployed model service.<br><br>* The "Custom" provider type is suitable for integrating model services not provided by ModelArk, such as OpenAI, Anthropic, or self\-hosted models. |
      |Term |Enter a configuration name for the custom provider.<br><br><br>* This name is only used to identify the provider in the model service console and does not affect the actual integration or calls.<br><br>* We recommend that you enter a name that reflects the provider's source or purpose, such as `openai-gpt4o` or `my-private-llm`. |
      |Specific model configuration |Configure the models that can be called under the current provider. Enter the standard model ID provided externally by the current provider in the text box (that is, the value of the `model` parameter passed when calling the API), for example, `deepseek-flash`, and then click "Add".<br><br><br>* The system does not automatically retrieve the model list. To add multiple models, repeat the operation.<br><br>* You can modify the model rate limit after you create the model service. For details, see [Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage). |
      |Provider Base URL |Enter the base URL for the provider's model service. The URL must be consistent with the selected protocol and the provider's requirements.<br><br><br>* This URL is the prefix of the API endpoint for the model service. The system uses this URL to send model call requests to the provider.<br><br>* Enter the full API base URL for the third\-party model service or privately deployed model, such as `https://api.openai.com/v1`. |
      |Protocol |Select the provider API protocol. **Compatible with OpenAI** and **Compatible with Anthropic** are supported.<br><br><br>* **Compatible with OpenAI**: This protocol is suitable for model services that are compatible with the OpenAI protocol. The model access URL must be an OpenAI\-compatible base URL, such as `https://<your-provider-domain>/v1`.<br><br>* **Compatible with Anthropic**: This protocol is suitable for model services that are compatible with the Anthropic protocol. The model access URL must be an Anthropic\-compatible base URL, such as `https://<your-provider-domain>`. |
      |API Key |Configure the actual API Key required to access the provider's model service. This key is used for authentication when call requests are sent to the model provider. |
      |Fallback model |Configure a fallback model to use when the current model is unavailable. If the current model encounters an access error or runs out of quota, the system will automatically switch to the fallback model. You can skip this parameter for now and configure it after you create the model service. For details, see[ Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage). |
      |**Proxy API Key configuration** ||
      |Term |Enter a name for the Proxy API Key to distinguish and manage different keys on the "Proxy API Key management" page.<br><br><br>* A Proxy API Key is the unified access credential exposed by the model service. Callers (such as agents or third\-party applications) use this key to send requests to the model service, which proxies and forwards the requests to the actual provider model. Callers do not need to hold the provider's original API Key directly, achieving key isolation and centralized control.<br><br>* After you enter a name, the system automatically generates the corresponding key value. Once the model service is created, you can view and manage the Proxy API Key on the "Proxy API Key management" tab. |
      |Available models |Set the scope of models that the Proxy API Key is allowed to call. The default scope is **All models**, which means all models configured under the model service can be called. You can modify the Proxy API Key usage limit after you create the model service. For details, see [Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage). |
      |**Other** ||
      |Failure retry count |Configure the number of retries after a model call fails. If a model call fails, the model service will automatically retry the specified number of times. |

4. After configuration, click the "Confirm" button.

   After you create a model service, you can provide multiple upstream models under a single invocation name and route them by weight. For more information, see [Creating and managing model groups](https://docs.byteplus.com/en/docs/agentkit/create-and-manage-model-group).

> **tip**

> After the model service is created, if a model is unavailable, first verify that the gateway instance, provider API Key, and provider model ID are entered correctly. If any issues are found, go to the "Provider and model management" tab, click "**...** \> Edit" in the upper\-right corner of the target provider card, and update the model configuration.
