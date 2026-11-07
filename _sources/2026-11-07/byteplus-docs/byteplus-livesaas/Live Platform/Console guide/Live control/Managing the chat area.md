---
title: "Managing the chat area"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-the-chat-area"
---

To enhance interactivity and maintain order in your live room, you can use the chat interaction menu. This guide provides step\-by\-step instructions on how to configure chat features such as top comments, bullet comments, and automatic translation, as well as how to perform real\-time moderation actions like pinning comments, muting viewers, and managing reported content.

<span id="0ce5b5e7"></span>
## Prerequisites

A BytePlus account or an IAM user with the following permissions. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


* Producer \> Edit permission: Used to configure the menu for chat interaction.

* Live control \> Edit permission: Used to perform operations such as viewing and replying to viewers' comments.


<span id="c4a3bf6b"></span>
## Context

The chat interaction menu is a common feature in a live room that provides various tools to increase engagement and maintain order.

<span id="7d02bbca"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. From the live room list, click a live room to open it.

3. On the left navigation pane, click **Producer** \> **Menus**.

4. Add the menu for chat interaction.

   1. Click **Edit** **menu**.

   2. Click **Add** in the dialog box that appears.

   3. Enter the menu name and select **Chat interaction** from the **Menu type** drop\-down list.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8a7ebb076bc465abc32fb8a28046c99~tplv-goo7wpa0wc-image.image) </span>

   4. (Optional) Drag to adjust the order of menus.

   5. Click **Confirm**.

   6. Click **Save** on the **Menus** page.

