---
title: "Configuring clipboard control policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-clipboard-control-policies"
---

SealSuite Data Loss Prevention (DLP) provides a standalone **Clipboard control policy** dedicated to monitoring and intercepting cross\-application copy and paste of sensitive data by employees on Windows and macOS endpoints. By configuring this policy, you can effectively prevent core source code, customer lists, and other sensitive information from being leaked through the clipboard.

# Prerequisites

Before configuring a clipboard control policy, make sure you have completed sensitive data rules and classification configuration in the **DLP** \> **Data Identification** module. Clipboard control policies rely on these rules to accurately identify and intercept outbound sensitive content. For details, see [Managing sensitive thesaurus](https://docs.byteplus.com/docs/sealsuite/managing-sensitive-thesaurus)and[Managing classification and grading rules](https://docs.byteplus.com/docs/sealsuite/managing-classification-and-grading-rules).

# Create a clipboard control policy

1. Log in to the Admin Console.

2. Navigate to **DLP** \> **Strategy Center** \> **Control Strategy** \> **Clipboard control policy**.

3. Click  **+ Add policy** in the upper\-right corner of the list.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5aa7d891d544ffc91cf01b45c2e8d41~tplv-goo7wpa0wc-topic.webp)

4. On the policy configuration page, complete the following settings, then click **Confirm** to save and publish.

   * **General**

      * **Policy name**: Enter a custom name to identify this policy.

      * **Policy description**: Enter supplementary information. This field does not affect policy logic.

      * **Priority**: Define the execution order of the policy (0–100). **A higher value means the policy is evaluated first.**  When policies with the same priority are both triggered, the most recently created or updated policy takes effect.

      * **Manage labels**: Associate the current policy with specific tags (optional). The drop\-down list only displays tags that the current administrator has access to. By associating tags, you can enforce policy permission isolation between administrators of different regions or business lines. To add or adjust the visible tag options in the drop\-down list, a super administrator must modify the **Managed tag scope** for your administrator role under **Settings** \> **Admin Access**.

   * **Control action**

      Choose a **Control action** based on your security requirements:

      * **Allow**: Detect and record copy/paste of sensitive content without intercepting it, enabling unobtrusive behavior tracing.

      * **Deny**: Intercept and record high\-risk copy/paste of sensitive content, enforcing security policies.

      > **注意**

      1. > **Platform Applicability**

         * > For **text** paste actions: Both Allow and Deny are supported on Windows and macOS endpoints.

         * > For **screenshot** paste actions: Both Allow and Deny are supported on Windows endpoints. On macOS endpoints, only audit\-based Allow is currently supported; Deny is not supported.

      2. > **Performance and User Experience Assurance**

         * > **Audit mode scan duration**: In Allow mode, you can configure the scan duration to ensure evidence completeness. The default duration is 5 seconds. To adjust it, go to **DLP \> Strategy Center \> System Configuration \> Scan resource configuration** and set **File scan timeout limit** (see [Scan resource configuration](https://docs.byteplus.com/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies#0eaf376f)).

         * > **Block mode latency safeguard**: For blocking **screenshot** paste actions, SealSuite uses a **300ms** response threshold. If content recognition cannot be completed within 300ms, the system will prioritize allowing the paste action to avoid noticeable endpoint lag. The system will still continue image recognition in the background and perform policy matching.

   * **Control channel**

      * **Clipboard paste**: Detects **text** or **screenshot** pasted from the clipboard into a target application. If sensitive data is matched, the system will perform an audit or block action.

      * **Clipboard copy (not recommended)** : Detects text copied or cut from an application to the clipboard. If sensitive data is matched, the system will perform an audit or block action.

         > **说明**

         > **Configuration guidance**: Employees frequently copy content during daily work. Intercepting or alerting on every copy action generates a high volume of false positives and severely disrupts productivity. We recommend controlling only the **paste** action — allow copying, but prevent sensitive content from being pasted into unauthorized external applications.

      * **Exclude internal address**: If you have selected to control clipboard activity across all websites but need to exclude specific sites (such as internal websites) from detection and auditing, first add those sites as internal addresses on the **Strategy Center** \> **Internal address** \> **Websites** page, then enable the toggle here and import the added addresses.

   * **Outgoing content**

      Apply the sensitive data you configured during the preparation phase to this policy as the core matching criteria. Click  **+ Add hierarchical classification data** on the right to select the specific sensitive data this policy should detect.

      > **注意**

      > Clipboard detection supports only sensitive data rule matching based on **file content**.

      * > **Underlying logic**: When an employee performs a "copy text/screenshot \-\> paste" action, the data is transferred directly in system memory without generating an actual local disk file. Therefore, this data flow does not have physical file attributes such as file name, file extension, or storage path.

      * > **Configuration recommendation**: Make sure the associated sensitive data rules include **file content** detection conditions (such as keywords or regular expressions). Otherwise, the policy will fail in clipboard scenarios as no match can be made.

   * **Action**

      Define what happens when the policy is triggered.

      |**Response action** |**Description** |
      |---|---|
      |**Log reporting** |Report violation events to the Admin Console. This option is enabled by default and cannot be turned off. You can view the logs on the **Investigation audit** \> **Audit log** \> **Clipboard log** page. For details, see [Viewing clipboard logs](https://docs.byteplus.com/docs/sealsuite/viewing-clipboard-logs). |
      |**Screenshot** |When enabled, the system captures the employee’s screen as evidence when an outbound file transfer is detected. Click **Configure** on the right to select the applicable operating systems (Windows, macOS, Linux).<br><br><br>* **Windows/Linux**: The employee is not notified.<br><br>* **macOS**: It requires the "Screen Recording" permission, which may result in frequent system privacy prompts on macOS 14+. Therefore, it is recommended to switch to **Outgoing Screenshot** mode in [Screenshot configuration for evidence collection](https://docs.byteplus.com/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies#5dfef9f3) to minimize disruption to employees’ work. |
      |**File archiving** |Archive the original outbound content as evidence. You can download and view archived content on the **Investigation audit** \> **Audit log** \> **Clipboard log** page. |
      |**Terminal notification** |Display a risk alert message to the employee on the endpoint. After enabling, click **Configure** on the right to go to the **Notification Pop\-up Template** configuration page, where you can create or reuse a notification template. For details, see [Configure Notification Pop-up Templates](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule#72d521ed). |

   * **Scope**

      Define the scope of this policy. You can fine\-tune the scope by **employees** (departments/roles) or **devices** (operating systems/groups), and configure exclusions.

# Manage clipboard control policies

After creating policies, you can view and manage all policies on the **Clipboard control policy** list page.

* **View policy statistics**: At the top of the policy list, the system provides a visual dashboard. After you deploy a new policy or modify an existing one, use this dashboard to track the policy's deployment progress and health across all endpoints in real time, ensuring that control requirements are enforced. The **Server configuration version** number is the key indicator for determining whether a client's policy is up to date. This version number changes every time you edit or update any policy. If the version number reported by a client matches the one displayed here, the client's policy is fully synchronized.

* **View policy change information**: In the policy list, you can directly view the **Last modified by** and **Last modified time** of each policy to quickly trace its change history.

* **View effective endpoints**: Click the number in the **Actual/Expected** column in the policy list to enter the **Policy in Effect** details page. You can view the **Policy version update time** of the endpoints. Click the **Refresh** button next to the number to proactively fetch the latest effective status data.

* **Enable/Disable**: Use the toggle in the **Status** column to quickly enable or disable a policy.

* **Edit/Copy/Delete**: In the **Action** column, modify a policy, quickly create a similar policy, or remove a policy you no longer need. Deleted policies cannot be restored, but events that have already been detected remain in the alert event list.
