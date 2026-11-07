---
title: "Scene segmentation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-scene-segmentation"
---

BytePlus VOD scene segmentation uses visual understanding algorithms to intelligently split an input video into independent clips based on scene transitions. The feature returns structured JSON data that contains the start and end time of each segment, and you can choose whether to generate independent video segment files. This automates manual, time\-consuming video splitting workflows and improves efficiency for content production and secondary creation. It is suitable for Vlog breakdown, film and variety show material preparation, and batch production of source clips for montage videos.

This guide describes how to implement video scene segmentation by calling the BytePlus VOD OpenAPI.

<span id="use-cases"></span>
## Use cases


* **Automated material splitting**: Quickly split Vlogs or travel videos that contain multiple locations and shots into independent shot clips for detailed editing and selection.

* **Shot\-level content indexing**: Segment movies, TV series, variety shows, and similar content at the shot level to provide basic data for later scene recognition, content analysis, marker annotation, and other workflows.

* **Batch short video material generation**: Quickly split long videos, such as film and TV content or game recordings, into a short video material library for secondary creation, including montage and beat\-synced videos.

* **Intelligent media asset management**: Run scene segmentation when videos are ingested, and manage videos as structured segments for later retrieval and analysis.


<span id="capabilities-and-limits"></span>
## Capabilities and limits


|Item |Description |
|---|---|
|Input file formats |Supports mainstream video formats, including MP4, FLV, ASF, RM, RMVB, MPEG, MOV, AVI, MPEGTS, M4S, WMV, 3GP, TS, MPG, WEBM, MKV, WM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, and QT. |
|Input duration |A single input file cannot exceed 2 hours. |
|Output artifacts |* Structured segment data in JSON format<br><br>* Independent video segment files in MP4 format |


<span id="pricing"></span>
## Pricing

Using scene segmentation incurs the following fees:


