---
title: "Channel Management"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Channel_Management"
---

<span id="通道管理"></span>
# Channel Management

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Support management through channels like Webhook, SMS, SMS signatures, WeChat Official Account, WeChat Mini Program, App pop\-ups and more, covering channel access parameter configuration, frequency control settings, and non\-disturbance time settings.</div>



---



<span id="746b6ade"></span>
# 1. Webhook Channel

<span id="0a780c21"></span>
### 1.1. Product Overview

The created Webhook channels are centrally managed in the "Management Center \- Webhook Channel".

<span id="aea49a94"></span>
### 1.2. Usage Restrictions


| **[📢 Prerequisites for Using This Feature]**  ||
|---|---|
|1. **Activate GMP permissions** |Admins grant permissions, permission path: Management Center \- Channel Management \- webhook |


<span id="926d5745"></span>
### 1.3. Feature Description

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a337cd6e641b46d39e7f2ec531d153fd~tplv-goo7wpa0wc-image.image" width="2872px" /></div>


<span id="4ac17a39"></span>
#### **1.3.1. New Webhook**

Webhook integration steps include basic information configuration, external template configuration, Webhook request response configuration, and receipt configuration.

If Webhook channel integration is needed, contact BytePlus project manager or customer success manager.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/824ee32445184c878df37acfceac5982~tplv-goo7wpa0wc-image.image" width="1917px" /></div>


<span id="e0926857"></span>
#### **1.3.2. Test Sending**

After clicking, you can test sending for this channel, which is useful for channel debugging.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c035bc4c0d174c669b4f8d040ba289e8~tplv-goo7wpa0wc-image.image" width="2054px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**ID Type** |Default to this channel's ID type, cannot be changed. |
|**User ID** |Mandatory, represents the user ID used during test sending. |
|**Template Parameters** |If this Webhook has a template, corresponding template parameters also need to be selected. |
|**Outreach Content** |You can input the content for this outreach. |


<span id="ddeb4042"></span>
#### **1.3.3. Update Configuration**

Channel must be closed before updating configuration. Supports editing Webhook name, message receiving address, external message template, authentication method, custom return codes, QPS limit, sending target ID, interface sending method, and other information.

<span id="da5a960f"></span>
#### **1.3.4. Frequency Control Settings**

Frequency control settings for this channel can be configured. Reach activities using this channel will undergo frequency control; if multiple conditions are checked, all conditions must be satisfied.

Currently supports daily, weekly, and monthly frequency control.

If a do\-not\-disturb strategy is set, reach activities using this channel will apply channel do\-not\-disturb.

Message Delivery Tasks, Process Canvas, and strategy elements within Process Canvas can have separate do not disturb settings. If multiple do not disturb conditions are set at the same time, all these conditions need to be satisfied.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cb889989ea743c2bf897709606d5291~tplv-goo7wpa0wc-image.image) </span>

<span id="375512f5"></span>
#### **1.3.5. Blacklist and Whitelist Configuration**

This feature allows for blacklist and whitelist control over channels.

There are three types of controls: **Channel Reach Scope Blacklist, Channel Frequency Control Whitelist, Channel Reach Scope Whitelist.** 


* **Channel Reach Scope Blacklist:**  This capability ensures that if a user ID is in the blacklist segment, no messages will be sent through this channel. If not selected, it means there are no restrictions.

* **Channel Frequency Control Whitelist:**  This capability ensures that user IDs in the segment will not be subject to frequency control on this channel.

* **Channel Reach Scope Whitelist:**  Actual sending through this channel will only target user IDs in this segment, and other users will not receive messages.


There are three ways to set up blacklists and whitelists, namely through specified  **「Segment」settings**, **specified 「Label」settings**, and **specified 「ID」settings**.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e2f76104a784d66a705ad9d3e4f2136~tplv-goo7wpa0wc-image.image" width="2034px" /></div>


 **① Via 「Segment」 settings**

To use this feature, VeCDP needs to be purchased. If the module is not purchased, the capability is not supported and you can ignore this section.

If VeCDP has been purchased, you can follow the steps below to set it up.


|**Steps** |**Detailed Explanation** |
|---|---|
|**Select to Set the Black/White List** |Select the type of Black/White list settings needed and choose the ID type for the segment package.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eae707c14c84e7095f450cd267def09~tplv-goo7wpa0wc-image.image) </span> |
|**Select 'Segment'**  |Use rule creation segments or existing segments to configure the Black/White list segments.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ec8c27bcb9f4ef9897f4ca0f9a6ea2f~tplv-goo7wpa0wc-image.image) </span> |
|**Activate Segment** |Click 'Activate' to complete the system import action and officially activate the segment.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71985bb6e9594224804453a5d07db742~tplv-goo7wpa0wc-image.image) </span> |


 **① Via 「Label」 settings**

To use this feature, VeCDP needs to be purchased. If the module is not purchased, the capability is not supported and you can ignore this section.

If VeCDP has been purchased, you can follow the steps below to set it up.


|**Steps** |**Detailed Description** |
|---|---|
|**Select to Set the Black/White List** |Select the type of Black/White list settings needed.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45a07b9b2e784f5a8e06e5a05f582977~tplv-goo7wpa0wc-image.image) </span> |
|**Configure "Label"**  |Select the corresponding label, fill in the label value information, and click "Add Channel Reach Range Blacklist Label" if you have multiple labels.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a269d9d3d8354ae3821a96a0f657ecb2~tplv-goo7wpa0wc-image.image) </span> |


 **③ Set up by "ID"** 

Using this feature, you can directly fill in the ID value information for whitelist and blacklist management.


|**Steps** |**Detailed Description** |
|---|---|
|**Select Set Whitelist/Blacklist** |Check the type of whitelist/blacklist you need to set.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c8c09fa29e641e3a32345180e8f5ae8~tplv-goo7wpa0wc-image.image) </span> |
|**Fill in ID** |Fill in the ID value, which should be consistent with the channel’s "Target ID". If the channel's Target ID is phoneid, the ID value entered here should also be of the phoneid type. Multiple IDs can be entered, use Enter to separate multiple lists, and it is recommended to keep the number of ID values within 20. |


