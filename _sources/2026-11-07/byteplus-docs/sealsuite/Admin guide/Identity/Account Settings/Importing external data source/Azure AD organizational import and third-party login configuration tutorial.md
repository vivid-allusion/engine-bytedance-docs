---
title: "Azure AD organizational import and third-party login configuration tutorial"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-azure-ad-organizational-import-and-third-party-login-configuration-tutorial"
---

SealSuite allows enterprises to import organizational structure information from third\-party platforms into SealSuite. This article mainly introduces how to import the AzureAD organization structure in the SealSuite Admin Portal and how to configure AzureAD third\-party login to SealSuite.

<span id="fd5299d5"></span>
# Instructions for use


* Import AzureAD organizational structure in the SealSuite Admin Portal. For specific operations, please refer to [Importing Azure AD organizational structure](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/65a4d37754da0d031206ab0f?docLang=en&bv=652fd8f3fb401502ea5effe0#344c22f2).

* Authorize AzureAD third\-party login in the SealSuite Admin Portal. For specific operations, please refer to [Configuring Azure AD third-party login SealSuite](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/65a4d37754da0d031206ab0f?docLang=en&bv=652fd8f3fb401502ea5effe0#75003cb3).


<span id="344c22f2"></span>
# Importing Azure AD organizational structure

<span id="b3e07e3e"></span>
## Step 1: Creating an application in AzureAD

Before importing the organizational structure of AzureAD within SealSuite or authorizing third\-party login to SealSuite, you need to register an application on Microsoft Azure Portal and complete the application configuration. The specific operation instructions are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">AzureAD official help document, please refer to: <a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app">Quickstart: Register an application with the Microsoft identity platform</a>.</div>



1. Create an Azure account on the Microsoft portal.

   When creating a new AzureAD tenant, you will be the first user of that tenant. As the first user, you will be automatically assigned to the global administrator role. You can view user information by navigating to the [user page](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UsersManagementMenuBlade/MsGraphUsers).

   You are also listed as the tenant's technical contact by default. You can change the technical contact information in [Properties](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties). For more information about global administrators and technical contacts, please refer to [Global Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#global-administrator) and [What do these fields mean](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/change-address-contact-and-more?view=o365-worldwide#what-do-these-fields-mean).

   1. Log in to[ Azure Portal](https://portal.azure.com/).

   2. In the **Manage Azure Active Directory** card of the Azure portal menu, click **View**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19c08e69de6e482ba059394f3eb517df~tplv-goo7wpa0wc-image.image) </span>

   3. On the **Azure Active Directory** page, click **Manage tenant**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c8380371bcb4af8a3448c7b27075433~tplv-goo7wpa0wc-image.image) </span>

   4. Click **Create**.

      Set the tenant name, domain name (ensure availability). The tenant type is Azure Active Directory.

      The sample configuration is shown below:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a0f6437e33f45ada640964c76eb2943~tplv-goo7wpa0wc-image.image) </span>

   5. On the **Basics** tab, select the tenant type you want to create, Azure Active Directory or Azure Active Directory (B2C).

   6. Click Next to go to the **Configuration** tab and fill in the following information.

      * Fill in the Contoso organization in the **Organization name**.

      * Fill in Contosoorg in the **Initial domain name**.

      * Select United States in **Country/Region**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16b8735863844133b0d23f997bd0a492~tplv-goo7wpa0wc-image.image) </span>

   7. Click Next to view the filled in configuration information. Complete the creation when there is no problem.

