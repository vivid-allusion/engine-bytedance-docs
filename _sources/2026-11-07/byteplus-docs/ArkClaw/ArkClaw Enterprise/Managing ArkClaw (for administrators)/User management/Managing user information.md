---
title: "Managing user information"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information"
---

After users log in via the authentication method, administrators can view user information in the console or perform operations such as creating user groups and managing group assignments.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">ArkClaw Enterprise adopts the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_tde">Transparent Data Encryption (TDE)</a> solution to encrypt and store user information and organizational structure data, effectively mitigating the risk of data leakage during storage and safeguarding enterprise data security.</div>


<span id="Znwtgrea"></span>
## Managing users

<span id="2SwppanL"></span>
### Viewing users

After users successfully log in via the login link, you can centrally view user information, including user identifiers, accounts, authentication methods, and Claw instance IDs.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the Users page, view employee information in the "employee list".

   The list displays information about all employees who have logged in.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To view the dedicated credentials associated with a user, click the associated credential entry for the target user. You are redirected to the Credentials page, where you can view the dedicated credentials associated with the user. For information about deleting credentials associated with a user, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Credential_management#TnDSwzwp">Managing credentials</a>.   </div>
   

<span id="7Ppne53s"></span>
### Modify user information

Administrators can modify basic user information, including user name, email, phone number, associated group, associated department, and custom user attributes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After the email address or mobile number is modified, it may affect user authentication via standard login protocols .</div>


* <div data-tips="true" data-tips-type="warning">Modifying the name, group, or department does not affect user login, but it will affect the display name, scope of affiliation, and permissions of users.</div>


* <div data-tips="true" data-tips-type="warning">We recommend notifying the relevant users in advance before the operation and confirming that the changes are correct.</div>


* <div data-tips="true" data-tips-type="warning">When you switch authentication methods, the user information field "Email" or "Mobile number" serves as the matching criterion (unique identifier) for employees. After the switching is complete, the system automatically associates the original accounts and permissions based on the selected field, without needing to recreate the accounts. You can configure the unique identifier policy when <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_users?lang=en#tGbEb66U">switching authentication methods</a>. We recommend selecting the field that records the most complete employee information as the unique identifier.</div>


* <div data-tips="true" data-tips-type="warning">For operations related to custom user attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?TagIDs=2,522,512,502&lang=en#ReGX3H0s">Managing user attributes</a>.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click "Edit" in the Actions column that corresponds to the target user on the "Employees" tab. Modify user information based on the following table.

   
   |Parameter​ |Description |
   |---|---|
   |Name |The display name of the user in the system. |
   |Email |The email address associated with the user. If the user logs in with an email address, the user will need to use the new email address for login after the email address modification. Make sure that the user is informed of the change. |
   |Mobile number |The mobile number associated with the user.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>In platform hosting mode</strong>, users can use this mobile number and verification code to log in. After changing the mobile number, promptly notify the corresponding user. The user can only log in using the new mobile number subsequently.</div><br> |
   |Group |The permission group to which the user belongs. After group modification, the features and resources accessible to the user will take effect based on the permission settings of the new group.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a user does not belong to any group, they will appear under the "Ungrouped" category in the "Display by group" view.</div><br> |
   |Department |The department to which the user belongs. After modification, the department of the user will be updated synchronously. This affects department\-level statistics and management views.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a user does not belong to any department, they will appear under the "Unassigned" category in the "Display by group" view.</div><br> |
   

4. After confirming the information, click "Confirm".

5. In the pop\-up confirmation window, click "Confirm" to complete the operation.


<span id="wAIx9Wfy"></span>
### Update employee information

If employee details change or the system detects missing critical information (such as email or mobile number) in employee profiles, you can synchronize or supplement employee information by using the employee data update feature. This ensures that employee profiles remain ‌complete and ready‌ for future management and use.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Two methods are supported for employee data updates: automatic synchronization and manual update. Automatic synchronization applies only to Feishu/Lark authentication scenarios.</div>