<span id="f2303e6b"></span>
#### **1.3.6. Delete Channel**

Only channels that are closed can be deleted. After deletion, it will no longer be possible to create tasks for that channel, so delete with caution.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/097318c3c94b4580a8353d7cca9b2e92~tplv-goo7wpa0wc-image.image" width="2878px" /></div>


<span id="c64a3409"></span>
#### **1.3.7. Preset Metrics Configuration**

For "Custom Webhook Types," if the channel's metrics cannot be counted through "deliveries, clicks" (such as the need to display "call volume, call rate" for outbound channels), this function can be utilized to configure the metrics.

If there is a need for Metrics Configuration, please contact the BytePlus Project Manager or Customer Success Manager. The specific configuration steps are as follows:

 **① Configure receipt metrics.** 

In "Channel Management\-Webhook\-Webhook Receipt Configuration," add a new configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4de28c90ae524dd591a1a13c46f87489~tplv-goo7wpa0wc-image.image" width="2878px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fd3b5adc756415aa7a11dee799d168d~tplv-goo7wpa0wc-image.image" width="2878px" /></div>



|**Field** |**Field Meaning and Use** |
|---|---|
|**Configuration Name** |Fill in yourself, this field is used to distinguish different receipt configurations |
|**Successful/Failed Delivery Configuration** |1. **This receipt correlates to the 'delivery volume' metric in Data Analysis, other custom receipt configurations**: You must select this item in 'Successful Delivery Configuration'. This selection represents the correlation between the receipt status code and the GMP metric. If the metric corresponds to 'delivery volume', then you can select 'This receipt correlates to the 'delivery volume' metric in Data Analysis'; if it is another metric, you can choose 'Other custom receipt configurations'.<br><br>2. **Jsonpath**: The path where the receipt is located and its corresponding matching relationship.<br><br>3. **Message**: Represents the name of the metric for this receipt, which can be defined by oneself, such as call volume, read volume. The name of this metric can be used for configuring Webhook channel for data analysis. This metric will not immediately appear on the Data Analysis page after configuration; further steps must be completed before the corresponding metric data is displayed. |


 **② Select receipt in the Webhook channel.** 

In the Webhook channel configuration "Receipt Configuration," you can choose the "Webhook Configuration" completed in the previous step.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c64f4f6789e4f4d9d144c6429755954~tplv-goo7wpa0wc-image.image" width="2878px" /></div>


 **③ Conduct metrics configuration.** 

In the Webhook channel card, click "...", select "Preset Metrics Configuration," and you can enter the "Configuration Entry."

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3c73dec457e4f7ba1e17babb7a175eb~tplv-goo7wpa0wc-image.image" width="2878px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f0a678dda8a4953a9f5886441a58db2~tplv-goo7wpa0wc-image.image" width="2878px" /></div>



|**Field** |**Meaning and Purpose of the Field** |
|---|---|
|**Set Custom Metrics** |The metrics configured in the "Webhook Receipt" will be automatically included for this channel, no extra configuration needed. If there are composite metrics (such as call\-out rates), they can be manually configured here, as shown below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deb41322cbb9436189251f95fcc7a8af~tplv-goo7wpa0wc-image.image) </span> |
|**Set Detailed Data Table** |Metrics related to the sending link cannot be modified on your own, but receipt metrics can be configured in this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfb89bedacb44c93b04c3a95291f0dd9~tplv-goo7wpa0wc-image.image) </span><br><br>The detailed data table for metrics has two columns: Available Metrics and Selected Metrics. Available Metrics include those set up in "Webhook Receipt" and "Custom Metrics" configured on this page. After selecting a metric, it will be displayed in Data Analysis and can be manually reordered. The order of metrics in this column determines the order of detailed metrics displayed on the Data Analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f91df18368d34cdfa1ed28d6e5780eba~tplv-goo7wpa0wc-image.image) </span> |
|**Set Funnel Metrics** |Sent link\-related funnel metrics cannot be modified by themselves; receipt\-related funnel metrics can be configured in this function.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ee2333462764b0b91193c9769ef1fbd~tplv-goo7wpa0wc-image.image) </span><br><br>Setting funnel metrics includes two columns: the left column represents the metrics displayed at each level in the funnel; the right column represents the "filter reasons" that need to be displayed between each level in the funnel, indicating the reasons for filtering from "the previous level" to "the current level."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/907ac4db7412443ea223cf6913301fb8~tplv-goo7wpa0wc-image.image) </span> |


<span id="f822f5c6"></span>
#### **1.3.8. SaaS Webhook Receipt Configuration with Independent API Address Domain**

Complete Request URL: https://gmp\-saas\-api.consol

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd406972cb554c3492ac96e67b212c82~tplv-goo7wpa0wc-image.image) </span>


---



<span id="bb8e9aa7"></span>
## 2. SMS Channel

<span id="8d18efa0"></span>
### 2.1. Product Overview

SMS Channel Management allows the addition of new SMS channels and the management of existing ones (view, configure parameters, and frequency control settings).

<span id="42a4346e"></span>
### 2.2. Usage Restrictions


| **[ 📢 Prerequisite of Using This Function ]**  ||
|---|---|
|1. **Activate GMP Permissions** |The administrator activates permissions, permission path: Management Center \- Channel Management \- SMS |


<span id="1d2719fa"></span>
### 2.3. Feature Description

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc92e3c9099a49f6b104ba8dd29204be~tplv-goo7wpa0wc-image.image" width="2878px" /></div>


<span id="03e49390"></span>
#### **2.3.1. Add New SMS Channel**

