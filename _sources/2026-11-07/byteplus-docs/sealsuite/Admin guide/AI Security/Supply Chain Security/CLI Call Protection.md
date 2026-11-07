---
title: "CLI Call Protection"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/cli-call-protection"
---

CLI Call Protection manages API requests from command\-line tools that pass through the Secure Web Gateway. administrators can select tools, effective targets, and disposition actions to log calls or block requests with specified risk levels.

## Feature introduction

When employees use tools such as lark\-cli and github\-cli, the same tool may perform different operations, such as queries, downloads, writes, or deletions. After traffic diversion is complete, the Secure Web Gateway identifies supported CLI applications and API behaviors, records behavior intent and risk level, and observes or blocks requests based on policies.

For example, to restrict a type of high\-risk operation, select the corresponding CLI application and employee scope, set the risk levels to block, and then view audit logs to check which requests were blocked. Manage tool installation and process runtime control on endpoints in Agent Asset Inventory.

## Prerequisites

Before configuring CLI Call Protection, enable the required license and route the CLI requests to be managed through the Secure Web Gateway. Confirm that the following preparations are complete.

* The enterprise has enabled the **Secure Web Gateway** license, and the administrator has the menu and operation permissions for the corresponding feature.

* The enterprise self\-signed root certificate, automatic certificate installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) are configured to route target traffic through the Secure Web Gateway. To inspect HTTPS request content, you must also [configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies).

* AI Access Security is enabled in **Secure Web Gateway \> AI Access Security**.

## Configure Call Protection

Call Protection policies specify the CLI tools to manage, the applicable personnel or devices, and the disposition method for observing or blocking requests. Select tools and effective targets based on business requirements, and create a policy as follows.

> **tip**

> Asset Inventory depends on log reporting. To collect the most complete statistics about CLI applications used in the enterprise that SealSuite can identify, configure a low\-priority policy that covers all employees first. In **CLI applications**, select all applications provided by the resource library, and set **Disposition method** to **Observe**. CLI requests that pass through the Secure Web Gateway and match this policy generate logs for **Asset Inventory** to summarize usage. This scope depends on the selectable applications in the resource library.

1. Log in to the SealSuite Admin Console.

2. Go to **AI Security \> Supply Chain Security \> CLI Call Protection**.

3. Switch to the **Policy Management** tab and click **Add a policy**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-24.png)

4. On the **Add CLI Security Policy** page, complete the following settings and click **Confirm**.

   * **Basic information**

      |Configuration item |Description |
      |---|---|
      |Policy name |Enter a custom, easy\-to\-identify policy name with up to 60 characters. Name it based on the control objective, such as "core code leak prevention policy" or "all\-employee AI usage audit". |
      |Priority |Set a value from 0 to 100. The default value is 50. A larger value indicates a higher priority. If the CLI application and effective target conflict with another policy, the system enforces only the policy with the highest priority. If priorities are the same, the system enforces the policy that was most recently added or modified. |
      |CLI application |Select the applications to control from the CLI protection resource library provided by SealSuite. Multiple selections are supported, such as lark\-cli and github\-cli. The available applications are subject to the list. |

   * **Disposition method**

      |Configuration item |Description |
      |---|---|
      |Observe |Allows users to use CLI applications normally and records related logs. |
      |Intercept (Beta) |Blocks requests for the selected CLI applications based on request risk level. In **Blocking risk**, select **High risk**, **Medium risk**, or **Low risk**. Select at least one option. The system blocks CLI requests that match the selected levels and generates logs. The blocking feature is currently in Beta. The UI indicates that stability is not guaranteed. |

   * **Effective target**

      |Configuration item |Description |
      |---|---|
      |Effective target |Select the departments, members, roles, or specific endpoint devices or device groups to which the policy applies. |

5. Configuration result:

   * **Observe mode**: Developers can run CLI commands normally. The system records API call paths and behavior intent in the background.

   * **Block mode**: CLI requests that match the risk levels are forcibly terminated. The endpoint command\-line interface usually returns a network connection error.

   * **Log audit**: After a policy is triggered, related logs are recorded on the **AI Security \> Supply Chain Security \> CLI Call Protection \> Audit Log** page. For viewing methods and field descriptions, see **View audit logs** below.

## Manage policies

On the **Policy Management** page, filter policies by policy name, employee, device, disposition action, effective status, and CLI application. Use policy cards to adjust priority and enable or disable policies. To modify rules, click **Edit**. To stop using a policy, click **Delete** and confirm.

## View audit logs

To check which operations employees performed through CLI tools, or why requests were observed or blocked, go to **AI Security \> Supply Chain Security \> CLI Call Protection \> Audit Log**. Filter records by time, employee, device, and risk conditions.

Logs record API usage details for command\-line tools such as github\-cli and lark\-cli by request. They show both the tool used and the identified behavior intent, helping administrators understand specific business operations.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-25.png)

### Core fields

The main fields in the log list are described below. Use them to verify the request tool, behavior intent, risk level, and matched policy.

|Field |Description |
|---|---|
|Trigger time |The time when the CLI request occurred. |
|Employee |The employee who initiated the request and the employee's department. |
|Device |The endpoint device that initiated the request. |
|Execution action |The disposition action hit by this request: observe or block. |
|Software name |The specific CLI tool identified. Hover over the name to view the **full request URL**. |
|Behavior intent |The call purpose identified by the system, such as calling a custom API or performing a Git pull. This helps administrators understand the purpose of the call and determine whether it meets enterprise usage requirements. |
|Risk level |The system automatically assigns a level based on behavior characteristics: high, medium, or low. This is an important basis for prioritizing investigations. If the system preset level does not match the enterprise's actual business scenario, the administrator can go to **AI Security \> Asset Inventory \> CLI** and manually adjust the sensitivity level of the behavior on the details page of the corresponding tool. |
|Matched policy |The specific protection rule matched by this behavior. Click the policy name to go directly to the policy configuration page, so administrators can verify rule details or quickly optimize rules. |

### View log details

For any high\-risk or suspicious record, click **Details** in the **Actions** column to view event details.

* **Trigger event information**: Centrally displays the decision basis, such as the trigger URL, matched policy, intent recognition, and risk classification, to clarify why the request was blocked or observed.

* **Detailed logs**: Displays network request information such as client IP, URL, and User\-Agent. Click **View details** to view recorded fields such as request time, request method, HTTP URL, status code, source port, and request size in **Basic information** and **More information** for further call troubleshooting.

* **Employee and device information**: Displays the **basic information** of the employee who initiated the request, including name, department, and account status, and the **device information** of the endpoint, including OS, IP address, and device ID. This helps locate the relevant personnel and device.

You can also configure rules and view records on the corresponding tabs for policy configuration and protection logs in **Secure Web Gateway \> AI Access Security**.
