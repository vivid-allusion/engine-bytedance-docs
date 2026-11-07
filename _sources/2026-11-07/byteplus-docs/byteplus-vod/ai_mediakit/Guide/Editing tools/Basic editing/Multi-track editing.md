---
title: "Multi-track editing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-multi-track-editing"
---

The multi\-track editing tool in AI MediaKit combines video, audio, images, text, subtitles, and other content into a single output. It supports transitions, visual effects, styled text, color filters, cropping, speed adjustment, and volume control. Define your edit using a structured `track` timeline and `canvas` and `output` settings, and the tool renders the result according to your configuration. When the task completes, you receive a download URL for the rendered output. Use multi\-track editing to produce short videos in batches, create new videos from templates, combine images and text in video layouts, or build picture\-in\-picture and split\-screen video walls.

## Core concepts

All parameters for multi\-track editing are organized around a four\-layer model: **canvas → track → element → filter**. The layers form a hierarchy: a canvas contains multiple tracks, each track contains multiple elements, and each element can have filters applied to it.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/5c09a19a-f910-4699-9320-ec260fff1a76.svg)

On the timeline, multiple tracks are stacked from bottom to top, and the elements within each track are arranged in order of their `target_time`:

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/436a9c27-dcc0-4b73-b96d-dbc486efedca.svg)

|Layer |Corresponding parameter |Description |
|---|---|---|
|Canvas |`canvas` |Defines the width, height, and background color of the output video. All visual elements are rendered onto this canvas. |
|Track |`track` |Organizes media and other content into layers. `track` is a two\-dimensional array that represents multiple tracks. A larger track index means a higher rendering layer. |
|Element |`track[i][j]` |An item of content placed on a track, such as a video clip, an image, a text block, or an effect. Each element has its own `type` and a `target_time` interval that determines when it appears on the timeline. |
|Filter |The `extra` array of an element |An effect applied to an element to change how it looks or sounds. Examples include cropping, transformation, color grading, speed adjustment, and transitions. |

### Canvas

The canvas defines the resolution and background color of the final output video and provides the surface on which all visual elements are rendered. Specify the resolution using `canvas.width`/`canvas.height` (in pixels, in the range [160, 8192]) and the background color using `canvas.background_color`. If you omit `canvas`, the system automatically determines the canvas based on the input media and output configuration. For details, see [Customize the canvas](https://docs.byteplus.com/en/docs/25/123430#customize-the-canvas).

### Track and rendering layers

`track` defines the editing timeline. Like the tracks in professional video editing software, it organizes when content plays and how it is layered. It is a two\-dimensional array in the format `track[trackIndex][elementIndex]`:

* The outer array contains the tracks. The index `[trackIndex]` determines the rendering layer of the track. In the `track` array, a larger index means a higher track layer, and the visual content of a higher track covers that of a lower track.

   * `track[0]`: The bottom layer, typically used for the background or main video.

   * `track[1]`: Above `track[0]`, typically used for picture\-in\-picture videos, stickers, and animated effects.

   * `track[2]`: Above `track[1]`, typically used for titles or subtitles that appear over the entire composition.

* Each inner array contains one or more elements on a single track. Multiple elements within the same track can be adjacent in time but should not overlap.

```JSON
"track": [
  // --- Track 0 (track[0]): The bottom layer ---
  [ 
    {"type": "video", "target_time": [0, 5000],  "source": "https://example.com/video-a.mp4"}, // Element track[0][0]
    {"type": "video", "target_time": [5000, 10000], "source": "https://example.com/video-b.mp4"} // Element track[0][1]
  ],
  // --- Track 1 (track[1]): Overlaid on top of track 0 ---
  [ 
    {"type": "text", "target_time": [1000, 4000], "text": "Title"} // Element track[1][0]
  ]
]
```

### Element types

Each element uses `type` to specify its content type and `target_time` to set its start and end times on the output timeline. Media elements use `source` for the source URL, and text elements use `text` for their content. The following element types are supported:

|`type` value |Category |Description |Required fields |
|---|---|---|---|
|`video` |Core media |Video |`type`, `target_time`, `source` |
|`audio` |Core media |Audio |`type`, `target_time`, `source` |
|`image` |Core media |Image |`type`, `target_time`, `source` |
|`text` |Overlay content |Text (including styled text), with the `text` field containing the text content |`type`, `target_time`, `text` |
|`subtitle` |Overlay content |Subtitle, with the `text` field containing the URL of a subtitle file (such as an SRT file) |`type`, `target_time`, `text` |
|`effect` |Overlay content |Effect, with the effect defined by a filter in `extra` |`type`, `target_time` |
|`gaussian` |Special effect |Gaussian blur, which blurs the entire source |`type`, `target_time`, `source` |
|`text_roll` |Special effect |Scrolling text, suitable for promotional videos |`type`, `target_time`, `text` |

For the full list of fields supported by each element type, see [Create a multi-track editing task](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task?lang=en).

### Filter categories

A filter applies an effect to an element and is defined in the element's `extra` array. You can apply multiple filters to one element. Each filter uses `type` to identify the effect and includes fields specific to that filter type.

|Category |Filter (`type` value) |Description |Applicable element types |
|---|---|---|---|
|Timing and cropping |`trim` |Trimming, which extracts a segment from the source media |`video`, `audio` |
| |`crop` |Cropping, which selects a rectangular area of the frame |`video`, `image` |
| |`speed` |Playback speed adjustment, which changes the playback speed (range [0.1, 4]) |`video`, `audio` |
|Transformation and layout |`transform` |2D transformation, which controls the position, size, rotation, and opacity of the element on the canvas |`video`, `image`, `text` |
|Visual effects |`lut_filter` |Color filter, which applies a preset color\-grading effect |`video`, `image`, `effect` |
| |`effect_filter` |Visual effects, such as split\-screen layouts and mirroring |`video`, `image`, `effect` |
| |`equalizer` |Color adjustment, which controls brightness, saturation, and tone |`video`, `image` |
| |`delogo` |Localized blur, which blurs a specified area (often used to cover a logo) |`video`, `image` |
| |`gaussian` |Gaussian blur, which applies blur to the entire element or background |`video`, `image`, `gaussian` |
|Animation and transition |`transition` |Transition, which creates a transition between adjacent video elements on the same track |`video` |
| |`video_animation` |Video animation, which adds entrance, exit, or loop animations |`video`, `image` |
| |`text_animation` |Text animation, which adds entrance, exit, or loop animations to text |`text` |
|Audio processing |`a_fade` |Audio fade\-in and fade\-out |`audio`, `video` |
| |`a_volume` |Volume adjustment (`0` means muted) |`audio`, `video` |

For the full list of filter parameters and available resource IDs, see [Create a multi-track editing task](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task?lang=en) and the [Resource IDs](https://docs.byteplus.com/en/docs/25/123430#resource-ids) section at the end of this document.

### Track layout practices

Group elements by content type on separate tracks to create visual overlays and mix audio.

* Visual tracks: Contain visual elements such as `video`, `image`, `text`, and `effect`. Content on higher tracks is rendered over content on lower tracks. A typical layout is:

   * Track 0 (bottom layer): Place the main video clip or background image.

   * Track 1 (middle layer): Place picture\-in\-picture videos, stickers, or dynamic effects.

   * Track 2 (top layer): Place titles that appear over the entire composition or subtitles.

   * `video` and `image` elements can be placed on the same track.

   * A `subtitle` element must be on its own track, and the total number of subtitle tracks must not exceed 10.

* Audio tracks: Contain `audio` elements and the audio included in `video` elements. Audio from these tracks is mixed together. You can dedicate separate tracks to `audio` elements, such as one for background music throughout the video and another for narration or sound effects at specific times.

## Quick start: Render a video with styled text

This section walks you through the full asynchronous workflow by rendering a video with a styled text overlay.

### Prerequisites

* **Create an API key**: Before you start, go to the [API key management page](https://console.byteplus.com/imp/ai-mediakit/settings) in the AI MediaKit console to create an **AI MediaKit API key**.

* **Prepare media files**: Upload the video, audio, images, and other media you want to combine to a publicly accessible server, and obtain URLs that the API can access.

### Procedure

Multi\-track editing runs asynchronously. The workflow is as follows:

1. After you call `POST /api/v1/tools/multi-track-edit` to submit a task, the API returns a task ID (`task_id`).

2. You can poll the [Get task details API](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details?lang=en) to check the task status until `status` changes to `completed`, or use [event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification?lang=en) to automatically receive task status changes.

3. After the task is complete, obtain the output video download URL (`video_url`) from the `result` field in the response.

#### Step 1: Submit the multi\-track editing task

Call the [Create a multi-track editing task API](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task?lang=en). Use the following cURL command to submit a multi\-track editing task: the first track contains a video (0–5000 ms), and the second track adds a styled text overlay (0–3000 ms).

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
            "width": 1000, "height": 200, "pos_x": 40, "pos_y": 860
          }
        ]
      }
    ]
  ],
  "output": {
    "format": "mp4",
    "fps": 30
  }
}'
```

> **Note**

* > Replace `{Your_API_Key}` with your valid API key.

* > `track[][].source`: Replace it with your own media URL.

After the request succeeds, you receive a response that contains a `task_id`, as shown below. Save this ID to check the task status and retrieve the result.

```JSON
{
  "success": true,
  "task_id": "amk-tool-multi-track-edit-123456789",
  "request_id": "20260901130000ABCDEFG12345"
}
```

#### Step 2: Obtain the task result

The task takes time to process. To retrieve the final result, poll the [Get task details API](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details?lang=en) until the task status changes to `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```

> **Note**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task completes successfully, you receive the following response. `result.video_url` is the download URL of the output video (a signed URL valid for 24 hours, so download and save it promptly). The response also returns the total output duration (`duration`, in seconds) and the output resolution (`resolution`).

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

## Advanced usage

Use the following parameters to customize the output after completing the basic workflow.

### Control the output container and frame rate

Use the [output object](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task?lang=en) to control the output container format, frame rate, alpha channel, and inclusion or exclusion of audio and video. The following example shows how to export audio only as an MP3 file.

```JSON
{
    "track": [
        [
            {"type": "audio", "source": "https://example.com/bgm.mp3", "target_time": [0, 10000]}
        ]
    ],
    "output": {
        "format": "mp3",
        "disable_video": true
    }
}
```

### Customize the canvas

Use the `canvas` parameter to define the resolution, background color, and aspect ratio settings of the final output video:

* `canvas.width` and `canvas.height`: Specify the canvas width and height (in pixels, in the range [160, 8192]). Expressions are also supported (see [Example 7: Set the canvas dimensions using expressions](https://docs.byteplus.com/en/docs/25/123430#example-7-set-the-canvas-dimensions-using-expressions)).

* `canvas.background_color`: The canvas background color (hexadecimal RGBA format), such as `#000000FF`.

