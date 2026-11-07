---
title: "Android Player SDK: Custom stream selection for standard Master M3U8 playback sources"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/custom-stream-selection-for-master-m3u8-android"
---

For a standard Master M3U8 playback source, the Player SDK provides fine\-grained control over stream selection. This allows you to programmatically choose which video and audio streams are used at different stages of the playback lifecycle.

<span id="987d2b2e"></span>
## Selecting initial video and audio streams

To specify the initial video and audio streams before playback begins, implement the `setPlayerHLSChooseStreamCallback` callback. This callback is triggered after the Player SDK has parsed the Master M3U8 file but before it starts downloading media segments.

The following example shows how to start playback with a 720p video stream and an English audio track.

```Java
private String mHlsAudioLanguage = "en"; // Target audio track language
private int mVideoStartupResolution = 720; // Target video resolution

private TTVideoEngineMasterPlaylist mMasterPlaylist;
private int mHlsVideoVariantIndex;
private int mHlsAudioRenditionInfoId;

videoEngine.setPlayerHLSChooseStreamCallback(new TTVideoEnginePlayHLSChooseStreamCallback() {
    // Triggered after the M3U8 parsing is complete, returning a masterPlaylist object that contains all video variantStreams and audio renditions. Iterate and decide on the index or ID of the stream to use.
    @Override
    public void streamInfos(TTVideoEngineMasterPlaylist ttVideoEngineMasterPlaylist) {
        // 1. Iterate through video streams to find the videoVariant that best matches the target resolution.
        mMasterPlaylist = ttVideoEngineMasterPlaylist;
        L.d(this, "streamInfos " + new Gson().toJson(mMasterPlaylist));
        for (int i = 0; i < ttVideoEngineMasterPlaylist.variantStreams.length; i++) {
            TTVideoEngineVariantStream videoVariant = ttVideoEngineMasterPlaylist.variantStreams[i];
            if (videoVariant.resolution.contains(mVideoStartupResolution + "x")) { // This is a simple demonstration for starting playback at 720p. In production code, it is better to match a numerical range (such as a height between 700-720) to handle variations in how standardized the video sources are.
                mHlsVideoVariantIndex = i;
                break;
            }
        }
        if (mHlsVideoVariantIndex == -1) {
            mHlsVideoVariantIndex = 0;
        }
    }

    // The player calls this method to get the bandwidth of the selected video stream. Return the bandwidth value of this stream in streamInfos.
    @Override
    public int chooseVariantBandWidth() {
        // 2. Return the bandwidth of the videoVariant found in the first step.
        if (mMasterPlaylist == null) {
            return -1;
        }
        if (mMasterPlaylist.variantStreams == null || mMasterPlaylist.variantStreams.length == 0) {
            return -1;
        }
        if (mHlsVideoVariantIndex >= mMasterPlaylist.variantStreams.length) {
            return -1;
        }
        TTVideoEngineVariantStream videoVariant = mMasterPlaylist.variantStreams[mHlsVideoVariantIndex];
        if (videoVariant == null) {
            return -1;
        }
        L.d(this, "chooseVariantBandWidth ", new Gson().toJson(videoVariant));
        return videoVariant.bandwidth;
    }

    // The player calls this method to get the selected audio track ID. Return the ID of the matched audio track.
    @Override
    public int chooseRenditionInfoId(int videoVariantIndex) {
        // 3. Based on the audioGroupId of the videoVariant found in the first step,
        // find the language-matching audio track from all renditions and return its infoId.
        L.d(this, "chooseRenditionInfoId " + videoVariantIndex);
        if (mMasterPlaylist == null) {
            return -1;
        }
        if (mMasterPlaylist.variantStreams == null || mMasterPlaylist.variantStreams.length == 0) {
            return -1;
        }
        if (videoVariantIndex >= mMasterPlaylist.variantStreams.length) {
            return -1;
        }
        TTVideoEngineVariantStream videoVariant = mMasterPlaylist.variantStreams[videoVariantIndex];
        if (videoVariant == null) {
            return -1;
        }
        if (mMasterPlaylist.renditions == null || mMasterPlaylist.renditions.length == 0) {
            return -1;
        }
        for (int i = 0; i < mMasterPlaylist.renditions.length; i++) {
            TTVideoEngineMasterPlaylist.TTVideoEngineRendition rendition = mMasterPlaylist.renditions[i];
            if (TextUtils.equals(videoVariant.audioGroupId, rendition.groupId)
                    && TextUtils.equals(rendition.type, "AUDIO")) {
                if (TextUtils.equals(rendition.language, mHlsAudioLanguage)) {
                    mHlsAudioRenditionInfoId = rendition.infoId;
                    return mHlsAudioRenditionInfoId;
                }
            }
        }
        return -1;
    }
});
```


