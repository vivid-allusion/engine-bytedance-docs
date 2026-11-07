---
title: "Android Player SDK: API details"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details"
---

<span id="TTVideoEngine"></span>
# TTVideoEngine

```java
public class com.ss.ttvideoengine.TTVideoEngine
```


The video engine. `TTVideoEngine` is the core class of the Player SDK, providing the core playback functions.

<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**static String** |[getEngineVersion](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getengineversion) |
|**static String** |[getEngineUniqueId](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getengineuniqueid) |
|**static String** |[getDeviceID](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getdeviceid) |
|**static void** |[setStrategySources](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setstrategysources) |
|**static void** |[addStrategySources](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-addstrategysources) |
|**static void** |[enableEngineStrategy](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-enableenginestrategy) |
|**static void** |[setEngineStrategyListener](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setenginestrategylistener) |
|**static TTVideoEngine** |[getPreRenderEngine](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getprerenderengine) |
|**static TTVideoEngine** |[getPreRenderEngine](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getprerenderengine) |
|**static void** |[clearAllStrategy](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-clearallstrategy) |
|**static void** |[addTask](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-addtask) |
|**static void** |[addTask](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-addtask) |
|**static void** |[cancelPreloadTask](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-cancelpreloadtask) |
|**static void** |[cancelPreloadTaskByVideoId](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-cancelpreloadtaskbyvideoid) |
|**static void** |[cancelAllPreloadTasks](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-cancelallpreloadtasks) |
|**static void** |[removeCacheFile](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-removecachefile) |
|**static void** |[forceRemoveCacheFile](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-forceremovecachefile) |
|**static DataLoaderHelper.DataLoaderCacheInfo** |[getCacheInfo](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getcacheinfo) |
|**static long** |[quickGetCacheFileSize](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-quickgetcachefilesize) |
|**static void** |[clearAllCaches](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-clearallcaches) |
|**static void** |[clearAllCaches](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-clearallcaches) |
|**static Resolution** |[findDefaultResolution](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-finddefaultresolution) |
|**static void** |[removeCacheFile](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-removecachefile) |
|**static String** |[encryptTimestamp](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-encrypttimestamp) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[setRadioMode](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setradiomode) |
|**void** |[setDisplayMode](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setdisplaymode) |
|**Bitmap** |[saveFrame](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-saveframe) |
|**void** |[snapshot](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-snapshot) |
|**boolean** |[clearSurface](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-clearsurface) |
|**void** |[openTextureSR](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-opentexturesr) |
|**void** |[setBarrageMaskUrlUseDataLoader](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setbarragemaskurlusedataloader) |
|**void** |[asyncInitSR](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-asyncinitsr) |
|**void** |[dynamicControlSR](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-dynamiccontrolsr) |
|**void** |[setSRInitConfig](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsrinitconfig) |
|**boolean** |[isplaybackUsedSR](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-isplaybackusedsr) |
|**void** |[ignoreSRResolutionLimit](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-ignoresrresolutionlimit) |
|**void** |[setMaskInfoListener](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setmaskinfolistener) |
|**void** |[setSubInfoListener](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsubinfolistener) |
|**void** |[setSubInfoCallBack](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsubinfocallback) |
|**void** |[setSubDesInfoModel](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsubdesinfomodel) |
|**void** |[setAdditionSubModel](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setadditionsubmodel) |
|**boolean** |[isSupportHDR](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-issupporthdr) |
|**boolean** |[isSupportSR](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-issupportsr) |
|**void** |[setSurface](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsurface) |
|**Surface** |[getSurface](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getsurface) |
|**void** |[setRotation](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setrotation) |
|**int** |[getRotation](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getrotation) |
|**void** |[setMirrorHorizontal](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setmirrorhorizontal) |
|**boolean** |[getMirrorHorizontal](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getmirrorhorizontal) |
|**void** |[setMirrorVertical](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setmirrorvertical) |
|**boolean** |[getMirrorVertical](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getmirrorvertical) |
|**void** |[setSurfaceHolder](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsurfaceholder) |
|**void** |[setSurfaceHolderSync](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsurfaceholdersync) |
|**void** |[setCustomHeader](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setcustomheader) |
|**void** |[setVolume](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setvolume) |
|**float** |[getMaxVolume](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getmaxvolume) |
|**float** |[getVolume](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getvolume) |
|**void** |[setIsMute](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setismute) |
|**boolean** |[isMute](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-ismute) |
|**void** |[setStartTime](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setstarttime) |
|**void** |[setVideoEngineCallback](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setvideoenginecallback) |
|**void** |[addVideoEngineCallback](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-addvideoenginecallback) |
|**void** |[removeVideoEngineCallback](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-removevideoenginecallback) |
|**void** |[setVideoInfoListener](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setvideoinfolistener) |
|**void** |[setVideoEngineInfoListener](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setvideoengineinfolistener) |
|**void** |[setDecryptionKey](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setdecryptionkey) |
|**boolean** |[isPrepared](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-isprepared) |
|**boolean** |[isReleased](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-isreleased) |
|**StrategySource** |[getStrategySource](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getstrategysource) |
|**void** |[setStrategySource](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setstrategysource) |
|**void** |[setSource](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsource) |
|**void** |[setTag](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-settag) |
|**void** |[setSubTag](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsubtag) |
|**void** |[setSubAuthToken](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setsubauthtoken) |
|**List<com.ss.ttvideoengine.model.SubInfo\>**  |[supportedSubInfoList](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-supportedsubinfolist) |
|**Resolution[]**  |[supportedResolutionTypes](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-supportedresolutiontypes) |
|**void** |[configResolution](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-configresolution) |
|**Resolution** |[getCurrentResolution](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getcurrentresolution) |
|**void** |[prepare](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-prepare) |
|**void** |[play](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-play) |
|**void** |[pause](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-pause) |
|**void** |[stop](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-stop) |
|**synchronized void** |[releaseAsync](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-releaseasync) |
|**void** |[setLooping](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setlooping) |
|**boolean** |[isLooping](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-islooping) |
|**int** |[getDuration](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getduration) |
|**int** |[getLoadedProgress](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getloadedprogress) |
|**int** |[getPlaybackState](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getplaybackstate) |
|**int** |[getLoadState](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getloadstate) |
|**boolean** |[isStarted](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-isstarted) |
|**int** |[getCurrentPlaybackTime](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getcurrentplaybacktime) |
|**int** |[getCurrentPlaybackTimeAsync](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getcurrentplaybacktimeasync) |
|**int** |[getVideoWidth](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getvideowidth) |
|**int** |[getVideoHeight](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getvideoheight) |
|**int** |[getWatchedDuration](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getwatchedduration) |
|**void** |[seekTo](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-seekto) |
|**VideoFormatInfo** |[getVideoFormatInfo](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getvideoformatinfo) |
|**void** |[setFFmpegProtocolObject](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-setffmpegprotocolobject) |
|**String** |[getTag](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-gettag) |
|**String** |[getSubTag](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getsubtag) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngine-getengineversion"></span>
### getEngineVersion

```java
public static String com.ss.ttvideoengine.TTVideoEngine.getEngineVersion()
```


Gets the SDK version.

**Returns**

The SDK version.

