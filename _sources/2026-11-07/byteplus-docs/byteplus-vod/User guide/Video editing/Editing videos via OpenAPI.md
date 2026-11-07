---
title: "Editing videos via OpenAPI"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/editing_videos_via_openapi"
---

To perform powerful, cloud\-based video editing via OpenAPI, you will use the `EditParam` JSON object. This reference guide details all the core parameters for building the `EditParam` structure, enabling you to programmatically control the canvas, timeline, materials, special effects, and animations for your video projects.

<span id="e315faf3"></span>
## How to use

Call the [SubmitDirectEditTaskAsync](https://docs.byteplus.com/en/docs/byteplus-vod/reference-submitdirectedittaskasync) API, passing the complete `EditParam` object directly in the request body to start an asynchronous editing task.

<span id="01144e7c"></span>
## Core concepts

Before building `EditParam`, you need to understand the following core concepts:


* **Canvas**: The workspace for the final output video. It defines video width, height, and background color. All visual elements are ultimately rendered onto this canvas.

* **Track**: It organizes and layers different materials. The `EditParam` contains a two\-dimensional array of `Track`, representing multiple tracks.

   * **Render order**: It correlates with the track index. Tracks with a larger index number will be rendered higher (for example, `Track[1]` appears above `Track[0]`).

   * **Timeline layout**: Multiple `Elements` on the same track can be arranged sequentially in time but should not overlap.

* **Element**: A specific content unit placed on a track, such as a video clip, an image, a piece of text, or a special effect. Each element has its own `Type` and occupies a specific time segment `TargetTime` on the track.

* **Filter**: Special effects attached to elements for modifying their visual or audio appearance, such as cropping, distortion, color grading, or speed adjustment. Filters are defined in the `Extra` array of the element.


<span id="d27ed0fb"></span>
## Parameters

<span id="95bd6607"></span>
### EditParam structure overview

The `EditParam` object primarily consists of the following top\-level properties:


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Upload |Object of [UploadInfo](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#1b37d1b9) |Yes |`-` |Upload configuration. It defines the video name and the space where the final video file will be stored. |
|Output |Object of [Output](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#e47d48bd) |No |`-` |Output configuration. It defines the codec, bitrate, frame rate, cover, and other parameters for the final video. |
|Canvas |Object of [Canvas](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#d78cadba) |No |`-` |Canvas configuration. It defines the final video resolution, background color, and more. |
|ExtraParam |Object of [ExtraParam](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#74a0cf6a) |No |`-` |Additional parameters. It injects AIGC metadata and other information. |
|Track |Array of [Track](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#91a754d5) |Yes |`-` |Track list. It defines all content and layout on the timeline. |


<span id="1b37d1b9"></span>
### UploadInfo


|Parameter |Category |Required |Sample value |Description |
|---|---|---|---|---|
|SpaceName |String |Yes |`edit` |Upload space. The output file will be stored in this space. |
|VideoName |String |No |`video_edit` |The name of the task product in VOD space. It must comply with the regex: `^[\p{Han}.()（）\w\s:-]+$`. The maximum size is 2048 bytes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is not set, the output name in the VOD space will be empty.</div><br> |
|FileName |String |No |`Project/VideoFiles/123.mp4` |The file path for the task product. If not provided, the `FileName` parameter in the callback will be empty. |


<span id="e47d48bd"></span>
### Output


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Alpha |Boolean |No |`false` |Whether the output video should include an alpha channel. The default value is `false`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Alpha</code> takes precedence over <code>VideoCodec</code>. When <code>Alpha</code> is set to <code>true</code>, <code>VideoCodec</code> will default to <code>VP9</code> and any other specified <code>VideoCodec</code> will be ignored.</div><br> |
|Format |String |No |`mp4` |The container format of the output file. Valid values as follows:<br><br><br>* `mp4`(default)<br><br>* `hls`<br><br>* `mp3`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>Format</code> takes precedence over <code>VideoCodec</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>Format</code> is set to <code>hls</code>, the video is output in HLS format. At this time, <code>VideoCodec</code> only supports <code>h264</code> and <code>h265</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DisableVideo</code> is set to <code>true</code>, the <code>Format</code> only supports<code>mp3</code>, representing the dedicated MP3 audio export format.</div><br> |
|Fps |Float |No |`30` |The frame rate of the output video in fps (frames per second). The default value is 30. |
|Codec |JSON |No |`-` |Audio and video encoding parameters. For details, see [Codec](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#6275d674). |
|DisableVideo |Boolean |No |`false` |Output audio only:<br><br><br>* `false`: (default) Output audio and video.<br><br>* `true`: Audio only.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If both <code>DisableVideo</code> and <code>DisableAudio</code> are set to <code>false</code>, a complete audio and video file is produced.</div><br> |
|DisableAudio |Boolean |No |`false` |Output video only:<br><br><br>* `false`: (default) Output audio and video.<br><br>* `true`: Video only. |
|Cover |JSON |No |`-` |Frame extraction and cover extraction settings. For details, see [Cover](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#f1dfa404). |
|CanvasWithMax |Boolean |No |`false` |Whether the canvas resolution follows the maximum resolution. Default value is `false`. If set to `true`, the canvas resolution matches the maximum resolution in the resources.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Maximum resolution refers to the largest value of width \* height among all resources.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Canvas resolution priority (decreasing order):</div><br><br><br>   1. <div data-tips="true" data-tips-type="tip">Integer type <code>Canvas.Width</code> and <code>Canvas.Height</code></div><br><br><br>   2. <div data-tips="true" data-tips-type="tip"><code>CanvasWithMax</code></div><br><br><br>   3. <div data-tips="true" data-tips-type="tip"><code>CanvasWithRatio</code></div><br><br><br>   4. <div data-tips="true" data-tips-type="tip">String type <code>Canvas.Width</code> and <code>Canvas.Height</code></div><br> |
|CanvasWithRatio |Boolean |No |`false` |Whether the canvas resolution follows a fixed aspect ratio ( long side to short side). Default value is`false`. If set to `true`, the ratio defaults to 16:9. You can customize it by using the `Long`, `Short`, and `Ratio` parameters within the `Canvas` structure. |
|AudioPhaseDetect |Boolean |No |`false` |Whether to perform audio phase detection (for phase inversion). The default is `false` (disabled). This operation can be time\-consuming for long source footage. |


<span id="6275d674"></span>
#### Codec


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|VideoCodec |String |No |`h264` |Video codec type. Valid values as follows:<br><br><br>* `h264`: (default) H.264<br><br>* `vp9`: VP9<br><br>* `h265`: H.265 |
|Preset |String |No |`Medium` |It adjusts video encoding speed and quality. The default value is `Medium`. Effective only when `VideoCodec` is set to `h264` or `h265`. |
|Crf |Integer |No |`23` |Constant Rate Factor (CRF). The default value is `23`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Effective only when <code>VideoCodec</code> is set to <code>h264</code> or <code>h265</code>.</div><br> |
|VideoBitRate |Integer |No | |Video encoding bitrate in bps. If this parameter is not set, the bitrate is controlled by `Crf`. If set, `Crf` will be disabled. |
|AudioCodec |String |No |`aac` |Audio encoding format. The default value is `aac`. Only supports `aac`. |
|AudioBitrate |Integer |No |`128` |Audio encoding bitrate in kbps. The default value is 128. |


<span id="f1dfa404"></span>
#### Cover


|Parameter |Data Type |Required |Sample value |Description |
|---|---|---|---|---|
|DisableCover |Boolean |No |`false` |Whether to disable cover frame extraction:<br><br><br>* `false`: (default) Save cover.<br><br>* `true`: Disable cover. |
|CoverTime |Array of Integer |No |`100` |Frame extraction time point (in milliseconds). The video editing service will capture a video frame at the specified time point and save it as an image file. |
|Format |String |No |`png` |Cover output format. Valid values as follows:<br><br><br>* `jpeg`: JPEG format.<br><br>* `png`: (default) PNG format. |


<span id="d78cadba"></span>
### Canvas


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Width |Integer ｜ String |No |`720` |The width of the output video in pixels. The default value is 720. Valid range: [160, 8192].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Canvas</code> also supports using expressions to automatically match the width and height of an Element. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#4e465fb4">Example 4: Specify canvas width and height with expressions</a>.</div><br> |
|Height |Integer ｜ String |No |`1280` |The height of the output video in pixels. The default value is 1280. Valid range: [160, 8192]. |
|BackgroundColor |String |No |`#FF0000FF` |The Canvas color in RGBA format. The default value is `#00000000`. |
|Long |Integer |No |`1280` |The long side of the output video canvas in pixels. The default value is 1280. Valid range: [160, 8192].<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Effective only when <code>CanvasWithRatio</code> is <code>true</code>.</div><br> |
|Short |Integer |No |`720` |The short side of the output video canvas in pixel. The default value is 720. Valid range: [160, 8192].<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Effective only when <code>CanvasWithRatio</code> is <code>true</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When both short side and long side are set, short side takes precedence over long side.</div><br> |
|Index |String |No |`0\|0` |It sets the screen orientation (landscape or portrait) for the output video canvas to match a selected resource. The default value is `0\|0`, which aligns with the 0th Element of the 0th Track. If `Index` is set to `MAX`, it matches the reference resolution, which means it aligns with the maximum resolution in the resource.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Effective only when <code>CanvasWithRatio</code> is <code>true</code>.</div><br> |
|Ratio |String |No |`16:9` |It sets the aspect ratio of the video canvas’s long side to short side. The default value is `16:9`. When `Ratio` is set to `-1:-1` or `-1`, the aspect ratio will follow the selected input source.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Effective only when <code>CanvasWithRatio</code> is <code>true</code>.</div><br> |


<span id="74a0cf6a"></span>
### ExtraParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Upload |Object |No |`-` |Upload additional parameters. You can write [Metadata for AI-generated content](https://docs.byteplus.com/docs/byteplus-vod/metadata_for_ai-generated_content) through this parameter. An example is shown below:<br><br>```JSON```<br>```{```<br>```  "ExtraParam": {```<br>```    "Upload": {```<br>```      "AigcMeta": "{\"Label\":\"1\",\"ContentProducer\":\"ByteplusVODAIGCvideogeneratedservice\",\"ProduceID\":\"aigc-prod-uuid-20240521-001\"}"```<br>```    }```<br>```  }```<br>```}```<br> |


<span id="91a754d5"></span>
## Track

The `Track` parameter is the core of `EditParam` and defines the video timeline. It functions like multi\-layer tracks in professional editing software, organizing all visual and audio content by time and space. `Track` is a **two\-dimensional array** in the format `Track[track index][element index]`.


* The first dimension (outer array) represents the track list. The array index `[track index]` determines the rendering hierarchy of the track.

* The second dimension (inner array) represents a single track containing one or more Elements arranged on that track.


```JSON
"Track": [
  // --- Track 0 (Track[0]) ---
  [ 
    { "Type": "video", "TargetTime": [0, 5000], ... }, // Element 0 (Track[0][0])
    { "Type": "video", "TargetTime": [5000, 10000], ... } // Element 1 (Track[0][1])
  ], 

  // --- Track 1 (Track[1]) ---
  [ 
    { "Type": "text", "TargetTime": [1000, 4000], ... } // Element 0 (Track[1][0])
  ]
]
```


<span id="1238ba1e"></span>
### Track rendering hierarchy

In the `Track` array, **the larger the index, the higher the track’s hierarchy**. During video composition, visual content on higher tracks will overlap content on lower tracks.


* `Track[0]`: The bottom layer, typically used for background or main video.

* `Track[1]`: Above `Track[0]`, and so on.


<span id="921ac352"></span>
### Track composition overview

Each track consists of one or more **Elements**. Elements are the basic content units in a video. Each element is a JSON object that defines what content appears at what time. Additionally, you can add multiple `filter` resources via the `Extra` field in each Element resource. An element object consists of **general parameters** and **type\-specific parameters**. The following are general structures and parameters supported by most `Element` types:

```JSON
{
  "Type": "video", // Element type (what it is)
  "Source": "vid://...", // Source of materials (What is used)
  "TargetTime": [ 0, 5000 ], // Time on track (When it appears and ends)
  "Extra": [ /* ... Additional effects ... */ ]  // Additional effects (How it is presented)
}
```



|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`audio` |Resource type. It determines the nature of the resource and available parameters. The following types are supported:<br><br><br>* Core media:<br><br>   * `audio`:audio<br><br>   * `video`: video<br><br>   * `image`: image<br><br>* Overlay content:<br><br>   * `effect`: special effect<br><br>* Special effect:<br><br>   * `gaussian`: gaussian blur |
|TargetTime |Array of Integer |Yes |[1000,2000] |The time range the element occupies on the track, specified as `[start time, end time]` in milliseconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The meaning of <code>TargetTime</code> varies across different data structures:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When in the track, <code>TargetTime</code> refers to the resource's time point in the track.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In the <code>Extra</code>, the <code>TargetTime</code> is relative to the main resource's time point.</div><br> |
|Source |String |Required condition |`-` |Resource source. It specifies the resources required for this element or effect. Its specific meaning and format depend on the context:<br><br><br>* For media elements (such as `video` and `image`): the value is the URI of the media asset, for example, `vid://...`. In this case, this parameter is required.<br><br>* For effect\-type filters (such as `lut_filter`): the value is the resource ID of the effect, for example `1183993`. |
|Extra |Array of JSON |No |`-` |Additional list. It adds effects such as filters, distortion, cropping, and animation. Each effect is an independent JSON object called a Filter. For more details, see [Filter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#6f077f9c). |


Example: A simple timeline with a background video and picture\-in\-picture (PiP)

```JSON
"Track": [
  // --- Track 0: Background video ---
  [
    {
      "Type": "video",
      "Source": "vid://background_video_vid",
      "TargetTime": [0, 10000] // You can access this element via Track[0][0]
    }
  ],
  // --- Track 1: Picture-in-picture (PiP) video ---
  [
    {
      "Type": "video",
      "Source": "vid://pip_video_vid",
      "TargetTime": [2000, 7000], // You can access this element via Track[1][0]
      "Extra": [
        {
          "Type": "transform",
          "Width": 320,
          "Height": 180,
          "PosX": 50,
          "PosY": 50
        }
      ]
    }
  ]
]
```


<span id="8db1d36a"></span>
### Track layout overview

You can place Elements on different tracks based on their properties to achieve complex visual overlays and audio mixing.


* Visual track: It includes elements with visual components such as `video`, `image`, `effect`, and more. During composition, the rendering follows the rule where upper layers cover lower layers. Common layout practices include:

   * Track 0 (bottom layer): It places the main video segment or background image.

   * Track 1 (top layer): It places picture\-in\-picture video, stickers, or dynamic effects.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Elements of <code>video</code> and <code>image</code> types can be placed on the same track.   </div>
   

* Audio track: It includes `audio` elements and audio tracks from `video` elements, following mixing rules rather than overlay. You can create one or more dedicated tracks for placing only `audio`, for example,

   * One track is used for background music throughout.

   * Another track is used for narration or sound effects for specific time periods.


<span id="a1e6b88d"></span>
### Track parameters

The following sections describe the proprietary parameters supported by different types of Elements.

<span id="7bd3d2e4"></span>
#### Audio

The table below introduces the parameters for audio resources.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`audio` |Resource type. For audio resources, the value is `audio`. |
|TargetTime |Array of Integer |Yes |`[1000,2000]` |The resource's time range on the track. Unit in milliseconds. Format: `[start, end]`. |
|Extra |Array of JSON |No |`-` |Extended resources. |
|Source |String |Yes |`vid://v02b6d970000bvg5pi*******` |Resource download address. The following types are supported:<br><br><br>* VOD Vid: If you have uploaded resources to BytePlus VOD and are using Vid mode, you can specify the resource's Vid using the `vid://${vid}` format. For example, `vid://v02b6d970000bvg5pi6******`<br><br>* VOD DirectUrl: If you have uploaded resources to BytePlus VOD and are using DirectUrl mode, you can specify the resource's FileName using the `directurl://{fileName}` format. For example, `directurl://test.mp3`<br><br>* Mounting TOS: If you have [added a TOS bucket](https://docs.byteplus.com/en/docs/byteplus-vod/process-media-files-stored-in-tos-buckets) in the VOD console, you can specify the resource address using the `tos://{bucketName}/{fileName}` format. For example, `tos://example/test.mp3` |


<span id="9aa4383d"></span>
#### Video

The table below introduces the parameters for video resources.


|Parameter |Data Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |Yes |`video` |Resource type. For video resources, the value is `video`. |
|TargetTime |Array of Integer |Yes |`[1000,2000]` |The resource's time range on the track. Unit in milliseconds. Format: `[start, end]` |
|Extra |Array of JSON |No |`-` |Extended resource. You can use the `Extra` field to pass `TransformFilter` configuration resources for layout on the output video canvas. If you do not provide `TransformFilter`, the element will be scaled to fill the canvas. |
|Source |String |Yes |`vid://v02b6d970000bvg5pi*******` |Resource download address. The following types are supported:<br><br><br>* VOD Vid: If you have uploaded resources to BytePlus VOD and are using Vid mode, you can specify the resource's Vid using the `vid://${vid}` format. For example, `vid://v02b6d970000bvg5pi6******`<br><br>* VOD DirectUrl: If you have uploaded resources to BytePlus VOD and use DirectUrl mode, you can specify the FileName using `directurl://{fileName}` format. For example, `directurl://test.mp3`<br><br>* Mounting TOS: If you have [added a TOS bucket](https://docs.byteplus.com/en/docs/byteplus-vod/process-media-files-stored-in-tos-buckets) in the VOD console, you can specify the resource's address using `tos://{bucketName}/{fileName}` format. For example, `tos://example/test.mp3` |


<span id="7efb2c72"></span>
#### Image

The table below introduces the parameters for image resources.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`image` |Resource type. For image resources, the value is `image`. |
|TargetTime |Array of Integer |Yes |`[1000,2000]` |The resource's time range on the track. Unit in milliseconds. The format is `[start, end]`. |
|Extra |Array of JSON |No |`-` |Extended resources. You can use the `Extra` field to pass `TransformFilter` configuration resources for layout on the output video canvas. If `TransformFilter` is not provided, the system will use `Canvas` for filling. |
|Source |String |Yes |`tos://example/test.png` |Resource download address. The following types are supported:<br><br><br>* VOD Mid: If you have uploaded image resources to VOD using the Mid mode, you can specify the resource’s Mid in the `mid://${mid}` format. For example, `mid://v02b6d970000bvg5pi6******`<br><br>* VOD DirectUrl: If you have uploaded image resources to VOD using the DirectUrl mode, you can specify the resource’s FileName in the `directurl://{fileName}` format. For example, `directurl://test.png`<br><br>* Mounting TOS: If you have [added a TOS bucket](https://docs.byteplus.com/en/docs/byteplus-vod/process-media-files-stored-in-tos-buckets) in the VOD console, you can specify the resource address using the `tos://{bucketName}/{fileName}` format. For example, `tos://example/test.png` |


<span id="text-element"></span>
#### Text/Subtitle

The table below introduces the parameters for text and subtitle resources.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`text` |Resource type. Set this parameter to `text` for text resources or `subtitle` for subtitle resources. |
|TargetTime |Array of Integer |Yes |`[1000,2000]` |The resource's time range on the track, in milliseconds. Format: `[start, end]`. |
|Extra |Array of JSON |Yes |`-` |Extended resources. You must pass a `TransformFilter` in `Extra` to configure the resource's layout on the output video canvas. Other filters are optional. |
|Text |String |Yes |`Example text` |Text content. |
|TextRes |String |No |`1109372` |[Stylized text ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#stylized-text-id). |
|FontType |String |No |`1109412` |[Font ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#font-id). |
|FontSize |Integer |No |`200` |Font size in pixels. When the default font is used, the default font size is `200`. |
|FontColor |String |No |`#FF0000FF` |Font color in RGBA format. The default color is white when stylized text is not used.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter applies only to basic text and does not take effect when stylized text is used.</div><br> |
|BackgroundColor |String |No |`#FF0000FF` |Text background color in RGBA format. The default value is `#00000000`. For multiple lines of text, the background width follows the longest line. This parameter applies only to basic text. |
|BackgroundBorderSize |Float |No |`0` |Text background border size. The default value is `0`, which makes the background follow the text. |
|BorderColor |String |No |`#FF0000FF` |Text outline color in RGBA format. The default value is `#00000000`. This parameter applies only to basic text. |
|BorderWidth |Integer |No |`1` |Text outline width. The minimum value is 1, and the maximum value is 10% of `FontSize`. |
|LineMaxWidth |Float |No |`-1` |Automatic line\-wrapping width. Set this parameter to `-1` (default) to disable automatic line wrapping, or to a value between 0 and 1 to specify the width ratio. When `Typesetting` is `0`, the ratio is based on `TransformFilter.Width`; when `Typesetting` is `1`, it is based on `TransformFilter.Height`. |
|Typesetting |Integer |No |`0` |Text direction: `0` (default) for horizontal text or `1` for vertical text. |
|AlignType |Integer |No |`0` |Text alignment used with `Typesetting`. For horizontal text, valid values are `0` (left), `1` (center), and `2` (right). For vertical text, valid values are `1` (center), `3` (top), and `4` (bottom). |


<span id="222bb756"></span>
#### Effect

The table below introduces the parameters for special effect resources.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`effect` |Resource type. For special effect resources, the value is `effect`. |
|TargetTime |Array of Integer |Yes |`[1000,2000]` |The resource's time range on the track. Unit in milliseconds. Format: `[start, end]`. |
|Extra |Array of JSON |No |`-` |Extended resources. It supports adding `LutFilter` or `EffectFilter` special effect types, but only one type can be added. |


<span id="82aa04da"></span>
#### **Gaussian**

The table below introduces the parameters for Gaussian blur resources. See the following for usage examples:


* [Example 5: Add Gaussian blur background](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#bbb8239e)

* [Example 6: Apply Gaussian blur to Element](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#96c7344a)



|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`gaussian` |Resource type. For Gaussian blur resources, the value is `gaussian`. |
|TargetTime |List |Yes |`[1000,2000]` |The resource's time range on the track. Unit in milliseconds. The format is `[start, end]`. |
|Extra |List |Yes |`-` |Extended resources. You must provide `TransformFilter` and `GaussianFilter`. |
|Source |String |Yes |`vid://v02b6d970000bvg5pi6******` |Resource download address. Supported types:<br><br><br>* Video on Demand (VOD) Vid: If you have uploaded resources to BytePlus VOD and use Vid mode, specify the resource Vid in the format `vid://${vid}`. Example: `vid://v02b6d970000bvg5pi6******`<br><br>* Video on Demand (VOD) DirectUrl: If you have uploaded resources to BytePlus VOD and use DirectUrl mode, specify the resource FileName in the format `directurl://{fileName}`. Example: `directurl://test.mp3`<br><br>* Mount TOS: If you have [added a TOS bucket](https://docs.byteplus.com/en/docs/byteplus-vod/process-media-files-stored-in-tos-buckets) in the VOD console, specify the resource address in the format `tos://{bucketName}/{fileName}`. Example: `tos://example/test.mp3` |


<span id="6f077f9c"></span>
### Filter

<span id="0ff0bda5"></span>
#### Overview

Filter is a special effect attached to an Element to change its visual or audio presentation during editing. You can add filters to the `Extra` field of other types of resources, allowing multiple different effects to be layered on one element. The basic structure is as follows:

```JSON
"Extra": [
  {
    "Type": "transform", // Type of filters
    ... // Exclusive parameter for this filter
  },
  {
    "Type": "trim",      // Another filter
    ... // Exclusive parameter for this filter
  }
]
```


`Filter` can be categorized as follows based on its functionality:


|Type |Name |Description |
|---|---|---|
|Time and cropping |[TrimFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#8c91573b) |**Time selection** means extracting a time segment from the original media. |
||[CropFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#ad114413) |**Frame cropping** means cutting out a rectangular area from a video or image. |
||[SpeedFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#fb413c9b) |**Playback speed** adjusts the playback speed of video or audio. |
|Transform and layout |[TransformFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#5b0f280f) |**2D transformation** controls the position, size, rotation, and transparency of elements on the canvas. |
|Visual effects |[LutFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#1b8ef32e) |**Color filters** apply preset color effects to the frame. |
||[EffectFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#5dcb3014) |**Visual special effects** add split\-screen, mirroring, and other visual effects to the frame. |
||[EqFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#f1949fe0) |**Make image adjustments** by modifying brightness, contrast, saturation, and other settings. |
||[DelogoFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#f51b0acf) |**Blur specific areas** to apply a blur effect to designated regions of the image, often used to cover marks. |
||[GaussianFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#58467829) |**Gaussian blur** applies a blur effect to the entire element or background. |
|Animation and transitions |[TransitionFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#154e975c) |**Transition** creates a seamless effect between two adjacent video elements on the same track. |
||[VideoAnimationsFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#1732888c) |**Video animation** adds entrance, exit, or loop animations to videos or images. |
||[TextAnimationsFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#text-animations-filter) |**Text animation** adds entrance, exit, or loop animations to text elements. |
|Audio processing |[AudioFadeFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#6a32b7bd) |**Audio fade in/out** adds fade\-in and fade\-out effects to audio tracks. |
||[AudioVolumeFilter](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#8b3655fd) |**Adjust volume** to change the loudness of the audio. |


<span id="1b8ef32e"></span>
#### LutFilter

LutFilter can be added to the `Extra` field of video, image, or effect resources to apply filters. The table below introduces the parameters of LutFilter.


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `lut_filter`. |
|TargetTime |Array of Integer |Yes |Filter duration within a single element. The unit is milliseconds. The format is `[start, end]`. If the element's `TargetTime` is set to `[50000, 60000]` and the filter's `TargetTime` is set to `[5000, 6000]`, then the filter effect will be added to the element in the generated clip at `[55000, 56000]`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is not valid in Effect Element.</div><br> |
|Source |String |Yes |[Filters ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#67aba7c7). |
|Intensity |Float |No |Filter intensity. The default value is 1. The valid range is [0, 1]. |


<span id="5dcb3014"></span>
#### EffectFilter

EffectFilter can be added to the `Extra` field of video, image, or effect resources to apply special effects. The table below introduces the parameters of EffectFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `effect_filter`. |
|TargetTime |Array of Integer |Yes |The time range of the filter within a single Element. The unit is milliseconds. The format is `[start, end]`. If the `TargetTime` of the Element is set to `[50000, 60000]` and the filter's `TargetTime` is set to `[5000, 6000]`, then the filter effect will be added to the Element in the output clip at `[55000, 56000]`<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is not valid in Effect Element.</div><br> |
|Source |String |Yes |[Special effect ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#e2b43c22). |


<span id="154e975c"></span>
#### TransitionFilter

The TransitionFilter can be added to the `Extra` field of video resources to apply transition effects. For transitions between adjacent videos A and B on the same track, add TransitionFilter only to video A. The table below describes the parameters of TransitionFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `transition`. |
|Source |String |Yes |[Transition ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#633b02c0). |
|Duration |Integer |Yes |Transition duration in milliseconds. |


<span id="5b0f280f"></span>
#### TransformFilter

TransformFilter can be added to the `Extra` field of video, image, and text resources to configure their layout on the output video canvas. If both CropFilter and TransformFilter are added to the same Element, CropFilter will be applied first. The table below describes the parameters of TransformFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `transform`. |
|PosX |Integer |Yes |The offset of the resource's top\-left corner from the output video canvas's top\-left corner along the X axis, measured in pixels. |
|PosY |Integer |Yes |The offset of the resource's top\-left corner from the output video canvas's top\-left corner along the Y axis, measured in pixels. |
|Width |Integer |Yes |The width of the resource on the output video canvas, measured in pixels. |
|Height |Integer |Yes |The height of the resource on the output video canvas, measured in pixels. |
|Rotation |Integer |No |Rotation angle in degrees, from \-360 to 360. Positive values indicate clockwise rotation. |
|FlipX |Boolean |No |Flip horizontally. |
|FlipY |Boolean |No |Flip vertically. |
|Alpha |Float |No |Transparency. Range: [0,1]. 0 means transparent. |


<span id="ad114413"></span>
#### CropFilter

CropFilter can be added to the `Extra` field of video and image resources to crop videos. The table below describes the parameters of CropFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `crop`. |
|PosX |Integer |Yes |The offset of the top left corner of the crop area relative to the top left corner of the original image on the X axis, measured in pixels. |
|PosY |Integer |Yes |The offset of the top\-left corner of the cropped area along the Y axis from the top\-left corner of the original image, measured in pixels. |
|Width |Integer |Yes |The width of the cropped area in pixels. |
|Height |Integer |Yes |The height of the cropped area in pixels. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_248019aea7c2fbb7ccb094497c93765d.jpg) </span>

As shown in the illustration above, suppose you want to crop an orange area of size a\*b from the original image. Then you need to set:


* Set `PosX` to b1

* Set `PosY` to a1

* Set `width` to (b2\-b1)

* Set `height` to (a2\-a1)


<span id="8c91573b"></span>
#### TrimFilter

TrimFilter can be added to the `Extra` field of video or audio resources to extract segments of audio or video. The following table describes the parameters for TrimFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value must be `trim`. |
|StartTime |Integer |Yes |Trim start time in milliseconds. |
|EndTime |Integer |Yes |Trim end time in milliseconds.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you extract an audio segment or if the video segment contains audio, the extracted length must be greater than 0.1 seconds. Otherwise, extraction will not occur, and the entire resource will be added to the output.</div><br> |


<span id="1732888c"></span>
#### VideoAnimationsFilter

VideoAnimationsFilter can be added to the `Extra` field of video or image assets to apply video animations. The following table describes the parameters of VideoAnimationsFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `video_animation`. |
|AnimRes |String |Yes |[Video animation ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#425324e2). |
|AnimStartTime |Integer |Yes |Animation start time. Unit in milliseconds. |
|AnimEndTime |Integer |Yes |Animation end time. Unit in milliseconds. |
|AnimLoop |Boolean |No |Whether the animation loops. The default value is false. |
|AnimLoopDuration |Integer |No |Loop animation duration. The default value is 0. This parameter is required for loop animations. |


<span id="text-animations-filter"></span>
#### TextAnimationsFilter

TextAnimationsFilter can be added to the `Extra` field of text resources to apply text animations. The following table describes its parameters.


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `text_animation`. |
|AnimInRes |String |No |[Entrance animation ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#text-in). `AnimInRes` and `AnimInDuration` must be set together. |
|AnimInDuration |Integer |No |Entrance animation duration in milliseconds. |
|AnimOutRes |String |No |[Exit animation ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#text-out). `AnimOutRes` and `AnimOutDuration` must be set together. |
|AnimOutDuration |Integer |No |Exit animation duration in milliseconds. |
|AnimLoopRes |String |No |[Loop animation ID](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#text-loop). `AnimLoopRes` and `AnimLoopDuration` must be set together. |
|AnimLoopDuration |Integer |No |Loop animation duration in milliseconds. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">The sum of <code>AnimInDuration</code> and <code>AnimOutDuration</code> must be shorter than the text display duration specified by <code>TargetTime</code>.</div>


<span id="f1949fe0"></span>
#### EqFilter

EqFilter can be added to the `Extra` field of video or image resources for picture equalization. The following table describes the parameters of EqFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `equalizer`. |
|TargetTime |Array of Integer |Yes |The filter time within a single element. The unit is milliseconds. The format is `[start, end]`. If the element's `TargetTime` is set to `[50000, 60000]` and the filter's `TargetTime` is set to `[5000, 6000]`, then the filter effect will be added to the element within `[55000, 56000]` in the output.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is not valid in Effect Element.</div><br> |
|Brightness |Float |No |Brightness. The value range is [0,1]. |
|Saturation |Float |No |Saturation. The value range is [0,1]. |
|Tone |Float |No |Tone. The value range is [0,1]. |


<span id="6a32b7bd"></span>
#### AudioFadeFilter

AudioFadeFilter can be added to the `Extra` field of audio or video resources to fade audio in and out. The following table describes the parameters of AudioFadeFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `a_fade`. |
|FadeIn |Integer |No |Fade\-in duration in milliseconds. If set to 2000, the audio will fade in over the first 2 seconds. |
|FadeOut |Integer |No |Fade\-out duration in milliseconds. If set to 2000, the audio will fade out over the last 2 seconds. |


<span id="8b3655fd"></span>
#### AudioVolumeFilter

AudioVolumeFilter can be added to the `Extra` field of audio or video resources to adjust audio volume. The following table describes the parameters for AudioVolumeFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `a_volume`. |
|Volume |Float |No |Volume. `0` means mute, and the default volume is `1`. |


<span id="fb413c9b"></span>
#### SpeedFilter

SpeedFilter can be added to the `Extra` field of audio or video resources to change the playback speed. If both TrimFilter and SpeedFilter are added to the same Element, TrimFilter will be applied first. The following table describes the parameters for SpeedFilter.


|Parameter |Category |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `speed`. |
|Speed |Float |No |Playback speed. The default value is `1`, which keeps the original speed. A value below 1 slows down playback; above 1 speeds it up. The valid range is [0.1, 4]. Values above 4 or below 0.1 are automatically set to 0.1. |


<span id="f51b0acf"></span>
#### DelogoFilter

DelogoFilter can be added to the `Extra` field of video or image resources to apply partial blurring. Multiple `DelogoFilter` instances are supported for applying Gaussian blur to different areas. In the same Element, CropFilter is applied first, followed by DelogoFilter, then TransformFilter. The table below introduces the parameters of DelogoFilter.


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The value is `delogo`. |
|TargetTime |List |Yes |The Filter's duration within a single Element. Unit in milliseconds. Format: `[start, end]`. If the `TargetTime` of an Element is set to `[50000, 60000]`, and the `TargetTime` of the Filter is set to `[5000, 6000]`, the Filter effect will be applied to the Element at `[55000, 56000]` in the output clip.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is not valid in Effect Element.</div><br> |
|DelogoType |String |No |Type of watermark removal. Currently, only `gaussian` is supported, which applies local Gaussian blur. |
|PosX |Int |Yes |The offset on the X axis in pixels, from the top left corner of the local blur area to the top left corner of the original image. |
|PosY |Int |Yes |The offset on the Y axis in pixels, from the top left corner of the local blur area to the top left corner of the original image. |
|Width |Int |Yes |The width of the local blur area in pixels. |
|Height |Int |Yes |The height of the local blur area in pixels. |
|Sigma |Int |No |The intensity of local blur. The default value is `0`, meaning no effect. The recommended range is [10, 70]. The larger the value, the stronger the local blur effect. |
|Radius |Int |No |The radius of local blur. The default value is `0`, meaning no effect. The recommended range is [10, 70]. The larger the value, the stronger the local blur effect, but the performance will decrease. It is generally recommended to set `Radius` and `Sigma` to the same value. |


<span id="58467829"></span>
#### **GaussianFilter**

GaussianFilter can be added to the `Extra` field of video, image, or Gaussian resources to produce different effects:


* When GaussianFilter is added to video or image resources, it creates a Gaussian blur effect on the background. If the `Canvas` resolution does not match the `Source` resolution, the system will perform uniform scaling and center cropping.

* When GaussianFilter is added to a Gaussian resource, it applies a Gaussian blur to the corresponding resource.


The table below introduces the parameters of GaussianFilter.


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Type |String |Yes |Resource type. The default value is `gaussian`. |
|TargetTime |List |Yes |The Filter's time in a single Element. The unit is milliseconds. The format is `[start, end]`. If the `TargetTime` of the Element is set to `[50000, 60000]` and the `TargetTime` of the Filter is set to `[5000, 6000]`, the Filter effect will be added to this Element in the clipping result at `[55000, 56000]`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is not valid in Effect Element.</div><br> |
|Radius |int |Yes |The radius of Gaussian blur. The default value is `0`, meaning no effect. The recommended range is [10, 70]. The higher the value, the stronger the Gaussian blur effect. |
|Sigma |int |Yes |The intensity of Gaussian blur. The default value is `0`, meaning no effect. The recommended range is [10, 70]. The higher the value, the stronger the Gaussian blur effect, but the lower the performance. It is generally recommended to set `Radius` and `Sigma` to the same value. |


<span id="ed950bde"></span>
## Common usage examples

This section provides several common editing scenarios and their corresponding `EditParam` configuration examples. You can directly reuse or modify these examples to quickly meet your business needs.

<span id="c1f69d3c"></span>
### Example 1: Concatenating multiple video segments in sequence


* **Overview**: Merge several separate video clips in chronological order to create one completely long video. This is the most basic editing operation.

* **Key steps**:

   * Place all video elements (`Type: "video"`) on **the same track** (`Track[0]`).

   * To ensure a seamless transition, the start time of each element must match the end time of the preceding element.


```JSON
{
  "Canvas": {
    "Width": 1280,
    "Height": 720
  },
  "Track": [
    [
      // --- Segment 1: On the timeline from 0s to 5s ---
      {
        "Source": "vid://your_vid_1",
        "Type": "video",
        "TargetTime": [ 0, 5000 ]
      },
      // --- Segment 2: On the timeline from 5s to 10s ---
      {
        "Source": "vid://your_vid_2",
        "Type": "video",
        "TargetTime": [ 5000, 10000 ]
      },
      // --- Segment 3: On the timeline from 10s to 13s ---
      {
        "Source": "vid://your_vid_3",
        "Type": "video",
        "TargetTime": [ 10000, 13000 ]
      }
    ]
  ],
  "Upload": {
    "SpaceName": "your_edit_space",
    "VideoName": "example 1"
  }
}
```


<span id="4dfc6ba3"></span>
### Example 2: Extracting and merging multiple video segments


* **Overview**: Select multiple highlight clips from a long video and merge them into a highlight reel.

* **Key steps**:

   * Create multiple `video` elements for the **same source video** on the same track.

   * Each element uses TrimFilter to specify the original time segment to extract from the source video.

   * The `TargetTime` of each element defines the new position of that extracted segment on the final video timeline.


```JSON
{
  "Canvas": { "Width": 1280, "Height": 720 },
  "Track": [
    [
      // --- Place the [5s, 15s] segment of the source video at [0s, 10s] in the new video ---
      {
        "Source": "vid://your_long_video_vid",
        "Type": "video",
        "TargetTime": [ 0, 10000 ],
        "Extra": [
          { "Type": "trim", "StartTime": 5000, "EndTime": 15000 }
        ]
      },
      // --- Place the [25s, 35s] segment of the source video at [10s, 20s] in the new video ---
      {
        "Source": "vid://your_long_video_vid",
        "Type": "video",
        "TargetTime": [ 10000, 20000 ],
        "Extra": [
          { "Type": "trim", "StartTime": 25000, "EndTime": 35000 }
        ]
      }
    ]
  ],
  "Upload": {
    "SpaceName": "your_edit_space",
    "VideoName": "example 2"
  }
}
```


<span id="bdc10021"></span>
### Example 3: Spatial layout of multiple videos


* **Overview**: Arrange three separate videos vertically in space and merge them into a new video with higher resolution. This layout is often used for video walls, comparison displays, or creative short videos.

* **Key steps**:

   * **Set canvas size**: Create a canvas large enough to fit the total size after all videos are merged. In this example, if each source video is 1280x720, the final canvas width is 1280 and height is 720 \* 3 = 2160.

   * **Use multiple tracks**: Place each video element on an **independent track**.

   * **Precise positioning** **`TransformFilter`**: Add a `TransformFilter` for each video element to accurately calculate and set the top\-left coordinates on the canvas using `PosX` and `PosY`.

   * **Time alignment**: Keep all video elements' `TargetTime` consistent to ensure simultaneous playback.

* **Effect example**:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bad967801a474f15b68acf81bd7c8bf5~tplv-goo7wpa0wc-image.image) </span>

Request parameters are as follows:

```JSON
{
  "Canvas": {
    "Width": 1280,
    "Height": 2160 // Canvas height is three times the height of a single video (720 * 3)
  },
  "Track": [
    // --- Track 0: Top video (Video 1) ---
    [
      {
        "Source": "vid://your_vid_1",
        "Type": "video",
        "TargetTime": [ 0, 10000 ], // Assume the merge video duration is 10 seconds
        "Extra": [
          {
            "Type": "transform",
            "Width": 1280,
            "Height": 720,
            "PosX": 0,
            "PosY": 0     // The Y-coordinate is 0
          }
        ]
      }
    ],
    // --- Track 1: Center Video (Video 2) ---
    [
      {
        "Source": "vid://your_vid_2",
        "Type": "video",
        "TargetTime": [ 0, 10000 ],
        "Extra": [
          {
            "Type": "transform",
            "Width": 1280,
            "Height": 720,
            "PosX": 0,
            "PosY": 720    // The Y-coordinate is the height of the first video (720 * 1)
          }
        ]
      }
    ],
    // --- Track 2: Bottom Video (Video 3) ---
    [
      {
        "Source": "vid://your_vid_3",
        "Type": "video",
        "TargetTime": [ 0, 10000 ],
        "Extra": [
          {
            "Type": "transform",
            "Width": 1280,
            "Height": 720,
            "PosX": 0,
            "PosY": 1440   // The Y-coordinate is the sum of the heights of the first two videos (720 * 2)
          }
        ]
      }
    ]
  ],
  "Upload": {
    "SpaceName": "your_edit_space",
    "VideoName": "example 3"
  }
}
```


<span id="4e465fb4"></span>
### Example 4: Specifying canvas width and height with expressions

`Canvas` supports expressions to automatically match the width and height of an element. You can specify this using the Track index. The example code below shows that `Height` and `Width` are set to the height and width values of the `Tracks[0][0]` element, which is the first element in the first track.

```json
{
    "Height": "$0|0.h",
    "Width": "$0|0.w"
}
```


<span id="bbb8239e"></span>
### Example 5: Adding Gaussian blur background

```JSON
{
  "Canvas": {
    "Height": 720,
    "Width": 1280
  },
  "Track": [
    [
      {
        "Extra": [
          {
            "Height": 360,
            "PosX": 0,
            "PosY": 0,
            "Type": "transform",
            "Width": 640
          },
          {
            "Radius": 30,
            "Sigma": 30,
            "TargetTime": [0, 10000],
            "Type": "gaussian"
          }
        ],
        "Source": "https://example.vod.com/obj/****-cn/oi52ceh*****fvbn/test_only/test.mp4",
        "TargetTime": [0, 10000],
        "Type": "video"
      }
    ]
  ],
  "Upload": {
    "SpaceName": "edit_test",
    "VideoName": "edit_test"
  }
}
```


<span id="96c7344a"></span>
### Example 6: Applying Gaussian blur to Element

```JSON
{
  "Canvas": {
    "Height": 720,
    "Width": 1280
  },
  "Track": [
    [
      {
        "Extra": [
          {
            "Height": 360,
            "PosX": 0,
            "PosY": 0,
            "Type": "transform",
            "Width": 640
          },
          {
            "Radius": 30,
            "Sigma": 30,
            "TargetTime": [0, 10000],
            "Type": "gaussian"
          }
        ],
        "Source": "https://example.vod.com/obj/****-cn/oi52c****wbfvbn/test_only/test.mp4",
        "TargetTime": [0, 10000],
        "Type": "gaussian"
      }
    ]
  ],
  "Upload": {
    "SpaceName": "edit_test",
    "VideoName": "edit_test"
  }
}
```


<span id="d11baa80"></span>
## References

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#67aba7c7">Filters ID</a>、<a href="https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#e2b43c22">Special effect ID</a> and <a href="https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi#425324e2">Video animation ID</a> currently in public beta. If the result does not meet expectations or there are resource compatibility issues, please <a href="https://console.byteplus.com/workorder/create">create a ticket</a> to contact technical support.</div>


<span id="67aba7c7"></span>
### Filters ID


|Category |ID |Effect |
|---|---|---|
|Clear |1109360 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a941de30b9ff9dfc0cb4d9c122093c50.jpg) </span> |
|Afternoon |1109362 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ed6f8b09f8e8055cc3cd99b55005794.jpg) </span> |
|MUJI |1109364 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e4d5449dbab3429670f158c635fa9c03.jpg) </span> |
|White |1109366 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b13f8a5a5ca1add7dfe8c4fd8ff58769.jpg) </span> |
|Walnut |1109368 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_001caa525fee8f9e65f5b928d9fb209b.jpg) </span> |
|Nature |1109370 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b80d9c842e94c8fc0bd232ffcb82d3fd.jpg) </span> |
|Hong Kong |1109348 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d64d224ca8f26dc6c7dd61909e426805.jpg) </span> |
|Childhood |1109350 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bd4f6bfa097646b44f206bac64b32c3e.jpg) </span> |
|Friends |1109352 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_617e6ce4f9f70143adae9be0ad67d45d.jpg) </span> |
|Miami |1109354 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_031e7117dbc2a1050c996d35571cf559.jpg) </span> |
|Vintage |1109356 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0221f60722f5ad44aeade1f157a0541d.jpg) </span> |
|American |1109358 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c651043aa754e605132088a026a9d2d6.jpg) </span> |
|Cream |1109336 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_286938d5ab624ce7e2c77a0913cfcd50.jpg) </span> |
|FirstMeet |1109338 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc22b8b9651eabee43400fb9ca44d2c8.jpg) </span> |
|Vivid |1109340 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a33145d24f1dbb972bd0be4dab65af1.jpg) </span> |
|Dreamland |1109342 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a5be0c8a3e0f56c425e6344dc2da341.jpg) </span> |
|Jeju |1109344 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff05f7ff9ff571b5444c193bbfa57228.jpg) </span> |
|Lucidly |1109346 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3718834878df1765fbe6838e2707cdbd.jpg) </span> |
|Japanese |1109326 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d500bc825c1c8b82629825ed7e9a60dd.jpg) </span> |
|Flavorful |1109328 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eda7747b702634c8b2c3c5db64b682dd.jpg) </span> |
|Warm food |1109330 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bbcee880f6b92965cd6a07c2f59c645.jpg) </span> |
|Tasty |1109332 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_809fb4eca1e09e3b432aa18d920b3b72.jpg) </span> |
|ShinyaShokudo |1109334 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa03d7fee31f0ebec74a08c38c96ce08.jpg) </span> |
|Sakura |1109324 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e854aceaa7b8311256635ba6807d4a3.jpg) </span> |
|LemonGreen |1109322 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e4876ed293bae930851262e1ef1086a8.jpg) </span> |
|Kyoto |1109314 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_826db95ccf8b8444a2ec501c108fc1a6.jpg) </span> |
|Sunset |1109316 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7de8b3367b7dee44d1b8399a2bc5f65d.jpg) </span> |
|GreenBeauty |1109318 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb5e6783abbc557b1ec97c069131def4.jpg) </span> |
|Spring |1109320 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5bfafeaf526ee1691502b680732bf892.jpg) </span> |


<span id="633b02c0"></span>
### Transition ID

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">This transition is not available for non\-overlapping clips.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Non\-overlapping transitions</strong> occur when <code>duration</code> is set for this element and the element’s <code>endTime</code> is equal to the next element’s <code>startTime</code>.</div>




|Category |ID |Animation display |Available for non\-overlapping transitions |
|---|---|---|---|
|WipeRight |1109548 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e165f920b0a106637fe53f9212fbf67.gif) </span> |No |
|Windowblinds |1109550 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3af165690d526e17bb10f9ffc071f9e1.gif) </span> |No |
|Wind |1109552 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a43cc8f6ec4de2f88192d93970c8283e.gif) </span> |No |
|Swap |1109556 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79f31d11b46584bdb6fdcc4540ab7261.gif) </span> |Yes |
|RotateScaleFade |1109558 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dff3b939cbe6a297ead483206bb97e22.gif) </span> |Yes |
|Ripple |1109560 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14f6b3c5ffd25c8cff18dbf593f0d67f.gif) </span> |Yes |
|Pinwheel |1109562 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04f5ea1646618363d7472d3bf79e7295.gif) </span> |No |
|MultiplyBlend |1109564 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5c76ded88580ffbb7f4af00cea7a3af.gif) </span> |No |
|MaskTrans |1109566 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2f1045c1329f77aa8b686aef1626674.gif) </span> |No |
|Hexagonalize |1109568 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64c4c859c391edf8bcefceb8c70a918f.gif) </span> |Yes |
|HeartOut |1109570 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9d211d03a141f56e34c47dad5149d82.gif) </span> |No |
|GlitchDisplay |1109572 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39d8866189a04200d87ea31a21af3500.gif) </span> |Yes |
|Flyeye |1109574 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86c7979c4470b795f5cd2d461c49477d.gif) </span> |Yes |
|DreamZoom |1109576 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2135ff204297e0fd2dd8f66ae0e710d5.gif) </span> |Yes |
|Doorway |1109578 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_543983c07d3f5c248ed09033bb9db17a.gif) </span> |Yes |
|DirectionalWipe |1109580 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d00eabd75d3b484794b56a0c8a72d9ff.gif) </span> |No |
|Cube |1109584 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_649c78b8e44e7965950865a9e50c19cb.gif) </span> |Yes |
|CrossWrap |1109586 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a57e9728e19e57bb4bf1fc22927f85.gif) </span> |Yes |
|ColorPhase |1109588 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9878d7abd8dbd4c72732046966adcd40.gif) </span> |Yes |
|CircleOut |1109590 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b073709b87403073c1f0c02bace877cc.gif) </span> |No |
|CircleOpen |1109592 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_824b0da6ccd492e97fe6d4b128537758.gif) </span> |No |
|CircleCrop |1109594 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_005f1685a105c0e3b617f1f9ea36495c.gif) </span> |Yes |
|Angular |1109596 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bd7145c85e41a227a6d93d7776e301a.gif) </span> |No |