Channel types include BytePlus Cloud SMS Channel, Alibaba Cloud, Tencent Cloud, Montnets, Yunpian, and Jiguang SMS Channel. New SMS channel requires entry of the channel's secret keys, target send ID, and QPS limit.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18f29ec89d8346619e5557253d507e20~tplv-goo7wpa0wc-image.image" width="2878px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48652c17402f42baa03032e532ece902~tplv-goo7wpa0wc-image.image" width="2874px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**SMS Channel Name** |You can set the name of this channel to distinguish between different channels. |
|**Key Information** |Different channels require different key information; the Byteplus Messaging Channel requires entering AK/SK.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3805bd7d6bcf458095c4e01998d41bf8~tplv-goo7wpa0wc-image.image) </span> |
|**Target ID for Sending** |This refers to the type of ID required by the channel for sending. The ID type for SMS is the phone number. |
|**QPS Limit** |QPS refers to the volume of messages sent per second by the channel during transmission. This value typically needs to be decided based on the actual capacity of the downstream channel to handle per second, combined with the operational volume. Below are common QPS values and the corresponding message volumes per hour:<br><br><br>* QPS = 100, able to send 360,000 messages per hour<br><br>* QPS = 500, able to send 1,800,000 messages per hour<br><br>* QPS = 1000, can send 3,600,000 messages per hour<br><br>* QPS = 3000, can send 10,800,000 messages per hour |


<span id="9306e055"></span>
#### **2.3.2. View**

Click to view the channel parameters, which vary by channel.

<span id="d94bec22"></span>
#### **2.3.3. Configuration Parameters**

Set the SMS channel\-related parameters, which can only be configured when the channel is deactivated.

<span id="bda5fb74"></span>
#### **2.3.4. Frequency Control Settings**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01c510c25a244f9583b8fead6ddcdddd~tplv-goo7wpa0wc-image.image" width="1670px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Channel Frequency Control** |Reaches conducted through this channel will undergo frequency control; if multiple criteria are checked, all conditions need to be met. Currently, supports daily, weekly, and monthly frequency controls. |
|**Channel Do Not Disturb Settings** |Reaches conducted through this channel will implement Do Not Disturb.,, and strategies in thecan also have individual Do Not Disturb settings; if set simultaneously, all Do Not Disturb conditions must be met. |
|**Channel Reach Blacklist** |Multiple IDs can be entered; use 'Enter' to separate multiple blacklists. Users listed in the blacklists will not be reached. It is recommended to enter no more than 20 IDs. |
|**Channel Reach Whitelist** |Multiple IDs can be entered; use 'Enter' to separate multiple whitelists. By listing these IDs, only the users specified will be reached while all others will not be reached. This scenario is suitable for channel initial testing and verification and is intended only for internal operational personnel. It is recommended to enter no more than 20 IDs. |
|**Channel Whitelist** |Multiple IDs can be entered; use 'Enter' to separate multiple whitelists. After entering these IDs, users on this whitelist will not be subject to channel frequency restrictions. However, if the task sets task\-level frequency control, these listed user IDs will still be regulated. It is recommended to enter no more than 20 IDs. |


<span id="e5a9d8e3"></span>
#### 2.3.5. SMS Receipt Configuration

If a customer has activated different SMS platform accounts, and needs to conduct SMS marketing campaigns and gauge their effectiveness through BytePlus, they must configure the SMS delivery result receipt URL on the respective platforms; otherwise, the success rate of SMS delivery for marketing campaigns cannot be tracked on BytePlus.

**How to obtain the receipt URL:** 


* Private user address: Private BytePlus domain/gmp/sms

* SaaS user address: Account ID

   * The main account ID is in the top right corner


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/479df92ffcd14393b2c296814e5b00a5~tplv-goo7wpa0wc-image.image" width="794px" /></div>


<span id="7d96ec00"></span>
##### (1) BytePlus SMS

If the customer's account has access to BytePlus SMS and needs to use this service on GMP for marketing outreach campaigns, it is required to configure the SMS outreach result receipt address on the BytePlus SMS platform; otherwise, GMP will not be able to track the success rate of the SMS sent for the marketing outreach campaigns.


* Log in to the BytePlus platform \- go to the SMS Service \- Console

* Fill in the receipt address:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2089057296ad402aa8a0f039533e98b7~tplv-goo7wpa0wc-image.image" width="2676px" /></div>


Video SMS receipt:


* Log in to the BytePlus platform \- go to the SMS Service \- Console

* The filled reply address, [Video SMS delivery receipt address]


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59c9865bcb1a4f539dbb244d154d8e4f~tplv-goo7wpa0wc-image.image" width="2666px" /></div>


<span id="d6c12bdf"></span>
##### (2) Yunpian SMS

If a customer has activated a **Yunpian SMS platform account**, and needs to use Yunpian SMS services on GMP for marketing reach campaigns, it is necessary to configure the SMS delivery receipt address on the Yunpian platform; otherwise, GMP will not be able to track the success rate of the SMS delivery for marketing campaigns.

Receipt address: domain/gmp/sms_yunpian/callback

Receipt status code: https://www.yunpian.com/official/document/sms/zh_CN/domestic_push_report

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26fce4b9a28f4f03a006eb660fde8b2b~tplv-goo7wpa0wc-image.image" width="2178px" /></div>


<span id="24c19c6e"></span>
##### (3) Tencent Cloud [Tencent Cloud supports active polling and callbacks, configuration is optional]

If a customer has activated a Tencent Cloud SMS platform account, and needs to use Tencent Cloud SMS services on GMP for marketing reach campaigns, it is necessary to configure the SMS delivery receipt address on the Tencent Cloud platform; otherwise, GMP will not be able to track the success rate of the SMS delivery for marketing campaigns.

Receipt address: domain/gmp/sms_tencent/callback

Receipt status code:

https://cloud.tencent.com/document/product/382/59177#.E5.9B.9E.E6.89.A7.E7.8A.B6.E6.80.81.E9.94.99.E8.AF.AF.E7.A0.81

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0737eba09a5b4ed49732bba4e7d490d0~tplv-goo7wpa0wc-image.image" width="2810px" /></div>


<span id="42932a8c"></span>
##### (4) Aurora

If the customer’s account has activated an Aurora SMS platform account and needs to use the Aurora SMS service on GMP for marketing outreach campaigns, it is necessary to configure the SMS outreach result receipt address on the Aurora SMS platform, otherwise GMP cannot track the success rate of SMS dispatches in marketing outreach campaigns.

Receipt address: domain/gmp/sms_jiguang/callback

