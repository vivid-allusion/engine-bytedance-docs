---
title: "AI Protection Log Audit"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/ai-protection-log-audit"
---

The **Protection Logs** of AI Access Security are the result records after the execution of AI protection policies. The system only records AI interaction behaviors within the scope hit by the policies and converts them into auditable logs. Through detailed log replay and deep traceback, the Administrator can verify whether the policy action meets expectations, and continuously tune the protection rules based on actual business scenarios, forming a closed\-loop governance process from control to audit and then to policy optimization.

 &nbsp;

<span id="view-ai-protection-logs"></span>
## View AI protection logs


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **SWG** \> **AI Access Security** \> **Protection Logs**. The system displays logs by asset type. Administrators can switch between tabs for targeted auditing.


 &nbsp;

<span id="ai-app-/-large-model-api-logs"></span>
## AI App / Large Model API Logs

These logs focus on web\-based conversations, such as ChatGPT and Doubao, and programmatic API calls, such as OpenAI API and Anthropic. Detailed interaction records help administrators identify semantic risks and shadow API risks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/194d92a226d649c5b486f6db12a75efa~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="core-fields"></span>
### Core Fields

In addition to basic fields such as trigger time, user, and device, focus on the following fields to evaluate security risks.


* **Request content**: The raw prompt text or API payload sent to the AI. The system captures and displays this text only if **AI Conversation Content Audit** is enabled in the policy.

* **Triggered policy**: The name of the specific protection rule that triggered the log. Click the policy name to quickly query the detailed policy configuration.

* **Detection classification**: The specific risk type identified by the semantic engine, such as "Role Play" or "Instruction Overriding".

* **Execute Action**: Indicates whether the system performed **Observe** or **Block** on this behavior.

* **Model Provider (Large Model API)** : Displays the name and URL of the called Model Provider. The Administrator can also precisely filter logs through the **Model Provider** and **Model Provider Source Type** (official, transfer station, self\-built, unknown) at the top of the page.


 &nbsp;

<span id="investigate-log-details"></span>
### Investigate log Details

Click **Details** in the **Action** column to enter the details page for in\-depth evidence collection, enabling an audit closed loop from behavior discovery to content determination.


* **Event Details**: Centrally displays the trigger URL, model provider, application name, execute action, and detection classification. It also provides detailed logs, including client IP address and POST path. Click **View Details** to view the original packet and collect underlying network evidence.

* **Context Tracing**: Restores the conversation context based on security audit records. Administrators can replay the complete conversation interaction process to help analyze whether jailbreak or privilege escalation attacks based on long\-context memory exist. This requires **AI Conversation Content Audit** to be enabled in the policy.

* **Subject profile**: Displays the **General** information of the employee who initiated the request, including name, department, and account status, as well as endpoint **Device information**, including OS, device IP, and device ID. This ensures that risks can be accurately located to specific personnel and devices.


 &nbsp;

<span id="log-archiving"></span>
### Log Archiving

For records that have been audited or no longer require attention, click **Archive** in the **Action** column on the log list page. Archived logs are no longer displayed in the list or details. This operation is recorded in administrator audit logs to ensure operational compliance.

 &nbsp;

<span id="mcp-logs"></span>
## MCP Logs

MCP logs provide dedicated auditing for Model Context Protocol services. By recording tool call details between AI applications and external Servers, the system helps administrators make hidden third\-party plugin calls through MCP visible, eliminating audit blind spots in Agent automation execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef6a889eef9640c2a927d27d4f76f789~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="core-fields-1"></span>
### Core Fields

In addition to basic fields such as trigger time, employee, and device, focus on the following fields to quantitatively evaluate security risks.


* **MCP Service**: The identified external MCP Server, such as Amap or Lark Docs. Hover over the name to view its **communication URL**. With this field, administrators can inventory active third\-party tool access points within the enterprise and identify potential supply chain risks.

* **Tool Call**: The specific atomic Tool name called in this interaction, such as `fetch-doc`.

* **Tool Description**: The tool function definition parsed by the system, helping administrators quickly understand the business action intent.


 &nbsp;

<span id="details-and-traceability"></span>
### Details and Traceability

Click **Details** in the **Action** column to enter the event details page for in\-depth evidence collection, enabling an audit closed loop from behavior discovery to content determination.


* **Event Details**: Displays the trigger URL, user subject profile, endpoint device information, and a link to the detailed log. Click **View Details** to view the original request packet and collect underlying network evidence.

