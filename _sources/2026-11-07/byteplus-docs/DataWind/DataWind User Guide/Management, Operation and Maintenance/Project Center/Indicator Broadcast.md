---
title: "Indicator Broadcast"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Indicator_Broadcast"
---

<span id="_1-概述"></span>
# 1. Overview

To regularly obtain key indicator data directly in enterprise office software or email, you can choose [Data Subscription](https://docs.byteplus.com/docs/DataWind/111717)to push dashboards and dashboard links. However, when there are too many data messages and it is difficult for the business to quickly access core data, indicator broadcasting can be used to push key data in text form.


* Indicator broadcasting targets **indicators within saved table charts**. You can configure the broadcast sentence structure and the required indicator fields.

* **Supports broadcasting via Lark and email**. For broadcasting via Larkrk, the system administrator needs to confirm [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9)steps two and six. For broadcasting via email, the system administrator needs to complete [2. Quick start](https://docs.byteplus.com/docs/DataWind/111720#_2-%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8) in advance; otherwise, this channel will be grayed out.


<span id="_2-快速入门"></span>
# 2. Quick start

The following is a quick introduction to creating a scheduled indicator broadcast.


* First, create and save a table. If you already have a chart, you can skip this step.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9802fa9cf6894af88190f89a9a7f4f0d~tplv-goo7wpa0wc-image.image) </span>

* In Project Center – Indicator broadcasting (Scheduled tasks section), click New broadcast.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4931d758eea5445683df1290df0a1ec1~tplv-goo7wpa0wc-image.image) </span>

* Configure the broadcast name and description. Set the broadcast content title. Search for and select the table as the source of broadcast information. Configure the broadcast content.

   * The broadcast name is the name of the push (the Larkrk card title or email subject).

   * The broadcast content consists of the content title and specific broadcast information. You can configure multiple broadcast contents, which will be displayed in a single broadcast message.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41a007f60e864830ae36c66e35997c33~tplv-goo7wpa0wc-image.image) </span>

* Configure the sending time, sending method, and recipients. Recipients can include Lark users, Lark groups, email addresses, or email groups. After configuration is complete, you can click Send test to send a test message, review the result, and make adjustments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0515e216a0948279065b2613904a24b~tplv-goo7wpa0wc-image.image) </span>

* Once the expected result is achieved, click Save. On the broadcast list page, you can view related information and perform manual push, edit, or delete operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a771182ff604925854bd1b2eb5e2fbb~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-基本信息"></span>
## 3.1 Basic information


|**Function name** |**Function purpose** |**Function description** |
|---|---|---|
|Broadcast name |Name of the push (Lark card title/email subject) |Directly enter the name according to custom rules |
|Broadcast description |Some custom text or description in the push information |* Text content can be set to appear before or after the previous or next step.<br><br>* Text can be bolded, underlined, or italicized.<br><br>* Links can be added, for example, directly placing dashboard stories related to the broadcast content in the link. Users can choose to view only key metric data or click the link to view detailed data reports. |


<span id="_3-2-播报内容"></span>
## 3.2 Broadcast content

The broadcast content consists of the content title and specific broadcast information.


|**Function name** |**Function purpose** |**Function description** |
|---|---|---|
|Title |Content title |As shown in the figure below |
|Chart selection |Select a saved table under this project for which you have dataset viewing, editing, and management permissions |As shown in the figure below |
|Detailed data template |Configure the data format for push notifications. Manual text input and insertion of existing fields from the chart are supported.<br><br><br>* Inserting a field means inserting a dimension or metric field from the chart. In the template, these appear with a gray background and <\>, while all other content is text.<br><br>* The serial number automatically generates a number for each row of data, as shown in the figure on the right.<br><br>* The template defines the message format for each metric value. Line breaks are supported, and you can also customize text, emoji images, and more. |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f0b7333c6f963f94c0269e8a6ae68296) </span><br><br><span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_218d9bda7b25e80993053b388a831bcc) </span> |
|Data conditional formatting |After configuring single\-color cell (red/green) conditional formatting for data in the chart and setting up metric reporting, the data in push notifications will display the same red and green text as in the chart. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a5bf975a7d47f492f01e31c3075b83~tplv-goo7wpa0wc-image.image) </span> |
|Add content |Add new broadcast content, which means you can add a new chart. |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b9ba38556cc403a793d3b5c7a333e9f3) </span><br><br><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a4443ac8e7d063787ada52fafe2e071c) </span> |
|Broadcast style |Insert a divider between multiple broadcast messages. |As shown in the figure, adding a divider allows for greater separation between multiple pushed messages.<br><br><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_06eda09ecd1a23a8fd4f277abb575262) </span><br><br><span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_7fd2be9a94a62cde8130107e4bd5cc4d) </span><br><br><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a41763132555885ad5dc1fb6ccfbf518) </span> |


<span id="_3-3-订阅时间"></span>
## 3.3 Subscription time

<span id="_3-3-1-定时推送"></span>
### 3.3.1 Scheduled push

When scheduled push is configured, the system will query the chart at the specified time and broadcast the query results. Supports day\-level, minute\-level, hour\-level, and week\-level broadcasts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1563ed13b4b43f3b65a83a50b38d9aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-2-数据完成同步时推送"></span>
### 3.3.2 Push upon data synchronization completion

It is also possible to configure push notifications to be triggered upon data synchronization completion. This way, the system will not broadcast metrics that have not been updated. If the data synchronization completion time is later than the scheduled broadcast time, the system will wait until data synchronization is complete before broadcasting.

As shown in the figure: if the data for the day is synchronized at 9:00, the metrics will be pushed at 10:30; if the data for the day is synchronized at 12:00, the metrics will be pushed at 12:00.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/177dace8e29e49488e0ae68ebe139f36~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-推送方式"></span>
## 3.4 Push methods

Supports push to Lark, Lark groups, email, and email groups, and only supports sending to internal organization users.


* For broadcasting via Lark, the system administrator needs to confirm [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9) Step 2 and Step 6

* For broadcasting via email, the system administrator needs to complete [2. Quick start](https://docs.byteplus.com/docs/DataWind/111720#_2-%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8), otherwise this channel will be grayed out.


**Permission description**


|**Delivery method** |**Selection logic** |**Permission verification logic** |**Points to note** |
|---|---|---|---|
|Lark, email |Select users who have already been added to the platform and bound to Lark or email.<br><br><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d5fa11b0c3b2e8d5d65a71ff41e4a7f6) </span> |Receive data according to the data permissions associated with the account on the platform.<br><br>For example: Suppose users A and B have both configured the same metric broadcast, and the pushed data includes region and revenue data. If A only has data permissions for the Shanghai region and B only for the Beijing region, then user A will receive data results for Shanghai and Shanghai revenue, while B will receive Beijing and Beijing revenue. | |
|Lark group, email group |Select according to the Lark group or email group to which the configurator belongs.<br><br><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ca15c044debbd749a3903c44576caef8) </span> |Verification is based on the creator (that is, the person configuring this metric broadcast) and their data permissions on the platform. The data received is pushed according to the creator's data permissions, so the results sent to the group are consistent. |**Please exercise caution when using this feature with sensitive data.**  |


> If pushing Lark/Lark groups, when the monitoring message is too long, due to the 30k size limit of Lark messages, the message may be truncated and incomplete.


<span id="_3-5-发送多条播报内容效果展示"></span>
## 3.5 Demonstration of sending multiple broadcast messages

Multiple broadcast messages can be added to a single broadcast. Click Add Content, and then select a chart and configure the title and template.
