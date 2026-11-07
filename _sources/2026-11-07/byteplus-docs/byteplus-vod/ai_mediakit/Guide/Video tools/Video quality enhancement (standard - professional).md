---
title: "Video quality enhancement (standard/professional)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-quality-enhancement"
---

To automatically improve video quality for scenarios like AIGC, UGC, and old film restoration, you can use the Al MediaKit Video Enhancement tool. It leverages over 30 Al algorithms, including intelligent super\-resolution, frame interpolation, and color enhancement. This guide provides a quickstart to enhance a 720p video to 1080p, explains how to retrieve results via polling orcallbacks, and details the tool's core capabilities and application scenarios.

## Quickstart: Enhance an AI\-generated video to 1080p

This section demonstrates how to use the Standard version of the tool to enhance a low\-resolution (720p) AI\-generated video to 1080p.

### Prerequisites

* Obtain an API key: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your AI MediaKit API Key, which is used for authentication in media processing.

* Prepare a video file: Have a video file ready for enhancement, accessible via a public HTTP/HTTPS URL. If you don't have a video yet, you can refer to the [BytePlus Model Ark video generation tutorial](https://docs.byteplus.com/en/docs/ModelArk/doubao-seedance-2-5) to generate one and obtain its URL.

### Procedure

Video enhancement is an asynchronous task:

1. Call `POST /api/v1/tools/enhance-video` and get a `task_id` for querying.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task status is `completed`, the download URL for the processed video is available in the `result.video_url` field.

#### Step 1: Submit the task

You need to call the [Create a video quality enhancement task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-task) API. You can copy the following cURL command to submit it directly.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://vod-ai-test.bytepluses.com/demo/demo_video_720p.mp4",
  "scene": "aigc",
  "resolution": "1080p"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > The `--data` part is the JSON request body. You can modify its key parameters to customize your video.

   * > `video_url`: Replace it with your own video URL.

   * > `scene`: Specify the scene as `"aigc"` to get optimal results for this scenario.

Upon successful submission, you will receive a response containing a `task_id`. Save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-1703200",
  "request_id": "20260415150000F6DE4C24A6A0D94B7FF1"
}
```

#### Step 2: Get the result

Video enhancement is a computationally intensive task and requires some processing time. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task is successfully completed, you will receive the following response. The result object contains the output details. You can get the download URL of the enhanced video from its `video_url` field. By default, the output is an **MP4** file, and the URL is valid for **24 hours**.

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-video-1755136",
    "task_type": "enhance-video",
    "status": "completed",
    "result": {
        "duration": 5.967,
        "fps": 30.168,
        "resolution": "1080p",
        "tool_version": "standard",
        "video_url": "https://example.com/enhanced_video.mp4"
    },
    "expires_at": 1775960452,
    "created_at": 1775787510,
    "finished_at": 1775787652,
    "request_id": "20260410102611A2F6BCCB40A5B534A302"
}
```

## Advanced usage

After completing the quickstart, you can use more parameters to customize the video enhancement effect to meet more complex business needs.

### How it works

The Video Enhancement tool's workflow follows an "analyze\-decide\-execute" process. It not only applies a series of independent algorithms but also dynamically selects appropriate enhancement strategies through a deep understanding of the video content.

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/11590f9702b64caeb21abb1c1bbbf5ff)

Its core process includes the following four key stages:

1. **Intelligent analysis**: The system first performs shot\-level segmentation on the video and then conducts deep content understanding and technical diagnosis for each shot. This stage extracts dozens of features, including:

   * **Content features**: Identifies faces, main subjects, scene types (indoor/outdoor, day/night).

   * **Quality features**: Detects clarity, color saturation, noise level, compression artifacts.

2. **Strategy generation**: Based on the analysis results from the previous step and combined with your business intent specified through the `scene` or `tool_version` parameters, the system dynamically generates an appropriate combination of operators from its library of over 30 atomic algorithms.

3. **Video enhancement**: In this stage, the system executes the generated strategy to perform pixel\-level fine\-grained processing on the video. This includes, but is not limited to, intelligent super\-resolution, intelligent frame interpolation, video denoising, color enhancement, and adaptive sharpening.

