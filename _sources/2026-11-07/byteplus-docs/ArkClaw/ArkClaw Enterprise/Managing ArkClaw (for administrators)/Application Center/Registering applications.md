---
title: "Registering applications"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Application_management"
---

This topic describes how to centrally register, manage, and publish AI application assets (agents, MCPs, and more) in the Application Center. The ArkClaw Enterprise Application Center provides a unified platform for registering and managing existing corporate AI application assets. Administrators can integrate and publish the existing corporate AI capabilities, including agents and MCPs (Method, Capability, and Plugin), to build an enterprise\-grade AI asset library. This library can be easily discovered, securely invoked, and efficiently managed by ArkClaw instances of employees within the space.

<span id="pahN4LCP"></span>
## Prerequisites

Before you perform any operations, make sure the following conditions are met:


* The applications (agents or MCPs) to be registered must be accessible via the network. The Application Center does not provide additional gateway proxy services. Network reachability depends on the network configuration of your ArkClaw Enterprise space.

* To register applications sourced from AgentKit, ensure that your BytePlus account has permissions to access the corresponding AgentKit resources.


<span id="4ayGbJah"></span>
## Access authentication description


* Applications sourced from AgentKit: Runtimes and MCPs support registration via API key and OAuth JWT authentication.

* Applications sourced from custom MCPs: They support no authentication, API key authentication, or OAuth JWT authentication.

* Applications sourced from custom agents: They support no authentication, API key authentication, or OAuth JWT authentication.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If API key or OAuth JWT authentication is used, you can create the credentials in advance on the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management">Credentials</a> page, and the system will automatically use the selected credentials for authentication when invoking the application.</div>


<span id="ffFj89xH"></span>
## Registering applications

<span id="Mxxy9IhZ"></span>
### Register an agent

Enterprise administrators can register A2A\-compliant agents in the Application Center of ArkClaw Enterprise. This enables these agents to be discovered and invoked by Claw instances of employees within the space.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise agent" tab, click the "Register agent" button.

