---
title: "客户端 SDK 组件"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination-zh-CN"
---

本文档提供了每个 VideoOne 演示应用版本集成的 SDK 的全面列表。按照本文所述的版本组合进行集成，可以确保集成过程顺利，避免因集成不同 BytePlus SDK 而产生的依赖冲突或兼容性问题。

<span id="ver-550"></span>
## 版本 5.5.0

<span id="ver-550-ios"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDKFramework |1.50.200.2\-premium |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推流 |依赖项：TTVideoEditor |
|||RTCSDK |实时互动 |无 |
|||ByteAudio |音频处理 |与 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|MediaAdsToB |2.0.1 |无 |MiniDrama 中的 CSAI |google\-ima\-sdk 与 BytePlus 点播的适配器 |


<span id="ver-550-android"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_premium |1.50.300.1 |流媒体拉流 |依赖项：commons\-net, okhttp |
|com.bytedanceapi |ttsdk\-player_premium |1.50.300.1 |点播播放 |依赖项：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.50.300.1 |点播上传 |依赖项：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttabr |1.50.300.1 |ABR 设置 |无 |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.50.300.1 |无 |基础组件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.50.300.1 |无 |基础组件 |
|com.bytedance.rtc |BytePlusRTC |3.60.103.5700 |实时互动 |无 |
|com.google.android.gms |play\-services\-cast\-framework |21.5.0 |投屏（Chromecast） |无 |
|androidx.mediarouter |mediarouter |1.8.1 |投屏（Chromecast） |无 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |流媒体拉流 |基础组件 |


<span id="63c26919"></span>
## 版本 5.3.0\-5.4.0

<span id="3f601fb4"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDKFramework |1.48.200.2\-premium |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推流 |依赖项：TTVideoEditor |
|||RTCSDK |实时互动 |无 |
|||ByteAudio |音频处理 |与 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|effect\-sdk |4.4.3_standard |无 |视频特效，如美颜 AR 和滤镜 |无 |
|TTVideoEditor |11.8.1.83\-D |无 |视频拍摄 |无 |
|TTNetworkManager |4.2.210.20 |无 |网络 |基础组件 |
|MediaAdsToB |2.0.1 |无 |MiniDrama 中的 CSAI |google\-ima\-sdk 与 BytePlus 点播的适配器 |


<span id="71c14aa8"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_premium |1.49.300.4 |流媒体拉流 |依赖项：commons\-net, okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush |1.49.300.4 |流媒体推流及实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-ttabr |1.49.300.4 |ABR 设置 | |
|com.bytedanceapi |ttsdk\-player_premium |1.49.300.4 |点播播放 |依赖项：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.49.300.4 |点播上传 |依赖项：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.49.300.4 |无 |基础组件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.49.300.4 |无 |基础组件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |
|com.byteplus |BytePlusRTC |3.58.1.53300 |* RTM 拉流<br><br>* 互动直播<br><br>* 合唱<br><br>* 媒体上下滑动 |无 |
|com.bytedance |effectsdk |cv_tob4.7.3_202510271120_2e88395de69 |视频特效，如美颜 AR 和滤镜 |无 |
|com.byteplus.mediaplus |mediaads |2.0.0 |MiniDrama 中的 CSAI |google\-ima\-sdk 与 BytePlus 点播的适配器 |


<span id="8f4819ba"></span>
## 版本 5.2.0

<span id="2b6f0af1"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDKFramework |1.43.300.2\-premium |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推流 |依赖项：TTVideoEditor |
|||RTCSDK |实时互动 |无 |
|||ByteAudio |音频处理 |与 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|effect\-sdk |4.4.3_standard |无 |视频特效，如美颜 AR 和滤镜 |无 |
|TTVideoEditor |11.8.1.83\-D |无 |视频拍摄 |无 |
|TTNetworkManager |4.1.127.43 |无 |网络 |基础组件 |


<span id="ea5c0536"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_rtc |1.43.300.3 |流媒体拉流 |依赖项：commons\-net, okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.43.300.3 |流媒体推流及实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-player_premium |1.43.300.3 |点播播放 |依赖项：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.43.300.3 |点播上传 |依赖项：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.43.300.3 |无 |基础组件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.43.300.3 |无 |基础组件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |
|com.byteplus |BytePlusRTC |3.58.1.20600 |* RTM 拉流<br><br>* 互动直播<br><br>* KTV<br><br>* 合唱<br><br>* 媒体上下滑动 |无 |


<span id="6e444905"></span>
## 版本 4.0.0–5.0.0

<span id="fa3c6705"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDK |1.43.300.2\-premium |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推流 |依赖项：TTVideoEditor |
|||RTCSDK |实时音视频互动 |无 |
|||ByteAudio |音频处理 |与 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|effect\-sdk |4.4.3_standard |无 |视频特效，如美颜 AR 和滤镜 |无 |


