---
title: "客戶端 SDK 元件"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination-zh-TW"
---

本文件提供了每個 VideoOne 演示應用版本整合的 SDK 的全面列表。按照本文所述的版本組合進行整合，可以確保整合過程順利，避免因整合不同 BytePlus SDK 而產生的依賴衝突或相容性問題。

<span id="ver-550"></span>
## 版本 5.5.0

<span id="ver-550-ios"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDKFramework |1.50.200.2\-premium |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推流 |依賴項：TTVideoEditor |
|||RTCSDK |實時互動 |無 |
|||ByteAudio |音訊處理 |與 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|MediaAdsToB |2.0.1 |無 |MiniDrama 中的 CSAI |google\-ima\-sdk 與 BytePlus 點播的介面卡 |


<span id="ver-550-android"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_premium |1.50.300.1 |流媒體拉流 |依賴項：commons\-net, okhttp |
|com.bytedanceapi |ttsdk\-player_premium |1.50.300.1 |點播播放 |依賴項：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.50.300.1 |點播上傳 |依賴項：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttabr |1.50.300.1 |ABR 設定 |無 |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.50.300.1 |無 |基礎元件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.50.300.1 |無 |基礎元件 |
|com.bytedance.rtc |BytePlusRTC |3.60.103.5700 |實時互動 |無 |
|com.google.android.gms |play\-services\-cast\-framework |21.5.0 |投屏（Chromecast） |無 |
|androidx.mediarouter |mediarouter |1.8.1 |投屏（Chromecast） |無 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |流媒體拉流 |基礎元件 |


<span id="63c26919"></span>
## 版本 5.3.0\-5.4.0

<span id="3f601fb4"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDKFramework |1.48.200.2\-premium |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推流 |依賴項：TTVideoEditor |
|||RTCSDK |實時互動 |無 |
|||ByteAudio |音訊處理 |與 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|effect\-sdk |4.4.3_standard |無 |影片特效，如美顏 AR 和濾鏡 |無 |
|TTVideoEditor |11.8.1.83\-D |無 |影片拍攝 |無 |
|TTNetworkManager |4.2.210.20 |無 |網路 |基礎元件 |
|MediaAdsToB |2.0.1 |無 |MiniDrama 中的 CSAI |google\-ima\-sdk 與 BytePlus 點播的介面卡 |


<span id="71c14aa8"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_premium |1.49.300.4 |流媒體拉流 |依賴項：commons\-net, okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush |1.49.300.4 |流媒體推流及實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-ttabr |1.49.300.4 |ABR 設定 | |
|com.bytedanceapi |ttsdk\-player_premium |1.49.300.4 |點播播放 |依賴項：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.49.300.4 |點播上傳 |依賴項：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.49.300.4 |無 |基礎元件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.49.300.4 |無 |基礎元件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |
|com.byteplus |BytePlusRTC |3.58.1.53300 |* RTM 拉流<br><br>* 互動直播<br><br>* 合唱<br><br>* 媒體上下滑動 |無 |
|com.bytedance |effectsdk |cv_tob4.7.3_202510271120_2e88395de69 |影片特效，如美顏 AR 和濾鏡 |無 |
|com.byteplus.mediaplus |mediaads |2.0.0 |MiniDrama 中的 CSAI |google\-ima\-sdk 與 BytePlus 點播的介面卡 |


<span id="8f4819ba"></span>
## 版本 5.2.0

<span id="2b6f0af1"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDKFramework |1.43.300.2\-premium |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推流 |依賴項：TTVideoEditor |
|||RTCSDK |實時互動 |無 |
|||ByteAudio |音訊處理 |與 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|effect\-sdk |4.4.3_standard |無 |影片特效，如美顏 AR 和濾鏡 |無 |
|TTVideoEditor |11.8.1.83\-D |無 |影片拍攝 |無 |
|TTNetworkManager |4.1.127.43 |無 |網路 |基礎元件 |