<span id="e2b43c22"></span>
### Special effect ID


|Category |ID |Animation display |
|---|---|---|
|Special_flipX |1109424 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_54f3c154f9e3cdd2ab92fbc3a6892052.jpg) </span> |
|NineDivide |1109414 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44a69f0bc25b5ec0e09947171cceb36f.jpg) </span> |
|SixDivide |1109416 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cc0795d316e08bd22ce01872240792b.jpg) </span> |
|FourDivide |1109418 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3a48a03e7090c085214202dab81fecf9.jpg) </span> |
|ThreeDivide |1109420 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5b4eb1a33c65124f0525043198801e8.jpg) </span> |
|TwoDivide |1109422 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68e0f72ffc6ba932dbbc9cc10cef069e.jpg) </span> |


<span id="425324e2"></span>
### Video animation ID

<span id="dba64039"></span>
#### Entrance animation ID


|Category |ID |Animation display |
|---|---|---|
|CircleIn |1109622 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dae02469013b0125aa142775d53f6d10.gif) </span> |
|TranslateRight |1109598 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_758606a2e74c33f5189cc76998bc7106.gif) </span> |
|TranslateLeft |1109600 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d1be342fd228eebca3f2de7bb6f34f89.gif) </span> |
|TranslateBottom |1109602 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5b75f1ce1a0faaba45badebb97d4dac3.gif) </span> |
|TranslateTop |1109604 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb487a1b02a4c96b079a92de47c55bfc.gif) </span> |
|AppearSmall |1109606 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_963a9eaf2fdb3b76b54167a62bd8bb56.gif) </span> |
|Dissolve |1109608 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_98532f40c271e368fd3f10c27c10954b.gif) </span> |
|Fade in |1109610 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11a2c1ca446008a59e309a130307fb26.gif) </span> |
|AppearLarge |1109612 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ddebf5664e05b22543e4f7ddca422e2.gif) </span> |
|BrushRight |1109614 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de8cbef6e4b2c6bf669561a006fa67b1.gif) </span> |
|BrushLeft |1109616 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a86351d43d583f6dafcb6a3f023d3d1.gif) </span> |
|BrushDown |1109618 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1ef6441dc1f38a915ac787bad14aafb.gif) </span> |
|BrushTop |1109620 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4c126446e74a4f3389bbe10cb97a04c.gif) </span> |