Receipt status code documentation: https://docs.jiguang.cn/jsms/server/callback

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7e474733d5848a0880aa0a346ef4572~tplv-goo7wpa0wc-image.image" width="2808px" /></div>


<span id="446753a7"></span>
##### (5) Alibaba Cloud (Active polling receipts, no configuration required)

<span id="ac0c8878"></span>
##### (6) Montnets (Receipts available only for major customer accounts, provide receipt address to Montnets R&D)

If the customer's account has activated a Montnets SMS platform and needs to use Montnets SMS services on GMP for marketing outreach campaigns, it is necessary to provide the receipt address to Montnets customer service, otherwise GMP cannot track the success rate of SMS dispatches in marketing outreach campaigns.

**Private receipt address**: domain/gmp/sms_monyun/callback


---



<span id="9530bb01"></span>
## 3. SMS Signature

<span id="6efe0c1b"></span>
### 3.1. Product Overview

The entry for creating SMS signatures is found under: Management Center \- SMS Signatures. Utilization of this feature requires the following permissions.

<span id="522c2c98"></span>
### 3.2. Usage Restrictions


| **[ 📢 Prerequisite for using this feature ]**  ||
|---|---|
|1. **Activate GMP permission** |Administrator activates permissions, permission path: Management Center \- Channel Management \- SMS Signature |


<span id="a4bccce6"></span>
### 3.3. Feature Description

<span id="e193a531"></span>
#### **3.3.1. "BytePlus SMS" Channel Signature**


1. **The BytePlus SMS channel allows you to directly create new SMS signatures and manage existing ones in GMP**. The management list displays the signature ID, signature content, signature type, application date, status, and actions. In China, sending SMS messages must include a signature, while it is optional for international/Hong Kong/Macau/Taiwan.

