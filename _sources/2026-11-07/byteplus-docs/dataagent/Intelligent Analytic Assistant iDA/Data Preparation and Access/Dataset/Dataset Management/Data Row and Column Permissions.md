---
title: "Data Row and Column Permissions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Row_and_Column_Permissions_"
---

<span id="_1-概述"></span>
# 1. Overview

On the data permissions page of a dataset, you can control row\-level permissions for fields and column permissions at the dataset level.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Row and column permissions for data are configured by the dataset administrator. If data permission rules (such as row permission rules or column permission rules) are set for the dataset, users subject to data permission restrictions can only access content for which they have permission.</div>


**Key terms**

**User attributes**: These are the attributes or tags of users within the project. User attribute information is an essential source of dynamic values for row\-level data permissions.

**Row permissions**: By adding a "row permissions" rule to a dataset, you can restrict specified users to view only specified rows of data. For example, user A can only view data in the dataset where the "region" field equals Shanghai.

**Column permissions**: By adding a "column permissions" rule to a dataset, you can configure sensitive columns so that users outside the specified scope cannot view data in those columns. For example, user A can view the "income" column in the dataset, while other users cannot.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57a1af3b398749e18e819bf6bd022869~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-创建数据权限规则"></span>
## 2.1 Create data permission rules

(1) Open the dataset details page where you need to set row or column permissions, click "Data Permissions" \- "Add Data Permission", and enter the data permission editing page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8b53332b3c44171be871aa941fc7690~tplv-goo7wpa0wc-image.image) </span>

(2) The name of the data permission rule can be customized.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3df6cd5da1d2457196cf03b63b3c4a59~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(3) Set specific rules for the dataset; you can choose row permissions or column permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4ae8e505bde43b896b3ebcc9d74edce~tplv-goo7wpa0wc-image.image) </span>

(4) Select the users, user groups, or role groups to which the rule applies.

**SaaS version:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84563463746a41c0b2c1e19699102371~tplv-goo7wpa0wc-image.image) </span>

**On\-premises version:**  For this capability, "Applicable members for rules" supports selecting "roles" within this project. Some roles do not support permission assignment by non\-role administrators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84563463746a41c0b2c1e19699102371~tplv-goo7wpa0wc-image.image) </span>

(5) Click the "Save Rule" button in the upper right corner. The configured data permissions will take effect immediately.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f51480858c94bd3a1f82d685274db27~tplv-goo7wpa0wc-image.image) </span>

(6) To set multiple data permission rules, repeat the steps above.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The platform provides row and column permission scope settings for users not mentioned in the data permission rule configuration. These settings are disabled by default, meaning that users not covered by row and column permission rules cannot view any data. Dataset administrators can switch these settings as needed.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19febd8c41654eeb9dc4096db728b789~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="_2-2-数据权限规则操作"></span>
## 2.2 Data permission rule operations

<span id="_2-2-1-查看详情"></span>
### 2.2.1 View details

Click the view details icon to see the content of the rule and the members to whom it applies.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef0f7a15a2de4298bb389e3bc4e834e3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/399b38b7d87f4e32ba6fee556c28df23~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-2-编辑"></span>
### 2.2.2 Edit

Go to the corresponding data permission editing page to modify the configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af5f1d9534284cfb892db56e9495fd70~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-3-复制"></span>
### 2.2.3 Copy

You can copy existing data permission rules. If multiple data permission rules have similar configurations, you can quickly set them up by copying existing rules.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2fa3026ee584ed1b30cb93a667918c3~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-4-删除"></span>
### 2.2.4 Delete

Supports deleting data permission rules that have already been configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/499de01b92ee4854b48bc68a095ab000~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-行权限·固定值"></span>
## 3.1 Row permissions · fixed value


* Select the dataset fields to be restricted by the row permission rule and set a fixed value. Grant affected users (or user groups) access to only the subset of data where the dataset field equals the specified value.

* This is suitable for scenarios where there are few controlled users, or where quick authorization can be achieved easily through user groups.

* Supports configuring one or more restriction rules.


As shown in the figure, when viewable members access charts generated from the dataset, they can only view data where p_sate <= '2026\-05\-12' and cannot access all data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ee28256939429f8d83162897633906~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-行权限·动态值"></span>
## 3.2 Row permissions · dynamic value


* Select the dataset fields to be restricted by the row permission rule and match user attributes. Dynamically grant affected users (or user groups) access to only the subset of data where the dataset field value equals the user's attribute value.

* This is suitable for scenarios where there are many controlled user attribute values, making configuration with fixed values inconvenient, and authorization can be distinguished by specific attributes.

