---
title: "Managing software licenses"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-software-licenses"
---

The software license function is used to manage commercial software purchased by your enterprise. With this function, you can effectively manage the usage of your software licenses by configuring the usage scope of licenses, utilizing the alert notification and software usage prohibition capabilities. When SealSuite detects unauthorized use of enterprise software on a particular device or by a specific user, it will send an alert to a designated administrator, who can choose to distribute required licenses or restrict the use of the specific software for the particular device or user.

<span id="5cfa9932"></span>
# Function introduction

When purchasing genuine software, it is necessary to plan procurement requirements based on the current business situation and distribute software licenses for users who initiate license acquisition requests. The licensing and authentication methods for different software are different. For example, a user can sign in to Office on multiple devices at the same time, with multiple devices consuming a single software license. However, the same user can only sign in to Alfed Powerpack on one device, with a device consuming a software license.

SealSuite's software license feature provides you with a comprehensive enterprise\-licensed software management solution.


* **A software management capability with comprehensive software statistics**: The software management module provides you with the capability to centrally manage enterprise software and view software statistics in the Admin Console, such as the installed software on user devices, the number of devices with a specific software installed, and more. The comprehensive software information provided by SealSuite can be used for later analysis when your enterprise makes procurement plans for commercial software.

* **Unified management of legitimate software, flexible configuration of software authorization**: The usage scope of software licenses can be centrally configured by a specific administrator based on the dimensions of users or devices.

* **Risk warning and alarm notification**: SealSuite automatically detects the unauthorized use of enterprise software on a particular device or by a specific user and displays risk alerts accordingly. SealSuite also offers an alert notification capability. When the number of devices or users experiencing license overages matches a specific limit, SealSuite can be configured to send an alert to a designated administrator through the third\-party IM or emails.

* **The software usage prohibition capability**: When SealSuite detects unauthorized uses of genuine software on a device or by a user, you can choose to prohibit the use of the software for the particular device or user. After the prohibition, the authorized users of the same software will not be affected, and the security risk associated with license overages can be prevented.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The software license function currently supports Windows and Mac.</div>


<span id="408fc8d6"></span>
# Adding genuine software

SealSuite includes over 100 built\-in applications. When employees install these applications, they automatically appear in the software license management list. You can filter and search for specific software, then click **Enable License** in the **Action** column to configure management settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22f14e16c1924841ad9b8b63cea9d4ad~tplv-goo7wpa0wc-image.image) </span>

If the built\-in library does not meet your needs, click **Add Software License** on the right side of the **License** page to manually add custom software. This section explains how to add custom software licenses.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86375453f28541259c2c3e893751efe2~tplv-goo7wpa0wc-image.image) </span>


1. Log in to the Admin Console.

2. In the left navigation bar, go to **Endpoint** \> **Software** ＞ **License**.

3. Click **Add Software License** on the right side of the page.

4. In the **Add Software License** interface, select an application or software group, then click **Add to License List** in the **Action** column. Alternatively, select multiple items and click **Add to License Management List** at the bottom left.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30c048eaaa0744dc8a07279dfb2eeb5d~tplv-goo7wpa0wc-image.image) </span>

   The list displays applications installed on employee devices and any software groups you have created.

5. On the **Enable Software License** page, configure authorization by device or user.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6e40b6cb695451eadb2088b2e87a535~tplv-goo7wpa0wc-image.image) </span>

   
   |**Authorization Mode** |**Description** |
   |---|---|
   |**Authorized by device** |Set the maximum number of devices allowed to use the software. This mode is ideal when each device consumes one license. The default limit is 100 devices and can be adjusted manually.<br><br>Select specific devices for authorization. You can select multiple devices or search by the owner's name, device name, or device ID. |
   |**Authorized by user** |Specify the users, departments, or roles authorized to use the software. This mode is ideal when each user consumes one license.<br><br>Select specific users, departments, or roles. You can select multiple items or use the search bar to find specific users, departments, or roles. |
   


