---
title: "Creating ArkClaw"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_"
---

You can create a ArkClaw by following the instructions in this topic.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This topic only applies to seat management type spaces. ArkClaw instances cannot be created in instance management type spaces. ArkClaw instances are deployed by the administrator. Please contact your administrator to obtain one.</div>


* <div data-tips="true" data-tips-type="default">The pages actually visible to employees (login/application/session pages) and the available resources (model sources/models/seat specifications) are customized by enterprise administrators. The screenshots in this topic are for reference only. The actual pages shall prevail.</div>


   * <div data-tips="true" data-tips-type="default">Seat permission: The platform displays only the seat editions for which you have permission to apply. The specific number of seats available per edition is set by the administrator.</div>


   * <div data-tips="true" data-tips-type="default">Two Claw types:</div>


      * <div data-tips="true" data-tips-type="default">Personal Claw: Created and used by individuals. Suitable for handling personal tasks. The users may configure preferred skills and tools.</div>


      * <div data-tips="true" data-tips-type="default">Shared Claw: Suitable for team collaboration. Team members can access it based on their permissions to consolidate agent configurations, share knowledge bases, and standardize the runtime environment. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Shared_Claw_overview?lang=en">Learn more</a>.</div>


   * <div data-tips="true" data-tips-type="default">Two creation methods:</div>


      * <div data-tips="true" data-tips-type="default">Template\-based creation: ready to use out of the box. This method allows you to use preset seat editions, souls, and skills. If a template meets your requirements, we recommend using this method.</div>


      * <div data-tips="true" data-tips-type="default">General partner creation: You can create a default ArkClaw, and define soul, install skills, plugins, and other basic capabilities as needed.</div>


   * <div data-tips="true" data-tips-type="default">Template usage rules:</div>


      * <div data-tips="true" data-tips-type="default">If the administrator has assigned an enterprise template to you, you can directly use it for quick creation. If no enterprise template is available, you can use a public template.</div>


      * <div data-tips="true" data-tips-type="default">If neither enterprise templates nor public templates can be used, it means the administrator has enabled the "Only allow creation via enterprise templates (custom templates)" restriction and has not assigned a template to you. Contact your enterprise administrator.</div>



<span id="SdWGV7CH"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. In the ArkClaw switching drop\-down list, click the "Create" button.

3. Complete the creation by referring to the table below.

   
   <Tabs>
   <Tab zoneid="bBLpGmYpHI" title="Personal Claw">
   <TabTitle>Personal Claw</TabTitle>
   
   Suitable for personal daily use. Created and used by an individual, it can be used to handle personal tasks and configure preferred skills and tools for personal use.
   
   
   |Parameter​ |Description |
   |---|---|
   |Select specification |Select the specification of the Claw to be created.<br><br><br>* **Starter**: Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations.<br><br>* **Standard**: The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations.<br><br>* **Premium**: Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects.<br><br>* **Ultimate**: Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   |Select Claw template |Select the creation method as needed.<br><br><br>* **Use a template**: You can quickly create ArkClaw based on a [preset template](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_Agent_Gallery_templates) or [image template](https://docs.byteplus.com/en/docs/ArkClaw/Managing_my_images) (a template with an image identifier) provided by the platform, without configuring from scratch.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the existing images do not meet your requirements, click "Custom" to create an image first, and then create Claw based on this image. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_my_images">Learn more</a>.   </div><br>   <br><br>* **General partner creation**: You can create a default ArkClaw. This method supports configuring basic capabilities flexibly, such as soul and skills. |
   |Recruit agents (optional) |If your business scenario requires flexible switching across different agent identities, you can select the target agent here to add an agent to the current ArkClaw. You can also add an agent to ArkClaw after you create ArkClaw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents?lang=en).<br><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="M8qnzNYdwA" title="Shared Claw instance">
   <TabTitle>Shared Claw instance</TabTitle>
   
   Suitable for team collaboration. Team members can access it based on their permissions to consolidate agent configurations, share knowledge bases, and standardize the runtime environment.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">After you create a shared Claw, submit it for approval from the enterprise administrator. After it is approved, you can continue configuring and using this Claw. The review result can be sent to you via platform notification, or you can contact the enterprise administrator to check the review progress.</div>
   
   
   
   |Parameter​ |Description |
   |---|---|
   |Select specification |Select the specification of the Claw to be created.<br><br><br>* **Starter**: Designed for ‌trials and lightweight tasks‌. It supports basic conversations and limited tool invocations.<br><br>* **Standard**: The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations.<br><br>* **Premium**: Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects.<br><br>* **Ultimate**: Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   |Select agent template |Only the **General knowledge Q&A assistant** and **ArkClaw intelligent Q&A assistant** templates are supported.<br><br><br>* General knowledge Q&A assistant: A knowledge Q&A expert suitable for multi\-industry Q&A scenarios, with a unified knowledge source from the OpenViking knowledge base. Users can modify the agent configuration file themselves to maintain knowledge data for specific industries and domains.<br><br>* ArkClaw Q&A assistant: A Volcanic Engine after\-sales expert. It comes with a pre\-built skill that can call the public VikingDB knowledge base (continuously updated and maintained by the Volcanic Engine technical support team), deeply integrating ArkClaw product expertise to handle customer inquiries during ArkClaw usage. |
   |Visibility scope |After you select the target agent template for the shared Claw, you need to specify which members can view and use this Claw. Set the visibility scope based on your actual collaboration needs to avoid exposing the Claw to unrelated members.<br><br>The following visibility scopes are supported:<br><br><br>* **Not open yet**: Only the administrator can view and use this Claw. Suitable for scenarios where the Claw is not yet ready to be shared.<br><br>* **Visible to all**: All members in the current space can view and use this Claw. Suitable for general\-purpose capability, common workflow, or team\-sharing scenarios.<br><br>* **Partially visible**: Only specified departments, user groups, or users can view and use this Claw. Suitable for scenarios where access needs to be controlled by team, role, or individual.<br><br>   > To create departments, user groups, or users, contact your enterprise administrator.   <br>   <br><br>   When "Partially visible" is selected, specify who can access the Claw by using the following methods:<br><br>   * **Department**: Enter the full department name to search, and then select the target department from the result.<br><br>   * **User group**: Enter the full user group name to search, and then select the target user group from the result.<br><br>   * **User**: Enter the user name to search, and then select the target user from the results.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If a department or user group is selected as the grantee, users subsequently added to this scope automatically inherit the corresponding permissions. When users are removed from the department or user group, the permissions will be automatically revoked. This can effectively reduce the permission maintenance workload caused by personnel changes.   </div><br>    |
   
   
   
   
   
   </Tab>
   </Tabs>
   

4. After the configuration is complete, click the "Create now" or "Submit application" button. 

   * If you are creating a personal Claw, the system will start the creation process after you submit the application. ArkClaw creation takes about 1–2 minutes. Once it is created, you can start using it.

   * If you are creating a shared Claw, the application will require approval from the enterprise administrator after submission. You can view the review progress by clicking the "Application records" button in the Claw switcher drop\-down list.

      > If you have not received the review result for your shared Claw application after an extended period, contact your enterprise administrator to check the review status.      
      

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you receive a prompt similar to the one below when creating ArkClaw, it means you have reached the maximum number of ArkClaw instances allowed per employee as set by your enterprise administrator.   </div>
