---
title: "Administrator capability overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Administrator_capability_overview"
---

You can perform centralized management on space rules, capability assets, identity permissions, instance O&M, security governance, and employee access by using the administrator backend. The backend integrates activation, distribution, usage, O&M, and reclaim into a single management system. This improves the overall management efficiency of enterprise\-grade ArkClaw.

<span id="s9NA8nBZ"></span>
## Feature overview


* The administrator management capabilities of ArkClaw Enterprise can be categorized into five types:

   * **Organization and permission management**: including space information, user management, permission management, and seat management.

   * **Instance and resource O&M**: instance management, tag management, cloud disk management, network management, and recycle bin management.

   * **Capability and asset governance**: template management, skill management, knowledge management, and application center.

   * **Security and observability governance**: security management, credential management, and observability data masking.

   * **Employee experience and custom branding**: custom branding, employee\-side console configuration, and employee feedback.

* Typically, administrators first configure space information and authentication methods, then create and distribute custom templates by role, and subsequently complete organization integration by importing user information and organizing user groups or departments.

   After employees start creating and using ArkClaw, administrators perform routine governance by using instance management, tag management, and permission management. In addition, they can use recycle bin management, custom branding, employee\-side console configuration, and employee feedback to complete the closed loops for reclaim, experience, and operations.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The preceding order is recommended. You can adjust the configuration order based on the actual needs of your enterprise.   </div>
   

<span id="NUuX55Ll"></span>
## Administrator capability overview


