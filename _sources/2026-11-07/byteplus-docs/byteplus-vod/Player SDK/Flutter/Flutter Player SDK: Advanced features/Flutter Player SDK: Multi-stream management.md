---
title: "Flutter Player SDK: Multi-stream management"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-multi-stream-management"
---

For videos with multiple resolutions, audio tracks, or subtitles, the player SDK enables precise management and switching throughout playback. This article provides the multi\-stream implementation in detail and guides you how to integrate and optimize the switching experience.

<span id="2ddf7e5f"></span>
## Overview

The player SDK supports both **self\-developed protocols** and **standard protocols** for multi\-stream solutions, allowing flexible selection based on your business needs and media asset sources.


|**Protocol type** |**Playback mode** |**Core principle** |**Advantages** |**Disadvantages** |**Applicable scenarios** |
|---|---|---|---|---|---|
|**Self\-developed protocol** |**Vid mode** |The client requests a video using its Vid. In response, the VOD server delivers a VideoModel containing all available resolutions. |* Easy integration with strong security.<br><br>* Clear client\-side logic.<br><br>* The server automatically handles resolution downgrades and associates related media assets.<br><br>* Supports smooth switching with frame alignment. |Relies on BytePlus VOD service with limited low\-level control over audio tracks and subtitles. |Suitable for scenarios where all media assets are fully hosted on BytePlus VOD. |
||**VideoModel mode** |Your server\-side application constructs or obtains a complete VideoModel from VOD and delivers it to the client. |* Optimal performance with reduced network requests from the client\-side to VOD services.<br><br>* Faster Time to First Frame (TTFF).<br><br>* Manages multiple streams in the same way as the Vid mode. |You must implement custom, moderately complex logic to build the VideoModel. |Designed for scenarios requiring extremely fast first\-frame performance, such as short video feeds. |
|**Standard protocol** |**HLS (Master M3U8)**  |The client directly plays standard Master M3U8 files. After the SDK parses the file, you have fine\-grained control over streams, audio tracks, and subtitles through underlying callbacks and option settings. |* Offers the highest compatibility, suitable for any source of HLS streams.<br><br>* Provides granular control and maximum flexibility. |* The most complex client\-side implementation.<br><br>* Requires you to manually handle stream traversal, decision\-making, and switching. |Used for scenarios where you need to play third\-party HLS streams or require precise management of audio tracks and subtitles. |
||**DASH** |This feature is in development. ||||


<span id="1fa29a96"></span>
## Vid/VideoModel mode

Vid mode and VideoModel mode share a simple and intuitive set of APIs.

<span id="1cc84fa3"></span>
### Prerequisites

Before starting any multi\-stream related development, make sure you have completed the following preparations:


1. Generate multi\-resolution videos and ensure your server\-side delivers correct video playback information:

   * For Vid mode:

      * You must use the video transcoding feature of the Video on Demand (VOD) media processing service to generate video streams in multiple resolutions. See [Audio and video transcoding](https://docs.byteplus.com/en/docs/byteplus-vod/docs-audio-and-video-transcoding).

      * When your server issues a `PlayAuthToken` to the client, you can omit the `Definition` parameter. When VOD responds to the playback request, it will return playback URLs for all available resolutions of the video by default.

   * For VideoModel mode: Video data can come from **BytePlus VOD**, **third\-party services** , or **custom data**. See [Android Player SDK: VideoModel](https://docs.byteplus.com/en/docs/byteplus-vod/videomodel-android).

2. Integrate SDK: Make sure you have followed the [Flutter Player SDK: Integrating the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-quickstart) and [Flutter Player SDK: Basic features](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features) to complete steps such as initializing the SDK, creating a player, and setting a playback source.


<span id="9fed9d57"></span>
### Set initial resolution

To specify the initial video resolution, call `play` after calling `configResolutionBeforeStart`. If the resolution you set does not exist in the `supportedResolutionTypes` list, the SDK will automatically select the next lowest available resolution for playback.

```Dart
// Set initial playback resolution
player.configResolutionBeforeStart(<TTVideoEngineResolutionType>);
```


<span id="a9e46d12"></span>
### Get current resolution

```Dart
// Get resolution information. This must be called after onPrepared
TTVideoEngineResolutionType resolution = await player.currentResolution;
```


<span id="3d040420"></span>
### Get resolution list

When TTVideoEngine receives the fetchedVideoModel callback, you can call the supportedResolutionTypes method to get an array of all available resolutions. You can use this array to display the resolution list and implement the logic for selecting resolutions. Here is an example:

```Dart
player.fetchedVideoModel = () async { 
    List<TTVideoEngineResolutionType>? resTypes = await player.supportedResolutionTypes; 
};
```


<span id="b9e4d12d"></span>
### Switch resolution

```Dart
// Set resolution before starting playback
player.configResolutionBeforeStart(<TTVideoEngineResolutionType>);

// Switch resolution after starting playback
player.configResolutionAfterStart(targetResolution:<TTVideoEngineResolutionType>);
```


<span id="01d1108b"></span>
## HLS Master M3U8 mode

<span id="619ca9fa"></span>
### Pre\-playback bitrate selection

```Dart
// Method defined in VodPlayerFlutter
/* 
    Pre-playback bitrate selection for master M3U8
    getHlsStreamInfos - Bitrate callback
    selectHlsVideoStream - Video bitrate selection, returns the bandwidth of the selected video stream
    selectHlsRendition - Audio track selection, returns the infoId of the selected audio rendition
    switchHlsVideoBitrate - Bitrate selection callback, returns the bandwidth of the selected bitrate if a switch occurs
*/
Future<void> setHLSMultiBitrateConfig(
    {void Function(TTMasterPlaylist playlist)? getHlsStreamInfos,
    int? Function()? selectHlsVideoStream,
    int? Function(int variantIndex)? selectHlsRendition,
    void Function(int bitrate)? switchHlsVideoBitrate})
    
// Example code (using random bitrate selection as an example, for reference only)
_player?.setHLSMultiBitrateConfig(
    getHlsStreamInfos: (TTMasterPlaylist playlist) {
      _playlist = playlist;
      print('HLS bitrate callback: ${playlist.toJson()}');
    },
    selectHlsVideoStream: () {
      // Example: Randomly select a bitrate
      if (_playlist!.variantStreams!.isNotEmpty) {
        int index = Random().nextInt(_playlist!.variantStreams!.length);
        TTMasterVariantStream stream = _playlist!.variantStreams![index];
        print('HLS video playback bitrate selected, random index=$index, resolution-${stream.resolution} bandwidth-${stream.bandwidth}');
        return stream.bandwidth;
      }
      return -1;
    },
    selectHlsRendition: (int variantIndex) {
      // Example: Select audio track 'en'
      for (TTMasterRendition rendition in _playlist!.renditions!) {
        if (rendition.variantIndex != variantIndex) {
          continue;
        }
        if (rendition.language == 'en') {
          print('HLS audio playback bitrate selected, rendition.language=${rendition.language}, rendition.infoId-${rendition.infoId}');
          return rendition.infoId;
        }
      }
      return -1;
    },
    switchHlsVideoBitrate: (int bitrate) {
      print("HLS bitrate selection completed, final bitrate = $bitrate");
    },
);
```


<span id="72e9fd77"></span>
### Bitrate switching during playback

```Dart
// Switch HLS video bitrate during playback. If the specified bitrate does not exist, the closest available bitrate will be selected.
Future<void> switchHlsVideoBitrate({required int bitrate})

// Switch the HLS audio track during playback. If the specified audioInfoId does not exist, no switch will occur.
Future<void> switchHlsAudioRendition({required audioInfoId})
```


<span id="e3fae593"></span>
### Bitrate selection for preloading

```Dart
// Method defined in TTVideoEnginePreload
/* 
    Pre-playback bitrate selection for master M3U8
    getHlsStreamInfos - Bitrate callback
    selectHlsVideoStream - Video bitrate selection, returns the bandwidth of the selected video stream
    selectHlsRendition - Audio track selection, returns the infoId of the selected audio rendition
    switchHlsVideoBitrate - Bitrate selection callback, returns the bandwidth of the selected bitrate if a switch occurs
*/
Future<void> setHLSMultiBitrateConfig(
    {void Function(TTMasterPlaylist playlist)? getHlsStreamInfos,
    int? Function()? selectHlsVideoStream,
    int? Function(int variantIndex)? selectHlsRendition,
    void Function(int bitrate)? switchHlsVideoBitrate})
    
    
// Example code (using random bitrate selection as an example, for reference only)
TTVideoEnginePreload.setMasterPlaylistPreloaderCallback(
      onMasterM3U8PlaylistSelectPreloadUrls: (TTMasterPlaylist playlist) {
    if (playlist.variantStreams!.isEmpty) {
      return null;
    }
    List<TTMasterPreloadURLInfo> urlInfos = [];

    // Preload video stream
    int index = Random().nextInt(playlist.variantStreams!.length);
    TTMasterVariantStream stream = playlist.variantStreams![index];
    TTMasterPreloadURLInfo urlInfo = TTMasterPreloadURLInfo(uri: stream.uri, preloadSize: 800 * 1024);
    urlInfos.add(urlInfo);
    print('Preloading playlist, randomly selected video stream uri=${stream.uri}, resolution=${stream.resolution} bandwidth=${stream.bandwidth}');

    // Preload audio stream
    if (playlist.renditions == null) {
      return urlInfos;
    }

    for (TTMasterRendition rendition in playlist.renditions!) {
      if (rendition.groupId == stream.audioGroupId) {
        TTMasterPreloadURLInfo urlInfo = TTMasterPreloadURLInfo(uri: rendition.uri, preloadSize: 500 * 1024);
        urlInfos.add(urlInfo);
        print('Preloading playlist audio stream uri=${rendition.uri}');
      }
    }
    return urlInfos;
  });
```


<span id="0569c84f"></span>
## Enable seamless switching

You can enable seamless resolution switching for frame\-aligned MP4, M3U8, and DASH videos generated by the BytePlus VOD service. This feature is available in Vid or VideoModel mode and enhances the playback experience. To enable it, use the following code:

```Dart
 player.setSmoothSwitchEnable(true);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please contact the BytePlus support team by <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">submitting a ticket</a> to receive assistance in setting up video transcoding templates to produce keyframe\-aligned videos.</div>


<span id="83e57bd0"></span>
## Reference

<span id="a1f6454a"></span>
### Resolution enumeration


|Resolution |Video resolution |Audio quality |Video description |Audio description |
|---|---|---|---|---|
|TTVideoEngineResolutionTypeSD |360P |medium |Standard definition |Standard audio quality |
|TTVideoEngineResolutionTypeHD |480P |higher |High definition |High audio quality |
|TTVideoEngineResolutionTypeHD_H |540P |`-` |540P |`-` |
|TTVideoEngineResolutionTypeFullHD |720P |highest |High definition |Highest audio quality |
|TTVideoEngineResolutionType1080P |1080P |original |1080P |Original resolution |
|TTVideoEngineResolutionType2K |2K |`-` |2K |`-` |
|TTVideoEngineResolutionType4K |4K |`-` |4K |`-` |


&nbsp;

&nbsp;