2. Register an application on the Microsoft presentation platform.

   To delegate identity and access management functions to AzureAD, the application must be registered with the AzureAD tenant. When you register an application with AzureAD, an identity configuration is created to allow it to integrate with AzureAD. When registering an application in the Azure portal, you can choose whether it is a single tenant (accessible only within your tenant) or a multi tenant (accessible within other tenants), and you can also choose to set a redirect URI (where the access token is sent).

   After completing application registration, a globally unique application instance (application object) will be obtained, which is located in your main tenant or directory. The application has a globally unique ID (application or client ID), and then adds a secret or certificate in the Azure portal to obtain the application Secret.

   1. Log in to[ Azure Portal](https://portal.azure.com/).

   2. (Optional) In the top menu bar, switch to the tenant who needs to register the application.

      If you have access to multiple tenants, you may need to switch to the target tenant first.

   3. Search and select **Azure Active Directory** management, and select **Add** \> **App registration** on the **App registrations** page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6928da061f84371a188ba54c29555d5~tplv-goo7wpa0wc-image.image) </span>

   4. Enter the name of the application.

      * Users who use the application may see the displayed application name.

      * The application (client) ID automatically generated by the registered application is the unique identification of the application.

   5. Set API access.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The corresponding API permission must be enabled, otherwise when importing AzureAD organizational structure or authorizing third\-party login within SealSuite, it will not be able to connect normally.      </div>
      

      1. Click the application to enter the application details page, and click **API permissions** on the left navigation bar.

      2. Click **Add a permission**, and then click **Microsoft Graph** on the pane that appears.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69362e1a2ca940d1b308038f0ff784c2~tplv-goo7wpa0wc-image.image) </span>

      3. Add delegation related permissions to **Delegated permissions** and application related permissions to **Application** **permissions**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d0af3dbf6bd4361b1d4d639232e11f3~tplv-goo7wpa0wc-image.image) </span>

         The specific permissions that need to be enabled are as follows:

         
         |**Permission Class** |**Specific Permissions** |
         |---|---|
         |Delegated Permissions |* Directory.AccessAsUser.All<br><br>* Directory.ReadWrite.All<br><br>* Group.ReadWrite.All<br><br>* User.Read<br><br>* User.ReadBasic.All |
         |Application related permissions |* Directory.ReadWrite.All<br><br>* Group.ReadWrite.All |
         

         The example of permission enabling is shown in the following figure:

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4eda125294584dc4a283e25ae718b8ef~tplv-goo7wpa0wc-image.image) </span>

   6. Configure the SealSuite portal domain name in the Redirect URI (optional).

      The SealSuite Portal Domain Name Address Format:`https://<SealSuite Portal Domain Name>:<Port>/api/tpslogin/callback/aad`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b816400111444a968b2b530d5b746fef~tplv-goo7wpa0wc-image.image) </span>

   7. Click register to complete the initial application registration.

      After registration, Azure portal will display an **Overview** pane for app registration. You can view **Application (client) ID**, also known as client ID. This value uniquely identifies your application in the Microsoft identity platform. Please save this value for future use in configuring the SealSuite Admin Portal.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2175e2f30a094bacae42782d7c85566f~tplv-goo7wpa0wc-image.image) </span>

      The configuration item description of **Supported account types**:

      This configuration item refers to the supported account types. Select the appropriate type according to your actual situation. If you want accounts from other organizations to also use this application, please select **Any Azure AD directory \- Multitenant**. If you only want members of your own organization to use this application, please select **Single tenant**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cf66afa5e7d4480bbfbd4926db0ced6~tplv-goo7wpa0wc-image.image) </span>

      When selecting **Single tenant**, users from other organizations will receive an error message similar to the following when attempting to log in using Azure AD.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b37bc1be9764f0f826c0bfa1678121d~tplv-goo7wpa0wc-image.image) </span>

