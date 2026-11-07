---
title: "AI Asset Discovery Management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/ai-asset-discovery-management"
---

The **Asset Discovery** feature of AI Access Security is used to inventory all AI assets called by Endpoints within the enterprise. Based on the configured AI protection policies, the system automatically identifies and summarizes generative AI applications used by employees in the office network environment through gateway\-side traffic features, including Web pages, Large Model APIs, MCP and CLI tools, and Skills. By monitoring the access frequency, number of active users, and risk exposure surface of assets in real\-time, the Administrator can achieve policy\-based asset visibility and quantitative governance without manual entry.

 &nbsp;

<span id="prerequisites"></span>
## Prerequisites

The statistics on the Asset Discovery page mainly come from records generated when protection policies are matched.


* **AI App / Large Model API / CLI assets**: Make sure you have completed [Configure AI Protection Policy ](https://docs.byteplus.com/docs/sealsuite/configure-ai-protection-policy). If no protection policy is configured for AI tools, no data is generated in the asset discovery list.

* **MCP assets**: You must enable **Protection Status** on the **Asset Discovery** \> **MCP** tab and configure the effective employee or device scope.

* **Skill assets**: These assets do not depend on specific policy configuration. As long as the global AI Security feature is enabled, the system can automatically identify and record related asset information.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip"><strong>Configure a full audit policy (recommended)</strong>: To implement global asset inventory, we recommend creating a lowest\-priority <strong>full audit</strong> policy in the policy configuration for the corresponding tool type. Select all AI applications, models, or tools, and set the action to <strong>Observe</strong>. This policy serves as the baseline to ensure that all AI access behaviors can be identified and summarized in the asset discovery list.</div>


 &nbsp;

<span id="asset-dashboard:-application-security-posture"></span>
## Asset Dashboard: Application Security Posture

On the **SWG** \> **AI Access Security** \> **Application Security Posture** page in the Admin Console, the system summarizes and displays AI application usage, organizational distribution, and blocking data within the enterprise. This helps administrators evaluate AI usage status and potential risks through quantitative data.


* **Asset discovery dashboard**: Displays access rankings and department distribution of AI applications, Model providers, MCP Servers, and CLI tools in visual cards. You can click a card or a value in the ranking list to drill down to asset management or protection logs and view detailed records.

* **Asset risk distribution**: Intuitively displays the API risk distribution of CLI tools (aggregated by high, medium, and low risks) and the Top 10 list of high\-risk API calls through charts. You can quickly lock onto CLI request behaviors with potential risks and conduct targeted troubleshooting.

* **Security protection capability**: Collects and displays the gateway\-side blocking effectiveness for malicious plugin or Skill downloads, non\-compliant semantics, and risky CLI requests, helping administrators quantify protection outcomes.


 &nbsp;

<span id="asset-management:-asset-discovery-list"></span>
## Asset Management: Asset Discovery List

On the **SWG** \> **AI Access Security** \> **Asset Discovery** sub\-tab, you can view detailed asset information and governance status by asset type, including **AI App**, **Large Model API**, **MCP**, and **CLI**. You can also quickly search for target assets by using filters at the top of the page, such as time range and tool name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebb3aec01bbb4f3faa4afe5ad5ca2072~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="common-fields"></span>
### Common Fields

The system provides the following basic statistical fields for different asset types to help administrators quantitatively evaluate asset activity and control status.


* **Application / Tool name**: The AI asset identifier recognized by the system.

* **Number of Users, Request / Visit Count**: The number of employees using this asset and the total number of calls initiated through the gateway. These fields can be used to evaluate the popularity and usage intensity of the asset within the enterprise and help determine whether targeted control policies are needed.

* **Associated policies**: The number of AI Security policies currently matched by this asset. Click the number to go to the policy list for the corresponding tool under the **Policy Configuration** tab, so administrators can verify the current control status and quickly adjust policy rules.

* **First discovered / Last active time**: The first time the asset was captured by the system and its most recent active time. These fields help identify the asset lifecycle and distinguish legacy assets from newly added shadow assets, enabling timely security governance for new assets.


 &nbsp;

<span id="dedicated-fields"></span>
### Dedicated Fields

 &nbsp;

<span id="ai-app-/-large-model-api-assets"></span>
#### AI App / Large Model API Assets

These two tabs mainly display web\-based AI applications called within the enterprise, such as Doubao, ChatGPT, and Workbuddy, as well as inference service assets called through programmatic APIs.


* **AI App**: Displays common fields such as application name, visit count, associated policies, number of users, and last active time.

* **Large Model API**: In addition to common fields, the system provides deeper quantitative dimensions for API calls:

   * **Model Provider / Model Version**: Identifies and displays the models called by specific inference service providers (such as GPT\-4, DeepSeek\-V3) and their sources (official, transfer station, self\-built, unknown). For unrecognized Model Providers, the system aggregates them under **Unknown Vendors**. Click the expand button ( **+** ) on the left to expand the list and view detailed information.

   * **Domain**: Displays the corresponding domain address requested by the Large Model API. Combined with the domain filter box at the top, you can quickly locate the asset call status under a specific network domain.

   * **Token consumption**: Counts the total token consumption generated by this asset, helping you quantitatively evaluate API usage costs and resource usage.


 &nbsp;

<span id="mcp-assets"></span>
#### MCP Assets

MCP (Model Context Protocol) asset control is used to discover and audit external Servers called by generative AI applications, such as AI coding assistants and AI Agents, through the MCP protocol.

 &nbsp;

<span id="enable-traffic-collection"></span>
##### Enable Traffic Collection

Because the system does not collect MCP traffic by default, you must enable traffic collection before related asset data can be identified and recorded.


1. On the **MCP** tab, click **Configure Protection Scope** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6e148ce423f414a85237114a17fbf9e~tplv-goo7wpa0wc-topic.webp) </span>

