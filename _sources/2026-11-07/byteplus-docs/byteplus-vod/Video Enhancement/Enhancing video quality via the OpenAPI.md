---
title: "Enhancing video quality via the OpenAPI"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/vCube_enhancement_use_cases"
---

This document describes how to programmatically submit video enhancement tasks and retrieve results using the BytePlus VOD API.

## Implementation steps

The following steps guide you through the complete workflow: from submitting a task to obtaining the final playback URL. For this walkthrough, we will use an **AIGC content enhancement** scenario as an example.

### Step 1: Submit a video enhancement Task

Call the [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-enhancement) API to submit an asynchronous task. You can define all parameters dynamically in the request body. Key parameters for a AIGC scenario:

* `Input`: Specifies the video file to be processed.

* `Operation.Task.Type`: Must be set to `Enhance`.

* `Operation.Task.Enhance`: Defines all enhancement parameters.

   * `Type`: Set to `Moe` to indicate the use of scenario\-based enhancement models.

   * `MoeEnhance`:

      * `Config`: Specifies a scenario\-based preset template. Set to `aigc`.

      * `Target`: Dynamically specifies output settings such as the output resolution `Res`, frame rate `Fps`, target bitrate `Bitrate`, color bit depth `BitDepth`, and encoding format `Codec`. `BitDepth` and `Codec` are supported only for the Pro enhancement tier.

         * `BitDepth` supports `8`, `10`, `12`, and `16` (default `8`), and `Codec` supports `h264`, `h265`, `prores`, `ffv1`, and `exr`. For the supported pairings, see [Encoding format and color depth combinations](https://docs.byteplus.com/en/docs/25/91006#encoding-format-and-color-depth-combinations).

         * `Codec` requires `BitDepth`; if you set `BitDepth` alone, the system applies the default encoding format for that color depth. The output container is determined automatically by the combination.

         * `PixFmt` sets the pixel format. `gbrp16le` produces a 16\-bit FFV1 file in the GBR pixel format, which the console lists as **MOV | FFV1 \- GBR | 16\-bit**.

         * `DynamicRange` set to `HLG` converts the output from SDR to HLG HDR. This value requires a 10\-bit, 12\-bit, or 16\-bit color depth and is not supported for `exr` output.

         * When `BitDepth` is `16` (`ffv1` or `exr`), the input video duration must not exceed 40 seconds, and `Bitrate` is not supported.

      * `VideoStrategy`:

         * `EnhanceLevel`: Choose your enhancement tier (`Fast`, `Standard`, `Pro`).

**Request example (AIGC 4K and Pro tier):**

```JSON
{
  "SpaceName": "your_space_name",
  "Input": {
    "Type": "Vid",
    "Vid": "v02399g10001***j9aljht5kim11hp0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Enhance",
      "Enhance": {
        "Type": "Moe",
        "MoeEnhance": {
          "Config": "aigc",
          "Target": { 
            "Res": "4k",
            "Bitrate": 8000,
            "BitDepth": 10,
            "Codec": "h265"
          },
          "VideoStrategy": {
            "RepairStrength": 0,
            "EnhanceLevel": "Pro"
          }
        }
      }
    }
  }
}
```

> **INFO**

> For more visual examples of how these configurations affect different content types, see the [Configuration examples and demos](https://docs.byteplus.com/docs/byteplus-vod/vCube_enhancement_use_cases#caa2de99) section below.

### Step 2: Retrieve task results

Since the task is processed asynchronously, you will receive a `RunId` in the Step 1 response. Use this ID to track progress:

* **Active polling**: Call the [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution) API periodically. When the `Status` is `Success`, locate the output `Vid` or `StoreUri` in the `Output.Task.Enhance` object.

* **Event notification**: Configure the [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete) event callback to receive the results automatically via a POST request.

Regardless of the path, you will ultimately receive a `TranscodeInfo` object containing detailed information about the enhanced video. Pay close attention to the `StoreUri` field. While `StoreUri` cannot be played directly, it is used to [Step 3：Concatenating the output video URL](https://docs.byteplus.com/docs/byteplus-vod/vCube_enhancement_use_cases#eaf53a4a).

### Step 3：Concatenating the output video URL

After obtaining `StoreUri` of the enhanced video, you must manually concatenate it into a publicly accessible URL for playback or download. Follow the steps below:

> **INFO**

> Before obtaining a public URL, you **must** add and configure a playback domain for the VOD space where the output is located. All URLs are generated based on this domain. For details, see [Adding and configuring domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-configuring).

1. Parse `FileName` from `StoreUri`: `StoreUri` consists of `BucketName` and `FileName`. If the `StoreUri` you obtain is `tos-vod-v-*****80626/40e62*****9eddcc16a5`, the `BucketName` is `tos-vod-v-*****80626` and the `FileName` is `/40e62*****9eddcc16a5`.

2. Concatenate the playback address:

   * A basic access URL consists of the following components: `Protocol://PlaybackDomain/FileName?auth_key=xxx`

      * `[Protocol]`: Typically `https` or `http`, depending on whether you have [Configuring SSL certificate](https://docs.byteplus.com/docs/byteplus-vod/docs-configuring-ssl-certificates).

      * `[PlaybackDomain]`: The playback domain you configured in the VOD console.

      * `[FileName]`: The `FileName` parsed from the `StoreUri`.

   * Concatenation example: Assuming your playback domain is `play.example.com` and the parsed `FileName` is `video.mp4`, the basic concatenated URL is: `https://play.example.com/video.mp4`

> **INFO**

> To prevent unauthorized hotlinking, BytePlus VOD supports URL signing. If you have enabled URL signing in the VOD console, the basic URL cannot be accessed directly; you must append a dynamically calculated authentication parameter (such as `auth_key`).

* > **How to generate signing parameters**: URL signing follows a strict signing algorithm. For detailed calculation methods and code samples in various languages, see [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview).

* > **Example of a full signed URL**: `https://play.example.com/video.mp4?auth_key=1732529334-0-0-a1b2c3d4e5f6...`

## Configuration examples and demos

The following tables demonstrate how specific `MoeEnhance` configurations translate into visual quality improvements across different tiers and scenarios.

### AIGC content

To address the resolution limitations often found in AI\-generated content (typically 480p/720p), vCube offers:

* **Super\-resolution:**  Upscales videos to 2K or 4K with advanced detail reconstruction.

* **Quality enhancement:**  Improves visual texture, clarity, and color depth.

* **Temporal stability:**  Ensures high frame\-to\-frame consistency during the upscaling process.

The following table shows how different **enhancement tiers** (defined by the `EnhanceLevel` parameter) affect the output.

|Sample code |Enhancement result |
|---|---|
|```JSON```<br>```{```<br>```  "Input": {```<br>```    "Type": "Vid",```<br>```    "Vid": "your_vid"```<br>```  },```<br>```  "Operation": {```<br>```    "Type": "Task",```<br>```    "Task": {```<br>```      "Type": "Enhance",```<br>```      "Enhance": {```<br>```        "Type": "Moe",```<br>```        "MoeEnhance": {```<br>```          "Config": "aigc",```<br>```          "Target": {```<br>```            "Res": "4k"```<br>```          },```<br>```          "VideoStrategy": {```<br>```            "EnhanceLevel": "Standard",```<br>```            "RepairStrength": 0```<br>```          }```<br>```        }```<br>```      }```<br>```    }```<br>```  }```<br>```}```<br> |**Original**<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f82aaacdd21d4393bd43fd81e271f677)<br> |
||**Fast**<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/aad003206b3f485f93ab4c6edf0ba1f5)<br> |
||**Standard**<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ee8c974141b746d6be71b69458e409cb)<br> |
||**Pro**<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/083f5c71d72b409d8385341b175a0d8c)<br> |

