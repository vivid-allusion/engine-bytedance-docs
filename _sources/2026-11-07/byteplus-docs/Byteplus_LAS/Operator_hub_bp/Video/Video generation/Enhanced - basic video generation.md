---
title: "Enhanced/basic video generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/video_gen_enhanced"
---

The LAS Enhanced Video Generation/Basic Video Generation service is built around the Seedance 2.x series models, and enhances both the pre\-processing and post\-processing workflows for video generation. It integrates capabilities such as video format conversion, video segmentation, Video Inpaint, subtitle generation, Audio and Video Merge, Video Super Resolution, and more, expanding the boundaries of video generation models, improving the quality and duration of generated videos, reducing token consumption costs, and helping customers increase production efficiency.

<span id="03d155f5"></span>
# **Operator introduction**

<span id="c946bbef"></span>
## Application scenarios

As a general\-purpose large video generation model, Seedance can be flexibly applied to a wide range of video generation scenarios. For example:


* Marketing and promotional videos: product promotion, brand advertising shorts, event or holiday marketing content. Supports direct generation from text or images, suitable for high\-frequency, batch material production.

* Short video content production: Douyin/Video Account/Bilibili content, MCN batch production, rapid content creation for individual creators. Provides generation, editing, and extension capabilities, with an emphasis on style, camera movement, and character stability control.

* Image\-to\-video / photo animation: converting static posters to dynamic content, dynamic interpretation of product or character images, animating old photos or illustrations. Supports text\-to\-video and image\-to\-video; some versions support control of the first and last frames.

* Video editing and remixing: re\-editing, video extension, stylization, multi\-source merging. The 2.x series explicitly supports video editing and extension, not just generation from scratch.

* Education and knowledge expression: course explanation shorts, animated picture books or science popularization, teaching demonstration videos. Visualizes abstract knowledge or script content to improve communication efficiency.

* Digital human / character consistency content: virtual anchors, virtual idols, digital humans for enterprise training. Ensures stable character features, object detail, and style restoration capabilities.

* E\-commerce and livestreaming materials: product display videos, virtual scene demonstrations, livestream room warm\-up or clips. Enables large\-scale, rapid, and low\-cost material production, highly suited for e\-commerce scenarios.


<span id="f1f8a70c"></span>
## Effect demonstration


---



<div style="text-align: center">
<strong>[Multimodal reference]</strong></div>



* Enter prompt

> Based on reference images and reference videos, generate an advertisement video for LAS tea drink with Peking Opera makeup. The opening of the video basically matches reference image 1. In the middle section, the character walks to a desk, sees a pot of wine and a cup of LAS tea drink (reference image 2), shows slight hesitation, then chooses the LAS tea drink and drinks a sip with a straw. Close\-up: after drinking, the character's previously dazed eyes instantly become bright, with a smile at the corner of their mouth, and says the line: "LAS tea drink, a sip of Beijing flavor. The story intoxicates, but you awaken." Then, at the end of the video, the character holds LAS in their left hand, raises their right hand's water sleeve slightly, and strikes the classic 'Please enjoy' pose. "


* Reference image 1

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f247971b2bd406eafb32d7e8a5a4297~tplv-goo7wpa0wc-image.image) </span>

* Reference image 2

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/220b33f3471a44d097c4ce90bf86e866~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc0321b7e4a4c36a9357d872cb962b1~tplv-goo7wpa0wc-image.image" controls></video>




---



<div style="text-align: center">
<strong>Edit video – convert video style</strong></div>



* Enter prompt

> Convert the reference video into a Chinese ink animation style video, changing only the video style to Chinese ink animation, including the character, environment, props, and camera movement, while keeping all other aspects unchanged.


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc0321b7e4a4c36a9357d872cb962b1~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2635dbc2ed824164854f1ffb5c96eda3~tplv-goo7wpa0wc-image.image" controls></video>



<div style="text-align: center">
<strong>Edit video – convert environment in video</strong></div>



* Enter prompt

