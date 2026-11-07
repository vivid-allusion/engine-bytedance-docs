---
title: "New feature release notes"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/New_feature_release_notes"
---

This topic describes the feature releases of the AgentKit service. New features will be gradually released across regions. We welcome you to explore them.

## November 3, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Agent Runtime |Added the **execution timeout** configuration capability. It supports setting the maximum execution duration for a single synchronous request. When request execution exceeds the configured duration, the system automatically terminates the request and returns an error. By configuring the execution timeout appropriately, you can achieve a balance between the success rate of long\-running requests and the resource release efficiency for abnormal requests. |* [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>* [Updating execution timeout](https://docs.byteplus.com/en/docs/agentkit/update-execution-timeout) |Asia Pacific (Johor) |

## October 30, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Identity and permissions |A middle\-tier agent can be configured during the creation of an access rule to meet the requirements of multi\-agent chained calls. |[Creating access rules](https://docs.byteplus.com/en/docs/agentkit/creating-access-rules) |Asia Pacific (Johor) |

## October 29, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Gateway \- MCP service |MCP services created using the "Deploy MCP service" method support instance configuration, including the minimum number of resident instances and the maximum number of instances after scaling. |[Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services?lang=en) |Asia Pacific (Johor) |
|Sandbox templates |Sandbox templates now support instance capacity management.<br><br><br>* Supports viewing instance statistics for a template, including the total number of instances, running instances, created instances, and the maximum number of instances.<br><br>* Supports setting the maximum number of instances allowed for a template as needed. |[Viewing and setting instance capacity](https://docs.byteplus.com/en/docs/agentkit/view-and-set-instance-capacity) ||

## October 27, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Sandbox templates |When manually creating  sandbox instances based on a sandbox template configured with private access, you can configure EFS mount points. |* [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools?lang=en)<br><br>* [Manually creating sandbox instances](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances?lang=en) |Asia Pacific (Johor) |
|Gateway \- MCP service |For MCP services with the Identity authentication plugin installed, you must configure the relevant Identity authentication token information during debugging. The system verifies the request identity and permission policies based on the specified Identity permission space. Debugging can be initiated only after authentication succeeds. |[Testing MCP services](https://docs.byteplus.com/en/docs/agentkit/Testing_MCP_service) ||
|Gateway \- Model gateway |Added the **model group** capability for the model service. You can combine multiple integrated upstream models into a unified call name. After the application specifies this name in the `model` field of the request, the gateway selects a model in the group based on the configured weights.<br><br><br>* If in\-group retries still fail, the gateway calls the fallback model at most once.<br><br>* Permissions on model groups can be granted to Proxy API Keys separately. Simulated call debugging is provided to verify authorization and routing results. |* [Creating and granting permissions on model groups](https://docs.byteplus.com/en/docs/agentkit/create-and-manage-model-group?lang=en)<br><br>* [Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage?lang=en)<br><br>* [Calling model services](https://docs.byteplus.com/en/docs/agentkit/call-model-service?lang=en) ||

## October 22, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Gateway \- gateway plugin |Dedicated gateways for the agent runtime type now support plugins. The following two plugins are provided.<br><br><br>* **Custom service extension**: Integrates your own services into the request/response processing pipeline. The processing logic is implemented by the user, allowing flexible extension of gateway capabilities.<br><br>* **Identity authentication**: Control access permissions to the agent runtime through the Identity authentication plugin. The plugin extracts the token from the request header and validates the request identity and permission policy in the specified Identity permission space. When authentication fails, the request is rejected. |[Configuring dedicated gateway plugins](https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description) |Asia Pacific (Johor) |

## October 20, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Gateway \- gateway plugin |Added support for controlling access permissions for MCP tools through the Identity authentication plugin. The plugin extracts the token from the request header and validates the request identity and permission policy in the specified Identity permission space. When authentication fails, the request is rejected. |[Configuring dedicated gateway plugins](https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description) |Asia Pacific (Johor) |

## October 14, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Identity and permissions |The redesigned identity and permissions module has been launched, providing new identity authentication and resource access control capabilities. |[Identity and permission](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01) |Asia Pacific (Johor) |

## October 10, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Skills |Added the skill workspace. This feature aggregates recently accessed skills and quality, security, and evaluation to\-dos, allowing you to quickly locate skills and handle to\-dos centrally. |[Viewing skill workspace](https://docs.byteplus.com/en/docs/agentkit/Viewing-skill-workspace?lang=en) |Asia Pacific (Johor) |

## October 8, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|AgentKit Studio |* AgentKit Studio  **"Traditional mode"**  now supports the  **"Create from workspace"**  method for creating agents, serving as persistent cloud code projects. Additionally, the workspace provides cloud\-based VS Code, making it convenient to write, debug, and manage project code online.<br><br>* When configuring LLM agents, you can add an ordered list of **fallback** models for each agent. If the primary model is unavailable, the system automatically switches to the next model in order, improving agent availability and stability. |[Building and deploying agents using AgentKit Studio](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio) |Asia Pacific (Johor) |

## September 24, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
| |To improve the user experience, the former "Skill Center" has been renamed "Skill", and the former "Skill space" has been renamed "Skills space". This update changes only the display names. Features and existing resources are not affected. |[Skill overview](https://docs.byteplus.com/en/docs/agentkit/SkillsOverview?lang=en) |Asia Pacific (Johor) |

## September 23, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
| <br><br>Skills |Added the capability to create skills via Vibe. You can describe business requirements in natural language, and enable AI to automatically generate, iterate on, and refine skills through multi\-turn conversations, significantly lowering the skill development threshold. |[Creating skills via Vibe](https://docs.byteplus.com/en/docs/agentkit/EditSkillsFile?lang=en) |Asia Pacific (Johor) |
|Gateway \- Model integration |The model gateway now supports credits\-based usage control. Credits are a unified usage unit for internal enterprise governance, helping administrators manage the call quotas of different models under a unified metric.<br><br>> **tip**<br><br><br>> Credits do not represent account balance, recharge benefits, bill amount, or model price, and are used only for internal enterprise usage governance.<br> |[Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage) |Asia Pacific (Johor) |

## September 21, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Skill Center |Added quality check capabilities to identify issues such as missing structures, configuration errors, and incomplete implementation, improving the delivery quality of skills. |[Viewing and fixing quality check issues](https://docs.byteplus.com/en/docs/AgentKit/Viewqualityinspection?lang=en) |Asia Pacific (Johor) |
||Added security scanning capabilities to identify sensitive information, dangerous operations, and high\-risk dependencies in skills, reducing security risks before publishing. |[Viewing and fixing security scan issues](https://docs.byteplus.com/en/docs/AgentKit/Reviewandfixsecurityscanningissues?lang=en) ||
||Added skill evaluation capabilities. You can use test cases to verify skill performance and help determine whether it meets expectations. |* [Running skill evaluation experiments](https://docs.byteplus.com/en/docs/AgentKit/ManagementSkillsAssessment?lang=en)<br><br>* [Viewing evaluation results and fixing skill issues](https://docs.byteplus.com/en/docs/AgentKit/view-evaluation-progress-and-report?lang=en) |Asia Pacific (Johor) |

## September 17, 2026

|Feature module |Feature description |**Document Link** |Release regions |
|---|---|---|---|
|Knowledge Base |Supports using an API Key for agent authentication and knowledge base access. |* [Accessing Viking knowledge bases by using API Key authentication](https://docs.byteplus.com/en/docs/agentkit/Accessing-Viking-knowledge-bases-by-using-API-Key-authentication)<br><br>* [Integrating knowledge base in agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent) |Asia Pacific (Johor) |
|AgentKit CLI |Supports one\-click browser login to your BytePlus account for CLI authorization, allowing you to call cloud resources without manually configuring an AK/SK. |[Developing and deploying agents with AgentKit CLI](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool) ||
|Sandbox templates |During the creation of a preset sandbox template of the ArkClaw Sandbox, Hermes Sandbox, or Code Sandbox type, a skills space and built\-in skills can now be configured so that sandbox instances automatically have the required skill capabilities upon startup. |[Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) ||
|Gateway \- MCP |MCP services and MCP toolsets are now fully compatible with the MCP 2026\-07\-28 protocol. Supports invoking MCP services and MCP toolsets by using the stateless protocol. Existing invocation methods are unaffected. |[MCP protocol version compatibility](https://docs.byteplus.com/en/docs/agentkit/MCP_protocol_version_compatibility) ||
|Gateway \- gateway plugin |Optimized the gateway plugin features. Supports selecting multiple MCP services as applicable resources when configuring a credential transformation plugin rule. |[Configuring dedicated gateway plugins](https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description) ||

## September 11, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Gateway |The MCP\-type dedicated gateway now supports the following two plugins.<br><br><br>* **Credential transformation**: Transforms authentication credentials in requests according to rules before forwarding them to backend services to meet the authentication requirements of different backend services.<br><br>* **Custom service extension**: Integrates your own services into the request/response processing pipeline. The processing logic is implemented by the user, allowing flexible extension of gateway capabilities. |[Configuring dedicated gateway plugins](https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description) |Asia Pacific (Johor) |

## September 10, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Sandbox instance |After the snapshot feature is enabled for a sandbox template, a snapshot can be manually created for a sandbox instance at any time. |[Using snapshots to back up and restore instances](https://docs.byteplus.com/en/docs/agentkit/Using_snapshots_to_restore_instances) |Asia Pacific (Johor) |
|Gateway \- MCP |In private network scenarios, MCP can be tested using a private domain name. |* [Testing MCP services](https://docs.byteplus.com/en/docs/agentkit/Testing_MCP_service)<br><br>* [Testing MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/Testing_MCP_toolset)<br><br>* [Enabling or disabling public network resolution for private domains](https://docs.byteplus.com/en/docs/agentkit/Enabling_or_disabling_public_network_resolution_for_private_domains) ||
|Gateway \- model service |The model gateway supports token usage control from two dimensions: Proxy API Key and model. |[Managing model gateway usage](https://docs.byteplus.com/en/docs/agentkit/Managing_model_gateway_usage) ||

## September 4, 2026

|Feature module |Feature description |**Document Link** |Release regions |
|---|---|---|---|
|AgentKit Studio |AgentKit Studio now supports **Fast mode**. Agents built in this mode automatically include **CreateAgentToolset** (a dynamic agent delegation toolset), which can dynamically create sub\-agents at runtime based on the task and have them work together. Fast mode also supports autonomous planning, multi\-agent collaboration, traceable task execution, and automatic result aggregation, improving the efficiency of complex task processing. |[Building and deploying agents using AgentKit Studio](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio) |Asia Pacific (Johor) |

## September 3, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Sandbox templates |* Optimized the default startup command and listening port for custom sandbox templates.<br><br>* Optimized the IAM role validation logic for preset sandbox templates. |[Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) |Asia Pacific (Johor) |
|Memory |The memory import list now includes a "Status" column. This allows you to view the current status of each memory to be imported and reduces misunderstandings caused by missing information. |[Importing memories](https://docs.byteplus.com/en/docs/agentkit/Importing_memories) ||
|Skill Center |When creating **skills ** by uploading a compressed package, you can now create multiple skills at a time. |[Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills?lang=en) ||

## September 1, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Agent Runtime |Added support for creating agent runtimes that use a dedicated gateway or the shared mode. A dedicated gateway is suitable for production environments, and the shared mode is suitable for POC and low\-traffic validation. |[Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) |Asia Pacific (Johor) |
|Gateway |You can create dedicated gateway instances of the agent runtime type, which are used to mount agent runtime resources. You can view information such as the shared gateway ID, internal service resources, and billing status. |* [Create a dedicated gateway instance](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en)<br><br>* [Viewing shared gateway information](https://docs.byteplus.com/en/docs/agentkit/Viewing_shared_gateway_information?type=preview) ||
|Sandbox templates |* Sandbox templates now support the **MCP Service** configuration item. When you create a sandbox template and enable this feature, the sandbox exposes its capabilities externally as an MCP service. Third\-party agents can then quickly connect to and call the sandbox via the MCP protocol. This effectively reduces the cost of integrating capabilities across agents.<br><br>* **Inbound identity authentication ** for sandbox templates now supports the ** OAuth JWT ** method. OAuth JWT is used to verify the identity of the caller, making this method suitable for integration scenarios with higher security and compliance requirements. |[Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) ||

## August 31, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Billing |AgentKit gateway model has been fully upgraded. MCP (MCP services and MCP toolsets) and agent runtimes are billed based on the ** actual usage** of each resource and the gateway instance mode each resource uses. |* [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items)<br><br>* [Billing rule](https://docs.byteplus.com/en/docs/agentkit/Billing_method)<br><br>* [Changing dedicated gateway instance specifications](https://docs.byteplus.com/en/docs/agentkit/Changing_dedicated_gateway_instance_specifications) |Asia Pacific (Johor) |

## August 28, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|AgentKit Studio |When AgentKit Studio is deployed on the cloud:<br><br><br>* Logging in with local accounts in a user pool is supported, facilitating feature verification and testing in controlled environments.<br><br>* If permissions required to create cloud resources are missing, you can ignore permission issues and continue to try creating cloud resources. This feature helps verify the deployment workflow and troubleshoot permission issues. |[Building and deploying agents using AgentKit Studio](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio) |Asia Pacific (Johor) |
|Gateway |**Gateway instances**<br><br><br>* Added support for ** monitoring** and ** logging ** capabilities. You can monitor the operational status of a service based on multiple metrics, such as QPS, the number of requests, and total inbound and outbound bandwidth. Access logs are also provided. You can use these access logs to track requests and troubleshoot issues.<br><br>* Gateway instance **specification changes** are supported to accommodate business growth or resource adjustment requirements.<br><br><br>**Model service**<br><br>Added support for ** monitoring** and ** logging** capabilities. You can monitor key business metrics, such as inference token usage, cache efficiency, and inference latency. Access logs are also provided to help troubleshoot issues and optimize the business. |* [Creating gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances)<br><br>* [Changing gateway instance specifications](https://docs.byteplus.com/en/docs/agentkit/Changing_gateway_instance_specifications)<br><br>* [Viewing gateway instance monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_gateway_instance_monitoring_data?lang=en)<br><br>* [Viewing model service monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_model_service_monitoring_data?lang=en)<br><br>* [Enable logs](https://docs.byteplus.com/en/docs/agentkit/Enabling_logs?lang=en) ||

## August 27, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Skills Center |The entry point for updating a skill is optimized, streamlining the workflow and improving the experience of skill\-related operations. |* [Updating skills](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills)<br><br>* Viewing skill change details |Asia Pacific (Johor) |

## August 21, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Agent Runtime |When you create a runtime, the minimum supported instance type is 0.5 vCPU. |[Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) |Asia Pacific (Johor) |
|Gateway |AgentKit has upgraded its gateway architecture, introducing dedicated gateway instances. These instances support the creation and management of model services and can be directly integrated and invoked within agents. |* [Creating gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances)<br><br>* [Managing gateway instances](https://docs.byteplus.com/en/docs/agentkit/Managing_gateway_instances)<br><br>* [Creating model services](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service)<br><br>* [Integrating model information in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_model_information_in_agents) ||
|AgentKit Studio |* Two agent creation methods, **Intelligent mode** and **Migrate from an existing project**, are added. Agents can be created by describing requirements in natural language. Existing agent projects developed with frameworks such as LangChain, LangGraph, and Dify can also be migrated and published to AgentKit.<br><br>* Agent runtime stability and task success rates can be improved via Harness Sidecar without modifying core agent code.<br><br>* You can preinstall CLI tools or use custom Dockerfiles to build agent runtime images. |[Building and deploying agents using AgentKit Studio](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio) ||

## August 14, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Sandbox templates |During the creation of a preset Skill Sandbox template, a Skills space and built\-in skills can now be configured so that sandbox instances automatically have the required skill capabilities upon startup. |[Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) |Asia Pacific (Johor) |

## August 7, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Agent Runtime |* A runtime can now be created using a cross\-account image with public network access enabled.<br><br>* When the runtime network configuration is set to "Private network", the associated VPC and subnet IDs can be viewed on the details page. You can navigate to the subnet details page to obtain information such as the subnet CIDR block (IPv4 CIDR). |* [Creating runtimes (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>* [Viewing runtime network information](https://docs.byteplus.com/en/docs/agentkit/Viewing_runtime_network_information) |Asia Pacific (Johor) |
|Sandbox templates |Preset sandbox templates now include two new types: ArkClaw Sandbox and Hermes Sandbox. For ArkClaw Sandbox, instances support configuring message channels to communicate with the agents associated with the instances in natural language and trigger runtime operations on those instances. |* [Template type](https://docs.byteplus.com/en/docs/agentkit/Tool_type)<br><br>* [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools)<br><br>* [Adding message channels to ArkClaw Sandbox template instances](https://docs.byteplus.com/en/docs/agentkit/Adding_message_channels_to_ArkClaw_Sandbox_tool_instances) ||

## July 31, 2026

|Feature module |Feature description |**Document Link** |Release regions |
|---|---|---|---|
|Gateway |When the network configuration mode of the MCP service or MCP toolset is set to "Private network", you can view the associated VPC ID and subnet ID on the details page and go to the subnet details page to obtain information such as the IPv4 CIDR block of the subnet. |* [Viewing MCP service network information](https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_service_network_information)<br><br>* [Viewing MCP toolset network information](https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_toolset_network_information) |Asia Pacific (Johor) |
|Session resource management |Added support for creating or importing a Serverless PostgreSQL database as a session resource. |* [Sessions overview](https://docs.byteplus.com/en/docs/agentkit/Sessions_overview)<br><br>* [Creating session resources](https://docs.byteplus.com/en/docs/agentkit/Creating_session_resources)<br><br>* [Import session resources](https://docs.byteplus.com/en/docs/agentkit/Importing_session_resources)<br><br>* [Integrating session resources in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_session_resources_in_agents) ||

## July 24, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Sandbox templates |Snapshot configuration is now supported during sandbox template creation. When the snapshot feature is enabled, the platform automatically creates a snapshot before an instance expires, preserving the instance data and environment. Snapshots can be used to restore template instances. |* [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools)<br><br>* [Using snapshots to restore instances](https://docs.byteplus.com/en/docs/agentkit/Using_snapshots_to_restore_instances) |Asia Pacific (Johor) |

## July 17, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Agent Runtime |Added a new AgentKit feature: Webshell, which allows you to open a browser\-based terminal directly from the instance management page to access running instances and run command\-line operations. This feature is suitable for in\-depth testing and troubleshooting scenarios. |[Viewing runtime instances via WebShell](https://docs.byteplus.com/en/docs/agentkit/Viewing_runtime_instances_via_WebShell) |Asia Pacific (Johor) |

## July 10, 2026

|Feature module |Feature description |**Document link** |Release regions |
|---|---|---|---|
|Sandbox templates |Sandbox templates now include a new Code Sandbox type, designed for code development scenarios. It supports code generation, debugging, dependency installation, script execution, and test validation. |[Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) |Asia Pacific (Johor) |

## March 6, 2026

|Feature module |Feature description |**Console interface and document link** |Release regions |
|---|---|---|---|
| | | |Asia Pacific (Johor) |
|Agent Runtime |* The maximum number of agent runtimes per account per region has been increased to 20.<br><br>* The maximum number of instances per agent runtime has been increased to 20.<br><br>* Agents can be registered to A2A spaces. This enables business applications to discover, schedule, and interact with external agents based on A2A agent spaces. |* [Limits](https://docs.byteplus.com/en/docs/agentkit/Limits)<br><br>* [Register to A2A space during creation](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>* [Updating A2A spaces](https://docs.byteplus.com/en/docs/agentkit/Updating_A2A_spaces) ||
|A2A Center |Agent to Agent (A2A) is an open protocol introduced by Google, designed to enable interconnection and collaboration between AI agents from different frameworks and vendors. A2A Center centrally manages the communication of A2A agents inside and outside the platform and provides synchronous and asynchronous communication capabilities compliant with the standard A2A protocol through the underlying gateway. |[A2A Center overview](https://docs.byteplus.com/en/docs/agentkit/A2A_Center_overview) ||
|Observability |Added support for MCP toolset monitoring. You can understand the operational status of the MCP toolset across dimensions such as bandwidth traffic, request invocation, retrieval type, performance latency, and tool index. |[Viewing MCP toolset monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_toolset_monitoring_data) ||
||Added the "Public egress response bandwidth" metric for MCP service monitoring. This metric can be used to monitor the traffic per second that the MCP service responds with to the MCP client (caller). |[Viewing MCP service monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_service_monitoring_data) ||
||* Trace data backflow<br><br>   Exports trace data in batches to the agent platform's evaluation sets and launches evaluation experiments directly with trace samples from the corresponding sets. This implements a closed loop between real\-world production data and evaluation, enhancing the observability platform's diagnostic accuracy and reliability.<br><br>* Added the session dashboard capability for the insight dashboard feature. Analysis dashboards are provided for all sessions in AgentKit to visualize session\-related data and trends. Currently provided:<br><br>   * Active session trend chart<br><br>   * Average session round trend chart<br><br>   * Trend chart of average session token consumption |\-\- ||
|IAM permissions |* Added AgentKitDeveloperAccess (a system preset policy).<br><br>   * Applicable to: IAM users, AgentKit developers and testers.<br><br>   * Permission scope: full access to AgentKit features, excluding administrator\-level permissions such as service activation, authorization management, and role creation. To obtain the above permissions, the root user must complete service activation and authorization.<br><br>* Project\-level configuration is supported. Some interfaces of dependent services (ModelArk, Agent identity and permission management platform, IAM, and Application Performance Management Plus) do not support project\-level authorization. Therefore, you need to grant the corresponding policies to the global scope simultaneously. |* [AgentKitDeveloperAccess](https://docs.byteplus.com/en/docs/agentkit/AgentKit_IAM_policy_types)<br><br>* [Granting AgentKit permissions to IAM users](https://docs.byteplus.com/en/docs/agentkit/Granting_AgentKit_permissions_to_IAM_users) ||

## February 28, 2026

|Feature module |Feature description |**Console interface and document link** |Release regions |
|---|---|---|---|
|Agent Runtime |* The gray release capability is available, supporting custom traffic allocation between the online version and the upcoming grey version. This ensures a stable and controlled release process and mitigates risks associated with updates.<br><br>* Release management and version management capabilities are available. Added support for version rollback enables traceable changes and rapid risk mitigation. This effectively enhances system release stability and O&M efficiency.<br><br>* Session resources can be associated. |* [Full release & Gray release](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6d06288981f2dc98455b71a21fd5976.png)<br><br>* [Release notes](https://docs.byteplus.com/en/docs/agentkit/Viewing_release_history)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6b86dafe790ad40c857a55434bd918b.png)<br><br>* [Rollback](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes#48kTRbF2)<br><br>* [Associate session resources](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61e67182b84e3d40a7982b92b1357620.png) |Asia Pacific (Johor) |
|Tool |* Instance specifications can be configured for tools.<br><br>* The model configuration capability is added to the preset Skill Sandbox tools. Models can be specified for agents within a sandbox to support Skill creation and selection.<br><br>* Sandbox tools and instances support TOS mounting.<br><br>* Webshell connection is supported. |* [Instance specification](https://docs.byteplus.com/en/docs/agentkit/Creating_tools)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec283f18f6e923dfa493547beb66f206.png)<br><br>* [Agent model](https://docs.byteplus.com/en/docs/agentkit/Creating_tools)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c52c67f626043bc3c597d6cc41165e81.png)<br><br>* [Mounting TOS to an instance](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bcde0f48b8d4db08ab3d3137b96082e5.png)<br><br>* [webshell](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3169a75720c446f8f98dc4f5e2697d7.png) ||
|Gateway |The OAuth 2.0 3\-Legged Authorization capability is added to MCP services. When the inbound authentication type of a service is OAuth JWT, outbound credentials of the "OAuth Client (USER_FEDERATION)" type can be configured. |[Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services)![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9db0e1ef7d6a782f4b3e49071eb088a4.png) ||
|Sessions |The sessions (STM) capability is released. Two types of storage resources are supported: **RDS PostgreSQL** and **RDS MySQL**.<br><br>Session resources can be imported and associated in the agent runtime.<br><br>Applicable scenarios:<br><br><br>* RDS PostgreSQL: Suitable for scenarios with high workload and large data volumes.<br><br>* RDS MySQL: Suitable for users who are familiar with MySQL and want to keep their existing workflows. |* [Importing session resources](https://docs.byteplus.com/en/docs/agentkit/Importing_session_resources)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8de2e4dfb78fcb00975ba0705b8174fa.png)<br><br>* [Associate session resources when creating an agent](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1426b3a7593f8eb0f2ff83bbb11b9c5a.png)<br><br>* [Associate session resources for an existing agent](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_configuration)<br><br>   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_62c69c9f81cc0412f9a1a71d7feb9dff.png)<br><br><br> ||

## February 10, 2026

|Feature module |Feature description |Release regions |Stage |
|---|---|---|---|
|AgentKit |AgentKit was released online for the first time. |Asia Pacific (Johor) |Beta |
