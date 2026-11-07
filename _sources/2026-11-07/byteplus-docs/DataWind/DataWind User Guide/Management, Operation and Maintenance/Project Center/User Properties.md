---
title: "User Properties"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/User_Properties"
---

<span id="_1-概述"></span>
# 1. Overview

In the Project Center module of Intelligent Data Insight, project administrators can add, delete, or modify attributes or tags for users within the project. User attribute information is an essential source of dynamic values for row\-level data permissions. The user attributes module is accessible only to project administrators.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-查看-编辑用户属性值"></span>
## 2.1 View/Edit user attribute values

(1) Go to the User Attributes page in the Project Center, and enter the username to be queried in the input box.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2f5c2d47689415abdcaea74636629d5~tplv-goo7wpa0wc-image.image) </span>

(2) Locate the attribute field column (for example, Region), and view the specific attribute value.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee52e0301ae84988a8ce4c710c32881e~tplv-goo7wpa0wc-image.image) </span>

(3) Hover the mouse over the cell of the attribute value, and click the edit button that appears on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f410da0ab5664bf5b93fb44ac8e7f3de~tplv-goo7wpa0wc-image.image) </span>

(4) Refer to the editing rules below to enter the attribute value, click Save, and the user attribute value will be updated successfully.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0e2f7de89874dec9b383dff10bc4e5c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-新增用户属性字段"></span>
## 2.2 Add a user attribute field

(1) Go to the User Attributes page, click the "User Attributes" button in the upper right corner, and open the attribute management dialog box.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83e9a24ca5a84b7cad4ab32379bf1d10~tplv-goo7wpa0wc-image.image) </span>

(2) In the attribute management dialog box, click [Add Attribute] to add an attribute field, enter the attribute name (for example, Product) in the Attribute Name column, select whether to make it public, and enter the person in charge.

> Attribute Name: The name of the attribute field column.

> Public: If "Yes" is selected, the attribute is visible and available to all users with project editing permissions; otherwise, it is only visible and available to project administrators and the person in charge of the attribute field.

> Person in charge: The person responsible for the attribute name. Only the person in charge can edit or delete the attribute name. Multiple usernames can be entered.

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e45891b0d87490bafa522d19f20efe2~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-属性字段管理"></span>
## 3.1 Attribute field management

<span id="_3-1-1-手动新增-编辑用户属性"></span>
### 3.1.1 Manually add/edit user attributes

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f230f5ef71c2445b884fe522133a2b71~tplv-goo7wpa0wc-image.image) </span>

(1) Go to the User Attributes page, click the "User Attributes" button in the upper right corner, and open the attribute management dialog box.

(2) In the attribute management dialog box, click [Add Attribute] to add an attribute field. The system will check whether the current user has exceeded the personal creation limit or if the total number of attribute fields has reached the maximum. If neither limit has been reached, a new record will be added at the end of the attribute field list. Note: To prevent excessive proliferation of project attributes, the total number of user attributes within a project must not exceed 50, and each user can add up to 15 new attributes.

(3) Enter the attribute name (for example, product) in the attribute name column, select whether to make it public, fill in the person responsible, and so on.

> Attribute name: This is the name of the attribute field column.

> Public: If "Yes" is selected, the attribute is visible and available to all users with project editing permissions; otherwise, it is only visible and available to project administrators and the person responsible for the attribute field.

> Person responsible: This is the person responsible for the attribute name. Only the person responsible can view, edit, and delete the attribute name. Multiple usernames can be entered.

> Action: Click the delete button to delete the attribute.


(4) Users can also scroll or search to find the field to edit, then select it for editing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7533f48c5ded47da9f497f15f41d9105~tplv-goo7wpa0wc-image.image) </span>

Note: Users can only edit or delete attribute fields for which they are the person responsible. When deleting, if the attribute field is referenced by row permissions, it cannot be deleted.

<span id="_3-1-2-从数据集同步用户属性"></span>
### 3.1.2 Synchronize user attributes from a dataset

In addition to manually entering user attributes one by one, users can also add user attributes by synchronizing from a dataset. This method supports the following dataset types: extracted datasets and ClickHouse direct connection datasets.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfea44d5db314472a7bd125c47fdec1b~tplv-goo7wpa0wc-image.image) </span>

First, in attribute management, select "Synchronize from dataset".

Next, enter the attribute name and select whether to make it public.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2531544ad4047f5a2d4090d62527f9e~tplv-goo7wpa0wc-image.image) </span>

Then, select which dataset to synchronize from (only extracted datasets or CK direct connection datasets are supported), and select the corresponding dataset field.

After that, set the matching field. To synchronize user attributes from a dataset, ensure that the dataset contains a field that can be matched with the system username. Only text\-type fields are supported for this purpose.

Finally, you can also perform actions such as deleting and clearing the cache.

**Caution:** 


1. After configuring the attributes to be synchronized from the dataset, manual maintenance is not required. By default, data is read from the latest partition (if available). There is a one\-hour cache. To clear the cache, click the Clear Cache button.

2. User attributes synchronized from datasets can only be applied to users and cannot be applied to user groups.

3. Only user attributes from datasets for which you have management or higher permissions can be synchronized.

4. To assign multiple values at once, separate them with English commas ',' or assign them in multiple lines. [\*] indicates all\-row permissions. To assign no values, leave the field empty (see the example below).

5. When the data or table structure of a dataset changes, user attributes will change accordingly. Please ensure the stability of the dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/962786fd8c99492ab6b3813602486755~tplv-goo7wpa0wc-image.image) </span>

    &nbsp;


<span id="_3-2-edit-attribute-field-values"></span>
## 3.2 Edit attribute field values

<span id="_3-2-1-单个编辑"></span>
### 3.2.1 Edit a single value

(1) Go to the user attributes page, search for the specific user attribute column (such as Region), and locate the corresponding attribute value cell (such as Shanghai).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4abf894a707942fda79d0fb50b485ab5~tplv-goo7wpa0wc-image.image) </span>

(2) Move the mouse over the attribute value cell and click the edit button that appears on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c7b5c98cd8a47f3b59eddaeea57c0b3~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the attribute value according to the editing rules below, click Save, and the user attribute value will be successfully updated.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea0c4f022acb49da9c8f78a4557c73f0~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bddced50a1e44759553dcccf38a3879~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-批量编辑"></span>
### 3.2.2 Batch edit

(1) Go to the user attributes page and click [Batch Update Attributes] to open the batch update attributes dialog box.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b09cd4f8b8e42c7b25b853bea0e78e0~tplv-goo7wpa0wc-image.image) </span>

(2) Click Download Template.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fb150dc57a04321b5c78153fd191657~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) Fill in the values for the user attribute columns to be updated according to the instructions and examples in the template document.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/895e4a4e8c574851b154d3fb566de189~tplv-goo7wpa0wc-image.image) </span>

(4) After completing the template, drag the file or click the Upload button to upload and preview the file.

(5) After confirming there are no issues, click [OK] to upload and update, as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bddced50a1e44759553dcccf38a3879~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-属性字段应用"></span>
## 3.3 Attribute field application

User attribute information is an essential source of dynamic values for row\-level data permissions. For private deployments, if the system administrator has configured custom attributes in the account management module of the system configuration, then project administrators or resource owners can view global user attributes when configuring row and column permission rules.

<span id="_3-4-用户属性下载"></span>
## 3.4 User attribute download

For user attributes, all attributes can be downloaded except for default sensitive attributes such as name, email, department, city, and other similar attributes. Click the download button in the upper right corner of the interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e283d0dd00242079b27b930daeeb61a~tplv-goo7wpa0wc-image.image) </span>