### Short drama scenarios

Designed for high\-paced mobile content, this scenario focuses on:

* **Texture refinement:**  Improves perceived quality by sharpening facial details and textures at the original resolution.

* **High\-end upscaling:**  Converts 480p content to 1080p/4K while eliminating pixelation and restoring lost information.

|Sample code |Enhancement result |
|---|---|
|```JSON```<br>```{```<br>```  "Input": {```<br>```    "Type": "Vid",```<br>```    "Vid": "your_vid"```<br>```  },```<br>```  "Operation": {```<br>```    "Type": "Task",```<br>```    "Task": {```<br>```      "Type": "Enhance",```<br>```      "Enhance": {```<br>```        "Type": "Moe",```<br>```        "MoeEnhance": {```<br>```          "Config": "short_series",```<br>```          "Target": { "Res": "1080p" },```<br>```          "VideoStrategy": {```<br>```            "EnhanceLevel": "Standard",```<br>```            "RepairStrength": 0```<br>```          }```<br>```        }```<br>```      }```<br>```    }```<br>```  }```<br>```}```<br> |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d025f7fbddde465987f38ce93fb6e97d)<br> |

### Classic film restoration

This scenario repairs complex defects in legacy film stock:

* **Defect repair:**  Removes scratches, flickers, and temporal noise using motion\-compensated algorithms.

