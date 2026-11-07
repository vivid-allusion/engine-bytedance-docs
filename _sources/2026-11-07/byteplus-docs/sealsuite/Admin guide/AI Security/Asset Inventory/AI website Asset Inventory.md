---
title: "AI website Asset Inventory"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/ai-website-asset-inventory"
---

AI website Asset Inventory helps an administrator understand the AI applications that employees access through browsers or supported identifiable clients. It also checks application usage based on access records and associated policies.

## Feature introduction

The **AI Websites** tab inventories access to AI applications identified by the Secure Web Gateway. This includes online services such as the Doubao web version and the ChatGPT web version, as well as supported identifiable client access from Cursor, Trae, and others. The software installation list shows tool installation status. This page helps an administrator understand which AI services were actually accessed, how many employees were involved, and whether corresponding management policies exist.

After traffic diversion is configured, AI application access traffic within the diversion scope passes through the **Secure Web Gateway**. The gateway identifies the AI application that corresponds to a request based on traffic characteristics such as the access domain name. It then records access logs according to configured protection policies. SealSuite aggregates these logs into assets. An administrator can view the access count, user count, and activity for each application. The administrator can also view access records and associated policies to understand specific usage and existing control rules.

For example, if multiple employees are using an AI website that is not yet included in the enterprise allowlist, the administrator can first view access records. The administrator can then evaluate whether to allow its use based on employees' business needs, and decide whether to add it to the allowlist or adjust protection policies. Asset Inventory helps you understand website usage. Whether access is allowed or blocked is determined by the corresponding protection policy.

## Prerequisites

Before using network\-side Asset Inventory, complete the following preparations.

* The enterprise has enabled the **Secure Web Gateway** license, and the administrator has access permissions for the corresponding menu.

* The enterprise self\-signed root certificate, automatic certificate installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) have been configured so that target traffic passes through the Secure Web Gateway. For HTTPS traffic that requires request content inspection, configure decryption for the target application or domain according to [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies).

* AI access security has been enabled in **Secure Web Gateway \> AI access security**.

* Policies that cover target AI websites have been configured in **AI Security \> Runtime Security \> LLM Semantic Protection \> Policy Management**. Asset data depends on policy hits and log reporting. For detailed configuration, see [Configure AI protection policies](https://docs.byteplus.com/en/docs/sealsuite/configure-ai-protection-policy).

For comprehensive inventory, configure a low\-priority policy that covers target employees. Select all AI applications, set the action to **Observe \> Record all logs**, and leave the protection content empty. Then use higher\-priority policies to control specific risks.

## View the asset list

1. Log in to the SealSuite Admin Console, go to **AI Security \> Asset Inventory**, and select the **AI Websites** tab.

2. Select the **Last 24 hours, Last 7 days, Last 30 days**, or **Custom** time range, and filter by **Software name**.

3. View the statistics in the asset list.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-03.png)

The list fields are described below.

|Field |Description |
|---|---|
|Software name |The identified AI application name. |
|Access count |The total number of accesses initiated through the gateway and recorded. Combined with the user count, this metric quantifies the asset's adoption and usage intensity within the enterprise. It helps determine whether targeted control policies are required. |
|Associated policies |The number of AI protection policies associated with the asset. Click the number to go to the corresponding policy list in **LLM Semantic Protection \> Policy Management**. This helps an administrator verify the current control status and quickly adjust policy rules. |
|User count |The number of employees who use the asset. Combined with the access count, this metric quantifies the asset's adoption and usage intensity within the enterprise. |
|First discovered at |The first time when the asset was captured by the system. Combined with the last active time, this field helps distinguish legacy assets from recently added shadow assets, enabling timely security governance for new assets. |
|Last active time |The most recent time when the system captured access activity for the asset. Combined with the first discovery time, this field helps identify the asset lifecycle and continuous usage status. |

## View access records and associated policies

To troubleshoot the usage of a specific website, continue from the asset list to view logs or policies.

* Click **Access count** to go to **Runtime Security \> LLM Semantic Protection \> Audit Log** and view the access records for the corresponding AI website.

* Click the **Associated policies** count to go to **Policy Management** for this feature and view the policies for the corresponding website.

You can also view AI website assets on the **Secure Web Gateway \> AI access security \> Asset discovery \> AI applications** page. Overall access rankings and department distribution are available in **Application security posture**. For more information, see [Manage AI asset discovery](https://docs.byteplus.com/en/docs/sealsuite/ai-asset-discovery-management).
