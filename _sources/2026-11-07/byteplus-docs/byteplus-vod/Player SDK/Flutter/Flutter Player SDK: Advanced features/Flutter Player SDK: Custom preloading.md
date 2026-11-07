---
title: "Flutter Player SDK: Custom preloading"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-custom-preloading"
---

To achieve fast video playback initiation and optimize the user experience in your Flutter application, this guide provides step\-by\-step instructions for implementing custom preloading. You will learn how to add, monitor, and cancel preloading tasks for different video sources and how to verify cache hits. For more information, see [Android Player SDK: Custom preloading](https://docs.byteplus.com/en/docs/byteplus-vod/docs-custom-preloading-android).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="898d9c39"></span>
## Implementation steps

<span id="fd3267f5"></span>
### Step 1: Construct a playback source and add a preloading task

You can add a preload task by calling the corresponding API based on your playback source type (`Vid` or `DirectUrl`).


<Tabs>
<Tab zoneid="XAuqkYItDS" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

```Dart
// Initialize vid source with vid, playAuthToken, and desired resolution for preloading
TTVideoEngineVidSource source = TTVideoEngineVidSource.init(
        vid: <vid>,
        playAuthToken: <playAuthToken>,
        resolution: <TTVideoEngineResolutionType>);

// Initialize PreloaderVidItem with source and preloadSize (default preload size is 800K)
TTVideoEnginePreloaderVidItem item = TTVideoEnginePreloaderVidItem.vidItemWithVideoSource(source, 800 * 1024);
// Add the preloading task
TTVideoEnginePreload.addTaskWithVidItem(item);
```



</Tab>
<Tab zoneid="ZRZDQjLU4k" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

```Dart
// Initialize url source with url and cacheKey (used as the file name for disk caching, we recommend using the MD5 value of the URL that identifies the video file)
TTVideoEngineUrlSource source = TTVideoEngineUrlSource.initWithURL(<url>, <url cache>);
// A unique ID for the video source, defined by your application. It represents a collection of videos with the same content but different resolutions, encoding formats, container formats, etc.
source.vid = <vid>;

// Initialize PreloaderURLItem with source and preloadSize (default preload size is 800K)
TTVideoEnginePreloaderURLItem item = TTVideoEnginePreloaderURLItem.urlItemWithVideoSource(source, 800 * 1024);
// Add the preloading task
TTVideoEnginePreload.addTaskWithURLItem(item);
```



</Tab>
</Tabs>


<span id="835209f3"></span>
### Step 2: Listen for preloading task status (optional)

You can set callbacks for each preload task `item` to monitor its completion, cancellation, or failure status.

```Dart
// For added preloading tasks (PreloaderURLItem), listen for the cancel and end callbacks of the item
// Preloading task canceled
item.onPreloadCancel = () {
    print('TTF -- Preloading canceled callback in Dart');
};
   
// Preloading task completed
// taskInfo - file information and download information of the preloading task
// error - error information of the preloading task
item.onPreloadEnd = (TTVideoEngineLocalServerTaskInfo? taskInfo, TTError? error) {
    Map<dynamic, dynamic? map = taskInfo?.toJson();
    String errorStr = error.toString();
    print('TTF -- Preloading end callback in Dart end = $map error = $errorStr');
};
```


<span id="78fafbf8"></span>
### Step 3: Cancel preloading tasks (optional)

If your business logic determines that a video no longer needs to be preloaded, you can cancel its task from the queue to save network resources.

```Dart
// Cancel all preloading tasks
TTVideoEnginePreload.cancelAllTask();

// Cancel a preloading task based on its cacheKey
TTVideoEnginePreload.cancelTaskByKey(Key);
```


<span id="6743ec7f"></span>
### Step 4: Listen for and verify cache hits

To verify if preloading is effective, you can listen for the player instance's `onMediaCacheChange` callback. When playback begins for a video that has successfully hit the preload cache, this callback will be triggered with a `cacheSize` greater than 0.

```Dart
// Media cache change callback (MDL hit cache info)
// @param key - The key of the preload task (usually the `cacheKey`)
// @param cacheSize - The size of the cache hit in bytes
void Function(String key, int cacheSize)? onMediaCacheChange;
```
