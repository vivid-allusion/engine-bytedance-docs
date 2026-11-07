---
title: "Managing image assets"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-image-asset-management"
---

Image assets let you manage an original image and its processed files under one picture ID (`Pid`). Use **Media assets** \> **Images** in your space to upload images, view their information, and access processing results.

## Choose a management mode

|Mode |Use it to |
|---|---|
|**Pid mode** |Find images by PID or name, inspect image metadata, and submit enhancement or basic processing tasks. |
|**DirectUrl mode** |Browse stored files by path, organize folders, inspect file information, and generate access addresses. This view can also contain other file types stored in the space. |

Use **Pid mode** for the processing procedures in this guide. Images uploaded as materials for covers, watermarks, or editing are a separate asset type. For those files, see [Upload overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview).

## Upload limits

The **Upload image** page supports the following files, up to 50 MB each:

|Image type |Formats |
|---|---|
|Static image |PNG, JPG, JPEG, WebP |
|Animated image |GIF, WebP |

Upload limits differ from processing limits. AI enhancement accepts PNG, JPG, JPEG, and WebP inputs up to 10 MB, with additional resolution limits. **Center fill** supports only static images. Review [processing requirements](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement#limits-and-configuration) before selecting processing options.

## Procedure

### Upload images

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/), enter your space, and open **Media assets** \> **Images**.

2. Select **Pid mode**, then click **Upload image**.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029112147-57631511470.png)

3. Under **Upload to**, use **Current directory** or select **Specified directory** and enter a storage directory. The directory and file path together determine the storage location.

4. (Optional) Under **Processing options**, select **Image enhancement**, **Image processing**, or both. Configure the options as described in [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement#limits-and-configuration). Leave both unchecked to upload without processing.

5. Click the upload area or drag local files into it. In the file list, check or edit **Title** and **File path (optional)** . Titles support up to 128 characters; file paths support up to 1,024 characters.

6. Click **Upload**. The console switches to **Uploading**, where you can check the upload status.

7. After uploading, open **Uploaded** and click **Refresh** to update the image list. Each image displays its PID. Upload completion and processing completion are separate; check processing tasks in the image's details.

> **Keep the upload page open**

> Do not refresh or close the browser while files are uploading.

### Find and edit image information

1. On **Uploaded** in **Pid mode**, select the search type and enter a PID or image name. You can also filter by creation time.

2. Click **Details** for an image.

3. On **Basic information**, inspect the thumbnail, title, picture ID, format, dimensions, tags, description, creation time, and file path.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029112544-75162957417.png)

4. Click **Edit** to change the title, tags, or description, then click **Save**. Click **Cancel** to discard your edits.

### View processing tasks and results

1. Open the image's **Details**.

2. Select **Process task** to view task IDs, processing types, statuses, and creation and update times. A submitted task is not necessarily complete; wait for **Success** before using its output.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029112851-505205817031.png)

3. Select **Processing result** to view generated files, their `FileId`, output resolution, format, size, and creation time.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261029112707-812931281248.png)

4. Click **Preview export** for a processed file to open it in a new browser tab. You can save the image from the browser.

Each image asset can retain up to 1,500 processed files. To remove outputs you no longer need, see [Delete images or processed files](https://docs.byteplus.com/en/docs/25/124104#delete-images-or-processed-files).

Configure an available [image domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management) for image distribution URLs. Console previews can use an external storage address when no image domain is available; this incurs [storage outbound traffic charges](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#storage-outbound-traffic-pricing). This fallback does not apply to [GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos): its `ImageUrl` is empty when the space has no usable image domain.

### Delete images or processed files

* To delete one processed file, open **Details** \> **processing result**, locate the file, and click its **Delete** action.

* To delete an image asset together with all its processed files, use **Delete** on the **Uploaded** list in **Pid mode**. Select multiple images to use the list's batch **Delete** action.

Check the selected scope in the confirmation dialog before confirming deletion.

## Manage images through APIs

|API |Purpose |
|---|---|
|[GetImageList](https://docs.byteplus.com/docs/byteplus-vod/reference-getimagelist) |List and search image assets. |
|[GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos) |Retrieve original and processed image information. |
|[UpdateImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-updateimageinfos) |Update image titles, descriptions, tags, and categories. |
|[DeleteImages](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteimages) |Delete original images and their processed files. |
|[DeleteImageProcessResults](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteimageprocessresults) |Delete selected processed files. |
|[ListFileMetaInfosByFileNames](https://docs.byteplus.com/docs/byteplus-vod/listfilemetainfosbyfilenames) |Look up image metadata and the PID by storage URI. |

For processing APIs and task queries, see [API workflow](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement#api-workflow). For deletion events, see [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).