<span id="TTVideoEngine-getengineuniqueid"></span>
### getEngineUniqueId

```java
public static String com.ss.ttvideoengine.TTVideoEngine.getEngineUniqueId(
    Context context)
```


Gets the unique DRM(Digital Rights Management) identifier of the current device.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|context |**Context** |Android Application Context |


**Returns**

The unique DRM identifier of the current device.

**Note**

If the app is deleted and reinstalled, the DRM identifier of the device will be reset.

<span id="TTVideoEngine-getdeviceid"></span>
### getDeviceID

```java
public static String com.ss.ttvideoengine.TTVideoEngine.getDeviceID()
```


Gets the device ID.

**Returns**

The device ID.

**Note**

The device ID can be used to trace the playback records of the device on the quality platform provided by BytePlus VOD. For more information, see Endpoint tracker.

<span id="TTVideoEngine-setstrategysources"></span>
### setStrategySources

```java
public static void com.ss.ttvideoengine.TTVideoEngine.setStrategySources(
    List<StrategySource> strategySources)
```


Sets the list of playback sources for the current page.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|strategySources |**List** |The playback sources. |


**Note**

Use this method for preloading or prerendering strategies.

Calling this method will reset the current list of playback sources, which is used for setting the playback sources for the first time or when refreshing the page to display new data.

<span id="TTVideoEngine-addstrategysources"></span>
### addStrategySources

```java
public static void com.ss.ttvideoengine.TTVideoEngine.addStrategySources(
    List<StrategySource> strategySources)
```


Adds playback sources to the current list of playback sources.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|strategySources |**List** |The playback sources. |


**Note**

Use this method for preloading or prerendering strategies.

This method is suitable for scenarios that load more data.

<span id="TTVideoEngine-enableenginestrategy"></span>
### enableEngineStrategy

```java
public static void com.ss.ttvideoengine.TTVideoEngine.enableEngineStrategy(
    int type,
    int scene)
```


Enables the playback strategy. The Player SDK supports preloading and prerendering strategies.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|type |**int** |The strategy type:<br><br><br>* `STRATEGY_TYPE_PRELOAD`: The preloading strategy.<br><br>* `STRATEGY_TYPE_PRE_RENDER`: The prerendering strategy. |
|scene |**int** |The use scenario. The strategy should be used with scenarios to achieve the best result.<br><br><br>* `STRATEGY_SCENE_SMALL_VIDEO`: The short video scenario.<br><br>* `STRATEGY_SCENE_SHORT_VIDEO`: The medium\-length video scenario. |


**Note**

It is recommended to enable the strategy after a user entering the page.

<span id="TTVideoEngine-setenginestrategylistener"></span>
### setEngineStrategyListener

```java
public static void com.ss.ttvideoengine.TTVideoEngine.setEngineStrategyListener(
    EngineStrategyListener listener)
```


