---
title: "DataRow and Column Permissions"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/DataRow_and_Column_Permissions"
---

<span id="_1-概述"></span>
# 1. Overview

On the data permissions page of a dataset, you can control row\-level and column\-level permissions at the dataset level.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Row and column permissions are configured by dataset administrators. If data permission rules (such as row permission rules and column permission rules) are configured for a dataset, users subject to data permission restrictions will be restricted by these data permissions when accessing charts, dashboards, or visual queries that use the dataset (including when using filters), and will only be able to access content for which they have permission.</div>


**Key terms**

**User attributes**: These are the attributes or tags of users within the project. User attribute information is an essential source of dynamic values for row\-level data permissions.

**Row permissions**: By adding a "row permissions" rule to a dataset, you can restrict specified users to view only specified rows of data. For example, user A can only view data in the dataset where the "region" field equals Shanghai.

**Column permissions**: By adding a "column permissions" rule to a dataset, you can configure sensitive columns so that users outside the specified scope cannot view data in those columns. For example, user A can view the "income" column data in the dataset, while other users cannot.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dda6c0658a1647a580c85739c8a68277~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-创建数据权限规则"></span>
## 2.1 Create data permission rules

(1) Open the dataset details page where you need to set row or column permissions, click "Data Permissions" \- "Add Data Permission", and enter the data permission editing page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/696e67119f2141649603bd12ef6f0c9a~tplv-goo7wpa0wc-image.image) </span>

(2) The name of the data permission rule can be customized.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c08380df15242e59717c0a21d58eb05~tplv-goo7wpa0wc-image.image) </span>

(3) Set specific rules for the dataset; you can choose row permissions or column permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/066119f7deed4bfca1f8862f15fd0cbc~tplv-goo7wpa0wc-image.image) </span>

(4) Select the users, user groups, or role groups to which the rule applies.

**SaaS version:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bb1e71482bb43eba282a7f39c6dba76~tplv-goo7wpa0wc-image.image) </span>

**Private deployment version:**  For this capability, "Applicable members for rules" supports selecting "roles" within this project. Some roles do not allow permissions to be granted by non\-role administrators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9e42ec2c6e4015a2adefde7d22dcdb~tplv-goo7wpa0wc-image.image) </span>

(5) Click the "Save Rule" button in the upper right corner. The configured data permissions will take effect immediately.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6244fd4fee084b6d8698c1a1ed1964ea~tplv-goo7wpa0wc-image.image) </span>

(6) To set multiple data permission rules, repeat the steps above.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For users not mentioned in the data permission rule configuration, the platform provides a setting for the scope of row and column permissions, which is disabled by default. This means that users not covered by the row and column permission rules cannot view any data. Dataset administrators can switch this setting as needed.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2b81cdc57f24fb197b03a2fe7640866~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="_2-2-数据权限规则操作"></span>
## 2.2 Data permission rule operations

<span id="_2-2-1-查看详情"></span>
### 2.2.1 View details

Click the view details icon to see the content of the rule and the members to whom it applies.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/558d58f79d534e2f9ade0405e4b3b9a5~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac24f9f35add4827808a8b47cc4831e1~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-2-编辑"></span>
### 2.2.2 Edit

Enter the corresponding data permission editing page to modify the configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ad9fdd6fe164d76810fee124fc642d5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-3-复制"></span>
### 2.2.3 Copy

Copying existing data permission rules is supported. If multiple data permission rules have similar configurations, you can quickly configure them by copying existing rules.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3417b59bd6514b0d9e7624320e3a5dc1~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-4-删除"></span>
### 2.2.4 Delete

Supports deleting data permission rules that have already been configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb4f99a8d244a11811962ced4d7df23~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-行权限·固定值"></span>
## 3.1 Row permissions · Fixed value


* Select the dataset fields restricted by the row permission rule and set fixed values to grant users (or user groups) access only to the subset of data where the field equals the specified value.

* This is suitable for scenarios with few controlled users, or where quick authorization can be achieved through simple user group operations.

* Supports configuring one or more restriction rules.


As shown in the figure, when members access charts generated from the dataset, they can only view data where Province = 'Shanghai' and cannot access all data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/502f6115036b4eb08cb962adcb880e1d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-行权限·动态值"></span>
## 3.2 Row permissions · Dynamic value


* Select the dataset fields restricted by the row permission rule and match user attributes to dynamically grant users (or user groups) access only to the subset of data where the field value equals the user's attribute value.

* This is suitable for scenarios where there are many controlled user attribute values, making it inconvenient to configure with fixed values, and where authorization can be distinguished by specific attributes.

* Supports configuring one or more restriction rules.


