---
title: "Adding subtitles to videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-smart-captioning"
---

BytePlus VOD provides a comprehensive suite of features for both generating and displaying subtitles. You can automatically generate subtitle files using AI, or permanently burn stylized subtitles into your video frames. This article explains the entire workflow, from subtitle creation to playback.

<span id="5115ec74"></span>
## Subtitle types

BytePlus VOD supports two main types of subtitles:


* **Hardcoded subtitles:**  The subtitle text is permanently rendered into the video frames during transcoding. This ensures subtitles are always visible with a consistent style across all devices and players, which is ideal for social media or platforms where videos may autoplay on mute. However, they cannot be turned off by the viewer.

* **External subtitles:**  The subtitle file (such as `.vtt`, `.srt`) is stored separately from the video. The player fetches this file and overlays the text during playback. This offers flexibility, allowing viewers to turn subtitles on/off or switch between different languages.


<span id="c95a6857"></span>
## Applicable scenarios

Subtitles are widely used in the following scenarios:


|Scenario |Description |
|---|---|
|Event or concert |Generate monolingual or multilingual subtitles. |
|Recorded audio/video resources |Generate monolingual or multilingual subtitles. |
|Short vlogs |The audio content in the video can be converted into text subtitles, which is convenient for users when they need to watch without sound. |
|Meeting minutes |Automatically or manually summarize meeting minutes from an audio file. |
|Online training |Import courses and quickly add subtitles to enhance the course materials. |
|Record clinical patient history |Physicians can create voice notes during outpatient consultations or surgery that are converted into text to create clinical histories more efficiently. |
|Games and entertainment |Convert in\-game voice chats to text messages to improve reading efficiency and the interactive experience. |
|Courtroom database entry |Identifies voice files from uploaded court records, converts the information to text, and enters the text into a database. |
|Smart customer service quality checks |Upload call center audio files for conversion to text, then search the text to identify illegal or sensitive terms and words. |


<span id="6d0d902f"></span>
## Overall workflow

The process of adding subtitles to a video generally involves two main steps, as shown in the flowchart below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4b57f2660a74853b51af2bf85961629~tplv-goo7wpa0wc-image.image) </span>

<span id="bb1c402a"></span>
## Step 1: Prepare the subtitle file

Before you can display subtitles, you need a subtitle file. You can either generate one using VOD's AI capabilities or upload one you already have.

<span id="f271cfa0"></span>
### Option 1: Generate subtitle files with AI

If you don't have a subtitle file, you can use a **Smart subtitling template** to automatically generate one. The subtitles are generated in the WebVTT file format. This template uses AI to perform tasks like:


* **Extract subtitles**: Extracts subtitles from the source video that you provide and generates subtitle files, allowing for convenient subtitle editing as required.

* **Speech\-to\-text**: Converts the audio in media files into text and generates accurate subtitles.

* **Machine translation**: Translates subtitles into other languages.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The BytePlus VOD smart subtitling feature is billed based on usage. Please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#e250f532">Smart subtitling pricing</a> for detailed information on pricing and billing.</div>


<span id="5a096a1e"></span>
#### 1. Create a smart subtitling template

Smart subtitling templates can be configured in the [BytePlus VOD console](https://console.byteplus.com/vodpaas/welcome/), as shown in the figure below. You can choose one of the pre\-built templates or create your own. For detailed steps, see [Smart subtitling template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-smart-subtitle-template).

If you need to generate subtitle files in multiple languages, enable **Machine translation** to translate existing subtitle files into other languages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/473572ce012149db9e65878fda78a0b3~tplv-goo7wpa0wc-image.image) </span>

<span id="05420c3e"></span>
#### 2. Configure a smart subtitling task in your workflow

Smart subtitling tasks can be configured in a workflow using the [BytePlus VOD console](https://console.byteplus.com/vodpaas/welcome/), as shown in the figure below. It is recommended to enable **Auto subtitle publishing**. Subtitles generated through this workflow will then be published automatically. If you need to generate subtitle files in multiple languages, it is recommended to enable **custom file** **path** and add `{{lang}}` variables to distinguish between subtitle files in multiple languages. For detailed steps, see the [workflow](https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36d75f7ebd79426d832cbc9227bd2675~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f02f587d9c304994ba06f022f83f12aa~tplv-goo7wpa0wc-image.image) </span>

<span id="cc1de642"></span>
#### 3. Trigger the smart subtitling task

Media processing tasks can be triggered via the console and OpenAPI to generate subtitle files. The details are as follows:


* Using the console: See [Media processing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-processing_1) for specific steps.

* Using OpenAPI: Calling the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) interface triggers the workflow. You need to pass in the workflow ID that contains the smart subtitling task.


<span id="5c304440"></span>
#### 4. Fetch the smart subtitling results

Use the BytePlus VOD console or OpenAPI to view the smart subtitling results and fetch the URL of the subtitle file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Make sure that you have added the domain name for VOD acceleration, enabled VOD scheduling, and set the primary distribution protocol to HTTPS, so that you can download and preview subtitles and obtain the URL of the subtitle file in the console. See <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-configuring">Adding and configuring domain name</a> for details.</div>



