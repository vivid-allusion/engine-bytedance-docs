---
title: "Managing the Q&A area"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-the-q-a-area"
---

The host and viewers can post and reply to questions in the Q&A area.

<span id="51a16f7b"></span>
## Prerequisite

A BytePlus account or an IAM user with the following permissions. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


* Producer \> Edit permission: Used to configure the menu for Q&A.

* Live control \> Edit permission: Used to perform operations such as posting and replying to questions.


<span id="7eab7b5b"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. Add a menu for Q&A using the following steps:

   1. On the left navigation pane, click **Producer** \> **Menus**.

   2. Click **Edit** **menu**.

   3. Click **Add** in the dialog box that appears.

   4. Enter the menu name and select **Q&A** from the **Menu type** drop\-down list.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83e67d33653a4e9fa29cdc32d26bc06a~tplv-goo7wpa0wc-image.image) </span>

   5. (Optional) Drag to adjust the order of menus.

   6. Click **Confirm**.

   7. Click **Save** on the **Menus** page.

4. Under the menu for Q&A, you can complete the following configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7d1d38fe1c44cb8a5c051c57c4842fb~tplv-goo7wpa0wc-image.image) </span>

   * Turn on the **Viewers ask questions** switch to allow viewers to post questions on the viewing page. If this switch is turned off, viewers can only reply to the questions posted by the host.

   * In the **Maximum number of questions per viewer** field, configure the maximum number of questions each viewer can post.

   * In the **Minimum sending interval** field, configure how long the minimum wait time should be between each user's comments. Value range: [1,300]. For example, if you enter 3 here, no one, host or viewer alike, can post or reply to a question until 3 seconds have elapsed since their previous entry.

   * In the **Text box placeholder** field, modify the message displayed in the text box of the Q&A area when no question is entered.

   * In the **Host's nickname** field, modify the host's nickname in the Q&A area.

   * Select the display mode of the Q&A area on PCs.

5. On the **Live control** page, you can perform the following operations on the menu for Q&A.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9052fa9f05d4411e9554486de6ac6eaa~tplv-goo7wpa0wc-image.image) </span>

   * Filter questions by status or content. Fuzzy search is supported.

   * Sort questions or replies by time or popularity.

   * Post questions.

   * Reply to questions.

   * Pin a question or reply to the top.

   * Like questions or replies.

   * Delete questions or replies from the viewing page. After a question is deleted, all replies to the question are synchronously deleted from the viewing page.

   * Mute or unmute a viewer. Move your pointer over the ellipsis icon next to a question or reply, and select **Mute** to mute the viewer who sent it. A muted viewer cannot post or reply to questions. To unmute the viewer, move your pointer over the ellipsis icon next to a question or reply sent by the viewer and select **Unmute**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Viewers are muted based on their UIDs, which vary depending on their login method. For example, you mute a viewer who logs in to the live room by entering the nickname only. The viewer then chooses to log in to the live room by phone number. In this way, the viewer has a UID that is different from the muted UID and can post and reply to questions.      </div>
      

   * Click the second icon from the left above the text box to stop viewers from posting questions or allow viewers to post questions.

   * Click the third icon from the left above the text box to enable or disable the manual review feature. With the feature enabled, questions and replies are only visible to viewers who send them. Click  **√**  next to a question or reply to approve it. Once approved, the question or reply is visible to everyone on the viewing page.

   * Click the **Export data** icon to export the Q&A data to your local storage.

   * Click the **Clear comments** icon to clear the Q&A area on the viewing page.


<span id="9979ed78"></span>
## What your viewers see


<Tabs>
<Tab zoneid="YuglcsxqA2" title="On PCs">
<TabTitle>On PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/613cc0a1ce654177b887ad69d53e1313~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="ZMG6OExvDw" title="On mobile devices">
<TabTitle>On mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a806fea82f74e31a98213ef03a074a0~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>
