---
title: "Managing department information"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments"
---

The department management feature allows you to flexibly configure multi\-level business departments and centrally manage employee affiliations.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">ArkClaw Enterprise adopts the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_tde">TDE (Transparent Data Encryption) solution</a> to encrypt and store user information and organizational structure data, effectively mitigating the risk of data leakage during storage and safeguarding enterprise data security.</div>


<span id="L8AF5IQC"></span>
## Concept

A department is a logical unit within the organizational structure of enterprises. You can manage employees hierarchically by business line, function, project, region, or another attribute. Departments serve both as a designation for employee affiliation and a critical basis for configuring role permissions, isolating business data, and routing approval workflows.

<span id="xC5Akjth"></span>
## Limits

A department can have up to 25 sub\-departments.

<span id="RThcGR6H"></span>
## Create departments

You can create departments based on business requirements to achieve hierarchical management of personnel, permissions, tasks, and more.

<span id="2fdHEP6N"></span>
### Prerequisites

To **add employees to a department while creating the department**, ensure that you have imported employee information before creating the department. The import method varies with the [space authentication method](https://docs.byteplus.com/en/docs/ArkClaw/Managing_users). For detailed steps, see [Importing user information](https://docs.byteplus.com/en/docs/ArkClaw/Importing_user_information-). Otherwise, ignore this prerequisite.

<span id="52a4tn80"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the "Departments" tab, click "Create department".

4. Refer to the following table to configure the parameters.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Department name |Enter the name of the department. |R&D Department 2 |
   |Parent department |Set this field based on your actual organizational hierarchy.<br><br><br>* If you **create a first\-level department**, you do not need to select a parent department. Leave this field blank.<br><br>* If you **create a sub\-department**, select the desired parent department from the drop\-down list to ensure a well\-designed organizational hierarchy.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also quickly <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments#X6SzpwVR">create a sub\-department</a> directly under the target parent department.   </div><br>   <br><br> |\- |
   |Department description |Provide a brief function description or remarks of the department. |Responsible for the core C\-end business line |
   |Department manager |Search for the employee by name. This employee may subsequently serve as a key node in the approval flow. |Tom |
   |External UID |Enter the external unique ID (UID) that identifies the department. This ID serves as the sole credential for synchronizing and integrating department data between this system and external systems (such as HR, OA, and ERP). As a stable identifier for departments, it effectively prevents the loss of associated data caused by department name changes.<br><br><br>* If the department has already been assigned a code (such as HR, OA, or ERP), we recommend directly using that code as the external UID.<br><br>* If no coding system exists, you can define a UID (for example, dept_hr, team_001). |HR001 |
   

5. Confirm the above information. If nothing is wrong, click "Next step".

6. Select whether to add (assign) employees to the department immediately.

   * If you want to **add employees** immediately, select the target employees and click "Confirm".

   * If you **do not add employees** immediately, click "Cancel".

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you do not assign employees at this step, you can do it later by using the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments#N6VAKTvd">Add employee</a> feature in the department list.      </div>
      

<span id="X6SzpwVR"></span>
## Create sub\-departments

You can create sub\-departments under the current department to achieve hierarchical management of the organizational structure and granular permission assignment.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click the "Departments" tab.

4. In the department list, find the target department and click "Add sub\-department".

5. Configure the relevant parameters. For parameter descriptions, see [Creating departments](https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments#RThcGR6H).


<span id="N6VAKTvd"></span>
## Import departments

If you need to create or synchronize department data in batches, you can quickly maintain department information by importing departments.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click the "Departments" tab.

4. Import department information.

   
   <Tabs>
   <Tab zoneid="q7C5DiHNVD" title="General-purpose authentication scenarios">
   <TabTitle>General-purpose authentication scenarios</TabTitle>
   
   1. On the Departments page, click "Import departments".
   
   2. On the “Import department data” page, click “Download table template”.
   
   3. Fill in the department information in the template, save the information, and then upload the file.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Departments for which “delete” is displayed in the “Action” column will be deleted. This operation is irreversible. Proceed with caution.</strong>   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the file is uploaded, you can preview the locally parsed data to check whether the added or deleted content is correct.   </div>
      
   
   4. Click “Next” to go to the data preview page.
   
   5. View differences between the data before and after this import. After confirming the import result is correct, click “Import” to complete the operation.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>If an imported department ID matches an existing department ID, the existing department structure will be automatically overwritten after this import. Carefully confirm the items to be updated and deleted.</strong>   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The preview page displays the complete department tree by default. After “Only display changes” is enabled, only the department nodes changed by this import are displayed. This helps you quickly check added, modified, and deleted items.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If some data fails to be imported, you can view the specific reasons in the “Failure details” section (for example, a department to be deleted is not found), correct the data file, and then import the data.   </div>
      
   
   
   </Tab>
   <Tab zoneid="Ermt2a0KaK" title="Feishu/Lark/Dingtalk authentication">
   <TabTitle>Feishu/Lark/Dingtalk authentication</TabTitle>
   
   In Feishu/Lark authentication scenarios, you can maintain department information in two ways: (1) Use "Full sync" to pull the organization structure from Feishu. (2) Use file import to batch upload department information.
   
   
   1. On the Departments page, click "Import departments".
   
   2. Import department information.
   
      
      <Tabs>
      <Tab zoneid="qFxW9or6t1" title="Synchronize department information from Feishu/Lark/Dingtalk.">
      <TabTitle>Synchronize department information from Feishu/Lark/Dingtalk.</TabTitle>
      
      **Prerequisites**
      
      
      * You need to grant permissions to the **target departments** in the Feishu/Lark/DingTalk app so that the system can fully synchronize department information within the app's availability scope.
      
      * **Feishu**: You may refer to steps **7**–**10** in [Configuring Feishu application permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication?TagIDs=2,522,502&lang=en#XT7ufHFt) to grant Feishu application permissions to specific departments and publish the application version. Directly calling the Feishu Open Platform API to update the availability scope is not recommended, as it will affect data synchronization on the ArkClaw side.
      
      * **Lark**: You may refer to steps **7**–**10** in [Configuring Lark application permissions](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication#C1WQ9cGJ) to grant Lark application permissions to specific departments and publish the application version. Directly calling the Lark Open Platform API to update the availability scope is not recommended, as it will affect data synchronization on the ArkClaw side.
      
      
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
      
      
      <div data-tips="true" data-tips-type="default">Perform this operation in the interface for your selected authentication method. The following screenshots demonstrate the steps under Feishu authentication.</div>
      
      
      **Procedure**
      
      
      1. Click the "Full sync" button.
      
      2. In the pop\-up window, go to the application to grant permissions.
      
         * **Feishu**: Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information, then click "Go to Feishu to authorize". For detailed authorization steps, see Step 1: [Configure the Feishu application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication#OCJTSobq)
      
         * **Lark**: Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information, then click "Go to Lark to authorize". For detailed authorization steps, see [Step 1: Configure the Lark application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication).
      
      3. After permissions are granted, go back to the dialog box to synchronize data.
      
         * **Feishu/Lark**: Click "Refresh". After all required permissions are tagged as "Authorized", click "Sync data" in the dialog box.
      
            <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
            
      
            <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you first import department information using an XLSX file and then switch to Feishu/Lark synchronization authentication, ensure that the authorization status for "Retrieve department organizational structure information" is "Authorized". Otherwise, the system will be unable to retrieve the top\-level parent department ID, and department information import will fail.      </div>
            
      
      4. The system will automatically synchronize department data from Feishu/Lark. After confirming that the synchronized information is correct, click "Confirm" in the dialog box to complete the operation.
      
      5. (Optional) Enable incremental synchronization.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If it is enabled, when a user logs in to the employee\-side console via Feishu/Lark SSO, the system will automatically synchronize the user's latest basic information and associated department information. This can continuously reflect personnel and department changes on the Feishu/Lark side and reduce the overhead of manual maintenance for administrators.   </div>
         
      
         1. Click "Incremental sync".
      
         2. Complete Feishu/Lark/DingTalk **user identity** authorization.
      
            1. In the pop\-up window, go to the application to grant permissions.
      
               * **Feishu**: Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information and then click "Feishu page" to go to the Feishu platform and complete the authorization there. For detailed authorization steps, see [Step 1: Configure the Feishu application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication#OCJTSobq).
      
               * **Lark**: Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information and then click "Lark page" to go to the Lark platform and complete the authorization there. For detailed authorization steps, see [Step 1: Configure the Lark application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication).
      
            2. After authorization is complete, go back to the dialog box and click "Authorization completed manually".
      
      
      </Tab>
      <Tab zoneid="dr028C9Twt" title="Manually upload department information in batches">
      <TabTitle>Manually upload department information in batches</TabTitle>
      
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
      
      
      <div data-tips="true" data-tips-type="default">Perform this operation in the interface for your selected authentication method. The following screenshots demonstrate the steps under Feishu authentication.</div>
      
      
      
      1. Click "Batch upload".
      
      2. On the “Import department data” page, click “Download table template”.
      
      3. Fill in the department information in the template, save the information, and then upload the file.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Departments for which “delete” is displayed in the “Action” column will be deleted. This operation is irreversible. Proceed with caution.</strong>   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the file is uploaded, you can preview the locally parsed data to check whether the added or deleted content is correct.   </div>
         
      
      4. Click “Next” to go to the data preview page.
      
      5. View differences between the data before and after this import. After confirming the import result is correct, click “Import” to complete the operation.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>If an imported department ID matches an existing department ID, the existing department structure will be automatically overwritten after this import. Carefully confirm the items to be updated and deleted.</strong>   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The preview page displays the complete department tree by default. After “Only display changes” is enabled, only the department nodes changed by this import are displayed. This helps you quickly check added, modified, and deleted items.   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If some data fails to be imported, you can view the specific reasons in the “Failure details” section (for example, a department to be deleted is not found), correct the data file, and then import the data.   </div>
         
      
      6. (Optional) Enable incremental synchronization.
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If it is enabled, when a user logs in to the employee\-side console via Feishu/Lark SSO, the system will automatically synchronize the user's latest basic information and associated department information. This can continuously reflect personnel and department changes on the Feishu/Lark side and reduce the overhead of manual maintenance for administrators.   </div>
         
      
         1. Click "Incremental sync".
      
         2. Complete Feishu/Lark/DingTalk **user identity** authorization.
      
            1. In the pop\-up window, go to the application to grant permissions.
      
               * **Feishu**: Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information and then click "Feishu page" to go to the Feishu platform and complete the authorization there. For detailed authorization steps, see [Step 1: Configure the Feishu application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication#OCJTSobq).
      
               * **Lark**: Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span>" to copy the permission information and then click "Lark page" to go to the Lark platform and complete the authorization there. For detailed authorization steps, see [Step 1: Configure the Lark application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication).
      
            2. After authorization is complete, go back to the dialog box and click "Authorization completed manually".
      
      
      </Tab>
      </Tabs>
      
   
   
   
   
   
   </Tab>
   </Tabs>
   


&nbsp;

<span id="gohTdGV9"></span>
## Add employees

After you create a department, you can assign employee accounts in the system to the department for unified management operations, such as authorization and data isolation.

<span id="nc0HS45S"></span>
### Prerequisites

You have [imported user information](https://docs.byteplus.com/en/docs/ArkClaw/Importing_user_information-).

<span id="OeOInLgx"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click the "Departments" tab.

4. In the department list, find the target department and click "Add employee".

5. Select the employees to add and click "Confirm".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If a user does not belong to any department, they will be placed in the "Unassigned" group.   </div>
   

<span id="rS3NrVaO"></span>
### Delete departments

Before deleting a department, delete all its sub\-departments first.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Note the following information when you delete a department:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Department data cannot be recovered.</strong> All basic information and historical data of this department will be permanently deleted.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Employee affiliations are automatically removed.</strong> Employees originally belonging to this department will lose their affiliation with this department.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click the "Departments" tab.

4. In the department list page, find the target department and select "···"  **\>**  "Delete department".

5. To confirm the deletion, click "Delete".


<span id="1VM7RPDj"></span>
## Display custom fields in the department list

The system allows administrators to customize visible data fields in the department list to accommodate different viewing preferences and screen width constraints. You can choose which data columns to show or hide in the list.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click the "Departments" tab.

4. In the upper\-right corner of the "Departments" page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_834a3b9a592dc3a482e35c3269601d41.png) </span>.

5. Select the target fields to display.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The "Name/ID" and "Actions" fields are displayed by default and cannot be hidden.   </div>
   

   * **Check a field (to display it)** : Select the checkbox to the left of the field (marked as ✓), and this field will appear as a column in the list below (for example, department relationship and sub\-department quantity).

   * **Deselect a field (to hide it)** : Deselect the checkbox, and this field will be hidden from the list for a cleaner view.

   * **Restore default view**: If adjusting numerous fields causes table layout issues, or if you wish to return to the initial view, click "Restore default" to reset header fields to the default configuration.