3. Create a Client Secret.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For official documentation, please refer to <a href="https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-configure-app-access-web-apis#add-credentials-to-your-web-application">Configure a client application to access a web API</a>.   </div>
   

   1. Go to the **Application Details** \> **Certificates & secrets** page, click  **+ New client secret**.

   2. Select the expiration time of the key or specify a custom lifecycle.

      * The validity period of the client key is limited to two years (24 months) or less. You cannot specify a custom lifecycle that exceeds 24 months.

      * Microsoft recommends that you set the expiration date to be less than 12 months.

   3. Record the Value.

      Value is used to configure the application Secret value when importing the organizational structure of Azure AD and third\-party login within SealSuite later.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The value will no longer be displayed when entering the value again after leaving this page.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91918808ad824d18bfa419f7b89ae934~tplv-goo7wpa0wc-image.image) </span>

   4. Select the expiration time for the secret.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cdbf32505ad4b7fac89e87dcd8c94b6~tplv-goo7wpa0wc-image.image) </span>

      After selection, you can see the generated password. Please save the value.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6682c491c87945acb27a4e8e8bde9b87~tplv-goo7wpa0wc-image.image) </span>


<span id="87922305"></span>
## Step 2: Synchronizing data in the SealSuite Admin Portal


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Directory Sync** tab of the **Account Setup** page, click **Add Data Source**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e52d124c0dd415a805ff2ab1b72e1b6~tplv-goo7wpa0wc-image.image) </span>

4. In the **Select data source** dialog box, click **Azure AD** and click **Create**.

5. In the **Data Source** area of the **Import configuration** page, configure the saved Azure AD application credentials in the **Tenant ID**, **User Pool Secret**, and **Client ID** fields, and then click **Next Step**.

   After filling in the field values, click **Test Connectivity** in the **Third\-Party permission detection** area to help you effectively check whether the permissions of the third\-party platform have been configured, avoiding the inability to use the import function normally after configuration is completed.

6. In the **Data Scope** area, complete the following configuration and click **Next Step**.

   1. In the **Select departments and members** area, select synchronization scope.

      The selected synchronization scope will be imported into the SealSuite Admin Portal.

   2. Set the field mapping relationship between the third party and SealSuite in the **Synchronous data field mapping** area.

      The synchronous data field mapping is used by enterprises to map the fields in the member information of the third party to SealSuite. The **mobile** and **email** are used to match the unique account relationship of the user. Currently, the mapping relationship between the mobile number and the email cannot be deleted.

      In the **Synchronous data field mapping** area, click **Edit** to adjust the field mapping relationship. The left\-side **Third Party Fields** refers to the user field set in the third\-party platform. The right\-side **SealSuite field** refers to the user field that the third\-party platform maps to SealSuite. The field configuration description is as follows:

      * In the SealSuite field column, the third\-party ID (user ID), mobile (mobile phone number), and email (user email) fields cannot be modified or deleted to match the unique account relationship of the user.

      * If the fields provided by SealSuite by default cannot meet the mapping requirements, you can click **Add Mapping** to add the field mapping relationship.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73d85936225f4681b0539727b03f376d~tplv-goo7wpa0wc-image.image) </span>

         When adding a mapping, in addition to the default fields provided by SealSuite, you can also add custom attributes.

         * The following figure shows how to add custom attributes to **Third Party Fields**.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5ad0e249f164ffd8f5d7e8c05d02fe5~tplv-goo7wpa0wc-image.image) </span>

         * The following figure shows how to add custom attributes to **SealSuite field**. The custom attributes are filled in as follows:

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c415fcce5154a3eabb16772762686f5~tplv-goo7wpa0wc-image.image) </span>

            * **Field Key**: Defines a field unique value.

            * **Field Name**: The display name of the field.

            * **Description**: Description of the field.

            * **Field Type**: Optional **String**, **Number**, **Boolean**, **Expression**, **Enum** value.

            * **Advanced configuration**: Optional **Required**, **Unique**, **Editable**.

               Click the settings icon to the right of the **Third Party Fields** and **SealSuite field** column to manage the custom attribute (including add, edit, and delete operations).

               <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/145fad9671bd48208702245583cd4847~tplv-goo7wpa0wc-image.image) </span>

