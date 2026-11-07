---
title: "Create a multi-track editing task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit`

Use this API to submit an asynchronous multi\-track editing task. Define your edit using a structured `track` timeline and `canvas` and `output` settings, including each element, filter, and animation. The tool combines video, audio, images, text, and subtitles according to this configuration. It supports transitions, visual effects, styled text, color filters, cropping, speed adjustment, and volume control. When the task completes, you can retrieve a download URL for the output.

The parameters for multi\-track editing are organized into a four\-layer model: **canvas → track → element → filter**. If you are new to the tool, start with [Multi-track editing](https://docs.byteplus.com/multi-track-editing) for core concepts, usage instructions, and examples. Then use this API reference to configure the fields in your request.

## Request parameters

### Header parameters

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |The authentication credential in the format `Bearer {Your_API_Key}`. To obtain an API key, see [Basic concepts and prerequisites](https://docs.byteplus.com/basic-concepts-and-prerequisites). |

### Body parameters

The following table lists the top\-level parameters of the request body. The structures of `track`, `output`, `canvas`, and `extra_param` are described in separate sections below.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`track` |Array of Array |Yes |See [Request example](https://docs.byteplus.com/en/docs/25/123501#request-example) |The multi\-track timeline as a two\-dimensional array. Each item in the outer array is a track, and each item in an inner array is an element on that track. Tracks with larger indices are rendered above tracks with smaller indices. The array must contain at least 1 track, and each track must contain at least 1 element. For an element's fields, see [Track element object](https://docs.byteplus.com/en/docs/25/123501#track-element-object) below. |
|`output` |Object |No |See [Request example](https://docs.byteplus.com/en/docs/25/123501#request-example) |The output configuration controls the container format, frame rate, inclusion or exclusion of audio and video, encoding parameters, cover images, and canvas sizing. For field details, see [output object](https://docs.byteplus.com/en/docs/25/123501#output-object) below. If omitted, each field uses its default value. |
|`canvas` |Object |No |`{"width": 1080, "height": 1920}` |The canvas configuration defines the resolution, background color, and aspect ratio settings of the final output video. For field details, see [canvas object](https://docs.byteplus.com/en/docs/25/123501#canvas-object) below. If you omit it, the system automatically determines the canvas based on the input media and output configuration. |
|`extra_param` |Object |No |See [Request example](https://docs.byteplus.com/en/docs/25/123501#request-example) |Additional parameters for adding information such as AIGC metadata. For field details, see [extra_param object](https://docs.byteplus.com/en/docs/25/123501#extra-param-object) below. If you omit it, no additional information is added. |
|`client_token` |String |No |`your_unique_request_id_135` |The client request token used for idempotency control. It is case\-sensitive and can contain no more than 64 printable ASCII characters. If you omit it, no idempotency control is applied and each request creates a new task. For details, see [Idempotency control](https://docs.byteplus.com/basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback data. The content you provide is returned unchanged in the [event notification](https://docs.byteplus.com/event-notification) when the task is complete, allowing you to associate the callback with data in your application. The maximum length is 512 bytes. If you omit it, the callback does not carry custom data. |
|`callback_url` |String |No |`https://example.com/callback` |The URL that receives the result callback for this task. If you provide this parameter, it takes precedence over the global callback URL configured in the console. The URL must start with `http://` or `https://`. Default behavior: if you omit it, the global callback URL configured in the console is used; if neither is configured, no callback is sent. To learn about the callback mechanism and message structure, see [Event notification](https://docs.byteplus.com/event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task is submitted. If you omit this parameter, the system\-created default queue is used. Submit tasks for different business workflows or priorities to separate queues to allocate costs to the project associated with each queue. You can create and manage queues on the queue management page in the AI MediaKit console, where the system automatically assigns each queue an ID. For details, see [Allocating costs by project or API Key](https://docs.byteplus.com/managing-costs-and-resources-with-projects-and-queues). |

## Data structures

### Track element object

`track` is a two\-dimensional array in the format `track[trackIndex][elementIndex]`. Each element is a JSON object that defines the content, when it appears, and how it is presented. The following table lists the common fields supported by all element types. Each element type also has specific fields, described in the sections that follow.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`type` |String |Yes |`video` |The element type, which determines the content type and the fields available for that type. Valid values: `video`, `audio`, `image`, `text`, `subtitle`, `effect`, `gaussian` (Gaussian blur), and `text_roll` (scrolling text). |
|`target_time` |Array of Integer |Yes |`[0, 5000]` |The element's start and end times on the output timeline, in milliseconds, in the format `[start_time, end_time]`. The array must contain exactly 2 integers, each ≥ 0. |
|`source` |String |Conditionally required |`https://example.com/clip.mp4` |The URL of the element's source media.<br><br><br>* For media elements (`video`/`audio`/`image`/`gaussian`): Required. Four input protocols are supported: a publicly accessible HTTP or HTTPS URL, local upload (`mediakit://`), BytePlus VOD (`vod://`), and BytePlus TOS object storage (`tos://`).<br><br>* For generated elements (`text`/`text_roll`/`effect`): Usually not required.<br><br>* For `subtitle`: The subtitle file URL is specified in the `text` field, so this field is not required. |
|`text` |String |Conditionally required |`Sample styled text` |The text content. Required for `text`/`subtitle`/`text_roll` elements (for `subtitle`, provide the subtitle file URL). Not required for non\-text elements. |
|`extra` |Array of Object |No |See [Request example](https://docs.byteplus.com/en/docs/25/123501#request-example) |Additional filters and effects to apply to the element, including cropping, transformation, color grading, speed adjustment, animations, and transitions. Each item is a filter object. For the object structure, see [Extra filter and effect objects](https://docs.byteplus.com/en/docs/25/123501#extra-filter-and-effect-objects) below. If omitted, no additional effects are applied. |

In addition to the common fields, each element type supports the following specific fields.

#### Dedicated fields for video / audio / image elements

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`loop` |Boolean |No |`false` |Whether to loop the source. When `true`, a source shorter than the interval defined by `target_time` repeats to fill that interval. If the source duration is greater than or equal to that interval, this field has no effect. Default: `false`. |

> To position `video` and `image` elements on the canvas, add a [2D transformation](https://docs.byteplus.com/en/docs/25/123501#_2d-transformation) configuration to `extra`. If omitted, these elements fill the `canvas` by default.

#### Dedicated fields for text / subtitle elements

The text (`text`) and subtitle (`subtitle`) elements share the following fields. For `text`, the `text` field contains the text content; for `subtitle`, the `text` field contains the publicly accessible URL of the subtitle file (such as an SRT file). For both element types, you **must** add a [2D transformation](https://docs.byteplus.com/en/docs/25/123501#_2d-transformation) to `extra` to define their display area on the canvas.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`text_res` |String |No |`1179433` |The styled text ID. For available values, see [Styled text IDs](https://docs.byteplus.com/multi-track-editing#styled-text-ids). |
|`font_type` |String |No |`1525745` |The font ID or a publicly accessible font file URL. The default font is FZYaSong.<br><br><br>* To use a preset font: Provide a font ID. For available values, see [Font IDs](https://docs.byteplus.com/multi-track-editing#font-ids).<br><br>* To use a custom font: Provide a publicly accessible URL of a TTF/OTF font file, for example, `https://example.com/font.ttf`. Ensure that you have a valid license to use the font. |
|`font_size` |Integer |No |`200` |The font size, in pixels. When the default font is used, the default value is `200`. |
|`font_color` |String |No |`#FF0000FF` |The text color in hexadecimal RGBA format. Defaults to white when styled text is not used. Supported only for basic text, not for styled text. |
|`bold` |Boolean |No |`false` |Whether to make the text bold. Default: `false`. |
|`italic` |Boolean |No |`false` |Whether to make the text italic. Default: `false`. |
|`underline` |Boolean |No |`false` |Whether to add an underline. Default: `false`. |
|`background_color` |String |No |`#FF0000FF` |The text background color in hexadecimal RGBA format. The background covers only the text area; for multiple lines, its width is based on the longest line. Default: `#00000000`. Supported only for basic text. |
|`background_border_size` |Float |No |`0` |The size of the text background border. The background follows the text area. Default: `0`. |
|`border_color` |String |No |`#FF0000FF` |The text outline color in hexadecimal RGBA format. Default: `#00000000`. Supported only for basic text. |
|`border_width` |Integer |No |`1` |The text outline width. The value must be at least 1 and no greater than 0.1 times `font_size`. |
|`line_max_width` |Float |No |`-1` |The width at which text wraps automatically. `-1` (default) disables automatic wrapping. A value between 0 and 1 specifies a ratio of the `transform` width when `typesetting=0`, or its height when `typesetting=1`. |
|`typesetting` |Integer |No |`0` |The text layout direction: `0` (default) for horizontal text; `1` for vertical text. |
|`align_type` |Integer |No |`0` |The text alignment. Use this field with `typesetting`. For horizontal layout: `0` for left\-aligned, `1` for centered, `2` for right\-aligned; for vertical layout: `1` for centered, `3` for top\-aligned, `4` for bottom\-aligned. |

#### Dedicated fields for text_roll elements

Use `text_roll` to create promotional videos with scrolling text.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`single_roll_duration` |Integer |No |`5000` |The display duration of each page, in milliseconds, used to control the scrolling speed. Default: `5000` (5 seconds). |
|`start_time` |Integer |No |`3000` |The display duration of the first frame, in milliseconds. Default: `3000`. |
|`end_time` |Integer |No |`3000` |The display duration of the last frame, in milliseconds. Default: `3000`. |
|`start_pos` |Float |No |`0.5` |The display position of the first frame, in the range [0, 1]. Default: `0.5`. |
|`end_pos` |Float |No |`-0.5` |The display position of the last frame, in the range [\-1, 0]. Default: `-0.5`. |
|`margin_left` |Integer / String |No |`0` |The left and right margins of the text display area (available only when `typesetting=0` for horizontal layout). An Integer value such as `10` means 10 px on each side; a String value such as `10%` means 10% on each side. |
|`margin_top` |Float / String |No |`0` |The top and bottom margins of the text display area, in the range [0, 0.5] (available only when `typesetting=1` for vertical layout). A Float value such as `10` means 10 px on each side; a String value such as `10%` means 10% on each side. |
|`font_type` |String |No |`1525745` |The font ID. The default is FZYaSong. For available values, see [Font IDs](https://docs.byteplus.com/multi-track-editing#font-ids). |
|`font_size` |Integer |No |`200` |The font size, in pixels. When the default font is used, the default value is `200`. |
|`line_padding` |Integer |No |`5` |The spacing between lines, in pixels. |
|`font_color` |String |No |`#FF0000FF` |The text color in hexadecimal RGBA format. Defaults to white when styled text is not used. |
|`inner_padding` |Float |No |`3` |The spacing between characters, in pixels. |
|`typesetting` |Integer |No |`0` |The text layout direction: `0` (default) for horizontal text; `1` for vertical text. |
|`align_type` |Integer |No |`0` |The text alignment. Use this field with `typesetting`. For horizontal layout: `0` for left\-aligned, `1` for centered, `2` for right\-aligned; for vertical layout: `1` for centered, `3` for top\-aligned, `4` for bottom\-aligned. |

#### Dedicated fields for effect elements

The `effect` element uses only the common fields. Define the effect using a [color filter](https://docs.byteplus.com/en/docs/25/123501#color-filter) or [visual effect](https://docs.byteplus.com/en/docs/25/123501#visual-effects) in `extra`, and add **only one** of these filters.

#### Dedicated fields for gaussian elements

The `gaussian` (Gaussian blur) element uses the common fields. You **must** add both a [2D transformation](https://docs.byteplus.com/en/docs/25/123501#_2d-transformation) and a [Gaussian blur](https://docs.byteplus.com/en/docs/25/123501#gaussian-blur) in `extra`. As a standalone element, `gaussian` blurs the entire source specified by `source`.

### Extra filter and effect objects

`extra` is an array of objects that applies one or more filters or effects to its element. Each object uses `type` to identify the filter and includes fields specific to that filter type. The available filters are listed below by function:

|Filter (`type` value) |Description |
|---|---|
|`trim` |Trimming, which extracts a segment from the source media. For details, see [Trimming](https://docs.byteplus.com/en/docs/25/123501#trimming). |
|`crop` |Cropping, which selects a rectangular area of the frame. For details, see [Cropping](https://docs.byteplus.com/en/docs/25/123501#cropping). |
|`speed` |Playback speed adjustment, which changes the playback speed of the video or audio. For details, see [Playback speed](https://docs.byteplus.com/en/docs/25/123501#playback-speed). |
|`transform` |2D transformation, which controls the position, size, rotation, and opacity of the element on the canvas. For details, see [2D transformation](https://docs.byteplus.com/en/docs/25/123501#_2d-transformation). |
|`lut_filter` |Color filter, which applies a preset color\-grading effect to the frame. For details, see [Color filter](https://docs.byteplus.com/en/docs/25/123501#color-filter). |
|`effect_filter` |Visual effects, such as split\-screen layouts and mirroring. For details, see [Visual effects](https://docs.byteplus.com/en/docs/25/123501#visual-effects). |
|`equalizer` |Color adjustment, which controls brightness, saturation, tone, and more. For details, see [Color adjustment](https://docs.byteplus.com/en/docs/25/123501#color-adjustment). |
|`delogo` |Localized blur, which blurs a specified area, often used to cover a logo. For details, see [Localized blur](https://docs.byteplus.com/en/docs/25/123501#localized-blur). |
|`gaussian` |Gaussian blur, which applies blur to the entire element or background. For details, see [Gaussian blur](https://docs.byteplus.com/en/docs/25/123501#gaussian-blur). |
|`transition` |Transition, which creates a transition effect between adjacent video elements on the same track. For details, see [Transition](https://docs.byteplus.com/en/docs/25/123501#transition). |
|`video_animation` |Video animation, which adds entrance, exit, or loop animations to a video or image. For details, see [Video animation](https://docs.byteplus.com/en/docs/25/123501#video-animation). |
|`text_animation` |Text animation, which adds entrance, exit, or loop animations to a text element. For details, see [Text animation](https://docs.byteplus.com/en/docs/25/123501#text-animation). |
|`a_fade` |Audio fade\-in and fade\-out. For details, see [Audio fades](https://docs.byteplus.com/en/docs/25/123501#audio-fades). |
|`a_volume` |Volume adjustment. For details, see [Volume adjustment](https://docs.byteplus.com/en/docs/25/123501#volume-adjustment). |

**Filter** **`target_time`**: Some filters have a `target_time` field that specifies a time interval relative to the start of their element, in milliseconds. For example, if the element `target_time` is `[50000, 60000]` and the filter `target_time` is `[5000, 6000]`, the effect applies during `[55000, 56000]` on the output timeline. This field has no effect in an `effect` element.

#### Trimming

Can be added to `video` and `audio` elements. When both `trim` and `speed` are added to the same element, `trim` runs first, then `speed`.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `trim`. |
|`start_time` |Integer |Yes |The trim start time, in milliseconds. |
|`end_time` |Integer |Yes |The trim end time, in milliseconds. When trimming an audio segment (or a video that contains audio), the duration of the trimmed segment must be greater than 0.1 seconds; otherwise, no trimming is performed and the entire source is included in the output. |

#### Cropping

Can be added to `video` and `image` elements. When both `crop` and `transform` are added to the same element, `crop` runs first, then `transform`.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `crop`. |
|`pos_x` |Integer |Yes |The horizontal offset of the top\-left corner of the crop area relative to the top\-left corner of the original image, in pixels. |
|`pos_y` |Integer |Yes |The vertical offset of the top\-left corner of the crop area relative to the top\-left corner of the original image, in pixels. |
|`width` |Integer |Yes |The width of the crop area, in pixels. |
|`height` |Integer |Yes |The height of the crop area, in pixels. |

#### Playback speed

Can be added to `video` and `audio` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `speed`. |
|`speed` |Float |No |The playback speed. Default: `1` (original speed); values below 1 slow playback down, and values above 1 speed it up. The range is [0.1, 4]; values outside this range are set to 0.1. |

#### 2D transformation

Can be added to `video`, `image`, and `text` elements to position and size the element on the output canvas.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `transform`. |
|`pos_x` |Integer |Yes |The horizontal offset of the element's top\-left corner relative to the top\-left corner of the output canvas, in pixels. |
|`pos_y` |Integer |Yes |The vertical offset of the element's top\-left corner relative to the top\-left corner of the output canvas, in pixels. |
|`width` |Integer |Yes |The width of the element on the output canvas, in pixels. |
|`height` |Integer |Yes |The height of the element on the output canvas, in pixels. |
|`rotation` |Integer |No |The rotation angle, in the range [\-360, 360]. Clockwise is positive. |
|`flip_x` |Boolean |No |Whether to flip the element horizontally. |
|`flip_y` |Boolean |No |Whether to flip the element vertically. |
|`alpha` |Float |No |The opacity, in the range [0, 1]. 0 is fully transparent. |

#### Color filter

Can be added to `video`, `image`, and `effect` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `lut_filter`. |
|`source` |String |Yes |The filter ID. For available values, see [Color filter IDs](https://docs.byteplus.com/multi-track-editing#color-filter-ids). |
|`target_time` |Array of Integer |Yes |The time interval during which the filter applies, relative to the start of its element, in milliseconds. Has no effect in an `effect` element. |
|`intensity` |Float |No |The filter intensity, in the range [0, 1]. Default: `1`. |

#### Visual effects

Can be added to `video`, `image`, and `effect` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `effect_filter`. |
|`source` |String |Yes |The effect ID. For available values, see [Visual effect IDs](https://docs.byteplus.com/multi-track-editing#visual-effect-ids). |
|`target_time` |Array of Integer |Yes |The time interval during which the effect applies, relative to the start of its element, in milliseconds. Has no effect in an `effect` element. |

#### Color adjustment

Can be added to `video` and `image` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `equalizer`. |
|`target_time` |Array of Integer |Yes |The time interval during which the effect applies, relative to the start of its element, in milliseconds. |
|`brightness` |Float |No |The brightness, in the range [0, 1]. |
|`saturation` |Float |No |The saturation, in the range [0, 1]. |
|`tone` |Float |No |The tone, in the range [0, 1]. |

#### Localized blur

Can be added to `video` and `image` elements. Add multiple instances to blur different areas. Within the same element, the execution order is: `crop` → `delogo` → `transform`.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `delogo`. |
|`target_time` |Array of Integer |Yes |The time interval during which the effect applies, relative to the start of its element, in milliseconds. |
|`delogo_type` |String |No |The watermark removal type. Default: `gaussian` (local Gaussian blur), which is currently the only supported value. |
|`pos_x` |Integer |Yes |The horizontal offset of the top\-left corner of the localized blur area relative to the top\-left corner of the original image, in pixels. |
|`pos_y` |Integer |Yes |The vertical offset of the top\-left corner of the localized blur area relative to the top\-left corner of the original image, in pixels. |
|`width` |Integer |Yes |The width of the localized blur area, in pixels. |
|`height` |Integer |Yes |The height of the localized blur area, in pixels. |
|`sigma` |Integer |No |The intensity of the localized blur. Default: `0` (no effect). The recommended range is [10, 70]; a larger value produces a stronger effect. |
|`radius` |Integer |No |The radius of the localized blur. Default: `0` (no effect). The recommended range is [10, 70]; matching this value to `sigma` is recommended. |

#### Gaussian blur

Can be added to `video`, `image`, and `gaussian` elements: on `video` and `image` elements, it creates a blurred background; on a `gaussian` element, it blurs the entire source.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `gaussian`. |
|`target_time` |Array of Integer |Yes |The time interval during which the effect applies, relative to the start of its element, in milliseconds. |
|`radius` |Integer |Yes |The Gaussian blur radius. Default: `0` (no effect). The recommended range is [10, 70]; a larger value produces a stronger effect. |
|`sigma` |Integer |Yes |The Gaussian blur intensity. Default: `0` (no effect). The recommended range is [10, 70]; matching this value to `radius` is recommended. |

#### Transition

Can be added to `video` elements. When applying a transition between two adjacent videos A and B on the same track, add the `transition` only to video A.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `transition`. |
|`source` |String |Yes |The transition ID. For available values, see [Transition IDs](https://docs.byteplus.com/multi-track-editing#transition-ids). |
|`duration` |Integer |Yes |The transition duration, in milliseconds. |

#### Video animation

Can be added to `video` and `image` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `video_animation`. |
|`anim_res` |String |Yes |The video animation ID. For available values, see [Video animation IDs](https://docs.byteplus.com/multi-track-editing#video-animation-ids). |
|`anim_start_time` |Integer |Yes |The animation start time, in milliseconds. |
|`anim_end_time` |Integer |Yes |The animation end time, in milliseconds. |
|`anim_loop` |Boolean |No |Whether the animation loops. Default: `false`. When this animation loops, other animations are disabled. |
|`anim_loop_duration` |Integer |No |The loop animation duration. Default: `0`. Required for a loop animation. |

#### Text animation

Can be added to `text` elements. The sum of `anim_in_duration` and `anim_out_duration` must be less than the text display duration defined by `target_time`.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `text_animation`. |
|`anim_in_res` |String |No |The entrance animation ID, which must be set together with `anim_in_duration`. For available values, see [Text animation IDs](https://docs.byteplus.com/multi-track-editing#text-animation-ids). |
|`anim_in_duration` |Integer |No |The text entrance animation duration, in milliseconds. |
|`anim_out_res` |String |No |The exit animation ID, which must be set together with `anim_out_duration`. For available values, see [Text animation IDs](https://docs.byteplus.com/multi-track-editing#text-animation-ids). |
|`anim_out_duration` |Integer |No |The text exit animation duration, in milliseconds. |
|`anim_loop_res` |String |No |The loop animation ID, which must be set together with `anim_loop_duration`. For available values, see [Text animation IDs](https://docs.byteplus.com/multi-track-editing#text-animation-ids). |
|`anim_loop_duration` |Integer |No |The loop animation duration, in milliseconds. |

#### Audio fades

Can be added to `audio` and `video` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `a_fade`. |
|`fade_in` |Integer |No |The fade\-in duration, in milliseconds. For example, if set to 2000, the audio fades in during the first 2 seconds. |
|`fade_out` |Integer |No |The fade\-out duration, in milliseconds. For example, if set to 2000, the audio fades out during the last 2 seconds. |

#### Volume adjustment

Can be added to `audio` and `video` elements.

|Parameter |Type |Required |Description |
|---|---|---|---|
|`type` |String |Yes |The value is `a_volume`. |
|`volume` |Float |No |The volume. `0` means muted. Default: `1`. |

### output object

The output configuration controls the container format, frame rate, inclusion or exclusion of audio and video, encoding parameters, cover images, and canvas sizing.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`format` |String |No |`mp4` |The container format. Valid values: `mp4`, `hls`, `mp3`. Default: `mp4`. When exporting `mp3`, you must also set `disable_video=true`; for `hls`, only h264/h265 video codecs are supported. |
|`fps` |Number |No |`30` |The output frame rate, in fps. The value must be `≥ 1`. Default: `30`. |
|`alpha` |Boolean |No |`false` |Whether to include an alpha channel. When `true`, the output uses a codec that supports an alpha channel (default `vp9`). This takes precedence over `codec.video_codec`. Default: `false`. |
|`disable_video` |Boolean |No |`false` |Whether to output audio only. Set to `true` when exporting mp3. Default: `false`. |
|`disable_audio` |Boolean |No |`false` |Whether to output video only. When both `disable_audio` and `disable_video` are `false`, the output includes both audio and video. Default: `false`. |
|`codec` |Object |No |`-` |The audio/video encoding parameters. For field details, see [output.codec object](https://docs.byteplus.com/en/docs/25/123501#output-codec-object) below. If you omit it, the default encoding settings are used. |
|`cover` |Object |No |`-` |The configuration for extracting cover images from video frames. For field details, see [output.cover object](https://docs.byteplus.com/en/docs/25/123501#output-cover-object) below. If you omit it, no additional cover image is generated. |
|`canvas_with_max` |Boolean |No |`false` |Whether to match the canvas resolution to the highest resolution among the input sources. Default: `false`. |
|`canvas_with_ratio` |Boolean |No |`false` |Whether to size the canvas using a fixed ratio of its long and short edges. Use this setting with `long`, `short`, and `ratio` in `canvas`. Default: `false`. |
|`audio_phase_detect` |Boolean |No |`false` |Whether to enable audio phase inversion detection. This can take a long time for lengthy sources, so consider the additional processing time before enabling it. Default: `false`. |

> **Canvas resolution priority** (from high to low): `canvas.width`/`canvas.height` (Integer) \> `output.canvas_with_max` \> `output.canvas_with_ratio` \> `canvas.width`/`canvas.height` (String expression).

#### output.codec object

The audio/video encoding parameters.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`video_codec` |String |No |`h264` |The video codec. Valid values: `h264` (default), `vp9`, `h265`. |
|`preset` |String |No |`medium` |The encoding preset, which controls the trade\-off between speed and quality, available only when `video_codec` is h264/h265. Default: `medium`. |
|`crf` |Integer |No |`23` |The constant rate factor, available only for h264/h265. Default: `23`. This parameter has no effect when `video_bit_rate` is set. |
|`video_bit_rate` |Integer |No |`-` |The video encoding bitrate, in bps. If omitted, `crf` controls the bitrate. If set, `crf` has no effect. |
|`audio_codec` |String |No |`aac` |The audio codec. Currently, only `aac` is supported. Default: `aac`. |
|`audio_bitrate` |Integer |No |`128` |The audio encoding bitrate, in kbps. Default: `128`. |

#### output.cover object

The configuration for extracting cover images from video frames.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`disable_cover` |Boolean |No |`false` |Whether to disable cover image generation. Default: `false` (the cover is saved). |
|`cover_time` |Array of Integer |No |`[100]` |The timestamps for extracting frames, in milliseconds. The service captures a frame at each specified timestamp and saves it as an image. |
|`format` |String |No |`png` |The cover image format. Valid values: `jpeg`, `png`. Default: `png`. |

### canvas object

The canvas configuration defines the resolution, background color, and aspect ratio settings of the final output video.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`width` |Integer / String |No |`1080` |The canvas width, in pixels, in the range [160, 8192]. It also supports an expression to automatically match a specific element's width, for example, `$0\|0.w` uses the width of the `track[0][0]` element. |
|`height` |Integer / String |No |`1920` |The canvas height, in pixels, in the range [160, 8192]. It also supports an expression, for example, `$0\|0.h`. |
|`background_color` |String |No |`#000000FF` |The canvas background color in hexadecimal RGBA format. Default: `#00000000`. |
|`long` |Integer |No |`1920` |The length of the canvas's longer edge when sizing it by aspect ratio, in pixels, in the range [160, 8192]. Available only when `output.canvas_with_ratio=true`. |
|`short` |Integer |No |`1080` |The length of the canvas's shorter edge when sizing it by aspect ratio, in pixels, in the range [160, 8192]. Available only when `canvas_with_ratio=true`, and takes precedence over `long`. |
|`index` |String |No |`0\|0` |The index of the element whose orientation the canvas follows, in the format `track\|element`. The default is `0\|0` (aligned to `track[0][0]`); `MAX` selects the source with the highest resolution. Available only when `canvas_with_ratio=true`. |
|`ratio` |String |No |`16:9` |The long\-to\-short edge ratio. Default: `16:9`; `-1` or `-1:-1` matches the specified input source. Available only when `canvas_with_ratio=true`. |

### extra_param object

Additional parameters for adding information such as AIGC metadata.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`upload` |Object |No |See below |Upload\-related extra parameters. For field details, see [extra_param.upload object](https://docs.byteplus.com/en/docs/25/123501#extra-param-upload-object) below. |

#### extra_param.upload object

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`aigc_meta` |String |No |See [Request example](https://docs.byteplus.com/en/docs/25/123501#request-example) |AIGC metadata encoded as a JSON object string, used to add compliance labels to generated content. Its fields follow relevant regulations on labeling AI\-generated and synthetic content. Common fields include `Label`, `ContentProducer`, `ProduceID`, `ReservedCode1`, `ContentPropagator`, `PropagateID`, and `ReservedCode2`. |

## Request example

The following example shows how to submit a multi\-track editing task: the first track contains a video (0–5000 ms), the second track adds a styled text overlay (0–3000 ms), the output is an mp4 video at 30 fps with a 1080×1920 canvas, and AIGC metadata labels are added.

**Additional examples**: For complete request examples for typical scenarios such as concatenation, trimming, split screen, picture\-in\-picture, subtitles, transitions, animations, color filters, and Gaussian blur, see the [Common scenario examples](https://docs.byteplus.com/multi-track-editing#common-scenario-examples) section in the multi\-track editing guide.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "track": [
    [
      {
        "type": "video",
        "source": "https://example.com/clip.mp4",
        "target_time": [0, 5000]
      }
    ],
    [
      {
        "type": "text",
        "text": "Sample styled text",
        "target_time": [0, 3000],
        "extra": [
          {
            "type": "transform",
            "width": 1000,
            "height": 200,
            "pos_x": 40,
            "pos_y": 860
          }
        ]
      }
    ]
  ],
  "output": {
    "format": "mp4",
    "fps": 30
  },
  "canvas": {
    "width": 1080,
    "height": 1920,
    "background_color": "#000000FF"
  },
  "extra_param": {
    "upload": {
      "aigc_meta": "{\"Label\":\"1\",\"ContentProducer\":\"multi-track-edit-test\",\"ProduceID\":\"produce-test-001\"}"
    }
  }
}'
```

## Response

When you submit a task, the API immediately returns a response indicating whether the task was successfully added to the processing queue.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was successfully submitted.<br><br><br>* `true`: The task was successfully submitted to the processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier of the task. A valid value is returned only when `success` is `true`. You can use this ID to check the task status and retrieve the result. |
|`request_id` |String |The unique identifier of this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. For details, see the Error object below. |

#### Error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For details about each error code, see [Error codes](https://docs.byteplus.com/error-codes). |
|`type` |String |The error category. For example, `BadRequest`. |
|`message` |String |A detailed error description to help with troubleshooting. |
|`param` |String |The specific parameter that caused the error. This field is optional. |

### Response examples

#### Success response

```JSON
{
  "success": true,
  "task_id": "amk-tool-multi-track-edit-123456789",
  "request_id": "20260901130000ABCDEFG12345"
}
```

#### Failure response

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20260901130500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `track` is required.",
    "param": "track",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Multi\-track editing runs asynchronously. The submission response does not include the task's execution status or final result. You can use either of the following methods to obtain the task result:

* **Method 1 (polling):**  Use the `task_id` returned when you submitted the task to periodically call the [Get task details API](https://docs.byteplus.com/get-task-details) until `status` changes to `completed` or `failed`.

* **Method 2 (event notification):**  Configure a callback URL in advance in the AI MediaKit console, or use the `callback_url` parameter when submitting the task to specify a callback URL for that individual task. After the task is complete, the system sends the detailed result to the specified URL. For details, see [Event notification](https://docs.byteplus.com/event-notification).

When the task completes successfully, the `result` field in the task details contains the following fields.

|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.com/multi_track_output.mp4` |The download URL of the output video. This temporary HTTPS URL is valid for 24 hours. Download and save the video before it expires. |
|`duration` |Number |`5.0` |The total duration of the output video, in seconds. The value must be `≥ 0` and is used for metering and billing. |
|`resolution` |String |`1080p` |The resolution of the output video. Valid values: `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, `4k`. |

The following example shows the complete task details after successful completion:

```JSON
{
    "success": true,
    "task_id": "amk-tool-multi-track-edit-123456789",
    "request_id": "20260901130000ABCDEFG12345",
    "status": "completed",
    "result": {
        "video_url": "https://example.com/multi_track_output.mp4",
        "duration": 5.0,
        "resolution": "1080p"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```
