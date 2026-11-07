---
title: "Viewer SDK for iOS FAQs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-faqs"
---

<span id="c980efcb"></span>
## Why does the system Picture\-in\-Picture (PiP) mode fail?

<span id="f78b66b8"></span>
### Description

Viewers switch the app to the background while watching live videos, previews, or playbacks. However, the system PiP does not appear.

<span id="35e4cc1c"></span>
### Possible reasons and solutions


* The iOS version of the viewer's mobile device is lower than 14.0.

   Only iOS 14.0 and above versions support system PiP. Viewers must update the iOS version.

* The system PiP is not enabled in the Viewer SDK.

   * To enable the system PiP for live videos, the sample code is as follows.

      ```objectivec
      BDLLiveEngine.sharedInstance.liveRoomConfiguration.playerConfig.common.enableLivePiP = YES;
      ```
      

   * To enable the system PiP for previews and playbacks, the sample code is as follows.

      ```objectivec
      BDLLiveEngine.sharedInstance.liveRoomConfiguration.playerConfig.common.enableVodPiP = YES;
      ```
      

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system PiP is enabled by default in the Viewer SDK. If you have modified the default configuration, see the preceding sample code to enable the system PiP again.   </div>
   

* Viewers do not turn on the **Start PiP** **Automatically** switch on their mobile devices.

   Viewers must turn on the switch on the **Settings** \> **General** \> **Picture in Picture** page of their mobile devices.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef82b7c11e4e45158f5d03dabca3d40d~tplv-goo7wpa0wc-image.image) </span>


If the problem persists, refer to the possible reasons and solutions in [Why does the system PiP mode fail? Why does the video pause in PiP mode? Or why is the sound in the live room abnormal?](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-faqs#f6b3f91b) for troubleshooting and handling.

<span id="f6b3f91b"></span>
## Why does the system PiP mode fail? Why does the video pause in PiP mode? Or why is the sound in the live room abnormal?

<span id="f943c493"></span>
### Description

Viewers switch the app to the background while watching live videos, previews, or playbacks, and then one or several of the following problems occur:


* The system PiP does not appear.

* The video pauses in PiP mode.

* No sound or the sound is unclear in the live room.


<span id="d9d061e6"></span>
### Possible reasons and solutions

After viewers enter the live room, the Viewer SDK changes the `AVAudioSession` to the default configuration. With the default configuration, the SDK's system PiP generally does not have the preceding problems. However, if other audio and video\-related codes in your app change the default configuration of `AVAudioSession` after viewers enter the live room, the preceding problems may occur.

The default configuration of `AVAudioSession` is as follows:


* Category: AVAudioSessionCategoryPlayback

* Mode: AVAudioSessionModeMoviePlayback

* routeSharingPolicy: AVAudioSessionRouteSharingPolicyDefault

* options: 0


Omit the audio and video\-related codes that change the default configuration of `AVAudioSession`. When viewers enter the live room again, `AVAudioSession` can be changed to the default configuration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the problem is the system PiP does not appear, we recommend that you troubleshoot and handle according to the possible reasons and solutions in <a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-faqs#c980efcb">Why does the system Picture\-in\-Picture (PiP) mode fail?</a> first.</div>


<span id="44a93306"></span>
## Why cannot viewers use the app's recording feature?

<span id="cd0bbf1f"></span>
### Description

After viewers enter the live room, they cannot use the recording feature of your app.

<span id="226f65da"></span>
### Possible reasons and solutions

After viewers enter the live room, the Viewer SDK changes the `AVAudioSession` to the default configuration.

The default configuration of `AVAudioSession` is as follows:


* Category: AVAudioSessionCategoryPlayback

* Mode: AVAudioSessionModeMoviePlayback

* routeSharingPolicy: AVAudioSessionRouteSharingPolicyDefault

* options: 0


If you want viewers to use features that require a microphone, such as recording, change `AVAudioSessionCategoryPlayback` to `AVAudioSessionCategoryPlayAndRecord`, and change `AVAudioSessionModeMoviePlayback` to `AVAudioSessionModeVideoChat`.

The sample code is as follows.

```objectivec
NSError *error = nil;
[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayAndRecord
                                        mode:AVAudioSessionModeVideoChat
                          routeSharingPolicy:AVAudioSessionRouteSharingPolicyDefault
                                     options:0
                                       error:&error];
[[AVAudioSession sharedInstance] setActive:YES error:&error];
```


You can change `AVAudioSession` back to the default configuration after viewers finish using features that require a microphone, such as recording.

The sample code is as follows.

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
## Why can viewers watch previews and playbacks normally, but they cannot load live content?

Make sure the Bundle ID used to apply for the live streaming license and VOD (Video\-on\-Demand) license and the app ID returned after the successful license application are the same as the ones passed in when initializing TTSDK. Also, make sure the Bundle ID passed in when initializing TTSDK is the same as that configured in the project. Otherwise, the authentication will fail.
