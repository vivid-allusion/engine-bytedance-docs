---
title: "Configuring block policy for application"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Configuring_block_policy_for_application"
---

To control file sharing through messaging and cloud storage applications on user devices, you can configure application blocking policies. This guide provides instructions for creating, copying, editing, and deleting policies to enforce your data security rules on Windows and macOS.

# Instructions for use

After you configure an application blocking policy, the SealSuite client will block some operations of messaging or cloud storage applications on user devices according to the policy configuration. The blocking policy currently applies to operating systems such as Windows and macOS.

* For Windows, you can block file sharing from desktop messaging applications, website access from web\-based messaging applications, internet connections from desktop cloud storage applications, and website access from web\-based cloud storage applications.

* For macOS, you can only block file sharing from desktop messaging applications.

# Creating an application blocking policy

1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Strategy Center** \> **Control Strategy** \> **Channel Control**.

3. In the upper right corner of the **Policy Management** tab, click  **+ New Policy**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04eb2f2ebed1482d8fdd5299172a909f~tplv-goo7wpa0wc-topic.webp)

4. On the **Add Blocking Policy** page, complete the following configuration and click **Confirm**.

   |**Items** |**Description** |
   |---|---|
   |**Policy Name** |Create a custom name to identify the policy. |
   |**Priority** |Specify the priority of the current policy. The value can range from 0 to 100, with a higher value indicating a higher priority. You can have multiple policies in effect at the same time. When SealSuite detects activity on user devices, it evaluates policies in order of priority. Once a policy match is found, SealSuite stops further evaluation. If there are two policies with the same priority value, the one that was most recently modified is applied first. |
   |**Blocking Scope** |Describes the blocking effects for Windows and macOS.<br><br><br>* The application types that can be blocked include Messaging Apps (desktop and web versions), Cloud Storage Apps (desktop and web versions), and Online Collaboration Tools (desktop and web versions).<br><br>* The following operations are supported on Windows: Block desktop messaging applications from sending internal files and web\-based messaging applications from opening websites; Block desktop cloud storage applications from connecting to the internet and web\-based cloud storage applications from opening websites.<br><br>* The following operation is supported on macOS: Block desktop messaging applications from sending internal files. It currently does not support other blocking operations. |
   |**Select Application** |Select the specified **Messaging Apps**, **Cloud Storage Apps,**  and **Online Collaboration Tools** as needed. Multiple selection is supported. |
   |**Notification** |Specifies whether to enable message notifications. After you enable this feature, when file sharing is blocked on a user's device, the SealSuite client sends a notification.<br><br>Click **Configure** on the right to go to the **Notification Pop\-up Template** configuration page, where you can create or reuse a notification template. For details, see [Configure Notification Pop-up Templates](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule#72d521ed). |
   |**Scope** |Limit the policy's scope by **Employee** or **Device**.<br><br><br>* When selecting **Employee**, you can limit the scope by **Department** or **Role.** <br><br>* When selecting **Device**, you can limit the scope by **Device**, **Operating System (OS)** , and **Group**. |

# Managing the policy lifecycle

Administrators can manage existing channel control policies within the **DLP** \> **Strategy Center** \> **Channel Control** policy list in the Admin Console.

* **View Analytics**: The top of the policy list displays real\-time statistics, including the **Total Number of Policies** and the **Number of Active Devices**.

   * **Note**: Monitor the **Server Configuration Version** at the top of the page. This version updates whenever a policy is edited. By comparing this version with the one reported by the client, administrators can verify whether the latest policy has been successfully deployed to the endpoints.

* **View policy change information**: In the policy list, you can directly view the **Last modified by** and **Last modified time** of each policy to quickly trace its change history.

* **View effective endpoints**: Click the number in the **Actual/Expected** column in the policy list to enter the **Policy in Effect** details page. You can view the **Policy version update time** of the endpoints. Click the **Refresh** button next to the number to proactively fetch the latest effective status data.

* **Enable/Disable**: Use the toggle in the **Status** column to activate or deactivate a policy. Once disabled, the policy becomes ineffective immediately, and the SealSuite client stops enforcing the corresponding blocking logic.

* **Edit and Copy**: Click **Edit** to modify current configurations. Click **Copy** to quickly create a new policy based on an existing template.

* **Verify Enforcement Status**: For **Enabled** policies, navigate to **More** \> **Policy in Effect** to view the real\-time deployment and execution details on each endpoint.

* **Delete**: Permanently remove policies that are no longer required.

   * **Caution**: Deletion is irreversible. Please confirm your requirements before proceeding.
