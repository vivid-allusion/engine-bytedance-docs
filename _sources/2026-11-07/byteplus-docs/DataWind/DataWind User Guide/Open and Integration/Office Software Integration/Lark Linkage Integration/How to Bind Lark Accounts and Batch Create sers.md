---
title: "How to Bind Lark Accounts and Batch Create sers"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_Bind_Lark_Accounts_and_Batch_Create_sers"
---

<span id="_1-概述"></span>
# Overview

After integrating the Lark application, the account binding feature is now supported. To bind users in DataWind (hereinafter referred to as DataWind) with Lark accounts, follow these steps: first, enable the necessary permissions for sending Lark messages; then, go to **System Management \-\> User Management** and bind users either individually or in batches as needed. The following sections describe the specific steps for single user binding and batch binding.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9502bc4ea471476ba57cd6d61170efbd~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-单个用户飞书账号绑定"></span>
# Single Lark account binding

After entering System Management \-\> User Management in the DataWind product, select the corresponding user to bind their Lark account.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33a0fbd5738c4f69ae6eb1bbe38aefe1~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3386ad530fe9435fb6770782a3ea39ce~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="_2-1-自动匹配"></span>
## 2.1 Automatic matching

After selecting automatic matching as the matching method, you can match Lark account information with DataWind account information.


* In the selection below: the left side displays Lark account information, and the right side displays DataWind account information; select the matching fields as appropriate.

* The system will automatically match the user's information in DataWind with their information in Lark, and you can make a selection.


<span id="_2-2-手动绑定"></span>
## Manual binding

<span id="_2-2-1-基本配置"></span>
### Basic configuration

After selecting manual binding as the matching method, the user manually searches for the user's name in Lark to perform manual matching. If the specified user is not found, click the refresh button on the right.

<span id="_2-2-2-批量绑定飞书账号"></span>
### Batch bind Lark accounts

Batch creating accounts through Lark can address the following issues:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab15274d769d4433b719c29749accdb4~tplv-goo7wpa0wc-image.image) </span>


* To allow users to log in to DataWind only through their Lark accounts

* To batch create and associate DataWind accounts when there are many accounts under your organization

* To dynamically adjust account addition and deletion based on users' onboarding and offboarding information


**The specific steps are described as follows:** 

<span id="7092e3d2"></span>
#### 2.2.2.1 Cloud Identity Center configuration

To allow users to log in to BytePlus directly using their enterprise Lark accounts, the **enterprise administrator** needs to configure settings in the **Cloud Identity Center of BytePlus**.

(1) Enable Cloud Identity Center: After enabling the enterprise organization, the administrator goes to the [Cloud Identity Center](https://console.volcengine.com/auth/login?redirectURI=%2Fcloudidentity%2Fregion%3Acn-beijing%2FServiceOpen%2F) page of BytePlus and clicks to enable the service. (For details, see [Enable Cloud Identity Center](https://www.volcengine.com/docs/7165/198141).)

(2) User synchronization settings: The administrator goes to the [User Synchronization Settings](https://console.volcengine.com/cloudidentity/region:cn-beijing/userSync/) page, clicks **Configure Identity Source**, selects Lark, then downloads the BytePlus app, enables the app, and scans the code to bind the Lark tenant. (For details, see [User Synchronization Settings](https://www.volcengine.com/docs/7165/198129).)

(3) Configure user access authorization: An IAM sub\-user with the appropriate permissions under the enterprise organization's administrator account logs in to the BytePlus console, goes to the [Multi-Account Access Management](https://console.volcengine.com/cloudidentity/region:cn-beijing/multiAccountAccess/) page, selects the accounts to be authorized, and then clicks **Configure User SSO** at the bottom of the list. (For details, see [Configure User Access Authorization](https://www.volcengine.com/docs/7165/198132).)

After completing the above steps, enterprise employees can log in to BytePlus using their Lark accounts.

<span id="0adf264c"></span>
#### Add users to DataWind


1. Open the BytePlus DataWind Workbench, log in with the administrator account, and click the settings icon in the upper right corner to enter system management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c517e7e39b564d28b9566fa2e766fe8e~tplv-goo7wpa0wc-image.image) </span>

2. Click Security Settings \- System Control \- License Control Method. You can set the license control method to "Automatically add when system users log in to this product". In this case, all accounts authorized in Cloud Identity Center can log in to DataWind directly using their Lark accounts.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1447f503cb54583a0b29cadf98def27~tplv-goo7wpa0wc-image.image) </span>


If you select "System administrator configures license list", the administrator needs to perform secondary authorization. After entering system management, the administrator clicks User Management, then clicks Add User in the upper right corner to add users. After users are added successfully, they can log in to DataWind.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a5d82938ecd4a86b926b4e49a4e31ba~tplv-goo7wpa0wc-image.image) </span>

<span id="e590f2e7"></span>
#### Grant project permissions

In addition to granting users access to the DataWind platform, to access resources within a specific project, the administrator needs to grant users edit or view permissions for the project.Please refer to [Getting Started Guide for Administrator](https://docs.byteplus.com/docs/DataWind/Getting_Started_Guide_for_Administrator).


1. Create a user group: Click Project Center \- User Group Management, then click the plus sign in the user group list to create a new user group. After navigating to the user group details page, click Add User and select the users to add to the group.

2. Grant project permissions to the user group: Click Permissions \- Add Permission, and select different permission categories. You can set global permissions and project permissions. When adding global permissions, the policy applies to all projects under the account (including projects added in the future). When adding project permissions, the policy applies only to resources within the project. After setting permissions, you can modify the scope of application in the list.

3. After adding the user group, return to Project Center \- User Group Management. The user group will appear in the user group list. You can specifically enable permissions for projects, dashboards, and datasets for a particular user group.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">User groups are used to centrally manage and authorize users with similar characteristics or requirements for project resources (for example, adding all finance personnel to one user group and granting access to dashboards related to financial reports). If a dashboard is used temporarily and its participants will not collaborate after the current activity ends, click Authorize in the upper right corner of the dashboard, paste the user list separated by <strong>English commas</strong>; you can also add participants to a Lark group and authorize the associated Lark group (make sure to configure the <a href="https://www.volcengine.com/docs/4726/67236#_3-2-%E6%9B%B4%E5%A4%9A%E5%9C%BA%E6%99%AF%EF%BC%88%E9%A3%9E%E4%B9%A6%E7%BE%A4%E6%8E%88%E6%9D%83%EF%BC%89">Lark Office System Integration</a> in advance).</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c734cb08dd404079a1432c15d82696d6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-更新设置"></span>
# Update settings

<span id="_3-1-自动更新"></span>
## Automatic update


* You can choose to perform matching updates at a specified time each day or hour, such as when users join or leave the organization.

* You can refresh at the specified automatic update time.


<span id="_3-2-手动更新"></span>
## Manual update

User information will not be updated along with changes in Lark; only when the system administrator clicks Update Now below will user matching information be updated.

<span id="_3-3-立即更新"></span>
## Update now

Click Update Now, and the DataWind platform account and the Lark account can now be matched according to the rules.