<span id="79389acc"></span>
## Switching streams during playback

You can dynamically switch audio and video streams during playback by setting the appropriate `PLAYER_OPTION`.

<span id="fb5e965d"></span>
### Switching video streams by bandwidth

To switch video resolution, get the bandwidth of the target stream and set it by using `setIntOption`.

```Java
// Assuming mMasterPlaylist is the object saved in the streamInfos callback.
// Assuming the user selects the i-th video stream.
TTVideoEngineVariantStream targetStream = mMasterPlaylist.variantStreams[i];
int targetBandwidth = targetStream.bandwidth;

// Set option to switch.
videoEngine.setIntOption(PLAYER_OPTION_SET_MASTER_M3U8_VIDEO_BANDWIDTH, targetBandwidth);

// Listen for the switch result.
videoEngine.setVideoEngineCallback(new VideoEngineCallback() {
    @Override
    public void onVideoStreamBitrateChanged(Resolution resolution, int bitrate) {
        // For Master M3U8 playback, the resolution might be null after a successful switch.
        // Rely on the bitrate to determine if the switch to the target bandwidth is successful.
        Log.d("VideoPlay", "Switched to bitrate: " + bitrate);
    }
});
```


<span id="5beb9e51"></span>
### Switching audio streams by rendition ID

Obtain the `infoId` of the target audio track and set it as an option to switch.

```Java
// Assuming the user selects the j-th audio track.
TTVideoEngineRendition targetRendition = mMasterPlaylist.renditions[j];
int targetInfoId = targetRendition.infoId;

videoEngine.setIntOption(PLAYER_OPTION_SET_AUDIO_INFO_ID, targetInfoId);
```


<span id="eddb2b69"></span>
### UI implementation example

The following code demonstrates how to dynamically generate UI elements for selecting resolutions and audio tracks based on the `masterPlaylist` object. Call this method to build or update your UI after the `streamInfos` callback is triggered.

```Java
// Assuming mHlsVideoVariants is the list of video streams parsed from the MasterPlaylist.
// Assuming context is the current context.

// --- 1. Build the resolution selection UI ---
LinearLayout videoResolutionSelectLayout = new LinearLayout(context);
// Iterate through all available video streams.
for (int i = 0; i < mHlsVideoVariants.size(); i++) {
    // Get a single video stream object.
    final HLSChooseBestStream.Variant videoVariant = mHlsVideoVariants.get(i);
    // Create a TextView to display the resolution.
    final TextView textView = new TextView(context);
    // Set the displayed text, for example, "1280x720". Map this to "HD," "Full HD," and many other based on the production need.
    textView.setText(videoVariant.mWidth + "x" + videoVariant.mHeight);
    // Add the TextView to the layout.
    videoResolutionSelectLayout.addView(textView);

    // Set an OnClickListener for each resolution option.
    textView.setOnClickListener(new OnClickListener() {
        @Override
        public void onClick(View view) {
            // When the user clicks, record the index of the selected resolution.
            mHlsVideoVariantIndex = i;
            // Call setIntOption, passing the bandwidth of the target video stream to perform the switch.
            videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_SET_MASTER_M3U8_VIDEO_BANDWIDTH, videoVariant.mBandWidth);
        }
    });
}

// --- 2. Build the audio track selection UI ---
LinearLayout audioLanguageSelectLayout = new LinearLayout(context);
// Get the currently playing video stream object.
HLSChooseBestStream.Variant videoVariants = mHlsVideoVariants.get(mHlsVideoVariantIndex);
// Iterate through the playlists associated with the current video stream.
for (int i = 0; i < videoVariants.mPlaylists.length; i++) {
    HLSChooseBestStream.Playlist playlist = videoVariants.mPlaylists[i];
    // Iterate through all Renditions in the playlist (usually including audio, subtitles, and many other).
    for (int j = 0; j < playlist.mRenditions.length; j++) {
        HLSChooseBestStream.Rendition rendition = playlist.mRenditions[i];
        // Check if the current Rendition is an audio track.
        if (rendition != null && rendition.mMediaTrackType == MediaPlayer.TrackInfo.MEDIA_TRACK_TYPE_AUDIO) {
            // Create a TextView to display the audio track information.
            final TextView textView = new TextView(context);
            // Set the displayed text, for example, "Audio:en". Map this to "English," "Chinese," and many other based on the production need.
            textView.setText("Audio:" + rendition.mLanguage);
            // Add the TextView to the layout.
            audioLanguageSelectLayout.addView(textView);
            
            // Set an OnClickListener for each audio track option.
            textView.setOnClickListener(new OnClickListener() {
                @Override
                public void onClick(View view) {
                    // When the user clicks, record the infoId of the selected audio track.
                    mHlsAudioRenditionInfoId = rendition.mInfoId;
                    // Call setIntOption, passing the infoId of the target audio track to perform the switch.
                    videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_SET_AUDIO_INFO_ID, rendition.infoId);
                }
            });
        }
    }
}
```