<Tabs>
<Tab zoneid="BPi5MSrmpv" title="Console">
<TabTitle>Console</TabTitle>

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/welcome/) and go to the corresponding space.

2. In the left navigation bar, click **Media assets** \> **Videos**.

3. On the **Videos** page, click **Details**.

4. On the **Video details** page, click **Subtitle file**.

5. On the **Subtitle file** page, you can save the generated subtitle files.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc5e715980324b1d9f7cd54c6bb9631f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="X3KVkLZqZH" title="OpenAPI/Server SDK">
<TabTitle>OpenAPI/Server SDK</TabTitle>

* Call the [GetWorkflowExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getworkflowexecution) interface to view the workflow execution status.

* Call the [GetSubtitleInfoList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getsubtitleinfolist) interface to fetch all subtitle files for the specified Vid. You can fetch the URL for the subtitle file using the `SubtitleUrl` field in the return parameter.


</Tab>
<Tab zoneid="s0NN58Rvxf" title="Event notifications">
<TabTitle>Event notifications</TabTitle>

If you have configured event notifications, you can fetch smart subtitling product information by receiving the `SubtitleInfo` field in the [workflowComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete) notification.


</Tab>
</Tabs>


<span id="83acc5cd"></span>
### Option 2: Managing existing subtitle files

If you already have a subtitle file, you can upload it to the BytePlus VOD service and bind it to the Vid. The subtitle file is then managed centrally via Vid. For example, the [GetSubtitleInfoList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getsubtitleinfolist) interface can be called to pass in the Vid and obtain the URL of the subtitle file. BytePlus VOD supports uploading subtitle files in WebVTT, SRT, ASS, and SSA formats.


<Tabs>
<Tab zoneid="bhGZmW6Rpa" title="Console">
<TabTitle>Console</TabTitle>

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/welcome/) and go to the corresponding space.

2. Click the **Details** button in the **Action** column for the target video.

3. On the **Subtitle File** page, click **Upload Subtitle**.

4. After selecting a local subtitle file, you can set the subtitle **Display label**, select the **Post automatically uploading** option, and set the **Subtitle language**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2e49fe9af7f4b8e94c6b52d5026277c~tplv-goo7wpa0wc-image.image) </span>

5. Click **Save**.


</Tab>
<Tab zoneid="SaY3bOfTYK" title="OpenAPI/Server SDK">
<TabTitle>OpenAPI/Server SDK</TabTitle>

When calling the [CommitUploadInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-commituploadinfo) interface, upload the subtitle file using the `CaptionUpload` parameter and bind it to the Vid.


</Tab>
</Tabs>


<span id="99dc7f40"></span>
## Step 2: Display the subtitles

<span id="aeb4587f"></span>
### Option 1: Displaying as hardcoded subtitles


1. **Create a hardcoded subtitle styling template**: This template defines the **visual style** of the subtitles, such as font size, color, position, and background. For detailed instructions, see [Hardcoded subtitle styling template parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template#10d8cc3c).

2. **Configure the Transcoding Task**: In your workflow, add a **Video transcoding task** or **Low\-bitrate HD transcoding task**. Within that task's configuration, enable the **Hardcode subtitles** option and select the **subtitle language** of the subtitle file you want to burn into the video and the **Hardcoded subtitle styling template** you created in the previous step. The subtitle file in the specified language will be hardcoded in the video.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Subtitle files need to be published before they can be hardcoded into video files.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The hardcoded subtitles come from the subtitle file that you previously generated or bound to your video in <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-smart-captioning#bb1c402a">Step 1: Prepare the subtitle file</a>, and the <strong>Subtitle language</strong> option corresponds to the language of the subtitle file.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a876a225d464e39b6d30a8eed102b39~tplv-goo7wpa0wc-image.image) </span>

3. **Trigger the workflow:**  When you trigger this workflow, the VOD service will perform the transcoding and burn the selected subtitles into the new video output, using the style you defined.

4. **Play the video:**  After transcoding, you can play the video with hardcoded subtitles using the console, the Player SDK, or other players. Please refer to [Playing videos overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-videos-overview) for further details.


<span id="b4d5686f"></span>
### Option 2: Adding external subtitles to playback

If you use the BytePlus VOD Player SDK to play audio and video, refer to the following documents to implement external subtitles in the player:


* [Adding external subtitles for Android Player SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-external-subtitles-android): Supports using Vid and DirectUrl to implement external subtitles.

* [Adding external subtitles for iOS Player SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-external-subtitles-android): Supports using Vid and DirectUrl to implement external subtitles.

* [External subtitles in Web SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-plugins-web#external-subtitle): Supports using Vid to implement external subtitles.

* [External subtitles in React Native SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-basic-features#external-subtitles): Supports using Vid and DirectUrl to implement external subtitles.
