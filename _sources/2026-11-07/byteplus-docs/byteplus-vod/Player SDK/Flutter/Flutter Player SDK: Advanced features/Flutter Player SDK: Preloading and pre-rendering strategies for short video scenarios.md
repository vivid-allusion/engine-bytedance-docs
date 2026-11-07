---
title: "Flutter Player SDK: Preloading and pre-rendering strategies for short video scenarios"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-preloading-pre-rendering"
---

To help you quickly build a short video feed and solve common issues like slow first\-frame loading and high resource consumption when users swipe between videos, the Player SDK offers two strategies based on real feedback and large\-scale practical experience:


* **Preloading strategy:**  Caches video data in advance to improve startup speed.

* **Pre\-rendering strategy:**  Creates the next player instance in advance to optimize the switching experience.


This guide will walk you through how to enable and configure these two strategies, helping you strike a balance between performance and user experience. For a detailed feature introduction, see [Android Player SDK: Best practices for short video scenarios](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-short-video-best-practices).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="f8a7066a"></span>
## Preloading strategy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The preloading strategy supports Vid, DirectUrl, and VideoModel playback sources. To ensure a successful cache hit, you need to pay attention to the following points when setting the preloading list:</div>



* <div data-tips="true" data-tips-type="warning">For Vid or VideoModel playback sources: You must explicitly specify the resolution field when building the playback source to determine which resolution to preload. The playback source set by setMediaSource for subsequent playback must have the same resolution field as the one set during preloading. If the resolutions do not match, a cache miss will occur.</div>


* <div data-tips="true" data-tips-type="warning">For DirectUrl playback sources: You must explicitly specify the cacheKey field when building the playback source. This cacheKey must be globally unique. The playback source set via setMediaSource for subsequent playback must have the same cacheKey field as the one set during preloading. If the cacheKey fields do not match, a cache miss will occur.</div>



```Dart
// Method definitions in TTVideoEngineStrategy
// Enable the preloading strategy, recommended to enable when entering the short video page
TTVideoEngineStrategy.enableEngineStrategy(
          strategyType: TTVideoEngineStrategyType.preload, scene: TTVideoEngineStrategyScene.smallVideo);
          
// Set the preloading list
static Future<void> setStrategyVideoSources({required List<TTVideoEngineMediaSource> videoSources})

// Update the preloading list
static Future<void> addStrategyVideoSources({required List<TTVideoEngineMediaSource> videoSources})

// Specifies the starting position of the preload list. After calling `setStrategyVideoSources`, this method can be used to immediately start the preload task.
// If index is not set, preloading starts by default from the second video in the feed. If index is set, preloading starts from the specified index.
static Future<void> startPreloadWithIndex({required int index})

// Disable all strategies
TTVideoEngineStrategy.clearAllEngineStrategy();
```


**Listening for preload cache hits:**  After a successful preload, when the player plays the corresponding source, it will prioritize using the cached data to start playback, thus speeding up the first frame. To verify if preloading is effective, you can listen to the player instance's `onMediaCacheChange` callback. When playback starts, if the video successfully hits the preload cache, this callback will be triggered, and the `cacheSize` will be greater than 0.

```Dart
// Media cache change callback (MDL hit cache info).
// @param key - The MDL task key.
// @param cacheSize - The size of the cache hit in bytes.
void Function(String key, int cacheSize)? onMediaCacheChange;
```


<span id="a52763d5"></span>
## Pre\-rendering strategy

In a feed scenario, another common technique to speed up the first frame—in addition to preloading—is to create the next player instance in advance. This way, when the user swipes to the next video, the player is already prepared, saving instantiation time and displaying the first frame faster. However, manually managing multiple instances has its drawbacks:


* Resource consumption: Creating multiple instances without limits can significantly increase CPU and memory usage, potentially causing app lag.

* Resource contention: Creating a player at the critical moment of video startup can actually slow down the first frame due to busy tasks or resource competition.


The pre\-rendering strategy is designed to solve these problems. It is a more intelligent multi\-instance management solution that automatically creates and prepares the next player instance for you at an opportune moment when playback tasks are relatively idle, striking the perfect balance between performance and user experience.

<span id="284f28f0"></span>
### Core implementation steps

<span id="e4deb270"></span>
#### Step 1: Enable the pre\-rendering strategy

Enable the pre\-rendering strategy when your short video page (e.g., the feed page) is initialized.

```Dart
// Method definitions are in TTVideoEngineStrategy

// Enable the pre-rendering strategy, recommended on entering the player page.
TTVideoEngineStrategy.enableEngineStrategy(
  strategyType: TTVideoEngineStrategyType.preRender,
  scene: TTVideoEngineStrategyScene.smallVideo,
);
```


<span id="16311ff6"></span>
#### Step 2: Set the Play Source List

Like the preloading strategy, the pre\-rendering strategy requires a list of video sources so the SDK knows which videos might be played next.

