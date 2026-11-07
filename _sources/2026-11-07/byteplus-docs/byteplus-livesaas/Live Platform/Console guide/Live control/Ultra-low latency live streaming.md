---
title: "Ultra-low latency live streaming"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ultra-low-latency-live-streaming"
---

BytePlus Live supports ultra\-low latency live streaming for tens of millions of concurrent viewers. Compared to normal latency live streaming with a latency of 5 to 10 seconds, ultra\-low latency live streaming can reduce latency to 1 to 2 seconds, offering you a smooth and high\-quality live viewing experience.

<span id="c0e8a860"></span>
## Context

With the rapid evolution of the "Live Streaming+" model across various industries, diverse forms of interactive live streaming such as e\-commerce, online classes, sports events, and interactive entertainment are becoming increasingly common. As the demand for real\-time interaction in live streaming grows among users, the era of end\-to\-end millisecond latency has arrived. Ultra\-low latency live streaming dramatically enhances the experience for both hosts and viewers in live scenarios like e\-commerce and online classes. The lower the latency, the more immediate and engaging the live streaming becomes. Therefore, reducing latency is essential to offering an improved live streaming experience.

<span id="cd0cd3c9"></span>
## Scenarios

Ultra\-low latency live streaming is ideal for the following live scenarios that require low network latency and strong interaction.


* E\-commerce: Hosts can immediately see viewers' comments and sales feedback after listing products, thereby enhancing the interaction between hosts and viewers, as well as the conversion rate of product purchases.

* Online classes: If students have questions about the knowledge points explained by the teacher and ask in the chat area, the teacher can respond promptly, thereby enhancing the quality of teaching.

* Sports events: Viewers can get real\-time updates on the situation at the venue.

* Interactive entertainment: When viewers reward hosts with gifts, they can get immediate feedback from hosts, thereby enhancing the interaction between hosts and viewers.

* Medical diagnosis: In a medical open class or live medical scenario, viewers can receive instant replies or diagnoses.


<span id="1e6289dc"></span>
## Prerequisites


* A BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

* Viewers who use the following browsers can watch ultra\-low latency live streaming:

   * Google Chrome

   * Safari

   * Lark

   * WeChat

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The latest version is recommended to ensure a smooth viewing experience.   </div>
   

<span id="438a3e77"></span>
## Notes


* Compared to normal latency live streaming, the watch time for ultra\-low latency live streaming is counted at a ratio of 1:2. For example, if you have 1,000 viewers and each of them has watched 30 minutes of normal latency live streaming, previews, or playbacks, along with 20 minutes of ultra\-low latency live streaming, then 70,000 minutes (1,000x30+1,000x20x2) of watch time is consumed.

* Currently, you cannot pull an ultra\-low latency live stream by using the pull stream broadcast method.


<span id="4bc5ee5c"></span>
## Procedure

You can enable the ultra\-low latency feature in the following two ways.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot enable or disable the ultra\-low latency feature during a live stream.</div>


<span id="05ea83b2"></span>
### Method 1: Create an ultra\-low latency live room


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Create live room** on the **Live rooms** page.

3. On the **Create a live room** tab of the **Create live room** page, select **Ultra\-low latency** as the live stream latency.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1541020d106648b880197745219aa65e~tplv-goo7wpa0wc-image.image) </span>

4. Complete the other configurations as instructed and click **Save**.


<span id="438f2c1b"></span>
### Method 2: Enable the ultra\-low latency feature in an existing live room


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the **Broadcast method** tab under the player, click **Manage live sources**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc836721eed3407eaeaf48cae3bf2c19~tplv-goo7wpa0wc-image.image) </span>

4. In the **Manage live sources** dialog box that appears, turn on the **Ultra\-low latency** switch for one or more live sources to enable the ultra\-low latency feature for these sources.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5297e47a59fd4cf987d7f7c98e0bd5c8~tplv-goo7wpa0wc-image.image) </span>

5. Click **Confirm**.
