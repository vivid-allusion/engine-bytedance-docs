---
title: "Feishu - User information import"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Importing_user_information"
---

You can use the import feature to flexibly synchronize user information (including custom attributes) into the system for subsequent identity identification, permission management, and resource access control.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic describes how to import employee information into ArkClaw. To manually add missing employee information or synchronize existing employee information from Feishu, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.</div>


<span id="Sjfaymb0"></span>
## Background information

User information in the user management module comes from two sources: 1. Administrators import user information in batches via the user management module. 2. When employees first log in and create a Claw instance, the system automatically records their information in the user management module.

<span id="lNf33ltx"></span>
## Prerequisites

When importing users, you can also import custom attributes. Before importing custom attributes, configure them in the ArkClaw console and ensure the attribute names in the table match those in the console. Otherwise, the corresponding attributes will not be imported. For detailed instructions on configuring custom attributes, see [Managing user attributes](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s).

<span id="36kvPToJ"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Employees need to be granted access permissions in the Feishu app before they can create and use ArkClaw. Otherwise, they do not have access to ArkClaw, even if you have imported the employee information.</div>


* <div data-tips="true" data-tips-type="warning">You may refer to steps <strong>7</strong>–<strong>10</strong> in <a href="https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication?TagIDs=2,522,502&lang=en#XT7ufHFt">Configuring Feishu application permissions</a> to grant Feishu app permissions to specific employees/organizations and publish an app version. Directly calling the Feishu Open Platform API to update the app's availability scope is not recommended, as it will affect data synchronization on the ArkClaw side.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. On the Users page, import user information.

   * **Full sync**: Have all employee information (including custom attributes) automatically synchronized from the organizational structure in Feishu to initialize the user list quickly. This reduces manual maintenance costs.

   * **Bulk upload**: Manually upload employee information (including custom attributes) from CSV/XLSX files. This is suitable for scenarios where Feishu has not yet been integrated or only a one\-off import of historical employee data is required.

   
   <Tabs>
   <Tab zoneid="6786SUBP" title="Synchronize all employee data">
   <TabTitle>Synchronize all employee data</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">During full or incremental user information synchronization from Feishu with a few clicks, the system supports deduplication using the phone number or the email address as the unique identifier. The unique identifier is derived from the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_users#tGbEb66U">unique identifier policy</a> in IdP authentication.</div>
   
   
   
   1. Click the "Full sync" button.
   
   2. In the pop\-up window, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63c193a480ce090a432f5bbb65b83c5e.png) </span> icon to copy the permission information and then go to the application to grant permissions. Click "Go to Feishu to authorize". For detailed authorization steps, see [Step 1: Configure the Feishu application and permissions](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication#tXfPdJrI).
   
   3. After permissions are granted, return to the dialog box and click "Refresh". After all required permissions are tagged as "Authorized", click "Sync data" in the dialog box.
   
   4. After confirming that the employee data is correctly synchronized, click "Confirm import" in the dialog box to complete the operation.
   
   5. (**Optional**) Synchronize incremental employee information. After full synchronization, if new or updated employee information exists in Feishu's organizational structure, run a synchronization task again to synchronize updates to ArkClaw.
   
      1. Click "Add employee".
   
      2. Click the "Full sync" button in the pop\-up window.
   
      3. The system will automatically synchronize employee data from Feishu. After synchronization is complete, verify that the results are correct, then click "Confirm import" in the dialog box to complete the operation.
   
   
   </Tab>
   <Tab zoneid="wAskXoaV" title="Batch upload employee data">
   <TabTitle>Batch upload employee data</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Description</div>
   
   
   <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Before importing user information in batches, ensure that you have prepared the user information file.</div>
   
   
   1. Click "Batch upload".
   
   2. On the "Batch add employee information" page, add employee information.
   
      1. Import data and configure mapping rules.
   
         1. Select "Unique identifier policy."
   
            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Select this option based on the primary identity information used within your enterprise. When you import employee information, the system automatically merges accounts that share the same mobile number or email address to avoid duplicate account creation. If you need to change this option later, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_users?lang=en">Configuring authentication methods</a> for more information.         </div>
            
   
            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3"><strong>Email addresses or mobile numbers cannot be used to log in to Claw instances</strong>.         </div>
            
   
         2. Upload the employee data file.
   
            1. Click "CSV/XLSX template" to download a standard file.
   
            2. Fill in the employee information as required by the template, then upload the file in the window.
   
               <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="4">warning            </div>
               
   
               <div data-tips="true" data-tips-type="warning" data-wrapper-indent="4">If you use the CSV template, mobile numbers in Column D must comply with the E.164 standard format. You can change the column format to "Text" before entering the mobile number.            </div>
               
   
   
   &nbsp;
   
         3. Click the "Next" button.
   
      2. Preview the data and handle exceptions.
   
         
         <Tabs>
         <Tab zoneid="GZ9S5rdLsh" title="Normal data">
         <TabTitle>Normal data</TabTitle>
         
         After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
         
         
         
         
         </Tab>
         <Tab zoneid="tNlP8Q4x5T" title="Abnormal data">
         <TabTitle>Abnormal data</TabTitle>
         
         If the user information in the imported file conflicts with existing user information in the system, update the user information.
         
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
         
         
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">If you do not handle conflicting data during import, the system will retain the existing user information and will not use the imported duplicate content.</div>
         
         
         1. Click the "Edit" button.
         
         2. Select the target data and click "Save".
         
         3. After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
         
         
         </Tab>
         </Tabs>
         
   
      3. View the import result and click "Complete". The employee information is uploaded.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If some user information fails to be imported, follow the on\-screen prompts to troubleshoot and then import it again.      </div>
         
   
   
   </Tab>
   </Tabs>
   


&nbsp;
