---
title: "Skill download protection"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/skill-download-protection"
---

Skill download protection checks Skill download requests that pass through the Secure Web Gateway. It blocks or allows access based on the risk level of the download source and records download activity.

## Feature introduction

When employees download Skills from third\-party sources, they may access malicious dependencies, counterfeit components, or other resources with supply chain risks. After traffic diversion is configured, the Secure Web Gateway identifies risks based on HTTP(S) download URLs and Threat Intelligence. administrators can set separate actions for high\-, medium\-, and low\-risk downloads.

For example, to prevent employees from downloading high\-risk Skills, an enterprise can set high\-risk downloads to Block. administrators can then use audit logs to view the blocked addresses, employees, and devices. For files already saved on endpoints, use Skill Security Detection for scanning.

## Prerequisites

Before configuring download protection, enable the required license and route the target download traffic through the Secure Web Gateway. Confirm that the following preparations are complete.

* The enterprise has enabled the **Secure Web Gateway** license, and the administrator has the menu and operation permissions for the corresponding feature.

* The enterprise self\-signed root certificate, certificate auto\-installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) have been configured to route target traffic through the Secure Web Gateway. To inspect HTTPS request content, you must also [configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies).

* AI access security has been enabled in **Secure Web Gateway \> AI access security**.

## Configure download protection

Skill security identifies supply chain risks in Agent tool and skill download paths. It prevents employees from downloading malicious Skill files that contain malicious dependencies or compromised third\-party components.

> **tip**

* > This policy sets the actions and effective scope for risky Skill downloads. The audit scope is limited to visits that pass through the Secure Web Gateway and are identified as Skill\-related risky addresses. After the feature is enabled in **Secure Web Gateway \> AI access security**, you can verify these requests in logs. Allowed risky downloads are also logged.

* > Gateway\-side Skill download protection blocks risky addresses at the download source. To check existing local Skill files on endpoints, see [Skill Security Detection](https://docs.byteplus.com/en/docs/sealsuite/configuring-skill-detection-policy).

1. Log in to the SealSuite Admin Console.

2. Go to **AI Security \> Supply Chain Security \> Skill download protection**.

3. Switch to the **Policy Management** tab and click **Edit**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-22.png)

4. In the pop\-up window, enable **Skill security**, complete the following configuration, and click **OK**.

   * **Risk level determination**: The security intelligence service determines high, medium, and low risk levels based on the Skill download URL, supply chain risk tags of associated resources, vulnerability information, and risk severity. The service periodically synchronizes the results to the Secure Web Gateway. When access matches these addresses, the gateway enforces the action for the corresponding risk level. administrators can view matched addresses, risk levels, and descriptions in **Audit Log** to understand the risk of a download and decide whether to adjust the action for the corresponding level.

   * **Action**: administrators do not need to manually assign a level to each download address. They can set **Block** or **Allow** separately for **high risk**, **medium risk**, and **low risk**. By default, high\-risk and medium\-risk downloads are set to **Block**, and low\-risk downloads are set to **Allow**.

      * **Block**: Blocks Skill downloads that match the risk level and records interception logs.

      * **Allow**: Allows the download but still reports audit logs, so administrators can trace the activity later.

   * **Block page configuration**: When the action is "Block", employees see an interception prompt in the browser. administrators can customize the prompt content. Multilingual notification titles and content are supported, and the preview pane shows the block page in real time.

   * **Effective scope**: Select the departments, members, roles, or specific endpoint devices (groups) to which this policy applies.

5. Configuration result:

   * **Policy effect**: The system performs interception only when the action is "Block" and the download activity matches the corresponding risk level.

   * **Log audit**: Within the scope where AI access security is enabled and traffic diversion is complete, visits to identified Skill risky addresses generate audit records. Allowed requests are also logged. Go to **AI Security \> Supply Chain Security \> Skill download protection \> Audit Log** to view the target address, risk level, and executed action. For details, see **View audit logs** below.

## View audit logs

To check which Skills employees downloaded, what risks exist in the download sources, and whether requests were blocked, go to **AI Security \> Supply Chain Security \> Skill download protection \> Audit Log** and filter records by time, employee, device, and risk conditions.

Logs record Skill download addresses, risk levels, and action results. Use them to locate high\-risk downloads and investigate related personnel and devices.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-23.png)

### Key fields

The following table describes the main fields in the log list. Use these fields to verify download addresses, risk evidence, and action results.

|Field |Description |
|---|---|
|Trigger time |The time when the risky address was accessed. |
|Employee |The employee who initiated the request and the employee's department. |
|Device |The Endpoint device that initiated the request. |
|Target address |The complete URL that initiated the Skill download request. administrators can use this field to inventory active third\-party Skill marketplaces or nonstandard download channels in the enterprise, and identify "shadow Skill" assets. |
|Description |The basis for the determination provided by the Threat Intelligence engine. High\-risk records usually display specific threat context, such as ClawHub third\-party marketplace or Typosquatting counterfeit packages, to help administrators understand the risks in the download source. |
|Risk level |The level determined by the system based on the intelligence database. The value can be **high risk**, **medium risk**, or **low risk**, and can be used as a reference for investigation priority. |
|Executed action |Indicates whether the risky activity was **blocked** or **allowed**, and is used to verify the actual result of the protection policy. |

### View log details

For any high\-risk or suspicious record, administrators can click **View details** in the Actions column to open the details page. The page displays the download request, risk level, executed action, and related employee and device.

* **Triggered event information**: Displays the event ID, target address, executed action, and risk level in one place, indicating why the request was blocked or allowed.

* **Detailed log records**: Displays network request information, such as client IP, request method, and URL. administrators can use this information to verify the source and target address of the download request.

* **Employee and device information**: Displays the **identity information** of the employee who initiated the request, such as name, department, and account status, and the **device information** of the endpoint, such as OS, public IP, and device ID. This helps locate the related personnel and devices.

You can also configure rules and view records on the corresponding tabs for policy configuration and protection logs in **Secure Web Gateway \> AI access security**.
