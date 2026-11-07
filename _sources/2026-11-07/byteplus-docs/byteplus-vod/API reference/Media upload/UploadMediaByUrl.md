---
title: "UploadMediaByUrl"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-uploadmediabyurl"
---

This interface is used to batch pull files from source file URLs and upload them to the VOD service. It supports audio and video files, material assets, and object\-type files.

> **Note**

* > This interface is designed for uploading files from public URLs (HTTP/HTTPS), not from local servers or client\-side storage.

* > Uploading media assets to VOD will incur storage costs. For details, refer to the [storage billing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing) documentation.

* > Before you begin, please review [Media asset upload overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) to understand our upload features, supported media types, formats, and size limits. This interface supports audio and video files, image assets, material assets, and object\-type files. Use `FileType` to specify the file type. To upload a file to the material library, set `RecordType` to `2` and use `Category` to specify the material category.

* > After a task is submitted, it is queued for asynchronous execution. Completion is not guaranteed to be real\-time.

* > After submitting an upload task, you can track its status in one of two ways:

   * > Periodically call [QueryUploadTaskInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-queryuploadtaskinfo) to query the status of the URL batch upload tasks.

   * > Configure [FileUploadByUrlComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadbyurlcomplete) event notification. You will receive a notification each time a URL upload is completed. For configuration methods, see [Configuring callback settings](https://docs.byteplus.com/docs/byteplus-vod/docs-system#configuring-callback-settings).

* > **URL requirement:** The `SourceUrl` must be a direct, publicly accessible link to the media file itself (`http://example.com/video.mp4`). It cannot be the URL of a web page that contains the video player (`http://example.com/watch?v=123`).

* > Please note that this interface does **not** use a JSON request body. Instead, all parameters must be sent in the Query String using the **application/x\-www\-form\-urlencoded** format.

## Requirements

The URL must be the source file URL, not the URL of a page containing video files.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UploadMediaByUrl&Version=2023\-01\-01

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UploadMediaByUrl` |The API action. For the current API, the value is `UploadMediaByUrl`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Spaces](https://console.byteplus.com/vodpaas/overview/?) page of the BytePlus console.<br><br>* Call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. |
|URLSets |Array of [VodUrlUploadURLSet](https://docs.byteplus.com/en/docs/25/8018#vodurluploadurlset) |Yes |`-` |The URL and their corresponding configurations, limited to 20 entries. |

### VodUrlUploadURLSet

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Md5 |String |No |`b9fd116504b***88e59a824878f07a` |The MD5 value of the file. When this parameter is not empty, the VOD server will calculate the MD5 value of the file and compare it with the MD5 value you have provided. If they do not match, an error will be reported.<br><br>> **Warning**<br><br><br>> This parameter is not effective for M3U8 files.<br> |
|Tags |String |No |`tag1` |The file tag. Multiple tags should be separated by commas and must not exceed 36 characters. |
|Title |String |No |`demo` |The file title. No more than 128 characters. |
|FileName |String |No |`example.mp4` |The file path. File path refers to the storage location of a file in VOD storage, similar to the ObjectKey concept in traditional object storage. You can customize the file path according to your business needs. The maximum length is 1024 characters.<br><br>> **Note**<br><br><br><br>* > The file path must include the file extension, such as `.mp4`. There is no mandatory requirement to include a file prefix.<br><br><br>* > For specific character rules, please refer to [Character rules for file naming](https://docs.byteplus.com/docs/byteplus-vod/docs-character-rules-for-file-naming).<br><br><br>* > When setting `FileName`, there is a risk of file overwriting if `FileName` is the same. Ensure that the `FileName` is different for different files.<br><br><br>* > After setting `FileName`, there is no need to set the `FileExtension` parameter.<br><br><br>* > This parameter is not valid when uploading M3U8 files.<br> |
|SourceUrl |String |No |`https://demourl` |The source file URL. |
|FileType |String |No |`image` |The file type. Valid values:<br><br><br>* `media`: (Default) An audio or video file.<br><br>* `image`: An image file.<br><br>* `object`: Another type of file, such as a subtitle or font file. |
|RecordType |Integer |No |`2` |The record type. Valid values:<br><br><br>* `1`: (Default) A media asset.<br><br>* `2`: A material asset.<br><br>* `3`: An image asset. Set `FileType` to `image`.<br><br><br>> **Note**<br><br><br>> To upload a material asset, set `RecordType` to `2` and use `Category` to specify the material category.<br> |
|Category |String |No |`image` |The material category. This parameter is required when `RecordType` is set to `2`. Valid values:<br><br><br>* `video`<br><br>* `audio`<br><br>* `image`<br><br>* `dynamic_img`<br><br>* `subtitle`<br><br>* `font`<br><br><br>> **Note**<br><br><br>> The mappings between `FileType` and `Category` are as follows: `media` corresponds to `video` and `audio`; `image` corresponds to `image` and `dynamic_img`; and `object` corresponds to `subtitle` and `font`.<br> |
|TemplateId |String |No |`25524a2dae45***b2e891d7daf4b9` |The workflow ID. After the upload is complete, to automatically trigger the media processing workflow, pass this parameter. The Workflow ID can be obtained from the **Media processing** \> **Workflows** page on the VOD console. |
|Description |String |No |`Video Testing` |The file description. No more than 1,024 characters. |
|CallbackArgs |String |No |`YourCallbackArgs` |Additional user information. It will be transparently passed through by the callback, with a maximum length of 512 bytes. |
|FileExtension |String |No |`.m3u8` |The file extension.<br><br>> **Note**<br><br><br><br>* > The file extension must start with a `.` and must not exceed 8 characters.<br><br><br>* > After setting `FileExtension`, there is no need to set the `FileName` parameter. VOD service will generate a 32\-bit random string, which will be concatenated with the `FileExtension` provided by you to form the file path.<br> |
|ClassificationId |Long |No |`6708` |The category ID. You can create the audio/video category as follows:<br><br><br>* Go to the BytePlus VOD console and navigate to **System settings** \> **Categories**.<br><br>* Call the [CreateVideoClassification](https://docs.byteplus.com/docs/byteplus-vod/reference-createvideoclassification) interface. |
|UrlEncryptionAlgorithm |String |No |`DES` |Source URL encryption method. The current supported value is `DES`, indicating PCKS5Padding encryption.<br><br>> **Warning**<br><br><br>> The encryption method must be submitted together with the file extension. You can choose to include the extension in `FileName`, or specify it by passing the `FileExtension` parameter.<br> |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Array of [ValuePair](https://docs.byteplus.com/en/docs/25/8018#valuepair) |`-` |Array of structures containing URL and corresponding JobId. |

### ValuePair

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SourceUrl |String |`https://demourl.mp4` |The source file URL. |
|JobId |String |`db3ab211095******b0955a30b550` |The corresponding JobId. It can be used to query the upload status. |

## Samples

### Sample request

```text
https://vod.byteplusapi.com?Action=UploadMediaByUrl&Version=2023-01-01
```

```json
{
    "SpaceName": "test",
    "URLSets": [
        {
            "Tags": "tag1",
            "Title": "demo",
            "FileName": "example.mp4",
            "SourceUrl": "https://demourl",
            "Templates": [
                {
                    "TemplateIds": [
                        "abcd***123"
                    ],
                    "TemplateType": "transcode"
                }
            ],
            "Description": "VideoTest",
            "CallbackArgs": "YourCallbackArgs",
            "ClassificationId": 6708
        }
    ]
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "Version": "2023-01-01",
        "Action": "UploadMediaByUrl",
        "Service": "vod",
        "RequestId": "202306041104200100100232280022D31",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "JobId": "db3ab211095******b0955a30b550",
                "SourceUrl": "https://demourl.mp4"
            }
        ]
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.UploadParamsError |*  |* Required field error, you can judge the specific field that is empty according to the prompt information.<br><br>* Parameter type error, you can determine whether the parameter type is correct based on the prompt information. |
|400 |InvalidParameter.AKMissMatchError |\- |Invalid parameter, the account has no permission. |
|500 |InternalError.QueryBodyError |\- |Internal error, failed to query JobId. |
|400 |InvalidParameter.JobIdEmptyError |\- |Invalid parameter, the JobIds field is empty. |
|400 |InvalidParameter.TitleLengthError |\- |Invalid parameter, the Title field exceeds 128 characters. |
|400 |InvalidParameter.DescriptionLengthError |\- |Invalid parameter, the Description field exceeds 256 characters. |
|400 |InvalidParameter.CategoryLengthError |\- |Invalid parameter, the Category field exceeds 256 characters. |
|400 |InvalidParameter.TagsLengthError |\- |Invalid parameter, the Tags field exceeds 36 characters. |
|400 |InvalidParameter.BodyParseError |\- |Invalid parameter, The format of the passed parameter is incorrect. |
|500 |InternalError.CreateUploadStateError |\- |Internal error, failed to create URL upload record. |
|500 |InternalError.BuildRavenDataError |\- |Internal error, failed to create internal message. |
|500 |InternalError.NsqSendError |\- |Internal error, failed to send the message. |
|500 |InternalError.GetAccountError |\- |Internal error, failed to retrieve account information. |
|400 |InvalidParameter.SpaceNotExistsError |\- |Invalid paramater, the space does not exist. |
|403 |RequestForbidden.AccessIsRestricted |\- |Account access is restricted. |
|400 |InvalidParameter.InvalidFileExtensionStyle |\- |Incorrect file extension format. |
