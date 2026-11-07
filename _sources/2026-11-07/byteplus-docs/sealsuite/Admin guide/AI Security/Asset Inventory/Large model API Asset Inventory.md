---
title: "Large model API Asset Inventory"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/large-model-api-asset-inventory"
---

Large model API Asset Inventory organizes model services called through APIs. It helps administrators identify service sources, understand usage scale, and trace protection policies associated with calls.

## Feature introduction

**Large model API assets** are large model services called by enterprise applications, development tools, or automated tasks through APIs, such as the OpenAI API and DeepSeek API. These services may come from official APIs of model vendors, third\-party relay sites, or enterprise\-built services. administrators need to know which services employees actually call, which domains requests are sent to, and whether any model access is not centrally managed by the enterprise.

After traffic diversion and the corresponding SSL decryption configuration are complete, large model API requests pass through the **Secure Web Gateway**. The gateway identifies model services based on traffic characteristics such as domains and APIs in requests, and records call logs according to configured protection policies. SealSuite then summarizes model providers, domains, call counts, user counts, and token consumption based on logs. This helps administrators understand the usage of different model services. administrators can view assets by source: **official, relay site, self\-built, or unknown**. Providers that cannot be identified are summarized in records related to **unknown vendors**. Whether these assets continue to be discovered depends on the policy configuration scope.

For example, when investigating whether a business uses an unapproved model relay service, administrators can filter assets by **relay site** source and domain, and then view call logs to understand related access. They can also check existing control rules through associated policies. Combined with call counts, user counts, and token consumption, administrators can evaluate the usage scale of the service, and then decide whether to adjust model access or protection policies.

## Prerequisites

Complete the following preparations before using network\-side Asset Inventory.

* The enterprise has enabled **Secure Web Gateway** license, and the administrator has access permissions to the corresponding menu.

* The enterprise self\-signed root certificate, automatic certificate installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) have been configured, so that target traffic passes through the Secure Web Gateway. For HTTPS traffic whose request content needs to be inspected, configure decryption for target applications or domains by following the steps in [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies).

* AI access security has been enabled in **Secure Web Gateway \> AI access security**.

* A LLM Semantic Protection policy that covers target model providers has been configured. For more information, see [Configure AI protection policies](https://docs.byteplus.com/en/docs/sealsuite/configure-ai-protection-policy). To inventory services from unknown sources, select **unknown vendors** in the model provider scope of the policy.

For a comprehensive inventory, configure a low\-priority observation policy, select the model providers to inventory, and enable **Record all logs**. After unknown vendors are deselected, the system stops adding and updating corresponding assets. Existing assets, policies, and audit logs are retained.

## View the asset list

1. Log in to the SealSuite Admin Console, go to **AI Security \> Asset Inventory**, and select the **LLM APIs** tab.

2. Select a statistics time range and a source type: **official, relay site, self\-built, or unknown**. Then filter by **model provider** or **domain**.

3. View the statistics in the asset list.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-04.png)

The list fields are described as follows.

|Field |Description |
|---|---|
|Model provider |Displays the name of the identified model provider. At the top of the page, filter by source: **official, relay site, self\-built, or unknown**. View specific model versions, such as GPT\-4 and DeepSeek\-V3, in **Associated model information** on the provider **Details** page. To supplement ownership information for unknown domains, use **Edit** or **Add model provider**. |
|Domain |Displays the domain address corresponding to the large model API request. Combined with the domain filter at the top, administrators can quickly locate asset calls under a specific domain. |
|Call count |The total number of calls initiated through the gateway and recorded. Combined with the user count, this field helps quantify how widely and intensively the asset is used in the enterprise. It also helps determine whether a targeted control policy is required. |
|Associated policies |The number of AI protection policies associated with the asset. Click the number to go to the corresponding policy list in **LLM Semantic Protection \> Policy Management**. This helps administrators verify the current control status and quickly adjust policy rules. |
|User count |The number of employees who called the service. |
|Token consumption |The total token consumption generated by the asset. This field helps you understand model usage scale and resource consumption. Usage returned by the upstream large model API is used first. If no usage is returned, the system estimates usage based on request and response content. Usage data may be unavailable if the request is blocked, the response is missing, or parsing fails. |
|First discovered at |The first time when the asset was captured by the system. Combined with the last active time, this field helps identify the asset lifecycle and distinguish legacy assets from recently added shadow assets, so that security governance can be performed on new assets in time. |
|Last active at |The last time when activity of the asset was captured by the system. Combined with the first discovered time, this field helps you understand whether the asset remains in use. |

