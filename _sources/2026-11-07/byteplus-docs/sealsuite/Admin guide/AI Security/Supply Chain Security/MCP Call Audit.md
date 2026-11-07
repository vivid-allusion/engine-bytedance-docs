---
title: "MCP Call Audit"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/mcp-call-audit"
---

MCP Call Audit records how AI applications access MCP Servers and call tools. It helps the administrator understand which employee called which tool at what time, and which parameters were passed during the call.

## Feature overview

MCP (Model Context Protocol) connects AI applications with external tools or data services. When employees use Agents to query information or call business tools, the administrator must understand which services and tools are actually accessed and check whether the calls comply with enterprise usage requirements.

After traffic diversion and collection are configured, the Secure Web Gateway parses MCP protocol interactions, such as retrieving tool lists and calling tools, and records service access addresses, tool information, and request parameters. **Audit Log** display tool call (`tools/call`) records. Information from retrieving tool lists (`tools/list`) is used to supplement tool names and descriptions, and to aggregate MCP assets. For example, after an unfamiliar tool call is found, the administrator can view the tool description, request parameters, and associated devices to understand the call purpose and involved personnel.

## Prerequisites

Before recording MCP calls, activate the required authorization and route network requests for target services through the Secure Web Gateway. Make sure the following preparations are complete.

* The enterprise has activated **Secure Web Gateway** license, and the administrator has menu and operation permissions for the corresponding features.

* The enterprise self\-signed root certificate, automatic certificate installation scope, and [traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) have been configured, so target traffic passes through the Secure Web Gateway. To inspect HTTPS request content, you must also [configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies).

* AI Access Security has been enabled in **Secure Web Gateway \> AI Access Security**.

## Configure the collection scope

Configure the collection scope to specify the employees or devices whose MCP network requests must be recorded. This configuration is also used for MCP asset discovery and Call Audit.

1. Go to **AI Security \> Supply Chain Security \> MCP Call Audit**, and select the **Policy Management** tab.

2. Click **Policy Management** on the page, and enable **Protection Status**.

3. To discover unregistered MCP services within the scope, enable **Collect Unknown MCP**.

4. Set **Scope**, and select the scope by employee (department, role, or member) or device.

5. Click **Confirm**. After MCP requests are generated within the scope, you can view records in **Audit Log** and view assets in **AI Security \> Asset Inventory \> MCP**.

You can also set the collection scope on the **Secure Web Gateway \> AI Access Security \> Asset Discovery \> MCP** page by using **Configure Protection Scope**.

## View audit logs

To identify which employee called which MCP tool and when, go to **AI Security \> Supply Chain Security \> MCP Call Audit \> Audit Log**. Filter by trigger time, employee, MCP service, tag, authentication status, or domain name. Click **Expand** to view other filter criteria.

You can also view call logs on the **Secure Web Gateway \> AI Access Security \> Protection Logs \> MCP** page.

The main fields in the log list are described below. Use them to verify the accessed MCP service, tool purpose, and associated employees and devices.

|Field |Description |
|---|---|
|MCP Service |The identified external MCP Server, such as Amap and Lark Docs. Hover over the name to view its **communication URL**. This field helps the administrator inventory active third\-party tool access points in the enterprise and identify potential supply chain risks. |
|Tool Name |The specific atomic tool name called in this interaction, such as `fetch-doc`. |
|Tool Description |Displays the tool description parsed from the most recent non\-empty tool list of the service, helping the administrator understand the tool purpose. This field is empty if no corresponding description is collected. |
|Tag |Distinguishes known official services from unknown services. |
|Authorization status |Displays the current authentication status of the accessed MCP service based on collected traffic aggregation.<br><br><br>* **Authenticated**: An authentication requirement has been observed for the service.<br><br>* **Unauthenticated**: Access that does not require authentication has been observed, and no authentication requirement has been observed.<br><br>* **Unknown**: Current information is insufficient for a determination.<br><br><br>This field indicates whether the service requires authentication. To check whether a specific request succeeded, view the status code in the detailed log record. |
|Trigger Time |The time when this MCP tool call occurred. |
|Employee |The employee who initiated the request and the employee's department. |
|Device |The Endpoint device that initiated the request. |

## View call details

To inspect the request content of an MCP call, click **Details** in the operation column of the log entry. View the service address, tool information, call parameters, and associated employees and devices.

* **Event Information**: Displays the trigger URL, employee information, Endpoint device information, and entry point to **detailed log records**. Click **View Details** to view recorded fields in **Basic Information** and **More Information**, including request time, request method, HTTP URL, status code, User\-Agent, source IP address, source port, and request size. Use these fields to verify the request source, destination, and return status.

* **Tool Call Information**: Displays the **request parameters (JSON)**  for this call. By viewing plaintext parameters, the administrator can understand the information passed into the call and determine whether it complies with enterprise usage requirements.
