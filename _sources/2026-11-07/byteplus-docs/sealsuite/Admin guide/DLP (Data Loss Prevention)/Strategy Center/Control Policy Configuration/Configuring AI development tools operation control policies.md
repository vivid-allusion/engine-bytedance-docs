---
title: "Configuring AI development tools operation control policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-ai-development-tools-operation-control-policies"
---

**AI development tools operation control** is a specialized SealSuite DLP module designed for R&D security. This feature enables enterprises to identify and audit when employees use AI collaboration tools—such as Trae, Cursor, or Claude Code—to access local sensitive code repositories, preventing core intellectual property from leaking to unauthorized external models.

## Feature Description

As AI coding tools become more widely used, employees may use personal accounts or connect to third\-party models that have not been authorized by the enterprise to process internal code, creating "shadow AI" risks. This feature addresses such risks through the following capabilities:

* **Multi\-form tool coverage**: Supports unified identification of AI IDEs, CLI Agents, and IDE plugins.

* **Access behavior audit**: Supports recording "Read locally" and "Upload inference" behaviors performed by AI tools on local code repositories, and collects complete repository path information.

* **Compliance assessment basis**: Collects the model Base URL and account information (personal or enterprise) associated with the tool, helping administrators determine whether the access is compliant.

## Prerequisites

Before configuring an AI development tools operation control policy, ensure that you have defined the **code repository sources** to protect in the Admin Console. For details, see [Managing the File Source Library](https://docs.byteplus.com/docs/sealsuite/managing-the-file-source-library).

## Procedure

1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Strategy Center**.

3. At the top of the right\-side page, select the **Control strategy** tab, and then click the **AI development tools operation control** subtab below.

4. In the upper\-right corner of the policy list, click  **+ New Strategy**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8d919a54e934933bfb357183d7424cb~tplv-goo7wpa0wc-topic.webp)

5. On the policy creation page, complete the following configurations:

   * **General**

      * **Policy Name**: Customize a name to identify the policy.

      * **Policy Description**: Briefly describe the control objective of the policy.

      * **Priority**: Define the policy execution order (0–100). **A higher value indicates a higher matching priority**. If policies with the same priority are hit, the most recently created or updated policy is executed.

      * **Management Labels**: Select a tag to associate with the current policy (optional). The drop\-down list displays only the tags granted to the current administrator. By associating tags, you can isolate policy permissions between administrators of different regions or business lines.

   * **Control Action**

      * **Audit**: AI tools are allowed to access internal code repositories, and detailed audit logs are generated.

      * **Deny**: AI tools are denied access to internal code repositories, and detailed audit logs are generated.

   * **Access Control**

      * **AI development tools**: Select the AI development tools to control. To view the specific control scope, see [AI Tool Control Capabilities List](https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list).

      * **Exclude internal addresses**: Operations hitting internal addresses will not be logged or blocked. Please first go to the **Strategy Center** \> **Internal Address** page to add the AI tools you want to exclude as internal addresses, and then import the added tools here. For details, see [Internal address configuration guide](https://docs.byteplus.com/en/docs/sealsuite/internal-address-configuration).

   * **Code repository source**

      Click  **+ Import** and select the sensitive code repositories to protect from the list. The repositories must be predefined in the File Source Library.

   * **Action**

      Define the response action after the policy is hit.

      * **Log reporting:**  It is enabled by default and cannot be disabled. After it is enabled, behaviors that hit the policy are recorded in audit logs. You can go to **DLP** \> **Investigation Audit** \> **Audit Log \> AI Development Tools Operation Log** to view details. For details, see [Viewing AI development tools operation logs](https://docs.byteplus.com/docs/sealsuite/viewing-ai-development-tools-operation-logs).

      * **Terminal notification**: Send a risk alert to employees on endpoints. After this is enabled, click **Configure** on the right to go to the **Notification Pop\-up Template** configuration page, where you can create or reuse an AI tool control notification template. For details, see [Configure Notification Pop-up Templates](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule#72d521ed).

   * **Scope**

      Define the scope of this policy. You can configure the scope by **User** (Department/Role) or **Device** (OS/Device Group), and configure excluded objects.

6. Click **Confirm** at the bottom of the page to complete policy creation.

## Manage the Policy Lifecycle

On the **AI development tools operation control** list page, you can manage created policies on a daily basis.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/811b26206dc44ab2afb37489dc3993d5~tplv-goo7wpa0wc-topic.webp)

* **View policy statistics**: At the top of the policy list, the system provides a visual data dashboard. After administrators issue a new policy or modify an existing policy, they can use this dashboard to track the delivery progress and health status of the policy across endpoints in real time. The **Server configuration version** number is the key basis for determining whether the client policy is up to date.

* **View policy change information**: In the policy list, you can directly view the **Last modified by** and **Last modified time** of each policy to quickly trace its change history.

* **View effective endpoints**: Click the number in the **Actual/Expected** column in the policy list to enter the **Policy in Effect** details page. You can view the **Policy version update time** of the endpoints. Click the **Refresh** button next to the number to proactively fetch the latest effective status data.

* **Enable/Disable**: Use the switch in the policy **Status** column to quickly control whether the policy takes effect.

* **Edit/Copy/Delete**: In the **Action** column of a policy, modify the policy, quickly create a similar policy, or remove a policy that is no longer needed.
