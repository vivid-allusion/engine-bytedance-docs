---
title: "Configuring a relay task"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay"
---

If your live\-stream source cannot push, or you want to use on\-demand videos for live streaming, you can use the relay feature to pull content from the source or on\-demand videos and then push it to your audience. This article details how you can best configure and manage relay tasks.

<span id="Context"></span>
## Context

You can relay content to BytePlus MediaLive's push stream address or a third\-party address. When you create or edit a relay task, BytePlus MediaLive identifies the type of push stream address based on the following rules.


* **BytePlus MediaLive's push stream address**: Uses the domain name that is added to your account (excluding deleted domain names) and has the correct CNAME record configured.

* **Third\-party push stream address**: Uses a domain name that is not added to your account.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d945097be1d9461d97bdfde7c77552e4~tplv-goo7wpa0wc-image.image) </span>


<span id="4d1be0a3"></span>
## **Considerations**


* Using the relay feature incurs relay fees. For details, please refer to [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1).

* Supports pushing one stream per relay task.

* Addresses used in relay tasks must not contain multibyte encoded characters, if included, they need to be converted to single\-byte encoded characters.


<span id="Prerequisites"></span>
## Prerequisites


* A source stream playback address.

* If you want to relay contents to BytePlus MediaLive's push stream address, make sure you have added a domain name with a CNAME record configured. For details, refer to [Domain](https://docs.byteplus.com/byteplus-media-live/docs/domain).

* A BytePlus MediaLive's push stream address or a third\-party address.


<span id="Procedure"></span>
## Procedure

<span id="e163627d"></span>
### Creating a task group


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, choose **Toolkits** \> **Relays**.

3. Click **Group management**, add, or delete task groups in **Group Management** dialog box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MediaLive presets the default group and associates the default project. The preset group does not support deletion.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the group is created, it is not supported to modify the group name and the project it belongs to.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a6e9dcfdff145f2bd7150b25300531d~tplv-goo7wpa0wc-image.image) </span>


<span id="47597d6d"></span>
### Creating a relay task


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, choose **Toolkits** \> **Relays**.

3. Click **Create relay**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9aba2969d6944e05b9e328881d9be03e~tplv-goo7wpa0wc-image.image) </span>

4. Fill in the relay information.

   Below is a more detailed description of each parameter:

   
   |**Parameter** |**Description** |
   |---|---|
   |Title |The title of the relay task. The default value is `Relay`.<br><br>Support Chinese, uppercase and lowercase letters, numbers, no more than 20 characters in length. |
   |Source type |The source type of the contents to be pulled. Options include **Live** and **VOD**. |
   |Group |Select Relay task group, which belongs to the project. You can use task groups to implement sub\-account access control based on projects. |
   |Relay time |Configure the start and end time of the relay task, the time range is ≤ 7 days. |
   |Pull stream address |When the **Source type** is **Live**, fill in the playback address of the live stream, and support entering HTTP, HTTPS, HLS, RTMP, RTMPS, SRT, and RTSP protocol addresses.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The address cannot contain multibyte\-encoded characters. If it contains, the address needs to be converted to single\-byte encoding.</div><br> |
   |VOD address |When the **Source type** is **VOD**, fill in the playback address of on\-demand videos, and support entering HTTP, HTTPS, HLS, RTMP, RTMPS, SRT, and RTSP protocol addresses.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can add a maximum of 30 addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The address cannot contain multibyte\-encoded characters. If it contains, the address needs to be converted to single\-byte encoding.</div><br> |
   |Loop mode |When the **Source type** is **VOD**, you can set the loop playback mode of on\-demand videos. Options include **Infinite list loop** and **Specified\-times list loop**. |
   |Push stream address |Fill in the push address, support entering HTTP, HTTPS, HLS, RTMP, RTMPS, SRT, RTSP protocol addresses. Support filling in non\-third\-party streaming addresses or third\-party streaming addresses. Non\-third\-party streaming addresses can be generated through the [Address generator](https://console.byteplus.com/live/main/locationGenerate).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The address cannot contain multibyte\-encoded characters. If it contains, the address needs to be converted to single\-byte encoding.</div><br> |
   |Watermark configuration |Add a watermark configuration.<br><br><br>* Add watermark: Upload a PNG or JPG image within 2 MB.<br><br>* Horizontal offset: Ratio to left Y\-axis.<br><br>* Vertical offset: Ratio to upper X\-axis.<br><br>* Relative width: The ratio of watermark width to actual image width.<br><br>* Preview: According to the width and height settings, view the preview effect. |
   |Callback address |The callback address for receiving relay task events. Maximum length: 512 characters. |
   

5. Click **Confirm** to create a relay task. You can view the task in the task list.


<span id="Viewing relay tasks"></span>
### Viewing relay tasks


1. Go to the **Relays** page to view the task list. You can view the task name, task ID, target push stream address, status, start time, and end time.

   * Third\-party target push stream addresses are marked **Third party**.

   * Each task may have one of the four statuses:

      * **Pending**: The relay task is ready to start.

      * **Enabled**: This indicates an ongoing relay task and is activated upon the defined start time.

      * **Disabled**: The relay task is disabled. Click **Enable** to revert the action.

      * **Ended**: This status appears after the defined end time of the relay task. Click **Edit** and specify a new relay time if you want to reuse the configuration.

2. Enter a task name in the **search field** to retrieve the target task. Fuzzy search is supported.


<span id="Managing relay tasks"></span>
### Managing relay tasks

Click the three\-dot menu in the **Actions** column and then select the operation you want to perform on a relay task, such as editing or disabling the task.