<span id="7ad50635"></span>
#### Exit animation ID


|Category |ID |Effect |
|---|---|---|
|CircleOut |1109624 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecf5b25c6875366c437c9548c6e145d5.gif) </span> |
|TranslateOutLeft |1109626 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb827a398f088e253ee8cd37d3d03f07.gif) </span> |
|TranslateOutRight |1109628 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8fd753a4e0b0aa42c6d2e6cdf0498d0.gif) </span> |
|TranslateOutBottom |1109630 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f017b4cd096987e09c59dfc4724ab0f4.gif) </span> |
|TranslateOutTop |1109632 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22bb5235728bbfee9c14c56d7ad78b01.gif) </span> |
|SmallOut |1109634 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_49f436b4f60f5d695b9fcd4689442cde.gif) </span> |
|DissolveOut |1180381 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fcb906ffd59cd03a7bfe893ec5ed66e4.gif) </span> |
|DissolveOut |1109636 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c4fa72a4179134e4ec34a64c66b9e9c5.gif) </span> |
|FadeOut |1109638 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/467950b0a40a4853b08f46faebef40da~tplv-goo7wpa0wc-image.image) </span> |
|BrushOutLeft |1109640 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177fd7b2df107541582552c0a8aab0e8.gif) </span> |
|BrushOutRight |1109642 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fdefdcb984d4499acc6aa512017e9ef2.gif) </span> |
|BrushOutBottom |1109644 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a687d5998ef20add7abe7b807bb4f085.gif) </span> |
|BrushOutTop |1109646 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e38ee94a98554113b3f2e63c944c3b55.gif) </span> |
|FlipLoop |1109648 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c60ca80966f0143d139a02a19d751895.gif) </span> |