<span id="aa229751"></span>
# Enabling the license management capability

By default, the license management capability for newly added software is disabled. After adding genuine software to the software license list, you can enable the capability for your target software and distribute licenses by devices or users.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. In the software license list, locate your target software and click **Enable license** in the **Action** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a5b12d6bd07401ea7c316979ebb77ac~tplv-goo7wpa0wc-image.image) </span>

4. In the **Enable Software License** dialog box, complete the following configurations and click **OK**.

   You need to choose an authorization mode, which can be either **Authorize by device** or **Authorize by user**. Multiple choices are not supported. The descriptions of configurations for the two authorization modes are shown in the table below.

   
   |**Authorization Mode** |**Description** |
   |---|---|
   |**Authorize by device** |In this mode, you need to specify the device limit for the software licenses of the current software. This option is applicable to the scenarios in which a device consume a license. The device limit is set to 100 devices by default. You can modify the value based on your requirements.<br><br>Specify your target device by selecting one or more devices listed in the **Enable Software License** dialog box. You can also filter your desired device by using the name or ID of the device's owner |
   |**Authorize by user** |In this mode, you need to specify the user, department, or role that you want to assign licenses for. This option is applicable to the scenarios in which a user consumes a license.<br><br>Specify your target user by selecting one or more users listed in the **Enable Software License** dialog box. You can also filter your desired user by using the name, department or role of a specific user. |
   

   After the configuration is completed, you can locate the corresponding software in the software license list. In the **Authorized/devices** column, click the number to view the authorization details of the current software.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d364f00153a431b94020bb85a820890~tplv-goo7wpa0wc-image.image) </span>


<span id="7fd3dda3"></span>
# Viewing software license information

In the software license list, you can view the basic information and license information of each software, which facilitates your unified management and maintenance of genuine software.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. On the **License** page, you can view the license information by using the following actions:

   
   |**Action Name** |**Description** |
   |---|---|
   |Use filter criteria to search for your target software license |At the top of the page, you can set filter conditions to view software license information. You can use the following filter criteria: OS, software name, software source, software license management, authorization type, software status, and software risk. Please pay attention to:<br><br><br>* **Software Name**: Support fuzzy searching, and the query results support multiple selections.<br><br>* **Software Source**:<br><br>   * **All**: All softwares are displayed by default.<br><br>   * **System built\-in:**  The built\-in software of SealSuite.<br><br>   * **Custom:**  The software you added includes applications selected via the user's installed list and applications customized via app detection items. |
   |View the software license list |* Basic information includes **Software Name**, **Publisher/BundleID**, **Software Version**, **OS**, and **Software Source**.<br><br>* Software license information includes **License management**, **Authorization Type**, **Authorized/All**, **Software Risk**, and **Software Status**. The instructions are as follows:<br><br>   * **License management**: Display the status of software license management capability, including two statuses: **Enabled** and **Disabled**.<br><br>   * **Authorization Type**: Display the authorization modes for the current software licenses, including **Authorize by device** or **Authorize by user**.<br><br>   * **Authorized/All**: Display the number of authorized devices or users, and the number of all devices or users within your enterprise. Support clicking on numerical values to jump to the authorization details page for viewing, displaying the authorized or unauthorized status of the device or user on this page. The description of different authorization statuses is as follows:<br><br>      * **Authorized**: By default, the devices or users included in this state are those within the authorized scope specified by you when software license management is enabled. In addition, it also includes devices or users that you add authorization for. Devices or users in this state can use the software.<br><br>      * **Unauthorized:**  When you enable the license management capability for software, if there are devices or users that have installed the software without authorization, SealSuite will collect such data information and automatically display the devices or users in the **Unauthorized** status list. If an unauthorized device or user installs and uses the software, **Risk found** is indicated in the **Software Risk** column field. You can **Disable License**, or **Restrict Software**. For relevant operations, please refer to [Managing software authorization](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565916901fc8d02edb08f20?docLang=en&bv=652fd8f3fb401502ea5effe0#7828aef4) and [Prohibiting software usage](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565916901fc8d02edb08f20?docLang=en&bv=652fd8f3fb401502ea5effe0#5e365f46).<br><br>   * **Software Risk**: This option is divided into two categories: **Risk found** and **No risk**.<br><br>      * **Risk found**: Software for which license management is not enabled, or software for which license management is enabled but runs excessively.<br><br>      * **No risk**: Software for which license management and software disabling is enabled, or software for which license management is enabled but is not overrun.<br><br>   * **Software Status**: This option consists of two statuses, which are **Restricted** and **Available**. |
   


<span id="7828aef4"></span>
# Managing software licenses

After enabling the license management capability for a specific software, you can navigate to the details page of the software by clicking the number under the **Authorized/All** column in the software license list. On the details page, you can view all devices or users associated with the software. You can switch the authorization mode or adjust the authorization scope according to actual needs.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. In the license list, locate the specific software, and in the **Authorized/devices** column, click the value to enter the details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d364f00153a431b94020bb85a820890~tplv-goo7wpa0wc-image.image) </span>

