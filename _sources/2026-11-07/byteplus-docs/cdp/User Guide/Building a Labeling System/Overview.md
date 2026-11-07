---
title: "Overview"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Overview___"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

Tags are the foundation of the Customer Data Platform, and user segmentation, group insights, and marketing applications all rely on tags. Users need to build a tag system suitable for their own business scenarios, logic, in order to provide precise operation and precise marketing services for the enterprise, thus further exploring potential business value.

Within this module, users can perform operations such as query, create, edit, and delete around tags to build a well\-structured tagging system that serves business goals.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8bf0a100ed8a5fe624b7bbadb7e86912.png) </span>

<span id="_2-使用前提"></span>
# 2. Prerequisites for Use


* Project administrators need to enable the corresponding users to access the Labeling System module in the Project Center\-Permissions. Once enabled, users can use this feature.

* Users need to complete the preparatory work of data integration in the Data Fusion module before they can build tags in this module.

* Tag construction needs to be within the total resource quota. When the resource quota is used up, users need to delete tags or segments to release resources before they can create new tags, or contact your account manager to purchase additional computing resources.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6904c2234326381d74ed5e0ada9470fb.png) </span>


* **Note: Only routine updated tags and segments will consume resource quota. Detailed consumption rules are as follows:** 



|**Resource type** |**Resource construction method** |**Update method** |||
|---|---|---|---|---|
|||**Manual update** |**Routine update** |**Real\-time update** |
|Tag |Rules tag |Consumption |Consumption |Not counted here in real\-time resource restrictions |
||First and last tag |Consumption |Consumption ||
||Statistical tag |Consumption |Consumption ||
||Preference Tags |Consumption |Consumption ||
||Sorting Tags |Consumption |Consumption ||
||Operation Tags |Consumption |Consumption ||
||Lifecycle Tags |Consumption |Consumption ||
||RFM Tags |Consumption |Consumption |/ |
||SQL Tags |Consumption |Consumption |According to real\-time resource constraints, do not consume statistics here |
||Import Tags |/ |Consumption |/ |
||Manually enter tags |Consumption |/ |/ |
||Intelligent outbound call tags |/ |Consumption |/ |
||Intelligent Listening Tagging System |/ |Consumption |/ |
||Custom Model Tags |Not Consume |Not Consume |/ |
|Segmentation |Grouping Rules (Private Domain) |Not Consume |Consumption |Based on real\-time resource constraints, statistics are not consumed here. |
||Upload crowd package |Not Consume |/ | |
||Private domain Lookalike crowd creation |Not Consume |/ | |
||Cluster model\-generated crowd |Not Consume |/ | |
||Insight report exported crowd |Not Consume |/ | |
||Subject transformation crowd |Not Consume |Consumption | |
||Exporting population through multidimensional feature analysis |Not Consume |/ | |
||Linked product sync population (e.g., ABI/Finder sync population) |Not Consume |/ | |


Explanation: Sub\-packages are not involved in the calculation; "/" indicates functions that are not supported, with logical explanations that require no consumption.

<span id="_3-基本概念"></span>
# 3. Basic Concepts