|Feature module |Feature overview |Applicable scenarios |
|---|---|---|
|**Organization and permission management** |||
|[Space information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information) |Define enterprise\-grade default rules and fallback policies.<br><br>You can manage basic settings in a centralized manner, such as the seat quantity, model scope, terminal login capabilities, SSO information, and cloud disks. |Centralized configuration of basic management rules after a space is enabled. |
|[User management](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information) |Maintain employee accounts, organizational relationships, and login methods.<br><br>You can manage users and user groups, maintain department information, and use common third\-party authentication methods such as Feishu and DingTalk for centralized employee login and account access. |Preparation for employee access, organization governance, and subsequent permission configuration. |
|[Permission management](https://docs.byteplus.com/en/docs/ArkClaw/Permission_overview) |Uses permission rules to manage the accessible scope of enterprise resources such as skill libraries, MCP, and shared agents. You can perform fine\-grained authorization by department, user group, or user. |Fine\-grained authorization and access control of enterprise resources. |
|[Seat management](https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats) |View and manage enterprise seat resources. You can change seats, manage orders, view CodingPlan information, and configure seat quotas and token upper limits by employee or user group. |Resource planning, cost management, and resource prioritization for key roles. |
|**Instance and resource O&M** |||
|[Managing instances](https://docs.byteplus.com/en/docs/ArkClaw/Managing_instances) |Perform full lifecycle management on ArkClaw instances (Claw instances). You can start, stop, restart, repair, adjust seats, reclaim, and delete instances. You can also view monitoring data, sessions, logs, and audits, and use backup and restore capabilities to ensure data security. |Routine O&M, troubleshooting, and instance resource adjustment. |
|[Tag management](https://docs.byteplus.com/en/docs/ArkClaw/Tag_management) |Create unified identifiers for Claw instances. You can add and remove key\-value pairs from one or more instances. You can also filter instances by key\-value pair. |Batch O&M, scenario\-based categorization, and quick instance identification. |
|[Cloud disk management](https://docs.byteplus.com/en/docs/ArkClaw/Cloud_Drive_Management) |Provide unified internal file storage for employees. You can quickly enable employee cloud disks, set capacity upper limits for each user based on the enterprise storage quota, and view usage. |Enterprise file accumulation and cross\-instance data sharing. |
|[Network management](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Network_Configuration_overview) |Configure ArkClaw network channels and access entries.<br><br>You can enable public network egress to enable ArkClaw to access resources over the Internet, enable private network egress to enable ArkClaw to access enterprise internal systems, enable cross\-border acceleration policies to reduce cross\-border access latency, and bind enterprise\-owned domains or custom prefixes to employee login links. |Centralized management of ArkClaw network access capabilities and login entries. |
|[Managing recycle bins](https://docs.byteplus.com/en/docs/ArkClaw/Managing_recycle_bins) |Manage deleted instances in a centralized manner and restore or permanently delete them within the retention period. |Recovery after accidental deletion and resource reclaim management. |
|**Capability and asset governance** |||
|[Managing templates](https://docs.byteplus.com/en/docs/ArkClaw/Managing_templates) |Distributes role\-based configurations in batches to employees or user groups. Employees can use a template to quickly create a Claw instance with standardized role capabilities.<br><br>You can create custom templates, preset professional personas, built\-in plugins, built\-in skills, specifications, and platform guidelines, and distribute a single template or multiple templates in batches as needed. |Role\-based standard configurations, batch activation, and fine\-grained cost control. |
|[Image management](https://docs.byteplus.com/en/docs/ArkClaw/Image_management) |Builds reusable custom images based on the official public images of BytePlus by presetting the professional soul, platform specifications, built‑in plugins, built‑in skills, and initialization startup commands. Enterprise employees can create Claw instances by using custom images to achieve centralized configuration. |Employees from different enterprises need to create Claw instances with a consistent Agent capability foundation. |
|[Managing skills](https://docs.byteplus.com/en/docs/ArkClaw/Managing_skills) |Manages skill resources available to enterprises in a centralized manner.<br><br>In the SkillHub, you can search for skills, set enterprise\-featured skills and employee visibility, upload enterprise\-specific skills, and install individual skills or entire skill libraries into specified Claw instances. |Centralized installation of enterprise skill assets and accumulation of organizational business experience. |
|[Managing knowledge](https://docs.byteplus.com/en/docs/ArkClaw/Managing_knowledge) |Integrates enterprise knowledge with ArkClaw. You can connect a Viking knowledge base by using the Knowledge Center. In this way, employees can perform searches, Q&A, and knowledge retrieval in ArkClaw. |Centralized integration with enterprise knowledge assets to improve knowledge usage efficiency. |
|[Application management](https://docs.byteplus.com/en/docs/ArkClaw/Application_management) |Manages Agent and MCP applications of enterprises in a centralized manner. You can register new applications, modify application information, set employee visibility, and unregister applications when you no longer need them. |Centralized publishing and access control for enterprise AI application assets. |
|**Security and observability governance** |||
|[Security management](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection) |View and configure instance security protection policies and skill security scan results in a centralized manner. This protects employee AI assistants from malicious attacks and data leakage risks. |Protection against high\-risk operations and sensitive data leakage, and security audit governance. |
|[Credential management](https://docs.byteplus.com/en/docs/ArkClaw/Credential_management) |Centrally manages access credentials required to invoke Agent applications and MCP applications. |Centralized management, secure storage, and associated invocation of sensitive access credentials. |
|[Masking observability data](https://docs.byteplus.com/en/docs/ArkClaw/Masking_observability_data) |For data security, such as employee sensitive data protection, observability data does not include Input and Output information by default. If you need to facilitate debugging and troubleshooting, you can configure custom observability data masking policies. |Balance privacy protection and issue investigation. |
|**Employee experience and custom branding** |||
|[Custom branding](https://docs.byteplus.com/en/docs/ArkClaw/Custom_branding) |Configure brand information displayed on the login page, the ArkClaw activation page, and the employee session page. The information includes the brand name, slogan, images, welcome message, and security and privacy information. |Alignment of the employee experience during login, ArkClaw application, and usage with the enterprise brand. |
|[Employee-side console configuration](https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_configuration) |Control which features employees can view and use in ArkClaw in a centralized manner. |Centralized management of employee access paths and feature availability. |
|[Employee feedback](https://docs.byteplus.com/en/docs/ArkClaw/Employee_feedback) |Views and manages employee\-submitted feedback in a centralized manner.<br><br>You can filter feedback records by time range, user, and other conditions, and export feedback data. This helps establish a closed loop for handling employee usage issues. |Collect issues and suggestions while employees use ArkClaw. This is used for troubleshooting, improving experience, and performing operational analysis. |
