---
title: "React Native Player SDK: Release notes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-release-notes"
---

This page provides the release notes of the BytePlus VOD React Native Player SDK.


|**Release date** |**Version** |**Description** |**Native Player SDK versions** |
|---|---|---|---|
|May 15, 2026 |1.10.0 |**New features**: Picture\-in\-Picture updates. For details, see [Configure PiP](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-pip#5555b19a).<br><br><br>* Added support for Picture\-in\-Picture on Android.<br><br>* Added support for synchronizing the player view’s content fill mode with the Picture\-in\-Picture window.<br><br><br>**Bug fixes**:<br><br><br>* Fixed an issue where specific conditions in the iOS mini window could cause a crash. |* Android: 1.50.200.3<br><br>* iOS: 1.50.200.2 |
|February 10, 2026 |1.9.0 |**New features:** <br><br><br>* [React Native Player SDK: Adaptive Bitrate Streaming (ABR)](https://docs.byteplus.com/docs/byteplus-vod/abr-playback-rn)<br><br>* [React Native Player SDK: Video download and offline playback](https://docs.byteplus.com/docs/byteplus-vod/downloading-videos-rn)<br><br>* [React Native Player SDK: Initial bitrate selection](https://docs.byteplus.com/docs/byteplus-vod/initial-bitrate-selection-rn) |* Android: 1.49.100.2<br><br>* iOS: 1.49.100.2 |
|December 22, 2025 |1.8.0 |Supported [React Native Player SDK: Custom preloading](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-custom-preloading) |* Android: 1.48.200.1<br><br>* iOS: 1.48.200.2 |
|November 25, 2025 |1.7.0 |Supported the new architecture |* Android: 1.48.200.1<br><br>* iOS: 1.48.200.2 |
|August 25, 2025 |1.5.0 |**New features:** <br><br><br>* Supported [Preloading external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-external-subtitles#5ca2c4cb)<br><br>* Supported [Seamless switching between multiple resolutions](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-features#2cc57ef2) |* Android: 1.47.200.5<br><br>* iOS: 1.47.200.2 |
|July 24, 2025 |1.4.0 |**New features:** <br><br><br>* Optimized the scaling mode on Android, allowing the video scaling mode to be set during player initialization.<br><br>* Improved Picture\-in\-Picture (PIP) interaction.<br><br>* Enabled the Media Data Loader (MDL) by default for subtitle loading to improve loading speed.<br><br><br>**Bug fixes:** <br><br><br>* Fixed an issue on iOS where audio played without video under specific conditions. |* Android: 1.46.300.1<br><br>* iOS: 1.46.300.1 |
|June 13, 2025 |1.3.0 |**New features:** <br><br><br>* Added support for [Picture-in-picture](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-basic-features#4ea4fb1f).<br><br>* Added support for video progress bar thumbnail preview, see [Displaying sprites](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-best-practices#8c107237). |* Android: 1.45.300.1<br><br>* iOS: 1.45.300.3 |
|April 29, 2025 |1.2.4 |**New features:** <br><br><br>* Added the `onCurrentPlaybackTimeUpdate` callback that monitors the current playback time.<br><br>* Added support for external subtitles in SRT format.<br><br><br>**Bug fixes:**  Fixed a bug that prevented the `PlayerViewComponent` from functioning properly in React 19. |* Android: 1.45.300.1<br><br>* iOS: 1.45.300.3 |
|April 10, 2025 |1.2.3 |Fixed crashes on Android devices running older versions. |* Android: 1.45.300.1<br><br>* iOS: 1.45.300.1 |
|March 14, 2025 |1.2.2 |Added support for arm64 and x86\-64 simulator testing and debugging on iOS. |* Android: 1.45.300.1<br><br>* iOS: 1.45.300.1 |
|February 10, 2025 |1.2.1 |Fixed an issue where the video displayed a black screen after returning from a secondary playback page. |* Android: 1.45.100.4<br><br>* iOS: 1.45.100.3 |
|January 24, 2025 |1.2.0 |Optimized memory usage. |* Android: 1.45.100.4<br><br>* iOS: 1.45.100.3 |
|December 19, 2024 |1.1.4 |Fixed an issue where the Android player container repeatedly triggered load events. |* Android: 1.42.300.101<br><br>* iOS: 1.42.300.102 |
|November 14, 2024 |1.1.3 |Enhanced the stability of Native Module calls in iOS development mode. |* Android: 1.42.300.101<br><br>* iOS: 1.42.300.102 |
|October 25, 2024 |1.1.1 |Lowered the minimum supported Android system version requirement from `minSdkVersion: 26` to `minSdkVersion: 23`. |* Android: 1.42.300.101<br><br>* iOS: 1.42.300.102 |
|October 12, 2024 |1.1.0 |**New features:** <br><br><br>* [Pre-rendering strategy](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-basic-features#44a16ad8)<br><br>* [External subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-basic-features#bb41753c) |* Android: 1.42.300.101<br><br>* iOS: 1.42.300.102 |
|September 9, 2024 |1.0.0 |This is the first release of the BytePlus VOD Player SDK for React Native. For supported features, see [Player SDK features](https://docs.byteplus.com/docs/byteplus-vod/docs-player-features). |* Android: 1.42.300.101<br><br>* iOS: 1.42.300.102 |
