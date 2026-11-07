---
title: "Android Player SDK: Best practices for short video scenarios"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-short-video-best-practices"
---

This article introduces how to build short video scenarios through the Android Player SDK, to achieve the so\-called "zero first frame."

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

```Java
final String vid = "YOUR_VIDEO_ID"; // Video ID provided by the appServer
final String playAuthToken = "YOUR_PLAYAUTHTOKEN"; // Play Auth Token provided by the appServer

final int encodeType = TTVideoEngine.CODEC_TYPE_H264;

// final int encodeType = TTVideoEngine.CODEC_TYPE_h265;
// final int encodeType = TTVideoEngine.CODEC_TYPE_h266;
// 1. Assemble Vid playback source
StrategySource vidSource = new VidPlayAuthTokenSource.Builder()
        .setVid(vid)
        .setPlayAuthToken(playAuthToken)
        .setEncodeType(encodeType)
        // Set the starting playback resolution, here it is set to 480P. If not provided, the default value of 360P will be used.
        .setResolution(Resolution.High)
        .build();
// 2. Set the playback source
ttVideoEngine.setStrategySource(vidSource);
// 3. Play
ttVideoEngine.play()
```


<span id="ef7ea020"></span>
### Method 2: Set Url playback source

See the sample code below to set a DirectUrl playback source. The `url`, `vid`, and `cacheKey` are all required parameters. Here,


* `vid`: Video ID. You can use the Vid or the Vid's MD5 value.

* `cacheKey`: Cache key, the unique identifier of the URL. Each video may have multiple URLs with different definitions, with each URL corresponding to one `cacheKey`, but multiple URLs will correspond to the same video ID. You can use the unchanging part of the URL for MD5 operations, using the MD5 value as a `cacheKey`. For example, in `https://www.xxx.com/xxx/x/number`, the part before `"number"` is unchanging.


```java
final String vid = "YOUR_VIDEO_ID"; // Replace with your own video ID
final String url = "http://www.example.com/h264.mp4"; // Replace with your own video URL
final String cacheKey = TTVideoEngine.computeMD5(h264Url);

// 1. Assemble the playback source
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(
                new DirectUrlSource.UrlItem.Builder()
                        .setEncodeType(TTVideoEngine.CODEC_TYPE_H264)
                        .setUrl(url)
                        .setCacheKey(cacheKey)
                        .build())
        .build();
       
// 2. Set the playback source
ttVideoEngine.setStrategySource(directUrlSource);
// 3. Play
ttVideoEngine.play()
```


<span id="166886ef"></span>
## Use preloading strategy

To implement the preloading strategy, pass the video playlist into the SDK as a preloading source. Based on the playlist you provide, the SDK will preemptively download the content of the next video while the current video is playing. In this process, the SDK will automatically manage the preloading timing and configuration based on the current playback status, such as the preloading concurrency and data size.

The specific steps for accessing the preloading strategy are as follows:


1. Call `enableEngineStrategy` to enable the preloading strategy.

2. Set the preloading source with suitable timing:

   1. When the playback source data is first loaded or in a scenario of refreshing the page to display new data, call `setStrategySources`.

   2. In a scenario of loading more data, call `addStrategySources`.


The sample code for using the preloading strategy is as follows:

```Java
// 1. Enable global preload strategy, must be called on the main thread
TTVideoEngine.enableEngineStrategy(STRATEGY_TYPE_PRELOAD, STRATEGY_SCENE_SMALL_VIDEO);

List sources = new ArrayList<>();
// 2. Reset the video playback list, called when loading for the first time or refreshing the list
TTVideoEngine.setStrategySources(sources);
// When there is new content added to the playlist (e.g., loading more data by scrolling up), you can use this interface to add data to the video playback list.
// It will accumulate after the list set to the SDK previously.
// TTVideoEngine.addStrategySources(sources);

// 3. Set the video source to start playback, refer to the "Setting Playback Source" section above
ttVideoEngine.setStrategySource(strategySource);
ttVideoEngine.play()
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


1. Call `enableEngineStrategy` to globally enable the pre\-rendering strategy. In addition, it is recommended to call `enableReleasePreRenderEngineInstanceByLRU` to enable the pre\-rendering engine release strategy for release based on the LRU (Least Recently Used) mechanism.

2. Set the pre\-rendering source with suitable timing:

   1. When the playback source data is first loaded or in a scenario of dragging down to refresh the page and show new data, call `setStrategySources` to reset the playlist.

   2. In a scenario of swiping up to load more data, call `addStrategySources` to add data to the playlist.

3. Call `setEngineStrategyListener` to set the pre\-rendering strategy callback, then perform other actions on the engine instance based on your business. For example, use `createPreRenderEngine` to configure the engine. To specify a playback start time, follow [Pre-rendering with a specified start time](https://docs.byteplus.com/en/docs/25/27053#prerender-with-start-time).

4. Call `getPreRenderEngine` to determine whether pre\-rendering is complete and process the pre\-rendered cover logic.

5. Call `removePreRenderEngine` to determine whether pre\-rendering is complete and process the playback logic.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">You can call either <code>getPreRenderEngine</code> or <code>removePreRenderEngine</code> to get the engine object, but they have the following differences:</div>



* <div data-tips="true" data-tips-type="tip">An engine object obtained by calling <code>getPreRenderEngine</code> will not be separated from the SDK's internal pre\-rendering module. It is recommended not to hold this object in the business logic.</div>


* <div data-tips="true" data-tips-type="tip">An engine object obtained by calling <code>removePreRenderEngine</code> will be separated from the SDK's internal pre\-rendering module. You will need to hold the object in the business logic and manage its release logic yourself.</div>



Sample code for using the pre\-rendering strategy is as follows:

```Java
// 1. Enable global pre-rendering strategy, must be called on the main thread
TTVideoEngine.enableEngineStrategy(STRATEGY_TYPE_PRE_RENDER, STRATEGY_SCENE_SMALL_VIDEO);
// (Recommended) Enable the release of pre-rendering engine instances based on the LRU mechanism
StrategyManager.instance().enableReleasePreRenderEngineInstanceByLRU(true);

