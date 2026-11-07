---
title: "OpenAPI changelog"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1"
---

## 2026\-11

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |2026\-11\-02 |Added the request parameters `Order` and `URLMode` to set the order and URL mode of substreams in the HLS master playlist. |ABR configuration |
|更新 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) ||Added the response parameters `Order` and `URLMode` to get the order and URL mode of substreams in the HLS master playlist. ||

## 2026\-10

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |2026\-10\-21 |Added the request parameters `Callback` and `Sei`. `Callback` specifies the URL used to receive AI Dubbing callback messages. `Sei` specifies whether to write subtitles into SEI messages in the live stream. |AI Dubbing |
|更新 [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) ||Added the request parameter `SIOutput`, which includes `Callback` and `Sei`. `Callback` specifies the URL used to receive AI Dubbing callback messages. `Sei` specifies whether to write subtitles into SEI messages in the live stream. |Subtitle configuration |
|更新 [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) ||||
|更新 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) ||Added the response parameter `SIOutput`, which includes `Callback` and `Sei`. `Callback` returns the URL used to receive AI Dubbing callback messages. `Sei` returns whether subtitles are written into SEI messages in the live stream. ||
|更新 [DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) ||||

## 2026\-09

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023) |2026\-09\-07 |* Added the request parameter `TransSuffixs` to specify the transcoded stream or ABR substream suffixes to which the watermark configuration applies.<br><br>* Request parameters `PosX` and `PosY` are required only when `WatermarkMode` is set to `static`.<br><br>* Added the request parameter `WatermarkMode` to specify the watermark type.<br><br>* Added the request parameters `DynamicMode` and `DynamicSpeedLevel` to configure dynamic watermarks. |Watermark |
|更新 [UpdateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023) ||* Added the request parameter `TransSuffixs` to specify the transcoded stream or ABR substream suffixes to which the watermark configuration applies.<br><br>* Added the request parameter `WatermarkMode` to specify the watermark type.<br><br>* Added the request parameters `DynamicMode` and `DynamicSpeedLevel` to configure dynamic watermarks.<br><br>* Updated how optional request parameters are handled. For more information, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023?lang=en#usage-scenario). ||
|更新 [ListWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023) ||* Added the response parameter `WatermarkMode` to get the watermark type.<br><br>* Added the response parameter `TransSuffixs` to get the transcoded stream or ABR substream suffixes to which the watermark configuration applies.<br><br>* Added the response parameters `DynamicMode` and `DynamicSpeedLevel` to get dynamic watermark configurations. ||
|更新 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) ||||

## 2026\-08

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) |2026\-08\-13 |Added the request parameter `PullRequestHeaders` to configure the HTTP request headers included in pull stream requests when a relay task pulls content from a live source or a VOD source. The supported headers are `Referer` and `UserAgent`. |Relay |

## 2026\-07

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |2026\-07\-22 |Added `udp_websdk` as a new value of the `Protocol` response parameter to support generating RTM pull stream addresses for the BytePlus MediaLive Player SDK for Web. |Pull stream address |

## 2026\-06

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |2026\-06\-25 |Added the request parameter `IsRtmAbr`, and added the value `rtm-abr` for the `Type` parameter, to support the RTM\-ABR protocol type when creating ABR configurations. |ABR configuration |
|更新 [DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023) ||Added the value `rtm-abr` for the `Type` parameter, to support deleting ABR configurations with the RTM\-ABR protocol type. ||

## 2026\-04

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |2026\-04\-21 |Added AI Dubbing task APIs, including creating, updating, restarting, deleting, querying, and searching tasks. |AI Dubbing |
|新增 [UpdateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask) ||||
|新增 [RestartSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask) ||||
|新增 [DeleteSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask) ||||
|新增 [GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) ||||
|新增 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) ||||
|新增 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) ||Added an API for getting the AI Dubbing configuration available to the current account. ||
|更新 [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) ||Added AI Dubbing mode support to subtitle configuration APIs, including creating, updating, listing, and querying details of subtitle configurations. ||
|更新 [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) ||||
|更新 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) ||||
|更新 [DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) ||||
|新增 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) ||Added an API for getting the fonts and languages available to the current account for AI Dubbing mode in subtitle configurations. ||

