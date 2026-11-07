---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086"
---

# ByteRTCMediaPlayer

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMediaPlayer :NSObject
```

> Available since 3.53

Media player

Call [setEventHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-seteventhandler) to set the callback handler to receive related callbacks.

## Member Functions

|Return |Name |
|---|---|
|int |[open:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-open-config) |
|int |[start](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-start) |
|int |[openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-openwithcustomsource-config) |
|int |[stop](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-stop) |
|int |[pause](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-pause) |
|int |[resume](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-resume) |
|int |[setVolume:type:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setvolume-type) |
|int |[getVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-getvolume) |
|int |[getTotalDuration](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-gettotalduration) |
|int |[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-getplaybackduration) |
|int |[getPosition](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-getposition) |
|ByteRTCPlayerState |[getState](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-getstate) |
|int |[setAudioPitch:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setaudiopitch) |
|int |[setPosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setposition) |
|int |[setAudioDualMonoMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setaudiodualmonomode) |
|int |[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-getaudiotrackcount) |
|int |[selectAudioTrack:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-selectaudiotrack) |
|int |[setPlaybackSpeed:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setplaybackspeed) |
|int |[setProgressInterval:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setprogressinterval) |
|int |[setLoudness:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setloudness) |
|int |[registerAudioFrameObserver:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-registeraudioframeobserver) |
|int |[pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-pushexternalaudioframe) |
|int |[setEventHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-seteventhandler) |

## Instructions

### open:config:

```objectivec
- (int)open:(NSString*_Nullable)filePath config:(ByteRTCMediaPlayerConfig*_Nullable)config;
```

Open the audio file.

You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.

For audio file in PCM format, see [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-openwithcustomsource-config). `openWithCustomSource` and this API are mutually exclusive.

**Input Parameters**

|Audio file paths.<br><br> <br><br>URL of online file, URI of local file, or full path to local file are supported. For URL of online file, only the https protocol is supported.<br><br> <br><br>Recommended sample rate for audio effect files: 8KHz, 16KHz, 22.05KHz, 44.1KHz, 48KHz.<br><br> <br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
|---|---|---|
|config |ByteRTCMediaPlayerConfig\* |See [ByteRTCMediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

### start

```objectivec
- (int)start;
```

Start playing the audio. Call this API when you call [open:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-open-config) and set `AutoPlay=False`.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* For audio file in PCM format, see [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-openwithcustomsource-config). `openWithCustomSource` and this API are mutually exclusive.

* After calling this API, call [stop](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-stop) to stop playing the audio file.

### openWithCustomSource:config:

```objectivec
- (int)openWithCustomSource:(ByteRTCMediaPlayerCustomSource*_Nullable)source config:(ByteRTCMediaPlayerConfig*_Nullable)config;
```

Enable audio mixing with audio raw data.

To open the audio file, see [open:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-open-config). `open` and this API are mutually exclusive.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|source |ByteRTCMediaPlayerCustomSource\* |See [ByteRTCMediaPlayerCustomSource](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaPlayerCustomSource). |
|config |ByteRTCMediaPlayerConfig\* |See [ByteRTCMediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling this API, you must call [pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalaudioframe) to push audio data and start the audio mixing.

* To stop the raw data audio mixing, call [stop](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-stop).

### stop

```objectivec
- (int)stop;
```

After calling [open:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-open-config), [start](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-start), or [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-openwithcustomsource-config) to start audio mixing, call this method to stop audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

### pause

```objectivec
- (int)pause;
```

After calling [open:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-open-config), or [start](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-start) to start audio mixing, call this API to pause audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling this API to pause audio mixing, call [resume](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-resume) to resume audio mixing.

* The API is valid for audio files, not PCM data.

### resume

```objectivec
- (int)resume;
```

After calling [pause](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

The API is valid for audio files, not PCM data.

### setVolume:type:

```objectivec
- (int)setVolume:(int)volume type:(ByteRTCAudioMixingType)type;
```

Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |
|type |ByteRTCAudioMixingType |See [ByteRTCAudioMixingType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioMixingType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Call this API only when audio is mixing.

### getVolume:

```objectivec
- (int)getVolume:(ByteRTCAudioMixingType)type;
```

Gets the current volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCAudioMixingType |See [ByteRTCAudioMixingType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioMixingType). |

**Return Value**

* \>0: Success, the current volume.

* < 0: Failed.

**Notes**

Call this API only when audio is mixing, including media file mixing and PCM mixing.

### getTotalDuration

```objectivec
- (int)getTotalDuration;
```

Gets the duration of the media file.

**Return Value**

* \>0: Success, the duration of the media file in milliseconds.

* < 0: Failed.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files, not PCM data.

### getPlaybackDuration

```objectivec
- (int)getPlaybackDuration;
```

Gets the actual playback duration of the mixed media file, in milliseconds.

**Return Value**

* \>0: Success, the actual playback time.

* < 0: Failed.

**Notes**

* The actual playback time refers to the playback time of the song without being affected by stop, jump, double speed, and freeze. For example, if the song stops playing for 30 seconds at 1:30 or skips to 2:00, and then continues to play normally for 2 minutes, the actual playing time is 3 minutes and 30 seconds.

* Call this API only when audio is mixing and the interval set by [setProgressInterval:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-setprogressinterval) is above `0`.

* The API is valid for audio files, not PCM data.

### getPosition

```objectivec
- (int)getPosition;
```

Gets the playback progress of the media file.

**Return Value**

* \>0: Success, the playback progress of media file in ms.

* < 0: Failed.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files, not PCM data.

### getState

```objectivec
- (ByteRTCPlayerState)getState;
```

Get the state of the media player.

**Return Value**

The current state of the media player. See [ByteRTCPlayerState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPlayerState).

**Notes**

You can call this method after creating a `ByteRTCMediaPlayer` instance.

### setAudioPitch:

```objectivec
- (int)setAudioPitch:(int)pitch;
```

Set the pitch of the local audio file mixing. Usually used in karaoke scenes.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pitch |int |The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* Support audio file only and not PCM data.

### setPosition:

```objectivec
- (int)setPosition:(int)position;
```

Sets the starting playback position of the media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|position |int |The starting position of the media file in milliseconds.<br><br> <br><br>You can get the total duration of the media file through [getTotalDuration](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-gettotalduration). The value of position should be less than the total duration of the media file. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* The API is valid for audio files, not PCM data.

* When playing online files, calling this API may cause playback delay.

### setAudioDualMonoMode:

```objectivec
- (int)setAudioDualMonoMode:(ByteRTCAudioMixingDualMonoMode)mode;
```

Sets the channel mode of the mixing of the media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCAudioMixingDualMonoMode |The mode of channel. The default channel mode is the same as the source file. See [ByteRTCAudioMixingDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioMixingDualMonoMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* Audio file is supported, but not PCM data.

### getAudioTrackCount

```objectivec
- (int)getAudioTrackCount;
```

Gets the track count of the current media file.

**Return Value**

* \>= 0：Success. Return the track count of the current media file.

* < 0：Failed.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

### selectAudioTrack:

```objectivec
- (int)selectAudioTrack:(int)index;
```

Specifies the playback track of the current media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|index |int |The specified playback audio track, starting from 0, and the range is `[0, getAudioTrackCount()-1]`. The value must be less than the return value of [getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-getaudiotrackcount). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

### setPlaybackSpeed:

```objectivec
- (int)setPlaybackSpeed:(int)speed;
```

Set the playback speed of the audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|speed |int |The ratio of the actual playback speed than that of the original speed of the audio file in %. The range is `[50,200]`. The default value is 100. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files and not PCM data.

### setProgressInterval:

```objectivec
- (int)setProgressInterval:(int64_t)interval;
```

Set the interval of the periodic callback [onMediaPlayerPlayingProgress:progress:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCMediaPlayerEventHandler-onmediaplayerplayingprogress-progress) during audio mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|interval |int64_t |interval in ms.<br><br><br> <br><br>* interval \> 0: The callback is enabled. The actual interval is a multiple of 10. If the input value is not divisible by 10, it will be automatically rounded up. For example, if the input is `52`, the actual interval will be 60 milliseconds.<br><br>* interval <= 0: The callback is disabled. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

### setLoudness:

```objectivec
- (int)setLoudness:(float)loudness;
```

To call [enableVocalInstrumentBalance:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|loudness |float |Original loudness in lufs. The range is `[-70.0, 0.0]`.<br><br> <br><br>When the value is less than \-70.0lufs, it will be adjusted to \-70.0lufs by default, and if it is more than 0.0lufs, the loudness will not be equalized. The default value is 1.0lufs, which means no processing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files and PCM data.

### registerAudioFrameObserver:

```objectivec
- (int)registerAudioFrameObserver:(_Nullable id<ByteRTCMediaPlayerAudioFrameObserver>)observer;
```

Register an observer to receive related callbacks when the local media file is mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |id<ByteRTCMediaPlayerAudioFrameObserver\> |See [ByteRTCMediaPlayerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCMediaPlayerAudioFrameObserver). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

The API is valid for audio files, not PCM data.

### pushExternalAudioFrame:

```objectivec
- (int)pushExternalAudioFrame:(ByteRTCAudioFrame*_Nullable)audioFrame;
```

Push PCM audio frame data for mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame).<br><br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity should be `audioFrame.samples × audioFrame.channel × 2`.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |

**Return Value**

* 0: Success.

* < 0: Failed.

**Notes**

* Before calling this method, the raw audio data mixing must be enabled through [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-openwithcustomsource-config).

* Suggestions: Before pushing data for the first time, please cache a certain amount of data (like 200 ms) on the application side, and then push it at once. Schedule subsequent push operation every 10 ms with audio data of 10 ms.

* To pause the playback, just pause the push.

### setEventHandler:

```objectivec
- (int)setEventHandler:(_Nullable id<ByteRTCMediaPlayerEventHandler>)handler;
```

Set the event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |id<ByteRTCMediaPlayerEventHandler\> |See [ByteRTCMediaPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCMediaPlayerEventHandler). |

**Return Value**

* 0: Success.

* < 0: Failed.

# ByteRTCAudioEffectPlayer

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioEffectPlayer :NSObject
```

> Available since 3.53

Audio effect player

Notes:

```Plain Text
 - Call [setEventHandler:](#ByteRTCAudioEffectPlayer-seteventhandler) to set the callback handler to receive related callbacks.
 - When using `ByteRTCAudioEffectPlayer`, you must call [setActive:withOptions:error:](https://developer.apple.com/documentation/avfaudio/avaudiosession/1616627-setactive?language=objc) to activate the app's audio session. You can deactivate the audio session after quitting audio mixing scenario.
```

## Member Functions

|Return |Name |
|---|---|
|int |[start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) |
|int |[stop:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-stop) |
|int |[stopAll](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-stopall) |
|int |[preload:filePath:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-preload-filepath) |
|int |[unload:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-unload) |
|int |[unloadAll](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-unloadall) |
|int |[pause:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-pause) |
|int |[pauseAll](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-pauseall) |
|int |[resume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-resume) |
|int |[resumeAll](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-resumeall) |
|int |[setPosition:position:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-setposition-position) |
|int |[getPosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-getposition) |
|int |[setVolume:volume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-setvolume-volume) |
|int |[setVolumeAll:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-setvolumeall) |
|int |[getVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-getvolume) |
|int |[getDuration:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-getduration) |
|int |[setEventHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-seteventhandler) |

## Instructions

### start:filePath:config:

```objectivec
-(int)start:(int)effectId filePath:(NSString* _Nullable)filePath config:(ByteRTCAudioEffectPlayerConfig* _Nullable)config;
```

Starts to play the audio effect file.

This API can be called multiple times with different IDs and file paths for multiple effects at the same time.

**Input Parameters**

|Audio effect file paths.<br><br> <br><br>URL of online file, URI of local file, or full path to local file are supported. For URL of online file, only the https protocol is supported.<br><br> <br><br>Recommended sample rate for audio effect files: 8KHz, 16KHz, 22.05KHz, 44.1KHz, 48KHz.<br><br> <br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
|---|---|---|
|config |ByteRTCAudioEffectPlayerConfig\* |See [ByteRTCAudioEffectPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioEffectPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* If the file has been loaded into memory via [preload:filePath:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-preload-filepath), make sure that the ID here is the same as the ID set by `preload`.

* After starting to play an audio effect file, you can call the [stop:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-stop) API to stop playing the audio effect file.

### stop:

```objectivec
-(int)stop:(int)effectId;
```

Stops the playback of audio effect files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling the [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) API to start playing the audio effect file, you can call this API to stop playing the audio effect file.

* After calling this API to stop playing an audio effect file, the audio effect file will be unloaded automatically.

### stopAll

```objectivec
-(int)stopAll;
```

Stops playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) to start playing audio effect files, you can call this API to stop playing all audio effect files.

* After calling this API to stop playing all audio effect files, the audio effect files will be unloaded automatically.

### preload:filePath:

```objectivec
-(int)preload:(int)effectId filePath:(NSString* _Nullable)filePath;
```

Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID. Used for identifying the audio effect. Please ensure that the audio effect ID is unique.<br><br> <br><br>If this API is called repeatedly with the same ID, the later one will overwrite the previous one.<br><br> <br><br>If you call [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) first and then call this API with the same ID, the SDK will stop the previous effect and then load the next one, and you will receive [onAudioEffectPlayerStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged-state-error).<br><br> <br><br>After calling this API to preload A.mp3, if you need to call [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) to play B.mp3 with the same ID, please call [unload:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-unload) to unload A.mp3 first, otherwise SDK will report an error AUDIO_MIXING_ERROR_LOAD_CONFLICT. |
|filePath |NSString\* |The filepath of effect file. URI or absolute path of a local file.<br><br> <br><br>The length of the pre\-loaded file must not exceed 20s.<br><br> <br><br>Audio effect file formats supported are the same as [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* This API just preloads the specified audio effect file, and only calls the [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) API to start playing the specified audio effect file.

* The specified audio effect file preloaded by calling this API can be unloaded by [unload:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-unload).

### unload:

```objectivec
-(int)unload:(int)effectId;
```

Unloads the specified audio effect file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

After calling this method, regarding the current mixing state, if [setEventHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-seteventhandler) is set, you will receive the `onAudioEffectPlayerStateChanged` callback.

### unloadAll

```objectivec
-(int)unloadAll;
```

Unloads all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

After calling this method, regarding the current mixing state, if [setEventHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-seteventhandler) is set, you will receive the `onAudioEffectPlayerStateChanged` callback.

### pause:

```objectivec
-(int)pause:(int)effectId;
```

Pauses the playback of audio effect files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) to start playing the audio effect file, you can pause the audio effect file by calling this API.

* After calling this API to pause the audio effect file, you can call the [resume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-resume) API to resume playback.

### pauseAll

```objectivec
-(int)pauseAll;
```

Pauses the Playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling the [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config) API to start playing audio effect files, you can pause playing all audio effect files by calling this API.

* After calling this API to pause the playback of all audio effect files, you can call the [resumeAll](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-resumeall) API to resume all playback.

### resume:

```objectivec
-(int)resume:(int)effectId;
```

Resumes the playback of audio effect files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

After calling the [pause:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-pause) API to pause the audio effect file, you can resume playback by calling this API.

### resumeAll

```objectivec
-(int)resumeAll;
```

Resumes the playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

After calling the [pauseAll](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-pauseall) API to pause all the audio effect files being played, you can resume playback by calling this API.

### setPosition:position:

```objectivec
-(int)setPosition:(int)effectId position:(int)position;
```

Sets the start position of the audio effect file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |
|position |int |The starting playback position of the audio effect file in milliseconds.<br><br> <br><br>You can get the total duration of the audio effect file by calling [getDuration:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-getduration), the value of position should be less than the total duration of the audio effect file. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config).

### getPosition:

```objectivec
-(int)getPosition:(int)effectId;
```

Gets the current position of audio effect file playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* \>0: Success, the current progress of audio effect file playback in milliseconds.

* < 0: Failure.

**Notes**

* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config).

### setVolume:volume:

```objectivec
-(int)setVolume:(int)effectId volume:(int)volume;
```

Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Call this API after [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config).

### setVolumeAll:

```objectivec
-(int)setVolumeAll:(int)volume;
```

Sets the volume of all audio effects, including audio effect files and PCM effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

This API has a lower priority than [setVolume:volume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-setvolume-volume), i.e. the volume of the audio effect set by `setVolume` is not affected by this API.

### getVolume:

```objectivec
-(int)getVolume:(int)effectId;
```

Gets the current volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* \>0: Success, the current volume value.

* < 0: Failed.

**Notes**

Call this API after [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config).

### getDuration:

```objectivec
-(int)getDuration:(int)effectId;
```

Get the duration of the audio effect file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* \>0: Success, the duration of the audio effect file in milliseconds.

* < 0: failed.

**Notes**

Call this API after [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config).

### setEventHandler:

```objectivec
-(int)setEventHandler:(_Nullable id<ByteRTCAudioEffectPlayerEventHandler>)handler;
```

Set the event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |id<ByteRTCAudioEffectPlayerEventHandler\> |See [ByteRTCAudioEffectPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioEffectPlayerEventHandler). |

**Return Value**

* 0: Success.

* < 0: Failed.

# ByteRTCSpatialAudio

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCSpatialAudio : NSObject
```

Spatial audio instance

## Member Functions

|Return |Name |
|---|---|
|void |[enableSpatialAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-enablespatialaudio) |
|void |[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-disableremoteorientation) |
|int |[updateSelfPosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateselfposition) |
|int |[updateRemotePosition:positionInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateremoteposition-positioninfo) |
|int |[removeRemotePosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-removeremoteposition) |
|int |[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-removeallremoteposition) |

## Instructions

### enableSpatialAudio:

```objectivec
- (void)enableSpatialAudio:(BOOL)enable;
```

Enables/disables spatial audio function.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable spatial audio function:<br><br><br> <br><br>* YES: Enable<br><br>* NO: Disable(Default setting) |

**Notes**

You need to call [updateSelfPosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateselfposition) as well to really enjoy the spatial audio effect.

### disableRemoteOrientation

```objectivec
-(void)disableRemoteOrientation;
```

Turn off the effect of the orientation of the local user as the sound source.

After the effect is off, all the other users in the room listen to the local user as if the local user is right in front of each of them.

**Notes**

* After the orientation effect as the sound source is disabled, you cannot enable it during the lifetime of the `SpatialAudio` instance.

* Calling this API does not affect the orientation effect of the local user as a listener. See [updateSelfPosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateselfposition) and [updateRemotePosition:positionInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateremoteposition-positioninfo).

### updateSelfPosition:

```objectivec
-(int)updateSelfPosition:(ByteRTCPositionInfo* _Nonnull)positionInfo;
```

> Available since 3.52

Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|positionInfo |ByteRTCPositionInfo\* |Information on the local user's position. Refer to [ByteRTCPositionInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPositionInfo) for details. |

**Return Value**

* 0: Success.

* <0: Failure.

* \-2: Failure. The reason is that any two of the 3D coordinate vectors of your position are not perpendicular to each other.

**Notes**

* You need to call this API after joining the room.

* Before calling this API, you should call [enableSpatialAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-enablespatialaudio) first to enable the spatial audio function.

* The settings made locally will not influence other users' spatial audio experience.

### updateRemotePosition:positionInfo:

```objectivec
-(int)updateRemotePosition:(NSString* _Nonnull)uid
                         positionInfo:(ByteRTCPositionInfo* _Nonnull)positionInfo;
```

> Available since 3.52

Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |NSString\* |User ID |
|positionInfo |ByteRTCPositionInfo\* |Information on the remote user's position. Refer to [ByteRTCPositionInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPositionInfo) for details. |

**Return Value**

* 0: Success.

* <0: Failure.

* \-2: Failure. The reason is that any two of the 3D coordinate vectors of the position of the remote user are not perpendicular to each other.

**Notes**

You must call this API after creating the room.

The settings made locally will not influence other users' spatial audio experience.

### removeRemotePosition:

```objectivec
-(int)removeRemotePosition:(NSString* _Nonnull)uid;
```

> Available since 3.52

Disables all spatial audio effects set by calling [updateRemotePosition:positionInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateremoteposition-positioninfo) for a certain remote user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |NSString\* |User ID of the remote user. |

**Return Value**

* 0: Success.

* <0: Failure.

### removeAllRemotePosition

```objectivec
-(int)removeAllRemotePosition;
```

> Available since 3.52

Disables all spatial audio effects set by calling [updateRemotePosition:positionInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio-updateremoteposition-positioninfo) for all remote users.

**Return Value**

* 0: Success.

* <0: Failure.

# ByteRTCRTSRoom

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRTSRoom : NSObject
```

RTS Room

## Member Property

|Type |Name |
|---|---|
|id<ByteRTCRTSRoomDelegate\> |[delegateRts](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-delegaterts) |

## Member Functions

|Return |Name |
|---|---|
|void |[destroy](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-destroy) |
|int |[setRTCRoomDelegateRts:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-setrtcroomdelegaterts) |
|int |[leaveRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-leaveroom) |
|int64_t |[sendRoomMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-sendroommessage) |
|int64_t |[sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-sendroombinarymessage) |
|int |[updateToken:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-updatetoken) |
|int64_t |[sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-sendusermessage-message-config) |
|int64_t |[sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-senduserbinarymessage-message-config) |
|int |[joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) |

## Instructions

### delegateRts

```objectivec
@property(nonatomic, weak) id<ByteRTCRTSRoomDelegate> _Nullable delegateRts;
```

## Instructions

### destroy

```objectivec
- (void)destroy;
```

Leaves and destroys the RTS room instance created by calling [createRTSRoom:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertsroom).

### setRTCRoomDelegateRts:

```objectivec
- (int)setRTCRoomDelegateRts:(id<ByteRTCRTSRoomDelegate> _Nullable)roomDelegate;
```

By setting [ByteRTCRTSRoomDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate), you can get informed of events related to this `ByteRTCRTSRoom` object.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomDelegate |id<ByteRTCRTSRoomDelegate\> |Refer to [ByteRTCRTSRoomDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### leaveRoom

```objectivec
- (int)leaveRoom;
```

Leave RTC room.

The user calls this method to leave the room, ending real\-time message communication and releasing all communication\-related resources.

**Return Value**

* 0: Success

* < 0: Failure

**Notes**

* When a visible user leaves the room, others in the room will receive [rtsRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onuserleave-reason).

* This method is an asynchronous operation, and the call returns without actually exiting the room. After you actually exit the room, you will receive a callback notification from [rtsRoom:OnLeaveRoom:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onleaveroom) locally.

* If the engine is destroyed immediately after this method is called, the SDK will not be able to trigger the [rtsRoom:OnLeaveRoom:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onleaveroom) callback.

### sendRoomMessage:

```objectivec
- (int64_t)sendRoomMessage:(NSString* _Nonnull)message;
```

Send text messages to all other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |NSString\* |The content of the text message sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending an in\-room text message, you must call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) to join the room.

* After calling this function, you will receive an [rtsRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroommessagesendresult-error) callback to notify the sender of the success or failure of the message;

* If the text message is sent successfully, all remote users in the room will receive [rtsRoom:onRoomMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-message) callback.

### sendRoomBinaryMessage:

```objectivec
- (int64_t)sendRoomBinaryMessage:(NSData*  _Nonnull)message;
```

Sends binary messages to all other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |NSData\* |The binary broadcast message sent by the user. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before broadcasting binary messages in the room, you must call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) to join the room.

* After calling this function, you will receive an [rtsRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroommessagesendresult-error) callback to notify the sender of the success or failure of the message;

* If the binary message is successfully sent, all users in the room will receive [rtsRoom:onRoomBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-message) callback.

### updateToken:

```objectivec
- (int)updateToken:(NSString*_Nullable)token;
```

Update Token.