4. **Quality monitoring and encoding**: The final stage includes quality monitoring and encoding. An integrated image quality assessment (IQA) algorithm evaluates the enhanced video to ensure a high\-quality result before encoding.

### Versions and scenes

You can specify a preset video enhancement strategy by setting the `tool_version` and `scene` parameters when submitting a task.

#### Versions

Video Enhancement offers two versions. Choose a version based on your quality requirements and budget.

|Feature |Standard version |Professional version |
|---|---|---|
|Positioning |Balances speed and quality (cost\-effective), meeting quality requirements for mainstream playback platforms. |Powered by large\-model\-driven restoration for cinematic\-grade image quality. This tier requires a longer processing time. It provides three versions for the General, UGC short video, AIGC content, and Short drama scenarios, while Classic film restoration uses a dedicated film restoration template. |
|Algorithm density |10+ built\-in common algorithms |30+ built\-in deep AI algorithms |
|Estimated processing time |A 1\-minute video is expected to take around **6 to 10 minutes** to process. |A 1\-minute video is expected to take **25 to 60 minutes** to process, depending on the output resolution. See the [Processing time estimation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement#a524cfcf) section below for details. |
|Cost |Lower price. |**10 times** the price of the Standard version |

Suppose you need to process a 1\-minute video with an output specification of 1080p, 30fps.

* **Choose Standard version:**

   * **Time**: Expected wait time is approximately 6 to 10 minutes.

   * **Cost**: 1 minute × 2 (coefficient) × $0.2066 = $0.4132.

* **Choose Professional version:**

   * **Time**: Since the output is 1080p, this task uses the Pro \- Medium tier. The expected wait time is approximately 25 minutes.

   * **Cost**: 1 minute × 20 (coefficient) × $0.2066 = $4.132.

#### Scenes

The Video Enhancement tool provides preset optimization templates for different scenarios. You can specify the corresponding scene via the `scene` parameter when submitting a task.

|Scene |`scene` value |Description and example |
|---|---|---|
|AIGC |`aigc` |Performs super\-resolution on low\-resolution videos generated by large models, bringing them to 2K or 4K resolution while redrawing details.<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/531067fa6e8b4e14a7c975dd6cd878ad)<br> |
|Short\-form drama |`short_series` |Enhances human figures and strengthens details in dramas, comprehensively improving visual expressiveness and immersion.<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d025f7fbddde465987f38ce93fb6e97d)<br> |
|UGC short video |`ugc` |Repairs quality degradation such as blurriness, blocking artifacts, and color banding that occur during multiple compressions and transmissions of short videos.<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d419cdbbdd8449d1885bcd970726b7f3)<br> |
|Classic film restoration |`old_film` |Repairs various flaws in old films, including motion\-compensated temporal denoising, scratch removal, flicker elimination, and color cast correction.<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ffd602807d5749da9cd5983632a32fd1)<br> |

#### Professional version tiers (Medium/Premium/Ultimate)

When you select the Professional version for `aigc`, `short_series`, `ugc`, or `general` scenes, one of the following tiers is automatically used based on your specified output resolution. Higher tiers use more advanced algorithms, resulting in superior quality but longer processing times and higher costs.

|**Pro version** |**Output resolution** |**Description** |
|---|---|---|
|Medium |1080p and below |Enhances low\-resolution or blurred videos for clear HD viewing. It uses a balanced combination of enhancement algorithms for fine textures, distant scenes, small text, and complex materials, prioritizing faster processing over maximum detail restoration. It is suitable for mobile viewing and regular playback. |
|Premium |2K |Produces a more natural and stable image with finer detail restoration. It better preserves facial features, clothing textures, and architectural lines; reduces compression blocks, blurred edges, and low\-bitrate artifacts; and improves motion texture stability without excessive sharpening. It is suitable for large\-screen and high\-definition playback. |
|Ultimate |4K and above |Provides ultra\-high\-definition output with maximum texture consistency. It preserves complex textures and the structure of distant or small objects, and improves edge, layer, and motion continuity on large screens. It is suitable for ultra\-high\-definition output, cinema\-grade large\-screen playback, and premium film restoration. |

The following demo compares outputs processed by the Premium and Ultimate versions.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828071236-1774335119119.png)

