---
title: "Best practices for resource registration and use in the Application Center"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_resource_registration_and_use_in_the_Application_Center"
---

Application Center is the unified entry point for managing Agent and MCP resources in ArkClaw Enterprise. After administrators complete resource registration, individual Claws within the space can directly discover and invoke these resources without repeated installation or manual configuration in each Claw.

This topic describes how to uniformly register, manage, and publish enterprise AI application resources (Agent, MCP, etc.) in the Application Center.

<span id="wqu2g7sK"></span>
## Resource type

The Application Center supports registration of the following types of AI application assets.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">AgentKit is a development tool platform that BytePlus offers to support the construction, deployment, and operation of AI Agents. It helps developers and enterprises lower the barrier to Agent development. The platform provides Agents with infrastructure beyond models, including security, built\-in tools, memory, knowledge, monitoring, and evaluation. It empowers enterprises to efficiently build, deploy, and operate complex intelligent enterprise\-grade Agents. <a href="https://docs.byteplus.com/en/docs/agentkit/What_is_AgentKit">Learn more</a></div>



|Asset type ||Asset source |
|---|---|---|
|Register an agent |AgentKit Agent |An A2A Agent service registered in AgentKit. [Learn more](https://docs.byteplus.com/en/docs/agentkit/A2A_Center_overview?lang=en) |
||Shared Claw |BytePlus shared Claw exposes a Claw as an Agent resource for invocation by other personal Claws. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Differences_between_shared_and_employee_Claw_instances?lang=en) |
||Custom Agent |An Agent that is developed by a user, supports the A2A communication protocol, and is accessible over the public network. |
|Register an MCP |AgentKit MCP |MCP service in AgentKit. [Learn more](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview?lang=en) |
||Custom MCP |An MCP service that is deployed by a user and accessible over the public network. |


<span id="g05Ca2hb"></span>
## Prerequisites

Ensure that ArkClaw activation and seat purchase have been completed. For detailed instructions, see [Quick start for space activation](https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide).

<span id="wsanrMHJ"></span>
## Register resources

<span id="Md3MMZ3N"></span>
### Register an agent

Enterprise administrators can register A2A\-compliant agents to the Application Center of ArkClaw Enterprise. This enables these agents to be discovered and invoked by ArkClaw instances of employees within the ArkClaw Enterprise space.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To register an application from AgentKit, ensure that your BytePlus root account has already <a href="https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents?lang=en">registered an A2A Agent</a>.</div>


* <div data-tips="true" data-tips-type="default">To register a custom application, prepare in advance the accessible service URL, authentication method, and necessary description.</div>




<Tabs>
<Tab zoneid="buXPDQrcA6" title="AgentKit Agent">
<TabTitle>AgentKit Agent</TabTitle>

This applies to Agents that have already been built in the AgentKit agent runtime. The advantage of this method is its low integration cost, as it typically does not require additional complex authentication parameters.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you need to deploy an Agent using a custom image, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_resource_registration_and_use_in_the_Application_Center?TagIDs=2,522,512,502&lang=en#lpfvmWcX">Custom image deployment guide</a> and complete registration.</div>


<span id="xmgwJ56Q"></span>
#### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" tab, click the "Register agent" button.

4. Refer to the table below to configure agent information.

   
   |Parameter​ |Description |
   |---|---|
   |Term |The name of the Agent application, which is the name displayed when ArkClaw invokes the application. |
   |Unique identifier |The unique identifier of the agent application, used to distinguish it from other applications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The unique identifier of the application is unique within the space and is used for ArkClaw context input. It cannot be modified after the application is created and will directly affect the subsequent resource retrieval and selection experience. We recommend making it as clear and specific as possible.</div><br> |
   |Application description |The description of the agent application.<br><br><br>* It will be used for ArkClaw context input. The description directly affects the effectiveness of ArkClaw's application invocation. We recommend making it as clear and specific as possible.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   An Internet search agent tailored for enterprise research and intelligence analysis scenarios. It automatically retrieves multi\-source web information and organizes key points based on natural language queries. It applies to scenarios such as quickly learning about industry trends, competitor developments, and technical solutions. Typical usage examples: Search for application cases of AIGC in the advertising industry over the past three years and categorize them by scenario. Summarize several authoritative articles on multi\-agent collaborative architecture. |
   |Source |Select **AgentKit** as the application source. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible to and usable by all employees.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible to and cannot be used by any employee. |
   |Associated project |Select the project to which the application belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/ArkClaw/managing_projects?lang=en). |
   |Agent Runtime |Select the agent runtime used to create the agent application.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can only select agent runtimes that meet all the following conditions: within the permission scope of the current BytePlus account, with a status of "Available", using "API Key" or "OAuth" inbound authentication, and supporting the A2A protocol.</div><br> |
   |Application address |Select the accessible address of the agent runtime used to create the agent application.<br><br><br>* If the accessible address of the application supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw.<br><br>* If the accessible address of the application supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management#m6CBEaSE) in this topic.instructions.instructions.<br><br>* If the accessible address of the application supports both "Public network" access and "Private network" access, configure either public network egress or private network egress based on your needs to ensure ArkClaw can access the address. |
   