> Replace the environment in the reference video with the environment from the reference image, keeping the character, props, and camera movement unchanged and smooth.


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11794a1e100146f2aa9241a735c1bbc5~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc0321b7e4a4c36a9357d872cb962b1~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c14938b7e094996a0cab7b283d00542~tplv-goo7wpa0wc-image.image" controls></video>



<div style="text-align: center">
<em><ins>\>\> LAS provides you with </ins></em><a href="https://docs.byteplus.com/docs/undefined/69f327096cf2690500653140"><em><ins>Video Editing Enhanced Edition</ins></em></a><em><ins>, and other operators, offering more convenient and stable editing for replacement, audio merging, and other capabilities.</ins></em></div>



---



<div style="text-align: center">
<strong>Extend video</strong></div>



* Enter prompt

> The arched window in video 1 opens, and the camera enters the interior of the art gallery, then continues with video 2. Afterwards, the camera moves into the painting, then continues with video 3.


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54519ff7266d4f1caa12b8cc95e2dd1d~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b15d56c80c884faa8526beb6ca540b98~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5d327311e094361b15dca0a37b14ab4~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/849b3f86f609495ca09d559aa14c79ed~tplv-goo7wpa0wc-image.image" controls></video>




---



<span id="733f6c8d"></span>
## Supported models


|Model series |Supported models |
|---|---|
|Seedance 2.x series models |* Video generation \- basic version:<br><br>   * dreamina\-seedance\-2\-0\-fast\-260128<br><br>   * dreamina\-seedance\-2\-0\-mini\-260615<br><br>* Video generation \- enhanced version:<br><br>   * dreamina\-seedance\-2\-0\-260128<br><br>   * dreamina\-seedance\-2\-5\-260628 |


<span id="d67abccd"></span>
## Model capabilities


|Function |Subfeature / parameter |Seedance 2.5 |Seedance 2.0 |Seedance 2.0 Fast |Seedance 2.0 Mini |
|---|---|---|---|---|---|
|Text\-to\-video |`"content.tpye": "text"` |✅ |✅ |✅ |✅ |
|Image\-to\-video |Image\-to\-video \- first frame |✅ |✅ |✅ |✅ |
||Image\-to\-video \- first and last frames |✅ |✅ |✅ |✅ |
|Multimodal reference |Image reference |✅ |✅ |✅ |✅ |
||Video reference |✅ |✅ |✅ |✅ |
||* Combined reference<br><br>   * Image + audio<br><br>   * Image + video<br><br>   * Video + audio<br><br>   * Image + video + audio |✅ |✅ |✅ |✅ |
|Edit video |Not applicable |✅ |✅ |✅ |✅ |
|Extend video |Not applicable |✅ |✅ |✅ |✅ |
|Generate video with audio |`"generate_audio": "true"` |✅ |✅ |✅ |✅ |


<span id="5f547f62"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="02af85da"></span>
## Operator performance


|Sub\-item |Performance impact description |
|---|---|
|Maximum RPM |* Non\-4k resolution: 600<br><br>* 4k resolution: 15 |
|Maximum concurrency |* Non\-4k resolution: 10<br><br>* 4k resolution: 1 |


<span id="ae7d120b"></span>
# Input and output requirements

<span id="b3a7a432"></span>
## Input requirements