```Dart
// Setting and updating the pre-rendering list is identical to the preloading list;
// it only needs to be set once.
TTVideoEngineStrategy.setStrategyVideoSources({
  required List<TTVideoEngineMediaSource> videoSources,
});
```


The pre\-rendering strategy uses the unique `vid` of a play source to match and reuse pre\-created player instances. Therefore, it is crucial to set a stable and unique `vid` for each play source. For `DirectURL` sources, also be sure to pass the `vid` during construction.


* For versions 1.49.101 and later, use the `TTVideoEngineUrlSource.initWithURLVidCacheKey` factory method for quick creation:


```Dart
// For 1.49.10+
final urlSource = TTVideoEngineUrlSource.initWithURLVidCacheKey(
  url: mainPlayUrl,
  vid: widget.episode.vid, // A unique vid is required.
  cacheKey: cacheKey,
);
```



* For versions before 1.49.101, you can use the default constructor:


```Dart
final urlSource = TTVideoEngineUrlSource(
  urls: [url],
  cacheKey: cacheKey,
  vid: widget.episode.vid, // A unique vid is also required here.
);
```


<span id="2386c7f9"></span>
#### Step 3: Set pre\-rendering callbacks

Due to differences in the underlying implementation of pre\-rendering between Android and iOS, the Flutter SDK provides two platform\-specific callbacks to allow for necessary pre\-playback configuration after a pre\-rendered player is created.


* **Android:**  You need to listen to the `onCreatePreRenderEngine` callback. In this callback, you must manually create the player instance, set the play source, and can perform other custom configurations (like enabling hardware decoding).


```Dart
// Initialize the strategy module to set the callback.
TTVideoEngineStrategy.init();

TTVideoEngineStrategy.onCreatePreRenderEngine = ((source) async {
  // This callback is only effective on Android.
  VodPlayerFlutter player = VodPlayerFlutter();

  // 1. Create the player. You must pass the vid from the source and set preCreated to true.
  String coreHashHex = await player.createPlayer(vid: source.getVid, preCreated: true);

  // 2. [Required] Set the play source for the pre-rendered player.
  await player.setMediaSource(source);

  // 3. [Optional] Apply custom settings as needed, such as enabling hardware decoding.
  player.setHardwareDecode(<enable>);
  // ...

  // 4. Note: You must `await` the completion of `createPlayer` and `setMediaSource`
  //    before returning the player.
  return player;
});
```



* **iOS:**  The SDK automatically handles creating the player and setting of the play source. You just need to listen to the `onPlayerCreated` callback to get the prepared player instance and apply any pre\-playback configurations.


```Dart
TTVideoEngineStrategy.onPlayerCreated = ((player) {
  // This callback is only effective on iOS.
  // Unlike Android, you do not need to create the player or set the play source here.
  
  // [Optional] Apply custom settings as needed, such as enabling hardware decoding.
  player.setHardwareDecode(<enable>);
});
```


<span id="7f3d0245"></span>
#### Step 4: Get and use the pre\-rendered player

In your feed's swipe logic, when you need to play the next video, simply pass the corresponding `vid` when calling `createPlayer`. If pre\-rendering was successful, the SDK will immediately return the pre\-created player instance.

```Dart
// When the user swipes to the next item
VodPlayerFlutter player = VodPlayerFlutter();

// Pass the target video's vid. If there's a pre-rendered instance,
// the SDK will return it directly.
await player.createPlayer(vid: source.getVid);
```


Pre\-rendering is not always successful (for example, if the user swipes too quickly). You can check the `isPreRender` property after calling `createPlayer` to determine if the returned instance was pre\-rendered.

```Dart
// After calling createPlayer
bool isPreRender = await _player!.isPreRender;
```


<span id="4a328740"></span>
### Advanced usage

<span id="405127fb"></span>
#### Using the pre\-rendered first frame as the video cover

You can use the first frame from a pre\-rendered video as a video cover. Compared to traditional image covers, this approach is faster to display and saves more data by reusing video data. Call the static method `VodPlayerFlutter.preRenderFirstFrame` **before** creating the player for the next video.

```Dart
// Method definition in VodPlayerFlutter
// @param vid: The vid of the video whose first frame is to be pre-rendered.
// @param viewId: The ID of the render view where the first frame will be displayed.
// @param displayMode: The scaling mode for the first frame (TTVideoEngineScalingMode).
String? res = await VodPlayerFlutter.preRenderFirstFrame(
  vid: vid, 
  viewId: viewId, 
  displayMode: displayMode,
);

// After calling preRenderFirstFrame, create the player for the next video as usual.
VodPlayerFlutter player = VodPlayerFlutter();
String coreHashHex = await player.createPlayer(vid: vid);
player.setMediaSource(source);
// Note: The viewId here must match the viewId used in preRenderFirstFrame.
player.setPlayerContainerView(viewId); 
player.play();
```
