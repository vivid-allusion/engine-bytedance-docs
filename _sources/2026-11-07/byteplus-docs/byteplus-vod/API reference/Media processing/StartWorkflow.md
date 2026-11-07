---
title: "StartWorkflow"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow"
---

This interface is used to trigger a media processing task by specifying the workflow ID, in order to process the designated media source.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">After submission, an asynchronously executed task will be generated. To obtain the media processing results, you can configure notifications for the <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete">WorkflowComplete</a> event. For configuration methods, please see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-system#aed0518b">Configuring callback settings</a>.</div>


* <div data-tips="true" data-tips-type="tip">For more information, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/startworkflow-request-examples">StartWorkflow API request examples</a>.</div>


* <div data-tips="true" data-tips-type="tip">Video enhancement tasks configured with a target resolution of 6K or 8K, a color depth of 12\-bit or 16\-bit, or a frame rate of 60 fps or higher have a very high risk of timing out when run in a workflow. To ensure reliable processing, use the <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template">StartExecution</a> API to run a single video enhancement template instead.</div>



<span id="requirements"></span>
## Requirements

The parameter settings of this interface have a higher priority than the parameter settings in the media processing templates and workflows in the BytePlus VOD console.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=StartWorkflow&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartWorkflow` |The API action. For the current API, the value is `StartWorkflow`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |No |`v023bbg10001***2n6qiboeb9dn73mg` |The video ID. After audio and video are uploaded to the VOD service, you can obtain the `Vid` through the [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete) event.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You must set either the <code>Vid</code> or the <code>DirectUrl</code> parameter, but not both at the same time.</div><br> |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/8040#directurl) |No |`-` |The file storage information in DirectUrl mode.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You must set either the <code>Vid</code> or <code>DirectUrl</code> parameter, but not both at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If it is a POST request, the parameter type is String. For example, <code>"{\"FileName\":\"example.mp4\"}"</code>.</div><br> |
|TemplateId |String |Yes |`63d92a1***b1795` |The workflow ID. You can obtain the `TemplateId` on the [Workflows ](https://console.byteplus.com/vodpaas/overview/?)page in the BytePlus VOD console. |
|Input |Object of [WorkflowParams](https://docs.byteplus.com/en/docs/25/8040#workflowparams) |No |`-` |Dynamic parameters. By default, BytePlus VOD executes media processing tasks based on the preset parameters in the workflow and its associated media processing templates. If you need to dynamically set processing parameters when triggering the workflow, such as setting the output file path or text watermark content, you can pass in dynamic parameters. Dynamic parameters will overwrite the corresponding parameters in the specified template.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is String. For example, <code>"{\"OverrideParams\":{\"Logo\":[{\"Vars\":{\"input_text\":\"Text watermark test\"}}]}}"</code>.</div><br> |
|Priority |Integer |No |`0` |The task priority. The default value is 0. The range of values is [\-5, 5]. The smaller the number, the higher the priority. |
|CallbackArgs |String |No |`YourCallbackArgs` |The customized field that will be transparently returned by the [WorkflowComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete) event. The maximum length is 512 bytes. |
|ClientToken |String |No |`QqS3o5L4BLFCDxGZ&b` |A unique client token provided by the user to distinguish between different requests. It is case\-sensitive and must not exceed 64 printable ASCII characters. By default, the VOD transcoding service implements idempotency for workflow trigger requests. This means that if a request is determined to be identical to a previously sent request, the service will not execute it again. For information on the workflow idempotent behavior, purpose, and conditions, please refer to [Idempotent behavior](https://docs.byteplus.com/en/docs/byteplus-vod/docs-idempotent-behavior). You can set this parameter to bypass idempotent behavior. For example, if you have modified the configuration of a media processing template bound to a workflow and want to re\-execute the same workflow for the same Vid, providing a new unique token will ensure the request is processed again. |


#{.custom\-md\-table\-5}#

<span id="directurl"></span>
### DirectUrl


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|SpaceName |String |No |`test` |The space name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to retrieve information about all the spaces under the current account.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the workflow you triggered is a preset workflow, then <code>SpaceName</code> is required.</div><br> |
|FileName |String |Yes |`example.mp4` |The file path. After audio and video are uploaded to the VOD service, you can obtain the `FileName` through the [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete) event. |
|BucketName |String |No |`tos-cn-v-cd3a11` |The bucket name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to get the bucket name bound to the space. |


#{.custom\-md\-table\-5}#

<span id="workflowparams"></span>
### WorkflowParams


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Condition |JSON Map |No |`{"xxxx":true}` |The execution conditions of the task and whether each node has been completed. The format is `"key":"value"`.<br><br><br>* `"key"`: String type, representing the task execution conditions.<br><br>* `"value"`: Boolean type, indicating whether each node has been completed. |
|OverrideParams |Object of [OverrideParams](https://docs.byteplus.com/en/docs/25/8040#overrideparams) |No |`-` |The override parameters, used to override the configurations in the media processing template. |


#{.custom\-md\-table\-5}#

<span id="overrideparams"></span>
### OverrideParams


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Logo |Array of [LogoOverride](https://docs.byteplus.com/en/docs/25/8040#logooverride) |No |`[{"TemplateId":"1091058d0**6b8f408c352ee1c52","Vars":{"keyword":"hello"}}]` |The watermark override parameters. |
|Snapshot |Array of [SnapshotOverride](https://docs.byteplus.com/en/docs/25/8040#snapshotoverride) |No |`[{"Type":["AnimatedPoster"],"OffsetTime":0,"OffsetTimeList":null,"SampleOffsets":null}]` |The screenshot override parameters. |
|TranscodeAudio |Array of [TranscodeAudioOverride](https://docs.byteplus.com/en/docs/25/8040#transcodeaudiooverride) |No |`[{"TemplateId":["1091058d0**6b8f408c352ee1c52"],"Clip":{"StartTime":0,"EndTime":20000}}]` |The audio transcoding override parameters. |
|TranscodeVideo |Array of [TranscodeVideoOverride](https://docs.byteplus.com/en/docs/25/8040#transcodevideooverride) |No |`[{"TemplateId":["1091058d0**6b8f408c352ee1c52"],"Clip":{"StartTime":0,"EndTime":20000}}]` |The video transcoding override parameters. |


#{.custom\-md\-table\-5}#

<span id="logooverride"></span>
### LogoOverride


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vars |JSON Map |No |`{"keyword":"hello"}` |The watermark override content. The format is `"key":"value"`.<br><br><br>* `"key"`: String type. This value is the custom variable key configured in your watermark template.<br><br>* `"value"`: String type. This value is the custom text watermark content. |
|TemplateId |String |Yes |`1091058d0**6b8f408c352ee1c52` |The watermark template ID. Supported values include `All`, indicating that it is effective for all watermark templates. |


#{.custom\-md\-table\-5}#

<span id="snapshotoverride"></span>
### SnapshotOverride


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|FileName |String |No |`{{fileTitle}}` |Set the screenshot file path dynamically. The file path can consist of fixed strings and variables, as detailed in [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path). Suppose you trigger the workflow `a378f66a5bc2495eb55fc14ac109625f` for the input video named `vodtest`, and set the `FileName` as `{{fileTitle}}_{{templateId}}`, then the file path generated for this screenshot will be `vodtest_a378f66a5bc2495eb55fc14ac109625f`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the packaging format is DASH, this parameter does not take effect.</div><br> |
|FileIndex |String |No |`{{fileTitle}}` |Set the file path for the sampling screenshot index dynamically. This is effective only when the screenshot type is **sampling screenshot**. The file path can consist of fixed strings and variables, as detailed in [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path). Suppose you trigger the workflow `a378f66a5bc2495eb55fc14ac109625f` for the video source named `vodtest`, and set the `FileIndex` to `{{fileTitle}}_{{templateId}}`, the file path generated for this screenshot will be `vodtest_a378f66a5bc2495eb55fc14ac109625f`. |
|OffsetTime |Integer |No |`100` |The screenshot interval. This parameter is only effective when the screenshot type is as follows:<br><br><br>* `Poster`: a static image.<br><br>* `Dynpost`: a dynamic image.<br><br>* `AnimatedPoster`: a continuously looping dynamic image. |
|TemplateId |Array of String |Yes |`1091058d0**6b8f408c352ee1c52` |The screenshot template ID list. Supported values include `All`, indicating that it is effective for all screenshot templates. |
|SampleOffsets |Array of Float |No |`[1.0,2.0]` |The sampling screenshot time point, measured in seconds. It is effective for the `Sample` type screenshot template. |
|OffsetTimeList |Array of Integer |No |`[10,20]` |The dynamic image screenshot time, measured in milliseconds. It is effective for the `Dynpost` type screenshot template. |


#{.custom\-md\-table\-5}#

<span id="transcodeaudiooverride"></span>
### TranscodeAudioOverride


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Clip |Object of [Clip](https://docs.byteplus.com/en/docs/25/8040#clip) |No |`{"StartTime":0,"EndTime":20000}` |The clipping parameters. |
|FileName |String |No |`{{fileTitle}}` |Set the file path of the transcoded output audio dynamically. The file path can consist of fixed strings and variables, as detailed in [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path). Suppose you trigger the workflow `a378f66a5bc2495eb55fc14ac109625f` for the input file named `vodtest`, and set the `FileName` as `{{fileTitle}}_{{templateId}}`, then the file path generated for this screenshot will be `vodtest_a378f66a5bc2495eb55fc14ac109625f`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the packaging format is DASH, this parameter does not take effect.</div><br> |
|TemplateId |Array of String |Yes |`1091058d0**6b8f408c352ee1c52` |The audio transcoding template ID list. Supported values include `All`, indicating that it is effective for all audio transcoding templates. |


#{.custom\-md\-table\-5}#

<span id="clip"></span>
### Clip


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StartTime |Integer |No |`0` |The clipping start time, measured in milliseconds. |
|EndTime |Integer |No |`2000` |The clipping end time, measured in milliseconds. |


#{.custom\-md\-table\-5}#

<span id="transcodevideooverride"></span>
### TranscodeVideoOverride


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Clip |Object of [Clip](https://docs.byteplus.com/en/docs/25/8040#clip) |No |`{"StartTime":0,"EndTime":20000}` |The clipping parameters. |
|FileName |String |No |`{{fileName}}` |Set the file path of the transcoded output video dynamically. The file path can consist of fixed strings and variables, as detailed in [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path). Suppose you trigger the workflow `a378f66a5bc2495eb55fc14ac109625f` for the input file named `vodtest`, and set the `FileName` as `{{fileTitle}}_{{templateId}}`, then the file path generated for this screenshot will be `vodtest_a378f66a5bc2495eb55fc14ac109625f`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the packaging format is DASH, this parameter does not take effect.</div><br> |
|TemplateId |Array of String |Yes |`["1091058****6b8f408c352ee1c52"]` |The video transcoding template ID list. Supported values include `All`, indicating that it is effective for all video transcoding templates. |
|LogoTemplateId |String |No |`1091058****6b8f408c352ee1c52` |The watermark template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is only effective when the <code>TemplateId</code> corresponds to a template that is for video transcoding.</div><br> |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RunId |String |`lb:0f557116******059cedf92f1bd` |The workflow execution ID. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=StartWorkflow&Version=2023-01-01&Vid=v023bbg10001***2n6qiboeb9dn73mg&TemplateId=63d92a1***b1795&Input=&Priority=0&CallbackArgs=YourCallbackArgs&EnableLowPriority=false&DirectUrl=
```


<span id="sample-response"></span>
### Sample response

```json
{
  "Result":{
    "RunId":"lb:0f557116******059cedf92f1bd"
  },
  "ResponseMetadata":{
    "Action":"StartWorkflow",
    "Region":"ap-southeast-1",
    "Service":"vod",
    "Version":"2023-01-01",
    "RequestId":"20230604110420****100232280022D31"
  }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |\- |The illegal parameter. |
|403 |RequestForbidden |\- |The request is forbidden. |
|404 |ResourceNotFound |\- |The ID cannot be found. |
|409 |ResourceInUse |\- |The ID is in use (during deletion). |
|429 |RequestLimitExceeded |\- |The request exceeds the limit. |
|500 |InternalError |\- |The internal error. |
|503 |ServiceUnavailable |\- |The service is unavailable. |


#{.custom\-md\-table\-4}#

&nbsp;