* Supports configuring one or more restriction rules.


As shown in the figure, when viewable members access charts generated from the dataset, they can only view data where the event end time greater than and equal to '2026\-05\-12' and cannot view other data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61a39bd49e89493cb47b2764d329f377~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-列权限"></span>
## 3.3 Column permissions

Set one or more specific columns in the dataset as sensitive columns. Only users or user groups designated as viewable members, dataset administrators, and users with project\-wide view permissions can access them. Other users cannot view data in sensitive fields. As shown in the figure, except for viewable members ("Administrator"), other users cannot view the sensitive column model field 'Activity Sending Time' when accessing charts or dashboards generated from the dataset. This column is hidden from members other than viewable members.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8115a04fb5f443fdb3b4fa412aeb3e56~tplv-goo7wpa0wc-image.image) </span>

Except for the sensitive column 'Activity Sending Time', fields created based on 'Activity Sending Time' will also be affected and hidden from users other than 'Administrators'.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f930e8077074905a563d1ce3227d85d~tplv-goo7wpa0wc-image.image) </span>

You can set individual dataset fields, rather than model fields, as sensitive columns to prevent associated fields from being affected.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ccdfb7165b94f02979e4bc46697e051~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-当数据集存在多个行-列权限规则"></span>
## 3.4 When a dataset has multiple row/column permission rules

When a dataset has multiple row and column permission rules at the same time, applicable users can view the union of the permission rules they have. For example, both Rule 1 and Rule 2 in a dataset apply to User A; Rule 1 allows User A to view data in Row A, and Rule 2 allows User A to view data in Row B; therefore, User A can view data in both Row A and Row B. When a dataset has multiple row and column permission rules that apply to some users simultaneously, the range of data that users can view can be considered separately. For example, Rules 1, 2, and 3 in a dataset all apply to User B; Rule 1 is a row permission rule that allows User B to view data in Row A; Rules 2 and 3 are column permission rules, where Rule 2 allows User B to view data in sensitive column B, and Rule 3 prevents User B from viewing data in column C; therefore, User B can view the portion of data in Row A that does not include column C. As shown in the figure, User B is included in the applicable users (groups) for Rules 1 and 2, but not for Rule 3:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85da3656c8a2476a8ccef6efc434fed0~tplv-goo7wpa0wc-image.image) </span>

The final data that User B can view is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2d9ba94169446d08f630f84803aeedc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-行列权限生效范围"></span>
## 3.5 Scope of row and column permissions

Caution: For users not mentioned in the configuration of row and column permission rules, the product provides a setting for the scope of row and column permissions, which is disabled by default. That is, users not matched by row and column permission rules cannot view any data. Dataset administrators can switch this setting as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3850d309241e42aaa3ead552efe16f37~tplv-goo7wpa0wc-image.image) </span>

**Row permissions**


* Users other than applicable members cannot view any row data.

* Members other than applicable members are not subject to row permission control and can view all row data.


<span id="_3-6-列权限"></span>
## 3.6 Column permissions


* Applicable members can view this column, while users other than applicable members cannot view it.

* Applicable members cannot view this column, while users other than applicable members can view it.


<span id="_3-7-权限模拟验证"></span>
## 3.7 Permission simulation validation

After completing the data permission configuration, dataset administrators can simulate user identities to view what data the corresponding user can see in the dataset, thereby validating data permissions and avoiding mismatches. Click "Permission Simulation Validation."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c394e36f32247528eac6fd0642c66db~tplv-goo7wpa0wc-image.image) </span>

Enter the user to be validated, that is, the user whose data permission scope needs to be simulated, and click "Start Validation."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a486150579c44aa964085dada4cfebf~tplv-goo7wpa0wc-image.image) </span>

You will then enter the visualization interface of the dataset as the validated user. You can configure charts to verify the data range that the user can view. You can switch between multiple users for permission simulation validation on the current page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cbc82ace434136bcf07670e1169522~tplv-goo7wpa0wc-image.image) </span>

After validation, click "Exit Validation" to return to the data permission interface. If there is an issue with the current user's viewing scope during validation, check and adjust the data permission configuration. Once the permission scopes for all user identities have been validated as correct, you can confidently proceed with publishing charts and dashboards.

<span id="_3-8-行列权限备注"></span>
## 3.8 Notes on row and column permissions

If customers use DataLeap concurrently, the row and column permissions of DataLeap will also take effect in DataAgent. After DataAgent accesses data from DataLeap, it will display which fields and which rows do not have permission. This capability also depends on the version of the platform. For lower versions, additional deployment of DataLeap components is required. For details, please contact your customer success manager.
