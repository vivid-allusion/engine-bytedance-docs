---
title: "Subtitle templates"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-smart-subtitle-template"
---

BytePlus VOD offers two powerful subtitle templates to enhance your videos: **smart subtitling templates** that use AI to automatically generate subtitles, and **hardcoded subtitle styling templates** that permanently burn custom styles into your video frames. This document introduces the capabilities of each and guides you through creating and configuring them.

<span id="62435394"></span>
## Feature overview

BytePlus VOD offers two types of subtitle templates to meet different needs:


* **Smart subtitling template:**  This template utilizes advanced AI algorithms to **automatically generate** subtitle files from your media. Key capabilities include:

   * **Extract subtitles**: Extracts subtitles from the source video that you provide and generates subtitle files, allowing for convenient subtitle editing as required.

   * **Speech\-to\-text**: Converts the audio in media files into text and generates accurate subtitles.

   * **Machine translation**: Translates subtitles into other languages.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The smart subtitling feature is billed based on usage. Please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#e250f532">Smart subtitling pricing</a> for detailed information on pricing and billing.   </div>
   

* **Hardcoded subtitle styling template:**  This template allows you to **hardcode permanent, stylized subtitles** directly onto your video frames during the transcoding process. It is ideal for ensuring subtitles are always visible and display with a consistent look across all platforms.


<span id="6dd6f799"></span>
## Creating a subtitle template


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar, and click **Enter space** to enter the designated space.

3. Click **Media processing** \> **Templates** on the left navigation bar.

4. Switch to the **Subtitle** tab. You can see two sub\-tabs: **Hardcoded subtitle template** and **Smart subtitling template**. Select the tab for the type of template you wish to create.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260717065340-1704872712505.png) </span>

5. Click the corresponding button to create a new template.