7. In the **Import Mode** area, select import mode and click **Complete configuration**.

   When Azure AD data changes, SealSuite provides you with the following options for synchronizing data, including **Manual Import** and **Automatic Import**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>real\-time synchronization</strong> method only supports Lark, DingTalk, and WeCom.   </div>
   

   
   |**Synchronization Method** |**Note** |**Rule** |
   |---|---|---|
   |**Manual Import** |After the data source is configured, the data synchronization operation is triggered manually. It is applicable to the enterprise administrator who does not want to perform the synchronization task immediately after the configuration is completed, and then manually synchronize after the debugging preparation is completed. |Manual active trigger full synchronization |
   |**Automatic import** |Specify the time to synchronize third\-party data sources. It is applicable to scenarios where enterprises need to complete data synchronization at a fixed time. |Full synchronization at specific time |
   

   * **Manual Import**: Select **Manual Import**, and then manually import the organization data in the data access list.

   * **Automatic import**: Select **Automatic import**, and then select the import mode, which allows you to set the number of minutes or hours, or set a fixed time point every day to import the organization structure.

8. In the **Directory Synchronization** tab, locate your target data source configuration in the list, and turn on the effective switch.

   After the effective switch is turned on, the data synchronization configuration takes effect. Subsequently, data synchronization is performed according to the set synchronization method.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the synchronization method is set for manual import, after the effective switch is turned on, you can click <strong>Start syncing</strong> according to actual needs.   </div>
   

   Click **AzureAD data synchronization** to view the following information:

   * The **Configuration** tab: View **Basic information**, **Synchronization mechanism**, and **Sync range** information.

   * The **Processing History** tab: View historical synchronization records. You can filter out the target synchronization tasks by using the following three filter criteria.

   * In the **Action** column of the synchronization data details, click **Details** to view the comparison of the information synchronized from upstream to the SealSuite data source. Comparing the information content before and after synchronization can help you audit logs or troubleshoot user data problems.

      
      |**Filter criteria** |**Description** |
      |---|---|
      |**Change action** |You can select **All**, **Create**, **Update**, and **Delete**. Only single choice is supported:<br><br><br>* **All**: Refers to the synchronization task that contains all change actions.<br><br>* **Create**: Indicates that a new synchronization task is created.<br><br>* **Update**: Indicates that an existing synchronization task has been updated.<br><br>* **Delete**: When data is deleted on behalf of the upstream data source, the data in the SealSuite is deleted synchronously. |
      |**Sync status** |You can select **All**, **Success**, **Fail**, and **Ignore**. Only single choice is supported:<br><br><br>* **All**: Refers to the synchronization task that contains all synchronization states.<br><br>* **Success**: Indicates that the synchronization task is successfully synchronized.<br><br>* **Fail**: Indicates that the synchronization task failed.<br><br>* **Ignore**: Due to various reasons, it is not stored in the warehouse. For example, when a full synchronization task finds that a real\-time task has stored new data, SealSuite chooses to ignore the data and does not store it. |
      |**Search department/employee** |Filter based on department or employee names contained in synchronized data. |
      


<span id="75003cb3"></span>
# Configuring Azure AD third\-party login SealSuite


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Third\-Party Login** tab, click  **+ Add Login Source**.

4. In the **Select Login Source** dialog box, click the **Azure AD** card.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select the <strong>international version</strong> or <strong>domestic version</strong> according to the actual situation of the Azure AD account. You can log in to your Azure AD account and determine the current version according to the Azure portal domain name information. For relevant information, please refer to <a href="https://learn.microsoft.com/en-us/azure/active-directory/develop/authentication-national-cloud">National clouds</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">International version domain name information: portal.azure.com   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Domestic domain name information: portal.azure.cn   </div>
   

