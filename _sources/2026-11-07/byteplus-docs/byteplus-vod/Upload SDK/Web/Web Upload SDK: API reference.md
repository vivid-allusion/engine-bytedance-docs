---
title: "Web Upload SDK: API reference"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-upload-sdk-api-reference"
---

This article introduces the methods, events, and error codes of the Web Player SDK.

<span id="57c0123f"></span>
## API

<span id="03a6a338"></span>
### addFile(fileOption)

This method adds the file to be uploaded. This method returns `key`, such as `'file_1495442273603_999031'`, which can be regarded as the ID of this uploading task.

When adding a video file, you can configure `fileOption`, which contains the following parameters:


|**Parameter** |**Type** |**Required** |**Default value** |**Description** |
|---|---|---|---|---|
|file |Blob |Yes |null |The file to be uploaded |
|stsToken |Object |Yes |null |The upload token |
|type |String |No |`video` |The file type. Supported values:<br><br><br>* `video`<br><br>* `image`<br><br>* `object`<br><br>* `media` |
||||||
||||||
||||||
||||||
|callbackArgs |String |No |null |The callback parameters. |
|fileName |String |No |null |The path of the file to upload, which can be regarded as the position where the file stored in the BytePlys VOD service. It is a counterpart to `ObjectKey` in traditional object storage services. `FileName` cannot exceed 2048 bytes. You can customize the file path according to your business needs.<br><br><br>* The file path must contain the file suffix, for example, `".mp4"`. The file prefix is not required.<br><br>* The file path cannot start with `/`. And characters such as `?`,`$`,`\a`,`\b`,`\t`,`\n`,`\v`,`\f`,`\r` are not supported.<br><br>* `FileName` must be unique. Otherwise, the file may be overwitten.<br><br>* If you have set `FileName`, you do not need to set `FileExtension`. |
||||||
||||||
||||||
||||||
||||||
||||||
|fileExtension |String |No |null |The file suffix. The file suffix must start with `.` and cannot exceed 8 digits. If you have set `FileExtension`, you do not need to set `FileName`. The VOD service will automatically generate a file path, combining the file suffix with a 32\-bit random string. |
||||||
||||||
||||||
||||||
|storageClass |Number |No |1 |The storage type. Supported values:<br><br><br>* `1`: (Default) Standard storage.<br><br>* `2`: Archival storage. |
||||||
||||||
|processAction |JSON Array |No |null |An array of processing action objects for media assets uploaded. These actions can be used to perform tasks like capturing screenshots, configuring media details, triggering workflows, and more. For additional information, please see [Upload functions](https://docs.byteplus.com/en/docs/byteplus-vod/upload-functions). |


<span id="cfa9845b"></span>
### start(key)

This method starts the video upload task. If the video upload is paused, calling this method can resume uploading from where it was terminated. If you do not set the `key` parameter, the upload of all files will be started.

```JavaScript
uploader.start();
```


<span id="accbecf6"></span>
### removeFile(key)

This method removes the file to be uploaded or cancels the upload of the file. The `key` is returned by the `addFile` method.

```JavaScript
uploader.removeFile('file_1495442273603_999031');
```


<span id="fca1d79b"></span>
### cancel(key)

This method cancels the uploading task and deletes the information of the current uploading task. If you do not set the `key` parameter, the SDK cancels the uploading of all files.

```JavaScript
uploader.cancel();
```


<span id="c0205d12"></span>
### pause(key)

This method pauses the uploading task. The SDK temporarily stores the information of the current uploading task.

```JavaScript
uploader.pause();
```


<span id="d175ae98"></span>
## Events

To listen for the events of the uploading task, refer to the following sample code:

```JavaScript
uploader.on('xxx', function(data) {
    console.log('xxx', data);
});
```


The following table lists the events that may be triggered by the SDK during the lifecycle of an uploading task:


|**Event Name** |**Description** |
|---|---|
|crc32 |Occurs when the SDK slices the video. When a video is being uploaded, the SDK slices the video into multiple parts. This event returns an array of the CRC\-32 information and the length of each slice.File sharding and fetching crc32 |
|preUpload |Occurs when Get video upload information |
|initUploadID |Initialize Multipart Upload |
|progress |Indicates the progress (%) of the uploading task. |
|fileMerge |Occurs when all the slices are uploaded successfully and merged into one file. |
|complete |Occurs when the uploading task completes. When the SDK triggers the `complete` event, the progress of the uploading task is 100%. The `data` parameter of this event contains the `uploadResult` parameter, in which you can get the `vid` property. `vid` is the unique identifier of the video file in the media library. |


When capturing each life cycle, data information describing the current state can be obtained. This information is continuously improved throughout the cycle. The final data information is shown in the following table:


|Parameter |Description |
|---|---|
|uploadResult |Various information after uploading, including vid, uri, etc. (complete acquisition). See uploadResult for details. |
|startTime |Timestamp when the file started uploading |
|endTime |Timestamp of file completion upload |
|stageStartTime |Start timestamp of each stage |
|stageEndTime |Timestamp of completion of each stage |
|duration |The duration of each stage, calculation formula: stageEndTime \- stageStartTime |
|extra |Description of the current state (changing over the life cycle) |
|fileSize |Current video file size |
|key |The key of the current video file (automatically generated when addFile) |
|oid |The ID of the stored file (obtained by preUpload) |
|percent |Current upload overall progress percentage (%) |
|signature |Upload the required signature information (preUpload to obtain) |
|sliceLength |The size of each sharding (obtained by crc32) |
|stage |Current lifetime, if it is an unsupported browser, the value is'browserError' |
|status |File upload running status. Supported values:<br><br><br>* `1`: running<br><br>* `2`: cancel the operation<br><br>* `3`: suspended operation. |
|||
|||
|||
|task |Queue instance |
|type |Current task status, success/failure |
|uploadID |Upload the required uploadID (initUploadID get) |


<span id="6c6fe6b5"></span>
### uploadResult

**Video upload**

For the return result of video upload, only Vid will be returned by default. If you want to obtain detailed video meta information and cover image, please add configuration when uploading.


|Parameter |Type |Description |
|---|---|---|
|Vid |String |Video id, vid is the unique id of the video in the video architecture |
|PosterUri |String |Cover image uri, returned when a configuration to intercept cover information is added |
|VideoMeta |Object |Video meta information, returned when a configuration to obtain meta information is added |
|VideoMeta.Duration |Number |Video duration in seconds |
|VideoMeta.Width |Number |Video width |
|VideoMeta.Height |Number |Video height |
|VideoMeta.Format |String |Video format |
|VideoMeta.Bitrate |Number |Video bit rate |
|VideoMeta.FileType |String |File type |
|VideoMeta.Size |Number |Video file size |
|VideoMeta.Md5 |String |Video file md5 value |
|VideoMeta.Uri |String |The video source file is uri in tos, get the video broadcast address, please do not use this way to access |
|SourceInfo.VodVideoStreamMeta |Object |Video stream meta information, returned when a configuration to obtain meta information is added |
|VideoStreamMeta.Duration |Number |Video duration in seconds |
|VideoStreamMeta.Width |Number |Video width |
|VideoStreamMeta.Height |Number |Video height |
|VideoStreamMeta.Codec |String |Video encoding format |
|VideoStreamMeta.Bitrate |Number |Video streaming bit rate in kbps |
|VideoStreamMeta.Definition |String |video definition |
|VideoStreamMeta.Fps |Number |Video frames per second |
|AudioStreamMeta |Object |Audio stream meta information |
|AudioStreamMeta.Code |String |Audio encoding format |
|AudioStreamMeta.Duration |Number |audio duration |
|AudioStreamMeta.SampleRate |Number |Audio sample rate |
|AudioStreamMeta.Bitrate |Number |Audio bit rate in Kbps |
|AudioStreamMeta.Quality |String |Audio quality |


**File upload**


|Parameter |Type |Description |
|---|---|---|
|Uri |String |The uri of the source file in tos, the format is bucket/oid |
|ObjectMeta |Object |File meta information, returned when a configuration to obtain meta information is added |
|ObjectMeta.Md5 |String |File md5 value |
|ObjectMeta.Uri |String |Consistent with the Uri in the upper layer |


<span id="63c85e84"></span>
## Error codes


|Error code |Description |
|---|---|
|1000001 |Error reading file, addFile added file attribute non\-Blob/File instance. |
|1000002 |StsToken is malformed. This error occurs because the incoming Object field is missing. |
|1001000 |Error during application to upload domain name |
|1002000 |An error occurred while initializing the upload |
|1003000 |An error occurred during file upload |
|1003003 |Failed to read the uploaded file, which usually occurs when the file being uploaded is deleted. |
|1004000 |File sharding merge phase error |
|1005000 |Finish uploading, get media info error. |
|100006 |The request expires or the signature time of the request is from the future. If only some users have this problem, the possible reason is that the user's system time is not allowed. |
|100026 |Bad STS2. There may be various errors, such as: wrong signature, expired, etc. |
|100013 |Permission issue. |
|100009 |The requested AK is invalid. |
