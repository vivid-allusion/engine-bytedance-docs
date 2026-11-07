---
title: "ListVhostRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023"
---

Call the `ListVhostRecordPresetV2` API to query all recording configurations under a Vhost, including all configurations at the three levels of Vhost, Vhost + App, Vhost + App + Stream.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListVhostRecordPresetV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListVhostRecordPresetV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space. |
|Type |String |No |`tos` |The type of storage you want to query. Valid values include:<br><br><br>* `tos` (Default): BytePlus TOS.<br><br>* `vod`: BytePlus VOD. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetList |Array of [PresetList](https://docs.byteplus.com/en/docs/24/27427#presetlist) |`-` |A list of recording configurations. |


<span id="presetlist"></span>
### PresetList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The AppName field. |
|Stream |String |`example_stream` |The StreamName field. |
|SlicePresetV2 |Object of [SlicePresetV2](https://docs.byteplus.com/en/docs/24/27427#slicepresetv2) |`-` |The configuration information. |


<span id="slicepresetv2"></span>
### SlicePresetV2


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ID |Long |`8` |The configuration ID. |
|Name |String |`RecordPresetexample` |The configuration name. |
|RecordPresetConfig |Object of [RecordPresetConfig](https://docs.byteplus.com/en/docs/24/27427#recordpresetconfig) |`-` |Recording parameters. |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TranscodeRecord |Integer |`1` |Whether to record transcoded streams. Valid values include:<br><br><br>* `0` (Default): Do not record;<br><br>* `1`: Record all transcoding streams;<br><br>* `2`: Record the specified transcoding stream which is specified by TranscodeSuffixList. If the transcoding stream suffix list is empty, it still means to record all transcoding streams. |
|TranscodeSuffixList |Array of String |`["_hd"]` |Transcoding stream suffix list. When the transcoded stream recording configuration takes effect according to the specified transcoding stream (`TranscodeRecord` value is `2`), the default configuration of `TranscodeSuffixList` is empty, and the effect is equivalent to recording all transcoded streams. |
|OriginRecord |Integer |`1` |Whether to record original streams. Valid values include:<br><br><br>* `0` (Default): Do not record original streams.<br><br>* `1`: Record original streams. |
|SliceDuration |Integer |`5` |The duration of an individual TS file, in seconds. The default value is `10`. Valid range: 5–30. This parameter takes effect when you store recording files in the HLS format. |
|FlvParam |Object of [RecordParam](https://docs.byteplus.com/en/docs/24/27427#recordparam) |`-` |Recording configurations when you store recording files in the FLV format. |
|HlsParam |Object of [RecordParam](https://docs.byteplus.com/en/docs/24/27427#recordparam) |`-` |Recording configurations when you store recording files in the HLS format. |
|Mp4Param |Object of [RecordParam](https://docs.byteplus.com/en/docs/24/27427#recordparam) |`-` |Recording configurations when you store recording files in the MP4 format. |


<span id="recordparam"></span>
### RecordParam


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Whether to enable recording in the current format. Valid values include:<br><br><br>* `false`: Disable<br><br>* `true`: Enable |
|Duration |Integer |`7200` |In the scenario where recording files are stored after recording is completed, the maximum duration of recording files and their values and meanings are as follows.<br><br><br>* `-1`: Indicates full recording. After recording is completed, a complete recording file is generated and stored.<br><br>* When the value is within the range of [300, 86400], it means that recording files are generated in segments according to the set duration. After recording is completed, the recording files are uploaded and stored together.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is only effective when the recording file is in HLS format and needs to be configured as one of two options with the scenario of segmented recording and real\-time storage.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is a disconnection during recording, the duration of the corresponding generated recording file will also be shortened accordingly.</div><br> |
|RealtimeRecordDuration |Integer |`7200` |In the scenario of segmented recording and real\-time storage, set the duration of segmented recording files, in seconds. The default value is 1800.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If there is a disconnection during recording, the duration of the corresponding generated recording file will also be shortened accordingly.</div><br> |
|Splice |Integer |`0` |In the scenario where recording files are stored after recording is completed, determines how recorded content is merged When the live stream is disconnected. Their values and meanings are as follows.<br><br><br>* `-1`: Merge stream segments. Regardless of any pauses, everything is joined into one file until the recording reaches the maximum duration.<br><br>* `0` (Default): Generate a new file. A new recording is made each time the live stream is resumed after a pause.<br><br>* Any value greater than 0: Set the maximum wait time before generating a new file, in seconds. If you pause and restart before this defined time is reached, your recording continues on the same file. Resuming after the defined wait time will split the file.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is only effective when the recording file is in HLS format and needs to be configured as one of two options with the scenario of segmented recording and real\-time storage.</div><br> |
|TOSParam |Object of [TOSParam](https://docs.byteplus.com/en/docs/24/27427#tosparam) |`-` |TOS storage configuration. |
|VODParam |Object of [VODParam](https://docs.byteplus.com/en/docs/24/27427#vodparam) |`-` |VOD storage configuration. |


<span id="tosparam"></span>
### TOSParam


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Defines whether to store recording files in the TOS storage. Valid values include:<br><br><br>* `false`: Do not store recording files in the TOS.<br><br>* `true`: Store recording files in the TOS. |
|Bucket |String |`live-test-tos-example` |The bucket of TOS storage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>Enable</code> is set to <code>true</code> in <code>TOSParam</code>, you must specify the <code>Bucket</code>.</div><br> |
|StorageDir |String |`live/liveapp` |The directory of the recording files in the bucket, which is empty by default. |
|ExactObject |String |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |Storage rules for recorded files. |


<span id="vodparam"></span>
### VODParam


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Whether to store recording files using BytePlus VOD. Valid values include:<br><br><br>* `false`: Do not store recording files using BytePlus VOD.<br><br>* `true`: Store recording files using BytePlus VOD. |
|VodRegion |String |`ap-singapore-1` |The VOD region. Valid values:<br><br><br>* `ap-singapore-1`: Asia Pacific (Singapore).<br><br>* `ap-southeast-1`: Asia Pacific (Johor). |
|VodNamespace |String |`SnapShot` |The name of the BytePlus VOD space, which belongs to the `VodRegion`. You can log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) to query the space name. |
|WorkflowID |String |`25524a2d*********891d7daf4b9` |The workflow ID. If you specify a workflow ID, the corresponding workflow will be applied to recording files stored in VOD. You can log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) to get the workflow ID. |
|ClassificationID |Integer |`12***45` |Video classification ID when live recording files are stored to on\-demand. You can query information such as video classification ID through the [ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications) interface of video on\-demand. Default is empty. |
|StorageClass |Integer |`1` |The storage type when live streaming recording files are stored to VOD. The default value is `1`. The supported values are as follows.<br><br><br>* `1`: Standard storage;<br><br>* `2`: Archive storage. |
|ExactObject |String |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |Set storage rules of recording files when storing in VOD. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListVhostRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220726*******************051B513A",
        "Action": "ListVhostRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SlicePresetV2": {
                "ID": 8,
                "Name": "RecordPresetexample",
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
        }
    ]
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