4. On the details page, manage devices or users.

   The relevant instructions are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dd99c75e0044b69b917f7fde7a248cb~tplv-goo7wpa0wc-image.image) </span>

   * In the list, you can view the **Authorization Status**, **Software Status**, and **Risk Status** of the device or user, and you can **Add authorization** or **Cancel authorization**.

      * **Authorization Status**: Divided into **Authorized** and **Unauthorized**.

         * **Authorized**: By default, the devices or users listed under the **Authorized** tab are those within the authorized scope specified by you when enabling the license management capability. In addition, it also includes devices or users that you add authorization to later. The device or user in this state can use the software normally, and you can also choose to **Cancel authorization** of the device or user according to actual needs.

         * **Unauthorized**: When you enable license management capabilities for software, if there are devices or users who have installed the software without authorization, SealSuite will collect such data information and automatically place the devices or users in the **Unauthorized** tab. If unauthorized devices or users are using the software, there will be a **Risk found** prompt in the **Risk Status** column field. You can choose to add authorization for the device or user, or disable the software. For relevant operations, please refer to [Restricting software](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565916901fc8d02edb08f20?docLang=en&bv=652fd8f3fb401502ea5effe0#5e365f46).

      * **Software Status**: Includes both **Installed** and **Uninstalled** states.

      * **Risk Status**: Includes two states: **Risk found** and **No risk**. If software disabling is not enabled and the software status is installed, it will be marked as risk found. It is recommended to enable software disabling.

      * **Action**: You can **Add authorization** or **Cancel authorization.** 

         You can also add authorization to the device or user via **Add Authorization** in the upper right corner of the list.


<span id="bff59d74"></span>
# Configuring alert notifications for administrators

When configuring alert notifications for administrators, you can set the ratio of unauthorized to authorized devices or users, which is called the excess ratio. When the license usage reaches the excess ratio, an alarm notification will be sent to the designated administrators, allowing them to promptly detect license overages issues.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">SealSuite sends alert notifications to administrators on a daily basis, which means if alert notifications on unauthorized uses of software licenses are generated, SealSuite only sends these notifications to the administrator once a day.</div>



1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. Hover over the **More Actions** button on the right side of the page, select **Admin Notification Configuration**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0371a227488240b4907802df26e0d1d3~tplv-goo7wpa0wc-image.image) </span>

