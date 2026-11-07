---
title: "Rule Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Rule_Tags"
---

<span id="_1-产品概述"></span>
# **1. Product Overview**

Support creating rule tags, customizing rules for each tag value through rule selection. The following will explain in detail based on product function operations.

<span id="f8f4a86c"></span>
# 2. Operation Steps

Go to the **Labeling System** module, click the **Create New Label** button, select **Rule Tags** to enter this functional module.

> You can view the prerequisites for creating a new tag in [概述](https://docs.byteplus.com/docs/undefined/672482cb9aa193032e53b06d).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92b30329bfd2030882ba3133b7abbc95.png) </span>

<span id="74333faa"></span>
## **2.1 Configure Basic Tag Information**

After logging in and accessing CDP\-Labeling System, click **Create New Label\>Rule Tags**, enter the **Create New Rule Tag** interface, and refer to the following text for configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5aab8651eb443f3ad15b96a8dc9321c~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Explanation |
|---|---|
|Tag Name |Name of the new tag (within 100 characters; for the same project, tag names cannot be duplicated) |
|Path |Select the folder category where this tag belongs<br><br>> Explanation— Two switches are involved in the creation of a new tag under the path<br><br>> 1. Group Switch: In the project center \- group configuration \- function configuration, there is a **label directory permission control** switch, which is off by default. When turned on, strict permission control will be applied to "directories" when creating labels, allowing only those with no **edit label tree** permission to place them in "unclassified".<br><br>   > Module switch: **Tag directory permission control** switch is turned on, users without **edit tag tree** permission will default to the "Uncategorized" path when **creating tags** (project administrators can authorize users in **Project Center\-Permissions**). |
|Description |Input labels for reference by other tag users. |
|Calculation type |Optional offline calculation or real\-time calculation |
|Updating the value logic of tags |* Each update recalculates: Each time it is calculated according to the latest value logic, so IDs with historical values not meeting the conditions in the latest calculation cycle will be removed.<br><br>* Each update allows the merging of historical data: once a tag value is set, if the ID is empty the following day, the last non\-empty partition value will be saved. The latest calculation will replace the old value if there is a change in value. |
|Save type for tags |Users can set rules for a tag to have multiple values. When a user meets the requirements of multiple values, they can choose a single value based on priority or keep all values that meet the conditions. |
|Update Type |Optional scheduled updates or manual updates |
|Execution Frequency |For scheduled updates, you need to set the update frequency and time, supporting daily/weekly/monthly synchronization. |
|Calculation result storage retention rules |For scheduled updates, you can set the number of historical versions to keep. The system will delete historical versions exceeding the limit the next day.<br><br><br>* If you choose **Unlimited** here, the default value set by the group will be used.<br><br>* If you choose **Specified duration,**  specify the number of recent result versions to retain. For example, entering 4 \- Daily retains the last 4 days; Weekly retains the last 4 weeks; Monthly retains the last 4 months of results. The final value is based on the smaller value in the group settings. |
|Online service switch |If you need to connect to other systems, please enable online services: You can quickly query the ID through the high QPS low\-latency interface |


<span id="91b79ddf"></span>
## **2.2 Configure Tag Rules**

On the data source, you can select tags, attribute data, behavior data, and detailed data, and support the use of multi\-end data, filtering out various tag values through "AND" and "OR".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e6c17758d35d29400f62792d2a253b76.png) </span>

<span id="d3c959f9"></span>
### **2.2.1 Use detailed data to configure tag rules**

When using **detailed data** to set rules, such as creating the "spending level" rule tag, users can select the order details table and set the tag value "high spending level" selection rule to "`past 7 days + actual amount + sum>8000`".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ba3e7e8c73fbeb91d7e729d6970dd24.png) </span>

**Points to consider when setting rules using detailed data:** 

① The aggregation methods of detailed data support total count, unique count, sum, average, maximum, minimum, etc.; for specific selection component usage, please refer to [usage instructions](https://www.volcengine.com/docs/7139/1345386).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1c724d0804646d0816fd021db855213~tplv-goo7wpa0wc-image.image) </span>

② Detailed data supports adding "AND meets" judgment conditions after filtering field aggregation, such as "`past 7 days order contains brand A, and ordering channel includes online mall`".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d057b4dba5494804bb3e52027f20a07e.png) </span>

<span id="11a4f1f4"></span>
### **2.2.2 Using behavioral data to configure tag rules**

