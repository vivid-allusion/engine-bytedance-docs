---
title: "Data Row and Column Permissions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Row_and_Column_Permissions"
---

<span id="_1-概述"></span>
# 1. Overview

On the data permissions page of a dataset, you can control row\-level permissions for fields and column permissions at the dataset level.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Row and column permissions for data are configured by dataset administrators. If the dataset has set data permission rules (such as row permission rules or column permission rules), users subject to data permission restrictions can only access authorized content.</div>


**Key terms**

**User attributes**: These are the attributes or tags of users within the project. User attribute information is an essential source of dynamic values for row\-level data permissions.

**Row permissions**: By adding a 'row permissions' rule to a dataset, you can restrict specified users to view only specified rows of data. For example, user A can only view data in the dataset where the 'region' field equals Shanghai.

**Column permissions**: By adding a 'column permissions' rule to a dataset, you can configure sensitive columns so that users outside the specified range cannot view the data in those columns. For example, user A can view the 'income' column data in the dataset, while other users cannot.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/491b8f73858f41c49ea3d80434fa84f4~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-创建数据权限规则"></span>
## 2.1 Create data permission rules

(1) Open the dataset details page for which you want to set row or column permissions, click 'Data Permissions' \- 'Add Data Permission', to enter the data permission editing page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8b53332b3c44171be871aa941fc7690~tplv-goo7wpa0wc-image.image) </span>

(2) You can customize the name of the data permission rule.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3df6cd5da1d2457196cf03b63b3c4a59~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(3) Configure specific rules for the dataset, choosing either row permissions or column permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4ae8e505bde43b896b3ebcc9d74edce~tplv-goo7wpa0wc-image.image) </span>

(4) Select the users, user groups, or role groups that the rule applies to.

**SaaS version:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84563463746a41c0b2c1e19699102371~tplv-goo7wpa0wc-image.image) </span>

**Private deployment version:**  This capability allows you to select 'roles' within this project as applicable members for rules. Some roles cannot have permissions assigned by non\-role administrators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84563463746a41c0b2c1e19699102371~tplv-goo7wpa0wc-image.image) </span>

(5) Click the 'Save Rule' button in the upper right corner. The configured data permissions will take effect immediately.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f51480858c94bd3a1f82d685274db27~tplv-goo7wpa0wc-image.image) </span>

(6) To set multiple data permission rules, repeat the steps above.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For users not mentioned in the data permission rule configuration, the platform provides a setting for the scope of row and column\-level permissions, which is disabled by default. That is, users not covered by the row and column\-level permission rules cannot view any data. Dataset administrators can enable or disable this setting as needed.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19febd8c41654eeb9dc4096db728b789~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="_2-2-数据权限规则操作"></span>
## 2.2 Data permission rule operations

<span id="_2-2-1-查看详情"></span>
### 2.2.1 View details

Click the view details icon to see the content of the rule and the members affected by the rule.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef0f7a15a2de4298bb389e3bc4e834e3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/399b38b7d87f4e32ba6fee556c28df23~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-2-编辑"></span>
### 2.2.2 Edit

Enter the corresponding data permission editing page to modify the configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af5f1d9534284cfb892db56e9495fd70~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-3-复制"></span>
### 2.2.3 Copy

You can copy existing data permission rules. If several data permission rules have similar configurations, you can quickly set them up by copying existing rules.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2fa3026ee584ed1b30cb93a667918c3~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-4-删除"></span>
### 2.2.4 Delete

Supports deleting data permission rules that have already been configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/499de01b92ee4854b48bc68a095ab000~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-行权限·固定值"></span>
## 3.1 Row permissions · fixed value


* Select the dataset field restricted by the row permission rule and set a fixed value. Grant the affected users (or user groups) access to only the subset of data where the dataset field equals the specified value.

* This is suitable for scenarios where there are few controlled users, or quick authorization can be achieved through simple operations with user groups.

* Supports configuring one or more restriction rules.


As shown in the figure, when viewable members access charts generated from the dataset, they can only view data where p_sate <= '2026\-05\-12' and cannot access all data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ee28256939429f8d83162897633906~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-行权限·动态值"></span>
## 3.2 Row permissions · dynamic value


* Select the dataset field restricted by the row permission rule and match user attributes. Dynamically grant affected users (or user groups) access to only the subset of data where the dataset field value equals the user's attribute value.

* This is suitable for scenarios where there are many controlled user attribute values, making configuration with fixed values inconvenient, and authorization can be distinguished by specific attributes.

* Supports configuring one or more restriction rules.


