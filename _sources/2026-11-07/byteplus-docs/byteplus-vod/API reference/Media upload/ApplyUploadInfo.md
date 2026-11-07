---
title: "ApplyUploadInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-applyuploadinfo"
---

This interface obtains the upload address and credentials for audio/video assets, image assets, and materials.

> **Note**

* > After successfully retrieving the upload address and credentials, you need to call [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) to confirm the upload.

* > We recommend using the [Server SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-server-sdk-overview) for uploads.

* > For a complete upload process instruction, please refer to the [Uploading media assets overview page](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview).

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ApplyUploadInfo&Version=2023\-01\-01

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ApplyUploadInfo` |The API action. For the current API, the value is `ApplyUploadInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Spaces page](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus Console.<br><br>* Call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. |
|SessionKey |String |No |`eyJleHRyYSI6InZpZ******YwODc4Njc1NTFcdTAwMjczdpMCJ9` |The session key returned from the last request. It is recommended to carry the session key when retrying, as the server will refer to this value for routing again. |
|FileType |String |No |`media` |The file type. When uploading assets, you can select based on the type of the asset. The options are as follows:<br><br><br>* `media`: Audio and video. Supports both materials and non\-materials.<br><br>* `image`: Images. Supports image assets and image materials. See [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement).<br><br>* `object`: Other types. Supports both materials and non\-materials.<br><br><br>> **Note**<br><br><br>> When uploading audio and video, the `FileType` is set to `media` by default, and you do not need to specify it.<br> |
|FileName |String |No |`example/123.mp4` |The file path. File path refers to the storage location of a file in VOD storage, similar to the ObjectKey concept in traditional object storage. You can customize the file path according to your business needs. The maximum length is 1024 characters.<br><br>> **Note**<br><br><br><br>* > The file path must include the file extension, such as `.mp4`. There is no mandatory requirement to include a file prefix.<br><br><br>* > For specific character rules, please refer to [Character rules for file naming](https://docs.byteplus.com/docs/byteplus-vod/docs-character-rules-for-file-naming).<br><br><br>* > When setting `FileName`, there is a risk of file overwriting if `FileName` is the same. Ensure that the `FileName` is different for different files.<br><br><br>* > After setting `FileName`, there is no need to set the `FileExtension` parameter.<br><br><br><br>  |
|FileExtension |String |No |`.mp4` |The file extension.<br><br>> **Note**<br><br><br><br>* > After setting `FileExtension`, there is no need to set the `FileName` parameter. VOD service will generate a 32\-bit random string, which will be concatenated with the `FileExtension` provided by you to form the file path.<br><br><br>* > The file extension must start with a `.` and must not exceed 8 characters.<br> |
|UploadHostPrefer |String |No |`dcdn` |The preferred upload domain type. This parameter takes precedence over the default domain configured for the VOD space. Valid values:<br><br><br>* `dcdn`: Prioritizes the IGA custom domain configured for the space. The VOD upload domain is returned as a backup domain.<br><br>* `vod`: Prioritizes the VOD upload domain.<br><br>   If you do not specify this parameter, the API follows the space's upload acceleration settings. If upload acceleration is not configured for the space, this parameter does not take effect. For configuration instructions, see [Cross-region upload acceleration](https://docs.byteplus.com/docs/byteplus-vod/docs-cross-region-upload-acceleration). |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [VodApplyUploadInfoData](https://docs.byteplus.com/en/docs/25/8016#vodapplyuploadinfodata) |`-` |Return data. |

### VodApplyUploadInfoData

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|UploadAddress |Object of [VodUploadAddress](https://docs.byteplus.com/en/docs/25/8016#voduploadaddress) |`-` |The upload information. |

### VodUploadAddress

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SessionKey |String |`eyJleHRyYSI6InZpZGM9Ym9******YwODc4Njc1NTFcdTAwMjczdpMCJ9` |A session key for one\-time upload, used when reporting at completion of upload, similar to the cookie mechanism in HTTP protocol. |
|StoreInfos |Array of [VodStoreInfo](https://docs.byteplus.com/en/docs/25/8016#vodstoreinfo) |`-` |The store information. |
|UploadHosts |Array of String |`-` |An ordered list of upload domain names. Use the domains in the returned order and implement fallback to the next domain if the current domain is unavailable. |
|UploadHeader |Array of [VodHeaderPair](https://docs.byteplus.com/en/docs/25/8016#vodheaderpair) |`-` |The HTTP Header for multipart upload. |

### VodStoreInfo

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Auth |String |`tos-v-da******b686cc06f489098` |The file upload credentials. |
|StoreUri |String |`SWT46O******iNjg2Y2MwNmY0ODkwOTg=` |The file storage address. |

### VodHeaderPair

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Key |String |`StorageClass` |The header key. |
|Value |String |`archive` |The header value. |

## Samples

### Sample request

```json
https://vod.byteplusapi.com?Action=ApplyUploadInfo&Version=2023-01-01&SpaceName=test&SessionKey=eyJleHRyYSI6InZpZ******YwODc4Njc1NTFcdTAwMjczdpMCJ9&FileType=media&FileName=example/123.mp4&FileExtension=.mp4
```

### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ApplyUploadInfo",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "UploadAddress": {
                "StoreInfos": [
                    {
                        "StoreUri": "tos-v-da******b686cc06f489098",
                        "Auth": "SWT46O******iNjg2Y2MwNmY0ODkwOTg="
                    }
                ],
                "UploadHosts": [
                    "tob-upload-x.snssdk.com"
                ],
                "UploadHeader": [
                    {
                        "Key": "StorageClass",
                        "Value": "archive"
                    }
                ],
                "SessionKey": "eyJleHRyYSI6InZpZGM9Ym9******YwODc4Njc1NTFcdTAwMjczdpMCJ9"
            }
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidAccessKeyError |\- |Invalid access key. |
|400 |InvalidParameter.InvalidParamError |\- |Invalid parameter. |
|400 |InvalidParameter.UserNotSupportTosError |\- |Account configuration error. |
|429 |RequestLimitExceeded.TooManyRequestError |\- |Request exceeds the limit. |
|400 |InvalidParameter.InvalidSpaceError |\- |Invalid space. |
|404 |ResourceNotFound.VideoNotFoundError |\- |Video not found. |
|400 |InvalidParameter.InvalidTopAccountError |\- |Account does not have permission. |
|403 |RequestForbidden.AccessIsRestricted |\- |Account access is restricted. |
|500 |InternalError.SaveDBError |\- |Internal error. |
|500 |InternalError.RunFunctionError |\- |Internal Error, function execution failed. |
|500 |InternalError.GetSignError |\- |Internal error, failed to get the upload URL signature. |
|500 |InternalError.RunPluginError |\- |Internal Error, plugin execution failed. |
|500 |InternalError.InternalError |\- |Internal Error. |
