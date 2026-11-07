---
title: "Creating and granting permissions on model groups"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-and-manage-model-group"
---

A model group combines multiple integrated upstream models into a stable call entry point. In the `model` field of the request, enter the call name of the model group. The model gateway selects an upstream model within the group based on the configured weights. If retries within the group fail, the gateway can call the fallback model. Model groups are suitable for scenarios that require multi\-provider traffic distribution, smooth switching, or a unified model name for business applications. This topic describes how to create and manage model groups.

## Limits

* Before creating a model group, you need to integrate at least one provider model on the "Provider and model management" tab. For related operations, see [Managing providers and models](https://docs.byteplus.com/en/docs/agentkit/Managing_model_service?lang=en#cdWPqRAN).

* A model group must be created separately. Its permissions must be granted to a Proxy API Key separately. Permissions already granted for specific provider models will not automatically allow access to model groups.

* After you save the model group configuration, the changes take effect immediately for new requests. Requests that are already in progress continue to use the configuration snapshot captured when they started.

## Create a model group

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Gateway \> Model integration" to go to the "Model service" page.

3. Click the "Model Group Management" tab and then click "Create Model Group".

4. Configure the model group information.

   |Parameter |Description |
   |---|---|
   |Model group name |Enter the name of the model group.<br><br>This name uniquely identifies the model group for calls. When an application calls the model group, enter this name in the `model` field of the request. You do not need to specify a provider. We recommend using a name that reflects the business purpose, such as `coding-fast`. |
   |Group models |Select the models configured in the model group. You can select one or more upstream models from providers that have been integrated. If the target model is not available, add a new model under an existing provider, or configure a new provider and model.<br><br><br>* For instructions on adding a model, see [Managing providers and models](https://docs.byteplus.com/en/docs/agentkit/Managing_model_service?lang=en#cdWPqRAN).<br><br>* You can add only one model under one model provider as an upstream model at a time, and configure up to **five** upstream models in each model group.<br><br>* Each upstream model consists of a provider, a model ID, and a weight.<br><br>   * **Provider**: Select a configured model provider.<br><br>   * **Model ID**: Select a model that has been configured under the model provider.<br><br>   * **Weight**: The gateway selects an upstream model based on the weight ratio of each model. A larger weight value indicates a higher priority. When the weight is **0**, requests stop being distributed to the upstream model. |
   |Failure handling |The number of in\-group retries is determined by the unified settings of the model service.<br><br><br>* After an upstream model fails to be called, the gateway first retries within the group based on this setting.<br><br>* All models in the group share this retry quota. Retries are counted per model group: the number of failed retries within the group as a whole, not the number of failed calls for any individual model. |
   |Fallback model |Optional. When in\-group retries fail after retries, the gateway calls the fallback model at most once. |

4. Click "Save" to create the model group. After the model group is created, you can view its information on the "Model Group Management" tab.

5. (Optional) After the model group is created, click "Edit" in the "Actions" column to adjust its name, in\-group models, weights, and other information. After modification, click "Confirm" to save the changes. The modified model group only affects new requests.

6. (Optional) If you no longer need to use the model group, click "Delete" in the "Actions" column. Then, click "Delete" again in the message that appears to delete the model group.

   > **warning**

   > Before deleting a model group, confirm that no application continues to send requests using this call name, and remove any Proxy API Key authorizations that you no longer need. After the model group is deleted, calls using this name will fail.

## Authorize a Proxy API Key to call a model group

> **warning**

> An application can call a model group only with an authorized Proxy API Key.

1. On the "Model service" page, click the "Proxy API Key management" tab, and click "Edit" in the "Actions" column that corresponds to the target Key.

2. For the "Vendor model permission" parameter, select "All vendor models".

3. For the "Model group permission" parameter, if you want to configure only some model groups, select "Custom scope", and then select the model groups that can be called. If you do not want to restrict model groups, select "All model groups".

4. Click "Confirm" in the lower\-right corner to save the configuration. After returning to the list, you can check the "Callable models" column to see which model groups this key is authorized to call and the number of models in each group.