## 2025\-12

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2025\-12\-22 |Added the request parameter `VodRegion` to configure the VOD region. |Recording |
|更新 [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) ||||
|更新 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) ||Added the response parameter `VodRegion` to get the VOD region. ||

## 2025\-10

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |2025\-10\-14 |Added the response parameter `AuthType` to get the URL authentication type for generating push or pull stream addresses. |URL authentication |
|更新 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) ||||
|更新 [DescribeAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023) ||Added the response parameter `AuthType` to get the URL authentication type. ||
|更新 [UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) ||* Added the request parameter `TimeStampBase` to set the time format of the timestamp.<br><br>* Added the request parameter `AuthType` to set the URL authentication type. ||

## 2025\-09

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |2025\-09\-15 |Support for getting the monitoring data, such as frame rate and bitrate of audios and videos, for all or specific origin\-pull streams under specific domain name for stream pulling within specific time range. You can use the monitoring data to assess the health of origin\-pull streams. |Data statistics |
|新增 [DescribeLiveStreamCountData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata) ||Support for getting the peak count of specific pushed streams, origin\-pull streams, or transcoded streams within a specific time range. ||
|新增 [CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) ||Replaced `CreateSnapshotPreset` with this API to add the screenshot configuration. |Screenshot configuration |
|新增 [UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) ||Replaced `UpdateSnapshotPreset` with this API to update the screenshot configuration. ||
|新增 [ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) ||Replaced `ListVhostSnapshotPreset` with this API to get screenshot configuration information. ||

## May, 2025

|API |Release date |Description |Related feature |
|---|---|---|---|
|新增 [UpdateRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023) |2025\-05\-29 |Added new Remote Authentication APIs for configuring, querying, deleting, and listing authentication settings for live stream pushing. |Remote authentication |
|新增 [DescribeRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023) ||||
|新增 [DeleteRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteremoteauth-2023) ||||
|新增 [ListVhostRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostremoteauth-2023) ||||

## April, 2025

|API |Release date |Description |Related feature |
|---|---|---|---|
|新增 [CreateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask) |2025\-04\-14 |Added new APIs for live stream looping, supporting dynamic content updates, playback order configuration, intro skipping, and instant switching. |Loop Playlist Configuration |
|新增 [DeleteCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask) ||||
|新增 [UpdateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask) ||||
|新增 [GetCarouselDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail) ||||
|新增 [ListCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask) ||||
|新增 [DescribeLiveCallbackData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata) ||Added a new API for querying callback records related to live stream publishing. The API provides event type, status, request, and response data for diagnosing abnormal callbacks and verifying callback delivery. |Callback |

## February, 2025

|API |Release date |Description |Related feature |
|---|---|---|---|
|更新 [DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata) |2025\-02\-05 |1. The `RefererList` parameter and associated values have been removed from the API request, simplifying the query process.<br><br>2. New `HitRate` and `TotalHitRate` parameters have been introduced to provide more detailed insights into edge request hit rates. |Statistics and analysis |

## January, 2025

|API |Release date |Description |Related feature |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2025\-01\-22 |Changed the value range of the request parameter `SliceDuration` from [5,30] to [2,100]. |Recording configuration |

## December, 2024

|API |Release date |Description |Related feature |
|---|---|---|---|
|新增 [CreateLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivepadpreset-2023) |2024\-12\-20 |Add related API for managing standby stream configuration and standby stream management. |Standby stream |
|新增 [DescribeLivePadPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivepadpresetdetail-2023) ||||
|新增 [UpdateLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatelivepadpreset-2023) ||||
|新增 [DeleteLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivepadpreset-2023) ||||
|新增 [DescribeLivePadStreamList](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivepadstreamlist-2023) ||||
|新增 [StopLivePadStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoplivepadstream-2023) ||||
|新增 [DescribeLiveTopPlayData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023) |2024\-12\-09 |Added an interface to query TOPN live stream or domain name traffic and bandwidth information. |Statistics and analysis |

