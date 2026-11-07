---
title: "Video enhancement overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-enhancement"
---

Video enhancement (vCube) is an AI\-driven solution for deep video quality optimization. It provides preset templates for five core scenarios: **general content**, **UGC short videos**, **AIGC content**, **short dramas**, and **classic film restoration**.

By intelligently analyzing video content and identifying issues like compression artifacts and color distortion, the feature adaptively applies the optimal processing strategy. This ensures that videos deliver a clearer, more vibrant visual experience, even at the same bitrate.

> **Try it online**

> You can preview video enhancement effects with sample videos or your own input in the [Video enhancement demo](https://demo.byteplus.com/aiexp/video-enhance).

## How to use video enhancement

Choose a guide based on how you want to submit and manage enhancement tasks.

|Guide |What you can do |
|---|---|
|[Using the console](https://docs.byteplus.com/docs/byteplus-vod/enhancing_video_quality_via_console) |Configure an enhancement template, trigger a task, and view the results in the BytePlus VOD console. |
|[Using the OpenAPI](https://docs.byteplus.com/docs/byteplus-vod/vCube_enhancement_use_cases) |Submit enhancement tasks programmatically and retrieve the results, with configuration examples for different content scenarios. |
|[Using the AI skill](https://docs.byteplus.com/docs/byteplus-vod/enhancing_video_quality_via_skill) |Set up the video enhancement skill and request enhancements through natural language instructions. |

## Highlights

* **Shot\-adaptive enhancement:**  The feature segments the video into individual shots and applies a customized combination of enhancement operators to each one. This ensures optimal and consistent visual performance across the entire video.

* **Quality and fidelity balance:**  Through semantic\-level video understanding, the feature enhances resolution and detail while preserving the original video's texture. This effectively prevents common issues like under\-restoration or over\-sharpening and is particularly effective at correcting detail distortion in AIGC\-generated content.

## Architecture

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8c6b12d0fac74a77a5dd91b9f74c7784)

The technical process is illustrated in the diagram above and consists of the following key steps:

* **Audio\-visual separation and shot segmentation:**  The video is segmented into shots based on the scene to achieve fine\-grained enhancement at the shot and pixel levels.

* **Source video feature extraction:**  It extracts various features from the video, including facial features, object features, color, sharpness, noise, and regions of interest (ROI).

* **Preprocessing and intelligent operator combination:**  It selects the appropriate combination of operators for different business scenarios.

* **Extreme compression:**  It compresses the bitrate and file size of the processed video.

* **Intelligent detection:**  Throughout the entire process, it conducts image quality assessment based on the video quality score, selecting the best result to ensure that the visual output is subjectively optimal.

## Feature availability and regional access

This is a significantly upgraded video enhancement feature. Please review the following regional availability details:

* **New video enhancement templates:**  This upgraded feature is exclusively available in the **Johor** region and uses a new billing model. For complete billing details, see [Video enhancement pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#53c6a0c7).

* **Legacy video enhancement templates:**  The previous version of this feature remains available in the **Singapore** region. For pricing details on this legacy version, please contact your technical support representative. For usage instructions, see [Video enhancement template (Legacy)](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement-template-legacy).

## Application scenarios

The feature offers preset models tailored for specific types of content.

|**Scenario** |**Key capabilities** |
|---|---|
|**General** |A balanced model suitable for most common video types. |
|**UGC short video** |Fixes issues common in user\-generated content, such as blur, compression artifacts (blockiness), and noise, while enhancing facial details. |
|**AIGC content** |Upscales low\-resolution AI\-generated videos (such as 480p, 720p) to 2K or 4K, reconstructing details and improving visual texture with high frame\-to\-frame stability. |
|**Short drama** |Refines image quality by improving facial details and texture at the original resolution, or upscales low\-resolution episodes to 1080p/4K. |
|**Classic film restoration** |Repairs defects in older films, including motion\-compensated denoising, scratch removal, flicker reduction, and color correction. When you select the **Classic film restoration** scenario and the **Pro** tier, BytePlus VOD uses a [dedicated film restoration template](https://docs.byteplus.com/en/docs/25/27051#pro-film-restoration). |
|**Custom enhancement (Legacy)**  |This refers to the previous method of manually combining individual enhancement operators (like super\-resolution, frame interpolation).<br><br>> **Warning**<br><br><br>> Creating new custom enhancement templates is no longer supported in the new scenario\-based system. This option is mentioned for legacy context only.<br> |

> **Note**

> For demos of different scenarios, please see [Configuration examples and demos](https://docs.byteplus.com/docs/byteplus-vod/vCube_enhancement_use_cases#caa2de99).

## Enhancement tiers

You can choose from three processing tiers to balance speed, quality, and cost. Each tier is priced differently. For detailed billing information, see [Video enhancement pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#53c6a0c7).

|**Tier** |**Description** |
|---|---|
|**Standard** |Uses adaptive algorithms to provide a superior balance between visual texture and processing speed. |
|**Pro** |Powered by large\-model\-driven restoration for cinematic\-grade image quality. This tier requires a longer processing time. It provides [three versions](https://docs.byteplus.com/en/docs/25/27051#pro-versions) for the General, UGC short video, AIGC content, and Short drama scenarios, while Classic film restoration uses a [dedicated film restoration template](https://docs.byteplus.com/en/docs/25/27051#pro-film-restoration). |
|**Fast** |Integrates essential upscaling and basic enhancements for a good balance between processing speed and visual clarity. |

### Pro versions

For the **General**, **UGC short video**, **AIGC content**, and **Short drama** scenarios, the Pro tier provides three versions. BytePlus VOD automatically selects the version based on the configured output resolution.

|Pro version |Output resolution |Description |
|---|---|---|
|Medium |1080p and below |Enhances low\-resolution or blurred videos for clear HD viewing. It uses a balanced combination of enhancement algorithms for fine textures, distant scenes, small text, and complex materials, prioritizing faster processing over maximum detail restoration. It is suitable for mobile viewing and regular playback. |
|Premium |2K |Produces a more natural and stable image with finer detail restoration. It better preserves facial features, clothing textures, and architectural lines; reduces compression blocks, blurred edges, and low\-bitrate artifacts; and improves motion texture stability without excessive sharpening. It is suitable for large\-screen and high\-definition playback. |
|Ultimate |4K and above |Provides ultra\-high\-definition output with maximum texture consistency. It preserves complex textures and the structure of distant or small objects, and improves edge, layer, and motion continuity on large screens. It is suitable for ultra\-high\-definition output, cinema\-grade large\-screen playback, and premium film restoration. |

The following demo compares outputs processed by the Premium and Ultimate versions.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828071236-1774335119119.png)

### Pro film restoration template

When you select the **Classic film restoration** scenario and the **Pro** tier, BytePlus VOD uses a dedicated restoration template. This template integrates super\-resolution, intelligent denoising, deblurring, and color reconstruction into a unified AI workflow. It analyzes and reconstructs degradation at the content level, preserving the authentic texture of archival footage while restoring low\-resolution, noisy, or faded source material to clear, stable, richly layered, 4K\-quality visuals.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260831075847-638485005482.png)

### Processing time estimation

Since video enhancement involves deep learning model inference, processing time is typically longer than the source video's duration. You can estimate the wait time using the RTF (Real\-Time Factor), where:

Estimated processing time = Source video duration × RTF

RTF varies based on the enhancement tier, the Pro version, and the source video's duration. The following values are for reference.

|**Tier** |**Condition** |**RTF** |
|---|---|---|
|Fast |No segmentation |Approximately 3–4 |
|Standard |Source video duration \> 20 seconds |Approximately 6–10 |
||Source video duration ≤ 20 seconds |Approximately 22 |
|Pro \- Medium |Output resolution ≤ 1080p |Approximately 25 |
|Pro \- Premium |Output resolution = 2K |Approximately 40 |
|Pro \- Ultimate |Output resolution ≥ 4K |Approximately 60 |

The following example curves show how the RTF of the Standard and Pro tiers changes with the source video's duration.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260717061630-637074372064.png)

> **Note**

> Actual processing time is also affected by the input video's resolution and bitrate, as well as the current system queue status.

### Enhancement quality comparison

The following video demos illustrate the difference in output quality for each tier.

|**Enhancement tier** |**Demo** |
|---|---|
|Original |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f82aaacdd21d4393bd43fd81e271f677)<br> |
|Fast |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/aad003206b3f485f93ab4c6edf0ba1f5)<br> |
|Standard |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ee8c974141b746d6be71b69458e409cb)<br> |
|Pro |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/083f5c71d72b409d8385341b175a0d8c)<br> |

## Enhancement intensity

The enhancement intensity option is available for the **Standard** and **Pro** tiers:

* **Natural version:**  Applies a softer enhancement while keeping the visual texture close to the source video. This setting can help reduce an oil\-paint\-like appearance in certain scenarios, such as AI\-generated human\-like videos.

* **High definition:**  Applies a sharper enhancement style.

[video](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260812092023-1531633908561.mp4)

This option is not supported by the **Fast** tier.

## Color depth

Color depth, also known as bit depth, refers to the number of binary bits used to represent a single color channel, such as RGB or YUV, for each pixel in a video or image. It determines how many different color transitions the image can display.

The following list describes common color depth levels:

* **8\-bit:**  Each channel has `2^8 = 256` brightness levels.

* **10\-bit:**  Each channel has `2^10 = 1024` brightness levels.

* **12\-bit:**  Each channel has `2^12 = 4096` brightness levels.

* **16\-bit:**  Each channel has `2^16 = 65536` brightness levels.

> **Core value**

> A higher color depth provides much smoother color transitions and helps eliminate banding in large single\-color or gradient areas, such as skies and underwater scenes. It is also a prerequisite for HDR (High Dynamic Range) video.

### Color depth comparison demo

The following demo compares the visual results of 8\-bit, 10\-bit, 12\-bit, and 16\-bit color depth. Higher color depth provides finer tonal gradations, which helps produce smoother transitions and reduce visible banding.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260826071432-1700410789289.png)

> **Note**

> The perceived difference varies depending on the source content, display capabilities, player, operating system, and color\-management settings.

### Application scenarios for color depth

|**Color depth** |**Typical scenarios** |**Core benefit** |
|---|---|---|
|8\-bit |TV broadcasts, social media, and standard web videos |Strong compatibility and small file sizes, but HDR is not supported. |
|10\-bit (recommended) |4K Blu\-ray movies, premium streaming platforms, refined short dramas, and high\-quality videos |Eliminates sky banding, supports HDR, and is currently the mainstream standard for premium global content distribution. |
|12\-bit |Film masters, commercial ads, and theatrical releases |Provides extensive room for post\-production color grading, dynamic brightness adjustment, and cinema\-grade viewing experiences. |
|16\-bit |Visual effects (VFX) and 3D\-rendered source masters |Serves as a data\-asset\-level format for extremely precise optical compositing. |

### Output format

For the **Pro** enhancement tier, you can select a combination of encoding format and color depth for the output. By default, the output container is determined automatically by the combination, so you do not need to set it separately.

The following table lists the supported combinations.

|**Encoding format** |**Color depth** |**Container** |
|---|---|---|
|H.264 |8\-bit |MP4 |
|H.265 |8\-bit, 10\-bit, 12\-bit |MP4 |
|ProRes |10\-bit |MOV |
|FFV1 |16\-bit |MOV |
|FFV1 (GBR pixel format) |16\-bit |MOV |
|EXR |16\-bit |EXR |

> **Note**

* > When you submit a task through the [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-enhancement) API, the encoding format, color depth, and pixel format are set through the `Codec`, `BitDepth`, and `PixFmt` parameters. Setting `Codec` requires `BitDepth`; if you set `BitDepth` alone, the system uses the default encoding format for that color depth. If you omit `PixFmt`, the system selects the pixel format automatically. The container is not passed through the API. On the console, these values are set through a single **Output format** option.

* > An EXR output is an image sequence and cannot be previewed directly in the console.

### EXR and ProRes formats

The **Pro** enhancement tier can output the professional EXR and ProRes formats in addition to H.264, H.265, and FFV1. Both formats are designed for film\-grade post\-production workflows.

#### EXR

The Pro tier can output 16\-bit floating\-point OpenEXR (`.exr`) files that fully preserve the high dynamic range (HDR) and the fine details produced by large\-model restoration. This makes EXR well suited to film\-grade scenarios such as classic film restoration and 4K/8K master remastering, where the output feeds directly into professional color grading and visual effects (VFX) compositing pipelines.

* **16\-bit half\-float encoding:**  EXR encodes each color channel using 16\-bit half\-precision floating\-point values. Compared with traditional 8\-bit encoding (about 16 million colors), it represents a much wider dynamic range than a screen can display, which prevents banding in shadows and clipping in highlights and preserves the full detail of the enhanced image.

* **OpenEXR format:**  OpenEXR (`.exr`) is a film\-industry standard format open\-sourced by Industrial Light & Magic (ILM). It supports high dynamic range, multiple channels, a linear color space, and lossless compression, and it is a common delivery format for film post\-production, color grading, and VFX compositing.

#### ProRes

The Pro tier can output Apple ProRes with a 10\-bit, 4:2:2 pixel format. Apple ProRes is a lossy video codec developed by Apple for video post\-production. It balances image quality, file size, and editing performance, and it is a mainstream intermediate format in the film post\-production industry.

The following table lists its core characteristics.

|**Characteristic** |**Description** |
|---|---|
|High\-quality lossy compression |Delivers visually lossless quality, far better than H.264 or H.265. |
|Intra\-frame compression |Encodes each frame independently, so you can trim at any frame precisely without decoding adjacent frames. |
|High bitrate |Retains rich color detail, which suits color grading and visual effects. |
|Wide color gamut and HDR support |Supports 10\-bit and 4:2:2, and can carry HDR metadata. |
|GPU and hardware acceleration |Natively accelerated by Apple hardware for smooth editing in Final Cut Pro. |

### GBR pixel format

The Pro tier can output 16\-bit FFV1 in the GBR pixel format (`gbrp16le`) in addition to the default YUV pixel format. In the GBR pixel format, each of the red, green, and blue channels is stored in its own plane, so the enhanced RGB data does not go through a color space conversion to YUV and is not affected by chroma subsampling or the luma and chroma information loss that such a conversion can introduce. Use this option when the output feeds a compositing or color grading workflow that works with RGB data.

The console lists this combination as **MOV | FFV1 \- GBR | 16\-bit**. Through the API, set `Codec` to `ffv1`, `BitDepth` to `16`, and `PixFmt` to `gbrp16le`. For how `PixFmt` interacts with other encoding formats, see [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-enhancement#volcmoetarget).

### Usage limits

* To ensure the best color grading effect, color depth configuration is supported only for the **Pro** enhancement tier and must be used together with advanced enhancement capabilities.

* When you configure 16\-bit color depth, note the following:

   * The input video duration must not exceed 40 seconds.

   * A 16\-bit output uses the FFV1 lossless encoding format or the EXR image sequence format, so you do not need to set a target bitrate.

   * 16\-bit tasks are processed serially, one task at a time. A new task starts only after the current task is complete, so the processing time can be long. Please wait patiently.

### Notes for 12\-bit and 16\-bit output

Conventional players and operating system rendering pipelines, such as the Windows SDR desktop, cannot correctly decode and render 12\-bit or 16\-bit data. To compare the output correctly, re\-import the exported asset into a professional tool such as DaVinci Resolve or Premiere, and review it on a professional monitor with color management enabled.

Do not export 16\-bit image sequences to ordinary hard drives or slow disks formatted as FAT32 or exFAT. The high read and write throughput can cause the system to freeze. Use a dedicated NVMe M.2 SSD and plan the storage array in advance.

A conventional `MP4` file with `H.264` or `H.265` encoding is often handled as 8\-bit or 10\-bit by playback and editing software. When higher bit depth data is forced into such a file, the software may dither or truncate it to 10\-bit, wasting the previous high\-precision processing. A 12\-bit output from the enhancement task is exported as `MP4` with `H.265`, so open the file in a professional tool to confirm that the 12\-bit data is preserved.

## Dynamic range and SDR to HDR

The Pro enhancement tier can convert the enhanced output from standard dynamic range (SDR) to high dynamic range (HDR) using the HLG (Hybrid Log\-Gamma) transfer function. Compared with an SDR output, HLG preserves a wider range between the darkest and brightest parts of the image, so the result can be displayed with the intended highlight range on HLG\-capable displays.

The following conditions apply:

* SDR to HDR conversion is supported only for the **Pro** enhancement tier and only for 10\-bit, 12\-bit, and 16\-bit output. 8\-bit output does not support it.

* EXR output is already HDR. EXR uses a floating\-point linear representation rather than HLG, so the two dynamic range settings are not combined: when you select an EXR output format, SDR to HDR conversion is unavailable and `DynamicRange` cannot be set to `HLG`.

* If you do not enable conversion, the output stays at SDR, except for an EXR output, which is always HDR. This also applies to HDR source videos: without conversion, an HDR input is converted to SDR. To enable conversion, do the following:

   * **Console:**  Turn on **SDR to HDR** in the video enhancement template. When the selected output format does not meet the conditions above, the switch is disabled and shows the message **Requires Pro version + 10/12/16\-bit color depth**.

   * **API:**  Set `DynamicRange` to `HLG` in `MoeEnhance.Target`. For parameter details, see [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-enhancement#volcmoetarget).

> **Note**

> HLG output is intended for display, player, and operating system pipelines that support HLG. On an SDR\-only pipeline, the asset may not render as intended. Review HLG assets in a color\-managed professional tool before delivery.

## Related references

* [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template)

* [Submit a video enhancement task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-enhancement)

* [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution)

* [Video enhancement pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#53c6a0c7)