2. **Description of fields for creating new signatures**:



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Purpose of the signature** |The use of signature currently only supports self\-use (for use within the company's own products, etc.) |
|**Type of signature** |Includes full name/abbreviation of the company, full name/abbreviation of the Ministry of Industry and Information Technology registered website, full name/abbreviation of APPs, full name/abbreviation of public accounts and mini\-programs, full name/abbreviation of trademarks, full name/abbreviation of online store names on e\-commerce platforms<br><br><br>* **Full/abbreviated name of the Ministry of Industry and Information Technology registered website**: Need to upload a document providing signature explanation, website, or ICP registration information.<br><br>* **APP Full Name/Acronym**: Requires the provision of APP screenshots or ICP record information. The screenshot must include the company entity applying for the signature and the signature content.<br><br>* **Official Account and Mini Program Full Name/Acronym**: Requires a screenshot of the official account or backend screenshot; confirm that the official account's entity matches the entity applying for the account; the signature content can be within the scope of the official account's name. |
|**Signature Content** |The length should be 2~12 characters, consisting of Chinese, English, and numbers, and should not include "【】". |
|**Website Address** |Enter the company official website address. |
|**This task is associated with an application.**  |This task represents the Message Delivery Task, and the gathered behavioral data will be channeled back under the Datafinder application; if Datafinder has not been purchased, this capability can be ignored. |
|**Qualification Type** |Select based on the actual situation |
|**Upload proof** |Upload the proof of the type selected in the previous step "Qualification Type" |
|**Application explanation** |Provide a brief reason for the application, within 300 characters |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ef3ec0878324c52b7db9bc2a5aedf0c~tplv-goo7wpa0wc-image.image" width="2039px" /></div>



3. **The approval process after submitting a signature**: The SMS signature requires two\-step approval.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30ccd2bab3e8421c9fcc84f07e270ad5~tplv-goo7wpa0wc-image.image" width="3222px" /></div>



4. **Explanation of fields in the signature list**:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e867de58f0548f2b022865e5ce39496~tplv-goo7wpa0wc-image.image" width="2047px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Signing status** |**Signing status**: Includes under review by business administrator, under review by SMS service provider, in effect, rejected, disabled, review withdrawn<br><br><br>* **Under review by business administrator**<br><br>* **The SMS service provider is reviewing.** <br><br>* **In effect**: Once all review processes are passed, the review status transitions to in effect. When creating SMS tasks, only signatures in the 'in effect' status can be used.<br><br>* **Rejected**: Hover to view the rejection steps and reasons. Editing is allowed, and after editing, you can resubmit for approval.<br><br>* **Disabled**: A signature in the 'in effect' status that has been disabled will transition to a disabled status.<br><br>* **Approval withdrawn**: Only SMS signatures in the review process support this action; if resubmission is desired after withdrawal, a new signature must be created for approval. |
|**Operations** |Display the submitted signature information; click 'View Progress' to see the review progress. |


<span id="b4264470"></span>
#### **3.3.2 "Alibaba Cloud / Tencent Cloud / Jiguang" Channel Signature**


1. If the SMS channel is using Alibaba Cloud, Tencent Cloud, or Jiguang, signatures must be applied for on the corresponding platform and then manually added to the GMP system.

2. **List Display**: Displays signature content, application date, status, and actions.

   1. **Status**: Active or Disabled.

   2. **Action**: Enable or Disable.

   3. **Add New Signature**: Supports entering signature content that is already active on third\-party platforms.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/102bb679762e4266a783c93193d89e47~tplv-goo7wpa0wc-image.image" width="1884px" /></div>


<span id="a7687060"></span>
#### **3.3.3. "Montnets / Yunpian" Channel Signature**

If the SMS channel is using Montnets or Yunpian, corresponding signature information can be provided, but the GMP does not support separate signature management.


---



<span id="392db22e"></span>
## **4. WeChat Official Account**

<span id="a0ce3369"></span>
### 4.1. Product Overview

WeChat Official Account integration can send Official Account template messages, Public Account Active Messages, and Official Account Group Messages.

<span id="31dfe6e3"></span>
### 4.2. Usage Restrictions


| **[ 📢 Prerequisite for using this function ]**  ||
|---|---|
|1. **Activate GMP Permissions** |The administrator opens permissions, permission path: Management Center\-Channel Management\-WeChat Official Account |


<span id="94942be0"></span>
### 4.3. Feature Description

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02a73a56ba6040648a891aabd03d9bc3~tplv-goo7wpa0wc-image.image" width="2870px" /></div>


Integrating an official account supports two modes: third\-party authorization and developer mode. **Third\-party authorization mode only requires authorization to complete the integration of the official account, and integration through third\-party authorization mode is recommended; Developer Mode: Access is made by configuring the official account secret and other related parameters on the front\-end, and it is necessary to provide an interface for it to obtain a token through GMP to develop its own services.** 

<span id="050341d4"></span>
#### **4.3.1. Integrating the official account through "third\-party authorization mode"** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c597f06fb0249debd1c0abef82969e6~tplv-goo7wpa0wc-image.image" width="1230px" /></div>


Third\-party authorization mode requires QR code authorization, with the authorization's permissions and application relationships as follows:


|**Permission** |**The scope of application after the permission is activated** |
|---|---|
|**Message Management** |For receiving WeChat message receipts and sending customer service messages |
|**User Management** |For the "WeChat Operations" functional module |
|**Account Management** |For generating parameterized QR codes |
|**Web Page Services** |Used for the activity landing page associated with Rubik's Cube campaigns. If the module is not purchased, this function can be deactivated. |
|**Bulk Messaging and Notifications** |Used for bulk messaging via WeChat |
|**WeChat Coupon** |Used for issuing WeChat coupons |
|**WeChat Scan** |Used for activating messages via WeChat QR scans |
|**Material Management** |Used for sending image and text messages |
|**Custom Menu Management** |For the 'WeChat Operations' personalized menu function |
|**Service account subscribe notifications** |Used to send service account subscription notifications |


<span id="c3b1ecf5"></span>
#### **4.3.2. Integrating the official account through "developer mode"** 

Users integrate by configuring the official account secret and other related parameters on the front end, and it is necessary to provide interfaces for users to obtain tokens through GMP and develop their own services. Integration configuration includes the official account name, WeChat AppID, official account type, APPsecret, user URL, id type, and others.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/921f88410e3e41ff854d7dfe3b17a7f1~tplv-goo7wpa0wc-image.image" width="1226px" /></div>


<span id="e1167670"></span>
#### **4.3.3. Edit**

You can edit the relevant configuration. Editing is only possible after the public account is deactivated.

<span id="bf038301"></span>
#### **4.3.4. Frequency Control and Blacklist/Whitelist Settings**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1159c506ed7849efb461e643a318e5c3~tplv-goo7wpa0wc-image.image" width="2876px" /></div>



|**Field** |**Field meaning and usage** |
|---|---|
|**Channel frequency control** |Any reaches made through this channel will be subject to channel frequency control. If multiple items are checked, all conditions must be satisfied. Currently supports daily, weekly, and monthly frequency control. |
|**Channel do not disturb settings** |Any reaches made through this channel will implement the do not disturb setting. Message Delivery Tasks, Process Canvases, and strategies within Process Canvases can also be set with individual Do Not Disturb settings. If multiple Do Not Disturb settings are applied, all conditions must be met. |
|**Channel Reach Scope Blacklist** |Mulitple IDs can be entered, separated by pressing enter, and users on the entered blacklist will not be reached. The number of IDs entered is recommended to be no more than 20. |
|**Channel Reach Scope Whitelist** |Multiple IDs can be entered, separated by pressing enter, and after entering this list, it means only the users on the whitelist will be reached within the channel reach scope, all other users will not be reached. This scenario is applicable for channel initial debugging and validation, and is meant for internal operations personnel only. The number of IDs entered is recommended to be no more than 20. |
|**Channel Whitelist** |Multiple IDs can be entered, separated by pressing enter. After entering this whitelist, users on it will not be subject to channel frequency control limits, but if the task has set frequency control at the task dimension, these users' IDs will still be controlled. The recommended ID value should be less than 20. |


<span id="c9237ede"></span>
#### **4.3.5. Permissions Obtained**

For public accounts that access via third\-party scanning authorization, click on Permissions Obtained to view the set of permissions of the accessed public account.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f5f8c6451be4086b4011eb23baae00a~tplv-goo7wpa0wc-image.image" width="2878px" /></div>



---



<span id="07939faf"></span>
## 5. WeChat Mini Program

<span id="efbb70ac"></span>
### 5.1. Product Overview

WeChat Mini Program pop\-ups, Mini Program Subscription Messages, and Mini Program short links all require authorization in "Channel Management" under "WeChat Mini Program" before they can be used.

<span id="29c51fdf"></span>
### 5.2. Usage Restrictions


| **[ 📢 Prerequisite for using this feature ]**  ||
|---|---|
|1. **Activate GMP permissions** |Administrators activate permissions, permission path: Management Center\-Channel Management\-WeChat Mini Program |


<span id="27235851"></span>
### 5.3. Feature Description

Mini Program Subscription Messages include **one\-time subscriptions** and **long\-term subscriptions**, but currently, **long\-term subscription** messages are only open to offline public services such as government and public welfare, medical, transportation, finance, education, etc. For specific details, refer to the WeChat official document ["Mini Program Subscription Messages"](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/subscribe-message.html).

**One\-time subscription messages are used to address notification issues in subsequent service phases when users use the Mini Program. After users subscribe on their own, developers can send a corresponding service message without time limits; each message can be individually subscribed to or unsubscribed. That is to say, C\-end users must first authorize subscriptions, and only after that can the enterprise reach them.** 

**Important Notice: WeChat Mini Program subscription message authorization feature requires customers to develop it within their own mini programs; the GMP platform is not responsible for development.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f93b447c96104689946cab9f5e1348b8~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24f0ca380796420d9b36447ee4d9362d~tplv-goo7wpa0wc-image.image) </span>

<span id="c7e7110a"></span>
#### **5.3.1. Add New WeChat Mini Program**

Adding a new WeChat Mini Program refers to completing the authorization action for the mini program, enabling it to be used in WeChat Mini Program pop\-ups and Mini Program subscription messages.