<span id="text-animation-id"></span>
### Text animation ID

<span id="text-in"></span>
#### Entrance animation ID


|Category |ID |Animation display |
|---|---|---|
|Circle sweep in |4281705580 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063718-427529775369.gif) </span> |
|Dissolve in |4281705567 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063713-552008709910.gif) </span> |
|Wipe right in |4281705568 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063704-1496651423881.gif) </span> |
|Wipe left in |4281705569 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063704-596420578809.gif) </span> |
|Wipe down in |4281705570 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063704-1033469782403.gif) </span> |
|Wipe up in |4281705571 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063704-197284563939.gif) </span> |
|Slide in left |4281705576 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063713-937689602056.gif) </span> |
|Slide in right |4281705572 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063723-917476357674.gif) </span> |
|Slide in down |4281705574 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063713-136256433500.gif) </span> |
|Slide in up |4281705573 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063713-1080369241439.gif) </span> |
|Fade in |4281705575 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063704-1247599245412.gif) </span> |
|Zoom in |4281705579 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063718-1355181781951.gif) </span> |
|Feather wipe down in |4281705582 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063718-515934504891.gif) </span> |
|Feather wipe left in |4281705583 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063718-133846055259.gif) </span> |
|Feather wipe up in |4281705578 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063723-518019233818.gif) </span> |
|Feather wipe right in |4281705577 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731063713-570331542685.gif) </span> |


