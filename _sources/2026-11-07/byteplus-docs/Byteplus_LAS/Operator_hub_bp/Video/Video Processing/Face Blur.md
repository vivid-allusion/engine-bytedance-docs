---
title: "Face Blur"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Face_Blur"
---

The face blur operator provides face detection and blurring for video content. It can output a blurred video and per\-frame face bounding boxes in a JSON file together, or return either result on its own.

# Operator introduction

> Operator ID: las_face_blur

## Application scenarios

|**Scenario** |**Description** |
|---|---|
|Privacy protection |Automatically blur faces on social media and video sharing platforms to protect user privacy |
|Content moderation |Blur faces in user\-uploaded videos to meet compliance requirements |
|Video production |Protect interviewees' privacy in news, documentaries, and other productions |
|Face blur preprocessing in training/evaluation datasets |When training/evaluating models, blur faces in video frames in the dataset to improve model generalization |

## Core capabilities

* Applies blur processing to faces in the input video and returns the processed video.

   * Automatically detects faces in video frames and applies blur processing.

   * Supports multiple blur types (mosaic, Gaussian).

   * Supports fine\-grained blur for various regions (such as elliptical face blur, fitted face blur, eye region blur, and more).

* Supports flexible output selection through `outputs`: request a blurred video and a per\-frame face bbox JSON file together, or return only the video or only the bbox JSON file.

* `blur_mode=detect` is retained for backward compatibility. For new requests, use `outputs=["bbox"]` for bbox\-only output.

## Effect demonstration

---

**Multiple face blur effects**

* Input video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10f5e58ee75e476bb40bd9e5ef882ecd~tplv-goo7wpa0wc-image.image)

* Face oval blur

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff4bc1efbfe14199952e96036ac81d0c~tplv-goo7wpa0wc-image.image)

* Face mosaic blur

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3ebd555de8c4af4ba29447279d362e8~tplv-goo7wpa0wc-image.image)

* Close\-fitting face blur

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9eff60777a34627927ddcfc830a8b91~tplv-goo7wpa0wc-image.image)

* Eye blur

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c94efd5462d046c587fd0e91457e790c~tplv-goo7wpa0wc-image.image)

---

**Face bbox detection and blurring**

* Core parameters

   ```json
   {
     "outputs": [
       "video",
       "bbox"
     ],
     "blur_mode": "face",
     "blur_type": "gaussian",
     "preserve_audio": true,
     "blur_strength": 99,
     "confidence_threshold": 0.6,
     "draw_box": false
   }
   ```

* Face bbox output excerpt

   ```json
   {
     "video": {
       "fps": 30.0,
       "width": 1080,
       "height": 1920,
       "total_frames": 2880,
       "duration_seconds": 96.0
     },
     "box_format": "[x1, y1, x2, y2]",
     "frames": [
       {
         "frame_index": 7,
         "faces": [
           {
             "box": [575, 780, 606, 818],
             "confidence": 0.608485
           }
         ]
       }
     ],
     "summary": {
       "total_faces": 3192,
       "frames_with_faces": 2395,
       "max_faces_in_frame": 5
     }
   }
   ```

* [Download the complete face bbox JSON](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/dbaf9ac1-c924-4716-9bc2-b2b0e26366d5.json)

* Gaussian\-blurred video output

   [video](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/6173e98b-99e6-45e3-b1ab-3b7bc00489de.mp4)

---

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Sub\-item |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Processing time |Directly proportional to video duration. |

# Input and output requirements

## Input requirements

|Subdivision |Detailed description |
|---|---|
|Supported input data modalities |Video |
|Input format: video |* Formats: mp4, mov, avi, mkv, flv, webm, and other common formats<br><br>* Size: up to 10 GB. |
|Input path requirements |Provide input data to the operator using the `url` request parameter. Currently, public URLs and TOS paths are supported.<br><br><br>* **Public URL**: A video URL accessible via the public internet, format is `http/https`.<br><br>* **TOS path**: Use an object in a TOS bucket under the same primary account and in the same region as the current LAS service. The calling account must have permission to read the object. Format: `tos://bucket_name/demo`. |

## Output requirements

|Subdivision |Detailed description |
|---|---|
|Output data modalities |* Video<br><br>* Text (face detection bbox JSON file) |
|Output format: video |Format, resolution, and duration are consistent with the original video |
|Output path requirements |Results are delivered in the following forms:<br><br><br>* **TOS path**: Set `output_tos_path` to a writable TOS bucket directory under the same primary account and in the same region as the current LAS service. The calling account must have permission to write to the directory. Format: `tos://bucket/output/`.<br><br>* **Presigned URL**: Poll returns presigned download URLs for the generated video and bbox JSON file. The URLs are valid for 2 hours. |