* Size the canvas by aspect ratio: Set `output.canvas_with_ratio=true` and use `canvas.long` (long edge), `canvas.short` (short edge, which takes precedence over `long`), `canvas.ratio` (such as `16:9`), and `canvas.index` (the index of the element whose orientation the canvas follows; `MAX` selects the source with the highest resolution).

* Match the highest input resolution: Set `output.canvas_with_max=true` to match the canvas to the highest resolution among the input sources.

Canvas resolution priority (from high to low): `canvas.width`/`canvas.height` (Integer) \> `output.canvas_with_max` \> `output.canvas_with_ratio` \> `canvas.width`/`canvas.height` (String expression).

The following example shows how to set a custom 1080x1920 canvas with a black background.

```JSON
{
    "track": [
        [
            {"type": "video", "source": "https://example.com/clip.mp4", "target_time": [0, 5000]}
        ]
    ],
    "canvas": {
        "width": 1080,
        "height": 1920,
        "background_color": "#000000FF"
    }
}
```

### Add AIGC metadata labels

To add compliance labels to generated content, you can provide AIGC metadata as a JSON\-encoded object string in the [extra_param.upload object](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task?lang=en). Its fields follow relevant regulations on labeling AI\-generated and synthetic content. Common fields include `Label`, `ContentProducer`, and `ProduceID`.

```JSON
{
    "track": [
        [
            {"type": "video", "source": "https://example.com/clip.mp4", "target_time": [0, 5000]}
        ]
    ],
    "extra_param": {
        "upload": {
            "aigc_meta": "{\"Label\":\"1\",\"ContentProducer\":\"multi-track-edit-test\",\"ProduceID\":\"produce-test-001\"}"
        }
    }
}
```

## Common scenario examples

The following examples illustrate common multi\-track editing workflows.

### Example 1: Join video clips with transitions

**Scenario**: Join separate video clips in sequence and add transitions for a smoother flow between clips.

**Key points**: The `transition` filter creates a transition between adjacent video elements, A and B, on the same track. Add it to the `extra` array of the first element, A. Depending on how you set `target_time` and the transition resource you select, there are two modes: non\-overlapping transitions and overlapping transitions.