|Subcategory |Detailed requirements |
|---|---|
|Input data modality |* Text<br><br>* Image<br><br>* Video<br><br>* Audio<br><br><br>The following combinations are supported:<br><br><br>* **Text**<br><br>* **Text + image**<br><br>* **Text + video**<br><br>* **Text + image + audio**<br><br>* **Text + image + video**<br><br>* **Text + video + audio**<br><br>* **Text + image + video + audio**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using different Seedance models, the supported input data modalities may vary. For details, refer to the "Model capabilities" section above.</div><br> |
|General requirements |The Seedance 2.x series models do not support directly uploading reference images or videos containing real human faces. To facilitate creators' use of portraits, you can apply to activate the LAS material library feature (allowlist feature), upload authorized real reference images or videos to the material library, and input the material library ID to the model. |
|Input format: image |* Formats: jpeg, png, webp, bmp, tiff, gif. Among them, Seedance 1.5 Pro and Seedance 2.x series models additionally support heic and heif.<br><br>* Aspect ratio (width/height): [0.4, 2.5]<br><br>* Width and height (px): [300, 6000]<br><br>* Size: Each image must be less than 30 MB. Request body size must not exceed 64 MB.<br><br>* Number of images:<br><br>   * Image\-to\-video \- first frame: 1 image<br><br>   * Image\-to\-video \- first and last frames: 2 images<br><br>   * Seedance 2.0 series multimodal reference video generation: 1–9 images.<br><br>   * Seedance 2.5 series multimodal reference video generation: 1–30 images. |
|Input format: video |* Format: mp4, mov.<br><br>* Resolution: 480p, 720p, 1080p, 4k<br><br>* Duration:<br><br>   * Seedance 2.0: Single video duration [2, 15] s, up to 3 reference videos can be provided, and the total duration of all videos must not exceed 15 s.<br><br>   * Seedance 2.0: Single audio duration [2, 30] s, up to 10 reference audio segments can be provided, and the total duration of all audio must not exceed 30 s.<br><br>* Dimensions:<br><br>   * Aspect ratio (width/height): [0.4, 2.5]<br><br>   * Width and height (px): [300, 6000]<br><br>   * Total pixel count: [640×640=409600, 3326×2494=8295044], that is, the product of width and height must be within the range [409600, 8295044].<br><br>* Size: Each video must not exceed 200 MB.<br><br>* Frame rate (FPS): [24, 60] |
|Input format: audio |* Format: wav, mp3<br><br>* Duration:<br><br>   * Seedance 2.0: Single audio duration [2, 15] s, up to 3 reference audio segments can be provided, and the total duration of all audio must not exceed 15 s.<br><br>   * Seedance 2.5: Single audio duration [2, 30] s, up to 10 reference audio segments can be provided, and the total duration of all audio must not exceed 30 s.<br><br>* Size: Each audio file must not exceed 15 MB, and the request body must not exceed 64 MB.<br><br>* Other:<br><br>   * Seedance 2.0 does not support inputting audio alone; at least one reference video or image must be included.<br><br>   * Seedance 2.5 supports inputting audio alone as a reference for video generation. |
|Input path requirements |Provide input data to the operator via the `content` request parameter. The following input methods are supported for images, audio, and video:<br><br><br>* Public URL: A publicly accessible video URL in the format `http/https`.<br><br>   * Public URLs that require login status or additional header authentication are not supported; temporary URLs must remain valid during task execution.<br><br>* Base64 encoding (supported for audio/images): Convert the local file to a Base64\-encoded string, then submit it to the large model. Follow the format: `data:image/<image or audio format>;base64,<Base64 encoding>`. Note that `<image or audio format>` must be lowercase, for example, `data:image/png;base64,{base64_image}`. Do not use Base64 encoding for large files.<br><br>* Asset ID (allowlist feature): After enabling the LAS asset library management feature, you can upload assets to the LAS asset library and obtain the corresponding asset ID from the LAS asset library management page. When calling the video generation operator, you can use the asset ID as a reference input for video generation, following the format: `asset://<ASSET_ID>`. |


<span id="ab411cf5"></span>
## Output requirements


|Breakdown |Detailed requirements |
|---|---|
|Output data type |* Video<br><br>* Restriction: Currently, frame rate adjustment is not supported. |
|dreamina\-seedance\-2\-0\-260128<br><br>(audio and video co\-generation) |* Resolution: 480p, 720p, 1080p, 4k (10\-bit depth)<br><br>* Frame rate: 24 fps<br><br>* Duration: 4–15 seconds<br><br>* Video format: mp4 |
|dreamina\-seedance\-2\-5\-260628<br><br>(audio and video co\-generation) |* Resolution: 480p, 720p<br><br>* Frame rate: 24 fps<br><br>* Duration: 4–30 seconds<br><br>* Video format: mp4 |
|dreamina\-seedance\-2\-0\-fast\-260128<br><br>(audio and video co\-generation) |* Resolution: 480p, 720p<br><br>* Frame rate: 24 fps<br><br>* Duration: 4–15 seconds<br><br>* Video format: mp4 |
|dreamina\-seedance\-2\-0\-mini\-260615<br><br>(audio and video co\-generation) |* Resolution: 480p, 720p<br><br>* Frame rate: 24 fps<br><br>* Duration: 4–15 seconds<br><br>* Video format: mp4 |
|Output path: API |After the operator completes processing, the pre\-signed link for the generated video is returned directly through the video generation task query interface. The link is valid for 24 hours. |


