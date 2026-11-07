---
title: "Importing organizational data from WeCom"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-importing-organizational-data-from-wecom"
---

SealSuite supports enterprises importing organizational structure information from third\-party platforms into SealSuite, and supports configuring third\-party login to SealSuite. This article introduces how to import the WeCom organizational structure in the SealSuite Admin Portal, and how to configure third\-party login to SealSuite through WeCom.

<span id="ebda214c"></span>
# Prerequisite

Please make sure you have completed registration in the WeCom management backend, and there is a complete organizational system in the WeCom management backend.

<span id="4fed444b"></span>
# Instructions for use


* If you need to import WeCom organizational structure, please refer to [Importing WeCom organizational structure](https://docs.byteplus.com/docs/sealsuite/docs-importing-organizational-data-from-wecom#cfcce013).

* If you need to configure third\-party login to SealSuite on WeCom, please refer to [Configuring third-party login on WeCom](https://docs.byteplus.com/docs/sealsuite/docs-importing-organizational-data-from-wecom#1acea714).


<span id="cfcce013"></span>
# Importing WeCom organizational structure

<span id="1169a5f7"></span>
## Step 1: Creating a self\-built enterprise application on the WeCom open platform


1. Use the WeCom administrator account to log in to the [homepage of the WeCom management backend](https://work.weixin.qq.com/wework_admin/frame#/index).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db8ad504a9b64f0d82716f91179dae42~tplv-goo7wpa0wc-image.image) </span>


2. Create an application and set the **Allowed users**.

   1. In the top navigation bar, click **App Management**, and in the **Apps** tab, drop down the page to the **Self\-built** area and click **Create an app**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79a8fadfb60d4d54895bb73b8db9064f~tplv-goo7wpa0wc-image.image) </span>

   2. On the **Create an app** page, fill in the application information and select the allowed users.

      You need to configure the **App Logo**, **App Name**, **About this App (Optional)** , and **Allowed users** in sequence. Only users set within the **Allowed users** range can log in to SealSuite through WeCom authorization after importing the organizational structure and configuring third\-party login.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96d94da48bb2432d92cf3dea3292b2f8~tplv-goo7wpa0wc-image.image) </span>

3. Obtain application Secret.

   1. After creating the application successfully, check the application details to obtain the Secret and Allowed users range of the application. If you are not creating an application for the first time, you can select a specific application in **App Management** \> **Self\-built** \> **View Created Apps**. Click **View** and then Secret will be distributed through the WeCom team.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adbc618375f94508a7082a382ba06b6e~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Send Secret to WeCom for Viewing** area, click **Send**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/447330962bf448b6b5a6e31fa094f7cf~tplv-goo7wpa0wc-image.image) </span>

   3. In WeCom, enter the **WeCom Team** dialog box and click **View Now** at the prompt.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fbb6bd99da4475bbba0f3cc5f850403~tplv-goo7wpa0wc-image.image) </span>

   4. Copy Secret on the details page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac17d758e66949b1834d2f1bba507884~tplv-goo7wpa0wc-image.image) </span>

4. On the **My Company** \> **Company Information** page of the WeCom Open Platform, obtain the Company ID.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/653d9d94e4ba4a4498aaef5f6a3a2c54~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Address book synchronization or event subscription.

   When there is a change in the data of the WeCom organization, SealSuite provides three synchronization methods for the enterprise to choose from, including manual synchronization, scheduled synchronization, and real\-time synchronization. If the enterprise chooses real\-time synchronization, it needs to obtain **Token** and **EncodingAESKey**.

   * **Manual import**: Manually initiate synchronization operations and click on synchronization to execute the synchronization task. It is suitable for enterprise administrators who do not want to perform synchronization tasks immediately after configuration is completed, and can manually synchronize after debugging preparation is completed.

   * **Auto** **import**: Specify a time to synchronize third\-party data sources. It is suitable for scenarios where enterprises need to complete data synchronization at a fixed time.

   * **Real time synchronization (recommended)** : Perform differential synchronization based on real\-time changes in organizational structure or personnel information. The characteristics of real\-time synchronization are fast synchronization speed, timely response, and no need for queuing and waiting. It is suitable for enterprise users who have significant daily adjustments to user and department data information, and need to obtain changes in a timely manner on SealSuite.

      The parameter description is as follows:

   * Obtain Token and EncodingAESKey

      1. In **Management Tool** \> **Set event receiving server**, click **Set event receiving server**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82b6cba5dd104967ab4e956341fe1b72~tplv-goo7wpa0wc-image.image) </span>

      2. Confirmation messages will be sent through the **WeCom Team**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa4e9674d72d44f88c79a1c174a7cda7~tplv-goo7wpa0wc-image.image) </span>

      3. In Wecom, enter the **WeCom Team** dialog box and click **View Now** at the prompt.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81341247e51c42a2b4f8210ec14909b0~tplv-goo7wpa0wc-image.image) </span>

      4. On the details page of **Set event receiving server**, click **Confirm**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b45655d9bea40daa495045db5fd3fbe~tplv-goo7wpa0wc-image.image) </span>

      5. Return to **Management Tool** \> **Set event receiving server** of the WeCom Management backend, click **Get randomly** to generate Token and EncodingAESKey.

         The **URL** field needs to be set to the URL of the receiving event server. The format is `http://<feilian portal domain name>:<port>/webhook/lark/<placeholder>`, such as `http://feilian-****:8443/webhook/lark/<placeholder>`.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/548a92cea1be44c0bb47eb4cc1724863~tplv-goo7wpa0wc-image.image) </span>