* <div data-tips="true" data-tips-type="default">Custom attributes can be imported synchronously during user import or update. Before importing custom attributes, configure them in the ArkClaw console and ensure the attribute names in the table match those in the console. Otherwise, the corresponding attributes will not be imported. For detailed instructions on configuring custom attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s">Managing user attributes</a>.</div>


* <div data-tips="true" data-tips-type="default">When you switch authentication methods, the user information field "Email" or "Mobile number" serves as the matching criterion (unique identifier) for employees. After the switching is complete, the system automatically associates the original accounts and permissions based on the selected field, without needing to recreate the accounts. You can configure the unique identifier policy when <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_users?lang=en#tGbEb66U">switching authentication methods</a>. We recommend selecting the field that records the most complete employee information as the unique identifier.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Update employee data.

   
   <Tabs>
   <Tab zoneid="QFz0ixzS9h" title="General-purpose authentication scenarios">
   <TabTitle>General-purpose authentication scenarios</TabTitle>
   
   1. Click "Update employee". Alternatively, click "Update data" in the system prompt.
   
   2. Update employee data.
   
      
      <Tabs>
      <Tab zoneid="hXQ4A28IUp" title="Batch upload employee data">
      <TabTitle>Batch upload employee data</TabTitle>
      
      1. Click "Batch upload".
      
         2. On the "Batch update employee information" page, update employee information.
      
         1. Import data and configure mapping rules.
      
            1. Select "Unique identifier policy."
      
               <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
               
      
               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Select this option based on the primary identity information used within your enterprise. When you import employee information, the system will automatically merge accounts that share the same mobile number or email address.         </div>
               
      
               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3"><strong>The platform\-hosted authentication is the only method that allows employees to log in to Claw instances via mobile numbers and SMS verification codes</strong>. Before an employee logs in using a mobile number and an SMS verification code, the administrator needs to first enter the mobile number of the employee in the user information. <strong>Other authentication methods do not allow login to Claw instances via either mobile number or email address.</strong>         </div>
               
      
            2. Upload the employee data file.
      
               1. Click "CSV/XLSX template" to download a standard file.
      
               2. Fill in the employee information as required by the template, then upload the file in the window.
      
            3. Click the "Next" button.
      
         2. Preview the data and handle exceptions.
      
            * After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
            * If the user information in the imported file conflicts with existing user information in the system, update the user information.
      
               <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
               
      
               <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">If you do not handle conflicting data during import, the system will retain the existing user information and will not use the imported duplicate content.         </div>
               
      
               1. Click the "Edit" button.
      
               2. Select the target data and click "Save".
      
               3. After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
         3. View the import result and click "Complete". The employee information is uploaded.
      
            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
            
      
            <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If some user information fails to be imported, follow the on\-screen prompts to troubleshoot and then import it again.      </div>
            
      
      
      
      
      </Tab>
      <Tab zoneid="EUJcVIvGUO" title="Manually update employee data">
      <TabTitle>Manually update employee data</TabTitle>
      
      1. Click "Manual update".
      
      2. In the "Abnormal employee data" list, select the target employee to manually update their information.
      
         
         |Parameter​ |Description |
         |---|---|
         |Name |The display name of the user in the system. |
         |Email |The email address associated with the user. If the user logs in with an email address, the user will need to use the new email address for login after the email address modification. Make sure that the user is informed of the change. |
         |Mobile number |The mobile number associated with the user. If the user logs in with a mobile number, the user will need to use the new mobile number for login after the mobile number modification. Make sure that the user is informed of the change. |
         
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you do not need to retain the user with information anomalies, you can delete the user.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the user to be deleted has already been associated with ArkClaw instances, delete all their associated instances before deleting the user. For detailed steps of deleting instances, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Deleting_Claw_instances">Deleting Claw instances</a>.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Deleting a user is irreversible. The system will simultaneously disassociate the user from other resources. Proceed with caution.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the deletion, the user will be forcibly logged out in about 5 minutes and will no longer be able to access the system.   </div>
         
      
      
      </Tab>
      </Tabs>
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="aQc7R8vSRE" title="Feishu/Lark/Dingtalk authentication">
   <TabTitle>Feishu/Lark/Dingtalk authentication</TabTitle>
   
   1. Click "Update employee".
   
   2. Update employee data.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an employee has not yet logged in via Feishu/Lark (for example, the employee still uses the original login method after the enterprise switches authentication methods), the system cannot automatically synchronize the latest information of the employee from Feishu/Lark. To update the information of such employees (e.g., adding phone numbers or emails), refer to the last two methods in the following tabs.   </div>
      
   
      
      <Tabs>
      <Tab zoneid="uAJXHaMAej" title="Synchronize employee data from Feishu/Lark/DingTalk">
      <TabTitle>Synchronize employee data from Feishu/Lark/DingTalk</TabTitle>
      
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
      
      
      <div data-tips="true" data-tips-type="default">During incremental user information synchronization from Feishu, Lark, or DingTalk, the system supports deduplication using the phone number or the email address as the unique identifier. The unique identifier is derived from the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_users#tGbEb66U">unique identifier policy</a> in IdP authentication.</div>
      
      
      
      1. Click the "Full sync" button.
      
      2. In the pop\-up window, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span> icon to copy the permission information and then go to the application to grant permissions.
      
         * **Feishu**: Click "Go to Feishu to authorize". For detailed authorization steps, see [Step 1: Configure the Feishu application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication#tXfPdJrI).
      
         * **Lark**: Click "Go to Lark to authorize". For detailed authorization steps, see [Step 1: Configure the Lark application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication).
      
      3. After permissions are granted, go back to the dialog box to synchronize data.
      
         * **Feishu/Lark**: Click "Refresh". After all required permissions are tagged as "Authorized", click "Sync data" in the dialog box.
      
      4. The system will automatically synchronize employee data from Feishu, Lark, . When the synchronization is complete, click "Close" in the dialog box to finish the operation.
      
      
      </Tab>
      <Tab zoneid="NfWjG8G2jB" title="Batch upload employee data from other sources">
      <TabTitle>Batch upload employee data from other sources</TabTitle>
      
      **Prerequisites**
      
      When importing users, you can also import custom attributes. Before importing custom attributes, configure them in the ArkClaw console and ensure the attribute names in the table match those in the console. Otherwise, the corresponding attributes will not be imported. For detailed instructions on configuring custom attributes, see [Managing user attributes](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s).
      
      **Procedure**
      
      
      1. Click "Batch upload".
      
         2. On the "Batch update employee information" page, update employee information.
      
         1. Import data and configure mapping rules.
      
            1. Select "Unique identifier policy."
      
               <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
               
      
               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Select this option based on the primary identity information used within your enterprise. When you import employee information, the system will automatically merge accounts that share the same mobile number or email address.         </div>
               
      
               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3"><strong>Email addresses or mobile numbers cannot be used to log in to Claw instances</strong>.         </div>
               
      
            2. Upload the employee data file.
      
               1. Click "CSV/XLSX template" to download a standard file.
      
               2. Fill in the employee information as required by the template, then upload the file in the window.
      
            3. Click "Next".
      
         2. Preview the data and handle exceptions.
      
            * After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
            * If the user information in the imported file conflicts with existing user information in the system, update the user information.
      
               <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
               
      
               <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">If you do not handle conflicting data during import, the system will retain the existing user information and will not use the imported duplicate content.         </div>
               
      
               1. Click "Edit".
      
               2. Select the target data and click "Save".
      
               3. After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
         3. View the import result and click "Complete". The employee information is uploaded.
      
      
      </Tab>
      <Tab zoneid="w1PYVrsqJC" title="Manually update employee data from other sources">
      <TabTitle>Manually update employee data from other sources</TabTitle>
      
      1. Click "Manual update".
      
      2. In the "Abnormal employee data" list, select the target employee to manually update their information.
      
         
         |Parameter​ |Description |
         |---|---|
         |Name |The display name of the user in the system. |
         |Email |The email address associated with the user. If the user logs in with an email address, the user will need to use the new email address for login after the email address modification. Make sure that the user is informed of the change. |
         |Mobile number |The mobile number associated with the user. If the user logs in with a mobile number, the user will need to use the new mobile number for login after the mobile number modification. Make sure that the user is informed of the change. |
         
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you do not need to retain the user with information anomalies, you can delete the user.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the user to be deleted has already been associated with Claw instances, delete all their associated instances before deleting the user. For detailed steps for deleting instances, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Deleting_Claw_instances">Deleting Claw instances</a>.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Deleting a user is irreversible. The system will simultaneously disassociate the user from other resources. Proceed with caution.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the deletion, the user will be forcibly logged out in about 5 minutes and will no longer be able to access the system.   </div>
         
      
      
      </Tab>
      </Tabs>
      
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="OzbEntiG"></span>
### Delete user

When a user no longer needs to use ArkClaw, administrators can delete the user.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">If the user to be deleted has already been associated with ArkClaw instances, delete all their associated instances before deleting the user. For detailed steps for deleting instances, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Deleting_Claw_instances">Deleting Claw instances</a>.</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">Before deleting a user, make sure that relevant applications no longer rely on the credentials of the employee. After the user is deleted, the associated credentials generated when the employee completes personal authorization by using dedicated OAuth client credentials are also deleted and cannot be recovered.</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">Deleting a user is irreversible. The system will simultaneously disassociate the user from other resources. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">After the deletion, the user will be forcibly logged out in about 5 minutes and will no longer be able to access the system.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. In the employee list, delete one or more users.

   * **Delete a single user**: Click "···  **\>**  Delete user" in the Actions column that corresponds to the target user to delete the user.

   * **Delete multiple users**: Select multiple target users and then click "Batch delete" to delete multiple users in a batch.

4. Confirm that the user to be deleted is correct. Then, click "Delete" to complete the operation.

   <span id="ReGX3H0s"></span>
   ## Manage user attributes

   <span id="fyXjYwzi"></span>
   ### Create a new user attribute

   When the system's predefined fields cannot meet employee information management requirements, you can add custom user attributes to supplement information such as employee identity, position, or business tags. To synchronize custom attributes during user information import, complete the creation and mapping of these custom attributes in advance.

   1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

   2. In the left navigation pane, click "Organizations" \> "Users".

   3. Select the "User attributes" tab and click the "Create attribute" button.

4. Refer to the following table to configure the parameters.

   
   |Parameters |Description |
   |---|---|
   |**Basic information** ||
   |Term |Enter the display name of the custom attribute in the system for administrators to identify and maintain this field. |
   |Type |Select based on the actual data type.<br><br><br>* **String**: Used to enter a single text value. Applicable to fixed text information such as employee ID or office location.<br><br>* **String array**: Used to enter multiple text values. Applicable to information that can contain multiple values, such as skills and responsible business areas.<br><br>* **Number**: Used to enter numerical values. Applicable to information that needs to be represented by numbers, such as length of service or job grade.<br><br>* **Boolean**: Used to indicate two states: yes or no. Applicable to information that presents a positive or negative state, such as whether an employee is an administrator or whether something is enabled.<br><br>* **Date/Time**: Used to enter a specific date or time. Applicable to time information, such as onboard date or regularization date. |
   |Minimum/Maximum |Minimum/Maximum values of the attribute.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value of the mapped field must fall within the value range set for the attribute. Otherwise, the field will not be updated.</div><br><br><br><div data-tips="true" data-tips-type="warning">For example, when the value of the mapped field is 4 and the value range of the attribute is set to [1, 5], the update can proceed normally. If the value range is set to [2, 3] or [6, 20], then 4 falls outside the range, and the field will not be updated.</div><br> |
   |Update types |Set the maintenance method for attribute values.<br><br><br>* When "Manual update" is selected, attribute values are manually maintained by administrators.<br><br>* When "Automatic update" is selected, the system can automatically update attribute information via attribute mapping when users log in to the employee\-side console via SSO. |
   |**Attribute mapping** ||
   |Authentication protocol |The current authentication protocol is automatically specified by the system and cannot be modified. |
   |Mapping fields |Enter the field corresponding to the current user attribute. When a user logs in to the employee\-side console via SSO, the system will read the value of this field and automatically synchronize it to this user attribute. |
   

5. After confirming that the above information is correctly filled in, click the "Confirm" button to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After user attributes are configured, click the icon in the "Employee list" tab and click <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_834a3b9a592dc3a482e35c3269601d41.png" width="23px" /> icon, then select whether to enable custom field display as needed.   </div>
   

&nbsp;

<span id="4FtNSitH"></span>
### Edit user attributes

When you need to adjust the attribute name or minimum/maximum values, or update types or mapping fields, you can edit an existing user attribute.

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

   2. In the left navigation pane, click "Organizations" \> "Users".

   3. Select the "User attributes" tab and click the "Edit" button in the Actions column of the target attribute.

4. After modifying the attribute parameters as needed, click the "Confirm" button to complete the operation.

&nbsp;

   <span id="PuQvUG3y"></span>
   ### Delete user attributes

   When a user attribute is no longer in use, administrators can delete it to reduce the interference of invalid fields in daily management.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">Deleting a user attribute is an irreversible operation. The system will also delete the mapping relationships associated with the attribute. Proceed with caution.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

   3. Select the "User attribute" tab.

   4. On the attribute list page, find the target attribute and click "Delete" in the Actions column to delete a single attribute.

5. After confirming that the attribute to be deleted is correct, click the "Delete" button to complete the operation.

   <span id="y6R20v3x"></span>
   ## Manage user groups

   <span id="L6gAnvfJ"></span>
   ### Create a user group

By organizing users into groups, administrators enable role\-based, consistent permission management at scale. Each user can belong to only one user group.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the upper\-right corner of the "Users" page, you can switch views:</div>



* <div data-tips="true" data-tips-type="default"><strong>List view</strong>: The default view, which displays all logged\-in or imported employees in a tiled layout. This view is suitable for searching for specific users, viewing personal information (such as login counts and recent activities), and editing the group affiliations of individual users.</div>


* <div data-tips="true" data-tips-type="default"><strong>Group view</strong>: A multi\-pane layout organized by permission group. User groups (for example, System administrators and Developers) are displayed on the left, and the member list of the selected group is displayed on the right. This view is suitable for managing users in batches by role.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Select the "Display by group" tab, and click the "Create group" icon.

4. Enter a user group name and description and click "Create".

5. Select the users to add to the user group and click "Confirm".


<span id="9JCEHRGP"></span>
### Edit user group

Administrators can change the user groups to which users belong by managing user groups.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Manage user groups on the "Employees" tab of the "Users" page.

   * **Change user group**: Click "Edit" in the "Actions" column to move a user to another group.

   * **Add user to group**: In the "Display by group" view of the employee list, click the "Add" icon next to an existing group to add a user to it.

   * **Remove ** **users from the current group**:

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When a user is removed from a group, they will automatically be moved to the "Ungrouped" category. You can view and manage ungrouped users in this category.      </div>
      

      * **Remove a single user**: In the "Display by group" view of the employee list, click "...  **\>**  Remove from group" in the Actions column that corresponds to a user to remove the user from the current group.

      * **Remove employees in batches**: In the "Display by group" view of the employee list, select multiple target users, and click "Batch remove" to remove them from the current group.
