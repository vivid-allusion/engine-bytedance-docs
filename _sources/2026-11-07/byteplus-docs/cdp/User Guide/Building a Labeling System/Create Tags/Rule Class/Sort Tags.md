---
title: "Sort Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Sort_Tags"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

Supports creating sorting tags.

<span id="_2-常见应用场景"></span>
# 2. Common Application Scenarios

Existing labels [Gender\-Manual] [Gender\-Inference], generate a more accurate label [Gender] based on priority: first obtain the label value of the user [Gender\-Manual], if empty, then obtain the user's [Gender\-Inference]

<span id="_3-操作步骤"></span>
# 3. Operation Steps

Go to **Labeling System** module, click the **Create New Label** button, select **Sort Label** to enter this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c59eb0bff8aa5571a5050f02c92eb23b.png) </span>

<span id="_3-1-配置标签基础信息"></span>
## 3.1 Configure Basic Label Information


* Label Name: The name of the newly created label (within 100 characters; label names cannot be duplicated under the same project)

* Path: Select the folder category where this tag is located.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Create a new tag \- Path involves two switches:</div>



1. <div data-tips="true" data-tips-type="tip">Group Switch: In Project Center \- Group Configuration \- Function Configuration, there is an <strong>authorization control for tag directories</strong> switch, which is off by default. When turned on, strict permission control will be applied to the "directory" when creating tags. Users without <strong>tag tree edit</strong> permission are only allowed to place tags in "Uncategorized."</div>


2. <div data-tips="true" data-tips-type="tip">Module Switch: When the <strong>label directory permissions control</strong> switch of the module is turned on, users without the permission to <strong>edit the label tree</strong> will default to the "Uncategorized" path when <strong>creating a new label</strong> (project administrators can grant users authorization in <strong>Project Center\-Permissions</strong>).</div>


* Description: Input label description for reference by other tag users.

* Calculation type: optional offline calculation or real\-time calculation

* Update type: Optional scheduled updates or manual updates

* Execution frequency: When setting the update frequency and time for timed updates, support synchronization on a daily/weekly/monthly basis.

* Calculation result storage rule: When updating regularly, you can set the number of historical versions to retain and the excess historical versions beyond the limit will be deleted the next day.

   * If you select **unlimited quantities** here, it will follow the [标签系统表TTL长度](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c8988a)group configuration；

   * If **Customize TTL** is selected here, the number of recent versions reserved will follow the TTL length set here (when the **Customize TTL** tag is a single tag in the group's tag system table TTL, the TTL length of the group's tag system table will prevail);


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): Data lifecycle, i.e., the time for stored data to expire.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6dce71b5dae7e06675544642dfadebaf.png) </span>

<span id="_3-2-配置标签规则"></span>
## 3.2 Configuration Tag Rules

Preselection of label types, drag to adjust the priority of label values (only supports creating logical tags of the same type)

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2dce88de56a786f878870185d26f56ff) </span>

<span id="标签值类型"></span>
#### Label value type

The system supports a total of 5 types of labels: text, integer, decimal, multi\-value, and date.


* Text type: used for text\-based label values, commonly used for labels such as name, username, city, etc.

* Integer type: used for integer\-based label values, commonly used for labels such as age, click count, visit count, etc.

* Decimal type: used for decimal\-based label values, commonly used for labels such as cost, percentage, etc.

* Multi\-value type: used when there are multiple values for a label, commonly used for labels such as interests, favorite topics, etc.

* Date type: used for date\-based label values, specifically for dates, commonly used for labels such as date of birth, etc.

* Date\-time type: used for date\-time\-based label values, specific to hours, minutes, seconds, commonly used for labels such as update date, etc.


<span id="选取标签字段并排序"></span>
#### Select label fields and sort them


* Select the required tags or user attributes on the left side.

* You can view the selected tags on the right side. Change the order by dragging to adjust the priority.


<span id="预估人数"></span>
#### Estimated number of people

Assist in judging whether the distribution of tag values meets expectations.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_caad9acc41d6dd0ad8da9779bcc35200.png) </span>

<span id="_3-3-查看标签详情"></span>
## 3.3 View tag details

Click **Complete creation** to finish creating the current tag. You can view the distribution of label value, historical details, and operation records on the tag details page. Below the tag preview, you can click on the tag rules to view details of sub\-tags.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f9b3128134b895f02efce6ed3066dad.png) </span>
