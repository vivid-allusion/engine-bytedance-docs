---
title: "Platform-hosted - user information import"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Feishu_-_User_information_import"
---

You can use the import feature to flexibly synchronize user information into the system for subsequent identity identification, permission management, and resource access control.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic describes how to import employee information into ArkClaw. To manually add missing employee information or synchronize existing employee information from Feishu, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=en#wAIx9Wfy">Updating user information</a>.</div>


<span id="jP7o4guz"></span>
## Background information

User information in the user management module comes from two sources: 1. Administrators import user information in batches via the user management module. 2. When employees first log in and create an ArkClaw instance, the system automatically records their information in the user management module.

<span id="XqS9stNK"></span>
## Prerequisites

Before importing user information in batches, prepare the user information file in advance.

<span id="aQTQ8ecf"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Organizations \> Users".

3. On the Users page, click "Add employee".

4. On the "Batch add employee information" page, add employee information.

   1. Import data and configure mapping rules.

      1. Select "Unique identifier policy."

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Select this option based on the primary identity information used within your enterprise. When you import employee information, the system will automatically merge accounts that share the same mobile number or email address.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3"><strong>Email addresses cannot be used to log in to Claw instances</strong>.         </div>
         

      2. Upload the employee data file.

         1. Click "CSV/XLSX template" to download a standard file.

         2. Fill in the employee information as required by the template, then upload the file in the window.

            <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="4">warning            </div>
            

            * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="4">The employee usernames and passwords entered here will serve as the login credentials for employees when using ArkClaw. Please keep them secure.            </div>
            

            * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="4">When importing users in batch, custom attributes can be imported simultaneously. Before importing, complete the custom attribute configuration in the ArkClaw console and ensure the attribute names in the table are consistent with those in the console. Otherwise, the corresponding attributes will not be imported. For detailed instructions on configuring custom attributes, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information#ReGX3H0s">Managing user attributes</a>.            </div>
            

            * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="4">If you use the CSV template, mobile numbers in Column E must comply with the E.164 standard format. You can change the column format to "Text" before entering the mobile number.            </div>
            

            * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="4">Employees can log in to Claw instances via SMS verification codes or reset their login passwords on their own. We recommend ensuring every employee is configured with a phone number to facilitate usage.            </div>
            

      3. Click the "Next" button.

   2. Preview the data and handle exceptions.

      
      <Tabs>
      <Tab zoneid="cmMee3Uq" title="Normal data">
      <TabTitle>Normal data</TabTitle>
      
      After confirming that the user information in the imported file does not conflict with existing user information in the system, click "Start import".
      
      
      </Tab>
      <Tab zoneid="4SfsGDLH" title="Abnormal data">
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