You must call this API to update token to ensure the RTC call continues when you receive [onTokenWillExpire:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-onpublishprivilegetokenwillexpire), or [onSubscribePrivilegeTokenWillExpire:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-onsubscribeprivilegetokenwillexpire).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |NSString\* |Valid token.<br><br> <br><br>If the Token is invalid, you will receive [rtsRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo) with the error code of `-1010`. |

**Return Value**

* 0: Success

* !0: Failure

**Notes**

* In versions before 3.50, the publish and subscribe privileges contained in the Token are reserved parameters with no actual control permissions. In version 3.50 and later, the publish/subscribe privileges will be effective for whitelisted users. Please contact the technical support team to include you in the whitelist if you need this function.

* Do not call both [updateToken:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-updatetoken) and [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) to update the Token. If you fail to join the room or have been removed from the room due to an expired or invalid Token, call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) with a valid token to rejoin the room.

### sendUserMessage:message:config:

```objectivec
- (int64_t)sendUserMessage:(NSString*_Nonnull)userId message:(NSString*_Nonnull)message config:(ByteRTCMessageConfig)config;
```

Sends a text message (P2P) to the specified user in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|userId |NSString\* |ID of the user receiving the message |
|message |NSString\* |Message content. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |
|config |ByteRTCMessageConfig |Reliability of the message. |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending an in\-room text message, you must call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) to join the room.

* After calling this API, you will receive an [rtsRoom:onUserMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onusermessagesendresult-error) callback to notify the sender of the success or failure of the message.

* If the text message is sent successfully, the user specified by uid will receive an [rtsRoom:onUserMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onusermessagereceived-message) callback.

### sendUserBinaryMessage:message:config:

```objectivec
- (int64_t)sendUserBinaryMessage:(NSString* _Nonnull)uid message:(NSData* _Nonnull)message config:(ByteRTCMessageConfig)config;
```

Sends a binary message (P2P) to the specified user in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |NSString\* |Message Receiving user's ID |
|message |NSData\* |Binary message content sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |
|config |ByteRTCMessageConfig |See [ByteRTCMessageConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMessageConfig). |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending the in\-room binary message, you must call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) to join the room.

* After calling this function, you will receive an [rtsRoom:onUserMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onusermessagesendresult-error) callback to notify the sender of the success or failure of the message;

* If the binary message is sent successfully, the user specified by uid will receive [rtsRoom:onUserBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-message) callback.

### joinRTSRoom:userInfo:

```objectivec
- (int)joinRTSRoom:(NSString*_Nullable)token userInfo:(ByteRTCUserInfo*_Nonnull)userInfo;
```

Joins an RTS room.

After creating a room by calling [createRTSRoom:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertsroom), call this API to join the room and make audio & video calls with other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |NSString\* |Dynamic key for authentication and verification of users entering the room.<br><br> <br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br> <br><br>Apps with different AppIDs are not interoperable.<br><br> <br><br>Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause joining the room to fail. |
|userInfo |ByteRTCUserInfo\* |User information. See [ByteRTCUserInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserInfo). |

**Return Value**

Method call result.

* 0: Success.

   * Local users receive notifications of the room state via [rtsRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo).

* \-1: Invalid parameter

* \-2: Already in the room. After the API call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-leaveroom) is not called successfully, this return value will be triggered when the room entry API is called again, regardless of whether the filled room ID and user ID are duplicated.

   The reason for the failure will be communicated via the [rtsRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo) callback.

**Notes**

* In the same room with the same AppID, the user ID of each user must be unique. If two users have the same user ID, the user who joined the room later will kick the user who joined the room first out of the room, and the user who joined the room first will receive [rtsRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo) callback notification, the error type is duplicate login ByteRTCErrorCodeDuplicateLogin.

* Local users will receive [rtsRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo) callback notification after calling this method to join the room successfully. If the local user is also a visible user, the remote user will receive an [rtsRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onuserjoined) callback notification when joining the room.

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this time [rtcEngine:onConnectionStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After successful reconnection, you will receive a callback notification from [rtsRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onuserjoined) locally.

# ByteRTCEngine

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCEngine : NSObject
```

## Member Property

|Type |Name |
|---|---|
|id<ByteRTCEngineDelegate\> |[delegate](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-delegate) |

## Static Functions

|Return |Name |
|---|---|
|ByteRTCEngine |[createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcengine-delegate) |
|void |[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-destroyrtcengine) |
|NSString\* |[getSDKVersion](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getsdkversion) |
|int |[setLogConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlogconfig) |

## Member Functions

|Return |Name |
|---|---|
|int |[setAudioSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudiosourcetype) |
|int |[setAudioRenderType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudiorendertype) |
|int |[startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture) |
|int |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopaudiocapture) |
|int |[setAudioScenario:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudioscenario) |
|int |[setAudioProfile:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudioprofile) |
|int |[setAnsMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setansmode) |
|int |[setVoiceChangerType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvoicechangertype) |
|int |[setVoiceReverbType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvoicereverbtype) |
|int |[setLocalVoiceEqualization:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvoiceequalization) |
|int |[setLocalVoiceReverbParam:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvoicereverbparam) |
|int |[enableLocalVoiceReverb:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enablelocalvoicereverb) |
|int |[muteAudioCapture:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-muteaudiocapture) |
|int |[muteScreenAudioCapture:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-mutescreenaudiocapture) |
|int |[setCaptureVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcapturevolume) |
|int |[setScreenCaptureVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setscreencapturevolume) |
|int |[setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setplaybackvolume) |
|int |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableaudiopropertiesreport) |
|int |[setRemoteAudioPlaybackVolume:volume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremoteaudioplaybackvolume-volume) |
|int |[setEarMonitorMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setearmonitormode) |
|int |[setEarMonitorMode:filter:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setearmonitormode-filter) |
|int |[setEarMonitorVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setearmonitorvolume) |
|int |[setBluetoothMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setbluetoothmode) |
|int |[setLocalVoicePitch:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvoicepitch) |
|int |[enableVocalInstrumentBalance:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enablevocalinstrumentbalance) |
|int |[enablePlaybackDucking:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableplaybackducking) |
|int |[setLocalVideoSink:withLocalRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvideosink-withlocalrenderconfig) |
|int |[setRemoteVideoSink:withSink:withRemoteRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremotevideosink-withsink-withremoterenderconfig) |
|int |[setVideoCaptureRotation:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideocapturerotation) |
|int |[setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideoencoderconfig) |
|int |[setLocalSimulcastMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalsimulcastmode) |
|int |[setLocalSimulcastMode:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalsimulcastmode-config) |
|int |[enableAlphaChannelVideoEncode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enablealphachannelvideoencode) |
|int |[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-disablealphachannelvideoencode) |
|int |[setVideoCaptureConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideocaptureconfig) |
|int |[setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvideocanvas) |
|int |[updateLocalVideoCanvas:withBackgroundColor:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updatelocalvideocanvas-withbackgroundcolor) |
|int |[setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremotevideocanvas-withcanvas) |
|int |[updateRemoteStreamVideoCanvas:withRemoteVideoRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updateremotestreamvideocanvas-withremotevideorenderconfig) |
|int |[startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) |
|int |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideocapture) |
|int |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvideomirrortype) |
|int |[setRemoteVideoMirrorType:withMirrorType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremotevideomirrortype-withmirrortype) |
|int |[setVideoRotationMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideorotationmode) |
|int |[setVideoOrientation:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideoorientation) |
|int |[switchCamera:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-switchcamera) |
|ByteRTCVideoEffect |[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getvideoeffectinterface) |
|int |[enableEffectBeauty:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableeffectbeauty) |
|int |[setBeautyIntensity:withIntensity:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setbeautyintensity-withintensity) |
|int |[setCameraZoomRatio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcamerazoomratio) |
|float |[getCameraZoomMaxRatio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getcamerazoommaxratio) |
|bool |[isCameraZoomSupported](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-iscamerazoomsupported) |
|bool |[isCameraTorchSupported](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-iscameratorchsupported) |
|int |[setCameraTorch:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcameratorch) |
|bool |[isCameraFocusPositionSupported](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-iscamerafocuspositionsupported) |
|int |[setCameraFocusPosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcamerafocusposition) |
|bool |[isCameraExposurePositionSupported](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-iscameraexposurepositionsupported) |
|int |[setCameraExposurePosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcameraexposureposition) |
|int |[setCameraExposureCompensation:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcameraexposurecompensation) |
|int |[enableCameraAutoExposureFaceMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enablecameraautoexposurefacemode) |
|int |[setCameraAdaptiveMinimumFrameRate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcameraadaptiveminimumframerate) |
|int |[sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe) |
|int |[sendLivePushSEIMessage:count:isKeyFrameOnly:allowOverwrite:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendlivepushseimessage-count-iskeyframeonly-allowoverwrite) |
|int |[setVideoDigitalZoomConfig:size:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomconfig-size) |
|int |[setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol) |
|int |[startVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideodigitalzoomcontrol) |
|int |[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideodigitalzoomcontrol) |
|int |[registerLocalVideoProcessor:withConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registerlocalvideoprocessor-withconfig) |
|int |[registerLocalEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registerlocalencodedvideoframeobserver) |
|int |[setAudioRoute:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudioroute) |
|ByteRTCAudioRoute |[getAudioRoute](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getaudioroute) |
|int |[enableExternalSoundCard:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableexternalsoundcard) |
|int |[setDefaultAudioRoute:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setdefaultaudioroute) |
|int |[startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startpushmixedstream-withpushtargetconfig-withmixedconfig) |
|int |[updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig) |
|int |[stopPushMixedStream:withPushTargetType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stoppushmixedstream-withpushtargettype) |
|int |[startPushSingleStream:singleStream:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startpushsinglestream-singlestream) |
|int |[stopPushSingleStream:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stoppushsinglestream) |
|ByteRTCWTNStream |[getWTNStream](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getwtnstream) |
|int |[pushExternalVideoFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalvideoframe) |
|int |[enableAudioFrameCallback:format:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableaudioframecallback-format) |
|int |[disableAudioFrameCallback:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-disableaudioframecallback) |
|int |[registerAudioFrameObserver:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registeraudioframeobserver) |
|int |[registerAudioProcessor:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registeraudioprocessor) |
|int |[enableAudioProcessor:audioFormat:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableaudioprocessor-audioformat) |
|int |[disableAudioProcessor:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-disableaudioprocessor) |
|int |[pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalaudioframe) |
|int |[pullExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pullexternalaudioframe) |
|int |[pushReferenceAudioPCMData:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushreferenceaudiopcmdata) |
|int |[setBusinessId:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setbusinessid) |
|int |[feedback:info:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-feedback-info) |
|void\* |[getNativeHandle](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getnativehandle) |
|int |[setPublishFallbackOption:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setpublishfallbackoption) |
|int |[setSubscribeFallbackOption:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setsubscribefallbackoption) |
|int |[setRemoteUserPriority:InRoomId:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremoteuserpriority-inroomid-uid) |
|int |[setEncryptInfo:key:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setencryptinfo-key) |
|int |[setCustomizeEncryptHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcustomizeencrypthandler) |
|ByteRTCRoom |[createRTCRoom:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcroom) |
|ByteRTCRTSRoom |[createRTSRoom:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertsroom) |
|int |[setExtensionConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setextensionconfig) |
|int |[setRuntimeParameters:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setruntimeparameters) |
|int |[startScreenCapture:bundleId:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startscreencapture-bundleid) |
|int |[updateScreenCapture:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updatescreencapture) |
|int |[stopScreenCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopscreencapture) |
|int |[sendScreenCaptureExtensionMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendscreencaptureextensionmessage) |
|int |[startFileRecording:type:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startfilerecording-type) |
|int |[stopFileRecording](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopfilerecording) |
|int |[startAudioRecording:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiorecording) |
|int |[stopAudioRecording](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopaudiorecording) |
|ByteRTCAudioEffectPlayer |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getaudioeffectplayer) |
|ByteRTCMediaPlayer |[getMediaPlayer:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getmediaplayer) |
|int |[login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) |
|int |[logout](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-logout) |
|int |[updateLoginToken:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updatelogintoken) |
|int |[setServerParams:url:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setserverparams-url) |
|int |[getPeerOnlineStatus:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getpeeronlinestatus) |
|NSInteger |[sendUserMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendusermessageoutsideroom-message-config) |
|NSInteger |[sendUserBinaryMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-senduserbinarymessageoutsideroom-message-config) |
|NSInteger |[sendServerMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendservermessage) |
|NSInteger |[sendServerBinaryMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendserverbinarymessage) |
|int |[startNetworkDetection:uplinkBandwidth:downlink:downlinkBandwidth:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startnetworkdetection-uplinkbandwidth-downlink-downlinkbandwidth) |
|int |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopnetworkdetection) |
|int |[setScreenAudioSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setscreenaudiosourcetype) |
|int |[pushScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushscreenaudioframe) |
|int |[setVideoSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideosourcetype) |
|int |[setExternalVideoEncoderEventHandler:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setexternalvideoencodereventhandler) |
|int |[pushExternalEncodedVideoFrame:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalencodedvideoframe-withencodedvideoframe) |
|int |[setVideoDecoderConfig:withVideoDecoderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodecoderconfig-withvideodecoderconfig) |
|int |[requestRemoteVideoKeyFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-requestremotevideokeyframe) |
|int |[registerRemoteEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registerremoteencodedvideoframeobserver) |
|int |[sendStreamSyncInfo:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendstreamsyncinfo-config) |
|int |[startEchoTest:playDelay:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startechotest-playdelay) |
|int |[stopEchoTest](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopechotest) |
|int |[setVideoWatermark:withRtcWatermarkConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideowatermark-withrtcwatermarkconfig) |
|int |[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-clearvideowatermark) |
|NSInteger |[takeLocalSnapshot:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-takelocalsnapshot) |
|NSInteger |[takeLocalSnapshotToFile:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-takelocalsnapshottofile) |
|NSInteger |[takeRemoteSnapshot:callback:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-takeremotesnapshot-callback) |
|NSInteger |[takeRemoteSnapshotToFile:filePath:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-takeremotesnapshottofile-filepath) |
|int |[startCloudProxy:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startcloudproxy) |
|int |[stopCloudProxy](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopcloudproxy) |
|int |[setDummyCaptureImagePath:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setdummycaptureimagepath) |
|ByteRTCNetworkTimeInfo |[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getnetworktimeinfo) |
|int |[startHardwareEchoDetection:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-starthardwareechodetection) |
|int |[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stophardwareechodetection) |
|int |[setCellularEnhancement:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcellularenhancement) |
|int |[setLocalProxy:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalproxy) |
|int |[deprecated] [setLocalVideoSink:withPixelFormat:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvideosink-withpixelformat) |
|int |[deprecated] [setRemoteVideoSink:withSink:withPixelFormat:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremotevideosink-withsink-withpixelformat) |
|int |[deprecated] [updateRemoteStreamVideoCanvas:withRenderMode:withBackgroundColor:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updateremotestreamvideocanvas-withrendermode-withbackgroundcolor) |

## Instructions

### delegate

```objectivec
@property (nonatomic, weak) id<ByteRTCEngineDelegate> _Nullable delegate;
```

## Instructions

### createRTCEngine:delegate:

```objectivec
+ (ByteRTCEngine* _Nullable) createRTCEngine:(ByteRTCEngineConfig* _Nonnull) config
                                      delegate:(id<ByteRTCEngineDelegate> _Nullable)delegate;
```

Creates an engine instance.

This is the very first API that you must call if you want to use all the RTC capabilities.

If there is no engine instance in current process, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |ByteRTCEngineConfig\* |[ByteRTCEngineConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEngineConfig) |
|delegate |id<ByteRTCEngineDelegate\> |Delegate sent from SDK to App. See [ByteRTCEngineDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate) |

**Return Value**

A [ByteRTCEngine](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine) instance

### destroyRTCEngine

```objectivec
+ (void)destroyRTCEngine NS_SWIFT_NAME(destroyRTCEngine());
```

Destroy the engine instance created by [createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcengine-delegate), and release all related resources.

**Notes**

* Call this API after all business scenarios related to the engine instance are destroyed.

* When the API is called, RTC SDK destroys all memory associated with the engine instance and stops any interaction with the media server.

* Calling this API will start the SDK exit logic. The engine thread is held until the exit logic is complete. The engine thread is retained until the exit logic is complete. Therefore, do not call this API directly in the callback thread, or it will cause a deadlock. This function takes a long time to execute, so it's not recommended to call this API in the main thread, or the main thread may be blocked.

* You can enable ARC for Objective\-C, to automatically trigger the destruction logic when the dealloc method is called.

### getSDKVersion

```objectivec
+ (NSString* _Nonnull)getSDKVersion;
```

Gets the current version number of the SDK.

**Return Value**

SDK The current version number.

### setLogConfig:

```objectivec
+ (int) setLogConfig:(ByteRTCLogConfig*_Nonnull) logConfig;
```

Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size, and the prefix of log file name.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|logConfig |ByteRTCLogConfig\* |Local log parameters. See [ByteRTCLogConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLogConfig). |

**Return Value**

* 0: Success.

* –1: Failure. This API must be called before creating engine.

* –2: Failure. Invalid parameters.

**Notes**

This API must be called before [createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcengine-delegate).

### setAudioSourceType:

```objectivec
- (int)setAudioSourceType:(ByteRTCAudioSourceType) type;
```

Switches the audio capture type.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCAudioSourceType |Audio input source type. See [ByteRTCAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioSourceType)<br><br> <br><br>Use internal audio capture by default. The audio capture type and the audio render type may be different from each other. |

**Return Value**

Method call result:

* =0: Success.

* <0: Failure.

**Notes**

* You can call this API before or after joining the room.

* If you call this API to switch from internal audio capture to custom capture, the internal audio capture is automatically disabled. You must call [pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalaudioframe) to push custom captured audio data to RTC SDK for transmission.

* If you call this API to switch from custom capture to internal capture, you must then call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture) to enable internal capture.

### setAudioRenderType:

```objectivec
- (int)setAudioRenderType:(ByteRTCAudioRenderType) type;
```

Switches the audio render type.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCAudioRenderType |Audio output source type. See [ByteRTCAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRenderType).<br><br> <br><br>Use internal audio render by default. The audio capture type and the audio render type may be different from each other. |

**Return Value**

Method call result:

* =0: Success.

* <0: Failure.

**Notes**

* You can call this API before or after joining the room.

* After calling this API to enable custom audio rendering, call [pullExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pullexternalaudioframe) for audio data.

### startAudioCapture

```objectivec
- (int)startAudioCapture;
```

Starts internal audio capturing. The default is off.

Internal capture refers to audio capture using the built\-in capture module of the SDK.

After calling this API is called, the local user will receive [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error).

If this API is called by a visible user, the other users in the room will receive [rtcEngine:onUserStartAudioCapture:info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onuserstartaudiocapture-info).

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Calling this API without obtaining permission to use the microphone of the current device will trigger [rtcEngine:onWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onwarning).

* Call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopaudiocapture) to stop the internal audio capture. Otherwise, the internal audio capture will sustain until you destroy the engine instance.

* To mute and unmute microphones, we recommend using [publishStreamAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamaudio), other than [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopaudiocapture) and this API. Because starting and stopping capture devices often need some time waiting for the response of the device, that may lead to a short silence during the communication.

* Once you create the engine instance, you can start internal audio capture regardless of the audio publishing state. The audio stream will start publishing only after the audio capture starts.

* To switch from custom to internal audio capture, stop publishing before disabling the custom audio capture module by calling [setAudioSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudiosourcetype) and then call this API to enable the internal audio capture.

### stopAudioCapture

```objectivec
- (int)stopAudioCapture;
```

Stops internal audio capturing. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error) after stopping audio capture by calling this API.

The remote clients in the room will be informed of the state change via [rtcEngine:onUserStopAudioCapture:info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onuserstopaudiocapture-info) after the visible client stops audio capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture) to enable the internal audio capture.

* Without calling this API the internal audio capture will sustain until you destroy the engine instance.

### setAudioScenario:

```objectivec
- (int)setAudioScenario:(ByteRTCAudioScenarioType)audioScenario;
```

> Available since 3.60.

Sets the audio scenarios.

After selecting the audio scenario, SDK will automatically switch to the proper volume modes (the call/media volume) according to the scenarios and the best audio configurations under such scenarios.

This API should not be used at the same time with the old one.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioScenario |ByteRTCAudioScenarioType |Audio scenarios. See [ByteRTCAudioScenarioType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioScenarioType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You can only use this API before joining the room.

* Call volume is more suitable for calls, meetings and other scenarios that demand information accuracy. Call volume will activate the system hardware signal processor, making the sound clearer. The volume cannot be reduced to 0.

* Media volume is more suitable for entertainment scenarios, which require musical expression. The volume can be reduced to 0.

### setAudioProfile:

```objectivec
- (int)setAudioProfile:(ByteRTCAudioProfileType)audioProfile;
```

Sets the sound quality. You should choose the appropriate sound quality according to the needs of the business scenario.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioProfile |ByteRTCAudioProfileType |Sound quality. See [ByteRTCAudioProfileType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioProfileType) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* This method can be called before and after entering the room;

* Support dynamic switching of sound quality during a call.

### setAnsMode:

```objectivec
- (int)setAnsMode:(ByteRTCAnsMode)ansMode;
```

> Available since 3.52

Set the Active Noise Cancellation(ANC) mode during audio and video communications.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|ansMode |ByteRTCAnsMode |ANC modes. See [ByteRTCAnsMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAnsMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You can call this API before or after entering a room. When you repeatedly call it, only the last call takes effect.

The AI noise cancellation can be enabled by calling this interface only in the following [ByteRTCRoomProfile](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRoomProfile) scenarios.

\- Game Voice: `ByteRTCRoomProfileGame`

\- High\-Quality Game: `ByteRTCRoomProfileGameHD`

\- Cloud Gaming: `ByteRTCRoomProfileCloudGame`

\- 1 vs 1 Audio and Video Call: `ByteRTCRoomProfileChat`

\- Multi\-End Synchronized Audio and Video Playback: `ByteRTCRoomProfileLwTogether`

\- Personal Device in Cloud Meeting: `ByteRTCRoomProfileMeeting`

\- Classroom Interaction: `ByteRTCRoomProfileClassroom`

\- Conference Room Terminals in Cloud Meetings: `ByteRTCRoomProfileMeetingRoom`

### setVoiceChangerType:

```objectivec
- (int)setVoiceChangerType:(ByteRTCVoiceChangerType)voiceChanger;
```

> Available since 3.32

Sets the type of voice change effect.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voiceChanger |ByteRTCVoiceChangerType |The sound change effect type. See [ByteRTCVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVoiceChangerType). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

* To use this feature, you need to integrate the SAMI dynamic library. See [Integrate Plugins on Demand](https://docs.byteplus.com/en/docs/12/1108726).

* You can call it before and after entering the room.

* Effective for both internal and external audio source.

* Only valid for mono\-channel audio.

* Mutually exclusive with [setVoiceReverbType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvoicereverbtype), and the effects set later will override the effects set first.

### setVoiceReverbType:

```objectivec
- (int)setVoiceReverbType:(ByteRTCVoiceReverbType)voiceReverb;
```

> Available since 3.32

Sets the reverb effect type

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voiceReverb |ByteRTCVoiceReverbType |Reverb effect type. See [ByteRTCVoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVoiceReverbType). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

* You can call it before and after entering the room.

* Effective for both internal and external audio source.

* Only valid for mono\-channel audio.

* Mutually exclusive with [setVoiceChangerType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvoicechangertype), and the effects set later will override the effects set first.

### setLocalVoiceEqualization:

```objectivec
-(int)setLocalVoiceEqualization:(ByteRTCVoiceEqualizationConfig* _Nonnull)config;
```

Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |ByteRTCVoiceEqualizationConfig\* |See [ByteRTCVoiceEqualizationConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVoiceEqualizationConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

According to the Nyquist acquisition rate, the audio acquisition rate must be greater than twice the set center frequency. Otherwise, the setting will not be effective.

### setLocalVoiceReverbParam:

```objectivec
-(int)setLocalVoiceReverbParam:(ByteRTCVoiceReverbConfig* _Nonnull)param;
```

Set the reverb effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|param |ByteRTCVoiceReverbConfig\* |See [ByteRTCVoiceReverbConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVoiceReverbConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Call [enableLocalVoiceReverb:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enablelocalvoicereverb) to enable the reverb effect.

### enableLocalVoiceReverb:

```objectivec
-(int)enableLocalVoiceReverb:(bool)enable;
```

Enable the reverb effect for the local captured voice.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable the reverb effect. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Call [setLocalVoiceReverbParam:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvoicereverbparam) to set the reverb effect.

### muteAudioCapture:

```objectivec
- (int)muteAudioCapture: (bool)mute;
```

> Available since 3.58.1

Set whether to mute the recording signal (without changing the local hardware).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool |Whether to mute audio capture.<br><br><br> <br><br>* True: Mute (disable microphone)<br><br>* False: (Default) Enable microphone |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Calling this API does not affect the status of SDK audio stream publishing.

* Adjusting the volume by calling [setCaptureVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture) to enable audio capture.

### muteScreenAudioCapture:

```objectivec
- (int)muteScreenAudioCapture: (bool)mute;
```

> Available since 3.60.

Mutes or unmutes the audio captured when screen sharing.

Calling this method will send muted data instead of the screen audio data, and it does not affect the local audio device capture status and the SDK audio stream publishing status.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool |Whether to mute the audio capture when screen sharing.<br><br><br> <br><br>* True: Mute the audio capture when screen sharing.<br><br>* False: (Default) Unmute the audio capture when screen sharing. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Adjusting the volume by calling [setCaptureVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture) to enable audio capture.

### setCaptureVolume:

```objectivec
- (int)setCaptureVolume: (int)volume;
```

Adjusts the audio capture volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio of capture volume to original volume. Ranging: [0,400]. Unit: %<br><br><br> <br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

Call this API to set the volume of the audio capture before or during the audio capture.

### setScreenCaptureVolume:

```objectivec
- (int)setScreenCaptureVolume:(int)volume;
```

Adjusts the volume of audio captured during screen sharing.

This method only changes the volume of audio data and does not affect the hardware volume of the local device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio(%) of capture volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure better call quality, we recommend setting the volume to [0, 100].<br><br><br> <br><br>* 0: Mute<br><br>* 100: Original volume<br><br>* 400: Four times the original volume with signal\-clipping protection |

**Return Value**

* 0: Success.

* <0: Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

You can call this method to set the capture volume before or after enabling screen audio capture. Unlike [setCaptureVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcapturevolume), this method only adjusts the audio capture volume during screen sharing.

### setPlaybackVolume:

```objectivec
- (int)setPlaybackVolume:(NSInteger)volume;
```

Adjusts the playback volume of the mixed remote audio. You can call this API before or during the playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |NSInteger |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted, if you use both this method and [setRemoteAudioPlaybackVolume:volume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremoteaudioplaybackvolume-volume)/[setRemoteRoomAudioPlaybackVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setremoteroomaudioplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

### enableAudioPropertiesReport:

```objectivec
- (int)enableAudioPropertiesReport:(ByteRTCAudioPropertiesConfig* _Nonnull)config;
```

Enables audio information prompts. After that, you will receive [rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onlocalaudiopropertiesreport), [rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onremoteaudiopropertiesreport-totalremotevolume), and [rtcEngine:onActiveSpeaker:uid:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onactivespeaker-uid).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |ByteRTCAudioPropertiesConfig\* |See [ByteRTCAudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioPropertiesConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### setRemoteAudioPlaybackVolume:volume:

```objectivec
- (int)setRemoteAudioPlaybackVolume:(NSString* _Nonnull)streamId volume:(int)volume;
```

Set the audio volume of playing the received remote stream. You must join the room before calling the API. The validity of the setting is not associated with the publishing status of the stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of stream. |
|volume |int |The ratio between the playing volume of the original volume. The range is `[0, 400]` with overflow protection. The unit is %.<br><br> <br><br>For better audio quality, you are recommended to set the value to `[0, 100]`. |

**Return Value**

result

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus).

**Notes**

Assume that a remote user A is always within the scope of the adjusted target users:

* When this API is used together with [setRemoteRoomAudioPlaybackVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setremoteroomaudioplaybackvolume), the volume of local listening user A is the volume set by the API called later;

* When this API is used together with the [setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setplaybackvolume), the volume of local listening user A will be the superposition of the two set volume effects.

* When you call this API to set the remote stream volume, if the remote user leaves the room, the setting will be invalid.

### setEarMonitorMode:

```objectivec
- (int)setEarMonitorMode:(ByteRTCEarMonitorMode)mode;
```

Enables/Disables in\-ear monitoring.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCEarMonitorMode |Whether or not in\-ear monitoring is enabled. See [ByteRTCEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEarMonitorMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* In\-ear monitoring is effective for audio captured by the RTC SDK.

* We recommend that you use wired earbuds/headphones for a low\-latency, high\-resolution audio experience.

* For iOS, you can only use SDK\-level in\-ear monitoring.

### setEarMonitorMode:filter:

```objectivec
- (int)setEarMonitorMode:(ByteRTCEarMonitorMode)mode filter:(int)filter;
```

> Available since 3.60.

Enables/disables in\-ear monitoring and controls whether to apply local audio processing to the in\-ear monitoring audio.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCEarMonitorMode |Whether to enable in\-ear monitoring. See [ByteRTCEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEarMonitorMode). Defaults to off. |
|filter |int |Whether to apply local audio processing to the in\-ear monitoring audio. See [ByteRTCEarMonitorAudioFilter](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEarMonitorAudioFilter). Defaults to no audio processing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* In\-ear monitoring is effective for audio captured by the RTC SDK.

* We recommend that you use wired earbuds/headphones for a low\-latency, high\-resolution audio experience.

* For iOS, you can only use SDK\-level in\-ear monitoring.

### setEarMonitorVolume:

```objectivec
- (int)setEarMonitorVolume:(NSInteger)volume;
```

Sets the in\-ear monitoring volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |NSInteger |The monitoring volume with the adjustment range between 0% and 100%. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Call [setEarMonitorMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setearmonitormode) before setting the volume.

### setBluetoothMode:

```objectivec
- (int)setBluetoothMode:(ByteRTCBluetoothMode) mode;
```

On iOS, you can change the Bluetooth profile when the media volume is set in all scenarios.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCBluetoothMode |The Bluetooth profiles. See [ByteRTCBluetoothMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCBluetoothMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

You will receive [rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicewarning-devicetype-devicewarning) in the following scenarios: 1) You cannot change the Bluetooth profile to HFP.;2) The media volume is not set in all scenarios. We suggest that you call [setAudioScenario:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudioscenario) to set the media volume scenario before calling this API.

### setLocalVoicePitch:

```objectivec
- (int)setLocalVoicePitch:(NSInteger)pitch;
```

Changes local voice to a different key, mostly used in Karaoke scenarios.

You can adjust the pitch of local voice such as ascending or descending with this method.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pitch |NSInteger |The value that is higher or lower than the original local voice within a range from \-12 to 12. The default value is 0, i.e. no adjustment is made.<br><br> <br><br>The difference in pitch between two adjacent values within the value range is a semitone, with positive values indicating an ascending tone and negative values indicating a descending tone, and the larger the absolute value set, the more the pitch is raised or lowered.<br><br> <br><br>Out of the value range, the setting fails and triggers [rtcEngine:onWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onwarning) callback, indicating `WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH` for invalid value setting with [ByteRTCWarningCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCWarningCode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### enableVocalInstrumentBalance:

```objectivec
- (int)enableVocalInstrumentBalance:(BOOL)enable;
```

Enables/disables the loudness equalization function.

If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness:loudness: and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable loudness equalization function:<br><br><br> <br><br>* true: Yes<br><br>* false: No |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

You must call this API before starting to play the audio file with [start:filePath:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer-start-filepath-config).

### enablePlaybackDucking:

```objectivec
- (int)enablePlaybackDucking:(BOOL)enable;
```

Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.

With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable playback ducking:<br><br><br> <br><br>* YES: Yes<br><br>* NO: No |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### setLocalVideoSink:withLocalRenderConfig:

```objectivec
- (int)setLocalVideoSink:(id<ByteRTCVideoSinkDelegate> _Nullable)videoSink
         withLocalRenderConfig:(ByteRTCLocalVideoSinkConfig*)config NS_SWIFT_NAME(setLocalVideoSink(withSink:withLocalRenderConfig:));
```

> Available since 3.57

Binds the local video stream with a custom renderer. You can set parameters to return video frame data at a specified location and format.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoSink |id<ByteRTCVideoSinkDelegate\> |The custom video renderer, see [ByteRTCVideoSinkDelegate](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkDelegate). |
|config |ByteRTCLocalVideoSinkConfig\* |Configuration for the local video frame callback, see [ByteRTCLocalVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalVideoSinkConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more error details.

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* The binding state will be reset when you leave the room.

* If you need to unbind the video stream from the custom render, set videoSink to `null`.

* Generally, after receiving the [rtcEngine:onFirstLocalVideoFrameCaptured:withFrameInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onfirstlocalvideoframecaptured-withframeinfo) callback notification that the first local video frame has been captured, call this method to bind a custom renderer to a video stream and join the room.

### setRemoteVideoSink:withSink:withRemoteRenderConfig:

```objectivec
- (int)setRemoteVideoSink:(NSString* _Nonnull)streamId
                 withSink:(id<ByteRTCVideoSinkDelegate> _Nullable)videoSink
          withRemoteRenderConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setRemoteVideoSink(_:withSink:withRemoteRenderConfig:));
