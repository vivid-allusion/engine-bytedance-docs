---
title: "Manual Entry of Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Manual_Entry_of_Tags"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

CDP supports creating manually entered tags.

<span id="_2-功能介绍"></span>
# 2. Function Introduction

Common applications of manually entered tags: sales and in\-store customer face\-to\-face communication, obtaining real information and labeling specific tags for the customer through their mobile phones, such as marital status \- married; whether there are children \- yes; another sales/operations colleague retrieves this customer's tag information in personal profiles/profile insights.

<span id="_3-使用限制"></span>
# 3. Usage Restrictions

Project administrators need to grant users permissions for "labeling system" under Project Center \- Permissions \- Content Management \- Modules to create new labels.

<span id="_4-操作步骤"></span>
# 4. Operational Steps

Go to the **Labeling System** module, click the **Create Label** button, select **Manually Enter Label** to enter this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4974a3ee57017d33a606e5b0aa7fd90.png) </span>

<span id="_4-1-配置基础信息"></span>
## 4.1 Configure Basic Information


* Tag name: The name of the newly created tag (up to 100 characters; tag names cannot be duplicated within the same project)

* Path: Select the folder category where this tag is located


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Create Tags \- The path involves two switches:</div>



1. <div data-tips="true" data-tips-type="tip">Group switch: In the Project Center \- Group Configuration \- Function Configuration, there is an <strong>authorization control for tagging directories</strong> switch, default to Off. Once turned on, strict permission control will be applied to the "directory" during tag creation, with those without <strong>label tree editing</strong> permission only allowed to place in "Uncategorized".</div>


   <div data-tips="true" data-tips-type="tip">Module Switch: Label Directory Access Control switch is turned on, users without Edit Label Tree permission will default to the "Uncategorized" path when creating a new tag (project administrators can authorize users in a i=4\>Project Center\-Permissions)   </div>
   

* Tag value types: The system supports five types of tags, including text, integer, decimal, multi\-value, and date.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Text Type: Used for tags with text values, commonly used for labels such as name, username, city, etc.</div>


* <div data-tips="true" data-tips-type="tip">Integer Type: Used for tags with integer values, commonly used for labels such as age, click count, visit count, etc.</div>


* <div data-tips="true" data-tips-type="tip">Decimal Type: Used for tags with decimal values, commonly used for labels such as cost, percentage, etc.</div>


* <div data-tips="true" data-tips-type="tip">Multi\-Value Type: Used when tags have multiple values, commonly used for labels such as interests, favorite topics, etc.</div>


* <div data-tips="true" data-tips-type="tip">Date Type: Used for tags with date values, commonly used for labels such as date of birth, update date, etc.</div>


* Separator: Supports 3 types of separators, comma, space, newline

* Online Service Switch: If this tag needs to be used in other systems, please turn on the online service switch.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b494f4d8625abaea7cdb261e7b5a7b6.png) </span>


<span id="_4-2-上传数据"></span>
## 4.2 Upload Data

After completing the basic information configuration, proceed to the next step of uploading data, and select the type of ID to be uploaded:

Files uploaded must meet the following requirements:


* Support file extensions: .csv, .xlsx, up to 100M

* The first column header must be "User ID", and the second column header must be "Tag Value"

* Upload field values starting from the second row by default

* Only reads data from the first sheet

* Does not support merging cells

* Unique user IDs are required for uploads

* If there are abnormal tag values during the upload, it will automatically skip and prioritize completing the upload

* If you want to remove a tag value for a particular ID:

   * Delete tag values by using an API

   * For users previously tagged, if you need to remove them through the web interface, re\-upload tag values as "None"


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba28ef27d94f5a14e579e9d82f3c56c6.png) </span>

<span id="_4-3-查看标签详情"></span>
## 4.3 View Tag Details

After uploading, you can view the current tag distribution, historical details, and operation records on the tag details page. For abnormal upload data, you can check in **upload records**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8952ea05478e5aef517a052a777ddf29.png) </span>

<span id="257962c1"></span>
## 4.4 Modify Edit

After creating manual tags, if you edit it, you can choose two ways of modification:


1. Override: The tag data of the newly uploaded file will overwrite the previous old data.

2. Remove: Remove the tag data in the newly uploaded file.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e63c0925435e424aa077f9242e11a053~tplv-goo7wpa0wc-image.image) </span>

Click to complete the modification.
