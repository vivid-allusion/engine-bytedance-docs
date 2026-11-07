---
title: "Video editing error codes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/video_editing_error_codes"
---

If you encounter an error while using the video editing feature, this article helps you identify its cause and find a solution. It provides a comprehensive list of error codes returned in the `Message` parameter of the [GetDirectEditProgress](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getdirecteditprogress) API, covering issues related to resource downloading, uploading, video editing and processing.

<span id="ec57aaf6"></span>
### Downloading error codes


|**Error Code** |**Scenario** |**Description** |
|---|---|---|
|**`22020001`** |Resource download failed due to a user parameter error |Resource download failed. Verify the resource's validity or [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
|**`22021001`** |Resource download failed due to a user parameter error |The `StoreUri` does not exist. You may have deleted the resource or it is invalid. Verify that the resource exists and is valid. |
|**`52020002`** |System error, resource download failed |Download timeout. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
|**`12020003`** |System error, resource download failed |Download throttling. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support to increase the storage throttling limit. |


<span id="266fb4fa"></span>
### Uploading error codes


|**Error Code** |**Scenario** |**Description** |
|---|---|---|
|**`55020009`** |System error, resource upload failed |The uploaded file is empty (0 bytes). This may be an output artifact issue. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
|**`15020010`** |System error, resource upload failed |Upload failed. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |


<span id="54953c02"></span>
### Editing and processing error codes


|**Error Code** |**Scenario** |**Description** |
|---|---|---|
|**`21020004`** |User parameter error, parameter type validation failed |Request parameter error. You can adjust the request parameters according to the error message, including parameter type and required field validation. |
|**`29090001`** |User parameter error, empty track |The track is empty. You can adjust the request parameters. |
|**`29090004`** |User parameter error, invalid track duration |The track duration is less than or equal to 0. You can adjust the request parameters. |
|**`14090006`** |System error, video stream synthesis failed |Synthesis failed. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
|**`14090007`** |System error, audio stream synthesis failed |Synthesis failed. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
|**`19020005`** |System error, unknown error |Unknown error. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
|**`17999903`** |Task retrieval failed |Unknown error. You can [create a new ticket](https://console.byteplus.com/workorder/create) to contact technical support. |
