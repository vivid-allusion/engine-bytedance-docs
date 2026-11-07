---
title: "Android Player SDK: Custom preloading"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-custom-preloading-android"
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


<div data-tips="true" data-tips-type="tip">To help you quickly build a short video scenario, the Player SDK provides two best strategies: the <strong>preloading strategy</strong> and <strong>pre\-rendering strategy</strong>. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-android-player-short-video-best-practices">Android Player SDK: Best practices for short video scenarios</a>.</div>


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

```Java
public static DirectUrlSource createDirectUrlSource() {
    final String vid = "video id";
    final String url = "http://www.example.com/h264.mp4";
    final String cacheKey = TTVideoEngine.computeMD5(url); 
    DirectUrlSource directUrlSource = new DirectUrlSource.Builder()
            .setVid(vid)
            .addItem(new DirectUrlSource.UrlItem.Builder()
                    .setUrl(url)
                    .setCacheKey(cacheKey)
                    .build())
            .build();
    return directUrlSource;
}
```


<span id="5a0439a5"></span>
### Add preloading task

```Java
public static void preloadUrlSource() {
    // Step 1: Construct the playback source
    final DirectUrlSource source = createDirectUrlSource();
    final long preloadSize = 800 * 1024; // Preload size: 800K
    // Step 2: Construct the preload item
    final PreloaderURLItem preloadItem = new PreloaderURLItem(source, preloadSize);
    preloadItem.setCallBackListener(new IPreLoaderItemCallBackListener() {
        @Override
        public void preloadItemInfo(PreLoaderItemCallBackInfo info) {
            if (info == null) return;
            final int key = info.getKey();
            switch (key) {
                case PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_SUCCEED: {
                    // Preload successful
                    DataLoaderHelper.DataLoaderTaskProgressInfo cacheInfo = info.preloadDataInfo;
                    if (cacheInfo == null) return;
                    String vid = cacheInfo.mVideoId; // Input vid
                    String cacheKey = cacheInfo.mKey; // File hash of the preloaded video
                    String cachePath = cacheInfo.mLocalFilePath; // Cached video file path
                    long mediaSize = cacheInfo.mMediaSize; // Total size of the cached video file
                    long cachedSize = cacheInfo.mCacheSizeFromZero; // Cached size
                    Log.d("VideoPlay", "[preload] result success."
                            + " vid = " + vid
                            + ", cacheKey = " + cacheKey
                            + ", mediaSize = " + mediaSize
                            + ", cachedSize = " + cachedSize);
                    break;
                }
                case PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_FAIL: {
                    // Preload failed
                    Log.d("VideoPlay", "[preload] result failed."
                            + " vid = " + source.vid()
                            + ", error = " + info.preloadError);
                    break;
                }
                case PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_CANCEL: {
                    // Preload canceled
                    Log.d("VideoPlay", "[preload] result canceled."
                            + " vid = " + source.vid());
                    break;
                }
                default: {
                    break;
                }
            }
        }
    });
    // Step 3: Add the preload task
    TTVideoEngine.addTask(preloadItem);
}
```


<span id="462a2f68"></span>
### Cancel preloading task

Cancelling a task will affect tasks that have not started as well as ongoing download tasks. It will not affect completed tasks. See the following sample code:

```Java
// Cancel a single preload task
// The cacheKey is the one passed when constructing the DirectUrlSource playback source
TTVideoEngine.cancelPreloadTask(cacheKey);

// Cancel all preload tasks
TTVideoEngine.cancelAllPreloadTasks();
```


<span id="4e277ec7"></span>
## Custom preloading in Vid mode

<span id="925f2832"></span>
### Construct playback source

Preloading and playback use the same playback source structure. To ensure that playback can hit the preloading cache, the `vid`, `playAuthToken`, `encodeType`, and `resolution` used in the playback source constructed for preloading and playback must be the same.

```Java
private static VidPlayAuthTokenSource createVidSource() {
    final String videoId = "your video id"; // Issued by the application server
    final String playAuthToken = "your video id's play auth token"; // Issued by the application server
    final String encodeType = Source.EncodeType.H264;
    // final String encodeType = Source.EncodeType.h265;
    // final String encodeType = Source.EncodeType.h266;
    final Resolution resolution = Resolution.High; // Initial playback/preload resolution

    VidPlayAuthTokenSource vidSource = new VidPlayAuthTokenSource.Builder()
            .setVid(videoId)
            .setPlayAuthToken(playAuthToken)
            .setEncodeType(encodeType) // Set codec type (h264, h265, h266). If not specified, default value h264 will be used.
            .setResolution(resolution)
            .build();
    return vidSource;
}
```


