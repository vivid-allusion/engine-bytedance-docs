---
title: "Video covers"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-cover"
---

BytePlus VOD supports automatic video cover generation and using a video snapshot as a custom cover. This page describes how to associate a cover image with a video and retrieve its URL. For image transformations and URL parameters, see [Real-time image processing](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing).

## Preparing your image asset

Before using an image as a cover, it needs to exist within the VOD service and be associated with a `StoreUri` (its unique storage identifier). You can obtain an image asset in several ways:

* **Uploading an image as an image asset:**  Upload and manage it on the Images page, then retrieve its original or processed file information with [GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos). For the procedure, see [Managing image assets](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management).

* **Uploading an image directly as a material:**  Use this method for auxiliary images such as posters, watermarks, or pre\-made covers. You can upload JPG or PNG files using any of the standard upload methods, such as the VOD console or the Upload SDKs. When the upload is complete, you will receive a `MaterialUploadComplete` event containing the asset's `StoreUri`. These images will be managed under **Media assets** \> **Materials**. For details, see [Upload overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview).

* **Generating a snapshot from a video:**  Use a [Snapshot template](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template) in a workflow to generate images from a video. The `StoreUri` for each snapshot will be available in the workflow completion results.

* **Auto\-generating a video cover:**  Configure your space to automatically extract the first non\-black frame of an uploaded video. This process generates an image asset and automatically links its `StoreUri` to the video's metadata.

## Use case: setting a video cover

A video cover (`Poster`) is simply a specific image asset that is officially associated with a video's metadata. There are two main ways to associate an image as a video's official cover:

### Method 1: Set ordinary cover image

1. Follow these steps to generate an ordinary cover:

   1. Enable **Auto cover generation** in the BytePlus VOD console. For details, see [Post-upload actions](https://docs.byteplus.com/docs/byteplus-vod/docs-system#3cd0f7b4).

   2. Upload the video to BytePlus VOD, and the system will automatically extract the first non\-black frame as the cover. You can also extract frames from a specific time point by setting the `SnapshotTime` parameter. For details, see [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo).

2. Choose either of the following options to get the cover image URL:

   * Option 1: Call [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) to directly retrieve the cover image URL. This method provides a straightforward way to obtain the URL without any manual construction.

   * Option 2: Get the `PosterUri` of the cover image through one of the following methods and then manually construct the cover image URL.

      * Retrieve the `PosterUri` from the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) callback.

      * Call [GetMediaInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getmediainfos) to get the `PosterUri`.

### Method 2: Set a snapshot as cover image

1. Use [Snapshot template](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template) to generate snapshots of the desired content.

2. Once the workflow execution is completed, get the `StoreUri` of the snapshots from the [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) callback.

3. Call [UpdateMediaInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-updatemediainfo) to update the media information. Set the `StoreUri` obtained in Step 2 as the value for the `PosterUri` parameter.

4. Choose one of the following options to get the cover image URL:

   * Option 1: Directly retrieve the cover image URL by calling the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API.

   * Option 2: Manually construct the cover image URL using the `StoreUri` obtained in Step 2.

## Constructing the image URL

Image domain prerequisites, URL syntax, output formats, and examples are now covered in [Constructing the image URL](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing#72e02267).

## Image processing methods

For resize, crop, padding, and compression parameters and examples, see [Image processing methods](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing#54777ae6).
