---
title: "Going live on TikTok via RTMP"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms"
---

You can push your BytePlus AI Live stream to TikTok via RTMP so viewers can watch your AI figure on TikTok. This guide explains how to configure TikTok as the streaming destination in AI Live and obtain the server URL and stream key using the TikTok app or TikTok LIVE Center.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b107d695409a419c88170e89cfbb29b6~tplv-goo7wpa0wc-image.image)

## Prerequisites

* You have set up an AI figure live room and are ready to go live. For more information, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

* You have permission to go live on TikTok. For more information, see [Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2).

## Procedure

In AI Live, configure the RTMP streaming settings for TikTok in the **Live platform** dialog.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) and open your AI live room.

2. In the top navigation bar, click **Live platform**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

3. In the **Live platform** dialog, configure the following settings, and then click **Save**.

   |**Configuration** |**Description** |
   |---|---|
   |Live platform setting |Choose **TikTok as** stream destination. |
   |Streaming method |When you choose **TikTok** as the Live platform, select **RTMP** as the streaming method. For **Virtual Camera**, see [Going live on TikTok via OBS virtual camera](https://docs.byteplus.com/docs/byteplus-livesaas/Going_live_on_TikTok_via_Digital_Human_and_OBS). |
   |TikTok ID |Get the ID in your TikTok app as shown below.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image) |
   |URL Server |Enter the push URL (RTMP server address) for your current TikTok live stream. For instructions, see [Get the server URL and stream key](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms). |
   |Stream Key |Enter the TikTok stream key associated with the server URL above. For instructions, see [Get the server URL and stream key](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms). |
   |Stream pushing |Enable this option to push your AI Live stream to TikTok. |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9269d0affec041ab96bc5e24801eb065~tplv-goo7wpa0wc-image.image)

4. Start your AI Live. For details, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

### Get the server URL and stream key

This section explains how to get the server URL and stream key using the TikTok app or TikTok LIVE Center. The methods and live\-streaming permission requirements may change as TikTok updates its policies.

1. Find and copy the server URL and stream key on TikTok.

   > **说明**

   > You must copy the server URL and stream key each time you go live on TikTok.

   **TikTok App**

Find and copy the server URL and stream key on the TikTok app.

      1. Open your TikTok app.

      2. Go to the navigation bar at the bottom and tap the plus "+" button.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75eece96c4641228a643f1cd42f32c8~tplv-goo7wpa0wc-image.image)

      3. Select the **Stream key** option and then click **Go LIVE**.

         > **说明**

         > If this option is not visible, your account lacks permission to go live. For more information, see [Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2).

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d3e968f9536438288b68d3c759612d6~tplv-goo7wpa0wc-image.image)

      4. Select your live topic as needed. Then you can see the server URL and stream key.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a414115857ec46c18bdac55cb92dcf15~tplv-goo7wpa0wc-image.image)

   **TikTok LIVE Center**

Find and copy the server URL and stream key on TikTok LIVE Center.

      1. Go to the [TikTok LIVE Center](https://livecenter.tiktok.com/producer).

      2. On the left navigation pane, click **Go LIVE**.

         > **说明**

         > If this option is not visible, your account lacks permission to go live. For more information, see [Who can use LIVE on TikTok](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2).

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d076bd36c2974227b8d36c5643953aca~tplv-goo7wpa0wc-image.image)

      3. Enter your stream details and upload a LIVE cover if needed.

      4. Click **Save & Go LIVE**.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80d6e9c8b8f84967b36611d3ebd26a51~tplv-goo7wpa0wc-image.image)

         This does not start your live stream yet. This generates your server URL and stream key, which you will need to add to BytePlus to start your stream. The server URL and stream key will remain active for 5 minutes, so you need to complete the next section within that time.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85bdf73e46c1475e8592a9ffd3fce217~tplv-goo7wpa0wc-image.image)

### Get a pull stream address from BytePlus Live

If a third\-party platform supports pulling a live stream from an external URL, you can get the pull stream address of your BytePlus Live room and use it on that platform.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) and open the live room.

2. On the left navigation pane, click **Marketing toolkits** \> **Multi\-platform streaming**.

3. Click **Get pull stream address** and copy the address in the dialog box that appears.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c4672bbd0f94f018254c6526b42a7cf~tplv-goo7wpa0wc-image.image)

