---
title: "First and Last Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/First_and_Last_Tags"
---

<span id="_1-产品概述"></span>
# Product Overview

Supports first and last occurrence tags, which use the user's first/last completion of a certain event's time, attributes, etc., as tag values. The supported features for calculation include:


* The first/last occurrence of a specific event within a designated period [exact time point].

* The first/last occurrence of a specific event within a designated period [days ago from today].

* The first/last occurrence of a specific event within a designated period [event attributes].


Common usage scenarios include: The time of first activation of an app, The number of days since the last order, The channel of the last data submission.

<span id="_2-操作步骤"></span>
# 2. Operating Steps

Go to the **labeling system** module, click the **create label** button, select **first and last label** to enter this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a3517f35d4384d86419457f1debc2143.png) </span>

<span id="_2-1-配置基础信息"></span>
## 2.1 Configure Basic Information


* Label Name: The name of the new label (within 100 characters; under the same project, label names cannot be repeated)

* Path: Select the folder classification where the label is located


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">New tag \- The path involves two switches:</div>



1. <div data-tips="true" data-tips-type="tip">Group switch: In the project center \- Group Configuration \- Function Configuration, there is a <strong>Tag Directory Access Control</strong> switch, defaulting to off. When turned on, strict permission control will be applied to the "directory" when creating tags, allowing only those without <strong>Edit Tag Tree</strong> permission to place tags under "Uncategorized."</div>


2. <div data-tips="true" data-tips-type="tip">Module switch: After the <strong>Tag Directory Access Control</strong> switch is turned on, users without <strong>Edit Tag Tree</strong> permission will default to the "Uncategorized" path when <strong>creating a new tag</strong> (project admins can authorize users in <strong>Project Center \- Permissions</strong>).</div>


* Description: Enter label description for reference by other label users

* Calculation Type: Optional offline calculation or real\-time calculation

* Update Type: Optional scheduled update or manual update

* Execution Frequency: When setting the scheduled update, specify the update frequency and time, supporting daily/weekly/monthly synchronization

* Calculation result storage rule: When updating regularly, you can set the number of historical versions to be retained. The excess historical versions will be deleted the next day.

   * If "unlimited quantity" is selected here, it will follow the group configuration.

   * If "customized TTL" is selected here, it will follow the number of recent versions to be retained (when the custom TTL of a single tag exceeds the TTL length of the group's tagging system table, it will be based on the TTL length of the group's tagging system table);


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): Data lifecycle, meaning the time to make the stored data invalid;</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dd050b35c9960c04efce8b3dd80f8340.png) </span>

<span id="_2-2-配置标签规则"></span>
## 2.2 Configure tag rules

Support selecting action tables or detailed tables. When the user selects an action table, support configuring statistical rules:


* When filtering dates, support dynamic dates, fixed dates, and single dates;

* Logical judgment only supports selecting the completion of certain events;

* Support adding filter conditions;

* Calculating features support specific time points of first/last occurrences, days from today, and attributes.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_28cd73517fd39702779fb3846090d16e) </span>When users choose the details table, you can configure the statistical rules:


* When filtering dates, support dynamic dates, fixed dates, and single dates;

* The calculation feature supports selecting the first/last occurrence of the [attribute] based on the reference time;

* Support adding filter conditions;


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4e22da98131bf31c3c53950d8fc951a8) </span>

<span id="_2-3-查看标签详情"></span>
## 2.3 View Tag Details

Click **Complete Creation** to complete the creation of the current tag. In the tag details page, you can view the current tag's distribution of people, historical details, and operation records.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0c7301e6061328d695f1e2c443f1198.png) </span>