```

> Available since 3.57

Binds the remote video stream to a custom renderer. You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|videoSink |id<ByteRTCVideoSinkDelegate\> |Custom video renderer. See [ByteRTCVideoSinkDelegate](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkDelegate). |
|config |ByteRTCRemoteVideoSinkConfig\* |remote video frame callback configuration, see [ByteRTCRemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoSinkConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more error details.

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* This method can be called both before and after entering the room. If you are unable to obtain remote stream information in advance, you can call this method after joining the room and receiving the remote stream information through the [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish) callback.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

### setVideoCaptureRotation:

```objectivec
- (int)setVideoCaptureRotation:(ByteRTCVideoRotation)rotation;
```

Set the rotation of the video images captured from the local device.

Call this API to rotate the videos when the camera is fixed upside down or tilted. For rotating videos on a phone, we recommend to use [setVideoRotationMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideorotationmode).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rotation |ByteRTCVideoRotation |It defaults to `ByteRTCVideoRotation0`, which means not to rotate. Refer to [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoRotation). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* For the videos captured by the internal module, the rotation will be combined with that set by calling [setVideoRotationMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideorotationmode).

* This API affects the external\-sourced videos. The final rotation would be the original rotation angles adding up with the rotation set by calling this API.

* The elements added during the video pre\-processing stage, such as video sticker and background applied using [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevirtualbackground-withsource) will also be rotated by this API.

* The rotation would be applied to both locally rendered videos and those sent out. However, if you need to rotate a video which is intended for pushing to CDN individually, use [setVideoOrientation:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideoorientation).

### setVideoEncoderConfig:

```objectivec
- (int)setVideoEncoderConfig:(ByteRTCVideoEncoderConfig* _Nullable) encoderConfig;
```

Sets the quality of the main video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|encoderConfig |ByteRTCVideoEncoderConfig\* |See [ByteRTCVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoEncoderConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Since V3.61, this method can only set a single profile for the video stream. If you intend to publish the stream in multiple qualities, use [setLocalSimulcastMode:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalsimulcastmode-config).

* Without calling this method, only one stream will be sent with a profile of 640px × 360px @15fps. The default encoding preference is frame rate\-first.

* This method applies to both the video stream from camera capture and screen sharing. When sharing screen on iOS, if you call this method to set the encoding parameters for the screen sharing stream, you must restart screen capture for the new settings to take effect.

### setLocalSimulcastMode:

```objectivec
- (int)setLocalSimulcastMode:(ByteRTCVideoSimulcastMode)mode ;
```

> Available since 3.60.

Enable the Simulcast feature.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCVideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [ByteRTCVideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSimulcastMode).<br><br>By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |

**Return Value**

* 0: Success.

* < 0 : Fail.

**Notes**

* Call this method before the user joins a room.

* The default specification of the video stream is 640px × 360px @15fps.

* If you intend to specify the lower\-quality streams, use (int)setVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) encoderConfig withParameters:(NSDictionary \* _Nullable) parameters.

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

### setLocalSimulcastMode:config:

```objectivec
- (int)setLocalSimulcastMode:(ByteRTCVideoSimulcastMode)mode config:(NSArray <ByteRTCVideoEncoderConfig*>* _Nullable)streamConfig;
```

> Available since 3.60.

Enable the Simulcast feature and configure the lower\-quality video streams settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCVideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [ByteRTCVideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSimulcastMode). By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |
|streamConfig |NSArray<ByteRTCVideoEncoderConfig\*\>\* |The specification of the lower quality stream. You can configure up to three low\-quality streams for a video source. See [ByteRTCVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoEncoderConfig). The resolution of the lower quality stream must be smaller than the standard stream set via [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideoencoderconfig). The specifications in the array must be arranged in ascending order based on resolution.<br><br>By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |

**Return Value**

* 0: Success.

* < 0 : Fail.

**Notes**

* The default specification of the video stream is 640px × 360px @15fps.

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

### enableAlphaChannelVideoEncode:

```objectivec
-(int)enableAlphaChannelVideoEncode:(ByteRTCAlphaLayout)alphaLayout;
```

> Available since 3.58

Enables the Alpha channel encoding feature for custom capture video frames.

Suitable for scenarios where the video subject needs to be separated from the background at the push\-streaming end, and the background can be custom rendered at the receive\-streaming end.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|alphaLayout |ByteRTCAlphaLayout |The arrangement position of the separated Alpha channel relative to the RGB channel information. Currently, only ByteRTCAlphaLayout.ByteRTCAlphaLayoutTop is supported, which is positioned above the RGB channel information. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* This API only applies to custom capture video frames that use ByteRTCVideoPixelFormat.ByteRTCVideoPixelFormatCVPixelBuffer.

* This API must be called before publishing the video stream.

* After enabling Alpha channel encoding with this API, you need to call [pushExternalVideoFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalvideoframe) to push custom captured video frames to the RTC SDK. If a video frame format that is not supported is pushed, the call to [pushExternalVideoFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushexternalvideoframe) will return the error code ByteRTCReturnStatus.ByteRTCReturnStatusParameterErr.

### disableAlphaChannelVideoEncode

```objectivec
-(int)disableAlphaChannelVideoEncode;
```

> Available since 3.58

Disables the Alpha channel encoding feature for custom captured video frames.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

This interface must be called after stopping publishing the video stream.

### setVideoCaptureConfig:

```objectivec
- (int)setVideoCaptureConfig:(ByteRTCVideoCaptureConfig* _Nullable)captureConfig;
```

Sets the video capture parameters for internal capture of the RTC SDK.

If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|captureConfig |ByteRTCVideoCaptureConfig\* |Video capture parameters. See: [ByteRTCVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoCaptureConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* This API can be called after the engine is created and takes effect immediately after being called. It is recommended to call this method before [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture).

* It is recommended that different Engines on the same device use the same video capture parameters.

* If you use the internal module to start video capture before calling this interface, the capture parameters default to Auto.

### setLocalVideoCanvas:

```objectivec
- (int)setLocalVideoCanvas:(ByteRTCVideoCanvas* _Nullable)canvas NS_SWIFT_NAME(setLocalVideoCanvas(withCanvas:));
```

Sets the view to be used for local video rendering and the rendering mode.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|canvas |ByteRTCVideoCanvas\* |View information and rendering mode. See [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoCanvas). |

**Return Value**

* 0: Success.

* \-2: Invalid parameter.

* \-12: This method is not available in the Audio SDK.

**Notes**

* You should bind your stream to a view before joining the room. This setting will remain in effect after you leave the room.

* If you need to unbind the local video stream from the current view, you can call this API and set the videoCanvas to `null`.

### updateLocalVideoCanvas:withBackgroundColor:

```objectivec
- (int)updateLocalVideoCanvas:(ByteRTCRenderMode)renderMode
          withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateLocalVideoCanvas(withBackgroundColor:));
```

Update the render mode and background color of local video rendering.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|renderMode |ByteRTCRenderMode |See [ByteRTCRenderMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRenderMode). |
|backgroundColor |NSUInteger |See [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoCanvas).backgroundColor. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Calling this API during local video rendering will be effective immediately.

### setRemoteVideoCanvas:withCanvas:

```objectivec
- (int)setRemoteVideoCanvas:(NSString* _Nonnull)streamId
                 withCanvas:(ByteRTCVideoCanvas* _Nullable)canvas NS_SWIFT_NAME(setRemoteVideoCanvas(_:withCanvas:));
```

Sets the view and rendering mode to use when rendering a video stream from a specified remote user uid.

If you need to unbind the video view, set canvas to empty.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|canvas |ByteRTCVideoCanvas\* |View information and rendering mode. See [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoCanvas). Starting from version 3.56, you can set the rotation angle of the remote video rendering using `renderRotation`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

When the local user leaves the room, the setting will be invalid. The remote user leaving the room does not affect the setting.

### updateRemoteStreamVideoCanvas:withRemoteVideoRenderConfig:

```objectivec
- (int)updateRemoteStreamVideoCanvas:(NSString* _Nonnull)streamId
         withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig* _Nonnull)remoteVideoRenderConfig
            NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRemoteVideoRenderConfig:));
```

> Available since 3.56

Modifies remote video frame rendering settings, including render mode, background color, and rotation angle, while using the internal rendering of the SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|remoteVideoRenderConfig |ByteRTCRemoteVideoRenderConfig\* |Video rendering settings. See [ByteRTCRemoteVideoRenderConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoRenderConfig). |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* After setting the rendering configuration for the remote video frame with [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremotevideocanvas-withcanvas), you can call this API to update settings including render mode, background color, and rotation angle.

* Calling this API during remote video rendering will be effective immediately.

### startVideoCapture

```objectivec
- (int)startVideoCapture NS_SWIFT_NAME(startVideoCapture());
```

Enables internal video capture immediately. The default setting is off.

Internal video capture refers to: capturing video using the built\-in module.

The local client will be informed via [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) after starting video capture by calling this API.

The remote clients in the room will be informed of the state change via [rtcEngine:onUserStartVideoCapture:info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onuserstartvideocapture-info) after the visible client starts video capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Call [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideocapture) to stop the internal video capture. Otherwise, the internal video capture will sustain until you destroy the engine instance.

* Once you create the engine instance, you can start internal video capture regardless of the video publishing state. The video stream will start publishing only after the video capture starts.

* To switch from custom to internal video capture, stop publishing before disabling the custom video capture module and then call this API to enable the internal video capture.

* Since the upgrade in v3.37.0, to start capture by calling this API, you need to request the capture permission in your App.

### stopVideoCapture

```objectivec
- (int)stopVideoCapture NS_SWIFT_NAME(stopVideoCapture());
```

Disables internal video capture immediately. The default is off.

Internal video capture refers to using the RTC SDK built\-in video capture module to capture.

The local client will be informed via [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) after stopping video capture by calling this API.

The remote clients in the room will be informed of the state change via [rtcEngine:onUserStopVideoCapture:info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onuserstopvideocapture-info) after the visible client stops video capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* A call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to enable the internal video capture.

* Without calling this API the internal video capture will sustain until you destroy the engine instance.

### setLocalVideoMirrorType:

```objectivec
- (int)setLocalVideoMirrorType:(ByteRTCMirrorType) mirrorType;
```

Sets the mirror mode for the captured video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mirrorType |ByteRTCMirrorType |Mirror type. See [ByteRTCMirrorType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMirrorType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Switching video streams does not affect the settings of the mirror type.

* This API is not applicable to screen\-sharing streams.

* When using an external renderer, you can set `mirrorType` to `0` and `3`, but you cannot set it to `1`.

* Before you call this API, the initial states of each video stream are as follows:

| |Front\-facing camera |Back\-facing camera |Custom capturing |Built\-in camera |
|---|---|---|---|---|
|Mobile device |The preview is mirrored. The published video stream is not mirrored. |The preview and the published video stream are not mirrored. |The preview and the published video stream are not mirrored. |/ |
|PC |/ |/ |The preview and the published video stream are not mirrored. |The preview is mirrored. The published video stream is not mirrored. |

  ### setRemoteVideoMirrorType:withMirrorType: ```objectivec \- (int)setRemoteVideoMirrorType:(NSString\* _Nonnull)streamId withMirrorType:(ByteRTCRemoteMirrorType)mirrorType; ``` \> Available since 3.57

When using internal rendering, enable mirroring for the remote stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|mirrorType |ByteRTCRemoteMirrorType |The mirror type for the remote stream, see [ByteRTCRemoteMirrorType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteMirrorType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### setVideoRotationMode:

```objectivec
- (int)setVideoRotationMode:(ByteRTCVideoRotationMode) rotationMode;
```

Sets the orientation of the video capture. By default, the App direction is used as the orientation reference.

During rendering, the receiving client rotates the video in the same way as the sending client does.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rotationMode |ByteRTCVideoRotationMode |Rotation reference can be the orientation of the App or gravity. Refer to [ByteRTCVideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoRotationMode) for details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The orientation setting is effective for internal video capture only. That is, the orientation setting is not effective to the custom video source or the screen\-sharing stream.

* If the video capture is on, the setting will be effective once you call this API. If the video capture is off, the setting will be effective on when capture starts.

### setVideoOrientation:

```objectivec
- (int)setVideoOrientation:(ByteRTCVideoOrientation) orientation;
```

Sets the orientation of the video frame before custom video processing and encoding. The default value is `Adaptive`.

You should set the orientation to `Portrait` when using video effects or custom processing.

You should set the orientation to `Portrait` or `Landscape` when pushing a single stream to the CDN.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|orientation |ByteRTCVideoOrientation |Orientation of the video frame. See [ByteRTCVideoOrientation](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoOrientation). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The orientation setting is only applicable to internal captured video sources. For custom captured video sources, setting the video frame orientation may result in errors, such as swapping width and height. Screen sources do not support video frame orientation setting.

* We recommend setting the orientation before joining room. The updates of encoding configurations and the orientation are asynchronous, therefore can cause a brief malfunction in preview if you change the orientation after joining room.

### switchCamera:

```objectivec
- (int)switchCamera:(ByteRTCCameraID) cameraId;
```

Switches to the front\-facing/back\-facing camera used in the internal video capture

The local client will be informed via [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) after calling this API.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|cameraId |ByteRTCCameraID |Camera type. Refer to [ByteRTCCameraID](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCCameraID) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Front\-facing camera is the default camera.

* If the internal video capturing is on, the switch is effective once you call this API. If the internal video capturing is off, the setting will be effective when capture starts.

### getVideoEffectInterface

```objectivec
- (ByteRTCVideoEffect* _Null_unspecified)getVideoEffectInterface NS_SWIFT_NAME(getVideoEffectInterface());
```

Gets video effect APIs.

**Return Value**

Video effect APIs. See [ByteRTCVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect).

### enableEffectBeauty:

```objectivec
- (int) enableEffectBeauty:(BOOL)enable;
```

Enables/Disables basic beauty effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable basic beauty effects.<br><br><br> <br><br>* YES: Enables basic beauty effects.<br><br>* NO: (Default) Disables basic beauty effects. |

**Return Value**

* 0: Success.

* –1001: This method is not available for your current RTC SDK.

* \-12: This method is not available in the Audio SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [Error Code Table](https://docs.byteplus.com/effects/docs/error-code-table).

**Notes**

* You cannot use the basic beauty effects and the advanced effect features at the same time. See [how to use advanced effect features](https://docs.byteplus.com/byteplus-rtc/docs/114717) for more information.

* You need to integrate Effect SDK before calling this API. Effect SDK v4.4.2+ is recommended.

* Call [setBeautyIntensity:withIntensity:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setbeautyintensity-withintensity) to set the beauty effect intensity. If you do not set the intensity before calling this API, the default intensity will be enabled. The default values for the intensity of each beauty mode are as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity.

* This API is not applicable to screen capturing.

### setBeautyIntensity:withIntensity:

```objectivec
- (int) setBeautyIntensity:(ByteRTCEffectBeautyMode) beautyMode
             withIntensity:(float)intensity;
