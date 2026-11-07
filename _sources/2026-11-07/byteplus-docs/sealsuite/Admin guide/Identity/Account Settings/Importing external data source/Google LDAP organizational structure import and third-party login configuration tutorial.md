---
title: "Google LDAP organizational structure import and third-party login configuration tutorial"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Google_LDAP_organizational_structure_import_and_third-party_login_configuration_tutorial"
---

SealSuite enables enterprises to import organizational structure data from third\-party platforms into SealSuite. This article primarily focuses on importing the Google LDAP organizational structure into the SealSuite Admin Console.

<span id="f852c77f"></span>
# Protocol introduction

LDAP (Lightweight Directory Access Protocol) is a software protocol that enables users to conveniently access information about organizations, individuals, and resources, such as files and devices on the Internet or within a corporate intranet. Google LDAP refers to the LDAP\-compliant service provided by Google, namely Google Workspace (formerly G Suite). Google Workspace is a suite of cloud computing and collaboration tools provided by Google on a subscription basis. It includes a user directory and authentication services that can be seamlessly integrated and interacted with through the LDAP protocol.

User accounts and organizational structures in Google Workspace can be synchronized with other systems through the LDAP interface, enabling features like single sign\-on and authentication.

<span id="3c4531c5"></span>
# Prerequisites


* The company has activated Google Workspace services and has maintained user directory within Google Workspace.

* The company has added a Client in Google Workspace's LDAP for validation in SealSuite and set the verification/read permissions for the entire domain (as shown below).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/215dab2bb130447196a6e7b5ba969333~tplv-goo7wpa0wc-image.image) </span>


<span id="70d70d8d"></span>
# Perform directory synchronization in the SealSuite Admin Console


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page's **Directory Sync** tab, click **Add Data Source**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b86e1ee23594d15a7a8e3cd63cc4228~tplv-goo7wpa0wc-image.image) </span>

4. In the **Select data source** dialog box, click **Google LDAP**, and then click **Create**.

5. On the **Import configuration** page, in the **Data Source** area, complete the following settings and click **Next Step**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Data source name** |The default name is "Google LDAP Data Sync", but you can rename it based on your specific business needs. |
   |**Server address** |Server address hosting the LDAP. It is recommended to follow the Secure Lightweight Directory Access Protocol LDAPs, address format: `ldaps://<host>:<post>`, where `<host>` refers to the server domain name or IP Address, `<post>` refers to the port number, example value: `ldaps://ldap.google.com:636`. |
   |**Administrator account** |Specifies a user who can connect to the LDAP server and has administrative rights. Administrator account is defined in LDAP with DC (Domain Component), CN (Common Name), OU (Organizational Unit) attributes, example value: `cn=admin, dc=seal, dc=com`. |
   |**Administrator Password** |Password corresponding to the Administrator account. |
   |**User Object Class** |This field corresponds to the user ObjectClass in LDAP. Example values for different LDAP servers are as follows:<br><br><br>* OpenLDAP: inetOrgPerson<br><br>* LDAP\-based AD domain: User or organizationalPerson |
   |**Organizational object class** |This field corresponds to the organizational ObjectClass in LDAP. Example values for different LDAP servers are as follows:<br><br><br>* openLDAP: organizationalUnit (or possibly groupOfNames)<br><br>* LDAP\-based AD domain: organizationalUnit |
   |**Base DN** |Search for organizational objects starting from this root. The path of nodes is defined by DC (Domain Component), CN (Common Name), OU (Organizational Unit) attributes in LDAP, with an example value of `dc=seal, dc=com`. |
   |**User ID** |Unique identifier attribute for each user instance in LDAP. Description of unique identifier attributes for different LDAP servers:<br><br><br>* OpenLDAP: uid or dn<br><br>* LDAP\-based AD domain: sAMAccountName |
   |**Member fields in the organizational structure** |If the organization type is "group," this field must be completed with personnel information from the group, for example, "member." |
   |**Organizational Structure Fields in Members** |Custom configuration: Please complete according to your specific needs. |
   |**User Termination Field Value** |Fill in the user termination field of each user instance in LDAP, example value: suspended. |
   |**User termination field mapping** |Fill in the user termination field value of each user instance in LDAP, example value: true. |
   |**Client side certificate** |Fill in the client's public key certificate, which is used when the client tries to establish a connection with the LDAP server address. |
   |**Client side certificate key** |Input the client's private key to pair it with the public key in the certificate. |
   |**Third\-party permission detection** |You can click the **Third\-Party permission detection** area's **Test Connectivity** to effectively check whether the permissions for the third\-party platform are enabled, avoiding issues during import after setup. For LDAP, it will test the communication between SealSuite and the LDAP data, and check whether the apply permissions are enabled. |
   

