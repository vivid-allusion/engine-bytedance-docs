---
title: "How to Bind Lark Accounts and Batch Create Users"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/How_to_Bind_Lark_Accounts_and_Batch_Create_Users"
---

<span id="ddaaf7db"></span>
# Overview

After integrating the Lark application, the account binding feature is now supported. To bind users in DataAgent (hereinafter referred to as DataAgent) with Lark accounts, go to System Management \> User Management, and bind users individually or in batches as needed. The following sections describe the specific procedures for binding a single user and for batch binding.

<span id="70364ab5"></span>
# Bind accounts

<span id="7daf63e1"></span>
## Bind a single Lark account


1. After entering System Management \-\> User Management in the DataAgent product, select the corresponding user to bind their Lark account.

2. Click the Account Binding button in the action column for the corresponding user in the user list to start the account binding process.

3. In the account binding pop\-up window, select the matching method: **automatic matching or manual matching**.

* After selecting **automatic matching** as the matching method, select the Lark account information (IM number, mobile number, or email) and the DataAgent account information (username, mobile number, or email) to match. Choose the matching fields according to your actual situation.

* After selecting **manual matching** as the matching method, manually search for the user's name in Lark to perform manual matching. If the specified user is not found, click the refresh function on the right to refresh.


<span id="2c6bf5b2"></span>
## Batch bind Lark accounts

Batch creating accounts through Lark can address the following issues: ensuring all users log in to DataAgent only through Lark accounts, handling a large number of accounts under the current enterprise organization by batch creating and associating DataAgent accounts, and dynamically adjusting account addition and deletion based on user onboarding and offboarding information. The specific steps are as follows:

<span id="c125d29a"></span>
### Cloud Identity Center configuration

To allow users to log in to BytePlus directly using their enterprise Lark accounts, **enterprise administrators** need to configure this in the **Cloud Identity Center of BytePlus**.


1. Enable Cloud Identity Center: After enabling the enterprise organization, the administrator goes to the Cloud Identity Center page in BytePlus and clicks to enable the service. See [Enable Cloud Identity Center](https://www.volcengine.com/docs/7165/198141) for details.

2. User synchronization settings: The administrator goes to the User Synchronization Settings page, clicks the **Configure Identity Source** button, selects Larkrk; after downloading the BytePlus application, enables the application and scans the code to bind the Larkrk tenant. See [User Synchronization Settings](https://www.volcengine.com/docs/7165/198129) for details.

3. Configure user access authorization: Use an IAM sub\-user account with permissions under the enterprise organization administrator account to log in to the BytePlus console, go to the [Multi-account Access Management](https://console.volcengine.com/cloudidentity/region:cn-beijing/multiAccountAccess/) page, select the accounts to be authorized, and then click **Configure User SSO** at the bottom of the list. See [Configure User Access Authorization](https://www.volcengine.com/docs/7165/198132) for details.


After completing the above steps, enterprise employees can log in to BytePlus using their Lark accounts.

<span id="6948657e"></span>
### Add users in DataAgent


1. Open the BytePlus Intelligent DataAgent workspace, log in with the administrator account, and click the settings icon in the upper right corner to enter system management.

2. In the side navigation, click System Settings \> Security Settings \> System Control \> License Control Method. You can set the license control method to "Automatically join when system users log in to this product". In this case, all accounts authorized in Cloud Identity Center can directly log in to DataAgent using their Lark accounts.


If you select "System administrator configures license list", the administrator needs to perform secondary authorization. After entering system management, the administrator clicks User Management, then clicks Add User in the upper right corner to add users. After successful addition, these users can log in to DataAgent.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8a9ff117cd341f2b3afc909eeaaa5e1~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="9fe801fa"></span>
### Grant project permissions

In addition to granting users access to the DataAgent platform, to access resources within a specific project, the administrator needs to grant the user edit or view permissions for the project.


1. Create a user group: Click Project Center \> User Group Management, then click the plus sign in the user group list to create a new user group. After jumping to the user group details page, click Add User and select the users to add to the group.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bfc3c6e01b046159b1686b04bc01f38~tplv-goo7wpa0wc-image.image" width="2940px" /></div>



2. Grant project permissions to user groups: Click Permissions \- Add Permission to select different permission categories. You can configure global permissions and project permissions. When adding global permissions, the policy applies to all projects within the account (including newly added projects in the future). When adding project permissions, the policy applies only to resources within the project. After setting permissions, you can modify the scope of application via list operations.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84ef8b9c087947f7ba59c1eb7c375593~tplv-goo7wpa0wc-image.image" width="2940px" /></div>



3. After the user group is added, return to Project Center \- User Group Management. The user group will appear in the user group list. You can enable permissions for projects, dashboards, and datasets for a specific user group.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">User groups are set up to centrally manage users with similar characteristics or requirements and to grant unified access to project resources (for example, adding all finance personnel to one user group and granting access permissions to dashboards related to financial reports). To authorize temporary access to a dashboard when its participants will not collaborate after the current activity ends, click Authorize in the upper right corner of the dashboard and paste the user list, separated by <strong>English commas</strong>. Alternatively, add the participants to a Lark group and authorize the associated Lark group (make sure to configure the<a href="https://www.volcengine.com/docs/4726/67236#_3-2-%E6%9B%B4%E5%A4%9A%E5%9C%BA%E6%99%AF%EF%BC%88%E9%A3%9E%E4%B9%A6%E7%BE%A4%E6%8E%88%E6%9D%83%EF%BC%89">Lark Office System Integration</a> in advance).</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1037e439343646448dc54dfed413f6db~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13f552df1fbe4f42800b6d187deafdbc~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="deb8bce5"></span>
# Account update configuration

Through **account binding configuration**, you can preset a fixed refresh frequency. The system can automatically perform user information matching and synchronization according to the rules, ensuring that relevant permissions, data associations, and other user matching relationships are updated promptly after personnel changes, reducing manual intervention and ensuring the accuracy and timeliness of user matching in business processes.


1. In System Management \-\> User Management, click the **account binding configuration** button at the top of the list to enter the account update configuration interface.

2. Select the matching method: When the matching method is set to automatic matching, use the dropdown to select Lark fields (IM number, mobile number, email) and DataAgent fields (username, mobile number, email). The system will automatically perform the matching.

3. Select update settings: Use the dropdown to select automatic update or manual update.

* When **automatic update** is selected, you can choose the automatic update time point. You can select to update every day (specific time point required) or at a specified time each hour (dropdown to select the hourly refresh time point: on the hour, 15 minutes, 30 minutes, or 45 minutes) for matching updates.

* When **manual update** is selected, you can click the **update now** button to update user matching information. At the same time, updates will not be synchronized with changes to user information in Lark; user matching information will only be updated when the system administrator clicks the Update Now button below.

4. After all the above configurations are completed, click the Update Now button to match DataAgent platform accounts and Lark accounts according to the rules.