```

Sets the beauty effect intensity.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|beautyMode |ByteRTCEffectBeautyMode |Basic beauty effect. See [ByteRTCEffectBeautyMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEffectBeautyMode). |
|intensity |float |Beauty effect intensity in the range of [0,1]. When you set it to 0, the beauty effect will be turned off.<br><br> <br><br>The default values for the intensity of each beauty mode are as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity. |

**Return Value**

* 0: Success.

* –2: `intensity` is out of range.

* –1001: This API is not available for your current RTC SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [Error Code Table](https://docs.byteplus.com/effects/docs/error-code-table).

**Notes**

* If you call this API before calling [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevideoeffect), the default settings of beauty effect intensity will adjust accordingly.

* If you destroy the engine, the beauty effect settings will be invalid.

### setCameraZoomRatio:

```objectivec
- (int) setCameraZoomRatio: (float) zoomRatio;
```

Sets the zoom magnification of the currently used camera (front/rear).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|zoomRatio |float |Camera zoom parameters. 1.0 means scaling to the original image, the maximum value that can be set is obtained through the [getCameraZoomMaxRatio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-getcamerazoommaxratio) method |

**Return Value**

* 0: Success.

* \-1: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* The camera zoom factor can only be set when [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) is called for video capture using the SDK internal capture module.

* The setting result fails after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideocapture) to turn off internal collection.

* Call [setVideoDigitalZoomConfig:size:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomconfig-size) to set digital zoom. Call [setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol) to perform digital zoom.

### getCameraZoomMaxRatio

```objectivec
- (float) getCameraZoomMaxRatio;
```

Gets the maximum zoom magnification of the currently used camera (front/rear).

**Return Value**

The maximum zoom parameters that can be set

### isCameraZoomSupported

```objectivec
- (bool) isCameraZoomSupported;
```

Detects whether the currently used camera supports zoom (digital/optical zoom).

**Return Value**

* true: supports scaling

* false: does not support scaling

### isCameraTorchSupported

```objectivec
- (bool) isCameraTorchSupported;
```

Detects whether the currently used camera supports flash.

**Return Value**

* true: support fill light

* false: not support fill light

### setCameraTorch:

```objectivec
- (int) setCameraTorch: (ByteRTCTorchState)torchState;
```

Turns on/off the flash of the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|torchState |ByteRTCTorchState |Fill light status. See [ByteRTCTorchState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCTorchState) |

**Return Value**

* 0: Success

* \-1: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

### isCameraFocusPositionSupported

```objectivec
- (bool)isCameraFocusPositionSupported;
```

Checks if manual focus is available for the currently used camera.

**Return Value**

* true: Available.

* false: Unavailable.

**Notes**

You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to start SDK internal video capturing before calling this API.

### setCameraFocusPosition:

```objectivec
- (int)setCameraFocusPosition:(CGPoint)position;
```

Sets the manual focus position for the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|position |CGPoint |The position of the focus point. Setting the upper\-left corner of the canvas as the origin, the `x` in `position` means the x\-coordinate of the focus point in the range of [0, 1], and the `y` in `position` means the y\-coordinate of the focus point in the range of [0, 1]. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to start SDK internal video capturing, and use SDK internal rendering before calling this API.

* When you set the focus point at the center of the canvas, the focus point setting will be canceled.

* The camera focus point setting will be invalid after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideocapture) to stop internal capturing.

### isCameraExposurePositionSupported

```objectivec
- (bool)isCameraExposurePositionSupported;
```

Checks if manual exposure setting is available for the currently used camera.

**Return Value**

* true: Available.

* false: Unavailable.

**Notes**

You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to start SDK internal video capturing before calling this API.

### setCameraExposurePosition:

```objectivec
- (int)setCameraExposurePosition:(CGPoint)position;
```

Sets the manual exposure position for the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|position |CGPoint |The position of the exposure point. Setting the upper\-left corner of the canvas as the origin, the `x` in `position` means the x\-coordinate of the exposure point in the range of [0, 1], and the `y` in `position` means the y\-coordinate of the exposure point in the range of [0, 1]. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to start SDK internal video capturing, and use SDK internal rendering before calling this API.

* When you set the exposure point at the center of the canvas, the exposure point setting will be canceled.

* The camera exposure point setting will be invalid after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideocapture) to stop internal capturing.

### setCameraExposureCompensation:

```objectivec
- (int)setCameraExposureCompensation:(float)val;
```

Sets the exposure compensation for the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|val |float |Exposure compensation in the range of [\-1, 1]. Default to 0, which means no exposure compensation. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to start SDK internal video capturing, and use SDK internal rendering before calling this API.

* The camera exposure compensation setting will be invalid after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideocapture) to stop internal capturing.

### enableCameraAutoExposureFaceMode:

```objectivec
- (int)enableCameraAutoExposureFaceMode:(bool)enable;
```

> Available since 353

Enable or disable face auto exposure mode during internal video capture. This mode fixes the problem that the face is too dark under strong backlight; but it will also cause the problem of too bright/too dark in the area outside the ROI region.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable the mode. True by default for iOS, False by default for Android. |

**Return Value**

* 0: Success.

* !0: Failure.

**Notes**

Calling this API takes effect immediately whether before or after internal video capturing.

### setCameraAdaptiveMinimumFrameRate:

```objectivec
- (int)setCameraAdaptiveMinimumFrameRate:(int)framerate;
```

> Available since 353

Set the minimum frame rate of the dynamic framerate mode during internal video capture.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|framerate |int |The minimum value in fps. The default value is 7.<br><br> <br><br>The maximum value of the dynamic framerate mode is set by calling [setVideoCaptureConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideocaptureconfig). When minimum value exceeds the maximum value, the frame rate is set to a fixed value as the maximum value; otherwise, dynamic framerate mode is enabled. |

**Return Value**

* 0: Success.

* !0: Failure.

**Notes**

* You must call this API before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to enable internal capture to make the setting valid.

* If the maximum frame rate changes due to performance degradation, static adaptation, etc., the set minimum frame rate value will be re\-compared with the new maximum value. Changes in comparison results may cause switch between fixed and dynamic frame rate modes.

* For Android, dynamic framerate mode is enabled.

* For iOS, dynamic framerate mode is disabled.

### sendSEIMessage:andRepeatCount:andCountPerFrame:

```objectivec
- (int)sendSEIMessage: (NSData* _Nonnull)message andRepeatCount:(int)repeatCount andCountPerFrame:(ByteRTCSEICountPerFrame) mode;
```

Sends SEI data.

In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |NSData\* |SEI data. No more than 4 KB SEI data per frame is recommended. |
|repeatCount |int |Number of times a message is sent repeatedly. The value range is [0, max{29, %{video frame rate}\-1}]. Recommended range: [2,4].<br><br> <br><br>After calling this API, the SEI data will be added to a consecutive `repeatCount+1` number of video frames starting from the current frame. |
|mode |ByteRTCSEICountPerFrame |SEI sending mode. See [ByteRTCSEICountPerFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSEICountPerFrame). |

**Return Value**

* \>= 0: The number of SEIs to be added to the video frame

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* We recommend the number of SEI messages per second should not exceed the current video frame rate. In a voice call, the blank\-frame rate is 15 fps.

* We recommend using the same sending mode from the start to the end of the program.

* In a voice call, this API can be called to send SEI data only in internal capture mode.

* In a video call, the custom captured video frame can also be used for sending SEI data if the original video frame contains no SEI data, otherwise calling this method will not take effect.

* Each video frame carries only the SEI data received within 2s before and after. In a voice call scenario, if no SEI data is sent within 1min after calling this API, SDK will automatically cancel publishing black frames.

* After the message is sent successfully, the remote user who subscribed your video stream will receive [rtcEngine:onSEIMessageReceived:info:andMessage:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onseimessagereceived-info-andmessage).

* When you switch from a voice call to a video call, SEI data will automatically start to be sent with normally captured video frames instead of black frames.

### sendLivePushSEIMessage:count:isKeyFrameOnly:allowOverwrite:

```objectivec
- (int)sendLivePushSEIMessage:(NSString*_Nonnull)jsonString
                        count:(NSInteger)count
               isKeyFrameOnly:(BOOL)isKeyFrameOnly
               allowOverwrite:(BOOL)allowOverwrite;
```

Sends SEI data in Key\-Value format through video frames.

Before calling this API, you must call [setLiveMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setlivemode) and set the room live mode to `ByteRTCRoomLiveModeSoloHost`.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|jsonString |NSString\* |JSON formatted key\-value pairs, for example, `{"key1":"value1","key2":"value2"}`:<br><br><br>* If a key has an empty value (e.g., `""` or `null`), that key will be deleted from the SEI dictionary.<br><br>* Total size of merged SEI data must not exceed 10 KB. |
|count |NSInteger |The number of times this SEI data is continuously sent.<br><br><br>* When `isKeyFrameOnly` is YES, it means sending with `count` keyframes (I\-frames);<br><br>* When `isKeyFrameOnly` is NO, it means sending with `count` video frames. |
|isKeyFrameOnly |BOOL |Whether to send SEI only with keyframes (I\-frames):<br><br><br>* YES: Send only with keyframes.<br><br>* NO: Send with all frames. |
|allowOverwrite |BOOL |whether subsequent requests are allowed to overwrite the value of this key:<br><br><br>* true: Subsequent requests can overwrite the key's value, and the `count` will also be updated to the new value;<br><br>* false: Subsequent requests will ignore any new value for this key and keep the original value. For an existing key, whether this write is allowed depends on the overwrite policy previously saved for that key. |

**Return Value**

* 0: Success.

* < 0: Failure.

* \-1: Video module not enabled.

* \-2: Parameter error (empty JSON or count <= 0).

* \-3: Invalid JSON format.

* \-4: Total SEI data size exceeds limit.

### setVideoDigitalZoomConfig:size:

```objectivec
- (int)setVideoDigitalZoomConfig:(ByteRTCZoomConfigType)type size:(float)size;
```

> Available since 3.51

Set the step size for each digital zooming control to the local videos.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCZoomConfigType |Required. Identifying which type the `size` is referring to. Refer to [ByteRTCZoomConfigType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCZoomConfigType). |
|size |float |Required. Reserved to three decimal places. It defaults to `0`.<br><br> <br><br>The meaning and range vary from different `type`s. If the scale or moving distance exceeds the range, the limit is taken as the result.<br><br><br> <br><br>* `ByteRTCZoomConfigTypeFocusOffset`: Increment or decrease to the scaling factor. Range: [0, 7]. For example, when it is set to 0.5 and [setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol) is called to zoom in, the scale will increase `0.5`. The scale ranges [1，8] and defaults to `1`, which means an original size.<br><br>* `ByteRTCZoomConfigTypeMoveOffset`：Ratio of the distance to the border of video images. It ranges [0, 0.5] and defaults to `0`, which means no offset. When you call [setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol) and choose `CAMERA_MOVE_LEFT`, the moving distance is size x original width. While for the `CAMERA_MOVE_UP`, the moving distance is size x original height. Suppose that a video spans 1080 px and the `size` is set to `0.5` so that the distance would be 0.5 x 1080 px = 540 px. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Only one size can be set for a single call. You must call this API to pass values respectively if you intend to set multiple `size`s.

* As the default `size` is `0`, you must call this API before performing any digital zoom control by calling [setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol) or [startVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideodigitalzoomcontrol).

### setVideoDigitalZoomControl:

```objectivec
- (int)setVideoDigitalZoomControl:(ByteRTCZoomDirectionType) direction;
```

Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|direction |ByteRTCZoomDirectionType |Action of the digital zoom control. Refer to [ByteRTCZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCZoomDirectionType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* As the default offset is `0`, you must call [setVideoDigitalZoomConfig:size:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomconfig-size) before this API.

* You can only move video images after they are magnified via this API or [startVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideodigitalzoomcontrol).

* When you request an out\-of\-range scale or movement, SDK will execute it with the limits. For example, when the image has been moved to the border, the image cannot be zoomed out, or has been magnified to 8x.

* Call [startVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideodigitalzoomcontrol) to have a continuous and repeatedly digital zoom control.

* Mobile devices can control the optical zoom of the camera, see `setCameraZoomRatio:`.

### startVideoDigitalZoomControl:

```objectivec
- (int)startVideoDigitalZoomControl:(ByteRTCZoomDirectionType)direction;
```

> Available since 3.51

Continuous and repeated digital zoom control. This action affects both the video preview locally and the stream published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|direction |ByteRTCZoomDirectionType |Action of the digital zoom control. Refer to [ByteRTCZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCZoomDirectionType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* As the default offset is `0`, you must call [setVideoDigitalZoomConfig:size:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomconfig-size) before this API.

* You can only move video images after they are magnified via this API or [setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol).

* The control process stops when the scale reaches the limit, or the images have been moved to the border. If the next action exceeds the scale or movement range, SDK will execute it with the limits.

* Call [stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopvideodigitalzoomcontrol) to stop the ongoing zoom control.

* Call [setVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodigitalzoomcontrol) to have a one\-time digital zoom control.

* Refer to [setCameraZoomRatio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setcamerazoomratio) if you intend to have an optical zoom control to the camera. For iOS only.

### stopVideoDigitalZoomControl

```objectivec
- (int)stopVideoDigitalZoomControl;
```

Stop the ongoing digital zoom control instantly.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Refer to [startVideoDigitalZoomControl:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideodigitalzoomcontrol) for starting digital zooming.

### registerLocalVideoProcessor:withConfig:

```objectivec
- (int)registerLocalVideoProcessor:(_Nullable id<ByteRTCVideoProcessorDelegate>) processor
                        withConfig:(ByteRTCVideoPreprocessorConfig* _Nullable)config NS_SWIFT_NAME(registerLocalVideoProcessor(_:withConfig:));