* **Overlapping transition**: The two elements must overlap on the timeline. The transition takes place during that overlap. All transition types support this mode.

   * Implementation: Set the `target_time` intervals of A and B to overlap. The overlap should be at least as long as the transition's `duration`.

   * Example: The `target_time` of A is `[0, 5000]` and the `target_time` of B is `[4000, 9000]`, with a transition `duration` of `1000` set on A. The transition takes place within the `[4000, 5000]` interval.

   * Example code (overlapping transition): The following example overlaps two video clips by 1000 ms and applies the "Pinwheel" transition during the overlap.

   ```Bash
   curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
   -H 'Authorization: Bearer {Your_API_Key}' \
   -H 'Content-Type: application/json' \
   -d '{
     "canvas": {"width": 1280, "height": 720},
     "track": [
       [
         {
           "type": "video",
           "source": "https://example.com/landscape_video_1.mp4",
           "target_time": [0, 5000],
           "extra": [
             {
               "type": "transition",
               "source": "vcr://trdbp72171789718375533ep",
               "duration": 1000
             }
           ]
         },
         {
           "type": "video",
           "source": "https://example.com/landscape_video_2.mp4",
           "target_time": [4000, 9000]
         }
       ]
     ]
   }'
   ```

* **Non\-overlapping transition**: The two elements meet on the timeline without overlapping. The transition occurs at their boundary: the system automatically overlaps the end of element A and the beginning of element B to apply it.

   * Implementation: Set the end time of element A's `target_time` equal to the start time of element B's `target_time`.

   * Limit: This mode is supported only for transition resources marked "Yes" in the "Supports non\-overlapping transitions" column of the [Transition IDs](https://docs.byteplus.com/en/docs/25/123430#transition-ids) table. If you use this mode for an unsupported resource, the transition does not take effect.

   * Example: A is `[0, 5000]` and B is `[5000, 10000]`, with a non\-overlapping transition `duration` of `1000` set on A. During playback, A ends at `4500 ms`, B starts at `5500 ms`, and the transition plays during `[4500, 5500]`.

   * Example code: The following example joins two videos seamlessly using the "ColorPhase" transition.

   ```Bash
   curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
   -H 'Authorization: Bearer {Your_API_Key}' \
   -H 'Content-Type: application/json' \
   -d '{
     "canvas": {"width": 1280, "height": 720},
     "track": [
       [
         {
           "type": "video",
           "source": "https://example.com/landscape_video_1.mp4",
           "target_time": [0, 10000],
           "extra": [
             {
               "type": "transition",
               "source": "vcr://trdbp19521789718383868ep",
               "duration": 3000
             }
           ]
         },
         {
           "type": "video",
           "source": "https://example.com/landscape_video_2.mp4",
           "target_time": [10000, 20000]
         }
       ]
     ]
   }'
   ```

### Example 2: Combine selected segments from a video

**Scenario**: Extract highlights from different parts of a long video and combine them into a highlights video.

**Key points**:

* On the same track, create multiple `video` elements for the same source video.

* Each element uses the `trim` filter to specify the time interval to extract from the source video.

* The `target_time` of each element defines the new position of the extracted segment on the final timeline.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 720},
  "track": [
    [
      {
        "type": "video",
        "source": "https://example.com/long_video.mp4",
        "target_time": [0, 10000],
        "extra": [
          {"type": "trim", "start_time": 5000, "end_time": 15000}
        ]
      },
      {
        "type": "video",
        "source": "https://example.com/long_video.mp4",
        "target_time": [10000, 20000],
        "extra": [
          {"type": "trim", "start_time": 25000, "end_time": 35000}
        ]
      }
    ]
  ]
}'
```

### Example 3: Arrange videos in a split\-screen video wall

**Scenario**: Stack three separate videos vertically to create a single video at a higher resolution. This layout is useful for video walls and comparison displays.

**Key points**:

* Set the canvas size: Create a canvas that can accommodate the combined dimensions of all three videos. This example assumes that each source video is 1280×720, so the final canvas width is 1280 and the height is 720×3 = 2160.

* Use multiple tracks: Place each video element on a separate track.

* Precise positioning: Add a `transform` filter to each video and set its top\-left corner coordinates on the canvas using `pos_x` and `pos_y`.

* Time alignment: Use the same `target_time` for all video elements to ensure that they play simultaneously.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 2160},
  "track": [
    [
      {
        "type": "video", "source": "https://example.com/clip_1.mp4", "target_time": [0, 10000],
        "extra": [{"type": "transform", "width": 1280, "height": 720, "pos_x": 0, "pos_y": 0}]
      }
    ],
    [
      {
        "type": "video", "source": "https://example.com/clip_2.mp4", "target_time": [0, 10000],
        "extra": [{"type": "transform", "width": 1280, "height": 720, "pos_x": 0, "pos_y": 720}]
      }
    ],
    [
      {
        "type": "video", "source": "https://example.com/clip_3.mp4", "target_time": [0, 10000],
        "extra": [{"type": "transform", "width": 1280, "height": 720, "pos_x": 0, "pos_y": 1440}]
      }
    ]
  ]
}'
```

### Example 4: Picture\-in\-picture (small window overlay)

**Scenario**: Overlay a scaled\-down picture\-in\-picture video on top of the main video (such as a commentary window or two people in the same frame).

**Key points**:

* Place the main video on the bottom track (`track[0]`) to fill the entire canvas.

* Place the picture\-in\-picture video on the upper track (`track[1]`), use the `transform` filter to scale it down, and position it in a corner of the frame (the bottom\-right corner in this example).

* The upper track is rendered above the lower track, so the picture\-in\-picture is overlaid on top of the main video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 720},
  "track": [
    [
      {"type": "video", "source": "https://example.com/main_video.mp4", "target_time": [0, 10000]}
    ],
    [
      {
        "type": "video",
        "source": "https://example.com/pip_video.mp4",
        "target_time": [0, 10000],
        "extra": [
          {"type": "transform", "width": 400, "height": 225, "pos_x": 840, "pos_y": 455}
        ]
      }
    ]
  ]
}'
```

### Example 5: Add background music and a text title

**Scenario**: Add full\-length background music and a centered text title to a video.

**Key points**:

* Place the video, audio, and text on three separate tracks.

* The `target_time` of the audio element covers the entire video duration, and you can use the `a_volume` filter to lower the volume.

* Use the text element's `transform` filter to set its position and size on the canvas, and `align_type` to set its text alignment.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1920, "height": 1080},
  "track": [
    [
      {"type": "video", "source": "https://example.com/main_video.mp4", "target_time": [0, 10000]}
    ],
    [
      {
        "type": "audio",
        "source": "https://example.com/bgm.mp3",
        "target_time": [0, 10000],
        "extra": [{"type": "a_volume", "volume": 0.3}]
      }
    ],
    [
      {
        "type": "text",
        "text": "Our wonderful journey",
        "target_time": [1000, 9000],
        "font_type": "SY_Black",
        "font_size": 120,
        "font_color": "#FFFFFFFF",
        "align_type": 1,
        "extra": [
          {"type": "transform", "width": 1800, "height": 200, "pos_x": 60, "pos_y": 440}
        ]
      }
    ]
  ]
}'
```

