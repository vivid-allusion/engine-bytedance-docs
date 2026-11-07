---
title: "Media upload"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload"
---

This article describes how to upload media resources to the BytePlus VOD console.

## Supported file types

BytePlus VOD supports audio/video assets, materials, and image assets:

* Audios and videos are media assets that can be processed and played. The following table lists the formats that can be uploaded to the BytePlus VOD console as audio and video assets.

   |**File type** |**Format** |**Maximum size** |
   |---|---|---|
   |Audio |MP3, M4A, WAV, WMA, AMR, AAC, OGG |20 GB |
   |Video |MP4, FLV, ASF (Advanced Systems Format, also known as WMV), RM, RMVB, MPEG, MOV, AVI, FLASH, MPEG\-TS (MTS), M4S, M3U8, Matroska (MKV) |20 GB |

* Materials are auxiliary media assets that can be used as video covers, watermarks, patches, or materials for video editing. Materials cannot be processed or played. The following table lists the formats that can be uploaded to the BytePlus VOD console as materials.

   |**File type** |**Format** |**Maximum size** |
   |---|---|---|
   |Audio |MP3, M4A, WAV, WMA, AMR, AAC, OGG |50 MB |
   |Video |MP4, FLV, ASF (Advanced Systems Format, also known as WMV), RM, RMVB, MPEG, MOV, AVI, FLASH, MPEG\-TS (MTS), M4S, M3U8, Matroska (MKV) |500 MB |
   |Image |PNG, JPG, JPEG |50 MB |
   |Cinemagraph |GIF, WebP |50 MB |
   |Subtitle |SRT, VTT, and ASS |50 MB |
   |Font |TTF, FON, and TTC |50 MB |

* Images uploaded as image assets have a unique picture ID (`Pid`) and support enhancement and basic processing. Static images support PNG, JPG, JPEG, and WebP; animated images support GIF and WebP. The maximum size is 50 MB per image. AI enhancement has stricter input limits; see [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement).

## Prerequisites

* Ensure that you have enabled the BytePlus VOD service.

* Ensure that you have created a space.

## Uploading an audio or video file

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media assets** \> **Videos** on the left navigation bar.

5. Click **Upload video**. In the dialog box that appears, add the files you want to upload. You can:

   * Upload files from your local PC. This method is suitable for small\-scale uploads.

   * Upload files from URLs. This method is suitable for large\-scale file migration.

6. (Optional) After adding the files you want to upload, you can edit the following information:

   * **Name**: The length of the file name should not exceed 128 characters.

   * **Category**: You can divide the files into different categories. If the category you need does not exist, click **System settings** \> **Categories** on the left navigation bar to create categories.

7. (Optional) Select a workflow to apply to the videos you are uploading for transcoding. For details, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow). If you don't select a workflow, the files will be uploaded without undergoing transcoding.

8. (Optional) For local video uploads, select **Upload and trigger the AI understanding task** under **upload process**, then click **Configure**. Configure preprocessing, model services, parameters, and the prompt, and choose the entire video or a specified time range. Click **Complete configuration** to return to the upload page. An incomplete configuration will not trigger an understanding task. See [Intelligent video understanding](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#understanding-on-upload). This option is not supported for URL\-based asynchronous uploads.

9. Click **Upload**. The console automatically redirects you to the **Uploading** page, where you can check the upload status.

   > **Warning**

   > Do not refresh or close the browser during the upload process.

## Uploading a material file

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media assets** \> **Materials** on the left navigation bar.

5. Click **Upload material**. In the dialog box that appears, add the files you want to upload from your local PC.

6. (Optional) After adding the files you want to upload, you can edit the file name. The length of the file name should not exceed 128 characters.

7. Click **Upload**. The console automatically redirects you to the **Uploading** page, where you can check the upload status.

   > **Warning**

   > Do not refresh or close the browser during the upload process.

## Uploading an image asset

Open **Media assets** \> **Images** in your space, select **Pid mode**, and click **Upload image**. Under **Processing options**, you can select **Image enhancement**, **Image processing**, or both to process the uploaded images. For directory selection, file information, and upload status, see [Uploading images](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management#upload-images).

## Next step

After uploading media files to the BytePlus VOD console, you can process your files. For details, see [Media processing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-processing-overview).
