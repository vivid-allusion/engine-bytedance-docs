---
title: "Flutter Player SDK: Adding external subtitles"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-adding-external-subtitles"
---

The Player SDK supports adding WebVTT (Web Video Text Tracks) subtitle files, allowing users to keep subtitles separate from video files and import them during video playback. For more details and prerequisites on this feature, please refer to [iOS Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-ios).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="c0d57a29"></span>
## Enabling the external subtitles feature

To enable the external subtitles feature, use the following sample code:

```Dart
/// Enable the external subtitles feature. Call this method before calling prepare
Future<void> setSubtitleEnabled(bool enabled)
```


<span id="a50371a6"></span>
## Setting subtitle source

The Player SDK offers two methods for setting the subtitle source. Select the appropriate method based on your specific needs:


* Method 1: Using Vid and SubtitleToken

   ```Dart
   /// Set subtitle auth token
   Future<void> setSubtitleAuthToken(String subtitleAuthToken)
   ```
   

* Method 2: Using the subtitle URL

   ```Dart
   /// Set url subtitle list. Call this method after createPlayer and before prepare
   Future<void> setSubtitles(List<TTSubtitle> subtitles)
   ```
   


<span id="9ff2cbcc"></span>
## Enabling or disabling subtitle display

To control whether subtitles are displayed during playback, use the following sample code:

```Dart
/// Enable subtitle rendering. Call this method after createPlayer
Future<void> setSubtitleShow(bool enabled)
```


<span id="a1127db3"></span>
## Switching between subtitles

To switch to a different subtitle during playback, use the following sample code:

```Dart
/// Select a subtitle to display. Call this method after createPlayer
Future<void> setSelectedSubtitle(int subtitleId);
```


<span id="dd51bcf4"></span>
## Setting subtitle callbacks

Use the following sample code to set the subtitle\-related callbacks:

```Dart
/// Callback for fetching subtitle information in Vid mode
Future<void> Function(bool success, List<TTSubtitle>? subtitles, TTError? error)? onSubtitlesFetched;

/// Callback for the result of loading a subtitle file
Future<void> Function(bool success)? onSubtitleFileLoadResult;

/// Callback for when a subtitle is selected
Future<void> Function(bool success, int subtitleId)? onSubtitleSelected;

/// Callback for updating subtitle content
Future<void> Function(String? content, int pts, int duration)? onSubtitleShow;
```