```

Set up a custom video preprocessor.

Using this video preprocessor, you can call [processVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCVideoProcessorDelegate-processvideoframe) to preprocess the video frames captured by the RTC SDK and use the processed video frames for RTC audio & video communication.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|processor |id<ByteRTCVideoProcessorDelegate\> |Custom video processor. See [ByteRTCVideoProcessorDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCVideoProcessorDelegate). If null is passed in, the video frames captured by the RTC SDK are not preprocessed.<br><br> <br><br>SDK only holds weak references to the processor, you should guarantee its Life Time.<br><br> <br><br>When designing the'processor ', the video frame data should be obtained from the'textureBuf' field of [ByteRTCVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrame);<br><br> <br><br>The video frame data returned after processing should be in the format of'ByteRTCVideoPixelFormat 'in [ByteRTCVideoPixelFormat](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoPixelFormat), and must be stored in the'textureBuf' field that returns the frame data. |
|config |ByteRTCVideoPreprocessorConfig\* |Customize the settings applicable to the video preprocessor. See [ByteRTCVideoPreprocessorConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoPreprocessorConfig).<br><br> <br><br>Currently, the 'required_pixel_format 'in'config' only supports: 'ByteRTCVideoPixelFormatI420' and'ByteRTCVideoPixelFormatUnknown ':<br><br><br> <br><br>* When set to'Unknown', the RTC SDK gives the format of the video frame for processing by the processor, that is, the format of the acquisition.<br><br>* When set to'ByteRTCVideoPixelFormatI420 ', the RTC SDK will convert the captured video into the corresponding format for pre\-processing. This method call fails when<br><br>* Is set to another value. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* When this interface is called repeatedly, only the last call takes effect. The effects do not stack.

* For iOS platforms, setting the requiredPixelFormat in [ByteRTCVideoPreprocessorConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoPreprocessorConfig) to'kVideoPixelFormatUnknown 'brings some performance optimization by avoiding format conversion.

### registerLocalEncodedVideoFrameObserver:

```objectivec
- (int)registerLocalEncodedVideoFrameObserver:(_Nullable id<ByteRTCLocalEncodedVideoFrameObserver>) frameObserver NS_SWIFT_NAME(registerLocalEncodedVideoFrameObserver(_:));
```

Register a local video frame observer.

This method applies to both internal capturing and custom capturing.

After calling this API, SDK triggers [onLocalEncodedVideoFrame:Frame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCLocalEncodedVideoFrameObserver-onlocalencodedvideoframe-frame) whenever a video frame is captured.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|frameObserver |id<ByteRTCLocalEncodedVideoFrameObserver\> |Local video frame observer. See [ByteRTCLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCLocalEncodedVideoFrameObserver). You can cancel the registration by setting it to `nullptr`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

You can call this API before or after entering the RTC room. Calling this API before entering the room ensures that video frames are monitored and callbacks are triggered as early as possible.

### setAudioRoute:

```objectivec
- (int)setAudioRoute:(ByteRTCAudioRoute)audioRoute;
```

Set the current audio playback route. The default device is set via [setDefaultAudioRoute:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setdefaultaudioroute).

When the audio playback route changes, you will receive [rtcEngine:onAudioRouteChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudioroutechanged).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioRoute |ByteRTCAudioRoute |Audio route. Refer to [ByteRTCAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRoute). You can only use the build\-in speaker or the default route. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You can implement most scenarios by calling [setDefaultAudioRoute:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setdefaultaudioroute) and the default audio route switching strategy of the RTC SDK. For details about the strategy, see [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836). You should use this API in a few exceptional scenarios like manually switching audio route with external audio device connected.

* This interface is supported in both communication mode and media mode, but the target route for switching only supports the built\-in speaker.

* For the volume type in different audio scenarios, refer to [ByteRTCAudioScenarioType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioScenarioType).

### getAudioRoute

```objectivec
- (ByteRTCAudioRoute)getAudioRoute;
```

Gets the information of currently\-using playback route.

**Return Value**

See [ByteRTCAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRoute).

**Notes**

To set the audio playback route, see [setAudioRoute:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudioroute). For mobile only.

### enableExternalSoundCard:

```objectivec
- (int)enableExternalSoundCard:(bool)enable;
```

Enables the audio process mode for external sound card.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |* true: enable<br><br>* false: disable (by default) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* When you use an external sound card for audio capture, enable this mode for better audio quality.

* When using the mode, you can only use earphones. If you need to use internal or external speaker, disable this mode.

### setDefaultAudioRoute:

```objectivec
- (int)setDefaultAudioRoute:(ByteRTCAudioRoute)audioRoute;
```

Set the speaker or earpiece as the default audio playback device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioRoute |ByteRTCAudioRoute |Audio playback device. Refer to [ByteRTCAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRoute). You can only use earpiece and speakerphone. |

**Return Value**

* 0: Success.

* < 0: failure. It fails when the device designated is neither a speaker nor an earpiece.

**Notes**

For the default audio route switching strategy of the RTC SDK, see [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836).

### startPushMixedStream:withPushTargetConfig:withMixedConfig:

```objectivec
- (int)startPushMixedStream:(NSString* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig*_Nullable)config;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPushMixedStreamToCDN:mixedConfig:observer:` and `startPushPublicStream:withLayout:` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these two methods, please migrate to this interface.

Specifies the streams to be mixed and initiates the task to push the mixed stream to CDN or WTN.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |NSString\* |Task ID. The length should not exceed 127 bytes.<br><br> <br><br>You may want to push more than one mixed stream to CDN from the same room. When you do that, use different ID for corresponding tasks; if you will start only one task, use an empty string. |
|pushTargetConfig |ByteRTCMixedStreamPushTargetConfig\* |Push target config, such as the push URL and WTN stream ID. See [ByteRTCMixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamPushTargetConfig). |
|config |ByteRTCMixedStreamConfig\* |Configurations to be set when pushing streams to CDN or WTN. See [ByteRTCMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamConfig). |

**Return Value**

* 0: Success. You can get notified the result of the task and the events in the process of pushing the stream to CDN via [rtcEngine:onMixedStreamEvent:withMixedStreamInfo:withErrorCode:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onmixedstreamevent-withmixedstreaminfo-witherrorcode).

* !0: Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* After calling this API, you will be informed of the result and errors during the pushing process via the [rtcEngine:onMixedStreamEvent:withMixedStreamInfo:withErrorCode:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onmixedstreamevent-withmixedstreaminfo-witherrorcode) callback.

* Subscribe to the Push\-to\-CDN and the WTN stream notifications in the [console](https://console.byteplus.com/rtc/cloudRTC?tab=callback) to receive notifications about task status changes. When calling this API repeatedly, subsequent calls to this API will trigger both [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) and [TranscodeUpdated](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodeupdated) callbacks.

* Call [stopPushMixedStream:withPushTargetType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stoppushmixedstream-withpushtargettype) to stop pushing streams to CDN.

* Call [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig) to update part of the configurations of the task.

* Call [startPushSingleStream:singleStream:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startpushsinglestream-singlestream) to push a single stream to CDN.

### updatePushMixedStream:withPushTargetConfig:withMixedConfig:

```objectivec
- (int)updatePushMixedStream:(NSString*_Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig*_Nonnull)config;
```

> Available since 3.60. Since version 3.60, this interface replaces the `updatePushMixedStreamToCDN:mixedConfig:` and `updatePublicStreamParam:withLayout:` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these two methods, please migrate to this interface.

Update parameters needed when pushing mixed media streams to CDN. You will be informed of the change via the [rtcEngine:onMixedStreamEvent:withMixedStreamInfo:withErrorCode:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onmixedstreamevent-withmixedstreaminfo-witherrorcode) callback.

After calling [startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startpushmixedstream-withpushtargetconfig-withmixedconfig) to enable the function of pushing streams to CDN, you can call this API to update the relevant configurations.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |NSString\* |Task ID. Specifies of which pushing task you want to update the parameters. |
|pushTargetConfig |ByteRTCMixedStreamPushTargetConfig\* |Push target config, such as the push url and WTN stream ID. See [ByteRTCMixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamPushTargetConfig). |
|config |ByteRTCMixedStreamConfig\* |Configurations that you want to update. See [ByteRTCMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamConfig) for specific indications. You can update any property for the task unless it is specified as unavailable for updates.<br><br> <br><br>If you left some properties blank, you can expect these properties to be set to their default values. |

**Return Value**

* 0: Success.

* !0: Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

### stopPushMixedStream:withPushTargetType:

```objectivec
- (int)stopPushMixedStream:(NSString*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType;
```

> Available since 3.60. Since version 3.60, this interface replaces the `stopPushStreamToCDN:` method for stopping the push of mixed streams to CDN. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Stops the task to push a mixing media stream to CDN or a WTN stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |NSString\* |Task ID. Specifies of which pushing task you want to update the parameters. |
|pushTargetType |ByteRTCMixedStreamPushTargetType |See [ByteRTCMixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamPushTargetType). |

**Return Value**

* 0: Success

* !0: Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* To start pushing a mixing stream to CDN or a WTN stream, see [startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startpushmixedstream-withpushtargetconfig-withmixedconfig).

### startPushSingleStream:singleStream:

```objectivec
- (int)startPushSingleStream:(NSString*_Nonnull)taskId singleStream:(ByteRTCPushSingleStreamParam*_Nonnull)singleStream;
```

Pushes a single media stream to CDN or RTC room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |NSString\* |Task ID.<br><br> <br><br>You may want to start more than one task to push streams to CDN or RTC room. When you do that, use different IDs for corresponding tasks; if you will start only one task, use an empty string. |
|singleStream |ByteRTCPushSingleStreamParam\* |Configurations for pushing a single stream to CDN or RTC room. See [ByteRTCPushSingleStreamParam](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPushSingleStreamParam). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Before calling this API，you need to enable Push to CDN on the [console](https://console.byteplus.com/rtc/workplaceRTC).

* After calling this API, you will be informed of the result and errors during the pushing process with [rtcEngine:onSingleStreamEvent:withTaskId:withErrorCode:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onsinglestreamevent-withtaskid-witherrorcode).

* Call [stopPushSingleStream:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stoppushsinglestream) to stop the task.

* Since this API does not perform encoding and decoding, the video stream pushed to RTMP will change according to the resolution, encoding method, and whether the camera on the publisher side is turned off.

### stopPushSingleStream:

```objectivec
- (int)stopPushSingleStream:(NSString*_Nonnull)taskId;
```

> Available since 3.60. Since version 3.60, this interface replaces the `stopPushStreamToCDN:` method for stopping the push of single media streams to CDN. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Stops the task to push a single media stream to CDN started via [startPushSingleStream:singleStream:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startpushsinglestream-singlestream).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |NSString\* |Task ID. Specifies the task you want to stop. |

**Return Value**

* 0: Success

* < 0 : Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

### getWTNStream

```objectivec
- (ByteRTCWTNStream*_Nullable)getWTNStream;
```

Get the WTN stream object.

**Return Value**

WTN stream object, see [ByteRTCWTNStream](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream).

### pushExternalVideoFrame:

```objectivec
- (int)pushExternalVideoFrame:(ByteRTCVideoFrameData* _Nonnull)frame;
```

Pushes external video frames, encapsulated with ByteRTCVideoFrame.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|frame |ByteRTCVideoFrameData\* |This video frame contains video data to be encoded by the SDK. Refer to [ByteRTCVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrame). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

Before pushing an external video frame, you must call [setVideoSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideosourcetype) Turn on external video source capture.

### enableAudioFrameCallback:format:

```objectivec
- (int)enableAudioFrameCallback:(ByteRTCAudioFrameCallbackMethod) method format:(ByteRTCAudioFormat* _Nullable)format;
```

Enable audio frames callback and set the format for the specified type of audio frames.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |ByteRTCAudioFrameCallbackMethod |Audio data callback method. See [ByteRTCAudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrameCallbackMethod).<br><br> <br><br>If `method` is set as `0`, `1`, `2`, or `5`, set `format` to the accurate value listed in the audio parameters format.<br><br> <br><br>If `method` is set as `3`, set `format` to `auto`. |
|format |ByteRTCAudioFormat\* |Audio parameters format. See [ByteRTCAudioFormat](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

After calling this API and [registerAudioFrameObserver:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer-registeraudioframeobserver), [ByteRTCAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameObserver) will receive the corresponding audio data callback. However, these two APIs are independent of each other and the calling order is not restricted.

### disableAudioFrameCallback:

```objectivec
- (int)disableAudioFrameCallback:(ByteRTCAudioFrameCallbackMethod) method;
```

Disables audio data callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |ByteRTCAudioFrameCallbackMethod |Audio data callback method. See [ByteRTCAudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrameCallbackMethod). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

Call this API after calling [enableAudioFrameCallback:format:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableaudioframecallback-format).

### registerAudioFrameObserver:

```objectivec
- (int)registerAudioFrameObserver:(_Nullable id<ByteRTCAudioFrameObserver>) audioFrameObserver NS_SWIFT_NAME(registerAudioFrameObserver(_:));
```

Register an audio frame observer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrameObserver |id<ByteRTCAudioFrameObserver\> |Audio data callback observer. See [ByteRTCAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameObserver). Use `null` to cancel the registration. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

After calling this API and [enableAudioFrameCallback:format:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableaudioframecallback-format), [ByteRTCAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameObserver) receives the corresponding audio data callback. You can retrieve the audio data and perform processing on it without affecting the audio that RTC SDK uses to encode or render.

### registerAudioProcessor:

```objectivec
- (int)registerAudioProcessor:(_Nullable id<ByteRTCAudioFrameProcessor>)processor;
```

Register a custom audio preprocessor.

After that, you can call [enableAudioProcessor:audioFormat:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-enableaudioprocessor-audioformat) to process the audio streams that either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|processor |id<ByteRTCAudioFrameProcessor\> |Custom audio processor. See [ByteRTCAudioFrameProcessor](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameProcessor)。<br><br> <br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. To cancel registration, set the parameter to nullptr. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* When this interface is repeatedly called, only the last call takes effect.

* Refer to [Custom Audio Processing](https://docs.byteplus.com/en/byteplus-rtc/docs/80635) for more information.

### enableAudioProcessor:audioFormat:

```objectivec
- (int)enableAudioProcessor:(ByteRTCAudioFrameMethod)method
                 audioFormat:(ByteRTCAudioFormat*_Nullable)format;
```

Enable audio frames callback for custom processing and set the format for the specified type of audio frames.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |ByteRTCAudioFrameMethod |The types of audio frames. See [ByteRTCAudioFrameMethod](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrameMethod). Set this parameter to process multiple types of audio.<br><br> <br><br>With different values, you will receive the corresponding callback:<br><br><br> <br><br>* For locally captured audio, you will receive [onProcessRecordAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameProcessor-onprocessrecordaudioframe).<br><br>* For mixed remote audio, you will receive [onProcessPlayBackAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameProcessor-onprocessplaybackaudioframe).<br><br>* For audio from remote users, you will receive [onProcessRemoteUserAudioFrame:info:audioFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameProcessor-onprocessremoteuseraudioframe-info-audioframe).<br><br>* For SDK\-level in\-ear monitoring audio, you will receive [onProcessEarMonitorAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameProcessor-onprocessearmonitoraudioframe) (Only on iOS).<br><br>* For shared\-screen audio, you will receive [onProcessScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCAudioFrameProcessor-onprocessscreenaudioframe). |
|format |ByteRTCAudioFormat\* |The format of the returned audio frame. See [ByteRTCAudioFormat](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Before calling this API, call [registerAudioProcessor:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registeraudioprocessor) to register a processor.

* To disable custom audio processing, call [disableAudioProcessor:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-disableaudioprocessor).

### disableAudioProcessor:

```objectivec
- (int)disableAudioProcessor:(ByteRTCAudioFrameMethod)method;
```

Disable custom audio processing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |ByteRTCAudioFrameMethod |Audio Frame type. See [ByteRTCAudioFrameMethod](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrameMethod). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### pushExternalAudioFrame:

```objectivec
- (int)pushExternalAudioFrame:(ByteRTCAudioFrame* _Nonnull) audioFrame;
```

Push custom captured audio data to the RTC SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Audio data frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame).<br><br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity should be audioFrame.samples × audioFrame.channel × 2.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Before pushing external audio data, you must call [setAudioSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudiosourcetype) to enable custom audio capture.

* You must push custom captured audio data every 10 milliseconds. The samples (number of audio sampling points) of a single push should be `audioFrame.sample Rate/100`. For example, when the sampling rate is set to 48000, data of 480 sampling points should be pushed each time.

### pullExternalAudioFrame:

```objectivec
- (int)pullExternalAudioFrame:(ByteRTCAudioFrame* _Nonnull) audioFrame;
```

Pull remote audio data. You can use the data for audio processing or custom rendering.

After calling this method, the SDK will actively pull the audio data that is ready to be played, including the decoded and mixed audio data from remote end for external playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Audio data frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |

**Return Value**

* 0: Success

* < 0: Failure

**Notes**

* Before pulling custom audio data, you must call [setAudioRenderType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudiorendertype) to enable custom audio capture and rendering.

* You should pull audio data every 10 milliseconds since the duration of a RTC SDK audio frame is 10 milliseconds. Samples x call frequency = audioFrame's sample rate. Assume that the sampling rate is set to 48000, call this API every 10 ms, so that 480 sampling points should be pulled each time.

* The audio sampling format is S16. The data format in the audio buffer is PCM, and its capacity size is `audioFrame.samples × audioFrame.channel × 2`.

### pushReferenceAudioPCMData:

```objectivec
- (int)pushReferenceAudioPCMData:(ByteRTCAudioFrame* _Nonnull) audioFrame;
```

Push custom aec reference audio data to the RTC SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Audio data frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |

**Return Value**

Method call result

* 0: Success

* <\-1: Failure

* <\-302：Warning. The configuration delivers an invalid aec scene.

* <\-303：Warning. The configuration delivers an invalid aec type.

**Notes**

* Before calling this API, you must call [setAudioRenderType](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setaudiorendertype) to enable custom audio render.

* `audioFrame` must include all playback audio signals that you expect AEC to remove, such as RTC playback and third\-party audio that is actually played by the device.

* Push one 10 ms audio frame every 10 ms from a stable thread. Keep the scheduling jitter within approximately 1 ms. The number of samples multiplied by the call frequency must equal `audioFrame`'s sample rate. For example, at a sample rate of 48000 Hz, push 480 samples per call.

* The audio sampling format is S16. The data format in the audio buffer is PCM data, and its capacity is `audioFrame.samples × audioFrame.channel × 2` bytes.

### setBusinessId:

```objectivec
- (int)setBusinessId:(NSString* _Nullable)businessId;
```

Sets the business ID

You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|businessId |NSString\* |Your customized businessId<br><br> <br><br>BusinessId is a tag, and you can customize its granularity. |

**Return Value**

* 0: Success.

* \-2: The input is invalid. Legal characters include all lowercase letters, uppercase letters, numbers, and four other symbols, including '.', '\-','_', and '@'.

**Notes**

* You must call this API before the [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) API, otherwise it will be invalid.

### feedback:info:

```objectivec
- (int)feedback:(ByteRTCProblemFeedbackOption)types info:(ByteRTCProblemFeedbackInfo* _Nullable)info;
```

The call ends and the user feedback problem is reported to RTC

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|types |ByteRTCProblemFeedbackOption |The list of preset problems. See [ByteRTCProblemFeedbackOption](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCProblemFeedbackOption) |
|info |ByteRTCProblemFeedbackInfo\* |Specific description of other problems other than the preset problem, and room's information. See [ByteRTCProblemFeedbackInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCProblemFeedbackInfo) |

**Return Value**

* 0: Success.

* \-3: Failure.

**Notes**

If the user is in the room when reporting, the report is associated with the room or rooms where the user is currently located;

If the user is not in the room when reporting, the report leads to the previously exited Room.

### getNativeHandle

```objectivec
- (void* _Nullable) getNativeHandle;
```

Get [IRTCEngine](https://docs.byteplus.com/byteplus-rtc/docs/70095#irtcengine) in C++ layer.

**Return Value**

* \>0：Success. Return the address of `IRTCEngine` in C++ layer.

* NULL：Failure.

**Notes**

In some scenarios, getting and working with `IRTCEngine` in C++ layer has much higher execution efficiency than through the OC encapsulation layer. Typical scenarios include: custom processing of video/audio frames, encryption of audio and video calls, etc.

### setPublishFallbackOption:

```objectivec
- (int)setPublishFallbackOption:(ByteRTCPublishFallbackOption)option;
```

Sets the fallback option for published audio & video streams.

You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|option |ByteRTCPublishFallbackOption |Fallback option, see [ByteRTCPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishFallbackOption). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* This API only works after you call [setLocalSimulcastMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalsimulcastmode) to enable the mode of publishing multiple streams.

* You must call this API before the user enters the room.

* After calling this method, if there is a performance degradation or recovery due to poor performance or network conditions, the local end will receive early warnings through the [rtcEngine:onPerformanceAlarms:info:mode:reason:sourceWantedData:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onperformancealarms-info-mode-reason-sourcewanteddata) callback to adjust the capture device.

* After setting the fallback option, the user subscribed to the audio/video stream will receive [rtcEngine:onSimulcastSubscribeFallback:info:event:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onsimulcastsubscribefallback-info-event) when the audio/video stream published by the local user falls back or resumes from the fallback.

* You can alternatively set fallback options in the console, which is of higher priority.

### setSubscribeFallbackOption:

```objectivec
- (int)setSubscribeFallbackOption:(ByteRTCSubscribeFallbackOption)option;
```

Sets the fallback option for subscribed RTC streams.

You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|option |ByteRTCSubscribeFallbackOption |Fallback option, see [ByteRTCSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSubscribeFallbackOption) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* You must call this API before entering the room.

* When the fallback option is set, the local user will receive [rtcEngine:onSimulcastSubscribeFallback:info:event:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onsimulcastsubscribefallback-info-event) and [rtcEngine:onRemoteVideoSizeChanged:info:withFrameInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onremotevideosizechanged-info-withframeinfo) when the subscribed audio/video stream falls back or resumes from a fallback.

* You can alternatively set fallback options in the console, which is of higher priority.

### setRemoteUserPriority:InRoomId:uid:

```objectivec
- (int)setRemoteUserPriority:(ByteRTCRemoteUserPriority)priority
                         InRoomId:(NSString*_Nonnull)roomId
                              uid:(NSString*_Nonnull)uid NS_SWIFT_NAME(setRemoteUserPriority(_:InRoomId:uid:));
```

Sets user priority

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|priority |ByteRTCRemoteUserPriority |Priority of remote user. See enumeration type [ByteRTCRemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteUserPriority) |
|roomId |NSString\* |Room ID |
|uid |NSString\* |ID of remote user |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* This method is used with [setSubscribeFallbackOption:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setsubscribefallbackoption).

* If the subscription flow fallback option is turned on, weak connections or insufficient performance will give priority to ensuring the quality of the flow received by high\-priority users.

* This method can be used before and after entering the room, and the priority of the remote user can be modified.

### setEncryptInfo:key:

```objectivec
- (int)setEncryptInfo:(ByteRTCEncryptType)encrypt_type key:(NSString* _Nonnull)key;
```

Sets the way to use built\-in encryption when transmitting.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|encrypt_type |ByteRTCEncryptType |Built\-in encryption algorithm. See [ByteRTCEncryptType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEncryptType) |
|key |NSString\* |Encryption key, limited to 36 bits in length, beyond which it will be truncated |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Use this method when using built\-in encryption when transmitting; if you need to use transmission See [onEncryptData:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEncryptHandler-onencryptdata).

   Built\-in encryption and custom encryption are mutually exclusive. Determine the scheme of transmission encryption according to the last called method.

* This method must be called before entering the room, and can be called repeatedly, taking the last called parameter as the effective parameter.

### setCustomizeEncryptHandler:

```objectivec
- (int)setCustomizeEncryptHandler:(id<ByteRTCEncryptHandler> _Nullable)handler NS_SWIFT_NAME(setCustomizeEncryptHandler(_:));
```

Sets custom encryption and decryption methods.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |id<ByteRTCEncryptHandler\> |Custom encryption handler, which needs to implement the encryption and decryption method. See [ByteRTCEncryptHandler](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEncryptHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The method and [setEncryptInfo:key:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setencryptinfo-key) are mutually exclusive relationships, that is, according to the call order, the last call method takes effect version.

* This method must be called before calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig), which can be called repeatedly, taking the last called parameter as the effective parameter.

* Whether encrypted or decrypted, the length of the modified data needs to be controlled under 180%. That is, if the input data is 100 bytes, the processed data must be less than 180 bytes. If the encryption or decryption result exceeds the limit, the audio & video frame may be discarded.

* Data encryption/decryption is performed serially, so depending on the implementation, the method may affect the final rendering efficiency. Whether to use this method needs to be carefully evaluated by the user.

### createRTCRoom:

```objectivec
- ( ByteRTCRoom* _Nullable)createRTCRoom:(NSString* _Nonnull)roomId;
```

Create a RTC room instance.

This API only returns a room instance. You still need to call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to actually create/join the room.

Each call of this API creates one [ByteRTCRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) of each RTCRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomId |NSString\* |The string matches the regular expression: `[a-zA-Z0-9_\@\-\.]{1,128}`. |

**Return Value**

[ByteRTCRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the roomId is valid. And the specified room is not yet created.

**Notes**

* If the room that you wish to join already exists, you still need to call this API first to create the ByteRTCRoom instance, and then call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig).

* Do not create multiple rooms with the same roomId, otherwise the newly created room instance will replace the old one.

* To forward streams to the other rooms, call [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms) instead of enabling Multi\-room mode.

### createRTSRoom:

```objectivec
- ( ByteRTCRTSRoom* _Nullable)createRTSRoom:(NSString* _Nonnull)roomId;
```

Create an RTS room instance.

This API only returns an RTS room instance. You still need to call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) to actually create/join the room.

Each call of this API creates one [ByteRTCRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRTSRoom-joinrtsroom-userinfo) of each ByteRTCRTSRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can send and receive RTS messages in the joined rooms at the same time.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomId |NSString\* |The string matches the regular expression: `[a-zA-Z0-9_\@\-\.]{1,128}`. |

**Return Value**

[ByteRTCRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the roomId is valid. And the specified room is not yet created.

**Notes**

* If the room that you wish to join already exists, you still need to call this API first to create the ByteRTCRTSRoom instance, and then call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig).

* Do not create multiple rooms with the same roomId, otherwise the newly created room instance will replace the old one.

### setExtensionConfig:

```objectivec
- (int)setExtensionConfig:(NSString*_Nullable)groupId;
```

Set Extension configuration. It should be set before capturing screen internally.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|groupId |NSString\* |Your app and Extension should belong to the same App Group. You need to put in their Group ID here. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

You must call this API immediately after calling [createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcengine-delegate). You only need to call this API once in the life cycle of the engine instance.

### setRuntimeParameters:

```objectivec
- (int)setRuntimeParameters:(NSDictionary* _Nullable)parameters;
```

Sets runtime parameters

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|parameters |NSDictionary\* |Reserved parameters |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

Call this API before [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) and [startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture).

### startScreenCapture:bundleId:

```objectivec
- (int)startScreenCapture:(ByteRTCScreenMediaType) type bundleId:(NSString*_Nullable)bundleId;
```

Starts capturing the screen audio and/or video stream with the RTC SDK internal module.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCScreenMediaType |Media type. See [ByteRTCScreenMediaType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCScreenMediaType). |
|bundleId |NSString\* |The bundle ID of the Extension, which is used to only display your Extension in your app. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicewarning-devicetype-devicewarning) or [rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicewarning-devicetype-devicewarning) after calling this API when the source is set to an external recorder.

* If you start the Extension from the iOS control center, this API do not need to be called.

* After the streams are captured, you need to call [publishStreamVideo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamvideo) and/or [publishStreamAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamaudio) to push the streams to the remote end.

* You will receive [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) and [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error) when the capturing is started.

### updateScreenCapture:

```objectivec
- (int)updateScreenCapture:(ByteRTCScreenMediaType) type;
```

Updates the media type of the internal screen capture.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCScreenMediaType |Media type. See [ByteRTCScreenMediaType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCScreenMediaType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Call this API after starting screen capture.

* You will receive [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) or [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error).

### stopScreenCapture

```objectivec
- (int)stopScreenCapture;
```

Stop internal screen capture.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicewarning-devicetype-devicewarning) or [rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicewarning-devicetype-devicewarning) after calling this API when the source is set to an external recorder.

* Calling this API changes the capturing status without affecting the publishing status.

* You will receive [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) and [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error).

### sendScreenCaptureExtensionMessage:

```objectivec
- (int)sendScreenCaptureExtensionMessage:(NSData*_Nonnull) messsage;
```

Sends message to screen capture Extension

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|messsage |NSData\* |Message sent to the Extension |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Call this API after calling [startScreenCapture:bundleId:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startscreencapture-bundleid).

* The extension will receive [onReceiveMessageFromApp:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRtcScreenCapturerExtDelegate-onreceivemessagefromapp) when the message is sent.

### startFileRecording:type:

```objectivec
- (int)startFileRecording: (ByteRTCRecordingConfig* _Nonnull)recordingConfig type:(ByteRTCRecordingType)recordingType NS_SWIFT_NAME(startFileRecording(withRecordingConfig:type:));
```

This method records the audio & video data during the call to a local file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|recordingConfig |ByteRTCRecordingConfig\* |Local recording parameter configuration. See [ByteRTCRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingConfig) |
|recordingType |ByteRTCRecordingType |Locally recorded media type, see [ByteRTCRecordingType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingType)<br><br> <br><br>Note: Screen stream only supports recording video (ByteRTCRecordingTypeVideoOnly); Main stream supports recording all types. |

**Return Value**

* 0: normal

* \-1: Parameter setting exception

* \-2: The current version of the SDK does not support this feature, please contact technical support

**Notes**

* You must join a room before calling this method.

* After calling this API is called, the local user will receive [rtcEngine:onRecordingStateUpdate:state:error_code:recording_info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onrecordingstateupdate-state-error_code-recording_info) callback.

* If the recording is normal, the system will report the recording progress through [rtcEngine:onRecordingProgressUpdate:process:recording_info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onrecordingprogressupdate-process-recording_info) callback every second.

### stopFileRecording

```objectivec
- (int)stopFileRecording;
```

Stops local recording

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* After calling [startFileRecording:type:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startfilerecording-type) to start local recording, you must call this method to stop recording.

* The recording result will be called back through [rtcEngine:onRecordingStateUpdate:state:error_code:recording_info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onrecordingstateupdate-state-error_code-recording_info).

### startAudioRecording:

```objectivec
- (int)startAudioRecording:(ByteRTCAudioRecordingConfig* _Nonnull) recordingConfig;
```

Starts recording audio communication and generates the local file.

If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|recordingConfig |ByteRTCAudioRecordingConfig\* |See [ByteRTCAudioRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRecordingConfig). |

**Return Value**

* 0: Success

* \-2: Invalid parameters

* \-3: Not valid in this SDK. Please contact the technical support.

**Notes**

* All audio effects are valid in the file. Mixed audio file is not included in the file.

* Call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopaudiorecording) to stop recording.

* You can call this API before and after joining the room. If this API is called before you join the room, you need to call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopaudiorecording) to stop recording. If this API is called after you join the room, the recording task ends automatically. If you join multiple rooms, audio from all rooms are recorded in one file.

* After calling the API, you'll receive [rtcEngine:onAudioRecordingStateUpdate:error_code:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiorecordingstateupdate-error_code).

### stopAudioRecording

```objectivec
- (int)stopAudioRecording;
```

Stop audio recording.

**Return Value**

* 0: Success

* <0: Failure

**Notes**

Call [startAudioRecording:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startaudiorecording) to start the recording task.

### getAudioEffectPlayer

```objectivec
- (ByteRTCAudioEffectPlayer*_Nullable)getAudioEffectPlayer;
```

> Available since 3.53

Create an instance for audio effect player.

**Return Value**

See [ByteRTCAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14172#ByteRTCAudioEffectPlayer).

### getMediaPlayer:

```objectivec
- (ByteRTCMediaPlayer*_Nullable)getMediaPlayer:(int)playerId;
```

> Available since 3.53

Create a media player instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|playerId |int |Media player id. The range is `[0, 3]`. You can create up to 4 instances at the same time. If it exceeds the range, nullptr will be returned. |

**Return Value**

Media player instance. See [ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/14172#ByteRTCMediaPlayer).

### login:uid:

```objectivec
- (int)login:(NSString* _Nonnull)token uid:(NSString* _Nonnull)uid;
```

Sign in to call [sendUserMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendusermessageoutsideroom-message-config) and [sendServerMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.

To sign out, call [logout](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-logout).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |NSString\* |Token is required during login for authentication.<br><br> <br><br>This Token is different from that required by calling joinRoom. You can assign any value even null to `roomId` to generate a login token. During developing and testing, you can use temporary tokens generated on the console. Deploy the token generating application on your server. |
|uid |NSString\* |User ID which need to be unique within one appid. |

**Return Value**

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

The local user will receive [rtcEngine:onLoginResult:errorCode:elapsed:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onloginresult-errorcode-elapsed) after this API is called successfully. But remote users will not receive notification about that.

### logout

```objectivec
- (int)logout;
```

Sign out of the RTS server.

After calling this API to sign out, you cannot call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Before calling this interface to log out, [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) Login

* After local users call this method to log out, they will receive [rtcEngine:onLogout:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onlogout) callback notification results, and remote users will not receive notifications.

### updateLoginToken:

```objectivec
- (int)updateLoginToken:(NSString* _Nonnull)token;
```

Updates the Token used by the user to sign in.

Token used by the user to sign in has a certain valid period. When the Token expires, you need to call this method to update the login Token information.

If [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) is called with an expired Token, the login fails and the local user will receive [rtcEngine:onLoginResult:errorCode:elapsed:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onloginresult-errorcode-elapsed) about corresponding error code. You need to reacquire a Token and update it with this method.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |NSString\* |Updated dynamic key |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* If the token is invalid and the login fails, call this method to update the token, and the SDK will automatically log in again. The user does not need to call the [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) method.

* If the token expires after you have successfully signed in, it will not be affected. An expired Token error will be notified to the user the next time you log in with an expired Token, or when you log in again due to a disconnection due to poor local network conditions.

### setServerParams:url:

```objectivec
- (int)setServerParams:(NSString* _Nonnull)signature url:(NSString* _Nonnull)url;
```

Sets application server parameters

Client side calls [sendServerMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendservermessage) or [sendServerBinaryMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-sendserverbinarymessage) Before sending a message to the application server, you must set a valid signature and application server address.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|signature |NSString\* |Dynamic signature. The App server may use the signature to verify the source of messages.<br><br> <br><br>You need to define the signature yourself. It can be any non\-empty string. It is recommended to encode information such as UID into the signature.<br><br> <br><br>The signature will be sent to the address set through the "url" parameter in the form of a POST request. |
|url |NSString\* |Address of the application server |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The user must call [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) before logging in to call this interface.

* After calling this interface, the SDK will use [rtcEngine:onServerParamsSetResult:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onserverparamssetresult) to return the corresponding result.

### getPeerOnlineStatus:

```objectivec
- (int)getPeerOnlineStatus:(NSString* _Nonnull)peerUserId;
```

Query the sign\-in status of the remote or local user

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|peerUserId |NSString\* |User ID to query |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You must call [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) After logging in, you can call this interface.

* After calling this interface, the SDK will use [rtcEngine:onGetPeerOnlineStatus:status:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-ongetpeeronlinestatus-status) callback to notify the query result.

* Before sending an out\-of\-room message, the user can know whether the peer user is signed in through this API to decide whether to send a message. You can also check your sign\-in status through this API.

### sendUserMessageOutsideRoom:message:config:

```objectivec
- (NSInteger)sendUserMessageOutsideRoom:(NSString* _Nonnull)userId message:(NSString* _Nonnull)messageStr config:(ByteRTCMessageConfig)config;
```

Sends a text message (P2P) to a specified user outside the room

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|userId |NSString\* |\- |
|messageStr |NSString\* |Text message content sent. Message does not exceed 64 KB. |
|config |ByteRTCMessageConfig |Message type, see [ByteRTCMessageConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMessageConfig). |

**Return Value**

* \> 0: Sent successfully, return the number of the sent message, increment from 1.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending an out\-of\-room text message, you should call [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) to complete login.

* After the user calls this API to send a text message, he will receive an [rtcEngine:onUserMessageSendResultOutsideRoom:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onusermessagesendresultoutsideroom-error) callback to know whether the message was sent successfully;

* If the text message is sent successfully, the user specified by the userId will receive the message through [rtcEngine:onUserMessageReceivedOutsideRoom:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-message) callback.

### sendUserBinaryMessageOutsideRoom:message:config:

```objectivec
- (NSInteger)sendUserBinaryMessageOutsideRoom:(NSString* _Nonnull)userId message:(NSData* _Nonnull)messageStr config:(ByteRTCMessageConfig)config;
```

Send binary messages (P2P) to the specified user outside the room

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|userId |NSString\* |Message receiving user's ID |
|messageStr |NSData\* |Binary message content sent. Message does not exceed 64KB. |
|config |ByteRTCMessageConfig |Message type, see [ByteRTCMessageConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMessageConfig). |

**Return Value**

* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sending failed due to an empty message.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending out\-of\-room binary messages, you must call [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) to complete login.

* After the user calls this API to send a binary message, he will receive an [rtcEngine:onUserMessageSendResultOutsideRoom:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onusermessagesendresultoutsideroom-error) callback to notify whether the message was sent successfully;

* If the binary message is sent successfully, the user specified by the userId will use [rtcEngine:onUserBinaryMessageReceivedOutsideRoom:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-message) callback Receive the message.

### sendServerMessage:

```objectivec
- (NSInteger)sendServerMessage:(NSString* _Nonnull)messageStr;
```

Client side sends a text message to the application server (P2Server)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|messageStr |NSString\* |The content of the text message sent. The message does not exceed 64 KB. |

**Return Value**

* \> 0: Sent successfully, return the number of the sent message, increment from 1.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending a text message to the application server, you must first call [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) to complete the login, and then call [setServerParams:url:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setserverparams-url) Set up the application server.

* After calling this interface, you will receive an [rtcEngine:onServerMessageSendResult:error:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onservermessagesendresult-error-message) callback to inform the message sender whether the message was sent successfully.

* If the text message is sent successfully, the application server that previously called [setServerParams:url:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setserverparams-url) will receive the message.

### sendServerBinaryMessage:

```objectivec
- (NSInteger)sendServerBinaryMessage:(NSData* _Nonnull)messageStr;
```

The client side sends binary messages to the application server (P2Server)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|messageStr |NSData\* |Binary message content sent. Message does not exceed 64KB. |

**Return Value**

* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sending failed due to an empty message.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending a binary message to the application server, call [login:uid:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-login-uid) to complete the login, then call [setServerParams:url:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setserverparams-url) Set up the application server.

* After calling this interface, you will receive an [rtcEngine:onServerMessageSendResult:error:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onservermessagesendresult-error-message) callback to inform the message sender that the sending succeeded or failed;

* If the binary message is sent successfully, the application server that previously called [setServerParams:url:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setserverparams-url) will receive the message.

### startNetworkDetection:uplinkBandwidth:downlink:downlinkBandwidth:

```objectivec
- (int)startNetworkDetection:(bool)isTestUplink uplinkBandwidth:(int)expectedUplinkBitrate downlink:(bool)isTestDownlink downlinkBandwidth:(int)expectedDownlinkBitrate;
```

Pre\-call network detection

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|isTestUplink |bool |Whether to detect uplink bandwidth |
|expectedUplinkBitrate |int |Expected uplink bandwidth, unit: kbps<br><br>Range: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bitrate. |
|isTestDownlink |bool |Whether to detect downlink bandwidth |
|expectedDownlinkBitrate |int |Expected downlink bandwidth, unit: kbps<br><br>Range: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bitrate. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* After calling this interface, you will receive [rtcEngine:onNetworkDetectionResult:quality:rtt:lostRate:bitrate:jitter:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onnetworkdetectionresult-quality-rtt-lostrate-bitrate-jitter) within 3s and every 2s thereafter notifying the probe result;

* If the probe stops, you will receive [rtcEngine:onNetworkDetectionStopped:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onnetworkdetectionstopped) Notify probe to stop.

### stopNetworkDetection

```objectivec
- (int)stopNetworkDetection;
```

Stop pre\-call network probe

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* After calling this interface, you will receive an [rtcEngine:onNetworkDetectionStopped:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onnetworkdetectionstopped) notification to stop the probe.

### setScreenAudioSourceType:

```objectivec
- (int)setScreenAudioSourceType:(ByteRTCAudioSourceType)sourceType;
```

Sets the screen audio source type. (internal capture/custom capture)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|sourceType |ByteRTCAudioSourceType |Screen audio source type. See [ByteRTCAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioSourceType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* The default screen audio source type is RTC SDK internal capture.

* You should call this API before calling publishScreenAudio:. Otherwise, you will receive [rtcEngine:onWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onwarning) with 'ByteRTCWarningSetScreenAudioSourceTypeFailed'.

* When using internal capture, you need to restart screen capture.

* When using custom capture, you need to call [pushScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-pushscreenaudioframe) to push the audio stream to the RTC SDK.

* Whether you use internal capture or custom capture, you must call publishScreenAudio: to publish the captured screen audio stream.

### pushScreenAudioFrame:

```objectivec
- (int) pushScreenAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```

Using a custom capture method, when capturing screen audio during screen sharing, push the audio frame to the RTC SDK for encoding and other processing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Audio data frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame)<br><br><br>* The audio sampling format is S16. The data format within the audio buffer must be PCM data, and its capacity should be samples × frame.channel × 2.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |

**Return Value**

Method call result

* 0: Setup succeeded.

* < 0: Setup failed. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* You must call this API after calling [setScreenAudioSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setscreenaudiosourcetype) to enable custom capture of the screen audio.

* You should call this method every 10 milliseconds to push a custom captured audio frame. A push audio frame should contain frame.sample _rate/100 audio sample points. For example, if the sampling rate is 48000Hz, 480 sampling points should be pushed each time.

* After calling this interface to push the custom captured audio frame to the RTC SDK, you must call publishScreenAudio: to push the captured screen audio to the remote end. Audio frame information pushed to the RTC SDK is lost before calling publishScreenAudio:.

### setVideoSourceType:

```objectivec
- (int)setVideoSourceType:(ByteRTCVideoSourceType)type NS_SWIFT_NAME(setVideoSourceType(_:));
```

Set the video source, including the screen recordings.

The internal video capture is the default, which refers to capturing video using the built\-in module.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCVideoSourceType |Video source type. Refer to [ByteRTCVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSourceType) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You can call this API whether the user is in a room or not.

* Calling this API to switch to the custom video source will stop the enabled internal video capture.

* To switch to internal video capture, call this API to stop custom capture and then call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startvideocapture) to enable internal video capture.

* To push custom encoded video frames to the SDK, call this API to switch `ByteRTCVideoSourceType` to `ByteRTCVideoSourceTypeEncodedManualSimulcast` or `ByteRTCVideoSourceTypeEncodedAutoSimulcast`.

### setExternalVideoEncoderEventHandler:

```objectivec
- (int)setExternalVideoEncoderEventHandler:(id<ByteRTCExternalVideoEncoderEventHandler> _Nullable)handler;
```

Register custom encoded frame push event callback

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |id<ByteRTCExternalVideoEncoderEventHandler\> |Custom encoded frame callback class. See [ByteRTCExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCExternalVideoEncoderEventHandler) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* This method needs to be called before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to nullptr.

### pushExternalEncodedVideoFrame:withEncodedVideoFrame:

```objectivec
- (int)pushExternalEncodedVideoFrame: (NSInteger)videoIndex
                withEncodedVideoFrame:(ByteRTCEncodedVideoFrame* _Nonnull)videoFrame NS_SWIFT_NAME(pushExternalEncodedVideoFrame(withVideoIndex:withEncodedVideoFrame:));
```

Push custom encoded video stream

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoIndex |NSInteger |The corresponding encoded stream subscript, starting from 0, if you call [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideoencoderconfig) The number of multiple streams must be consistent here |
|videoFrame |ByteRTCEncodedVideoFrame\* |Encoding For streaming video frame information. See [ByteRTCEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEncodedVideoFrame). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

* Currently, only video frames in H264 and ByteVC1 formats are supported, and the video stream protocol must be in an Annex B format.

* This function runs within the user calling thread

* Before pushing a custom encoded video frame, you must call [setVideoSourceType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideosourcetype) to switch the video input source to the custom encoded video source.

### setVideoDecoderConfig:withVideoDecoderConfig:

```objectivec
- (int)setVideoDecoderConfig:(NSString* _Nonnull)streamId
       withVideoDecoderConfig:(ByteRTCVideoDecoderConfig)config NS_SWIFT_NAME(setVideoDecoderConfig(_:withVideoDecoderConfig:));
```

Before subscribing to the remote video stream, set the remote video data decoding method

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|config |ByteRTCVideoDecoderConfig |Video decoding method. See [ByteRTCVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoDecoderConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* When you want to custom decode a remote stream, you need to call [registerRemoteEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-registerremoteencodedvideoframeobserver) Register the remote video stream monitor, and then call the interface to set the decoding method to custom decoding. The monitored video data is called back through [onRemoteEncodedVideoFrame:info:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe-info-withencodedvideoframe).

* Since version 3.56, for automatic subscription, you can set `streamId` to a specific value (if there is corresponding logic). In this case, the decoding settings set by calling the API apply to all remote main streams or screen sharing streams based on the relevant logic of `streamId`.

### requestRemoteVideoKeyFrame:

```objectivec
- (int)requestRemoteVideoKeyFrame:(NSString* _Nonnull)streamId;
```

After subscribing to the remote video stream, request the keyframe

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* This method is only suitable for manual subscription mode and is used after successful subscription to the remote stream.

* This method is suitable for calling [setVideoDecoderConfig:withVideoDecoderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideodecoderconfig-withvideodecoderconfig) After the custom decoding function is turned on, and the custom decoding fails

### registerRemoteEncodedVideoFrameObserver:

```objectivec
- (int)registerRemoteEncodedVideoFrameObserver:(id<ByteRTCRemoteEncodedVideoFrameObserver> _Nullable)observer NS_SWIFT_NAME(registerRemoteEncodedVideoFrameObserver(_:));
```

Video data callback after registering remote encoding.

After registration, when the SDK detects a remote encoded video frame, [onRemoteEncodedVideoFrame:info:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe-info-withencodedvideoframe) callback

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |id<ByteRTCRemoteEncodedVideoFrameObserver\> |Remote encoded video data monitor. See [ByteRTCRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRemoteEncodedVideoFrameObserver) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* See [Custom Video Encoding and Decoding](https://docs.byteplus.com/byteplus-rtc/docs/82921#custom-video-decoding) for more details about custom video decoding.

* This method applies to manual subscription mode and can be called either before or after entering the Room. It is recommended to call it before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to nullptr.

### sendStreamSyncInfo:config:

```objectivec
- (int)sendStreamSyncInfo:(NSData* _Nonnull)data config:(ByteRTCStreamSyncInfoConfig* _Nonnull)config;
```

Sends audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the API is successfully called, the remote user will receive [rtcEngine:onStreamSyncInfoReceived:info:streamType:data:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onstreamsyncinforeceived-info-streamtype-data).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|data |NSData\* |Message content. |
|config |ByteRTCStreamSyncInfoConfig\* |For configuration of media stream information synchronization. See [ByteRTCStreamSyncInfoConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamSyncInfoConfig). |

**Return Value**

* \> = 0: Message sent successfully. Returns the number of successful sends.

* \-1: Message sending failed. Message length greater than 16 bytes.

* \-2: Message sending failed. The content of the incoming message is empty.

* \-3: Message sending failed. This screen stream was not published when the message was synchronized through the screen stream.

* \-4: Message sending failed. This audio stream is not yet published when you synchronize messages with an audio stream captured by a microphone or custom device, as described in the error code [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCErrorCode).

**Notes**

* Regarding the frequency, we recommend no more than 50 calls per second.

* When using `ByteRTCRoomProfileInteractivePodcast` as room profile, the data will be delivered. For other room profiles, the data may be lost when the local user is muted.

### startEchoTest:playDelay:

```objectivec
- (int)startEchoTest:(ByteRTCEchoTestConfig*_Nullable)echoConfig playDelay:(NSInteger)delayTime;
```

Starts a call test.

Before entering the room, you can call this API to test whether your local audio/video equipment as well as the upstream and downstream networks are working correctly.

Once the test starts, SDK will record your sound or video. If you receive the playback within the delay range you set, the test is considered normal.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|echoConfig |ByteRTCEchoTestConfig\* |Test configurations, see [ByteRTCEchoTestConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEchoTestConfig). |
|delayTime |NSInteger |Delayed audio/video playback time specifying how long you expect to receive the playback after starting the test. The range of the value is [2,10] in seconds and the default value is 2. |

**Return Value**

API call result:

* 0: Success

* \-2: Failure due to parameter exception.

* \-4: Failure because the user has joined a room.

* \-6: Failure for the testing is in progress.

* \-7: Failure for the request included neither video nor audio.

* \-8: Failure for the roomID is already used.

**Notes**

* Once you start the test, you can either call [stopEchoTest](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopechotest) or wait until the test stops automatically after 60s, to start the next test or enter the room.

* All APIs related to device control and stream control called before this API are invalidated during the test and are restored after the test.

* All APIs related to device control, stream control, and room entry called during the test do not take effect, and you will receive [rtcEngine:onWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onwarning) with the warning code `ByteRTCWarningCodeInEchoTestMode`.

* You will receive the test result from [rtcEngine:onEchoTestResult:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onechotestresult).

### stopEchoTest

```objectivec
- (int)stopEchoTest;
```

Stops the current call test.

After calling [startEchoTest:playDelay:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startechotest-playdelay), you must call this API to stop the test.

**Return Value**

API call result:

* 0: Success

* \-3: Failure, no test is in progress.

**Notes**

After stopping the test with this API, all the system devices and streams are restored to the state they were in before the test.

### setVideoWatermark:withRtcWatermarkConfig:

```objectivec
- (int)setVideoWatermark: (NSString* _Nullable)imagePath
   withRtcWatermarkConfig:(ByteRTCVideoWatermarkConfig* _Nonnull)rtcWatermarkConfig;
```

Adds a watermark to the designated video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|imagePath |NSString\* |The absolute path of the watermark image. The path should be less than 512 bytes.<br><br> <br><br>The watermark image should be in PNG or JPG format. |
|rtcWatermarkConfig |ByteRTCVideoWatermarkConfig\* |Watermark configurations. See [ByteRTCVideoWatermarkConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoWatermarkConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* On iOS, setting a watermark is not supported when sharing the screen.

* Call [clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-clearvideowatermark) to remove the watermark on the designated video stream.

* You can only add one watermark to one video stream. The newly added watermark replaces the previous one. You can call this API multiple times to add watermarks to different streams.

* You can call this API before and after joining room.

* If you mirror the preview, or the preview and the published stream, the watermark will also be mirrored locally, but the published watermark will not be mirrored.

* When you enable simulcast mode, the watermark will be added to all video streams, and it will scale down to smaller encoding configurations accordingly.

### clearVideoWatermark

```objectivec
- (int)clearVideoWatermark;
```

Removes video watermark from designated video stream.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### takeLocalSnapshot:

```objectivec
- (NSInteger)takeLocalSnapshot:(id<ByteRTCVideoSnapshotCallbackDelegate> _Nullable)callback;
```

Take a snapshot of the local video.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|callback |id<ByteRTCVideoSnapshotCallbackDelegate\> |See [ByteRTCVideoSnapshotCallbackDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCVideoSnapshotCallbackDelegate). |

**Return Value**

The index of the local snapshot task, starting from `1`.

**Notes**

* The snapshot is taken with all video effects on, like rotation, and mirroring.

* You can take the snapshot either using SDK internal video capture or customized capture.

### takeLocalSnapshotToFile:

```objectivec
- (NSInteger)takeLocalSnapshotToFile:(NSString* _Nonnull)filePath;
```

> Available since 3.60.

Takes a snapshot of the local video stream and saves it as a JPG file at the specified local path.

After calling this method, the SDK triggers [rtcEngine:onLocalSnapshotTakenToFile:filePath:width:height:errorCode:taskId:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onlocalsnapshottakentofile-filepath-width-height-errorcode-taskid) to report whether the snapshot is taken successfully and provide details of the snapshot.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filePath |NSString\* |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Example: `/Users/YourName/Pictures/snapshot.jpg`. |

**Return Value**

The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### takeRemoteSnapshot:callback:

```objectivec
- (NSInteger)takeRemoteSnapshot:(NSString* _Nonnull)streamId callback:(id<ByteRTCVideoSnapshotCallbackDelegate> _Nullable)callback;
```

Take a snapshot of the remote video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the remote video stream for taking snapshot. |
|callback |id<ByteRTCVideoSnapshotCallbackDelegate\> |See [ByteRTCVideoSnapshotCallbackDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCVideoSnapshotCallbackDelegate). |

**Return Value**

The index of the remote snapshot task, starting from `1`.

### takeRemoteSnapshotToFile:filePath:

```objectivec
- (NSInteger)takeRemoteSnapshotToFile:(NSString* _Nonnull)streamId filePath:(NSString* _Nonnull)filePath;
```

> Available since 3.60.

Take a snapshot of the remote video stream and save it as a JPG file at the specified local path.

After calling this method, the SDK triggers [rtcEngine:onRemoteSnapshotTakenToFile:info:filePath:width:height:errorCode:taskId:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onremotesnapshottakentofile-info-filepath-width-height-errorcode-taskid) to report whether the snapshot is taken successfully and provide details of the snapshot.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the remote video stream for taking snapshot. |
|filePath |NSString\* |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Example: `/Users/YourName/Pictures/snapshot.jpg`. |

**Return Value**

The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### startCloudProxy:

```objectivec
- (int)startCloudProxy:(NSArray <ByteRTCCloudProxyInfo*>* _Nullable)cloudProxiesInfo;
```

Starts cloud proxy

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|cloudProxiesInfo |NSArray<ByteRTCCloudProxyInfo\*\>\* |cloud proxy information list. See [ByteRTCCloudProxyInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCCloudProxyInfo). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Call this API before joining the room.

* Start pre\-call network detection after starting cloud proxy.

* After starting cloud proxy and connects the cloud proxy server successfully, receives [rtcEngine:onCloudProxyConnected:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-oncloudproxyconnected).

* To stop cloud proxy, call [stopCloudProxy](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stopcloudproxy).

### stopCloudProxy

```objectivec
- (int)stopCloudProxy;
```

Stop cloud proxy

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

To start cloud proxy, call [startCloudProxy:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startcloudproxy).

### setDummyCaptureImagePath:

```objectivec
- (int)setDummyCaptureImagePath:(NSString* _Nonnull)filePath;
```

Set an alternative image when the local internal video capture is not enabled.

When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image.

You can repeatedly call this API to update the image.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filePath |NSString\* |Set the path of the static image.<br><br> <br><br>You can use the absolute path (file://xxx). The maximum size for the path is 512 bytes.<br><br> <br><br>You can upload a .JPG, .JPEG, .PNG, or .BMP file.<br><br> <br><br>When the aspect ratio of the image is inconsistent with the video encoder configuration, the image will be proportionally resized, with the remaining pixels rendered black. The framerate and the bitrate are consistent with the video encoder configuration. |

**Return Value**

* 0: Success.

* \-2: Failure. Ensure that the filePath is valid.

* \-12: This method is not available in the Audio SDK.

**Notes**

* The API is only effective when publishing an internally captured video.

* You cannot locally preview the image.

* You can call this API before and after joining an RTC room. In the multi\-room mode, the image can be only displayed in the room you publish the stream.

* You cannot apply effects like filters and mirroring to the image, while you can watermark the image.

* The image is not effective for a screen\-sharing stream.

* When you enable the simulcast mode, the image will be added to all video streams, and it will be proportionally scaled down to smaller encoding configurations.

### getNetworkTimeInfo

```objectivec
- (ByteRTCNetworkTimeInfo*_Nonnull)getNetworkTimeInfo;
```

Obtain the synchronization network time information.

**Return Value**

See [ByteRTCNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCNetworkTimeInfo).

**Notes**

* When you call this API for the first time, you start synchronizing the network time information and receive the return value `0`. After the synchronization finishes, you will receive [rtcEngineOnNetworkTimeSynchronized:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengineonnetworktimesynchronized). After that, calling this API will get you the correct network time.

* Under chorus scenario, participants shall start audio mixing at the same network time.

### startHardwareEchoDetection:

```objectivec
- (int)startHardwareEchoDetection:(NSString* _Nonnull)testAudioFilePath;
```

Start echo detection before joining a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|testAudioFilePath |NSString\* |Absolute path of the music file for the detection. It is expected to encode with UTF\-8. The following files are supported: mp3, aac, m4a, 3gp, wav.<br><br> <br><br>We recommend to assign a music file whose duration is between 10 to 20 seconds.<br><br> <br><br>Do not pass a Silent file. |

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure due to the ongoing process of the previous detection. Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stophardwareechodetection) to stop it before calling this API again.

* \-2: Failure due to an invalid file path or file format.

**Notes**

* You can use this feature only when [ByteRTCRoomProfile](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRoomProfile) is set to `ByteRTCRoomProfileMeeting` or `ByteRTCRoomProfileMeetingRoom`.

* Before calling this API, ask the user for the permissions to access the local audio devices.

* Before calling this api, make sure the audio devices are active and keep the capture volume and the playback volume within a reasonable range.

* The detection result is passed as the argument of [rtcEngine:onHardwareEchoDetectionResult:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onhardwareechodetectionresult).

* During the detection, the SDK is not able to respond to the other testing APIs, such as [startEchoTest:playDelay:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-startechotest-playdelay).

* Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-stophardwareechodetection) to stop the detection and release the audio devices.

### stopHardwareEchoDetection

```objectivec
- (int)stopHardwareEchoDetection;
```

Stop the echo detection before joining a room.

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure.

**Notes**

* Refer to [startHardwareEchoDetection:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-starthardwareechodetection) for information on how to start an echo detection.

* We recommend calling this API to stop the detection once getting the detection result from [rtcEngine:onHardwareEchoDetectionResult:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onhardwareechodetectionresult).

* You must stop the echo detection to release the audio devices before the user joins a room. Otherwise, the detection may interfere with the call.

### setCellularEnhancement:

```objectivec
- (int)setCellularEnhancement:(ByteRTCMediaTypeEnhancementConfig* _Nonnull)config;
```

Enable cellular network assisted communication to improve call quality.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |ByteRTCMediaTypeEnhancementConfig\* |See [ByteRTCMediaTypeEnhancementConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaTypeEnhancementConfig). |

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure, internal error.

* \-2: Failure, invalid parameters.

**Notes**

The function is off by default.

### setLocalProxy:

```objectivec
- (int)setLocalProxy:(NSArray <ByteRTCLocalProxyInfo*>* _Nonnull)configurations;
```

Sets local proxy.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configurations |NSArray<ByteRTCLocalProxyInfo\*\>\* |Local proxy configurations. Refer to [ByteRTCLocalProxyInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalProxyInfo) for details.<br><br> <br><br>You can set both Http tunnel and Socks5 as your local proxies, or only set one of them based on your needs. If you set both Http tunnel and Socks5 as your local proxies, then media traffic and signaling are routed through Socks5 proxy and Http requests through Http tunnel proxy. If you set either Http tunnel or Socks5 as your local proxy, then media traffic, signaling and Http requests are all routed through the proxy you chose.<br><br> <br><br>If you want to remove the existing local proxy configurations, you can call this API with the parameter set to null. |

**Notes**

* You must call this API before joining the room.

* After calling this API, you will receive [rtcEngine:onLocalProxyStateChanged:withProxyState:withProxyError:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onlocalproxystatechanged-withproxystate-withproxyerror) callback that informs you of the states of local proxy connection.

### setLocalVideoSink:withPixelFormat:

```objectivec
- (int)setLocalVideoSink:(id<ByteRTCVideoSinkDelegate> _Nullable)videoSink
         withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setLocalVideoSink(withSink:withPixelFormat:))
         __deprecated_msg("Will be removed in new version");
