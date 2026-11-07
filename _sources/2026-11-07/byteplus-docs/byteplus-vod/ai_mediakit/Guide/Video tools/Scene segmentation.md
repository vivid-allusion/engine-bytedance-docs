---
title: "Scene segmentation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-scene-segmentation"
---

The AI MediaKit Scene Segmentation tool intelligently analyzes video content and, based on shot changes, transitions, and changes in the visual content, automatically splits a long video into multiple meaningful scene segments. The tool outputs the start and end timestamps for each segment and provides download URLs for the corresponding independent video files, helping you easily implement downstream applications such as video splitting, highlight reels, and keyframe extraction.

This guide walks you through:


* Understanding how scene segmentation works.

* Quickly obtaining scene timecodes and independent video files from a video.

* Learning how to adjust the segmentation granularity and obtain independent clip files.


<span id="effect-preview"></span>
## Demo

With the Scene Segmentation tool, you can achieve the following:


|Input video |Segmented videos |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a74edf56c9c4e02a96c4cf2e5f948ec~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b172e58c40546d8be1b7ef0dfe6ad1f~tplv-goo7wpa0wc-image.image" controls></video><br><br><br><video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db1d1ff911fd4686911510d4b43e9f6b~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="quickstart-get-scene-timeline-and-clip-files-from-a-video"></span>
## Quickstart: Get scene timestamps and clip files from a video

This section uses a concrete example to demonstrate how to perform scene segmentation on a video file and obtain the start/end timestamps and independent video files of all scene segments.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

2. **Prepare a video file**: Have a video file ready for processing. Make it accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Scene segmentation is an asynchronous task. The overall workflow is as follows:


1. Call `POST /api/v1/tools/segment-scenes` and get a `task_id` to query the task status.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field in the response to get the information of all scene segments from the `segments` array.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a scene segmentation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-scene-segmentation-task) API. You can copy the following cURL command to submit a basic scene segmentation task to the API.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/segment-scenes' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own prepared video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-segment-scenes-123456789",
  "request_id": "20240521130000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video processing takes time, you need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed` to get the final result.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `segments` array in the `result` field contains the timestamps and independent video file download URLs for all clips.

```JSON
{
    "success": true,
    "task_id": "amk-tool-segment-scenes-123456789",
    "status": "completed",
    "result": {
        "duration": 185.5,
        "segments": [
            {
                "start_time": 0.0,
                "end_time": 15.2,
                "segment_video_url": "https://example.com/clip_1.mp4"
            },
            {
                "start_time": 15.2,
                "end_time": 45.8,
                "segment_video_url": "https://example.com/clip_2.mp4"
            },
            {
                "start_time": 45.8,
                "end_time": 185.5,
                "segment_video_url": "https://example.com/clip_3.mp4"
            }
        ]
    }
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="adjust-the-segmentation-granularity"></span>
### Adjust the segmentation granularity

You can use the `segment_threshold`, `min_duration`, `max_duration`, and `enable_clip_fade` parameters to fine\-tune the scene segmentation results.


* `segment_threshold`: The sensitivity threshold for scene segmentation. The range is [0, 100]. The recommended empirical value is `10`.

   * The lower the value, the more granular the segmentation: The algorithm is more sensitive to visual changes and may identify even subtle changes as segmentation points.

   * The higher the value, the coarser the segmentation: The algorithm ignores some less significant scene changes.

* `min_duration`: The minimum duration (in seconds) of a single clip. Any segment shorter than this duration is automatically merged into an adjacent segment.

* `max_duration`: The maximum duration (in seconds) of a single clip. Any segment longer than this duration is forcibly split.

* `enable_clip_fade`: Whether to output the detected fade\-in/fade\-out segments as independent clips. The default is `false`.


The following is an example request showing how to use these parameters to customize your scene segmentation task:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/segment-scenes' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4",
  "segment_threshold": 15,
  "min_duration": 2.5,
  "max_duration": 30,
  "enable_clip_fade": true
}'
```


In this example, the API will:


* Perform segmentation with a sensitivity of 15.

* Ensure that each generated video clip is at least 2.5 seconds long.

* Forcibly split any scene that lasts longer than 30 seconds.

* Identify fade\-in/fade\-out effects in the video and output them as independent segments.


<span id="references"></span>
## References

<span id="limits-and-performance"></span>
### Limits and performance


|Limit |Description |
|---|---|
|**Input file limits** |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Video duration**: A single video must not exceed 2 hours. |


<span id="related-apis"></span>
## Related APIs


* [Create a scene segmentation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-scene-segmentation-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
