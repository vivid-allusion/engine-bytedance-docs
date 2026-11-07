---
title: "Face mosaic"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-face-mosaic"
---

Face mosaic is a professional video privacy protection solution that provides efficient and accurate face/facial feature mosaicking capabilities. Many AI video generation platforms, such as Seedance 2.0, enforce strict content policies that block reference videos containing real human faces. Face mosaic eliminates this friction by pre\-processing your videos automatically. Whether you are a content creator or a platform operator, you can easily implement video privacy protection through our service without manual and tedious anonymization work.

<span id="3b84bcdd"></span>
## Key features

<span id="be442760"></span>
### Intelligent face detection

Adopting advanced face detection algorithms to accurately identify all faces in videos, supporting multi\-angle, multi\-pose, and multi\-person scenarios.

<span id="d70f19f3"></span>
### Flexible mosaic configuration

Configuration parameters are optional with sensible default values. You can use the default settings for quick implementation or customize them based on your needs:


* **Mosaic intensity**: low, medium, high (default: medium)

* **Masking method**: mosaic (pixelation) or blur (Gaussian blur) (default: mosaic)

* **Expand ratio**: configurable detection box expansion (default: 0.2)

* **Confidence threshold**: adjustable face detection confidence (default: 0.4)

* **Upright only**: process only upright faces (default: false)


<span id="2d5ef5fc"></span>
### Batch asynchronous processing

Each API call processes a single video. Batch workloads can be distributed across multiple concurrent calls, with a limit of 20 simultaneous jobs per account.

<span id="5bbca262"></span>
### Convenient result retrieval


* Automatic storage after processing completion

* Video URL and download capabilities


<span id="721566bb"></span>
## Capabilities and limitations


|Category |Specifications |
|---|---|
|Input format |`.mp4`, `.mov`, `.mkv`, `.webm`, `.avi` |
|Encoding format |H.264 |
|Output format |MP4 (H.264, AAC) |
|Frame rate |25–60 FPS |
|Real\-Time Factor (RTF) |4–17 |
|Resolution range |No limit |
|Maximum faces per frame |Up to 10 faces |
|Concurrent tasks |Up to 20 concurrent jobs per account |


<span id="226e99c0"></span>
## Pricing

Billing is based on processed video duration. For detailed pricing information, please refer to [Face mosaic pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#a6b9cac3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Content storage fees for the processed videos are not included in the Face mosaic processing fees. Storage will be charged separately based on your VOD space usage. For detailed pricing information, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#310bc067">Storage pricing </a>.</div>


<span id="1b9970d3"></span>
## Prerequisites


* Create a [BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console.

* Enable the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started) and create a space.

* [Upload video files](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to the target space and obtain the Vid or FileName.

* To preview or play the processed video through a public URL, [add and configure a domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-configuring) for the VOD space.


<span id="use-face-mosaic-via-the-console"></span>
## Use Face mosaic via the console

This section provides step\-by\-step instructions for starting a Face mosaic task in the BytePlus VOD console.

<span id="step-1-initiate-face-mosaic"></span>
### Step 1: Initiate Face mosaic


1. [Sign in to the VOD console](https://console.byteplus.com/vodpaas) and enter the target space.

2. Upload a video or select an existing video in the video list.

3. Click **AI processing** above the video list, and then select **Video face blur**. The Video face blur processing panel opens.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260714065307-1679032512719.png) </span>


<span id="step-2-configure-face-mosaic-parameters"></span>
### Step 2: Configure Face mosaic parameters

In the **Video face blur processing** panel, configure the following parameters.


|Parameter |Description |Options |
|---|---|---|
|Face blur strength |Sets the strength of the face blur effect. A higher strength provides stronger privacy protection. |Low, Medium, High |
|Face blur method |Controls the visual style of the face blur effect. |Mosaic, Gaussian Blur |
|Expansion ratio |Controls how far the detected face box extends outward. Increasing the value helps cover areas such as ears, hairline, and facial edges. |Default: `0.2` |
|Confidence level threshold |Controls how confidently the algorithm must detect a face before applying the effect. A lower value is more sensitive and reduces missed detections, while a higher value is stricter and reduces false detections. |Default: `0.4` |
|Only code the front face |When enabled, only upright faces are processed. |Default: off |


<span id="step-3-submit-the-face-mosaic-task"></span>
### Step 3: Submit the Face mosaic task

After the parameters are configured, click **Start processing**. The system starts the task asynchronously.

<span id="step-4-check-task-status-and-retrieve-results"></span>
### Step 4: Check task status and retrieve results


1. In the left navigation pane, choose **Media processing** \> **Tasks**.

2. Find the task whose Processing template is Face blur task. You can filter tasks by date or search for a specific task by its task ID.

3. Check the task status. When the status changes to **Success**, click **View details** in the Action column.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260714065443-1334552857577.png) </span>

4. In the Task process section, find the successful Face blur task subtask and click **View product**.

5. The console opens the details page of the processed video. Click the **Playback address** tab, and click **Preview** to play the processed video and verify the Face mosaic effect.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260714065501-622308629117.png) </span>


