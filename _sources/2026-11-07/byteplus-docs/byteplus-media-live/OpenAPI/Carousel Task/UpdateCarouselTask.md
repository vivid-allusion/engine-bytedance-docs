---
title: "UpdateCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask"
---

Call the `UpdateCarouselTask` API to modify the specified carousel task configuration, adjust the playback content, playback rules, or time range, and the system will execute the carousel task according to the new configuration after the update.

<span id="requirements"></span>
## Requirements


* Rate limit: 10 queries per second per account.

* Keep the original configuration: When the non\-mandatory parameters are not passed, the original configuration of the current carousel task will be maintained and will not be restored to the default value.

* Only support updating running tasks: Only support updating tasks in the `running` state. You can call the `GetCarouselDetail` and `ListCarouselTask` API to query the task status.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateCarouselTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateCarouselTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`44c5da50318440*********2d62c910b8` |The ID of the carousel task to be updated, which is the unique identifier of the task. It is returned when the `CreateCarouselTask` interface is called to create a carousel task. |
|Rule |Object of [Rule](https://docs.byteplus.com/en/docs/24/47072#rule) |Yes |`-` |Carousel rules are used to specify the materials and behaviors of carousel playback, etc. |


<span id="rule"></span>
### Rule


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Loop |Integer |No |`1` |Specify the number of times this material is continuously played. The value of this field must be greater than or equal to `0`. If not passed, the original carousel configuration will be maintained. The supported values and meanings are as follows:<br><br><br>* `0`: Do not loop playback;<br><br>* Other positive integers: Loop playback according to the specified number of times. |
|Source |Array of [Source](https://docs.byteplus.com/en/docs/24/47072#source) |Yes |`-` |Carousel material list, used to specify the material resources to be played in the carousel process. |
|SeekInfo |Object of [SeekInfo](https://docs.byteplus.com/en/docs/24/47072#seekinfo) |No |`-` |Configuration parameters for controlling the playback behavior after the material is updated. |


<span id="source"></span>
### Source


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ID |String |Yes |`1` |The unique identifier of the carousel material. In the same playlist, the `ID` of each material must be unique and duplication is not allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>ID</code> of the material does not change (that is, the updated <code>ID</code> is the same as the original material's <code>ID</code>), only other parameters except <code>Type</code> and <code>Url</code> can be updated.</div><br> |
|Type |String |Yes |`vod` |The file type of the carousel material is used to specify the file source type of the material. The following values are supported:<br><br><br>* `vod`: on\-demand MP4 or FLV file;<br><br>* `m3u8`: on\-demand M3U8 file.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>ID</code> of the material does not change (that is, the updated <code>ID</code> is the same as the <code>ID</code> of the original material), the value of <code>Type</code> should be consistent with the original material.</div><br> |
|Url |String |Yes |`https://live.example.com/video.mp4` |The publicly accessible address of the carousel material. Ensure that the provided address can be normally accessed by the public network so as to correctly load the content of the carousel material.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>ID</code> of the material has not changed (that is, the updated <code>ID</code> is the same as the <code>ID</code> of the original material), the value of <code>Url</code> should be consistent with that of the original material.</div><br> |
|Seek |Integer |No |`10` |Used to control skipping a period of time at the beginning when playing the current material. For example, skipping the opening credits, with the unit being seconds. This field is only valid when the material type is video on demand (`type=vod`). The following are the usage rules for this field:<br><br><br>* If the value of `Seek` is less than or equal to `0` or greater than the actual duration of the video, this field will not take effect.<br><br>* Ensure that an appropriate value is set according to the actual length of the on\-demand material to achieve the effect of skipping the opening credits. |
|Loop |Integer |No |`1` |Specify the number of consecutive playbacks of this material. The value of this field must be greater than or equal to `0`. If not passed, the original carousel configuration will be maintained. The supported values and meanings are as follows:<br><br><br>* `0`: Do not loop playback;<br><br>* Other positive integers: Loop playback according to the specified number of times. |


<span id="seekinfo"></span>
### SeekInfo


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Immediate |Long |No |`1` |Used to set the way of material switching, and the default value is `0`. The supported values and their meanings are as follows:<br><br><br>* `0`: After playing the current material, switch to the next material;<br><br>* `1`: Immediately switch to the specified material and start playing from the specified playback progress. |
|SourceID |String |No |`1f9f207a55a43f45` |The updated material ID for playback is only valid when `Immediate=1`.<br><br><br>* If not filled, it will start playing directly from the first material of the new material.<br><br>* If filled, it will start playing from the corresponding `SourceID`. |
|SourceSeek |Long |No |`10` |After switching the material, the position where the material is played, in seconds, indicating that the playback starts from this position, and it is only valid when `Immediate=1`. If not filled in, it means that the playback starts from the starting position of the material corresponding to `SourceID`. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/47072#data) |`-` |A data object containing information related to task updates. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|OptID |Integer |`2` |The serial number of the currently effective task configuration, which is used to identify the latest task modification record. This value will be incremented after each task configuration update. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateCarouselTask&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8",
    "Rule": {
        "Loop": 1,
        "Source": [
            {
                "ID": "1",
                "Type": "vod",
                "Url": "https://live.example.com/video.mp4",
                "Seek": 10,
                "Loop": 1
            }
        ],
        "SeekInfo": {
            "Immediate": 1,
            "SourceID": "1f9f207a55a43f45",
            "SourceSeek": 10
        }
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301532184E885F20A2263C133082",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "OptID": 2
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/47072#request-parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |


&nbsp;
