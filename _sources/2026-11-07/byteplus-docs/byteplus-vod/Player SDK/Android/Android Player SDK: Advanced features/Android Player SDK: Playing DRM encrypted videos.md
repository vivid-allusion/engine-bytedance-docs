---
title: "Android Player SDK: Playing DRM encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-drm-videos-android"
---

BytePlus VOD supports DRM (Digital Rights Management) encryption for scenarios requiring copyright protection. This article introduces how to play DRM\-encrypted videos using the Player SDK.

<span id="511315ad"></span>
## Prerequisites


* Configure the DRM licenses and encrypt your content in the BytePlus VOD console. For details, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption).

* To play DRM encrypted videos in Vid mode, your application server needs to generate temporary playback token and DRM auth token before playback, and then provide them to the client. You can use the BytePlus VOD Server SDKs to generate these tokens. For more information, refer to the documentation provided below:

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* Integrate the Player SDK 1.42.300.101 or later versions.

* To play Widevine encrypted videos, the device must support Widevine technology and associated decryption capabilities. For details, see [MediaDrm](https://developer.android.com/reference/android/media/MediaDrm) or [MediaPlayer.DrmInfo](https://developer.android.com/reference/android/media/MediaPlayer.DrmInfo).


<span id="6c12304f"></span>
## Implementation


1. Build the video source:

   ```Java
   String vid = "YOUR_VIDEO_ID"; // Obtained from your app server
   String playAuthToken = "YOUR_PLAYAUTHTOKEN"; // Obtained from your app server
   String drmLicenseAuthToken = "YOUR_DRMLICENSE_TOKEN"; // Obtained from your app server
   
   // Set playback source with Vid
   VidPlayAuthTokenSource vidSource = new VidPlayAuthTokenSource.Builder()
           .setVid(vid)
           .setPlayAuthToken(playAuthToken)
           .build();
   ```
   

2. Initialize the video player:

   ```Java
   // To play DRM videos, the following features must be enabled
   // Enable DRM playback
   mVideoEngine.setIntOption(PLAYER_OPTION_UPDATE_WIDEVINE_DRM, 1);
   // Set DRM type to WideVine
   mVideoEngine.setIntOption(PLAYER_OPTION_DRM_TYPE, DRM_TYPE_WIDEVINE);
   // Enable hardware video decoding
   mVideoEngine.setIntOption(PLAYER_OPTION_ENABEL_HARDWARE_DECODE, 1);
   // Enable hardware audio decoding
   mVideoEngine.setIntOption(PLAYER_OPTION_SET_MEDIA_CODEC_AUDIO, 1);
   // Disable software decoding fallback
   mVideoEngine.setIntOption(PLAYER_OPTION_ENABLE_FALLBACK_SW_DEC, 0);
   // Disable hardware decoding reuse
   mVideoEngine.setIntOption(PLAYER_OPTION_DISABLE_MC_REUSE, 1);
   ```
   

3. Set the video source and start playback:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When playing DRM videos, it is recommended to use <code>SurfaceView</code> for video rendering.   </div>
   

   ```Java
   mVideoEngine.setStrategySource(vidSource);
   // Set the DRM auth token
   mVideoEngine.setDrmLicenseAuthToken(drmLicenseAuthToken);
   mVideoEngine.setSurface(surface);
   mVideoEngine.play();
   ```