> **说明**

> Each live room has only one pull stream address.

### Get push stream addresses for other platforms

This section describes how to get the server URL and stream key, or the equivalent push stream address, on other major live\-streaming platforms. The methods and live\-streaming permission requirements may change as the platforms update their policies.

#### YouTube Live

1. Log in to [YouTube Live](https://www.youtube.com/).

2. In the upper\-right corner of the page, click the **Create** icon and select **Go live**.

If this is your first time enabling the live stream feature, it may take up to 24 hours to get access to live streaming.

3. On the **STREAM SETTINGS** tab, concatenate the stream URL and stream key. Make sure the stream URL comes first, followed by the stream key.

4. Use the concatenated string as the push stream address.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6887d8038a4d8c868cc4f1b6318c14~tplv-goo7wpa0wc-image.image)

#### MetaLive

1. Log in to [Facebook](https://www.facebook.com/live/create).

2. Click **Go live** in the **Go live** section.

3. Select **Streaming software** as your video source.

4. If you want the stream key to be permanently valid, turn on the **Persistent stream key** switch. Otherwise, the stream key cannot be used again after the live stream ends.

5. Concatenate the server URL and stream key with a forward slash (/). Make sure the server URL comes first, followed by the stream key.

6. Use the concatenated string as the push stream address.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/269d663243664680b93e050dd2e0f107~tplv-goo7wpa0wc-image.image)

#### LinkedIn Live

LinkedIn Live is only available to approved users. To check if you are eligible, learn more about access criteria for [LinkedIn Live](https://www.linkedin.com/help/linkedin/answer/a568503?src=li-other&veh=www.linkedin.com%7Cli-other).

1. Log in to [LinkedIn Live](https://www.linkedin.com/video/golive/now/).

2. Select **Go live now** under **New stream** in the upper\-left corner of the page.

3. On the **Stream settings** tab, select your region and then click **Get URL**.

4. Concatenate the stream URL and stream key. Make sure the stream URL comes first, followed by the stream key.

5. Use the concatenated string as the push stream address.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b20f3fd0857c41bcab188dbaa97d19d3~tplv-goo7wpa0wc-image.image)

#### Twitch TV

1. Log in to [Twitch TV](https://www.twitch.tv/).

2. Click your avatar and select **Settings** in the drop\-down list.

3. Click the **Channel and Videos** tab.

4. On the left navigation pane, click **Stream** \> **Settings**.

5. Concatenate the server URL and stream key with a forward slash (/). Make sure the server URL comes first, followed by the stream key. The RTMP server URL of Twitch TV is always `rtmp://live.twitch.tv/app`.

6. Use the concatenated string as the push stream address.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9fcd551f7f49a5af90766164057405~tplv-goo7wpa0wc-image.image)

#### Instagram

1. Enable a professional account.

   1. Log in to [Instagram](https://www.instagram.com/).

   2. Select **More** \> **Settings** on the left navigation pane.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cef1bc62f846f3867c45d8ebebf1ba~tplv-goo7wpa0wc-image.image)

   3. Click **Account type and tools** under **For professionals** and then click **Switch to professional account**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359470824d7d4ac687621d41c153aaf1~tplv-goo7wpa0wc-image.image)

   4. Select **Creator** or **Business** as needed.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dff9b0ecb64d0d9305c96c79ae75fa~tplv-goo7wpa0wc-image.image)

2. Get the stream URL and stream key.

   1. Select **Create** \> **Live video** from the left navigation pane on [Instagram](https://www.instagram.com/accounts/edit/).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8e825007124527b08baa146c13eb3f~tplv-goo7wpa0wc-image.image)

   2. In the dialog box that appears, enter a title for your live video and select your viewers. For this example, select **Public**. Then, click **Next**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a18338b3834fc4b647dfa561bd9f7e~tplv-goo7wpa0wc-image.image)

   3. Get the stream URL and stream key.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eed50beb29d4b078372e9de3bdff193~tplv-goo7wpa0wc-image.image)

A new stream key is generated for each Instagram live stream.

3. Concatenate the stream URL and stream key. Make sure the stream URL comes first, followed by the stream key.

4. Use the concatenated string as the push stream address.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b3336dd7854c32b15237ed71fefeb5~tplv-goo7wpa0wc-image.image)
