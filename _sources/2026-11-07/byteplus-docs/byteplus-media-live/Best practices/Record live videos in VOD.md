---
title: "Record live videos in VOD"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/recordinvod"
---

To save your live streams for on\-demand playback and further processing, you can configure BytePlus MediaLive to automatically record them into BytePlus VOD. This topic provides step\-by\-step instructions on how to create a recording template, configure callbacks, and start a recording task. Once your live stream is recorded, you can use VOD's features to transcode, edit, and add watermarks before distributing the final video to your audience.

<span id="86d66040"></span>
## Prerequisites


* To store recorded files in VOD, activate the [VOD service](https://console.byteplus.com/vodpaas/totalOverview/).

* The domain name for stream pushing has been added, and the CNAME has been configured. For details, you can refer to [Adding domain names](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337) and [Adding a CNAME record](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adding-a-cname-record).

* Complete the domain name configuration on VOD Console, for details, please refer to [Distribution acceleration](https://docs.byteplus.com/en/docs/byteplus-vod/docs-accelerated-distribution).


<span id="1d4ffeb7"></span>
## Procedure

<span id="6791add7"></span>
### Create recording template

The following steps describe how to create a recording template in the console. You can also create recording templates by calling the [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) API.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and choose the **Recording** tab.

3. Find **Domain name space** at the top of the page and select a domain name space from the drop\-down menu.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to select VOD as the storage location, click <strong>VOD</strong> in the panel.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed009ab1f32f4ae78e7a724924a1ca86~tplv-goo7wpa0wc-image.image) </span>

4. Click **Add configuration** to open the **Add recording configuration** dialog.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to complete an authorization process for the first time to allow MediaLive to access the VOD service. Please follow the instructions on the screen to complete the process before proceeding to the next step.   </div>
   

5. Configure parameters such as AppName, VOD space, and workflow templates as prompted on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fce24b3399d43ea808f026569e4400b~tplv-goo7wpa0wc-image.image) </span>


The following table describes the configuration parameters.