|**Steps** |**Detailed description** |
|---|---|
|**Open the channel integration page** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d4dcff4e7894deda592ea0aaca196d3~tplv-goo7wpa0wc-image.image) </span> |
|**Proceed with the integration** |1. The integration method is "Third\-Party Authorization Mode," which allows customers to authorize by scanning a QR code.<br><br>2. ID type: You need to choose a composite ID, usually selecting the type as appid+openid.<br><br>3. QPS limit: represents the number of GMP messages sent per second.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01db338caa144b5b8375effc76fdd132~tplv-goo7wpa0wc-image.image) </span> |
|**Scan for authorization** |When authorizing, you must select  **"Obtain Mini Program Code"** ,  **"Mini Program Basic Information Management"** , and  **"Mini Program Link Management"**  permissions; other permissions are optional.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09caf9c8f18248de990e90471de1bfb8~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5528502b7e5b488c9eb2fb54d5d2e728~tplv-goo7wpa0wc-image.image) </span> |


<span id="04cc1c40"></span>
#### **5.3.2. Frequency Control and Black/White List Settings**

This setting only applies to Mini Program subscription messages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd9ec41e6d5b484a841cf45a86ca7484~tplv-goo7wpa0wc-image.image) </span>


|**Field** |**Field meaning and usage** |
|---|---|
|**Channel frequency control** |Reach conducted through this channel will undergo channel frequency control; if multiple options are selected, all conditions must be met. Currently supports daily, weekly, and monthly frequency control. |
|**Channel do\-not\-disturb settings** |Reach conducted through this channel will implement channel do\-not\-disturb. The message delivery task, process canvas, and the strategy tools within the process canvas can also be set individually with the 'Do Not Disturb' mode. If multiple 'Do Not Disturb' settings are activated, each condition must be satisfied. |
|**Channel reach blacklist** |Multiple IDs can be entered, separated by a return key. Users included in the entered blacklist will not be reached. The number of IDs entered is recommended to be less than 20. |
|**Channel reach whitelist** |Multiple IDs can be entered, separated by a return key. After entering this list, only the users specified in the whitelist will be reached; all others will not be reached. This scenario is suitable for debugging and verification at the initial stage of channel creation, intended for internal operational staff only. The number of IDs entered is recommended to be less than 20. |
|**Channel Whitelist** |Multiple IDs can be entered, separated by a return key. After entering this list, the users in this whitelist will not be subject to channel frequency control limitations. However, if a frequency control at the task dimension is set, the user IDs within this list will still be managed. The recommended ID value should be within 20. |


<span id="e96712b6"></span>
#### **5.3.3. Mini Program Subscription Message Configuration**