4. On the **Admin Notification Configuration** page, complete the following configurations and click **Ok**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08b7068638014996b293206f732e0941~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Function Switch |On the right side of the **Admin Notification Configuration**, ensure the **Admin Notification Configuration** toggle switch is turned on. |
   |Excess ratio |Set the ratio of the number of unauthorized devices or users to the number of authorized devices or users. For example, if the number of authorized devices is 10 devices, and the excess ratio is set to 20%, then an alert notification will be sent to the administrator on the condition that the number of unauthorized devices exceeds 2 devices. |
   |Approval Notification |You can choose either **IM notification** or **Email Notification**. The description of the options is as follows:<br><br><br>* **IM notification**<br><br>   * **Select Third\-Party IM**: Operation instructions for adding robots, please refer to [Manage third-party IM](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#7e2d6168).<br><br>   * **Scope**: Set the recipient of the notification, generally selecting enterprise administrator.<br><br>* **Email Notification**<br><br>   * **Mailbox gateway configuration**: Configure a dedicated gateway for mailbox. For more information, please refer to [Manage Email configuration](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#598a8170).<br><br>   * **Recipient's email**: Enter one or more email addresses in this option. |
   


<span id="fb81248f"></span>
# Configuring alert notifications for users

When the software is disabled, devices or users in an **unauthorized** state cannot use the software. If you turn on user notifications, when an **unauthorized** device or user cannot open the software, the system will pop up a user notification stating that the software has been disabled.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you modify the enabled or disabled status of the user notification feature, the feature will take effect in 10 minutes.</div>



1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. Hover over the **More Actions** button on the right side of the page, select **User Notification Configuration**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e3df0560fea466da63d7271e16c821a~tplv-goo7wpa0wc-image.image) </span>

4. On the **User Notification Configuration** page, ensure that the feature is turned on.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eeafa46907644f7886f2c542e8e4b148~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Modify English prompt texts.

   SealSuite provides software disable notification content by default, and you can also modify the notification content according to actual needs. When modifying, you need to modify English text to avoid the problem of inconsistent text prompts when the client switches languages.

6. After the configuration is complete, click **Ok** at the bottom of the **User Notification Configuration** page.


<span id="5e365f46"></span>
# Prohibiting software usage

The software usage prohibition function offers promptly control over the unauthorized uses of software. After you prohibit the use of specific software within your enterprise, the **unauthorized** device or user associated with the software can no longer use prohibited software. For example, when you view a software record labeled with **Risk found** in the **Software Risk** column of the software license list, it indicates unauthorized uses of the specific software are detected by SealSuite. You can resolve this issue by prohibiting the use of specific software.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The software usage prohibition feature cannot take effect on previous versions of the SealSuit client, such as v2.1.14 or earlier.</div>


* <div data-tips="true" data-tips-type="warning">When you modify the enabled or disabled status of this function, the function will take effect in 10 minutes.</div>


* <div data-tips="true" data-tips-type="warning">When you disable the software, all macOS devices that do not have full disk access enabled require authorization.</div>


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. In the license list, locate the software that needs to be disabled, and click **More** \> **Restrict** in the **Action** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1900c148bf7f4077ac3882038b8d2b8a~tplv-goo7wpa0wc-image.image) </span>

4. In the **Confirm disabling software** dialog box, click **Confirm disable**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After disabling the software, you can choose to remove the disabled status for software by using the <strong>Cancel disabled</strong> button in the <strong>Action</strong> column.   </div>
   

<span id="a37e5dbf"></span>
# **Modifying the** usage scope of the license management capability

The software license activation scope is enabled for all administrators by default. If you need to conduct a gray test, you can modify the license activation scope to enable license statistics, authorization, and disablement within the specific range.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **License**.

3. Hover over the **More Actions** button on the right side of the page, select **Software** **Disablement Scope**.

4. Modify by selecting one of the following options:

   * **All Employees**: Applicable to most scenarios. In this mode, the software's license statistics, authorization, and disabling will be enabled across the board.

   * **Selected Employees**: This mode applies when grey testing. When turned on, the software's license statistics, authorization, and disabling will be enabled within the scope of your configuration.

      After selecting **Selected Employees**, you need to further configure the enabled **Department** or **Role**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To exclude certain objects, choose <strong>General Settings</strong> \> <strong>Allowlist Settings</strong>.      </div>
      

5. Click **OK** to complete the modifications.