### Example 6: Add a subtitle file and apply a filter

**Scenario**: Add an SRT subtitle file to a video and apply the "Friends" color filter to the entire video.

**Key points**:

* The subtitle element (`type: "subtitle"`) must be on its own track, and its `text` field contains the publicly accessible URL of the subtitle file.

* Add a `lut_filter` to the video element's `extra` array and set `source` to the filter ID.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 720},
  "track": [
    [
      {
        "type": "video",
        "source": "https://example.com/video_to_filter.mp4",
        "target_time": [0, 20000],
        "extra": [
          {"type": "lut_filter", "source": "vcr://trdbp45851789719754401ep", "intensity": 0.8, "target_time": [0, 20000]}
        ]
      }
    ],
    [
      {
        "type": "subtitle",
        "text": "https://example.com/subtitles/sample.srt",
        "target_time": [0, 20000],
        "font_type": "ALi_PuHui",
        "font_size": 60,
        "extra": [
          {"type": "transform", "width": 1200, "height": 150, "pos_x": 40, "pos_y": 550}
        ]
      }
    ]
  ]
}'
```

### Example 7: Set the canvas dimensions using expressions

**Scenario**: Automatically match the canvas dimensions to a specific element without entering a fixed resolution.

**Key points**: The `canvas.width` and `canvas.height` fields accept expressions that reference an element's dimensions. Use `$trackIndex|elementIndex.w` for width or `.h` for height. The following example matches the canvas dimensions to `track[0][0]`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "track": [
    [
      {"type": "video", "source": "https://example.com/clip.mp4", "target_time": [0, 5000]}
    ]
  ],
  "canvas": {
    "width": "$0|0.w",
    "height": "$0|0.h"
  }
}'
```

### Example 8: Add a Gaussian blur background

**Scenario**: Center a smaller video and give its background a Gaussian blur effect.

**Key points**: Add both the `transform` (positioning and scaling) and `gaussian` (background blur) filters to the `video` element. If the canvas resolution differs from the source resolution, the system automatically scales the source video while preserving its aspect ratio, crops it around the center, and uses a blurred version as the background.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 720},
  "track": [
    [
      {
        "type": "video",
        "source": "https://example.com/test.mp4",
        "target_time": [0, 10000],
        "extra": [
          {"type": "transform", "width": 640, "height": 360, "pos_x": 0, "pos_y": 0},
          {"type": "gaussian", "radius": 30, "sigma": 30, "target_time": [0, 10000]}
        ]
      }
    ]
  ]
}'
```

### Example 9: Apply Gaussian blur to an element

**Scenario**: Blur the entire element.

**Key points**: Use the `gaussian` element type and add the `gaussian` filter to it. Unlike Example 8, this method blurs the entire source specified by `source` rather than generating a blurred background.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 720},
  "track": [
    [
      {
        "type": "gaussian",
        "source": "https://example.com/test.mp4",
        "target_time": [0, 10000],
        "extra": [
          {"type": "transform", "width": 640, "height": 360, "pos_x": 0, "pos_y": 0},
          {"type": "gaussian", "radius": 30, "sigma": 30, "target_time": [0, 10000]}
        ]
      }
    ]
  ]
}'
```

### Example 10: Add entrance and exit animations to video and text

**Scenario**: Add entrance and exit animations to visual elements to make the visuals more engaging.

**Key points**:

* For video and image elements, add a `video_animation` filter and set `anim_res` to the video animation ID. Use `anim_start_time` and `anim_end_time` to define when the animation runs, relative to the start of the element, in milliseconds.