<span id="ff794252"></span>
## Step 2: Synchronize data in the Admin Portal


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Directory Sync** tab of the **Account Setup** page, click **Add data source**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2bace710ff344df815a557230c422a1~tplv-goo7wpa0wc-image.image) </span>

4. In the **Select data source** dialog box, click **WeCom**, and click **Create**.

5. In the **Data Source** area of the **Import configuration** page, configure the saved WeCom application credentials in the **Corporate ID** and **Secret** fields, and click **Next Step**.

   After filling in the field values, you can click **Test Connectivity** in the **Third\-Party permission detection** area. This helps you to effectively check whether the permissions of the third\-party platform have been configured, avoiding not being able to use the import function properly after configuration is completed.

6. On the **Data Scope** page, complete the following configurations and click **Next Step**.

   1. In the **Select departments and members** area, select the synchronization scope.

      The selected synchronization scope is imported to the Admin Portal.

   2. In the **Synchronous data field mapping** area, set the field mapping relationship between the third party and SealSuite.

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

            * **Field Type**: Optional **String**, **Number**, **Boolean**, **Expression**, **Enum** **value**.

            * **Advanced configuration**: Optional **Required**, **Unique**, **Editable**.

               Click the settings icon to the right of the **Third Party Fields** and **SealSuite field** column to manage the custom attributes (including add, edit, and delete operations).

               <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/145fad9671bd48208702245583cd4847~tplv-goo7wpa0wc-image.image) </span>

7. In the **Import Mode** area, select import mode and click **Complete configuration**.

   When WeCom data changes, SealSuite provides you with the following options for synchronizing data, including **Manual import**, \*\*Automatic import \*\*and **Real\-time Synchronization**.

   
   |**Synchronization method** |**Description** |**Rule** |
   |---|---|---|
   |**Manual import** |After the data source is configured, the data synchronization operation is triggered manually. It is applicable to the enterprise administrator who does not want to perform the synchronization task immediately after the configuration is completed, and then manually synchronize after the debugging preparation is completed. |Manual active trigger full synchronization |
   |**Automatic import** |Specify the time to synchronize third\-party data sources. It is applicable to scenarios where enterprises need to complete data synchronization at a fixed time. |Full synchronization at specific time |
   |**Real\-time Synchronization** |A fine\-grained synchronization method. Real\-time synchronization will perform differential synchronization based on real\-time changes in organizational structure or personnel information. The characteristics of real\-time synchronization are fast synchronization speed, timely response, and no need for queuing and waiting. It is suitable for enterprise users who have significant daily adjustments to user and department data information, and need to obtain changes in a timely manner on SealSuite. |Incremental synchronization (only synchronizing changed department and user information) |
   

   * **Manual Import**: Select **Manual Import**, and then manually import the organization data into the data access list.

   * **Automatic import**: Select **Automatic import**, and then select the import mode, which allows you to set the number of minutes or hours, or set a fixed time point every day to import the organization structure.

   * **Real\-time Synchronization**: Select **Real\-time Synchronization** and fill in the obtained **encrypted aes_Key** and **signature token**.

