---
title: "Android Player SDK: VideoModel"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/videomodel-android"
---

VideoModel is a self\-developed protocol for an optimal playback experience in multi\-resolution scenarios. It allows you to consolidate multi\-resolution and multi\-format video streams into a single object and directly passes the information to the Player SDK for playback. The advantages are as follows:


* **Reduced first\-frame time**: Compared to the Vid mode (the Player SDK requests playback information from the VOD server via a Vid), VideoModel skips this client\-to\-server network request. Your business server can directly generate or your client can assemble the VideoModel playback source, and pass it to the Player SDK to start loading.

* **Complete features**: VideoModel supports all VOD features, including ABR (Adaptive Bitrate), smooth switching, and private encryption.

* **High flexibility**: You have complete control over the VideoModel's generation and distribution timing to better integrate with your business logic.


This document demonstrates how to construct the VideoModel playback source based on the video data source.

<span id="395351a7"></span>
## Video data flows

The construction method for the VideoModel depends on the source of your video data. There are two main paths:


* **Third\-party services or custom data:** 

   1. The business server retrieves video data and encapsulates it into a custom data structure to distribute to the client.

   2. The client calls methods in the `Builder` class (such as `setUrl` and `setBitrate`) to populate the `IVideoModel` object with information for each video stream.

* **VOD service data:** 

   1. The business server calls VOD's `GetPlayInfo` to retrieve a JSON string containing the video metadata.

   2. The server distributes the string to the client via a business API.

   3. The client uses an SDK\-provided method to directly convert the JSON string into an `IVideoModel` object. This eliminates the need for manual parsing and field setting.


<span id="c6d1234f"></span>
## Constructing the VideoModel playback source

<span id="856ad04f"></span>
### Step 1: Construct the IVideoModel

<span id="ea658e16"></span>
#### **Method 1: Manual field setting (for third\-party service/custom data)** 

Assume your business data model `VideoItem` is structured as follows:

```Java
// Business Video Model
public class VideoItem {
    public String videoId;
    public long durationInS;
    public List<StreamItem> streamItems;

    // Every StreamItem represents a single video stream of a specific resolution
    public static class StreamItem {
        public String url;
        public String cacheKey;
        public String codecType; // "h264", "h265"
        public String format;    // "dash", "hls", "mp4"
        public int width;
        public int height;
        public int bitrate;
        public Resolution resolution;
        public String playAuth;  // Private DRM key
    }
}
```


The following example code shows how to convert the `VideoItem` object into an `IVideoModel`:

```Java
public static IVideoModel createVideoModel(VideoItem videoItem) {
    List<VideoInfo> videoInfos = new ArrayList<>();
    // Iterate through all resolution streams, creating a VideoInfo object for each
    for (VideoItem.StreamItem streamItem : videoItem.streamItems) {
        videoInfos.add(new BareVideoInfo
                .Builder()
                // --- Basic Information ---
                .urls(Arrays.asList(streamItem.url)) // URL list for the video stream. **Required**.
                .fileHash(streamItem.cacheKey)      // Unique cache key for the stream. **Required**.
                .resolution(streamItem.resolution) // Resolution level enum. **Required**.
                .codecType(streamItem.codecType)    // Encoding type (for example, "h264", "h265"). **Required**.
                
                // --- Information Required for ABR and Smooth Switching ---
                .bitrate(streamItem.bitrate) // Bitrate in bps. Required for ABR and smooth switching.
                .vWidth(streamItem.width)    // Video width. Necessary for ABR.
                .vHeight(streamItem.height)  // Video height. Necessary for ABR.
                .format(streamItem.format)    // Format type (for example, "dash", "hls"). Necessary for ABR and smooth switching.
                .mediaType(VideoRef.TYPE_VIDEO) // Stream type. Must be explicitly set to video or audio for DASH playback.
                
                // --- Information Required for DRM Encryption ---
                .spadea(streamItem.playAuth) // Private DRM key (playAuth), for video stream decryption.
                .build());
    }
    
    // Aggregate all VideoInfo objects into a BareVideoModel
    return new BareVideoModel.Builder()
            .vid(videoItem.videoId)          // Unique video ID. **Required**.
            .duration(videoItem.durationInS)    // Total video duration in seconds.
            .setVideoInfos(videoInfos)          // List containing all resolution streams. **Required**.
            .adaptive(true)                      // Set to true to enable smooth switching or ABR.
            .dynamicType(TTVideoEngine.DYNAMIC_TYPE_SEGMENT_BASE) // Must be set when the format is DASH or fmp4.
            .build();
}
```