* For text elements, add a `text_animation` filter and configure the entrance (`anim_in_res` + `anim_in_duration`) and exit (`anim_out_res` + `anim_out_duration`) animations separately. The sum of the entrance and exit durations must be less than the text display duration.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/multi-track-edit' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "canvas": {"width": 1280, "height": 720},
  "track": [
    [
      {
        "type": "video",
        "source": "https://example.com/clip.mp4",
        "target_time": [0, 8000],
        "extra": [
          {"type": "video_animation", "anim_res": "vcr://trdbp70981790068967897ep", "anim_start_time": 0, "anim_end_time": 1000}
        ]
      }
    ],
    [
      {
        "type": "text",
        "text": "Highlights",
        "target_time": [1000, 7000],
        "font_type": "SY_Black",
        "font_size": 100,
        "font_color": "#FFFFFFFF",
        "align_type": 1,
        "extra": [
          {"type": "transform", "width": 1200, "height": 200, "pos_x": 40, "pos_y": 260},
          {"type": "text_animation", "anim_in_res": "vcr://trdbp71251789537944186ep", "anim_in_duration": 800, "anim_out_res": "vcr://trdbp55111789538006675ep", "anim_out_duration": 800}
        ]
      }
    ]
  ]
}'
```

## Reference

### Billing

Multi\-track editing is billed based on the output video duration, with a conversion factor applied according to the output resolution. For detailed billing rules and prices, see [Pricing](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-pricing?lang=en).

### Resource IDs

Use resource IDs to select preset color filters (`lut_filter`), visual effects (`effect_filter`), transitions (`transition`), video and text animations (`video_animation`/`text_animation`), styled text (`text_res`), and fonts (`font_type`).

#### Color filter IDs

Used for the `source` field of the `lut_filter` filter.

|Filter name |Filter ID |Sample image |Description |
|---|---|---|---|
|Friends |`vcr://trdbp45851789719754401ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/4a97a0bc-1964-40da-9de5-4a5c1fc623b0.gif) |A warm, retro filter with the look of classic American television. Suitable for lifestyle vlogs and videos about friendship. |
|Jeju |`vcr://trdbp45681789719788967ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/9bef76d7-a707-4630-9929-e46a88f2db3c.gif) |A fresh blue filter inspired by island scenery and travel on Jeju Island. Suitable for travel, landscape, and summer content. |
|Vintage |`vcr://trdbp73631789719756083ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/7c804bc2-956b-40ef-82a7-5a6beb6c914c.gif) |A nostalgic filter with a vintage film texture. Suitable for retro videos, stories about people and culture, and reminiscences. |
|GreenBeauty |`vcr://trdbp92751789719719795ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/279d747b-9776-4541-90c6-73405aa88031.gif) |A fresh green filter with a natural, vibrant look. Suitable for outdoor, plant, and healthy living content. |
|MUJI |`vcr://trdbp28821789719815042ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/5c43a2c4-84f3-446b-83ab-7dc227f583dc.gif) |A minimalist Japanese\-style filter with subtle, low\-saturation colors. Suitable for lifestyle, home, and artistic videos. |
|White |`vcr://trdbp25281789719816051ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/6e9d13d6-4fba-44ee-9336-20b47d9fefb9.gif) |A bright filter with a clean, clear look and light tones. Suitable for portrait, beauty, and fashion content. |
|LemonGreen |`vcr://trdbp18431789719716691ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/3f232bca-bc19-441d-b79b-131c3038a132.gif) |A lemon yellow and green filter with a refreshing summer look. Suitable for drinks, summer videos, and content with a fresh, light aesthetic. |
|Afternoon |`vcr://trdbp04041789719814183ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0c553648-9fde-4eb5-b262-2af20935059d.gif) |A warm yellow filter reminiscent of afternoon sunlight, with a relaxed, cozy atmosphere. Suitable for lifestyle, coffee, and leisure content. |
|Hong Kong |`vcr://trdbp27651789719752508ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d9177de4-131c-49f9-a85f-4d41957f91cc.gif) |A retro Hong Kong\-style filter with the feel of a neon\-lit city. Suitable for urban night scenes, retro videos, and Hong Kong\-inspired content. |
|Japanese |`vcr://trdbp93831789719631128ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/3a3655f8-9315-4e18-8aa6-0ffda2b489aa.gif) |The mapping to the existing preview is inferred and requires confirmation. |
|Tasty |`vcr://trdbp98221789719685529ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/ad342f29-850a-4088-b1c9-f90f52cf5118.gif) |A warm red filter that makes food look appetizing. Suitable for food videos, restaurant reviews, and mukbang content. |
|Sunset |`vcr://trdbp15011789719718845ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/fba67a90-33fa-4078-9cba-d9edeace61c0.gif) |A soft, romantic filter with the pink and purple glow of a sunset. Suitable for sunset footage, landscapes, and videos that convey emotion. |
|Flavorful |`vcr://trdbp78341789719683310ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/7d4cdb37-073d-42f7-8b78-40ea8f9e461b.gif) |A warm filter designed to bring out the texture and color of food. Suitable for cooking videos and restaurant reviews. |
|American |`vcr://trdbp66791789719756912ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/00743642-3aaa-40cb-a712-f958a62391de.gif) |An American retro\-style filter with a rich film texture. Suitable for travel videos, stories about people and culture, and retro content. |
|Spring |`vcr://trdbp46311789719720727ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/8fc4ca5e-a214-41cc-a4eb-088ce7961f94.gif) |A fresh, lively filter with springlike pink and green tones. Suitable for spring and flower content, and videos with a fresh, light aesthetic. |
|Lucidly |`vcr://trdbp66351789719789933ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/fa5c0cbd-5761-48e7-8217-e0ef2e37b227.gif) |A natural filter with a clean, bright look. Suitable for everyday videos, portraits, and recordings of daily life. |
|Cream |`vcr://trdbp69371789719784602ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/ccb84b74-6e09-48e1-b464-8822c9d99305.gif) |A soft, warm cream filter with a sweet, gentle look. Suitable for dessert, lifestyle, and softly styled content. |
|Nature |`vcr://trdbp88571789719817943ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/ee12d12d-ce70-4e1e-949a-0e40689d393b.gif) |A natural filter that faithfully reproduces the original colors. Suitable for landscapes, documentaries, and everyday videos. |
|FirstMeet |`vcr://trdbp99851789719785902ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/66deff6f-9ca2-42fd-aedb-21cc05423621.gif) |A fresh filter with soft, light pink tones that evoke first love. Suitable for videos about emotions and youth, and portrait content. |
|Vivid |`vcr://trdbp91441789719787049ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d91e7ee3-1de3-46b4-80f1-4addc6bda9ac.gif) |A highly saturated filter with rich, lively colors. Suitable for landscapes, travel, and energetic videos. |
|Warm food |`vcr://trdbp59121789719684297ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/45a264a5-cbdc-4100-b62e-6704b5316eeb.gif) |A warm food filter with a comforting look. Suitable for home cooking, food, and lifestyle content. |
|Miami |`vcr://trdbp92691789719755234ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f42091e2-2138-42c2-9ee6-e68e52b97105.gif) |A tropical seaside filter with contrasting blue and orange tones. Suitable for travel, vacation, and summer videos. |
|Childhood |`vcr://trdbp54761789719753416ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/ebc7cd6d-b9b8-4058-91ad-a827d2a310bc.gif) |A warm, nostalgic filter that evokes childhood memories. Suitable for videos about growing up, family, and reminiscences. |
|ShinyaShokudo |`vcr://trdbp56971789719686465ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0fbd3f0c-11c2-40e0-ae2c-64ddb6e2834c.gif) |A dark filter with warm lighting that evokes a late\-night diner. Suitable for food videos, night scenes, and videos that convey emotion. |
|Dreamland |`vcr://trdbp87181789719787996ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/7aa97076-8fd1-4881-ada3-3c97e8862949.gif) |A dreamy, soft\-focus filter with a hazy, poetic look. Suitable for ethereal imagery, videos that convey emotion, and atmospheric artistic content. |
|Walnut |`vcr://trdbp45911789719816963ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/15462426-bc3f-4d27-8793-f271890392ec.gif) |A warm brown filter with woody tones and a grounded, retro look. Suitable for home, coffee, and artistic videos. |
|Clear |`vcr://trdbp88691789719813304ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/012a5f69-f6e3-471e-a705-5149624f66b3.gif) |A clear, sharp filter that brings out fine detail. Suitable for product showcases, landscapes, and documentaries. |
|Kyoto |`vcr://trdbp76151789719717862ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/9079244c-11da-4f87-9782-4d1b41485c9b.gif) |An elegant, serene Japanese\-style filter. Suitable for travel videos, stories about people and culture, and Zen\-inspired content. |
|Sakura |`vcr://trdbp12421789719715677ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/b6132769-1098-409a-8e3d-27ae76499ec0.gif) |A romantic pink filter inspired by cherry blossoms in spring. Suitable for spring, portrait, and emotionally expressive content. |

#### Transition IDs

Used for the `source` field of the `transition` filter.