|**Core Steps** |**Operation Instructions** |
|---|---|
|1. Access WeChat Mini Program |**Management Center \- Channel Management \- WeChat Mini Program \- Add New Mini Program**<br><br><br>* **Access method:**  Third\-party authorization mode<br><br>* **ID type:**  app_id+open_id<br><br>* **QPS limit:**  Fill in yourself (calls per second, maximum value is 2000)<br><br>* **Authorization**: Mandatory "Obtain Mini Program Code"  **,**  "Mini Program Basic Information Management"  **,**  "Mini Program Link Management"; [Permission Set Detailed Introduction](https://developers.weixin.qq.com/doc/oplatform/Third-party_Platforms/2.0/product/third_party_authority_instructions.html)<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0672af2de510410abafa0fe598da4156~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fed8985c1ee4406a55ad9ebb16fa9e4~tplv-goo7wpa0wc-image.image) </span> |
|2. Subscribe Message Configuration |**Management Center \- Channel Management \- WeChat Mini Program \- Mini Program Subscription Messages Configuration**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80a0250560ad46a09b9a9fc9842bef86~tplv-goo7wpa0wc-image.image) </span><br><br>Description: If authorization for Mini Program Development and Data Analysis is granted during the integration of the mini program, the subscription message configuration is as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ccfc705cab6470f807e7769e1922b95~tplv-goo7wpa0wc-image.image) </span> |
|3. Access Token Configuration (see integration mode comparison for interactive logic) |**Method One:**  Please configure the mini program secret (secret) into the GMP platform. Once effective, we will use appID and secret to call the mini program interface<br><br>**Method Two:**  This method is generally used when the mini program is managed by a third party and an Token token has been generated previously, paste the URL to get the Access Token; and configure your HTTP service to use GET method, returning accessToken information in JSON format:<br><br>```JSON```<br>```{```<br>```    "errcode": 0,   // 0代表成功，非0代表失败```<br>```    "errmsg": "",   // 失败时的错误信息```<br>```    "access_token": "", // accessToken```<br>```    "expires_in": 7200  // accessToken剩余的有效期时间，单位秒```<br>```}```<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87a0226ac9d44f309ba95b366192eac0~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Version 5.6 update: when GMP requests the 'Access Token Url' from the counterpart, it supports two request methods, non\-authentication and aksk authentication, requiring ak, sk, and signature validity period. During the request, GMP will calculate the signature and place it in the Authorization header.<br><br><br>For detailed calculation method, see [GMP ak/sk authentication calculation explanation](https://www.volcengine.com/docs/6315/1472192)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a73a23c6022f4e71a4f1623f67add61a~tplv-goo7wpa0wc-image.image) </span> |
|4. Event Callback Address Configuration<br><br><br>(Event Callback Address Integration Mode Comparison) |**Configuration Method**<br><br><br>* "Developer Mode Access to Mini Programs": Similar to developer mode available for GMP usage<br><br>* "Non\-Developer Mode Access to Mini Programs": The client has outsourced the mini program to a third party; for example:<br><br>   * The client has developed a WeChat service platform and needs to select "Non\-Developer Mode Access to Mini Programs"<br><br>   * The client has previously used developer mode to interface with the mini program and needs to select "Non\-Developer Mode Access to Mini Programs"<br><br><br>**URL Server Address (GMP WeChat Receipt Reception Address)** <br><br><br>* "Developer Mode Access to Mini Programs": Log in to the WeChat backend \> Development Management \> Development Settings \> Message Push, paste the GMP platform's URL server address, this address needs to include ?wechat_appid=. For example: https://xxx/gmp/wechatproxy?wechat_appid=xxx<br><br>* "Non\-Developer Mode Access to Mini Programs": No need to copy the URL server address to the WeChat backend<br><br>   * If a push event is required, please send the event to **URL Server Address (GMP WeChat Receipt Reception Address)** <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Event Callback Process for Third\-Party Mini Program Development:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="tip">GMP will provide a receipt interface address (the interface protocol is consistent with the protocol required by WeChat callback interface, which also supports direct calling of push event information from WeChat).</div><br><br><br>2. <div data-tips="true" data-tips-type="tip">After receiving the event information pushed from WeChat, the customer's existing WeChat callback interface calls the receipt interface provided by GMP to synchronize the event information pushed from WeChat to GMP.</div><br><br><br><br><div data-tips="true" data-tips-type="tip"><a href="https://developers.weixin.qq.com/miniprogram/dev/framework/server-ability/message-push.html">WeChat Callback Request Parameters Description</a></div><br><br><br><div data-tips="true" data-tips-type="tip"><a href="https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/subscribe-message.html#%E8%AE%A2%E9%98%85%E6%B6%88%E6%81%AF%E8%AF%AD%E9%9F%B3%E6%8F%90%E9%86%92">Explanation of the Meaning of Each Section in the Receipt Content</a></div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>When forwarding by a third party, a "wechat_appid" query parameter must be added to the path</strong></div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Query Parameters:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">wechat_appid: WeChat appid</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">encrypt_type: Encryption Type</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">timestamp: Timestamp</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">nonce: Random Number</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">msg_signature: WeChat Encryption Signature, the signature combines the token parameter filled in by the developer and the timestamp and nonce parameters in the request.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Body parameters, consistent with the body returned by WeChat:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">XML Format Example</div><br><br><br>   <div data-tips="true" data-tips-type="tip">161096946817008271328195543040   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip">JSON Format Example</div><br><br><br>   <div data-tips="true" data-tips-type="tip">{   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"ToUserName": "gh_123456789abc",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"FromUserName": "o7esq5PHRGBQYmeNyfG064wEFVpQ",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"CreateTime": "1620963428",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"MsgType": "event",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"Event": "subscribe_msg_sent_event",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"List": {   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"TemplateId": "BEwX0BO\-T3MqK3Uc5oTU3CGBqzjpndk2jzUf7VfExd8",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"MsgID": "1864323726461255680",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"ErrorCode": "0",   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">"ErrorStatus": "success"   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">}   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip">}   </div><br>   <br><br><br>**Token, EncodingAESKey:** <br><br><br>* "Developer Mode Access to Mini Programs": Log in to the WeChat Open Platform \> Development Management \> Development Settings \> Message Push, then copy and paste the content into the GMP platform<br><br>* "Non\-Developer Mode Access to Mini Programs": Fill in Token and EncodingAESKey consistently with the third\-party platform<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c3ae9d4064b4d2e8a87948cebf2e856~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd727a0a65b140df8585756134034136~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11a73f63020467896101f8d0bc3a2f3~tplv-goo7wpa0wc-image.image) </span><br><br>**Message Encryption Method:** <br><br><br>* "Developer Mode Access to Mini Programs": Consistent with the Mini Program backend<br><br>* "Non\-Developer Mode Access to Mini Programs": Maintain consistency with the third\-party platform configuration<br><br><br>**Data Format:** <br><br><br>* "Developer Mode Access to Mini Programs": Consistent with the Mini Program backend<br><br>* "Non\-Developer Mode Access to Mini Programs": Maintain consistency with the third\-party platform configuration |


**Comparison of Access Modes**

**Comparison of Access Token Entry Modes (Sending Link)** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a09f161de15b48c6a830c75d4543266b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6a550407bae49a5894dd655ad613db0~tplv-goo7wpa0wc-image.image) </span>

**Comparison of Event Callback URL Entry Modes (Receipt Link)** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdb514056b5d41498696a95142ab04b6~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bea9928fd92547af83e96175b42ce0d7~tplv-goo7wpa0wc-image.image) </span>

<span id="fd35da65"></span>
#### **5.3.4. Send Mini Program Subscription Messages**


|**Core Steps** |**Operation Instructions** |
|---|---|
|1. Select Mini Program Subscription Messages delivery method |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dd689969fa742a286da453b17fea8da~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Click 'Confirm' to validate whether the selected Mini Program has completed subscription message configuration in [Channel Management] |
|2. Set up sending subscription messages |The audience users, trigger conditions, and target settings are the same as other Message Delivery Tasks on the GMP platform<br><br>Delivery configuration: Supports choosing a Mini Program Subscription Messages template, configure fields based on the selected template; after clicking the template card, it will redirect to a page that only supports this Mini Program<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a776e7ec502248728f88c2bf3f4d2928~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/588d763854d14d6994fbce8b16ff381f~tplv-goo7wpa0wc-image.image) </span> |


<span id="f3e462ef"></span>
## 6. WeChat Mini Program Pop\-up

<span id="d5424824"></span>
### 6.1. Product Overview

WeChat Mini Program pop\-up allows pop\-ups on the WeChat Mini Program pages. To use the WeChat Mini Program pop\-ups, you must first integrate the BytePlus SDK. If needed, please contact the BytePlus Project Manager or Client Success Manager.

<span id="91554465"></span>
### 6.2. Usage Restrictions


| **[ 📢 Prerequisite for using this function ]**  ||
|---|---|
|1. **Activate GMP permissions** |Administrator activates permissions, permission path: Management Center\-Channel Management\-WeChat Mini Program Pop\-up |


<span id="41cbb6c1"></span>
### 6.3. Feature Description

The integration process for the WeChat Mini Program Pop\-up is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e90c9a78c026473bbcc36f58ff39f2b8~tplv-goo7wpa0wc-image.image" width="3222px" /></div>


<span id="f449eb51"></span>
#### **6.3.1. Mini Program Authorization**

For WeChat Mini Program authorization, please refer to the previous chapter "[WeChat Mini Program](https://www.volcengine.com/docs/6315/67403#_5-%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F)".