<span id="9f1f0e5c"></span>
## Selecting streams during preloading

If you are using the SDK's [preloading strategy](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-short-video-best-practices), you can specify which streams to preload. This optimizes playback start time and saves bandwidth. To do this, implement `setPreloadChooseUrlCallback` and return a list of stream URLs and their desired preload sizes. The example below shows how to preload a 720p video stream and its corresponding audio track.

```Java
// Set the preload stream selection callback.
TTVideoEngine.setPreloadChooseUrlCallback(new TTVideoEnginePreloadHLSChooseUrlCallback() {
    /**
     * Implement custom preload selection logic in this callback.
     * @param masterPlaylist The parsed Master M3U8 object containing all stream information.
     * @return A list that informs the preload module which streams to cache.
     */
    @Override
    public List<TTVideoEnginePreloadUrlInfo> chooseUrls(TTVideoEngineMasterPlaylist masterPlaylist) {
        Log.v("VideoPlay", "chooseUrls:" + new Gson().toJson(masterPlaylist));

        if (masterPlaylist.variantStreams == null) {
            return null;
        }
        List<TTVideoEnginePreloadUrlInfo> urlInfos = new ArrayList<>();
        for (int i = 0; i < masterPlaylist.variantStreams.length; i++) {
            TTVideoEngineMasterPlaylist.TTVideoEngineVariantStream videoVariantStream = masterPlaylist.variantStreams[i];
            
            // 1. Find the target video stream to preload based on production requirements (such as resolution).
            if (videoVariantStream != null && videoVariantStream.resolution.equals("720x1280")) {
                
                TTVideoEnginePreloadUrlInfo videoUrlInfo = new TTVideoEnginePreloadUrlInfo();
                videoUrlInfo.uri = videoVariantStream.uri;
                videoUrlInfo.preloadSize = 500 * 1024; // Set the preload size.
                urlInfos.add(videoUrlInfo);

                if (masterPlaylist.renditions != null) {
                    for (int j = 0; j < masterPlaylist.renditions.length; j++) {
                        TTVideoEngineMasterPlaylist.TTVideoEngineRendition rendition = masterPlaylist.renditions[j];
                        if (rendition != null) {
                            // 2. Find the audio track associated with the video stream (AUDIO type and matching groupId).
                            if (TextUtils.equals(rendition.type, "AUDIO")
                                    && TextUtils.equals(videoVariantStream.audioGroupId, rendition.groupId)) {
                                
                                TTVideoEnginePreloadUrlInfo audioUrlInfo = new TTVideoEnginePreloadUrlInfo();
                                audioUrlInfo.uri = rendition.uri;
                                audioUrlInfo.preloadSize = 300 * 1024;
                                urlInfos.add(audioUrlInfo);
                                break;
                            }
                        }
                    }
                }
                break;
            }
        }
        Log.v("VideoPlay", "[preload] streams " + new Gson().toJson(urlInfos));
        return urlInfos;
    }
});
```


<span id="9bd8ac3d"></span>
## Resolving audio and video stuttering after HLS (TS) switching

If you are playing an HLS format video source with TS media segments and experience a brief audio and video stutter after switching the resolution, you can enable `PLAYER_OPTION_ENABLE_M3U8_SWITCH_OPTIMIZE` by using the `setIntOption` method.

```Java
// Enable HLS (TS) switch optimization to solve the audio and video stuttering issue after switching. (Added in version 1.50.200.3)
// Set the parameter to 1 to enable, and 0 to disable.
ttVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_M3U8_SWITCH_OPTIMIZE, 1);
```
