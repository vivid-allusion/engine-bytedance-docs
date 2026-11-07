---
title: "iOS 观播 SDK 常见问题"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-faqs-about-ios-viewer-sdk-zh-CN"
---

<span id="why-does-the-system-picture-in-picture-pip-mode-fail"></span>
## 为什么系统画中画（PiP）模式无法使用？

<span id="description"></span>
### 接口行为

观众在观看直播、预告或回放时，将应用切换到后台。但系统画中画未出现。

<span id="possible-reasons-and-solutions"></span>
### 可能原因与解决方案


* 观众的设备运行的 iOS 版本低于 14.0。

   仅 iOS 14.0 及以上版本支持系统画中画。

* iOS 观播 SDK 未开启系统画中画。

   * 如需为直播开启系统画中画，示例代码如下。

      ```objectivec
      BDLLiveEngine.sharedInstance.liveRoomConfiguration.playerConfig.common.enableLivePiP = YES;
      ```
      

   * 如需为预告和回放开启系统画中画，示例代码如下。

      ```objectivec
      BDLLiveEngine.sharedInstance.liveRoomConfiguration.playerConfig.common.enableVodPiP = YES;
      ```
      

   iOS 观播 SDK 默认已开启系统画中画。如你已修改默认配置，请参考上述示例代码重新开启系统画中画。

* 观众未在移动设备上打开**自动启动画中画**开关。

   观众需在移动设备的**设置** \> **通用** \> **画中画**页面打开该开关。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef82b7c11e4e45158f5d03dabca3d40d~tplv-goo7wpa0wc-image.image) </span>


<span id="troubleshooting-pip-failures-video-pauses-and-audio-issues"></span>
## 画中画异常、视频暂停及音频问题排查

<span id="description"></span>
### 接口行为

观众在观看直播、预告或回放时，将应用切换到后台，随后出现以下一种或多种问题：


* 系统画中画未出现。

* 画中画模式下视频暂停。

* 直播间无声音或声音不清晰。


<span id="possible-reasons-and-solutions"></span>
### 可能原因与解决方案

观众进入直播间后，iOS 观播 SDK 会将`AVAudioSession`切换为默认配置。在默认配置下，SDK 的系统画中画通常不会导致上述问题。但如果你的应用中其他音视频相关代码在观众进入直播间后修改了`AVAudioSession`的默认配置，则可能出现上述问题。

`AVAudioSession`的默认配置如下：


* 分类：AVAudioSessionCategoryPlayback

* 模式：AVAudioSessionModeMoviePlayback

* routeSharingPolicy：AVAudioSessionRouteSharingPolicyDefault

* options：0


请移除任何会修改`AVAudioSession`默认配置的代码。观众再次进入直播间时，SDK 会恢复默认`AVAudioSession`配置。

<span id="why-cannot-viewers-use-the-app-s-recording-feature"></span>
## 为什么观众无法使用应用的录音功能？

<span id="description"></span>
### 接口行为

观众进入直播间后，无法使用应用的录音功能。

<span id="possible-reasons-and-solutions"></span>
### 可能原因与解决方案

观众进入直播间后，iOS 观播 SDK 会将`AVAudioSession`切换为默认配置。

`AVAudioSession`的默认配置如下：


* 分类：AVAudioSessionCategoryPlayback

* 模式：AVAudioSessionModeMoviePlayback

* routeSharingPolicy：AVAudioSessionRouteSharingPolicyDefault

* options：0


如需观众使用录音等需要麦克风的功能，请将`AVAudioSessionCategoryPlayback`修改为`AVAudioSessionCategoryPlayAndRecord`，并将`AVAudioSessionModeMoviePlayback`修改为`AVAudioSessionModeVideoChat`。

示例代码如下。

```objectivec
NSError *error = nil;
[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayAndRecord
                                        mode:AVAudioSessionModeVideoChat
                          routeSharingPolicy:AVAudioSessionRouteSharingPolicyDefault
                                     options:0
                                       error:&error];
[[AVAudioSession sharedInstance] setActive:YES error:&error];
```


观众完成录音等需要麦克风的功能后，可将`AVAudioSession`切换回默认配置。

示例代码如下。

```objectivec
NSError *error = nil;
[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback
                                        mode:AVAudioSessionModeMoviePlayback
                          routeSharingPolicy:AVAudioSessionRouteSharingPolicyDefault
                                     options:0
                                       error:&error];
[[AVAudioSession sharedInstance] setActive:YES error:&error];
```


<span id="why-can-viewers-watch-previews-and-playbacks-normally-but-they-cannot-load-live-content"></span>
## 为什么观众可以正常观看预告和回放，但无法加载直播内容？

确保用于许可证申请的 Bundle ID 和成功申请后返回的应用 ID 与初始化 TTSDK 时传入的值一致。此外，确保初始化 TTSDK 时传入的 Bundle ID 与项目中配置的 Bundle ID 保持一致。否则，认证将失败。
