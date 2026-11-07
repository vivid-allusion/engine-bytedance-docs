---
title: "React Native Player SDK: Custom preloading"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-custom-preloading"
---

Custom preloading allows you to proactively initiate a preloading task for any video at any point in your business logic. When the player later needs to play that video, it will prioritize using the already cached data. This significantly reduces startup buffering and accelerates the time\-to\-first\-frame, resulting in a superior playback experience. This guide will walk you through how to use the custom preloading feature, including adding and canceling preload tasks.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="a1e9f198"></span>
## Custom preloading vs. preloading strategy

While both features are designed to improve startup performance, they are suited for different business scenarios.


* **Preloading strategy:**  This is ideal for **predictable, sequential list\-based playback scenarios**, such as a short\-video feed. In this case, the SDK's strategy automatically manages the preloading queue for you.

* **Custom preloading:**  This is ideal for **unpredictable, user\-driven scenarios**. For example, in a short drama app, a user might browse through various episode cards. When the user lingers on or shows interest in a specific card, you can immediately trigger a custom preload task for that episode's video. If the user then decides to play it, the playback will be nearly instant thanks to the locally available data.


<span id="26177f53"></span>
## Adding a custom preloading task

You can add a preload task by calling the API that corresponds to your play source type (`Vid`, `DirectUrl`, or `VideoModel`). You can specify the amount of data to preload and use callback functions to monitor the task's lifecycle. Upon a successful call, the API returns a unique task ID, `taskId`, which you can later use to cancel the task.

<span id="9edfc975"></span>
### Vid source

```TypeScript
import { preloadVidSource } from '@byteplus/react-native-vod-player';
 
// Initiate a preload task for a VidSource
const taskId = preloadVidSource(
  vidSource,
  { preloadSize: 800 * 1024 }, // Optional: Preload configuration.
                               // `preloadSize` is the desired cache size in bytes. Defaults to 800KB.
  // Optional: Callbacks to monitor the task's lifecycle.
  {
    // `onLoadSuccess`: Triggered when the requested amount of data is successfully cached.
    // `cacheSize`: The actual number of bytes cached.
    onLoadSuccess: (source, cacheSize) => {
      const message = `preload success: ${source.vid()}... (cache size: ${Math.round(
        cacheSize / 1024,
      )}KB)`;
      console.log(`[PreLoad] ${message}`);
    },
    // `onLoadFail`: Triggered if an error occurs during preloading.
    onLoadFail: (source, error) => {
      const message = `preload fail: ${source.vid()}... - ${
        error.message || error.code || 'unknown error'
      }`;
      console.log(`[PreLoad] ${message}`);
    },
    // `onLoadCancel`: Triggered if the task is canceled before completion.
    onLoadCancel: source => {
      const message = `preload cancel: ${source.vid()}...`;
      console.log(`[PreLoad] ${message}`);
    },
  },
);
```


<span id="277b2cac"></span>
### DirectUrl source

When using `DirectUrlSource`, ensure the `cacheKey` in the play source object is a unique and stable identifier for the video URL, as the SDK uses it to identify the cache.

```TypeScript
import { preloadDirectUrlSource } from '@byteplus/react-native-vod-player';

// Initiate a preload task for a DirectUrlSource
const taskId = preloadDirectUrlSource(
  directUrlSource,
  { preloadSize: 800 * 1024 }, // Optional: Preload configuration.
                               // `preloadSize` is the desired cache size in bytes. Defaults to 800KB.
  // Optional: Callbacks to monitor the task's lifecycle.
  {
    // `onLoadSuccess`: Triggered when the requested amount of data is successfully cached.
    // `cacheSize`: The actual number of bytes cached.
    onLoadSuccess: (source, cacheSize) => {
      const message = `preload success: ${source.cacheKey}... (cache size: ${Math.round(
        cacheSize / 1024,
      )}KB)`;
      console.log(`[PreLoad] ${message}`);
    },
    // `onLoadFail`: Triggered if an error occurs during preloading.
    onLoadFail: (source, error) => {
      const message = `preload fail: ${source.cacheKey}... - ${
        error.message || error.code || 'unknown error'
      }`;
      console.log(`[PreLoad] ${message}`);
    },
    // `onLoadCancel`: Triggered if the task is canceled before completion.
    onLoadCancel: source => {
      const message = `preload cancel: ${source.cacheKey}...`;
      console.log(`[PreLoad] ${message}`);
    },
  },
);
```


<span id="bbbc6323"></span>
### VideoModel source

```TypeScript
import { preloadVideoModelSource } from '@byteplus/react-native-vod-player';

// Initiate a preload task for a VideoModelSource
const taskId = preloadVideoModelSource(
  videoModelSource,
  { preloadSize: 800 * 1024 }, // Optional: Preload configuration.
                               // `preloadSize` is the desired cache size in bytes. Defaults to 800KB.
  // Optional: Callbacks to monitor the task's lifecycle.
  {
    // `onLoadSuccess`: Triggered when the requested amount of data is successfully cached.
    // `cacheSize`: The actual number of bytes cached.
    onLoadSuccess: (source, cacheSize) => {
      const message = `preload success: ${source.vid()}... (cache size: ${Math.round(
        cacheSize / 1024,
      )}KB)`;
      console.log(`[PreLoad] ${message}`);
    },
    // `onLoadFail`: Triggered if an error occurs during preloading.
    onLoadFail: (source, error) => {
      const message = `preload fail: ${source.vid()}... - ${
        error.message || error.code || 'unknown error'
      }`;
      console.log(`[PreLoad] ${message}`);
    },
    // `onLoadCancel`: Triggered if the task is canceled before completion.
    onLoadCancel: source => {
      const message = `preload cancel: ${source.vid()}...`;
      console.log(`[PreLoad] ${message}`);
    },
  },
);
```


<span id="92d36f4b"></span>
## Using the preload cache

You don't need to take any additional action to use the cache. When you call `play()` with a play source, the player automatically detects if a valid cache exists for that source (matched by `vid` or `cacheKey`). If a cache is found, playback starts instantly from the cached data.

<span id="caf1b1fc"></span>
## Canceling preloading tasks

If a user's action indicates that a pending preload task is no longer needed (for example, the user swipes away from a video card), you can cancel the task to save network bandwidth and system resources.

<span id="bd74fb0d"></span>
### Canceling a specific task

Use the `taskId` to cancel a specific, ongoing task.

```TypeScript
import { cancelPreloadByTaskId } from '@byteplus/react-native-vod-player';

// `taskId` is the string returned when you first added the preload task.
cancelPreloadByTaskId(taskId);
```


<span id="d0aaf972"></span>
### Canceling all tasks

You can also cancel all currently active preload tasks at once. This is useful when the user navigates away from a screen or feature where preloading was active.

```TypeScript
import { cancelPreload } from '@byteplus/react-native-vod-player';

// Cancels all ongoing preload tasks.
cancelPreload();
```
