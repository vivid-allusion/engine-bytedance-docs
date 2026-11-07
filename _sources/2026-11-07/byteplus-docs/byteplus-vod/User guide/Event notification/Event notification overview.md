---
title: "Event notification overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-callback-notifications-"
---

To receive timely notifications when asynchronous tasks like video uploads or media processing complete, you can use the BytePlus VOD event notification feature. When a task finishes, VOD sends a notification callback to your service, allowing you to automate subsequent business processes. This document explains the callback mechanism and lists all supported events.

## **Introduction**

Operations in BytePlus Video on Demand (VOD), such as the completion of a video upload or a workflow, are considered events. These tasks require some time to complete. To ensure timely notification upon task completion, VOD provides an event notification callback feature. When an event is completed, VOD sends a callback message to you. You can then handle subsequent business processes. VOD currently supports HTTP callbacks, which means VOD pushes event notifications to your service. The callback event notification is configured at space level.

## **Callback mechanism**

The BytePlus VOD callback mechanism operates as follows:

1. When a specific event occurs, such as the completion of a task, the BytePlus VOD server sends a POST request to the URL that you have configured in the console.

2. To indicate a successful callback, your HTTP/HTTPS service should respond with a 200 status code.

3. If a callback fails, the BytePlus VOD server makes three retry attempts at intervals of 5, 10, and 30 seconds. If all retry attempts fail, the event notification is discarded.

## **Configuring event notifications**

* **Console:**  See [Callbacks](https://docs.byteplus.com/docs/byteplus-vod/docs-system#aed0518b).

* **OpenAPI:**

   * Set callback events using [SetCallbackEvent](https://docs.byteplus.com/docs/byteplus-vod/reference-setcallbackevent).

   * Add callback subscription addresses using [AddCallbackSubscription](https://docs.byteplus.com/docs/byteplus-vod/reference-addcallbacksubscription).

* **Server SDKs:**

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

## **Event list**

The following table provides a list of events and their descriptions:

|**Event** |**Description** |
|---|---|
|[FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) |Occurs when a file upload is complete. |
|[FileUploadByUrlComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadbyurlcomplete) |Occurs when a batch upload via URL is complete. |
|[WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) |Occurs when a workflow execution is complete. |
|[DeleteMediaComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-deletemediacomplete) |Occurs when the deletion of an audio or video file is complete. |
|[DeleteTranscodesComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-deletetranscodescomplete) |Occurs when all transcoded files for an audio or video file are deleted. |
|[MaterialUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-materialuploadcomplete) |Occurs when a material upload is complete. |
|[UploadGetMetaComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-uploadgetmetacomplete) |Occurs when the metadata extraction is complete. |
|[ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete) |Occurs when the media processing task is complete. |
|[ImageProcessComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imageprocesscomplete) |Occurs when an image enhancement or basic image processing task completes. |
|[ImageDeleteComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imagedeletecomplete) |Occurs when deletion of an image asset and its processed files completes. |