8. In the **Directory Synchronization** tab, locate the added data source configuration in the list, and turn on the effective switch.

   After the effective switch is turned on, the data synchronization configuration takes effect. Later, data synchronization is performed according to the set synchronization method.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the synchronization method is set for manual import, after the effective switch is turned on, you can click <strong>Start syncing</strong> according to actual needs.   </div>
   

   In addition, clicking **WeChat data synchronization** to view the following information:

   * The **Configuration** tab: View **Basic information**, **Synchronization mechanism**, and **Sync range** information.

   * The **Processing History** tab: View historical synchronization records. You can filter out the target synchronization tasks by using the following three filter criteria.

      In the **Action** column of the synchronization data details, click **Details** to view the comparison of the information synchronized from upstream to the SealSuite data source. Comparing the information content before and after synchronization can help you audit logs or troubleshoot user data problems.

      
      |**Filter criteria** |**Description** |
      |---|---|
      |**Change action** |You can select **All**, **Create**, **Update**, and **Delete**. Only single choice is supported:<br><br><br>* **All**: The synchronization task that contains all change actions.<br><br>* **Create**: Indicates that a new synchronization task is created.<br><br>* **Update**: Indicates that an existing synchronization task has been updated.<br><br>* **Delete**: When deleting data from upstream data sources, the data in the SealSuite is deleted synchronously. |
      |**Sync status** |You can select **All**, **Success**, **Fail**, and **Ignore**. Only single choice is supported:<br><br><br>* **All**: The synchronization task that contains all synchronization states.<br><br>* **Success**: Indicates that the synchronization task is successfully synchronized.<br><br>* **Fail**: Indicates that the synchronization task failed.<br><br>* **Ignore**: The situation of not being stored for various reasons. For example, when a full synchronization task finds that a real\-time task has stored new data, SealSuite chooses to ignore the data and does not store it. |
      |**Search department/employee** |Filter based on department or employee names contained in synchronized data. |
      


<span id="1acea714"></span>
# Configuring third\-party login on WeCom

<span id="835f78a2"></span>
## Step 1: Configure WeCom to obtain application credentials


1. Use the WeCom administrator account to log in to the [homepage of the WeCom management backend](https://work.weixin.qq.com/wework_admin/frame#/index).

2. Create an application and set the **Allowed users**.

   1. Select **App Management** \> **Apps**. In the **Self\-built** area at the bottom of the page, click **Create an app**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9d6c6d5bf99473f87b710b5dd0c1fd4~tplv-goo7wpa0wc-image.image) </span>

   2. On the **Create an app** page, complete the following configurations and click **Create an app**.

      * Custom **App logo**, **App Name**, and **About this App (Optional)** .

      * Set **Allowed users**, only users within the **Allowed users** range can log in through WeCom authorization after configuring successfully.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7a7175e7e9d4aedabaf5043ef63fdfa~tplv-goo7wpa0wc-image.image) </span>

3. Obtain application Secret.

   1. After creating the application, enter the application details page to obtain the **AgentId**, **Secret**, and **Allowed users**.

      * If you are not creating an application for the first time, you can select a specific application to view in **App Management** \> **Self\-built**.

      * Click **View** in the **Secret** area, and the Secret will be distributed through the WeCom team.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9aa97aa7e9d4d1ca27887079d1920d8~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Send Secret to WeCom for Viewing** area, click **Send**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf6a065903c5420cb8858bf28e2a9e7d~tplv-goo7wpa0wc-image.image) </span>

   3. In WeCom, enter the **WeCom Team** dialog box and click **View Now** at the prompt.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f316b8e247e34282bef468e7fb6efc6b~tplv-goo7wpa0wc-image.image) </span>

   4. Enter the details page and click **Copy** to copy the Secret.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/624b6ac1e9b54c518182178fdcac317b~tplv-goo7wpa0wc-image.image) </span>

4. On the WeCom Open Platform, go to **My Company** \> **Company Information** to obtain the Company ID.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25cb4548bd3e49dfb66a727660c273db~tplv-goo7wpa0wc-image.image) </span>

5. Obtain schema.

   1. In the **Developer API** area at the bottom of the application details page, click **Setting** in the **Log in to via authorization by WeCom** card.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73620c023a6045ef9341dda4b52da522~tplv-goo7wpa0wc-image.image) </span>

   2. On the **Log in to via authorization by WeCom** page, configure the required categories and obtain schema.

      * Fill in the authorized callback field of the Web page:`<feilian portal domain name>:<port>`.

      * Fill in the Bundle ID of iOS:`com.volcengine.corplink`.

      * Fill in the application signature of Android:`3e9cb873ed7fa8ba2d5d470812e1bab4`.

      * Fill in the application package name of Android:`com.volcengine.corplink`.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba0f8904830346738a0d0d4346fbf36c~tplv-goo7wpa0wc-image.image) </span>

   3. When the configuration is complete, click **Back** in the upper left corner of the page.