<span id="360f8dbc"></span>
#### **6.3.2. Accessing the SDK**

[Refer to technical integration documents](https://www.volcengine.com/docs/6315/1222894), and contact BytePlus project manager or customer success manager if there are any questions.

<span id="a1d15ba4"></span>
#### **6.3.3. Configure Template**

Click on 'Add New Template' to enter the template editing page, or 'Update Configuration' based on an existing system template.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5778cd5f5a94a21b6cf0ad84c9fc3f2~tplv-goo7wpa0wc-image.image" width="1901px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/870260861f3547d2a575809af4e49fc2~tplv-goo7wpa0wc-image.image" width="1909px" /></div>


Popup templates created through the visual editor can flexibly adjust layout and components based on needs, and each component's content and style can be reset during campaigns. Component Support: Supports three types of components \- Image, text, and button.

<span id="ee6d4c26"></span>
#### **6.3.4. Frequency Control and Blacklist/Whitelist Setting**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f64404115f547edbc9f21e85fdbcedd~tplv-goo7wpa0wc-image.image" width="1899px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Channel Frequency Control** |Any outreach conducted through this channel will be subject to channel frequency control. If multiple conditions are selected, all conditions must be met. Currently supports daily, weekly, and monthly frequency control. |
|**Channel Do Not Disturb Settings** |Any outreach conducted through this channel will implement channel do not disturb. Message Delivery Tasks, Process Canvases, and devices within the Process Canvas can also have separate do not disturb settings. If do not disturb is set simultaneously, all do not disturb conditions must be satisfied. |
|**Channel Outreach Scope Blacklist** |Multiple IDs can be entered, separated by enter/return, and listed blacklist users will not be contacted. The number of IDs entered should preferably be no more than 20. |
|**Channel Outreach Scope Whitelist** |Multiple IDs can be entered for the whitelist, separated by line breaks. Once this whitelist is specified, the reach will be limited to only the few users listed in it; all other users will not be reached. This scenario is suitable for channel creation and initial debugging verification, and is only available to internal operations staff. The number of IDs entered is recommended to be no more than 20. |
|**Channel Whitelist** |Multiple IDs can be entered for the whitelist, separated by line breaks. After specifying this whitelist, these users will not be subject to channel frequency control restrictions. However, if the task has set frequency control at the task level, the user IDs in this list will still be managed. The number of IDs entered is recommended to be no more than 20. |



---



<span id="4b40903c"></span>
## 7. App Popup

<span id="e51f1c7b"></span>
### 7.1. Product Overview

The App pop\-up can facilitate pop\-ups on apps; to use [App pop-up, you must first integrate the GMP SDK](https://www.volcengine.com/docs/6315/1171069). If needed, please contact the BytePlus project manager or the customer success manager.

<span id="f72fe1a1"></span>
### 7.2. Usage Restrictions


| **[ 📢 Prerequisite for using this feature ]**  ||
|---|---|
|1. **Grant GMP Permission** |Administrators enable permissions, permission path: Management Center \- Channel Management \- WeChat Mini Program Pop\-up |


<span id="18628243"></span>
### 7.3. Feature Description

The process for integrating the App pop\-up is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f486f263101740edb60e9eef07fb1f23~tplv-goo7wpa0wc-image.image" width="3222px" /></div>


<span id="8595f3dc"></span>
#### **7.3.1. Create an Application**

You need to create an application on the “**Management Center\-App Pop\-up**” page. Subsequent pop\-up templates will be managed based on the application dimension.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93b2c75920f242b1aad671a46eae3708~tplv-goo7wpa0wc-image.image" width="1917px" /></div>


<span id="eed5ed47"></span>
#### **7.3.2. Integrate the SDK**

You can refer to the [technical docking documentation](https://www.volcengine.com/docs/6315/1171069). If you have any questions, please contact the BytePlus project manager or customer success manager.

<span id="961a1b74"></span>
#### **7.3.3. Configure the Template**

Click to add a new template or update existing configuration via "**Update Configuration**".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1de925920d4443e4ab80942c5b8c0068~tplv-goo7wpa0wc-image.image" width="1901px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45fe9eb7981b4236b628c4d843f69274~tplv-goo7wpa0wc-image.image" width="1909px" /></div>


The pop\-up templates created with the visual editor can flexibly adjust the layout and components according to the requirements, where the content and style of each component can be reset during campaigns. Component support: Supports three types of components – Image, Text, and Button.

<span id="b8e29bbb"></span>
#### 7.3.4. **Frequency Control and Whitelist/Blacklist Settings**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9356aa758929441a8685de62c2b84bd8~tplv-goo7wpa0wc-image.image" width="1899px" /></div>



|**Field** |**Field Meaning and Usage** |
|---|---|
|**Channel Frequency Control** |Access via this channel will undergo channel frequency control; if multiple options are selected, all conditions must be met. Currently supports daily, weekly, and monthly frequency controls. |
|**Channel Do Not Disturb Settings** |Access via this channel will implement channel do not disturb. Message Delivery Tasks, Process Canvases, and Strategy Tools in the Process Canvas can also have their own do not disturb settings; if do not disturb is set simultaneously, all do not disturb conditions must be satisfied. |
|**Channel Outreach Range Blacklist** |Multiple IDs can be entered, with multiple blacklists separated by a return; users on the entered blacklist will not be reached. The number of IDs entered is recommended to be within 20. |
|**Channel Reach Whitelist** |ID can contain multiple values. Separate multiple whitelist IDs with a newline. Filling out this list means that only the users specified in the whitelist will be reached through the channel, and all other users will not be accessed. This scenario is suitable for debugging and verifying at the initial stage of channel creation and is intended only for internal operational staff. The number of ID values should ideally be no more than 20. |
|**Channel Whitelist** |ID can contain multiple values. Separate multiple whitelist IDs with a newline. Adding names to this list means that these whitelist users will not be subject to channel frequency control limits. However, if the task has set task\-level frequency control, the user IDs in these lists will still be regulated. The number of ID values should ideally be no more than 20. |