<span id="18ab577d"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_rtc |1.43.300.3 |流媒体拉流 |依赖项：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.43.300.3 |流媒体推送与实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-player_premium |1.43.300.3 |点播播放 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.43.300.3 |点播上传 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.43.300.3 |无 |基础组件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.43.300.3 |无 |基础组件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |
|com.byteplus |BytePlusRTC |3.58.1.20600 |* RTM 流媒体拉流<br><br>* 互动直播<br><br>* KTV<br><br>* 合唱<br><br>* 媒体上下滑动 | |


<span id="56378140"></span>
## 版本 3.3.0

<span id="4beaf1a4"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDK |1.41.300.203\-rtc |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推送 |依赖项：TTVideoEditor |
|||RTC\-Framework |实时音视频互动 |无 |
|||ByteAudio |音频处理 |与 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|effect\-sdk |4.4.3_standard |无 |视频特效，如美颜 AR 与滤镜 |无 |
|TTVideoEditor |11.8.1.83\-D |无 |视频拍摄 |无 |
|TTNetworkManager |5.0.29.2\-adu |无 |无 |基础组件 |


<span id="2f4848de"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.41.300.201\-rtc |流媒体拉流 |依赖项：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.41.300.201\-rtc |流媒体推送与实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-player_premium |1.41.300.201\-rtc |点播播放 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.41.300.201\-rtc |点播上传 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.41.300.201\-rtc |无 |基础组件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.41.300.201\-rtc |无 |基础组件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |


<span id="b23a5d05"></span>
## 版本 3.0.0–3.1.0

<span id="a67e6b8c"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDK |1.40.200.5\-premium |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推送 |无 |
|||RTC\-Framework |实时音视频互动 |无 |
|||ByteAudio |音频处理 |与 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|EffectSDK_iOS_TOB |11.6.0\-VE\-LENS |无 |视频特效，如美颜 AR 与滤镜 |无 |
|TTVideoEditor |11.8.3.1\-VE |无 |视频拍摄与编辑 |依赖项：<br><br><br>* EffectSDK_iOS_TOB<br><br>* DVEInject<br><br>* AudioSdkTob<br><br>* NLEPlatform |
|NLEPlatform |0.5.7 |无 |无 |基础组件 |
|DVEInject |0.0.5 |无 |无 |基础组件 |
|AudioSdkTob |5.0.7\-alpha.1\-tobonekit |无 |音频特效 |基础组件 |
|TTNetworkManager |5.0.29.2\-adu |无 |无 |基础组件 |


<span id="adc5b4d0"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.39.100.9.onekit |流媒体拉流 |依赖项：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.39.100.9.onekit |流媒体推送与实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-player_premium |1.39.100.9.onekit |点播播放 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.39.100.9.onekit |点播上传 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |3.14.9 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |
|com.bytedance.ugc.framework.libs |vesdk |11.8.2.15\-vevos\-tob |视频拍摄与编辑 |依赖项：<br><br><br>* ck\-base<br><br>* effectsdk<br><br>* NLEMediaPublic<br><br>* NLERecorderJava<br><br>* NLETemplateModel<br><br>* NLEEditor<br><br>* NLEProcessor |
|com.bytedance |effectsdk |202305061135_1_202305061135_870eed96abe |视频特效，如美颜 AR 与滤镜 |无 |
|com.volcengine.ckbase |ck\-base |1.0.0 |无 |基础组件 |
|com.volcengine.ck.nle |NLEMediaPublic |4.0.2 |无 |基础组件 |
||NLERecorderJava |4.0.2 |无 |基础组件 |
||NLETemplateModel |4.0.2 |无 |基础组件 |
||NLEEditor |4.0.2 |无 |基础组件 |
||NLEProcessor |4.0.2 |无 |基础组件 |


<span id="fb67de67"></span>
## 版本 2.4.0

<span id="9b0ebffb"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDK |1.40.200.5\-premium |LivePull\-RTS |流媒体拉流 |无 |
|||LivePush\-RTS |流媒体推送 |无 |
|||RTC\-Framework |实时音视频互动 |无 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|EffectSDK_iOS_TOB |11.6.0\-VE\-LENS |无 |视频特效，如美颜 AR 与滤镜 |无 |
|TTVideoEditor |11.8.3.1\-VE |无 |视频拍摄与编辑 |依赖项：<br><br><br>* EffectSDK_iOS_TOB<br><br>* DVEInject<br><br>* AudioSdkTob<br><br>* NLEPlatform |
|NLEPlatform |0.5.7 |无 |无 |基础组件 |
|DVEInject |0.0.5 |无 |无 |基础组件 |
|AudioSdkTob |5.0.7\-alpha.1\-tobonekit |无 |音频特效 |基础组件 |
|TTNetworkManager |5.0.29.2\-adu |无 |无 |基础组件 |


<span id="20819a22"></span>
### Android


