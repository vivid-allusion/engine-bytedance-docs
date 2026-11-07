---
title: "UpdateRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023"
---

Call the `UpdateRecordPresetV2` API to update the created recording configuration.

<span id="requirements"></span>
## Requirements


* Rate limit: 10 queries per second per account.

* Effective description: For adding, updating, and deleting recording configurations, you need to re\-push and pull the stream after the adding, updating, and deleting operations (3\-5 minutes) to use the changed configuration.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateRecordPresetV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRecordPresetV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to obtain the domain name space of configuration to be updated. |
|App |String |No |`live` |The AppName field. You can call the [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to obtain the AppName field of configuration to be updated. |
|Stream |String |No |`example_stream` |The StreamName field. You can call the [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to obtain the StreamName field of configuration to be updated. |
|Preset |String |Yes |`liverecord` |The name of configuration. You can call the [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to obtain the name of configuration to be updated. |
|RecordPresetConfig |Object of [RecordPresetConfig](https://docs.byteplus.com/en/docs/24/27426#recordpresetconfig) |No |`-` |Detailed configuration for recording.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The following parameters, when no value is passed in, indicates the same as the configuration before the update.</div><br> |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TranscodeRecord |Integer |No |`1` |Whether to record transcoded streams. Valid values:<br><br><br>* `0`(Default): Do not record;<br><br>* `1`: Record all transcoding streams;<br><br>* `2`: Record the specified transcoding stream which is specified by TranscodeSuffixList. If the transcoding stream suffix list is empty, it still record all transcoding streams.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select either <code>TranscodeRecord</code> or <code>OriginRecord</code> to record.</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> and <code>OriginRecord</code> cannot both be <code>0</code>.</div><br> |
|OriginRecord |Integer |No |`1` |Whether to record original streams. Valid values:<br><br><br>* `0` (Default): Do not record;<br><br>* `1`: Record original streams.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select either <code>TranscodeRecord</code> or <code>OriginRecord</code> to record.</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> and <code>OriginRecord</code> cannot both be <code>0</code>.</div><br> |
|SliceDuration |Integer |No |`5` |The duration of an individual TS file, in seconds. The default value is `10`. Valid range: 5–30. This parameter takes effect when you store recording files in the HLS format. |
|FlvParam |Object of [RecordParam](https://docs.byteplus.com/en/docs/24/27426#recordparam) |No |`-` |Recording configurations when you store recording files in the FLV format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify at least one of the recording formats by setting one of the parameter values, <code>FlvParam</code>, <code>HlsParam</code>, and <code>Mp4Param</code>.</div><br> |
|HlsParam |Object of [RecordParam](https://docs.byteplus.com/en/docs/24/27426#recordparam) |No |`-` |Recording configurations when you store recording files in the HLS format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify at least one of the recording formats by setting one of the parameter values, <code>FlvParam</code>, <code>HlsParam</code>, and <code>Mp4Param</code>.</div><br> |
|Mp4Param |Object of [RecordParam](https://docs.byteplus.com/en/docs/24/27426#recordparam) |No |`-` |Recording configurations when you store recording files in the MP4 format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify at least one of the recording formats by setting one of the parameter values, <code>FlvParam</code>, <code>HlsParam</code>, and <code>Mp4Param</code>.</div><br> |
|TranscodeSuffixList |Array of String |No |`["_hd"]` |Transcoding stream suffix list. The transcoded stream recording configuration takes effect when the specified transcoding stream matches(`TranscodeRecord` value is `2`), the default configuration of `TranscodeSuffixList` is empty, when it is empty, it is to record all the transcoded streams. |


<span id="recordparam"></span>
### RecordParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`true` |Whether to enable recording in the current format. Valid values:<br><br><br>* `false` (Default): Disable<br><br>* `true`: Enable |
|Duration |Integer |No |`7200` |In the scenario where recording files are stored after recording is completed, the duration of recording a single file with the unit of seconds is 7200 by default, and the value range is \-1 and 300\-86400.<br><br><br>* `-1`: No limit on recording time. After recording is completed, a complete recording file is generated and stored.<br><br>* When the value is between [300,86400], it means that the recording file is generated immediately when the recording file duration is reached, and uploaded together after the recording is completed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is only effective when the recording file is in HLS format and needs to be configured as one of two options with the scenario of segmented recording and real\-time storage.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is a disconnection during recording, the duration of the corresponding generated recording file will also be shortened accordingly.</div><br> |
|Splice |Integer |No |`0` |In the scenario where recording files are stored after recording is completed, the duration of merged splice time with unit of seconds is 0 by default. Their values and meanings are as follows.<br><br><br>* `-1`: Merge stream segments. Regardless of any pauses, everything is joined into one file until the recording reaches the maximum duration.<br><br>* `0` (Default): Do not merge streams. Generate a new file. A new recording is made each time the live stream is resumed after a pause.<br><br>* Any value greater than 0: Set the maximum wait time before generating a new file, in seconds. If you pause and restart before this defined time is reached, your recording continues on the same file. Resuming after the defined wait time will split the file.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is only effective when the recording file is in HLS format and needs to be configured as one of two options with the scenario of segmented recording and real\-time storage.</div><br> |
|RealtimeRecordDuration |Integer |No |`7200` |In the scenario of segmented recording and real\-time storage, set the duration of segmented recording files, in seconds. The default value is 1800, and the value range is `300-21600`. When the recording time reaches the set single\-file recording time, the recording file will be generated immediately and uploaded and stored in real time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If there is a disconnection during recording, the duration of the corresponding generated recording file will also be shortened accordingly.</div><br> |
|ContinueDuration |Integer |No |`180` |In the scenario of segmented recording real\-time storage, set the connection interruption recovery waiting time in seconds, the default value is 180, and the value range is [0,3600].<br><br>If the connection interruption duration is less than this value, the recording task will not stop; if the actual connection interruption duration is longer than this value, the recording task will stop, and a new recording task will be started after the connection interruption is resumed. |
|TOSParam |Object of [TOSParam](https://docs.byteplus.com/en/docs/24/27426#tosparam) |No |`-` |TOS storage configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only specify one location to store the recording file, either <code>TOSParam</code> or <code>VODParam</code>, not both.</div><br> |
|VODParam |Object of [VODParam](https://docs.byteplus.com/en/docs/24/27426#vodparam) |No |`-` |VOD storage configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only specify one location to store the recording file, either <code>TOSParam</code> or <code>VODParam</code>, not both.</div><br> |


<span id="tosparam"></span>
### TOSParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`true` |Defines whether to store recording files in the TOS storage. Valid values:<br><br><br>* `false`: Do not store recording files in the TOS.<br><br>* `true`: Store recording files in the TOS. |
|Bucket |String |No |`live-test-tos-example` |The bucket of BytePlus TOSstorage. For example, when the storage location is live\-test\-tos\-example/live/liveapp, the `Bucket` value is `live-test-tos-example`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If TOS storage is used, that is to set <code>Enable</code> in <code>TOSParam</code> to <code>true</code>, then you must specify <code>Bucket</code>.</div><br> |
|StorageDir |String |No |`live/liveapp` |The directory of the Bucket of TOS storage. , which is empty by default. For example, when the storage location is live\-test\-tos\-example/live/liveapp, the value of `StorageDir` is `live/liveapp`. |
|ExactObject |String |No |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |Storage path. The default value is<br><br>&nbsp;<br><br>`"record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"`.<br><br>You can delete fixed segments in the path, such as `{App}/{Stream}`.<br><br>The parameter format requirements are as follows:<br><br><br>* The path must not start with a forward slash `/` or backslash `\`;<br><br>* The path must not contain `//` or `/./`;<br><br>* The path must not contain escape sequences such as `\b`, `\t`, `\n`, `\v`, `\f`, `\r`;<br><br>* The last segment is taken as the file name and must follow the file naming conventions. For example, it cannot be `..`.<br><br>   If you keep the default value for `ExactObject`, the resulting storage directory will be similar to this: `record/your_domain_name.com/app1/stream1/1683357987_1683358299.mp4`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you set ExactObject to a custom value that does not guarantee the uniqueness of the storage path, there is a risk that old recording files may be overwritten by new ones if they happen to have the same storage path.</div><br> |


<span id="vodparam"></span>
### VODParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`true` |Whether to store recording files using BytePlus VOD. Valid values:<br><br><br>* `false`: Do not store recording files using BytePlus VOD.<br><br>* `true`: Store recording files using BytePlus VOD. |
|VodRegion |String |No |`ap-singapore-1` |The VOD region. Valid values:<br><br><br>* `ap-singapore-1`: Asia Pacific (Singapore).<br><br>* `ap-southeast-1`: Asia Pacific (Johor).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>Enable</code> in <code>VODParam</code> is set to <code>true</code>, this parameter is required.</div><br> |
|VodNamespace |String |No |`Snapshot` |The name of the BytePlus VOD space, which must belong to the specified `VodRegion`. You can log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) to query the space name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>Enable</code> in <code>VODParam</code> is set to <code>true</code>, this parameter is required.</div><br> |
|WorkflowID |String |No |`25524a2d*********891d7daf4b9` |The workflow ID. If you specify a workflow ID, the corresponding workflow will be applied to recording files stored in VOD. You can log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) to get the workflow ID. The default value is empty. |
|ClassificationID |Integer |No |`12**34` |Video classification ID when live recording files are stored to on\-demand. You can query information such as video classification ID through the [ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications) interface of video on\-demand. Default is empty. |
|StorageClass |Integer |No |`1` |The storage type when live streaming recording files are stored to VOD. The default value is `1`. The supported values and their meanings are as follows.<br><br><br>* `1`: Standard storage;<br><br>* `2`: Archive storage. |
|ExactObject |String |No |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |Set storage rules of recording files when storing in VOD. The default value is `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`. You can delete fixed segments in the path, such as `{App}/{Stream}`.<br><br><br>* The path must not start with a forward slash `/` or backslash `\`;<br><br>* The path must not contain `//` or `/./`;<br><br>* The path must not contain escape sequences such as `\b`, `\t`, `\n`, `\v`, `\f`, `\r`;<br><br>* The last segment is taken as the file name and must follow the file naming conventions. For example, it cannot be `..`.<br><br>   If you keep the default value, the resulting storage directory will be similar to this: `record/your_domain_name/app1/stream1/1683357987_1683358299.mp4`. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Preset": "liverecord",
    "RecordPresetConfig": {
        "OriginRecord": 1,
        "HlsParam": {
            "Enable": "true",
            "RealtimeRecordDuration": 7200,
            "Splice": 0,
            "TOSParam": {
                "Enable": true,
                "Bucket": "live-test-tos-example",
                "StorageDir": "",
                "RecordObject": "record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"
            }
        }
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220726*******************051B513A",
        "Action": "UpdateRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27426#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.PresetNotExist |preset not found |The configuration was not found. Please check if the passed\-in configuration is consistent with the created configuration. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
