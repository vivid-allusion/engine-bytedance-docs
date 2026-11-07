---
title: "iOS Player SDK: Custom preloading"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-custom-preloading-ios"
---

Preloading refers to downloading the header data of the upcoming video before starting playback, to achieve a fast start and improve the playback experience. Preloading is suitable for various playback scenarios, with a low cost for implementation and clear results.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="7b2e331e"></span>
## Preloading rules

This section introduces the preloading rules and results in different playback scenarios. By selecting reasonable, refined preloading timing and settings, the preloading hit rate can be improved, thereby enhancing the first frame experience. Note that overly broad or unreasonable preloading timing may result in wasted traffic and increased costs.

<span id="6bc552ed"></span>
### Short videos


* **Scenario features**: Only one vertical video is displayed at a time, and only one video is swiped at a time.

* **Preloading timing**: When the current video buffering duration exceeds 20 seconds or once all buffering is complete, preloading can start from the top down.

* **Number of preloads**: It is recommended to preload three videos. The user stays in the current video position to watch the video. The current position is recorded as "index," and n videos are preloaded from the top down, with a preloading range of [index + 1, index + n].

* **Preloading size**: It is recommended to set the preloading size to 800 kB.

* **Cancel**: When swiping to switch the video that is playing, all preloading is canceled. This is to avoid competition for bandwidth with the video that is currently playing, affecting the first frame of the current video.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To help you quickly build a short video scenario, the Player SDK provides two best strategies: the <strong>preloading strategy</strong> and <strong>pre\-rendering strategy</strong>. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-ios-player-short-video-best-practices">iOS Player SDK: Best practices for short video scenarios</a>.</div>


<span id="10142714"></span>
### Medium\-length videos


* **Scenario features:**  Two or more videos simultaneously appear on one screen. You can quickly swipe through feed streams, potentially across multiple videos at once.

* **Preloading timing:**  When the current video buffering duration exceeds 20 seconds or once all buffering is complete, preloading can start from the top down.

* **Number of preloads:**  It is recommended to preload five videos. The user stays in the current video position to watch the video. The current position is recorded as "index," and n videos are preloaded from the top down, with a preloading range of [index + 1, index + n].

* **Preloading size:**  It is recommended to set the preloading size to 800 kB.

* **Cancel:**  When swiping to switch the video that is playing, all preloading is canceled. This is to avoid competition for bandwidth with the video that is currently playing, affecting the first frame of the current video.


<span id="9ec13448"></span>
### Long videos


* **Scenario features**: Immersive fullscreen playback scenario or playback page scenario, such as movies, TV shows, variety shows, and other long video playback scenarios.

* **Preloading timing**: This can be based on the specific scenario. For instance, for movies, TV shows, or variety shows, when playback of the current episode is about to end, the next episode can be preloaded.


<span id="1ea44cd9"></span>
## Custom preloading in DirectURL mode

<span id="b07fd629"></span>
### Construct preloading data source

Use the same data source structure for preloading and playback. To ensure that playback can hit the preloading cache, the `vid`, `url`, and `cacheKey` used when constructing the preloading data source and playback data source must be the same. See the following sample code:

```objectivec
#import <TTSDK/TTVideoEngineHeader.h>
-(TTVideoEngineUrlSource *)createUrlSource {
    NSString *vid = @"video id"; // The video ID
    NSString *url = @"http://www.example.com/h264.mp4";
    // cacheKey is used as the filename for disk caching. It is recommended to use the MD5 value of the URL that can identify the video file. 
    NSString *cacheKey = [url md5String];
    // If you need to specify the encodetype and decryption key of the URL source, or indicate whether it is an HDR playback source, you can use other overloaded interfaces.
    TTVideoEngineUrlSource *source = [[TTVideoEngineUrlSource alloc] initWithUrl:url cacheKey:cacheKey videoId:vid];
    return source;
}
```


<span id="5a0439a5"></span>
### Add preloading task

```Java
- (void)addPreloadTask {
    // Set the preload size, such as 800k
    TTVideoEnginePreloaderURLItem * urlItem = [TTVideoEnginePreloaderURLItem urlItemWithVideoSource:[self createUrlSource] preloadSize:800 * 1024];
    urlItem.preloadProgress = ^(TTVideoEngineLoadProgress * _Nonnull progress) {
        // preload progress
    };
    urlItem.preloadEnd = ^(TTVideoEngineLocalServerTaskInfo * _Nullable info, NSError * _Nullable error) {
        // preload end
    };
    [TTVideoEngine ls_addTaskWithURLItem:urlItem];
}
```