|Concept |Explanation |
|---|---|
|Label |Based on data such as behaviors/attributes, created with business guidance significance based on business logic or model capabilities, in an enumerable form of label values |
|Tag System |Composed of tags, presenting and managing the content of tags in a structured manner, including the number, classification, hierarchical relationships of tags. |
|Full Tags (Mautag) |The total number of all users under the group, updated daily. |
|Text\-based Tag Values |Used for tags with text\-based values, such as name, username, city, etc. |
|Integer\-based Tag Values |For tags with integer type values, this type of tag is commonly used for labels such as age, click count, store visit count, etc. |
|Decimal\-based Tag Values |Used for tags with decimal\-based values, such as cost, proportion, etc. |
|Multi\-value Tag Values |When there are multiple values for the tag, this type of tag is commonly used for interests, favorite topics, etc. |
|Date type label value |For tags that hold date values, they are specific to dates, commonly used for labels such as birthdates, etc. |
|Datetime\-based Tag Values |Tags are used for labeling values as date and time types, down to hours, minutes, and seconds, commonly used for labels like update dates. |
|AIPL model |A means of quantifying and operating brand audience assets in a chain\-like manner. A (Awareness) represents the brand awareness group; I (Interest) represents the brand interest group; P (Purchase) represents the brand purchase group; L (Loyalty) represents the brand loyalty group |
|5A model |Philip Kotler proposed the marketing model in "Marketing 4.0" where A1 Awareness represents customers passively receiving information; A2 Appeal represents customers whose brand impression is enhanced; A3 Ask represents curious customers actively searching for information; A4 Act represents customers taking action; A5 Advocate represents loyal customers who promote the brand |
|RFM Model |The model evaluates the high and low values of R, F, and M for each user, categorizing them into 8 customer value types: Important\-Value Customers, Important\-Respond Customers, Important\-Cultivate Customers, Important\-Retain Customers, Potential Customers, New Customers, General Maintenance Customers, Lost Customers<br><br>R: Recency reflects a customer's activity based on their most recent purchase<br><br>F: Frequency reflects a customer's loyalty based on purchase frequency<br><br>M: Monetary reflects a customer's contribution based on spending amount |
|Selection criteria "AND" |Fulfilling all rules or combination rules is considered compliant with tag rules |
|Selection criteria "OR" |Fulfilling any rules or combination rules is considered compliant with tag rules |
|Not Included |Users who do not meet the conditions within the data range of the current dataset |
|Included |Users that meet the conditions within the data range of the current dataset. |
|Global Exclude |Excluding users with this label value from all users (including those who have not been assigned this label) (For example: If there are 100 users in total, and 10 of them are labeled "elderly": 4 are labeled "yes," 5 are labeled "no," and 1 is labeled "other." So, selecting not to include "yes" in this label globally means selecting 96 users.) |
|Divide label values by discrete numerical values |Directly use the result of the indicator computation as the tag value. |
|Divide label values into numerical value intervals |Setting threshold range of user segmentation labels based on indicator calculation results |


<span id="_4-应用价值"></span>
# 4. Application Value


1. Layered operations based on user lifecycle stages

2. Dividing user value levels based on quadrant decomposition of indicators, clarifying operational goals

3. Based on activity characteristics, selectively targeting user groups to enhance activity ROI


<span id="_5-常见问题"></span>
# 5. Common Questions

<span id="q1-圈选组件中的聚合逻辑是否支持去重计数呢？"></span>
## Q1. Does the aggregation logic in the selection component of the circle support deduplicated counting?

A: Deduplicated counting is supported. Support deduplicated counting of text data in behavior tables, with the calculation logic being: statistical counting of the number of deduplicated event attribute values under specified events in the behavior table.

**Application Scenarios**


* Number of unique accesses to the city (event) and the number of provinces with (event property 2) in the APP.

* Based on SQL logic, i.e., Select count **distinct** event_x_key1 (event attribute 1).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Application Module: The scope of this aggregation logic includes: rule tags, rule clusters, individual portraits, group portraits (optional clustering), and statistical tags.</div>


**Operating Steps**

For example, for rule tags, click **Tag System\-New Tag\-Rule Tag** to enter the rule tag creation interface.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0017c41fe336c2c367350503c1e1799.png) </span>

After completing the basic information configuration, enter the tag rule interface. You can perform a distinct count on **detail data types**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b92fc47beb99fb72b13f4e0b516735f1.png) </span>

Image Explanation: If **the same user ID** makes \>1 purchases within seven days with a purchase amount \>1000, **count the user only once**.

<span id="f6e84419"></span>
## Q2. What logic is supported by the full **tag update value**?

A: Supports **historical data merging**: When updating tags, you can choose to retain historical data for data continuity.

Support **full data update**: or choose to recalculate based on the latest rules to ensure the accuracy of the labels.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c54bca8ecb5549cba919ec80da299941~tplv-goo7wpa0wc-image.image) </span>

<span id="923f089e"></span>
## Q3. Can date\-type labels/attributes be used for the calculation of "days from today"?

Date\-type labels/attributes support configuring **1970\-style date\-type labels**, which can be displayed in modules such as analysis after configuration.

For example: Date\-type labels/attributes can be used (such as registration time, birthday, media release year, etc.) for calculations like "days from today," "preferences," and so on.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff0a2fc457bb425d844d8a14119a644c~tplv-goo7wpa0wc-image.image) </span>
