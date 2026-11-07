---
title: "OpenAPI 更新日志"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1-zh-CN"
---

## 2026\-10

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |2026\-10\-21 |新增请求参数 `Callback` 和 `Sei`。`Callback` 用于指定接收 AI 配音回调消息的 URL。`Sei` 用于指定是否将字幕写入直播流中的 SEI 消息。 |AI 配音 |
|更新 [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) ||新增请求参数 `SIOutput`，其中包含 `Callback` 和 `Sei`。`Callback` 用于指定接收 AI 配音回调消息的 URL。`Sei` 用于指定是否将字幕写入直播流中的 SEI 消息。 |字幕配置 |
|更新 [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) ||||
|更新 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) ||新增响应参数 `SIOutput`，其中包含 `Callback` 和 `Sei`。`Callback` 返回用于接收 AI 配音回调消息的 URL。`Sei` 返回直播流中的字幕是否已写入 SEI 消息。 ||
|更新 [DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) ||||

## 2026\-09

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [CreateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023) |2026\-09\-07 |* 新增请求参数 `TransSuffixs`，用于指定水印配置生效的转码流或 ABR 子流后缀。<br><br>* 仅当 `WatermarkMode` 设置为 `static` 时，请求参数 `PosX` 和 `PosY` 才为必填。<br><br>* 新增请求参数 `WatermarkMode`，用于指定水印类型。<br><br>* 新增请求参数 `DynamicMode` 和 `DynamicSpeedLevel`，用于配置动态水印。 |水印 |
|更新 [UpdateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023) ||* 新增请求参数 `TransSuffixs`，用于指定水印配置生效的转码流或 ABR 子流后缀。<br><br>* 新增请求参数 `WatermarkMode`，用于指定水印类型。<br><br>* 新增请求参数 `DynamicMode` 和 `DynamicSpeedLevel`，用于配置动态水印。<br><br>* 更新了可选请求参数的处理方式。更多信息，请参见[使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023?lang=en#usage-scenario)。 ||
|更新 [ListWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023) ||* 新增响应参数 `WatermarkMode`，用于获取水印类型。<br><br>* 新增响应参数 `TransSuffixs`，用于获取水印配置生效的转码流或 ABR 子流后缀。<br><br>* 新增响应参数 `DynamicMode` 和 `DynamicSpeedLevel`，用于获取动态水印配置。 ||
|更新 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) ||||

## 2026\-08

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) |2026\-08\-13 |新增请求参数 `PullRequestHeaders`，用于在中继任务从直播源或点播源拉取内容时，配置拉流请求中包含的 HTTP 请求头。支持的请求头为 `Referer` 和 `UserAgent`。 |拉流转推 |

## 2026\-07

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |2026\-07\-22 |将 `udp_websdk` 新增为 `Protocol` 响应参数的取值，以支持为 BytePlus MediaLive Player SDK for Web 生成 RTM 拉流地址。 |拉流地址 |

## 2026\-06

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |2026\-06\-25 |新增请求参数 `IsRtmAbr`，并为 `Type` 参数新增取值 `rtm-abr`，以支持创建 ABR 配置时使用 RTM\-ABR 协议类型。 |ABR 配置 |
|更新 [DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023) ||为 `Type` 参数新增取值 `rtm-abr`，以支持删除 RTM\-ABR 协议类型的 ABR 配置。 ||

## 2026\-04

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|新增 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |2026\-04\-21 |新增 AI 配音任务 API，包括创建、更新、重启、删除、查询和搜索任务。 |AI 配音 |
|新增 [UpdateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask) ||||
|新增 [RestartSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask) ||||
|新增 [DeleteSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask) ||||
|新增 [GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) ||||
|新增 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) ||||
|新增 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) ||新增用于获取当前账号可用 AI 配音配置的 API。 ||
|更新 [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) ||字幕配置 API 新增支持 AI 配音模式，包括创建、更新、列出和查询字幕配置详情。 ||
|更新 [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) ||||
|更新 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) ||||
|更新 [DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) ||||
|新增 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) ||新增用于获取当前账号在字幕配置的 AI 配音模式下可用字体和语言的 API。 ||

