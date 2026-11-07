---
title: "Managing SSO application"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-application-management_1"
---

In the application list, you can view and manage all Single Sign\-On (SSO) applications that have been integrated with SealSuite. Management tasks include viewing application data, adjusting SSO configurations, and managing user authorizations. This article describes how to manage applications from the application list.

<span id="40f99abe"></span>
# Viewing application list


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, view the application information and perform the associated tasks.

   * At the top of the page, filtering conditions such as **Status**, **Application Scenario**, or **Application group** can be configured to display applications within a specified range. Click on **Custom Filter** to modify the filter conditions that are shown.

   * In the list, you can view the basic information for each application, including its name, address, and function.

   * Click on the app name to access the details page, where you can view or configure detailed app information. For specific operations, please refer to the [Viewing or configuring app details](https://docs.byteplus.com/docs/sealsuite/docs-application-management_1#86ac2721) section.

   * Click on **Address** to quickly access the application.

   * In the **Actions** column, you can choose to **Disable** or **Delete** the app.

      * **Disable**: After disabling, the application will be unavailable. You can re\-enable the application as needed.

      * **Delete:**  After deletion, the application will no longer be available and cannot be recovered. Please proceed with caution.


<span id="86ac2721"></span>
# Viewing or configuring app details

Once you enter the application details page, you can manage various configurations through different tabs.

<span id="data-overview"></span>
## Data Overview

This tab tracks the application's login data, including total users, today's login, total login, today's registration, and the daily percentage change for each data category. At the same time, you can also view the login trend chart for a custom period, by filter, or by login count, or filter by employee count on this tab.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only applications configured with the single sign\-on feature will display the <strong>Overview</strong> tab in the console.</div>


<span id="general"></span>
## General

This tab displays basic information, security setup, and portal quick access configuration for the application.


* **General** area: Displays the application's icon, name, description, group, and access address. You can click **Edit** on the right to adjust the basic information.

* **Security Setup** area: Displays the acknowledgment of user agreement and privacy policy for two\-factor authentication. You can click **Edit** on the right to enable or disable **Two\-factor authentication**. Once enabled, you need to configure **MFA Method** and **MFA Expiration Period**. Subsequently, employees will need to perform two\-factor authentication upon logging into applications based on the configurations.

* **Portal Quick Access** area: Configure the application's display on SealSuite and other third\-party platforms. For specific configuration operations, please refer to [Configuring portal quick access](https://docs.byteplus.com/docs/sealsuite/docs-application-management_1#d2d03e7a).


<span id="single-sign-on"></span>
## Single Sign\-On

This tab shows the general info and mapping relation for the application's single sign\-on.


* **General** area: Displays the SealSuite configurations and application configuration required for single sign\-on. Single sign\-on configurations vary across different applications; please refer to the actual information displayed. For example, within the GitLab application, the single sign\-on details contain SealSuite **Client ID**, **CLIENT SECRET** (both primary and backup), **ACCESS TOKEN** configurations, as well as the application's configurations for the single sign\-on callback address. You can click **Edit** on the right to adjust the related configuration.

* **Mapping Relation** area: View or edit the user attribute mapping relation between the app and SealSuite, used to match employee single sign\-on applications. Different applications have default enabled mapping relations, click **Edit** to add, delete, or modify mappings. Both **Data Field Mapping** and **Expression Mapping** rules are supported. See the [Expression Syntax](https://docs.byteplus.com/docs/sealsuite/configuring-data-source-mappings#4e89f04d) for supported expression syntax.


<span id="aae6ae1b"></span>
## Service Account

In corporate office scenarios, some business systems (such as Jira, O&M platforms, or financial systems) often have situations where multiple people share a common public account or a specific project account. To achieve the security goal of "shared account, unique responsibility," SealSuite provides the service account management feature.

By configuring a service account allocation policy, you can bind the business system's "service identity" with the employee's SealSuite "main account." When logging in via SSO, employees can select the corresponding service identity to enter the system based on their authorization. This not only allows employees to avoid remembering multiple sets of credentials but also ensures that backend audit logs can trace the real natural person behind every operation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This tab is displayed only when the application is integrated using the <strong>SAML</strong> or <strong>OIDC</strong> protocol.</div>


<span id="6d502ac8"></span>
### Add a Service Account


1. In the **Policy List** sub\-tab of the **Service Account** tab, click  **+ Add Account** on the right.

2. In the **Add Service Account** dialog, complete the following configurations and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Service Account Name** |The display name for this service identity. Used in the selection box during employee login. It is recommended to name it after the business identity (e.g., "Jira Administrator," "Finance Reimbursement Account") for intuitive identification. |
   |**Unique Identity ID** |The account identifier for this service identity in the business system. During SSO, SealSuite passes this ID as an identity credential to the downstream application, which then identifies the user and grants corresponding business permissions. |
   |**Account Description** |A supplementary description of the service account's purpose. |
   |**Scope** |Select the range of employees authorized to use this service identity. Only main accounts included in the target scope will see the corresponding service account options when logging in to the application. Supports precise authorization by department, role, or member. |
   |**Custom Attribute Mapping** |Specific attribute values set for this service account. Corresponding mapping items will be displayed here only if extended fields have been pre\-defined in the **Attribute Field** tab. You can enter exclusive attribute values for this specific service identity (e.g., a specific project group code). |
   


<span id="c265a654"></span>
### Define Attribute Fields

If the downstream business system needs to obtain other business attributes (such as project group, confidentiality level, role level, etc.) in addition to the account ID during login, extended fields must be defined here. These fields serve as "attribute placeholders," allowing you to fill in differentiated business information when allocating service accounts to different employees.


1. Switch to the **Attribute Field** sub\-tab on the **Service Account** page and click  **+ Add Field** in the top right.

2. Complete the following configurations on the **Add Custom Attribute** page and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Field Key** |The raw key name for this attribute in protocol transmission. Must strictly match the field name required by the downstream application. For example, if the application requires `project_code`, you cannot enter `project_id`. |
   |**Field Name** |The name of this field displayed in the SealSuite Admin Console, facilitating intuitive identification by administrators. |
   |**Field Type** |The data format for this attribute. Currently supports **String**, **Number**, and **Boolean** types. |
   |**Default Value** |The default value automatically filled by the system when you do not enter a specific attribute value in "Add Service Account". |
   


<span id="f6c23b82"></span>
### Configure Mapping Relationships

Establish the correspondence between SealSuite service account attributes and downstream application attribute fields to ensure that the business information of the service account can be correctly passed to third\-party applications.


1. Switch to the **Mapping Relation** sub\-tab on the **Service Account** page and click  **+ Add Mapping** in the top right.

2. Complete the following configurations in the **Add Mapping** dialog and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Service Account Field** |Select the extended item you defined in "Attribute Field". |
   |**Application Field** |Select the attribute field that the third\-party application requires (such as employee ID, email, etc.). Determine the application\-side target field corresponding to the SealSuite attribute value in the SSO protocol. Supports selecting system preset fields or manually adding extended fields. |
   |**Scope** |Determines when the attribute mapping takes effect during the SSO process. Usually, keeping it at **Default** is sufficient, meaning the system automatically passes this attribute in all stages agreed upon by the protocol standard, providing the strongest compatibility. If the application has special attribute carrying requirements for specific Tokens (such as ID Token), you can select **Custom** and check the corresponding range.<br><br><br>* **ID Token**: The attribute will be included in the identity token of the initial login, suitable for scenarios where the application side needs to obtain information immediately.<br><br>* **User Info**: The attribute is returned only when the application subsequently calls the user information interface, suitable for transmitting sensitive or large volumes of information.<br><br>* **Logout Token**: Passed only when the user logs out, used for status synchronization on the business side. |
   


<span id="13b518cc"></span>
### Endpoint Effect Description

After configuration, the login experience for employees within the service account's scope will change from "single\-step login" to "authentication + selection" mode.


1. **Main Account Authentication**: Employees first verify their real identity through their SealSuite main account.

2. **Select Service Identity**: After authentication passes, the system pops up a list of optional service accounts for the employee based on the policy you configured.

3. **Automatic Identity Switching**: After the employee selects an account, SealSuite automatically logs in to the target application as that service account, without requiring the user to re\-enter the business system password. If an employee is authorized for only one service account and the administrator has enabled automatic login during configuration, the system will skip the selection process and log in to the application directly.


<span id="0710d3ee"></span>
## Application Authorization

In this tab, you can view or edit the application's authorized usage scope.


* **Full**: This application is available for all employees within the company.

* **Restricted**: Authorization of the usage scope is required by dimensions such as **Department**, **Individual**, or **Role**. For example, assigning the **R&D Department** in the **Department Permissions** area restricts application access to only those employees within the **R&D Department**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When configuring <strong>Restricted</strong>, you can choose to <strong>allow employees to apply for application permissions</strong>. After selecting this configuration item, employees with access permission to the application can copy the application link and share it with other employees without permission. After accessing the link, unauthorized employees can apply to use the application.</div>


<span id="7d15260c"></span>
## Provisioning

Applications that support the SCIM (System for Cross\-domain Identity Management) protocol can be configured with the Provisioning feature. When employee accounts are created, updated, or deleted within SealSuite, the data can be synchronized to the application, facilitating unified management of enterprise employee accounts. Furthermore, when an employee leaves, their account in the application can be immediately deleted through this feature, ensuring the security of internal corporate resources.

To use the Provisioning feature, navigate to the **Provisioning** tab, click **Enable Provisioning**, and complete the following configurations.

<span id="1f5f5546"></span>
### General settings

**Provisioning Mode**: \*\*\*\* Choose either **Automatic** or **Manual**.


* **Automatic**: Automatically synchronizes account data from SealSuite to the application. If you select this mode, you must also configure the following:

   * **Auto\-Provision for Initial Setup**:

      * **Yes**: \*\*\*\* After initial setup, users within scope will be immediately provisioned.

      * **No**: \*\*\*\* After initial setup, current users will not be provisioned. Synchronization will only be triggered for subsequent events, such as new account creation, attribute updates, or account deletion upon employee departure.

   * **Trigger Interval**:

      * **Immediate**: On each trigger event, user data will be immediately synchronized downstream.

      * **60 Minutes**: The system will batch all changes that occurred and synchronize the changes every 60 minutes.

* **Manual**: \*\*\*\* Synchronization for this application will not run automatically. After completing the configuration, you can trigger a sync task at any time by clicking the **Manual Sync** button in the upper\-right corner of the **Provisioning** tab.


**Provisioning Action**: \*\*\*\* Select whether to synchronize when accounts are created, updated, or deleted. Multiple selections are supported.

<span id="7892e78e"></span>
### Authentication


* **Base URL**: The application's SCIM URL. It must begin with `http` or `https`.

* **API Key**: \*\*\*\* The API token provided in the user provisioning setup page

* **Connectivity Test**: After configuring the Base URL and API Key, click this button to verify that the credentials are correct.


<span id="4f8d0b0a"></span>
### Mapping Configuration


* **Scope**: Defines the scope of employees to which this provisioning configuration applies. Only employee accounts within this scope will be synchronized to the application.

* **Field Mapping**: View or edit the mapping relationship between SealSuite fields and the application's fields. Both **Data Field Mapping** and **Expression Mapping** rules are supported. See the [Expression Syntax](https://docs.byteplus.com/docs/sealsuite/configuring-data-source-mappings#4e89f04d) for supported expression syntax.


After completing the configuration, click **Confirm** in the lower\-right corner. The system will activate the Provisioning feature based on your settings. You can later view and manage provisioning information on the **Provisioning** tab.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The toggle switch on the right side of the "<strong>Provisioning</strong>" area controls the feature. If you turn it off, subsequent account changes will no longer be synchronized to the application.</div>


* <div data-tips="true" data-tips-type="tip">The <strong>Provisioning Logs</strong> section displays the history of all provisioning tasks, including trigger time, task status, and the number of synced employees.</div>



<span id="ccf48502"></span>
## Authentication Policy

Centrally displays the dynamic security access rules implemented for the application.

This tab is displayed only if a policy with the "Application Access" scenario and an "Application Scope" including the current application has been created in **Identity** \> **Account Setup** \> **Advanced Authentication**. For details, see [Configuring advanced authentication policies](https://docs.byteplus.com/docs/sealsuite/configuring-advanced-authentication-policies).

<span id="d2d03e7a"></span>
# Configuring portal quick access

In the **General** tab on the application details page, you can configure the app to be available for clients or link it to the portal quick access for third\-party IM applications such as Feishu, DingTalk, and WeCom. Employees can access the application seamlessly and securely through the SealSuite client or third\-party IM portal quick access.

Click **Edit** to configure the display settings for the app in the SealSuite client and to manage its visibility in the portal quick access for third\-party IM applications. Specific configuration instructions are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b822a4d44c5f4bb493f59b7dbbb9f75e~tplv-goo7wpa0wc-image.image) </span>


* **SealSuite** section: **Access Points** are by default selected for **Mobile**, **Desktop**, and **Web Portal**. You can adjust the scope according to actual needs.

* **Feishu**, **WeCom**, **DingTalk** section:

   1. Configuring third\-party login authentication source

      If not configured, you need to click on the **third\-party login authentication source configuration** area to **configure**. For the configuration of third\-party login authorization, please refer to:

      * [Importing organizational data from Lark](https://docs.byteplus.com/docs/sealsuite/docs-import-organizational-data-from-lark)

      * [Importing organizational data from WeCom](https://docs.byteplus.com/docs/sealsuite/docs-importing-organizational-data-from-wecom)

   2. Return to the application details page, locate the **Portal Quick Access** area and click **Continue to** **configure**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c83c7e93862b4eb8a664cb579f7734b9~tplv-goo7wpa0wc-image.image) </span>

   3. Follow the information in the configuration flow dialog box to create an app in the corresponding third\-party platform and set the application's homepage address.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afda13e3d41a4aba8839f2ecd17464d2~tplv-goo7wpa0wc-image.image) </span>

      Once the configuration is complete, you can access the application entrance through the portal quick access of third\-party IM applications.