When using **behavioral data** to set rules, such as creating the "coupon usage frequency" rule tag, users can select the behavior table and set the tag value "high usage frequency" selection rule to "`past 7 days + done + coupon redemption + total count>8`".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8cf460e39cdfe8fb794edae9e042d247.png) </span>

**Points to consider when setting rules using behavioral data:** 

① The aggregation methods of behavioral data support total count, daily count, days, consecutive days, sum, average, maximum, unique count, minimum value; for specific selection component usage, please refer to [usage instructions](https://www.volcengine.com/docs/7139/1345386).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46e1f1e3de9144e983ce665ea2690d16~tplv-goo7wpa0wc-image.image) </span>

Behavioral data supports adding the judgment condition "and meets" after filtering and aggregating fields. For example, "`Browsed the A brand activity page more than 10 times in the past 7 days, and the ordering channel includes the online store`."

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06eaee58f0afc863f612aab1ae04ca1e.png) </span>

Support creating tags based on behavioral paths, common scenarios include, companies needing to create tags for the "response rate to activities" based on user behavior. Low\-grade tag rules are: first clicking on the activity pop\-up page, then browsing the activity details, and then exiting the program; high\-grade tag rules are: first clicking on the activity pop\-up page, then browsing the activity details, and then participating in the activity and placing an order.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8774d4fa87e5565eb68f75436dabbf0a.png) </span>

\*Note:


* Behavioral sequences across data sources do not support sequential behaviors, meaning you cannot choose to have done behavior a from data source A, behavior b from data source B, but you can choose to have done behavior a, b, c from data source A sequentially.

* When selecting the "done sequentially" logic, you can choose multiple behavioral events in a single step. For example, as shown in the image below, in step 1 (browsing, interacting, sharing any of the three behaviors) and step 2 (authorization).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c386a7dcd715ef9c5c82b8a86b46d6a3.png) </span>

Selection logic supports the "not done" and "global not done" logics. Note the logical differences between different selection conditions. For example:


* Not done: Refers to users excluding the event in the corresponding partition. For example, if there are 100 users in total and 10 users had the event today, then the **not done** logic would be selecting from those 10 users.

* Global not done: Refers to excluding users who have not had any events from all users (including those who haven't had any events). For example, if there are 100 total users and 10 users had the event today, then the **global not done** logic would be selecting from those 100 users.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_33a32a34c973fbab37b1156d13552e9e.png) </span>

For example, the underlying data details are as follows:


|User ID |Event |Event attribute |Event occurrence time | |
|---|---|---|---|---|
|1 |Register |Android |2023/9/16 12:10 | |
|2 |Register |IOS |2023/9/16 14:10 | |
|3 |Login |IOS |2023/9/16 15:01 | |
|4 |Login |IOS |2023/9/16 15:34 | |
|5 |Login |IOS |2023/9/16 16:12 | |
|6 |Login |Web |2023/9/16 16:48 | |
|7 |Login |Web |2023/9/16 17:10 | |
|8 |Login |Web |2023/9/16 17:14 | |
|9 |Login |Web |2023/9/16 17:50 | |
|10 |Login |Web |2023/9/16 18:02 | |
|11\-100 |The other 90 people had no incidents that day ||||


For different business requirements, the differences in selection logic based on the underlying data for the example in the table above are as follows:


| |Scenario One (Not done before) |Scenario Two (Global Not Done) |
|---|---|---|
|Business Requirements |Want to exclude users who registered using Android from users who have had behavioral events in the last 1 day (i.e., September 16th) |Want to exclude users who registered using Android in the last 1 day from the full user pool |
|Operation Instructions |1. Select the date as "last day"<br><br>2. Filter out users registered using Android<br><br>3. Exclude these users from the group of users who have had behavioral events (i.e., not done) |1. Select the date as "last day"<br><br>2. Filter out users registered using Android<br><br>3. Exclude this group of users from the entire population (i.e., never done globally) |
|Product configuration and logic explanation |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34e0ea689d314c59f21092079061a151.png) </span> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5291be9e59ae214aa1845ab38fea5d8.png) </span> |
|Result description |The final selected group consists of 9 people (i.e., user ID 2 to 10) = event occurring group (10 people, user ID 1 to 10) \- users who registered using the Android platform (1 person, user ID 1) |The final selected group consists of 99 people (i.e., user ID 2 to 100) = all population (100 people, user ID 1 to 100) \- users who registered using the Android platform (1 person, user ID 1) |


<span id="43c82622"></span>
### 2.2.3 Using attribute data to configure tag rules