5. The reference interface prompts configuration parameters, and the key parameter descriptions are as follows. After completing the configuration, click **Confirm**.

   
   |**Module name** |**Configuration Item** |**Required** |**Desription** |
   |---|---|---|---|
   |**General** |**Login display icon** |Yes |The identity source icon displayed on the login interface button, click **Upload** to upload the custom display icon. |
   ||**Login Abbreviation (Chinese)**  |Yes |The name below the button on the login interface, such as Azure AD quick login. Click the **View example here** below the input box to learn about the display effect. |
   ||**Login Abbreviation (English)**  |Yes |The name below the button on the login interface. |
   ||**Unique sign** |Not involved |The unique identifier of the login source, used to distinguish tenants with different login authentication, consists of lowercase letters, numbers, and \-, with less than 32 characters in length. Provided by SealSuite by default and cannot be modified. |
   ||**Description** |No |Authentication source description, non\-client display field, is only used to manage backend notes, with a length of less than 40 characters. |
   ||**Login authentication location** |Yes |SealSuite login location allows multiple options for **Mobile**, **Desktop**, or **Web Portal**. |
   |**Authentication Information** |**Application (Client) ID** |Yes |Fill in the saved Azure AD application credential Application (Client) ID. You can enter the **Overview** page of the Azure AD default directory to obtain the Application (client) ID. |
   ||**Tenant ID** |Yes |Fill in the saved Azure AD application credential Tenant ID. You can enter the **Overview** page of the Azure AD default directory to obtain the Directory (tenant) ID.<br><br>The Tenant ID can receive the following types of values, and the last one is configured here. For relevant information, please refer to [Endpoints](https://learn.microsoft.com/en-us/entra/identity-platform/v2-protocols#endpoints).<br><br><br>* common: Allow users to log in to the application from Azure AD using personal Microsoft accounts and work/school accounts.<br><br>* organizations: Only allow users to log in to the application from Azure AD using their work/school accounts.<br><br>* consumers: Only allow users to log in to the application using their personal Microsoft account (MSA).<br><br>* 8eaef023\-2b34\-4da1\-9baa\-8bc8c9d6a490 or contoso.onmicrosoft.com: Only allow users to log in to the application from specific Azure AD tenants using their work and school accounts. You can use the friendly domain name of Azure AD tenant or the tenant's Guid identifier. |
   ||**Client Secret** |Yes |Fill in the saved Azure AD application credentials Client Secret. You can go to the **Certificates & secrets** \> **Client secrets** page in the default directory of Azure AD to obtain the New client secret. |
   |**Advanced Settings** |**Attribute mapping strategy** |Yes |Map the user information of the third\-party login authentication source directly to the user information of SealSuite, that is, establish the mapping relationship between the third party and the SealSuite user during the login process:<br><br><br>* Adjust field mapping: The Azure AD field on the left indicates the user field set in Azure AD. The SealSuite field on the right indicates the user field to be mapped to the SealSuite.<br><br>* Enable automatic login update: When **Open** is selected next to the mapping field, it indicates that if a user exists in the system during login, the user attributes in the system will be updated using the user attributes of the current login.<br><br>* **Delete**: Delete the current mapping rule.<br><br>* **Add**: If the fields provided by SealSuite by default cannot meet mapping requirements, click **Add** to add field mappings.<br><br>* **Add custom attribute**: If the current field does not meet the mapping rule, click **Add custom attribute** and fill in the following parameters:<br><br>   * **Field Key**: Define a unique value for a field.<br><br>   * **Field Name**: Set the display name of the field.<br><br>   * **Description**: Fill in the field description. |
   ||**Uniquely identify priority** |Yes |By dragging and dropping to set the priority of matching identifiers, SealSuite will match the upstream unique identifiers in order of priority. If the current ID does not meet requirements, click **Add** to add the ID. |
   ||**When the login does not match the employee, select the disposal method** |No |When enterprise members log in to SealSuite, if the organizational structure of SealSuite does not match the user, the automatic account creation service will be provided. There are two optional options:<br><br><br>* **Automatically create employee accounts**: After this function is enabled, if no user is matched, a user account is automatically created and the user is associated with the specific department.<br><br>* **Employee login failed, account will not be created**: After this function is enabled, no account will be created if no user is matched. |
   


<span id="0295718f"></span>
## Configuration effect

When opening the SealSuite client, users will find the **Azure AD** icon in the **Or sign in with** area.