6. On the **Data Scope** interface, complete the following settings and click **Next Step**.

   * In the **Select departments and users** area, select the synchronization objects.

      The selected synchronization objects will be imported into the SealSuite Admin Console.

   * In the **Synchronous data field mapping** area, set up the mapping relationship between third\-party and SealSuite fields.

      Synchronous data field mapping is used by companies to map fields from third\-party member information to SealSuite, where the **Phone number** and **email** are used to match the unique user account relationship, mapping relationship of phone number and email is temporarily and cannot deleted.

      In the **Synchronous data field mapping** area, click **Edit** to adjust the mapping relationship; the left side **Third Party Fields** refers to the user fields set within the third\-party platform. The right side **SealSuite field** refers to the user fields that are mapped from the third\-party platform to SealSuite. Configuration instructions for the fields are as follows:

      * In the SealSuite field column, Third Party User ID (third_party_user_id), Mobile (mobile)), and Email (email) fields cannot be modified or deleted, as they are used to match unique user account relationships.

      * If the default fields provided by SealSuite do not meet the mapping needs, you can click **Add mapping** to manually add a field mapping.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8079083812d446978d4e63bf2f3bc1b1~tplv-goo7wpa0wc-image.image) </span>

         When adding mappings, besides selecting the default fields provided by SealSuite, it also supports manually adding custom attributes.

         * The method of adding custom attributes in **Third Party Fields** is shown in the figure below.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9c1d8c0fda3413395abd42309249355~tplv-goo7wpa0wc-image.image) </span>

         * The method of adding custom attributes in **SealSuite fields** is shown in the figure below, and the instructions for filling in custom attributes are as follows:

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84dc410ade1a49c0b0cc455c5a43b2a5~tplv-goo7wpa0wc-image.image) </span>

            * **Field Key**: Define the unique value of the field.

            * **Field Name**: The display name of the field.

            * **Description**: The explanation of the field.

            * **Field Type**: Options include **String**, **Number**, **Boolean**, **Expression**, **Enum**.

            * **Advanced configuration**: Options include **Required**, **Unique**, **Editable**.

               On the right side of the column names for **Third Party Fields** and **SealSuite** **field**, click the settings icon to manage custom attribute uniformly (including add, edit, and delete operations).

               <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82925a9b58dd444ebae8accf7fe6a6c4~tplv-goo7wpa0wc-image.image) </span>

7. In the **Import Mode** area, select the import mode and click **Complete configuration**.

   When LDAP data changes, SealSuite provides you with the following methods to import data, including \*\*Manual sync \*\*and **Automatic sync**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Real\-time sync</strong> is only supported by Lark, DingTalk, and WeCom.   </div>
   

   
   |**Import method** |**Description** |**Strategy** |
   |---|---|---|
   |**Manual sync** |Once the data source is configured, the data import process is manually initiated by the admin. Suitable for corporate administrators to configure, and when they do not want to execute the import task immediately, they can manually import it after debugging preparations are complete. |Manual full import |
   |**Automatic sync** |Specify the time to import the third\-party data source. It is suitable for scenarios where the company needs to complete data imports at a fixed time. |Scheduled full import |
   

   * **Manual sync**: Select **Manual sync**, and then manually start importing the organizational structure data from the directory sync list.

   * **Automatic sync**: Select **Automatic sync**, and choose the import mode, and enable settings for importing organizational structure every few minutes or hours, or set at a fixed time daily.