Rule setting using **user attribute data**, such as when creating the rule tag "membership type," users can select attributes as tables and set the tag value for the "Silver Member" selection rule as "`attribute table + membership type + contains + Silver Member`".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d39593384860c6abc397478e4c6e906.png) </span>

<span id="ae804283"></span>
### 2.2.4 **Using mulit\-channel data, filter out tag values using "and, or"** 

Multiple sets of rules can be defined using multi\-channel data, and the effective way of defining rules is through the logical functions "and/or":


* And: Meeting all rule or combination rule conditions is considered compliant with the tag rule.

* Or: Meeting any rule or combination rule conditions is considered compliant with the tag rule.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_714ed22dd84e6343b6fff13c6b07f650.png) </span>

<span id="e94d7eff"></span>
### 2.2.5 Explanation of date selection

Supports fixed dates, dynamic dates, and single date selection.

**1) Selection of fixed dates:** 


* Date\-type tags support the selection of a single day or a range of dates, such as 2024\-11\-01 to 2024\-11\-13.

* Time and date\-type labels can be fine\-tuned to dynamic ranges down to the hour, minute, and second levels, such as 2024\-11\-01 to 2024\-11\-13 00:00:00 to 02:02:02.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c43a95d7ad42d0932cdb9f7b066ed7~tplv-goo7wpa0wc-image.image) </span>

**2) Dynamic Date Selection:**  Supports selecting a period based on today, such as the last 1/3/7/14/30 days, this month/bimonthly, the last 3/6 months, the last 1/2 years, this/last quarter, this year/last year, last week/month, or customizing the last X days (including today).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8c3a4c880e24e068d0d0707a3e2dacf~tplv-goo7wpa0wc-image.image) </span>

**3) Single Date Selection:**  Date\-type labels support selecting a single date, like 2024\-11\-12. Time and date\-type labels can also be fine\-tuned to select time points at the hour, minute, and second levels, like 2024\-11\-12 00:00:00.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d641ee33a59469b87db4a95f03c8da3~tplv-goo7wpa0wc-image.image) </span>

<span id="747ca2e2"></span>
# 3. Support Exclusion in Circular Selection Controls

Supports **Exclusion Function** in the filtering conditions of rule tags, allowing users to quickly filter out audience packages that do not belong to a certain crowd. Both "Meet" and "Exclude" components are arranged at the same level. That is, **Meet Condition A and Exclude Condition B**.

<span id="e33b527b"></span>
## 3.1 Application Scenarios


* Case Description

   Users want to select **the group of users who have clicked on** **mini\-app activities within 7 days (\>=3 times) and have not placed an order within 7 days**.


That is, the logic of excluding users who have placed orders in the last 7 days should be:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b603720752f8b38fa50208154ea33ca1.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73200825d054581df4488e110162dcf9.png) </span>

Only behavioral data support a period of time based on the time of the event, such as the registration time on the same day/week/month as the xx event, or the registration time in the future/past 3 days/seconds/minutes/hours/weeks from the occurrence of the xx event.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9e326037f1f4d4cc9a765ae7a149033.png) </span>

<span id="653b2428"></span>
# 4. Common Issues

<span id="1ffd49a0"></span>
### Q: When configuring selection rules, can the dropdown list for selecting values support searching for all tag values?

Support

<span id="60b9d2d4"></span>
### Q: When selecting tags, does the drop\-down display and support the selection of tag values from all partitions?

When selecting tags, the drop\-down only displays and supports the selection of the tag values from the most recent partition.

<span id="259a29ce"></span>
### Q: Can array type be selected when configuring rule tags?


* Supports the array property, calculation logic supports inclusion, exclusion, and inclusion of all aspects


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_300e2f802a86a65759716a4057793e26.png) </span>

<span id="c05708d7"></span>
### Q: When creating rule tags, what is the calculation logic of the current tag if text & numerical type data from the detail table is selected when configuring the rules?

When configuring rules and selecting text & numerical type data from the detail table, the calculation logic supports "deduplication count."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75ca79aac6684c73b6183ecc02edbec4~tplv-goo7wpa0wc-image.image) </span>

For example, in the following detail table, before setting the deduplication count, if calculating "number of cities ordered in the last 3 days," it would be 3; if deduplication count is set, when calculating "number of cities ordered in the last 3 days," it would be 2, meaning the same city (Shanghai) will not be counted repeatedly.


|User ID |Order ID |City of order placement |Number of cities where orders are placed \- total counts |Number of unique cities where orders are placed |
|---|---|---|---|---|
|123 |789 |Shanghai |3 |2 |
|123 |790 |Shanghai |||
|123 |791 |Beijing |||