For user attribute configuration, refer to the documentation: [User Properties](https://docs.byteplus.com/docs/DataWind/User_Properties) As shown in the figure, when members access charts generated from the dataset, they can only view data where the user field matches their own name and cannot view other users' data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e89e5f1cfd3c44cd9e9402655f768ad6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-列权限"></span>
## 3.3 Column permissions

Set specific columns in the dataset as sensitive columns, which are only accessible to users or user groups designated as viewers, dataset administrators, and users with project\-wide view permissions. Other users cannot view data in sensitive fields. As shown in the figure, except for viewers with the "Administrator" role, other users cannot view the sensitive column model field 'Job Submission Rate' when accessing charts or dashboards generated from the dataset. This column is hidden from members other than viewers.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0eeb41031564bdc973b15bae82c7d67~tplv-goo7wpa0wc-image.image) </span>

Except for the sensitive column '作业提交率', the fields created based on '作业提交率', namely '是否达成提交率目标' and '平均提交率', will also be affected. These fields will be hidden from users other than administrators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/706edd28021c4ea38633bc197250466d~tplv-goo7wpa0wc-image.image) </span>

To prevent associated fields from being affected, set a single dataset field, rather than a model field, as a sensitive column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be45bb1af2ca4d208109ff5d1c125be0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-当数据集存在多个行-列权限规则"></span>
## 3.4 When multiple row or column permission rules exist in a dataset

When a dataset contains multiple row and column permission rules at the same time, applicable users can view the union of the rule permissions they possess. For example, if both Rule 1 and Rule 2 in a dataset apply to User A; Rule 1 allows A to see row A, and Rule 2 allows A to see row B; then A can see both rows A and B. When a dataset contains multiple row and column permission rules that apply to some users at the same time, the data range that users can view can be considered separately. For example, if Rule 1, Rule 2, and Rule 3 in a dataset all apply to User B; Rule 1 is a row permission rule that allows B to see row A; Rule 2 and 3 are column permission rules, where Rule 2 allows B to see the sensitive column B, and Rule 3 prevents B from seeing column C; then B can see the part of row A that does not include column C. As shown in the figure, User B is included in the users (groups) to whom Rules 1 and 2 apply, but not in the users (groups) to whom Rule 3 applies:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc39d6dbefcf47cfa05cc502f0f4b38b~tplv-goo7wpa0wc-image.image) </span>

The final data that User B can see is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d841bc392e94be6b0cf332fb8db120b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-行列权限生效范围"></span>
## 3.5 Scope of row and column permissions

Caution: For users not mentioned in the row and column permission rule configuration, the product provides a setting for the scope of row and column permissions, which is disabled by default. That is, users not covered by the row and column permission rules cannot view any data. Dataset administrators can switch this setting as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8006469e84c14604a6576f3556f57afb~tplv-goo7wpa0wc-image.image) </span>

**Row permissions**


* Users other than applicable members cannot view any row data.

* Members other than applicable members are not subject to row permission control and can view all row data.


<span id="_3-6-列权限"></span>
## 3.6 Column permissions


* Applicable members can view this column, while users other than applicable members cannot view it.

* Applicable members cannot view this column, while users other than applicable members can view it.


<span id="_3-7-权限模拟验证"></span>
## 3.7 Permission simulation and verification

After completing the data permission configuration, dataset administrators can simulate user identities to verify which data each user can access in the dataset, thereby verifying data permissions and avoiding misconfiguration. Click "Permission simulation and verification"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f8f96513c554a34bc851e8140a7da9b~tplv-goo7wpa0wc-image.image) </span>

Enter the user to be verified, that is, the user whose data permission scope needs to be simulated, and click "Start verification".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7f951f9bb2d4271b0522e1eb95fcdfd~tplv-goo7wpa0wc-image.image) </span>

You will then enter the visualization interface of the dataset as the verified user. You can configure charts to check the data range that the user can view. You can switch between multiple users on the current page for permission simulation and verification.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68158842eaa94261ba86a9486227253b~tplv-goo7wpa0wc-image.image) </span>

After verification, click "Exit verification" to return to the data permission interface. If there is an issue with the data range viewed by the current user during verification, you can check and adjust the data permission configuration. Once the permission scopes for all user identities are verified to be correct, you can confidently publish charts and dashboards.

<span id="_3-8-行列权限备注"></span>
## 3.8 Notes on row and column permissions

Starting from version V2.54.0, if customers use DataLeap simultaneously, DataLeap's row and column permissions will also take effect in DataWind. After DataWind connects to DataLeap's data, it will display which fields and which rows do not have permissions. This capability also depends on the platform version. If the version is lower, additional deployment of DataLeap components is required. For specific situations, please contact the customer success manager for details.

<span id="_4-最佳实践"></span>
# 4. Best practices

**For details, see**:[Best Practices for Configuring Row and Column Permissions](https://docs.byteplus.com/docs/DataWind/Best_Practices_for_Configuring_Row_and_Column_Permissions).
