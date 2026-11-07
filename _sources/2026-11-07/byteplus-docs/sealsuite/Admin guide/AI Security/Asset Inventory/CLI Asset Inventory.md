---
title: "CLI Asset Inventory"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/cli-asset-inventory"
---

CLI Asset Inventory uses requests recorded by the Secure Web Gateway to help the administrator understand actual command\-line tool usage and API behavior risks, and view related protection policies and call logs.

## Feature introduction

Developers and automated tasks often use command\-line tools to access external platforms or services. The same CLI tool may perform different operations, such as queries, downloads, writes, or deletions. The administrator must analyze actual requests to understand how widely each tool is used in the enterprise, and which API behaviors require focused auditing or restrictions.

SealSuite aggregates CLI requests that pass through the Secure Web Gateway and are identified and recorded as tool assets. From tool usage, the administrator can open asset details to view API request methods, application endpoints, and identified behavior intents. The administrator can then use risk levels and recent call trends to determine which behaviors need attention.

For example, if a preset high\-risk behavior is an approved business operation, the administrator can first verify the request purpose, adjust its risk level, and check the handling rules for that level in the CLI Call Protection policy. To investigate a specific behavior or adjust a policy, open call logs or associated policies from the asset list.

## Prerequisites

Before using network\-side Asset Inventory, complete the following preparations.

* The enterprise has activated the **Secure Web Gateway** license, and the administrator has access permissions for the corresponding menu.

* The enterprise self\-signed root certificate, automatic certificate installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) have been configured so target traffic passes through the Secure Web Gateway. For HTTPS traffic that requires request content inspection, follow the steps in [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies) to configure decryption for the target application or domain.

* AI Access Security has been enabled in **Secure Web Gateway \> AI Access Security**.

* A policy that covers the target CLI application has been configured in **AI Security \> Supply Chain Security \> CLI Call Protection \> Policy Management**. For detailed steps, see [AI protection policy configuration](https://docs.byteplus.com/en/docs/sealsuite/configure-ai-protection-policy).

To comprehensively discover supported CLI tools, configure a low\-priority observation policy that covers target employees, and select all CLI applications. Asset statistics depend on log reporting after a policy is matched.

## View the asset list

1. Log in to the SealSuite Admin Console, go to **AI Security \> Asset Inventory**, and select the **CLI** tab.

2. Select a statistical time range and filter by **CLI application**.

3. View statistics in the asset list.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-11.png)

The following table describes the list fields.

|Field |Description |
|---|---|
|Tool name |The identified CLI tool. |
|Requests |The total number of requests initiated through the gateway and recorded. Use this field together with the number of users to quantify the asset's adoption and usage intensity in the enterprise, and to determine whether targeted control policies are required. |
|Associated policies |The number of AI protection policies associated with this asset. Click the number to go to the corresponding policy list in **CLI Call Protection \> Policy Management**. This helps the administrator verify the current control status and quickly adjust policy rules. |
|Users |The number of employees who use this tool. |
|First detected at |The first time the asset was captured by the system. Use this field together with the last active time to identify the asset lifecycle and distinguish legacy assets from recently added shadow assets, so new assets can be included in security governance promptly. |
|Last active at |The most recent time the system captured activity from the asset. Use this field together with the first detection time to understand continuous asset usage. |

## View API behavior and adjust risk levels

In the **AI Security \> Asset Inventory \> CLI** list, click **Details** in the operation column of the target tool to open **API Usage Profile**. Filter by **Behavior intent** and **Sensitivity level** to view the request method, application endpoint, behavior intent, sensitivity level, requests in the last 7 days, and last call time.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-12.png)

* **API call details**: Centrally summarizes all API calls related to this tool, including the request **method** (GET/POST/DELETE and more), **application endpoint** (URL), and **identified behavior intent** (such as calling a custom API or discovering a Git pull service).

* **Sensitivity level calibration**: The system presets sensitivity levels for behaviors. The administrator can manually adjust sensitivity levels based on actual enterprise business scenarios. For example, if a behavior that the system classifies as high risk is a trusted business operation, change its risk level to low risk. This ensures asset discovery results better match the current business context and reduces audit noise. When making adjustments, check the impact against the risk levels selected in the CLI Call Protection policy.

* **Call trends**: The **Requests in the last 7 days** column supports ascending and descending sorting. This helps the administrator quickly identify the most frequent or abnormal behavior patterns and quantify activity levels across behaviors.

To adjust the sensitivity level of an API behavior, click the edit icon next to the item in the **Sensitivity level** column, select **High risk**, **Medium risk**, or **Low risk**, and then click **OK**. **Last call time** shows the most recent time this behavior was recorded.

## View call logs and associated policies

From the tool asset list, continue to view the corresponding protection records and rules.

* Click **Requests** to go to **AI Security \> Supply Chain Security \> CLI Call Protection \> Audit Log** and view the call time, employee, CLI tool, behavior intent, risk level, and handling result. Click **Details** in a log to view the request address and associated device information.

* Click the number of **Associated policies** to go to **AI Security \> Supply Chain Security \> CLI Call Protection \> Policy Management** and view the control scope, risk level selection, and handling method of the tool.

You can also view CLI assets on the **Secure Web Gateway \> AI Access Security \> Asset Discovery \> CLI** page.
