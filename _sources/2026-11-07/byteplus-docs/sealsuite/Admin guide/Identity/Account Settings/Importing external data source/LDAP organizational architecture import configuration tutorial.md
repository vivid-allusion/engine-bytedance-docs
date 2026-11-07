---
title: "LDAP organizational architecture import configuration tutorial"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-ldap-organizational-architecture-import-configuration-tutorial"
---

SealSuite allows enterprises to import organizational structure data from third\-party platforms into SealSuite. This article primarily focuses on importing the LDAP organizational structure into the SealSuite Admin Console.

<span id="138a43c9"></span>
# Protocol introduction

LDAP (Lightweight Directory Access Protocol) is a software protocol that allows users to easily access information about organizations, individuals, and resources, such as files and devices, either on the Internet or within a corporate intranet. As a lightweight version of the Directory Access Protocol (DAP), LDAP is part of the X.500 standard, which defines the standard for directory services on the network.

<span id="a640e920"></span>
# Prerequisites

Enterprises must have an existing LDAP service and a well\-defined organizational structure within the LDAP.

<span id="dbb0e9f5"></span>
# Perform directory synchronization in the SealSuite Admin Console


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page's **Directory Sync** tab, click **Add Data Source**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed5401ee3dff41f3bfeca5be1a5aafc3~tplv-goo7wpa0wc-image.image) </span>

4. In the **Select data source** dialog box, under the **Upstream Synchronization** tab, click **LDAP**, and then click **Create**.

5. On the **Import configuration** page, in the **Data Source** area, complete the following settings and click **Next Step**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Server Host** |Address of the server that holds LDAP. It is recommended to follow the secure lightweight directory access protocol LDAPs, with the address format: `ldaps://<host>:<post>`, where `<host>` refers to the server domain name or IP address, and `<post>` refers to the port number. Example values: `ldaps://xxx`, `ldap://xxx:389`. |
   |**Administrator DN** |Specifies a user who has administrative rights and can connect to the LDAP server. An Administrator account is defined in LDAP using attributes such as DC (Domain Component), CN (Common Name), and OU (Organizational Unit). For example, the value could be: `cn=admin, dc=feilian, dc=com`. |
   |**Administrator Password** |Password information corresponding to the **Administrator DN**. |
   |**User Object Class** |User Object (objectClass). Example values for different LDAP servers are as follows:<br><br><br>* OpenLDAP:inetOrgPerson<br><br>* LDAP\-based AD domain: User or organizationalPerson |
   |**Organizational object class** |Organizational object (objectClass). Example values for different LDAP servers are as follows:<br><br><br>* openLDAP: organizationalUnit (or possibly groupOfNames)<br><br>* Based on LDAP's AD domain: organizationalUnit. |
   |**Base DN** |Search for organizational objects starting from this root. The path of nodes is defined by DC (Domain Component), CN (Common Name), OU (Organizational Unit) attributes in LDAP. For example, the value could be: `dc=feilian, dc=com`. |
   |**User ID** |Unique identifier attribute for each user instance in LDAP. Description of unique identifier attributes for different LDAP servers:<br><br><br>* OpenLDAP:uid、dn<br><br>* LDAP\-based AD domain: sAMAccountName |
   |**Member fields in the organizational structure** |If the organization type is a group, information about the members within the group is required for this field. Example value: member. |
   |**Organizational Structure Fields in Members** |Custom Configuration: Please tailor it to meet your specific needs. |
   |**User Termination Field Value** |Fill in the User Termination Field Value corresponding to each user instance in LDAP. |
   |**User termination field mapping** |Fill in the user termination field mapping for each user instance in the LDAP. |
   |**Unit** |Please select a unit for data source synchronization. |
   |**Third\-party permission detection** |After entering the value, you can click on the **Third\-Party Permission Detection** area and **Test Connectivity** to effectively ensure that the permissions for the third\-party platform are enabled. This helps prevent issues during normal use after the configuration is complete during the import process. For LDAP, it will test the communication between SealSuite and the LDAP data, and check whether the apply permissions are enabled. |
   