<span id="ea5c0536"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_rtc |1.43.300.3 |流媒體拉流 |依賴項：commons\-net, okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.43.300.3 |流媒體推流及實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-player_premium |1.43.300.3 |點播播放 |依賴項：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.43.300.3 |點播上傳 |依賴項：RangersAppLog\-Lite\-global, okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.43.300.3 |無 |基礎元件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.43.300.3 |無 |基礎元件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |
|com.byteplus |BytePlusRTC |3.58.1.20600 |* RTM 拉流<br><br>* 互動直播<br><br>* KTV<br><br>* 合唱<br><br>* 媒體上下滑動 |無 |


<span id="6e444905"></span>
## 版本 4.0.0–5.0.0

<span id="fa3c6705"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDK |1.43.300.2\-premium |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推流 |依賴項：TTVideoEditor |
|||RTCSDK |實時音影片互動 |無 |
|||ByteAudio |音訊處理 |與 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|effect\-sdk |4.4.3_standard |無 |影片特效，如美顏 AR 和濾鏡 |無 |


<span id="18ab577d"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull_rtc |1.43.300.3 |流媒體拉流 |依賴項：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.43.300.3 |流媒體推送與實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-player_premium |1.43.300.3 |點播播放 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.43.300.3 |點播上傳 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.43.300.3 |無 |基礎元件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.43.300.3 |無 |基礎元件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |
|com.byteplus |BytePlusRTC |3.58.1.20600 |* RTM 流媒體拉流<br><br>* 互動直播<br><br>* KTV<br><br>* 合唱<br><br>* 媒體上下滑動 | |


<span id="56378140"></span>
## 版本 3.3.0

<span id="4beaf1a4"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDK |1.41.300.203\-rtc |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推送 |依賴項：TTVideoEditor |
|||RTC\-Framework |實時音影片互動 |無 |
|||ByteAudio |音訊處理 |與 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|effect\-sdk |4.4.3_standard |無 |影片特效，如美顏 AR 與濾鏡 |無 |
|TTVideoEditor |11.8.1.83\-D |無 |影片拍攝 |無 |
|TTNetworkManager |5.0.29.2\-adu |無 |無 |基礎元件 |


<span id="2f4848de"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.41.300.201\-rtc |流媒體拉流 |依賴項：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.41.300.201\-rtc |流媒體推送與實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-player_premium |1.41.300.201\-rtc |點播播放 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.41.300.201\-rtc |點播上傳 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttlicense2 |1.41.300.201\-rtc |無 |基礎元件 |
|com.bytedanceapi |ttsdk\-ttcommon |1.41.300.201\-rtc |無 |基礎元件 |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |4.12.0 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |


<span id="b23a5d05"></span>
## 版本 3.0.0–3.1.0

<span id="a67e6b8c"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDK |1.40.200.5\-premium |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推送 |無 |
|||RTC\-Framework |實時音影片互動 |無 |
|||ByteAudio |音訊處理 |與 RTC\-Framework 或 LivePull\-RTS 等 SDK 配合使用 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|EffectSDK_iOS_TOB |11.6.0\-VE\-LENS |無 |影片特效，如美顏 AR 與濾鏡 |無 |
|TTVideoEditor |11.8.3.1\-VE |無 |影片拍攝與編輯 |依賴項：<br><br><br>* EffectSDK_iOS_TOB<br><br>* DVEInject<br><br>* AudioSdkTob<br><br>* NLEPlatform |
|NLEPlatform |0.5.7 |無 |無 |基礎元件 |
|DVEInject |0.0.5 |無 |無 |基礎元件 |
|AudioSdkTob |5.0.7\-alpha.1\-tobonekit |無 |音訊特效 |基礎元件 |
|TTNetworkManager |5.0.29.2\-adu |無 |無 |基礎元件 |


<span id="adc5b4d0"></span>
### Android


