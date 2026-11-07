---
title: "iOS Player SDK: Best practices for short video scenarios"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-short-video-best-practices"
---

This article introduces how to build short video scenarios through the iOS Player SDK, to achieve the so\-called "zero first frame."

<span id="34e6e92b"></span>
## Background information

In a short video scenario, minimizing the time to first frame (TTFF) and improving the smoothness of swiping videos up and down are important measures for improving users' viewing experience:


* TTFF is the time it takes for the first frame of a video to appear after the user taps the play button. This is a core metric for video apps because it directly impacts the user experience. If the first frame takes several seconds to load, users may become impatient or even give up on the video. That’s why short video apps strive for a “zero TTFF”. This does not mean playback must start at exactly millisecond 0, but that the TTFF is reduced to a point where viewers do not perceive any delay.

* In the short video scenario, users generally browse different video content by swiping up and down. If videos stutter during swiping, it will impede user viewing. Improving the smoothness of swiping videos up and down ensures that users can browse videos and enjoy video content more easily. This improves overall viewing smoothness and continuity, thereby increasing the number of video views per capita and user stay duration.


To help you quickly build a short video scenario, the Player SDK provides two best strategies: the **preloading strategy** and **pre\-rendering strategy**. These strategies can be applied individually or in combination with one another.

By using these strategies, you can reduce the time required for a video's first frame to **100–300 milliseconds**, presenting users with an extremely fast first frame and a sleek playback experience.

<span id="2259b9df"></span>
## Introduction to strategies


|**Strategy** |**Description** |**Optimization results** |
|---|---|---|
|Preloading strategy |Preloading refers to preemptively downloading the data of the next video while playing the current video, to achieve a fast start when switching to the next video. This optimizes the user's playback experience. |Reduces time required for video's first frame |
|Pre\-rendering strategy |Pre\-rendering refers to preemptively creating a player to decode and render the next video while playing the current video. At the same time, you can also use the pre\-rendered first frame as a video cover to preemptively display to users and enhance the visual effect. |Reduces time required for video's first frame |
|Set cover image |It is recommended that you use the first non\-black frame extracted from the video by default as the cover image, to avoid a situation in which a black screen with no content appears before the image is rendered. If you don't set the cover image yourself, the Player SDK's pre\-rendering strategy will also extract the first frame as the cover image. However, this strategy only applies to videos when swiping down, and it can't pre\-render too many videos, to avoid loss of performance. Therefore, it is recommended that you choose to set your own cover image to improve the user experience. |Prevents a black screen and improves the user experience |


<span id="cf07412b"></span>
## Setting playback source

To use the preloading strategy or pre\-rendering strategy, use the methods below to set the playback source.

<span id="be4a131d"></span>
### Method 1: Set Vid playback source

See the sample code below to set the Vid playback source. Apart from the `vid` and `playAuthToken`, you will also need to specify the `resolution`. In addition, the `resolution` set here must be consistent with the resolution when you set the preloading source `resolution`.

```objectivec
/// Create the video source
NSString *vid = @"YOUR_VIDEO_ID"; // Provided by the app server
NSString *playAuthToken = @"YOUR_PLAYAUTHTOKEN"; // Provided by the app server
TTVideoEngineResolutionType resolution = TTVideoEngineResolutionTypeHD;
TTVideoEngineVidSource *source = [[TTVideoEngineVidSource alloc] initWithVid:vid playAuthToken:playAuthToken resolution:resolution];

/// Set the video source
[engine setVideoEngineVideoSource:source];

/// Play
[engine play];
```


<span id="ef7ea020"></span>
### Method 2: Set Url playback source

See the sample code below to set a DirectUrl playback source. The `url`, `vid`, and `cacheKey` are all required parameters. Here,


* `vid`: Video ID. You can use the Vid or the Vid's MD5 value.

* `cacheKey`: Cache key, the unique identifier of the URL. Each video may have multiple URLs with different definitions, with each URL corresponding to one `cacheKey`, but multiple URLs will correspond to the same video ID. You can use the unchanging part of the URL for MD5 operations, using the MD5 value as a `cacheKey`. For example, in `https://www.xxx.com/xxx/x/number`, the part before `"number"` is unchanging.


```objectivec
/// Create the video source
NSString *vid = @"YOUR_VIDEO_ID"; // Replace with your own video ID
NSString *url = @"http://www.example.com/test.mp4"; // Replace with your own video URL
NSString *cacheKey = [url vloc_md5String];
TTVideoEngineUrlSource *source = [[TTVideoEngineUrlSource alloc] initWithUrl:url cacheKey:cacheKey videoId:vid];

/// Set the video source
[engine setVideoEngineVideoSource:source];

/// Play
[engine play];
```


<span id="166886ef"></span>
## Use preloading strategy

To implement the preloading strategy, pass the video playlist into the SDK as a preloading source. Based on the playlist you provide, the SDK will preemptively download the content of the next video while the current video is playing. In this process, the SDK will automatically manage the preloading timing and configuration based on the current playback status, such as the preloading concurrency and data size.

The specific steps for accessing the preloading strategy are as follows:


1. Call `enableEngineStrategy:scene:` to enable the preloading strategy.

2. Set the preloading source with suitable timing:

   1. When the playback source data is first loaded or in a scenario of refreshing the page to display new data, call `setStrategyVideoSources:`.

   2. In a scenario of loading more data, call `addStrategyVideoSources:`.