8. In the **Directory Synchronization** tab, find the added data source, and turn on the enable switch.

   After turning on the enable switch, the directory synchronization configuration takes effect, and data will be synchronized according to the set synchronization rule thereafter.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the synchronization method is set to <strong>Manual sync</strong>, after the enable switch is turned on, you can manually click <strong>Start syncing</strong> as needed.   </div>
   

   Besides, click on **Google LDAP Directory Synchronization** to support viewing the following information:

   * **Configuration** tab: View **Basic configuration**, **Synchronization mechanism**, and **Sync Scope** information.

   * **Processing History** tab: View Synchronization History. You can refine your search of the Processing History by applying these three filters.

      In the **Action** column of sync data details, click **Details** to view the comparison of the information synchronized upstream to the SealSuite data source. Comparing data before and after synchronization can assist in conducting audit logs or troubleshooting user data issues.

      
      |**Filters** |**Description** |
      |---|---|
      |**Change action** |Only supports a single selection:<br><br><br>* **All**: Includes synchronization tasks of all change actions.<br><br>* **Create**: Represents the creation of a new synchronization task.<br><br>* **Update**: Represents the updating of an existing synchronization task.<br><br>* **Delete**: Represents the deletion of data in SealSuite when data is deleted from the upstream data source. |
      |**Sync status** |Only supports a single selection:<br><br><br>* **All**: Includes synchronization tasks of all sync statuses.<br><br>* **Success**: Represents a successfully completed synchronization task.<br><br>* **Fail**: Represents a synchronization task that failed.<br><br>* **Ignore**: Represents a situation where it is not stored for various reasons, such as when a full synchronization task finds that an existing real\-time task has stored new data, SealSuite chooses to ignore the data and not store it. |
      |**Search department/employee names** |Filter based on the department or employee names included in the sync data. |
      


<span id="e628ab72"></span>
# Log in to the SealSuite Admin Console to set up a third\-party login


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation bar, select **Identity** \> **Account Setup**.

3. Click the **Third\-Party Login** tab, and then click **Add Login Source** at the top right corner.

4. In the **Select Login Source** dialog box, click on the **Google Secure LDAP** card.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In a corporate organization, you can only add one LDAP authentication source. If you have previously added LDAP as an authentication source, you cannot add Google LDAP as an authentication source, and vice versa.   </div>
   

