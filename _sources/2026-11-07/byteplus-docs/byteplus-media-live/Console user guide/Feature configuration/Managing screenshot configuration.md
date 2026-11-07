---
title: "Managing screenshot configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-screenshot-capturing"
---

MediaLive supports live screenshot capturing. You can create screenshot configurations for the live stream and store the screenshot files in TOS. This article introduces how to add and manage screenshot configurations through the video live streaming console.

<span id="Notes"></span>
## Notes


* Using the screenshot feature leads to the following fees:

   * Screenshot fees billed by MediaLive. Refer to [Screenshot capturing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing).

   * Storage fees billed by TOS. Refer to [Storage Fee](https://docs.byteplus.com/en/docs/tos/docs-storage-fee).

* For adding, updating, and deleting screenshot configurations, you need to re\-push and pull the stream 3\-5 minutes after adding, updating, and deleting operations to use the changed configuration.


<span id="674288b8"></span>
## Prerequisite

To store recorded files in TOS, activate the [TOS service](https://console.byteplus.com/tos/).

<span id="Procedure"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Feature configuration**. Click the **Screenshot** tab.

3. Find **Domain name space** at the top of the page and select a domain name for stream pushing from the drop\-down list.

4. Click **Add configuration** to open the **Add screenshot configuration** dialog box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you choose <strong>TOS</strong> for the first time, you will be asked to complete an authorization process to authorize MediaLive to access the TOS service. You must follow the instructions on the screen to complete the process before proceeding to the next step.   </div>
   

5. Configure the AppName, screenshot interval, image format, storage space, screenshot type and other parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |AppName |Specify the AppName of the live stream to screenshot. Make sure that this is the same as the AppName specified in the push stream address. |
   |Screenshot interval |The interval time between screenshots (measured in seconds). |
   |Image format |Select **JPG** or **JPEG**. By default, **JPG** is selected. |
   |TOS bucket |Select a folder under a bucket in TOS as the storage location. |
   |Screenshot type |Select **Overwrite** or **Non\-overwrite**. By default, **Non\-overwrite** is selected.<br><br><br>* **Overwrite**: Capture screenshots in sequence based on the snapshot interval, overwriting the previous screenshot with the new one.<br><br>* **Non\-overwrite**: Capture screenshots in sequence based on the snapshot interval, storing new screenshots in order. |
   |Storage path |If you select **Overwrite** as the **Screenshot type**, the storage path format is `{PushDomain}/{App}/{Stream}`.<br><br>If you select **Non\-overwrite** as the **Screenshot type**, the storage path format is `{PushDomain}/{App}/{Stream}/{UnixTimestamp}`.<br><br>The path supports the following characters:<br><br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Numbers (0\-9)<br><br>* Hyphen (\-)<br><br>* Exclamation point (!)<br><br>* Underscore (_)<br><br>* Period (.)<br><br>* Asterisk (\*)<br><br>* Placeholder |
   

6. Click **Confirm** to save and list your configuration. You can always click **Edit** or **Delete** in the **Actions** column to modify or delete these settings.


<span id="Result"></span>
## What to do next

After completing the screenshot configuration, if you use a live stream with the same stream parameters for live playing, screenshots of your live stream will be captured and saved. Refer to [Managing screenshots](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-screenshots).
