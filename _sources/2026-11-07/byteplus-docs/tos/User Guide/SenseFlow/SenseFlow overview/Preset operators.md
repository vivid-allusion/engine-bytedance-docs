---
title: "Preset operators"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Preset-operators"
---

TOS SenseFlow offers a variety of preset operators. This topic describes the currently available preset operators.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">SenseFlow is currently only available in China (Beijing). Please contact your account manager for access.</div>


<span id="QImPkryc"></span>
## Preset operator list

<span id="jBUjU7bM"></span>
### TOS‑developed operators


|Operator name |Description |
|---|---|
|[Audio transcoding](https://docs.byteplus.com/en/docs/tos/Preset-operators#qsiAgXd3) |Converts WAV audio files to MP3 or AAC format and allows you to specify the audio specifications. |
|[Video transcoding](https://docs.byteplus.com/en/docs/tos/Preset-operators#6uwcbILR) |Converts MP4 video files to MP4 or HLS format and allows you to specify the encoding format and video specifications. |
|[Video generation animation](https://docs.byteplus.com/en/docs/tos/Preset-operators#RzKbqznl) |Generates GIF or WebP files from MP4 video files. |
|[Automatic speech recognition](https://docs.byteplus.com/en/docs/tos/Preset-operators#bbjp0vAD) |Recognizes speech content in Chinese or English from WAV or MP4 files and delivers results in JSON format. |


<span id="cjfxCFZ0"></span>
### Operators from other services


|Operator name |Description |
|---|---|
|Subtitle erasure |Removes subtitles from MP4 files and outputs video files without subtitles.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This operator is provided by <a href="https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-overview">AI MediaKit</a>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Make sure you have activated AI MediaKit and granted TOS the necessary permissions.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Usage constraints and additional billing apply (charged by AI MediaKit). </div><br> |


<span id="qsiAgXd3"></span>
## Audio transcoding operator

The audio transcoding operator uses preset templates to convert WAV files to the specified format. The default start time for transcoding is 00:00:00, and the duration matches that of the source file. These settings cannot be modified.

The table below lists the available templates and their details.


|Template name |Output format |Bitrate |Bitrate policy |Sample format |Sample rate |Number of channels |
|---|---|---|---|---|---|---|
|mp3\-320k |MP3 |320 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|mp3\-192k |MP3 |192 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|mp3\-128k |MP3 |128 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|mp3\-96k |MP3 |96 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|aac\-256k |AAC |256 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|aac\-160k |AAC |160 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|aac\-96k |AAC |96Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |
|aac\-64k |AAC |64 Kbps |Use the source audio bitrate when the source audio bitrate is less than the audio bitrate |\- |44100 Hz |2 |


<span id="6uwcbILR"></span>
## Video transcoding operator

The video transcoding operator uses preset templates to convert MP4 files to the specified format. The default start time for transcoding is 00:00:00, and the duration matches that of the source file. These settings cannot be modified.

The table below lists the available templates and their details.

<span id="6rEje1om"></span>
### MP4 templates


|Template name |Output format |Video parameters |Audio parameters |
|---|---|---|---|
|* h264\-mp4\-ld<br><br>* h265\-mp4\-ld |MP4 |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-mp4\-ld: 500 kbps<br><br>   * h265\-mp4\-ld: 400 kbps<br><br>* Resolution: 640 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 80 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-mp4\-sd<br><br>* h265\-mp4\-sd |MP4 |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-mp4\-sd: 800 kbps<br><br>   * h265\-mp4\-sd: 500 kbps<br><br>* Resolution: 720 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 80 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-mp4\-hd<br><br>* h265\-mp4\-hd |MP4 |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-mp4\-hd: 2000 kbps<br><br>   * h265\-mp4\-hd: 1200 kbps<br><br>* Resolution: 1280 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 128 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-mp4\-fhd<br><br>* h265\-mp4\-fhd |MP4 |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-mp4\-fhd: 3500 kbps<br><br>   * h265\-mp4\-fhd: 2200 kbps<br><br>* Resolution: 1920 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 160 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-mp4\-2k<br><br>* h265\-mp4\-2k |MP4 |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-mp4\-2k: 4800 kbps<br><br>   * h265\-mp4\-2k: 3000 kbps<br><br>* Resolution: 2048 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 160 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-mp4\-4k<br><br>* h265\-mp4\-4k |MP4 |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-mp4\-4k: 5600 kbps<br><br>   * h265\-mp4\-4k: 4000 kbps<br><br>* Resolution: 3840 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 160 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |


<span id="FZ4UTkuY"></span>
### HLS templates


|Template name |Output format |Shard duration |Video parameters |Audio parameters |
|---|---|---|---|---|
|* h264\-hls\-ld<br><br>* h265\-hls\-ld |HLS |5000 ms |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-hls\-ld: 500 kbps<br><br>   * h265\-hls\-ld: 400 kbps<br><br>* Resolution: 640 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 80 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-hls\-sd<br><br>* h265\-hls\-sd |HLS |5000 ms |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-hls\-sd: 800 kbps<br><br>   * h265\-hls\-sd: 500 kbps<br><br>* Resolution: 720 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 80 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-hls\-hd<br><br>* h265\-hls\-hd |HLS |5000 ms |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-hls\-hd: 2000 kbps<br><br>   * h265\-hls\-hd: 1200 kbps<br><br>* Resolution: 1280 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 128 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-hls\-fhd<br><br>* h265\-hls\-fhd |HLS |5000 ms |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-hls\-fhd: 3500 kbps<br><br>   * h265\-hls\-fhd: 2200 kbps<br><br>* Resolution: 1920 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 160 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-hls\-2k<br><br>* h265\-hls\-2k |HLS |5000 ms |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-hls\-2k: 4800 kbps<br><br>   * h265\-hls\-2k: 3000 kbps<br><br>* Resolution: 2048 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 160 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |
|* h264\-hls\-4k<br><br>* h265\-hls\-4k |HLS |5000 ms |* Delete video stream: No<br><br>* Encoding format: H.264 or H.265<br><br>* Bitrate control factor: 0<br><br>* Bitrate:<br><br>   * h264\-hls\-4k: 5600 kbps<br><br>   * h265\-hls\-4k: 4000 kbps<br><br>* Resolution: 3840 px × proportional height<br><br>* Frame rate: \- |* Delete audio stream: No<br><br>* Encoding format: AAC<br><br>* Bitrate: 160 kbps<br><br>* Sample format: \-<br><br>* Sample rate: 44100 Hz<br><br>* Number of channels: \- |


<span id="RzKbqznl"></span>
## Video generation animation operator

The video generation animation operator uses preset templates to convert a specified range of frames from an MP4 file into an animated image.

The following conversion parameters can be used to create GIF or WebP files.


|Parameter |Description |
|---|---|
|Start time |Sets the start time for video conversion. |
|Intercept duration |Sets the duration of the video segment to be converted. |
|Animation format |Sets the format of the animated image file. Supported formats: GIF and WebP. |
|Configuration output width and height |Sets the output width and height. If left unconfigured, the output dimensions will match those of the original video. |
|Frame rate |Sets the frame rate and scaling mode. Supported scaling modes: crop, stretch, fill, and fit. |
|Frame extraction interval |Sets the frame sampling interval and the number of sampled frames. |


<span id="bbjp0vAD"></span>
## Automatic speech recognition operator

The automatic speech recognition operator uses preset templates to recognize speech content from WAV or MP4 files and delivers the results in JSON format.

The following conversion parameters can be used for speech recognition.


|Parameter |Description |
|---|---|
|Recognize language |Specifies the language to be recognized:<br><br><br>* auto: Automatic detection.<br><br>* zh: Chinese.<br><br>* en: English. |
|Single\-segment result |Sets whether to deliver the recognition result as a single combined text segment:<br><br><br>* true: Single segment.<br><br>* false: Multiple segments. |
|Output format |Sets the output format for the recognition results. Currently, only the JSON format is supported. |


<span id="ccXLyv6q"></span>
## Subtitle erasure operator

The subtitle erasure operator uses preset templates to remove subtitles from MP4 files.

The following conversion parameters can be used to remove subtitles.


|Parameter |Description |
|---|---|
|Erase mode |Sets the subtitle removal mode:<br><br><br>* Subtitle: Removes text detected as subtitles.<br><br>* Text: Removes all detected text, not just subtitles. |
|Output coding mode |Sets the output video encoding format:<br><br><br>* Quality<br><br>* Size |
|Erase region |Sets a region for subtitle removal.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_33345844972a80781b25cbd803d2d5bb.png) </span> |