5. To set up the parameters, follow the prompts on the interface. Key parameters are explained below. Afteryou have completed the configuration, click **Confirm**.

   
   |**Module** |**Configuration Item** |**Required** |**Description** |
   |---|---|---|---|
   |**General** |**Login icon** |Yes |The identity source icon displayed on the login interface button. Click **Upload** to upload a custom display icon. |
   ||**Login abbreviation (Chinese)**  |Yes |The name displayed below the button on the login interface, such as Feishu Quick Login, click the **Example** below the input field to see a preview of how it will appear. |
   ||**Login abbreviation (English)**  |Yes |The name displayed under the button on the login interface. |
   ||**Unique identifier** |Not involved |The unique identifier for the login source, designed to differentiate logins across various tenants for authentication purposes, is composed of lowercase letters, numbers, and hyphens, with a maximum length of 32 characters. This identifier is provided by default within SealSuite and cannot be altered by the user. |
   ||**Unit** |Yes |Please select the unit applicable for this authentication source. Once configured, the employees of this unit can authenticate using this login method. |
   ||**Description** |No |Description for the authentication source, intended solely for internal Admin Console use and not visible to clients, must be concise and within a 40\-character limit. |
   ||**Login page** |Yes |Please select the appropriate verification method for the SealSuite client type. By default, the SealSuite **Mobile**, **Desktop** or **Web Portal** can all use this verification method. |
   |**LDAP/AD Authentication Configuration** |**Server Host** |Yes |Server address hosting the LDAP. It is recommended to follow the secure Lightweight Directory Access Protocol LDAPS, address format: `ldaps://<host>:<post>`. Example value: `ldaps://ldap.google.com:636`.<br><br><br>* `<host>` indicates the server domain name or IP address.<br><br>* `<post>` refers to the port number. The default protocol for LDAP is 389, and for LDAPS it is 636. |
   ||**Base DN** |Yes |Enter the saved Lark app credentials **App Secret**. You can obtain the App Secret on the **App Details** page of the **Credentials and Basic Information** on the Feishu Open Platform. |
   ||**Administrator DN** |Yes |Specifies a user who can connect to the LDAP server and has administrative rights. Example value: `cn=admin, dc=feilian, dc=com`. |
   ||**Administrator Password** |Yes |**Administrator DN** and associated password information. |
   ||**User ID** |Yes |The unique identifier for each user instance in LDAP. Example values are as follows:<br><br><br>* OpenLDAP: uid or dn<br><br>* AD domain: sAMAccountName |
   ||**User Object Class** |Yes |user object (objectclass). Example values are as follows:<br><br><br>* OpenLDAP: inetOrgPerson<br><br>* LDAP\-based AD domain: User or organizationalPerson |
   ||**SSL certificate file** |Yes |Click **Upload file** below to upload the certificate file, which is in PEM (Privacy Enhanced Mail) text format. The format description is as follows:<br><br><br>* Beginning: "\-\-\-\-\-BEGIN \*\*\*\-\-\-\-\-", example value: "\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-".<br><br>* Midsection: The content is encoded using Base64, and the file is designated with a .crt suffix.<br><br>* End :“\-\-\-\-\- END \*\*\*\-\-\-\-\-”, example value: "\-\-\-\-END CERTIFICATE \-\-\-\-\-”. |
   ||**SSL certificate key file** |Yes |Click **Upload file** below to upload certificate files. The key uses the PEM (Privacy Enhanced Mail) text format. The format description is as follows:<br><br><br>* Beginning: "\-\-\-\-\-BEGIN \*\*\*\-\-\-\-\-", example value: "\-\-\-\-\-BEGIN \* PRIVATE KEY\-\-\-\-\-".<br><br>* Mid\-section: The content is encoded using Base64, and the file is designated with a .key" suffix.<br><br>* Ending: "\-\-\-\-\-END \*\*\*\-\-\-\-\-", example value: "\-\-\-\-\-END \* PRIVATE KEY\-\-\-\-\-". |
   ||**User Termination Field Value** |No |If LDAP attributes indicate a user's termination, please enter them. Example values are as follows:<br><br><br>* OpenLDAP: employeeType<br><br>* AD Domain: UserAccountControl |
   ||**Termination Identifier** |No |Keyword indicating user's departure status. Example values are as follows:<br><br><br>* OpenLDAP: separated<br><br>* LDAP\-based AD Domain: 514 (decimal) |
   ||**Connectivity Test** |N/A |Click on the **Connectivity Test** to verify the network connection between the LDAP server and the SealSuite Admin Console. |
   |**Advanced Settings** |**Attribute Mapping** |Yes |Map employee details directly from the third\-party login authentication source to SealSuite's employee records, thereby establishing a link between third\-party and SealSuite users during the login process.<br><br><br>* Adjust the mapping relation: Left side refers to the user fields set within Feishu. The right side SealSuite field refers to the user fields that need to be mapped to SealSuite.<br><br>* Enable **Auto Update**: If this option is checked, it means that during login, if a user with matching credentials is found, their attributes will be updated with the information from the current login session.<br><br>* **Delete**: Delete the current mapping strategy.<br><br>* **Add**: If the default fields provided by SealSuite do not meet the mapping requirements, you can click **Add** to manually add field mapping relation.<br><br>* **Add Custom Attribute**: If the current field does not conform to the mapping strategy, you can click **Add Custom Attribute**. The explanation for the field is as follows:<br><br>   * **Field Key**: Defines the unique value of the field.<br><br>   * **Field Name**: Sets the display name of the field.<br><br>   * **Description**: Provides the explanation of the field. |
   ||**Uniquely ID Priority** |Yes |Set the priority of the matching identifiers by dragging and SealSuite will match the unique identifiers upstream in order of priority. If the current identifier does not meet the requirements, you can click **Add** to manually add the Identifier. |
   ||**When the login does not match the employee** |No |When corporate members log in to SealSuite and their profiles are not matched within the organizational structure, an auto\-creation service is triggered. Available options include:<br><br><br>* **Automatically create employee accounts**: When activated, if an employee is not matched at login, an employee account will be automatically created and associated with the designated department.<br><br>* **Do not create new account**: When activated, if an employee is not matched at login, an account will not be created. |
