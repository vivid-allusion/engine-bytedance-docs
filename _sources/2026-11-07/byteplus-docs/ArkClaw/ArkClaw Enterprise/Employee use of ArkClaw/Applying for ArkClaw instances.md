---
title: "Applying for ArkClaw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_"
---

This topic describes how enterprise employees apply for ArkClaw.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic only applies to seat management type spaces. You do not need to apply for ArkClaw instances in instance management type spaces. ArkClaw instances are deployed by the administrator. Please contact your administrator to obtain one.</div>


<span id="BEB2QtYF"></span>
## Prerequisites


* **You have been granted permission to use ArkClaw**. If you have no permission to use ArkClaw, contact your administrator to grant permissions.

* **You have obtained the ArkClaw login URL**. If not, contact your administrator to obtain it. For details, see [Viewing space configurations](https://docs.byteplus.com/en/docs/ArkClaw/Space_information#ftsmTKKb).


<span id="s7wRX1YA"></span>
## Apply for ArkClaw

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The login, application, and session pages visible to enterprise employees, as well as optional model sources, models, seat editions, and available capabilities, are all specified by the enterprise administrator. Screenshots in the following steps are for reference only, and the actual pages may vary.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. On the displayed page, click the "Try now" button.

3. On the authorization page, click the "Authorize" button to authorize ArkClaw Enterprise. After successful authorization, you can apply for your own ArkClaw.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ArkClaw supports multiple authorization methods. The enterprise administrator can configure an appropriate method based on the actual situation of the enterprise. The figure below shows the authorization page using Feishu SSO authorization as an example.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If password\-based login is used, when you forget your password, you can verify your identity and reset your password on the login page by receiving an SMS verification code sent to your associated mobile number, without contacting an administrator.   </div>
   

4. Refer to the table below to complete Claw configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Seat permission: The platform displays only the seat editions for which you have permission to apply. The specific number of seats available per edition is set by the administrator.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Two Claw types:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Personal Claw: Suitable for personal daily use. Created and used by an individual, it can be used to handle personal tasks and configure preferred skills and tools for personal use.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Shared Claw: Suitable for team collaboration. Team members can access it based on their permissions to consolidate agent configurations, share knowledge bases, and standardize the runtime environment. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Shared_Claw_overview?lang=en">Learn more</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Two creation methods:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Use a template: You can create using a template from public templates, enterprise templates, or image templates. These templates are ready to use and provide preset souls, skills, and plugins. If a template meets your requirements, we recommend using this method.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">General partner creation: You can create a default ArkClaw. This method supports configuring basic capabilities flexibly, such as soul and skills.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Template usage rules:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the administrator has assigned an enterprise template to you, you can directly use it for quick creation. If no enterprise template is available, you can use a public template.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If neither enterprise templates nor public templates can be used, it means the administrator has enabled the "Only allow creation via enterprise templates (custom templates)" restriction and has not assigned a template to you. Contact your enterprise administrator.   </div>
   

   
   <Tabs>
   <Tab zoneid="cbwj7tUHOo" title="Personal Claw">
   <TabTitle>Personal Claw</TabTitle>
   
   Suitable for personal daily use. Created and used by an individual, it can be used to handle personal tasks and configure preferred skills and tools for personal use.
   
   
   |Parameters |Description |
   |---|---|
   |Select specification |Select the specification of the Claw to be created.<br><br><br>* **Starter**: Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations.<br><br>* **Standard**: The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations.<br><br>* **Premium**: Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects.<br><br>* **Ultimate**: Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   |Select Claw template |Select the creation method as needed.<br><br><br>* **Use a template**: You can quickly create ArkClaw based on a [preset template](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_Agent_Gallery_templates) or [image template](https://docs.byteplus.com/en/docs/ArkClaw/Managing_my_images) (a template with an image identifier) provided by the platform, without configuring from scratch.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the existing images do not meet your requirements, click "Custom" to create an image first, and then create Claw based on this image. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_my_images">Learn more</a>.   </div><br>   <br><br>* **General partner creation**: You can create a default ArkClaw. This method supports configuring basic capabilities flexibly, such as soul and skills. |
   |Recruit agents (optional) |If your business scenario requires flexible switching across different agent identities, you can select the target agent here to add an agent to the current ArkClaw.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also add an agent to ArkClaw after you create ArkClaw. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents?lang=en">Learn more</a>.</div><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="rCkAlcOhR3" title="Shared Claw instance">
   <TabTitle>Shared Claw instance</TabTitle>
   
   Suitable for team collaboration. Team members can access it based on their permissions to consolidate agent configurations, share knowledge bases, and standardize the runtime environment.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">After you create a shared Claw, submit it for approval from the enterprise administrator. After it is approved, you can continue configuring and using this Claw. The review result can be sent to you via platform notification, or you can contact the enterprise administrator to check the review progress.</div>
   
   
   
   |Parameter​ |Description |
   |---|---|
   |Select specification |Select the specification of the Claw to be created.<br><br><br>* **Starter**: Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations.<br><br>* **Standard**: The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations.<br><br>* **Premium**: Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects.<br><br>* **Ultimate**: Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   |Select agent template |Only the **General knowledge Q&A assistant** and **ArkClaw intelligent Q&A assistant** templates are supported.<br><br><br>* General knowledge Q&A assistant: A knowledge Q&A expert suitable for multi\-industry Q&A scenarios, with a unified knowledge source from the OpenViking knowledge base. Users can modify the agent configuration file themselves to maintain knowledge data for specific industries and domains.<br><br>* ArkClaw intelligent Q&A assistant: A Volcanic Engine after\-sales expert. It comes with a pre\-built skill that can call the public VikingDB knowledge base (continuously updated and maintained by the Volcanic Engine technical support team), deeply integrating ArkClaw product expertise to handle customer inquiries during ArkClaw usage. |
   |Visibility scope |After you select the target agent template for the shared Claw, you need to specify which members can view and use this Claw. Set the visibility scope based on your actual collaboration needs to avoid exposing the Claw to unrelated members.<br><br>The following visibility scopes are supported:<br><br><br>* **Not open yet**: Only the administrator can view and use this Claw. Suitable for scenarios where the Claw is not yet ready to be shared.<br><br>* **Visible to all**: All members in the current space can view and use this Claw. Suitable for general\-purpose capability, common workflow, or team\-sharing scenarios.<br><br>* **Partially visible**: Only specified departments, user groups, or users can view and use this Claw. Suitable for scenarios where access needs to be controlled by team, role, or individual.<br><br>   > To create departments, user groups, or users, contact your enterprise administrator.   <br>   <br><br>   When "Partially visible" is selected, specify who can access the Claw by using the following methods:<br><br>   * **Department**: Enter the full department name to search, and then select the target department from the result.<br><br>   * **User group**: Enter the full user group name to search, and then select the target user group from the result.<br><br>   * **User**: Enter the user name to search, and then select the target user from the results.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If a department or user group is selected as the grantee, users subsequently added to this scope automatically inherit the corresponding permissions. When users are removed from the department or user group, the permissions will be automatically revoked. This can effectively reduce the permission maintenance workload caused by personnel changes.   </div><br>    |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. After the configuration is complete, click the "Create now" or "Submit application" button. 

   * If you are creating a personal Claw, the system will start the creation process after you submit the application. ArkClaw creation takes about 1–2 minutes. Once it is created, you can start using it.

   * If you are creating a shared Claw, the application will require approval from the enterprise administrator after submission. You can view the review progress by clicking the "Application records" button in the Claw switcher drop\-down list.

      > If you have not received the review result for your shared Claw application after an extended period, contact your enterprise administrator to check the review status.      
      

&nbsp;

&nbsp;

&nbsp;