* **Tool call information**: Displays the request parameters of this call in JSON format. By viewing plaintext parameters, administrators can accurately determine whether the interaction content is compliant.


 &nbsp;

<span id="cli-logs"></span>
## CLI Logs

CLI logs provide dedicated auditing for developer command\-line tools, such as `github-cli` and `lark-cli`. The system provides fine\-grained API usage details, enabling visibility from “tools” to “behaviors”. Administrators can not only see which CLI tool is running, but also intuitively understand its specific business actions, breaking through the “black\-box” audit blind spot of command\-line tool calls.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f84844a9ff114811b60ce749b28f823b~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="core-fields-2"></span>
### Core Fields

In addition to basic fields such as trigger time, user, device, and execute action, focus on the following core fields to quantitatively evaluate security risks.


* **Application name**: The specific CLI tool identified. Hover over the name to instantly view the complete request URL.

* **Behavior intention**: The call purpose automatically determined by the system, such as calling a custom API or executing Git pull. This helps administrators understand developers’ specific business actions and identify potential non\-compliant logic.

* **Risk level**: The level automatically assigned by the system based on behavior characteristics, including high, medium, and low. This serves as an important basis for troubleshooting priority. If the system preset level does not match the enterprise’s actual business scenario, administrators can go to **Asset Discovery \> CLI** and manually adjust the sensitivity level of the behavior on the details page of the corresponding tool.

* **Triggered policy**: The specific protection rule matched by this behavior. Click the policy name to go directly to the policy configuration page, so administrators can verify rule details or quickly optimize the policy.


 &nbsp;

<span id="details-and-traceability-1"></span>
### Details and Traceability

For any high\-risk or suspicious record, click **Details** in the **Action** column to view event details.


* **Triggered event information**: Centrally displays the trigger URL, triggered policy, intent identification, risk level, and other criteria, clarifying why the behavior was blocked or observed.

* **Detailed log**: Displays network\-layer parameters such as client IP address, complete URL, and User\-Agent. Click **View Details** to view the original packet. Administrators can retrieve the lowest\-level request and response data for in\-depth evidence collection or complex network troubleshooting.

* **Subject profile**: Displays the **General** information of the employee who initiated the request, including name, department, and account status, as well as endpoint **Device information**, including OS, device IP, and device ID. This ensures that risks can be accurately located to specific personnel and devices.


 &nbsp;

<span id="skill-logs"></span>
## Skill Logs

Skill logs provide dedicated audit records for Skill download links of intelligent agents. By identifying risk characteristics of download sources, they help administrators accurately locate high\-risk download behaviors and prevent AI supply chain poisoning risks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c43ebeb0f9f49709e74d785e366e612~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="core-fields-3"></span>
### Core Fields

In addition to basic fields such as trigger time, user, and device, administrators can focus on the following fields to quantitatively evaluate security risks.


* **Destination address**: The complete URL that initiates the Skill download request. Administrators can use this field to inventory active third\-party Skill marketplaces or unconventional download channels within the enterprise and identify shadow Skill assets.

* **Description**: The criteria provided by the threat intelligence engine. High\-risk records usually display specific threat context, such as ClawHub third\-party marketplace or Typosquatting counterfeit packages, helping administrators understand the specific nature of the risk.

* **Risk level**: The level automatically determined by the system based on the intelligence library, including high risk, medium risk, and low risk. This can be used as key reference information for troubleshooting priority.

* **Execute Action**: Indicates whether the system performed **Observe** or **Block** on this behavior. It is used to evaluate the effectiveness of existing protection policies.


 &nbsp;

<span id="details-and-traceability-2"></span>
### Details and Traceability

For any high\-risk or suspicious record, administrators can click **Details** in the **Action** column to enter the details page. By aggregating multi\-dimensional data, this page provides administrators with a complete risk profile and evidence chain, enabling an audit closed loop from risk discovery to accurate identification.


* **Triggered event information**: Centrally displays the event ID, destination address, execute action, and risk level, clarifying why the behavior was blocked or allowed.

* **Detailed log**: Displays original network request details, including client IP address, request method, and complete path. Administrators can use this information for underlying network evidence collection and verify the authenticity of the download behavior.

* **Subject profile**: Displays the **General** information of the employee who initiated the request, including name, department, and account status, as well as endpoint **Device information**, including OS, device IP, and device ID. This ensures that risks can be accurately located to specific personnel and devices.