|Parameter |||Description |
|---|---|---|---|
|AppName |||Fill in the AppName for this recording configuration. It supports uppercase and lowercase letters, numbers, hyphens (\-), and underscores (_), with a maximum length of 30 characters.<br><br><br>* You can use an asterisk (\*) to apply the recording policy to all AppNames in the namespace. This creates a global policy for the namespace.<br><br>* If both a global policy and a separate policy are configured for an AppName, a separate policy is used for recording by default. |
|StreamName |||Specify the StreamName of the live streams to be recorded. For the same App, you can specify up to 20 stream names. |
|Recording stream type |||Select the type of live stream recording. The following two types are supported.<br><br><br>* Original stream<br><br>* Transcoded stream<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Recording with a transcoded stream will generate a transcoding pull stream which may incur costs. If the transcoding configuration is deleted, the stream will not be recorded.</div><br> |
|VOD space |||Select VOD space as the storage location. The recording files will be stored in the selected space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/byteplus-vod/docs/space-management">Create a VOD space</a> if you do not have one yet.</div><br><br><br>. |
|Recording format |HLS |File generation mode |HLS format supports segmented recording and full recording. |
|||Fixed time |The maximum duration of a single recorded file. When the recording duration exceeds this value, a new recording will be generated. The supported value ranges for segmented recording and full recording are different:<br><br><br>* Segmented recording: Supports values ranging from 5 to 360 minutes.<br><br>* Full recording: Unlimited. |
|||Waiting time |When the **File generation mode** is configured as **Full recording**, you can specify the waiting time for resuming recording after an interruption. After the interruption exceeds the waiting time, the recording task will end, and a recording file will be generated. The valid range for this waiting time is 0 to 3600 seconds. |
|||Duration of a TS slice |The duration of each TS segment for the live recording. The value can range from 5 to 30 seconds |
|||VOD category |[Select the VOD category for storing the recorded files. For the category configuration method, please refer to VOD Categories](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system). |
|||Workflow Template |This parameter is optional. Select a workflow template from the drop\-down list.<br><br><br>* If you select a workflow name here, the corresponding workflow will be applied to the recording files after they are uploaded to BytePlus VOD.<br><br>* If you do not select a workflow template here, a default workflow template will be applied to the recording files after they are uploaded to BytePlus VOD.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can use the default workflow template of VOD, or you can refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow">workflow template</a> for customization instructions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The workflow template you configured for MediaLive recording takes precedence over the default workflow template configured in VOD.</div><br> |
|||File name |Enter the file path. The default path is `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`. You can manually add path components, up to a maximum length of 200 characters. Manually added paths must meet the following requirements.<br><br><br>* You can delete fixed path components, such as {App}/{Stream}.<br><br>* The path cannot start with a forward slash (/) or backslash (\).<br><br>* Strings such as "//" and “/./” are not supported;<br><br>* Characters such as \b, \t, \n, \v, \f, and \r are not supported.<br><br>* ".." is not supported as a filename.<br><br>* The directory hierarchy must contain at least two levels, such as `live/{App}/{Stream}` |
||MP4 |Fixed time |The maximum duration of a single recorded file. When the recording duration exceeds this value, a new recording file will be generated. Supported values range from 5 to 360 minutes. |
|||VOD category |Select the category of live recording file storage to VOD. For the category configuration method, please refer to VOD [Categories](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system). |
|||Workflow Template |Not required, select the workflow template in the drop\-down list.<br><br><br>* If you select a workflow name here, the corresponding workflow will be applied to the recording files after they are uploaded to BytePlus VOD.<br><br>* If you do not select a workflow template here, a default workflow template will be applied to the recording files after they are uploaded to BytePlus VOD.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can use the default workflow template of VOD, or you can refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow">workflow template</a> to customize.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The workflow template you configured in MediaLive recording takes precedence over the default workflow template configured in VOD.</div><br> |
|||File name |Enter the file path. The default path is `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`. You can manually add path components, up to a maximum length of 200 characters. Manually added paths must meet the following requirements.<br><br><br>* You can delete fixed path components, such as {App}/{Stream}.<br><br>* The path cannot start with a forward slash (/) or backslash (\).<br><br>* Strings such as "//" and “/./” are not supported;<br><br>* Characters such as \b, \t, \n, \v, \f, and \r are not supported.<br><br>* ".." is not supported as a filename.<br><br>* The directory hierarchy must contain at least two levels, such as `live/{App}/{Stream}` |
||FLV |Fixed time |The maximum duration of a single file recorded. When the recording duration exceeds this value, a new recording file will be generated. Supported values range from 5 to 360 minutes. |
|||VOD category |Select the category of live recording file storage to VOD. For the category configuration method, please refer to VOD [Categories](https://docs.byteplus.com/en/docs/byteplus-vod/docs-system). |
|||Workflow Template |Not required, select the workflow template in the drop\-down list.<br><br><br>* If you select a workflow name here, the corresponding workflow will be applied to the recording files after they are uploaded to BytePlus VOD.<br><br>* If you do not select a workflow template here, a default workflow template will be applied to the recording files after they are uploaded to BytePlus VOD.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can use the default workflow template of VOD, or you can refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow">workflow template</a> to customize.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The workflow template you configured in MediaLive recording takes precedence over the default workflow template configured in VOD.</div><br> |
|||File name |Enter the file path. The default path is `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`. You can manually add path components, up to a maximum length of 200 characters. Manually added paths must meet the following requirements.<br><br><br>* You can delete fixed path components, such as {App}/{Stream}.<br><br>* The path cannot start with a forward slash (/) or backslash (\).<br><br>* Strings such as "//" and “/./” are not supported;<br><br>* Characters such as \b, \t, \n, \v, \f, and \r are not supported.<br><br>* ".." is not supported as a filename.<br><br>* The directory hierarchy must contain at least two levels, such as `live/{App}/{Stream}` |



6. Click the OK button to complete the configuration. The configuration results can be viewed in the list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c16108cc6649479f8b7ba739f7e5ef59~tplv-goo7wpa0wc-image.image) </span>


