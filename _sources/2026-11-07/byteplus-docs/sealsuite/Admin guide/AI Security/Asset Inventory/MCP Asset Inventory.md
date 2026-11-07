---
title: "MCP Asset Inventory"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/mcp-asset-inventory"
---

MCP Asset Inventory identifies external MCP services called by AI applications. It helps administrators understand which Servers are connected, which tools they provide, and how these services are actually called.

## Feature introduction

MCP (Model Context Protocol) connects AI applications with external tools or data services. When employees use AI programming assistants or Agents, they may query information, read business data, or call external tools through MCP Servers. One Server can provide multiple tools (Tool). Therefore, administrators need to understand which services are connected, and review the tools and actual calls for these services.

After traffic diversion and MCP collection are configured, MCP network requests within the effective scope pass through the Secure Web Gateway. The gateway parses MCP protocol interactions, such as obtaining tool lists and calling tools. It records service access addresses, tool information, and call information. For HTTPS traffic, complete the corresponding SSL decryption configuration first. SealSuite summarizes MCP Server assets based on these records.

Administrators can view service sources, tool information, and call information, and use the MCP intelligence library to understand known services. For example, after discovering an unfamiliar Server, first view its developer, service description, and tool definitions to understand its purpose. Then, go to the call logs to verify actual usage.

MCP Asset Inventory depends on enabled collection configurations. To discover unregistered services, enable **Collect unknown MCP**.

## Prerequisites

Before you use network\-side Asset Inventory, complete the following preparations.

* The enterprise has activated the **Secure Web Gateway** license, and the administrator has access permissions for the corresponding menu.

* The enterprise self\-signed root certificate, automatic certificate installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) are configured, so target traffic passes through the Secure Web Gateway. For HTTPS traffic that requires request content inspection, follow the steps in [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies) to configure decryption for target applications or domains.

* AI access security is enabled in **Secure Web Gateway \> AI Access Security**.

* MCP traffic collection is enabled, and an effective employee or device scope is configured. For detailed steps, see the following section.

## Enable MCP traffic collection

The system does not collect MCP traffic by default. **AI Security \> Asset Inventory \> MCP** is used to view assets. Configure the collection scope from either of the following entrances.

* **AI Security entrance**: Go to **AI Security \> Supply Chain Security \> MCP Call Audit**, select the **Policy Management** tab, and click **Policy Management** on the page.

* **Secure Web Gateway entrance**: Go to **Secure Web Gateway \> AI Access Security \> Asset Discovery \> MCP**, and click **Configure Protection Scope**.

After you open the configuration panel, complete the following settings.

1. Enable **Protection Status**.

2. To discover unregistered MCP services within the effective scope, enable **Collect unknown MCP**.

3. Configure **Scope**, and select the scope by **User** (department, role, or member) or **Device**.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-08.png)

1. Click **Confirm** to save.

   After requests that comply with the MCP protocol are generated within the scope, the system identifies and records assets and call information.

## View the asset list

1. Log in to the SealSuite Admin Console, go to **AI Security \> Asset Inventory**, and select the **MCP** tab.

2. Select the statistics period and the **Official** or **Unknown** type. **Official** displays services that match the MCP intelligence library. You can filter by **Category, Developer, and Server Name**. **Unknown** displays services discovered in traffic but not matched in the intelligence library. Click **Expand** to filter by **Authorization status** and **Domain Name**.

3. View the statistics in the asset list.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-09.png)

When an unknown service is not matched in the intelligence library, the category, developer, service description, and official description from the intelligence library are not provided. You can verify the service source based on the collected name, access address, and call records.

The following information is available in the list.

|Field |Description |
|---|---|
|Server Name |The identified MCP service name, used to locate a specific service. For unknown services, the service name collected from traffic is displayed first. If no name is collected, the service access address is displayed. |
|Category |The use category of the MCP service, including productivity, lifestyle, developer tools, design, business, research, finance, marketing, analytics, and legal. You can filter services by category. |
|Developer |Developer information for the MCP service, used to understand the service source. |
|Authorization status |Indicates whether identity verification is required to access the MCP service. The status is determined based on collected traffic information.<br><br><br>* Authentication required: An authentication requirement has been observed for this service.<br><br>* No authentication required: Access without authentication has been observed, and no authentication requirement has been observed yet.<br><br>* Unknown: Existing traffic information is insufficient to determine whether the service requires authentication. |
|Number of Tools |The number of tools identified from the collected tool list for this service. The statistics use the most recent non\-empty tool list and are not reset to 0 based on the current access time filter. If no tool list has been collected, 0 is displayed, even if call records already exist. |
|Number of Requests |The number of MCP tool call requests recorded within the selected time range. Other MCP requests, such as obtaining tool lists, are not counted. Click the number to view tool call logs for this service. |
|Number of Users |The number of employees who use this MCP service. |
|First Discovery Time |The first time the system identified this MCP service. |
|Last Discovery Time |The most recent time the system discovered this MCP service. |

## View MCP details

Select one of the following operations based on the troubleshooting objective.

* **View Server details**: Click **Details** in the operation column of the list to view basic information about the Server, such as the vendor and detailed description, as well as the tools (Tool) it provides and their call frequency. Click **MCP Official Documentation** in the upper\-right corner of the page to open the official documentation or hosted repository for the service. Review tool definitions, parameter specifications, and permission requirements to understand what the tools do, what information must be passed in, and what permissions are required. Then, determine whether the service meets enterprise usage requirements.

* **View the MCP intelligence library**: Click **MCP Intelligence Library** to view preset MCP Server information, covering more than ten categories such as productivity, developer tools, and finance. Search by industry category or keyword to understand the category, purpose, source, and known risks of services in the asset list.

* **View call logs**: Click **Number of Requests** for the target MCP service to go to **AI Security \> Supply Chain Security \> MCP Call Audit \> Audit Log**. View the call records for this service to learn which employee called which tool and when. Click **Details** in a log to view the request parameters passed in during the call and the associated device information.

You can also view MCP assets on the **Secure Web Gateway \> AI Access Security \> Asset Discovery \> MCP** page, and set the collection scope through **Configure Protection Scope**.