<span id="text-out"></span>
#### Exit animation ID


|Category |ID |Animation display |
|---|---|---|
|Wipe right out |4281705587 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065059-53677688803.gif) </span> |
|Wipe left out |4281705586 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065051-112130537210.gif) </span> |
|Wipe down out |4281705585 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065051-241941548462.gif) </span> |
|Wipe up out |4281705584 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065108-1320047236542.gif) </span> |
|Fade out |4281705581 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065533-1234828122086.gif) </span> |
|Circle sweep out |4281705591 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065059-1357837732443.gif) </span> |
|Dissolve out |4281705592 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065544-910389910754.gif) </span> |
|Zoom out |4281705593 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065104-1487674149260.gif) </span> |
|Slide out right |4281705599 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065059-146012509249.gif) </span> |
|Slide out left |4281705588 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065051-549104944078.gif) </span> |
|Slide out down |4281705589 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065104-1572233105961.gif) </span> |
|Slide out up |4281705596 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065108-1571191869166.gif) </span> |
|Feather wipe down out |4281705597 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065051-504672405180.gif) </span> |
|Feather wipe left out |4281705598 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065059-1029528761027.gif) </span> |
|Feather wipe right out |4281705590 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065059-677378047768.gif) </span> |
|Feather wipe up out |4281705594 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065051-330511889584.gif) </span> |


