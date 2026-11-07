---
title: "Preference Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Preference_Tags"
---

<span id="_1-产品概述"></span>
# 1. **Product Overview**

Preference tags support grouping and sorting by an attribute of completed events, selecting the TOP groups as tag values.

<span id="_2-常见应用场景"></span>
# 2. **Common Usage Scenarios**


* Mark x categories most loved by customers in orders with amounts exceeding 100 yuan in the past week

* Mark the top x number of users in cities corresponding to the completed purchase events in the last 3 days


<span id="_3-操作步骤"></span>
# 3. **Operating Steps**

Go to the **Label System** module, click the **Create Label** button, select **Preference Tags** to access this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb7224c08d543f5aac3e26f2bb5b3df8.png) </span>

<span id="_3-1-配置基础信息"></span>
## 3.1 Configuring Basic Information


* Tag name: Name of the new tag (up to 100 characters; within the same project, tag names must be unique).

* Path: Select the folder category where this tag is located


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Creating a Tag \- The path involves two switches:</div>



1. <div data-tips="true" data-tips-type="tip">Group Switch: In the Project Center \- Group Configuration \- Function Configuration section, there is a <strong>label directory access control</strong> switch, which is off by default. When turned on, strict permission control will be applied to "directory" when creating labels, and those without <strong>edit label tree</strong> permission are only allowed to place them in "Unclassified".</div>


2. <div data-tips="true" data-tips-type="tip">Module switch: <strong>Label Catalog Permission Control</strong> switch, after turning on, users without <strong>Edit Label Tree</strong> permission will default to the "Uncategorized" path when <strong>creating a new label</strong> (project administrators can authorize users in <strong>Project Center\-Permissions</strong>).</div>


* Description: Input tag description, for reference by other tag users.

* Calculation Type: Optional offline or real\-time calculation

* Update type: Optional scheduled update or manual update

* Update frequency: For scheduled updates, set the update frequency and time, supporting daily/weekly/monthly synchronization

* Storage rule for calculation results: When updated regularly, you can set the number of historical versions to retain. Excess historical versions beyond the limit will be deleted the next day.

   * If **Unlimited** is selected here, the default value will be based on the group settings;

   * If you select specify a duration here, specify the number of recent result versions to keep. For example, input 4 \- by day, keep the last 4 days; by week, keep the last 4 weeks; by month \- keep the last 4 months of results. The smaller value in the group settings prevails.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): the data lifecycle, which is the time that makes stored data invalid;</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c4384f6c84441ca5caf6a5f2d3e508e.png) </span>

<span id="_3-2-配置标签规则"></span>
## 3.2 Configuration Label Rules


1. When the table type selected is a behavior table, the rule format is as follows: `Partition Date + Event + (Filter Conditions) + Most Frequent Value/Max Value + Top xx + Attribute Field`

* Supports three date formats when selecting a date: dynamic date, fixed date, and single date.

* Data types corresponding to the highest frequency: all types are optional.

* Data types corresponding to the maximum value: only numerical/date types can be selected.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d294d1f5a0f6eda63761c75ce92c1e1e.png) </span>

2) When the table type selected is a detail table, the rule format is as follows: `Partition Date + Most Frequent Value/Max Value + Top xx + Attribute Field + (Filter Conditions)`

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9cf3cc2cbd9b4586890f412ea066e74.png) </span>

<span id="_3-3-查看标签详情"></span>
## **3.3 View Tag Details**

Click on estimated number of people to preview the tag calculation results. If the settings are correct, click **complete creation** to complete the creation of the current tag.

You can view the current tag distribution, historical details, and operation records in the tag details page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_383ae4912ea228dfeb79801e335501e0.png) </span>