// 2. Reset the playback list, called when loading for the first time or refreshing the list. If both preloading strategy and pre-rendering strategy are implemented, the video playback list only needs to be set once.
List sources = new ArrayList<>();
TTVideoEngine.setStrategySources(sources);
// When there is new content added to the playlist (e.g., loading more data by scrolling up), you can use this interface to add data to the playback list.
// It will accumulate after the list set to the SDK previously.
// TTVideoEngine.addStrategySources(sources);

// 3. Set the Listener to listen for pre-rendering callbacks
TTVideoEngine.setEngineStrategyListener(new EngineStrategyListener() {
    @Override
    public TTVideoEngine createPreRenderEngine(final StrategySource source) {
        // Create an engine for pre-rendering the next video, and return it to the SDK.
        TTVideoEngine engine = getTTVideoEngine(source);
        return engine;
    }
});

// 4. Set the pre-rendering cover.
// It is recommended to set it in the onSurfaceTextureAvailable method of the TextureView's SurfaceTextureListener.
TTVideoEngine preRenderEngine = TTVideoEngine.getPreRenderEngine(mStrategySource);
if (preRenderEngine != null) {
    // Use the first frame rendered by the pre-rendering player as the cover. Here, only the Surface is set for rendering the cover, the business does not need to hold onto the preRenderEngine.
    preRenderEngine.setSurface(surface);
    preRenderEngine.forceDraw();
} else {
    // Use the business's own image loading library to load the cover image.
}

// 5. When playing the next video, check if pre-rendering is complete.
TTVideoEngine mEngine;
TTVideoEngine preRenderEngine = TTVideoEngine.removePreRenderEngine(mStrategySource.vid());
if (preRenderEngine != null) {
    // If not null, it means pre-rendering is complete, just call play. The business holds onto this player and is responsible for releasing the instance.
    mEngine = preRenderEngine;
} else {
    // If null, it means there is no pre-rendering, so you need to construct an engine and then play.
    mEngine = getTTVideoEngine(source);
}
// Set the available surface for the current page, it is recommended to get the surface in the onSurfaceTextureAvailable method of the TextureView's SurfaceTextureListener.
mEngine.setSurface(surface);
// Play
mEngine.play();

private static TTVideoEngine getTTVideoEngine(final StrategySource source) {
    TTVideoEngine engine = new TTVideoEngine(this, ITTVideoEngineInternal.PLAYER_TYPE_OWN);
    // (Required) Set the playback source.
    engine.setStrategySource(source);
    // Customize the settings according to your needs.
    // engine.setIntOption(PLAYER_OPTION_USE_TEXTURE_RENDER, 1);
    engine.setIntOption(....);
    return engine;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">The SDK pre\-rendering module will query the index of the video that is currently playing in the playlist, and pre\-render the index+1 video source.</div>


* <div data-tips="true" data-tips-type="tip">Only one video can be pre\-rendered.</div>


* <div data-tips="true" data-tips-type="tip">Instructions on the pre\-render engine release timing are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">When you call <code>getPreRenderEngine</code> and <code>removePreRenderEngine</code> to get the pre\-render engine, if the engine's pre\-rendering fails, it will be released.</div>


   * <div data-tips="true" data-tips-type="tip">An engine object obtained by calling <code>removePreRenderEngine</code> will be separated from the SDK's internal pre\-rendering module. You will need to hold the object in the business logic and manage its release logic yourself.</div>


   * <div data-tips="true" data-tips-type="tip">When the pre\-rendering conditions are met, before creating a new pre\-render engine, the SDK will release the previous engine that has not been removed by <code>removePreRenderEngine</code>.</div>



<span id="prerender-with-start-time"></span>
### Pre\-rendering with a specified start time

This feature requires the Android Player SDK `1.52.100.5` or later.

To pre\-render from a specified position, such as the last playback position, set the start time on the engine created in `createPreRenderEngine` and set `PLAYER_OPTION_ENABLE_START_TIME_SKIP_AVSKIPSERIAL` to `1`.

The following example extends the callback above and pre\-renders from 1 second. Set the start time in milliseconds according to your application's needs, and complete this configuration before calling `prepare`.

```Java
TTVideoEngine.setEngineStrategyListener(new EngineStrategyListener() {
    @Override
    public TTVideoEngine createPreRenderEngine(final StrategySource source) {
        TTVideoEngine engine = getTTVideoEngine(source);
        int startPlayPositionMS = 1000; // Example: start at 1 second.
        engine.setStartTime(startPlayPositionMS);
        engine.setIntOption(PLAYER_OPTION_ENABLE_START_TIME_SKIP_AVSKIPSERIAL, 1);
        return engine;
    }
});
```


<span id="b483cd9c"></span>
## Clear all strategies

When exiting a video page or switching to another page, call `clearAllStrategy` to close all strategies and release resources.

```java
TTVideoEngine.clearAllStrategy();
```


<span id="96d1a320"></span>
## Note

If you simultaneously access the preloading strategy and pre\-rendering strategy, you only need to set one video playlist.
