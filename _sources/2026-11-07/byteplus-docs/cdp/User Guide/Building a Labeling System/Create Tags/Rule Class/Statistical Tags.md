---
title: "Statistical Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Statistical_Tags"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

Supports creating statistical tags, where the number of times users complete tasks is used as tag values. Commonly used for calculating statistical results, such as the total number of views of product A in the last 30 days.

<span id="_2-操作步骤"></span>
# 2. Operation Steps

Go to **Labeling System** module, click on the **Create New Tag** button, select **Statistical Tags** to enter this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9534733cc871d25af2971bcc7ddaf10c.png) </span>

<span id="_2-1-配置基础信息"></span>
## **2.1 Configure Basic Information**


* Tag Name: The name of the new tag (within 100 characters; tag names cannot be duplicated within the same project).

* Path: Select the folder category where the tag is located


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are two switches involved in the new tag creation path.</div>



1. <div data-tips="true" data-tips-type="tip">Group Switch: In Project Center \- Group Configuration \- Function Configuration, there is a <strong>Tag Directory Permission Control</strong> switch. It is off by default. When turned on, strict permission control will be applied to "Directory" when creating tags. Users without <strong>Edit Label Tree</strong> permission are only allowed to place tags under "Uncategorized".</div>


2. <div data-tips="true" data-tips-type="tip">Module Switch: <strong>Tag Directory Permission Control</strong> switch, when turned on, users without <strong>edit tag tree</strong> permission will default to the "Uncategorized" path when <strong>creating a new tag</strong> (project administrators can authorize users in <strong>Project Center\-Permissions</strong>)</div>


* Description: Input tag description for reference by other tag users.

* Calculation type: optional offline calculation or real\-time calculation

* Update type: Optional scheduled update or manual update

* Execution Frequency: When updating regularly, you need to set the update frequency and time, supporting daily/weekly/monthly synchronization.

* Calculation result storage rule: When updating regularly, you can set the number of historical versions to be retained, and any versions beyond the limit will be deleted the next day.

   * If **unlimited number** is selected here, it will follow the [标签系统表TTL长度](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c8988a)group configuration.

   * If you choose **custom TTL** here, it will follow the setting of keeping the number of recent versions (when the **custom TTL** is a single tag\> the TTL length of the corporate tag system table, based on the TTL length of the corporate tag system table);


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): Data lifecycle, which refers to the time after which stored data expires.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6cfc7fd5d8fd8df9248643b9dc6f7b2d.png) </span>

<span id="_2-2-配置标签规则"></span>
## **2.2 Configuration tag rules**

Supports selecting behavior tables or detail tables. When the user selects the behavior table, the configuration of statistical rules supports:


* When filtering dates, it supports dynamic dates, fixed dates, and a single date.

* Logical judgment only supports selecting "performed" a certain event.

* Statistical methods support total count, days, consecutive days, summation, average, maximum, and minimum.

* Supports filtering field aggregation and condition judgment.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38b6d1d7b865812ca4acf07ee3bdb0f5.png) </span>When users select the detailed table, during the configuration of statistical rules, it supports:


* When filtering dates, dynamic dates, fixed dates, single dates are supported;

* Supported statistical methods include total count, unique count, summation, average, maximum, minimum values;


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The calculation method of the average value: grouping by base_id, then summing the actual amount, and finally, taking the statistical algorithm (average value) as the tag value.</div>



* Supports judging conditions after aggregating filtered fields;


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9ce66dd58b41b1315ed54c4610f6d7a.png) </span>

<span id="_2-3-配置标签展示方式"></span>
## **2.3 Configuration of Tag Display Method**

supports two display methods: displaying by discrete numerical values and by numerical range:


* Split by discrete numerical values: directly use the calculated indicator result value as the tag value (performance may decline when the tag value is a discrete numerical value, used for user grouping and insight).

* Split by numerical range: set user stratification labels based on the threshold range of the calculated indicator result value.

   * During the initial configuration, you can set infinite intervals as [\-∞, empty], [empty, +∞]; once the infinite intervals are deleted, they will no longer be displayed

   * The names within the hierarchical columns cannot be repeated.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_208ead4c527bd86701c9fdf8678c0b0a.png) </span>Click **Create Complete** to complete the creation of the current tag. You can check the distribution of current tag participants, historical details, and operation records on the tag details page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4e0312358ef90a80b8e188d481dbf761.png) </span>
