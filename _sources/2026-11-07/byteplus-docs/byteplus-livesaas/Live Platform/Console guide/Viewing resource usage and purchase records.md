---
title: "Viewing resource usage and purchase records"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-viewing-resource-usage"
---

On the **Account overview** page, you can view your resource usage and purchase records.

<span id="prerequisite"></span>
## Prerequisite

A BytePlus account or an IAM user with Account overview \> View only or Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="procedure"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the left navigation bar, click **Account overview**.

3. On the **Account overview** page, view the following data.

   * Media library capacity usage only includes uploaded videos and playbacks that have been transferred to the video library.

   * The peak daily media library capacity usage is considered your actual usage for that day. For example, if you store 100 GB of videos and then delete 50 GB, your usage is 100 GB. If you then add another 20 GB the next day, your usage for that day is calculated as 70 GB (100 \- 50 + 20).

   
   |Figure |Description |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66c5d8601f824d268b427b9475d9f297~tplv-goo7wpa0wc-image.image) </span> |Your subscribed feature version and the corresponding expiration date. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bec78588846e4ade84d70b2e72ec5296~tplv-goo7wpa0wc-image.image) </span> |You can view the following data in a specific time range. If today is the first day of the month, you can view data from the last month. Otherwise, you can view data from the first day of the current month to yesterday.<br><br><br>* Total watch time: Viewers' watch time of live videos, playbacks, and previews.<br><br>* Maximum concurrent viewers: The peak concurrent viewers in all live rooms.<br><br>   Devices with identical device IDs are considered the same device. Viewers who use the same device are regarded as one person.<br><br>* Total co\-host time: The total co\-host time of hosts and guests.<br><br>* Media library capacity usage: The usage in the media library.<br><br><br>Data is updated at 00:30 (UTC+0) every day. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc126ecab06740438862b51891a8dd9d~tplv-goo7wpa0wc-image.image) </span> |You can view the following data.<br><br><br>* The available concurrent viewers, watch time, co\-host time, and media capacity.<br><br>* The total amount of watch time, co\-host time, and media capacity in the corresponding package.<br><br>* The percentage of the available amount relative to the total amount.<br><br><br>The available watch time and co\-host time are updated daily at 9:00 AM (UTC+0) if billed daily, or at the beginning of each month if billed monthly. Other data is updated in real time. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4903f1a71c174b78b0b54007b16b9b1a~tplv-goo7wpa0wc-image.image) </span> |Your subscribed feature version and resource packages, whether they are in use, used up, or expired, and their available resources, validity period, and source.<br><br>The available watch time and co\-host time are updated daily at 9:00 AM (UTC+0) if billed daily, or at the beginning of each month if billed monthly. Other data is updated in real time. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ce29ce31b334ba781873d545233e671~tplv-goo7wpa0wc-image.image) </span> |Viewers' watch time of normal latency live streaming, previews, playbacks, live streams pushed to third\-party platforms, ultra\-low latency live streaming, and the total watch time.<br><br>You can perform the following operations.<br><br><br>* Select an organization from the **Organization** drop\-down list to view the corresponding usage of the selected organization.<br><br>* Filter data based on the time range.<br><br>* Select the time granularity in the chart.<br><br>* Click **Normal latency live**, **Preview**, **Playback**, **Multi\-platform streaming**, **Ultra\-low latency live**, or **Total duration** to hide or display the corresponding data in the chart.<br><br>* Move your pointer over the chart to view the watch time and the corresponding time point.<br><br>* The watch time of live streams pushed to third\-party platforms cannot be displayed on this page in real time but with a one\-day delay, while the other data is updated in real time.<br><br>* You will see the watch time of live streams pushed to third\-party platforms only if the multi\-platform streaming feature is enabled. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9076ce55330b43d5a52317c087419217~tplv-goo7wpa0wc-image.image) </span> |The peak concurrent viewers in all live rooms. Data is updated in real time.<br><br>You can perform the following operations.<br><br><br>* Select an organization from the **Organization** drop\-down list to view the corresponding usage of the selected organization.<br><br>* Filter data based on the time range.<br><br>* Select the time granularity in the chart.<br><br>* Click **Billable concurrent viewers**, **Normal latency concurrent viewers**, or **Ultra\-low latency concurrent viewers** to hide or display the corresponding data in the chart.<br><br>* Move your pointer over the chart to view the number of concurrent viewers and the corresponding time point.<br><br><br>The number of billable concurrent viewers is the sum of normal latency concurrent viewers plus twice the number of ultra\-low latency concurrent viewers. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a834970afdfc45b58bfe3f2817fd6ea9~tplv-goo7wpa0wc-image.image) </span> |The total co\-host time of hosts and guests. Data is updated in real time.<br><br>You can perform the following operations.<br><br><br>* Select an organization from the **Organization** drop\-down list to view the corresponding usage of the selected organization.<br><br>* Filter data based on the time range.<br><br>* Select the time granularity in the chart.<br><br>* Move your pointer over the chart to view the co\-host time and the corresponding time point. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b5d922904b349c19a5113559392dd32~tplv-goo7wpa0wc-image.image) </span> |The total usage in the media library. Data is updated in real time.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the time range.<br><br>* Move your pointer over the chart to view the usage and the corresponding time point. |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/353f5575fc6e4bc88df2c3e6b081fa34~tplv-goo7wpa0wc-image.image) </span> |You can get URLs for videos in the media library by calling a specific server\-side API. You can then play these videos using your own player. The watch time for these videos will be displayed on the Third\-party Video on Demand (VOD) watch time tab. For more information on the server\-side API, contact BytePlus Live technical support. |