# Billing instructions

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing item |Charges are calculated based on the duration of the output video. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual usage. Billing precision: rounding |
   |Unit price |0.1 USD/minute |

* Billing details

   Billing formula: `Total cost = unit price * usage`

# Notes and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## API usage instructions

* The API for this operator is an asynchronous task interface. You need to submit a task through the `Submit` interface to obtain the task's `task_id`, then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator processing result.

* Caution: After submitting a task, the `task_id` is valid for 3 days. After 3 days, you will not be able to use this `task_id` to obtain the operator processing result.

## Submit

### API description

Submit the las_face_blur operator to perform a face blur task.

### Request parameters

**operator_id** string 必选 `Example value: las_face_blur`

The ID of this operator is `las_face_blur`.

**operator_version** string 必选 `Example value: v1`

Currently only `v1` is supported.

**data** FaceBlurReqParams 必选

Operator parameters

**url** string 必选 `Example value: tos://xxx/video.mp4`

Input video path. Supported formats: `mp4`, `mov`, `avi`, `mkv`, `flv`, `webm`. Maximum video size: 10 GB.

**output_tos_path** string 必选 `Example value: tos://testbucket/path/`

TOS path to save results (`tos://bucket/key`). When both video and bbox are requested, the bbox JSON file is saved in the same directory as the video.

**output_filename** string

Custom output filename (basename only; directories are not allowed). For bbox\-only output, use a `.json` filename. For video\-only output, normally use `.mp4`. When both outputs are requested, normally use `.mp4`; the bbox filename is derived as `<video_filename_without_suffix>_face_bbox.json`. If omitted, the service derives the filename from the input URL.

**outputs** array of string `Example value: ["video", "bbox"]`

Output artifact types. Supports `video` (blurred video) and `bbox` (per\-frame face bbox JSON); both may be requested and values cannot be duplicated. If omitted, the value is inferred from `blur_mode`: `detect` maps to `bbox`, while all other modes map to `video`.

**blur_mode** string `Example value: face`

Blur region mode. Supports `face`: oval face blur, `face_oval`: face\-shaped blur, and `eyes`: eye\-region blur. Default is `face`. `detect` is deprecated and retained only for backward compatibility; use `outputs=["bbox"]` instead. The detect mode does not support video output.

**blur_type** string `Example value: gaussian`

Blur type. Supports `gaussian` and `mosaic`. Effective only when blurred video output is requested. Default is `gaussian`.

**preserve_audio** boolean `Example value: true`

Whether to preserve the original audio in the output video. Effective only when blurred video output is requested. Default is true.

**blur_strength** integer `Example value: 99`

Gaussian blur strength (kernel size). Effective only when blur_mode != detect and blur_type is gaussian. Larger value: heavier blur and stronger anonymization, but blurrier output, more haloed edges, slower computation. Smaller value: clearer and faster, but weaker anonymization. Default is 99. Range: [3, 151].

**mosaic_scale** integer `Example value: 16`

Mosaic scale factor. Effective only when blur_mode != detect and blur_type is mosaic. Larger value: larger blocks and rougher look, stronger anonymization. Smaller value: finer blocks and more natural look, but weaker anonymization. Default is 16. Range: [2, 64].

**confidence_threshold** float `Example value: 0.6`

Detection confidence threshold. Larger value: fewer false positives but more missed detections. Smaller value: more detected targets but more false positives (non\-human faces may also get blurred). Default `0.6`, range `(0, 1]`.

**draw_box** boolean `Example value: false`

Whether to draw face boxes in the output video. Effective only when blurred video output is requested. Default is false.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-xxx`

Task ID in async mode, used for job status polling.

**task_status** string `Example value: PENDING`

Task status in async mode.

* PENDING, request received

* RUNNING, running

* COMPLETED, completed

* FAILED, failed

* TIMEOUT, timeout

**business_code** string `Example value: 0`

Business code.

**error_msg** string

If any exception occurs, detailed error information will be returned.

### Example

#### Request example

```Bash
# Please set OUTPUT_PATH_TEMPLATE to a writable TOS path for this account
export OUTPUT_PATH_TEMPLATE="tos://xxxx/output/"
# Initiate an operator service request
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_face_blur",
    "operator_version": "v1",
    "data": {
        "url": "tos://xxxx/sample.mp4",
        "output_tos_path": "$OUTPUT_PATH_TEMPLATE"
    }
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20251125163544-abc123",
    "task_status": "PENDING",
     "business_code": "0",
    "error_msg": ""
  }
}
```

### Error code

|**HttpStatusCode** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameters |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.InValid |The api key is invalid. |Invalid API key |

## Poll

### API description

Query the execution status and result of the face blur task.

### Request parameters

**operator_id** string 必选 `Example value: las_face_blur`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**task_id** string 必选 `Example value: task-xxx`

Task ID

### Response parameters

**metadata** metadata

Request metadata.

**task_status** string `Example value: COMPLETED`

Task status.

* ACCEPTED, request accepted

* RUNNING, running

* COMPLETED, completed

* FAILED, failed

* TIMEOUT, timeout

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.

**business_code** string `Example value: 0`

Business code.

**error_msg** string `Example value: The api key is invalid.`

If any exception occurs, detailed error information will be returned.

**task_id** string `Example value: task-xxx`

Task ID in async mode.

**data** FaceBlurResponse

Response data.

**output_tos_uri** string `Example value: tos://bucket/test.mp4`