|**组 ID** |**构件 ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.39.100.9.onekit |流拉取 |依赖项：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.39.100.9.onekit |流推送及实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-player_premium |1.39.100.9.onekit |点播播放 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.39.100.9.onekit |点播上传 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |3.14.9 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |
|com.bytedance.ugc.framework.libs |vesdk |11.8.2.15\-vevos\-tob |视频拍摄与编辑 |依赖项：<br><br><br>* ck\-base<br><br>* effectsdk<br><br>* NLEMediaPublic<br><br>* NLERecorderJava<br><br>* NLETemplateModel<br><br>* NLEEditor<br><br>* NLEProcessor |
|com.bytedance |effectsdk |202305061135_1_202305061135_870eed96abe |视频特效，如美颜 AR 及滤镜 |无 |
|com.volcengine.ckbase |ck\-base |1.0.0 |无 |基础组件 |
|com.volcengine.ck.nle |NLEMediaPublic |4.0.2 |无 |基础组件 |
||NLERecorderJava |4.0.2 |无 |基础组件 |
||NLETemplateModel |4.0.2 |无 |基础组件 |
||NLEEditor |4.0.2 |无 |基础组件 |
||NLEProcessor |4.0.2 |无 |基础组件 |


<span id="40a35537"></span>
## 版本 2.0.0~2.3.0

<span id="967275cf"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |**备注** |
|---|---|---|---|---|
|TTSDK |1.37.200.5\-premium |LivePull\-RTS |流拉取 |无 |
|||LivePush\-RTS |流推送 |无 |
|||RTC\-Framework |实时音视频互动 |无 |
|||Uploader |点播上传 |无 |
|||Player |点播播放 |无 |
|EffectSDK_iOS_TOB |11.6.0\-VE\-LENS |无 |视频特效，如美颜 AR 及滤镜 |无 |
|TTVideoEditor |11.8.3.1\-VE |无 |视频拍摄与编辑 |依赖项：<br><br><br>* EffectSDK_iOS_TOB<br><br>* DVEInject<br><br>* AudioSdkTob<br><br>* NLEPlatform |
|NLEPlatform |0.5.7 |无 |无 |基础组件 |
|DVEInject |0.0.5 |无 |无 |基础组件 |
|AudioSdkTob |5.0.7\-alpha.1\-tobonekit |无 |音频特效 |基础组件 |
|TTNetworkManager |5.0.29.2\-adu |无 |无 |基础组件 |


<span id="12292d05"></span>
### Android


|**组 ID** |**构件 ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.37.200.6.onekit |流拉取 |依赖项：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.37.200.6.onekit |流推送及实时音视频互动 |无 |
|com.bytedanceapi |ttsdk\-player_premium |1.37.200.6.onekit |点播播放 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.37.200.6.onekit |点播上传 |依赖项：RangersAppLog\-Lite\-global，okhttp |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |无 |基础组件 |
|com.squareup.okhttp3 |okhttp |3.14.9 |无 |基础组件 |
|commons\-net |commons\-net |3.9.0 |无 |基础组件 |
|com.bytedance.ugc.framework.libs |vesdk |11.8.2.15\-vevos\-tob |视频拍摄与编辑 |依赖项：<br><br><br>* ck\-base<br><br>* effectsdk<br><br>* NLEMediaPublic<br><br>* NLERecorderJava<br><br>* NLETemplateModel<br><br>* NLEEditor<br><br>* NLEProcessor |
|com.bytedance |effectsdk |202305061135_1_202305061135_870eed96abe |视频特效，如美颜 AR 及滤镜 |无 |
|com.volcengine.ckbase |ck\-base |1.0.0 |无 |基础组件 |
|com.volcengine.ck.nle |NLEMediaPublic |4.0.2 |无 |基础组件 |
||NLERecorderJava |4.0.2 |无 |基础组件 |
||NLETemplateModel |4.0.2 |无 |基础组件 |
||NLEEditor |4.0.2 |无 |基础组件 |
||NLEProcessor |4.0.2 |无 |基础组件 |


<span id="a8115f0a"></span>
## 版本 1.0.0

<span id="17bffd48"></span>
### iOS


|**Pod** |**版本** |**子规格** |**相关功能** |
|---|---|---|---|
|TTSDK |1.37.200.5\-premium |LivePull\-RTS |流拉取 |
|||LivePush\-RTS |流推送 |
|||RTC\-Framework |实时音视频互动 |
|effect\-sdk |4.4.3_standard |无 |视频特效，如美颜 AR 及滤镜。[请联系您的销售代表](https://www.byteplus.com/en/contact)以获取 BytePlus Effects SDK。 |


<span id="98eb3acc"></span>
### Android


|**组 ID** |**构件 ID** |**版本** |**相关功能** |**备注** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.37.200.5 |流拉取 |依赖项：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.37.200.5 |流推送及实时音视频互动 |无 |
|com.squareup.okhttp3 |okhttp |4.2.1 |无 |基础组件 |
|commons\-net |commons\-net |3.6 |无 |基础组件 |
|无 |effectsdk |4.3.2 |视频特效，如美颜 AR 及滤镜 |[请联系您的销售代表](https://www.byteplus.com/en/contact)以获取 BytePlus Effects SDK。 |