<span id="9125e26d"></span>
# Billing information


* Billing standards

   
   |Breakdown |Description of billing standards |
   |---|---|
   |Billing item |Duration of input/output video. |
   |Billing type |Pay\-as\-you\-go, unit: USD/second, billed hourly based on actual billing usage. |
   |Unit price |Related to the model version you select (Basic version, Enhanced version). |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Total cost: In addition to the unit price, it also depends on the duration and resolution of the input/output video.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only tasks that successfully generate videos will incur charges. Scenarios where video generation fails due to review or other operational reasons will not be charged.   </div>
   

* Billing details

   Billing estimate: `Total cost ≈ Unit price * Billing usage = Unit price * (Video duration * Duration conversion factor)`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The above formula is for cost estimation only. Actual charges are determined by the bill.   </div>
   

   
   |Version breakdown |Unit price |Model type |Scenario breakdown |Billing item: Video duration |Duration conversion factor: Related to video resolution |
   |---|---|---|---|---|---|
   |Basic version |0.242 USD/second |seedance2.0fast |No input video |Output video duration |* 480P：0.465<br><br>* 720P：1 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.2770<br><br>* 720P：0.5988 |
   |||seedance2.0mini |No input video |Output video duration |* 480P：0.2907<br><br>* 720P：0.625 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.1769<br><br>* 720P：0.3812 |
   |Enhanced version |0.303 USD/second |seedance2.0 |No input video |Output video duration |* 480P：0.4651<br><br>* 720P：1<br><br>* 1080P：2.5<br><br>* 4k：5.0761 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.2830<br><br>* 720P：0.6098<br><br>* 1080P：1.5251<br><br>* 4k：3.1348 |
   |||seedance 2.5 |No input video |Output video duration |* 480P：0.6785<br><br>* 720P：1.525 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.406<br><br>* 720P：0.9125 |
   

* Billing example

   * Example scenario: Using the enhanced version of video generation (Seedance 2.0), the input includes a reference video (duration: 10 seconds), the output video duration is 10 seconds, and the resolution is 1080p.

   * Cost details:

      `Total cost ≈ Unit price * Billing usage = 0.303 USD/second * (10 seconds + 10 seconds) * 1.5251 = 9.2421 USD`


<span id="9e8b5806"></span>
# Notes and prerequisites


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="8bc1e275"></span>
# **API call**

<span id="1a237a84"></span>
## Generate

`POST https://operator.las.ap-southeast-1.bytepluses.com/api/v1/contents/generations/tasks`

<span id="7391dd64"></span>
### API description

Use the seedance model to generate videos.

<span id="e7b73623"></span>
### Request parameters