## October, 2024

|API |Release date |Description |Related feature |
|---|---|---|---|
|更新 [Callback description](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description) |2024\-10\-16 |The PlayProgress field has been added to the callback message for Relay, used to return the playback duration (in seconds) of Video\-on\-Demand (VOD) files. This field is only returned when the stream pulling source is a VOD file (Type=1).<br><br>**Impact of the Change**<br><br><br>* **Applicable Scenarios**: If you are pulling a VOD source for pushing, this field allows more accurate tracking of the playback progress. It is suitable for scenarios requiring progress synchronization, such as ad insertion and content switching.<br><br>* **Unaffected Scenarios**: If you are pulling a live stream source for pushing, this change does not affect you. |Callback |
|更新 [Callback description](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description) |2024\-10\-11 |To support the recording of larger files and avoid data overflow issues caused by excessively large files, the type of the size field in the callback message for Recording, which represents the size of the recorded file, has been updated from Integer to Long. This improves stability and accuracy when handling large files. |Callback |

## September, 2024

|API |Release date |Description |Related feature |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2024\-09\-18 |Support creating recording configurations for transcoded streams. And support storing recorded files in BytePlus TOS. |Recording |
|更新 [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) ||||
|更新 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) ||||
|更新 [DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) ||||
|更新 CreateSnapshotPreset ||Supports storing screenshot files to BytePlus TOS. |Screenshot capture |
|更新 UpdateSnapshotPreset ||||
|更新 ListVhostSnapshotPreset ||||
|更新 [DescribeCDNSnapshotHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023) ||||
|更新 [CreateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023) ||Time\-shifted file storage supports BytePlus TOS. |Time shifting |
|更新 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) ||||
|更新 [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) ||Support setting the loop playback times for on\-demand videos. And support adding watermarks to streamed output videos. |Relay |
|更新 [UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) ||||

## August 02, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023)<br><br>* [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023)<br><br>* [RestartPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-restartpulltopushtask-2023)<br><br>* [StopPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppulltopushtask-2023)<br><br>* [DeletePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushtask-2023)<br><br>* [UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) |Update |Add, update, delete, query, enable, and disable Group parameters for creating, updating, deleting, querying, enabling, and disabling Relay interfaces in BytePlus. |
|* [ListPullToPushTaskV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023)<br><br>* [CreatePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023)<br><br>* [DeletePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushgroup-2023) |New |To query the Relay task list, we have added a new interface that supports the POST method.<br><br>Support creating, updating, and deleting relay task group. |
|* [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023)<br><br>* [DeleteSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023)<br><br>* [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023)<br><br>* [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) |New |Support creating subtitle configurations, adding subtitles to the specified transcoded stream, and supporting subtitle translation. |

## July 19, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [UpdateEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencrypthls)<br><br>* [DescribeEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls)<br><br>* [GetHLSEncryptDataKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-gethlsencryptdatakey) |New |Support configuring the key acquisition address required for HLS encryption. |
|* [BindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1)<br><br>* [ListBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4) |Updated |Support adding new HLS standard encryption configuration. |

## June 30, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|[CreateDomainV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn) |Updated |Support for configuring acceleration regions for each domain name. |
|* [UpdateRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateregionaccessrule)<br><br>* [DescribeRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeregionaccessrule) |Updated |Supports the configuration of regional restrictions at the provincial level. |

## April 16, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [UpdateHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig)<br><br>* [DescribeHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig)<br><br>* [DeleteHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig) |New |Update, describe and delete HLS configuration. |
|* [UpdateCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig)<br><br>* [DescribeCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig)<br><br>* [DeleteCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletecmafconfig) |New |Update, describe and delete DASH configuration. |
|* [UpdateLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig)<br><br>* [DescribeLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig)<br><br>* [DeleteLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletelatencyconfig) |New |Update, describe and delete latency configuration. |