```

> Deprecated since 3.57, use [setLocalVideoSink:withLocalRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvideosink-withlocalrenderconfig) instead.

Binds the local video stream to a custom renderer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoSink |id<ByteRTCVideoSinkDelegate\> |Custom video renderer. See [ByteRTCVideoSinkDelegate](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkDelegate). |
|requiredFormat |ByteRTCVideoSinkPixelFormat |Video frame encoding format that applies to custom rendering. See [ByteRTCVideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkPixelFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* If you need to unbind the video stream from the custom render, you must set videoSink to `null`. The binding status will be cleared when you leave room.

* You should call this API before joining the room, and after receiving [rtcEngine:onFirstLocalVideoFrameCaptured:withFrameInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onfirstlocalvideoframecaptured-withframeinfo) which reports that the first local video frame has been successfully captured.

* This method gets video frames that have undergone preprocessing. If you need to obtain video frames from other positions, such as after capture, you should call [setLocalVideoSink:withLocalRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalvideosink-withlocalrenderconfig) instead.

### setRemoteVideoSink:withSink:withPixelFormat:

```objectivec
- (int)setRemoteVideoSink:(NSString* _Nonnull)streamId
                 withSink:(id<ByteRTCVideoSinkDelegate> _Nullable)videoSink
          withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setRemoteVideoSink(_:withSink:withPixelFormat:))
         __deprecated_msg("Will be removed in new version");
