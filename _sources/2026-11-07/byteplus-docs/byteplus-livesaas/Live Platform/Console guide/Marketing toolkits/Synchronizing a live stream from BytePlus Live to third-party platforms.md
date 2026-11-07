---
title: "Synchronizing a live stream from BytePlus Live to third-party platforms"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms"
---

You can use the multi\-platform streaming feature to synchronize a live stream from BytePlus Live to third\-party platforms, allowing viewers to watch the same live stream simultaneously on different platforms and expanding the reach of your live streaming content.

<span id="prerequisite"></span>
## Prerequisites


* A BytePlus account or an IAM user with **Marketing toolkits** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

* To synchronize a live stream, you must have permission to go live on the destination platform.


<span id="procedure"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Marketing toolkits** \> **Multi\-platform streaming**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6f1411fec524fed9624f4d489f54cb5~tplv-goo7wpa0wc-image.image) </span>

4. You can add third\-party platforms or get the pull stream address of this live room.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the live room has multiple live sources, only the live stream from the first source can be synchronized to the added third\-party platforms. For more information about multiple live sources, see <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming">Managing live sources</a>. To synchronize the live stream from other sources, contact the sales representative for custom settings. If you do not have a sales representative, click <a href="https://www.byteplus.com/en/contact">here</a> to fill out this form to have our sales team contact you.   </div>
   

   * Add third\-party platforms: Click **Add platform**. In the **Add platform** dialog box, select the platform to which you want to synchronize the live stream. Then, enter the name and push stream address of the platform. The **Stream pushing** switch is turned on by default. For more information about how to get the push stream address, see the next section.

      With the **Stream pushing** switch enabled, the stream is automatically synchronized to the platform when your live event starts, allowing viewers to watch on both BytePlus Live and the third\-party platform simultaneously.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/032aa5707a0c4a1cbe5163059bee305a~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only push stream address in RTMP format is supported.      </div>
      

   * Get the pull stream address: Click **Get pull stream address** and then copy the address in the dialog box that appears. You can use this address on a third\-party platform to synchronize the live stream from this live room to the platform.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c4672bbd0f94f018254c6526b42a7cf~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each live room has only one pull stream address.      </div>
      

5. Start a live stream using broadcast methods except for prerecorded videos.

6. (Optional) After adding third\-party platforms, you can perform the following operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2df6c1cbf4c4d91a0b2c178330dfd63~tplv-goo7wpa0wc-image.image) </span>

   * View push stream status.

   * Edit or delete platform information.

   * Turn on or off the **Stream pushing** switch to synchronize or stop synchronizing the live stream to specific platforms.


<span id="how-to-synchronize-a-live-stream-to-major-live-streaming-platforms"></span>
## How to synchronize a live stream to major live\-streaming platforms

This section describes how to get the server URL and stream key on the following major live\-streaming platforms: TikTok, YouTube Live, MetaLive (Facebook), LinkedIn Live, Twitch, and Instagram.

The following platforms may change the methods for getting the push stream address and requirements for being able to go live due to changes in their policies. Refer to the latest requirements of specific platforms.

<span id="tiktok"></span>
### TikTok

The following steps explain how to find your server URL and stream key on TikTok and add them to the BytePlus Live console.


1. Find and copy the server URL and stream key on TikTok.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You must copy the server URL and stream key each time you go live on TikTok.   </div>
   

   
   <Tabs>
   <Tab zoneid="W9maGC549g" title="TikTok App">
   <TabTitle>TikTok App</TabTitle>
   
   Find and copy the server URL and stream key on TikTok App.
   
   
      1. Open your TikTok App.
   
      2. Go to the navigation bar at the bottom and tap the plus " **+** " button.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75eece96c4641228a643f1cd42f32c8~tplv-goo7wpa0wc-image.image) </span>
   
      3. Select the **Cast on PC/Mac** option and then click **Go LIVE**.
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If this option is not visible, your account lacks permission to go live. For more information, see <a href="https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2">Who can use LIVE on TikTok</a>.      </div>
         
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46afb30216844bde9f52f0791d2ed725~tplv-goo7wpa0wc-image.image) </span>
   
         Then you can see the server URL and stream key.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e09dd69817149a0a826d34c55b31e2d~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   <Tab zoneid="yplmr0RWdV" title="TikTok LIVE Center">
   <TabTitle>TikTok LIVE Center</TabTitle>
   
   Find and copy the server URL and stream key on TikTok LIVE Center.
   
   
      1. Go to the [TikTok LIVE Center](https://livecenter.tiktok.com/producer).
   
      2. On the left navigation pane, click **Go LIVE**.
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If this option is not visible, your account lacks permission to go live. For more information, see <a href="https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2">Who can use LIVE on TikTok</a>.      </div>
         
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43e2a98aa8e040b985d5f3fe581f3569~tplv-goo7wpa0wc-image.image) </span>
   
      3. Enter your stream details and upload a LIVE cover if needed.
   
      4. Click **Save & Go LIVE**.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16680a4d7a344d429a78a4db60fa45df~tplv-goo7wpa0wc-image.image) </span>
   
         This does not start your live stream yet. This generates your server URL and stream key, which you will need to add to BytePlus to start your stream. The server URL and stream key will remain active for 5 minutes, so you need to complete the next section within that time.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/127823a7435147b9ba289b32d03c8e41~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   </Tabs>
   