```mixin-react
const properties = ({
  "columns": [
    { "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
    { "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
    { "title": "Required", "dataIndex": "column_2", "key": "column_2", "width": 80 },
    { "title": "Example value", "dataIndex": "column_3", "key": "column_3", "width": 150 },
    { "title": "Description", "dataIndex": "column_4", "key": "column_4" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "model",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "dreamina-seedance-2-0-260128",
      "column_4": <div> The model ID you need to call. Supported:<ul><li>dreamina-seedance-2-5-260628</li><li>dreamina-seedance-2-0-260128</li><li>dreamina-seedance-2-0-mini-260615</li><li>dreamina-seedance-2-0-fast-260128</li></ul></div>
    },
    {
      "key": "2",
      "column_0": "content",
      "column_1": "object[]",
      "column_2": "Yes",
      "column_3": "https://example.com/reference-image.png",
      "column_4": "Content provided to the model for generation. Supports text, image, video, and audio.",
      "children": [
        {
          "key": "2-1",
          "column_0": "type",
          "column_1": "string",
          "column_2": "Yes",
          "column_3": "text",
          "column_4": <div> Content type. Supported:<ul><li><b> text</b>: Prompt information provided to the model. </li><li><b> image_url</b>: Image information provided to the model. </li><li><b> video_url</b>: Video information provided to the model. </li><li><b> audio_url</b>: Audio information provided to the model. </li></ul></div>
        },
        {
          "key": "2-2",
          "column_0": "text",
          "column_1": "string",
          "column_2": "No",
          "column_3": "",
          "column_4": <div> Required when type is text. The text prompt provided to the model, describing the expected video to be generated. <ul><li> Prompt language support: All models support Chinese and English prompts; the Seedance 2.x series additionally supports Japanese, Indonesian, Spanish, and Portuguese. </li><li> Chinese prompts must not exceed 500 characters, English prompts must not exceed 1,000 words. Excessive word count can lead to dispersed information, causing the model to overlook details and focus only on key points, which may result in missing elements in the generated video. </li></ul></div>
        },
        {
          "key": "2-3",
          "column_0": "image_url",
          "column_1": "object",
          "column_2": "No",
          "column_3": "",
          "column_4": "Required when type is image_url. Image input object.",
          "children": [
            {
              "key": "2-3-1",
              "column_0": "url",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "",
              "column_4": <div> Image object provided to the model. Supports: public image URL, image Base64 encoding, or asset ID. <ul><li> For requirements regarding image format, size, quantity, and so on, please refer to the above <code> Input and Output</code> section. </li><li> When providing image input to the model, you can also use the <code> role</code> request parameter to specify the position or purpose of the input image. </li></ul></div>
            }
          ]
        },
        {
          "key": "2-4",
          "column_0": "video_url",
          "column_1": "object",
          "column_2": "No",
          "column_3": "",
          "column_4": "Required when type is video_url. Video input object.",
          "children": [
            {
              "key": "2-4-1",
              "column_0": "url",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "",
              "column_4": <div> Video object provided to the model. Supports: public video URL, asset ID. <ul><li> For requirements regarding video format, size, quantity, and so on, please refer to the above <code> Input and Output</code> section. </li><li> When providing video input to the model, you can also use the <code> role</code> request parameter to specify the position or purpose of the input video. </li></ul></div>
            }
          ]
        },
        {
          "key": "2-5",
          "column_0": "audio_url",
          "column_1": "object",
          "column_2": "No",
          "column_3": "",
          "column_4": "Required when type is audio_url. Audio input object.",
          "children": [
            {
              "key": "2-5-1",
              "column_0": "url",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "",
              "column_4": <div> Audio object input to the model. Supported input: public audio URL, audio Base64 encoding, or material ID. <ul><li> For requirements regarding audio format, size, and quantity, refer to the <code> Input and Output</code> section above. </li><li> When providing audio input to the model, you can also use the <code> role</code> request parameter to specify the position or purpose of the input audio. </li></ul></div>
            }
          ]
        },
        {
          "key": "2-7",
          "column_0": "role",
          "column_1": "string",
          "column_2": "No",
          "column_3": "",
          "column_4": <div> Position or purpose of the media content. Supported values for different types are as follows:<br/><br/> For image input, <code> role</code> values include:<ul><li><b> first_frame</b>: Image-to-video - first frame. </li><li><b> last_frame</b>: Image-to-video - last frame. Inputting only the last frame image is not supported. When generating a video based on first and last frame images, you need to provide two image_url objects and set the role value for each image as first_frame and last_frame, respectively. </li><li><b> reference_image</b>: Image-to-video: reference image. </li></ul><br/> For video input, <code> role</code> values include:<b> reference_video</b>, indicating the input is a reference video. <br/><br/> For audio input, <code> role</code> values include:<b> reference_audio</b>, indicating the input is a reference audio. </div>
        }
      ]
    },
    {
      "key": "3",
      "column_0": "callback_url",
      "column_1": "string",
      "column_2": "Optional",
      "column_3": "`http://xxx/callback`",
      "column_4": <div> Callback notification address for the result of this generation task. When the task status changes, ModelArk will send a POST request to this address. Callback statuses include:<ul><li> queued: queued</li><li> running: running</li><li> succeeded: succeeded</li><li> failed: failed</li><li> expired: expired</li></ul> </div>
    },
    {
      "key": "4",
      "column_0": "return_last_frame",
      "column_1": "boolean",
      "column_2": "Optional",
      "column_3": "false",
      "column_4": <div> Whether to return the last frame image of the video. Default is false. <ul><li> true: Returns the last frame image, which can be used to stitch consecutive videos</li><li> false: Does not return the last frame image</li></ul> </div>
    },
    {
      "key": "5",
      "column_0": "execution_expires_after",
      "column_1": "integer",
      "column_2": "Optional",
      "column_3": "172800",
      "column_4": "Task timeout threshold, in seconds. Default is 172800 seconds (48 hours), value range is 3600 to 259200."
    },
    {
      "key": "6",
      "column_0": "generate_audio",
      "column_1": "boolean",
      "column_2": "Optional",
      "column_3": "true",
      "column_4": <div> Controls whether the generated video includes sound synchronized with the visuals. Default is true. <ul><li> true: Outputs video with synchronized audio</li><li> false: Outputs silent video</li></ul> </div>
    },
    {
      "key": "8",
      "column_0": "resolution",
      "column_1": "string",
      "column_2": "Optional",
      "column_3": "720p",
      "column_4": <div> Video resolution. Optional values:<ul><li> 480p</li><li> 720p: Seedance 2.x series defaults to 720p</li><li> 1080p</li><li> 4k</li></ul> Among them:<ul><li> 1080p: Not supported in reference image scenarios; Seedance 2.5, Seedance 2.0 Fast, and Seedance 2.0 Mini are not supported. </li><li> 4k: Supported only by Seedance 2.0. </li></ul></div>
    },
    {
      "key": "9",
      "column_0": "ratio",
      "column_1": "string",
      "column_2": "Optional",
      "column_3": "16:9",
      "column_4": <div> Aspect ratio for the generated video. Supported:<ul><li> 16:9</li><li> 4:3</li><li> 1:1</li><li> 3:4</li><li> 9:16</li><li> 21:9</li><li> adaptive: Automatically selects the most suitable aspect ratio based on the input. </li></ul><br/> adaptive adaptation rules:<ul><li> Text-to-video: Intelligently selects the most suitable aspect ratio based on the input prompt. </li><li> First frame / first and last frame video generation: Automatically selects the closest aspect ratio based on the ratio of the uploaded first frame image. </li><li> Multimodal reference video generation: Determine based on the user's prompt intent. If it is first-frame video generation, video editing, or video extension, select the aspect ratio closest to that image or video; otherwise, select the aspect ratio closest to the first media file provided (priority: "video" is higher than "image"). </li></ul></div>
    },
    {
      "key": "10",
      "column_0": "duration",
      "column_1": "integer",
      "column_2": "Optional",
      "column_3": "5",
      "column_4": "Either duration or frames can be specified; frames has higher priority than duration. To generate a video with an integer number of seconds, it is recommended to specify duration. Supported range: Seedance 2.0 supports 4 to 15 seconds; Seedance 2.5 supports 4 to 30 seconds."
    },
    {
      "key": "14",
      "column_0": "watermark",
      "column_1": "boolean",
      "column_2": "Optional",
      "column_3": "false",
      "column_4": <div> Whether the generated video contains a watermark. <ul><li> false: No watermark</li><li> true: Contains watermark</li></ul> </div>
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="ae635383"></span>
### Response parameters


|Parameter |Type |Note |
|---|---|---|
|id |string |Task ID, retained for 7 days only (calculated from the **created at** timestamp); after expiration, it will be automatically deleted. |


<span id="c9e98399"></span>
### Example

<span id="31b672c9"></span>
#### Request example

```Bash
curl --location 'https://operator.las.ap-southeast-1.bytepluses.com/api/v1/contents/generations/tasks' \
--header 'Authorization: Bearer $LAS_API_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "model": "dreamina-seedance-2-0-260128",
    "content": [
        {
            "type": "text",
            "text": "请把@视频1的背景替换成@图片1"
        },
        {
            "type": "image_url",
            "image_url": {
                "url": "image_url"
            },
            "role": "reference_image"
        },
        {
            "type": "video_url",
            "video_url": {
                "url": "video_url"
            },
            "role": "reference_video"
        }
    ],
    "generate_audio":false,
    "seed":42,
    "watermark": false
}'
```


<span id="8f7f70f4"></span>
#### Response example

```JSON
{
    "id": "lsd-89b8ea3232b8f1205702"
}
```


<span id="6e53c70c"></span>
## Task

`GET https://operator.las.ap-southeast-1.bytepluses.com/api/v1/contents/generations/tasks/{id}`

<span id="3114119a"></span>
### API description

Query the status of the video generation task.

<span id="ed123623"></span>
### Request parameters


|Parameter |Type |Required |Example value |Note |
|---|---|---|---|---|
|id |string |Yes |cgt\-2025\*\*\*\*\*\*\-\*\*\*\* |The ID of the video generation task you need to query.<br><br>This parameter is passed as a URL path segment. |


<span id="858d159b"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
{ "title": "Example value", "dataIndex": "column_2", "key": "column_2", "width": 150 },
{ "title": "Description", "dataIndex": "column_3", "key": "column_3" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "id",
      "column_1": "string",
      "column_2": "xxxx",
"column_3": "Video generation task ID."
    },
    {
      "key": "2",
      "column_0": "model",
      "column_1": "string",
      "column_2": "dreamina-seedance-2-0-260128",
"column_3": "Model name and version used for the task."
    },
    {
      "key": "3",
      "column_0": "status",
      "column_1": "string",
      "column_2": "succeeded",
"column_3": < div> Task status:< ul>< li>< code> queued</ code>(Queued)</ li>< li>< code> running</ code>(Running)</ li>< li>< code> cancelled</ code>(Cancelled, automatically deleted after 24 hours)</ li>< li>< code> succeeded</ code>(Succeeded)</ li>< li>< code> failed</ code>(Failed)</ li>< li>< code> expired</ code>(Timed out)</ li></ ul></ div>
    },
    {
      "key": "4",
      "column_0": "error",
      "column_1": "error",
      "column_2": "",
"column_3": < div> Error message. Returns < code> null</ code> when the task succeeds; returns an error object when the task fails. </div>,
      "children": [
        {
          "key": "4-1",
          "column_0": "code",
          "column_1": "string",
          "column_2": "Model.InvalidName",
"column_3": "Error code."
        },
        {
          "key": "4-2",
          "column_0": "message",
          "column_1": "string",
          "column_2": "The model name is invalid.",
"column_3": "Error message."
        }
      ]
    },
    {
      "key": "5",
      "column_0": "created_at",
      "column_1": "integer",
      "column_2": "1779348818",
"column_3": "Unix timestamp for task creation time, in seconds."
    },
    {
      "key": "6",
      "column_0": "updated_at",
      "column_1": "integer",
      "column_2": "1779348874",
"column_3": "Unix timestamp for the current task status update time, in seconds."
    },
    {
      "key": "7",
      "column_0": "content",
      "column_1": "content",
      "column_2": "",
"column_3": "Output content of the video generation task.",
      "children": [
        {
          "key": "7-1",
          "column_0": "video_url",
          "column_1": "string",
          "column_2": "https://example.com/generated.mp4",
"column_3": "URL of the generated video, in MP4 format, valid for 24 hours. Please download or save it promptly."
        },
        {
          "key": "7-2",
          "column_0": "last_frame_url",
          "column_1": "string",
          "column_2": "https://example.com/last-frame.png",
"column_3": < div> URL of the last frame image of the video, valid for 24 hours. Returned only if < code> return_last_frame=true</ code> is set when creating the task. </div>
        }
      ]
    },
    {
      "key": "8",
      "column_0": "seed",
      "column_1": "integer",
      "column_2": "78674",
"column_3": "Seed integer value actually used for this task."
    },
    {
      "key": "9",
      "column_0": "resolution",
      "column_1": "string",
      "column_2": "720p",
"column_3": "Resolution of the generated video."
    },
    {
      "key": "10",
      "column_0": "ratio",
      "column_1": "string",
      "column_2": "16:9",
"column_3": < div> Actual aspect ratio of the generated video; when < code> adaptive</ code> is used when creating the task, this field provides the final ratio. </div>
    },
    {
      "key": "11",
      "column_0": "duration",
      "column_1": "integer",
      "column_2": "5",
"column_3": < div> Actual duration of the generated video, in seconds; when < code> duration=-1</ code> is set when creating the task, this field provides the duration chosen by the model. </div>
    },
    {
      "key": "12",
      "column_0": "framespersecond",
      "column_1": "integer",
      "column_2": "24",
"column_3": "Frame rate of the generated video."
    },
    {
      "key": "13",
      "column_0": "generate_audio",
      "column_1": "boolean",
      "column_2": "true",
"column_3": < div> Whether the generated video contains synchronized audio. < code> true</ code> indicates a video with audio, < code> false</ code> indicates a silent video. </div>
    },
    {
      "key": "14",
      "column_0": "safety_identifier",
      "column_1": "string",
      "column_2": "user_7f3a9c",
"column_3": "Unique identifier for the end user set when creating the task; not returned if not set."
    },
    {
      "key": "15",
      "column_0": "priority",
      "column_1": "integer",
      "column_2": "0",
"column_3": "Execution priority of the current request."
    },
    {
      "key": "16",
      "column_0": "service_tier",
      "column_1": "string",
      "column_2": "default",
"column_3": < div> Service tier used for actual task processing. Default < code> default</ code>. </div>
    },
    {
      "key": "17",
      "column_0": "execution_expires_after",
      "column_1": "integer",
      "column_2": "172800",
"column_3": "Task timeout threshold, in seconds."
    },
    {
      "key": "18",
      "column_0": "usage",
      "column_1": "token_usage",
      "column_2": "",
"column_3": "Token usage for this request.",
      "children": [
        {
          "key": "18-1",
          "column_0": "completion_tokens",
          "column_1": "integer",
          "column_2": "108900",
"column_3": "Number of tokens consumed by the model for video generation, which can be used as a basis for billing reconciliation. Seedance 2.0 has a minimum token usage limit; if actual usage is below the minimum, this field returns the minimum usage."
        },
        {
          "key": "18-2",
          "column_0": "total_tokens",
          "column_1": "integer",
          "column_2": "108900",
"column_3": < div> Total number of tokens consumed by this request. The video generation model does not count input tokens, so this value equals < code> completion_tokens</ code>. </div>
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="933d45df"></span>
### Example

<span id="81d4f50c"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/contents/generations/tasks/lsd-89b8ea3232b8f1205702" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY"
```


<span id="7f671d50"></span>
#### Response example

```JSON
{
  "id": "lsd-89b8ea3232b8f1205702",
  "model": "dreamina-seedance-2-0-260128",
  "status": "succeeded",
  "content": {
    "video_url": " `https://ark-acg-cn-beijing.tos-cn-beijing.volces.com/dreamina-seedance-2-0/02178419371805600000000000000000000f****21.mp4?X-Tos-Algorithm=*****d&X-Tos-SignedHeaders=host` "
  },
  "usage": {
    "completion_tokens": 648900,
    "total_tokens": 648900
  },
  "created_at": 1784193717,
  "updated_at": 1784194096,
  "seed": 84841,
  "resolution": "720p",
  "ratio": "16:9",
  "duration": 15,
  "framespersecond": 24,
  "service_tier": "default",
  "execution_expires_after": 172800,
  "generate_audio": true,
  "draft": false,
  "priority": 0
}
```


<span id="e96f86c0"></span>
### Error code


|HttpCode |Error code |Error message |Note |
|---|---|---|---|
|401 |ApiKey.Invalid |The api key is invalid. |API is invalid |