5. Under the menu for chat interaction, complete the following configurations and then click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a93f92341174075985c1f1fd15f6a16~tplv-goo7wpa0wc-image.image) </span>

   * Turn on the **Hot list** switch to enable the top comments feature.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/046854a302cc499ca355e080b9be39ee~tplv-goo7wpa0wc-image.image) </span>

      After the feature is enabled, you can:

      * Change the name of the menu for top comments.

      * Turn on the **Manually select top comments** switch. Then, the top comments displayed on the viewing page are the ones you manually select, rather than being based on the number of likes.

      * Turn on the **Like** switch. This displays the like icon under the chat interaction and top comments menus, and it shows the number of likes under the top comments menu on the viewing page.

      * Configure the maximum number of comments that can be displayed under the menu for top comments.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For mobile devices, the menu for top comments only displays in landscape mode.      </div>
      

   * In the **Minimum sending interval** field, set the minimum time a user must wait between sending comments. Value range: [1,300]. For example, if you enter 3, no one (neither the host nor viewers) can send another comment for 3 seconds after their previous one.

   * In the **Text box placeholder** field, edit the placeholder text that appears in the chat input box on the viewing page.

   * In the **Host's nickname** field, modify the host's nickname.

   * Turn on the **Bullet comments** switch. Then, during the live stream, comments will scroll across the viewing page. Viewers can enable or disable bullet comments, and configure their opacity, display area, speed, and font size.

   * Turn on the **Comment translation** switch.

      To use this feature, you must turn on the **Languages** switch and select the corresponding languages on the **Producer** \> **Basic information** page. For example, if most comments are in English and you want to help viewers who do not understand English follow the conversation, you can turn on the **Languages** switch and select a target language, such as **Japanese**. For viewers whose default browser language on PCs or system language on mobile devices is Japanese, comments are automatically translated into Japanese. Viewers can also manually switch the page language to Japanese on the viewing page to view comments in Japanese.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Currently, translations between the following languages are supported:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Simplified Chinese      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">English      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Japanese      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Traditional Chinese      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Korean      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Thai      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Vietnamese      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Arabic      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Turkish      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Spanish      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Indonesian      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Portuguese      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Russian      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Tagalog      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Khmer      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Lao      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Burmese      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Malay      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Hindi      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">French      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">German      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Italian      </div>
      

   * Turn on the **Bot comments** switch to allow bots to automatically send comments based on configured sending rules and content.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ef4e99074f5420ab7cd29782670b7c3~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">At most 2,000 bot comments are supported.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This feature is only available when the live room is in the <strong>Live</strong> status and you are not muting all viewers.      </div>
      

   * Turn on the **Welcome message** switch, and configure the title and content of the welcome message as needed. You can use the welcome message to inform viewers about important information, such as the chat rules for the live room.

   * Turn on the **Chat only during live stream** switch. Then, viewers can only send comments during the live stream. For more information, see [Muting all the viewers](https://docs.byteplus.com/docs/byteplus-livesaas/docs-muting-viewers).

6. Under the menu for chat interaction on the right of the **Live control** page, you can perform the following operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6a20bfb192844b988f3057cc4f386cc~tplv-goo7wpa0wc-image.image) </span>

   * Filter comments by status or content. Fuzzy search is supported.

   * View top comments on the **Popular** tab if the top comments feature is enabled in step 5.

   * Send text comments and emojis.

   * Click the icon to stop viewers from sending comments or allow viewers to send comments. For more information, see [Muting all the viewers](https://docs.byteplus.com/docs/byteplus-livesaas/docs-muting-viewers).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bb3c66407f24239aaea6da86bf321f0~tplv-goo7wpa0wc-image.image) </span>

   * Click the **Chat settings** icon and perform the following operations as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d73db8d30684127a6c21e599931d514~tplv-goo7wpa0wc-image.image) </span>

      * Configure the host's nickname.

      * Enable or disable the chat moderation feature.

         With the feature enabled, comments are only visible to viewers who send them. Move your pointer over a comment and click **Approve** to approve it. Once approved, the comment is visible to everyone on the viewing page.

      * Enable or disable the chatbot feature.

         To use this feature, make sure you have configured the sending rules and content in step 5.

      * Enable or disable system notifications for viewer entrances and gifts on the console and the web\-based live streaming page.

      * Enable or disable the gift effects on the console.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The <strong>Gift effects</strong> switch appears only when the gift rewards feature is enabled. For how to enable the feature, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts">Rewarding hosts with gifts</a>.         </div>
         

      * Click **Configure** to enable or disable notifications for lucky draws, dynamic emojis, gifts, and viewer entrances in the **Manage system notifications** dialog box.

      * Click **Export comments** to export the comment data to your local storage.

      * Click **Clear comments** to clear the chat area on the viewing page.

   * Click the ellipsis icon on the right of a comment and then you can perform the following operations.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a869b9eb0047403aa5e080709a3d71ab~tplv-goo7wpa0wc-image.image) </span>

      * Reply to the comment.

      * Like the comment.

      * Pin the comment to the top of the chat area.

      * Mute or unmute a viewer. After selecting **Mute**, the viewer who sent the comment is muted and the comment is deleted from the viewing page. A muted viewer can still send comments, but their messages are only visible to them. To unmute a viewer, click the ellipsis icon next to one of their comments and select **Unmute**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Viewers are muted based on their UIDs, which vary depending on their login method. For example, you mute a viewer who logs in to the live room by entering the nickname only. The viewer then chooses to log in to the live room by phone number. This gives the viewer a new UID, allowing them to send comments again.         </div>
         

      * Delete the comment from the viewing page.

      * Block or unblock a viewer's IP address. For more information, see [Kicking a viewer out or blocking a viewer's IP address](https://docs.byteplus.com/docs/byteplus-livesaas/kicking-a-viewer-out-or-blocking-a-viewer-s-IP-address).

      * Kick a viewer out of the live room or allow them to rejoin. For more information, see [Kicking a viewer out or blocking a viewer's IP address](https://docs.byteplus.com/docs/byteplus-livesaas/kicking-a-viewer-out-or-blocking-a-viewer-s-IP-address).

      * If you have turned on the **Manually select top comments** switch (see step 5), select **Popular** and set a number of likes in the dialog box to feature the comment in the top comments menu.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/521c66be715f47f99d05e2c4600932a8~tplv-goo7wpa0wc-image.image) </span>

   * View why a comment was reported in any of the following ways.

      Based on the report, you can decide whether to delete the comment or mute the viewer who sent it.

      * Click the **Reported** tag to view the reason for the report.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/855e7cb33d0d4179843115ce29d15326~tplv-goo7wpa0wc-image.image) </span>

      * Click the **Message** icon to view the comment report message.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0fbb58a2dd54b34a14c269e40f226ff~tplv-goo7wpa0wc-image.image) </span>

         You can also perform the following operations on the **Message list** page:

         * To view all comment report messages, click the filter icon next to the **Type** column and select **Comment report** in the dialog box.

         * Click the live room link to view the comment in its corresponding live room.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To use this feature, you must turn on the <strong>Comment report</strong> switch on the <strong>Producer</strong> \> <strong>Security control</strong> page. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/configuring-security-control">Configuring security control</a>.      </div>
      

<span id="c16b857a"></span>
## What your viewers see


|Feature |On PCs |On mobile devices |Description |
|---|---|---|---|
|Chat area |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b23e522e1ef48eeae34fd4c43efaf41~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6459b0657e7a48cd9f102b525cbfea3e~tplv-goo7wpa0wc-image.image) </span> |None. |
|Menu for top comments |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d63db59688294bd285e495db736c4c74~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae1debc07f5c48b98e04b436c09bb41e~tplv-goo7wpa0wc-image.image) </span> |For mobile devices, only supported in landscape mode. |
|Reply to a comment |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d188cca23aa34ce8853c29276a59a4cc~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0de973f690b846de93c4d59f0414deac~tplv-goo7wpa0wc-image.image) </span> |Right\-click the comment on PCs or tap the comment on mobile devices, and then select **Reply**. |
|View the welcome message |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e195f4a8543e4613aa429cd5a70ab653~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ad66a94c0664853b553653efd725ad7~tplv-goo7wpa0wc-image.image) </span> |The welcome message is the first item viewers see in the chat area. As new comments appear, the welcome message scrolls up and eventually disappears from view.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each viewer will see the welcome message each time they enter the live room.</div><br> |
