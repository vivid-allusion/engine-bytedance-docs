---
title: "Other authentication methods - User information import"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Other_authentication_methods_-_User_information_import"
---

You can use the import feature to flexibly synchronize user information into the system for subsequent identity identification, permission management, and resource access control.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic describes how to import employee information into ArkClaw. To manually supplement missing employee information, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.</div>


<span id="GTeCAHjo"></span>
## Background information

User information in the user management module comes from two sources: 1. Administrators import user information in batches via the user management module. 2. When employees first log in and create a Claw instance, the system automatically records their information in the user management module.

<span id="xikSxmNK"></span>
## Prerequisites


* Before importing user information in batches, ensure that you have prepared the user information file.

* Custom attributes can be imported synchronously during user import. Before importing custom attributes, configure them in the ArkClaw console and ensure the attribute names in the table match those in the console. Otherwise, the corresponding attributes will not be imported. For detailed instructions on configuring custom attributes, see [Managing user attributes](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s).


<span id="bSpnn9Fb"></span>
## Procedure

An administrator can upload a CSV file containing information about multiple users to import user data in batches to ArkClaw Enterprise for user and permission management by group.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Organizations" \> "Users".

3. Click "Add employee".

   4. On the "Batch add employee information" page, add employee information.

   1. Import data and configure mapping rules.

      1. Select "Unique identifier policy."

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Select this option based on the primary identity information used within your enterprise. When you import employee information, the system automatically merges accounts that share the same mobile number or email address to avoid duplicate account creation. If you need to change this option later, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_users?lang=en">Configuring authentication methods</a> for more information.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3"><strong>Email addresses or mobile numbers cannot be used to log in to Claw instances</strong>.         </div>
         

      2. Upload the employee data file.

         1. Click "CSV/XLSX template" to download a standard file.

         2. Fill in the employee information as required by the template, then upload the file in the window.

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">Each import supports up to 500 rows of data. If the number of employees exceeds 500, upload employee information in batches, with a maximum of 500 rows per batch.            </div>
            

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">When importing users in batch, custom attributes can be imported simultaneously. Before importing custom attributes, configure them in the ArkClaw console and ensure the attribute names in the table match those in the console. Otherwise, the corresponding attributes will not be imported. For detailed instructions on configuring custom attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s">Managing user attributes</a>.            </div>
            

      3. Click the "Next" button.

   2. Preview the data and handle exceptions.

      
      <Tabs>
      <Tab zoneid="SHwgLg7X" title="Normal data">
      <TabTitle>Normal data</TabTitle>
      
      After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
      
      </Tab>
      <Tab zoneid="NP6ZSy0z" title="Abnormal data">
      <TabTitle>Abnormal data</TabTitle>
      
      If the user information in the imported file conflicts with existing user information in the system, update the user information.
      
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
      
      
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">If you do not handle duplicate data during import, the system will retain the existing user information and will not use the imported duplicate content.</div>
      
      
      1. Click the "Edit" button.
      
      2. Select the target data and click "Save".
      
      3. After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
      
      </Tab>
      </Tabs>
      

   3. View the import result and click "Complete". The employee information is uploaded.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the import is complete, users need to log in using the login link provided by the administrator. The system will log them in using the authentication method configured by the IdP.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If some user information fails to be imported, follow the on\-screen prompts to troubleshoot and then import it again.      </div>
