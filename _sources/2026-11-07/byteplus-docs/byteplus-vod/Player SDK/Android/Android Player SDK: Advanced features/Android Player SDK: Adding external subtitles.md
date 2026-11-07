---
title: "Android Player SDK: Adding external subtitles"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-external-subtitles-android"
---

This article provides instructions on how to add external subtitles when using the Player SDK.

<span id="5a29ad94"></span>
## Overview

The "External subtitles" feature enables users to store subtitle files separately from video files and import them while playing the video. The Player SDK currently supports the WebVTT (Web Video Text Tracks) format for subtitle files. This approach provides flexibility, allowing users to decide whether to import subtitle files or load subtitles in various languages. Importantly, there is no requirement for additional video transcoding, as the feature can be activated with proper settings on the player's side.

<span id="a5306045"></span>
## Prerequisites

Before adding the external subtitles, make sure you have:


* Integrated the SDK according to [Android Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk).

* If you are playing videos in Vid mode, you need to prepare the subtitle file:

   * If you already have a separate subtitle file, you can upload the subtitle file on the **Video details** page in the [BytePlus VOD console](https://console.byteplus.com/vodpaas), as shown in the following picture.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b5b084b692e416bbbdcf5114f1a7814~tplv-goo7wpa0wc-image.image) </span>

   * If you don't have a separate subtitle file, you can use the [Smart subtitling template](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template) to generate the subtitle file.


<span id="84108d83"></span>
## Enabling the external subtitles feature

To enable the external subtitles feature, use the following sample code:

```Java
// Enable the external subtitles feature. Call this method before setting subtitle source.
mVideoEngine.setIntOption(PLAYER_OPTION_ENABLE_OPEN_SUB_THREAD, 1);

// Enable subtitle loading optimization.
// 0: Disable subtitle loading optimization
// 1: Enable subtitle loading optimization
mVideoEngine.setIntOption(PLAYER_OPTION_ENABLE_OPT_SUB_LOAD_TIME, 1);

// Use the data loading module (MDL) to load external subtitles, improving the success rate of loading 
// 1: Use MDL to load external subtitles 
// 0: Do not use MDL to load external subtitles
mVideoEngine.setIntOption(PLAYER_OPTION_SUB_ENABLE_MDL, 1);
```


<span id="81fcbe34"></span>
## Setting subtitle source

The Player SDK offers two methods for setting the subtitle source. Select the appropriate method based on your specific needs:


* (Recommended) Method 1: Using the subtitle URL

   ```Java
   final String vid = "YOUR_VIDEO_ID"; // The video source must correspond to the Vid
   final String url = "http://www.example.com/h264.mp4";
   final String cacheKey = TTVideoEngine.computeMD5(url);
   final String subtitleJSONStr = ""; // See the Subtitle JSON example section for reference.
   
   // Set the DirectURL playback source
   DirectUrlSource directUrlSource = new DirectUrlSource.Builder()
           .setVid(vid)
           .addItem(new DirectUrlSource.UrlItem.Builder()
                   .setUrl(url)
                   .setCacheKey(cacheKey)
                   .build())
           .build();
   ttVideoEngine.setStrategySource(directUrlSource);
   
   // Set the subtitle source in DirectURL mode
   SubDesInfoModel subtitleModel = null;
   try {
       JSONObject subtitleJSON = new JSONObject(subtitleJSONStr);
       subtitleModel = new SubDesInfoModel(subtitleJSONStr);
   } catch (JSONException e) {
       e.printStackTrack();
   }
   // Set the subtitleModel after setting the video source
   if (subtitleModel != null) {
       mVideoEngine.setSubDesInfoModel(subtitleModel);
   }
   ```
   

* Method 2: Using Vid and SubtitleToken

   ```Java
   String vid = "YOUR_VIDEO_ID"; // Provided by your app server
   String playAuthToken = "YOUR_PLAYAUTHTOKEN"; // Provided by your app server
   String subAuthToken = "YOUR_SUBAUTHTOKEN"; // Provided by your app server
   
   // Set the Vid playback source
   VidPlayAuthTokenSource vidSource = new VidPlayAuthTokenSource.Builder()
           .setVid(vid)
           .setPlayAuthToken(playAuthToken)
           .build();
   mVideoEngine.setStrategySource(vidSource);
   
   // Set the subtitle authentication token
   mVideoEngine.setSubAuthToken(subAuthToken);
   
   // Set the callback for successful video source retrieval
   mVideoEngine.setVideoInfoListener(new VideoInfoListener() {
       @Override
       public boolean onFetchedVideoInfo(VideoModel videoModel) {
           // Callback for successful video data retrieval
           Log.v("VideoPlay", "onFetchedVideoInfo " + videoModel);
           if (videoModel == null) return false;
           if (mVideoEngine == null) return false;
           
           // Request the ID array of the Chinese and English subtitle files
           List<String> subtitleIds = new ArrayList<>();
           // Get the interface for obtaining all subtitle languages
           List<SubInfo> subInfoList = mVideoEngine.supportedSubInfoList();
           // See the subtitle language table at: https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language
           if (subInfoList != null && subInfoList.size() > 0) {
               for (SubInfo info : subInfoList) {
                   if (info.mLanguageId == 1) { 
                       subtitleIds.add(info.mSubId); // CN
                   } else if (info.mLanguageId == 2) {
                       subtitleIds.add(info.mSubId); // EN
                   }
               }
           }
           String subIds = trans(subtitleIds); // Implementation omitted, convert subtitleIds to a comma-separated string, such as "1111,2222"
           // Pass the list of subtitle language IDs
           mVideoEngine.setStringOption(PLAYER_OPTION_SUB_IDS, subIds);
           return false;
       }
   });
   ```
   


<span id="13d4b760"></span>
## Controlling subtitles

<span id="4dc37848"></span>
### Enabling/Disabling subtitles output

To control the enabling or disabling of subtitle output during playback, use the following sample code:

```Java
// Enable or disable subtitles during playback
// 1: Output subtitles; 0: Stop outputting subtitles
mVideoEngine.setIntOption(PLAYER_OPTION_ENABLE_OPEN_SUB, 1);
// Show the subtitle TextView
textView.setVisibility(View.VISIBLE);
```


<span id="fb14e9e9"></span>
### Switching between subtitles

Use the following sample code to switch to a different subtitle by passing the subtitle ID:

```Java
// Maintain the mapping between subtitle IDs and languages for easy expansion
mVideoEngine.setIntOption(PLAYER_OPTION_SWITCH_SUB_ID, sub_id);
```


<span id="d9bc7f42"></span>
## Setting subtitle callback

Call the `setSubInfoCallBack` method to set the subtitle\-related callbacks. Use the following sample code:

```Java
mVideoEngine.setSubInfoCallBack(new SubInfoSimpleCallBack() {
    @Override
    public void onSubPathInfo(String subPathInfoJson, Error error) {
        // Callback for subtitle list information when playing with Vid + SubtitleToken
    }

    @Override
    public void onSubInfoCallback(int code, String infoJson) {
        // Callback for subtitle information
        JSONObject jsonObject = new JSONObject(infoJson);
        String subtitle = jsonObject.optString("info");
        textView.setText(subtitle); // Set the subtitle to the TextView
    }
        
    @Override
    public void onSubSwitchCompleted(int success, int subId) {
        // Callback for subtitle language switch
    }
    
    @Override
    public void onSubLoadFinished(int success) {
        // Callback for subtitle file download result

    }
})
```


<span id="dd4df4e1"></span>
## Implementing subtitle preloading

Subtitle preloading improves subtitle loading speed and success rate when users watch videos.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Subtitle preloading is based on the preload strategy. Before using it, make sure you've implemented the preload strategy in <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-android-player-short-video-best-practices">Android Player SDK: Best practices for short video scenarios</a>.</div>


* <div data-tips="true" data-tips-type="tip">DirectURL subtitle preloading is supported from version 1.45.200.4; Vid subtitle preloading is supported from version 1.47.100.2.</div>



<span id="2832e041"></span>
### **Preloading phase**

<span id="2dee7d13"></span>
#### **DirectUrl mode**


1. Before initializing the SDK, enable preload strategy version 2 and the preload strategy itself.

   ```Java
   // Enable preload strategy version 2
   StrategyManager.setVersion(StrategyManager.VERSION_2);
   // Initialize the player SDK
   Env.init(
   /* initialization code omitted */
   );
   // Enable and use the preload strategy
   TTVideoEngine.enableEngineStrategy(STRATEGY_TYPE_PRELOAD, STRATEGY_SCENE_SMALL_VIDEO);
   ```
   

2. Construct the subtitle source and playback source.

   ```Java
   // 1. Create the subtitle source model
   SubDesInfoModelProvider subtitleModel = null;
   String subtitleJson = "{
       \"list\": [
           {
               \"language\": \"cmn-Hans-CN\",
               \"language_id\": 1,
               \"url\": \"https://example.com/subtitle1.vtt\",
               \"cache_key\": \"cachekey_1\", // Subtitle cache key
               \"expire\": 1618253637,
               \"format\": \"webvtt\",
               \"sub_id\": 0
           },
           {
               \"language\": \"eng-US\",
               \"language_id\": 2,
               \"url\": \"https://example.com/subtitle2.vtt\",
               \"cache_key\": \"cachekey_2\", // Subtitle cache key
               \"expire\": 1618253637,
               \"format\": \"webvtt\",
               \"sub_id\": 1
           }
       ]
   }";
   
   try {
       subtitleModel = new SubDesInfoModel(new JSONObject(subtitleJson));
   } cache (JSONException e) {
       e.printStackTrace();
   }
   
   int subtitleId = ""; // Preloaded subtitle ID
   
   String vid = "";
   String videoUrl = "";
   String videoCacheKey = "";
   
   // 2. Set the subtitle source model in the playback source
   DirectUrlSource directUrlSource = new DirectUrlSource.Builder()
       .setVid(vid)
       .addItem(new UrlItem.Builder()
           .setUrl(videoUrl)
           .setCacheKey(videoCacheKey)
           .build())
       .setSubtitleModel(subtitleModel)
       .setSubtitleId(subtitleId)
       .build();
   
   // 3. Set the playback source list with the strategy module; the SDK will automatically preload the subtitle source.
   TTVideoEngine.setStrategySources(list);
   // TTVideoEngine.addStrategySources(list);
   ```
   


<span id="a3949d92"></span>
#### Vid mode


1. Before initializing the SDK, enable preload strategy version 2 and the preload strategy itself.

   ```Java
   // Enable preload strategy V2
   StrategyManager.setVersion(StrategyManager.VERSION_2);
   // Initialize the player SDK
   Env.init(/* initialization code omitted */);
   // Enable and use the preload strategy
   TTVideoEngine.enableEngineStrategy(STRATEGY_TYPE_PRELOAD, STRATEGY_SCENE_SMALL_VIDEO);
   
   // Set the preload task factory for constructing preload tasks within the preload strategy
   StrategyManager.instance().setPreloadTaskFactory(new PreloadTaskFactory() {
       @Override
       public PreloaderVidSubtitleItem createSubtitleVidItem(VidPlayAuthTokenSource vidSource, long preloadSize) {
           final PreloaderVidSubtitleItem item = PreloadTaskFactory.super.createSubtitleVidItem(vidSource, preloadSize);
           item.setFetchEndListener(new PreloaderVidSubtitleItemFetchListener() {
           
               @Override
               public void onGetPlayInfoResult(VideoModel videoModel, Error error) {
                   // If the user can switch video resolutions, you need to reset the resolution using item.setResolution to override the resolution in VidPlayAuthTokenSource
                   
                   if (videoModel == null) return;
                   
                   Resolution resolution = Resolution.High; // 480P
                   resolution = TTVideoEngine.findDefaultResolution(videoModel, resolution);
   
                   final VideoInfo videoInfo = videoModel.getVideoInfo(resolution, false);
                   if (videoInfo == null) return;
                   item.setResolution(videoInfo.getResolution());
               }
   
               @Override
               public void onGetSubtitleInfoResult(SubDesInfoModel subDesInfoModel, Error error) {
                   // If multiple subtitle files are sent for different languages, you need to find the corresponding subtitle ID based on the language. Setting it via item.setSubtitleId allows preloading of the corresponding language subtitle
                   
                   if (subDesInfoModel == null) return;
   
                   final List<SubModelProvider> subInfos = subDesInfoModel.getSubModelList();
                   if (subInfos == null || subInfos.isEmpty()) return;
                   
                   // Language ID enum; refer to the official documentation: https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language
                   final int languageId = 1; // User's default selected subtitle language (e.g., Chinese)
                   Integer subtitleId = findPreloadSubtitleIdByLanguageId(subInfos, languageId);
                   if (subtitleId != null) {
                       item.setSubtitleId(subtitleId);
                   }
               }
           });
           return item;
       }
   });
   ```
   

2. Construct the Vid playback source. In addition to the video's `vid` and `playAuthToken`, you also need to provide the subtitle authentication token.

   ```Java
   // 1. Construct the Vid playback source
   String vid = "your video id";
   String playAuthToken = "your video playAuthToken";
   Resolution resolution = Resolution.SuperHigh; // 720P
   String subtitleAuthToken = "your subtitleAuthToken"; // Subtitle authentication token
   
   VidPlayAuthTokenSource vidSource = new VidPlayAuthTokenSource.Builder()
           .setVid(vid)
           .setPlayAuthToken(playAuthToken)
           .setResolution(resolution)
           .setSubtitleAuthToken(subtitleAuthToken)
           .build();
           
   // 2. Set the playback source list using the strategy module; the subtitle source will be preloaded automatically
   TTVideoEngine.setStrategySources(list);
   TTVideoEngine.addStrategySources(list);
   ```
   


<span id="32f60b91"></span>
### Playback phase


1. To use subtitle preloading, you must enable the Media Data Loader (MDL) module to load external subtitles.

   ```Java
   // 0: Do not use MDL; 1: Use MDL
   mVideoEngine.setIntOption(PLAYER_OPTION_SUB_ENABLE_MDL, 1);
   ```
   

2. Specify the subtitle ID to play. Make sure this ID matches the subtitle ID used in your preloaded playback source.

   ```Java
   mVideoEngine.setIntOption(PLAYER_OPTION_SWITCH_SUB_ID, sub_id);
   ```
   

3. Monitor the cache hit callback: Use `VideoEngineInfoListener` to listen for the `USING_MDL_HIT_CACHE_SIZE_SUBTITLE` event. A `cacheSize` greater than 0 confirms a cache hit. If there is a cache miss, check if the preloading task was successful and if the `subtitleId` used for playback matches the one used for preloading.

   ```Java
   // Set a listener for the TTVideoEngine instance
   mVideoEngine.setVideoEngineInfoListener(new VideoEngineInfoListener() {
       @Override
       public void onVideoEngineInfos(VideoEngineInfos videoEngineInfos) {
           if (videoEngineInfos == null) {
               return;
           }
           
           // Listen for subtitle cache hits
           if (videoEngineInfos.getKey().equals(USING_MDL_HIT_CACHE_SIZE_SUBTITLE)) {
               // Check if the cache was hit during playback
               String taskKey = videoEngineInfos.getUsingMDLPlayTaskKey();// Key used
               long cacheSize = videoEngineInfos.getUsingMDLHitCacheSize();// Size of cached file
               
               // cacheSize > 0: Cache hit
               // cacheSize = 0: Cache miss. Check if the preloading task was successful and if the subtitle IDs used for preloading and playback match.
           }
       }
   });
   ```
   


<span id="fd647a33"></span>
## References

<span id="1c8e6dcc"></span>
### JSON subtitle information example

```JSON
{
  "list": [
    {
      "id": 0,
      "language": "rus-RU",
      "language_id": 6,
      "url": "https://***.com/cbebedaad*******17f0b13/6087d12f/video/tos/cn/tos-cn-o-0004/52ce3882d709***913cbd83d969/",
      "expire": 1619513647,
      "format": "webvtt",
      "sub_id": 328934091
    },
    {
      "id": 1,
      "language": "cmn-Hans-CN",
      "language_id": 1,
      "url": "https://***.com/93adb942***bdfce8cb/6087d12f/video/tos/***a4122dac42d69e8233a4dfda82fe/",
      "expire": 1619513647,
      "format": "webvtt",
      "sub_id": 429984091
    },
    {
      "id": 2,
      "language": "cmn-Hans-CN|eng-US",
      "language_id": 5,
      "url": "https://***.com/d782d36702***7b9719/6087d12f/video/tos/***5f0d106146a19ad566b967211091/",
      "expire": 1619513647,
      "format": "webvtt",
      "sub_id": 829987091
    }
  ]
}
```


Description:


* `sub_id` is the subtitle ID, and `language_id` is the language ID. You need to maintain the mapping relationship between subtitle ID and language ID by yourself.

* Refer to [Subtitle languages](https://docs.byteplus.com/docs/byteplus-vod/docs-subtitle-language) for the values of `language` and `language_id`.

* `url` is the URL of the subtitle file.

* `id` can be set as an index.

* `expire` is the expiration time of the subtitle URL. If there is no expiration time, it can be left empty.
