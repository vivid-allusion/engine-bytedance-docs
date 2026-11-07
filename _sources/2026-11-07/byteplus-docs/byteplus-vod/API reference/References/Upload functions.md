---
title: "Upload functions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/upload-functions"
---

With the upload functions, you can capture screenshots, add media details, start workflows, and carry out additional tasks on media files uploaded to the BytePlus VOD service. Here's when you can use the upload functions:

* If you're uploading from the server, you can specify the upload function by setting the `Functions` parameter in the [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) interface.

* When uploading from the client using the Web Upload SDK, you can specify the upload function by setting the `processAction` parameter in the [addFile(fileOption)](https://docs.byteplus.com/docs/byteplus-vod/docs-web-upload-sdk-api-reference#03a6a338) method.

This document provides a detailed explanation of the upload functions.

## Functions

The supported parameters for JSON arrays are as follows:

|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Name |String |Yes |Upload function names. The following functions are supported:<br><br><br>* `Snapshot`: Capture a snapshot from the uploaded video. Once configured, you can retrieve the image URI from the `PosterUri` field in the response.<br><br>* `AddOptionInfo`: Use this function to specify details such as title, tags, type, and other metadata for the media.<br><br>* `StartWorkflow`: Trigger a workflow. Use this function to automatically initiate transcoding after the upload is finished. Keep in mind that media upload and workflow triggering happen asynchronously. Even if the workflow trigger fails, it will not impact the successful submission of the upload task. When employing this method, remember to monitor the workflow's execution status.<br><br>* `CaptionUpload`: Upload subtitle files and associate them with a Vid.<br><br>* `MediaUnderstand`: Trigger an AI video understanding task after the uploaded video metadata has been written. |
|Input |Object |No |Upload feature configuration. For different upload functions, pass different configurations as follows:<br><br><br>* [SnapshotInput](https://docs.byteplus.com/docs/byteplus-vod/upload-functions#a4cb9858): Snapshot configuration.<br><br>* [OptionInfo](https://docs.byteplus.com/docs/byteplus-vod/upload-functions#69f6e49c): Media information configuration.<br><br>* [WorkflowInput](https://docs.byteplus.com/docs/byteplus-vod/upload-functions#42b6ef14): Workflow trigger configuration.<br><br>* [CaptionUpload](https://docs.byteplus.com/docs/byteplus-vod/upload-functions#d0f097fd): Subtitle upload configuration.<br><br>* [MediaUnderstandInput](https://docs.byteplus.com/en/docs/25/35916#mediaunderstandinput): Video understanding configuration. |

### SnapshotInput

|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|SnapshotTime |Float |No |2 |Snapshot time, measured in seconds. The VOD server captures the video frame at this time to use as the video's cover. The default value is 0. |

### OptionInfo

|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Title |String |No |`upload` |Media asset title. Maximum 128 characters. |
|Tags |String |No |`01` |Media asset tags. Multiple tags can be separated by commas. |
|Description |String |No |`test` |Media asset description. |
|RecordType |Int |No |`1` |Media asset type:<br><br><br>* `1`: Audios and videos.<br><br>* `2`: Materials.<br><br>* `3`: Image assets. Generates a unique picture ID (`Pid`) for image management and processing. See [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement).<br><br><br>> **Note**<br><br><br>> Please refer to the [Uploading media assets overview page](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) for definitions of audio/video assets, image assets, and materials.<br> |
|Category |String |No |`video` |Material category. When RecordType is `2`, you must set this parameter to further divide materials into different categories:<br><br><br>* `video`<br><br>* `audio`<br><br>* `image`<br><br>* `dynamic_img`<br><br>* `subtitle`<br><br>* `font` |
|Format |String |No |`mp4` |Media asset format. If you pass a value for `Format`, the console displays the value you provided. Otherwise, it displays the format identified by the system. If the system cannot identify the file's format, this field may be empty. |
|ClassificationId |int64 |No |`1702994957` |The category ID for audio/video. When the `RecordType` parameter is set to 1 (audio and video), you can classify audio and video files by using the `ClassificationId` parameter. To create and manage the category of audio/video, follow these methods:<br><br><br>* Create it on the `Categories` page in the BytePluis VOD console.<br><br>* Create it using the [CreateVideoClassification](https://docs.byteplus.com/docs/byteplus-vod/reference-createvideoclassification) interface. |
|IsHlsIndexOnly |Boolean |No |`true` |Whether it is an HLS index file. Values are as follows:<br><br><br>* `true`: An HLS index file. When deleting the Vid file, the associated TS files are not deleted.<br><br>* `false`: (Default) When deleting the Vid file, the associated TS files are deleted. |

### WorkflowInput

|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TemplateId |String |No |`732db535401***8c234dc3aef` |The workflow ID. Used to automatically trigger the media processing workflow after uploading. To provide this parameter, obtain the workflow ID on the **Media processing** \> **Workflows** page in the BytePlus VOD console. For details, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow). |

### CaptionUpload

|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Vid |String |Yes |`v03c***eg0` |The video ID. |
|Fid |String |Yes |`v03c2***8eg0` |The file ID. Can be the same as `Vid`. |
|Language |String |Yes |`eng-US` |The subtitle language. For specific values, see [Subtitle languages](https://docs.byteplus.com/docs/byteplus-vod/docs-subtitle-language). |
|Format |String |Yes |`webvtt` |The subtitle format. The following values are available:<br><br><br>* `webvtt`<br><br>* `ass`<br><br><br>> **Note**<br><br><br>> When the subtitle format is `webvtt`, subtitle files with numbered lines are not supported for upload.<br> |
|StoreUri |String |No |`tos-vod-cn-v-03e4d54ef31***66a7d8c39f` |The subtitle file storage URI. |
|Title |String |No |`test` |The subtitle title. Maximum 128 characters. If this parameter is not provided, the title is not modified. If you provide an empty string, the existing title is cleared. |
|Source |String |No |`MU` |The subtitle upload source. The following values are available:<br><br><br>* `MT`: Machine translation.<br><br>* `ASR`: Speech to text.<br><br>* `MU`: (Default) Manual upload. |
|Tag |String |No |`01` |The subtitle tags. Maximum 128 characters. If this parameter is not provided, the tags are not modified. If you provide an empty string, the existing tags are cleared. |
|AutoPublish |Boolean |No |`true` |Whether to publish automatically. The following values are available:<br><br><br>* `true`: Auto publish.<br><br>* `false`: (Default) Do not auto publish. |
|ActionType |String |No |`upload` |Operation type. The following values are available:<br><br><br>* `upload`: (Default) Upload.<br><br>* `replace`: Replace. |

### MediaUnderstandInput

For `Name=MediaUnderstand`, `Input` uses the request\-body structure described in [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand). The upload service triggers the task after writing the uploaded video's metadata. Query the resulting understanding task with [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution).

This upload function is supported by the synchronous upload confirmation flow. Triggering Intelligent video understanding during URL\-based asynchronous upload is not supported.

## Example

```JSON
[
    {
        "Name": "Snapshot",
        "Input": {
            "SnapshotTime": 2.0
        }
    },
    {
        "Name": "AddOptionInfo",
        "Input": {
            "Title": "Test"
        }
    }
]
```

## Correspondence between `FileType` and `Category`

The table below shows the correspondence between the `FileType` parameter values and the `Category` parameter values:

|**FileType** |**Category** |
|---|---|
|`media` |* `video`<br><br>* `audio` |
|`image` |* `image`<br><br>* `dynamic_img` |
|`object` |* `subtitle`<br><br>* `font` |