Sets the callback for strategy\-related events.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**EngineStrategyListener** |The callback for strategy\-related events, see [EngineStrategyListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#enginestrategylistener)。 |


<span id="TTVideoEngine-getprerenderengine"></span>
### getPreRenderEngine

```java
public static TTVideoEngine com.ss.ttvideoengine.TTVideoEngine.getPreRenderEngine(
    StrategySource source)
```


Gets the `TTVideoEngine` object that has been prerendered based on `StrategySource`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**StrategySource** |The playback source. |


**Returns**

The `TTVideoEngine` object that has been prerendered.

<span id="TTVideoEngine-getprerenderengine"></span>
### getPreRenderEngine

```java
public static TTVideoEngine com.ss.ttvideoengine.TTVideoEngine.getPreRenderEngine(
    String vid)
```


Gets the `TTVideoEngine` object that has been prerendered based on `vid`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid |**String** |The video ID. |


**Returns**

The `TTVideoEngine` object that has been prerendered.

<span id="TTVideoEngine-clearallstrategy"></span>
### clearAllStrategy

```java
public static void com.ss.ttvideoengine.TTVideoEngine.clearAllStrategy()
```


Clears all strategies and releases resources.

**Note**

Call this method when the user exits the current page or switches to another page.

<span id="TTVideoEngine-addtask"></span>
### addTask

```java
public static void com.ss.ttvideoengine.TTVideoEngine.addTask(
    PreloaderVidItem vidItem)
```


Adds a preloading task for the `Vid` playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vidItem |**PreloaderVidItem** |The preloading task for a `Vid` playback source. See [PreloaderVidItem](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-type-definitions?version=v1.0#preloaderviditem). |


<span id="TTVideoEngine-addtask"></span>
### addTask

```java
public static void com.ss.ttvideoengine.TTVideoEngine.addTask(
    PreloaderURLItem urlItem)
```


Adds a preloading task for the URL playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urlItem |**PreloaderURLItem** |The preloading task for the URL playback source. See [PreloaderURLItem](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-type-definitions?version=v1.0#preloaderurlitem). |


<span id="TTVideoEngine-cancelpreloadtask"></span>
### cancelPreloadTask

```java
public static void com.ss.ttvideoengine.TTVideoEngine.cancelPreloadTask(
    String key)
```


Cancels the preloading task based on the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |The cache key, which is the unique identifier for a URL playback source preloading task. |


<span id="TTVideoEngine-cancelpreloadtaskbyvideoid"></span>
### cancelPreloadTaskByVideoId

```java
public static void com.ss.ttvideoengine.TTVideoEngine.cancelPreloadTaskByVideoId(
    String vid)
```


Cancels the preloading task based on the video ID.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid |**String** |The video ID. |


<span id="TTVideoEngine-cancelallpreloadtasks"></span>
### cancelAllPreloadTasks

```java
public static void com.ss.ttvideoengine.TTVideoEngine.cancelAllPreloadTasks()
```


Cancels all preloading tasks.

<span id="TTVideoEngine-removecachefile"></span>
### removeCacheFile

```java
public static void com.ss.ttvideoengine.TTVideoEngine.removeCacheFile(
    String key)
```


Removes the cache file based on the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |The cache key. |


**Note**

If the cache file is being referenced, removal may fail.

<span id="TTVideoEngine-forceremovecachefile"></span>
### forceRemoveCacheFile

```java
public static void com.ss.ttvideoengine.TTVideoEngine.forceRemoveCacheFile(
    String key)
```


Forcefully removes the cache file based on the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |The cache key. |


<span id="TTVideoEngine-getcacheinfo"></span>
### getCacheInfo

```java
public static DataLoaderHelper.DataLoaderCacheInfo com.ss.ttvideoengine.TTVideoEngine.getCacheInfo(
    String key)
```


Gets the cached video information.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |The cache key. |


**Returns**

The video information.

<span id="TTVideoEngine-quickgetcachefilesize"></span>
### quickGetCacheFileSize

```java
public static long com.ss.ttvideoengine.TTVideoEngine.quickGetCacheFileSize(
    String key)
```


Gets the size of the local cached file.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |The cache key. |


**Returns**

The size of the local cached file.

<span id="TTVideoEngine-clearallcaches"></span>
### clearAllCaches

```java
public static void com.ss.ttvideoengine.TTVideoEngine.clearAllCaches()
```


Deletes the cached data.

**Note**

This method does not delete all cached data. Instead, it keeps about the last 10 or so piece of data according to the Least Recently Used (LRU) algorithm to optimize the playback experience.

<span id="TTVideoEngine-clearallcaches"></span>
### clearAllCaches

```java
public static void com.ss.ttvideoengine.TTVideoEngine.clearAllCaches(
    boolean force)
```


Deletes all the cached data.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|force |**boolean** |Whether to forcefully delete all cached data:<br><br><br>* `true`: Forcefully delete all cached data.<br><br>* `false`: Same as calling the `clearAllCaches` method, it does not delete all cached data. Instead, it keeps about the last 10 or so piece of data according to the Least Recently Used (LRU) algorithm to optimize the playback experience. |


<span id="TTVideoEngine-finddefaultresolution"></span>
### findDefaultResolution

```java
public static Resolution com.ss.ttvideoengine.TTVideoEngine.findDefaultResolution(
    VideoModel model,
    Resolution defaultResolution)
```


Gets the specified resolution.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|model |**VideoModel** |The playback source. |
|defaultResolution |**Resolution** |The resolution. Usually set this parameter as the default resolution of the application. |


**Returns**

If `defaultResolution` exists in `VideoModel`, this method returns `defaultResolution`.

If `defaultResolution` does not exist in `VideoModel`, this method returns the resolution closest to `defaultResolution`.

<span id="TTVideoEngine-removecachefile"></span>
### removeCacheFile

```java
public static void com.ss.ttvideoengine.TTVideoEngine.removeCacheFile(
    IVideoModel model)
```


Removes the local cached file.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|model |**IVideoModel** |The playback source. |


<span id="TTVideoEngine-encrypttimestamp"></span>
### encryptTimestamp

```java
public static String com.ss.ttvideoengine.TTVideoEngine.encryptTimestamp(
    Context context,
    long timestamp)
```


Encrypts the local timestamp for the private DRM encrption.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|context |**Context** |Android Application Context |
|timestamp |**long** |The timestamp to be encrypted. |


**Returns**

The encrypted timestamp.

**Note**

This timestamp is bound to the current device.

<span id="TTVideoEngine-setradiomode"></span>
### setRadioMode

```java
public void com.ss.ttvideoengine.TTVideoEngine.setRadioMode(
    boolean on)
```


Enables or disables audio\-only mode.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|on |**boolean** |Whether to enable audio\-only mode:<br><br><br>* `true`: Enable audio\-only mode.<br><br>* `false`: (Default) Disable audio\-only mode. |


<span id="TTVideoEngine-setdisplaymode"></span>
### setDisplayMode

```java
public void com.ss.ttvideoengine.TTVideoEngine.setDisplayMode(
    View disPlayView,
    int disPlayMode)
```


Sets video fill mode.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|disPlayView |**View** |The `TextureView` or `SurfaceView` that displays the video. |
|disPlayMode |**int** |Video fill mode:<br><br><br>* `TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FIT`: No distortion; maintains the aspect ratio; the video may have black bars.<br><br>* `TTVideoEngineInterface.IMAGE_LAYOUT_TO_FILL`: May cause distortion; the video fills the width and height of the view; the video is not cropped; no black bars.<br><br>* `TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FILL`: No distortion; maintains the aspect ratio; the video may be cropped; no black bars.<br><br>* `TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FILL_X`: No distortion; the video fills the width of the view and adapts the height according to the video aspect ratio; the video may be cropped; may have black bars. Does not take effect when Texture Render is enabled.<br><br>* `TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FILL_Y`: No distortion; the video fills the height of the view and adapts the width according to the video aspect ratio; the video may be cropped; may have black bars. Does not take effect when Texture Render is enabled. |


<span id="TTVideoEngine-saveframe"></span>
### saveFrame

```java
public Bitmap com.ss.ttvideoengine.TTVideoEngine.saveFrame()
```


Gets the current video frame data.

**Returns**

The current video frame data.

<span id="TTVideoEngine-snapshot"></span>
### snapshot

```java
public void com.ss.ttvideoengine.TTVideoEngine.snapshot(
    SnapshotListener)
```


Takes a snapshot.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|snapshotListener |**SnapshotListener** |The callback for snapshot\-related events. See [SnapshotListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#snapshotlistener). |


<span id="TTVideoEngine-clearsurface"></span>
### clearSurface

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.clearSurface(
    Surface surface,
    boolean async)
```


Clears the content on the `Surface`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|surface |**Surface** |The `Surface` to be cleared. |
|async |**boolean** |Whether to execute asynchronously. |


**Returns**

The result of the content clearing. If it is executed asynchronously, this method will not return `false`.

<span id="TTVideoEngine-opentexturesr"></span>
### openTextureSR

```java
public void com.ss.ttvideoengine.TTVideoEngine.openTextureSR(
    boolean useSRTexture,
    boolean open)
```


Enables or disables super resolution.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|useSRTexture |**boolean** |Whether to use Texture Render with super resolution. |
|open |**boolean** |Whether to enable super\-resolution:<br><br><br>* `true`: Enable super resolution.<br><br>* `false`: Disable super resolution. |


<span id="TTVideoEngine-setbarragemaskurlusedataloader"></span>
### setBarrageMaskUrlUseDataLoader

```java
public void com.ss.ttvideoengine.TTVideoEngine.setBarrageMaskUrlUseDataLoader(
    String barrageMaskUrl,
    String key)
```


Sets the URL of the masking bullet comments.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|barrageMaskUrl |**String** |The URL of the masking bullet comments. |
|key |**String** |The cache key. |


<span id="TTVideoEngine-asyncinitsr"></span>
### asyncInitSR

```java
public void com.ss.ttvideoengine.TTVideoEngine.asyncInitSR(
    boolean asyncInit)
```


Sets whether to initialize super resolution asynchronously.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|asyncInit |**boolean** |Whether to initialize super resolution asynchronously:<br><br><br>* `true`: Initialize super resolution asynchronously. If this parameter is set to `true`, the SDK will only enable Texture Render when super resolution is enabled.<br><br>* `false`: Initialize super resolution synchronously. |


<span id="TTVideoEngine-dynamiccontrolsr"></span>
### dynamicControlSR

```java
public void com.ss.ttvideoengine.TTVideoEngine.dynamicControlSR(
    boolean dynamicControl)
```


Enables or disables dynamic super resolution during playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|dynamicControl |**boolean** |Whether to enable dynamic super resolution during playback:<br><br><br>* `true`: Enable dynamic super resolution during playback.<br><br>* `false`: (Default) Disable dynamic super resolution during playback. |


<span id="TTVideoEngine-setsrinitconfig"></span>
### setSRInitConfig

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSRInitConfig(
    int algType,
    String strKernelBinPath,
    String strOclModuleName,
    String strDspModuleName,
    int backend,
    int scaleType,
    int poolSize)
```


Sets the super\-resolution parameters.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|algType |**int** |The super\-resolution algorithm type. Set this parameter to `5`. |
|strKernelBinPath |**String** |The local path of the core library. |
|strOclModuleName |**String** |Set this parameter to `SR`. |
|strDspModuleName |**String** |Set this parameter to `SR`. |
|backend |**int** |Set this parameter to `0`. |
|scaleType |**int** |Set this parameter to `0`, which represents 2x super\-resolution. |
|poolSize |**int** |Set this parameter to `0`. |


<span id="TTVideoEngine-isplaybackusedsr"></span>
### isplaybackUsedSR

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isplaybackUsedSR()
```


Checks if super resolution is enabled for the current playback.

**Returns**

Whether super resolution is enabled for the current playback.

<span id="TTVideoEngine-ignoresrresolutionlimit"></span>
### ignoreSRResolutionLimit

```java
public void com.ss.ttvideoengine.TTVideoEngine.ignoreSRResolutionLimit(
    boolean ignore)
```


Sets whether to ignore the resolution limit for super resolution.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|ignore |**boolean** |Whether to ignore the resolution limit:<br><br><br>* `true`: (Recommended) Ignore the resolution limit.<br><br>* `false`: Super resolution is subject to the resolution limit. |


<span id="TTVideoEngine-setmaskinfolistener"></span>
### setMaskInfoListener

```java
public void com.ss.ttvideoengine.TTVideoEngine.setMaskInfoListener(
    MaskInfoListener listener)
```


Sets the callback for masking bullet comments.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**MaskInfoListener** |The callback for masking bullet comments. See [MaskInfoListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#maskinfolistener) for details. |


<span id="TTVideoEngine-setsubinfolistener"></span>
### setSubInfoListener

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSubInfoListener(
    SubInfoListener listener)
```


Sets the callback for subtitle information.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**SubInfoListener** |The callback for subtitle information. See [SubInfoListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#subinfolistener) for details. |


<span id="TTVideoEngine-setsubinfocallback"></span>
### setSubInfoCallBack

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSubInfoCallBack(
    SubInfoSimpleCallBack callback)
```


Sets the callback for subtitles.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|callback |**SubInfoSimpleCallBack** |The callback for subtitles. See [SubInfoSimpleCallBack](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#subinfosimplecallback) for details. |


<span id="TTVideoEngine-setsubdesinfomodel"></span>
### setSubDesInfoModel

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSubDesInfoModel(
    SubDesInfoModelProvider subDesInfoModel)
```


Sets the subtitle source, including the information of multiple\-language subtitles.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subDesInfoModel |**SubDesInfoModelProvider** |The subtitle source. See [SubDesInfoModelProvider](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-type-definitions?version=v1.0#subdesinfomodelprovider) for details. |


<span id="TTVideoEngine-setadditionsubmodel"></span>
### setAdditionSubModel

```java
public void com.ss.ttvideoengine.TTVideoEngine.setAdditionSubModel(
    SubModelProvider subModel)
```


Adds a subtitle source for a different language.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subModel |**SubModelProvider** |The subtitle source for a single language. |


<span id="TTVideoEngine-issupporthdr"></span>
### isSupportHDR

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isSupportHDR()
```


Checks if the current device supports HDR playback.

**Returns**

Whether the device supports HDR playback:

`true`: The device supports HDR playback.

`false`: The device does not support HDR playback.

<span id="TTVideoEngine-issupportsr"></span>
### isSupportSR

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isSupportSR()
```


Checks if the current device supports super resolution.

**Returns**

Whether super resolution is supported:

`true`: Supported.

`false`: Not supported.

<span id="TTVideoEngine-setsurface"></span>
### setSurface

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSurface(
    Surface surface)
```


Sets the `Surface` object.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|surface |**Surface** |The `Surface` object. |


<span id="TTVideoEngine-getsurface"></span>
### getSurface

```java
public Surface com.ss.ttvideoengine.TTVideoEngine.getSurface()
```


Gets the `Surface` object.

**Returns**

The `Surface` object.

<span id="TTVideoEngine-setrotation"></span>
### setRotation

```java
public void com.ss.ttvideoengine.TTVideoEngine.setRotation(
    int rotation)
```


Sets the video rotation degree.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|rotation |**int** |The video rotation degree. Only `0`, `90`, `180`, and `270` are supported. After setting the video rotation degree, the video will rotate clockwise. |


**Note**

You need to enable Texture Render before calling this method.

<span id="TTVideoEngine-getrotation"></span>
### getRotation

```java
public int com.ss.ttvideoengine.TTVideoEngine.getRotation()
```


Gets the video rotation degree.

**Returns**

The video rotation degree.

**Notes**

You need to enable Texture Render before calling this method.

<span id="TTVideoEngine-setmirrorhorizontal"></span>
### setMirrorHorizontal

```java
public void com.ss.ttvideoengine.TTVideoEngine.setMirrorHorizontal(
    boolean isMirror)
```


Sets whether to enable horizontal mirroring.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isMirror |**boolean** |Whether to enable horizontal mirroring:<br><br><br>* `true`: Enable horizontal mirroring.<br><br>* `false`: Disable horizontal mirroring. |


**Note**

You need to enable Texture Render before calling this method.

<span id="TTVideoEngine-getmirrorhorizontal"></span>
### getMirrorHorizontal

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.getMirrorHorizontal()
```


Gets whether horizontal mirroring is enabled.

**Returns**

Whether horizontal mirroring is enabled.

**Note**

You need to enable Texture Render before calling this method.

<span id="TTVideoEngine-setmirrorvertical"></span>
### setMirrorVertical

```java
public void com.ss.ttvideoengine.TTVideoEngine.setMirrorVertical(
    boolean isMirror)
```


Sets whether to enable vertical mirroring.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isMirror |**boolean** |Whether to enable vertical mirroring:<br><br><br>* `true`: Enable vertical mirroring.<br><br>* `false`: Disable vertical mirroring. |


**Note**

You need to enable Texture Render before calling this method.

<span id="TTVideoEngine-getmirrorvertical"></span>
### getMirrorVertical

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.getMirrorVertical()
```


Gets whether vertical mirroring is enabled.

**Returns**

Whether vertical mirroring is enabled.

**Note**

You need to enable Texture Render before calling this method.

<span id="TTVideoEngine-setsurfaceholder"></span>
### setSurfaceHolder

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSurfaceHolder(
    SurfaceHolder surfaceHolder)
```


Sets the `SurfaceHolder` object.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|surfaceHolder |**SurfaceHolder** |The `SurfaceHolder` object. |


<span id="TTVideoEngine-setsurfaceholdersync"></span>
### setSurfaceHolderSync

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSurfaceHolderSync(
    SurfaceHolder surfaceHolder)
```


Synchronously sets the `SurfaceHolder` object in engine looper mode.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|surfaceHolder |**SurfaceHolder** |The `SurfaceHolder` object. |


<span id="TTVideoEngine-setcustomheader"></span>
### setCustomHeader

```java
public void com.ss.ttvideoengine.TTVideoEngine.setCustomHeader(
    String key,
    String value)
```


Sets a custom header.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |Key |
|value |**String** |Value |


**Note**

You can use this method to change the User\-Agent, for example: `engine.setCustomHeader("User-Agent", " ByteVod(Playback)");`.

<span id="TTVideoEngine-setvolume"></span>
### setVolume

```java
public void com.ss.ttvideoengine.TTVideoEngine.setVolume(
    float left,
    float right)
```


Sets the system volume.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|left |**float** |The volume of the left channel. The value range is [0, maxVolume]. |
|right |**float** |The volume of the right channel. The value range is [0, maxVolume]. |


**Note**

You can call `getMaxVolume` to get the maximum system volume.

<span id="TTVideoEngine-getmaxvolume"></span>
### getMaxVolume

```java
public float com.ss.ttvideoengine.TTVideoEngine.getMaxVolume()
```


Gets the maximum system volume.

**Returns**

The maximum system volume.

<span id="TTVideoEngine-getvolume"></span>
### getVolume

```java
public float com.ss.ttvideoengine.TTVideoEngine.getVolume()
```


Gets the current volume.

**Returns**

The current volume.

<span id="TTVideoEngine-setismute"></span>
### setIsMute

```java
public void com.ss.ttvideoengine.TTVideoEngine.setIsMute(
    boolean isMute)
```


Sets whether to mute the video.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isMute |**boolean** |Whether to mute the video:<br><br><br>* `true`: Mute the video.<br><br>* `false`: (Default) Do not mute the video. |


<span id="TTVideoEngine-ismute"></span>
### isMute

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isMute()
```


Checks whether the video is muted.

**Returns**

Whether the video is muted:

`true`: The video is muted.

`false`: The video is not muted.

<span id="TTVideoEngine-setstarttime"></span>
### setStartTime

```java
public void com.ss.ttvideoengine.TTVideoEngine.setStartTime(
    int msec)
```


Sets the start position of the playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|msec |**int** |The start position of the playback, in milliseconds. |


<span id="TTVideoEngine-setvideoenginecallback"></span>
### setVideoEngineCallback

```java
public void com.ss.ttvideoengine.TTVideoEngine.setVideoEngineCallback(
    VideoEngineCallback videoEngineCallback)
```


Sets the video engine callback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngineCallback |**VideoEngineCallback** |The video engine callback object. See [VideoEngineCallback](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#videoenginecallback) for details. |


<span id="TTVideoEngine-addvideoenginecallback"></span>
### addVideoEngineCallback

```java
public void com.ss.ttvideoengine.TTVideoEngine.addVideoEngineCallback(
    VideoEngineCallback videoEngineCallback)
```


Adds a video engine callback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngineCallback |**VideoEngineCallback** |The video engine callback object. See [VideoEngineCallback](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#videoenginecallback) for details. |


<span id="TTVideoEngine-removevideoenginecallback"></span>
### removeVideoEngineCallback

```java
public void com.ss.ttvideoengine.TTVideoEngine.removeVideoEngineCallback(
    VideoEngineCallback videoEngineCallback)
```


Removes a video engine callback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngineCallback |**VideoEngineCallback** |The video engine callback object. See [VideoEngineCallback](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#videoenginecallback) for details. |


<span id="TTVideoEngine-setvideoinfolistener"></span>
### setVideoInfoListener

```java
public void com.ss.ttvideoengine.TTVideoEngine.setVideoInfoListener(
    VideoInfoListener listener)
```


Sets the video information listener.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**VideoInfoListener** |The video information listener object. See [VideoInfoListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#videoinfolistener) for details. |


<span id="TTVideoEngine-setvideoengineinfolistener"></span>
### setVideoEngineInfoListener

```java
public void com.ss.ttvideoengine.TTVideoEngine.setVideoEngineInfoListener(
    VideoEngineInfoListener listener)
```


Sets the general listener for the player.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**VideoEngineInfoListener** |The general listener object for the player. See [VideoEngineInfoListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#videoengineinfolistener) for details. |


<span id="TTVideoEngine-setdecryptionkey"></span>
### setDecryptionKey

```java
public void com.ss.ttvideoengine.TTVideoEngine.setDecryptionKey(
    String decryptionKey)
```


Sets the decryption key for the private DRM encryption.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|decryptionKey |**String** |The decryption key. |


<span id="TTVideoEngine-isprepared"></span>
### isPrepared

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isPrepared()
```


Checks whether the player is in the `prepared` state.

**Returns**

Whether the player is in the `prepared` state, that is, whether the decoder is ready.

<span id="TTVideoEngine-isreleased"></span>
### isReleased

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isReleased()
```


Checks whether the player has been released.

**Returns**

Whether the player has been released.

<span id="TTVideoEngine-getstrategysource"></span>
### getStrategySource

```java
public StrategySource com.ss.ttvideoengine.TTVideoEngine.getStrategySource()
```


Gets the current playback source.

**Returns**

The current playback source.

<span id="TTVideoEngine-setstrategysource"></span>
### setStrategySource

```java
public void com.ss.ttvideoengine.TTVideoEngine.setStrategySource(
    StrategySource strategySource)
```


Sets the playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|strategySource |**StrategySource** |The playback source. |


<span id="TTVideoEngine-setsource"></span>
### setSource

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSource(
    Source source)
```


Sets the playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**Source** |The playback source. |


<span id="TTVideoEngine-settag"></span>
### setTag

```java
public void com.ss.ttvideoengine.TTVideoEngine.setTag(
    String tag)
```


Sets the business tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|tag |**String** |The business tag can be used to distinguish different types of audio and video within the same application (`appid`). You can divide them according to your scenario or video duration, such as immersive feed stream, short videos, or long videos. |


<span id="TTVideoEngine-setsubtag"></span>
### setSubTag

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSubTag(
    String subTag)
```


Sets the business sub\-tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subTag |**String** |The sub\-tag can be used to further distinguish different types of audio and video with the same business tag, such as whether the audio and video are encrypted. |


<span id="TTVideoEngine-setsubauthtoken"></span>
### setSubAuthToken

```java
public void com.ss.ttvideoengine.TTVideoEngine.setSubAuthToken(
    String authToken)
```


Sets the subtitle token.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|authToken |**String** |The subtitle token. |


<span id="TTVideoEngine-supportedsubinfolist"></span>
### supportedSubInfoList

```java
public List<com.ss.ttvideoengine.model.SubInfo> com.ss.ttvideoengine.TTVideoEngine.supportedSubInfoList()
```


Gets the list of all supported subtitle source objects.

**Returns**

The list of all supported subtitle source objects.

<span id="TTVideoEngine-supportedresolutiontypes"></span>
### supportedResolutionTypes

```java
public Resolution[] com.ss.ttvideoengine.TTVideoEngine.supportedResolutionTypes()
```


Gets the list of all supported resolutions.

**Returns**

The list of all supported resolutions.

<span id="TTVideoEngine-configresolution"></span>
### configResolution

```java
public void com.ss.ttvideoengine.TTVideoEngine.configResolution(
    Resolution resolution)
```


Switches to the specified resolution.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolution |**Resolution** |The resolution to switch to. |


<span id="TTVideoEngine-getcurrentresolution"></span>
### getCurrentResolution

```java
public Resolution com.ss.ttvideoengine.TTVideoEngine.getCurrentResolution()
```


Gets the current resolution.

**Returns**

The current resolution.

<span id="TTVideoEngine-prepare"></span>
### prepare

```java
public void com.ss.ttvideoengine.TTVideoEngine.prepare()
```


Prepares for playback.

**Note**

This method is used for the pre\-rendering strategy. After setting the playback source, you need to call this method. The SDK will render the first frame of the video but will not start playing immediately. After rendering the first frame, the SDK triggers the [onReadyForDisplay](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onreadyfordisplay) callback.

<span id="TTVideoEngine-play"></span>
### play

```java
public void com.ss.ttvideoengine.TTVideoEngine.play()
```


Starts playback.

<span id="TTVideoEngine-pause"></span>
### pause

```java
public void com.ss.ttvideoengine.TTVideoEngine.pause()
```


Pauses playback.

<span id="TTVideoEngine-stop"></span>
### stop

```java
public void com.ss.ttvideoengine.TTVideoEngine.stop()
```


Stops playback.

<span id="TTVideoEngine-releaseasync"></span>
### releaseAsync

```java
public synchronized void com.ss.ttvideoengine.TTVideoEngine.releaseAsync()
```


Asynchronously releases the player.

<span id="TTVideoEngine-setlooping"></span>
### setLooping

```java
public void com.ss.ttvideoengine.TTVideoEngine.setLooping(
    boolean looping)
```


Sets whether to enable looping playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|looping |**boolean** |Whether to enable looping playback. |


<span id="TTVideoEngine-islooping"></span>
### isLooping

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isLooping()
```


Checks if looping playback is enabled.

**Returns**

Whether looping playback is enabled.

<span id="TTVideoEngine-getduration"></span>
### getDuration

```java
public int com.ss.ttvideoengine.TTVideoEngine.getDuration()
```


Gets the total duration of the video.

**Returns**

The total duration of the video in milliseconds.

<span id="TTVideoEngine-getloadedprogress"></span>
### getLoadedProgress

```java
public int com.ss.ttvideoengine.TTVideoEngine.getLoadedProgress()
```


Gets the video loading progress.

**Returns**

The video loading progress. The value ranges from 0 to 100.

<span id="TTVideoEngine-getplaybackstate"></span>
### getPlaybackState

```java
public int com.ss.ttvideoengine.TTVideoEngine.getPlaybackState()
```


Gets the current playback state.

**Returns**

The current playback state:

`TTVideoEngine.PLAYBACK_STATE_STOPPED`: Playback stopped.

`TTVideoEngine.PLAYBACK_STATE_PLAYING`: Playback in progress.

`TTVideoEngine.PLAYBACK_STATE_PAUSED`: Playback paused.

`TTVideoEngine.PLAYBACK_STATE_ERROR`: Playback error.

<span id="TTVideoEngine-getloadstate"></span>
### getLoadState

```java
public int com.ss.ttvideoengine.TTVideoEngine.getLoadState()
```


**Returns**

The current load state of the player:

`TTVideoEngine.LOAD_STATE_UNKNOWN`: Initial state.

`TTVideoEngine.LOAD_STATE_PLAYABLE`: Loading completed and ready to play.

`TTVideoEngine.LOAD_STATE_STALLED`: Loading in progress and buffering.

`TTVideoEngine.LOAD_STATE_ERROR`: Loading error.

<span id="TTVideoEngine-isstarted"></span>
### isStarted

```java
public boolean com.ss.ttvideoengine.TTVideoEngine.isStarted()
```


Checks whether the player has started playing.

**Returns**

Whether the player has started playing.

**Note**

After calling `play`, the returned value of `isStarted` is `true`.

After calling `pause`, the returned value of `isStarted` is `false`.

<span id="TTVideoEngine-getcurrentplaybacktime"></span>
### getCurrentPlaybackTime

```java
public int com.ss.ttvideoengine.TTVideoEngine.getCurrentPlaybackTime()
```


Gets the current playback position.

**Returns**

The current playback position in milliseconds.

<span id="TTVideoEngine-getcurrentplaybacktimeasync"></span>
### getCurrentPlaybackTimeAsync

```java
public int com.ss.ttvideoengine.TTVideoEngine.getCurrentPlaybackTimeAsync()
```


Gets the current playback position (less accurate).

**Returns**

The current playback progress in milliseconds.

**Note**

The playback position returned by this method is the same as the one returned in the [onCurrentPlaybackTimeUpdate](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-oncurrentplaybacktimeupdate) callback.

This method takes less time than [getCurrentPlaybackTime](https://docs.byteplus.com/en/docs/25/7957#TTVideoEngine-getcurrentplaybacktime).

<span id="TTVideoEngine-getvideowidth"></span>
### getVideoWidth

```java
public int com.ss.ttvideoengine.TTVideoEngine.getVideoWidth()
```


Gets the video width.

**Returns**

The video width.

<span id="TTVideoEngine-getvideoheight"></span>
### getVideoHeight

```java
public int com.ss.ttvideoengine.TTVideoEngine.getVideoHeight()
```


Gets the video height.

**Returns**

The video height.

<span id="TTVideoEngine-getwatchedduration"></span>
### getWatchedDuration

```java
public int com.ss.ttvideoengine.TTVideoEngine.getWatchedDuration()
```


Gets the accumulated playback duration.

**Returns**

The accumulated playback duration in milliseconds.

**Note**

Suppose you are currently watching a video, first watching up to the 10th second, then going back to the 5th second, and then watching up to the 10th second again. At this point, the accumulated playback duration is 15 seconds.

<span id="TTVideoEngine-seekto"></span>
### seekTo

```java
public void com.ss.ttvideoengine.TTVideoEngine.seekTo(
    int msec,
    SeekCompletionListener listener)
```


Seeks to the specified position for playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|msec |**int** |The position to seek to in milliseconds. |
|listener |**SeekCompletionListener** |The seek completion listener. See [SeekCompletionListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#seekcompletionlistener) for details. |


<span id="TTVideoEngine-getvideoformatinfo"></span>
### getVideoFormatInfo

```java
public VideoFormatInfo com.ss.ttvideoengine.TTVideoEngine.getVideoFormatInfo()
```


Gets the information of the video that is being played.

**Returns**

The video information of the video that is being played. See [VideoFormatInfo](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-type-definitions?version=v1.0#videoformatinfo) for details.

<span id="TTVideoEngine-setffmpegprotocolobject"></span>
### setFFmpegProtocolObject

```java
public void com.ss.ttvideoengine.TTVideoEngine.setFFmpegProtocolObject(
    TTVideoEngineFFmpegProtocol obj)
```


Sets the `TTVideoEngineFFmpegProtocol` object for supporting private FFmpeg encryption protocols.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|obj |**TTVideoEngineFFmpegProtocol** |The `TTVideoEngineFFmpegProtocol` object. |


<span id="TTVideoEngine-gettag"></span>
### getTag

```java
public String com.ss.ttvideoengine.TTVideoEngine.getTag()
```


Gets the business tag.

**Returns**

The business tag.

<span id="TTVideoEngine-getsubtag"></span>
### getSubTag

```java
public String com.ss.ttvideoengine.TTVideoEngine.getSubTag()
```


Gets the business sub\-tag.

**Returns**

The business sub\-tag.

<span id="Downloader"></span>
# Downloader

```java
public class com.ss.ttvideoengine.download.Downloader
```


The downloader class, which can be used for managing downloading tasks.

<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**static Downloader** |[getInstance](https://docs.byteplus.com/en/docs/25/7957#Downloader-getinstance) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[loadAllTasks](https://docs.byteplus.com/en/docs/25/7957#Downloader-loadalltasks) |
|**DownloadURLTask** |[urlTask](https://docs.byteplus.com/en/docs/25/7957#Downloader-urltask) |
|**DownloadVidTask** |[vidTask](https://docs.byteplus.com/en/docs/25/7957#Downloader-vidtask) |
|**void** |[setListener](https://docs.byteplus.com/en/docs/25/7957#Downloader-setlistener) |
|**IDownloaderListener** |[getListener](https://docs.byteplus.com/en/docs/25/7957#Downloader-getlistener) |
|**void** |[setMaxDownloadOperationCount](https://docs.byteplus.com/en/docs/25/7957#Downloader-setmaxdownloadoperationcount) |
|**long** |[getMaxDownloadOperationCount](https://docs.byteplus.com/en/docs/25/7957#Downloader-getmaxdownloadoperationcount) |
|**void** |[setLimitFreeDiskSize](https://docs.byteplus.com/en/docs/25/7957#Downloader-setlimitfreedisksize) |
|**long** |[getLimitFreeDiskSize](https://docs.byteplus.com/en/docs/25/7957#Downloader-getlimitfreedisksize) |
|**void** |[resumeAllTasks](https://docs.byteplus.com/en/docs/25/7957#Downloader-resumealltasks) |
|**void** |[suspendAllTasks](https://docs.byteplus.com/en/docs/25/7957#Downloader-suspendalltasks) |
|**void** |[invalidateAndCancelAllTasks](https://docs.byteplus.com/en/docs/25/7957#Downloader-invalidateandcancelalltasks) |


<span id="Function details"></span>
## Function details

<span id="Downloader-getinstance"></span>
### getInstance

```java
public static Downloader com.ss.ttvideoengine.download.Downloader.getInstance()
```


Gets the instance of the downloading task manager.

**Returns**

An instance of `Downloader`.

<span id="Downloader-loadalltasks"></span>
### loadAllTasks

```java
public void com.ss.ttvideoengine.download.Downloader.loadAllTasks(
    Context context)
```


Gets all downloading tasks, including completed and uncompleted.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|context |**Context** |Android Application Context |


**Note**

Call this method to get the list of completed and uncompleted downloading tasks when the user re\-enters the app after exiting.

Call this method after the SDK initialization. After this method is executed, the SDK triggers the [downloaderDidLoadAllTask](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#IDownloaderListener-downloaderdidloadalltask) callback.

<span id="Downloader-urltask"></span>
### urlTask

```java
public DownloadURLTask com.ss.ttvideoengine.download.Downloader.urlTask(
    String[] urls,
    String key,
    @Nullable String videoId)
```


Creates a URL downloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urls |**String[]**  |The URLs from which the SDK downloads video. Supports primary and backup URLs. |
|key |**String** |The unique identifier for a URL downloading task. |
|videoId | **@Nullable String** |The video ID. |


**Returns**

An instance of [DownloadURLTask](https://docs.byteplus.com/en/docs/25/7957#downloadurltask).

<span id="Downloader-vidtask"></span>
### vidTask

```java
public DownloadVidTask com.ss.ttvideoengine.download.Downloader.vidTask(
    String videoId,
    Resolution resolution,
    String authToken)
```


Creates a VID downloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoId |**String** |The video ID. |
|resolution |**Resolution** |The video resolution. |
|authToken |**String** |The video playback token. |


**Returns**

An instance of [DownloadVidTask](https://docs.byteplus.com/en/docs/25/7957#downloadvidtask).

<span id="Downloader-setlistener"></span>
### setListener

```java
public void com.ss.ttvideoengine.download.Downloader.setListener(
    IDownloaderListener listener)
```


Sets the download callback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**IDownloaderListener** |The download callback object. See [IDownloaderListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#idownloaderlistener) for details. |


<span id="Downloader-getlistener"></span>
### getListener

```java
public IDownloaderListener com.ss.ttvideoengine.download.Downloader.getListener()
```


Gets the download callback.

**Returns**

The download callback object.

<span id="Downloader-setmaxdownloadoperationcount"></span>
### setMaxDownloadOperationCount

```java
public void com.ss.ttvideoengine.download.Downloader.setMaxDownloadOperationCount(
    long maxDownloadOperationCount)
```


Sets the maximum number of downloading tasks.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|maxDownloadOperationCount |**long** |The maximum number of downloading tasks. The default value is 1. |


<span id="Downloader-getmaxdownloadoperationcount"></span>
### getMaxDownloadOperationCount

```java
public long com.ss.ttvideoengine.download.Downloader.getMaxDownloadOperationCount()
```


Gets the maximum number of downloading tasks.

**Returns**

The maximum number of downloading tasks.

<span id="Downloader-setlimitfreedisksize"></span>
### setLimitFreeDiskSize

```java
public void com.ss.ttvideoengine.download.Downloader.setLimitFreeDiskSize(
    long limitFreeDiskSize)
```


Sets the limit on remaining disk size for caching.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|limitFreeDiskSize |**long** |The limit of remaining disk size for caching. The unit is bytes. The default value is 1024 \* 1024 \* 1024 \* 1, which represents 1 GB. If the remaining disk size is less than 1 GB, the `ERROR_CODE_DOWNLOAD_DISK_FULL` error will be returned. |


<span id="Downloader-getlimitfreedisksize"></span>
### getLimitFreeDiskSize

```java
public long com.ss.ttvideoengine.download.Downloader.getLimitFreeDiskSize()
```


Gets the limit on remaining disk size for caching.

**Returns**

The limit on remaining disk size for caching.

<span id="Downloader-resumealltasks"></span>
### resumeAllTasks

```java
public void com.ss.ttvideoengine.download.Downloader.resumeAllTasks()
```


Starts or resumes all downloading tasks.

<span id="Downloader-suspendalltasks"></span>
### suspendAllTasks

```java
public void com.ss.ttvideoengine.download.Downloader.suspendAllTasks()
```


Suspends all downloading tasks.

<span id="Downloader-invalidateandcancelalltasks"></span>
### invalidateAndCancelAllTasks

```java
public void com.ss.ttvideoengine.download.Downloader.invalidateAndCancelAllTasks()
```


Deletes all downloading tasks.

<span id="DownloadTask"></span>
# DownloadTask

```java
public class com.ss.ttvideoengine.download.DownloadTask
```


The class of a downloading task.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**MediaType** |[getMediaType](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-getmediatype) |
| **@Nullable String** |[getAvailableLocalFilePath](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-getavailablelocalfilepath) |
|**long** |[getBytesExpectedToReceive](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-getbytesexpectedtoreceive) |
|**long** |[getBytesReceived](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-getbytesreceived) |
|**int** |[getState](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-getstate) |
|**String** |[getVideoId](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-getvideoid) |
|**void** |[invalidateAndCancel](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-invalidateandcancel) |
|**void** |[suspend](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-suspend) |
|**void** |[resume](https://docs.byteplus.com/en/docs/25/7957#DownloadTask-resume) |


<span id="Function details"></span>
## Function details

<span id="DownloadTask-getmediatype"></span>
### getMediaType

```java
public MediaType com.ss.ttvideoengine.download.DownloadTask.getMediaType()
```


Gets the media type.

**Returns**

The media type.

**Note**

If the media type is `M3U8`, the progress will be in percentage instead of the actual received size or the media size.

<span id="DownloadTask-getavailablelocalfilepath"></span>
### getAvailableLocalFilePath

```java
@Nullable public String com.ss.ttvideoengine.download.DownloadTask.getAvailableLocalFilePath()
```


Gets the available local path.

**Returns**

The available local path.

<span id="DownloadTask-getbytesexpectedtoreceive"></span>
### getBytesExpectedToReceive

```java
public long com.ss.ttvideoengine.download.DownloadTask.getBytesExpectedToReceive()
```


Gets the number of bytes expected to receive.

**Returns**

The number of bytes expected to receive.

<span id="DownloadTask-getbytesreceived"></span>
### getBytesReceived

```java
public long com.ss.ttvideoengine.download.DownloadTask.getBytesReceived()
```


Gets the number of bytes received.

**Returns**

The number of bytes received.

<span id="DownloadTask-getstate"></span>
### getState

```java
public int com.ss.ttvideoengine.download.DownloadTask.getState()
```


Gets the state of the downloading task.

**Returns**

The state of the downloading task:

`DOWNLOAD_TASK_STATE_INIT`: Initialized.

`DOWNLOAD_TASK_STATE_WAITING`: Waiting.

`DOWNLOAD_TASK_STATE_RUNNING`: Running.

`DOWNLOAD_TASK_STATE_SUSPENDED`: Suspended.

`DOWNLOAD_TASK_STATE_CANCELING`: Canceling.

`DOWNLOAD_TASK_STATE_COMPLETED`: Completed.

<span id="DownloadTask-getvideoid"></span>
### getVideoId

```java
public String com.ss.ttvideoengine.download.DownloadTask.getVideoId()
```


Gets the video ID associated with the downloading task.

**Returns**

The video ID.

<span id="DownloadTask-invalidateandcancel"></span>
### invalidateAndCancel

```java
public void com.ss.ttvideoengine.download.DownloadTask.invalidateAndCancel()
```


Deletes a downloading task.

<span id="DownloadTask-suspend"></span>
### suspend

```java
public void com.ss.ttvideoengine.download.DownloadTask.suspend()
```


Suspends a downloading task.

<span id="DownloadTask-resume"></span>
### resume

```java
public void com.ss.ttvideoengine.download.DownloadTask.resume()
```


Starts or resumes a downloading task.

<span id="DownloadURLTask"></span>
# DownloadURLTask

```java
public class com.ss.ttvideoengine.download.DownloadURLTask
```


The class of a URL downloading task.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[getVideoId](https://docs.byteplus.com/en/docs/25/7957#DownloadURLTask-getvideoid) |
|**void** |[suspend](https://docs.byteplus.com/en/docs/25/7957#DownloadURLTask-suspend) |
|**void** |[resume](https://docs.byteplus.com/en/docs/25/7957#DownloadURLTask-resume) |


<span id="Function details"></span>
## Function details

<span id="DownloadURLTask-getvideoid"></span>
### getVideoId

```java
public String com.ss.ttvideoengine.download.DownloadURLTask.getVideoId()
```


Gets the video ID.

**Returns**

The video ID, which may be empty.

<span id="DownloadURLTask-suspend"></span>
### suspend

```java
public void com.ss.ttvideoengine.download.DownloadURLTask.suspend()
```


Suspends the downloading task.

<span id="DownloadURLTask-resume"></span>
### resume

```java
public void com.ss.ttvideoengine.download.DownloadURLTask.resume()
```


Resumes the downloading task.

<span id="DownloadVidTask"></span>
# DownloadVidTask

```java
public class com.ss.ttvideoengine.download.DownloadVidTask
```


The class of a Vid downloading task.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[getVideoId](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-getvideoid) |
|**IDownloadVidTaskListener** |[getFetchListener](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-getfetchlistener) |
|**VideoModel** |[getVideoModel](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-getvideomodel) |
|**void** |[setVideoModel](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-setvideomodel) |
|**boolean** |[isBaseDashEnable](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-isbasedashenable) |
|**boolean** |[ish265Enable](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-ish265enable) |
|**Resolution** |[getCurrentResolution](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-getcurrentresolution) |
|**void** |[invalidateAndCancel](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-invalidateandcancel) |
|**void** |[suspend](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-suspend) |
|**void** |[resume](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-resume) |
| **@Nullable @Override String** |[getAvailableLocalFilePath](https://docs.byteplus.com/en/docs/25/7957#DownloadVidTask-getavailablelocalfilepath) |


<span id="Function details"></span>
## Function details

<span id="DownloadVidTask-getvideoid"></span>
### getVideoId

```java
public String com.ss.ttvideoengine.download.DownloadVidTask.getVideoId()
```


Gets the video ID.

**Returns**

The video ID.

<span id="DownloadVidTask-getfetchlistener"></span>
### getFetchListener

```java
public IDownloadVidTaskListener com.ss.ttvideoengine.download.DownloadVidTask.getFetchListener()
```


Gets the video information listener.

**Returns**

The video information listener.

<span id="DownloadVidTask-getvideomodel"></span>
### getVideoModel

```java
public VideoModel com.ss.ttvideoengine.download.DownloadVidTask.getVideoModel()
```


Gets the video model for video information.

**Returns**

The video model for video information.

<span id="DownloadVidTask-setvideomodel"></span>
### setVideoModel

```java
public void com.ss.ttvideoengine.download.DownloadVidTask.setVideoModel(
    VideoModel videoModel)
```


Sets the video model.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoModel |**VideoModel** |The video model. |


<span id="DownloadVidTask-isbasedashenable"></span>
### isBaseDashEnable

```java
public boolean com.ss.ttvideoengine.download.DownloadVidTask.isBaseDashEnable()
```


Checks whether DASH is enabled.

**Returns**

Whether DASH is enabled.

<span id="DownloadVidTask-ish265enable"></span>
### ish265Enable

```java
public boolean com.ss.ttvideoengine.download.DownloadVidTask.ish265Enable()
```


Checks whether the codec is H.265.

**Returns**

Whether the codec is H.265.

<span id="DownloadVidTask-getcurrentresolution"></span>
### getCurrentResolution

```java
public Resolution com.ss.ttvideoengine.download.DownloadVidTask.getCurrentResolution()
```


Gets the current resolution.

**Returns**

The current resolution.

<span id="DownloadVidTask-invalidateandcancel"></span>
### invalidateAndCancel

```java
public void com.ss.ttvideoengine.download.DownloadVidTask.invalidateAndCancel()
```


Deletes the Vid downloading task.

<span id="DownloadVidTask-suspend"></span>
### suspend

```java
public void com.ss.ttvideoengine.download.DownloadVidTask.suspend()
```


Suspends the downloading task.

<span id="DownloadVidTask-resume"></span>
### resume

```java
public void com.ss.ttvideoengine.download.DownloadVidTask.resume()
```


Resumes the downloading task.

<span id="DownloadVidTask-getavailablelocalfilepath"></span>
### getAvailableLocalFilePath

```java
@Nullable @Override public String com.ss.ttvideoengine.download.DownloadVidTask.getAvailableLocalFilePath()
```


Gets the available local path.

**Returns**

The available local path.