6. On the **Data Scope** interface, complete the following settings, and click **Next Step**.

   1. In the **Select departments and members** area, select the synchronization objects.

      The selected synchronization objects will be imported into the SealSuite Admin Console.

   2. In the **Synchronous data field mapping** area, set up the mapping relationship between third\-party and SealSuite fields.

      Companies use synchronous data field mapping to transfer fields from third\-party member information into SealSuite. Here, the **Mobile** and **Email** fields are crucial for matching the unique user account relationship. Currently, deleting the mapping relationship of phone numbers and emails is not supported.

      In the **Synchronous data field mapping** area, click **Edit** to manually adjust the mapping relationship; the left side **Third Party Fields** refers to the user fields set within the third\-party platform. The right side **SealSuite field** refers to the user fields that are mapped from the third\-party platform to SealSuite. Configuration instructions for the fields are as follows:

      * In the SealSuite field column, Third Party User ID (third_party_user_id), Mobile (mobile), and Email (email) fields cannot be modified or deleted, as they are used to match unique user account relationships.

      * If the default fields provided by SealSuite do not meet the mapping needs, you can click **Add mapping** to manually add a field mapping.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b57f1af56fe43cdb25d6529d0c95ed6~tplv-goo7wpa0wc-image.image) </span>

         When adding mappings, in addition to selecting the default fields provided by SealSuite, you can also manually add custom attributes.

         * The method of adding custom attributes in **Third Party Fields** is shown in the figure below.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75013e2bada441a0ad41786456d313f3~tplv-goo7wpa0wc-image.image) </span>

         * The method of adding custom attributes in **SealSuite fields** is shown in the figure below, and the instructions for filling in custom attributes are as follows:

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a9d0266423c4543932d3a434fd935db~tplv-goo7wpa0wc-image.image) </span>

            * **Field Key**: Define the unique value of the field.

            * **Field Name**: The display name of the field.

            * **Description**: The explanation of the field.

            * **Field Type**: Options include **String**, **Number**, **Boolean**, **Expression**, **Enum**.

            * **Advanced configuration**: Options include **Required**, **Unique**, **Editable**.

               To manage Custom Attributes uniformly (including adding, editing, and deleting), click the settings icon located to the right of the column names for **Third Party Fields** and **SealSuite field**.

               <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07a997d03319461a9898565e25ec430e~tplv-goo7wpa0wc-image.image) </span>

7. In the **Import Mode** area, select the import mode and click **Complete configuration**.

   When LDAP data changes, SealSuite provides you with the following methods to import data, including **Manual Import** and **Automatic import**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Real\-time Import</strong> method only supports Feishu, DingTalk, and WeCom.   </div>
   

   
   |**Import method** |**Note** |**Strategy** |
   |---|---|---|
   |**Manual Import** |Once the data source is configured, the data import process is manually initiated by staff. This function is designed for corporate administrators to configure. If they prefer not to execute the import task immediately, they can opt for a manual import once the debugging preparations are complete. |Manual full import |
   |**Automatic import** |Specify the time to import the third\-party data source. Suitable for scenarios where the company needs to complete data imports at a fixed time. |Scheduled full import |
   

   * **Manual Import**: Select **Manual Import**, then manually start importing the organizational structure data from the directory sync list.

   * **Automatic import**: Select **Automatic import**, choose the import mode, and enable settings for importing organizational structure every few minutes or hours, or set at a fixed time daily.

8. In the **Directory Synchronization** tab, find the added data source, and turn on the enable switch.

   Once the enable switch is activated, the directory synchronization configuration becomes effective, and data synchronization will proceed according to the established rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the synchronization method is set to Manual Import, once the effective switch is activated, you can manually click <strong>Start syncing</strong> whenever necessary.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34f72a5f0ff34839bd8690f41e28264a~tplv-goo7wpa0wc-image.image) </span>

   In addition, click **LDAP Sync** to view the following information:

   * **Configuration** tab: View **Basic Configuration**, **Synchronization Mechanism**, and **Sync Scope** information.

   * **Processing History** tab: View synchronization history. You can refine your search of the processing history by applying these three filters.

      In the View Information column of Sync data details, click **Action** and then click **Details** to view the comparison of the information synchronized upstream to the SealSuite data source. Comparing data before and after synchronization can assist in conducting audit logs or troubleshooting user data issues.

      
      |**Filters** |**Note** |
      |---|---|
      |**Change action** |Available options are **all**, **create**, **update**, and **delete**. Please note that only one option can be selected at a time.<br><br><br>* **All**: Includes synchronization tasks of all change actions.<br><br>* **Create**: Represents the creation of a new synchronization task.<br><br>* **Update**: Represents the updating of an existing synchronization task.<br><br>* **Delete**: Represents the deletion of data in SealSuite when data is deleted from the upstream data source. |
      |**Sync status** |Available options are **all**, **successful**, **failed**, and **ignore**. Please note that only one option can be selected at a time.<br><br><br>* **All**: Includes synchronization tasks of all sync statuses.<br><br>* **Successful**: Represents a successfully completed synchronization task.<br><br>* **Failed**: Represents a synchronization task that failed.<br><br>* **Ignore**: Represents a situation where it is not warehoused for various reasons, such as when a full synchronization task finds that an existing real\-time task has stored new data, SealSuite chooses to ignore the data and not store it. |
      |**Search department/employee names** |Filter based on the department or employee names included in the sync data. |
      


<span id="547bf9fd"></span>
# Configuring a third\-party login through the SealSuite Admin Console.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. Click the **Third\-Party Login** tab, and then click **Add Login Source** at the top right corner.

4. In the **Select Login Source** dialog box, click on the **LDAP** card.