|Transition name |Transition ID |Supports non\-overlapping transitions |Sample image |Description |
|---|---|---|---|---|
|Pinwheel |`vcr://trdbp72171789718375533ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0021857c-229b-405d-9be7-47d30cfca436.gif) |Reveals the next clip from the center with a rotating pinwheel effect. Suitable for lively, dynamic scene transitions. |
|ColorPhase |`vcr://trdbp19521789718383868ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/44c7297d-a7ee-42b7-9374-f6895b16c080.gif) |A warm sunset gradient that creates a soft, romantic transition. Suitable for joining emotionally expressive videos and landscape footage. |
|MultiplyBlend |`vcr://trdbp84991789718376310ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/30d2e319-9050-49b4-9052-0bda3f078ded.gif) |Blends interwoven colors into a rich gradient transition. Suitable for trendy and artistic content. |
|Angular |`vcr://trdbp81391789718386095ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/19e43946-7d68-4998-905b-16652308a264.gif) |Reveals the next clip section by section, like a clock hand sweeping across the frame. Suitable for time\-themed and countdown videos. |
|Ripple |`vcr://trdbp21851789718374949ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/fa603d60-8637-4922-b691-3157898ae36d.gif) |Fades in the next clip through ripples spreading from a water drop. Suitable for transitions with a fresh, natural look. |
|Waterdrop |`vcr://trdbp82841789718373008ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/e01aa93e-d60f-4d2e-8eec-f97b49243245.gif) |Fades in the next clip through ripples spreading from a water drop. Suitable for transitions with a fresh, natural look. |
|Flyeye |`vcr://trdbp07411789718379578ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/a526d58b-9170-4a6c-8024-20cab2411982.gif) |Opens the frame from the center toward both sides, like an eye opening, to create a sense of focus and discovery. |
|CircleCrop |`vcr://trdbp27441789718385604ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/52fd9f99-3ecb-4158-b790-180db3c46084.gif) |Reveals the next frame with a circular wipe that expands from the center. Suitable for highlighting a subject or drawing attention to key details. |
|CircleOut |`vcr://trdbp18421789718384449ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d32d7412-f7e7-4dfe-a51a-6ffbe551202f.gif) |Alternates two circles across the frame to create a rhythmic transition. Suitable for fast\-paced, dynamic content. |
|Wind |`vcr://trdbp59961789718372439ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0d892dac-3031-4f68-97f8-dd7b52fe85d1.gif) |Moves the content across the frame as though blown by the wind. Suitable for nature footage, outdoor videos, and videos with flowing movement. |
|DirectionalWipe |`vcr://trdbp53811789718381391ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/b67e6ec6-da90-4da3-9dcf-7e501d42edc0.gif) |Reveals the next clip with a diagonal wipe. Creates a clean, crisp geometric transition. |
|Hexagonalize |`vcr://trdbp96011789718377990ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/79110c8e-52bb-4ac9-9965-3aef209855b0.gif) |Uses a hexagonal pattern that unfolds from the center as a polygonal transition mask. Suitable for technology content and geometric designs. |
|MaskTrans |`vcr://trdbp65961789718376928ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/fd8f7f49-4909-4e70-a163-6d96aaff9e18.gif) |Uses a shape mask to transition smoothly between two frames. Suitable for a wide range of uses. |
|Windowblinds |`vcr://trdbp58381789718371717ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f19c3a9f-9095-4e31-aa62-a061982bba76.gif) |Alternates strips horizontally or vertically, like window blinds opening and closing. Creates a neat, orderly visual rhythm. |
|GlitchDisplay |`vcr://trdbp73251789718379007ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/35153443-00b4-453a-b8b3-021fd6597d81.gif) |Shakes and displaces the frame and separates its colors before switching to the next clip. Suitable for trendy and cyberpunk styles. |
|RotateScaleFade |`vcr://trdbp79031789718374392ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/b7953ea5-3425-4755-9a6d-c89dc9cb40b4.gif) |Rotates and zooms the frame into the next clip for a dynamic perspective shift. Suitable for high\-impact transitions at a video's climax. |
|DreamZoom |`vcr://trdbp35621789718380141ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/42ef715d-827f-4d89-8775-f395d067b704.gif) |A soft, blurred zoom transition with a dreamy, hazy look. Suitable for reminiscences, dream sequences, and emotionally expressive content. |
|WipeRight |`vcr://trdbp87061789718371134ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/b7e0fedd-4fe1-4a1e-a214-786a4aea24c6.gif) |Flips the frame along its central axis, like turning a leaf, to create a lively 3D transition. |
|HeartOut |`vcr://trdbp00931789718378513ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/93af3aa1-1e93-4acb-8383-0012d64fd20b.gif) |Opens a heart\-shaped pattern from the center toward both sides. Suitable for romantic, heartwarming, and festive videos. |
|Cube |`vcr://trdbp27701789719582970ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/36c8cdbd-4745-46be-9355-3c430a82f6e9.gif) |Switches between two frames on adjacent faces of a rotating 3D cube. Suitable for technology and product showcases that emphasize depth. |
|Doorway |`vcr://trdbp20161789718380809ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/c4f7968a-a00b-4565-8cbb-9c16acda5b8b.gif) |Reveals the next frame from the center toward both sides, like double doors opening. Creates a ceremonial feel for openings and reveals. |
|Swap |`vcr://trdbp95371789718373869ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/b01a6a44-7193-4931-9b1d-fb641f968ed5.gif) |Flashes between multiple clips to create a rhythmic collage transition. Suitable for fast cuts, mashups, and music videos. |
|CrossWrap |`vcr://trdbp85951789718383251ep` |Yes |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/72c76ca3-c435-4b3d-bb32-6cd321242b86.gif) |Distorts the frame as though light were refracting through a lens before revealing the next frame. Creates visual tension and a distinctive, creative look. |
|CircleOpen |`vcr://trdbp50331789718385054ep` |No |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/cab17840-9be5-4085-a056-75d35d249292.gif) |Reveals the next frame through a circle that expands from the center. A classic, versatile transition that draws attention to the center. |

#### Visual effect IDs

Used for the `source` field of the `effect_filter` filter.

|Effect name |Effect ID |Sample image |Description |
|---|---|---|---|
|SixDivide |`vcr://trdbp55711789719857862ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/06148e47-9b95-4361-aae4-5ee64e5e2732.gif) |Divides the frame into a 2×3 grid with six panels displayed simultaneously. Suitable for comparing scenes and presenting highlights. |
|ThreeDivide |`vcr://trdbp04741789719858949ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/649f5473-cb9c-4bab-b7f8-f472252b5b87.gif) |Divides the frame into three vertical columns displayed simultaneously. Suitable for comparisons and storytelling from multiple perspectives. |
|Special_flipX |`vcr://trdbp30711789719856687ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/b08a092e-c5c3-498c-b26f-ab529361253a.gif) |Mirrors the frame horizontally to create a symmetrical composition. Suitable for creative, artistic, and dance videos. |
|NineDivide |`vcr://trdbp04021789719857331ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/15822b59-70bd-4d43-b7e2-5cf62b1d8225.gif) |Divides the frame into a 3×3 grid with nine panels displayed simultaneously. Suitable for highlights from multiple cameras or scenes. |
|TwoDivide |`vcr://trdbp07511789719859540ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/8550acb3-7bda-400c-98d6-e7b93178fc6a.gif) |Divides the frame into two columns displayed side by side. Suitable for before\-and\-after comparisons and dialogue between two people. |
|FourDivide |`vcr://trdbp27601789719858415ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/bbf25242-c3c9-4bd1-95ad-a47470e210d7.gif) |Divides the frame into a 2×2 grid with four panels displayed simultaneously. Suitable for content featuring multiple scenes or people. |

