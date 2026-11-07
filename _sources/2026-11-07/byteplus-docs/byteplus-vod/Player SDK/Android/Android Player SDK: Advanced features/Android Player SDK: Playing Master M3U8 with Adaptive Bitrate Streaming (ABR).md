---
title: "Android Player SDK: Playing Master M3U8 with Adaptive Bitrate Streaming (ABR)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-m3u8-abr-playback-android"
---

Adaptive Bitrate Streaming (ABR) playback refers to the process of dynamically and seamlessly switching to the most suitable video resolution based on the user's network conditions. This ensures smooth video playback while providing the best possible viewing experience. This document guides you on how to play standard HLS Master M3U8 videos in **DirectUrl mode**.

<span id="bf773af3"></span>
## Prerequisites

Before integrating the ABR playback feature, ensure that you have completed the following steps:


* **Obtain a License**: ABR playback is only supported by Premium Edition. Make sure your license includes the ABR playback functionality. For details, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).

* **Integrate the Premium SDK and ABR module**: Refer to [Android Player SDK: Integrating the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-integration-android) to integrate the 1.47.200.5 or later versions of the Premium SDK.

   ```Plain
   def ttsdk_version = "1.47.200.5"
   implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdk_version"
   implementation "com.bytedanceapi:ttsdk-ttabr:$ttsdk_version"
   ```
   

* **Complete basic SDK initialization**: Refer to [Android Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk) to complete the basic configuration and initialization of your project.

* **Verify the Master M3U8 File**: Ensure that in your Master M3U8 file, every `#EXT-X-STREAM-INF` tag includes the `"AVERAGE-BANDWIDTH"` attribute. The ABR strategy relies heavily on this attribute to assess the match between network conditions and bitrate for automatic switching. For example:

   ```Plain
   #EXT-X-STREAM-INF:BANDWIDTH=2628000,AVERAGE-BANDWIDTH=2500000,RESOLUTION=...
   /path/to/1080p.m3u8
   ```
   


<span id="351fa64d"></span>
## **Implementing ABR playback**

<span id="b961141d"></span>
### Step 1: Initialize network detection and enable ABR

After creating a player instance and before calling `play()`, you need to enable network speed detection and set a series of options to activate the ABR feature for Master M3U8.

```Java
// 1. Initialize the network speed detector to provide data for ABR decision-making
TTVideoEngine.setIntValue(
        DataLoaderHelper.DATALOADER_KEY_INT_NEED_SPEED_TEST_BY_TIMEINTERNAL, 1);
TTVideoEngine.startSpeedPredictor(TTVideoEngine.TESTSPEED_HECNET, 500, 1, 100);

// 2. Configure the player instance for Master M3U8 ABR
// Enable the Master M3U8 ABR feature
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_MASTER_M3U8_ABR, 1);
// Enable optimizations for Master M3U8
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_MASTER_M3U8_OPTIMIZE, 1);
// Disable the legacy ABR strategy to avoid conflicts
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_GEAR_STRATEGY, 0);

// 3. (Optional) Set display dimensions to optimize stream selection
// Setting these parameters helps the ABR strategy prioritize streams with resolutions that
// better match the current display area, especially when bitrates are similar.
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_PLAYER_DISPLAY_WIDTH, displayWidth);
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_PLAYER_DISPLAY_HEIGHT, displayHeight);
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_DEVICE_SCREEN_WIDTH, screenWidth);
videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_DEVICE_SCREEN_HEIGHT, screenHeight);
```


<span id="89e15eed"></span>
### Step 2: Set the startup resolution

When playing a Master M3U8 video, you need to implement the `TTVideoEnginePlayHLSChooseStreamCallback` interface. This callback mechanism allows you to decide which bitrate to use for initial playback.

```Java
private int mVideoStartupResolution = 720; // Desired startup resolution height
private TTVideoEngineMasterPlaylist mMasterPlaylist; // To store the parsed M3U8 information
private int mHlsVideoVariantIndex = -1; // To store the index of our chosen startup stream

videoEngine.setPlayerHLSChooseStreamCallback(new TTVideoEnginePlayHLSChooseStreamCallback() {
    /**
     * This callback is triggered after the player successfully parses the Master M3U8 file,
     * providing all available stream information.
     */
    @Override
    public void streamInfos(TTVideoEngineMasterPlaylist ttVideoEngineMasterPlaylist) {
        if (ttVideoEngineMasterPlaylist == null || ttVideoEngineMasterPlaylist.variantStreams == null) {
            return;
        }
        mMasterPlaylist = ttVideoEngineMasterPlaylist;
        
        // Example: Iterate through all streams to find the one closest to 720p for startup
        for (int i = 0; i < mMasterPlaylist.variantStreams.length; i++) {
            TTVideoEngineVariantStream videoVariant = mMasterPlaylist.variantStreams[i];
            // Resolution format is typically "1280x720"
            if (videoVariant.resolution != null && videoVariant.resolution.contains(String.valueOf(mVideoStartupResolution))) { 
                mHlsVideoVariantIndex = i;
                break; // Exit after finding a match
            }
        }

        // If no match is found, default to the first stream (usually the lowest bitrate) to ensure a fast start
        if (mHlsVideoVariantIndex == -1) {
            mHlsVideoVariantIndex = 0;
        }
    }

    /**
     * After the streamInfos callback, the player calls this method to ask for your final decision
     * on which stream to start with. You must return the bandwidth of the stream you selected in streamInfos.
     */
    @Override
    public int chooseVariantBandWidth() {
        if (mMasterPlaylist == null || mMasterPlaylist.variantStreams == null || mHlsVideoVariantIndex < 0 || mHlsVideoVariantIndex >= mMasterPlaylist.variantStreams.length) {
            return -1; // Return -1 indicates an error; the player will use its default strategy (usually the highest bitrate)
        }
        
        TTVideoEngineVariantStream selectedStream = mMasterPlaylist.variantStreams[mHlsVideoVariantIndex];
        if (selectedStream == null) {
            return -1;
        }

        // Return the bandwidth of the selected stream; the player will use this stream for startup
        return selectedStream.bandwidth;
    }
});
```


<span id="8486b4b0"></span>
### Step 3: Set the playback source and start playback

After completing all the above configurations, set the Master M3U8 URL as the playback source and call `play()`.

```Java
// 1. Prepare your playback information
final String masterM3u8Url = "http://example.com/path/to/master.m3u8";

// Provide a unique Vid for this URL source. This Vid serves as the unique identifier for the source
// within the SDK (for modules like preloading, caching, statistics). Even for a URL source,
// providing a stable and unique Vid helps the SDK manage playback sessions and optimize performance.
// It can be a unique identifier from your own video management system or an ID generated at the app level.
final String vid = "your_unique_video_id_for_this_url"; 

// Use the MD5 hash of the URL as the cache key to ensure uniqueness.
final String cacheKey = TTVideoEngine.computeMD5(masterM3u8Url);

// 2. Build the DirectUrlSource object
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(new DirectUrlSource.UrlItem.Builder()
                .setUrl(masterM3u8Url)
                .setCacheKey(cacheKey)
                .build())
        .build();
       
// 3. Set the playback source for the player
videoEngine.setStrategySource(directUrlSource);

// 4. Start playback
videoEngine.play();
```