## View call records and associated policies

From the asset list, continue tracing model calls and their control rules.

* Click **Call count** to view **LLM APIs** records in **Runtime Security \> LLM Semantic Protection \> Audit Log**.

* Click the **Associated policies** count to go to **LLM Semantic Protection \> Policy Management** and view policies for the corresponding model provider.

You can also view large model API assets on the **Secure Web Gateway \> AI access security \> Asset discovery \> Large model API** page.

## View asset details and edit providers

To understand the usage of a model provider, or to supplement ownership information for an unknown service, use the **Actions** column in the asset list.

* **Details**: View the model provider, domain, and basic statistics, including first discovered time, last active time, associated model count, associated policies, call count, user count, and token consumption. For identified providers, the details page also displays **Associated model information**. You can view call count, access user count, token consumption, and discovery time by model. Click the call count to view logs for the corresponding model.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-05.png)

* **Edit**: To modify information about a custom model provider, or to supplement provider ownership for an unknown domain, click **Edit**. For an unknown domain, create a model provider or add the domain to an existing model provider. Built\-in provider information cannot be modified here.

## Manage model provider resources

**Resource management** maintains custom model providers and their domain ownership. For example, after an unidentified model API domain is discovered, register it as a new provider or add it to an existing provider. This makes subsequent access easier to manage by explicit name and source.

### Add a resource

Follow these steps to register a model provider and domain.

1. In the upper\-right corner of the **AI Security \> Asset Inventory \> Large model API** page, click **Resource management**.

2. In the resource list, click **Add resource** to open the **Add model provider** panel.

3. Select **Configuration method**.

   * **Create a model provider**: Create a provider for an unregistered service. Enter a **Model provider name** that does not duplicate an existing custom provider. The name can contain up to 255 characters.

   * **Add to an existing model provider**: Select an existing custom **Model provider name** and add the domain to the provider.

4. Enter **Domain address list**. Enter at least one exact domain. Wildcards and regular expressions are not supported. Separate multiple addresses with line breaks, commas, semicolons, or spaces. Set **Model source type**. Available options are **official, relay site, and self\-built**.

   To set an icon, click **Re\-upload**.

5. Click **OK** to save.

   After creating a model provider, you must associate it with related protection policies. Only then do the policies take effect for the provider.

After the source of an unknown model is changed to another source type, only newly reported logs update the model provider name, domain, and source type. Historical logs are not updated.

### Batch supplement ownership for unknown domains

To add multiple unknown domains to the same model provider, select **Unknown** on the **LLM APIs** tab, select target records, and then click **Batch edit** at the bottom of the list. In the configuration panel, create a model provider or add the domains to an existing custom provider. Check the domain list and source type, and then save. You can also register resources separately by clicking **Add model provider** in the upper\-right corner of the page.

### Edit or delete a resource

In **Resource management**, filter registered resources by model provider, domain, and model source type, and then perform the following operations.

* **Edit**: Modify the name, domain, source type, and icon of a custom model provider.

* **Delete**: Delete a custom model provider that is no longer needed. After deletion, associated policies are automatically disassociated. If the scope of a policy becomes empty as a result, the policy is disabled. Check associated policies before confirming deletion.
