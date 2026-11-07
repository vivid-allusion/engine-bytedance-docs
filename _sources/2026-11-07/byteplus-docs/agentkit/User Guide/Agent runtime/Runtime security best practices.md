---
title: "Runtime security best practices"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Runtime_security_best_practices"
---

This topic describes the security practices recommended when you use the AgentKit agent runtime in production environments. It covers key areas such as session isolation, network, identity, permissions, credentials, observability, guardrails, and command execution. You can use this topic as a pre\-launch checklist to reduce the risks of your agents being called without authorization, sensitive data leakage, tool misuse, and uncontrolled configuration changes.

> The AgentKit agent runtime (Runtime) provides a framework\- and model\-agnostic managed runtime environment for agents. It supports automatic scaling of instances based on business traffic and controls the runtime's access to BytePlus cloud resources through associated IAM roles. Each runtime hosts one agent and serves as the core unit for advancing an agent from development and testing to production.


<span id="4JCG2o6j"></span>
## Session isolation and data protection

> The platform's session persistence capability does not mean that all context should be saved. For one\-time inputs, temporary authorization codes, user privacy, and low\-value content, prioritize not writing them or masking them before writing.


Runtimes host agents through independent managed instances, with isolation boundaries maintained by the platform. Isolation of user identities, session identifiers, short\-term context, and long\-term memory still needs to be implemented by you in the agent code, request headers, and business storage. To maintain session isolation and data protection, refer to the following practices:


* **Maintain user\-to\-session mappings in your client backend**: When you call the runtime, use the user_id request header to identify the user initiating the request, and the session_id request header to identify the current session. We recommend that your backend maintain the association between users and session IDs, their lifecycles, and the maximum number of sessions per user. The default values defaultUser and defaultSession are for testing only and should not be used in production.

* **Extract user identifiers from verified identity sources**: If the runtime uses OAuth JWT inbound identity authentication, the user identifier should be extracted from a JWT Claim that has been validated for issuer, audience, not\-before time, and expiration time, and then mapped to the user_id used internally by the agent. Do not directly trust any user ID, tenant ID, or role field passed by the client in request headers.

* **Isolate data by user, session, and tenant**: Session resources, memory, and knowledge base all support data isolation by dimensions such as app_name, user_id, and session_id. In multi\-tenant scenarios, explicitly bind the tenant identifier to session resources, memory retrieval conditions, knowledge retrieval conditions, tool parameters, and business database query conditions, rather than relying solely on prompts to restrict access by the model.

* **Manage the data lifecycle in tiers**: Session is used to hold the short\-term context of the current session and currently supports RDS PostgreSQL and RDS MySQL as backends. Memory is used to accumulate long\-term information across sessions and currently supports two backends: Viking memory and mem0 memory. Knowledge base is used to hold the results of external knowledge retrieval. Based on the data lifecycle, data value, and compliance requirements, determine which fields can be written to session, which can be written to memory, and which are used only within the current request.

* **Do not write highly sensitive data to long\-term context**: Long\-lived tokens, keys, ID card numbers, bank card numbers, and unmasked business secrets should not be written to session or memory as ordinary context. Memory extraction may be delayed, and the extraction result may be reinjected into the prompt in subsequent conversations.

* **Perform sensitive data detection and masking at both ends of the pipeline**: Before data enters the runtime, perform necessary sensitive data detection and masking on user inputs, file contents, and values returned by external APIs. Avoid writing the full request body, full response body, credentials, user privacy data, and business secrets to logs.


<span id="8pQmSpt2"></span>
## IAM and permission management

<span id="mOWYaHoA"></span>
### IAM and least privilege

> Do not treat "a successful call" as the criterion for completing permission configuration. Production permissions should be able to specify the caller, accessible resources, allowed actions, the auditing method, and the revocation method.


IAM governance in runtime scenarios involves three types of identities: the IAM identity used to manage the runtime, the IAM role assigned to the runtime, and the inbound credentials for calling the runtime. The three types should be designed separately to prevent a single credential from covering all permissions. Apply the principle of least privilege to all IAM policies associated with the runtime:


* **Prioritize using system preset policies and scope them by project**: The following system preset policies are available for AgentKit:

   
   |**Policy** |**Permission scope** |**Recommended audience** |
   |---|---|---|
   |**AgentKitFullAccess** |Full management permissions for AgentKit, including creating, modifying, deleting, and viewing resources. |Platform\-level administrators. When you grant authorization, we recommend further narrowing the scope by project and region. |
   |**AgentKitDeveloperAccess** |Full\-featured development permissions for AgentKit. This policy supports the creation, configuration, updating, testing, and release of resources. It does not include advanced administrator permissions such as service activation, authorization management, and role creation. |Default policy for developers and testers. |
   |**AgentKitReadOnlyAccess** |AgentKit read\-only permission. You can view resources only and it does not permit any management actions. |Auditing, observability, and troubleshooting scenarios. |
   

   We recommend associating AgentKit policies with a specific project and granting access to "All resources" only when necessary. For more information, refer to [AgentKit IAM policy types](https://docs.byteplus.com/en/docs/agentkit/AgentKit_IAM_policy_types) and [Granting AgentKit permissions to IAM users](https://docs.byteplus.com/en/docs/agentkit/Granting_AgentKit_permissions_to_IAM_users).

* **Add permissions for dependent services as needed**: Some AgentKit features depend on other cloud services. Do not add permissions by default if the corresponding capability is not used:

   
   |**Dependent feature** |**Recommended policy** |**Trigger scenarios** |
   |---|---|---|
   |ModelArk |ArkGlobalInitAccess |ModelArk is used. |
   |Agent identity and permission management platform |IDLimitedAccess |Use unified identity, credential hosting, and permission management capability. |
   |Access Control |IAMFullAccess |Need to create/maintain the runtime IAM role. |
   |LLM Application Firewall |LLMShieldFullAccess |The Guardrails service has been enabled. |
   |Application Performance Management Plus |APMPlusServerWithoutProjectAccess |The observability service is enabled. |
   

* **Avoid granting policies dedicated to the platform**: AgentKitTosAccess (the TOS access permissions required for Skills Sandbox tasks to run properly) and AgentKitToolAccess (a platform\-internal policy for AgentKit tools) are policies dedicated to the platform and are not recommended to be granted to IAM users.

* **Review the IAM identity of the release pipeline**: The execution identity of AgentKit CLI and automated pipelines should also follow the principle of least privilege. Avoid exposing access keys (Access Key ID / Secret Access Key) in command history, the shell environment, or CI logs. We recommend using credential hosting or the key injection capability of your CI/CD platform.


<span id="LzsXqqA2"></span>
### IAM role trust relationship and permission escalation prevention

When a runtime accesses BytePlus cloud resources, it relies on the associated IAM role for authentication. Overly permissive trust or permission policies may grant the runtime permissions beyond business requirements and even expose it to cross‑service proxy invocations.

Follow the practices below to restrict trust relationships and permissions:


* **Restrict the trust relationship to the service that the runtime depends on**: Since runtimes run on veFaaS, the trust policy for the IAM role shall permit only this service to assume the role. Example:

   ```JSON
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": ["sts:AssumeRole"],
         "Principal": {
           "Service": ["vefaas"]
         }
       }
     ]
   }
   ```
   

   If the veFaaS service identifier is missing in the trust policy, the runtime may not run properly. If the trust policy is too permissive, the role may be unintentionally assumed by other services or identities.

* **Separate IAM roles by business and environment**: Independent IAM roles should be used in development, test, and production environments, and different business lines should also use independent roles. Avoid sharing a single IAM role among multiple runtimes, which blurs the boundaries of permissions.

* **Grant only the least permissions required for agent operation**: You can reuse existing IAM roles or create new ones as needed. Regardless of the approach, ensure that the role's permissions cover only the resources and actions required for the agent to run. If the role permissions related to veFaaS are missing, the runtime will be unavailable.

* **Prevent permission escalation**: The permissions of the IAM role assumed by the runtime must be equal to or less than those of the principal calling the runtime. Avoid paths where a low\-privilege user gains high\-privilege access to cloud resources by calling the runtime.

* **Include IAM role modifications in the release process**: Adjusting IAM role permissions is a security modification. Risks should be controlled through release records, canary release, rollback capabilities, and complete verification in the test environment.

* **Prioritize full ARNs over wildcards**: When you reference specific resources in a permission policy, use complete resource identifiers whenever possible and avoid broad wildcards.


<span id="uUi8AMey"></span>
## Project isolation and resource\-level access control

AgentKit implements resource grouping and access control through projects and tags. Use these two mechanisms appropriately to establish resource\-level boundaries:


* **Group resources by project and tag**: A resource can belong to only one project. After a project is selected, only users with permissions for that project can access the corresponding runtime. Tags can be used for cost attribution and retrieval aggregation, but they do not constitute a strong authorization boundary and should not be used as the sole means of isolation.

* **Separate runtimes by business and environment**: Independent runtimes should be used in development, test, and production environments. We also recommend separating runtimes by business line, tenant, or data sensitivity level to reduce the risk of cross\-business permission sprawl and data commingling.

* **Determine the project a resource belongs to during creation**: A resource can belong to only one project, and you can change it as needed after creation. Before you open the creation page, if you have already selected a specific project in the top navigation bar, the newly created runtime can be associated only with that project. If you need to associate another project, first switch to the target project or "All resources" in the top navigation bar.

* **Understand the authorization impact of project modification**: Modifying the project of a resource also changes the users who can access the resource. A project switch should be included in audits as an authorization change to avoid unintentionally expanding or narrowing permissions on a production runtime.

* **Maintain consistent project governance for associated components**: Session resources, memory, knowledge base, sandbox tools, and MCP toolset associated with a runtime should reside in the same project and use the same network access method as the runtime; otherwise, association or calling will fail.

* **Use tags to manage cost and searchability**: Tags consist of key\-value pairs (Key\-Value). A single resource can have up to 50 tags associated, and a single operation can be associated with up to 20 tags. Tags are only used for classification, search, and cost attribution and are not recommended as a basis for access control decisions.

* **Plan resource quotas in advance**: Before production launch, confirm the following platform limits to prevent your business scale from reaching these caps:

   
   |**Limit item** |**Upper limit** |**Adjustable on request** |
   |---|---|---|
   |Number of agent runtimes that a single account can create in a single region |20 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
   |Number of instances that a single agent runtime can create |20 |No |
   |Maximum size of an image file that can be imported |10 GB |No |
   |Runtime synchronous request execution timeout |30 min |No |
   |Maximum request load |16 MB |No |
   


<span id="NnCGho4v"></span>
## Use agent gateway as a controlled entry point

Agent gateway (Gateway) is the unified entry point for agents to access external systems and services, responsible for connectivity, routing, and inbound/outbound authentication and call governance. Converting existing REST/OpenAPI services into MCP services through the Gateway, or deploying and importing MCP services through the Gateway, allows you to centrally apply controls outside the agent environment:

> Authentication only indicates that the caller's identity is trusted; it does not mean the caller can perform all business actions. The business side should still perform authorization checks based on the relationships among users, tenants, roles, and resources.



* **Align authentication configurations of the runtime and gateway**: Authentication configurations of the runtime and gateway should be reviewed separately. Protecting only the runtime while ignoring the MCP service entry point exposed by the gateway creates a bypass path.

* **Align network access methods**: When you associate an MCP toolset under the gateway with the runtime, the network access method of the associated components must be consistent with that of the runtime; otherwise, the association or calling cannot be completed.

* **Inbound identity authentication**: MCP services and MCP toolsets under the gateway support two types of inbound identity authentication: API Key and OAuth JWT, which are mutually exclusive. A single MCP service or MCP toolset can be configured with up to 5 API Key inbound identity authentications, and OAuth JWT can be bound to up to 5 clients. For MCP services and MCP toolsets in production environments, enforce inbound authentication to prevent unprotected interfaces from being accessed directly.

* **Centralized hosting of outbound credentials**: Gateway supports managing outbound credentials through the agent identity and permission management platform. When the inbound authentication of the MCP service is of the OAuth JWT type, you can configure user\-delegation (USER_FEDERATION) outbound credentials for the OAuth 2.0 3\-Legged Authorization flow. API Key outbound credentials can also be managed by Identity, with credentials stored in the Key Management Service (KMS) in non\-plaintext form.

* **Select the appropriate backend service type**: the gateway supports VKE, ECS, and other backends as the backend of an MCP service. For an MCP service with private network access enabled, you can select VKE instances and ECS instances within the same VPC to avoid traffic traversing the public internet.

* **Restrict the outbound access surface**: MCP toolsets support switching the calling mode (full return, semantic retrieval, tag\-based retrieval). In production, decide the scope of exposed tools based on the agent's capability needs, and avoid exposing all high\-risk tools by default.

* **Review tool calling parameters**: tool calling parameters should be validated against an allowlist in the agent code to prevent the model from directly concatenating high\-risk commands, SQL, URLs, or file paths.


<span id="tqbY3D0w"></span>
## Identity authentication best practices

Runtime inbound identity authentication supports two methods: API Key and OAuth JWT; only one can be selected. Once selected during runtime creation, it cannot be changed. Therefore, before selecting a solution for the production environment, clearly define the caller, identity source, authorization model, and credential rotation method. Follow these practices:

> Authentication configuration cannot be modified once created. To switch the authentication method, you must recreate the runtime and complete client migration. Conduct a thorough evaluation before production launch.



* **Select authentication method based on calling entity**:

   
   |**Authentication method** |**Applicable scenario** |**Security recommendations** |
   |---|---|---|
   |**API Key** |Service\-to\-service calls, backend system integration, automated tasks, controlled integration\-testing environments. |Store and use them only on the server side; split keys by caller, environment, and purpose; rotate regularly; revoke promptly upon discovering a leak. |
   |**OAuth JWT** |Applications that need to represent end\-user identity, connect to an enterprise identity system, and apply access control by user or role. |Create the user pool and client in advance. Validate the issuer, audience, effective time, and expiration time. Extract the user identity from the verified Claim. Restrict permissions based on scope or role. |
   

* **Fully validate JWT**: When you are using OAuth JWT, validate the discovery address, issuer, audience, allowed clients, allowed scopes, and required custom claims. Do not complete authorization based solely on being able to obtain a token.

* **Do not hardcode tokens in production code**: inject API Key and OAuth credentials through environment variables, the controlled configuration center, or a credential hosting capability. Tokens hardcoded in source code or built images will propagate with the deliverables.

* **Establish rotation and revocation processes for API Key**: When API Key is used in production, do not write the Key into frontend pages, mobile packages, browser scripts, public repositories, prompts, logs, or error information. We recommend injecting credentials into the runtime environment through the secure configuration center or a credential hosting capability and establishing rotation, revocation, and call auditing mechanisms.

* **Confirm consistency of online test paths**: for a runtime created based on OAuth JWT inbound identity authentication, only the M2M type client is supported for online testing. To use the console online test feature for testing, create an M2M\-type client in the user pool to avoid an inconsistent identity model between the testing path and the production path.

* **Prioritize performing online tests only under public network access**: the online test feature is available only when the network access method is set to public network; for a runtime using private network access, you are required to initiate calls manually within a controlled network.

* **Do not directly trust ** **`X-user-id`** ** type request headers**: to represent user identity at the business layer, derive `user_id `from the JWT Claim or the authenticated principal's context, rather than using arbitrary values passed in by the caller.


<span id="QbqrFImq"></span>
## Credential and key management

Common credentials in runtime scenarios include the runtime inbound API Key, OAuth client credentials, access keys (Access Key ID / Secret Access Key), database account passwords, third\-party API Keys, gateway outbound credentials, and credentials required for tool calls. The core goal of credential management is to prevent keys from being scattered across code, prompts, images, logs, command history, and personal terminals:

> If the same key is used simultaneously for local testing, test environments, and production runtime, subsequent auditing, rotation, and leak handling all become more difficult. Production credentials should be created, authorized, and rotated independently.



* **Distinguish inbound credentials from outbound credentials**: The API Key or OAuth JWT used to call the runtime should not be mixed with credentials used by the runtime to access third\-party systems. The two differ in their authorization models, rotation cycles, and visibility scopes and should be managed separately.

* **Use credential hosting capability to manage outbound credentials**: Outbound credentials should be hosted through the credential hosting capability (API Key credentials, OAuth Client credentials) of the agent identity and permission management platform, and provided to the runtime through environment variables or a controlled configuration method. Hosted credentials are stored in KMS in non\-plaintext form.

* **Prioritize hosting gateway outbound credentials:**  the API Key outbound credentials configured through the gateway can optionally be managed by Identity. In production environments, you should preferably manage outbound credentials through a managed approach and avoid storing plaintext keys long\-term in agent code, images, or environment variables.

* **Narrow the visibility scope of managed credentials: ** managed credential resources themselves should also be brought under IAM and project permission governance, and only the people, runtimes, gateways, or tools that need to manage or use the credentials can access the corresponding credentials.

* **Prohibit writing keys in plaintext to prevent propagation along the execution chain:**  do not write keys in plaintext in agent code, prompts, Dockerfile, example requests, WebShell commands, or environment variables; even if credentials are protected by encryption in static storage, once written to logs, traces, or error stacks, they are propagated in plaintext. On the business side, make sure to perform data masking and log content review.

* **Audit environment variables**: Runtime supports configuring environment variables in form or JSON format. For the production runtime, perform a pre\-release review of every environment variable change to confirm whether it contains plaintext keys, temporary testing switches, or expired fields.

* **Split credentials by environment and caller**: Use different credentials for development, test, and production environments; use different credentials for different callers or downstream systems. Do not reuse the same key between local testing, test environments, and production runtime.

* **Establish rotation and revocation processes**: credentials should be rotated or revoked promptly in cases of personnel departure, system decommissioning, caller migration, suspected leakage, or permission reduction. Regularly inventory credentials and remove credentials that have not been used for a long time.

* **Control the visibility range of credentials**: Only personnel, runtime, gateway, or tools that need to manage or use credentials can access the corresponding credentials. The credential hosting resource itself should also be included in IAM and project\-level permission governance.

* **Reduce the credential exposure surface in the deployment chain**: When you deploy runtime with AgentKit CLI and automated pipelines, avoid exposing access keys in command history or logs. We recommend managing credentials through environment variables, the controlled configuration center, or the secret injection capability of the CI/CD platform, and restricting the IAM permissions of the pipeline execution identity to prevent the deployment path from becoming a new secret leak surface.


<span id="3E1wDxNj"></span>
## Network security

Runtime supports two network access methods: **Public network** and **Private network**. Select based on the location of the caller, downstream resource location, and compliance requirements:

> Once the network access method is determined, it affects the range of selectable associated components. Switching the network access method is a high\-risk operation and should be performed only after full regression is completed in a test environment.



|**Network mode** |**Applicable scenario** |**Security recommendations** |
|---|---|---|
|Public network |For public network callers, external SaaS, third\-party callbacks, or cross\-network integration. |Enforce the use of API Key or OAuth JWT. On the business side, add rate limiting, caller validation, and anomaly alerts. Avoid mixing management APIs with business invocation APIs. |
|Private network access |Enterprise internal systems, downstream resources within the VPC, and production agents with low requirements for public\-network exposure. |Create the VPC and subnets in advance. Confirm that the network access method of the associated components matches. Restrict the runtime to access only the services required by your business. |
|Private network access with the shared public network access enabled |The runtime resides in a private network but still needs to access public network resources. |The runtime accesses the internet through the platform\-provided internet egress. Enable this mode only when outbound access is actually required, and evaluate the accessible public domain names, dependency package downloads, third\-party APIs, and audit requirements. |
|Private network access with the shared public network access disabled |The runtime resides in a private network and accesses the internet through a public network egress that you build. |Provide your own available public network egress within the VPC (for example, an EIP or a NAT gateway) and monitor and apply access control to outbound traffic. |


Follow the practices below to reduce the network access surface:


* **Plan the VPC topology in advance**: For scenarios that use private network access, enable VPC in advance and prepare the VPC and subnets in the region where you plan to deploy. Only one subnet can be selected per availability zone. Therefore, we recommend completing network topology planning before going into production and verifying the connectivity among callers, the runtime, session, memory, knowledge, gateway backend services, and other downstream services.

* **Align the network access method of associated components**: When the runtime is associated with session resources, memory, knowledge base, sandbox tool, or MCP toolset, the network access method of the associated components must be consistent with that of the runtime; otherwise, the association or invocation cannot be completed.

* **Clarify the semantics of shared public network access**: Shared public network access only changes the outbound path for Runtime accessing the internet in private network scenarios. It does not equate to relaxing inbound identity authentication. Regardless of whether the shared public network access is enabled, you should continue to use an API Key or OAuth JWT to protect the access entry point.

* **Validate network configuration in a test environment**: For the production environment, we recommend first validating private network connectivity, domain name resolution, outbound access, and the release process in a test environment before migrating to the production runtime.

* **Restrict the sources of calls**: For internet\-facing runtimes, you can combine business\-side caller IP allowlists, source validation, rate limiting, and anomaly alerts to prevent exposed endpoints from being brute\-force scanned or abused.


<span id="GOQFlLOL"></span>
## Auditing and monitoring

When you create an AgentKit resource, the platform enables the observability service by default and simultaneously enables **APMPlus** and **TLS**. APMPlus is responsible for writing logs and provides a unified observability capability across metrics, traces, and logs.

> The goal of observability is not to retain as much data as possible, but to quickly identify the impact scope and remediation path when abnormal calls, unauthorized access, prompt injection attacks, sensitive data leakage, or release failures occur.


Follow the practices below to establish an observability baseline that can be used for auditing and troubleshooting:


* **Basic monitoring**: Used to observe resource changes of runtimes and instances, with a focus on metrics such as number of requests, request distribution, average latency, outbound response bandwidth, CPU usage, memory usage, and instance quantity. The query window ranges from a minimum of 1 hour to a maximum of 15 days; only the most recent 30 days of data are retained, and the collection frequency is 30 seconds.

* **Application observability**: Used to locate issues related to models, runtime, gateway, tools, sessions, or memory, with a focus on whether capabilities such as runtime overview, session analysis, trace analysis, model monitoring, log analysis, tool analysis, insight dashboards, and alert templates form a closed loop.

* **Log governance**: Runtime logs are automatically delivered to the log topic apmplus\-server\-log under the AgentKit dedicated log project apmplus\-server. Logs should record the caller, time, target runtime, request ID, error code, and trace identifier; Avoid logging plaintext credentials, full tokens, user privacy, and business secrets.

* **Trace**: With trace data, you can correlate a single business request across the runtime, tool calls, session, memory, knowledge, and external system calls for issue location and impact analysis. For the production environment, we recommend integrating trace data into the evaluation set to form a closed loop of "real production data → evaluation validation".

* **Guardrails observability**: The security overview is used to observe the number of requests, number of protections, execution action distribution, and overall attack distribution; the attack logs are used to trace back the inspection type, matched rules, detection category, action taken, and time. Routine O&M should include the security overview and attack logs in inspections, focusing on phenomena such as surges in prompt injection attacks, surges in sensitive\-data hits, abnormal block ratios, and the same caller repeatedly triggering attack rules.

* **Release records and canary release**: Runtimes support full release and canary release, and the traffic percentage of the new version can be adjusted between 10% and 100%. For each change, define observation metrics, anomaly thresholds, and rollback conditions in advance, and keep traceable version records. During the canary release, continuously monitor metrics such as error rate, latency, authentication failures, and security blocks, and promptly stop the traffic ramp\-up and roll back if anomalies occur.

* **Set up anomaly alerts**: We recommend setting alert thresholds for the following metrics: request count, average latency, error rate, instance count, CPU and memory usage, the number of API Key or OAuth JWT authentication failures, the number of security guardrail hits, the error rate of session/memory/knowledge base calls, and WebShell and high\-risk change events.

* **Permission governance**: Log download and log query permissions, Trace query permissions, and observability dashboard permissions should be incorporated into IAM and project permission governance to prevent observability data from being accessed without authorization.


<span id="zOU1g5aC"></span>
## Command execution security

Runtime supports running command\-line operations directly in the instance through ** WebShell**, which is suitable for file viewing, task creation, and in\-depth troubleshooting. The command execution capability is essentially a high\-risk operations entry point. Grant it only to trusted O&M or R&D personnel, and bring it under auditing, approval, and least\-privilege control.

> Commands executed in WebShell directly affect the online instance status. Treat WebShell as an exceptional troubleshooting measure, not a routine change entry point.


Follow the practices below to restrict WebShell usage:


* **Restrict the IAM identities that can access WebShell**: Grant only personnel with troubleshooting responsibilities permission to enter runtime instances and execute commands. The API for querying the WebShell connection endpoint of a runtime instance (GetRuntimeWebshellEndpoint) should be explicitly restricted through IAM policies.

* **Audit command execution**: For each command execution, log the caller, timestamp, target runtime, target instance, command content, execution result, and the failure reason. Correlate audit logs with the corresponding business logs.

* **Do not read/write sensitive credentials in WebShell**: Do not output, copy, or save API Key, OAuth credentials, access keys, database passwords, or user privacy in WebShell. Avoid using commands such as env and cat to export environment variables in bulk.

* **Do not use WebShell to bypass the release process**: Changes to images, environment variables, model configurations, IAM role permissions, associated components, and the observability service should be made through the runtime configuration and release process, and version records should be retained.

* **Control long\-running tasks**: Long\-running tasks should not rely on the synchronous request path and should be split or redesigned to run asynchronously based on the runtime synchronous request execution timeout limit of 30 minutes.

* **Verify in a test environment before execution**: Before operations such as deleting files, modifying configuration, installing dependencies, initiating external requests, or accessing sensitive directories, confirm the scope of impact and prioritize verification in the test environment.

* **Clean up temporary assets after troubleshooting**: After troubleshooting is completed, clean up temporary files, temporary credentials, and temporary testing scripts to avoid leaving them in the instance over the long term.


<span id="GeKiu0VC"></span>
## Shared responsibility model

The platform is responsible for providing security capabilities and the runtime foundation, and you are responsible for correctly configuring, integrating, and validating these capabilities within your business context.

AgentKit provides platform capabilities such as runtime management and operations, basic isolation, auto\-scaling, IAM role integration, agent gateway, session management, memory, knowledge base, the Agent identity and permission management platform, observability, evaluation, guardrails, and logging and release management. Platform capabilities provide a security foundation for production operations, but they do not automatically replace your business security responsibilities.


|**Responsible party** |**Primary responsibilities** |
|---|---|
|**Platform** |Provides the capabilities of a managed runtime environment, resource isolation, elastic scaling, inbound authentication, IAM role integration, observability and logging, security guardrail integration, agent gateway, and associated components; performs security maintenance and vulnerability remediation for the platform service itself. |
| ** **  |Design business identity and authorization model; protect API Keys, OAuth credentials, and access keys; write secure agent code; validate user input and tool parameters; govern data in session, memory, and knowledge; manage images, dependencies, releases, auditing, and incident response processes. |


Before production launch, we recommend completing at least the following checks:


* Appropriate inbound authentication (API Key or OAuth JWT) is enabled at the calling entry point.

* Runtime management permissions follow the principle of least privilege, and the trust relationship and permission scope of the IAM role have been narrowed.

* The public or private network access method meets business needs, and the network access method of associated components is consistent.

* If the guardrails service is enabled, it has been integrated into the agent code and the runtime has been redeployed.

* Logs, monitoring, trace, and attack logs are available for troubleshooting.

* Restricted WebShell permissions have been granted to trusted personnel.

* Credentials are not scattered in plaintext in code, logs, images, or command history.

* For the first release, a canary strategy, observation metrics, and rollback conditions have been defined.
