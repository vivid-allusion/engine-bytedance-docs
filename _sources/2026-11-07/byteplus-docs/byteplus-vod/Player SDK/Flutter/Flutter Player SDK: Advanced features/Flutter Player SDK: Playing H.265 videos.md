---
title: "Flutter Player SDK: Playing H.265 videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-playing-h265-videos"
---

To play high\-efficiency H.265 (HEVC) videos in your Flutter application while avoiding common compatibility issues, you can leverage the Player SDK. This guide demonstrates how to implement H.265 playback using the SDK's intelligent decoding strategy. The SDK automatically switches between software and hardware decoding based on device profiles, effectively preventing playback failures, screen tearing, and black screens.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="28ab5513"></span>
## Playing H.265 videos in Vid mode

```Dart
void vidPlay() async {
    String vid = "your play vid";
    String playAuthToken = "your play auth token";
    TTVideoEngineResolutionType? resolutionType = TTVideoEngineResolutionType.TTVideoEngineResolutionTypeHD;
    TTVideoEngineEncodeType encodeType = TTVideoEngineEncodeType.h264;
    // If the device supports H.265, request an H.265 playback source
    var enableH265 = await FlutterTTSDKManager.isSupportH265HardwareDecode();
    if (!(enableH265 == null || !enableH265)) {
      encodeType = TTVideoEngineEncodeType.h265;
    }
    // Initialize the playback source
    TTVideoEngineVidSource source = TTVideoEngineVidSource.init(
        vid: vid, playAuthToken: playAuthToken, resolution: resolutionType, encodeType: encodeType);
    // Set playback source
    await _player?.setVidSource(source);
    // Start playback
    await _player?.play();
}
```


<span id="e729854b"></span>
## Playing H.265 videos in DirectUrl mode

```Dart
void urlPlay() async {
    // If FlutterTTSDKManager.isSupportH265HardwareDecode(): true, then set the H.265 playback source
    // If FlutterTTSDKManager.isSupportH265HardwareDecode(): false, then set the H.264 playback source
    String url = "play url"; 
    String cacheKey = "cache key";
    // Initialize the playback source
    TTVideoEngineUrlSource source = TTVideoEngineUrlSource.initWithURL(url, cacheKey);
    // Set playback source
    await _player?.setUrlSource(source);
    // Start playback
    await _player?.play();
}
```


&nbsp;