#### Video animation IDs

Used for the `anim_res` field of the `video_animation` filter.

**Entrance animations**

|Category |ID |Preview |
|---|---|---|
|CircleIn |`vcr://trdbp25291790068967616ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0492554d-c2b2-4d59-8e85-c624b83e1424.gif) |
|TranslateRight |`vcr://trdbp94001790068967684ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/4f937794-ae19-4a07-9c9f-ca52e23f72f6.gif) |
|TranslateLeft |`vcr://trdbp42611790068967733ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/949be699-6100-4158-9c58-f947d88b5004.gif) |
|TranslateBottom |`vcr://trdbp70851790068967774ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/a4ee8460-02ff-4ffb-8192-3f9d20335f6e.gif) |
|TranslateTop |`vcr://trdbp75391790068967804ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f5ee12ac-7669-4e66-8e90-ad70d16b219b.gif) |
|AppearSmall |`vcr://trdbp70461790068967836ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f88172b6-2406-4f12-a034-6df6268d144a.gif) |
|Dissolve |`vcr://trdbp02951790068967868ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/427e906d-3d8b-4fae-87f0-ccca23210099.gif) |
|Fade in |`vcr://trdbp70981790068967897ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c54e5aab0cc14edb939d84dffd7a020b~tplv-goo7wpa0wc-topic.webp) |
|AppearLarge |`vcr://trdbp67181790068967925ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/4c85330c-fb21-4a99-bd4f-8fc2eedcbc8f.gif) |
|BrushRight |`vcr://trdbp07131790068967954ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f033638e-bd1c-4bc7-9f45-0b48d40eccdd.gif) |
|BrushLeft |`vcr://trdbp19951790068967982ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/8bfa6455-6378-4bd7-b5d6-28eea356b026.gif) |
|BrushDown |`vcr://trdbp74171790068968011ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d28e2054-f048-4811-8abd-4fb4ff831e1a.gif) |
|BrushTop |`vcr://trdbp10791790068968037ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/adf53f08-4f1b-46b0-a066-a630f8ecd2e9.gif) |

**Exit animations**

|Category |ID |Preview |
|---|---|---|
|CircleOut |`vcr://trdbp13671790069002309ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/39bc5b67-ea89-48d1-a0b0-0872dad63583.gif) |
|TranslateOutLeft |`vcr://trdbp33691790069002387ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/99d46099-5711-4a22-92ea-8d0065c7de82.gif) |
|TranslateOutRight |`vcr://trdbp18471790069002423ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f5f8e930-cac5-4e42-92d5-ad1dbe8a4024.gif) |
|TranslateOutBottom |`vcr://trdbp75621790069002456ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/98b883eb-9a82-411a-b3e6-aff75dced29d.gif) |
|TranslateOutTop |`vcr://trdbp24521790069002487ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d1a3da08-f852-46d4-b012-3bf256c68c9c.gif) |
|SmallOut |`vcr://trdbp29061790069002517ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/a17e346f-7508-4dce-8dc8-6223c0e6e0e7.gif) |
|DissolveOut |`vcr://trdbp17591790069002547ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/3bdb5d00-0e0e-46ee-af53-e8a6a6768bec.gif) |
|FadeOut |`vcr://trdbp91311790069002574ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/8011d4b6-2e0d-4361-b25c-83e097edd363.gif) |
|BrushOutLeft |`vcr://trdbp11231790069002605ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f4bc5bca-778d-4652-a2b0-1353d3dc3a66.gif) |
|BrushOutRight |`vcr://trdbp32571790069002635ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/e7725cfe-48c3-4d32-84b5-b5c5a190a96a.gif) |
|BrushOutBottom |`vcr://trdbp93911790069002664ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/9d21ee16-a4a9-421d-9471-c4f80f883a8b.gif) |
|BrushOutTop |`vcr://trdbp14921790069002694ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/bf341ffd-453c-4fdb-998a-182b83d8eb79.gif) |

**Combined animations**

|Category |ID |Preview |
|---|---|---|
|FlipLoop |`vcr://trdbp42611790069063948ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/a566eaf6-981f-42a5-a38b-9d468719712e.gif) |

#### Text animation IDs

Used for the `anim_in_res` (entrance), `anim_out_res` (exit), and `anim_loop_res` (loop) fields of the `text_animation` filter.

**Entrance animations**

|Category |ID |Preview |
|---|---|---|
|Circle sweep in |`vcr://trdbp22531789537937746ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/fa7febfe-4a75-4415-81be-a34d7484547c.gif) |
|Dissolve in |`vcr://trdbp14761789537938823ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/99d2b424-53b6-412b-8970-225d0040a871.gif) |
|Wipe right in |`vcr://trdbp95291789537939867ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/c19c3f14-ac93-4b40-858a-be9e15b0446a.gif) |
|Wipe left in |`vcr://trdbp34041789537940393ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0ccf431e-9310-476d-8592-5be3d459d400.gif) |
|Wipe down in |`vcr://trdbp06261789537940928ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/9bd8b47c-9087-41ea-a577-6a8c6d1b37b4.gif) |
|Wipe up in |`vcr://trdbp54561789537941632ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/67d77666-9097-49ea-9c73-c9ecd67201ca.gif) |
|Slide in left |`vcr://trdbp86581789537942171ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/2e01a113-d3d4-4011-bab1-ceebba50a1df.gif) |
|Slide in right |`vcr://trdbp14081789537942651ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/68700e96-53aa-46f3-b9a3-7aba089c6efb.gif) |
|Slide in down |`vcr://trdbp57761789537943150ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/8e9c33d7-48bc-4698-8101-04a66ecaf77c.gif) |
|Slide in up |`vcr://trdbp70191789537943651ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/9506dbea-e22a-4584-b3c7-139d6ab8cf2b.gif) |
|Fade in |`vcr://trdbp71251789537944186ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0061ad2e-8284-49fd-bd93-760e4cd3f66b.gif) |
|Zoom in |`vcr://trdbp74821789537944684ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/1641aff8-a8c7-42df-a866-f79ffde63154.gif) |
|Feather wipe down in |`vcr://trdbp97581789537945218ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/dda3c874-a272-464c-8e43-6f99243d2a01.gif) |
|Feather wipe left in |`vcr://trdbp52641789537945727ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/cee2b053-570a-4766-ad82-9386283dde45.gif) |
|Feather wipe up in |`vcr://trdbp05821789537946211ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/da589739-9051-4e18-8e56-850991d002cc.gif) |
|Feather wipe right in |`vcr://trdbp97081789537946676ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/fca3b9c4-50ed-488d-a368-1e4298e2aa0f.gif) |

