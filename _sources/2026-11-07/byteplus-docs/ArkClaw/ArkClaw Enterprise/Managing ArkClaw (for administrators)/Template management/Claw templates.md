---
title: "Claw templates"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_templates"
---

Claw templates are blueprints for creating Claw instances. Enterprise administrators can uniformly create Claw configuration templates for different roles and departments and assign these templates in batches. Employees can rapidly create Claw instances using assigned custom templates. This template\-based workflow enables refined permission control and cost management while enhancing assignment efficiency.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The template feature provides enterprise administrators with ‌advanced fine\-grained management capabilities. Employees with assigned custom templates create Claw instances using the template's settings (such as plugins/skills). Employees without assigned templates inherit ‌the space\-level configuration. For more information about space\-level configuration, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Space_information">Space information</a>.</div>


* <div data-tips="true" data-tips-type="default">If administrators enable the <strong>Employees can only claim Claw via a custom template</strong> option, employees can create Claw instances only by using the assigned custom templates (enterprise templates). Employees without templates assigned to them cannot create Claw instances. For information about how to enable it, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_configuration">Employee\-side console configuration</a>.</div>



<span id="VxSilPv0"></span>
## Claw template types

Claw templates are divided into two types:


* **Public templates**: Preconfigured fundamental Claw templates provided by the platform. These templates are visible to all employees by default and can be used directly without requiring administrators to assign them.

* **Custom templates**: Templates created by enterprise administrators for specific business scenarios. Employees can create Claw instances based on these templates ‌only after administrators explicitly assign them.


<span id="mMtWgQOg"></span>
## Public Claw templates

The ArkClaw Enterprise edition provides basic, general\-purpose public templates. These templates are visible to all users and do not require assignment to employees by administrators.

<span id="J9gQNE31"></span>
### View template details


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Public templates" tab, hover over the target template card and click "View details".

4. In the details window, view the professional soul, platform guidelines, built\-in plugins, and built\-in skills. After you check the desired information, click "Close" to exit the window.


<span id="GwiGfWth"></span>
## Custom Claw templates

If the templates in Template Center fail to meet specific requirements of employees, you can create custom templates with tailored soul settings, built\-in plugin options, and seat edition options.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Custom templates are not automatically available to employees. To make custom templates accessible to employees, administrators need to assign them to the target employees.</div>


<span id="SP7QKhN1"></span>
### Create custom Claw templates


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Custom templates" tab, click "Create template".

