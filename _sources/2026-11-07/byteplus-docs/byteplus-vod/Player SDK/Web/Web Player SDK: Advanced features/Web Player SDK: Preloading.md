---
title: "Web Player SDK: Preloading"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/preloading_web"
---

VePlayer provides a video resource preloading feature that supports manual preloading and automatic preloading for video playback in Feed stream scenarios, reducing the first\-frame loading time and optimizing the playback experience.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only available in the advanced version. Please ensure you have purchased an advanced license. See <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-license-management">Licenses</a> for details.</div>


<span id="052e1341"></span>
## **Effect Demonstration**

No need to request data during the video's starting playback phase. The player directly uses the preloaded buffered data to start playback, as shown in the image below.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d5ae895d416436a93cc55c8e0da024f~tplv-goo7wpa0wc-image.image" width="700px" /></div>


<span id="ef8e313d"></span>
## **Compatibility**


* Container Format: Currently only support MP4 format.

* Playback Mode: Only support DirectUrl mode for now; Not support Vid mode yet.

* Playback Environment: Require browser support for MSE (Media Source Extensions), compatible with PC, Android, and iOS (iOS 17.1 and above only).


<span id="dbb160ad"></span>
## Working Principle

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79023290b77a4024a1d458f2d0ae981a~tplv-goo7wpa0wc-image.image) </span>

<span id="b10ad6d8"></span>
## **Initializing Preload Module**

Call `prepare` to initialize the preload module:

```TypeScript
VePlayer.prepare({
  appId: number; // Application ID, get on the application management page of the Video on Demand console.
  strategies: {
     preload: boolean | IPreloadConfig; // Enable advanced preloading capabilities, set a boolean value to use the default configuration, and configure initial preload parameters.
  }
})
```


<span id="540a60be"></span>
## **Manual Preloading**

In manual mode, set the preload resource list in advance. When a player is instantiated, if the target duration of a video resource is loaded, it starts playback directly using the preloaded cached data and continues downloading new data from that point.


1. Set the preload mode to manual mode:


```TypeScript
VePlayer.setPreloadScene(0)
```



2. Set the preload resource list:


```TypeScript
VePlayer.setPreloadList(list: IPreloadStream[])
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In manual mode, the player adds all preload resources to the preload task queue.</div>


* <div data-tips="true" data-tips-type="tip">The player will not preload videos that are already playing.</div>


3. Use preloaded data:

   1. Create a player instance:


```TypeScript
new VePlayer({
  playList: [ IPreloadStream ], // Current video information
  vid: 'xxxvid', // Unique video ID
  enableMp4MSE: true, // Enable MP4 MSE playback mode
})
```



2. Switch to a new video:


```TypeScript
playerSdk.playNext({
  playList: [ IPreloadStream ], // Current video information
  vid: 'xxxvid', // Unique video ID
})
```


<span id="85439cb4"></span>
## **Automatic Preloading**

VePlayer provides an automatic preloading feature for Feed stream video playback scenarios. After setting the list of videos to be preloaded, the player automatically searches for videos to preload based on the current video's ID, then adding (`prevCount`) videos before and (`nextCount`) after the current one to the preload task queue and dynamically preloading them based on the current video's status.


1. Set the preload mode to automatic and configure `prevCount` and `nextCount`:


```TypeScript
VePlayer.setPreloadScene(1,{
  prevCount: 1, // Preload the video before the current one.
  nextCount: 2, // Preload the two videos after the current one.
})
```



2. Set the list of resources to be preloaded:


```TypeScript
// Set the list of resources to be preloaded. Based on the current video's ID, the player retrieves the videos before and after it and add them to the preload task queue, executing preloading based on the current video's state.
VePlayer.setPreloadList(list: IPreloadStream[])
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The player will not preload videos that are already playing.</div>


3. Use preloaded data:

   1. Create a player instance:


```TypeScript
new VePlayer({
  playList: [ IPreloadStream ], // Current video information
  vid: 'xxxvid', // Unique video ID
  enableMp4MSE: true, // Enable MP4 MSE playback mode
})
```



2. Switch to a new video:


```TypeScript
playerSdk.playNext({
  playList: [ IPreloadStream ], // Current video information
  vid: 'xxxvid', // Unique video ID
})
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a player instance or switching videos, the player checks if preloaded data exists based on the<code>vid</code> and <code>playList</code>. If it does, it uses that data directly and triggers a new preload task check.</div>


<span id="913bd85c"></span>
## **Related APIs**


* `VePlayer.preloader.removeAll()`: Remove all preloaded data. This does not affect subsequent preload tasks.

* `VePlayer.preloader.removeAllPreloadTask()`: Cancel all preload tasks, clear the preload resource list, remove the current task list, and interrupt any currently loading tasks.

* `VePlayer.preloader.clearPreloadList()`: Clear the list of all resources to be preloaded.
