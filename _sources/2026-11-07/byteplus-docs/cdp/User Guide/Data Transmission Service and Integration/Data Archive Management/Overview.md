---
title: "Overview"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Overview__"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

In the Data Archive Management module, it supports registering and managing **raw data** into **business\-readable and understandable business data content** according to different business types and formats. Downstream applications can efficiently call data based on the agreed format, businesses can quickly understand data through redefined naming and interpretation, enabling rapid identification and application of data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only data that has been registered in data archive management can be used for subsequent activities such as tag creation and group selections.</div>


The data archive list is in a flat structure, clicking on the archive name will redirect to the data archive details page.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f33ca6794d234fee904b33bf31558f1c~tplv-goo7wpa0wc-image.image" width="3268px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a99f063d59834fee973cee059dbe2f1d~tplv-goo7wpa0wc-image.image" width="3272px" /></div>


<span id="_2-使用前提"></span>
# 2. Prerequisites

Only **administrators** and those with the permission to **view or add/remove data archives in the Project Center\-Modules\-Data Archive Management** can use this module.

<span id="_3-名词解释"></span>
# 3. Glossary


|**Product Terminology** |**Explanation** |
|---|---|
|Data Archive |Data archiving is the abstraction of a data set into a data model understandable by business personnel, containing four types: subject attributes, behavioral events, business details, and dimension archives. |
|Subject Attribute Archive |Describes the most basic attribute information about the subject, such as ownership, interests, preferences, providing a profile of "who am I," including gender, age, membership level, etc. |
|Behavioral Event Archive |Describes behavioral information based on what users do in certain scenarios at certain times, such as clicks, purchases, shares, and other behavioral events. |
|Business Detail Archive |Based on detailed data records generated in actual business production, it describes the details of business processes, such as order details, after\-sales repair records. |
|Dimension Archive |Dimension archives are extensions of metadata for a specific subject object. For example, the user subject includes the "user's favorite product" attribute. The product dimension file contains metadata descriptions of the product, such as category, price, etc. After linking the dimension file with the user subject file, more detailed product preference information about the user can be understood. |


<span id="_4-配置流程"></span>
# 4. Configuration Process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1810e14d2ac606d568e89c35b986bc11.png) </span>

<span id="_5-数据结构规范"></span>
# 5. Data Structure Specification

> Unique Primary Key: Deduplicate around a specific ID, with one line of data per ID

> Incremental: Add new data every day

> Full Load: Add all historical data + new data every day

> Real\-time: Update in real\-time

> Offline: Update on a scheduled basis, daily updates, no support for hourly updates at the moment



|Data Archive Type |Whether to limit partitioned tables |Whether to limit primary key uniqueness |Whether to limit incremental/full |Whether to limit real\-time/offline |
|---|---|---|---|---|
|Subject Attributes |Partition Table |OneID Unique |Full Table |Only offline (daily) |
|Business details |Partitioned table |No restriction, can have multiple |Incremental table (subsequent optimization supports full amount) |Real\-time/offline (daily) |
|Behavioral events |No restriction |No restriction, can have multiple |Incremental table |Real\-time/Offline (Daily) |
|Business Dimension |Partitioned Table |Unique Dimension Primary Key |Full Table |Offline Only (Daily) |


<span id="_6-操作说明"></span>
# 6. Operation Instructions


|**Functionality** |**Function Description** |
|---|---|
|**Data Archive Management** |Register and manage underlying data in different business types and formats to make it readable and understandable for business purposes, enabling quick identification and application of data. |
|**Subject Profile** |Define and manage data archive information for subjects, including subject attributes, detailed data, behavioral events, etc., defining the fields of data sources as interpretable data characteristics under different subjects for business applications. |
|**Dimension Archive** |Supplemental attribute values around a dimension object within the subject profile, enabling related queries to be built for data across multiple subjects. |
|**Table Template** |Built\-in automotive industry table templates in the system to improve data processing and management efficiency. |


<span id="_7-特殊情况说明"></span>
# 7. Special Cases Instructions

> If a user simultaneously purchases and uses the Customer Data Platform VeCDP and the Growth Analysis DataFinder product, and they are deployed on the same cluster, the following will provide special instructions for the usage scenarios of the two products in a linked scenario:


<span id="_7-1-概念对齐"></span>
## 7.1 Concept Alignment


|Customer Data Platform VeCDP |DataFinder product for Growth Analysis |Remarks |
|---|---|---|
|Subject Attributes |User Attributes | |
|Behavioral Events |General Events/Virtual Events |Behavioral Events, General and Virtual are types of events |
|Event Attribute |Event Attribute/Virtual Attribute |Event Attribute, General and Virtual are types of events |
|Business Dimension |Business Object | |


<span id="_7-2-联动能力"></span>
## 7.2 Linkage Capability


|Linkage |Description |
|---|---|
|Data Storage and Query |DataFinder data does not need to be stored repeatedly. When VeCDP uses DataFinder, it directly queries DataFinder data |
|Metadata Synchronization |The metadata of DataFinder's General Events/Virtual Events/Event Attributes/Virtual Attributes will automatically synchronize to VeCDP for use |
|Metadata Usage Restrictions |1. The metadata of DataFinder cannot be edited within VeCDP. If editing is required, it should be done uniformly within DataFinder.<br><br>2. DataFinder's behavioral attributes cannot be used to build query relationships with VeCDP's business dimensions<br><br>3. DataFinder's business objects also cannot be used to build query relationships with VeCDP's core metadata<br><br>4. DataFinder's real\-time streaming data is not currently system\-integrated. If using VeCDP's real\-time rules engine, Finder kafka data can be manually accessed through visual modeling |


<span id="6f5b7c19"></span>
# FAQ

**Q1: Does VeCDP support controlling the resource permissions of data archives? Does it support controlling row\-level permissions for data archive resources (i.e., specifying that only certain users can use specific data archives)?** 

In VeCDP, data archives/data sources are visible to all users by default, but users can achieve finer access control by configuring permission rules:


1. Go to VeCDP\-Project Center\-Permissions\-By content management.

2. On the data row permission configuration page, create a new rule. In the Node Configuration\-Data Resource Type, select "Detail Table/Main Attribute/Action" and configure to exclude certain data archives to control access to data archive resources at a granular level.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c67067c9c6d4929bf5776ead69aae4f~tplv-goo7wpa0wc-image.image) </span>

   \*Note: The ability to configure permissions directly based on the granularity of "data archives" resources will be optimized in future versions.