```

> Deprecated since 3.57, use [setRemoteVideoSink:withSink:withRemoteRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremotevideosink-withsink-withremoterenderconfig) instead.

Binds the remote video stream to a custom renderer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|videoSink |id<ByteRTCVideoSinkDelegate\> |Custom video renderer. See [ByteRTCVideoSinkDelegate](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkDelegate). |
|requiredFormat |ByteRTCVideoSinkPixelFormat |Encoding format that applies to the custom renderer. See [ByteRTCVideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkPixelFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* This API can be called before and after entering the room. To call before entering the room, you need to get the remote stream information before joining the room; if you cannot get the remote stream information in advance, you can call the API after joining the room and getting the remote stream information through [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish).

* If you need to unbind the remote stream from the renderer, you must set videoSink to null.

* This method gets video frames that have undergone preprocessing.

### updateRemoteStreamVideoCanvas:withRenderMode:withBackgroundColor:

```objectivec
- (int)updateRemoteStreamVideoCanvas:(NSString* _Nonnull)streamId
                      withRenderMode:(ByteRTCRenderMode)renderMode
                 withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRenderMode:withBackgroundColor:));
```

> Deprecated since 3.56, and will be deleted in 3.62. Use [updateRemoteStreamVideoCanvas:withRemoteVideoRenderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-updateremotestreamvideocanvas-withremotevideorenderconfig) instead.

Modifies remote video frame rendering settings, including render mode and background color.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of Remote stream. |
|renderMode |ByteRTCRenderMode |See [ByteRTCRenderMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRenderMode). |
|backgroundColor |NSUInteger |See [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoCanvas).backgroundColor. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

Calling this API during remote video rendering will be effective immediately.

# ByteRTCWTNStream

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCWTNStream :NSObject
```

[onWTNAudioSubscribeStateChanged:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnaudiosubscribestatechanged-state-reason) callback.

WTN stream process

## Member Functions

|Return |Name |
|---|---|
|int |[subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-subscribewtnvideostream-subscribe) |
|int |[subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-subscribewtnaudiostream-subscribe) |
|int |[setWTNRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremotevideocanvas-withcanvas) |
|int |[setWTNRemoteVideoSink:withSink:withConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremotevideosink-withsink-withconfig) |
|int |[setWTNRemoteAudioPlaybackVolume:volume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremoteaudioplaybackvolume-volume) |
|void |[setWTNStreamDelegate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnstreamdelegate) |

## Instructions

### subscribeWTNVideoStream:subscribe:

```objectivec
- (int)subscribeWTNVideoStream:(NSString* _Nonnull)streamId subscribe:(bool)subscribe;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream:` and `stopPlayPublicStream:` methods for subscribing to and unsubscribing from WTN video streams. If you are using these methods, please migrate to this interface.

Subscribe/ unsubscribe WTN video stream

A user can call this method to subscribe or unsubscribe to a WTN stream whether he/she has joined the room or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |bool |Whether to subscribe to the WTN stream.<br><br><br> <br><br>* true: Subscribe<br><br>* false: Unsubscribe |

**Return Value**

* 0: Success. You will also be informed by [onWTNAudioSubscribeStateChanged:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnaudiosubscribestatechanged-state-reason).

* !0: Failure because of invalid parameter or empty parameters.

**Notes**

A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-subscribewtnvideostream-subscribe)/[subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-subscribewtnaudiostream-subscribe) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend you bind a view for the WTN stream before calling this API.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremotevideocanvas-withcanvas).

   \- Custom renderer: By calling [setWTNRemoteVideoSink:withSink:withConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremotevideosink-withsink-withconfig).

* After calling this API, the local user will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteVideoFrameDecoded:withFrameInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnfirstremotevideoframedecoded-withframeinfo).

* If the WTN stream contains SEI information, the local user will be informed by [onWTNSEIMessageReceived:andChannelId:andMessage:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnseimessagereceived-andchannelid-andmessage).

### subscribeWTNAudioStream:subscribe:

```objectivec
- (int)subscribeWTNAudioStream:(NSString* _Nonnull)streamId subscribe:(bool)subscribe;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream:` and `stopPlayPublicStream:` methods for subscribing to and unsubscribing from WTN audio streams. If you are using these methods, please migrate to this interface.

Subscribes to/unsubscribes from the specified WTN audio stream.

A user can call this method to subscribe to a WTN stream whether he/she has joined the room or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |bool |Whether to subscribe to the WTN stream.<br><br><br> <br><br>* true: Subscribe<br><br>* false: Unsubscribe |

**Return Value**

* 0: Success. You will also be informed by [onWTNVideoSubscribeStateChanged:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnvideosubscribestatechanged-state-reason).

* !0: Failure because of invalid parameter or empty parameters.

**Notes**

* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-subscribewtnvideostream-subscribe)/[subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-subscribewtnaudiostream-subscribe) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe to a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremotevideocanvas-withcanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink:withSink:withConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCWTNStream-setwtnremotevideosink-withsink-withconfig)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnfirstremoteaudioframe).

* If the WTN stream contains SEI information, you will be informed by [onWTNSEIMessageReceived:andChannelId:andMessage:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate-onwtnseimessagereceived-andchannelid-andmessage).

### setWTNRemoteVideoCanvas:withCanvas:

```objectivec
- (int)setWTNRemoteVideoCanvas:(NSString*_Nonnull)streamId
                    withCanvas:(ByteRTCVideoCanvas* _Nullable)canvas NS_SWIFT_NAME(setWTNRemoteVideoCanvas(_:withCanvas:));
```

> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamVideoCanvas:withCanvas:` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.

Assign an internal render view to the WTN stream

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |
|canvas |ByteRTCVideoCanvas\* |Internal render view. Set to be a blank view if you want to unbind. Refer to [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoCanvas) for more details. |

**Return Value**

* 0: Success

* !0: Failure

### setWTNRemoteVideoSink:withSink:withConfig:

```objectivec
- (int)setWTNRemoteVideoSink:(NSString*_Nonnull)streamId
                    withSink:(id<ByteRTCVideoSinkDelegate> _Nullable)videoSink
                  withConfig:(ByteRTCRemoteVideoSinkConfig*)config   NS_SWIFT_NAME(setWTNRemoteVideoSink(_:withSink:withConfig:));
```

> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamVideoSink:withSink:withPixelFormat:` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.

Assign a custom renderer to the WTN stream. See [Custom Video Rendering](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |
|videoSink |id<ByteRTCVideoSinkDelegate\> |Custom renderer. Set to be `null` when you want to release the renderer. Refer to [ByteRTCVideoSinkDelegate](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSinkDelegate) for more details. |
|config |ByteRTCRemoteVideoSinkConfig\* |Remote video frame callback configuration. Refer to [ByteRTCRemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoSinkConfig) for more details. |

**Return Value**

* 0: Success

* !0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

### setWTNRemoteAudioPlaybackVolume:volume:

```objectivec
- (int)setWTNRemoteAudioPlaybackVolume:(NSString*_Nonnull)streamId volume:(NSInteger)volume;
```

> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamAudioPlaybackVolume:volume:` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.

Set the audio playback volume of the WTN stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream. |
|volume |NSInteger |Ratio(%) of the audio playback volume to the original volume, in the range `[0, 400]`, with overflow protection. The default volume is 100.<br><br> <br><br>To ensure the audio quality, the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* \-2: Wrong parameter.

### setWTNStreamDelegate:

```objectivec
- (void)setWTNStreamDelegate:(_Nullable id<ByteRTCWTNStreamDelegate>)delegate;
```

> Available since 3.60.

Set the WTN event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|delegate |id<ByteRTCWTNStreamDelegate\> |See [ByteRTCWTNStreamDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCWTNStreamDelegate). |

# ByteRTCRoomLiveMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRoomLiveMode
)
```

## Enumerated Value

|Type |Value |Instructions |
|---|---|---|
|ByteRTCRoomLiveModeCoHost |1 |Co\-hosted live streaming. Focus on quality, the default video bitrate is higher. |
|ByteRTCRoomLiveModeSoloHost |2 |Single host live streaming. |

# ByteRTCAudioSource

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioSource : NSObject
```

# ByteRTCVideoEffect

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoEffect : NSObject
```

Advanced video effects. See [integration guide](https://docs.byteplus.com/byteplus-rtc/docs/114717).

## Member Functions

|Return |Name |
|---|---|
|int |[getAuthMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-getauthmessage) |
|int |[initCVResource:withAlgoModelDir:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-initcvresource-withalgomodeldir) |
|int |[enableVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevideoeffect) |
|int |[disableVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-disablevideoeffect) |
|int |[setEffectNodes:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-seteffectnodes) |
|int |[updateEffectNode:key:value:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-updateeffectnode-key-value) |
|int |[setColorFilter:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-setcolorfilter) |
|int |[setColorFilterIntensity:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-setcolorfilterintensity) |
|int |[enableVirtualBackground:withSource:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevirtualbackground-withsource) |
|int |[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-disablevirtualbackground) |
|int |[enableFaceDetection:withInterval:withModelPath:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablefacedetection-withinterval-withmodelpath) |
|int |[disableFaceDetection](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-disablefacedetection) |

## Instructions

### getAuthMessage:

```objectivec
- (int)getAuthMessage:(NSString*_Nullable*_Nullable)ppmsg;
```

Get authorization messages from the Effect SDK for the online license.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|ppmsg |NSString\* \* |Authorization message string address |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table) for specific instructions.

**Notes**

* You must get an online license for the Effect SDK before using the CV functions.

* After getting authorization messages with this API, implement the code of getting the online license with [Online License Guide](https://docs.byteplus.com/en/effects/docs/windows-license-guide). Then call [initCVResource:withAlgoModelDir:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-initcvresource-withalgomodeldir) to validate the license. After that, you can use the CV function.

### initCVResource:withAlgoModelDir:

```objectivec
- (int) initCVResource:(NSString* _Nonnull)licenseFile
            withAlgoModelDir: (NSString* _Nonnull)algoModelDir;
```

Checks video effect license, sets the video effect resource model path, and initializes video effect.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|licenseFile |NSString\* |The absolute path of the license file for authorization. |
|algoModelDir |NSString\* |The absolute path of the Effects SDK's models file. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

When validating the license, the difference of the timestamp of the CV server and the timestamp of the client is checked. You must not change the time of the client.

### enableVideoEffect

```objectivec
- (int) enableVideoEffect;
```

Enables video effects including beauty and color filters.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

* You must call [initCVResource:withAlgoModelDir:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-initcvresource-withalgomodeldir) before calling this API.

* This API does not enable video effects directly, you must call [setEffectNodes:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-seteffectnodes) or [setColorFilter:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-setcolorfilter) next.

* Call [disableVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-disablevideoeffect) to turn off video effects.

### disableVideoEffect

```objectivec
- (int) disableVideoEffect;
```

Disables video effects.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

Call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevideoeffect) to enable video effects.

### setEffectNodes:

```objectivec
- (int) setEffectNodes:(NSArray<NSString*>*_Nonnull)effectNodes;
```

Sets the video effects material package.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectNodes |NSArray<NSString\*\>\* |Array of effect material package paths.<br><br> <br><br>To remove the current video effect, set it to null. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

You must call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevideoeffect) before calling this API.

### updateEffectNode:key:value:

```objectivec
- (int) updateEffectNode:(NSString* _Nonnull)node
                     key:(NSString* _Nonnull)key value:(float) value;
```