## 2025\-12

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2025\-12\-22 |新增请求参数 `VodRegion`，用于配置 VOD 区域。 |录制 |
|更新 [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) ||||
|更新 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) ||新增响应参数 `VodRegion`，用于获取 VOD 区域。 ||

## 2025\-10

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|更新 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |2025\-10\-14 |新增响应参数 `AuthType`，用于获取生成推流或拉流地址的 URL 鉴权类型。 |URL 鉴权 |
|更新 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) ||||
|更新 [DescribeAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023) ||新增响应参数 `AuthType`，用于获取 URL 鉴权类型。 ||
|更新 [UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) ||* 新增请求参数 `TimeStampBase`，用于设置时间戳的时间格式。<br><br>* 新增请求参数 `AuthType`，用于设置 URL 鉴权类型。 ||

## 2025\-09

|API |发布时间 |变更记录 |相关功能 |
|---|---|---|---|
|新增 [DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |2025\-09\-15 |支持获取指定时间范围内指定拉流域名下全部或指定回源拉流的监控数据，例如音视频帧率和码率。您可以使用监控数据评估回源拉流的健康状况。 |数据统计 |
|新增 [DescribeLiveStreamCountData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata) ||支持获取指定时间范围内指定推流、回源拉流或转码流的峰值数量。 ||
|新增 [CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) ||使用此 API 替代 `CreateSnapshotPreset`，用于新增截图配置。 |截图配置 |
|新增 [UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) ||使用此 API 替代 `UpdateSnapshotPreset`，用于更新截图配置。 ||
|新增 [ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) ||使用此 API 替代 `ListVhostSnapshotPreset`，用于获取截图配置信息。 ||

## 2025 年 5 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|新增 [UpdateRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023) |2025\-05\-29 |新增远程鉴权 API，用于配置、查询、删除和列出直播推流鉴权设置。 |远程鉴权 |
|新增 [DescribeRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023) ||||
|新增 [DeleteRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteremoteauth-2023) ||||
|新增 [ListVhostRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostremoteauth-2023) ||||

## 2025 年 4 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|新增 [CreateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask) |2025\-04\-14 |新增直播循环播放 API，支持动态内容更新、播放顺序配置、跳过片头和即时切换。 |循环播放列表配置 |
|新增 [DeleteCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask) ||||
|新增 [UpdateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask) ||||
|新增 [GetCarouselDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail) ||||
|新增 [ListCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask) ||||
|新增 [DescribeLiveCallbackData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata) ||新增用于查询直播推流相关回调记录的 API。该 API 提供事件类型、状态、请求和响应数据，用于诊断异常回调并验证回调送达情况。 |回调 |

## 2025 年 2 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|更新 [DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata) |2025\-02\-05 |1. 已从 API 请求中移除 `RefererList` 参数及关联取值，简化查询流程。<br><br>2. 新增 `HitRate` 和 `TotalHitRate` 参数，用于提供更详细的边缘请求命中率洞察。 |统计与分析 |

## 2025 年 1 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2025\-01\-22 |将请求参数 `SliceDuration` 的取值范围从 [5,30] 调整为 [2,100]。 |录制配置 |

## 2024 年 12 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|新增 [CreateLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivepadpreset-2023) |2024\-12\-20 |新增用于管理备用流配置和备用流管理的相关 API。 |备用流 |
|新增 [DescribeLivePadPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivepadpresetdetail-2023) ||||
|新增 [UpdateLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatelivepadpreset-2023) ||||
|新增 [DeleteLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivepadpreset-2023) ||||
|新增 [DescribeLivePadStreamList](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivepadstreamlist-2023) ||||
|新增 [StopLivePadStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoplivepadstream-2023) ||||
|新增 [DescribeLiveTopPlayData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023) |2024\-12\-09 |新增用于查询 TOPN 直播流或域名流量和带宽信息的接口。 |统计与分析 |

## 2024 年 10 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|更新 [回调说明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description) |2024\-10\-16 |已在拉流转推的回调消息中新增 PlayProgress 字段，用于返回点播（VOD）文件的播放时长（秒）。仅当拉流源为点播文件（Type=1）时返回此字段。<br><br>**变更影响**<br><br><br>* **适用场景**：如果您拉取点播源进行推流，此字段可更准确地跟踪播放进度。它适用于需要进度同步的场景，例如广告插入和内容切换。<br><br>* **不受影响的场景**：如果您拉取直播流源进行推流，则此变更不影响您。 |回调 |
|更新 [回调说明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description) |2024\-10\-11 |为支持录制更大文件，并避免文件过大导致的数据溢出问题，录制回调消息中表示录制文件大小的 size 字段类型已从 Integer 更新为 Long。这提高了处理大文件时的稳定性和准确性。 |回调 |

## 2024 年 9 月

|API |发布日期 |描述 |相关功能 |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2024\-09\-18 |支持为转码流创建录制配置。支持将录制文件存储到 BytePlus TOS。 |录制 |
|更新 [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) ||||
|更新 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) ||||
|更新 [DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) ||||
|更新 CreateSnapshotPreset ||支持将截图文件存储到 BytePlus TOS。 |截图 |
|更新 UpdateSnapshotPreset ||||
|更新 ListVhostSnapshotPreset ||||
|更新 [DescribeCDNSnapshotHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023) ||||
|更新 [CreateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023) ||时移文件存储支持 BytePlus TOS。 |时移 |
|更新 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) ||||
|更新 [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) ||支持设置点播视频的循环播放次数。支持为转推输出视频添加水印。 |拉流转推 |
|更新 [UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) ||||

