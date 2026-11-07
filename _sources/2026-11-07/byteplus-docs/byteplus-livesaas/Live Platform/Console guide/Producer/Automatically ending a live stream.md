---
title: "Automatically ending a live stream"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/automatically-ending-a-live-stream"
---

By enabling the feature of live stream end time, a countdown timer is displayed on the live streaming page in a web browser after the stream starts. This timer provides the host with a clear view of the remaining time until the end of the stream. The live stream will automatically end once the specified end time arrives. This feature is widely applicable to educational and training scenarios.

<span id="cebaa5c6"></span>
## What the host sees

The countdown timer is displayed on top of the live streaming page and becomes more noticeable within the last 5 minutes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dbaf059519845edba078044978fa042~tplv-goo7wpa0wc-image.image) </span>

<span id="f9c9a280"></span>
## Prerequisite

A BytePlus account or an IAM user. To enable the feature in an existing live room, the IAM user must have the Producer \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="843c2dbd"></span>
## Procedure

You can enable the feature of live stream end time in one of the following ways.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The live stream end time must be later than the start time, with a maximum difference of 72 hours.</div>


* <div data-tips="true" data-tips-type="tip">You cannot enable or disable the feature, or modify the live stream end time during a live stream.</div>


* <div data-tips="true" data-tips-type="tip">After the live stream automatically ends, you must reset the live stream time to start the stream again.</div>



<span id="8577380a"></span>
### Method 1: Create a live room with the feature enabled


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Create live room** on the **Live rooms** page.

3. On the **Create live room** page, choose to create one or more live rooms at a time.

   * Create a live room: On the **Create a live room** tab, turn on the **End time** switch and configure the end time. Complete the other configurations as indicated and click **Save**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ac3050042e342e788b6dc0fc2ade6df~tplv-goo7wpa0wc-image.image) </span>

   * Create multiple live rooms at a time: On the **Create multiple live rooms** tab, click **Add live** or **Add recording**. Turn on the **End time** switch and configure the end time. Complete the other configurations as indicated and click **Save**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a7498401bd2413da41f838b442b8099~tplv-goo7wpa0wc-image.image) </span>


<span id="9bc33c31"></span>
### Method 2: Enable the feature in an existing live room


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Producer** \> **Basic information**.

4. In the **Basic settings** section, turn on the **End time** switch and configure the end time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59d0b707405141b7b1ad91f86993a88b~tplv-goo7wpa0wc-image.image) </span>
