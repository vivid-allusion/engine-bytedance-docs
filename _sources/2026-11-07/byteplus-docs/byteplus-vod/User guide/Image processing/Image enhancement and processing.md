---
title: "Image enhancement and processing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-image-enhancement"
---

BytePlus VOD provides AI super resolution to improve the clarity and texture of images, including AI\-generated content, user uploads, and existing image libraries. You can also resize, crop, pad, or convert images through basic image processing. Original images and processed files are stored together as image assets for preview and distribution.

## Image assets and processing options

Each image asset has a unique picture ID (`Pid`). Use this ID to submit processing tasks, retrieve the original image and its processed files, or delete the asset. For upload, search, metadata, and deletion procedures, see [Managing image assets](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management).

|Option |Description |
|---|---|
|Image enhancement |Uses AI super resolution to increase image resolution and improve detail while reducing noise and compression artifacts. |
|Basic image processing |Resizes, center\-crops, or pads an image and supports output format conversion. |
|Real\-time image processing |Applies transformations when an image URL is requested. For URL syntax and transformation parameters, see [Real-time image processing](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing). |

Upload images as image assets to use PID\-based enhancement and processing. Images uploaded as materials for video covers, watermarks, or editing remain a separate asset type.

## Limits and configuration

### Upload limits

The console accepts static PNG, JPG, JPEG, and WebP images and animated GIF and WebP images up to 50 MB each. AI enhancement has stricter input requirements, as listed below. See [Uploading images](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management#upload-images).

### Image enhancement

|Setting or limit |Requirement |
|---|---|
|Input format |PNG, JPG, JPEG, or WebP. |
|Input size |No more than 10 MB per image. |
|Input resolution |The short edge must be at least 256 pixels, and the long edge must be no more than 2,048 pixels. |
|Super resolution scale |Set **super multiple** from 1.1 to 30. The default is 2. Decimal values such as 1.5 or 2.3 are supported. |
|Output resolution |Calculated from the input dimensions and scale. You cannot specify the output dimensions directly for AI enhancement. The task fails if the calculated long edge exceeds 10,240 pixels. |
|Output format |The same as the input format. |

Before submitting a task, check that `input long edge × scale ≤ 10240`. For example, an image with a long edge of 2,048 pixels can use a scale of up to 5 without exceeding the output limit.

If the input exceeds the supported size, format, or resolution, prepare an image that meets these requirements before submitting it for enhancement. To resize or convert an enhanced file when accessing it, use that file's `StoreUri` with [Real-time image processing](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing).

### Image processing

Select **Image processing**, then choose an operation and **Output format**:

|Console option |Configuration |
|---|---|
|**Zoom** |Enter **Width** and **Height** in pixels. The image is resized to fit within these dimensions while preserving its aspect ratio. |
|**Limit height** |Enter **Height** in pixels to resize proportionally by height. |
|**Center crop** |Enter **Width** and **Height** in pixels for a center crop. |
|**Center fill** |Enter **Width** and **Height** in pixels and select **Background color**. The default color is white (`#FFFFFF`). This option supports only static images. |

Dimensions must be positive integers. The console output format selector and the [ImageProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageprocess) API support `jpeg`, `jpg`, `png`, `webp`, `awebp`, `gif`, `image`, `avif`, and `avis`. Select `image` to retain the input format. In API requests, omitting `OutputFormat` has the same effect. GIF output requires an animated input image.

> **Animated images**

> Center padding is not supported for animated images. Basic processing of animated images can return the original image; check the processed file before using it.

## Procedure

### Process images during upload

1. Open **Media assets** \> **Images** in your space and click **Upload image**.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029112147-57631511470.png)

2. Select the upload directory and add local images. Check their titles, file paths, and input limits.

3. Under **Processing options**, select **Image enhancement**, **Image processing**, or both. Configure the parameters above.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029113219-1220176531749.png)

4. Click **Upload** and check upload progress on **Uploading**.

5. When the image appears on **Uploaded**, click **Details** to check its tasks and results.

