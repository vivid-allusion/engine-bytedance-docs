---
title: "iOS Player SDK: Custom stream selection for standard Master M3U8 playback sources"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/custom-stream-selection-for-master-m3u8-ios"
---

For a standard Master M3U8 playback source, the Player SDK provides fine\-grained control over stream selection. This allows you to programmatically choose which video and audio streams to use at different stages of the playback lifecycle.

<span id="a2e36382"></span>
## Selecting initial video and audio streams

To specify the initial video and audio stream indexes through delegate methods, implement the `masterPlaylistDelegate`. This callback is triggered after the Player SDK has parsed the Master M3U8 file, but before it starts downloading media segments. The procedures are as follows:


1. Set the delegate: Set the `masterPlaylistDelegate` for the player instance and conform to the `TTVideoEngineMasterPlaylistDelegate` protocol.

2. Receive streams: The SDK triggers the `onMasterPlaylist` callback after it has parsed M3U8. You can obtain and save the `masterPlaylist` object of all video streams (`variantStreams`) and audio streams (`renditions`).

   ```objectivec
   // Conform to the TTVideoEngineMasterPlaylistDelegate protocol
   // @interface YourViewController () <TTVideoEngineMasterPlaylistDelegate>
   
   // Set the delegate
   self.videoEngine.masterPlaylistDelegate = self;
   
   #pragma mark - TTVideoEngineMasterPlaylistDelegate
   /**
    * Callback after M3U8 is parsed.
    * Save the masterPlaylist object for use when switching resolution or audio track during playback.
    */
   - (void)videoEngine:(TTVideoEngine *)videoEngine onMasterPlaylist:(TTVideoEngineMasterPlaylist *)masterPlaylist {
       self.masterPlaylist = masterPlaylist;
       NSLog(@"Master playlist parsed, available video streams: %ld", (long)masterPlaylist.variantStreams.count);
   }
   ```
   

3. Return decision indexes: Return to your selected video and audio stream indexes by `indexOfVariantOnPlayMasterPlaylist` and `indexOfRenditionOnPlayMasterPlaylist`. The following example code displays starting playback with 720p resolution and an English audio:

   ```objectivec
   // Return the index of the initial video stream, -1 means automatic selection
   - (int)videoEngine:(TTVideoEngine *)videoEngine indexOfVariantOnPlayMasterPlaylist:(TTVideoEngineMasterPlaylist *)masterPlaylist {
       if (self.masterPlaylistPlayTargetIndex >= -1 && self.masterPlaylistPlayTargetIndex < (int)masterPlaylist.variantStreams.count) {
           return self.masterPlaylistPlayTargetIndex;
       }
       NSLog(@"Resolution selection error: Current video supports: -1 ~ %d. Default resolution will be played.", (int)(masterPlaylist.variantStreams.count - 1));
       return -1;
   }
   
   // Return the streamId of the initial audio stream, -1 means automatic selection
   - (int)videoEngine:(TTVideoEngine *)videoEngine indexOfRenditionOnPlayMasterPlaylist:(TTVideoEngineMasterPlaylist *)masterPlaylist {
       if (self.masterPlaylistAudioTrackIndex == -1) {
           return -1;
       }
   
       if (self.masterPlaylistAudioTrackIndex >= 0 && self.masterPlaylistAudioTrackIndex < (int)masterPlaylist.renditions.count) {
           return [[self.masterPlaylist.renditions objectAtIndex:self.masterPlaylistAudioTrackIndex].inStreamId intValue];;
       }
       NSLog(@"Resolution selection error (rendition): Current video supports: -1 ~ %d. Default rendition will be played.", (int)(masterPlaylist.renditions.count - 1));
       return -1;
   }
   ```
   


<span id="7a018f6b"></span>
## Switching streams during playback

<span id="eb7db2eb"></span>
### Switching video streams by bandwidth

To switch video resolution, get the bandwidth of the target stream and call `setIntOption` to pass the`PLAYER_OPTION_SET_MASTER_M3U8_VIDEO_BANDWIDTH` as the key and the bandwidth as the value.

```objectivec
NSString* inputBitrate = [_inputBitrateTextView.text stringByTrim];
// Switch video stream via setOptionForKey
[self.player.videoEngine setOptionForKey:VEKKeySetMasterm3u8VideoBandwidth_NSInteger value:@(inputBitrate.intValue)];
```


<span id="63dc2b44"></span>
### Switching audio streams by Info ID

Get the `InfoId` of the target audio track and call `setOptionForKey:value:`to switch. This passes the `VEKKeyPlayerSwitchAudioInfoId_NSInteger` as the key and the `InfoId` as the value.

```objectivec
NSString* inputStreamId = [_inputStreamIdTextView.text stringByTrim];
// Switch audio stream via setOptionForKey
[self.player.videoEngine setOptionForKey:VEKKeyPlayerSwitchAudioInfoId_NSInteger value:@(inputStreamId.intValue)];
```


<span id="fc9bd516"></span>
## Selecting streams during preloading

If you are using the SDK's [Use preloading strategy](https://docs.byteplus.com/docs/byteplus-vod/docs-ios-player-short-video-best-practices#166886ef), you can specify which streams to preload. By setting `TTVideoEnginePreloadDelegate`, you can return the indexes of the streams to be preloaded through delegate methods after the M3U8 has been parsed.

```objectivec
// Set the preload delegate
// @interface YourAppDelegate () <TTVideoEnginePreloadDelegate>
[TTVideoEngine ls_setPreloadDelegate:self];

#pragma mark - TTVideoEnginePreloadDelegate

// Return the index of the video stream to be preloaded, -1 means automatic selection
- (int)indexOfVariantOnPreloadMasterPlaylist:(TTVideoEngineMasterPlaylist *)masterPlaylist {
    if (self.masterPlaylistPreloadTargetIndex >= -1 && self.masterPlaylistPreloadTargetIndex < (int)masterPlaylist.variantStreams.count) {
        return self.masterPlaylistPreloadTargetIndex;
    }
    NSLog(@"Resolution selection error: Current video supports: -1 ~ %d. Default resolution will be preloaded.", (int)(masterPlaylist.variantStreams.count - 1));
    return -1;
}

// Returns the index of the audio stream to be preloaded, -1 means automatic selection
- (int)indexOfRendtionOnPreloadMasterPlaylist:(TTVideoEngineMasterPlaylist *)masterPlaylist {
    if (masterPlaylist.renditions.count == 0) {
        return -1;
    }

    if (self.masterPlaylistPreloadTargetIndex >= -1 && self.masterPlaylistPreloadTargetIndex < (int)masterPlaylist.renditions.count) {
        return self.masterPlaylistPreloadTargetIndex;
    }
    NSLog(@"Resolution selection error (rendition): Current video supports: -1 ~ %d. Default rendition will be preloaded.", (int)(masterPlaylist.renditions.count - 1));
    return -1;
}
```


<span id="5a5a4a4b"></span>
## Resolving audio and video stuttering after HLS (TS) switching

If you are playing an HLS format video source with TS media segments and experience a brief audio and video stutter after switching the resolution, you can enable `VEKKeyIsHLSEnableMasterSwitchOptimize` by using the `setOptionForKey` method.

```objectivec
// Enable this switch for the videoEngine instance before playback to resolve the issue.
[self.videoEngine setOptionForKey:VEKKeyIsHLSEnableMasterSwitchOptimize value:@(YES)];
```
