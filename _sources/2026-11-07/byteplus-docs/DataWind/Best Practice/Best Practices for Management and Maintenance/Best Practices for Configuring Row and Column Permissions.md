---
title: "Best Practices for Configuring Row and Column Permissions"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Best_Practices_for_Configuring_Row_and_Column_Permissions"
---

<span id="_1-行列权限动态配置"></span>
# 1. Dynamic configuration of row and column permissions

<span id="_1-1-适用场景"></span>
## 1.1 Applicable scenarios

 **(1) Scenario 1:** 

Team personnel changes frequently. For example, each business staff member's assigned business line often changes. If each business staff member is restricted to viewing only the data for their assigned business line, the applicable members for row and column permissions must be frequently updated during normal configuration. When there are many resources or personnel, this configuration becomes very cumbersome.

 **(2) Scenario 2:** 

There are some region fields in the dataset. Now, it is expected that the business staff responsible for a region can automatically obtain permissions based on the value of the region field in the dataset, so there is no need to manually configure or modify permissions.

<span id="_1-2-配置过程"></span>
## 1.2 Configuration process

(1) For example, our dataset contains a province field. Each Sales representative is responsible for a different province and can only view the data for their assigned province.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/338b6758be0a4d23accbdb803fc18871~tplv-goo7wpa0wc-image.image) </span>

(2) At this point, the dynamic configuration feature for row and column permissions can be used. First, add a province attribute in the user properties in the project center, then set the province attribute value for each corresponding Sales representative to the province they are responsible for.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f007aae722764be4be0c8e739aea4151~tplv-goo7wpa0wc-image.image) </span>

(3) Next, on the row and column permissions configuration page, select Sync from dataset, then select the "sale_province" field equal to the "province" attribute. In this way, the applicable members for this row and column permission will automatically obtain dataset row and column permissions based on their own attribute values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1add56501e49a591625e4589750276~tplv-goo7wpa0wc-image.image) </span>

(4) Dynamic values also support configuring attributes for user groups. After adding row and column permissions to the entire user group, business staff within the user group can directly obtain the corresponding permissions. User attributes also support batch configuration through [User Management](https://docs.byteplus.com/docs/DataWind/User_Management).

<span id="_2-利用行权限配置绩效仪表盘"></span>
# 2. Use row permissions to configure a performance dashboard

<span id="_2-1-基本概念"></span>
## 2.1 Basic concepts

<span id="_2-1-1-行权限"></span>
### 2.1.1 Row permissions

By adding dataset 'row\-level permission' rules, users within a specified scope can only view the rows of data within their permitted range. Row\-level permissions apply to datasets and control the data range that users can access when viewing charts or dashboards created from these datasets.

Therefore, when charts on a dashboard originate from different datasets, it is sometimes necessary to configure multiple sets of row\-level permissions for each dataset to control the data range users can view across the entire dashboard.

<span id="_2-1-2-仪表盘与数据集"></span>
### 2.1.2 Relationship between dashboards and datasets

The relationship between dashboards and datasets can be one\-to\-one or one\-to\-many. Datasets can be used to create charts, and charts can be saved to dashboards; dashboards can display multiple charts from different datasets within the same project.

<span id="_2-2-实现效果"></span>
## 2.2 Expected outcome

**This configuration applies to the following scenarios:** 

To enable dashboards to display personalized data for each user. For example, with a performance dashboard, only one dashboard is configured, but different users see their own performance data when viewing the dashboard, while managers can view the data for the personnel they are responsible for.

Taking the course performance dashboard as an example, dashboard viewers are divided by permission into: managers, regional leaders, and frontline tutors. The data accessible to these three types of users is as follows:


|Administrator: All data |Regional leader: Data of the bases they are responsible for |Frontline mentor: Their own performance data |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06c81301f8334bf597149a9d8f9ac106~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8236929b65a41ff9e213f0dc3c475ee~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/697af987e9044777a5226172dbb4f914~tplv-goo7wpa0wc-image.image) </span> |


<span id="_2-3-操作步骤"></span>
## 2.3 Steps for implementation

<span id="_2-3-1-明确需求"></span>
### 2.3.1 Clarify requirements

Before configuration, clarify the permissions to be configured, including which datasets are used by the dashboard, user types, and the data matching rules for each user type.


* Dashboard: Identify which charts on which dashboards require row\-level permissions and define the configuration scope.

* Dataset: Identify which datasets correspond to the charts that need to be configured.

* User roles: Determine the configuration rules, specifying which types of users require row\-level permissions, as the rules differ among user types.

* Key attributes and corresponding dataset fields: The matching criteria for each user role's configuration rules.


Taking the performance dashboard as an example, suppose the performance dashboard is created from a single dataset. The permission rules are organized as follows:

In the performance dashboard, the charts correspond to the performance dataset, and permissions need to be granted to administrators, regional leaders, and frontline coaches. Administrators are granted full permissions, regional leaders are granted permissions for the bases they are responsible for, and frontline coaches are granted their own performance permissions based on their email prefix (username).


