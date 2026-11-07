---
title: "Model management"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Model_management"
---

ArkClaw Enterprise supports centralized configuration and management of models in a space. On the model details page, administrators can configure the default models and available models for employee Claws, Enterprise service agent, and the knowledge center to meet requirements in different scenarios.

## Model configuration overview

* **Employee Claw models**: Configure models by seat edition (Starter, Standard, Advanced, and Ultimate) to manage the models available to employee Claw instances.

   > **warning**

   * > Administrators can configure chat models and memory embedding models for Claw instances based on the seat edition (Starter, Standard, Premium, or Ultimate). **This configuration determines only the range of chat models available in the employee workspace.**When using skills, Claw instances may also call Coding Plan, Agent Plan, and other multimodal models listed in the Foundation models.

   * > Note that **adding a chat model in the model configuration does not mean the model already has the invocation permissions, nor does it mean that the model has been configured with a quota**. The invocation permissions and quota for models are uniformly managed by the ModelArk platform. If administrators need to manage model\-related permissions and quotas, go to the [ModelArk](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=model&projectName=default) console.

* **Enterprise service agent models**: Configure models separately for enterprise service agents used by teams. These models are shared across teams or business scenarios, and their configuration is managed independently of employee Claw models.

* **Knowledge Center models**: Configure chat models and Embedding models for knowledge bases. This affects knowledge retrieval and Q&A results. Knowledge Center models are part of the basic space configuration and can currently be viewed but not configured.

## Configure employee Claw models

### Configuration instructions

