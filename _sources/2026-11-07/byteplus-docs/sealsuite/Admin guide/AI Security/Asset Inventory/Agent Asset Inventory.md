---
title: "Agent Asset Inventory"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/agent-asset-inventory-and-control"
---

Agent Asset Inventory helps administrators understand AI tool installations on employee endpoints and disable Agent configurations that do not meet enterprise access requirements.

## Feature introduction

Employees may use AI through desktop applications, command\-line tools, or IDE plugins. When managing AI tool access, administrators need to know which tools are installed in the enterprise, which versions are in use, and which endpoints have them installed. This helps determine which tools can remain in use and which versions need upgrades.

**Agent assets** refer to AI tools installed on employee endpoints, including the following types.

* **Desktop clients**: AI applications that can run independently after installation, such as the Doubao client and ChatGPT Desktop.

* **Command\-line tools (CLI)** : AI tools used through commands in a terminal, such as Claude Code CLI and Codex CLI.

* **IDE plugins**: AI extensions installed in code editors or integrated development environments (IDEs), such as Claude Code for VS Code and GitHub Copilot in VS Code.

On the Asset Inventory page, desktop clients and CLI tools are included in the **Agent** view. AI extensions in editors are included in the **IDE plugin** view. The scope of tools supported for detection is subject to the capability list referenced in this article.

Agent Asset Inventory identifies installed AI tools based on software names, application identifiers, plugin identifiers, and other information reported by endpoints. It then aggregates installation information from different endpoints into an asset list. administrators can view the overall installation status across the enterprise. They can also open the details of a specific tool to view version distribution and endpoints where it is installed.

For example, if an enterprise has approved an AI coding tool but needs to upgrade older versions uniformly, the administrator can filter for that version in the tool details and identify devices that require an upgrade.

Asset identification and control capabilities vary by tool. For details, see [AI tool control capability list](https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list).

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-00.png)

## Prerequisites

* The enterprise has purchased the **AI Security license**. For billing details, see [Billable items](https://docs.byteplus.com/en/docs/sealsuite/pricing).

* **Agent Asset Inventory** depends on endpoint software information reporting. Before using inventory features, make sure the **Software statistics** switch is enabled on the **Endpoint \> Software management \> Software statistics** page. Otherwise, this feature cannot take effect.

## Enable Agent Asset Inventory

After this feature is enabled, SealSuite identifies AI tools based on software information reported by endpoints and aggregates installation status.

1. Log in to the SealSuite Admin Console and go to **AI Security \> Asset Inventory \> Agent**.

2. Turn on the **Agent Asset Inventory** switch at the top of the page.

   Inventory data is updated every other day by default. To retrieve the latest data immediately, click the refresh button on the right. The refresh is expected to take 30 minutes.

## View the inventory overview

Use the overview at the top of the page to understand Agent installation and control status in the enterprise. Some metrics support filtering the asset list below after you click them.

|Field |Description |
|---|---|
|Number of Agents |Total number of AI Agents identified across the network. Click to reset the filter criteria in the list below and display all Agent assets. |
|Number of disabled Agents |Number of Agents configured as **partially disabled** or **fully disabled**. Click to quickly filter tools that are currently under control. Whether a policy has taken effect on endpoints still depends on the delivery time and endpoint status. |
|New Agents in the last 7 days |Total number of Agents first discovered on endpoints in the last 7 days. Click to identify new AI tools that employees recently attempted to use, facilitating timely compliance assessment. |
|Number of installed endpoints |Total number of endpoints across the network with at least one AI Agent installed, deduplicated by device. This helps assess the overall adoption rate of AI tools in the enterprise. |
|TOP 5 statistics |Displays the top 5 Agents by number of installed endpoints. administrators can use this information to determine whether compliance guidance or centralized procurement is needed. |

## Filter, export, and view asset details

In the asset list, administrators can filter target assets, export inventory results, or open the details page to view version distribution and endpoints where the tool is installed.

The fields in the asset list are described below.

|Field |Description |
|---|---|
|Name |Name of the identified Agent or IDE plugin. |
|Bundle ID / Publisher |Displays the application identifier or software publisher information to help distinguish tool sources. In the **IDE plugin** view, this column is named **Identifier / Publisher** and displays the plugin identifier and publisher. |
|Agent status |Displays the disable configuration status of the tool. You can filter by **normal**, **partially disabled**, or **fully disabled**. |
|Number of installed endpoints |Number of endpoints where the tool is installed. |
|Number of installed users |Number of users who have installed the tool. |
|Actions |Click Details to view version and endpoint distribution. To restrict tool execution, click Disable to configure the scope. |

* **Quick filter**: Switch between the **Agent** and **IDE plugin** tabs to view different types of AI Agent assets. Use conditions such as Agent name, Agent status, and department information to quickly filter target assets.

* **Export**: Click **Export** in the upper\-right corner of the list to export the current asset inventory results.

* **Asset details**: Click **Details** in the actions column of the target Agent to view version distribution and installed endpoints, and identify devices that need upgrades or remediation.

   * **General**: View the Agent version distribution and the installation percentage of each version. If a lower version has known vulnerabilities, use version filtering on the **Devices Installed** tab to find endpoints that need upgrades.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-01.png)

   * **Devices Installed**: Filter affected employees and devices by software version, device information/group, department information, and more. You can view the installation time, running status, and specific installation path of each endpoint. You can also view the current logged\-in user, usage duration, software version, device group, and first discovery time. To export the current results, click **Export** in the upper\-right corner of this tab.

## Disable an Agent

After discovering an Agent that does not meet enterprise access requirements, you can block it from running by employee or device scope. SealSuite disables the Agent by intercepting the startup of related processes. After the disable configuration is saved for active endpoints, it is expected to take effect in 20 minutes.

Before disabling an Agent, confirm the following conditions.

* **administrator permission requirement**: To disable or re\-enable an Agent, the administrator must have the **Disable Agent** permission.

* **macOS permission requirement:**  Disablement control depends on macOS **Full Disk Access (FDA)** .

   * **Recommendation**: Use SealSuite MDM to silently grant FDA permissions in the background, ensuring transparent interception for users.

   * **Caution**: If authorization is not granted through MDM, endpoints will display a permission request pop\-up, which may affect user experience.

* **Priority**: If an employee is configured as exempt from Agent disabling in the [system allowlist](https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-global-allowlist), this setting takes precedence over the disable policy of an individual Agent.

To disable an Agent, perform the following steps:

1. On the **AI Security \> Asset Inventory \> Agent** page, find the target tool in the **Agent** asset list and click **Disable**.

   Disabling can be configured for Agents that have not reported installation information.

2. Configure the following items as needed.

   * **Interception notification**: Turn on the **Notification** switch and click **Modify configuration**. administrators can customize the message pushed to users when interception occurs, with multiple languages supported. The message explains the interception reason and guides users to use enterprise\-approved tools.

   * **Effective conditions**: Select **All objects** or **Partial objects**. If you select partial objects, specify the scope by employee dimensions, including departments, roles, and members, or by device dimensions.

   * **Excluded objects**: Exclude users or devices that do not need to be disabled. For example, disable a tool for the whole company while retaining usage permissions for the testing department.

3. Click **Disable** to save the configuration and wait for the policy to be delivered.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-02.png)

To restore the use of a disabled tool, click **Enable** in the disable configuration panel of the corresponding tool.
