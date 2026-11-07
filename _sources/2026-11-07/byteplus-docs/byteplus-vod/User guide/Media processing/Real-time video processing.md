---
title: "Real-time video processing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-real-time-video-processing"
---

To perform real\-time video processing on assets stored in BytePlus VOD, you can add the `x-vod-process` parameter to the resource URL. This guide explains how to use this parameter to take snapshots and obtain video metadata on the fly, providing detailed request parameters and result descriptions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Real\-time processing is an allowlist feature. Please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">contact us</a> to enable this feature.</div>


<span id="a80ae024"></span>
## Real\-time snapshots

Set `x-vod-process` to `video/snapshot` to take a single\-image snapshot of a specified time point in the video stream and compress it into an image of a specified size. For example:

```Bash
https://example.byteplus.com/video.mp4?x-vod-process=video/snapshot,t_7000
```


<span id="a33b8b12"></span>
### Request parameters


|**Parameters** |**Required** |**Parameter Description** |
|---|---|---|
|t |No |Snapshot time point. Value range is [0, video duration]. Only supports integers. Default value is 0, the unit is milliseconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the snapshot time is less than 0, the value of 0 will be used, which corresponds to the first frame. If the snapshot time exceeds the duration of the input video, an error message will be displayed.</div><br> |
|w |No |Snapshot width. Value range is [0, video width]. Only supports integers. The unit is pixel (px).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the snapshot width and height are both 0, the snapshot will use the resolution of the input video. If the height is 0, the snapshot will use the specified width and calculate the height according to the aspect ratio of the input video (and vice versa).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the specified height and width are not consistent with the aspect ratio of the input video, the snapshot may be stretched or deformed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If only the height or width is specified, the snapshot will be scaled according to the aspect ratio of the input video.</div><br> |
|h |No |Snapshot height. Value range is [0, video height]. Only supports integers. The unit is pixel (px). |
|m |No |Snapshot mode. It can take the following values:<br><br><br>* `accurate`: (Default) Accurate snapshots based on the specified snapshot time point.<br><br>* `fast`: Takes a snapshot of the last keyframe before the specified snapshot time point. |
|f |No |Image output format. It can take the following values:<br><br><br>* `jpg` (default)<br><br>* `png` |
|rotate |No |Snapshot rotation angle. It can take the following values:<br><br><br>* `auto`: (Default) automatically rotates the snapshot once generated based on the video information.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the video has no rotation information, it will not be rotated by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the video has rotation information, it is automatically corrected by default.</div><br><br><br>* `90`, `180`, and `270`: Rotates the snapshot clockwise by the specified number of degrees. |


<span id="1d36d75a"></span>
### Processing result

Returns the binary data stream of the snapshot:


* If the output image format is set to `jpg`, the HTTP Content\-Type header is `image/jpeg`

* If the output image format is set to `png`, the HTTP Content\-Type header is `image/png`


<span id="860f7833"></span>
## Obtaining metadata in real time

Set `x-vod-process` to `video/info` to get metadata for the specified video resource. For example:

```Bash
https://example.byteplus.com/video.mp4?x-vod-process=video/info
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have enabled URL signing for the domain name:</div>



* <div data-tips="true" data-tips-type="tip">Add the processing parameters to the query and avoid clashing with the URL signing parameter.</div>


* <div data-tips="true" data-tips-type="tip">Be careful when modifying the CDN cache rules for the domain name. Please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">contact technical support</a> to configure the cache with only video processing parameters.</div>



<span id="6995dbaf"></span>
### Processing result

Returns the extracted metadata JSON string. For example:

```JSON
{
    "format": {
        "nb_streams": 2,
        "nb_programs": 0,
        "format_name": "mov,mp4,m4a,3gp,3g2,mj2",
        "format_long_name": "QuickTime / MOV",
        "start_time": "0",
        "duration": "10.006",
        "size": "3390677",
        "bit_rate": "2710915",
        "probe_score": 100,
        "tags": {
            "compatible_brands": "isommp41mp42",
            "creation_time": "2021-11-02T14:48:46.000000Z",
            "major_brand": "mp42",
            "minor_version": "1"
        }
    },
    "streams": [
        {
            "index": 0,
            "codec_name": "h264",
            "codec_long_name": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
            "codec_type": "video",
            "codec_tag_string": "avc1",
            "codec_time_base": "1/60",
            "codec_tag": "0x31637661",
            "duration": "103.5",
            "bit_rate": "1397708",
            "disposition": {
                "default": 1
            },
            "bits_per_raw_sample": "8",
            "r_frame_rate": "30/1",
            "avg_frame_rate": "30/1",
            "nb_frames": "3105",
            "time_base": "1/15360",
            "start_pts": 0,
            "start_time": "0.000000",
            "duration_ts": 1589760,
            "profile": "High",
            "width": 720,
            "height": 1280,
            "coded_width": 720,
            "coded_height": 1280,
            "has_b_frames": 2,
            "sample_aspect_ratio": "1:1",
            "display_aspect_ratio": "9:16",
            "level": 31,
            "chroma_location": "left",
            "refs": 1,
            "is_avc": "true",
            "nal_length_size": "4",
            "pix_fmt": "yuv420p",
            "channels": 0,
            "sample_rate": "0",
            "sample_fmt": "",
            "channel_layout": "",
            "bits_per_sample": 0,
            "initial_padding": 0,
        },
        {
            "index": 1,
            "codec_name": "aac",
            "codec_long_name": "AAC (Advanced Audio Coding)",
            "codec_type": "audio",
            "codec_tag_string": "mp4a",
            "codec_time_base": "1/48000",
            "codec_tag": "0x6134706d",
            "duration": "103.531",
            "bit_rate": "139644",
            "disposition": {
                "default": 1
            },
            "bits_per_raw_sample": "",
            "r_frame_rate": "0/0",
            "avg_frame_rate": "0/0",
            "nb_frames": "4855",
            "time_base": "1/48000",
            "start_pts": 0,
            "start_time": "0.000000",
            "duration_ts": 4969488,
            "profile": "LC",
            "display_aspect_ratio": "",
            "channels": 2,
            "sample_rate": "48000",
            "sample_fmt": "fltp",
            "channel_layout": "stereo",
            "bits_per_sample": 0,
            "initial_padding": 0,
            "tags": {
                "handler_name": "#Mainconcept MP4 Sound Media Handler",
                "language": "eng"
            }
        }
    ]
}
```


<span id="1c61f876"></span>
### Metadata parameters

The `video/info` type returns a JSON string with the following parameters:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Parameters that are empty due to video and container format differences will not be returned.</div>



|**Parameters** |**Type** |**Note** |
|---|---|---|
|streams |Array of [Stream](https://docs.byteplus.com/docs/byteplus-vod/docs-real-time-video-processing#cb307886) |Video stream information. |
|format |[Format](https://docs.byteplus.com/docs/byteplus-vod/docs-real-time-video-processing#357582f0) |Container information. |


<span id="cb307886"></span>
#### Stream


|**Parameters** |**Type** |**Note** |
|---|---|---|
|index |int |Stream index value. |
|codec_name |string |Encoder name. |
|codec_long_name |string |Full encoder name. |
|codec_type |string |Encoder type. Possible values are as follows:<br><br><br>* `audio`: Audio stream<br><br>* `video`: Video stream<br><br>* `subtitle`: Subtitle stream |
|codec_tag_string |string |Encoder tag signature. |
|codec_time_base |string |Encoder duration per frame. |
|codec_tag |string |Encoder tag signature. |
|duration |string |Duration, in seconds. |
|bit_rate |string |Bit rate, in bps. |
|disposition |map[string]string |See [Disposition](https://docs.byteplus.com/docs/byteplus-vod/docs-real-time-video-processing#2f8b3dda) for additional information about this stream. |
|bits_per_raw_sample |string |Bits per sample in the original data. |
|r_frame_rate |string |Real video base frame rate. |
|avg_frame_rate |string |Average video frame rate, in fps. |
|nb_frames |string |Number of audio or video frames. |
|time_base |string |Time base. |
|start_pts |int |Starting presentation time stamp (PTS). |
|start_time |string |Start time, in seconds. |
|duration_ts |int |Duration calculated from the time base. |
|profile |string |Encoder configuration. |
|width |int |Video width, in px. |
|height |int |Video height, in px. |
|coded_width |int |Video codec width, in px. |
|coded_height |int |Video codec height, in px. |
|has_b_frames |int |1 if the video has B frames, 0 if it does not. |
|sample_aspect_ratio |string |Sample aspect ratio. |
|display_aspect_ratio |string |Display aspect ratio. |
|level |int |Video codec level. |
|chroma_location |string |Location of chromatic data. |
|refs |int |Number of reference frames. |
|is_avc |string |Whether or not the stream uses Advanced Video Coding (AVC). |
|nal_length_size |string |NAL unit length in bytes. |
|pix_fmt |string |Video pixel format. |
|channels |int |Number of audio channels. |
|sample_rate |string |Audio sampling rate, in Hz. |
|sample_fmt |string |Audio sampling format. |
|channels_layout |int |Audio channel layout. |
|bits_per_sample |int |Audio sampling bitrate, in bits. |
|initial_padding |int |Number of padding bytes at the start of the audio. |
|tags |map[string]string |Bitstream metadata. See [Tags](https://docs.byteplus.com/docs/byteplus-vod/docs-real-time-video-processing#9f440ee6) for details.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Custom fields written by the user are included in addition to the fields written by the video processing tool.</div><br> |


<span id="2f8b3dda"></span>
#### Disposition


|**Parameters** |**Type** |**Note** |
|---|---|---|
|default |int |Default stream flag. |
|dub |int |Dub track flag. |
|original |int |Original audio track flag. |
|comment |int |Comment track flag. |
|lyrics |int |Lyric track flag. |
|karaoke |int |Karaoke track flag. |
|forced |int |Forced subtitle flag. |
|hearing_impaired |int |Audio\-description captions flag. |
|visual_impaired |int |Visual\-description captions flag. |
|clean_effects |int |Clean effects track flag. |
|attached_pic |int |Attached picture flag. |
|timed_thumbnails |int |Timed thumbnail flag. |
|captions |int |Captions flag. |
|descriptions |int |Descriptions flag. |
|metadata |int |Metadata flag. |
|dependent |int |Dependent stream flag. |
|still_image |int |Static image flag. |


<span id="9f440ee6"></span>
#### Tags


|**Parameters** |**Type** |**Note** |
|---|---|---|
|compatible_brands |string |Container compatibility flag. This is generally written by the processing tool. |
|creation_time |string |Creation time. This is generally written by the processing tool. |
|major_brand |string |Major container flag. This is generally written by the processing tool. |
|minor_version |string |Minimum version. This is generally written by the processing tool. |
|handler_name |string |The name of the stream media handler, generally written by the processing tool. |
|language |string |Language. This is generally written by the processing tool. |


<span id="357582f0"></span>
#### Format


|**Parameters** |**Type** |**Note** |
|---|---|---|
|nb_streams |int |Number of streams for the file. |
|nb_programs |int |Number of programs for the file. |
|format_name |string |Container name. |
|format_long_name |string |Full container name. |
|start_time |string |Start time, in seconds. |
|duration |string |Duration, in seconds. |
|size |string |Size, in bytes. |
|bit_rate |string |Bit rate, in bps. |
|probe_score |int |Media file detection score; the higher the score, the higher the probability that the result is accurate. |
|tags |map[string]string |Container metadata. |


&nbsp;