* **Authentic restoration:**  Intelligently restores colors and sharpens edges while preserving the original film grain and cinematic texture.

|Sample code |Enhancement result |
|---|---|
|```JSON```<br>```{```<br>```  "Input": {```<br>```    "Type": "Vid",```<br>```    "Vid": "your_vid"```<br>```  },```<br>```  "Operation": {```<br>```    "Type": "Task",```<br>```    "Task": {```<br>```      "Type": "Enhance",```<br>```      "Enhance": {```<br>```        "Type": "Moe",```<br>```        "MoeEnhance": {```<br>```          "Config": "old_film",```<br>```          "Target": {```<br>```            "Res": "4k"```<br>```          },```<br>```          "VideoStrategy": {```<br>```            "EnhanceLevel": "Standard",```<br>```            "RepairStrength": 0```<br>```          }```<br>```        }```<br>```      }```<br>```    }```<br>```  }```<br>```}```<br> |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ffd602807d5749da9cd5983632a32fd1)<br> |

### **General content**

This scenario uses the `common` configuration to provide general quality improvements and artifact removal.

* Comprehensive quality improvement:

   * Deblurring: Sharpens blurry or out\-of\-focus footage.

   * Compression artifact removal: Reduces noise, blocking effects, and color banding.

   * Face and detail Enhancement: Optimizes facial clarity and restores fine textures.

* Upscaling:

   * Low\-to\-High resolution: Employs AI\-driven super\-resolution to upscale content (such as 480p to 1080p/4K).

   * Detail reconstruction: Restores lost information while enlarging the image.

|Sample code |Enhancement result |
|---|---|
|```JSON```<br>```{```<br>```  "Input": {```<br>```    "Type": "Vid",```<br>```    "Vid": "your_vid"```<br>```  },```<br>```  "Operation": {```<br>```    "Type": "Task",```<br>```    "Task": {```<br>```      "Type": "Enhance",```<br>```      "Enhance": {```<br>```        "Type": "Moe",```<br>```        "MoeEnhance": {```<br>```          "Config": "common",```<br>```          "Target": {```<br>```            "Res": "4k"```<br>```          },```<br>```          "VideoStrategy": {```<br>```            "EnhanceLevel": "Standard",```<br>```            "RepairStrength": 0```<br>```          }```<br>```        }```<br>```      }```<br>```    }```<br>```  }```<br>```}```<br> |[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9e7aeb1208724d4194221da53f055455)<br> |

## Reference

### Encoding format and color depth combinations

`Codec` requires `BitDepth`, but you can set `BitDepth` on its own. When you provide both, they must form one of the combinations in the following table; when you provide only `BitDepth`, the system applies the default `Codec` for that color depth.

|`BitDepth` |Supported `Codec` |Default `Codec` |
|---|---|---|
|`8` |`h264`, `h265` |`h264` |
|`10` |`h265`, `prores` |`h265` |
|`12` |`h265` |`h265` |
|`16` |`ffv1`, `exr` |`ffv1` |
