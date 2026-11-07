---
title: "GetPlayInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo"
---

Gets the playback addresses with the video ID. You can get the desired playback addresses by specifying parameters such as container format, codec, and definition.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Playback degrading logic: When you make a call to the <code>GetPlayInfo</code> interface, you have the option to specify parameters like container format, codec, and resolution in order to retrieve the corresponding playback address from the BytePlus VOD service. However, there are instances where the video information returned by the interface may not align with your expectations, potentially due to the activation of the playback degrading logic. For example, the transcoding service might only output H.264 videos, even if your business request calls for H.265 videos. Additionally, if you request an encrypted video and only set the <code>FileType</code> to <code>evideo</code>, leaving parameters like <code>Format</code> and <code>Codec</code> empty and resorting to default values, the VOD service may not be able to locate videos that meet the specific requirements. In such scenarios, the interface is unable to deliver results based on the initial request parameters, leading the playback service to implement specific logic for degradation. As a result, alternative transcoded videos will be selected for playback.</div>


<span id="requirements"></span>
## Requirements


* Before getting the playback address, you must:

   * Call [UpdateMediaPublishStatus](https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatemediapublishstatus) and set `Status` to `Published`.

   * [Adding domain names](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-management).

* Billing information: After adding the domain names, directly downloading or playing videos from the playback address will incur content distribution charges. For details, see [Content distribution](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing#content-acceleration).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetPlayInfo&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetPlayInfo` |The API action. For the current API, the value is `GetPlayInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v029c1g10003civ2i5mqib*******` |The video ID. After you upload audio and video files to the BytePlus VOD service, you can use the following methods to get the `Vid`:<br><br><br>* Get the `Vid` through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) API.<br><br>* If you have set a callback event for media upload completion, the `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|Format |String |No |`mp4` |The container format.<br><br><br>* When `FileType` is video, the supported values are as follows:<br><br>   * (Default) `mp4`<br><br>   * `dash`<br><br>   * `hls`<br><br>* When `FileType` is audio, the supported values are as follows:<br><br>   * (Default) `m4a`<br><br>   * `mp4`<br><br>   * `mp3`<br><br>   * `dash`<br><br>   * `hls`<br><br>   * `ogg` |
|Codec |String |No |`H265` |The codec:<br><br><br>* When `FileType` is video, the supported values are as follows:<br><br>   * (Default) `H264`<br><br>   * `H265`<br><br>* When `FileType` is audio, the supported values are as follows:<br><br>   * (Default) `aac`<br><br>   * `mp3`<br><br>   * `opus`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">When playing a video using the <code>Vid</code> and <code>PlayAuthToken</code>, it is advisable for the server not to specify the encoding format while generating the <code>PlayAuthToken</code>. When the client sends a playback request, the VOD service will dynamically select between H.264 or H.265 based on the configured policy. This approach allows for automatic and flexible encoding selection during playback, enhancing the viewing experience.</div><br> |
|Definition |String |No |`1080p` |The video resolution. This parameter is only valid when `FileType` is video. If you do not set `Definition`, the addresses of all resolutions are returned by default. Supported values:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br>* `od` (repackaging with the original resolution)<br><br>* `oe` (video enhancement)<br><br>* `auto` (ABR)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <code>Definition</code> parameter value is <code>oe</code>, if there is no video of the <code>oe</code> resolution in the VOD service, an empty list will be returned.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When both the <code>Definition</code> and <code>HDRDefinition</code> parameter values are <code>oe</code>, the union of the results will be taken.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To obtain the address of the adaptive bitrate streaming file, you should set <code>Definition</code> to <code>auto</code>. For how to generate the adaptive bitrate streaming file, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-abr-streaming">ABR streaming</a>. In cases where the BytePlus VOD service has not yet generated the adaptive bitrate streaming file, only the information of the original source video will be provided. It is also necessary to specify the <code>Codec</code> and <code>Format</code>. If no stream matching the specified format is available, an empty list will be returned.</div><br> |
|FileType |String |No |`video` |The file type. Supported values:<br><br><br>* `video`: (Default) Unencrypted video stream.<br><br>* `audio`: Unencrypted audio stream.<br><br>* `private_evideo`: Private encrypted video stream.<br><br>* `private_eaudio`: Private encrypted audio stream.<br><br>* `standard_evideo`: HLS standard encrypted video stream.<br><br>* `standard_eaudio`: HLS standard encrypted audio stream.<br><br>* `drm_evideo`: Widevine and FairPlay DRM encrypted video stream.<br><br>* `drm_eaudio`: Widevine and FairPlay DRM encrypted audio stream.<br><br>* `drm_evideo_playready`: PlayReady DRM encrypted video stream.<br><br>* `drm_eaudio_playready`: PlayReady DRM encrypted audio stream.<br><br>* `evideo`: (Deprecated) Private encrypted video stream.<br><br>* `eaudio`: (Deprecated) Private encrypted audio stream. |
|LogoType |String |No |`aa` |The watermark label. You can set the watermark label when creating a [watermark template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) in the BytePlus VOD console. |
|Ssl |String |No |`1` |Whether to return HTTPS playback addresses. Supported values:<br><br><br>* `1`: Yes.<br><br>* `0`: (Default) No.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Ensure that you have <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates">configured the SSL certificate</a>.</div><br> |
|NeedThumbs |String |No |`0` |Whether to return the CSS sprites. Supported values:<br><br><br>* `1`: Yes.<br><br>* `0`: (Default) No.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Ensure that you have generated the <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-sprites">CSS sprites</a>.</div><br> |
|NeedBarrageMask |String |No |`0` |Whether to return the masking bullet comments. Supported values:<br><br><br>* `1`: Yes.<br><br>* `0`: (Default) No. |
|UnionInfo |String |No |`87878***` |Used for playing private encrypted video and audio, the playback side extracts information from the browser or device that can identify access or device uniqueness. For details, see [Private encryption](https://docs.byteplus.com/en/docs/byteplus-vod/docs-private-encryption). |
|HDRDefinition |String |No |`1080p` |The HDR resolution. By default, this API does not return the video info of HDR resolution. Supported values:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br>* `oe` (video enhancement)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If <code>Definition</code> is set to <code>oe</code>, but there is no <code>oe</code> video on the BytePlus VOD server, the API will return an empty list.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If both <code>Definition</code> and <code>HDRDefinition</code> are set to <code>oe</code>, the result will be the union of the two.</div><br> |
|DrmExpireTimestamp |String |No |`1695037103` |The private encryption expiration timestamp in seconds. Once set, the issued `PlayAuthToken` will include an expiration timestamp for private encryption. |
|Quality |String |No |`higher` |The audio quality. Valid only when `FileType` is `audio` or `eaudio`. If `Quality` is not specified, this API returns the URLs of audio for all quality levels. Suppoted values:<br><br><br>* `medium`: Standard.<br><br>* `higher`: High.<br><br>* `highest`: Music. |
|PlayConfig |String |No |`{"PlayDomain":"vod.test_domain"}` |Custom playback configuration. It is a JSON string that can specify a playback domain. For example: `{"PlayDomain":"vod.test_domain"}`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not set the <code>PlayConfig</code> parameter and its <code>PlayDomain</code>, or if the <code>PlayDomain</code> is invalid, the VOD server will use the default domain name set in the <strong>Distribution acceleration</strong> \> <strong>Distribution settings</strong> page of the BytePlus VOD console to generate the playback address. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-settings#configuring-the-distribution-rule">Configuring the distribution rule</a>. However, if you set the <code>PlayConfig</code> parameter and its <code>PlayDomain</code> is valid, the VOD server will use the <code>PlayDomain</code> you provided to generate the playback address.</div><br> |
|ForceExpire |String |No |`60` |The valid duration of the playback address in seconds, ranging from 60 to 315360000. The `ForceExpire` parameter takes precedence over the URL expiration time configured in the BytePlus VOD console. |
|DashMode |String |No |`mpd` |When `Format` is set to `dash`, specify whether to deliver the video model or the MPD file (required for playback using third\-party players).<br><br><br>* `video_model`: (Default) Video model.<br><br>* `mpd`: MPD file.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">DASH (including regular DASH and DRM DASH) must be delivered via MPD for playback using third\-party players. However, domain configuration is required. Please contact our technical support team for assistance.</div><br> |
|DrmKEK |String |No |`DrmKEK` |A KEK (Key Encryption Key) generated by the client\-side Player SDK, used to encrypt or wrap the video private encryption key. This parameter is required for playing videos using BytePlus private encryption. For details, please refer to [Private encryption](https://docs.byteplus.com/en/docs/byteplus-vod/docs-private-encryption). |
|JSPlayer |String |No |`1` |Indicates whether the request comes from the Web Player SDK. A value of `1` signifies that the request is from the Web Player SDK. This parameter is required for playing videos using BytePlus private encryption. For details, please refer to [Private encryption](https://docs.byteplus.com/en/docs/byteplus-vod/docs-private-encryption). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v030c9g1000***imqljht955iqlsog` |The video ID. |
|Status |Integer |`10` |The video status. Supported values:<br><br><br>* `10`: The request was successful.<br><br>* Other values indicate that the video cannot be played. The following values may be returned:<br><br>   * `1000`: The video is not published.<br><br>   * `1010`: The video has been removed. |
|PosterUrl |String |`https://img.example.com/1234/image.jpeg` |The cover URL |
|Duration |Float |`0.1` |The video duration in seconds |
|FileType |String |`video` |The file type. Supported values:<br><br><br>* `evideo`: Encrypted video stream.<br><br>* `eaudio`: Encrypted audio stream.<br><br>* `video`: (Default) Unencrypted video stream.<br><br>* `audio`: Standard audio stream.<br><br>* `drm_evideo`: DRM encrypted video stream.<br><br>* `drm_eaudio`: DRM encrypted audio stream. |
|EnableAdaptive |Boolean |`false` |Whether key frames are aligned |
|TotalCount |Integer |`1` |The number of videos in the playlist |
|PlayInfoList |Array of [VodPlayInfo](https://docs.byteplus.com/en/docs/25/8045#vodplayinfo) |`-` |The list of playback information |
|ThumbInfoList |Array of [VodThumbInfo](https://docs.byteplus.com/en/docs/25/8045#vodthumbinfo) |`-` |The list of CSS sprite information |
|SubtitleInfoList |Array of [VodSubtitleInfo](https://docs.byteplus.com/en/docs/25/8045#vodsubtitleinfo) |`-` |The list of subtitle information |
|BarrageMaskUrl |String |`http://example.com/460224c***a9177b80b` |The URL of masking bullet comments |
|BarrageMaskInfo |Object of [BarrageMaskInfo](https://docs.byteplus.com/en/docs/25/8045#barragemaskinfo) |`-` |The masking bullet comment information |
|AdaptiveBitrateStreamingInfo |Object of [AdaptiveBitrateStreamingInfo](https://docs.byteplus.com/en/docs/25/8045#adaptivebitratestreaminginfo) |`-` |The information of ABR mainstream. Returned only when `Definition` is set to `auto`. |


#{.custom\-md\-table\-4}#

<span id="vodplayinfo"></span>
### VodPlayInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FileId |String |`v029c1g10003civ2i5mqib*******` |The file ID |
|Md5 |String |`398e352f8342aa29a6feee2a18e*****` |The MD5 value |
|FileType |String |`video` |The file type. Supported values:<br><br><br>* `evideo`: Encrypted video stream.<br><br>* `eaudio`: Encrypted audio stream.<br><br>* `video`: (Default) Unencrypted video stream.<br><br>* `audio`: Standard audio stream.<br><br>* `drm_evideo`: DRM encrypted video stream.<br><br>* `drm_eaudio`: DRM encrypted audio stream. |
|Definition |String |`1080p` |The video resolution |
|Quality |String |`normal` |The audio quality. Supported values:<br><br><br>* `medium`<br><br>* `higher`<br><br>* `highest` |
|Format |String |`mp4` |The container format |
|Codec |String |`H265` |The codec |
|LogoType |String |`aa` |The watermark label that you specified when creating a [watermark template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) in the BytePlus VOD console. |
|MainPlayUrl |String |`http://video.***.com/oIpB7fCZQ2ttbMe4Iklnvx********` |The main playback address |
|BackupPlayUrl |String |`http://video.***.com/oIpB7fCZQ2ttbMe4Iklnvx********` |The backup playback address |
|Bitrate |Integer |`1381635` |The bitrate (Kbps) |
|Width |Integer |`1920` |The video width in pixels. |
|Height |Integer |`1080` |The video height in pixels (px). |
|Size |Double |`1653067` |The video size, in bytes. |
|CheckInfo |String |`a:v029c1g10003civ2i5mqib*******\|b:0-983-ac368d50ea39b160********\|c:0-983-****` |Hijacking check information |
|IndexRange |String |`974-1089` |DASH segment_base to describe the range of header information |
|InitRange |String |`0-973` |DASH segment_base to describe the scope of the sidx |
|PlayAuth |String |`****` |Encrypted key. Used for the Web Player SDK to play private encrypted videos. For details, see [Playing private encrypted videos](https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-advanced-features-web#playing-private-encrypted-videos). |
|PlayAuthId |String |`****` |The key ID (Kid). Used for the Web Player SDK to play private encrypted videos. For details, see [Playing private encrypted videos](https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-advanced-features-web#playing-private-encrypted-videos). |
|BarrageMaskOffset |String |`100` |The offset of masking bullet comments |
|KeyFrameAlignment |String |`-` |The version of key frame alignment transcoding |
|Volume |Object of [VodVolumeInfo](https://docs.byteplus.com/en/docs/25/8045#vodvolumeinfo) |`-` |The volume infomation |
|Duration |Float |`0.1` |The video duration in seconds. |
|Channels |Integer |`2` |The number of audio channels in the stream. |
|MainUrlExpire |String |`1690534212` |The expiration time of the main playback address, represented as a Unix timestamp. |
|BackupUrlExpire |String |`1690534212` |The expiration time of the backup playback address, represented as a Unix timestamp. |


#{.custom\-md\-table\-4}#

<span id="vodvolumeinfo"></span>
### VodVolumeInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Peak |Double |`0.1` |Peak volume. |
|Loudness |Double |`0.1` |Volume loudness. |


#{.custom\-md\-table\-4}#

<span id="vodthumbinfo"></span>
### VodThumbInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CaptureNum |Integer |`27` |The total number of spapshots |
|StoreUrls |Array of String |`["http://vod-cover.com/tos-**a9/622ceb0***9eb7572971~tplv-vod-noop.image", "http://vod-cover.com/tos-**a9/26d92b1fdb***24~tplv-vod-noop.image"]` |The list of CSS sprite URLs |
|CellWidth |Integer |`242` |The width of a snapshot in pixels. |
|CellHeight |Integer |`136` |The height of a snapshot in pixels. |
|ImgXLen |Integer |`5` |The number of snapshots contained in each row of the sprite. |
|ImgYLen |Integer |`5` |The number of snapshots contained in each column of the sprite. |
|Interval |Double |`10` |The interval of taking snapshots, in seconds |
|Format |String |`jpg` |The image format |


#{.custom\-md\-table\-4}#

<span id="vodsubtitleinfo"></span>
### VodSubtitleInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v029c1g10003civ2i5mqib*******` |The video ID. |
|FileId |String |`v029c1g10003civ2i5mqib*******` |The subtitle file ID. |
|Language |String |`eng-US` |The subtitle language. |
|LanguageId |Integer |`1` |The subtitle language ID. For details, see [subtitle languages](https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language). |
|Format |String |`webvtt` |The subtitle format. |
|SubtitleId |String |`123` |The subtitle ID. |
|Title |String |`subtitle.vtt` |The subtitle caption. |
|Tag |String |`subtitle` |The subtitle tag. |
|Status |String |`enable` |The subtitle status. |
|Source |String |`MU` |The subtitle source. |
|StoreUri |String |`tos-vod-cn-**/191fe22a1c4a49************` |The subtitle file storage location. |
|SubtitleUrl |String |`http://example.com/191fe22a1c4a************` |The subtitle file URL. |
|CreateTime |String |`2019-10-12T07:20:50.52Z` |The creation time. |
|Version |String |`1` |The subtitle version. |


#{.custom\-md\-table\-4}#

<span id="barragemaskinfo"></span>
### BarrageMaskInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Version |String |`v1` |The version of masking bullet comments. |
|BarrageMaskUrl |String |`http://****.com/460224cfc86a9177b80b************` |The URL of the file containing masking bullet comments |
|FileId |String |`v029c1g10003civ2i5mqib*******` |The ID of the file containing masking bullet comments |
|FileSize |Double |`1` |The size of the file containing masking bullet comments |
|FileHash |String |`c2e595ab2db511daf6fc************` |The hash value of the file containing masking bullet comments |
|UpdatedAt |String |`1676017784` |The update date of the file containing masking bullet comments |
|Bitrate |Integer |`1` |The bitrate of the file containing masking bullet comments |
|HeadLen |Double |`1` |The header size of the file containing masking bullet comments |


#{.custom\-md\-table\-4}#

<span id="adaptivebitratestreaminginfo"></span>
### AdaptiveBitrateStreamingInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AbrFormat |String |`hls` |The container format of the ABR streaming file:<br><br><br>* `hls`<br><br>* `dash` |
|MainPlayUrl |String |`http://video.example.com/oIpB7fCZQ2ttb***` |The main URL of the main stream. |
|BackupPlayUrl |String |`http://video.example.com/oIpB7fCZQ2ttb***` |The backup URL of the main stream. |
|PlayAuth |String |`-` |The key ID of the main stream when private encryption is enabled.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, ABR does not support private encryption, so this field is empty.</div><br> |
|PlayAuthId |String |`66e2e8a1eaa17e7860422fc900111***` |The key ID of the main stream when DRM encryption is enabled. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetPlayInfo&Version=2023-01-01&Vid=v029c1g10003civ2i5mqib*******
```


<span id="Sample response"></span>
### Sample response

```json
{
    "Result": {
        "Vid": "v030c9g1000***imqljht955iqlsog",
        "Status": 10,
        "Duration": 0.1,
        "FileType": "video",
        "PosterUrl": "https://img.example.com/1234/image.jpeg",
        "TotalCount": 1,
        "PlayInfoList": [
            {
                "Md5": "398e352f8342aa29a6feee2a18e*****",
                "Size": 1653067,
                "Codec": "H265",
                "Width": 1920,
                "FileId": "v029c1g10003civ2i5mqib*******",
                "Format": "mp4",
                "Height": 1080,
                "Volume": {
                    "Peak": 0.1,
                    "Loudness": 0.1
                },
                "Bitrate": 1381635,
                "Quality": "normal",
                "FileType": "video",
                "LogoType": "aa",
                "PlayAuth": "****",
                "CheckInfo": "a:v029c1g10003civ2i5mqib*******|b:0-983-ac368d50ea39b160********|c:0-983-****",
                "InitRange": "0-973",
                "Definition": "1080p",
                "IndexRange": "974-1089",
                "PlayAuthId": "****",
                "MainPlayUrl": "http://video.***.com/oIpB7fCZQ2ttbMe4Iklnvx********",
                "BackupPlayUrl": "http://video.***.com/oIpB7fCZQ2ttbMe4Iklnvx********",
                "MainUrlExpire": "1690534212",
                "BackupUrlExpire": "1690534212",
                "BarrageMaskOffset": "100",
                "KeyFrameAlignment": "-"
            }
        ],
        "ThumbInfoList": [
            {
                "Format": "jpg",
                "ImgXLen": 5,
                "ImgYLen": 5,
                "Interval": 10,
                "CellWidth": 242,
                "StoreUrls": [
                    "http://vod-demo-cover.***.com/tos-**a9/622ceb0********9eb7572971_1639039860~tplv-vod-noop.image",
                    "http://vod-demo-cover.***.com/tos-**ba9/26d92b1fdb*******824_1639039860~tplv-vod-noop.image"
                ],
                "CaptureNum": 27,
                "CellHeight": 136
            }
        ],
        "BarrageMaskUrl": "http://example.com/460224c***a9177b80b",
        "EnableAdaptive": true,
        "BarrageMaskInfo": {
            "FileId": "v029c1g10003civ2i5mqib*******",
            "Bitrate": 1,
            "HeadLen": 1,
            "Version": "v1",
            "FileHash": "c2e595ab2db511daf6fc************",
            "FileSize": 1,
            "UpdatedAt": "1676017784",
            "BarrageMaskUrl": "http://****.com/460224cfc86a9177b80b************"
        },
        "SubtitleInfoList": [
            {
                "Tag": "subtitle",
                "Vid": "v029c1g10003civ2i5mqib*******",
                "Title": "subtitle.vtt",
                "FileId": "v029c1g10003civ2i5mqib*******",
                "Format": "webvtt",
                "Source": "MU",
                "Status": "enable",
                "Version": "1",
                "Language": "eng-US",
                "StoreUri": "tos-vod-cn-****/191fe22a1c4a49189a69************",
                "CreateTime": "2019-10-12T07:20:50.52Z",
                "LanguageId": 1,
                "SubtitleId": "123",
                "SubtitleUrl": "http://****.com/191fe22a1c4a49189a69************"
            }
        ],
        "AdaptiveBitrateStreamingInfo": {
            "AbrFormat": "hls",
            "MainPlayUrl": "http://video.example.com/oIpB7fCZQ2ttb***",
            "BackupPlayUrl": "http://video.example.com/oIpB7fCZQ2ttb***"
        }
    },
    "ResponseMetadata": {
        "Action": "GetPlayInfo",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidVid |\- |Invalid Vid. This may be due to the Vid being empty or having an abnormal length in the request parameters. |
|400 |InvalidParameter.VidNotExist |\- |The video does not exist. |
|404 |ResourceNotFound.NoAvailableDomain |\- |You have not configured the CDN domain. |


#{.custom\-md\-table\-4}#

&nbsp;
