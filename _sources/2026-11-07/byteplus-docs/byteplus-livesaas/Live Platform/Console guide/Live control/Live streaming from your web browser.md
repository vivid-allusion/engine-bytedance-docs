---
title: "Live streaming from your web browser"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser"
---

This topic describes how to start a live stream from your web browser. This broadcast method is simple to use and does not require the installation of any clients or tools, which is applicable to solo hosts.

<span id="4db24b10"></span>
## Limitation

This method supports PC platforms only and is not available on H5 pages.

<span id="f0338064"></span>
## Prerequisite

A BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Adding IAM users, organizations, or roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="d66d12ba"></span>
## Environmental requirements to start a live stream


* To use basic features such as camera, microphone, sharing, interaction tools, chat, and viewer list for a smooth live streaming experience, we recommend that you use a device that meets the following conditions.

   * Memory: 8 GB or higher

   * CPU: Core i3 or higher

   * Graphics card: Integrated graphics card

* To use advanced features such as video chat, Beauty AR, and AI noise reduction, for a smooth live streaming experience, we recommend that you use a device that meets the following conditions.

   * Memory: 8 GB or higher

   * CPU: Core i5 or higher

   * Graphics card: Discrete graphics card (with 4 GB of video memory)

* Recommended browser and version: Google Chrome browser, version 96.0.4664 or later.

* Recommended network bandwidth: Upload and download bandwidth of 5 Mbps or higher. Click [here](https://www.speedtest.net/) to test your network bandwidth.

* Check if your current device has too many browser pages open to prevent potential issues with live streaming due to excessive consumption of browser performance.

* We recommend that you live stream in a quiet environment so that viewers can hear you clearly.


<span id="0593e5fe"></span>
## Note

During the live stream, do not change the audio input device unless necessary, as this may result in disruptive or sudden loss of audio on the viewing page.

<span id="772f9d20"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the **Live control** page, click **Web browser** on the **Broadcast method** tab under the player.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af42963e36fb47268dc038656bfca656~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) Click **Settings**. In the **Settings** dialog box that appears, turn on the switch to display the corresponding feature on the live streaming page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a282b36f730d4f73b4b907be0ca05a16~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Interaction tools</strong> field appears only after the menu for interaction tools is added in the live room.   </div>
   

5. Enter the live streaming page in any of the following ways as needed.

   * Click **Go to live streaming page**.

   * Click **Click to copy the link to start a live stream** to copy the link and send it to the corresponding host. The host can then use the link to enter the live streaming page without the need for logging in.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">BytePlus Live provides the API <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getwebpushliveclientapi">GetWebPushLiveClientAPI</a> to get the URL for the live streaming page of a live room, allowing the host to start a live stream from a web browser without the need for logging in. You can create a live room on the BytePlus Live console first and call <code>GetWebPushLiveClientAPI</code> to get the URL when the host needs to live stream in the future.      </div>
      

