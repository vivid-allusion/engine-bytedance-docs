---
title: "iOS Player SDK: Troubleshooting"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-troubleshooting"
---

This document describes common issues and solutions when using the iOS Player SDK.

<span id="75339b13"></span>
## Progress regression due to audio/video track duration mismatch

<span id="56ac82b6"></span>
### Issue

Some MP4 files have audio tracks that are shorter than the video tracks. When playback is enabled on iOS devices, the progress bar may regress approximately 1 second near the end of playback.

<span id="9a1ce8b7"></span>
### Solution

Set the player clock type before playback:

```objectivec
[self.videoEngine setOptionForKey:VEKKeyPlayerNormalClockType_NSInteger value:@(2)];
```


<span id="c1dcbd0e"></span>
## Playback failure due to invalid cached data

<span id="d963750f"></span>
### Issue

When local MDL cache data is abnormal or corrupted, the player may return error code `-499960`. This error typically indicates that the cached data is invalid, causing resource loading to fail.

<span id="fb8c702c"></span>
### Solution

Enable the SDK's automatic cleanup of abnormal cache data:

```objectivec
[self.videoEngine setOptionForKey:VEKKeyEnableClearMdlCache_BOOL value:@(YES)];
```