<span id="462a2f68"></span>
### Cancel preloading task

Cancelling a task will affect tasks that have not started as well as ongoing download tasks. It will not affect completed tasks. See the following sample code:

```objectivec
// Cancel a single preload task
// The cacheKey is the one passed when constructing the DirectUrlSource playback source
[TTVideoEngine ls_cancelTaskByKey:cacheKey]; 
// Cancel all preload tasks
[TTVideoEngine ls_cancelAllTasks];
```


<span id="4e277ec7"></span>
## Custom preloading in Vid mode

<span id="925f2832"></span>
### Construct playback source

Preloading and playback use the same playback source structure. To ensure that playback can hit the preloading cache, the `vid`, `playAuthToken`, `encodeType`, and `resolution` used in the playback source constructed for preloading and playback must be the same.

```Java
#import <TTSDK/TTVideoEngineHeader.h>
- (TTVideoEngineVidSource *)createVidSource {
    NSString *vid = @"your video id"; // Issued by appServer
    NSString *playAuthToken = @"your video id's play auth token"; // Issued by appServer
    TTVideoEngineEncodeType encodeType = TTVideoEngineH264;
    // TTVideoEngineEncodeType encodeType = TTVideoEngineh265;
    TTVideoEngineResolutionType resolution = TTVideoEngineResolutionTypeSD;
    TTVideoEngineVidSource *vidSource = [[TTVideoEngineVidSource alloc] initWithVid:vid playAuthToken:playAuthToken resolution:resolution encodeType:encodeType isDash:NO isHLS:NO];
    return vidSource;
} 
```


<span id="a95b89e9"></span>
### Add preloading task

```objectivec
- (void)addPreloadTask1 {
    TTVideoEnginePreloaderVidItem *item = [TTVideoEnginePreloaderVidItem vidItemWithVideoSource:[self createVidSource] preloadSize:GLOBAL_CONFIG.cacheSize ?: (800 * 1024)];
    item.fetchDataEnd = ^(TTVideoEngineModel * _Nullable model, NSError * _Nullable error) {
        // get video model end
    }; 
    item.preloadProgress = ^(TTVideoEngineLoadProgress * _Nonnull progress) {
        // preload progress
    };
    item.preloadEnd = ^(TTVideoEngineLocalServerTaskInfo * _Nullable info, NSError * _Nullable error) {
        // preload end
    };
    [TTVideoEngine ls_addTaskWithVidItem:item];
}
```


During playback, call the `configResolution:` method and set the desired resolution to ensure that the resolution information for playback is consistent with the preloading settings. The code example is shown below.

```objectivec
// Same as the resolution used for preloading
[engine configResolution:TTVideoEngineResolutionTypeSD];
```


<span id="6dde71b2"></span>
### Cancel preloading task

Cancelling a task will affect tasks that have not started as well as ongoing download tasks. It will not affect completed tasks. See the following sample code:

```objectivec
// Cancel a single preload task by videoId
[TTVideoEngine ls_cancelTaskByVideoId:vid]; 
// Cancel all preload tasks
[TTVideoEngine ls_cancelAllTasks];
```


<span id="2e78a822"></span>
## Verify hit for preloading

Confirm a hit for preloading by monitoring the player callback. See the following sample code:

```objectivec
// Delegate method of the engine instance.
- (void)videoEngine:(TTVideoEngine *)videoEngine mdlKey:(NSString *)key hitCacheSze:(NSInteger)cacheSize {
    // cacheSize > 0 indicates that cache information is hit.
    // cacheSize = 0 indicates cache miss. Please check if the preloading task is successful. If using the video ID (vid) method, check if the playback and preloading resolution are consistent.
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The player supports simultaneous download and playback by default. If a video is playing for the first time, the hit cache is preloaded with downloaded data. The second playback may be a cache of the first playback.</div>


* <div data-tips="true" data-tips-type="tip">If you want to test the hit rate of the preloaded cache, make sure that each video is playing for the first time. We recommend testing this at first installation.</div>



<span id="d629e4e4"></span>
## Set preloading task concurrency

See the following sample code:

```objectivec
// Set the concurrency of preload tasks, default value is 2
// Setting preloadParallelNum to 1 means preload tasks are executed sequentially
[TTVideoEngine ls_localServerConfigure].preloadParallelNum = 1;
```
