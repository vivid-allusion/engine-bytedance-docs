---
title: "Flutter Player SDK: Release notes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-release-notes"
---

This page provides the release notes of the BytePlus VOD Flutter Player SDK.

|**Release date** |**Version** |**Description** |
|---|---|---|
|October 16, 2026 |1.52.101 |Supports [log retrieval](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-log-retrieval). |
|September 22, 2026 |1.52.100 |* Upgraded the Android native SDK dependency to 1.52.100.5.<br><br>* Upgraded the iOS native SDK dependency to 1.52.100.4. |
|August 14, 2026 |1.51.201 |* Supports [Flutter Player SDK: Playing private encrypted videos](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-playing-private-encrypted-videos).<br><br>* Supports playing local video files using a [local file playback source](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#fde3b4dd).<br><br>* Added the `onCurrentPlaybackTimeUpdate`, `onVideoSizeChanged`, and `onVideoStreamBitrateChanged` [callbacks](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#6ffe13c6) for the playback time, video size, and video stream bitrate. |
|July 10, 2026 |1.50.103 |Supports [Flutter Player SDK: Automatic playback source refresh](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-automatic-playback-source-refresh). |
|April 27, 2026 |1.50.100 |Optimized the retry configuration for VideoModel. |
|January 14, 2026 |1.49.101 |* **New features**: Added the `onMediaCacheChange` callback. You can now listen to this callback to determine if the current playback has successfully hit the preloaded cache. For details, see [Flutter Player SDK: Custom preloading](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-custom-preloading) and [Preloading strategy](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-preloading-pre-rendering#f8a7066a).<br><br>* **Improvements:** <br><br>   * Supported downloading **FairPlay encrypted videos**. For details, see [Flutter Player SDK: Downloading videos](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-downloading-videos).<br><br>   * Optimized the APIs for the pre\-rendering feature, improving stability and ease\-of\-use, especially in complex feed scenarios. For details, see [Pre-rendering strategy](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-preloading-pre-rendering#a52763d5).<br><br>   * Updated the volume control APIs. The original `setVolume` and `getVolume` methods have been deprecated. Please migrate to the new `setNormalizedVolume` and `getNormalizedVolume` methods. For details, see [Set the volume](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#f757beef) and [Get the volume](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#b8922776). |
|December 15, 2025 |1.48.200 |Supports [Flutter Player SDK: Picture-in-picture](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-picture-in-picture) (PiP) on Android. |
|December 8, 2025 |1.48.100 |* Supports VideoModel playback sources:<br><br>   * Adds the ability to build playback sources using VideoModel, compatible with HLS and MP4 formats. For details, see [Set the playback source](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#fde3b4dd).<br><br>   * Enables seamless resolution switching and includes an improved preloading strategy.<br><br>* Supports initial bitrate playback selection, see [Flutter Player SDK: Initial bitrate selection for M3U8](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-initial-bitrate-selection).<br><br>* Fixed several issues. |
|September 28, 2025 |1.47.203 |Fixed several issues. |
|September 17, 2025 |1.47.200 |* Android: Optimized memory allocation to align with [Android's 16KB page size](https://developer.android.com/guide/practices/page-sizes).<br><br>* iOS: Added support for seeking while the app is in background mode. |
|August 6, 2025 |1.46.303 |Fixed several issues. |
|June 30, 2025 |1.46.302 |* Supports [Flutter Player SDK: Picture-in-picture](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-picture-in-picture) (PiP) on iOS.<br><br>* Supports [Using a prerendered first frame as the cover image](https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-preloading-pre-rendering#advanced-usage). |
|May 28, 2025 |1.46.301 |* Supports [Flutter Player SDK: Downloading videos](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-downloading-videos).<br><br>* Supports taking and saving [Screenshots](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#f92e26e0).<br><br>* Supports specifying the index for the preload strategy, see [Preloading strategy](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-preloading-pre-rendering#f8a7066a).<br><br>* Supports arm64 simulator testing and debugging. See [Test and debug in arm64 simulator (iOS)](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features#18e23277). |
|January 23, 2024 |1.44.3\-7 |Fixed several issues. |
|January 7, 2024 |1.44.3\-4 |Supports seamless resolution switching during playback. |
|December 30, 2024 |1.44.3\-3 |Supports [Flutter Player SDK: Playing DRM encrypted videos](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-playing-drm-encrypted-videos). |
|November 29, 2024 |1.44.2\-1 |Supports preloading and pre\-rendering strategies for short video scenarios on iOS. |
|October 10, 2024 |1.42.3\-4 |(iOS only) Adds the `clipToBounds` method to support clipping the canvas. |
|August 9, 2024 |1.42.3\-2 |Supports [Flutter Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-adding-external-subtitles). |
|July 25, 2024 |1.42.3\-1 |This is the first release of the BytePlus VOD Player SDK for Flutter. For supported features, see [Player SDK features](https://docs.byteplus.com/docs/byteplus-vod/docs-player-features). |