|Dashboard |Dataset |User role |Key attribute |Corresponding dataset field |
|---|---|---|---|---|
|Performance dashboard |Performance dataset |Administrator |*  |*  |
|Performance dashboard |Performance dataset |Regional leader |Responsible base |Base |
|Performance dashboard |Performance dataset |Frontline mentor |Username |Mentor |



* If the dashboard corresponds to multiple datasets, this means that row\-level permissions may need to be configured for multiple datasets. In this case, each dataset requires its own rules to be organized and configured one by one.

* What is the key attribute: that is, which user attribute should be used to match the user's permissions. After determining the attribute and field, the row\-level permission rule is that the user's key attribute equals the corresponding dataset field. In other words, users can only view the corresponding data when the value of the field in the dataset matches the value of the user's key attribute.


<span id="_2-3-2-用户组和用户属性配置"></span>
### 2.3.2 User group and user attribute configuration

When configuring user groups, it is recommended to create user groups based on roles to facilitate batch selection when configuring row\-level permissions later. If user groups are not created based on roles, you can also manually enter usernames one by one when configuring row\-level permission rules.

> Note: Only project administrators can create and modify user groups.


In Project Center \> User Management \> User Groups, click + to add a user group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cbad73006be4747ae9cf4d6ae32ecc1~tplv-goo7wpa0wc-image.image) </span>

You can use User Group Management \-\-\> "Add User Group" to batch add all users in a department to a user group, or use User Management \-\-\> "Add User" to add a single user.

> Tip: When adding a single user, you can separate multiple email prefixes with commas and paste them into the input box to add users in bulk.

> For example: zhangsan,lisi,wangwu. Copy this segment into the add user input box to add Zhang San, Li Si, and Wang Wu in bulk.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42dfb4e731c2472e93dc57e181e0a27b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c4edfecc52a4a2f806e2126ef392ec7~tplv-goo7wpa0wc-image.image) </span>

Configure user attributes in Project Center \- User Attributes. User attributes are the attributes of users in the project, and by default include username, name, email, and department. By configuring user attributes, you can add attribute tags for users and match permissions based on these attributes.

If there are no attributes in the project, click "Attribute Management" to manage and add attributes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5191452931154f6e9c242254fca94eab~tplv-goo7wpa0wc-image.image) </span>

Click "Batch Update Attributes" to assign corresponding attribute values to users in bulk.


* For frontline tutors, since the system includes the username by default (that is, the email prefix), there is no need to update attributes.

* For regional leaders, update the value of the "Responsible Base" attribute to the base they are responsible for; the format must match that in the dataset. If the base field in the dataset is something like "Beijing", the attribute value must also be "Beijing" and not "Beijing City".

* For administrators, since they need to view all permissions, it is recommended to create a dedicated attribute "Enable All Row\-Level Data Permissions" and set the administrator's attribute value to [\*].


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9938c6ee276a44648df13561da20efcd~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-3-3-行权限规则配置"></span>
### 2.3.3 Row\-level permission rule configuration

Go to the performance dataset \-\- Row and Column Permissions to create row\-level permission rules. In this case, three row\-level permission rules need to be created for the performance dataset, with configurations as shown in the figures below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35f099caa9b5469290fc93fcc92b7545~tplv-goo7wpa0wc-image.image) </span>

Tutor: Use dynamic value matching. As shown below, when the value of the Tutor field in the performance dataset is equal to the value of the Username attribute of the user in the Tutor user group, the tutor can view the corresponding data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/289d86e1f0144dcc9c13ea3072d2c746~tplv-goo7wpa0wc-image.image) </span>

Regional leader: Use dynamic value matching. As shown below, when the value of the Base field in the performance dataset is equal to the value of the Responsible Base attribute of the user in the Leader user group, the leader can view the corresponding data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ec4794653b040069cb89e968675c89a~tplv-goo7wpa0wc-image.image) </span>

Administrator: Use dynamic value matching. As shown below, when the value of the Base field in the performance dataset is any value, the administrator can view the corresponding data, that is, view all data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c59d0a30534c4ca9b0ce2f6ddc869e8a~tplv-goo7wpa0wc-image.image) </span>

Configure and save in sequence. On the data permission rules page for the dataset, you can see that there are three corresponding row\-level permission rules under this dataset. If you are unsure whether the rules are effective, you can use the [3.7 Permission simulation and verification](https://docs.byteplus.com/docs/DataWind/DataRow_and_Column_Permissions#_3-7-%E6%9D%83%E9%99%90%E6%A8%A1%E6%8B%9F%E9%AA%8C%E8%AF%81) feature to verify.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad7583a35939435d9e2d5a31886e321d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-4-仪表盘权限开通"></span>
### 2.3.4 Dashboard permission activation

After completing the row\-level permission configuration, you also need to grant dashboard permissions to the corresponding users. In the upper right corner of the dashboard, click Authorize, search for the user group, and directly grant permissions to the user group.