<span id="bc1d9f53"></span>
#### **Method 2: Direct construction from JSON (for VOD data)** 

When your business server obtains the JSON string returned by the VOD [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo), you can use the following method to convert it directly into an `IVideoModel` object.

```Java
/**
 * Helper method to create an IVideoModel instance from a JSON string.
 * @param jsonModel The JSON string from the VOD GetPlayInfo interface.
 * @return An IVideoModel instance; returns null if parsing fails.
 */
@Nullable
static IVideoModel create(String jsonModel) {
    if (TextUtils.isEmpty(jsonModel)) return null;

    VideoRef ref = new VideoRef();
    try {
        ref.extractFields(new JSONObject(jsonModel));
        VideoModel model = new VideoModel();
        model.setVideoRef(ref);
        return model;
    } catch (Throwable throwable) {
        return null;
    }
}
```


The JSON string you pass should be the JSON object from the `Result` field in the `GetPlayInfo` API response, not the entire response string. Example structure of the `Result` JSON object is as follows:

```JSON
{
    "Vid": "v029c1g10003civ2i5mqib*******",
    "Status": 1,
    "PosterUrl": "https://img.***.com/1234/8511abe****.jpeg",
    "Duration": 0.1,
    "FileType": "video",
    "EnableAdaptive": true,
    "TotalCount": 1
    // ... more fields
}
```


<span id="7f0bad9d"></span>
### Step 2: Encapsulate in a VideoModelSource

The `IVideoModel` must be encapsulated into a `VideoModelSource` object. This allows the Player SDK to recognize and utilize it.

```Java
public static VideoModelSource createVideoModelSource(IVideoModel videoModel) {
    // Construct the VideoModelSource
    final VideoModelSource videoModelSource = new VideoModelSource.Builder()
            // The video ID. This must be consistent with the vid in the IVideoModel.
            .setVid(videoModel.getVideoRefStr(VideoRef.VALUE_VIDEO_REF_VIDEO_ID))
            // Pass the IVideoModel object created in the previous step. **Required**.
            .setVideoModel(videoModel)
            // (Optional) Specify the starting resolution. Omit this to use automatic resolution selection or ABR.
            .setResolution(Resolution.Standard)
            .build();
    return videoModelSource;
}
```


<span id="7193e0c5"></span>
## Advanced usage

<span id="dee5b0cd"></span>
### (Optional) Enabling the VideoModel playback retry strategy

After constructing and setting the `VideoModelSource`, you can optimize the playback experience by enabling specific player options. If you encounter playback failures caused by network fluctuations (such as socket receive timeouts, error code: \-499793) or data source anomalies, you can enable the `PLAYER_OPTION_OPTIMIZE_VIDEO_MODEL_RETRY_STRATEGY` option.


* **Default behavior (Disabled)** : Upon playback failure, the player attempts to use backup URLs if they exist.

* **Behavior when enabled**: Upon playback failure, the player prioritizes retrying the current failing URL first instead of switching immediately to a backup URL. This facilitates faster recovery during temporary network jitters.


**How to enable**: Call the `setIntOption` method to enable `PLAYER_OPTION_OPTIMIZE_VIDEO_MODEL_RETRY_STRATEGY` before setting the playback source.

```Java
// 1. Initialize the player engine
TTVideoEngine mTTVideoEngine = new TTVideoEngine(context, 0);

// 2. Enable the VideoModel playback retry strategy
// This option is disabled by default (value 0). Set it to 1 to enable.
mTTVideoEngine.setIntOption(PLAYER_OPTION_OPTIMIZE_VIDEO_MODEL_RETRY_STRATEGY, 1);

// 3. Set the VideoModelSource
// 'videoModelSource' is the object created in the previous section.
mTTVideoEngine.setVideoModelSource(videoModelSource);

// 4. Start playback
mTTVideoEngine.play();
```