## 2024 年 8 月 02 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023)<br><br>* [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023)<br><br>* [RestartPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-restartpulltopushtask-2023)<br><br>* [StopPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppulltopushtask-2023)<br><br>* [DeletePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushtask-2023)<br><br>* [UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) |更新 |新增、更新、删除、查询、启用和禁用 Group 参数，用于在 BytePlus 中创建、更新、删除、查询、启用和禁用拉流转推接口。 |
|* [ListPullToPushTaskV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023)<br><br>* [CreatePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023)<br><br>* [DeletePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushgroup-2023) |新增 |为查询拉流转推任务列表，新增支持 POST 方法的接口。<br><br>支持创建、更新和删除拉流转推任务组。 |
|* [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023)<br><br>* [DeleteSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023)<br><br>* [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023)<br><br>* [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) |新增 |支持创建字幕配置，为指定转码流添加字幕，并支持字幕翻译。 |

## 2024 年 7 月 19 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [UpdateEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencrypthls)<br><br>* [DescribeEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls)<br><br>* [GetHLSEncryptDataKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-gethlsencryptdatakey) |新增 |支持配置 HLS 加密所需的密钥获取地址。 |
|* [BindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1)<br><br>* [ListBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4) |更新 |支持新增 HLS 标准加密配置。 |

## 2024 年 6 月 30 日

|**API** |**类型** |**描述** |
|---|---|---|
|[CreateDomainV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn) |更新 |支持为每个域名配置加速区域。 |
|* [UpdateRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateregionaccessrule)<br><br>* [DescribeRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeregionaccessrule) |更新 |支持省级区域限制配置。 |

## 2024 年 4 月 16 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [UpdateHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig)<br><br>* [DescribeHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig)<br><br>* [DeleteHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig) |新增 |更新、查询和删除 HLS 配置。 |
|* [UpdateCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig)<br><br>* [DescribeCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig)<br><br>* [DeleteCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletecmafconfig) |新增 |更新、查询和删除 DASH 配置。 |
|* [UpdateLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig)<br><br>* [DescribeLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig)<br><br>* [DeleteLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletelatencyconfig) |新增 |更新、查询和删除延迟配置。 |

