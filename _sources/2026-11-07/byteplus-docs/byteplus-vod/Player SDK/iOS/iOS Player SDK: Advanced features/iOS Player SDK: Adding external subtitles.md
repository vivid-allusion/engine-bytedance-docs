---
title: "iOS Player SDK: Adding external subtitles"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-external-subtitles-ios"
---

This article provides instructions on how to add external subtitles when using the Player SDK.

<span id="324fef1a"></span>
## Overview

The "External subtitles" feature enables users to store subtitle files separately from video files and import them while playing the video. The Player SDK currently supports the WebVTT (Web Video Text Tracks) format for subtitle files. This approach provides flexibility, allowing users to decide whether to import subtitle files or load subtitles in various languages. Importantly, there is no requirement for additional video transcoding, as the feature can be activated with proper settings on the player's side.

<span id="8519bb18"></span>
## Prerequisites

Before adding the external subtitles, make sure you have:


* Integrated the SDK according to [iOS Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk).

* If you are playing videos in Vid mode, you need to prepare the subtitle file:

   * If you already have a separate subtitle file, you can upload the subtitle file on the **Video details** page in the [BytePlus VOD console](https://console.byteplus.com/vodpaas), as shown in the following picture.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b5b084b692e416bbbdcf5114f1a7814~tplv-goo7wpa0wc-image.image) </span>

   * If you don't have a separate subtitle file, you can use the [Smart subtitling template](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template) to generate the subtitle file.


<span id="43ebb5d0"></span>
## API sequence

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05cf7fbe473f495e8133d5e47f2fa46a~tplv-goo7wpa0wc-image.image) </span>

<span id="ede5da6a"></span>
## Enabling the external subtitles feature

To enable the external subtitles feature, use the following sample code:

```objectivec
// Enable the external subtitles feature. Call this method before setting subtitle source.
[self.videoEngine setOptionForKey:VEKKeyPlayerEnableSubThread_BOOL value:@(YES)];

// Enable subtitle loading optimization.
// NO: Disable subtitle loading optimization
// YES: Enable subtitle loading optimization
[self.videoEngine setOptionForKey:VEKKeyPlayerSubtitleOptEnable_BOOL value:@(YES)];

// Use the data loading module (MDL) to load external subtitles, improving the success rate of loading
// YES: Use MDL to load external subtitles
// NO: Do not use MDL to load external subtitles
[self.videoEngine setOptionForKey:VEKKeySubTitleEnableMDL_BOOL value:@(YES)];
```


<span id="4a3681dc"></span>
## Setting subtitle source

The Player SDK offers two methods for setting the subtitle source. Select the appropriate method based on your specific needs:


* (Recommended) Method 1: Using the subtitle URL

   ```objectivec
   NSString *url = @"http://www.example.com/h264.mp4";
   NSString *cacheKey = [url md5String]; // cacheKey is used as the filename for disk caching. It is recommended to use the MD5 value of the part of the URL that identifies the video file.
   TTVideoEngineUrlSource *source = [[TTVideoEngineUrlSource alloc] initWithUrl:url cacheKey:cacheKey];
   [self.videoEngine setVideoEngineVideoSource:source];
   
   // Set the subtitle source in DirectURL mode
   // The subtitle source needs to implement the TTVideoEngineSubDecInfoProtocol protocol
   [self.videoEngine setSubDecInfoModel:self];
   [self.videoEngine play];
   
   // MARK: - TTVideoEngineSubDecInfoProtocol
   // Return a JSON string containing subtitle information, including the subtitle URL. See the Subtitle JSON example section for reference.
   - (NSString *_Nullable)jsonString {
       return subtitleJSONStr;
   }
   
   // Return the number of subtitles in the subtitle list
   - (NSInteger)subtitleCount {
       return count;
   }
   ```
   

* Method 2: Using Vid and SubtitleToken

   ```objectivec
   NSString *vid = @"YOUR_VIDEO_ID"; // Provided by your app server
   NSString *playAuthToken = @"YOUR_PLAYAUTHTOKEN"; // Provided by your app server
   TVideoEngineVidSource *vidSource = [[TTVideoEngineVidSource alloc] initWithVid:vid playAuthToken:playAuthToken resolution:resolution];
   
   // Set the subtitle auth token before starting playback
   [self.videoEngine setSubtitleAuthToken:@"SUBTITLE_AUTHTOKEN"]; // Provided by your app server
   
   // Set the default language with the SubtitleID. If not set, the SDK will display the first language in the order provided by the BytePlus VOD server.
   // See the subtitle language table at: https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language
   // You can obtain the SubtitleID using the -[TTVideoEngine subtitleIDs] method.
   [self.videoEngine setOptionForKey:VEKeyPlayerSwitchSubtitleId_NSInteger value:@(<#SubtitleID#>)];
   
   [self.videoEngine setVideoEngineVideoSource:vidSource];
   [self.videoEngine play];
   ```
   