#### Professional version for Classic film restoration

When you select the **Classic film restoration** scene and the **Professional** version, a dedicated restoration template is used. This template integrates super\-resolution, intelligent denoising, deblurring, and color reconstruction into a unified AI workflow. It analyzes and reconstructs degradation at the content level, preserving the authentic texture of archival footage while restoring low\-resolution, noisy, or faded source material to clear, stable, richly layered, 4K\-quality visuals.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260831075847-638485005482.png)

#### Example: Enhance a video using the Professional version

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/old_film.mp4",
  "tool_version": "professional",
  "resolution": "4k"
}'
```

Since the output resolution is set to `4k`, this task will use the **Ultimate** tier of the Professional version.

### Configure enhancement style

You can control the overall style of the video enhancement using the `enhance_style` parameter, which is supported by both Standard and Professional versions.

* `hd` (Default): High Definition. Provides a moderate enhancement strength, resulting in a sharp and clear image.

* `natural`: Natural. Reduces the enhancement intensity for fewer sharpening artifacts and a more natural\-looking image. This is suitable for scenarios where a realistic texture is preferred and sensitivity to "AI look" or sharpening artifacts is high.

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ab250572399143498da0b346c2d7e9f8)

#### Example: Enhance a video using the natural style

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source.mp4",
  "resolution": "1080p",
  "enhance_style": "natural"
}'
```

### Configure output resolution

AI MediaKit provides two mutually exclusive ways to define the output resolution.

|Method |Parameter |Description |
|---|---|---|
|Specify resolution level |`resolution` |Suitable for standard distribution scenarios (such as `720p`, `1080p`, `4k`, `6k`, `8k`, up to `8k`). The system will automatically scale the video to the preset specification. |
|Short\-side pixel limit |`resolution_limit` |Suitable for engineering scenarios with precise requirements for output dimensions. The system will lock the video's **short\-side pixel value** to the set value (range: `[128, 4320]`) and scale it proportionally while maintaining the original aspect ratio. For example, if the original video is 640x480 (4:3) and `resolution_limit` is set to 720, the output video's short side will be upscaled to 720, and the width will be scaled proportionally to 960. |

#### Example: Lock the short side to 720 pixels

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source.mp4",
  "resolution_limit": 720
}'
```

### Configure output frame rate

You can use the `fps` parameter to adjust the video's frame rate (up to 120 fps), enabling intelligent frame interpolation for smoother motion.

* **Default behavior**: If the `fps` parameter is not specified, the output video will maintain the same frame rate as the original source.

* **Configuration advice**: If the target frame rate is higher than the original, the system will automatically trigger the AI intelligent frame interpolation algorithm. To ensure natural\-looking motion and manage processing costs, it is recommended that the output frame rate not exceed 4 times the original frame rate.

#### Example: Intelligently interpolate a video to 60fps

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source.mp4",
  "fps": 60
}'
```

### Configure output bitrate

The output bitrate determines the video's visual quality and final file size. AI MediaKit provides two methods for control.