<span id="use-face-mosaic-via-the-api"></span>
## Use Face mosaic via the API

You can also initiate and manage Face mosaic tasks programmatically by calling the BytePlus VOD OpenAPI.

<span id="step-1-submit-a-face-mosaic-task"></span>
### Step 1: Submit a Face mosaic task

Call the [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-face-mosaic) API to submit a Face mosaic task. You can identify the target video by `Vid` or `DirectUrl`, and configure the task using `Operation.Task.FaceMosaic`.

Core parameters:


* `Input`: Specify the input video file.

   * `Type`: Set to `Vid` or `DirectUrl`.

   * `Vid` / `DirectUrl`: Provide the Vid or FileName of the file to be processed.

* `Operation.Task.Type`: Set to `FaceMosaic`.

* `Operation.Task.FaceMosaic`: Configure optional Face mosaic parameters, such as `Strength`, `Mode`, `Expand`, `Confidence`, and `UprightOnly`.


**Sample request:** 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The following HTTP example displays only core parameters and omits authentication details, such as the signature calculation in the <code>Authorization</code> header.</div>


```JSON
POST https://vod.byteplusapi.com?Action=StartExecution&Version=2025-07-01
{
    "Input": {
        "Type": "Vid",
        "Vid": "v0325cg10001*****"
    },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "FaceMosaic",
            "FaceMosaic": {
                "Expand": 0.2,
                "Confidence": 0.4,
                "Mode": "blur",
                "Strength": "medium",
                "UprightOnly": false
            }
        }
    }
}
```


You will receive the `RunId` of the task to query the execution result.

**Sample response:** 

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202605110303554EEC20674E***1FA7958",
        "Action": "StartExecution",
        "Version": "2025-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RunId": "p0:5c3ef8b22ec27d94aeed3479f0755d5a"
    }
}
```


<span id="374fc8e0"></span>
### Step 2: Getting the task result

After you submit the task, the system will process the task asynchronously. You can get the result through the following methods:


* **Active query:**  Call [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution) and pass the `RunId` to retrieve the task result.

   ```HTTP
   GET https://vod.bytedanceapi.com?Action=GetExecution&Version=2025-07-01&RunId=p0:5c3ef8b22ec27d94aeed3479f0755d5a
   ```
   

* **Event notification:** 

   1. Add a callback subscription address and select [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete). For details, please refer to [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

   2. When the task is completed, you will receive an HTTP POST request whose `EventType` is `ExecutionComplete`.

* **Console:**  You can check the execution status through the console. A status of "Success" indicates that the task has been completed.

   1. [Sign in to the VOD console](https://console.byteplus.com/vodpaas) and enter the specific space.

   2. Navigate to **Media processing** \> **Tasks** in the left navigation bar to check the status of the target task.


<span id="25375edc"></span>
### Step 3: Obtaining the URL of the processed video

After video processing, you can generate a public URL for playback and download.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Before retrieving the public URL, you must <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-configuring">add and configure a domain name</a> for the specified VOD space. All URLs generated are based on this domain name.</div>


<span id="d2f63343"></span>
#### Method 1: Calling GetPlayInfo

Call the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API and pass the Vid. Upon a successful call, the system will return the URL in the `Result.PlayInfoList` field of the response body.

<span id="c43040bf"></span>
#### Method 2: Manually constructing the URL using the FileName

A public URL consists of the following components: `[Protocol]://[PlaybackDomain]/[FileName]`


* `[Protocol]`: Generally `https` or `http`, depending on whether you [have configured an SSL certificate](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates).

* `[PlaybackDomain]`: The playback domain name that you have configured in the VOD console.

* `[FileName]`: The FileName of the processed file retrieved from the task result.


Example: If your domain name is `play.example.com` and the `FileName` is `video.mp4`, the basic URL is `https://play.example.com/video.mp4`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To prevent unauthorized hotlinking, VOD supports URL signing. If you have enabled URL signing in the console, the basic URL will not grant access. You must append a dynamically calculated signing parameter (such as <code>auth_key</code>) to the URL.</div>



* <div data-tips="true" data-tips-type="tip"><strong>How to generate signing parameters:</strong> The URL signing follows a strict signing algorithm. For details, please see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview">URL signing overview</a>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Example of a full URL with signing:</strong><code>https://play.example.com/video.mp4?auth_key=1732529334-0-0-a1b2c3d4e5f6...</code></div>