**Exit animations**

|Category |ID |Preview |
|---|---|---|
|Wipe right out |`vcr://trdbp38121789538006067ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/20e8ac98-9db5-4af1-bd5b-5af8aa368e05.gif) |
|Wipe left out |`vcr://trdbp55111789538006675ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d466b40c-876b-4069-b364-e9f7470993dc.gif) |
|Wipe down out |`vcr://trdbp39231789538007257ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/37d2216c-a93e-4691-8284-8d48d624b73c.gif) |
|Wipe up out |`vcr://trdbp51001789538007813ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/3465387c-2f22-46ec-9188-89a9de7df7df.gif) |
|Fade out |`vcr://trdbp57811789538008332ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/871f0fae-1a0e-4621-aae3-4b1fe3cd1653.gif) |
|Circle sweep out |`vcr://trdbp01981789538008802ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d4864fcf-4adb-418d-9872-f14baa46110a.gif) |
|Dissolve out |`vcr://trdbp47671789538009794ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/02ecfce3-1d42-4b89-a730-6237da543971.gif) |
|Zoom out |`vcr://trdbp16671789538010956ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/f3a6a19b-b2a9-437a-93c0-281c0f476fd8.gif) |
|Slide out right |`vcr://trdbp23331789538011491ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/728d8705-6fcc-45c1-ae51-d1c325fb6630.gif) |
|Slide out left |`vcr://trdbp00361789538012086ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/efee3214-6319-4010-bc01-be7df00c4b4e.gif) |
|Slide out down |`vcr://trdbp00361789538012542ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/47617c39-269e-4660-a5cb-fa4d533eaf46.gif) |
|Slide out up |`vcr://trdbp91011789538013749ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/9ac0b8f6-b378-40bb-a126-770033e8c301.gif) |
|Feather wipe down out |`vcr://trdbp08081789538003975ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/d0ba0ba3-cb5f-4050-b8f4-0d61a69e05bb.gif) |
|Feather wipe left out |`vcr://trdbp20421789538004465ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/2e61e24f-e609-4d45-90ec-e437a407e6e5.gif) |
|Feather wipe right out |`vcr://trdbp89951789538005002ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/0baa205c-5516-4732-80f2-2a60c86a87f2.gif) |
|Feather wipe up out |`vcr://trdbp27041789538005503ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/c2e2fb47-2e2b-4a19-a22f-6b46b5f9d5c0.gif) |

**Loop animations**

|Category |ID |Preview |
|---|---|---|
|Wave |`vcr://trdbp16281789538042263ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/a7f1ac54-d537-440d-8e06-803571725c47.gif) |
|Flip |`vcr://trdbp09911789538043368ep` |![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/nupfupfups/221dfe42-f034-4585-8837-6ba791d07b82.gif) |

#### Font IDs

Used for the `font_type` field of text/subtitle elements. To use a custom font instead of a preset font ID, set `font_type` to the publicly accessible URL of a TTF or OTF font file.

A commercial license is not included for FounderType (FZ) fonts. To use these fonts commercially, you must obtain a license directly from FounderType. The other fonts listed here are open source and can be used commercially.

|Text name |Text ID |Preview |
|---|---|---|
|Source Han Serif |`vcr://trdbp49741789537771550ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad499cafac924910b425a0438caad99e~tplv-goo7wpa0wc-raw.image) |
|Roboto |`vcr://trdbp81651789537770822ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cee06ba7287f42eb87ba5ed7270e0c0d~tplv-goo7wpa0wc-raw.image) |
|OPPO Sans |`vcr://trdbp96821789537769343ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1955a1aad342188a415eeafe13b008~tplv-goo7wpa0wc-raw.image) |
|Montserrat |`vcr://trdbp14651789537768378ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fcb95540aa14e438f7b252ac0e573c7~tplv-goo7wpa0wc-raw.image) |
|Inter |`vcr://trdbp18621789537767269ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/571540010df74d439f368df4b7bf91fb~tplv-goo7wpa0wc-raw.image) |

#### Styled text IDs

Used for the `text_res` field of text elements.

|Styled text name |Styled text ID |Sample image |
|---|---|---|
|Green glow |`vcr://trdbp90451789537637180ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1abfa1cfd7dc4b6e8766b7ec7896c367~tplv-goo7wpa0wc-topic.webp) |
|Gradient shadow |`vcr://trdbp94701789537633732ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b98eb4d1623b47b0ba8c379b7c275145~tplv-goo7wpa0wc-topic.webp) |
|Galaxy |`vcr://trdbp31961789537632309ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a3d1a1572c24e508c6324180cfdd9b8~tplv-goo7wpa0wc-topic.webp) |
|Blue glow |`vcr://trdbp07251789537630680ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c24b7d2c8f7441ca96d1b2120d7913c5~tplv-goo7wpa0wc-topic.webp) |
|Blue shadow glow |`vcr://trdbp61701789537629477ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f4f86fc1b22462a97797762517ade6f~tplv-goo7wpa0wc-topic.webp) |
|ByteDance |`vcr://trdbp06811789537628112ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dee4a8784aa4163a22a1678aeb13b2d~tplv-goo7wpa0wc-topic.webp) |
|Orange ring |`vcr://trdbp28491789537626951ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99fa5449823941b5b1d3fa92714037aa~tplv-goo7wpa0wc-topic.webp) |
|Rainbow |`vcr://trdbp71781789537625748ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/236012b5fdcd43b38ee3fdb00de6aca7~tplv-goo7wpa0wc-topic.webp) |
|Sunset |`vcr://trdbp06751789537624335ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4d30a445aa3463bb2e71f13a66656fc~tplv-goo7wpa0wc-topic.webp) |
|Yellow white pop |`vcr://trdbp14001789537623015ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/221da5b00c6649d48f859851c5d7d325~tplv-goo7wpa0wc-topic.webp) |
|Yellow purple 3D |`vcr://trdbp90981789537621415ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/238b2b06c8624f00b60d118a2c6831ce~tplv-goo7wpa0wc-topic.webp) |
|Basic text |`vcr://trdbp80031789537572061ep` |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0f07c89158143af9997f95ed0385cb7~tplv-goo7wpa0wc-topic.webp) |

## Related APIs

* [Create a multi-track editing task](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-multi-track-editing-task?lang=en)

* [Get task details API](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details?lang=en)

* [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification?lang=en)