4. Refer to the table below to configure agent information.

   
   <Tabs>
   <Tab zoneid="GajoKjy279" title="AgentKit">
   <TabTitle>AgentKit</TabTitle>
   
   The following table describes parameters and their settings for applications sourced from AgentKit.
   
   
   |Parameter​ |Description |
   |---|---|
   |Term |Unique application identifier for the agent application.<br><br><br>* When the application is called by another Claw, this name will be used as the context input for the Client Claw.<br><br>* The name must be 2 to 64 characters long, and the total length after UTF\-8 encoding must not exceed 64 bytes. Chinese characters, English letters, digits, underscores (_), and hyphens (\-) are supported. **You cannot modify the application after you create it.** <br><br>* **Application names must be unique within the ArkClaw Enterprise space. Agent and MCP applications cannot use the same name.**  |
   |Application description |The description of the agent application.<br><br><br>* This information is used as context input for Claw. The description directly affects the result of application invocation by Claw. The description can be 1 to 4,000 characters in length.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   An Internet search agent tailored for enterprise research and intelligence analysis scenarios. It automatically retrieves multi\-source web information and organizes key points based on natural language queries. It applies to scenarios such as quickly learning about industry trends, competitor developments, and technical solutions. Typical usage examples: Search for application cases of AIGC in the advertising industry over the past three years and categorize them by scenario. Summarize several authoritative articles on multi\-agent collaborative architecture. |
   |Source |Select the application source. For this example, select **AgentKit** to indicate that the application is sourced from the agent runtime registered in AgentKit. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible and available to all users.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible and unavailable to all users. |
   |Access Scope |**This parameter is required only when the access permission is set to "Controlled Access"** . Click "Add" to add departments, user groups, or specified users who can access this agent application. |
   |Associated project |Select the project to which the application belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/ArkClaw/managing_projects?lang=en). |
   |Agent Runtime |Select the agent runtime used to create the agent application.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can only select agent runtimes that meet all the following conditions: within the permission scope of the current BytePlus account, with a status of "Available", using "API Key" or "OAuth" inbound authentication, and supporting the A2A protocol.</div><br> |
   |Application address |Select the accessible address of the agent runtime used to create the agent application.<br><br><br>* If the accessible address of the application supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw.<br><br>* If the accessible address of the application supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management?TagIDs=2,522,512,502&lang=en#wfChbm5u) in this topic.instructions.instructions.<br><br>* If the accessible address of the application supports both "Public network" and "Private network" access, configure either public or private network egress as needed to ensure ArkClaw can access the address. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="vw1Xyj8zTE" title="Shared Claw">
   <TabTitle>Shared Claw</TabTitle>
   
   The following table describes parameters and their settings for applications sourced from a shared Claw.
   
   
   |Parameter​ |Description |
   |---|---|
   |Term |Unique application identifier for the agent application.<br><br><br>* When the application is called by another Claw, this name will be used as the context input for the Client Claw.<br><br>* The name must be 2 to 64 characters long, and the total length after UTF\-8 encoding must not exceed 64 bytes. Chinese characters, English letters, digits, underscores (_), and hyphens (\-) are supported. **You cannot modify the application after you create it.** <br><br>* **Application names must be unique within the ArkClaw Enterprise space. Agent and MCP applications cannot use the same name.**  |
   |Application description |The description of the agent application.<br><br><br>* This information is used as context input for Claw. The description directly affects the result of application invocation by Claw. The description can be 1 to 4,000 characters in length.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   An Internet search agent tailored for enterprise research and intelligence analysis scenarios. It automatically retrieves multi\-source web information and organizes key points based on natural language queries. It applies to scenarios such as quickly learning about industry trends, competitor developments, and technical solutions. Typical usage examples: Search for application cases of AIGC in the advertising industry over the past three years and categorize them by scenario. Summarize several authoritative articles on multi\-agent collaborative architecture. |
   |Source |* Agent applications registered via "Shared Claw" will have their corresponding Claw instances displayed in both the **Application Center** and **Claws**.<br><br>* A shared Claw can only be deleted synchronously when you deregister the application in the Application Center. Deletion from the "Claws" is not supported. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible and available to all users.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible and unavailable to all users.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For agents from the "Shared Claw" source, the administrators of the shared Claw instances have permission to use these applications by default. Even if you set this parameter to "Deny all", the administrators can still view, manage, and access these agents in the console for employees.   </div><br>    |
   |Access Scope |**This parameter is required only when the access permission is set to "Controlled Access"** . Click "Add" to add departments, user groups, or specified users who can access this agent application. |
   |Template |Select the template for creating a shared Claw instance. The drop\-down list displays only agent templates available for shared Claw instances. [What are the differences between a shared Claw and an employee Claw?](https://docs.byteplus.com/en/docs/ArkClaw/Differences_between_shared_and_employee_Claw_instances?lang=en) |
   |Specifications |Select the seat edition for creating the shared Claw.<br><br><br>* A shared Claw is a space\-level Claw instance. Registering an agent application via a shared Claw creates a shared Claw instance based on the selected template. This instance consumes one seat of the corresponding edition in the current space.<br><br>* Claw instances created in the current ArkClaw space are listed under "Claws \> Instances \> Shared Claw" in the ArkClaw console.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Shared Claw instances do not support the following models:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">AgentPlan models</div><br><br><br>* <div data-tips="true" data-tips-type="warning">CodingPlan models</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Custom models with employee\-configured API keys</div><br><br><br><br><div data-tips="true" data-tips-type="warning">If the default model for the space that uses the selected edition is one of the above types, the shared Claw will be temporarily unavailable after creation. The administrator needs to switch to a supported model in the employee\-side console.</div><br> |
   |Professional profile / Built\-in skills |You can click the "Professional soul" and "Built\-in skills" tabs to view the corresponding template information. <br><br><br>   * ArkClaw Q&A assistant: A Volcanic Engine after\-sales expert. It comes with a pre\-built skill that can call the public VikingDB knowledge base (continuously updated and maintained by the Volcanic Engine technical support team), deeply integrating ArkClaw product expertise to handle customer inquiries during ArkClaw usage.<br><br>   * General knowledge Q&A assistant: A knowledge Q&A expert suitable for multi\-industry Q&A scenarios, with a unified knowledge source from the OpenViking knowledge base. Users can modify the agent configuration file themselves to maintain knowledge data for specific industries and domains. |
   |Administrator |Add employees who can manage the shared Claw as its administrators.<br><br><br>* Employees who are shared Claw administrators: They can manage the shared Claw instances and internal agents, manage knowledge imports, and use the shared Claw instances.<br><br>* Employees who are not shared Claw administrators: If authorized, they can use the shared Claw instance.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you cannot find the target employee, the employee's information may be missing. Go to "User management" to check and complete the employee's information. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.</div><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="dw7JkhfrDg" title="Custom">
   <TabTitle>Custom</TabTitle>
   
   The following table describes parameters and their settings for applications from a custom source.
   
   
   |Parameter​ |Description |
   |---|---|
   |Term |Unique application identifier for the agent application.<br><br><br>* When the application is called by another Claw, this name will be used as the context input for the Client Claw.<br><br>* The name must be 2 to 64 characters long, and the total length after UTF\-8 encoding must not exceed 64 bytes. Chinese characters, English letters, digits, underscores (_), and hyphens (\-) are supported. **You cannot modify the application after you create it.** <br><br>* **Application names must be unique within the ArkClaw Enterprise space. Agent and MCP applications cannot use the same name.**  |
   |Application description |The description of the agent application.<br><br><br>* This information is used as context input for Claw. The description directly affects the result of application invocation by Claw. The description can be 1 to 4,000 characters in length.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   An Internet search agent tailored for enterprise research and intelligence analysis scenarios. It automatically retrieves multi\-source web information and organizes key points based on natural language queries. It applies to scenarios such as quickly learning about industry trends, competitor developments, and technical solutions. Typical usage examples: Search for application cases of AIGC in the advertising industry over the past three years and categorize them by scenario. Summarize several authoritative articles on multi\-agent collaborative architecture. |
   |Source |Select the application source. For this example, select **Custom** to indicate that a custom agent application is used. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible and available to all users.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible and unavailable to all users. |
   |Access Scope |**This parameter is required only when the access permission is set to "Controlled Access"** . Click "Add" to add departments, user groups, or specified users who can access this agent application. |
   |Access authentication |Select the access method for the Agent application.<br><br><br>* **No authentication required**: This is the default method and does not require access authentication.<br><br>* **API Key**: Select the target API key from the drop\-down list.<br><br>* **OAuth JWT**: Select the target credential from the drop\-down list.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The authentication method for the Agent is decided by the <strong>Access authentication</strong> option, not the <code>security</code> field in the AgentCard JSON file. It means that the field will not be used by the system even if you assign it a value.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click "Add credential" in the drop\-down list to add a new credential. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management">Credential management</a>.</div><br> |
   |JWT identity token |You can configure this parameter only when "Access authentication" is **No authentication required**, **API Key**, or **OAuth JWT**, and the credential type is "Machine\-to\-machine". This parameter specifies whether to include the caller's identity information when requesting the agent.<br><br><br>* **Disabled** (default): The platform does not issue an additional identity token. This option is suitable for scenarios where the agent service does not need to identify specific callers.<br><br>* **Enabled**: The platform attaches an identity token to each agent request via the `x-arkclaw-jwt` header. The agent service can use this token to identify callers and perform signature verification, confirming that the request source is legitimate and the identity information is trustworthy. This option is suitable for scenarios that require permission control, data isolation, or audit logs by user.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For information about how to obtain and verify the token, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Sample_code_for_obtaining_a_JWT_and_decoding_and_verifying_its_signature">JWT acquisition and sample code for decoding and signature verification</a>.</div><br> |
   |Import method |Select the import method for the agent application. Two import formats are supported: JSON and AgentCard URL. Supported authentication types include API Key and OAuth JWT.<br><br><br>* **Import methods:** <br><br>   * **JSON**: Paste the JSON file directly. You can edit the file content online.<br><br>   * **AgentCard**: AgentCard is a standardized information carrier of the A2A agent in its space, which contains core attributes such as ID, name, protocol version, and communication mode. AgentCard is associated with the corresponding A2A agent space. For this method, enter the AgentCard address, click "Parse" to manually parse the content, and edit the file content online.<br><br>* **Import requirements**:<br><br>   * **Format requirements**: For the specifications, including the definition, value range, and validation rule of each field in the JSON file, refer to the [official A2A protocol documentation](https://a2a-protocol.org/latest/specification/#441-agentcard). For a sample JSON file, see [Sample A2A agent JSON file](https://docs.byteplus.com/en/docs/ArkClaw/Sample_A2A_agent_JSON_file).<br><br>   * **Network requirements**: The `url` in the directly pasted JSON file or the JSON file parsed from the AgentCard address is the accessible address of the application. Configure the corresponding network egress based on the access method of this address:<br><br>      * If the address supports only "Public network" access, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw space.<br><br>      * If the address supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw space, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management?TagIDs=2,522,512,502&lang=en#wfChbm5u) in this topic.instructions.instructions.<br><br>      * If the address supports both "Public network" and "Private network" access, configure either public or private network egress as needed to ensure the ArkClaw space can access the address. |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Click the "Confirm" button to complete the configuration.


<span id="GFpXHMi7"></span>
### Register an MCP

Enterprise administrators can register internal MCP (Model Context Protocol) services or toolkits to the Application Center. This enables these MCP services or toolkits to be discovered and invoked by ArkClaw instances of employees within the ArkClaw Enterprise space.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left\-side navigation pane, select "Capability Center \> Application Center".

3. On the "Enterprise MCP" tab, click the "Register MCP" button.

4. Refer to the table below to configure MCP information.

   
   <Tabs>
   <Tab zoneid="vnvqPsYxwW" title="AgentKit">
   <TabTitle>AgentKit</TabTitle>
   
   The following table describes parameters and their settings for applications sourced from AgentKit.
   
   
   |Parameter​ |Description |
   |---|---|
   |Term |Unique application identifier for the MCP application.<br><br><br>* When the application is called by another Claw, this name will be used as the context input for the Client Claw.<br><br>* The name must be 2 to 64 characters long, and the total length after UTF\-8 encoding must not exceed 64 bytes. Chinese characters, English letters, digits, underscores (_), and hyphens (\-) are supported. **You cannot modify the application after you create it.** <br><br>* **Application names must be unique within the ArkClaw Enterprise space. Agent and MCP applications cannot use the same name.**  |
   |Application description |The description of the MCP application.<br><br><br>* This information is used as context input for Claw. The description directly affects the result of application invocation by Claw. The description can be 1 to 4,000 characters in length.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   A model context protocol server that provides web content crawling capabilities. It enables large language models to retrieve and process content from web pages and convert HTML into Markdown for easier utilization. |
   |Source |Select the application source. For this example, select **AgentKit** to indicate that the application is sourced from the MCP service in AgentKit. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible and available to all users.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible and unavailable to all users. |
   |Access Scope |**This parameter is required only when the access permission is set to "Controlled Access"** . Click "Add" to add departments, user groups, or specified users who can access this MCP application. |
   |Associated project |Select the project to which the application belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/ArkClaw/managing_projects?lang=en). |
   |MCP |Select the MCP service or MCP to register and use. |
   |Application address |The address of the MCP application.<br><br><br>* **Address type:** <br><br>   * When the application source is "AgentKit", select the source address of the MCP application from the drop\-down list.<br><br>   * When the application source is "Custom", manually enter the source address of the MCP application.<br><br>* **Network requirements**:<br><br>   * If the accessible address of the application supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw space.<br><br>   * If the accessible address of the application supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw space, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management?TagIDs=2,522,512,502&lang=en#wfChbm5u) in this topic.instructions.instructions.<br><br>   * If the accessible address of the application supports both "Public network" and "Private network" access, configure either public or private network egress as needed to ensure the ArkClaw space can successfully access the address. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="m2PxMSqQP7" title="Custom">
   <TabTitle>Custom</TabTitle>
   
   The following table describes parameters and their settings for applications from a custom source.
   
   
   |Parameter​ |Description |
   |---|---|
   |Term |Unique application identifier for the MCP application.<br><br><br>* When the application is called by another Claw, this name will be used as the context input for the Client Claw.<br><br>* The name must be 2 to 64 characters long, and the total length after UTF\-8 encoding must not exceed 64 bytes. Chinese characters, English letters, digits, underscores (_), and hyphens (\-) are supported. **You cannot modify the application after you create it.** <br><br>* **Application names must be unique within the ArkClaw Enterprise space. Agent and MCP applications cannot use the same name.**  |
   |Application description |The description of the MCP application.<br><br><br>* This information is used as context input for Claw. The description directly affects the result of application invocation by Claw. The description can be 1 to 4,000 characters in length.<br><br>* The description must cover the core capabilities of the application and clarify applicable and inapplicable scenarios. You may also provide typical invocation examples for reference by employees.<br><br>* Description example:<br><br>   A model context protocol server that provides web content crawling capabilities. It enables large language models to retrieve and process content from web pages, and converts HTML into Markdown for easier utilization. |
   |Source |Select the application source. For this example, select **Custom** to indicate that a custom MCP application is used. |
   |Access permission |Set the accessible scope of the application.<br><br><br>* **Allow all**: The application is visible and available to all users.<br><br>* **Controlled access**: This application is available to specified departments, user groups, or users. Only authorized employees can view and use this application.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The application is invisible and unavailable to all users. |
   |Access Scope |**This parameter is required only when the access permission is set to "Controlled Access"** . Click "Add" to add departments, user groups, or specified users who can access this MCP application. |
   |Protocol |Currently, only the **Streamable HTTP** protocol is supported. |
   |Application address |The address of the MCP application.<br><br><br>* **Address type:** <br><br>   * When the application source is "AgentKit", select the source address of the MCP application from the drop\-down list.<br><br>   * When the application source is "Custom", manually enter the source address of the MCP application.<br><br>* **Network requirements**:<br><br>   * If the accessible address of the application supports "Public network" access only, make sure public network egress is enabled in "Network Configuration" of the current ArkClaw space.<br><br>   * If the accessible address of the application supports "Private network" access only, make sure private network egress is enabled in "Network Configuration" of the current ArkClaw space, and configure accessible private network egress information. For specific operations, see [Network configuration description](https://docs.byteplus.com/en/docs/ArkClaw/Application_management?TagIDs=2,522,512,502&lang=en#wfChbm5u) in this topic.instructions.instructions.<br><br>   * If the accessible address of the application supports both "Public network" and "Private network" access, configure either public or private network egress as needed to ensure the ArkClaw space can successfully access the address. |
   |Access authentication |Select the access method for the application.<br><br><br>* **No authentication required**: This is the default method and does not require access authentication.<br><br>* **API Key**: Select the target API key from the drop\-down list.<br><br>* **OAuth JWT**: Select the target credential from the drop\-down list.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click "Add credential" in the drop\-down list to add a new credential. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management">Credential management</a>.</div><br> |
   |Type |This parameter is required only when "Access authentication" is set to **OAuth JWT**.<br><br><br>* **Exclusive credential**: This type of credential is for use by a single account. The credential list below displays only exclusive credentials.<br><br>* **Shared credential**: This type of credential can be shared by multiple accounts. The credential list below displays credentials filtered by the shared account type. When this option is selected, the **JWT Identity Token** option is hidden, and the system will no longer pass the JWT downstream.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Regardless of the credential type selected, a single MCP service can be associated with only one credential.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the "Credential" drop\-down list does not contain the target credential, click "Add credential" in the drop\-down list to add one. For more information, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management">Credential management</a>.</div><br> |
   |JWT identity token |You can configure this parameter only when "Access authentication" is **No authentication required**, **API Key**, or **OAuth JWT**, and the credential type is "Machine\-to\-machine". This parameter specifies whether to include the caller's identity information when requesting the MCP.<br><br><br>* **Disabled** (default): The platform does not issue an additional identity token. This option is suitable for scenarios where the MCP service does not need to identify specific callers.<br><br>* **Enabled**: The platform attaches an identity token to each MCP request via the `x-arkclaw-jwt` header. The MCP service can use this token to identify callers and perform signature verification, confirming that the request source is legitimate and the identity information is trustworthy. This option is suitable for scenarios that require permission control, data isolation, or audit logs by user.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For information about how to obtain and verify the token, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Sample_code_for_obtaining_a_JWT_and_decoding_and_verifying_its_signature">JWT acquisition and sample code for decoding and signature verification</a>.</div><br> |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Click the "Confirm" button to complete the configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After MCP application registration is successful, the system periodically synchronizes the tool list, which you can view on the MCP details page. Automatic tool retrieval is currently not supported for MCP applications sourced from AgentKit or custom\-source MCP applications that use the OAuth JWT user delegation as their authentication method.   </div>
   

<span id="wfChbm5u"></span>
## Network configuration description

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>The Network configuration page varies by interface version. This section only describes the operations in the new interface.</strong> <strong>For details on the configuration information and procedures for the new and legacy versions, see </strong><a href="https://docs.byteplus.com/en/docs/ArkClaw/Public-network-egress?lang=en">Public network egress</a> and <a href="https://docs.byteplus.com/en/docs/ArkClaw/Private-network-egress">Private network egress</a>.</div>


<span id="JeTvn4oj"></span>
### Configure public network egress

When you activate an ArkClaw space, if no CIDR block is specified during network configuration, public network egress is enabled by default after the space is activated. Verify the status again. If public network egress is not enabled, follow the steps below to enable it.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space egress" tab and click the "Public network egress" tab. Click the edit icon next to the configuration information.

4. Enable the public network egress and click "Confirm" to complete the operation.


<span id="1fWhV5XV"></span>
### Configure private network egress

After the private network egress is configured, if you need to modify the VPC or subnet, disable private network egress first and then re\-enable it. When you activate an ArkClaw space with a specific CIDR block, if the VPC of enterprise services is already connected to the ArkClaw VPC via Transit Router (TR) or Cloud Enterprise Network (CEN), enabling private network egress is not supported.

**Step 1: Enable the private network egress**


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space egress" tab, select the "Private network egress" tab, and click "Edit" next to the configuration information.

4. On the private network egress page, configure private network parameters by referring to the table below. This ensures that ArkClaw can access the addresses of registered applications over the private network. Then, click "Confirm" to complete the operation.

   
   |Parameter |Description |
   |---|---|
   |Private network egress switch |Turn on the private network egress switch. After the private network egress is enabled, the ArkClaw space and enterprise applications communicate through the private network. |
   |**Basic information** ||
   |Associated project |The project to which the current space belongs. It cannot be modified. |
   |VPC |Select the VPC where the accessible address of the application is located. |
   |Availability zone and subnet |Select two availability zones and their subnets for the private network egress.<br><br><br>* Subnets are used to assign private IP addresses to the private network egress.<br><br>* The private network egress occupies 6 private IP addresses in each subnet to ensure access performance. |
   |Security group |Select the security group associated with the private network egress. You can configure up to 4 groups simultaneously.<br><br><br>* Only outbound security group rules take effect for the private network egress.<br><br>* When the private network egress is deployed across two separate availability zones, the two zones share the same specified security group configuration. |
   |**Specify access target** ||
   |Specify target CIDR block |Enter the accessible IP address or CIDR block of the application.<br><br><br>* The entered IP addresses or CIDR blocks must not belong to the following ranges: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/0`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, and `169.254.0.0/16`.<br><br>* You can enter up to 50 items at a time. Separate multiple IP addresses or CIDR blocks with commas (,). |
   |**Private network access to applications** ||
   |Private application access switch |Control whether the ArkClaw space can access private addresses of Agent/MCP applications registered in the Application Center, over the private network.<br><br><br>* **Enable**: The ArkClaw space can use the private network to access private addresses (such as private domains or private IP addresses) configured in the Application Center.<br><br>* **Disable**: The ArkClaw space does not use the private network to access the private addresses configured in the Application Center. If you provide only the private address of an application, ArkClaw may fail to access the application.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For spaces created after this feature is released, this switch is immediately available. For spaces created before this feature release, the switch will take effect after a background upgrade. (expected to be completed by the end of July 2026).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Before the upgrade is complete, private addresses of enterprise agents or MCP applications with "Custom" as the source in the Application Center are temporarily inaccessible. Enterprise agents or MCP applications with "AgentKit" or "Shared Claw" as the source are not affected.</div><br> |
   


**Step 2: Configure DNS resolution for the private network egress**


1. In the "Configuration information" section on the "Private network egress" tab, click "Edit" next to "DNS resolution configuration".

2. Configure private network information based on the following table. After completing the configuration, click "Confirm".

   
   |Parameter |Description |
   |---|---|
   |Configure DNS resolution |Whether to enable domain name resolution configuration.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the AgentKit runtime and MCP use private domain names and are deployed in the same region, such as the China (Shanghai) region, as the ArkClaw space, no additional domain name resolution configuration is required. Public DNS servers of BytePlus support resolution by default.</div><br><br><br><br>* **Disable configuration**:<br><br>   * ArkClaw forwards DNS queries within the space to public DNS servers of BytePlus (`100.96.0.2` and `100.96.0.3`) by default.<br><br>   * Applicable scenarios:<br><br>      * No domain name resolution required: The entered application access address is an IP address (such as `http://192.168.1.100`).<br><br>      * Public or standard domain names: Your application uses a standard domain name resolvable over the public network. The default DNS servers of BytePlus can directly resolve it to the corresponding real IP address.<br><br>* **Enable configuration**:<br><br>   * After domain name resolution configuration is enabled, you need to manually specify the IP address of the internal DNS server for resolving private application addresses. ArkClaw will only send DNS queries to the manually specified server.<br><br>   * Applicable scenarios:<br><br>      * Private domain names within the enterprise service VPC: The application uses a private domain name that only takes effect in the current VPC (such as `http://my-agent.internal.local`). The default DNS servers of BytePlus cannot resolve such internal domain names. You need to enable this configuration and enter the IP address of your self\-built internal DNS server within the VPC that can resolve the private domain name. Otherwise, application access will fail. ArkClaw forwards DNS queries within the space to DNS servers of BytePlus (`100.96.0.2` and `100.96.0.3`). |
   |IP address and port of the external DNS system |Specify the IP address and port of the external DNS server.<br><br><br>* Only IPv4 addresses are supported currently. You can configure up to 10 external DNS server addresses.<br><br>* DNS server addresses are not allowed to be system\-reserved addresses `100.96.0.2` and `100.96.0.3`.<br><br>* The port is optional. If left blank, it defaults to port **53**. |
   |Forwarding domain name |After the domain name resolution configuration is enabled, this parameter must be configured. Specify the domain names to be resolved by the external DNS server. Enter the accessible addresses or wildcard domain names that include the accessible addresses, and then press "Enter" to confirm the input.<br><br><br>* Batch pasting of multiple forwarding domain names is supported. Separate domain names with English commas (,).<br><br>* You can add up to 500 forwarding domain names.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If cross\-border acceleration for public network access is enabled, we recommend that you specify forwarding domain names different from the public network acceleration domain names. If a forwarding domain name is the same as a public network acceleration domain name, requests for that domain name will preferentially pass through the public network acceleration channel.</div><br> |
   

&nbsp;