2. Concatenate the server URL and stream key with a forward slash (/). Make sure the server URL comes first, followed by the stream key.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Make sure there is exactly one <code>/</code> between the server URL and the stream key. For example, the final push stream URL should look like this: <code>rtmps://push-rtmp-xxx-xxxx.tiktokcdn.com:4x3/game/stream-21367xxxxxx9830?amun=true&c=PH&dsnp=1&expire=1776409004&l_region=Singapore-Central&rtcRoomId=762702085xxxxx77522&rtcStreamId=stream-213678483xxxxxx0984_rtc&rtcStreamToken=eyJhbGxxxx-ya0&rtcToken=0015dadxxxxxZs%3D&rtcUserId=7627xxxxxx23443222_8928xxx1812_0&sign=bcxxx4&th_region=sg</code>.   </div>
   

3. Enter the concatenated string as the push stream address in the **Add platform** dialog box of the BytePlus Live console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a28dd17f142344008e47081117852f4b~tplv-goo7wpa0wc-image.image) </span>


<span id="youtube-live"></span>
### YouTube Live


1. Log in to [YouTube Live](https://www.youtube.com/).

2. In the upper\-right corner of the page, click the **Create** icon and select **Go live**.

   If this is your first time enabling the live stream feature, it may take up to 24 hours to get access to live streaming.

3. On the **STREAM SETTINGS** tab, concatenate the stream URL and stream key. Make sure the stream URL comes first, followed by the stream key.

4. Enter the concatenated string as the push stream address in the **Add platform** dialog box of the BytePlus Live console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6887d8038a4d8c868cc4f1b6318c14~tplv-goo7wpa0wc-image.image) </span>


<span id="metalive"></span>
### MetaLive


1. Log in to [Facebook](https://www.facebook.com/live/create).

2. Click **Go live** in the **Go live** section.

3. Select **Streaming software** as your video source.

4. If you want the stream key to be permanently valid, turn on the **Persistent stream key** switch. Otherwise, the stream key cannot be used again after the live stream ends.

5. Concatenate the server URL and stream key with a forward slash (/). Make sure the server URL comes first, followed by the stream key.

6. Enter the concatenated string as the push stream address in the **Add platform** dialog box of the BytePlus Live console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/269d663243664680b93e050dd2e0f107~tplv-goo7wpa0wc-image.image) </span>


<span id="linkedin-live"></span>
### LinkedIn Live

LinkedIn Live is only available to approved users. To check if you are eligible, learn more about access criteria for [LinkedIn Live](https://www.linkedin.com/help/linkedin/answer/a568503?src=li-other&veh=www.linkedin.com%7Cli-other).


1. Log in to [LinkedIn Live](https://www.linkedin.com/video/golive/now/).

2. Select **Go live now** under **New stream** in the upper\-left corner of the page.

3. On the **Stream settings** tab, select your region and then click **Get URL**.

4. Concatenate the stream URL and stream key. Make sure the stream URL comes first, followed by the stream key.

5. Enter the concatenated string as the push stream address in the **Add platform** dialog box of the BytePlus Live console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b20f3fd0857c41bcab188dbaa97d19d3~tplv-goo7wpa0wc-image.image) </span>


<span id="twitch-tv"></span>
### Twitch TV


1. Log in to [Twitch TV](https://www.twitch.tv/).

2. Click your avatar and select **Settings** in the drop\-down list.

3. Click the **Channel and Videos** tab.

4. On the left navigation pane, click **Stream** \> **Settings**.

5. Concatenate the server URL and stream key with a forward slash (/). Make sure the server URL comes first, followed by the stream key. The RTMP server URL of Twitch TV is always `rtmp://live.twitch.tv/app`.

6. Enter the concatenated string as the push stream address in the **Add platform** dialog box of the BytePlus Live console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9fcd551f7f49a5af90766164057405~tplv-goo7wpa0wc-image.image) </span>


<span id="instagram"></span>
### Instagram


1. Enable a professional account.

   1. Log in to [Instagram](https://www.instagram.com/).

   2. Select **More** \> **Settings** on the left navigation pane.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cef1bc62f846f3867c45d8ebebf1ba~tplv-goo7wpa0wc-image.image) </span>

   3. Click **Account type and tools** under **For professionals** and then click **Switch to professional account**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359470824d7d4ac687621d41c153aaf1~tplv-goo7wpa0wc-image.image) </span>

   4. Select **Creator** or **Business** as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dff9b0ecb64d0d9305c96c79ae75fa~tplv-goo7wpa0wc-image.image) </span>

2. Get the stream URL and stream key.

   1. Select **Create** \> **Live video** from the left navigation pane on [Instagram](https://www.instagram.com/accounts/edit/).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8e825007124527b08baa146c13eb3f~tplv-goo7wpa0wc-image.image) </span>

   2. In the dialog box that appears, enter a title for your live video and select your viewers. For this example, select **Public**. Then, click **Next**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a18338b3834fc4b647dfa561bd9f7e~tplv-goo7wpa0wc-image.image) </span>

   3. Get the stream URL and stream key.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eed50beb29d4b078372e9de3bdff193~tplv-goo7wpa0wc-image.image) </span>

      A new stream key is generated for each Instagram live stream.

3. Concatenate the stream URL and stream key. Make sure the stream URL comes first, followed by the stream key.

4. Enter the concatenated string as the push stream address in the **Add platform** dialog box of the BytePlus Live console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b3336dd7854c32b15237ed71fefeb5~tplv-goo7wpa0wc-image.image) </span>