* **Scene segmentation fees**: Charged based on the duration of the input source file. For details, see [Scene segmentation pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#scene-segmentation-pricing).

* **Media asset storage fees**: The original video file that you upload for processing and the generated segment files are stored in your BytePlus VOD space. Storage fees are charged based on storage volume and duration. For details, see [Storage pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#storage-pricing).

* **Video distribution fees**: If you use BytePlus VOD CDN distribution acceleration to play or download generated videos, distribution acceleration fees are incurred. For details, see [Distribution acceleration pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#distribution-acceleration).


<span id="prerequisites"></span>
## Prerequisites


* Create a [BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console.

* Enable the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started) and create a space.

* [Upload audio or video files](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to the VOD space and obtain the Vid or FileName.


<span id="procedure"></span>
## Procedure

<span id="step-1-submit-a-scene-segmentation-task"></span>
### Step 1: Submit a scene segmentation task

Call the `StartExecution` API to submit an asynchronous scene segmentation task. The following are the key task parameters:


* `Input`: Specifies the input file.

   * `Type`: Set to `Vid` or `DirectUrl`.

   * `Vid` / `DirectUrl`: Provides the Vid or DirectUrl information of the file to process.

* `Operation.Task`: Defines the task to execute.

   * `Type`: Must be set to `Segment`.

   * `Segment`: Optional. Configures the segmentation policy for more granular control over segmentation behavior.


```JSON
POST https://vod.byteplusapi.com?Action=StartExecution&Version=2025-07-01
{
  "Input": {
    "Type": "Vid",
    "Vid": "v0d25cg10001***jcvqljht8dj05mde0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Segment",
      "Segment": {}
    }
  }
}
```


<span id="step-2-get-the-task-result"></span>
### Step 2: Get the task result

After the task is submitted, the system processes it asynchronously in the background. You can get the result in either of the following ways:


* **Active query**: Call the [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution) API and pass in the `RunId` obtained in step 1.

   ```HTTP
   GET https://vod.byteplusapi.com?Action=GetExecution&Version=2025-07-01&RunId=hb:ebd05bee1f3873***f7316c742b5f
   ```
   

* **Event notification**:

   1. Refer to [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-) to configure a service address for receiving callbacks. When subscribing to events, select [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete).

   2. When the task is complete, your service receives an HTTP POST request whose `EventType` is `ExecutionComplete`.


When the returned `Status` value is `Success`, the task has completed successfully. You can find all segment information in the `Output.Task.Segment.Segments` array. The following table describes each object in the `Segments` array. For the complete response parameter structure, see [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution).


|Field |Type |Description |
|---|---|---|
|`Start` |Double |The start time of the segment in the source video, in seconds. |
|`End` |Double |The end time of the segment in the source video, in seconds. |
|`Frames` |Array of Integer |An array that contains the start frame and end frame of the segment. |
|`File` |Object |**Segment file information**. If `NoFile` is set to `true` in the request, this field is empty. |
|`File.FileName` |String |The storage path of the segment file. |
|`File.Size` |String |The size of the segment file, in bytes. |


Successful response example:

```JSON
{
  "ResponseMetadata": {
    // ... Common metadata omitted
  },
  "Result": {
    "RunId": "hb:a1b2c3d4e5f6***g7h8i9j0k1l2m3n4",
    "Status": "Success",
    // ... Task metadata, input, and operation information omitted
    "Output": {
      "Type": "Task",
      "Task": {
        "Type": "Segment",
        "Segment": {
          "Segments": [
            {
              "Start": 0.0,
              "End": 15.5,
              "Frames": [0, 465],
              "File": {
                "FileName": "40902fd61***65bbe7555c2dfa44c66.mp4",
                "Size": "2345678"
              }
            },
            {
              "Start": 15.5,
              "End": 42.8,
              "Frames": [465, 1284],
              "File": {
                "FileName": "68392bf19439***db268ea9b9ff97a05.mp4",
                "Size": "5123456"
              }
            }
            // ... More segments
          ]
        }
      }
    }
  }
}
```


<span id="step-3-get-segment-file-urls"></span>
### Step 3: Get segment file URLs

If you choose to generate segment files in step 1 by setting `NoFile` to `false`, you can obtain the `FileName` of each segment file. Next, convert each value to a public URL for playback or download.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Before obtaining a public URL for a file, you <strong>must</strong> add and configure an acceleration domain name for the VOD space where the artifact is stored. All URLs are generated based on this domain name.</div>


A basic access URL consists of the following parts: `[Protocol]://[PlaybackDomain]/[FileName]`


* `[Protocol]`: Usually `https` or `http`, depending on whether you have configured an SSL certificate.

* `[PlaybackDomain]`: The acceleration domain name that you configured in the VOD console.

* `[FileName]`: The artifact `FileName` obtained from the task result.


Concatenation example: Assume that your acceleration domain name is `play.example.com` and the obtained `FileName` is `video.mp4`. The concatenated URL is `https://play.example.com/video.mp4`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To prevent hotlinking, BytePlus VOD supports URL signing. If URL signing is enabled in the VOD console, the basic URL cannot be accessed directly. You must append a dynamically calculated authentication parameter, such as <code>auth_key</code>.</div>



* <div data-tips="true" data-tips-type="tip"><strong>Generate authentication parameters</strong>: URL signing must follow a strict signature algorithm. For calculation methods and examples in different languages, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication">URL signing</a>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Complete URL example with authentication</strong>: <code>https://play.example.com/video.mp4?auth_key=1732529334-0-0-a1b2c3d4e5f6...</code></div>



<span id="getting-task-results-and-follow-up-processing"></span>
### Getting task results and follow\-up processing

Scene segmentation is an asynchronous task. After submitting the task, record the `RunId` returned by the API and get the result in the following ways:


1. Call [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) to query the task execution result, or receive a completion notification through [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete).

2. When the returned `Status` is `Success`, the task has executed successfully. You can view the start and end time, frame information, and file information of each segment in `Output.Task.Segment.Segments`.

3. If you choose to generate segment files when submitting the task by setting `NoFile` to `false`, you can obtain `File.FileName` from each segment object and generate playable or downloadable URLs by referring to [Step 3: Get segment file URLs](https://docs.byteplus.com/en/docs/25/112790#step-3-get-segment-file-urls).

4. If you only need segment time information, read fields such as `Start`, `End`, and `Frames` from `Segments` directly. You do not need to download segment files.


If the task fails, first check whether the input file meets the capability limits, whether the request parameters meet API requirements, whether the account has sufficient balance, and whether an acceleration domain name has been configured for the space where artifacts are stored.

<span id="related-api-documentation"></span>
## Related API documentation


* [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-scene-segmentation)

* [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution)

* [ExecutionComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-executioncomplete)