<span id="a5e43951"></span>
### Configure recording callback

The following steps describe how to add a callback configuration in BytePlus MediaLive console. You can also call [UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023) API to configure it.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Feature configuration**. Click the **Callback** tab.

3. Find **Domain name space** at the top of the page and select a domain name space from the drop\-down menu.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c846b992def44347a4bfc578354621f7~tplv-goo7wpa0wc-image.image) </span>

4. Click Add configuration to open Add callback configuration dialog.

5. Configure parameters such as the callback address, callback type, and AppName, as prompted on the page.

   Parameter descriptions are shown in the table below.

   
   |Parameter |Description |
   |---|---|
   |Callback address |The callback address to receive the callback messages. It supports HTTP and HTTPS protocols. |
   |Callback type |For the callback type, select **Recording events**. |
   |Callback key |The callback key. It supports uppercase and lowercase letters and numbers, with a maximum length of 32 characters. |
   |AppName |The application name. This must be the same one used when creating the recording template. |
   

6. Click **Confirm** to save the callback configuration. You can see the newly added configuration in the list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/639d18064d01434fadb769baf18d3219~tplv-goo7wpa0wc-image.image) </span>


<span id="50d2d99f"></span>
### Generate push stream address

This section describes how to generate a push stream address from the BytePlus MediaLive console. You can also generate it by calling the [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) API.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the navigation bar, select [Address generator](https://console.byteplus.com/live/main/locationGenerate).

3. Select the address type and domain name according to the page prompts, and enter the AppName (which must be the same one used when creating the recording template), a custom StreamName, and an expiration time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea908c886ba4d12bb51041b411e3b6e~tplv-goo7wpa0wc-image.image) </span>

4. Click **Generate address** to get a push stream address in the **Result** section.


<span id="3d28d39b"></span>
### Start pushing the stream

Use the generated push stream address to push the stream. MediaLive supports the following push streaming configurations.


* Use the [Web push](https://console.byteplus.com/live/main/WebPushStream) function on BytePlus MediaLive console to push the stream

* Use streaming tools (e.g., [OBS](https://obsproject.com/)) to push the stream

* Use [Client SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-client-sdks-4d36c282) to push the stream


<span id="dc72915d"></span>
### Get video Vid

After a live stream ends, the recorded file is stored in the corresponding VOD space. You can find the video using its video ID (Vid). There are three ways to get the Vid:


<Tabs>
<Tab zoneid="mLduLsK2yk" title="Method 1: Get through the BytePlus MediaLive console">
<TabTitle>Method 1: Get through the BytePlus MediaLive console</TabTitle>

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live)

2. Select **Live management** \> **Recordings**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff1d3c5677a142f4b8b82bd85fb23ea7~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the domain name, AppName, StreamName according to the prompts, and select the time range. Click **Search** to get the recording result. The domain name space and time range are required.

4. Click **Search** to start the query.

5. You can see the Vid of the corresponding recording in the result list. You can also click **Enter VOD to view** to enter the VOD console to view the recording results.


</Tab>
<Tab zoneid="fRoGCRxYne" title="Method 2: Get by recording callback Method ">
<TabTitle>Method 2: Get by recording callback Method </TabTitle>

If you configure a recording callback, MediaLive sends the recording file information to your callback server when a recording file is generated.

You can get the Vid of the recording file in the callback message. For a detailed description of the callback message, refer to the documentation for callback content.


</Tab>
<Tab zoneid="VcNmVtimZu" title="Method 3: Get through the API">
<TabTitle>Method 3: Get through the API</TabTitle>

You can obtain the Vid of the recorded file by calling the [DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023?lang=en) API.


</Tab>
</Tabs>