6. In the **Test your device** dialog box that appears, select your camera and microphone. Once your camera, microphone, network, and browser are detected to be functioning normally, click **Go live**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ea3462deb0a472c9e622618b43443a9~tplv-goo7wpa0wc-image.image) </span>

   You can also select **OBS Virtual Camera** from the **Select camera** drop\-down list to synchronize the OBS source to the live room. Audio is not supported for synchronization. For more information, see [How to use the OBS virtual camera?](https://docs.byteplus.com/docs/byteplus-livesaas/docs-faqs-about-live-streaming#45b1e9c3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Make sure to grant your browser permissions to use your camera and microphone.   </div>
   

7. Perform the following operations as needed and then click **Start live** to start a live stream.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b857411f1740219dcdbeace93b9fd5~tplv-goo7wpa0wc-image.image) </span>

   
   |No. |Feature |Description |
   |---|---|---|
   |1 |View upstream network status |Move your pointer over the network status icon to check the current upstream network status. If the network condition is poor, we recommend that you check the network environment to avoid affecting the live streaming effect. |
   |2 |View the live duration |View the duration of this live stream. |
   |3 |Switch the language of the live streaming page |Click the current page language and select the target language from the drop\-down list. |
   |4 |Lock the preview |Click **Lock preview** to lock the viewing page in the **Preview** status. Then, viewers can only view the cover image or watch the preview on the viewing page. This is applicable to scenarios that require testing the quality of the live stream in advance. |
   |5 |Get viewing page address |Move your pointer over **Viewing page**. Then, you can get:<br><br><br>* The viewing page address on PCs.<br><br>* The address and QR code of viewing page on mobile devices in landscape and portrait mode. |
   |6 |Share the screen |Click **Share** and select to share the entire screen, a window, or a Chrome tab to the viewing page.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Share a Chrome tab for synchronized audio sharing and higher\-definition viewing.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Do not minimize the window when sharing it to avoid affecting viewers' experience.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Use two displays, for example a laptop and an external monitor, to have one for sharing and the other for operating and previewing the live content.</div><br> |
   |7 |Share the whiteboard |Click **Whiteboard** to share the whiteboard. For more information, see [Sharing the whiteboard](https://docs.byteplus.com/docs/byteplus-livesaas/sharing-the-whiteboard). |
   |8 |Share documents and pictures |Click **Document** to share documents and pictures. For more information, see [Sharing documents and pictures](https://docs.byteplus.com/docs/byteplus-livesaas/sharing-documents-and-pictures). |
   |9 |Media settings |Click the **Media settings** icon and perform the following operations in the **Media settings** dialog box that appears.<br><br><br>* Change your camera, microphone, or speaker.<br><br>* Change the resolution of your camera. The actual resolution depends on the camera's capability. For example, if the camera only supports 720p, the resolution will be at most 720p regardless of selecting a higher resolution.<br><br>* Turn on the **Video mirroring** switch to horizontally flip the host's camera on the live streaming page.<br><br>* Turn on the **Beauty AR** switch to enable features such as whitening, smoothing, and sharpening.<br><br>* Turn on the **AI noise reduction** switch to reduce transient noises such as keyboard typing, collisions, and tapping.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Changes made in the dialog box take effect immediately without the need for saving.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only devices using Core i5 processor and above support the beauty AR and AI noise reduction features. For how to check your processor model, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/how-to-check-the-processor-model-of-your-computer">How to check your computer's processor model?</a>.</div><br> |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your camera is turned on when you are using the <strong>Share</strong>, <strong>Whiteboard</strong>, or <strong>Document</strong> feature, you can drag your camera to a desired location.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the same live room, only one live streaming page can be opened at the same time.   </div>
   

8. (Optional) On the right of the live streaming page, you can perform the following operations.

   * On the tab for chat interaction, you can:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72d531b7d40948faa3f3a8385f518097~tplv-goo7wpa0wc-image.image) </span>

      * Filter comments by status or content. Fuzzy search is supported.

      * View top comments on the **Popular** tab if the top comments feature is enabled. For how to enable the top comments feature, see [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area).

      * Send text comments and emojis.

      * Click the icon to stop viewers from sending comments or allow viewers to send comments. For more information, see [Muting all the viewers](https://docs.byteplus.com/docs/byteplus-livesaas/docs-muting-viewers).

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dda0924d948c4a0396f0ffb0e1b8dcf9~tplv-goo7wpa0wc-image.image) </span>

      * Click the **Chat settings** icon and perform the following operations as needed.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26e29b1ef50d44e2aeeaef9bc4a66024~tplv-goo7wpa0wc-image.image) </span>

         * Configure the host's nickname.

         * Enable or disable the chat moderation feature.

            With the feature enabled, comments are only visible to viewers who send them. Move your pointer over a comment and click **Approve** to approve it. Once approved, the comment is visible to everyone on the viewing page.

         * Enable or disable the chatbot feature.

            To use this feature, make sure you have configured the sending rules and content. For how to configure the sending rules and content, see [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area).

         * Enable or disable system notifications for viewer's entrance and gifts on the console and live streaming page in a web browser.

         * Enable or disable the gift effects on the console.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4">The <strong>Gift effects</strong> switch appears only when the gift rewards feature is enabled. For how to enable the feature, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts">Rewarding hosts with gifts</a>.            </div>
            

         * Click **Configure** to configure whether to enable the notifications for lucky draws, dynamic emojis, gifts, and viewer's entrance in the **Manage system notifications** dialog box that appears.

         * Click **Export comments** to export the comment data to your local storage.

         * Click **Clear comments** to clear the chat area on the viewing page.

      * Click the ellipsis icon on the right of a comment and then you can perform the following operations.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ac33edc6020491db9c12add4376d98c~tplv-goo7wpa0wc-image.image) </span>

         * Reply to the comment.

         * Like the comment.

         * Pin the comment to the top of the chat area.

         * Mute or unmute a viewer. After selecting **Mute**, the viewer who sent the comment is muted and the comment is deleted from the viewing page. A muted viewer can still send comments, but the comments are only visible to the muted viewer. To unmute the viewer, click the ellipsis icon on the right of a comment sent by the viewer and select **Unmute**.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4">Viewers are muted based on their UIDs, which vary depending on their login method. For example, you mute a viewer who logs in to the live room by entering the nickname only. The viewer then chooses to log in to the live room by phone number. In this way, the viewer has a UID that is different from the muted UID and can send comments.            </div>
            

         * Delete the comment from the viewing page.

         * Block or unblock a viewer's IP address. For more information, see [Kicking a viewer out or blocking a viewer's IP address](https://docs.byteplus.com/docs/byteplus-livesaas/kicking-a-viewer-out-or-blocking-a-viewer-s-IP-address).

         * Kick a viewer out of the live room or unkick the viewer. For more information, see [Kicking a viewer out or blocking a viewer's IP address](https://docs.byteplus.com/docs/byteplus-livesaas/kicking-a-viewer-out-or-blocking-a-viewer-s-IP-address).

         * If the feature of manually selecting top comments is enabled, select **Popular** and set the number of likes in the dialog box that appears to display the comment under the menu for top comments. For how to enable the feature of manually selecting top comments, see [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area).

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8632e749442b404abd7f4b93d985da32~tplv-goo7wpa0wc-image.image) </span>

      * View the reason why a comment is reported in any of the following ways.

         You can judge whether to delete the comment from the viewing page or mute the viewer who sent the comment based on the reported comment.

         Click the **Reported** tag to view the latest reason why a comment is reported.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16a65dec52b54aa489f376f49d9d02af~tplv-goo7wpa0wc-image.image) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">To use this feature, you must turn on the <strong>Comment report</strong> switch on the <strong>Producer</strong> \> <strong>Security control</strong> page. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/configuring-security-control">Configuring security control</a>.         </div>
         

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Make sure the menu for chat interaction is added. For how to add the menu, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area">Managing the chat area</a>.      </div>
      

   * On the tab for interaction tools, you can send documents, questionnaires, check\-ins, quizzes, announcements, and lucky draws. For more information, see [Managing the interaction area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area), [Sending a questionnaire](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-questionnaire), [Sending a check-in](https://docs.byteplus.com/docs/byteplus-livesaas/sending-a-check-in), [Sending a quiz](https://docs.byteplus.com/docs/byteplus-livesaas/sending-a-quiz), [Sending an announcement](https://docs.byteplus.com/docs/byteplus-livesaas/sending-an-announcement), and [Sending a real-time lucky draw](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-real-time-lucky-draw).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eee93a073746495598b82849c924d8c7~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Make sure the menu for interaction tools is added. For how to add the menu, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area">Managing the interaction area</a>.      </div>
      

   * On the tab for Q&A, you can:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ee4b29a0a2b4ea1ae2686553d7e2fb8~tplv-goo7wpa0wc-image.image) </span>

      * Filter questions by status or content. Fuzzy search is supported.

      * Sort questions or replies by time or popularity.

      * Post questions.

      * Reply to questions.

      * Pin a question or reply to the top.

      * Like questions or replies.

      * Delete questions or replies from the viewing page. After a question is deleted, all replies to the question are synchronously deleted from the viewing page.

      * Mute or unmute a viewer. Move your pointer over the ellipsis icon next to a question or reply, and select **Mute** to mute the viewer who sent it. A muted viewer cannot post or reply to questions. To unmute the viewer, move your pointer over the ellipsis icon next to a question or reply sent by the viewer and select **Unmute**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Viewers are muted based on their UIDs, which vary depending on their login method. For example, you mute a viewer who logs in to the live room by entering the nickname only. The viewer then chooses to log in to the live room by phone number. In this way, the viewer has a UID that is different from the muted UID and can post and reply to questions.         </div>
         

      * Click the second icon from the left above the text box to stop viewers from posting questions or allow viewers to post questions.

      * Click the third icon from the left above the text box to enable or disable the manual review feature. With the feature enabled, questions and replies are only visible to viewers who send them. Click  **√**  next to a question or reply to approve it. Once approved, the question or reply is visible to everyone on the viewing page.

      * Click the **Export data** icon to export the Q&A data to your local storage.

      * Click the **Clear comments** icon to clear the Q&A area on the viewing page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Make sure the menu for Q&A is added. For how to add the menu, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-q-a-area">Managing the Q&A area</a>.      </div>
      

   * On the tab for co\-host, invite guests to join the co\-host. For more information, see [Starting a co-host with guests](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-video-chat).

   * On the tab for viewer list, view the information of viewers.


<span id="f75e6f9e"></span>
## FAQ

[Live streaming FAQs](https://docs.byteplus.com/docs/byteplus-livesaas/docs-faqs-about-live-streaming)