|Method |Parameter |Description |
|---|---|---|
|Bitrate level |`bitrate_level` |Controls the target average bitrate using a preset level. Options: low, medium (default and recommended), high. The actual bitrate is automatically calculated based on the target resolution and frame rate. For the specific bitrates for each level, refer to [Bitrate reference](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-task#63decc4e). |
|Precise bitrate |`bitrate` |Directly specifies the target average bitrate in kbps. The value must be within the range of [10, 150000]. This is suitable for engineering scenarios requiring precise bitrate control. When this parameter is not set, the bitrate is determined by bitrate_level, resolution, and frame rate. |

#### Example: Specify the output bitrate as 8000 kbps

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source.mp4",
  "resolution": "1080p",
  "bitrate": 8000
}'
```

### Configure advanced color and encoding (Professional version only)

For Professional version enhancement tasks, you can perform lower\-level color and encoding control to meet the needs of professional post\-production, theatrical release, or high\-quality streaming distribution. This process is typically configured in a progressive sequence: first determine the required **bit depth**, then decide whether to enable **HDR dynamic range**, and finally match the **codec and container** that support these features; or, for the highest level of production, directly enable **ultimate lossless output**.

#### Bit depth selection

Bit depth, also known as color depth, refers to the number of binary bits used to represent a single color channel (e.g., R/G/B) for each pixel. It determines how many distinct color transitions the image can display and is a key prerequisite for HDR video. You can specify this via the `bit_depth` parameter.

Higher bit depths provide extremely smooth color transitions, effectively eliminating or reducing "color banding" that often occurs in large areas of solid color or gradients (such as skies or underwater scenes).

* `8` (Default): 8\-bit depth. Each color channel has 256 brightness levels. Highly compatible with small file sizes, but cannot represent HDR. Suitable for standard distribution such as TV broadcasts and social media.

* `10` (Recommended): 10\-bit depth. Each color channel has 1,024 brightness levels. Eliminates sky banding and supports HDR. It is currently the mainstream standard for 4K Blu\-ray and high\-quality global content distribution.

* `12`: 12\-bit depth. Each color channel has 4,096 brightness levels. Provides ultimate latitude for post\-production color grading and dynamic brightness adjustment. Suitable for film masters and commercial advertisements.

* `16`: 16\-bit depth. Each color channel has 65,536 brightness levels. Considered "data asset" grade, used for extremely precise optical compositing (e.g., VFX). At this level, the tool limits input video to 40 seconds, the bitrate is automatically determined, and tasks are processed serially.

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0530c2a6645f4dda87ccdd422780e843)

#### Dynamic range configuration (SDR / HDR)

After determining the bit depth, you can control the brightness detail and color richness of the output video via the `dynamic_range` parameter.

* `sdr` (Default): Outputs Standard Dynamic Range video. If you only need conventional HD quality, keep the default; it offers maximum playback compatibility.

* `hdr`: If you want to enhance the visual impact of your video by converting standard SDR video into HDR video with stronger contrast and more vivid colors (using the HLG standard), set this to `hdr`.

**Note**: Enabling HDR mode requires an effective bit depth of `10`, `12`, or `16`. Additionally, if you subsequently set `codec` to `exr`, the system forces HDR output, and this parameter configuration will not take effect.

#### Bit depth, codec, and container matching

Different codecs (`codec`) have varying support for bit depth and container formats. When specifying a `codec`, ensure it forms a valid combination with your chosen `bit_depth`. If you specify only the bit depth without a codec, the system automatically selects an appropriate default codec (h264 for 8\-bit, h265 for 10/12\-bit, ffv1 for 16\-bit).

|Codec (`codec`) |Bit depth (`bit_depth`) |Output container |Description |
|---|---|---|---|
|`h264` |`8` |MP4 |Strongest compatibility. Suitable for standard distribution such as TV broadcasts, social media, and web videos. |
|`h265` |`8`, `10`, `12` |MP4 |Mainstream HD codec. 10\-bit supports HDR and is the mainstream standard for premium global content distribution; 12\-bit provides greater latitude for color grading. |
|`prores` |`10` |MOV |Apple ProRes, output with 10\-bit, 4:2:2 pixel format. Visually lossless, uses intra\-frame compression, and can carry HDR metadata. A mainstream intermediate format for film post\-production color grading and editing. |
|`ffv1` |`16` |MOV |Lossless codec that fully preserves the color data of every frame. Used for extremely precise optical compositing and master archiving. |
|`exr` |`16` |EXR (image sequence) |16\-bit half\-float OpenEXR output. The output is an image sequence. |

> **NOTE**

> The `prores`, `ffv1`, and `exr` codecs do not support a specified bitrate; the `bitrate` and `bitrate_level` parameters do not take effect.

#### Ultimate lossless output (GBR 16\-bit)

If you are dealing with professional color grading, optical compositing, or high\-quality master archiving scenarios with ultimate lossless requirements, you can configure this directly via the `pix_fmt` parameter.

Currently, setting this to `gbrp16le` is supported, representing a lossless combination of the GBR color space and 16\-bit color depth, which fully preserves the color data of every frame. When this format is configured, the system automatically forces `codec` to `ffv1` and `bit_depth` to `16` to generate a MOV file; you do not need to redundantly configure the aforementioned parameters.

**Note**: The output file generated in this format is extremely large and not suitable for direct streaming distribution. The input video duration must not exceed 40 seconds. Please plan your storage capacity in advance and verify that your downstream editing/color grading software supports MOV, FFV1, and GBR 16\-bit formats.

#### Configuration examples

**Example 1: Output a 10\-bit video using the Professional version**

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
    "video_url": "https://example.com/source.mp4",
    "tool_version": "professional",
    "resolution": "4k",
    "bit_depth": 10
}'
```