As shown in the figure, when viewable members access charts generated from the dataset, they can only view data where the event end time greater than and equal to '2026\-05\-12' and cannot view other data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61a39bd49e89493cb47b2764d329f377~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-列权限"></span>
## 3.3 Column permissions

Set one or more specific columns in the dataset as sensitive columns. Only users or user groups designated as viewable members, dataset administrators, and users with project\-wide view permissions can access them. Other users cannot view sensitive field data. As shown in the figure, users other than viewable members (such as "Administrator") cannot view the sensitive column model field 'Activity Sending Time' when accessing charts or dashboards generated from the dataset. This column is hidden from members other than viewable members.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8115a04fb5f443fdb3b4fa412aeb3e56~tplv-goo7wpa0wc-image.image) </span>

Except for the sensitive column 'Activity Sending Time', fields created based on 'Activity Sending Time' will also be affected and hidden from users other than '管理者'.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f930e8077074905a563d1ce3227d85d~tplv-goo7wpa0wc-image.image) </span>

To prevent associated fields from being affected, set individual dataset fields as sensitive columns instead of model fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ccdfb7165b94f02979e4bc46697e051~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-当数据集存在多个行-列权限规则"></span>
## 3.4 When a dataset contains multiple row/column permission rules

When a dataset has multiple row and column permission rules simultaneously, affected users can view the union of the permissions they possess. For example, if both rule 1 and rule 2 in a dataset apply to user 甲, rule 1 allows 甲 to view data in row A, and rule 2 allows 甲 to view data in row B, then 甲 can view data in both rows A and B. When a dataset has multiple row and column permission rules, and these rules apply to some users, the scope of data that users can view can be considered separately. For example, if rules 1, 2, and 3 in a dataset all apply to user 乙, rule 1 is a row permission rule that allows 乙 to view data in row A; rules 2 and 3 are column permission rules, where rule 2 allows 乙 to view data in sensitive column B, and rule 3 prevents 乙 from viewing data in column C; then 乙 can view the portion of data in row A that does not include column C. As shown in the figure, user (group) 乙 is included in the affected users (groups) for rules 1 and 2, but not for rule 3:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85da3656c8a2476a8ccef6efc434fed0~tplv-goo7wpa0wc-image.image) </span>

The final data that user 乙 can view is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2d9ba94169446d08f630f84803aeedc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-行列权限生效范围"></span>
## 3.5 Scope of row and column permissions

Caution: For users not mentioned in the configuration of row and column permission rules, the product provides a setting for the scope of row and column permissions, which is disabled by default. That is, users not targeted by row and column permission rules cannot view any data. Dataset administrators can switch this setting as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3850d309241e42aaa3ead552efe16f37~tplv-goo7wpa0wc-image.image) </span>

**Row permissions**


* Users other than applicable members cannot view any row data.

* Members other than applicable members are not subject to row permission control and can view all row data.


<span id="_3-6-列权限"></span>
## 3.6 Column permissions


* Applicable members can view this column, while users other than applicable members cannot view it.

* Applicable members cannot view this column, while users other than applicable members can view it.


<span id="_3-7-权限模拟验证"></span>
## 3.7 Permission simulation verification

After completing the data permission configuration, dataset administrators can simulate user identities to view what data the corresponding user can access in the dataset, thereby verifying data permissions and avoiding misconfiguration. Click "Permission simulation verification."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c394e36f32247528eac6fd0642c66db~tplv-goo7wpa0wc-image.image) </span>

Enter the user to be verified, that is, the user whose data permission scope needs to be simulated, and click "Start verification."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a486150579c44aa964085dada4cfebf~tplv-goo7wpa0wc-image.image) </span>

You will then enter the visualization interface of the dataset as the verified user, where you can configure charts to check the data range that the user can view. You can switch between multiple users for permission simulation verification on the current page.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cbc82ace434136bcf07670e1169522~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


After verification, click "Exit verification" to return to the data permission interface. If there is an issue with the viewing scope of the current user during verification, you can check and adjust the data permission configuration. Once the permission scopes for all user identities have been verified to be correct, you can confidently proceed with chart and dashboard publishing.

<span id="_3-8-行列权限备注"></span>
## 3.8 Notes on row and column permissions

If customers are also using DataLeap, then DataLeap's row and column permissions will also take effect in DataAgent. After DataAgent connects to DataLeap's data, it will display which fields and which rows do not have permissions. This capability also depends on the product platform version. If the platform is an earlier version, additional deployment of DataLeap components is required. For specific details, please contact the customer success manager.