## April 8, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)<br><br>* [DescribeLiveStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023) |Updated |As an IAM user, you can now create a transcoding template and retrieve information of specified live streams. |

## March 18, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|[DescribeLiveLogData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |New |Retrieve the information of log files for streaming playback, streaming push, source retrieval, and streaming playback with push. |
|* [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023)<br><br>* [DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023?lang=en) |New |Configure transcoding templates for adaptive bitrate streaming in batch. |
|* [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)<br><br>* [UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1) |Updated |You can now query and update the transcoding template for adaptive bitrate streaming. |
|[DescribeLivePushStreamInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |New |Query the information of the ended push streams. |

## March 14, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [EnableHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-enablehttpheaderconfig)<br><br>* [DeleteHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-deletehttpheaderconfig)<br><br>* [DescribeHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-describehttpheaderconfig)<br><br>* [UpdateHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-updatehttpheaderconfig) |New |Configure additional HTTP headers in the request sent to a third\-party origin server during an origin\-pull task and the response sent from an edge server to a client. |

## March 07, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|[DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata?lang=en) |Updated |You can now query the cache hit rate of edge servers. |

## March 06, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [DescribeRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-dakt2mfojk)<br><br>* [DeleteRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-3nf0nln2b2)<br><br>* [UpdateRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-updaterelaysourcerewrite) |New |Configure the origin address rewrite rules for on\-demand origin\-pull tasks. |

## February 07, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|[ListCertV2](https://docs.byteplus.com/docs/byteplus-media-live/docs-listcertv2) |New |Query the SSL certificates under your account. |

## January 25, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm)<br><br>* [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm)<br><br>* [UpdateEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateencryptdrm)<br><br>* [DescribeEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_2)<br><br>* [BindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_1)<br><br>* [UnBindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_3)<br><br>* [ListBindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_4) |New |Implement Digital Rights Management (DRM) encryption on your live streams. |
|* [UpdateIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateipaccessrule)<br><br>* [DescribeIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule)<br><br>* [DeleteIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteipaccessrule) |New |Configure an IP blocklist or allowlist to restrict access to your domain names. |
|* [UpdateRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateregionaccessrule)<br><br>* [DescribeRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeregionaccessrule)<br><br>* [DeleteRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteregionaccessrule) |New |Limit requests from specific geographic regions. |
|* [UpdateFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateformataccessrule)<br><br>* [DescribeFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeformataccessrule)<br><br>* [DeleteFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteformataccessrule) |New |Limit requests to pull live streams of specific protocols. |

## January 11, 2024

|**API** |**Type** |**Description** |
|---|---|---|
|* [DescribeUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeuseragentaccessrule)<br><br>* [DeleteUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1)<br><br>* [UpdateUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateuseragentaccessrule) |New |Manage a User\-Agent (UA) blocklist or allowlist. |

## October 31, 2023

|**API** |**Type** |**Description** |
|---|---|---|
|* [CreateDomainV2](https://docs.byteplus.com/docs/byteplus-media-live/docs-dj3h3u96xn) |New |Creates one or more domain names for stream pushing or pulling. |
|* [UpdateDomainVhost](https://docs.byteplus.com/docs/byteplus-media-live/docs-updatedomainvhost) |New |Changes the domain name space associated with a domain name. |
|* [UpdateClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateclusterratelimit)<br><br>* [DeleteClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteclusterratelimit)<br><br>* [DescribeClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeclusterratelimit) |New |Manage the frequency limit for pull\-stream requests. |
|* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en) |New |Manage scheduled origin\-pull tasks. |

## July 28, 2023

|**API** |**Type** |**Description** |
|---|---|---|
|* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en)<br><br>* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |New |Create, update, and query origin\-pull tasks. |
|* UpdateRelaySourceV2<br><br>* DeleteRelaySourceV2<br><br>* DescribeRelaySourceV2 |Deleted |Use the following endpoints instead:<br><br><br>* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en)<br><br>* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |

## July 6, 2023

|**API** |**Type** |**Description** |
|---|---|---|
|* [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)<br><br>* [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023)<br><br>* [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |New |Create, update, and query recording templates. You can now store recordings using BytePlus VOD. |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |Updated |* You can now query recordings stored in BytePlus VOD. |
|* [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)<br><br>* [UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1)<br><br>* [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)<br><br>* [ListCommonTransPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023) |Updated |* The value ranges for several parameters have been expanded.<br><br>* A new parameter, `Roi`, has been added. This parameter determines whether to transcode using the low\-bitrate HD mode. |
|* [UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023)<br><br>* [DescribeCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023) |Updated |* You now have the option to set a key for your callbacks, allowing you to authenticate the callbacks sent from BytePlus MediaLive.<br><br>* In addition, new fields are added to [callback messages](https://docs.byteplus.com/en/byteplus-media-live/docs/callback-description). |
|* CreateRecordPreset<br><br>* ListVhostRecordPreset<br><br>* UpdateRecordPreset |Deprecated |Use the following endpoints instead:<br><br><br>* [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)<br><br>* [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023)<br><br>* [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |

## June 6, 2023

|**API** |**Type** |**Description** |
|---|---|---|
|* [DescribeLiveBatchPushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023)<br><br>* [DescribeLiveSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics)<br><br>* [DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |New |Query push\- and pull\-stream statistics for single or multiple streams. |
|* [DescribeLiveSourceTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata)<br><br>* [DescribeLiveSourceBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcebandwidthdata) |New |Query origin\-pull traffic and bandwidth, which is the traffic from the origin servers to the edge servers, for single or multiple streams. |
|[DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) |New |Query the number and percentage of pull\-stream requests that receive a certain status code. |
|* CreateDomain<br><br>* DescribeDomain<br><br>* ListDomainDetail |Updated |Additional values are now supported by the `Region` parameter. |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |Updated |* A new field, `URLExpire`, is added to the response.<br><br>* The `TTL` parameter is now deprecated. |
|[DescribeLiveP95PeakBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata) |Updated |You can now query the bandwidth data for specified domain names, streaming protocols, and regions. |
|DescribeTranscodeData |Updated |Adds a `TranscodeType` field in the response, returning the target codec and encoding mode of the transcoding tasks. |
|* [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata)<br><br>* [DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata)<br><br>* DescribeRecordData<br><br>* DescribePullToPushBandwidthData<br><br>* [DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata)<br><br>* [DescribeLiveMetricTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivemetrictrafficdata)<br><br>* [DescribeLiveMetricBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata) |Updated |Query span and range are extended. With a time granularity of 300 seconds, you can query the data for the past 93 days and set a time range of up to 31 days. |
|* DescribeLiveDomainLog<br><br>* DescribeLivePullToPushLog |Updated |The download links for log files are now extended to seven days, at which point they expire. |
|Usage query APIs and Statistics and analysis APIs |Updated |The [region map](https://docs.byteplus.com/en/byteplus-media-live/docs/region-map) supports additional regions and countries. |
|[ListStorageSpaceDetail](https://docs.byteplus.com/en/byteplus-media-live/docs/liststoragespacedetail) |Updated |The `TTL` parameter is now deprecated. |
|DescribePlayResponseStatusStat |Deprecated |Use [DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) instead. |

## February 6, 2023

|**API** |**Type** |**Description** |**Document** |
|---|---|---|---|
|GeneratePushURL<br><br>GeneratePlayURL |New |* Generates the push stream addresses for a specified stream.<br><br>* Generates the pull stream addresses for a specified stream. |[GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023)<br><br>[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |

## November 29, 2022

This is the first release of the BytePlus MediaLive OpenAPI.
