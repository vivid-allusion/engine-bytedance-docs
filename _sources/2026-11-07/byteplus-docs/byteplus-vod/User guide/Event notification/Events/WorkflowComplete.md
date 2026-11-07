---
title: "WorkflowComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete"
---

This article provides a description of the event parameters and includes examples of the `WorkflowComplete` event.

<span id="18bc48ca"></span>
## Event description

If you have configured callbacks for workflow completion, you will receive a notification when the workflow finishes. For information about how to set up a callback notification, see [Callbacks](https://docs.byteplus.com/docs/byteplus-vod/docs-system#aed0518b). Related API: [StartWorkflow](https://docs.byteplus.com/docs/byteplus-vod/reference-startworkflow).

<span id="dc1b466e"></span>
## Parameter


|Parameter |Type |Required |Description |
|---|---|---|---|
|RequestId |String | |The unique ID of the request |
|Version |String | |The callback version |
|EventType |String | |The name of the event |
|EventTime |String | |The time when the event occurred in UTC |
|Data |[Data](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#eb17237e) | |The callback content in JSON format |


<span id="eb17237e"></span>
### Data


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Code |String |The status code |
|Message |String |The message associated with the status code |
|Vid |String |The video ID |
|RunId |String |The ID of the workflow task |
|SpaceName |String |The space name |
|TemplateId |String |The workflow ID |
|CallbackArgs |String |Pass\-through information. If you set the `CallbackArgs` parameter when triggering the workflow, the custom data will be returned in the event. |
|SourceInfo |[SourceInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#439c5d31) |Information about the source file |
|PosterUri |String |The URI of the video cover image |
|TranscodeInfos |Array of [TranscodeInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#b129ac82) |Information about the transcoding output file |
|AdaptBitrateTranscodeInfos |Array of [AdaptBitrateTranscodeInfos](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#d92a5b8b) |Information about the ABR file. For how to generate the adaptive bitrate streaming file, see [ABR streaming](https://docs.byteplus.com/en/docs/byteplus-vod/docs-abr-streaming). |
|Snapshots |Array of [Snapshot](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#e9342424) |The results of snapshots. |


<span id="439c5d31"></span>
### SourceInfo

Information about the source file


|**Parameter** |**Type** |**Description** |
|---|---|---|
|FileId |String |The ID of the file |
|Md5 |String |The hash value of the file |
|FileType |String |The type of the file (either `video` or `audio`) |
|Codec |String |The codec of the file |
|Height |Integer |The video height in pixels. |
|Width |Integer |The video width in pixels. |
|Format |String |The video format |
|Duration |Float |The video duration in seconds |
|Size |Integer |The file size in bytes |
|FileName |String |The file path of the video |
|StoreUri |String |The address of the object storage |
|Definition |String |The video resolution |
|Bitrate |Integer |The video bitrate in bps |
|Fps |Float |The video frame rate in fps. |
|CreateTime |String |The creation time of the video |
|Inspection |[Inspection](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#d72be748) |The result of the source file inspection. Only available if you have enabled source file inspection. |
|SourceAdjustResult |[SourceAdjustResult](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#adc1e00d) |The result of the source file adjustment. Only available if you have enabled source file adjustment. |
|RepairResult |[RepairResult](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#ba501b8e) |The result of the source file repair. Only available if you have enabled source file repair. |


<span id="d72be748"></span>
### Inspection

Source file detection result


|**Parameter** |**Type** |**Description** |
|---|---|---|
|BlackFrames |Array of [BlackFrameInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#9a1fa140) |The result of black frame detection |
|Interlace |Boolean |The result of interlace detection |
|Quality |[Quality](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#f0936660) |The video quality parameters |
|DeLogo |Array of [DeLogoInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#3831c458) |The result of watermark removal |
|Suffix |[Suffix](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#9d457374) |The result of patch detection |


<span id="9a1fa140"></span>
### BlackFrameInfo

Black frame detection result


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Start |Float |The start time of the black frame in seconds |
|End |Float |The end time of the black frame in seconds |
|Duration |Float |The duration of the black frame in seconds |


<span id="f0936660"></span>
### Quality

Video quality detection result


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Visual |[VisualQuality](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#bd023acb) |The visual quality of the video |
|VolumeInfo |[VolumeInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#562a7fa6) |The volume of the video |


<span id="bd023acb"></span>
### VisualQuality


|**Parameter** |**Type** |**Description** |
|---|---|---|
|VQScore |Float |The quality score of video detection (VQScore) |
|Contrast |Float |The contrast |
|Colorfulness |Float |The colorfulness |
|Brightness |Float |The brightness |
|Texture |Float |The texture |
|Noise |Float |The noise |


<span id="562a7fa6"></span>
### VolumeInfo

Volume information


|Parameter |Type |Description |
|---|---|---|
|Loudness |Float |The loudness. Unit: LUFS |
|Peak |Float |The peak value. The range is (0, 1.0]. |
|MeanVolume |Float |The mean value. Unit: dB |
|MaxVolume |Float |The maximum value. Unit: dB |


<span id="3831c458"></span>
### DeLogoInfo

Watermark removal result


|**Parameter** |**Type** |**Description** |
|---|---|---|
|AnchorWidth |Integer |The anchor width |
|AnchorHeight |Integer |The anchor height |
|PosX |Integer |The X coordinate of the top\-left corner of the watermark |
|PosY |Integer |The Y coordinate of the top\-left corner of the watermark |
|SizeX |Integer |The width of the watermark |
|SizeY |Integer |The height of the watermark |


<span id="9d457374"></span>
### Suffix

Post\-roll detection result


|**Parameter** |**Type** |**Description** |
|---|---|---|
|StartTime |Float |Start time of the post\-roll in seconds. |
|EndTime |Float |End time of the post\-roll in seconds. |


<span id="adc1e00d"></span>
### SourceAdjustResult


|**Parameter** |**Type** |**Description** |
|---|---|---|
|AdjustType |String |The adjustment type:<br><br><br>* `origin_video`: Replacing the source video<br><br>* `new_vid`: Generating a new `Vid` |
|Vid |String |The new `Vid`. This field is only returned when `AdjustType` is `new_vid`. |


<span id="ba501b8e"></span>
### RepairResult

Source file repair result


|**Parameter** |**Type** |**Description** |
|---|---|---|
|BlackFrames |Integer |The result of black frame removal:<br><br><br>* `0`: Not executed<br><br>* `1`: Executed |
|Interlace |Integer |The result of ripple removal:<br><br><br>* `0`: Not executed<br><br>* `1`: Executed |
|DeLogo |Integer |The result of logo removal:<br><br><br>* `0`: Not executed<br><br>* `1`: Roughly executed<br><br>* `2`: Finely executed |
|Suffix |Integer |The result of patch removal:<br><br><br>* `0`: Not executed<br><br>* `1`: Executed |


<span id="b129ac82"></span>
### TranscodeInfo

Information about the transcoding output file


|**Parameter** |**Type** |**Description** |
|---|---|---|
|FileId |String |The file ID |
|Md5 |String |The file hash |
|FileType |String |The file type |
|LogoType |String |The watermark label that you specified when creating a [watermark template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) in the BytePlus VOD console. |
|Encrypt |Boolean |Whether the file is encrypted |
|EncodedType |String |The encryption type:<br><br><br>* `normal`: Normal non\-encrypted audio and video<br><br>* `encrypt`: Video encrypted with BytePlus' private encryption solution<br><br>* `audio_encrypt`: Audio encrypted with BytePlus' private encryption solution<br><br>* `drm_encrypt`: Video encrypted with DRM<br><br>* `drm_audio_encrypt`: Audio encrypted with DRM |
|Format |String |The format |
|Duration |Float |The duration of the transcoding output file in seconds |
|Size |Integer |The file size in bytes |
|FileName |String |The file path |
|StoreUri |String |The object storage address |
|VideoStreamMeta |[VideoStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#eb8ac66d) |The video stream metadata |
|AudioStreamMeta |[AudioStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#43cfdff2) |The audio stream metadata |
|Quality |[EncodedQuality](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#43e56dd2) |The quality of the transcoded stream. Only available if you have enabled the quality detection feature. |
|RepairResult |[RepairResult](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#ba501b8e) |The repair result of the transcoded stream. Only available if you have enabled repair feature. |
|CreateTime |String |The creation time |
|Height |Integer |Video height in pixels |
|Width |Integer |Video width in pixels |
|Fps |Float |Video frame rate in fps |
|Bitrate |Integer |Video bitrate in bps |


<span id="eb8ac66d"></span>
### VideoStreamMeta


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Duration |Float |The video stream duration in seconds |
|Definition |Float |The definition |
|Codec |String |The codec type |
|Bitrate |Integer |The video bitrate in bps |


<span id="43cfdff2"></span>
### AudioStreamMeta


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Codec |String |The codec type. Only available for audio\-only files. |
|Duration |Float |The audio stream duration in seconds. |
|SampleRate |Float |The audio sample rate. Only available for audio\-only files. |
|Bitrate |Integer |The audio bitrate. Only available for audio\-only files. |
|Channels |Integer |The number of audio channels. |


<span id="43e56dd2"></span>
### EncodedQuality


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Visual |[VisualQuality](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#bd023acb) |The visual quality of the video |
|VolumeInfo |[VolumeInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#562a7fa6) |The volume information |
|PSNR |PSNR |The PSNR (Peak Signal\-to\-Noise Ratio) result |
|SSIM |SSIM |The SSIM (Structural SIMilarity) result |
|VMAF |Float |The VMAF (Video Multi\-method Assessment Fusion) result |


<span id="d96835bb"></span>
### PSNR


|**Parameter** |**Type** |**Description** |
|---|---|---|
|PSNR_Y |Float |The Y value |
|PSNR_U |Float |The U value |
|PSNR_V |Float |The V value |
|PSNR_G |Float |The global PSNR |


<span id="d92a5b8b"></span>
### **AdaptBitrateTranscodeInfos**

Information about the ABR file


|**Parameter** |**Type** |**Description** |
|---|---|---|
|FileId |String |The file ID |
|Encrypt |Boolean |Whether the file is encrypted |
|LogoType |String |The watermark label that you specified when creating a [watermark template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) in the BytePlus VOD console. |
|Format |String |The container format |
|Size |Integer |The file size in bytes |
|StoreUri |String |The file URI |
|SubAdaptBitrateStreamMetas |Array of [SubAdaptBitrateStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#996ce963) |The sub\-stream metadata |
|CreateTime |String |Creation time |


<span id="996ce963"></span>
### **SubAdaptBitrateStreamMeta**

The sub\-stream metadata


|**Parameter** |**Type** |**Description** |
|---|---|---|
|FileType |String |The file type. Possible values:<br><br><br>* `video`: Normal video stream.<br><br>* `audio`: Normal audio stream. |
|Codec |String |The codec. When `FileType` is `video`, only the video codec is returned. |
|Height |Integer |The video height in pixels. This parameter is returned only when `FileType` is `video`. |
|Width |Integer |The video width in pixels. This parameter is returned only when `FileType` is `video`. |
|Duration |Float |The file duration in seconds |
|Definition |String |The video resolution. This parameter is returned only when `FileType` is `video`. |
|Bitrate |Integer |Bitrate in bps |
|Fps |Float |The video frame rate in fps. This parameter is returned only when `FileType` is `video`. |
|Size |Integer |The file size in bytes |


<span id="b46ea597"></span>
### SSIM


|**Parameter** |**Type** |**Description** |
|---|---|---|
|SSIM_Y |Float |The Y value |
|SSIM_U |Float |The U value |
|SSIM_V |Float |The V value |
|SSIM_G |Float |The global SSIM |


<span id="e9342424"></span>
### Snapshot

The results of snapshots


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Type |String |The snapshot type. Possible values are:<br><br><br>* `Poster`: The static image<br><br>* `Dynpost`: The dynamic image<br><br>* `AnimatedPoster`: The repeating animated image<br><br>* `Sprite`: The sprite image<br><br>* `Sample`: The sampled image<br><br>* `AIDynpost`: The AI\-generated dynamic image |
|Params |Object |The object containing specific parameters based on different snapshot types. The details are as follows:<br><br><br>* [Poster](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#7ff76318): The parameters of the static image<br><br>* [Dynpost](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#1ee8ae6c): The parameters of the dynamic image<br><br>* [AnimatedPoster](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#32ef45b4): The parameters of the repeating animated image<br><br>* [Sprite](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#93baeaf2): The parameters of the sprite image<br><br>* [Sample](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#aa2c8765): The parameters of the sampled image<br><br>* [AIDynpost](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete#cdd1f4f8): The parameters of the AI\-generated dynamic image |


<span id="7ff76318"></span>
### Poster

The static image


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Format |String |The file format |
|StoreUri |String |The file storage location |
|Width |Integer |The width in pixels |
|Height |Integer |The height in pixels |


<span id="1ee8ae6c"></span>
### Dynpost


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Format |String |The file format |
|StoreUri |String |The storage location |
|Width |Integer |The width in pixels |
|Height |Integer |The height in pixels |


<span id="32ef45b4"></span>
### AnimatedPoster


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Format |String |The file format |
|StoreUri |String |The storage location |
|Width |Integer |The width in pixels |
|Height |Integer |The height in pixels |


<span id="93baeaf2"></span>
### Sprite


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Format |String |The file format |
|StoreUris |Array of String |The storage locations of sprites |
|CellWidth |Integer |The width in pixels |
|CellHeight |Integer |The height in pixels |
|ImgXLen |Integer |The number of small images in the horizontal direction |
|ImgYLen |Integer |The number of small images in the vertical direction |
|Interval |Integer |The time interval between snapshots in seconds |
|CaptureNum |Integer |The number of snapshots |


<span id="aa2c8765"></span>
### Sample


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Format |String |The file format |
|StoreUris |Array of String |The storage locations of multiple sampled images. This parameter is only available when you set the output method of sampling snapshots to `Uri` in the snapshot template. |
|IndexUri |String |The URI of the snapshot index file. This parameter is only available when you set the output method of sampling snapshots to `Index file` in the snapshot template. The index file at this URI lists the snapshots in the order specified by the `Offsets` parameter. Example: `{"StoreUri": "xxx/uri1", "Offset": [2.5]}` |
|Width |Integer |The width in pixels |
|Height |Integer |The height in pixels |
|Interval |Float |The time interval between snapshots in seconds |
|CaptureNum |int32 |The number of snapshots |
|Duration |Float |The duration of the original video in seconds |
|Offsets |Array of Float |The time points of each snapshot. The snapshots will be output in ascending order by default. |


<span id="cdd1f4f8"></span>
### AIDynpost


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Format |String |The file format |
|StoreUri |String |The storage location |
|Width |Integer |The width in pixels |
|Height |Integer |The height in pixels |


<span id="f2935d2d"></span>
## Error code


|**Error Code** |**Description** |
|---|---|
|Success |Success |
|InvalidParameter.InvalidMediaStream |Media stream parsing failed. |
|InvalidParameter.MissingMediaStream |The media stream is missing. |
|InvalidParameter.InvalidUriError |The user address is invalid. |
|InvalidParameter.InvalidVidOrUri |The input source does not exist. |
|InternalError |An internal error has occurred. |
|InternalError.DownloadError |There was an error during the download. |
|InternalError.UploadError |There was an error during the upload. |
|InternalError.ExecutionTimeout |The execution timed out due to a system error. |


<span id="6b8d0082"></span>
## Example

Below is an example of the event that is triggered when the workflow execution in Vid mode is completed:

```JSON
{
        "EventType": "WorkflowComplete",
        "EventTime": "2020-09-16T06:58:36Z",
        "Version": "2.0",
        "Data": {
                "Code": "Success",
                "Snapshots": [{
                        "Params": {
                                "Width": 640,
                                "StoreUri": "tos-***c939aa/0923d7d3728d4d***1624a49_1600154189",
                                "Height": 360,
                                "OffsetTime": 0,
                                "Format": "jpeg"
                        },
                        "Type": "Poster"
                }, {
                        "Params": {
                                "Width": 640,
                                "StoreUri": "tos-***c939aa/2c7f0758cfb444b***e21a0bccff_1600238826",
                                "Height": 360,
                                "OffsetTime": 0,
                                "Format": "webp"
                        },
                        "Type": "Dynpost"
                }, {
                        "Params": {
                                "Width": 640,
                                "StoreUri": "tos-***c939aa/79311773a96b44***19b08e362_1600238743",
                                "Height": 360,
                                "Format": "webp"
                        },
                        "Type": "AnimatedPoster"
                }],
                "Vid": "v0c278ff00***s056tf1t526o5g",
                "SourceInfo": {
                        "Definition": "unknown",
                        "FileType": "video",
                        "Width": 1280,
                        "Codec": "h264",
                        "Fps": 59.9,
                        "StoreUri": "tos-***c939aa/6b539dfd4***8fc02a6bbe533",
                        "Format": "MP4",
                        "FileId": "v0c278ff0***s056tf1t526o5g",
                        "Height": 720,
                        "Duration": 111.706,
                        "Md5": "92246c899f***6e48b30a19ac31",
                        "Bitrate": 1331151,
                        "CreateTime": "2020-08-02T10:48:35Z",
                        "Size": 18587202
                },
                "PosterUri": "tos-***-0000/d25332d45b***4664df75b6b5",
                "TranscodeInfos": [{
                        "Encrypt": false,
                        "EncodedType": "normal"，
                        "Format": "MP4",
                        "FileType": "video",
                        "VideoStreamMeta": {
                                "Duration": 111.645,
                                "Definition": "360p",
                                "Codec": "h264",
                                "Bitrate": 325540.0
                        },
                        "LogoType": "",
                        "Height": 360,
                        "Width": 640,
                        "CreateTime": "2020-09-16T06:58:34Z",
                        "Size": 5622038,
                        "Fps": 59.94,
                        "Duration": 111.712,
                        "StoreUri": "tos-***c939aa/578f4e796***cc87a2bf97ce425",
                        "Bitrate": 402609,
                        "AudioStreamMeta": {
                                "Duration": 111.665,
                                "SampleRate": 44100,
                                "Bitrate": 64056.0
                        },
                        "FileId": "642b38362***82579e847e2c9ba7"
                }, {
                        "Encrypt": true,
                        "EncodedType": "encrypt"，
                        "Format": "MP4",
                        "FileType": "video",
                        "VideoStreamMeta": {
                                "Duration": 111.645,
                                "Definition": "540p",
                                "Codec": "h264",
                                "Bitrate": 608744.0
                        },
                        "LogoType": "",
                        "Height": 540,
                        "Width": 960,
                        "CreateTime": "2020-09-16T06:46:30Z",
                        "Size": 10467548,
                        "Fps": 59.94,
                        "Duration": 111.712,
                        "StoreUri": "tos-***c939aa/4057bf88870***93cffac8c8ec",
                        "Bitrate": 749609,
                        "AudioStreamMeta": {
                                "Duration": 111.665,
                                "SampleRate": 44100,
                                "Bitrate": 128020.0
                        },
                        "FileId": "2e8c27eace***26721cbf43b4c71"
                },{
                        "Encrypt": true,
                        "EncodedType" : "drm_encrypt",
                        "Format": "MP4",
                        "FileType": "video",
                        "VideoStreamMeta": {
                                "Duration": 111.645,
                                "Definition": "540p",
                                "Codec": "h264",
                                "Bitrate": 608744.0
                        },
                        "LogoType": "",
                        "Height": 540,
                        "Width": 960,
                        "CreateTime": "2020-09-16T06:46:30Z",
                        "Size": 10467548,
                        "Fps": 59.94,
                        "Duration": 111.712,
                        "StoreUri": "tos-***c939aa/4057bf88870***dda93cffac8c8ec",
                        "Bitrate": 749609,
                        "AudioStreamMeta": {
                                "Duration": 111.665,
                                "SampleRate": 44100,
                                "Bitrate": 128020.0
                        },
                        "FileId": "2e8c27eace9***6721cbf43b4c71"
                }],
                "RunId": "be:4c5f2f52e***955247efb9ee73c",
                "CallbackArgs": "",
                "TemplateId": "6340249409***b0df1f7abd5e65c4",
                "Message": "Success",
                "SpaceName": "test"
        },
        "RequestId": ""
}
```
