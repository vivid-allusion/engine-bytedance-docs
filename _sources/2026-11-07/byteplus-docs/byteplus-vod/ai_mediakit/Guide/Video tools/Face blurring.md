---
title: "Face blurring"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-face-mosaic"
---

The AI MediaKit Face Blurring tool automatically and accurately detects face regions in a video and applies a blur or mosaic effect to all faces. Many AI video generation platforms, such as Seedance 2.0, enforce strict content policies that block reference videos containing real human faces. Face blurring eliminates this friction by pre\-processing your videos automatically. Whether you are a content creator or a platform operator, you can easily implement video privacy protection through our service without manual and tedious anonymization work.

This guide walks you through:


* A quickstart on applying a mosaic to faces in a video.

* How to use the various parameters to fine\-tune the method, strength, and scope of the masking.


<span id="7d2250e7"></span>
## Demo

With the Face Blurring tool, you can take a video containing faces as input and quickly generate a video in which all faces are precisely masked with a mosaic or Gaussian blur.


|Input video |Output video |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/886e33bf9e194bcdabee2503ab5a464d" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8a0f3a7c184c4a3f893c08763ca2f76c" controls></video><br> |


<span id="quickstart-apply-a-mosaic-to-faces"></span>
## Quickstart: Apply a mosaic to faces

This section demonstrates how to quickly generate a video with mosaicked face regions.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing. Make your video file accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Face blurring is an asynchronous task. The complete workflow is as follows:


1. Call `POST /api/v1/tools/face-blur-video` and get a `task_id` for querying.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field in the response to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a face blurring task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-face-mosaic-task) API. You can copy the following cURL command to submit a masking task using default parameters (mosaic, medium strength).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_url": "https://vod-ai-test.bytepluses.com/demo/drama_ep01.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with your own URL.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-face-blur-video-123456789",
  "request_id": "20260415160000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. You can find the download URL of the final masked video in the `result.video_url` field (valid for **24 hours** by default).

```JSON
{
    "success": true,
    "task_id": "amk-tool-face-blur-video-123456789",
    "request_id": "20260415160000ABCDEFG12345",
    "status": "completed",
    "result": {
        "video_url": "https://example.com/blurred_video.mp4?auth_key=...",
        "duration": 180.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


<span id="advanced-usage"></span>
## Advanced usage

Building on the quickstart, you can achieve more fine\-grained masking effects by configuring different parameters when submitting a task.

<span id="choose-the-masking-method-gaussian-blur-or-mosaic"></span>
### Choose the masking method: Gaussian blur or mosaic

Use `mask_mode` to choose whether to apply a mosaic or a Gaussian blur to face regions.


* `mosaic`: (Default) Mosaic.

* `blur`: Gaussian blur.


<span id="example-mask-using-gaussian-blur"></span>
#### **Example: Mask using Gaussian blur**

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "mask_mode": "blur"
}'
```


<span id="adjust-the-masking-strength"></span>
### Adjust the masking strength

Use `mask_strength` to control the strength of the masking to accommodate different levels of privacy protection.


* `low`: Low strength.

* `medium`: (Default) Medium strength.

* `high`: High strength.


<span id="example-mask-with-high-strength"></span>
#### **Example: Mask with high strength**

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "mask_strength": "high"
}'
```


<span id="expand-the-masking-scope"></span>
### Expand the masking scope

To more completely cover the face contour, you can use `face_box_expand` to set an expansion ratio that enlarges the masking area outward from the face bounding box detected by the system. For example, `0.2` means expanding 20% outward on each edge of the original bounding box.

<span id="example-expand-the-masking-scope-by-20-outward"></span>
#### **Example: Expand the masking scope by 20% outward**

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "face_box_expand": 0.2
}'
```


<span id="adjust-the-face-detection-sensitivity"></span>
### Adjust the face detection sensitivity

Use `face_confidence` to adjust the confidence threshold for face detection, controlling how strict the face recognition is. The higher the value, the more conservative the detection (i.e., requiring higher face similarity), which may miss some blurry or non\-frontal faces; the lower the value, the more likely some non\-face objects are misidentified as faces. The value range is `[0.1, 1.0]`, with a default of `0.35`.

<span id="example-set-a-higher-detection-confidence"></span>
#### **Example: Set a higher detection confidence**

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "face_confidence": 0.5
}'
```


<span id="only-mosaic-upright-faces"></span>
### Detect upright faces only

In some scenarios, such as news footage, videos might contain faces that are lying down or upside down. To detect these non\-upright faces, the system needs to rotate the frame for inspection, which increases processing time. However, in most common scenarios like TV series or e\-commerce videos, faces are generally upright. In such cases, you can enable this parameter to skip the rotation check, significantly reducing the processing time.


* `true`: (Default) The system only detects and processes upright or slightly angled faces (including side faces), but does not detect faces that are lying down, upside down, or tilted at large angles. This mode is faster.

* `false`: The system attempts to detect and process faces in all orientations, including those lying down or upside down. This mode has a wider detection range but takes longer to process.


If you need to mosaic as many faces as possible in a video (for example, to anonymize footage from a public space), we recommend setting `upright_face_only` to `false`.

<span id="example-mask-all-faces-including-side-profiles"></span>
#### **Example: Mask faces** in all orientations

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://vod-ai-test.tos-cn-beijing.volces.com/demo/drama_ep01.mp4",
  "upright_face_only": false
}'
```


<span id="references"></span>
## References

<span id="4487ba06"></span>
### Limits


|Category |Specifications |
|---|---|
|Input video |* **Video source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution**: Up to 4K; 1080P is recommended.<br><br>* **Duration**: Must not exceed 10 minutes.<br><br>* **Frame rate**: Must be within 25–60.<br><br>* **Encoding format**: H.264. |
|Output video |**Format**: MP4 (Video: H.264, Audio: AAC). |
|Maximum faces per frame |Up to 10 faces. |
|Concurrent tasks |Up to 20 concurrent jobs per account. |


<span id="aa6b9902"></span>
### Processing time estimation

You can estimate the wait time using the **RTF (Real\-Time Factor)** , where:

Estimated processing time = Video duration × RTF

The RTF for face blurring is 4–17. This means processing is 4 to 17 times faster than real time, and the processing time is the video duration divided by the RTF. For example, a 1\-minute video can be processed in approximately 3.5 to 15 seconds.

<span id="related-api-references"></span>
## Related APIs


* [Create a face blurring task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-face-mosaic-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
