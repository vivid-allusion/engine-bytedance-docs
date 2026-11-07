---
title: "Managing model service"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Managing_model_service"
---

After a model service is created, you can go to its details page to manage providers, models, model groups, and Proxy API Keys. You can also view logs and monitoring data, or delete the model service. This topic describes the routine management operations for the model service after it is created.

## Prerequisites

Make sure that you have logged in to the AgentKit console and created the model service. For more information, see [Creating model service](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service).

## Recommendation

* Do not store provider API Keys or Proxy API Keys in plain text in documentation, code repositories, logs, or tickets.

* Create separate Proxy API Keys for different applications or use cases to avoid sharing a single key across all applications.

* For Proxy API Keys used in production environments, use a **custom scope** and grant access only to the required models, following the principle of least privilege.

* A model group must be granted to a Proxy API Key separately. Provider model call permissions do not automatically extend to model groups.

* Regularly review Proxy API Key usage and delete keys that are no longer in use.

* If a key is suspected to have been leaked, disable it immediately.

* Configure model rate limiting to prevent excessive resource consumption caused by abnormal calls.

## Procedure

### Manage providers and models

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Model integration" and click the "Provider and model management" tab.

3. On the "Provider and model management" tab, you can perform the following operations: view information about added providers and models, add new models to an existing provider, and add models from a new provider.

   **View information about added providers and models**

**Suitable for**: Scenarios where you only need to confirm which models are currently configured under a provider, or view information such as its API Key and endpoint.

   **Operation details**: Click the target model provider card to view the models configured under that provider, the provider API Key, and other information.

   **Add new models to an existing provider**

**Suitable for**: Scenarios where an existing provider needs to expand its model coverage, for example, when a provider releases new models or your application needs to call more models from that provider. You can add new models by editing the existing provider without having to reconfigure the provider information.

   **Operation details**: Click " **... ** \> ****Edit" in the upper\-right corner of the target model provider card. On the "Edit model" page, configure the model information. For parameter descriptions and configuration guidance, see [Creating model service](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service). After the configuration is complete, click the "Confirm" button.

   **Add models from a new provider**

**Suitable for**: Scenarios where you need to integrate a new model source, such as adding a new third\-party provider or adding a model from ModelArk Foundation models, Agent Plan, or Coding Plan.

   **Operation details**: Click "Add". On the "Add model" page, fill in the model configuration parameters. For parameter descriptions and configuration guidance, see [Creating model service](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service). After the configuration is complete, click "Confirm".

### Manage Proxy API Keys

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Model integration" and click the "Proxy API Key management" tab.

3. You can view information about added Proxy API Keys, modify Proxy API Key information, add new Proxy API Keys, and more.

   **View Proxy API Key information**

**Suitable for**: Scenarios where you need to retrieve a generated Proxy API Key value for configuring model access in an application or agent, or confirm the available model scope and quota settings for a specific key.

   **Operation details**: In the Proxy API Key list, in the "Proxy Key" column of the target Proxy API Key row, click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8269671aad5b875bd9c243ebdce35753.png) to view Proxy Key information.

   **Modify Proxy API Key information**

**Suitable for**: Scenarios where you need to adjust permissions granted to a caller (such as modifying the list of available models), adjust the token usage quota, or rename a Key for easier identification and management.

   **Operation details**: In the Proxy API Key list, click "Edit" in the "Actions" column of the target Proxy API Key to modify its provider model permissions, model group permissions, model rate limits, and quota settings.

   * **All provider models/All model groups**: All provider models and all models in model groups under the current model service can be called.

   * **Custom scope**: Specify particular provider models and model groups to restrict the scope for different callers. Model group authorization and provider model authorization are independent of each other.

   **Add a new Proxy API Key**

**Suitable for**: Scenarios where you need to assign separate access credentials to a new business line, developer, or agent instance to isolate call permissions or enable granular traffic statistics.

   **Operation details**: Click "Add". On the "Add" page, enter a Proxy API Key name. Configure provider model permissions, model group permissions, rate limits, and quota settings. Then click "OK". The system generates a key value automatically.

   * **All provider models/All model groups**: All provider models and all models in model groups under the current model service can be called.

   * **Custom scope**: Specify particular provider models and model groups to restrict the scope for different callers. Model group authorization and specified provider model authorization are independent of each other.

   **Delete a Proxy API Key**

**Application scenarios**: An application has been discontinued, the corresponding caller no longer needs access to the model service, or a key is suspected of posing a security risk. Delete the key promptly to revoke access.

   > **warning**

   > Calls using the deleted key will fail immediately. A deleted key cannot be recovered.

   **Operation details: ** In the Proxy API Key list, click "More \> Delete" in the "Actions" column of the target Proxy API Key row. In the dialog box that appears, click "Delete" to complete the operation.

### Manage model groups

A model group combines multiple upstream models under a unified invocation name, and supports weight\-based upstream selection, in\-group retries, and fallback models. For operations such as creating, authorizing, calling, testing, and deleting model groups, refer to [Creating and managing model groups](https://docs.byteplus.com/en/docs/agentkit/create-and-manage-model-group).

### Delete the model service

> **warning**

> Before you delete the model service, confirm that no application is still using the Proxy API Keys associated with the model service.

* > **Irreversible operation**: The model service cannot be recovered after it is deleted. Associated data, including model provider configurations and Proxy API Keys, will also be deleted.

* > **Call interruption**: All Proxy API Keys associated with the model service will be invalidated immediately. Agents or applications that depend on the service will no longer be able to call models. Confirm in advance that the relevant agents or applications have stopped using the service or have completed migration.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Model integration" and click the "Delete" button in the upper\-right corner.

3. In the pop\-up window, click the "Delete" button to complete the operation.