The sample code for using the preloading strategy is as follows:

```Java
- (void)startPreloadStrategy {
    // Enable preload strategy, it is recommended to enable it when entering the short video page
    [TTVideoEngine enableEngineStrategy:TTVideoEngineStrategyTypePreload scene:TTVEngineStrategySceneSmallVideo];
}

// Set preload sources
- (void)configVideoEngineStrategyMediaSources:(NSArray<VEVideoModel *> *)videoModels refresh:(BOOL)refresh {
    NSMutableArray *sources = [NSMutableArray array];
    [videoModels enumerateObjectsUsingBlock:^(VEVideoModel * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
        [sources addObject:[VEVideoModel videoEngineVidSource:obj]];
    }];
    if (refresh) { 
        /// Called when loading for the first time or refreshing the list
        [TTVideoEngine setStrategyVideoSources:sources];
    } else { 
        /// Called when loading more by scrolling up
        [TTVideoEngine addStrategyVideoSources:sources];
    }
}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">The wrong playlist will cause preloading to fail.</div>


* <div data-tips="true" data-tips-type="warning">The preloading strategy will query the index of the video that is currently playing in the playlist, and preload index+1, index+2... index+n videos.</div>



<span id="02c10f86"></span>
## Use pre\-rendering strategy

To use the pre\-rendering strategy, pass the video playlist into the SDK as the pre\-rendering source. Based on the playlist you provide, while playing the current video, the SDK will preemptively create a player to decode and render the next video in the playlist. The Player SDK currently only supports pre\-rendering of the next video, and does not support pre\-rendering of the previous video.

<span id="configure-the-pre-rendering-strategy"></span>
### Configure the pre\-rendering strategy

The specific steps for accessing the pre\-rendering strategy are as follows:


1. Call `enableEngineStrategy:scene:` to globally enable the pre\-rendering strategy.

   ```objectivec
   [TTVideoEngine enableEngineStrategy:TTVideoEngineStrategyTypePreRender scene:TTVEngineStrategySceneSmallVideo];
   ```
   

2. Set the pre\-rendering source with suitable timing:

   1. When the playback source data is first loaded or in a scenario of dragging down to refresh the page and show new data, call `setStrategyVideoSources:` to reset the playlist.

   2. In a scenario of swiping up to load more data, call `addStrategyVideoSources:` to add data to the playlist.

   ```objectivec
   - (void)configVideoEngineStrategyMediaSources:(NSArray<VEVideoModel *> *)videoModels refresh:(BOOL)refresh {
       NSMutableArray *sources = [NSMutableArray array];
       [videoModels enumerateObjectsUsingBlock:^(VEVideoModel * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
           [sources addObject:[VEVideoModel videoEngineVidSource:obj]];
       }];
       if (refresh) {        
           [TTVideoEngine setStrategyVideoSources:sources];
       } else {
           [TTVideoEngine addStrategyVideoSources:sources];
       }
   }
   ```
   

3. Call `setPreRenderVideoEngineDelegate:` to set the pre\-rendering strategy callback, then perform other actions on the engine instance based on your business. For instance, you can set the video fill mode, playback start time, and so on.

   ```objectivec
   + (void)setPreRenderVideoEngineDelegate:(id<TTVideoEnginePreRenderDelegate>)delegate;
   ```
   

4. Call `getPreRenderVideoEngineWithVideoSource:` to determine whether pre\-rendering is complete and process the pre\-rendered cover logic.

   ```objectivec
   TTVideoEngine *preRenderVideoEngine = [TTVideoEngine getPreRenderVideoEngineWithVideoSource:mediaSource];
   if (preRenderVideoEngine) {
       [preRenderVideoEngine play];
   } else {
   }
   ```
   


<span id="prerender-with-start-time"></span>
### Pre\-rendering with a specified start time

This feature requires the iOS Player SDK `1.52.100.4` or later.

Use `setPreRenderVideoEngineDelegate:` to register a pre\-rendering delegate. In its `videoEngine:willPreRenderSource:` callback:


1. Set `VEKKeyPlayerEnableStartTimeSkipAVSkipSerial` to `YES`. This option is required when combining a start time with pre\-rendering.

2. Set the pre\-rendering player's start time in seconds using `VEKKeyPlayerStartTime_CGFloat`.


The following example pre\-renders from 5 seconds. Add this method to your `TTVideoEnginePreRenderDelegate` implementation and adjust the start time for your application.

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine willPreRenderSource:(id<TTVideoEngineMediaSource>)source {
    NSTimeInterval startTime = 5.0;
    // Required when combining a start time with pre-rendering.
    [videoEngine setOptionForKey:VEKKeyPlayerEnableStartTimeSkipAVSkipSerial value:@YES];
    // Set the pre-rendering player's start time in seconds.
    [videoEngine setOptionForKey:VEKKeyPlayerStartTime_CGFloat value:@(startTime)];
}
```


<span id="b7a44e98"></span>
## Clear all strategies

When exiting a video page or switching to another page, call `clearAllStrategy` to close all strategies and release resources.

```java
- (void)close { 
    [TTVideoEngine clearAllEngineStrategy]; 
}
```


<span id="96d1a320"></span>
## Note

If you simultaneously access the preloading strategy and pre\-rendering strategy, you only need to set one video playlist.
