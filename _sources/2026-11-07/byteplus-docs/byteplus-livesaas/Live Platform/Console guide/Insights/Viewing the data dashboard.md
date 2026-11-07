---
title: "Viewing the data dashboard"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewing-the-data-dashboard"
---

During a live stream, you can view streaming data in real time on the data dashboard, which allows you to adjust your streaming strategies in time for achieving the best streaming effects.

<span id="a96c04c4"></span>
## Prerequisite

A BytePlus account or an IAM user with the following permissions at the same time. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


* Live control \> View only or Edit permission.

* Insights \> View only or Edit permission.


<span id="28448298"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. Click **Data dashboard** under the player.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b055ba441d5414493b91d949796398d~tplv-goo7wpa0wc-image.image) </span>

4. View the following data metrics on the data dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e900f91dbb34d649a9c86ce9aa7a7b7~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Data on the dashboard is refreshed automatically.</div>


* <div data-tips="true" data-tips-type="tip">You can view data within the following time ranges.</div>


   * <div data-tips="true" data-tips-type="tip">User portrait: Data from the past 30 days.</div>


   * <div data-tips="true" data-tips-type="tip">Online viewers: Data in the last 1, 2, and 3 hours, the latest live stream, or during a live stream.</div>


   * <div data-tips="true" data-tips-type="tip">Product cards, real\-time comments, and top comments: All the data in the live room.</div>


   * <div data-tips="true" data-tips-type="tip">Other metrics: Data from the past year.</div>




|Screenshot |Metric |Description |Unit |Granularity |Update frequency |
|---|---|---|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68e873f19e5a458a8cfbd0407173c62c~tplv-goo7wpa0wc-image.image) </span> |Live stream time |The live stream time configured on the **Producer** \> **Basic information** page of your live room. Format: mm\-dd\-yyyy hh:mm. |Not applicable |Fixed value |Not applicable |
||Live duration |The duration of the live stream in the live room. |Seconds |Cumulative |In real time |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f14a3995e41f4e8980c07e76864b8911~tplv-goo7wpa0wc-image.image) </span> |Live room status |Displayed on top of the dashboard.<br><br>Valid values:<br><br><br>* Preview<br><br>* Live<br><br>* Playback<br><br>* Over |Not applicable |Not applicable |In real time |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0a75609d8c24d888a6a6f6e65bf011d~tplv-goo7wpa0wc-image.image) </span> |Online viewers |The number of online viewers in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person. |People |Real\-time |1 minute |
||UV |The number of unique viewers in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person.<br><br>For example, if one viewer visits the viewing page twice using Device A, another viewer visits the viewing page once using Device B, and one more viewer visits the viewing page three times using Device C, the number of unique viewers increases by 3. |People |Cumulative |1 minute |
||PV |The number of views in the live room.<br><br>For example, if one viewer visits the viewing page twice and another viewer visits the viewing page once, the number of views increases by 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer refreshes the viewing page once during the visit, the number of views increases by 1.</div><br> |Times |Cumulative |1 minute |
||Peak online viewers |The peak concurrent viewers in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person. |People |Real\-time |1 minute |
||Average watch time |The average watch time per viewer in the live room, which is calculated as the total watch time for all viewers in the live room divided by the number of unique viewers (UV).<br><br>For example, if the total watch time is 1000 minutes and the number of unique viewers is 20, the average watch time is 50 minutes (1000/20). |Minutes |Cumulative |1 minute |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c36997317764d04ab0611469f674a02~tplv-goo7wpa0wc-image.image) </span> |Number of comments |The number of comments sent by the host, viewers, guests, and bots in the live room, including deleted comments and comments under review. |Not applicable |Cumulative |1 minute |
||Number of likes |The displayed number of likes for the live room. |Not applicable |Cumulative |1 minute |
||Number of gifts |The number of gifts sent in the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metric appears only when you enable the gift rewards feature.</div><br> |Not applicable |Cumulative |1 minute |
||Live room shares |The total number of times viewers click **Live poster** or **Share** on the viewing page of PCs and click the share icon on the viewing page of mobile devices. |Times |Cumulative |1 minute |
||Lucky draw participations |The number of times viewers participate in real\-time lucky draws in the live room. |Times |Cumulative |1 minute |
||Gift value |The total points used for redeeming gifts sent in the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metric appears only when you enable the gift rewards feature and has a value only when viewers redeem points for gifts to reward hosts.</div><br> |Points |Cumulative |1 minute |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca09fd52e40451cb0c19dc24af8cd93~tplv-goo7wpa0wc-image.image) </span> |User portrait \- Country, Province, or City |The geographic distribution of viewers in the live room, presented as percentages.<br><br>Only the top 5 countries, provinces, and cities by percentage of viewers can be displayed on the corresponding tab. |% |Cumulative |1 minute |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fa680498b61408886efeed89088fbad~tplv-goo7wpa0wc-image.image) </span> |User portrait \- Source |The source distribution of viewers in the live room, that is, the distribution of viewers based on the channels they come from.<br><br>Only the top 5 channels and their corresponding percentages can be displayed.<br><br>If no channel is configured, **Default** is displayed with a 100% value, indicating all the viewers come from the primary channel. |% |Cumulative |1 minute |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc833224325d4a58b27f8cc08e1c2fe5~tplv-goo7wpa0wc-image.image) </span> |Online viewers |A trend chart for the number of online viewers in the live room.<br><br>You can select to display the trend chart in the following time range:<br><br><br>* Last 1 hour<br><br>* Last 2 hours<br><br>* Last 3 hours<br><br>* This live stream<br><br>   * If the live room has never started a live stream, this option cannot be selected.<br><br>   * If the live room is in the **Live** status, the trend of online viewers during the live stream is displayed.<br><br>   * If a live stream has ended in the live room, the trend of online viewers in the last live stream is displayed.<br><br><br>Move your pointer over the chart, you can then view the number of online viewers and the corresponding time points. |People |Real\-time |1 minute |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2d7178bd0ab4015a6767908f502e116~tplv-goo7wpa0wc-image.image) </span> |Card data |The number of times (PV) viewers click the product card and the number of unique viewers (UV) who click the product card in the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metric appears only when you enable the menu for product cards.</div><br> |PV: Times<br><br>UV: People |Cumulative |1 minute |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffc334fc19a74e3eb96f8900ad1f326e~tplv-goo7wpa0wc-image.image) </span> |Real\-time comments |The comments displayed under the menu for chat interaction on the viewing page. |Not applicable |Not applicable |In real time |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/585e56e9eaa4439a826d2f5ef65d7c13~tplv-goo7wpa0wc-image.image) </span> |Popular |The top comments.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metric appears only when you enable the top comments feature in the menu for chat interaction.</div><br> |Not applicable |Not applicable |In real time |
