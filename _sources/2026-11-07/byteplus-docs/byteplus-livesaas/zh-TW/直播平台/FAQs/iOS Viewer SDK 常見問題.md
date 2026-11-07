---
title: "iOS Viewer SDK 常見問題"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ios-viewer-sdk-chang-jian-wen-ti-zh-TW"
---

<span id="c980efcb"></span>
## 為什麼系統畫中畫（PiP）模式無法啟用？

<span id="f78b66b8"></span>
### 說明

觀眾在觀看直播、預覽或回放時，將應用程式切換至背景。但系統畫中畫未顯示。

<span id="35e4cc1c"></span>
### 可能原因與解決方法


* 觀眾的裝置運行的 iOS 版本低於 14.0。

   僅 iOS 14.0 及以上版本支援系統畫中畫。

* Viewer SDK 未啟用系統畫中畫。

   * 若需啟用直播的系統畫中畫，範例程式碼如下。

      ```objectivec
      BDLLiveEngine.sharedInstance.liveRoomConfiguration.playerConfig.common.enableLivePiP = YES;
      ```
      

   * 若需啟用預覽與回放的系統畫中畫，範例程式碼如下。

      ```objectivec
      BDLLiveEngine.sharedInstance.liveRoomConfiguration.playerConfig.common.enableVodPiP = YES;
      ```
      

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Viewer SDK 預設啟用系統畫中畫。如果你已修改預設設定，請參考上方的範例程式碼以重新啟用系統 PiP。   </div>
   

* 觀眾尚未在行動裝置上開啟 **自動啟用畫中畫** 開關。

   觀眾必須在行動裝置的 **設定** \> **一般** \> **畫中畫** 頁面開啟該開關。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef82b7c11e4e45158f5d03dabca3d40d~tplv-goo7wpa0wc-image.image) </span>


若問題仍然存在，請參考 [排查畫中畫失效、影片暫停及音訊問題](https://docs.byteplus.com/docs/byteplus-livesaas/ios-viewer-sdk-chang-jian-wen-ti-zh-TW#f6b3f91b) 中的可能原因與解決方法進行排查。

<span id="f6b3f91b"></span>
## 排查畫中畫失效、影片暫停及音訊問題

<span id="f943c493"></span>
### 說明

觀眾在觀看直播、預覽或回放時，將應用程式切換至背景，然後出現以下一項或多項問題：


* 系統畫中畫未顯示。

* 畫中畫模式下影片暫停。

* 直播間無聲或聲音不清楚。


<span id="d9d061e6"></span>
### 可能原因與解決方法

觀眾進入直播間後，Viewer SDK 會將 `AVAudioSession` 設為預設配置。使用預設配置時，SDK 的系統畫中畫通常不會導致這些問題。但若應用程式中其他音訊或視訊相關程式碼在觀眾進入直播間後修改了 `AVAudioSession` 的預設配置，則可能出現上述問題。

`AVAudioSession` 的預設配置如下：


* Category: AVAudioSessionCategoryPlayback

* Mode: AVAudioSessionModeMoviePlayback

* routeSharingPolicy: AVAudioSessionRouteSharingPolicyDefault

* options: 0


請移除任何修改 `AVAudioSession` 預設配置的程式碼。觀眾再次進入直播間時，SDK 會恢復 `AVAudioSession` 的預設配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若系統 PiP 未顯示，我們建議你先依據<a href="https://docs.byteplus.com/docs/byteplus-livesaas/ios-viewer-sdk-chang-jian-wen-ti-zh-TW#c980efcb">為什麼系統畫中畫（PiP）模式無法啟用？</a>中的可能原因與解決方案進行故障排除與處理。</div>


<span id="44a93306"></span>
## 為什麼觀眾無法使用應用程式的錄音功能？

<span id="cd0bbf1f"></span>
### 說明

觀眾進入直播間後，無法使用應用程式的錄音功能。

<span id="226f65da"></span>
### 可能原因與解決方法

觀眾進入直播間後，Viewer SDK 會將 `AVAudioSession` 設為預設配置。

`AVAudioSession` 的預設配置如下：


* Category: AVAudioSessionCategoryPlayback

* Mode: AVAudioSessionModeMoviePlayback

* routeSharingPolicy: AVAudioSessionRouteSharingPolicyDefault

* options: 0


若需讓觀眾使用需麥克風的功能（如錄音），請將 `AVAudioSessionCategoryPlayback` 改為 `AVAudioSessionCategoryPlayAndRecord`，並將 `AVAudioSessionModeMoviePlayback` 改為 `AVAudioSessionModeVideoChat`。

範例程式碼如下。

```objectivec
NSError *error = nil;
[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayAndRecord
                                        mode:AVAudioSessionModeVideoChat
                          routeSharingPolicy:AVAudioSessionRouteSharingPolicyDefault
                                     options:0
                                       error:&error];
[[AVAudioSession sharedInstance] setActive:YES error:&error];
```


觀眾完成需麥克風的功能（如錄音）後，可將 `AVAudioSession` 改回預設配置。

範例程式碼如下。

```objectivec
NSError *error = nil;
[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback
                                        mode:AVAudioSessionModeMoviePlayback
                          routeSharingPolicy:AVAudioSessionRouteSharingPolicyDefault
                                     options:0
                                       error:&error];
[[AVAudioSession sharedInstance] setActive:YES error:&error];
```


<span id="4a47ac15"></span>
## 為什麼觀眾能正常觀看預覽與回放，但無法載入直播內容？

請確認初始化 TTSDK 時傳入的 Bundle ID（用於申請授權）與 app ID（申請成功後返回）與專案設定值一致。同時，請確認初始化 TTSDK 時傳入的 Bundle ID 與專案設定的 Bundle ID 一致。否則，驗證將失敗。
