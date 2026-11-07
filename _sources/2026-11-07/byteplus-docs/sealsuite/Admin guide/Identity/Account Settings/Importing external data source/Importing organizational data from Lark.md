---
title: "Importing organizational data from Lark"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-import-organizational-data-from-lark"
---

To centralize identity management, you can synchronize your Lark organizational data, including users and departments, into SealSuite. This guide provides step\-by\-step instructions for configuring the integration, covering manual, scheduled, and real\-time synchronization methods to keep your organizational data up\-to\-date.

<span id="d286c5de"></span>
# Uses

SealSuite provides the following three synchronization mechanisms for efficiently importing organizational data changes from Lark:


* **Manual synchronization**: Allows you to trigger the synchronization task manually. It is suitable for the scenario where you want to execute the synchronization task after the configuration has been fully tested.

* **Automatic synchronization**: Synchronizes organizational data automatically at scheduled times. It is suitable for scenarios where maintenance personnel want to synchronize data at a fixed frequency.

* **Real\-time Synchronization (Recommended):**  Incrementally synchronizes data based on real\-time changes in organizations or personnel. This mechanism is recommended for scenarios where frequent and significant changes occur in enterprise organizational data, and immediate synchronization is necessary.


<span id="6b29469d"></span>
# Before you begin

Before configuring, ensure that the following requirements are met:


* You have a developer account on the Lark Open Platform.

* You have established your organization's structure.


<span id="3d825fe4"></span>
# Step 1: Configuring Lark application

First, you need to create a Lark application and get the permission to read your organization's account information.

To create and configure a Lark application:


1. Log in to [Lark Developer Console](https://open.larksuite.com/app?lang=en-US).

2. Click **Custom App** and then **Create Custom App**. Follow the guidelines to create an application.

3. Click the created application to enter the configuration page.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41d0636c9bb647ffbea6978deb9f4b54~tplv-goo7wpa0wc-image.image" width="850px" />   </div>
   

4. In the left navigation bar, click **Permissions & Scope** and configure the permission as follows:

   1. In the **Range of contacts data to access** section, click **Configure** to select the Lark accounts to be synchronized to SealSuite.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ef863d5dc6d4eaa9c93c9209eed9cfd~tplv-goo7wpa0wc-image.image" width="850px" />   </div>
   

   2. In the **Manage Scopes** section, click **Contacts** and select the following permissions:

      * Update Contacts.

      * Read Contacts as an app.

      * Obtain department's basic information

      * Obtain department's organizational structure in contacts.

      * Obtain user groups information.

      * Obtain role information.

      * Obtain user's basic information.

      * Obtain user's organization information.

      * Obtain user's email information.

      * Obtain user's employment information

      * Obtain user ID.

      * Obtain user ID via email or mobile number.

      * Obtain user's mobile number.

      * Search users.

5. In the left navigation bar, click **Security Settings** and **Batch Modify** to enter three redirect URLs as follows:

   ```JSON
   https://SealSuite User Portal:Port/multiple-pages/third-login.html
   https://SealSuite User Portal:Port/api/tpslogin/callback/larksuite
   https://SealSuite User Portal:Port/login
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SealSuite User Portal is the end user portal that is configured through SealSuite <strong>Admin Portal \> System Settings \> Enterprise Setup</strong>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dddf9852032468eb99e637db73cb858~tplv-goo7wpa0wc-image.image) </span>

6. Click **Features** \> **Web app** \> **Web app configurations**.

   * If you need to log in to SealSuite by Lark workbench, enter the portal URL in **Desktop homepage**.

   * If you need to log in to SealSuite mobile client by Lark app, enter the portal URL in Mobile homepage.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29b09aa6360a4c01839b4a1cd6ac466b~tplv-goo7wpa0wc-image.image) </span>

7. In the left navigation bar, click **Version Management & Release** and **Create a version**, and configure data source information as follows:

   * **App version**: Enter an application version.

   * **Update** **Notes**: Enter a description for this version.

   * **Availability**: Click **Edit** and select the departments to be imported to SealSuite.

8. Click **Save** and **Submit for release** to publish the application.

   After the administrator approves the release, the application status will be changed to **Released**.

9. After the application is released, obtain the following information of the application:

   * App ID and Secret: Click **Credentials & Basic** **Info**, and obtain the App ID and Secret in the **Credentials** section.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/731e6956f8dd4dee8bd77091613f780b~tplv-goo7wpa0wc-image.image" width="850px" />      </div>
      

   * Encryption Key and Verification Token: Click **Event Subscription**, and obtain the Encryption Key and Verification Token in the **Event Subscriptions** section.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a12ac5df13a84f2bac6c55b61e0e7812~tplv-goo7wpa0wc-image.image" width="850px" />      </div>
      


<span id="74108844"></span>
# Step 2: Adding Lark as the source data in SealSuite


1. Log in to the SealSuite Admin Console.

2. In the left panel, click **Identity \> Account Setup**.

3. On the **Account Setup** page, click **Directory Sync** and then **Add data source**.

4. In the pop\-up window, click **Lark** and then **Create**, and configure data source information as follows:

   * **App ID**: Enter the ID of the Lark Application created in step 1.

   * **App Secret**: Enter the secret of the Lark Application created in step 1.

   * **Lark Host**: Default is `https://open.larksuite.com` for non\-China Lark tenants.

5. Click **Start detection** to check if the permissions required are enabled.

   If the detection fails, please verify the permissions by going to **Permissions & Scope** in [Lark Developer Console](https://open.larksuite.com/app?lang=en-US) as described in Step 1.

6. Click **Next Step**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6eca8f86f1d4152a6f1294dc9d99508~tplv-goo7wpa0wc-image.image) </span>

7. Select data to import:

   1. Select the departments and users to import.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If no Lark account data is loaded, check the configurations of the Lark Application, including permission and security settings, as described in Step 1.      </div>
      

   2. Click **Edit** to update the user field mapping as needed.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The following fields must be added: <strong>user_id</strong>, <strong>email</strong>, and <strong>mobile</strong>, which are used to identify the user account and \*\*\*\* cannot be deleted.      </div>
      

   3. If you want to add more fields, click **Edit** and **Add Mapping** to add attributes.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa2f35dd167e4c16b122ccb1de306ff3~tplv-goo7wpa0wc-image.image) </span>

   4. Click **Next Step**.

8. Select a data synchronization method and click **Complete configuration** to save your changes.

   * **Manual Import**: Click **Manual Import** to start synchronization.

   * **Automatic Import**: Click **Automatic Import** and enter the synchronization frequency as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8131ef218e754f079904f7041a961ac5~tplv-goo7wpa0wc-image.image) </span>

   * **Real\-time Sync (Recommended)** : Click **Real\-time sync** and enter the enterprise key and verification token.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acae59766b8443dcbdef37920902d0b7~tplv-goo7wpa0wc-image.image) </span>

      For **Real\-time Sync**, you need to complete the following configurations:

      1. Click on the synchronization card and navigate to the Synchronization mechanism.

      2. Copy the **Request address** and paste it into **Lark platform** \> **Event Subscriptions** \> **Request URL configuration**, remembering to change the PortalDomain to the actual SealSuite portal name.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ed09e790490486ab09cbd4a5400fe8e~tplv-goo7wpa0wc-image.image) </span>

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6719d7aef8234376811a9e59052677d3~tplv-goo7wpa0wc-image.image) </span>

      3. In the **Directory Synchronization** tab, find the synchronization task and enable it to start the synchronization.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65cc35474edd49ddbe082cf1a99653b2~tplv-goo7wpa0wc-image.image) </span>

      4. Click the synchronization card and **Synchronize tasks** to view the synchronization progress.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6b7b9df2e3e41ad83aa84e57b33204d~tplv-goo7wpa0wc-image.image) </span>