|**Group ID** |**Artifact ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.39.100.9.onekit |流媒體拉流 |依賴項：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.39.100.9.onekit |流媒體推送與實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-player_premium |1.39.100.9.onekit |點播播放 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.39.100.9.onekit |點播上傳 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |3.14.9 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |
|com.bytedance.ugc.framework.libs |vesdk |11.8.2.15\-vevos\-tob |影片拍攝與編輯 |依賴項：<br><br><br>* ck\-base<br><br>* effectsdk<br><br>* NLEMediaPublic<br><br>* NLERecorderJava<br><br>* NLETemplateModel<br><br>* NLEEditor<br><br>* NLEProcessor |
|com.bytedance |effectsdk |202305061135_1_202305061135_870eed96abe |影片特效，如美顏 AR 與濾鏡 |無 |
|com.volcengine.ckbase |ck\-base |1.0.0 |無 |基礎元件 |
|com.volcengine.ck.nle |NLEMediaPublic |4.0.2 |無 |基礎元件 |
||NLERecorderJava |4.0.2 |無 |基礎元件 |
||NLETemplateModel |4.0.2 |無 |基礎元件 |
||NLEEditor |4.0.2 |無 |基礎元件 |
||NLEProcessor |4.0.2 |無 |基礎元件 |


<span id="fb67de67"></span>
## 版本 2.4.0

<span id="9b0ebffb"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDK |1.40.200.5\-premium |LivePull\-RTS |流媒體拉流 |無 |
|||LivePush\-RTS |流媒體推送 |無 |
|||RTC\-Framework |實時音影片互動 |無 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|EffectSDK_iOS_TOB |11.6.0\-VE\-LENS |無 |影片特效，如美顏 AR 與濾鏡 |無 |
|TTVideoEditor |11.8.3.1\-VE |無 |影片拍攝與編輯 |依賴項：<br><br><br>* EffectSDK_iOS_TOB<br><br>* DVEInject<br><br>* AudioSdkTob<br><br>* NLEPlatform |
|NLEPlatform |0.5.7 |無 |無 |基礎元件 |
|DVEInject |0.0.5 |無 |無 |基礎元件 |
|AudioSdkTob |5.0.7\-alpha.1\-tobonekit |無 |音訊特效 |基礎元件 |
|TTNetworkManager |5.0.29.2\-adu |無 |無 |基礎元件 |


<span id="20819a22"></span>
### Android


|**組 ID** |**構件 ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.39.100.9.onekit |流拉取 |依賴項：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.39.100.9.onekit |流推送及實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-player_premium |1.39.100.9.onekit |點播播放 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.39.100.9.onekit |點播上傳 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |3.14.9 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |
|com.bytedance.ugc.framework.libs |vesdk |11.8.2.15\-vevos\-tob |影片拍攝與編輯 |依賴項：<br><br><br>* ck\-base<br><br>* effectsdk<br><br>* NLEMediaPublic<br><br>* NLERecorderJava<br><br>* NLETemplateModel<br><br>* NLEEditor<br><br>* NLEProcessor |
|com.bytedance |effectsdk |202305061135_1_202305061135_870eed96abe |影片特效，如美顏 AR 及濾鏡 |無 |
|com.volcengine.ckbase |ck\-base |1.0.0 |無 |基礎元件 |
|com.volcengine.ck.nle |NLEMediaPublic |4.0.2 |無 |基礎元件 |
||NLERecorderJava |4.0.2 |無 |基礎元件 |
||NLETemplateModel |4.0.2 |無 |基礎元件 |
||NLEEditor |4.0.2 |無 |基礎元件 |
||NLEProcessor |4.0.2 |無 |基礎元件 |


<span id="40a35537"></span>
## 版本 2.0.0~2.3.0