<span id="text-loop"></span>
#### Loop animation ID


|Category |ID |Animation display |
|---|---|---|
|Wave |4281705600 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065654-371205032814.gif) </span> |
|Flip |4281705595 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065654-1585290394487.gif) </span> |


<span id="font-id"></span>
### Font ID


|Category |ID |Font display |
|---|---|---|
|Inter |4304241011 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731062952-238032243767.png) </span> |
|Montserrat |4304241012 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731062952-1396239195299.png) </span> |
|OPPO Sans |4304241009 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731062952-718824641386.png) </span> |
|Roboto |4304241007 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731062952-1766626978598.png) </span> |
|Source Han Serif |4304241010 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731062952-1431957977400.png) </span> |


<span id="stylized-text-id"></span>
### Stylized text ID


|Category |ID |Stylized text display |
|---|---|---|
|Yellow purple 3D |4280712022 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065942-290985170824.jpeg) </span> |
|Yellow white pop |4280712024 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065947-299769870861.jpeg) </span> |
|Sunset |4280712023 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065947-1022264267731.jpeg) </span> |
|Rainbow |4280712025 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065947-1527624835147.jpeg) </span> |
|Orange ring |4280712027 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065952-165693950917.jpeg) </span> |
|ByteDance |4280712026 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065942-1193083876893.jpeg) </span> |
|Blue shadow glow |4280712028 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065942-1515074073532.jpeg) </span> |
|Blue glow |4280712032 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065942-1435229620591.jpeg) </span> |
|Galaxy |4280712030 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065947-1257214279194.jpeg) </span> |
|Gradient shadow |4280712031 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065947-1272497277125.jpeg) </span> |
|Green glow |4280712033 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065952-1401319606932.jpeg) </span> |
|Basic text |4280712034 |<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260731065942-1715346510196.jpeg) </span> |
