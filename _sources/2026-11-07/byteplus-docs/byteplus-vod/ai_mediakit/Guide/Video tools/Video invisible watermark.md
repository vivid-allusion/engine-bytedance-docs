---
title: "Video invisible watermark"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-invisible-watermark"
---

The AI MediaKit Video Invisible Watermark tool invisibly embeds a string of numeric information, such as a user ID or content ID, into a video file without affecting the video's visual quality or integrity. This technology is essential for video copyright protection, content leak tracing, and file authenticity verification. Even if the video is compressed, transcoded, cropped, or screen\-recorded, there is still a high probability that the embedded invisible watermark can be successfully extracted, providing strong evidence for copyright tracking and rights protection.

This guide walks you through:

* How the Video Invisible Watermark tool works.

* How to get started by adding an invisible watermark to a video through the API and successfully extracting it from the processed video.

* How to adjust the watermark's resistance to attacks through parameters.

## How it works

The core Video Invisible Watermark workflow consists of two main stages, "add" and "extract":

1. **Add an invisible watermark**: Takes the source video and a custom numeric string (the watermark content) as input. The algorithm processes them to produce a new video that looks identical to the naked eye but contains the hidden information.

2. **Extract an invisible watermark**: Takes a suspected leaked or pirated video as input and analyzes it through the Video Invisible Watermark extraction API to restore the numeric information that was originally embedded. If multiple invisible watermarks have been embedded in the same video, the tool can extract all of them.

## Quickstart: Add and extract a Video Invisible Watermark

This section demonstrates the complete workflow of adding an invisible watermark to a video and extracting it through API calls.

### Prerequisites

* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and copy your API Key.

* **Prepare a video file**: Prepare a video file and upload it to a publicly accessible server or the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain a URL that the API can access.

### Procedure

Adding and extracting an invisible watermark is a workflow consisting of two asynchronous tasks with the following core steps:

1. **Submit an invisible watermark add task and get the output**:

   1. Call `POST /api/v1/tools/add-video-invisible-watermark` to submit an invisible watermark add task.

   2. Poll `GET /api/v1/tasks/{task_id}` until the task is complete, and then parse the URL of the video with the invisible watermark (`video_url`) from the `result` field in the response.

2. **Submit an invisible watermark extraction task and get the result**:

   1. Call `POST /api/v1/tools/extract-video-invisible-watermark`, passing in the video URL obtained in the previous step, to submit an invisible watermark extraction task.

   2. Poll `GET /api/v1/tasks/{task_id}` for the final task status. After the task is complete, obtain the extracted watermark content (`watermark_contents`) from the `result` field.

#### Step 1: Submit a Video Invisible Watermark add task

First, call the Create a Video Invisible Watermark add task API to embed the numeric information you specify into a video. You can copy the following cURL command to submit the task. This example embeds the numeric string `"12345678901234567"` into the video as the invisible watermark content.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-video-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/demo/drama_ep01.mp4",
  "watermark_content": "12345678901234567"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > `video_url`: Replace the placeholder URL in the example with your own video URL.

After the request is successfully submitted, you receive a `task_id` for querying the progress, for example, `{add_watermark_task_id}`.

Next, use this `task_id` to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API. When the task `status` becomes `completed`, **locate and save the value of** **`video_url`** in the response's `result` field. This URL points to the video in which the invisible watermark was successfully embedded. The following is an example response for a successfully completed invisible watermark add task:

```JSON
{
    "success": true,
    "task_id": "{add_watermark_task_id}",
    "status": "completed",
    "result": {
        "video_url": "https://example.com/watermarked_output.mp4",
        "duration": 120.5,
        "resolution": "1080p"
    }
}
```

#### Step 2: Submit a Video Invisible Watermark extraction task

After obtaining the URL of the video with the invisible watermark, call the Create a Video Invisible Watermark extraction task API to parse the information hidden in it. Replace the `video_url` value in the following cURL command with the `video_url` obtained in the previous step, and then submit the request.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-video-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/watermarked_output.mp4"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > Replace `video_url` with the URL of the video with the invisible watermark obtained from the polling result in Step 1.

After the request is successfully submitted, you receive a new `task_id`, for example, `{extract_watermark_task_id}`. Save this ID for querying the extraction result.

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API again until the task `status` becomes `succeeded`.

After the task is successfully completed, you receive the following response. You can find the extracted invisible watermark content in the `result.watermark_contents` array.

```JSON
{
    "success": true,
    "task_id": "{extract_watermark_task_id}",
    "status": "succeeded",
    "result": {
        "watermark_contents": [
            {
                "watermark_content": "12345678901234567"
            }
        ],
        "duration": 120.5
    }
}
```

#### Step 3: Compare the watermark content

Compare the watermark content extracted in Step 2 (`"12345678901234567"`) with the watermark content embedded in Step 1. If they match, the source of the video has been successfully verified.

