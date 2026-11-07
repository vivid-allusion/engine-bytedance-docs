---
title: "TempToMediaActivityMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/temptomediaactivitymediaapi"
---

Transfers videos from temporary storage to a specific category in the video library for permanent storage. The videos will be deleted from temporary storage after the transfer.

<span id="requirements"></span>
## Requirements


* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with **Media library** \> **Videos** \> **Temporary storage** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=TempToMediaActivityMediaAPI&Version=2020\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`TempToMediaActivityMediaAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Ids |Array of String |Yes |`["40**44","40**54"]` |IDs of the videos to transfer. You can get the video ID based on the response parameter `Id` from [ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can configure at most 100 IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When calling this API with an IAM user, make sure the IAM user can access or edit the videos. For more information on how to configure the user range and classification range of IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div><br> |
|FolderId |Long |No |`4**21` |Category ID. Videos are transferred to the category with this ID. The default value is `0`, which means videos are transferred to the default category. You can get the category ID by calling [GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When calling this API with an IAM user, if you need to pass this parameter, make sure the category with this ID is visible to the IAM user. For more information on how to configure the classification range of IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Success |Boolean |`false` |Whether videos are successfully transferred. Valid values:<br><br><br>* `true`: Successful, which means all videos are transferred successfully.<br><br>* `false`: Failed, which means one or more videos failed to transfer. |
|FailedList |Array of [FailedList](https://docs.byteplus.com/en/docs/11/47202#failedlist) |`-` |The list of videos that failed to transfer. This list is returned only if one or more videos failed to transfer, which means the value of `Success` is `false`. |


<span id="failedlist"></span>
### FailedList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |String |`40**44` |ID of the video. |
|Name |String |`video1` |Name of the video. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=TempToMediaActivityMediaAPI&Version=2020-06-01
{
    "Ids": [
        "40**44",
        "40**54"
    ],
    "FolderId": 4**21
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TempToMediaActivityMediaAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Success": false,
        "FailedList": [
            {
                "Id": "40**44",
                "Name": "video1"
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