4. Refer to the table below. Configure template information.

   
   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |Name |Specify the name of the custom template. |
   |Specifications |Select the seat editions for the custom template. Multiple editions can be selected.<br><br><br>* **Seat quota description**:<br><br>   * After a custom template is assigned to an enterprise employee, the employee can use the seat editions defined in the custom template to create Claw instances. Successfully creating a Claw instance consumes the seat quota in the corresponding seat edition for employees.<br><br>   * If a custom template is configured with multiple seat editions, employees to whom the template is assigned can select a seat edition as needed from the available ones when creating Claw instances.<br><br>   * The seat editions available for selection in a custom template are derived from the seat editions already purchased for the ArkClaw space. [View space configuration information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information).<br><br>* **Seat edition description**:<br><br>   * **Starter**: Designed for ‌trial use and lightweight tasks‌. It supports basic conversations and limited tool invocations.<br><br>   * **Standard**: The edition for daily use in production. It supports medium\-complexity workflows and multi\-turn conversations.<br><br>   * **Premium**: Suitable for complex workloads. It can handle parallel invocations of multiple tools and workflows for medium\-sized projects.<br><br>   * **Ultimate**: Designed for large\-scale projects and high\-load scenarios. It supports end\-to\-end orchestration of complex processes. |
   |**Advanced configurations** ||
   |Image |Select the image for the template. <br><br><br>* **Public image**: Select a public image. Public images are properly licensed, secure, and stable images provided by the BytePlus platform, with various built\-in souls, plugins, and skills. |
   |Soul for role |Configure the soul (SOUL.md) for the role in the current template.<br><br><br>* **Template\-based**: Select a built\-in professional soul from the public image, such as Sales expert, Operations expert, HR expert, or Finance expert.<br><br>* **Custom**: Define a custom soul based on the template purposes to specify a position type, working style, response logic, and more. |
   |Built\-in plugin |Configure the built\-in plugins for the current template.<br><br>Common plugins preconfigured in the public image, including Feishu, DingTalk, WeChat, QQ, and Security Protection, are available by default. If these plugins do not meet your requirements, click "Custom plugins‌" at the bottom of the drop\-down list to add custom plugins.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Custom plugins can be specified using one of the two source types: NPX or a download address.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>NPX</strong>: The NPM package name and plugin name that can be pulled via NPX must be provided.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Download address</strong>: A publicly accessible resource download URL must be provided. TOS and other object storage URLs are supported. The plugin name is also required.</div><br> |
   |Built\-in skills |Configure the built\-in skills for the current template.<br><br>You can add platform\-preset skills and enterprise\-exclusive skills. To use enterprise\-exclusive skills, create a space and upload them to it first. For detailed instructions, see [Managing skills](https://docs.byteplus.com/en/docs/ArkClaw/Managing_skills).<br><br>**Procedure**:<br><br><br>1. In the built\-in skills section, click the icon on the right to expand the skills details page.<br><br>2. Switch to the "Preset skills" or "Enterprise\-exclusive" tab, and enable the required skills. |
   |Platform guidelines |To define the global behavioral guidelines for ArkClaw across the enterprise, set platform guidelines (AGENT.md).<br><br>Click "View and edit" to configure the platform guidelines (AGENT.md) for the current template. |
   |**Startup command** ||
   |Command source |Select the startup command type. Only Linux shell is supported. |
   |Command details |Edit or paste the prepared startup command in the custom command input area. |
   

5. Click "Confirm" to complete template creation.


<span id="eF291lBP"></span>
### Manage custom Claw templates


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Custom templates" tab, manage custom templates.

   * **View template details**

      1. In the custom template list, click the target template card.

      2. View template details.

         * On the "Template information" tab, view template details, such as the applicable edition, image, built\-in plugins, skills, and soul.

         * On the "Assigned personnel" tab, view the enterprise employees and user groups to whom the current template is assigned.

   * **Edit templates**

      1. In the custom template list, click "..." \> "Edit template" in the upper\-right corner of the target template card.

      2. On the "Edit template" page, edit the template settings, such as name, edition, and image.

      3. Click "Confirm" to complete the operation.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Each template edit generates a new version number, which is visible in the upper\-right corner of the template details page.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If a template has multiple edit records, select the desired template version before assigning the template to employees.      </div>
      


<span id="tqOrD4fR"></span>
### Assign or remove custom Claw templates

After a Claw template is assigned to ‌designated organizations, departments, or employees, authorized personnel can create Claw instances based on the template. Before this operation, ensure that you have imported user information. To assign templates by user group, also ensure that user groups have been created. For details, see [Importing users](https://docs.byteplus.com/en/docs/ArkClaw/Importing_user_information-) in batches and [Creating user groups](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information).


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Custom templates" tab, assign custom templates to employees or remove the template assignment.

   
   <Tabs>
   <Tab zoneid="YRHxRui4z0" title="One-by-one assignment/removal">
   <TabTitle>One-by-one assignment/removal</TabTitle>
   
   1. Click "..." \> "Manage assignees" in the upper\-right corner of the target custom template card.
   
   2. Assign templates or remove assignments.
   
      * On the left side of the "Manage assignees" page, select the checkbox in front of the user name to whom the template will be assigned. Click "Confirm" to assign the template to the specified employee.
   
      * On the right side of the "Manage assignees" panel, find the target employee and click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_37051fb63f1293e7b6bc931e1cc8ee66.png) </span> icon and click "Confirm" to remove the employee from the assignee list. After removal, new Claw instances created by this employee will no longer be restricted by the template.
   
   
   </Tab>
   <Tab zoneid="HpYQA1Xbim" title="Batch template assignment">
   <TabTitle>Batch template assignment</TabTitle>
   
   1. Click the "Batch assign template" button.
   
   2. Select the templates to be assigned, check the employees to whom the templates will be assigned, and click the "Confirm" button to complete the assignment.
   
   
   </Tab>
   </Tabs>