<span id="ab579ee6"></span>
## Controlling subtitles

<span id="f1743415"></span>
### Enabling/Disabling subtitles output

To control the enabling or disabling of subtitle output during playback, use the following sample code:

```objectivec
// Enable or disable subtitles during playback
// YES: Enable subtitles
// NO: Disable subtitles
[self.videoEngine setOptionForKey:VEKKeyPlayerSubEnabled_BOOL value:@(YES)];
```


<span id="e640b370"></span>
### Switching between subtitles

Use the following sample code to switch to a different subtitle by passing the subtitle ID:

```objectivec
[self.videoEngine setOptionForKey:VEKeyPlayerSwitchSubtitleId_NSInteger value:@(<#NSInteger#>)];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When setting the subtitle source with the Vid, set the <code>SubtitleId</code> parameter. You can obtain the <code>SubtitleId</code> by calling the <code>-[TTVideoEngine subtitleIDs]</code> method.</div>


* <div data-tips="true" data-tips-type="tip">When setting the subtitle source with the HTTP URL, set the <code>sub_id</code> parameter from the subtitle JSON.</div>



<span id="ef9c7ffb"></span>
## Setting subtitle callback

Use the `setSubtitleDelegate` method to set the subtitle callback:

```objectivec
// Set the callback receiver
[self.videoEngine setSubtitleDelegate:self];
```


The subtitle callback can be used as follows:

```objectivec
/**
 * Subtitle Callback
 * <TTVideoEngineSubtitleDelegate>
 */

// Callback for each line of subtitle information.  Returns the subtitle content at the video's current playback position. You must render the subtitles yourself after receiving this information.
// content: The single-line subtitle content.
// pts: The timestamp.
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubtitleInfoCallBack:(NSString *)content pts:(NSUInteger)pts {
    // Refresh subtitles.
    // Example: [self.subtitleView refreshContent:content];
}

// Callback for each line of subtitle information.
// subInfo: TTVideoEngineSubInfo
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubtitleInfoCallBack:(TTVideoEngineSubInfo *)subInfo {
    // subInfo.pts: The timestamp when the subtitle starts displaying.
    // subInfo.content: The subtitle content.
    // subInfo.duration: The duration for which the subtitle should be displayed.
}

// For Vid playback, the player calls this method when subtitles are requested. You can use it to update the subtitle list or set the default subtitle.
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubtitleInfoRequested:(id _Nullable)info error:(NSError * _Nullable)error {
    NSArray *supportSubtitlesIds = [videoEngine subtitleIDs]; // Get all supported subtitles at this point, and update the subtitle list if necessary
    
    // [videoEngine setOptionForKey:VEKeyPlayerSwitchSubtitleId_NSInteger value:@(<#NSInteger#>)]; Set the default subtitle or switch subtitles
}

// Subtitle switch completed.
// currentLangId: The current language ID
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubSwitchCompleted:(BOOL)success currentLangId:(NSInteger)currentLangId {
    
}

// Current subtitle loading completed
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubLoadFinished:(BOOL)success info:(TTVideoEngineLoadInfo *)info {
    if (!success) {
        // Subtitle loading failed. You can remove the subtitle rendering or request again.
    } else {
        // Subtitle loading succeeded.
        // info.firstPts: The timestamp when the subtitle first appears
    }
}
```


<span id="25a06ede"></span>
## References

<span id="f20d1d21"></span>
### Subtitle JSON example

```JSON
{
  "list": [
    {
      "id": 0,
      "language": "rus-RU",
      "language_id": 6,
      "url": "https://***.com/cbebedaad*******17f0b13/6087d12f/video/tos/cn/tos-cn-o-0004/52ce3882d709***913cbd83d969/",
      "expire": 1619513647,
      "format": "webvtt",
      "sub_id": 328934091
    },
    {
      "id": 1,
      "language": "cmn-Hans-CN",
      "language_id": 1,
      "url": "https://***.com/93adb942***bdfce8cb/6087d12f/video/tos/***a4122dac42d69e8233a4dfda82fe/",
      "expire": 1619513647,
      "format": "webvtt",
      "sub_id": 429984091
    },
    {
      "id": 2,
      "language": "cmn-Hans-CN|eng-US",
      "language_id": 5,
      "url": "https://***.com/d782d36702***7b9719/6087d12f/video/tos/***5f0d106146a19ad566b967211091/",
      "expire": 1619513647,
      "format": "webvtt",
      "sub_id": 829987091
    }
  ]
}
```


Description:


* `sub_id` is the subtitle ID, and `language_id` is the language ID. You need to maintain the mapping relationship between subtitle ID and language ID by yourself.

* Refer to [Subtitle languages](https://docs.byteplus.com/docs/byteplus-vod/docs-subtitle-language) for the values of `language` and `language_id`.

* `url` is the URL of the subtitle file.

* `id` can be set as an index.

* `expire` is the expiration time of the subtitle URL. If there is no expiration time, it can be left empty.