## Advanced usage: Adjust the invisible watermark strength

When calling the Create a Video Invisible Watermark add task API, you can use the `watermark_level` parameter to adjust the invisible watermark strength. The strength determines the balance between the watermark's resistance to attacks (its ability to withstand video compression, transcoding, screen recording, and other processing) and its impact on the image.

* **Stronger attack resistance**: The watermark is less likely to be lost and more likely to be successfully extracted after various forms of secondary processing.

* **Impact on the image**: Although an invisible watermark is designed to be imperceptible to the naked eye, it still modifies the video's pixel data. A higher strength results in relatively greater changes to the source image.

You can choose from the following strength levels based on your business scenario:

* `normal`: (Default) Standard strength. Provides a good balance between image quality and attack resistance and is suitable for most scenarios.

* `high`: High strength. Provides the strongest attack resistance and can withstand more intensive video processing, such as high\-compression\-ratio transcoding and repeated screen recording, but it may also have a relatively greater potential impact on the image.

### Example: Add a high\-strength invisible watermark

```JSON
{
  "video_url": "https://example.com/demo/drama_ep01.mp4",
  "watermark_content": "987654321",
  "watermark_level": "high"
}
```

## Typical scenarios and best practices

This section describes typical Video Invisible Watermark workflows and best practices in real\-world business scenarios to help you protect your digital assets more effectively.

### Scenario 1: End\-to\-end tracing for AI\-generated videos

In AI\-generated content (AIGC) applications, you often need to protect not only the final composite output but also trace it back to the specific source materials used to create it. By adding different layers of invisible watermarks to the source materials and the final output, you can establish a complete copyright tracing chain.

**Recommended workflow:**

1. **Asset\-level watermark**: Suppose you generated video clip A and video clip B with AI. Call the Video Invisible Watermark add API separately for the two videos and embed a first\-layer watermark using `high` strength to identify each source asset.

2. **Content concatenation**: Concatenate videos A and B, which contain the first\-layer watermarks, to generate the final video C.

3. **Final\-output watermark**: Call the Video Invisible Watermark add API again to embed a second\-layer watermark in the final video C using `normal` strength. This layer identifies the content that is ultimately distributed, for example, by marking the distribution channel or purchaser's user ID.

**Result:**

* If only video A or B is leaked, you can extract the first\-layer watermark from the leaked clip to identify exactly which source asset was leaked.

* If the final video C is pirated, you can extract both layers of watermarks from the pirated video. This lets you trace the distribution of the final output and associate it with the source asset information contained in the video.

> **INFO**

> **Process first, then add the watermark:** To ensure the invisible watermark's attack resistance and extraction success rate, we strongly recommend completing all other video processing operations, such as quality enhancement, subtitle removal, trimming, and concatenation, **before** adding the invisible watermark. Editing a video that already contains an invisible watermark may damage the embedded information and prevent it from being extracted correctly.

### Scenario 2: Enhance video attack resistance with two watermark layers

For core video content with extremely high copyright value and stringent anti\-piracy requirements, you can maximize attack resistance by layering two invisible watermarks of different strengths to defend against malicious operations such as recompression and screen recording.

**Recommended workflow:**

1. **First\-layer watermark**: Call the Video Invisible Watermark add API for the source video and embed the first\-layer watermark, for example, using `high` strength, to produce video A.

2. **Second\-layer watermark**: Call the Video Invisible Watermark add API again for video A and embed a second\-layer watermark using a strength different from the first layer, for example, `normal`.

The Video Invisible Watermark extraction API can automatically identify and parse both watermark layers in a video.

**Result:**

* **Enhanced attack resistance**: Using watermarks of different strengths is equivalent to applying different algorithms and embedding strategies. Even if a pirate happens to damage one watermark layer through a particular type of processing, there is still a high probability that the other layer will remain intact and can be successfully extracted.

* **Balance between cost and benefit**: From the perspective of attack and defense costs and technical effectiveness, layering two invisible watermarks is generally sufficient for most high\-security scenarios, making it a cost\-effective protection approach.

## Usage limits

|Limit |Description |
|---|---|
|Input video |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `mov`, `mkv`, `flv`, `ts`, `avi`, and `wmv`.<br><br>* **Resolution**: Up to 4K. |
|Watermark content |* **Format**: Must be a string containing digits only, for example, `"12345"`.<br><br>* **Range**: The number represented by the string must be between `1` and `9223372036854775807` (a positive 64\-bit integer).<br><br>* **Constraints**: Leading zeros, such as in `"0123"`, and non\-numeric characters are not allowed. |
|Compatibility |The Video Invisible Watermark extraction API only supports extracting watermarks embedded by the Video Invisible Watermark add API. It cannot extract any form of invisible watermark added by third\-party tools. |

## Related APIs

* [Create a video invisible watermark add task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-video-invisible-watermark-add-task)

* [Create a video invisible watermark extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-video-invisible-watermark-extraction-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
