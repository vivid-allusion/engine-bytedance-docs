---
title: "Managing live sources"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming"
---

By managing live sources, you can configure multiple sources in a live room. This allows viewers to choose from these sources to watch live videos.

<span id="d5392021"></span>
## What your viewers see


<Tabs>
<Tab zoneid="dBcPs4u46e" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fde93276d764da39d14576e7383115b~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="NWiriP1rI0" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ff36330346a423db81708abe8e9083f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="1a481fa1"></span>
## Prerequisite

A BytePlus account or an IAM user with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="dd9b2127"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the **Broadcast method** tab under the player, click **Manage live sources**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c1dd50431c7408ca2d44e56e104d5d5~tplv-goo7wpa0wc-image.image) </span>

4. In the **Manage live sources** dialog box that appears, add sources and complete the configurations as needed for sources viewers can choose from during the live stream.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57ed631089c1432c898e770465f5427a~tplv-goo7wpa0wc-image.image) </span>

   * Display name on viewing page: Enter the name of the source selection entry on the viewing page.

   * Click **Add** to add sources and complete the configurations as needed.

      * Source name: Enter the name of the source.

      * Cover: Upload the cover for the source.

      * Source language: Select the default page language for the source. The live content to play on the viewing page by default is determined by the language settings of the viewer's PC browser or mobile device. For example, if the language of source A is set to English, and the viewer's PC browser language is also English, then when the viewer enters the live room, the viewing page will play the live content of source A by default.

      * Quality: Select one or more resolutions for the source. Viewers can only switch between the resolutions selected here. A higher resolution requires better network conditions.

      * Primary/Backup stream: With the switch turned on, the source has a primary stream and a backup stream. The system will push both the primary and backup streams to viewers during the live stream, and viewers will watch the live content from the primary stream. If the primary stream is interrupted, the system automatically switches to the backup stream, which ensures the stability of live streaming.

      * Ultra\-low latency: With the switch turned on, viewers selecting this source can watch ultra\-low latency live streaming with a latency of 1 to 2 seconds. For more information, see [Ultra-low latency live streaming](https://docs.byteplus.com/docs/byteplus-livesaas/ultra-low-latency-live-streaming).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A live room can have at most 20 sources.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot modify the configurations during a live stream.   </div>
   

5. Select the source from the **Switch source** drop\-down list and then configure the broadcast method for the source.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4dbbce05e964482a16754ce91ffbb83~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, you cannot live stream in multiple sources at the same time if you choose to live stream from your web browser.   </div>
