---
title: "ImageDeleteComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-imagedeletecomplete"
---

The `ImageDeleteComplete` event is sent when deletion of image assets and their processed files completes. Use `JobId` to associate the notification with the task returned by [DeleteImages](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteimages).

For callback configuration and delivery, see [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

## Parameters

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RequestId |String |`a586ea18d0cd4f9ba41edb9a67e3fd92` |The callback request ID. |
|Version |String |`1.0` |The callback version. |
|EventType |String |`ImageDeleteComplete` |The event name. |
|EventTime |String |`2026-10-16T10:11:21Z` |The time when the event occurred, in UTC. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/25/124091#data) |`-` |The callback content. |

## Data

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CallbackArgs |String |`""` |The custom information passed through from the API request. |
|Code |String |`Success` |The result code. `Success` indicates success. |
|JobId |String |`a586ea18d0cd4f9ba41edb9a67e3fd92` |The asynchronous deletion task ID. |
|Message |String |`Success` |The result message. |
|Results |Array of [ImageDeleteResult](https://docs.byteplus.com/en/docs/25/124091#imagedeleteresult) |`-` |The deletion result for each image. |

## ImageDeleteResult

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |String |`Success` |The deletion result code for this image. `Success` indicates success. |
|FileNames |Array of String |`["60e53fe3c870e8c29f3f2e13720b9dd7.jpg","86977c91e3321a0dcad45756ab49d73d.jpeg","15643d3cfa8ca02180bd24d12fd5f374.jpeg"]` |The file names deleted for this image, including its original file and processed files. |
|Message |String |`Success` |The deletion result message for this image. |
|Pid |String |`i256c3gm0018db8vc1itgd6bcq42r0e0` |The image asset ID. |

## Example

The following example shows a successful image deletion task.

```json
{
    "Data": {
        "CallbackArgs": "",
        "Code": "Success",
        "JobId": "a586ea18d0cd4f9ba41edb9a67e3fd92",
        "Message": "Success",
        "Results": [
            {
                "Code": "Success",
                "FileNames": [
                    "60e53fe3c870e8c29f3f2e13720b9dd7.jpg",
                    "86977c91e3321a0dcad45756ab49d73d.jpeg",
                    "15643d3cfa8ca02180bd24d12fd5f374.jpeg"
                ],
                "Message": "Success",
                "Pid": "i256c3gm0018db8vc1itgd6bcq42r0e0"
            }
        ]
    },
    "EventTime": "2026-10-16T10:11:21Z",
    "EventType": "ImageDeleteComplete",
    "RequestId": "a586ea18d0cd4f9ba41edb9a67e3fd92",
    "Version": "1.0"
}
```
