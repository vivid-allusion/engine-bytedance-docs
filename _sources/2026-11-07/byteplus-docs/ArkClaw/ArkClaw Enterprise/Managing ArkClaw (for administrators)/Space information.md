---
title: "Space information"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Space_information"
---

After ArkClaw Enterprise is activated, you can view the overall operation status of the space, employee activity, model configuration details, employee workspace configuration, and basic space information. You can also modify the enterprise service agent quota, information about models selectable for different seats, and the login configuration information used for SSO.

## Space description

* ArkClaw Enterprise space\-level settings, such as seat and model settings, provide broad controls and fallback policies for all enterprise employees with ArkClaw access, including the number of ArkClaw instances employees can request for different seat editions and the models they can use.

* ArkClaw Enterprise offers more precise seat quota controls and bulk template assignment capabilities. Seat quotas allow administrators to directly configure the number of ArkClaw seats that employees and user groups can apply for. Templates allow administrators to define seat specifications, selectable models, built\-in skills, built\-in plugins, and other preset configuration options and assign templates in bulk to employees and user groups. For details, see [Seat management](https://docs.byteplus.com/en/docs/ArkClaw/Seat_management).

## Configuration precedence rules

When configurations exist at multiple levels (space, seat quota, and template), the final effective settings for enterprise employees are merged and resolved according to two core principles: "**the strictest first**" and "**template over space**".

* **Available models**: The final available model pool is determined by the **template** configuration. Template\-defined models take precedence over space\-defined models.

* **Available seat quota**: The final effective seat quota is determined by the strictest (minimum) value among the limits at each layer.

* **Default model and specification**: The model in the template takes precedence over the default model in the space configuration.

> **tip**

> Priority examples:

* > **Template first**: If the space configuration permits 5 models, and the template assigned to an employee contains only 2 models, the employee can eventually use only these 2 models.

* > **Minimum value first**: If the seat quota in the space configuration is 10 and the seat quota for an employee is 3, the employee eventually has 3 seats available.

## View space\-level configurations

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Space Overview".

3. On the "Space overview" page, you can view the information about the current space.

4. View space configurations and descriptions.

   |Information name |Description |
   |---|---|
   |**Data overview** ||
   |Seat overview |Displays information about seats and ModelArk Plans purchased in the current space. You can configure the maximum number of ArkClaw instances that employees can apply for under each seat edition, current seat usage, and ModelArk Plans. For more detailed seat information, see [Seat management](https://docs.byteplus.com/en/docs/ArkClaw/Seat_management).<br><br>> **warning**<br><br><br>> If you have enabled the **"Space management type" beta feature** and selected **"Instance Management"** as the space management type when activating the ArkClaw space, this information is not displayed on the interface page.<br> |
   |Enterprise service agent |* Quota settings for enterprise service agents in the current space. You can configure space quota and per\-person agent request limit.<br><br>   * **Enterprise service agent quota**: The maximum number of enterprise service agents that all employees in the current space can request to create. Administrators can adjust this quota at any time, but it cannot exceed the quota value allocated to the space in the quota center. The default value is 20.<br><br>   * **Per\-person application limit**: The maximum number of enterprise service agents that a single employee can request to create. Administrators can adjust this at any time, but it cannot exceed the space quota. The default value is 3. This limit includes the total number of enterprise service agents that employees have successfully created and those that are being reviewed. Applications that are rejected do not count toward this limit.<br><br>   * **Pending review**: The number of enterprise service agents in the current space that employees have requested and are awaiting administrator review. For review details, see [Reviewing enterprise service agents](https://docs.byteplus.com/en/docs/ArkClaw/Managing_applications#MvOQCnCK).<br><br>* If the space quota does not meet your requirements, administrators can increase the quota limit for enterprise service agents. To do so, follow these steps:<br><br>   1. On the enterprise service agent card, click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_451d683a75b02770edd60bdf9c157323.png).<br><br>   2. Click "Quota Center" in the pop\-up dialog box.<br><br>   3. In the BytePlus Quota Center, select "ArkClaw" from the product drop\-down list, search for and check the quota parameter "claw_space/multiplayer_agent", and then select the target region.<br><br>   4. Click "Apply" in the Actions column for the target enterprise service agent quota. Set the target quota and provide your reason.<br><br>   5. Click Submit. After the application is approved, the enterprise service agent quota for the space takes effect. |
   |Trend metrics |Displays key usage data and trends for the current space on the current day.<br><br><br>* **Today's Claw Activity Rate**: Displays the daily activity of Claws in the current space. This is used to determine the actual usage status of Claws.<br><br>* **Today's Employee Activity Rate**: Displays the daily activity of employees in the current space. This is used to determine the overall participation of employees.<br><br>* **Today’s Token Consumption**: Displays the token usage for the current space on the current day. This is used to determine overall model call and resource consumption levels. |
   |**Model Details** ||
   |Model configuration |Configure models for employee Claw instances and enterprise service agents. For details, see [Model Management](https://docs.byteplus.com/en/docs/ArkClaw/Model_management).<br><br><br>* **Employee Claw model**: The models configured for employees' personal Claw instances. This applies to each employee's Claw use cases. The configuration applies to all employee Claw instances of each seat edition.<br><br>* **Enterprise service agent model**: The models configured for enterprise service agents. Enterprise service agents are shared across teams or business scenarios. Their model configurations are managed separately from employee Claw models.<br><br>* **Knowledge Center model**: The models configured for the knowledge center (knowledge base). The model configuration of the knowledge center affects knowledge base retrieval and Q&A across the entire space and is a space\-level infrastructure configuration. |
   |**Space information** ||
   |Basic information |Displays the name, ID, and the project that the ArkClaw space belongs to. The space name can be modified:<br><br><br>1. Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_451d683a75b02770edd60bdf9c157323.png).<br><br>2. Enter the new space name and click "Confirm". |
   |**Employee Workspace** ||
   |Download Desktop Version |Provides the download link for the ArkClaw desktop client. Administrators can download the client installation package for the corresponding version based on the target operating system and distribute the installation package to employees. |
   |Employee login link |The link used for enterprise employees to log in to ArkClaw. Enterprise administrators can click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ae127601f9b9bef04e5f86a61cc93544.png)icon to copy this link and provide it for enterprise employees who need to use ArkClaw. Employees can apply for and use ArkClaw using this link. For related operations, see [Usage instructions for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_usage_overview). |
   |Employee\-side log in configuration |When you create a space, if you use the Feishu, DingTalk, or WeCom authentication method, you can view the enterprise application information used for SSO authorization after the space is created. This topic uses Feishu authentication as an example. This section displays the App ID and App Secret of the Feishu application associated with ArkClaw Enterprise.<br><br>Administrators can perform the following steps to modify the associated application and login method.<br><br><br>1. Click "Configuration" in the upper\-right corner.<br><br>2. Select the protocol authentication method and enter the required information, then click "Save".<br><br>   > **tip**<br>   <br><br>   > Before you change the protocol authentication method, ensure that you have configured the required application permissions and obtained the information required for authentication settings. For detailed steps, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide).<br>    |
   |Employee\-side capability opening |Configure the features available on the employee\-side console. Enterprise administrators can flexibly configure the employee\-side console. For detailed instructions, see [Employee-side console configuration](https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_configuration). |