2. Turn on the **Protection Status** toggle.

3. Configure effective **Scope** as needed. You can select **User** by department, role, or employee, or select **Device** by device or group.

4. Click **Confirm** to enable the feature.


 &nbsp;

<span id="view-mcp-assets"></span>
##### View MCP Assets


* **View the asset list**: When users within the protection scope initiate traffic calls that comply with the MCP protocol specifications, the gateway can capture and record the asset. In the MCP asset list, you can view the captured Server name, developer, and call popularity (number of requests/users).

* **View the MCP intelligence library**: Click **MCP Intelligence Database** to open a wiki\-style intelligence center. The system provides built\-in MCP Server information across more than ten categories, such as productivity, developer tools, and finance. You can search by industry category or keyword to understand the risk background of known tools and obtain classification labels and background intelligence for assets in the list.

* **View Server details**: Click **Details** in the **Action column** to view basic information about the Server, such as vendor and detailed description, as well as all atomic Tools it provides and their call frequency. This enables visibility from Server to Tool behavior. Click **MCP Official Description** in the upper\-right corner of the page to go directly to the official documentation or hosted repository page of the MCP Server. By viewing the official Tool definitions, parameter specifications, and permission requirements, you can more accurately assess the compliance of related call behaviors.


 &nbsp;

<span id="cli-assets"></span>
#### CLI Assets

For CLI tools, the system further provides a fine\-grained API usage profile. This page centrally displays all API calls identified under the tool, helping administrators understand the usage depth and potential risk distribution of the tool from a global perspective.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c55d31e5fbb4e72923e46ccdaee6b56~tplv-goo7wpa0wc-topic.webp) </span>


* **API call details**: Centrally summarizes all API calls related to the tool, including request methods such as GET, POST, and DELETE, application endpoints (URLs), and identified behavior intents, such as calling a custom API or discovering Git pull services.

* **Sensitivity level calibration**: The system presets sensitivity levels for behaviors. Administrators can manually adjust sensitivity levels based on actual business scenarios. For example, if a behavior that is preset as high risk by the system is a trusted business operation, you can adjust its risk level to low risk, ensuring that asset discovery results better align with the business context and reducing audit noise.

* **Call trend**: The **Requests in the last 7 days** column supports ascending and descending sorting, helping administrators quickly identify the most frequent or most abnormal behavior patterns and quantitatively evaluate the activity level of different behaviors.