6. Set trusted domain name.

   1. In the **Developer API** area at the bottom of the application details page, click **Set trusted domain name** in the **Web Authorization and JS\-SDK** area.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a134c2823f34cd88a8e979561871ec0~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Can be used as the callback domain name for app's OAuth2.0\-based webpage authorization feature** area of the **Set trusted domain name** dialog box, fill in`<feilian portal domain name>:<port>`.

      This configuration is used to achieve login\-free access to SealSuite within the App, no longer requires manual login.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5b27017435a4f3682b644cfa3533c9b~tplv-goo7wpa0wc-image.image) </span>


<span id="9b980818"></span>
## Step 2: Configure a third\-party login in the SealSuite Admin Portal


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Third\-Party Login** tab, click  **+ Add Login Source**.

4. In the **Select Login Source** dialog box, click the **WeCom** card.

5. The reference interface prompts configuration parameters, and the key parameter descriptions are as follows. After completing the configuration, click **Confirm**.

   
   |**Module name** |**Configuration Item** |**Required** |**Description** |
   |---|---|---|---|
   |**General** |**Login display icon** |Yes |The identity source icon displayed on the login interface button, click **Upload** to upload the custom display icon. |
   ||**Login Abbreviation (Chinese)**  |Yes |The name below the button on the login interface, such as WeCom quick login. Click the **View example here** below the input box to learn about the display effect. |
   ||**Login Abbreviation (English)**  |Yes |The name below the button on the login interface. |
   ||**Unique sign** |Not involved |The unique identifier of the login source, used to distinguish tenants with different login authentication, consists of lowercase letters, numbers, and \-, with less than 32 characters in length. Provided by SealSuite by default and cannot be modified. |
   ||**Description** |No |Authentication source description, non\-client display field, is only used to manage backend notes, with a length of less than 40 characters. |
   ||**Login authentication location** |Yes |SealSuite login location allows multiple options for **Mobile**, **Desktop**, or **Web Portal**. |
   |**Authentication Information** |**Corporate ID** |Yes |Enter the Company ID obtained by WeCom's management backend. You can go to **My Company** page of WeCom's management background to get the company ID. |
   ||**Agent ID** |Yes |Enter the AgentId obtained by WeCom's management backend. You can go to the **App Management** \> **Apps** of WeCom Management backend to obtain the AgentId. |
   ||**Secret** |Yes |Enter the Secret obtained by WeCom's management backend. You can go to the **App Management** \> **Apps** of WeCom Management backend to obtain the Secret. |
   ||**Schema** |Yes |Enter the Schema obtained by WeCom's management backend. You can go to **App Management** \> **Apps** \> **Login in to via authorization by WeCom** page to obtain Schema. |
   ||**Upload Domain Name Verification File** |No |To upload verification files, you can download verification files at **App Management** \> **Apps** \> **Set trusted domain name** \> **Domain name to be verified**. Please do not modify the inspection files. |
   |**Advanced Settings** |**Attribute mapping strategy** |Yes |Map the user information of the third\-party login authentication source directly to the user information of SealSuite, that is, establish the mapping relationship between the third party and the SealSuite user during the login process:<br><br><br>* Adjust field mapping: The WeCom field on the left indicates the user field set in WeCom. The SealSuite field on the right indicates the user field to be mapped to the SealSuite.<br><br>* Enable automatic login update: When **Open** is selected next to the mapping field, it indicates that if a user exists in the system during login, the user attributes in the system will be updated using the user attributes of the current login.<br><br>* **Delete**: Delete the current mapping rule.<br><br>* **Add**: If the fields provided by SealSuite by default cannot meet mapping requirements, click **Add** to add field mappings.<br><br>* **Add custom attribute**: If the current field does not meet the mapping rule, click **Add custom attribute** and fill in the following parameters:<br><br>   * **Field Key**: Define a unique value for a field.<br><br>   * **Field Name**: Set the display name of the field.<br><br>   * **Description**: Fill in the field description. |
   ||**Uniquely identify priority** |Yes |By dragging and dropping to set the priority of matching identifiers, SealSuite will match the upstream unique identifiers in order of priority. If the current ID does not meet requirements, click **Add** to add the ID. |
   ||**When the login does not match the employee, select the disposal method** |No |When enterprise members log in to SealSuite, if the organizational structure of SealSuite does not match the user, the automatic account creation service will be provided. There are two optional options:<br><br><br>* **Automatically create employee accounts**: After this function is enabled, if no user is matched, a user account is automatically created and the user is associated with the specific department.<br><br>* **Employee login failed, account will not be created**: After this function is enabled, no account will be created if no user is matched. |
   


<span id="6f2e2886"></span>
## Configuration effect

When opening the SealSuite client, users will find the **WeCom** icon in the **Or sign in with** area.