<span id="967275cf"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |**備註** |
|---|---|---|---|---|
|TTSDK |1.37.200.5\-premium |LivePull\-RTS |流拉取 |無 |
|||LivePush\-RTS |流推送 |無 |
|||RTC\-Framework |實時音影片互動 |無 |
|||Uploader |點播上傳 |無 |
|||Player |點播播放 |無 |
|EffectSDK_iOS_TOB |11.6.0\-VE\-LENS |無 |影片特效，如美顏 AR 及濾鏡 |無 |
|TTVideoEditor |11.8.3.1\-VE |無 |影片拍攝與編輯 |依賴項：<br><br><br>* EffectSDK_iOS_TOB<br><br>* DVEInject<br><br>* AudioSdkTob<br><br>* NLEPlatform |
|NLEPlatform |0.5.7 |無 |無 |基礎元件 |
|DVEInject |0.0.5 |無 |無 |基礎元件 |
|AudioSdkTob |5.0.7\-alpha.1\-tobonekit |無 |音訊特效 |基礎元件 |
|TTNetworkManager |5.0.29.2\-adu |無 |無 |基礎元件 |


<span id="12292d05"></span>
### Android


|**組 ID** |**構件 ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.37.200.6.onekit |流拉取 |依賴項：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.37.200.6.onekit |流推送及實時音影片互動 |無 |
|com.bytedanceapi |ttsdk\-player_premium |1.37.200.6.onekit |點播播放 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedanceapi |ttsdk\-ttuploader |1.37.200.6.onekit |點播上傳 |依賴項：RangersAppLog\-Lite\-global，okhttp |
|com.bytedance.applog |RangersAppLog\-Lite\-global |6.14.3 |無 |基礎元件 |
|com.squareup.okhttp3 |okhttp |3.14.9 |無 |基礎元件 |
|commons\-net |commons\-net |3.9.0 |無 |基礎元件 |
|com.bytedance.ugc.framework.libs |vesdk |11.8.2.15\-vevos\-tob |影片拍攝與編輯 |依賴項：<br><br><br>* ck\-base<br><br>* effectsdk<br><br>* NLEMediaPublic<br><br>* NLERecorderJava<br><br>* NLETemplateModel<br><br>* NLEEditor<br><br>* NLEProcessor |
|com.bytedance |effectsdk |202305061135_1_202305061135_870eed96abe |影片特效，如美顏 AR 及濾鏡 |無 |
|com.volcengine.ckbase |ck\-base |1.0.0 |無 |基礎元件 |
|com.volcengine.ck.nle |NLEMediaPublic |4.0.2 |無 |基礎元件 |
||NLERecorderJava |4.0.2 |無 |基礎元件 |
||NLETemplateModel |4.0.2 |無 |基礎元件 |
||NLEEditor |4.0.2 |無 |基礎元件 |
||NLEProcessor |4.0.2 |無 |基礎元件 |


<span id="a8115f0a"></span>
## 版本 1.0.0

<span id="17bffd48"></span>
### iOS


|**Pod** |**版本** |**子規格** |**相關功能** |
|---|---|---|---|
|TTSDK |1.37.200.5\-premium |LivePull\-RTS |流拉取 |
|||LivePush\-RTS |流推送 |
|||RTC\-Framework |實時音影片互動 |
|effect\-sdk |4.4.3_standard |無 |影片特效，如美顏 AR 及濾鏡。[請聯絡您的銷售代表](https://www.byteplus.com/en/contact)以獲取 BytePlus Effects SDK。 |


<span id="98eb3acc"></span>
### Android


|**組 ID** |**構件 ID** |**版本** |**相關功能** |**備註** |
|---|---|---|---|---|
|com.bytedanceapi |ttsdk\-ttlivepull |1.37.200.5 |流拉取 |依賴項：commons\-net，okhttp |
|com.bytedanceapi |ttsdk\-ttlivepush_rtc |1.37.200.5 |流推送及實時音影片互動 |無 |
|com.squareup.okhttp3 |okhttp |4.2.1 |無 |基礎元件 |
|commons\-net |commons\-net |3.6 |無 |基礎元件 |
|無 |effectsdk |4.3.2 |影片特效，如美顏 AR 及濾鏡 |[請聯絡您的銷售代表](https://www.byteplus.com/en/contact)以獲取 BytePlus Effects SDK。 |