6. Configure the parameters as described in the relevant section below.

   * [Hardcoded subtitle styling template parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template#10d8cc3c)

   * [Smart subtitling template parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template#7cd57594)

7. Click **Save**.


<span id="10d8cc3c"></span>
## Hardcoded subtitle styling template parameters

This template is used to hardcode subtitles into video frames during a transcoding job.

<span id="b4805a82"></span>
### Basic information


|**Parameter** |**Description** |
|---|---|
|Template name |A unique name for your template (up to 64 characters). |
|Template description |An optional description of the template's purpose (up to 140 characters). |
|Label |A unique identifier for the template. The label acts as a query parameter in the `GetPlayInfo` API call, allowing you to fetch a playback URL with this specific hardcoded subtitle style applied. Only lowercase letters and underscores (`_`) are allowed. |


<span id="5c3514b1"></span>
### Subtitle configuration

Configure the visual appearance and positioning of the hardcoded subtitles.


|**Parameter** |**Description** |
|---|---|
|Video resolution |Sets the reference canvas resolution that subtitle styling (such as font size, margins) is based on. The console preview window will update to match the aspect ratio you select. The available options are:<br><br><br>* 16:9 (1280 × 720)<br><br>* 9:16 (720 × 1280)<br><br>* 4:3 (960 × 720)<br><br>* 3:4 (720 × 960)<br><br>* 1:1 (720 × 720)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This resolution serves only as a styling reference. During transcoding, the subtitle style will be proportionally scaled to fit the actual output resolution of the video.</div><br> |
|Subtitle position |The vertical alignment of the subtitles on the video frame. The available options are:<br><br><br>* At the bottom of the video<br><br>* At the center of the video<br><br>* At the top of the video |
|Distance from bottom |This parameter is only available when **Subtitle position** is set to **At the bottom of the video**. Defines the vertical margin between the subtitle text and the bottom edge of the video frame, measured in pixels. |
|Distance from top |This parameter is only available when **Subtitle position** is set to **At the top of the video**. Defines the vertical margin between the subtitle text and the top edge of the video frame, measured in pixels. |
|Font |The font family to be used for the subtitle text. See [Font options](https://docs.byteplus.com/en/docs/25/7867#hardcoded-subtitle-font-options). |
|Font size |The size of the subtitle font. |
|Text color |The color of the subtitle text, specified in RGBA hex format. |
|Subtitle track mode |Determines how the width of the subtitle's background box is calculated. The available option is:<br><br>**Fit to text**: The background box will dynamically resize to match the length of each line of subtitle text. |
|Subtitle track background color |The color of the semi\-transparent background box behind the text, specified in RGBA hex format. |
|Background border |The shape of the background box's corners. The available option is **Right angle**. |


<span id="hardcoded-subtitle-font-options"></span>
### Font options

The following fonts are available for hardcoded subtitle styling templates.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The available fonts collectively cover Simplified Chinese, Traditional Chinese, Japanese, Korean, Thai, and many languages written in Latin, Cyrillic, and Greek scripts, such as English, Turkish, and Portuguese. Character coverage varies by font. Select a font that supports the subtitle language and all characters used in the subtitle file; otherwise, subtitles may appear garbled or may not be displayed.</div>



|**Font family** |**Available weights** |
|---|---|
|SourceHan Sans CN |Regular, Medium, Bold |
|ResourceHan Rounded CN |Regular, Medium, Bold |
|HanziPinyin |Regular |
|SourceHan Serif TW |Regular, Medium, Bold |
|Taipei Sans TC |Regular, Bold |
|AbhayaLibre |Regular, Medium, Bold |
|S\-Core Dream |Regular, Medium, Bold |
|AndikaNew Basic |Regular, Bold |
|TH Bai Jamjuree CP |Regular, Medium, Bold |
|Inter |Regular, Medium, Bold |
|Noto Sans |Regular, Medium, Bold |
|Noto Sans SC |Regular, Medium, Bold |
|Roboto |Regular, Medium, Bold |
|OPPO Sans |Regular, Medium, Bold |
|Montserrat |Regular, Medium, Bold |


<span id="7cd57594"></span>
## Smart subtitling template parameters

<span id="04888607"></span>
### Basic information


|**Parameter** |**Description** |
|---|---|
|Template name |The length of the template name cannot exceed 64 characters. It is recommended to use a name that identifies the template's purpose. |
|Template description |The length of the template description cannot exceed 140 characters. |


<span id="b6b9d123"></span>
### Subtitle parameters

Select the subtitle source and configure subtitle settings accordingly. The following settings are available:

<span id="462029dd"></span>
#### Extract subtitle stream

Subtitle stream extraction is suitable for scenarios where the source video already contains subtitle streams. The supported parameters are as follows:


|**Parameter** |**Description** |
|---|---|
|Identify language |* Simplified Chinese<br><br>* English<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If the source video lacks subtitle streams or the system fails to recognize the subtitle language you specified, no subtitle file will be output.</div><br> |
|Container format |* WebVTT<br><br>* SRT |


<span id="d720d2b0"></span>
#### Speech\-to\-text subtitles

If the source video's language matches the selected speech recognition language, the system will perform speech\-to\-text to generate subtitles. The supported parameters are as follows:


|**Parameter** |**Description** |
|---|---|
|Identify language |Supports Simplified Chinese, English, Korean, Japanese, Spanish, Indonesian, Traditional Chinese, Thai, Malay, Vietnamese, Filipino, and Russian. Multiple selections are supported. |
|Container format |* WebVTT<br><br>* SRT |


<span id="d75f4274"></span>
#### Machine translation subtitles

With machine translation subtitles enabled, the system will translate existing subtitle files into other languages. The supported parameters are as follows:


|**Parameter** |**Description** |
|---|---|
|Source language |Supports Simplified Chinese, English, Korean, Japanese, Thai, Malay, Indonesian, Hindi, Vietnamese, Spanish, Traditional Chinese, Filipino, Russian, and Ukrainian. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Machine translation will not be performed if no subtitle file is present.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Machine translation will not be performed if the source and target languages are the same.</div><br> |
|Target language |Supports Simplified Chinese, English, Korean, Japanese, Thai, Malay, Indonesian, Hindi, Vietnamese, Spanish, Traditional Chinese, Filipino, Russian, and Ukrainian. Multiple selections are supported. |
|Container format |* WebVTT<br><br>* SRT |


<span id="698cef3f"></span>
## Next step

For a comprehensive guide on how to use the smart subtitling feature, please see [Adding subtitles to videos](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-captioning).