|**Chat model** |**Memory Embedding model** |
|---|---|
|The models used by ArkClaw instances to process tasks. The model settings include the model source and the model type available for different seat editions. Four model sources are currently supported: **Agent Plan Team**, **Coding Plan Team**, Foundation models, and **Custom models**.<br><br><br>* **Agent Plan Team**: Models sourced from ModelArk Agent Plan.<br><br>* **Coding Plan Team**: Models sourced from ModelArk Coding Plan.<br><br>* **Foundation model**: Foundation models.<br><br>* **Custom model**: User\-defined models. |For a performance comparison between offline and online Embedding models, see [ArkClaw memory performance](https://docs.byteplus.com/en/docs/ArkClaw/Analysis_of_ArkClaw_memory_capability).<br><br><br>* **Agent Plan Team**: Uses the online Embedding model **doubao\-embedding\-vision** from Agent Plan.<br><br>* **Coding Plan Team**: Uses the online Embedding model **doubao\-embedding\-vision** from Coding Plan.<br><br>* **Foundation models**: Uses the online Embedding model **doubao\-embedding\-vision** from the Foundation models.<br><br>* **Basic model** (default): Uses the basic Embedding model **bge\-small\-zh\-v1.5**. |

### Configuration rules

* **General rules**

   * **Effective scope of model configurations:**  If the model configurations are modified, the new model configurations take effect only for newly created Claw instances by default. To apply the new configurations to existing Claw instances, enterprise administrators can deliver the latest model configurations in a unified manner. For detailed instructions, see [Switching models uniformly for Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Bulk_switching_models_for_Claw_instances).

* **Special model rules**

   * **Configuration rules**

      * **Quantity limit**: Each seat edition requires a minimum of **1** model source and supports a maximum of **4**.

      * **Default model**: **One** model needs to be specified as the default model for each seat edition.

      * **Employee use**: Multiple available models can be added for each model source.

         * **Coding Plan Team, Foundation models**, and **custom models:**  If only **1** model is configured, employees can only use that model. If multiple models are configured, employees can select and switch between them as needed.

         * **Agent Plan Team:**  If models from the AgentPlan are used, the following models are enabled by default:  deepseek\-v4\-flash (default model), deepseek\-v4\-pro, Dola\-Seed\-2.0\-pro, Dola\-Seed\-2.0\-lite, Dola\-Seed\-2.0\-Code, Skylark\-embedding\-vision, Dreamina\-Seedance\-2.0, Dreamina\-Seedance\-2.0\-fast, Dola\-Seedream\-5.0\-lite.

   * **Switch model sources**

      * If the configured model sources for a seat edition are fewer than **4**, switching can be done according to the following rules:

         * **Source without the default model**: You can directly switch to another model source.

         * **Source with the default model**: You cannot directly switch to another model source. (To switch to another model source, specify one model as the default model in the target source first, and then switch the source.)

   > **tip**

   > For example, if the current default model comes from the Foundation models and you want to replace the entire "Foundation models" group, you need to first select a model from another source (such as "Coding Plan") and set it as the default, then change the "Foundation models" source.

   * **About models from ModelArk Plan**

      * To configure models from ModelArk Plan (Agent Plan Team or Coding Plan Team), you must have **purchased or managed Agent Plan Team or Coding Plan Team resources**. For detailed instructions, see [Managing ModelArk Plans](https://docs.byteplus.com/en/docs/ArkClaw/Managing_CodingPlan).

      * To use ModelArk Plan models on the employee side, **the administrator must have configured ModelArk Plan models**, and **employees must have been allocated ModelArk Plans**. The details are as follows:

         * **ModelArk Plan allocated**: If an employee has been allocated a ModelArk Plan, the employee can use models from the plan normally.

         * **ModelArk Plan not allocated**: If an employee has not been allocated a ModelArk Plan, the employee can use only models from the "Foundation models" source and custom sources.

### Procedure

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar​, click "Space Overview".

3. In the "Model details" section, click the "Employee Claw model" tab and then click "Configuration".

4. Configure models as needed based on the following table. After the configuration is complete, click "Confirm".

   > **tip**

   > You can modify model settings at any time. The modified settings take effect based on the following rules:

   * > **Claw instance models**: After the configuration is modified, newly requested ArkClaw instances automatically use the new configuration. For existing ArkClaw instances, employees must manually switch models in Settings for the modified configuration to take effect. To apply the modified configuration to existing Claw instances, uniformly deliver the latest model configuration. For more information, see [Switching models uniformly for Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Bulk_switching_models_for_Claw_instances).

   * > **Memory Embedding models**: Model configuration changes take effect only for newly requested ArkClaw instances. They do not apply to existing ArkClaw instances.

   |Parameter |Configuration instructions |
   |---|---|
   |Chat model |Configure primary chat models available for **Claw instances** and **desktop clients**. Claw instance models are used for Claw instance conversations, and desktop client models are used for local assistants and local application operations.<br><br><br>* **Add model source:**  Add available models to the purchased seat editions.<br><br>   1. Click "Add model source" below the target seat edition.<br><br>   2. Select a model source and add models. To add models from a custom source, refer to the [Configure custom model pools](https://docs.byteplus.com/en/docs/ArkClaw/Model_management?TagIDs=2,522,512,502&lang=en#ki5b7RN3) section of this topic.<br><br>      > **tip**<br>      <br><br>      > The desktop client does not support custom models. It supports only models from the Foundation models and ModelArk Plan (Agent Plan Team and Coding Plan Team).<br>      <br><br>   3. Click "Set as default" next to a model to specify the model as the default model.<br><br>* **Enable backup model**: After this feature is enabled, if an exception occurs on the current model or the quota is used up, the system will automatically switch to the backup model.<br><br>   > **tip**<br>   <br><br>   * > A fallback model can be enabled only when the **default model** source is Foundation models, Coding Plan Team, or Agent Plan.<br>   <br><br>   * > Only backup models from "Foundation models" are supported, and only one model can be configured.<br>   <br><br>   1. Switch on "Enable backup model".<br><br>   2. Select a backup model. |
   |Embedding model |The models are used for ArkClaw memory retrieval and recall to improve task success rates. You need to configure Embedding models separately for different seat editions.<br><br><br>1. On the "Model configuration" page, click the edit icon in the upper\-right corner of the "Embedding model" section.<br><br>2. Configure the Embedding model used by different seat editions. After the configuration is complete, click "Confirm" to complete the operation. |
   |Picture models |An image model is used to process static image data in ArkClaw. The image model defaults to the **doubao\-seedream\-5.0\-lite** model from AgentPlan. Administrators can switch to other model sources as needed. |
   |Video models |This model is used by ArkClaw to process video data with a time dimension. By default, the available video models are doubao\-seedance\-2.0, doubao\-seedance\-2.0\-fast, and doubao\-seedance\-1.5\-pro from AgentPlan, with **doubao\-seedance\-2.0** set as the default model. |
   |Model throttling configuration |In the "Model throttling configuration" section of the model configuration page, enter the per\-minute and daily token limits for a single employee.<br><br>> **tip**<br><br><br>> This throttling configuration applies to all employees. To adjust the throttling configuration for some employees, you can configure it on the "Seats" page. For details, see [Editing employee seat quotas](https://docs.byteplus.com/en/docs/ArkClaw/Managing_employee-level_seat_settings?lang=en#Wwp77Heu).<br> |

## Configure enterprise service agent models

### Configuration rules

* **Model source**

   * **Conversation models** (chat models) support models from the "Foundation models" and "Custom" sources. Models from custom sources support only API keys uniformly configured by the enterprise.

* **Rate limiting**

   * **Model access by all enterprise service agents in a space is rate\-limited as a whole based on the space's rate\-limiting configuration**. The total rate limit increases linearly with the space's default per\-employee rate limit. If rate limiting occurs, the enterprise administrator can increase the space's default rate limit.

* **Switch model sources**

   * If fewer than **2** model sources are configured for a seat edition, you can switch model sources based on the following rules:

      * **Source without the default model**: You can directly switch to another model source.

      * **Source with the default model**: You cannot directly switch to another model source. (To switch to another model source, specify one model as the default model in the target source first, and then switch the source.)

      > **tip**

      > For example, if the current default model comes from the Foundation models and you want to replace the entire "Foundation models" group, you need to first select a model from another source (such as "Custom") and set it as the default, then change the "Foundation models" source.

### Procedure

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar​, click "Space Overview".

3. In the "Model details" section, click the "Enterprise service agent model" tab and then click "Configuration" in the upper\-right corner.

4. In the "Conversation model" section, click "Add model source".

5. Select the model source and then the target models. You must select one as the default model.

   > **tip**

   > Only models from the **Foundation models** and **Custom** sources can be added. To add a model from a custom source, see [Configuring custom model pools](https://docs.byteplus.com/en/docs/ArkClaw/Model_management?TagIDs=2,522,512,502&lang=en#ki5b7RN3).

   6. After the configuration is complete, click "Confirm".

## Configure custom model pools

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar​, click "Space Overview".

3. In the "Model configuration" section, click "Edit" in the upper\-right corner.

4. Click "Add model source" below any seat edition.

5. Add a "Custom" model source. Then, click "Manage custom model" at the bottom of the Custom drop\-down box.

6. Add a model pool based on the following table.

   |Parameter​ |Description |
   |---|---|
   |Model pool name |Click the edit icon to change the name of the model pool. The default model pool name is "Model pool 1". |
   |Model name |Enter the name of the custom model.<br><br><br>* At least one model needs to be configured for each model pool. You can configure multiple models.<br><br>* To configure multiple models, click "Add" and add the name of each model separately.<br><br><br>> **warning**<br><br><br>> Enter the **standard model name** provided by the model vendor. **Do not enter a custom model name**.<br> |
   |Model API Key source |Select the API key source of the custom models.<br><br><br>* **Unified configuration by enterprise admin**: When a model pool is added, the enterprise administrator provides the API key. Employees do not need to provide the API key when using custom models.<br><br>* **Configured by employees**: When a model pool is added, the enterprise administrator does not need to provide the API Key. Employees need to provide the API Key when using custom models. |
   |API protocol |Select an API protocol type. The requirements for the model access address vary based on different types of API protocols.<br><br><br>* **OpenAI**: This protocol applies to model services that are compatible with the OpenAI protocol. The model access URL must be an OpenAI\-compatible Base URL, such as `https://<your-provider-domain>/v1`.<br><br>* **Anthropic**: This protocol applies to model services that are compatible with the Anthropic protocol. The model access address must be an Anthropic\-compatible Base URL, such as `https://<your-provider-domain>`. |
   |Call Methods |The supported invocation methods for a custom model's API protocol depend on the selected interface protocol.<br><br><br>*  **"OpenAI" API protocol**: Supports "openai\-completions" and "openai\-responses".<br><br>   * **openai\-completions**: This method applies to model services that are compatible with the Chat Completions API. This method requires including the full conversation messages in each request. It generally offers wider compatibility and is suitable for scenarios where universal compatibility is the priority.<br><br>   * **openai\-responses**: This method applies to model services that are compatible with the Responses API and is suitable for scenarios where the target model service explicitly supports the Responses API.<br><br>*  **"Anthropic" API protocol**: Only "anthropic\-messages" is supported. |
   |Access address/Access address & API Key |Enter the model access address that meets the requirements of the selected "API protocol" type.<br><br><br>* If the "Model API key source" parameter is set to "Unified configuration by enterprise admin", you need to enter an API key.<br><br>* To add multiple model access addresses, click "Add" to add them separately. |