## 2024 年 4 月 8 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)<br><br>* [DescribeLiveStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023) |更新 |作为 IAM 用户，您现在可以创建转码模板并检索指定直播流的信息。 |

## 2024 年 3 月 18 日

|**API** |**类型** |**描述** |
|---|---|---|
|[DescribeLiveLogData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |新增 |检索拉流播放、推流、回源和推流播放的日志文件信息。 |
|* [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023)<br><br>* [DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023?lang=en) |新增 |批量配置自适应码率转码模板。 |
|* [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)<br><br>* [UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1) |更新 |现在可以查询和更新自适应码率转码模板。 |
|[DescribeLivePushStreamInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |新增 |查询已结束推流的信息。 |

## 2024 年 3 月 14 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [EnableHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-enablehttpheaderconfig)<br><br>* [DeleteHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-deletehttpheaderconfig)<br><br>* [DescribeHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-describehttpheaderconfig)<br><br>* [UpdateHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-updatehttpheaderconfig) |新增 |配置回源任务期间发送到第三方源站的请求，以及从边缘服务器发送到客户端的响应中的附加 HTTP 头。 |

## 2024 年 3 月 07 日

|**API** |**类型** |**描述** |
|---|---|---|
|[DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata?lang=en) |更新 |现在可以查询边缘服务器的缓存命中率。 |

## 2024 年 3 月 06 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [DescribeRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-dakt2mfojk)<br><br>* [DeleteRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-3nf0nln2b2)<br><br>* [UpdateRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-updaterelaysourcerewrite) |新增 |配置点播回源任务的源地址重写规则。 |

## 2024 年 2 月 07 日

|**API** |**类型** |**描述** |
|---|---|---|
|[ListCertV2](https://docs.byteplus.com/docs/byteplus-media-live/docs-listcertv2) |新增 |查询您账号下的 SSL 证书。 |

## 2024 年 1 月 25 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm)<br><br>* [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm)<br><br>* [UpdateEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateencryptdrm)<br><br>* [DescribeEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_2)<br><br>* [BindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_1)<br><br>* [UnBindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_3)<br><br>* [ListBindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_4) |新增 |为您的直播流实现数字版权管理（DRM）加密。 |
|* [UpdateIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateipaccessrule)<br><br>* [DescribeIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule)<br><br>* [DeleteIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteipaccessrule) |新增 |配置 IP 黑名单或白名单，以限制对您域名的访问。 |
|* [UpdateRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateregionaccessrule)<br><br>* [DescribeRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeregionaccessrule)<br><br>* [DeleteRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteregionaccessrule) |新增 |限制来自特定地理区域的请求。 |
|* [UpdateFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateformataccessrule)<br><br>* [DescribeFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeformataccessrule)<br><br>* [DeleteFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteformataccessrule) |新增 |限制特定协议的直播流拉流请求。 |

## 2024 年 1 月 11 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [DescribeUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeuseragentaccessrule)<br><br>* [DeleteUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1)<br><br>* [UpdateUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateuseragentaccessrule) |新增 |管理 User\-Agent（UA）黑名单或白名单。 |

## 2023 年 10 月 31 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [CreateDomainV2](https://docs.byteplus.com/docs/byteplus-media-live/docs-dj3h3u96xn) |新增 |创建一个或多个用于推流或拉流的域名。 |
|* [UpdateDomainVhost](https://docs.byteplus.com/docs/byteplus-media-live/docs-updatedomainvhost) |新增 |更改与域名关联的域名空间。 |
|* [UpdateClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateclusterratelimit)<br><br>* [DeleteClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteclusterratelimit)<br><br>* [DescribeClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeclusterratelimit) |新增 |管理拉流请求的频率限制。 |
|* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en) |新增 |管理定时回源任务。 |

## 2023 年 7 月 28 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en)<br><br>* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |新增 |创建、更新和查询回源任务。 |
|* UpdateRelaySourceV2<br><br>* DeleteRelaySourceV2<br><br>* DescribeRelaySourceV2 |已删除 |请改用以下端点：<br><br><br>* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en)<br><br>* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |

## 2023 年 7 月 6 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)<br><br>* [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023)<br><br>* [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |新增 |创建、更新和查询录制模板。现在可以使用 BytePlus VOD 存储录制内容。 |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |更新 |* 现在可以查询存储在 BytePlus VOD 中的录制内容。 |
|* [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)<br><br>* [UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1)<br><br>* [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)<br><br>* [ListCommonTransPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023) |更新 |* 已扩展多个参数的取值范围。<br><br>* 新增参数 `Roi`。该参数用于确定是否使用低码率高清模式进行转码。 |
|* [UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023)<br><br>* [DescribeCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023) |更新 |* 现在，您可以为回调设置密钥，从而对 BytePlus MediaLive 发送的回调进行鉴权。<br><br>* 此外，[回调消息](https://docs.byteplus.com/en/byteplus-media-live/docs/callback-description)新增字段。 |
|* CreateRecordPreset<br><br>* ListVhostRecordPreset<br><br>* UpdateRecordPreset |已弃用 |请改用以下端点：<br><br><br>* [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)<br><br>* [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023)<br><br>* [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |

## 2023 年 6 月 6 日

|**API** |**类型** |**描述** |
|---|---|---|
|* [DescribeLiveBatchPushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023)<br><br>* [DescribeLiveSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics)<br><br>* [DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |新增 |查询单个或多个流的推流和拉流统计数据。 |
|* [DescribeLiveSourceTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata)<br><br>* [DescribeLiveSourceBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcebandwidthdata) |新增 |查询单个或多个流的回源拉流流量和带宽，即从源站到边缘服务器的流量。 |
|[DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) |新增 |查询收到特定状态码的拉流请求数量和占比。 |
|* CreateDomain<br><br>* DescribeDomain<br><br>* ListDomainDetail |更新 |`Region` 参数现在支持更多取值。 |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |更新 |* 响应中新增字段 `URLExpire`。<br><br>* `TTL` 参数现已弃用。 |
|[DescribeLiveP95PeakBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata) |更新 |现在可以查询指定域名、流媒体协议和区域的带宽数据。 |
|DescribeTranscodeData |更新 |响应中新增 `TranscodeType` 字段，返回转码任务的目标编码器和编码模式。 |
|* [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata)<br><br>* [DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata)<br><br>* DescribeRecordData<br><br>* DescribePullToPushBandwidthData<br><br>* [DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata)<br><br>* [DescribeLiveMetricTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivemetrictrafficdata)<br><br>* [DescribeLiveMetricBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata) |更新 |查询跨度和范围已扩展。在 300 秒时间粒度下，您可以查询过去 93 天的数据，并设置最长 31 天的时间范围。 |
|* DescribeLiveDomainLog<br><br>* DescribeLivePullToPushLog |更新 |日志文件的下载链接现在延长至七天，之后过期。 |
|用量查询 API 和统计与分析 API |更新 |[区域映射](https://docs.byteplus.com/en/byteplus-media-live/docs/region-map)支持更多区域和国家。 |
|[ListStorageSpaceDetail](https://docs.byteplus.com/en/byteplus-media-live/docs/liststoragespacedetail) |更新 |`TTL` 参数现已弃用。 |
|DescribePlayResponseStatusStat |已弃用 |请改用 [DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata)。 |

## 2023 年 2 月 6 日

|**API** |**类型** |**描述** |**文档** |
|---|---|---|---|
|GeneratePushURL<br><br>GeneratePlayURL |新增 |* 为指定流生成推流地址。<br><br>* 为指定流生成拉流地址。 |[GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023)<br><br>[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |

## 2022 年 11 月 29 日

这是 BytePlus MediaLive OpenAPI 的首次发布。