Backward\-compatible output path. Points to the blurred video when video is requested, or to the per\-frame face bbox JSON file for bbox\-only output.

**output_url** string `Example value: https://bucket/xxx&X-Tos-SignedHeaders=xxx`

Pre\-signed download URL for `output_tos_uri`, valid for 2 hours.

**bbox_output_tos_uri** string `Example value: tos://bucket/test_face_bbox.json`

Path of the bbox JSON file. Returned only when bbox output is generated. For bbox\-only output, this is the same as `output_tos_uri`.

**bbox_output_url** string `Example value: https://bucket/xxx&X-Tos-SignedHeaders=xxx`

Pre\-signed download URL for `bbox_output_tos_uri`, valid for 2 hours. Returned only when bbox output is generated.

**duration_seconds** float `Example value: 123.36`

Video duration in seconds.

#### Bbox JSON file format

When `outputs` includes `bbox`, `bbox_output_tos_uri` and `bbox_output_url` point to the JSON file containing face detection results for the input video. For bbox\-only output, `output_tos_uri` and `output_url` also point to this JSON file; when both video and bbox are requested, the generic output fields point to the video.

* Field structure of the JSON file

**video** VideoMeta

Input video metadata.

**fps** float

Input video frame rate.

**width** int

Input video width, in pixels.

**height** int

Input video height, in pixels.

**total_frames** int

Total number of frames in the input video.

**duration_seconds** float

Input video duration, in seconds.

**summary** Summary

Summary of face detection results.

**total_faces** int

Total number of faces detected across all frames.

**frames_with_faces** int

Number of frames containing at least one face.

**max_faces_in_frame** int

Maximum number of faces detected in a single frame.

**box_format** string

Bbox coordinate format, default is `[ x1, y1, x2, y2]`.

**frames** list[Frame]

A list of frames with at least one detected face. Frames without detected faces are not included in this list.

**frame_index** int

Frame index in the input video.

**faces** list[FaceBBox]

List of face bounding boxes detected in the current frame.

**box** list[int]

Bounding box coordinates, ordered as specified by box_format.

**confidence** float

Detection confidence for the current bounding box.

Example

```JSON
{
  "video": {"fps": 30.0, "width": 1280, "height": 960, "total_frames": 5376, "duration_seconds": 179.2},
  "summary": {"total_faces": 3710, "frames_with_faces": 3710, "max_faces_in_frame": 1},
  "box_format": "[x1, y1, x2, y2]",
  "frames": [
    {"frame_index": 489, "faces": [{"box": [917, 3, 1001, 70], "confidence": 0.644342}]},
    {"frame_index": 490, "faces": [{"box": [915, 3, 1003, 72], "confidence": 0.807955}]}
  ]
}
```

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_face_blur",
    "operator_version": "v1",
    "task_id": "task-20251125163544-abc123"
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "06ecbd66031e7006022d",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "0",
    "error_msg": "Task processed successfully"
  },
  "data": {
    "output_tos_uri": "tos://{bucket}/xxx.mp4",
    "output_url": "https://{bucket}.tos-ap-southeast-1.bytepluses.com/xxx.mp4?xxx",
    "duration_seconds": 123.36
  }
}
```

### Error code

|**HttpStatusCode** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |Parameter.Missing |Missing required parameter. |Missing required parameter in request body |
|400 |Parameter.Invalid |Invalid parameter. |Invalid parameter |
|400 |Url.Invalid |Invalid URL. |The video URL cannot be accessed or does not exist |
|400 |Video.Invalid |Invalid video file. |Unsupported video format or corrupted file |
|400 |Video.DownloadFailed |Video download failed. |Download failed or access was denied |
|400 |Ffmpeg.error |Failed to process video. |Failed to process the video |