For the complete upload procedure, see [Managing image assets](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management#upload-images).

### Process existing images

1. Open **Media assets** \> **Images** and select **Pid mode**.

2. On **Uploaded**, find an image by PID or name, or filter by creation time.

3. Click **Process** in the image's **Action** column. For batch processing, select the images and click **Process** above the list.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029113424-777181081157.png)

4. In the **Image processing** dialog, select **Image enhancement**, **Image processing**, or both, and configure the parameters.

5. Click **Start processing**.

6. Click **Details** for an image, then open **Process task** to check each task. Open **Processing result** to inspect the outputs and use **Preview export**.

Selecting both enhancement and basic processing creates separate tasks and outputs for the original image. It does not automatically apply the basic operation to the enhanced output. For example, for a 640 × 480 input, a scale of 2 produces a 1,280 × 960 enhanced image, while a 320 × 240 resize produces a separate 320 × 240 image.

If a batch submission reports failed PIDs, check those images before retrying. A successful submission does not mean that processing has completed. For result and distribution details, see [View processing tasks and results](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management#view-processing-tasks-and-results).

## API workflow

The task APIs [ImageAIProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageaiprocess), [ImageProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageprocess), and [GetImageProcessTasks](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageprocesstasks) use version `2023-07-01` and accept POST requests at `https://vod.byteplusapi.com`. Use the [common API request and authentication rules](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction).

1. Upload an image asset and obtain its `Pid` from [GetImageList](https://docs.byteplus.com/docs/byteplus-vod/reference-getimagelist). For URL uploads, call [UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl) with `RecordType=3` and `FileType=image`. For the [server-side upload flow](https://docs.byteplus.com/docs/byteplus-vod/docs-server-side-uploads), set `RecordType=3` in the `AddOptionInfo` [upload function](https://docs.byteplus.com/docs/byteplus-vod/upload-functions) passed to `CommitUploadInfo`. If the image already exists, use its PID from the image list or [look it up by storage URI](https://docs.byteplus.com/docs/byteplus-vod/listfilemetainfosbyfilenames).

2. Submit a processing task:

   * **AI enhancement:**  Call [ImageAIProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageaiprocess) with `Pid`, `ProcessType` set to `AISuperResolution`, and `WorkflowParameter`, which contains the AI parameters as a JSON string. `SpaceName` and `CallbackArgs` are optional.

   * **Basic processing:**  Call [ImageProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageprocess) with `Pid` and `ProcessType` set to `rs`, `cc`, or `pad`. For proportional resizing with `rs`, specify one of `Width` or `Height`. For `cc` and `pad`, specify both dimensions. For padding, also set `Color` to a six\-digit hexadecimal RGB value without `#`, such as `FFFFFF`. `Width` and `Height` are strings containing positive integers. Set `OutputFormat` if you need format conversion. `SpaceName` and `CallbackArgs` are optional.

3. Save the returned `TaskId`. A successful submission returns `Status` set to `pending`.

4. Call [GetImageProcessTasks](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageprocesstasks) with `SpaceName` and `Pid`. Supply `TaskId` to query a particular task. Task states are `pending`, `processing`, `success`, and `failed`. For a failed task, inspect `ErrorCode` and `ErrorMessage`.

5. After the task succeeds, retrieve image details through [GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos). Pass one or more PIDs in `Pids`, separated by commas. The response includes `OriginalImageInfo` and `ProcessedImageInfos`. Task queries return output file metadata, including `FileId` and `StoreUri`, but do not return image access URLs.

For asset listing, metadata updates, and deletion APIs, see [Manage images through APIs](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management#manage-images-through-apis).

For event\-based integration, configure the [ImageProcessComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imageprocesscomplete) and [ImageDeleteComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imagedeletecomplete) events. See [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

## Pricing and usage

Image enhancement is charged at **USD 9.6 per 1,000 successful requests**. Image previews that use an external storage address incur storage outbound traffic charges. See [Image enhancement pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#image-enhancement-pricing) and [Storage outbound traffic pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#storage-outbound-traffic-pricing).

To check usage, open **Utilization insights** \> **Usage** \> **Image processing**. **Batch processing** groups enhancement and basic processing usage by space, while **Real\-time processing** groups URL\-based processing usage by domain. For details, see [Usage](https://docs.byteplus.com/docs/byteplus-vod/docs-usage#image-processing-usage).