5. To configure the settings, please follow the prompts displayed on the interface. Below, key parameters are detailed for your understanding. Once you have finished setting up, click **Confirm**.

   
   |**Module** |**Configuration Item** |**Required** |**Note** |
   |---|---|---|---|
   |**Basic Info** |**Login icon** |Yes |The identity source icon displayed on the login interface button. Click **Reupload** to upload a custom display icon. |
   ||**Login abbreviation (Chinese)**  |Yes |The name displayed below the button on the login interface, such as Feishu Quick Login, click the **example** below the input field to see a preview of how it will appear. |
   ||**Login abbreviation (English)**  |Yes |The name displayed under the button on the login interface. |
   ||**Unique identifier** |Not involved |The login source unique identifier is used for authentication to differentiate between various tenant logins. It is composed of lowercase letters, numbers, and "\-", and must be fewer than 32 characters in length. SealSuite provides this by default; it cannot be modified. |
   ||**Unit** |is |Please select the unit applicable for this authentication source. Once set up, the employees of this unit can log in using this method. |
   ||**Description** |No |Description for authentication source, not visible to clients, intended solely for Admin Console notes, must be under 40 characters. |
   ||**Login page** |Yes |Please choose the suitable authentication method for the SealSuite client type. By default, the **SealSuite Mobile**, **Desktop**, or **Web Portal** are all available to use this authentication method. |
   |**LDAP/AD Authentication Configuration** |**Server Host** |is |Server address hosting the LDAP. It is recommended to follow the secure Lightweight Directory Access Protocol LDAPS, address format: `LDAPS://<host>:<post>`.<br><br><br>* `<host>` indicates the server domain name or IP address.<br><br>* `<post>` refers to the port number. The default protocol for LDAP is 389, and for LDAPS it is 636. |
   ||**Base DN** |Yes |Enter the saved Lark app credentials **App Secret**. You can obtain the App Secret on the **App Details** page of the **Credentials and Basic Information** on the Feishu Open Platform. |
   ||**Administrator DN** |is |Specifies a user who can connect to the LDAP server and has administrative rights. Example value: `cn=admin, dc=feilian, dc=com`. |
   ||**Administrator Password** |Yes |**Administrator DN** and associated password information. |
   ||**User ID** |Yes |The unique identifier for each user instance in LDAP. Example values are as follows:<br><br><br>* OpenLDAP:uid、dn<br><br>* AD domain: sAMAccountName |
   ||**User Object Class** |Yes |user object (objectclass). Example values are as follows:<br><br><br>* OpenLDAP:inetOrgPerson<br><br>* LDAP\-based AD domain: User or organizationalPerson |
   ||**User Termination Field Value** |No |If LDAP attributes indicate a user's termination, please enter them. Example values are as follows:<br><br><br>* OpenLDAP:employeeType<br><br>* AD Domain: UserAccountControl |
   ||**Termination Identifier** |No |Keyword indicating user's departure status. Example values are as follows:<br><br><br>* OpenLDAP: separated<br><br>* LDAP\-based AD Domain: 514 (decimal) |
   ||**Connectivity Test** |N/A |Click on the **Connectivity Test** to verify the network connection between the LDAP server and the SealSuite Admin Console. |
   |**Advanced Settings** |**Attribute Mapping** |Yes |Map employee details directly from the third\-party login authentication source to SealSuite's employee records, thereby establishing a link between third\-party and SealSuite users during the login process.<br><br><br>* Adjust the mapping relation: Left side refers to the user fields set within Feishu. The right side SealSuite field refers to the user fields that need to be mapped to SealSuite.<br><br>* Enable Auto Update: If this option is **checked**, it means that during login, if a user with matching credentials is found, their attributes will be updated with the information from the current login session.<br><br>* **Delete**: Delete the current mapping strategy.<br><br>* **Add**: If the default fields provided by SealSuite do not meet the mapping requirements, you can click **Add** to manually add field mapping relations.<br><br>* **Add Custom Attribute**: If the current field does not conform to the mapping strategy, you can click **Add Custom Attribute**. The explanation for the field is as follows:<br><br>   * **Field Key**: Defines the unique value of the field.<br><br>   * **Field Name**: Sets the display name of the field.<br><br>   * **Description**: Provides the explanation of the field. |
   ||**Uniquely ID Priority** |Yes |Arrange the priority of matching identifiers by dragging them and SealSuite will match the unique identifiers upstream according to the established priority. If the current identifier does not meet the requirements, you can click **Add** to manually add an identifier. |
   ||**When the login does not match an employee, select a mitigation method.**  |No |When corporate members log in to SealSuite and their profiles are not matched within the organizational structure, an auto\-creation service is triggered. Available options include:<br><br><br>* **Automatically create employee accounts**: When activated, if an employee is not matched at login, an employee account will be automatically created and associated with the designated department.<br><br>* **If employee login fails, an account will not be created**: When activated, if an employee is not matched at login, an account will not be created. |