5. Click the "Confirm" button to complete the configuration.


</Tab>
<Tab zoneid="j4i5FXtnQW" title="Shared Claw instance">
<TabTitle>Shared Claw instance</TabTitle>

This applies to scenarios where an existing Claw is shared as an A2A Agent for use by other personal Claws.

<span id="0Y3VsGO2"></span>
#### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" tab, click the "Register agent" button.

4. Refer to the table below to configure agent information.

   
   |Parameter​ |Description |
   |---|---|
   |Term |The name of the Agent application, which is displayed when ArkClaw invokes the application. |
   |Unique identifier |The unique identifier of the agent application, used to distinguish it from other applications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The unique identifier of the application is unique within the space and is used for ArkClaw context input. It cannot be modified after the application is created and will directly affect the subsequent resource retrieval and selection experience. We recommend making it as clear and specific as possible.</div><br> |
   |Application description |The description of the agent application.<br><br><br>* It will be used for ArkClaw context input. The description directly affects the effectiveness of ArkClaw's application invocation. We recommend making it as clear and specific as possible.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   An Internet search agent tailored for enterprise research and intelligence analysis scenarios. It automatically retrieves multi\-source web information and organizes key points based on natural language queries. It applies to scenarios such as quickly learning about industry trends, competitor developments, and technical solutions. Typical usage examples: Search for application cases of AIGC in the advertising industry over the past three years and categorize them by scenario. Summarize several authoritative articles on multi\-agent collaborative architecture. |
   |Source |Select **Shared Claw** as the application source. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible to and usable by all employees.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible to and cannot be used by any employee.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For agents from the "Shared Claw" source, the administrators of the shared Claw instances have permission to use these applications by default. Even if you set this parameter to "Deny all", the administrators can still view, manage, and access these agents in the console for employees.   </div><br>    |
   |Template |Select a template for creating the shared Claw. Currently, only the "ArkClaw Q&A assistant" and "General knowledge Q&A assistant" templates are supported. [What are the differences between shared Claw and employee Claw?](https://docs.byteplus.com/en/docs/ArkClaw/Differences_between_shared_and_employee_Claw_instances?lang=en)<br><br><br>* **Edition configuration**: Select the seat edition for creating the shared Claw.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A shared Claw is a space\-level ArkClaw instance. Registering an agent application via a shared Claw creates a shared Claw instance based on the selected template. This instance consumes one seat of the corresponding edition in the current space.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Created shared Claws in the current ArkClaw workspace can be viewed under "Claws" in "Instances" \> "Shared Claw" in the ArkClaw console.   </div><br>   <br><br>* **Other configurations**: Click the "Professional soul", "Platform guidelines", "Built\-in plugins", and "Built\-in skills" tabs respectively to view the corresponding template information. You can refer to the [Best practices for defining shared claw templates](https://docs.byteplus.com/en/docs/87732/2522333) to modify the template to match your own business requirements.<br><br>   * ArkClaw Q&A assistant: A Volcanic Engine after\-sales expert. It comes with a pre\-built skill that can call the public VikingDB knowledge base (continuously updated and maintained by the Volcanic Engine technical support team), deeply integrating ArkClaw product expertise to handle customer inquiries during ArkClaw usage.<br><br>   * General knowledge Q&A assistant: A knowledge Q&A expert suitable for multi\-industry Q&A scenarios, with a unified knowledge source from the OpenViking knowledge base. Users can modify the agent configuration file themselves to maintain knowledge data for specific industries and domains. |
   |Administrator |Add employees who can manage the shared Claw as its administrators.<br><br><br>* Employees who are shared Claw administrators: They can manage the shared Claw instances and internal agents, manage knowledge imports, and use the shared Claw instances.<br><br>* Employees who are not shared Claw administrators: If authorized, they can use the shared Claw instance.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you cannot find the target employee, the employee's information may be missing. Go to "User management" to check and complete the employee's information. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.</div><br> |
   

5. Click the "Confirm" button to complete the configuration.


</Tab>
<Tab zoneid="pG3uqbiRs9" title="Custom Agent">
<TabTitle>Custom Agent</TabTitle>

This applies to integrating externally developed in\-house Agent services. This method offers high flexibility, but has clear requirements for protocol compatibility and network accessibility.

<span id="CEXm8Fc1"></span>
#### Integration requirements


* The Agent service must support the A2A communication protocol.

* The Agent service must be accessible over the public network.


<span id="veXVI5TA"></span>
#### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" tab, click the "Register agent" button.

4. Refer to the table below to configure agent information.

   
   |Parameter​ |Description |
   |---|---|
   |Term |The name of the Agent application, which is the name displayed when ArkClaw invokes the application. |
   |Unique identifier |The unique identifier of the agent application, used to distinguish it from other applications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The unique identifier of the application is unique within the space and is used for ArkClaw context input. It cannot be modified after the application is created and will directly affect the subsequent resource retrieval and selection experience. We recommend making it as clear and specific as possible.</div><br> |
   |Application description |The description of the agent application.<br><br><br>* It will be used for ArkClaw context input. The description directly affects the effectiveness of ArkClaw's application invocation. We recommend making it as clear and specific as possible.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   An Internet search agent tailored for enterprise research and intelligence analysis scenarios. It automatically retrieves multi\-source web information and organizes key points based on natural language queries. It applies to scenarios such as quickly learning about industry trends, competitor developments, and technical solutions. Typical usage examples: Search for application cases of AIGC in the advertising industry over the past three years and categorize them by scenario. Summarize several authoritative articles on multi\-agent collaborative architecture. |
   |Source |Select **Custom** as the application source. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible to and usable by all employees.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible to and cannot be used by any employee. |
   |Access authentication |Select the access method for the Agent application.<br><br><br>* **No authentication required**: This is the default method and does not require access authentication.<br><br>* **API Key**: Select the target API key from the drop\-down list.<br><br>* **OAuth JWT**: Select the target credential from the drop\-down list.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">‌Agent access authentication is governed solely by the <strong>Access authentication</strong> settings. The security field in the AgentCard JSON file ‌is not read by the system and will ‌not take effect even if configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click "Add credential" in the drop\-down list to add a new credential. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management">Credential management</a>.</div><br> |
   |Import method |Select the import method for the agent application. Two import formats are supported: JSON and AgentCard URL. Supported authentication types include API Key and OAuth JWT.<br><br><br>* **Import methods:** <br><br>   * **JSON**: Paste the JSON file directly. You can edit the file content online.<br><br>   * **AgentCard**: AgentCard is a standardized information carrier of the A2A agent in its space, which contains core attributes such as ID, name, protocol version, and communication mode. AgentCard is associated with the corresponding A2A agent space. For this method, enter the AgentCard address, click "Parse" to manually parse the content, and edit the file content online.<br><br>* **Import requirements**:<br><br>   * **Format requirements**: For the specifications including the definition, value range, and validation rule of each field in the JSON file, refer to the [official A2A protocol documentation](https://a2a-protocol.org/latest/specification/#441-agentcard). A sample JSON file is provided in [Sample A2A agent JSON file](https://docs.byteplus.com/en/docs/ArkClaw/Sample_A2A_agent_JSON_file).<br><br>   * **Network requirements**: The "url" in the directly pasted JSON file or the JSON file parsed from the AgentCard address is the accessible address of the application. Configure the corresponding network egress based on the access method of this address:<br><br>      * If the address supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw.<br><br>      * If the address supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management#m6CBEaSE) in this topic.<br><br>      * If the address supports both "Public network" access and "Private network" access, configure either public network egress or private network egress based on your needs to ensure ArkClaw can access the address. |
   

5. Click the "Confirm" button to complete the configuration.


</Tab>
</Tabs>


<span id="MPDmmdQZ"></span>
### Register an MCP

Enterprise administrators can register internal MCP (Model Context Protocol ) services or toolkits to the Application Center. This enables these MCP services or toolkits to be discovered and invoked by ArkClaw instances of employees within the ArkClaw Enterprise space.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To register an application from AgentKit, ensure that your BytePlus root account has already <a href="https://docs.byteplus.com/en/docs/agentkit/MCP_services">created an MCP service</a>.</div>


* <div data-tips="true" data-tips-type="default">To register a custom application, prepare in advance the accessible service URL, authentication method, and necessary description.</div>




<Tabs>
<Tab zoneid="eg9FSYBBR0" title="AgentKit MCP">
<TabTitle>AgentKit MCP</TabTitle>

This applies to MCP services that have already been created in the AgentKit Gateway.

<span id="TjeQIhAG"></span>
#### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. Under the "Enterprise Agent" tab, click the "Register MCP" button.

4. Refer to the table below to configure MCP information.

   
   |Parameter​ |Description |
   |---|---|
   |Term |The name of the MCP application, which is displayed when ArkClaw calls the application. |
   |Unique identifier |The unique identifier of the MCP application, used to distinguish it from other applications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The unique identifier of the application is unique within the space and is used for ArkClaw context input. It cannot be modified after the application is created and will directly affect the subsequent resource retrieval and selection experience. We recommend making it as clear and specific as possible.</div><br> |
   |Application description |The description information for the MCP application.<br><br><br>* It will be used for ArkClaw context input. The description directly affects the effectiveness of ArkClaw's application invocation. We recommend making it as clear and specific as possible.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   * A model context protocol server that provides web content crawling capabilities. It enables large language models to retrieve and process content from web pages, and converts HTML into Markdown for easier utilization. |
   |Source |Select "AgentKit" as the application source. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible to and usable by all employees.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible to and cannot be used by any employee. |
   |Associated project |Select the project to which the application belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/ArkClaw/managing_projects?lang=en). |
   |MCP |Select the MCP service or MCP to register and use. |
   |Application address |The address of the MCP application.<br><br><br>* **Address type:** <br><br>   * When the application source is "AgentKit", select the source address of the MCP application from the drop\-down list.<br><br>   * When the application source is "Custom", manually enter the source address of the MCP application.<br><br>* **Network requirements**:<br><br>   * If the accessible address of the application supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw.<br><br>   * If the accessible address of the application supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management#m6CBEaSE) in this topic.instructions.<br><br>   * If the accessble address of the application supports both "Public network" access and "Private network" access, configure either public network egress or private network egress based on your needs to ensure ArkClaw can access the address. |
   

5. Click the "Confirm" button to complete the configuration.


</Tab>
<Tab zoneid="c2F59XfKyS" title="Custom MCP">
<TabTitle>Custom MCP</TabTitle>

This applies to integrating self\-built or third\-party hosted MCP services.

<span id="ujMxJ6HM"></span>
#### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. Under the "Enterprise Agent" tab, click the "Register MCP" button.

4. Refer to the table below to configure MCP information.

   
   |Parameter​ |Description |
   |---|---|
   |Term |The name of the MCP application, which is displayed when ArkClaw calls the application. |
   |Unique identifier |The unique identifier of the MCP application, used to distinguish the application from other applications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The unique identifier of the application is unique within the space and is used for ArkClaw context input. It cannot be modified after the application is created and will directly affect the subsequent resource retrieval and selection experience. We recommend making it as clear and specific as possible.</div><br> |
   |Application description |The description information for the MCP application.<br><br><br>* It will be used for ArkClaw context input. The description directly affects the effectiveness of ArkClaw's application invocation. We recommend making it as clear and specific as possible.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   * A model context protocol server that provides web content crawling capabilities. It enables large language models to retrieve and process content from web pages, and converts HTML into Markdown for easier utilization. |
   |Source |Select "Custom" as the application source. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible to and usable by all employees.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible to and cannot be used by any employee. |
   |Protocol |Currently, only the **Streamable HTTP** protocol is supported. |
   |Application address |The address of the MCP application.<br><br><br>* **Address type:** <br><br>   * When the application source is "AgentKit", select the source address of the MCP application from the drop\-down list.<br><br>   * When the application source is "Custom", manually enter the source address of the MCP application.<br><br>* **Network requirements**:<br><br>   * If the accessible address of the application supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw.<br><br>   * If the accessible address of the application supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management#m6CBEaSE) in this topic.instructions.<br><br>   * If the accessble address of the application supports both "Public network" access and "Private network" access, configure either public network egress or private network egress based on your needs to ensure ArkClaw can access the address. |
   |Access authentication |Select the access method for the application.<br><br><br>* **No authentication required**: This is the default method and does not require access authentication.<br><br>* **API Key**: Select the target API key from the drop\-down list.<br><br>* **OAuth JWT**: Select the target credential from the drop\-down list.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click "Add credential" in the drop\-down list to add a new credential. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management">Credential management</a>.</div><br> |
   

5. Click the "Confirm" button to complete the configuration.


</Tab>
</Tabs>


<span id="e5KsnFFU"></span>
## Resource usage guide

After registration, resources will enter the unified resource pool of the Enterprise edition and can be invoked in the ArkClaw client via natural language or shortcut commands.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Before using resources, enterprise users need to complete the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_?lang=en">application process for an ArkClaw instance</a> and <a href="https://docs.byteplus.com/en/docs/ArkClaw/Initiating_tasks">start a task</a> in the client.</div>


* <div data-tips="true" data-tips-type="default">The visibility of enterprise applications to employees is controlled by enterprise administrators. Specifically, it is subject to the "access permissions" they set when <a href="https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_resource_registration_and_use_in_the_Application_Center?lang=en#wsanrMHJ">registering Agents and MCPs</a>.</div>



<span id="I2LXPWkb"></span>
### Agent usage

After an Agent is successfully registered, enterprise users can invoke it in the following two ways. For details, see [Using enterprise applications](https://docs.byteplus.com/en/docs/ArkClaw/Using_enterprise_applications_?_vtm_=a106466.b106468.0_0.0_0.0.4083_7611000293480416809).


<Tabs>
<Tab zoneid="MmJjOQoUYK" title="Natural language invocation">
<TabTitle>Natural language invocation</TabTitle>

Describe the task directly in the dialog, and ArkClaw will automatically select or invoke the relevant Agent.


</Tab>
<Tab zoneid="M2KgKvBgDY" title="@ Command invocation">
<TabTitle>@ Command invocation</TabTitle>

Use `@` to specify the target Agent.


</Tab>
</Tabs>


<span id="I56FBKtO"></span>
### MCP usage

After an MCP resource is successfully registered, users can invoke it in the following two ways. For details, see [Using enterprise applications](https://docs.byteplus.com/en/docs/ArkClaw/Using_enterprise_applications_?_vtm_=a106466.b106468.0_0.0_0.0.4083_7611000293480416809).


<Tabs>
<Tab zoneid="AeiQNMoX" title="Natural language invocation">
<TabTitle>Natural language invocation</TabTitle>

Describe the task directly in the dialog, and ArkClaw will automatically select or invoke the relevant Agent.


</Tab>
<Tab zoneid="BYzZIohK" title="/ Command invocation">
<TabTitle>/ Command invocation</TabTitle>

Use `/` to specify the target MCP service.


</Tab>
</Tabs>


<span id="IjDyioaO"></span>
### Plugin installation and update

In ArkClaw Enterprise, the communication capabilities of Agents and MCPs, as well as the discovery capability for newly registered resources, typically rely on plugins that comply with the OpenClaw standard. We recommend installing the latest plugins to use the full feature set.


<Tabs>
<Tab zoneid="VyeVxbwpHN" title="Automatic installation">
<TabTitle>Automatic installation</TabTitle>

1. By default, plugins are installed together with ArkClaw.

2. If a pop\-up window appears when you use `@` or `/` for the first time, follow the on\-screen instructions to enable, install, or update the plugin.

3. After the plugin installation is complete, close the terminal window and return to the conversation interface to continue using the resource.





</Tab>
<Tab zoneid="zd0poA2OrF" title="Manual installation">
<TabTitle>Manual installation</TabTitle>

If `@` or `/` fails to trigger resource invocation properly, you can enter the [ArkClaw terminal](https://docs.byteplus.com/en/docs/ArkClaw/Accessing_ArkClaw_from_terminals_) and run the following command:

```Bash
curl -fsSL https://mse.tos-cn-beijing.volces.com/arkclaw/upgrade.py | python
```





</Tab>
</Tabs>


<span id="5edUszF5"></span>
## Appendix

<span id="lpfvmWcX"></span>
### How to deploy an Agent with a custom image?


1. Push the image.

   1. Install docker commands in the local environment.

   2. Go to the [BytePlus Container Registry](https://console.byteplus.com/cr).

   3. Click the "Enter Instance" button on the card of the target instance. If no instance exists, [create a standard instance](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

   4. In the Overview page, save the access domain.

   5. In the left navigation pane, select "Namespace" and save the name of the created namespace. If no namespace exists, [create a namespace](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

   6. In the left navigation pane, select "Overview", click the "Get temporary access instruction" button, and in the pop\-up window, click the "Copy" icon to copy the generated login command.

   7. Open the terminal and enter the copied login command.

   8. Enter the command to push the image (in this example, the image names are openclaw\-a2a and fin\-a\-share\-mcp). Replace the highlighted content in the command.

      ```Bash
      IMG_DM=xxxx-Region.cr.volces.com #Replace with the access domain of the Container Registry instance
      IMG_NS=superagent #Replace with the access domain of the Container Registry instance
      for i in openclaw-a2a:0428-2 fin-a-share-mcp:f8a0d40; do # In this example, the image names are openclaw-a2a and fin-a-share-mcp
        docker pull agentkit-platform-2107625663-cn-beijing.cr.volces.com/agentkit/$i
        docker tag  agentkit-platform-2107625663-cn-beijing.cr.volces.com/agentkit/$i $IMG_DM/$IMG_NS/$i
        docker push $IMG_DM/$IMG_NS/$i
      done
      ```
      

2. Deploy MCP and Claw service.

   1. Log in to the [AgentKit agent runtime console](https://console.byteplus.com/agentkit/region:agentkit+cn-beijing/runtime?pageSize=10&currentPage=1).

   2. Click the "Create agent" button. The table below only describes parameters relevant to this example. For other parameters, see [Creating a runtime (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

      
      |Parameter​ |Description |
      |---|---|
      |Image |You need to select "Custom image \> Select from Container Registry", and choose the previously used Container Registry instance, namespace, and the pushed image fin\-a\-share\-mcp. |
      

         3. Click the "Create" button and wait for the publication, i.e., the MCP Server deployment, to complete.

   4. Click the Agent name and save the public domain and API Key in the "**Quick call"**  section at the top.

   5. Click the "Create agent" button again. The table below only describes parameters relevant to this example. For other parameters, see [Creating a runtime (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

      
      |Parameter​ |Description |
      |---|---|
      |Image |You need to select "Custom image \> Select from Container Registry", and choose the previously used Container Registry instance, namespace, and the pushed image openclaw\-a2a. |
      |Environment variables |Select "JSON\-formatted editing" and replace the highlighted content in the command.<br><br>```Bash```<br>```{```<br>```  "MCP_URL": "https://xxxxx.com/mcp/", # Replace with the public domain of the created Agent and append /mcp/ to the public domain.```<br>```  "MCP_APIKEY": "xxxx", # Replace with the API Key of the created Agent.```<br>```  "MODEL_API_KEY": "xxxx", # Replace with the API Key of the LLM. See How to obtain an API Key of a large model.```<br>```  "MODEL_BASE_URL": "https://ark.cn-beijing.volces.com/api/v3/",```<br>```  "MODEL_NAME": "doubao-seed-1-8-251228"```<br>```}```<br><br><br> |
      

         6. Click the "Create" button and wait for the publication, i.e., the deployment of the Claw instance that supports the A2A protocol, to complete.

         7. (Optional) You can run the following command for debugging. Replace the highlighted content in the command.

      ```JSON
      curl https://Replace with the public domain of the created Agent/a2a/jsonrpc -H authorization:Bearer\Replace with the API Key of the created Agent -H content-type:application/json -d '{
        "jsonrpc": "2.0",
        "id": "unique-request-id",
        "method": "message/send",
        "params": {
          "message": {
            "parts": [{"kind": "text", "text": "Who are you"}],
            "messageId": "unique-message-id", "role": "user"
          }
        }
      }
      '
      ```