**Example 2: Output a lossless GBR 16\-bit HLG HDR video**

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source.mp4",
  "tool_version": "professional",
  "pix_fmt": "gbrp16le",
  "dynamic_range": "hdr"
}'
```

> This request automatically sets `codec` to `ffv1` and `bit_depth` to `16` without extra declaration.

#### Considerations for high bit depth

* **Compatibility and playback environment verification**: 12\-bit and 16\-bit videos contain a vast amount of color data, far exceeding the decoding and rendering capabilities of standard players and operating systems (like the SDR desktop environment in Windows). Direct playback in an incompatible environment will not only fail to show the enhanced effect but may also lead to severe color distortion (such as washed\-out or incorrect colors). Therefore, to accurately assess the enhancement, you must import the output video file into professional post\-production software (like DaVinci Resolve or Premiere Pro) and view it on a professionally calibrated, color\-managed monitor. For HDR videos, an HLG HDR\-capable display is also required to accurately render brightness and detail.

* **Output format and precision retention**: Output precision depends on a valid bit depth, codec, and container combination. H.265 can produce 12\-bit MP4 output, while 16\-bit output can use FFV1/MOV or an EXR image sequence. If your workflow requires strict end\-to\-end GBR 16\-bit precision, use `pix_fmt=gbrp16le` and first test a small sample to verify that downstream software supports the corresponding formats.

* **Resource consumption and storage planning**: Higher bit depths exponentially increase file size and processing time. 16\-bit tasks, in particular, generate enormous amounts of data, which not only significantly extends processing time but also places high demands on subsequent storage, transfer, and editing. When processing large files, it is recommended to plan your storage space in advance and use high\-performance drives (like NVMe SSDs) to ensure a smooth workflow.

## References

### Pricing

Video Enhancement is billed on a pay\-as\-you\-go basis. The cost is calculated based on your selected **version** (Standard/Professional), **output resolution**, and **output frame rate**. For detailed billing rules and examples, see [Video quality enhancement pricing (standard and pro)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#cb99c95d).

### Processing time estimation

Since video enhancement involves deep learning model inference, processing time is typically longer than the video's duration. You can estimate the wait time using the **RTF (Real\-Time Factor)** , where:

Estimated processing time = Video duration × RTF

The RTF varies based on the tool version and the video's duration. The following values are for reference.

|**Tool version** |**Condition** |**RTF** |**Processing time estimation** |
|---|---|---|---|
|Standard |Video duration \> 20s |6–10 |A 1\-minute video is expected to take around **6 to 10 minutes** to process. |
||Video duration ≤ 20s |≈22 |A 10\-second video is expected to take around **220 seconds** (about 3.7 minutes) to process. |
|Pro \- Medium |Output resolution ≤ 1080p |≈25 |A 1\-minute video is expected to take around **25 minutes** to process. |
|Pro \- Premium |Output resolution = 2K |≈40 |A 1\-minute video is expected to take around **40 minutes** to process. |
|Pro \- Ultimate |Output resolution ≥ 4K |≈60 |A 1\-minute video is expected to take around **60 minutes** (1 hour) to process. |

The following image shows processing time examples for the Standard and Professional versions:

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/28203d515fe54566937e923be365b5a4)

> **INFO**

> The actual processing time is also affected by the input video's resolution, bitrate, and the current system queue status. It is recommended to configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) in a production environment to receive completion notifications in real time.

### Limits

|Limit item |Description |
|---|---|
|Input video limits |* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* File size: The maximum recommended size for a single input file is 10 GB.<br><br>* Input video resolution: Supports up to 2K. |
|Concurrency limit |By default, the maximum number of concurrent processing tasks for each account is **20**. New tasks submitted beyond this limit will be automatically queued. |

## Related APIs

* [Create a video quality enhancement task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
