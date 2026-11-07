---
title: "Media Processing Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-overview_7"
---

You can process videos stored in Torch Object Storage (TOS) by specifying video processing parameters when you call the GetObject API . Video processing operations supported by TOS include video frame capture and metadata acquisition.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The use of the video processing service incurs fees for video frame capture, requests, and data traffic. For more information on billing, see <a href="https://docs.byteplus.com/en/tos/docs/data-processing-fee?version=1.0.0">Data processing fee</a>, <a href="https://docs.byteplus.com/en/tos/docs/request-fee?version=1.0.0">Request fee</a>, and <a href="https://docs.byteplus.com/en/tos/docs/traffic-fee?version=1.0.0">Traffic fee</a>.</div>


<span id="4c8385f0"></span>
## Restrictions


|**Category** |**Usage Restrictions** |
|---|---|
|Format |Video processing only supports certain video codecs and container formats. The specific supported formats are as follows:<br><br><br>* Video Encoding Formats: MPEG\-4 Part 2, HEVC, AVI, VP8, VP9, H264, and H265.<br><br>* Video packaging formats: avi, mp4, mkv, mov, webm, flv, ts. |
|Concurrency |The maximum concurrency for media processing operations in each region is 20.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you have a compute\-intensive workload or usage that exceeds these limits, <a href="https://console.volcengine.com/workorder/create?step=2&SubProductID=P00000245">submit a ticket</a> to consult with our technical team or your designated account manager.</div><br> |
|Server\-side Encryption |Supports the processing of videos encrypted with SSE\-TOS, SSE\-C, and SSE\-KMS, with the following restrictions:<br><br><br>* When processing videos encrypted with SSE\-C, it is necessary to carry the `x-tos-server-side-encryption-customer-algorithm`, `x-tos-server-side-encryption-customer-key`, `x-tos-server-side-encryption-customer-key-MD5` headers. For detailed information on SSE\-C headers, please refer to [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br>* Anonymous processing of videos encrypted with SSE\-KMS is not supported. You must subscribe to the KMS service and have access to the master key to process encrypted videos with a valid signature. You can use pre\-signed URLs, API, or SDK to process videos encrypted with SSE\-KMS. For detailed information about the video processing API and SDK, please see the instructions on using the REST API. |


<span id="da1cd70c"></span>
## Video processing methods

You can process videos through a RESTful API or a file URL. You can capture a frame from a video stored in a bucket, obtain video metadata, and quickly access the processed video.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Processed videos are returned immediately and are not stored in your bucket.</div>



* Sample request of a RESTful API:

   ```JSON
   GET /misc/video?x-tos-process=video/snapshot,t_30000 HTTP/1.1
   Host: endpoint
   X-Tos-Date: 20220827T132948Z
   Authorization: authorization
   json
   ```
   

* Sample request of a file URL:

   A video processing URL is in the format of `file URL?x-tos-process=video/feature,parameter name_parameter value`. Separate multiple parameters in a URL with commas ( , ). Sample URL:

   ```JSON
   https://tos-tools.tos-cn-beijing.bytepluses.com.cn/misc%2Fvideo.mp4?x-tos-process=video/snapshot,t_30000
   json
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To process private videos, you need to use an SDK to generate a pre\-signed URL that includes video processing parameters.   </div>
   

<span id="6453947c"></span>
## Video processing features

TOS supports the following video processing features. If you specify multiple parameters in a request, TOS will process the video in the order of the parameters.


|**Feature** |**Parameter** |**Description** |
|---|---|---|
|[Video frame capture](https://docs.byteplus.com/en/tos/docs/video-frame-capture?version=1.0.0) |snapshot |Captures a frame at a specified point in time and resizes it to a specified size. |
|[Viewing video information](https://docs.byteplus.com/en/tos/docs/viewing-video-information?version=1.0.0) |info |Obtains video metadata. |
