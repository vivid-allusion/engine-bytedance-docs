---
title: "DataFinder Data Integration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/DataFinder_Data_Integration"
---

<span id="_1-概述"></span>
# 1. Overview

DataWind supports direct integration with BytePlus DataFinder (hereinafter referred to as Finder). Behavior analytics data collected by Finder can be analyzed directly, or associated with business data for analysis, providing more analytical insights and conclusions.

**Prerequisites**:


* For private deployment of DataWind, the corresponding Finder must also be privately deployed. Both products need to be deployed in advance.

* For SaaS DataWind, the corresponding Finder must be SaaS. To obtain a Finder account in advance, the primary account used to apply for both DataWind and Finder must be the same primary account.

* **Version requirements:** 

   * Private deployment: Finder must be version V4.3.0 or above, and DataWind must be version V2.50.0 or above.

   * SaaS: Finder must be the SaaS cloud\-native version.


<span id="_2-功能说明"></span>
# 2. Feature description

<span id="_2-1-数据连接步骤"></span>
## 2.1 Data connection steps

(1) Click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Create Data Connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) Click Application Data Source on the left, and select "BytePlus Growth Analytics DataFinder".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0795c71e54a493682f1550c561da63e~tplv-goo7wpa0wc-image.image) </span>

(3) In the basic information of the data connection, select the corresponding application from the dropdown and click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f29e40c888b4afea56b367deb753dc6~tplv-goo7wpa0wc-image.image) </span>

(4) Click the One\-Click Create Dataset button, and the system will automatically create the dataset.

(5) In the pop\-up window after successful creation, click "View Here" to jump to the corresponding dataset and view details.

<span id="_2-2-在数据连接环节可选择的应用范围"></span>
## 2.2 Application scope available during data connection


* For private deployment, there is a one\-to\-one relationship between projects. Each project space has one selectable application.

* For the SaaS version, all applications created under the primary Volcano account can be selected.


<span id="_2-3-用户权限限制"></span>
## 2.3 User permission restrictions

Who can create a Finder data connection?


* No distinction between private deployment or SaaS

* Authorization for the SQL custom query feature is managed on Finder. Users who are authorized to use this feature can create Finder data connections in DataWind; those who are not authorized cannot.


<span id="_2-4-接入表结构说明"></span>
## 2.4 Description of integrated table structures


* DataWind can connect to the events, users, and items tables from Finder.

* The table structure information for connected Finder data can be viewed in the dataset details.

* For the mapping of connectable fields to Finder sources, see [Data Format](https://www.volcengine.com/docs/6285/66211).

* For detailed parsing instructions, see the events table, users table, and items table in [Field Description](https://www.volcengine.com/docs/6285/66211).

* When using the event_params.loc_city_id field in the events table, note that this field must be converted before it can be used.

   * Click Field Configuration in the dataset to go to the field configuration details page, then click Add Field.

   * Enter the following expression in the field expression box, and click Save.


`dictGetOrDefault('default_user_dictionary', 'target_value', tuple('loc_city_id', ifNull(event_params.loc_city_id, 'null')), 'unknown')`


* In subsequent applications of the events table, when the city field needs to be used, this field can be used directly.

* Parsed fields of the events table

   The event_params.xxx.yyy field, user_profiles.xxx field, and item_profiles.xxx.yyyy field will be parsed into multiple fields based on the actual reported data and definitions. The following is an example of parsing the event_params.xxx.yyy field.


<span id="_2-5-功能限制"></span>
## 2.5 Feature limitations


* Only direct connection is supported for dataset extraction.

* The dataset does not support join or union operations.

* Visual modeling capability is not supported.