Sets the intensity of video effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|node |NSString\* |The absolute path of the effects resource package, see [Resource Package Structure](https://docs.byteplus.com/effects/docs/resource-package-structure-v421-and-later). |
|key |NSString\* |The name of the material key to be set, see [Functions of Resource Keys](https://docs.byteplus.com/effects/docs/functions-of-resource-keys-v421-and-later) for the value. |
|value |float |The intensity value that needs to be set, the value range [0,1], and the setting is invalid when it exceeds the range. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### setColorFilter:

```objectivec
- (int) setColorFilter:(NSString* _Nonnull)filterRes;
```

Sets the color filter.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filterRes |NSString\* |Filter effects package absolute path. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

Call [setColorFilterIntensity:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-setcolorfilterintensity) to set the intensity of the color filter enabled. Set the intensity to 0 to turn off color filter.

### setColorFilterIntensity:

```objectivec
- (int) setColorFilterIntensity:(float) intensity;
```

Sets the intensity of the color filter enabled.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|intensity |float |Filter intensity. The value range [0,1] is set to be invalid when the range is exceeded.<br><br> <br><br>Set the intensity to 0 to turn off color filter. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### enableVirtualBackground:withSource:

```objectivec
- (int) enableVirtualBackground:(NSString* _Nonnull)backgroundStickerPath
                     withSource:(ByteRTCVirtualBackgroundSource* _Nonnull)source;
```

Sets the original background to a specified image or a solid color.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|backgroundStickerPath |NSString\* |The absolute path of virtual background effects. |
|source |ByteRTCVirtualBackgroundSource\* |Virtual background source. See [ByteRTCVirtualBackgroundSource](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVirtualBackgroundSource). |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

* You must call [initCVResource:withAlgoModelDir:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-initcvresource-withalgomodeldir) before calling this API.

* Call [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-disablevirtualbackground) to turn off the virtual background.

### disableVirtualBackground

```objectivec
- (int) disableVirtualBackground;
```

Turns off the virtual background.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

After calling [enableVirtualBackground:withSource:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCVideoEffect-enablevirtualbackground-withsource) to enable the virtual background function, you can call this API to turn it off.

### enableFaceDetection:withInterval:withModelPath:

```objectivec
- (int) enableFaceDetection:(_Nullable id<ByteRTCFaceDetectionObserver>) observer
               withInterval:(NSUInteger)interval
              withModelPath:(NSString* _Nonnull)path;
```

Starts face detection and registers the observer for the result.

With this observer, you will receive [onFaceDetectResult:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCFaceDetectionObserver-onfacedetectresult) periodically.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |id<ByteRTCFaceDetectionObserver\> |See [ByteRTCFaceDetectionObserver](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCFaceDetectionObserver). |
|interval |NSUInteger |The minimum time interval between two callbacks in milliseconds. The value should be greater than 0. The actual time interval is between interval and interval+the time slot of a captured video frame. |
|path |NSString\* |The absolute path of the face detection algorithm file. Typically it is the tt_face_vXXX.model file in the ttfacemodel folder. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* \-1004: Initializing. This function will be available when the initialization is completed.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### disableFaceDetection

```objectivec
- (int) disableFaceDetection;
```

Stops face detection.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

# ByteRTCRoom

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRoom : ByteRTCRTSRoom
```

## Member Property

|Type |Name |
|---|---|
|id<ByteRTCRoomDelegate\> |[delegate](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-delegate) |

## Member Functions

|Return |Name |
|---|---|
|void |[destroy](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-destroy) |
|NSString\* |[getRoomId](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-getroomid) |
|int |[setRTCRoomDelegate:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setrtcroomdelegate) |
|int |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) |
|int |[setUserVisibility:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setuservisibility) |
|int |[setMultiDeviceAVSync:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setmultideviceavsync) |
|int |[leaveRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-leaveroom) |
|int |[publishStreamVideo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamvideo) |
|int |[publishStreamAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamaudio) |
|int |[subscribeStreamVideo:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribestreamvideo-subscribe) |
|int |[subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribestreamaudio-subscribe) |
|int |[subscribeAllStreamsVideo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribeallstreamsvideo) |
|int |[subscribeAllStreamsAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribeallstreamsaudio) |
|int |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-pauseallsubscribedstreamvideo) |
|int |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-pauseallsubscribedstreamaudio) |
|int |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeallsubscribedstreamvideo) |
|int |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeallsubscribedstreamaudio) |
|NSInteger |[sendRoomMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-sendroommessage) |
|NSInteger |[sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-sendroombinarymessage) |
|int |[startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms) |
|int |[updateForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-updateforwardstreamtorooms) |
|int |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-stopforwardstreamtorooms) |
|int |[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-pauseforwardstreamtoallrooms) |
|int |[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeforwardstreamtoallrooms) |
|ByteRTCRangeAudio |[getRangeAudio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-getrangeaudio) |
|ByteRTCSpatialAudio |[getSpatialAudio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-getspatialaudio) |
|int |[setRemoteRoomAudioPlaybackVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setremoteroomaudioplaybackvolume) |
|int |[setAudioSelectionConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setaudioselectionconfig) |
|NSInteger |[setRoomExtraInfo:value:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setroomextrainfo-value) |
|NSInteger |[setStreamExtraInfo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setstreamextrainfo) |
|int |[setRemoteSimulcastStreamType:streamType:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setremotesimulcaststreamtype-streamtype) |
|int |[setRemoteVideoConfig:remoteVideoConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setremotevideoconfig-remotevideoconfig) |
|NSString\* |[getCallId](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-getcallid) |
|int |[setLiveMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setlivemode) |

## Instructions

### delegate

```objectivec
@property(nonatomic, weak) id<ByteRTCRoomDelegate> _Nullable delegate;
```

## Instructions

### destroy

```objectivec
- (void)destroy;
```

Leave and destroy the room instance created by calling [createRTCRoom:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcroom).

### getRoomId

```objectivec
- (NSString*_Nonnull)getRoomId;
```

Get room ID.

**Return Value**

Room ID.

### setRTCRoomDelegate:

```objectivec
- (int)setRTCRoomDelegate:(id<ByteRTCRoomDelegate> _Nullable)roomDelegate;
```

Listens for event callbacks related to the [ByteRTCRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom) instance by setting the event handler of this instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomDelegate |id<ByteRTCRoomDelegate\> |Refer to [ByteRTCRoomDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

### joinRoom:userInfo:userVisibility:roomConfig:

```objectivec
- (int)joinRoom:(NSString*_Nullable)token userInfo:(ByteRTCUserInfo*_Nonnull)userInfo userVisibility:(BOOL)userVisibility roomConfig:(ByteRTCRoomConfig*_Nonnull)roomConfig NS_SWIFT_NAME(joinRoom(_:userInfo:userVisibility:roomConfig:));
```

Join the RTC room.

After creating a room by calling [createRTCRoom:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room.

> Users (including backend bots) who successfully join the RTC room will start billing. If the room only has 1 user, the audio billing time will be calculated. See [Audio Billing](https://docs.byteplus.com/en/docs/12/docs-69871) for more details.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |NSString\* |Dynamic key. It is used for authentication and verification of users entering the room.<br><br> <br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br> <br><br>Apps with different AppIDs are not interoperable.<br><br> <br><br>Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause joining the room to fail. |
|userInfo |ByteRTCUserInfo\* |User information. See [ByteRTCUserInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserInfo). |
|userVisibility |BOOL |User visibility. We recommend setting the user visibility to `false` when entering the room, and then setting it to `true` via [setUserVisibility:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setuservisibility) when the user needs to send audio & video streams. Joining fails when the number of users in an RTC room reaches the upper limit. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Capability of Users and Streams](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|roomConfig |ByteRTCRoomConfig\* |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to the flow. See [ByteRTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRoomConfig) for the specific configuration mode. |

**Return Value**

Method call result.

* 0: Success.

   * Local users receive notifications of the room state via [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).

   * Local users receive notifications of the local\-stream state via [rtcRoom:onVideoPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason), [rtcRoom:onAudioPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason).

   * Local users receive notifications of the published\-stream state via [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish).

   * If the local user is also a visible user, the other participants receive [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined) callback.

* \-1: Invalid parameter

* \-2: Already in the room. After the API call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-leaveroom) is not called successfully, this return value will be triggered when the room entry API is called again, regardless of whether the filled room ID and user ID are duplicated.

   The reason for the failure will be communicated via the [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) callback.

**Notes**

* In the same room with the same AppID, the user ID of each user must be unique. If two users have the same user ID, the user who joined the room later will kick the user who joined the room first out of the room, and the user who joined the room first will receive [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) callback notification, the error type is duplicate login ByteRTCErrorCodeDuplicateLogin.

* Local users will receive [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) callback notification after calling this method to join the room successfully. If the local user is also a visible user, the remote user will receive an [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined) callback notification when joining the room.

* By default, the user is visible in an RTC room. Joining fails when the number of users in an RTC room reaches its upper limit. To avoid this, call [setUserVisibility:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setuservisibility) to change the visibility of the audience users to `false` by considering the capacity for the invisible users is much larger than that for visible users. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Capability of Users and Streams](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this time [rtcEngine:onConnectionStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After successful reconnection, you will receive a callback notification from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) locally.

### setUserVisibility:

```objectivec
- (int)setUserVisibility:(BOOL)enable;
```

Set the visibility of the user in the room. The local user is visible to others by default before calling this API.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Visibility of the user in the room.<br><br><br> <br><br>* YES: The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* NO: The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

   You will receive [rtcRoom:onUserVisibilityChanged:errorCode:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuservisibilitychanged-errorcode) after calling this API. (Available since v3.54)

* If you call this API before joining room, and the set value is different from the default value, you will receive the callback when you join the room.

* If you call this API after joining room, and the current visibility is different from the previous value, you will receive the callback.

* When reconnecting after losing internet connection, if the visibility changes, you will receive the callback.

**Notes**

* You can call this API whether the user is in a room or not.

   * When you call this API while you are in the room, the other users in the room will be informed via the following callback.

      • When you switch from `false` to `true`, they will receive [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined).

• When you switch from `true` to `false`, they will receive [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason).

• The invisible user will receive the warning code, `ByteRTCWarningCodeSubscribeStreamForbiden`, when trying to publish media streams.

### setMultiDeviceAVSync:

```objectivec
- (int)setMultiDeviceAVSync:(NSString* _Nullable) audioUserId;
```

Synchronizes published audio and video.

When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioUserId |NSString\* |The ID of audio publisher. You can stop the current A/V synchronization by setting this parameter to null. |

**Return Value**

* 0: Success. When the A/V synchronization state changes, you will receive [rtcRoom:onAVSyncStateChange:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onavsyncstatechange).

* < 0 : Fail. Learn more details via [rtcRoom:onAVSyncEvent:userId:eventCode:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onavsyncevent-userid-eventcode). More than one pair of audio and video can be synchronized simultaneously in the same RTC room, but you should note that one single audio source cannot be synchronized with multiple video sources at the same time.

**Notes**

* You can call this API anytime before or after entering the room.

* The source user IDs of the audio and video stream to be synchronized must be in the same RTC room.

* If you want to change the audio source, call this API again with a new `audioUserId`. If you want to change the video source, you need to stop the current synchronization first, then call this API on the new video publisher side.

### leaveRoom

```objectivec
- (int)leaveRoom NS_SWIFT_NAME(leaveRoom());
```

Leaves the RTC room.

The user calls this method to leave the room, end the call process, and release all call\-related resources.

**Return Value**

* 0: Success. If the user is a host:

   * The other participants receive [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason) callback.

   * The publishing streams stop and the other participants receive notifications of the stream states via [rtcRoom:onVideoPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason), [rtcRoom:onAudioPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason).

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* After the user leaves the room, the local will receive a callback for [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo);

* Call [setUserVisibility:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setuservisibility) method sets itself to be visible. After the user leaves the room, other users in the room will receive [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason) callback notification.

### publishStreamVideo:

```objectivec
- (int)publishStreamVideo:(BOOL)publish;
```

> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the following functions. If you have upgraded to version 3.60 or above and are still using these two methods, please migrate to this interface.

Publishes or stops publishing video streams.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|publish |BOOL |Whether to publish the video stream.<br><br><br> <br><br>* true: Publish.<br><br>* false: Stop publishing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig).

* An invisible user cannot publish media streams. Call [setUserVisibility:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamaudio) to start or stop publishing the audio stream captured by the microphone.

* Call [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish). Those who successfully received your streams will receive [rtcEngine:onFirstRemoteVideoFrameDecoded:info:withFrameInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onfirstremotevideoframedecoded-info-withframeinfo) at the same time.

### publishStreamAudio:

```objectivec
- (int)publishStreamAudio:(BOOL)publish;
```

> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the following functions. If you have upgraded to version 3.60 or above and are still using these two methods, please migrate to this interface.

Publishes or stops publishing media streams captured by the local microphone in the current room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|publish |BOOL |Whether to publish the media stream.<br><br><br> <br><br>* true: Publish.<br><br>* false: Stop publishing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig).

* An invisible user cannot publish media streams. Call [setUserVisibility:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamVideo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-publishstreamvideo) to start or stop publishing the video stream captured by the camera.

* Call [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish). Those who successfully received your streams will receive [rtcEngine:onFirstRemoteAudioFrame:info:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onfirstremoteaudioframe-info) at the same time.

### subscribeStreamVideo:subscribe:

```objectivec
- (int)subscribeStreamVideo:(NSString*_Nonnull)streamId subscribe:(BOOL)subscribe;
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeStream:mediaStreamType:` and `unsubscribeStream:mediaStreamType:` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from specific remote video streams captured by the local camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |The ID of the target remote video stream. |
|subscribe |BOOL |Whether to subscribe to the video stream.<br><br><br> <br><br>* true: Subscribe.<br><br>* false: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

* Calling this API updates the subscribe configuration when the user has subscribed to the remote user either by calling this API or by auto\-subscribe.

* You must first get the remote stream information through [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish) before calling this API to subscribe to streams accordingly.

* After calling this API, you will be informed of the calling result with [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling this method to cancel.

* Any other exceptions will be included in [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason), see [ByteRTCSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSubscribeStateChangeReason) for the reasons.

### subscribeStreamAudio:subscribe:

```objectivec
- (int)subscribeStreamAudio:(NSString*_Nonnull)streamId subscribe:(BOOL)subscribe;
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeStream:mediaStreamType:` and `unsubscribeStream:mediaStreamType:` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from specific remote audio streams captured by the local microphone.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |The ID of the target remote audio stream. |
|subscribe |BOOL |Whether to subscribe to the audio stream.<br><br><br> <br><br>* true: Subscribe.<br><br>* false: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for specific reasons.

**Notes**

* Calling this API updates the subscribe configuration when the user has subscribed to the remote user either by calling this API or by auto\-subscribe.

* You must first get the remote stream information through [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish) before calling this API to subscribe to streams accordingly.

* After calling this API, you will be informed of the calling result with [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribestreamaudio-subscribe).

* Any other exceptions will be included in [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).

### subscribeAllStreamsVideo:

```objectivec
- (int)subscribeAllStreamsVideo:(BOOL)subscribe;
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from all remote video streams captured by camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|subscribe |BOOL |Whether to subscribe to the video stream.<br><br><br> <br><br>* true: Subscribe.<br><br>* false: Unsubscribe. |

**Return Value**

API call result:

* 0: Success

* !0: Failure

**Notes**

* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* In the Audio selection, if the number of media streams exceeds the limit, we recommend you call [subscribeAllStreamsVideo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribeallstreamsvideo) to subscribe each target media stream other than calling this API.

* After calling this API, you will be informed of the calling result with [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeAllStreamsVideo:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribeallstreamsvideo).

* Any other exceptions will be included in [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo), see [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCErrorCode) for the reasons.

### subscribeAllStreamsAudio:

```objectivec
- (int)subscribeAllStreamsAudio:(BOOL)subscribe;
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from all remote audio streams (captured by microphone).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|subscribe |BOOL |Whether to subscribe to all remote audio streams.<br><br><br> <br><br>* true: Subscribe.<br><br>* false: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* In the Audio selection, if the number of media streams exceeds the limit, we recommend you call [subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribestreamaudio-subscribe) to subscribe each target media stream other than calling this API.

* After calling this API, you will be informed of the calling result with [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-subscribestreamaudio-subscribe).

* Any other exceptions will be included in [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo), see [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCErrorCode) for the reasons.

### pauseAllSubscribedStreamVideo

```objectivec
- (int)pauseAllSubscribedStreamVideo;
```

> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Pauses receiving all remote video streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Calling this API does not change the capture and transmission state of the remote stream.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume receiving streams, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

### pauseAllSubscribedStreamAudio

```objectivec
- (int)pauseAllSubscribedStreamAudio;
```

> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Pauses receiving all remote audio streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Calling this API does not change the capture and transmission state of the remote stream.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume receiving streams, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

### resumeAllSubscribedStreamVideo

```objectivec
- (int)resumeAllSubscribedStreamVideo;
```

> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Resumes receiving all remote video streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Calling this API does not change the capture and transmission state of the remote stream.

* Calling this API does not change any subscription configuration.

### resumeAllSubscribedStreamAudio

```objectivec
- (int)resumeAllSubscribedStreamAudio;
```

> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Resumes receiving all remote audio streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

* Calling this API does not change the capture and transmission state of the remote stream.

* Calling this API does not change any subscription configuration.

### sendRoomMessage:

```objectivec
- (NSInteger)sendRoomMessage:(NSString*_Nonnull)message NS_SWIFT_NAME(sendRoomMessage(_:));
```

Sends text messages to all other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |NSString\* |The content of the text message sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending an in\-room text message, you must call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to join the room.

* After calling this function, you will receive an [rtcRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroommessagesendresult-error) callback to notify the sender of the success or failure of the message;

* If the text message is sent successfully, all remote users in the room will receive [rtcRoom:onRoomMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroommessagereceived-message) callback.

### sendRoomBinaryMessage:

```objectivec
- (NSInteger)sendRoomBinaryMessage:(NSData*  _Nonnull)message NS_SWIFT_NAME(sendRoomBinaryMessage(_:));
```

Sends binary messages to all other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |NSData\* |The binary broadcast message sent by the user. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before broadcasting binary messages in the room, you must call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to join the room.

* After calling this function, you will receive an [rtcRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroommessagesendresult-error) callback to notify the sender of the success or failure of the message;

* If the binary message is successfully sent, all users in the room will receive [rtcRoom:onRoomBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroombinarymessagereceived-message) callback.

### startForwardStreamToRooms:

```objectivec
- (int)startForwardStreamToRooms:(NSArray <ByteRTCForwardStreamConfiguration*>* _Nullable)configurations NS_SWIFT_NAME(startForwardStreamToRooms(_:));
```

Starts relaying media stream across rooms.

After calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig), call this API to achieve the relaying of media streams to multiple rooms, which applies to cross\-room concatenation and other scenarios.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configurations |NSArray<ByteRTCForwardStreamConfiguration\*\>\* |Information of the rooms where you want to relay the media stream to. Refer to [ByteRTCForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCForwardStreamConfiguration) for more information. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Calling this method will trigger [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged).

* After calling this method, listen the events from each room during the relaying by registering [rtcRoom:onForwardStreamEvent:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamevent).

* Once the relaying begins, the other users in the room will receive callback of [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined), [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish).

* Call [updateForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-updateforwardstreamtorooms) to add or remove the designated room(s) after calling this method.

* Call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-stopforwardstreamtorooms) to stop relaying to all rooms after calling this method.

* Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-pauseforwardstreamtoallrooms) to pause relaying to all rooms after calling this method.

### updateForwardStreamToRooms:

```objectivec
- (int)updateForwardStreamToRooms:(NSArray <ByteRTCForwardStreamConfiguration*>* _Nullable)configurations NS_SWIFT_NAME(updateForwardStreamToRooms(_:));
```

Updates information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms).

Adding and removing rooms by calling this method will trigger [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged) on the local.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configurations |NSArray<ByteRTCForwardStreamConfiguration\*\>\* |Information of the rooms where you want to relay the media stream to. Refer to [ByteRTCForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCForwardStreamConfiguration) for more information. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

Users in the room which is added or removed from the target list by calling this method will receive [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined), [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish).

### stopForwardStreamToRooms

```objectivec
- (int)stopForwardStreamToRooms;
```

Stops relaying media stream to all rooms after calling [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms).

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

* Calling this method will trigger [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged).

* The other users in the room will receive callback of [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined) and [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined) when you stop relaying.

* To stop relaying media stream to specific rooms, call [updateForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-updateforwardstreamtorooms) instead.

* To pause the relaying for a short time, call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-pauseforwardstreamtoallrooms), and then call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeforwardstreamtoallrooms) to resume after that.

### pauseForwardStreamToAllRooms

```objectivec
- (int)pauseForwardStreamToAllRooms;
```

Pauses relaying media stream to all rooms after calling [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-startforwardstreamtorooms).

After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-resumeforwardstreamtoallrooms) to resume.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

The other users in the room will receive callback of [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish) when you pause relaying.

### resumeForwardStreamToAllRooms

```objectivec
- (int)resumeForwardStreamToAllRooms;
```

Resumes relaying media streams paused by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-pauseforwardstreamtoallrooms) to all rooms.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details.

**Notes**

The other users in the room will receive callback of [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined) and [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined) when you resume relaying.

### getRangeAudio

```objectivec
- (ByteRTCRangeAudio*_Nullable)getRangeAudio;
```

Gets range audio instance.

**Return Value**

API call result:

* ByteRTCRangeAudio: Success. You will get a [ByteRTCRangeAudio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio) returned from the SDK.

* NULL: Failure. The current SDK does not offer range audio function.

**Notes**

The first time this API is called must be between creating a room and actually entering the room. Refer to [Range Voice](https://docs.byteplus.com/byteplus-rtc/docs/114727) for more information.

### getSpatialAudio

```objectivec
- (ByteRTCSpatialAudio*_Nullable)getSpatialAudio;
```

Gets spatial audio instance.

**Return Value**

API call result:

* ISpatialAudio: Success. You will get a [ByteRTCSpatialAudio](https://docs.byteplus.com/en/docs/12/14172#ByteRTCSpatialAudio) returned from the SDK.

* NULL: Failure. The current SDK does not offer spatial audio function.

**Notes**

* The first time this API is called must be between you create a room and you actually enter the room. Refer to [Spatial Audio](https://docs.byteplus.com/byteplus-rtc/docs/93903) for more information.

* Only using real dual\-channel playback device can users actually enjoy spatial audio effect.

* Low\-end device may have audio stalling issues due to its poor performance, so it is not recommended to enable spatial audio function on such kind of devices.

* SDK currently supports up to 30 users publishing audio with spatial audio enabled at the same time in the same room.

### setRemoteRoomAudioPlaybackVolume:

```objectivec
- (int)setRemoteRoomAudioPlaybackVolume:(NSInteger)volume;
```

Adjusts the audio playback volume from all the remote users in a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |NSInteger |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: mute<br><br>* 100: original volume. Default value.<br><br>* 400: Up to 4 times the original volume (with overflow protection) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ByteRTCReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReturnStatus) for more details

**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted,

* If you use both this method and [setRemoteAudioPlaybackVolume:volume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setremoteaudioplaybackvolume-volume), the volume that the local user hears from user A is the volume set by the method called later.

* If you use both this method and [setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

### setAudioSelectionConfig:

```objectivec
- (int)setAudioSelectionConfig:(ByteRTCAudioSelectionPriority)audioSelectionPriority;
```

> Available since 3.52.

Set the priority of the local audio stream to be published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioSelectionPriority |ByteRTCAudioSelectionPriority |The priority of the local audio stream which defaults to be subscribable only up to the result of the Audio Selection. Refer to [ByteRTCAudioSelectionPriority](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioSelectionPriority). |

**Notes**

* You must enable Audio Selection in the RTC console before using this API. You can call this API whether the user has joined a room. Refer to [Audio Selection](https://docs.byteplus.com/byteplus-rtc/docs/113547).

* The setting is independent in each room that the user joins.

### setRoomExtraInfo:value:

```objectivec
- (NSInteger)setRoomExtraInfo:(NSString*_Nonnull)key value:(NSString*_Nonnull)value;
```

> Available since 3.52.

Sets extra information about the room the local user joins.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|key |NSString\* |Key of the extra information, less than 10 bytes in length.<br><br> <br><br>A maximum of 5 keys can exist in the same room, beyond which the first key will be replaced. |
|value |NSString\* |Content of the extra information, less than 128 bytes in length. |

**Return Value**

API call result:

* 0: Success with a taskId returned.

* <0: Failure. See [ByteRTCSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSetRoomExtraInfoResult) for the reasons.

**Notes**

* Call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) first before you call this API to set extra information.

* After calling this API, you will receive [rtcRoom:onSetRoomExtraInfoResult:result:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onsetroomextrainforesult-result) callback informing you the result of the setting.

* After the extra information is successfully set, other users in the same room will receive the information through [rtcRoom:onRoomExtraInfoUpdate:value:lastUpdateUserId:lastUpdateTimeMs:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomextrainfoupdate-value-lastupdateuserid-lastupdatetimems) callback.

* Users who join the room later will be notified of all extra information in the room set prior to entering.

### setStreamExtraInfo:

```objectivec
- (NSInteger)setStreamExtraInfo:(NSString*_Nonnull)extra_info;
```

Sets extra information about the stream the local user publishes.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|extra_info |NSString\* |Extra information of the stream. The length does not exceed 1024 bytes. |

**Return Value**

* 0: Success.

* < 0: Failure.

**Notes**

* You can use this function to set extra information about the stream the local user publishes. Stream extra information is an additional information attached to the stream ID. Unlike the stream ID, the stream extra information can be modified during the publishing of the corresponding stream ID. Developers can use the stream extra information to synchronize the content of the stream ID with the corresponding stream ID.

* You can call this API before or after you call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig).

* Other users in the same room will receive the notification through [rtcRoom:onRoomStreamExtraInfoUpdate:info:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstreamextrainfoupdate-info-extrainfo).

### setRemoteSimulcastStreamType:streamType:

```objectivec
- (int)setRemoteSimulcastStreamType:(NSString* _Nonnull) streamId streamType:(ByteRTCVideoSimulcastStreamType)streamType;
```

> Available since 3.60.

Sets the type of the remote video stream to subscribe to.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the remote video stream you expect to subscribe to. |
|streamType |ByteRTCVideoSimulcastStreamType |Video stream type, see [ByteRTCVideoSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoSimulcastStreamType). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure.

**Notes**

* This API only works after the publisher calls [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setvideoencoderconfig) to enable publishing multiple\-quality video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps.

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

* This API only affects camera video streams published by remote users.

### setRemoteVideoConfig:remoteVideoConfig:

```objectivec
- (int)setRemoteVideoConfig:(NSString* _Nonnull) streamId remoteVideoConfig:(ByteRTCRemoteVideoConfig*_Nonnull) remoteVideoConfig;
```

Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the remote video stream you want to configure subscription parameters for. |
|remoteVideoConfig |ByteRTCRemoteVideoConfig\* |Parameters you want to configure for the remote video stream, see [ByteRTCRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoConfig). |

**Return Value**

API call result:

* 0: Success.

* !0: Failure.

**Notes**

* This API only works after the publisher calls [setLocalSimulcastMode:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCEngine-setlocalsimulcastmode) to enable publishing multiple video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps..

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

* You should call this API in the room.

* The SDK will automatically select the stream to be published or subscribed to based on the settings of both sides. See for details.

### getCallId

```objectivec
- (NSString* _Nonnull)getCallId;
```

> Available since 3.60.

Gets the call ID.

Call this method after joining a room. After creating a room, a call ID is generated to identify the call for this room.

**Return Value**

Call ID.

### setLiveMode:

```objectivec
- (int)setLiveMode:(ByteRTCRoomLiveMode)mode;
```

> Available since 3.60.

Sets live mode of this room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |ByteRTCRoomLiveMode |Live mode, see [ByteRTCRoomLiveMode](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRoomLiveMode). |

**Return Value**

* 0: Success.

* <0: Failure.

# ByteRTCRangeAudio

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRangeAudio :NSObject
```

Range audio instance

## Member Functions

|Return |Name |
|---|---|
|void |[enableRangeAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-enablerangeaudio) |
|int |[updateReceiveRange:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-updatereceiverange) |
|int |[updatePosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-updateposition) |
|int |[setAttenuationModel:coefficient:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-setattenuationmodel-coefficient) |
|void |[setNoAttenuationFlags:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-setnoattenuationflags) |

## Instructions

### enableRangeAudio:

```objectivec
- (void)enableRangeAudio:(BOOL)enable;
```

Enables/disables the range audio function.

Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [updateReceiveRange:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-updatereceiverange) to set audio receiving range.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable audio range function:<br><br><br> <br><br>* YES: Enable<br><br>* NO: Disable (Default setting) |

**Notes**

You can call this API anytime before or after entering a room. To ensure a smooth switch to the range audio mode after entering the room, you need to call [updatePosition:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-updateposition) before this API to set your own position coordinates, and then enable the range audio function.

### updateReceiveRange:

```objectivec
- (int)updateReceiveRange:(ByteRTCReceiveRange* _Nonnull) range;
```

Updates the audio receiving range for the local user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|range |ByteRTCReceiveRange\* |Audio receiving range, see [ByteRTCReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCReceiveRange). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

### updatePosition:

```objectivec
- (int)updatePosition:(ByteRTCPosition* _Nonnull) pos;
```

Updates the coordinate of the local user's position in the rectangular coordinate system in the current room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pos |ByteRTCPosition\* |3D coordinate values, the default value is [0, 0, 0], see [ByteRTCPosition](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPosition). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

**Notes**

After calling this API, you should call [enableRangeAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-enablerangeaudio) to enable range audio function to actually enjoy the range audio effect.

### setAttenuationModel:coefficient:

```objectivec
- (int)setAttenuationModel:(ByteRTCAttenuationType) type coefficient:(float)coefficient;
```

Set the volume attenuation mode of the range audio.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ByteRTCAttenuationType |Volume roll\-off mode. It is linear roll\-off mode by default. Refer to [ByteRTCAttenuationType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAttenuationType) for more details. |
|coefficient |float |Coefficient for the exponential roll\-off mode. The default value is 1. It ranges [0.1,100]. We recommended to set it to `50`. The volume roll\-off speed gets faster as this value increases. |

**Return Value**

Result of the call

* `0`: Success

* `-1`: Failure because of calling this API before the user has joined a room or before enabling the Range Audio feature by calling [enableRangeAudio:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-enablerangeaudio).

**Notes**

Call [updateReceiveRange:](https://docs.byteplus.com/en/docs/12/14172#ByteRTCRangeAudio-updatereceiverange) to set the range outside which the volume of the sound does not attenuate.

### setNoAttenuationFlags:

```objectivec
- (void) setNoAttenuationFlags:(NSArray <NSString*>*_Nonnull)flags;
```

Set the flags to mark the user groups, within which the users talk without attenuation.

In the RTC room, if the flags of the users intersect with each other, the users talk without attenuation.

For example, the user is a member of multiple teams, and teammates of the same team talk without attenuation. You can set the flag for each team, and include the flags of the user's teams in the user's flags.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|flags |NSArray<NSString\*\>\* |Array of flags. |
