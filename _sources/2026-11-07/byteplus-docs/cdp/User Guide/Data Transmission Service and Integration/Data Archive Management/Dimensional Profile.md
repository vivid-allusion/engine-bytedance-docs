---
title: "Dimensional Profile"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Dimensional_Profile"
---

<span id="_1-功能概述"></span>
# 1. Functional Overview

In this functional module, users can supplement the attribute values around a dimension object in the main file. They can associate data from multiple subjects to build associative queries.

<span id="_2-使用前提"></span>
# 2. Prerequisites

**Administrator** and those with permission to view or add, delete, and modify data files in **Project Center\-Modules\-Data Archive Management** can use this module.

<span id="_3-数据集要求"></span>
# 3. Data Set Requirements

<span id="_3-1-概述"></span>
### 3.1 Overview

The core content of the dimensional data model supplements the attribute values around a dimension object in the main file. It does not strictly belong to a single subject and can construct query logic that associates data from multiple subjects, similar to the structure of a subject attribute table.

<span id="_3-2-数据样例"></span>
### 3.2 Example


|Subject Key Field |Date |Subject |Project Center |Project Center |
|---|---|---|---|---|
|Dimension Primary Key Field |Partition Date |Dimension Attribute 1 |Dimension Attribute 2 |Dimension Attribute 3 |
|10001 |2022\-01\-01 |Air Conditioner |Expensive |Shanghai |
|10002 |2022\-01\-01 |TV |Cheap |Shanghai |
|10003 |2022\-01\-01 |Water Heater |Expensive |Beijing |
|10004 |2022\-01\-01 |Bicycle |Cheap |Beijing |


<span id="_3-3-数据结构及字段要求"></span>
### 3.3 Data Structure and Field Requirements


|Field |Field type |Instruction |
|---|---|---|
|* Dimension primary key field |Numerical type/Text type |* Required field<br><br>* Dimension primary key fields must be unique and deduplicated |
|* Partition date |Date type |* Required field<br><br>* Automatically generated or designated partition field, no manual configuration required |
|Dimension attributes |Numerical/text/time/array multi\-values do not support map types |* Optional field<br><br>* Attribute fields revolve around the primary keys of dimensions, such as age/gender, used to directly generate user profiles<br><br>* Attribute fields support numerical/text/time/array multi\-values, text types support setting enumeration fields, such as city code configuring city names<br><br>* Attribute fields do not support special fields like maps |


<span id="_3-4-圈选组件使用逻辑"></span>
### 3.4 Usage Logic of the Selection Component

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_49e827510287211ac6d147d33a3e59f7.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Primary keys in dimensions do not need to undergo IDMapping conversion</div>


2. <div data-tips="true" data-tips-type="tip">Dimension primary keys must ensure uniqueness for deduplication</div>


3. <div data-tips="true" data-tips-type="tip">Can be a partitioned table, but must follow full partition logic, i.e., saving the latest full data daily</div>


4. <div data-tips="true" data-tips-type="tip">Product linkage Finder metadata and Finder business object tables do not currently support associations</div>



<span id="_4-操作说明"></span>
# 4. Operation Instructions

<span id="_4-1-查看维度档案列表"></span>
### 4.1 View Dimension Archives List

> Attachment properties of a specific business object under the main archive can be associated with the primary key field of the business object's main properties to construct a related query.


Show information such as attribute name, display name, description, etc., and support quick search.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d9c902cd379beda16a28574d8ef414a.png) </span>

<span id="_4-2-上传维度字典"></span>
### 4.2 Upload Dimension Dictionary

Support uploading dimension dictionary files to translate attribute values, turning hard\-to\-read numbers into more readable text. Click **View** button to support **single or batch upload**.


* Support for adding individual configurations is limited to 1000 rows.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dcc2135307544b48804fc0f453a5f45e.png) </span>Bulk Upload:


* Please use the UTF\-8 encoding format, and the file format should be either csv or xlsx.

* One corresponding relationship per line, separated by commas in English, in the format: original value, translated value.

* The content should be less than 1000 rows or 10Mb.

* Upload modes supported: Overwrite (the content uploaded in bulk will completely replace the existing content), Append (based on the existing content, bulk add configurations of enumeration values – if there are duplicates in the original values, the latest configuration will be used).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f512707bfd919c752caf0bbd2781c9a.png) </span>

<span id="_4-3-主体档案关联"></span>
### 4.3 Subject Profile Association

Click the **Subject Profile Association \- Create Association** button to access the configuration page, where you can set the associated profile type and fields, supplementing more dimensional information related to that field.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30a88835f2ebe3709b8b123c5b238b4c.gif) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Each subject profile field can only be associated with one dimension table. If the field is already associated, it cannot be associated again.</div>


* <div data-tips="true" data-tips-type="warning">Only integer/float numerical data types of profile fields can be mutually compatible, where String and integer are compatible, while others are not. If the field's data type does not match the dimensional profile field type, the association relationship cannot be built.</div>