<span id="a95b89e9"></span>
### Add preloading task

```Java
public static void preloadVidSource() {
    // Step 1: Construct the playback source
    final VidPlayAuthTokenSource source = createVidSource();
    final long preloadSize = 800 * 1024; // Preload size: 800K
    // Step 2: Construct the preload item
    final PreloaderVidItem preloadItem = new PreloaderVidItem(source, preloadSize);
    preloadItem.setCallBackListener(new IPreLoaderItemCallBackListener() {
        @Override
        public void preloadItemInfo(PreLoaderItemCallBackInfo info) {
            if (info == null) return;
            final int key = info.getKey();
            switch (key) {
                case PreLoaderItemCallBackInfo.KEY_IS_FETCH_END_VIDEOMODEL: {
                    VideoModel videoModel = info.fetchVideoModel;
                    if (videoModel == null) return;
                    // VideoModel fetched successfully using the getPlayInfo interface
                    Log.d("VideoPlay", "[preload] preloadItemInfo videoModel fetched."
                            + " vid = " + source.vid()
                            + ", resolution = " + source.resolution()
                            + ", all = " + Arrays.toString(videoModel.getSupportResolutions()));
                    break;
                }
                case PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_SUCCEED: {
                    // Preload successful
                    DataLoaderHelper.DataLoaderTaskProgressInfo cacheInfo = info.preloadDataInfo;
                    if (cacheInfo != null) {
                        String vid = cacheInfo.mVideoId; // Input video id
                        Resolution resolution = cacheInfo.mResolution; // Resolution of the preloaded video file
                        String cacheKey = cacheInfo.mKey; // File hash of the preloaded video
                        String cachePath = cacheInfo.mLocalFilePath; // Cached video file path
                        long mediaSize = cacheInfo.mMediaSize; // Total size of the cached video file
                        long cachedSize = cacheInfo.mCacheSizeFromZero; // Cached size

                        Log.d("VideoPlay", "[preload] result success."
                                + " vid = " + vid
                                + ", resolution = " + resolution
                                + ", cacheKey = " + cacheKey
                                + ", mediaSize = " + mediaSize
                                + ", cachedSize = " + cachedSize);
                    }
                    break;
                }
                case PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_FAIL: {
                    // Preload failed
                    Log.d("VideoPlay", "[preload] result failed."
                            + " error = " + info.preloadError);
                    break;
                }
                case PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_CANCEL: {
                    // Preload canceled
                    Log.d("VideoPlay", "[preload] result canceled.");
                    break;
                }
                default: {
                    break;
                }
            }
        }
    });    
    // Step 3: Add the preload task
    TTVideoEngine.addTask(preloadItem);
}
```


<span id="6dde71b2"></span>
### Cancel preloading task

Cancelling a task will affect tasks that have not started as well as ongoing download tasks. It will not affect completed tasks. See the following sample code:

```Java
// Cancel a single preload task by videoId
TTVideoEngine.cancelPreloadTaskByVideoId(source.vid());

// Cancel all preload tasks
TTVideoEngine.cancelAllPreloadTasks();
```


<span id="2e78a822"></span>
## Verify hit for preloading

Confirm a hit for preloading by monitoring the player callback. See the following sample code:

```Java
// Set listener for TTVideoEngine instance
ttVideoEngine.setVideoEngineInfoListener(new VideoEngineInfoListener() {
    @Override
    public void onVideoEngineInfos(VideoEngineInfos videoEngineInfos) {
        if (videoEngineInfos == null) {
            return;
        }
          
        if (videoEngineInfos.getKey().equals(USING_MDL_HIT_CACHE_SIZE)) {
            // Check if the cache is hit during playback
            String taskKey = videoEngineInfos.getUsingMDLPlayTaskKey(); // Key information used
            long cacheSize = videoEngineInfos.getUsingMDLHitCacheSize(); // Size of the cached file that is hit
            
            // cacheSize > 0 indicates cache hit
            // cacheSize = 0 indicates cache miss. Please check if the preload task is successful. If using vid, check if the playback and preload resolutions are consistent.
        }
    }
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The player supports simultaneous download and playback by default. If a video is playing for the first time, the hit cache is preloaded with downloaded data. The second playback may be a cache of the first playback.</div>


* <div data-tips="true" data-tips-type="tip">If you want to test the hit rate of the preloaded cache, make sure that each video is playing for the first time. We recommend testing this at first installation.</div>



<span id="d629e4e4"></span>
## Set preloading task concurrency

See the following sample code:

```Java
// Set the concurrency of preload tasks, default value is 1, which means preload tasks are executed sequentially
TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_PARALLEL_NUM, 1);
```
