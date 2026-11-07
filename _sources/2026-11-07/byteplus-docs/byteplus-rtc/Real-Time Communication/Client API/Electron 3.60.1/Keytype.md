---
title: "Keytype"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85535"
---

## AudioEffectPlayerConfig

* **Type**: `interface`

* **Description**: Mixing configuration.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |type |[AudioMixingType](https://docs.byteplus.com/en/docs/12/14199#audiomixingtype) |Mixing playback types. |
   |play_count |number |Mix playback times<br><br><br>* Play_count < = 0: Infinite loop<br><br>* Play_count == 1: Play once (default)<br><br>* Play_count \> 1: Play play_count times. |
   |pitch |number |Pitch shift relative to the original audio, in semitones. The range is `[-12, 12]`, and the default value is `0`. Positive values raise the pitch and negative values lower it. |
   |start_pos |number |The starting position in ms. 0 by default. |

## AudioMixingType

* **Type**: `enum`

* **Description**: Mixing type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioMixingTypePlayout |`0` |Play at the local device only. |
   |kAudioMixingTypePublish |`1` |Send to the remote devices only. |
   |kAudioMixingTypePlayoutAndPublish |`2` |Play and send to remote. |

## EventType

* **Type**

   ```ts
   {
     Type: string;
     Object: { [key: string]: any };
   }
   ```

## MediaPlayerConfig

* **Type**: `interface`

* **Description**: Mixing configuration.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |play_count |number |Mix playback times<br><br><br>* Play_count < = 0: Infinite loop<br><br>* Play_count == 1: Play once (default)<br><br>* Play_count \> 1: Play play_count times. |
   |start_pos |number |The starting position in ms. 0 by default. |
   |callback_on_progress_interval |string |Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) during audio mixing in ms.<br><br><br>* interval \> 0: The callback is enabled. The actual interval is always a multiple of 10. If the provided value is not divisible by 10, it will automatically be rounded up using a ceiling function. For example, if 52 is provided, the actual interval will be 60ms.<br><br>* interval <= 0: The callback is disabled. |
   |sync_progress_to_record_frame |boolean |Attach the process information of local audio file mixing to the captured audio data. Enable the function to enhance the synchronicity of the remote audio mixing.<br><br>**Notes**:<br><br><br>* The function is effective when mixing a single audio file.<br><br>* Use `true` for enabling the function and `false` for disabling the function. The default is `false`. |
   |auto_play |boolean |Play the audio automatically. If not, call [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to play the file. |
   |type |[AudioMixingType](https://docs.byteplus.com/en/docs/12/14199#audiomixingtype) |For mixing playback types. |

## AudioMixingDualMonoMode

* **Type**: `enum`

* **Description**: Mix playback channel type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioMixingDualMonoModeAuto |`0` |Consistent with audio files. |
   |kAudioMixingDualMonoModeL |`1` |Only the left channel audio in the audio file can be heard. |
   |kAudioMixingDualMonoModeR |`2` |Only the right channel audio in the audio file can be heard. |
   |kAudioMixingDualMonoModeMix |`3` |Can hear the left and right audio channels in the audio file at the same time. |

## MediaPlayerCustomSource

* **Type**: `interface`

* **Description**: Custom audio source.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |mode |[MediaPlayerCustomSourceMode](https://docs.byteplus.com/en/docs/12/14199#mediaplayercustomsourcemode) |Source mode. |
   |type |[MediaPlayerCustomSourceStreamType](https://docs.byteplus.com/en/docs/12/14199#mediaplayercustomsourcestreamtype) |Source stream type. |

## MediaPlayerCustomSourceMode

* **Type**: `enum`

* **Description**: Custom audio source mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMediaPlayerCustomSourceModePush |`0` |Use this option to push local PCM data. |
   |kMediaPlayerCustomSourceModePull |`1` |Use this option to pull audio data from memory. |

## MediaPlayerCustomSourceStreamType

* **Type**: `enum`

* **Description**: Custom audio stream type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMediaPlayerCustomSourceStreamTypeRaw |`0` |Raw PCM audio data. |
   |kMediaPlayerCustomSourceStreamTypeEncoded |`1` |Encoded audio data. |

## ExternalAudioFrame

* **Type**: `interface`

* **Description**: External audio frame.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |frame_type |[AudioFrameType](https://docs.byteplus.com/en/docs/12/14199#audioframetype) |Value: `0`<br><br>Audio frame type. Only PCM is supported. |
   |sample_rate |[AudioSampleRate](https://docs.byteplus.com/en/docs/12/14199#audiosamplerate) |Audio sample rate in Hz. |
   |channel |[AudioChannel](https://docs.byteplus.com/en/docs/12/14199#audiochannel) |Number of audio channels. For stereo audio, samples are interleaved in LRLRLR order. |
   |timestamp_ms |number \| undefined |Timestamp of the audio frame in milliseconds. |
   |data |Uint8Array |PCM audio frame data. Only 10 ms frames are supported.<br><br>Example: at 48 kHz, mono, and 16\-bit depth, the frame size is 48000 \* 0.01 s \* 1 \* 16 bits = 7680 bits = 960 bytes. |

## AudioSampleRate

* **Type**: `enum`

* **Description**: Audio sample rate in Hz.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioSampleRateAuto |`-1` |Default value. 48000 Hz. |
   |kAudioSampleRate8000 |`8000` |8000 Hz. |
   |kAudioSampleRate16000 |`16000` |16000 Hz. |
   |kAudioSampleRate32000 |`32000` |32000 Hz. |
   |kAudioSampleRate44100 |`44100` |44100 Hz. |
   |kAudioSampleRate48000 |`48000` |48000 Hz. |

## AudioChannel

* **Type**: `enum`

* **Description**: Audio channel.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioChannelAuto |`-1` |Default value. |
   |kAudioChannelMono |`1` |Mono channel. |
   |kAudioChannelStereo |`2` |Dual channels. |

## RoomLiveMode

* **Type**: `enum`

* **Description**: Live\-streaming mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRoomLiveModeCoHost |`1` |Co\-hosting or multi\-host live\-streaming mode. |
   |kRoomLiveModeSoloHost |`2` |Solo\-host live\-streaming mode. |

## UserInfo

User info.

* **Type**

   ```ts
   {
     uid: string;
     extra_info?: string;
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |uid |string |User ID. The string matches the regular expression: `[a-zA-Z0-9_@\-\.]{1,128}`. You must set or manage the uid yourself and ensure that each uid within the same room is unique. |
   |extra_info |string \| undefined |Additional information of the user. The maximum length is 200 bytes. The remote user will receive the info in [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined). |

## RTCRoomConfig

* **Type**: `interface`

* **Description**: Configuration for the room. Room is a abstract concept for an RTC call. Users can interact with each other in the same room.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_profile_type |[RoomProfileType](https://docs.byteplus.com/en/docs/12/14199#roomprofiletype) \| undefined |Room profile. The default is the standard audio and video call mode. The setting cannot be changed after joining the room. |
   |live_mode |[RoomLiveMode](https://docs.byteplus.com/en/docs/12/14199#roomlivemode) \| undefined |Live\-streaming mode. The default value is `kRoomLiveModeCoHost`.<br><br>**Notes**:<br><br>This setting takes effect only when `room_profile_type` is `kRoomProfileTypeLive`. You can call [setLiveMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setlivemode) after joining the room to update it. |
   |is_auto_publish_audio |boolean \| undefined |Whether to publish audio streams automatically. The default is automatic publishing.<br><br><br>* Changing the user role to audience via [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) will void this setting.<br><br>* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only. |
   |is_auto_publish_video |boolean \| undefined |Whether to publish video streams automatically. The default is automatic publishing.<br><br><br>* Changing the user role to audience via [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) will void this setting.<br><br>* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only. |
   |is_auto_subscribe_audio |boolean \| undefined |Whether to automatically subscribe to audio streams. The default is automatic subscription. |
   |is_auto_subscribe_video |boolean \| undefined |Whether to automatically subscribe to video streams. The default is automatic subscription. |
   |stream_id |string \| undefined |The stream ID for the published stream. |

## RoomProfileType

* **Type**: `enum`

* **Description**: Room profile

   Choose an appropriate room\-profile option to meet the requirement of the scenario for media encoding algorithm, video profiles, and network configurations.

   Call [setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioprofile) to apply another audio quality option.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRoomProfileTypeCommunication |`0` |General mode by default<br><br>It equals to `kRoomProfileTypeMeeting = 16`.<br><br>Contact us to alter the default settings. |
   |kRoomProfileTypeGame |`2` |Game voice mode. Low consumption of computing resources and network data<br><br>Additional performance optimizations have been made for low\-end devices:<br><br><br>* Encodes frame length 40/60 for some low\-end models.<br><br>* Disables software 3A audio processing for some low\-end models.<br><br><br>Enhance iOS Compatibility with other screen recordings to avoid audio recordings being interrupted by RTC. |
   |kRoomProfileTypeCloudGame |`3` |Cloud game mode.<br><br>Use this mode for game App requiring low latency.<br><br>During poor network connection, communication experiences get worse with this mode. |
   |kRoomProfileTypeLowLatency |`4` |Cloud render mode featuring extra\-low latency.<br><br>Choose this mode if it is not a game App yet requires low latency.<br><br>In this mode, latency will significantly decrease at the cost of lower audio quality as well as the bad performance with weak network signal. |
   |kRoomProfileTypeChat |`5` |For 1 vs 1 video and audio calls. |
   |kRoomProfileTypeChatRoom |`6` |For video and audio chat rooms of 3 or more people. |
   |kRoomProfileTypeLwTogether |`7` |For scenarios such as "Watch together." and "Listen together." Multiple clients are capable of playing the same videos and audios synchronously.<br><br>In these scenarios, RTC does not involve the transportation of the sharing media but only synchronizes video/music playback across multiple clients via signaling. |
   |kRoomProfileTypeGameHD |`8` |For the game apps demanding high\-resolution audio. In this mode, RTC plays audio using the media mode only. |
   |kRoomProfileTypeCoHost |`9` |For the events of co\-hosting in the live\-streaming<br><br>During a livestreaming using a CDN network, the host can invite another host to join the co\-hosting event using RTC. |
   |kRoomProfileTypeInteractivePodcast |`10` |For interactive podcasts that the host can have video and audio interactions with the audience. The voice mode is set to communication mode to avoid volume spiking and dipping acutely. |
   |kRoomProfileTypeKTV |`11` |For the online karaoke with high\-quality audio and low latency<br><br>In these scenarios, RTC transports the accompaniment and mixed audio, such as solo and non\-realtime chorus. |
   |kRoomProfileTypeChorus |`12` |For the online\-chorusing scenarios requiring high\-quality audio and low latency. Contact our technical specialists before you apply it to your App. |
   |kRoomProfileTypeVRChat |`13` |For VR chat with support for 192 KHz audio sample rate and feature of 360 Reality Audio. It is available since V3.45. |
   |kRoomProfileTypeGameStreaming |`14` |For scenarios of streaming live videos to only one client on the LAN. It can be applied to devices on the Internet or LAN. |
   |kRoomProfileTypeLanLiveStreaming |`15` |For scenarios of streaming live videos to multiple clients within the LAN with the support of 60fps. |
   |kRoomProfileTypeMeeting |`16` |For meeting Apps installed on personal devices. |
   |kRoomProfileTypeMeetingRoom |`17` |For meeting Apps installed on terminals of meeting rooms, such as Rooms. |
   |kRoomProfileTypeClassroom |`18` |For the online classrooms and lectures that over 10 participants in the room are allowed to join the video chat. |
   |kRoomProfileTypeCall |`19` |Call mode with a relatively low default bitrate, prioritizing smooth communication. |
   |kRoomProfileTypeLive |`20` |Live\-streaming mode with a relatively high default bitrate, prioritizing video quality. |

## RemoteVideoConfig

* **Type**: `interface`

* **Description**: Information on remote video frame.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |framerate |number \| undefined |Expected maximum frame rate of the subscribed stream in fps. The default value is 0, which represents full\-frame\-rate; values greater than 0 take effect.<br><br>The frame rate that the subscriber will receive at depends on the lower one between the sender and the subscriber settings.<br><br>Only valid if the stream is coded with SVC technique. |
   |resolution_width |number \| undefined |Width of the video frame in px. |
   |resolution_height |number \| undefined |Height of the video frame in px. |

## MessageConfig

* **Type**: `enum`

* **Description**: RTM message.

* **Notes**

   Used as the `config` parameter of [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendusermessageoutsideroom), [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-senduserbinarymessageoutsideroom), [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendusermessage), and [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage).

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMessageConfigReliableOrdered |`0` |Low latency reliable and orderly message. |
   |kMessageConfigUnreliableOrdered |`1` |Ultra\-low latency ordered message. |
   |kMessageConfigUnreliableUnordered |`2` |Ultra\-low latency unordered message. |

## ForwardStreamConfiguration

* **Type**: `interface`

* **Description**: Information of the rooms where you want to relay the media stream to.

* **Notes**

   Used as the `configuration` parameter of [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms) and [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms).

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |forward_stream_dests |[ForwardStreamInfo](https://docs.byteplus.com/en/docs/12/14199#forwardstreaminfo)[] |Information of the rooms where you want to relay the media stream to. |

## ForwardStreamInfo

* **Type**: `interface`

* **Description**: Information of the rooms where you want to relay the media stream to.

* **Notes**

   Used as the element type of the `forward_stream_dests` field in [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-85535#forwardstreamconfiguration).

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |token |string |RoomId and UserId are required to generate the Token to forward media streams to the room.<br><br>During developing and testing, you can use temporary tokens generated on the console. At the production stage, Tokens are generated by the token generating application deployed on your server.<br><br>Forwarding will fail if the token is invalid. |
   |room_id |string |ID of the room where the media stream aims to relay to. |

## ReceiveRange

The range where local user can hear audio with attenuation effect.

* **Notes**

   Used as the `range` parameter of [updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatereceiverange).

* **Type**

   ```ts
   {
     max: number;
     min: number;
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |max |number |The maximum distance at which the local user can hear audio from remote users.<br><br>The value must be greater than 0 and greater than or equal to `min`.<br><br>Audio attenuates when the distance between the listener and sound source is in the range `[min, max)`. Audio beyond this distance cannot be heard. |
   |min |number |The minimum distance at which the local user can hear attenuated audio from remote users.<br><br>The value must be greater than or equal to 0 and less than or equal to `max`.<br><br>Audio does not attenuate at distances below this value. |

## Position

Coordinate value of the local user's position in the rectangular coordinate system in the RTC room.

* **Type**

   ```ts
   {
     x: number;
     y: number;
     z: number;
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |x |number |X\-coordinate. |
   |y |number |Y\-coordinate. |
   |z |number |Z\-coordinate. |

## AttenuationType

* **Type**: `enum`

* **Description**: Volume Roll\-off modes that a sound has in an audio source.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAttenuationTypeNone |`0` |Disable Volume Attenuation. |
   |kAttenuationTypeLinear |`1` |Linear roll\-off mode which lowers the volume of the sound over the distance. |
   |kAttenuationTypeExponential |`2` |Exponential roll\-off mode which exponentially decreases the volume of the sound with the distance raising. |

## AudioSelectionPriority

* **Type**: `enum`

* **Description**: User priority in the audio selection.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioSelectionPriorityNormal |`0` |Normal. Whether the stream can be subscribed is determined by the result of audio selection. |
   |kAudioSelectionPriorityHigh |`1` |High priority with which the stream can skip the audio selection and always be subscribable. |

## PositionInfo

* **Type**: `interface`

* **Description**: Information on the user's position in the rectangular coordinate system for the spatial audio.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |position |[Position](https://docs.byteplus.com/en/docs/12/14199#position) |3D coordinate values of the user's position in the rectangular coordinate system for the spatial audio. You need to build your own rectangular coordinate system. |
   |orientation |[HumanOrientation](https://docs.byteplus.com/en/docs/12/14199#humanorientation) |Information on the three\-dimensional orientation of the user in the rectangular coordinate system for the spatial audio. Any two of the 3D coordinate vectors of the user's position need to be perpendicular to each other. |

## HumanOrientation

* **Type**: `interface`

* **Description**: Three\-dimensional orientation information, each pair of vectors need to be perpendicular.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |forward |[Orientation](https://docs.byteplus.com/en/docs/12/14199#orientation) |Forward orientation, the default value is {1,0,0}, i.e., the forward orientation is in the positive direction of x\-axis. |
   |right |[Orientation](https://docs.byteplus.com/en/docs/12/14199#orientation) |Rightward orientation, the default value is {0,1,0}, i.e., the rightward orientation is in the positive direction of y\-axis. |
   |up |[Orientation](https://docs.byteplus.com/en/docs/12/14199#orientation) |Upward orientation, the default value is {0,0,1}, i.e., the upward orientation is in the positive direction of z\-axis. |

## Orientation

* **Type**: `interface`

* **Description**: Orientation.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |x |number |The angle the vector makes with the x\-axis. |
   |y |number |The angle the vector makes with the y\-axis. |
   |z |number |The angle the vector makes with the z\-axis. |

## EngineConfig

* **Type**: `interface`

* **Description**: Engine configuration.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |app_id |string |App ID of the RTC application. |
   |parameters |string |JSON string containing private engine parameters. Pass an empty string when no parameter is required. |

## ProblemFeedbackOption

* **Type**: `enum`

* **Description**: Audio & video quality feedback problem.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kProblemFeedbackOptionNone |`0` |No problem. |
   |kProblemFeedbackOptionOtherMessage |`1` |Other issues. |
   |kProblemFeedbackOptionDisconnected |`2` |Connection failed. |
   |kProblemFeedbackOptionEarBackDelay |`3` |High latency for the ear monitor. |
   |kProblemFeedbackOptionLocalNoise |`11` |Noise on the local end. |
   |kProblemFeedbackOptionLocalAudioLagging |`12` |Audio stall on the local end. |
   |kProblemFeedbackOptionLocalNoAudio |`13` |No sound on the local end. |
   |kProblemFeedbackOptionLocalAudioStrength |`14` |Too little/loud sound on the local end. |
   |kProblemFeedbackOptionLocalEcho |`15` |Echo noise on the local end. |
   |kProblemFeedbackOptionLocalVideoFuzzy |`25` |Unclear video on the local end. |
   |kProblemFeedbackOptionLocalNotSync |`26` |Audio and video are out of sync on the local end. |
   |kProblemFeedbackOptionLocalVideoLagging |`27` |Video stall on the local end. |
   |kProblemFeedbackOptionLocalNoVideo |`28` |No picture on the local end. |
   |kProblemFeedbackOptionRemoteNoise |`38` |Noise on the remote end. |
   |kProblemFeedbackOptionRemoteAudioLagging |`39` |Audio stutters on the remote end. |
   |kProblemFeedbackOptionRemoteNoAudio |`40` |No sound on the remote end. |
   |kProblemFeedbackOptionRemoteAudioStrength |`41` |Too little/loud sound on the remote end. |
   |kProblemFeedbackOptionRemoteEcho |`42` |Echo noise on the remote end. |
   |kProblemFeedbackOptionRemoteVideoFuzzy |`52` |Unclear video on the remote end. |
   |kProblemFeedbackOptionRemoteNotSync |`53` |Audio & video out of sync on the remote end. |
   |kProblemFeedbackOptionRemoteVideoLagging |`54` |Video stall on the remote end. |
   |kProblemFeedbackOptionRemoteNoVideo |`55` |No picture on the remote end. |

## ProblemFeedbackInfo

* **Type**: `interface`

* **Description**: Information for audio & video quality feedback.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |problem_desc |string |Specific description of problems other than the preset problem. |
   |room_info |[ProblemFeedbackRoomInfo](https://docs.byteplus.com/en/docs/12/14199#problemfeedbackroominfo)[] |Room information for audio & video quality feedback. |

## ProblemFeedbackRoomInfo

* **Type**: `interface`

* **Description**: Room information for audio & video quality feedback.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_id |string |Room ID. |
   |user_id |string |The ID of the local user. |

## RTCPluginInfo

* **Type**: `interface`

* **Description**: Information required to register a plugin.

* **Notes**

   Pass this object to [registerPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-registerplugin). After registration succeeds, call [getPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getplugin) with the same plugin ID to obtain the corresponding [RTCPlugin](https://docs.byteplus.com/en/docs/12/docs-85535#rtcplugin) instance.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |id |string |Plugin ID, the unique identifier of the plugin. |
   |path |string |Plugin library path. |

## RTCPlugin

* **Type**: `interface`

* **Description**: Control interface for a registered plugin.

* **Notes**

   Returned by [getPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getplugin) after [registerPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-registerplugin) succeeds. `setEnabled` and `setParameter` are members of this interface.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |id |string |Plugin ID, the unique identifier of the plugin. |
   |setEnabled |`(enabled: boolean) => number` |Enables or disables the plugin. Returns `0` on success and `-1` on failure. |
   |setParameter |`(json_string: string) => number` |Sets plugin parameters. Returns `0` on success and `-1` on failure. |

## VoiceChangerType

* **Type**: `enum`

* **Description**: Voice changer effect type. Contact technical support for more effect types.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVoiceChangerTypeOriginal |`0` |Original voice without effects. |
   |kVoiceChangerTypeGiant |`1` |Giant. |
   |kVoiceChangerTypeChipmunk |`2` |Chipmunk. |
   |kVoiceChangerTypeMinionst |`3` |Minions. |
   |kVoiceChangerTypeVibrato |`4` |Vibrato. |
   |kVoiceChangerTypeRobot |`5` |Robot. |

## VoiceReverbType

* **Type**: `enum`

* **Description**: Voice reverb effect type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVoiceReverbTypeOriginal |`0` |Original voice without effects. |
   |kVoiceReverbTypeEcho |`1` |Echo. |
   |kVoiceReverbTypeConcert |`2` |Concert. |
   |kVoiceReverbTypeEthereal |`3` |Ethereal. |
   |kVoiceReverbTypeKTV |`4` |Karaoke. |
   |kVoiceReverbTypeStudio |`5` |Recording studio. |
   |kVoiceReverbTypeVirtualStereo |`6` |Virtual stereo. |
   |kVoiceReverbTypeSpacious |`7` |Spacious. |
   |kVoiceReverbType3D |`8` |3D voice. |

## EchoTestConfig

* **Type**: `interface`

* **Description**: Video/audio call test configurations.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |audio_properties_report_interval |number |Volume prompt interval in ms, the default value is 100.<br><br><br>* `<= 0`: Turn off prompt<br><br>* `(0,100]` Invalid interval value, and will be automatically reset to 100ms.<br><br>* `> 100`: the actual value of interval. |
   |uid |string |User ID for testing. |
   |room_id |string |ID of the room that the tested user will join. |
   |token |string |Token used for authenticating users when they enter the room. |
   |enable_audio |boolean |Whether to test audio. The system default audio device is used.<br><br><br>* true:<br><br>* With internal capture, the microphone starts automatically. When `audio_properties_report_interval` is greater than 0, use [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalaudiopropertiesreport) to check the microphone status.<br><br>* With custom capture, call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalaudioframe) to push captured audio to the SDK.<br><br>* false: Do not test audio. |
   |enable_video |boolean |Whether to test video. On desktop platforms, the first video device in the list is used by default.<br><br><br>* true:<br><br>* With internal capture, the camera starts automatically.<br><br>* With custom capture, call [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalvideoframe) to push captured video to the SDK.<br><br>* false: Do not test video.<br><br><br>The fixed publishing configuration is 640 x 360 at 15 fps. |

## AudioPropertiesConfig

* **Type**: `interface`

* **Description**: Configuration for audio property prompt.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |interval |number |Prompt interval in ms<br><br><br>* `<= 0`: Turn off prompt<br><br>* `(0,100]`: Invalid interval value, and will be automatically reset to 100ms.<br><br>* `> 100`: the actual value of interval. |
   |enable_spectrum |boolean \| undefined |Whether to enable audio spectrum detection. |
   |enable_vad |boolean \| undefined |Whether to enable Voice Activity Detection. |
   |local_main_report_mode |[AudioReportMode](https://docs.byteplus.com/en/docs/12/14199#audioreportmode) \| undefined |The volume callback modes. |
   |audio_report_mode |[AudioPropertiesMode](https://docs.byteplus.com/en/docs/12/14199#audiopropertiesmode) \| undefined |Configuration of whether including locally mixed audio info in [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalaudiopropertiesreport).<br><br>Locally captured microphone audio info and locally captured screen audio info are included by default. |
   |smooth |number \| undefined |The smoothing coefficient for audio attribute information prompt. The range is `(0.0, 1.0]`.<br><br>The default value is `1.0`, which means the smoothing effect is off by default. The smaller the value, the smoother the audio volume prompt. If you want to enable the smooth effect, the recommended value is `0.3`. |
   |enable_voice_pitch |boolean \| undefined |Whether to report the fundamental frequency of the local user's voice. |

## AudioReportMode

* **Type**: `enum`

* **Description**: The volume callback modes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioReportModeNormal |`0` |Always\-on(Default). |
   |kAudioReportModeDisconnect |`1` |After visibly joining a room and unpublishing your streams, disable the volume callback. |
   |kAudioReportModeReset |`2` |After visibly joining a room and unpublish your streams, enable the volume callback. The volume is reset to 0. |

## AudioPropertiesMode

* **Type**: `enum`

* **Description**: Configuration of whether including locally mixed audio info in the audio properties report.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioPropertiesModeMicrophone |`0` |Only locally captured microphone audio info and locally captured screen audio info are included in the audio properties report. |
   |kAudioPropertiesModeAudioMixing |`1` |Locally mixing audio info is included in the audio properties report, in addition to locally captured microphone audio info and locally captured screen audio info. |

## VideoEncoderConfig

* **Type**: `interface`

* **Description**: Video encoding configuration. Refer to [Setting Video Encoder Configuration](https://docs.byteplus.com/byteplus-rtc/docs/70122) to learn more.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |Width of the video frame in px. |
   |height |number |Height of the video frame in px. |
   |frame_rate |number |Video frame rate in fps. |
   |max_bitrate |number \| undefined |Maximum bit rate in kbps. Optional for internal capturing while mandatory for custom capturing.<br><br>The default value is \-1 in internal capturing mode, SDK will automatically calculate the applicable bit rate based on the input resolution and frame rate.<br><br>No stream will be encoded and published if you set this parameter to 0. |
   |min_bitrate |number \| undefined |Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `minBitrate`.<br><br>It defaults to `0`.<br><br>It ranges within [0, maxBitrate). When `maxBitrate` < `minBitrate`, the bitrate is self\-adapted.<br><br>In the following circumstance, the assignment to this variable has no effect:<br><br><br>* When `maxBitrate` = `0`, the video encoding is disabled.<br><br>* When `maxBitrate` < `0`, the bitrate is self\-adapted. |
   |key_frame_interval_ms |number \| undefined |Key frame interval in milliseconds. The default value is `0`. |
   |encoder_preference |[VideoEncodePreference](https://docs.byteplus.com/en/docs/12/14199#videoencodepreference) \| undefined |Encoding policy preference. The default policy is quality first. |

## VideoEncodePreference

* **Type**: `enum`

* **Description**: Encoder preference.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoEncodePreferenceDisabled |`0` |No preference. The frame rate and the resolution will not be adjusted. |
   |kVideoEncodePreferenceFramerate |`1` |(Default) Frame rate first. The resolution will not be changed. |
   |kVideoEncodePreferenceQuality |`2` |Resolution first. |
   |kVideoEncodePreferenceBalance |`3` |Balancing resolution and frame rate. |

## StreamIndex

* **Type**: `enum`

* **Description**: Reserved parameter.

## AlphaLayout

* **Type**: `enum`

* **Description**: Layout of an encoded video frame that contains an alpha channel.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAlphaLayoutTop |`0` |Place alpha data at the top. |

## MirrorType

* **Type**: `enum`

* **Description**: Mirror type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMirrorTypeNone |`0` |The preview and the published video stream are not mirrored. |
   |kMirrorTypeRender |`1` |The preview is mirrored. The published video stream is not mirrored. |
   |kMirrorTypeRenderAndEncoder |`3` |The preview and the published video stream are mirrored. |

## VideoSimulcastMode

* **Type**: `enum`

* **Description**: Simulcast mode for local video publishing.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoSimulcastModeOnlyOne |`0` |Publish only one stream. |
   |kVideoSimulcastModeOnDemand |`1` |Publish simulcast streams on demand. |
   |kVideoSimulcastModeAlwaysSimulcast |`2` |Always publish all configured simulcast streams. |

## EffectBeautyMode

* **Type**: `enum`

* **Description**: Basic beauty effect.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kEffectBeautyWhite |`0` |Brightness. |
   |kEffectBeautySmooth |`1` |Smoothness. |
   |kEffectBeautySharpen |`2` |Sharpness. |
   |kEffectBeautyModeClear |`3` |Clarity. Requires Effects SDK v4.4.2 or later. |

## VideoSourceType

* **Type**: `enum`

* **Description**: Video input source type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoSourceTypeExternal |`0` |External video source. |
   |kVideoSourceTypeInternal |`1` |Internal video source. |

## ExternalVideoFrame

* **Type**: `interface`

* **Description**: External video frame.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |pixel_fmt |[VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14199#videopixelformat) |Pixel format of the video frame. |
   |data |[(Uint8Array \| undefined)?, (Uint8Array \| undefined)?, (Uint8Array \| undefined)?] |Video frame plane data.<br><br>For I420: data[0] is Y, data[1] is U, and data[2] is V.<br><br>For NV12: data[0] is Y and data[1] is UV.<br><br>For RGBA, ARGB, and BGRA: data[0] contains the packed pixel data. |
   |linesize |[(number \| undefined)?, (number \| undefined)?, (number \| undefined)?] |Stride of each video frame plane.<br><br>For I420: linesize[0] is width, and linesize[1] and linesize[2] are width/2.<br><br>For NV12: linesize[0] and linesize[1] are width.<br><br>For RGBA, ARGB, and BGRA: linesize[0] is width \* 4. |
   |extra_data |Uint8Array \| undefined |Address of the SEI data. |
   |supplementary_info |Uint8Array \| undefined |Address of supplementary data. |
   |width |number |Width of the video frame. |
   |height |number |Height of the video frame. |
   |rotation |[VideoRotation](https://docs.byteplus.com/en/docs/12/14199#videorotation) \| undefined |Rotation of the video frame.<br><br>When the receiver uses the RTC SDK's internal renderer, the engine rotates the frame before rendering.<br><br>When the receiver uses a custom renderer, this setting does not take effect. |
   |timestamp_ms |number \| undefined |Timestamp of the video frame in milliseconds. |

## VideoPixelFormat

* **Type**: `enum`

* **Description**: Video pixel format.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoPixelFormatUnknown |`0` |Unknown pixel format. |
   |kVideoPixelFormatI420 |`1` |YUV I420 format. |
   |kVideoPixelFormatNV12 |`2` |YUV NV12 format. |
   |kVideoPixelFormatNV21 |`3` |YUV NV21 format. |
   |kVideoPixelFormatRGB24 |`4` |24\-bit RGB format. |
   |kVideoPixelFormatRGBA |`5` |RGBA format. |
   |kVideoPixelFormatARGB |`6` |ARGB format. |
   |kVideoPixelFormatBGRA |`7` |BGRA format. |

## VideoRotation

* **Type**: `enum`

* **Description**: Information on video frame rotation angle.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoRotation0 |`0` |Video does not rotate. |
   |kVideoRotation90 |`90` |Video rotates 90 degrees clockwise. |
   |kVideoRotation180 |`180` |Video rotates 180 degrees clockwise. |
   |kVideoRotation270 |`270` |Video rotates 270 degrees clockwise. |

## AudioSourceType

* **Type**: `enum`

* **Description**: Audio input source type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioSourceTypeExternal |`0` |External audio source. |
   |kAudioSourceTypeInternal |`1` |Audio source captured internally by the RTC SDK. |

## PushSingleStreamParam

* **Type**: `interface`

* **Description**: Configurations to be set when pushing media streams to CDN.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_id |string |The room ID of the media stream. |
   |user_id |string |The user ID of the media stream. |
   |uri |string |the target address of the CDN. |
   |is_screen_stream |boolean |Reserved parameter. |
   |dest_info |[DestInfo](https://docs.byteplus.com/en/docs/12/14199#destinfo)[] \| undefined |forward dest room info. |
   |dest_info_size |number \| undefined |The length of `dest_info`. |
   |push_type |[SingleStreamPushType](https://docs.byteplus.com/en/docs/12/14199#singlestreampushtype) \| undefined |forward stream type, CDN OR ACROSS ROOM. |

## DestInfo

* **Type**: `interface`

* **Description**: Destination information for cross\-room stream forwarding.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_id |string |Destination room ID. |
   |user_id |string |User ID used to publish the stream in the destination room. |

## SingleStreamPushType

* **Type**: `enum`

* **Description**: Single\-stream forwarding target type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPushToCDN |`1` |Push the stream to CDN. |
   |kPushToRTC |`2` |Forward the stream to another RTC room. |

## AnsMode

* **Type**: `enum`

* **Description**: Audio noise suppression mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAnsModeDisable |`0` |Disable audio noise suppression. |
   |kAnsModeLow |`1` |Apply light noise suppression. |
   |kAnsModeMedium |`2` |Suppress moderate stationary noise, such as air conditioner or fan noise. |
   |kAnsModeHigh |`3` |Suppress loud non\-stationary noise, such as keyboard, tapping, impact, or animal sounds. |
   |kAnsModeAutomatic |`4` |Enable audio noise suppression and let the RTC SDK select the algorithm automatically. |

## StreamSyncInfoConfig

* **Type**: `interface`

* **Description**: Configuration related to media stream information synchronization.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |repeat_count |number |The number of duplicates sent by the message, the value range is [0,25], it is recommended to set it to [3,5]. |
   |stream_type |[SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/14199#syncinfostreamtype) |Value: `0`<br><br>Stream types for media stream information synchronization. |

## CloudProxyInfo

* **Type**: `interface`

* **Description**: Cloud Proxy Information.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |cloud_proxy_ip |string |Cloud proxy IP. |
   |cloud_proxy_port |number |Cloud Proxy Port. |

## ScreenCaptureSourceInfo

* **Type**: `interface`

* **Description**: Detailed information of the screen sharing object

   Parameter type of the [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |type |[ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/14199#screencapturesourcetype) |Type of the screen\-sharing object. |
   |source_id |number |ID of the screen\-sharing object. |
   |source_name |string |Name of the screen\-sharing object. |
   |application |string |The title of the application to be shared.<br><br>Only available if the sharing object is an application window. |
   |primary_monitor |boolean |Tag for the screen to be shared identifying whether it is the primary screen<br><br>Only available when the screen\-sharing object is a screen. |
   |pid |number |Process pid of the application to be shared.<br><br>Only available if the sharing object is an application windows. |
   |region_rect |[Rectangle](https://docs.byteplus.com/en/docs/12/14199#rectangle) |Coordinate of the screen\-sharing object. (0, 0), the origin is the top left on the main screen for clients with multiple screens. |

## ScreenCaptureSourceType

* **Type**: `enum`

* **Description**: Type of the screen capture object.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kScreenCaptureSourceTypeUnknown |`0` |Type unknown. |
   |kScreenCaptureSourceTypeWindow |`1` |Application window. |
   |kScreenCaptureSourceTypeScreen |`2` |Desktop. |

## Rectangle

* **Type**: `interface`

* **Description**: Coordinates of the screen\-sharing object.

   * When there are several screens, the origin (0, 0) is different for different platforms:

   * For Windows, the origin (0, 0) is the top\-left corner of the main screen.

   * For Linux, the origin (0, 0) is the top\-left corner of the rectangle that merely covers all screens.

   * The region of the window is different for different platforms:

   * For Windows and macOS, the region includes the system title bar of the window.

   * For Linux, the region does not include the system title bar of the window.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |x |number \| undefined |The x coordinate of the upper left corner of the rectangular area. |
   |y |number \| undefined |The y coordinate of the upper left corner of the rectangular area. |
   |width |number \| undefined |Rectangle width. |
   |height |number \| undefined |Rectangular height. |

## ScreenCaptureParameters

* **Type**: `interface`

* **Description**: Screen internal capture parameters.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |region_rect |[Rectangle](https://docs.byteplus.com/en/docs/12/14199#rectangle) |Collection area. |
   |capture_mouse_cursor |[MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/14199#mousecursorcapturestate) \| undefined |To collect mouse status. |
   |filter_config |number[] |Screen filtering settings. Provide ID of the windows to be excluded. |
   |highlight_config |[HighlightConfig](https://docs.byteplus.com/en/docs/12/14199#highlightconfig) |Configuration of highlighted borders. |

## MouseCursorCaptureState

* **Type**: `enum`

* **Description**: Whether to collect mouse information when collecting screen video stream internally.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMouseCursorCaptureStateOn |`0` |Collect mouse information. |
   |kMouseCursorCaptureStateOff |`1` |Do not collect mouse information. |

## HighlightConfig

* **Type**: `interface`

* **Description**: Border highlighting settings for screen sharing.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |enable_highlight |boolean \| undefined |Whether to display a highlighted border. Yes by default. |
   |border_color |number \| undefined |The color of the border in hexadecimal ARGB: 0xAARRGGBB. It defaults to 0xFF29CCA3. |
   |border_width |number \| undefined |The width of the border in pixels. It defaults to 4. |

## ThumbnailInfo

* **Type**: `interface`

* **Description**: Thumbnail of the screen\-sharing object which returns after calling [getThumbnail](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getthumbnail).

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |Width in pixel. |
   |height |number |Height in pixel. |
   |data |string |PNG string which is encoded with base64. |

## AppIconInfo

* **Type**: `interface`

* **Description**: application window preview thumbnail for screen sharing which returns after calling [getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getwindowappicon).

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |Width in pixel. |
   |height |number |Height in pixel. |
   |data |string |PNG string which is encoded with base64. |

## SEICountPerFrame

* **Type**: `enum`

* **Description**: SEI sending mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSEICountPerFrameSingle |`0` |Single\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent frame by frame in a queue. |
   |kSEICountPerFrameMulti |`1` |Multi\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent together in the next frame. |

## VideoCaptureConfig

Video capture configuration parameters.

* **Type**

   ```ts
   {
     capture_preference: CapturePreference;
     width?: number;
     height?: number;
     frame_rate?: number;
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |capture_preference |[CapturePreference](https://docs.byteplus.com/en/docs/12/14199#capturepreference) |Video capture preference. |
   |width |number \| undefined |The width of video capture resolution in px. |
   |height |number \| undefined |The height of video capture resolution in px. |
   |frame_rate |number \| undefined |Video capture frame rate in fps. |

## CapturePreference

* **Type**: `enum`

* **Description**: Video capture preference.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAuto |`0` |(Default) Video capture preference: auto<br><br>SDK determines the best video capture parameters referring to the camera output parameters and the encoder configuration. |
   |kManual |`1` |Video capture preference: manual<br><br>Set the resolution and the frame rate manually. |
   |kAutoPerformance |`2` |Video capture preference: encoder configuration<br><br>The capture parameters are the same as the parameters set in [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideoencoderconfig). |

## RecordingConfig

* **Type**: `interface`

* **Description**: Local recording parameter configuration.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |dir_path |string |The absolute path to save the recording file. You need to specify a legal path with read and write permissions. |
   |file_type |number |Recording stored file format.<br><br><br>* aac : 0<br><br>* mp4 : 1. |

## RecordingType

* **Type**: `enum`

* **Description**: Media type for local recording.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRecordingTypeAudioOnly |`0` |Record audio only. |
   |kRecordingTypeVideoOnly |`1` |Record video only. |
   |kRecordingTypeVideoAndAudio |`2` |Record both audio and video. |

## RemoteUserPriority

* **Type**: `enum`

* **Description**: Priority of the publisher. When a user encounters performance insufficiency of either the network or the device, the media stream will fall back in the ascending order of `RemoteUserPriority`.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRemoteUserPriorityLow |`0` |Low, the default. |
   |kRemoteUserPriorityMedium |`100` |Medium. |
   |kRemoteUserPriorityHigh |`200` |High. |

## VirtualBackgroundSource

* **Type**: `interface`

* **Description**: Virtual background Object.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |source_type |[VirtualBackgroundSourceType](https://docs.byteplus.com/en/docs/12/14199#virtualbackgroundsourcetype) \| undefined |Virtual background type. |
   |source_path |string |The absolute path of the specified image.<br><br><br>* You can upload a .JPG, .PNG, or .JPEG file.<br><br>* The image with a resolution higher than 1080p(Full HD) will be rescaled proportionally to fit in the video.<br><br>* If the image's aspect ratio matches the video's, the image will be rescaled proportionally to fit in the video.<br><br>* If the image’s aspect ratio doesn't match the video's, the shortest side (either height or width) of the image will be stretched proportionally to match the video. Then the image will be cropped to fill in the video.<br><br>* The transparent area in the image will be filled with white color. |
   |source_color |number \| undefined |Color used for a solid\-color virtual background. |

## VirtualBackgroundSourceType

* **Type**: `enum`

* **Description**: Virtual background type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVirtualBackgroundSourceTypeColor |`0` |Replace the original background with a solid color. |
   |kVirtualBackgroundSourceTypeImage |`1` |Replace the original background with the specified image. |

## RTCWatermarkConfig

* **Type**: `interface`

* **Description**: Watermark configurations.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |visible_in_preview |boolean \| undefined |Whether the watermark is visible in preview. Its default value is `true`. |
   |position_in_landscape_mode |[ByteWatermark](https://docs.byteplus.com/en/docs/12/14199#bytewatermark) |Watermark's coordinates and size in landscape mode. |
   |position_in_portrait_mode |[ByteWatermark](https://docs.byteplus.com/en/docs/12/14199#bytewatermark) |Watermark's coordinates and size in portrait mode. |

## ByteWatermark

* **Type**: `interface`

* **Description**: Watermark's scaled coordinates and size, relative to the video stream.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |x |number |The watermark's horizontal offset from the upper left corner of the video stream to the video stream's width in range of [0,1). |
   |y |number |The ratio of the watermark's vertical offset from the upper\-left corner to the video stream's height, in the range `[0, 1)`. |
   |width |number |The ratio of the watermark's width to the video stream's width, in the range `[0, 1)`. |
   |height |number |The ratio of the watermark's height to the video stream's height, in the range `[0, 1)`. |

## RenderOptions

* **Type**: `interface`

* **Description**: Render options.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |render_mode |[RenderMode](https://docs.byteplus.com/en/docs/12/14199#rendermode) |Scale mode when rendering. |
   |mirror |boolean |Whether to turn on mirror mode. |

## RenderMode

* **Type**: `enum`

* **Description**: Video rendering scale mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |FIT |`1` |Fit.<br><br>The video frame is scaled with fixed aspect ratio, until it fits just within the canvas. The other part of the canvas is filled with the background color. |
   |HIDDEN |`2` |Fill and Crop.<br><br>The video frame is scaled with fixed aspect ratio, until it completely fills the canvas. The region of the video exceeding the canvas will be cropped. |

## LocalVideoSinkPosition

* **Type**: `enum`

* **Description**: Local video sink position.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalVideoSinkPositionAfterCapture |`0` |Callback after capture. |
   |kLocalVideoSinkPositionAfterPreProcess |`1` |Callback after preprocessing. This is the default value. |

## RemoteVideoSinkConfig

* **Type**: `interface`

* **Description**: Remote video sink config.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |pixel_format |[PixelFormat](https://docs.byteplus.com/en/docs/12/14199#pixelformat) \| undefined |Callback pixel format. See `PixelFormat`. The default value is `kUnknown`. |
   |apply_rotation |[VideoApplyRotation](https://docs.byteplus.com/en/docs/12/14199#videoapplyrotation) \| undefined |Whether to rotate the frame automatically. See `VideoApplyRotation`. The default value is `kVideoApplyRotationDefault`. |
   |mirror_type |[VideoSinkMirrorType](https://docs.byteplus.com/en/docs/12/14199#videosinkmirrortype) \| undefined |Whether to mirror the frame. See `VideoSinkMirrorType`. The default value is `kVideoSinkMirrorTypeOFF`. |

## PixelFormat

* **Type**: `enum`

* **Description**: Video frame encoding format.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kI420 | |YUV I420 format. |
   |kRGBA | |RGBA format. |

## VideoApplyRotation

* **Type**: `enum`

* **Description**: Whether to apply rotation automatically.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoApplyRotationDefault |`-1` |Do not rotate automatically. This is the default value. |
   |kVideoApplyRotation0 |`0` |Rotate the frame to 0 degree automatically according to its rotation metadata. |

## VideoSinkMirrorType

* **Type**: `enum`

* **Description**: Whether to mirror the video sink frame.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoSinkMirrorTypeON |`1` |Enable mirroring. |
   |kVideoSinkMirrorTypeOFF |`2` |Disable mirroring. This is the default value. |

## LocalVideoSinkConfig

* **Type**: `interface`

* **Description**: Local video sink config.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |position |[LocalVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14199#localvideosinkposition) \| undefined |Callback position. See `LocalVideoSinkPosition`. The default value is `kLocalVideoSinkPositionAfterPreProcess`. |
   |pixel_format |[PixelFormat](https://docs.byteplus.com/en/docs/12/14199#pixelformat) \| undefined |Callback pixel format. See `PixelFormat`. The default value is `kUnknown`. |

## VoiceEqualizationConfig

* **Type**: `interface`

* **Description**: Voice equalization config.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |frequency |[VoiceEqualizationBandFrequency](https://docs.byteplus.com/en/docs/12/14199#voiceequalizationbandfrequency) |Frequency band. |
   |gain |number |Gain of the frequency band in dB. The range is `[-15, 15]`. |

## VoiceEqualizationBandFrequency

* **Type**: `enum`

* **Description**: Audio Equalization effect.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVoiceEqualizationBandFrequency31 |`0` |The frequency band with a center frequency of 31Hz. |
   |kVoiceEqualizationBandFrequency62 |`1` |The frequency band with a center frequency of 62Hz. |
   |kVoiceEqualizationBandFrequency125 |`2` |The frequency band with a center frequency of 125Hz. |
   |kVoiceEqualizationBandFrequency250 |`3` |The frequency band with a center frequency of 250Hz. |
   |kVoiceEqualizationBandFrequency500 |`4` |The frequency band with a center frequency of 500Hz. |
   |kVoiceEqualizationBandFrequency1k |`5` |The frequency band with a center frequency of 1kHz. |
   |kVoiceEqualizationBandFrequency2k |`6` |The frequency band with a center frequency of 2kHz. |
   |kVoiceEqualizationBandFrequency4k |`7` |The frequency band with a center frequency of 4kHz. |
   |kVoiceEqualizationBandFrequency8k |`8` |The frequency band with a center frequency of 8kHz. |
   |kVoiceEqualizationBandFrequency16k |`9` |The frequency band with a center frequency of 16kHz. |

## VoiceReverbConfig

* **Type**: `interface`

* **Description**: Voice reverb effect.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_size |number |The room size for reverb simulation. The range is `[0.0, 100.0]`. The default value is `50.0f`. The larger the room, the stronger the reverberation. |
   |decay_time |number |The decay time of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`. |
   |damping |number |The damping index of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`. |
   |wet_gain |number |The Intensity of the wet signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`. |
   |dry_gain |number |The Intensity of the dry signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`. |
   |pre_delay |number |The delay of the wet signal in ms. The range is `[0.0, 200.0]`. The default value is `0.0f`. |

## AudioRecordingConfig

* **Type**: `interface`

* **Description**: Audio recording config.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |absolute_file_name |string |Absolute path of the recorded file, file name included. The App must have the write and read permission of the path.<br><br>**Notes**:<br><br>The file format is restricted to .aac and .wav. |
   |frame_source |[AudioFrameSource](https://docs.byteplus.com/en/docs/12/14199#audioframesource) |The source of the recording.<br><br>It is kAudioFrameSourceMixed = 2, by default. |
   |sample_rate |[AudioSampleRate](https://docs.byteplus.com/en/docs/12/14199#audiosamplerate) |Audio sample rate. |
   |channel |[AudioChannel](https://docs.byteplus.com/en/docs/12/14199#audiochannel) |Number of audio channels.<br><br>**Notes**:<br><br>If number of audio channels of recording is different from that of audio capture, the behavior is:<br><br><br>* If the number of capture is 1, and the number of recording is 2, the recorded audio is two\-channel data after copying mono\-channel data.<br><br>* If the number of capture is 2, and the number of recording is 1, the recorded audio is recorded by mixing the audio of the two channels. |
   |quality |[AudioQuality](https://docs.byteplus.com/en/docs/12/14199#audioquality) |Recording quality. Only valid for .aac file.<br><br>**Notes**:<br><br>When the sample rate is 32kHz, the file (10min) size for different qualities are:<br><br><br>* low: 1.2MB;<br><br>* [Default] medium: 2MB;<br><br>* high: 3.75MB;<br><br>* ultra high: 7.5MB. |

## AudioFrameSource

* **Type**: `enum`

* **Description**: Audio file recording source type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioFrameSourceMic |`0` |The audio captured by the local microphone. |
   |kAudioFrameSourcePlayback |`1` |The audio obtained by mixing all remote users' audio. |
   |kAudioFrameSourceMixed |`2` |The audio got by mixing the local captured audio and all remote user's audio. |

## AudioQuality

* **Type**: `enum`

* **Description**: Audio quality.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioQualityLow |`0` |low quality. |
   |kAudioQualityMedium |`1` |medium quality. |
   |kAudioQualityHigh |`2` |high quality. |
   |kAudioQualityUltraHigh |`3` |ultra high quality. |

## ZoomConfigType

* **Type**: `enum`

* **Description**: Digital Zoom type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kZoomConfigTypeFocusOffset |`0` |To set the offset for zooming in and zooming out. |
   |kZoomConfigTypeMoveOffset |`1` |To set the offset for panning and tiling. |

## ZoomDirectionType

* **Type**: `enum`

* **Description**: Action of the digital zoom control.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kZoomDirectionTypeMoveLeft |`0` |Move to the left. |
   |kZoomDirectionTypeMoveRight |`1` |Move to the right. |
   |kZoomDirectionTypeMoveUp |`2` |Move upwards. |
   |kZoomDirectionTypeMoveDown |`3` |Move downwards. |
   |kZoomDirectionTypeZoomOut |`4` |Zoom out. |
   |kZoomDirectionTypeZoomIn |`5` |Zoom in. |
   |kZoomDirectionTypeReset |`6` |Reset digital zoom. |

## IMixedStreamConfig

* **Type**: `interface`

* **Description**: Configurations to be set when pushing media streams to CDN.(new).

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_id |string |The room ID of the media stream. Required. |
   |user_id |string |The user ID of the media stream. |
   |push_url |string |the target address of the CDN. |
   |push_target_type |[MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/14199#mixedstreampushtargettype) \| undefined |Sets the push target type. The default target is CDN. |
   |push_wtn_stream_id |string \| undefined |Sets the WTN stream ID when pushing to WTN. This field takes effect only when `push_target_type` is `kMixedStreamPushTargetTypeToWTN`. |
   |layout_mode |[StreamLayoutMode](https://docs.byteplus.com/en/docs/12/14199#streamlayoutmode) \| undefined |Sets the layout mode for a WTN stream. |
   |interpolation_mode |[InterpolationMode](https://docs.byteplus.com/en/docs/12/14199#interpolationmode) \| undefined |Sets the interpolation mode for a WTN stream. |
   |audio_config |[MixedStreamAudioConfig](https://docs.byteplus.com/en/docs/12/14199#mixedstreamaudioconfig) |Audio transcoding configurations. |
   |video_config |[MixedStreamVideoConfig](https://docs.byteplus.com/en/docs/12/14199#mixedstreamvideoconfig) |Video transcoding configurations. |
   |layout_regions |[MixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14199#mixedstreamlayoutregionconfig)[] |Stream mixing region configuration. Required. |
   |background_color |string |Background color of the mixed stream. |
   |user_config_extra_info |string \| undefined |Additional data that you want to import. |
   |server_control_config |[MixedStreamServerControlConfig](https://docs.byteplus.com/en/docs/12/14199#mixedstreamservercontrolconfig) \| undefined |Server\-side stream mixing control configuration. |
   |background_image_url |string \| undefined |URL of the background image for the entire mixed\-stream canvas. The maximum length is 1024 bytes.<br><br>JPG, JPEG, and PNG images are supported. If the image aspect ratio differs from the canvas, the image is scaled to fill the canvas. |

## MixedStreamPushTargetType

* **Type**: `enum`

* **Description**: Push target types for mixed stream tasks.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamPushTargetTypeToCDN |`0` |Push to CDN. |
   |kMixedStreamPushTargetTypeToWTN |`1` |Publish as a WTN stream. |

## StreamLayoutMode

* **Type**: `enum`

* **Description**: Layout modes for WTN streams.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kStreamLayoutModeAuto |`0` |Use automatic layout. |
   |kStreamLayoutModeCustom |`2` |Use custom layout. |

## InterpolationMode

* **Type**: `enum`

* **Description**: Interpolation modes for WTN streams.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kInterpolationModeLastFrameFill |`0` |Fill missing frames with the last frame. |
   |kInterpolationModeBackgroundImageFill |`1` |Fill missing frames with the configured background image. |

## MixedStreamAudioConfig

* **Type**: `interface`

* **Description**: Audio transcoding configurations. With invalid or empty input, the configurations will be set as the default values.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |sample_rate |32000 \| 44100 \| 48000 |The sample rate (Hz). Supported sample rates: 32,00 Hz, 44,100 Hz, 48,000 Hz. Defaults to 48,000 Hz. |
   |channels |1 \| 2 |The number of channels. Supported channels: 1 (single channel), 2 (dual channel). Defaults to 2. |
   |bitrate |number |The bitrate (Kbps) in range of [32, 192]. Defaults to 64 Kbps. |
   |audio_profile |[MixedStreamAudioProfile](https://docs.byteplus.com/en/docs/12/14199#mixedstreamaudioprofile) |AAC profile. Defaults to `0`. |
   |audio_codec |[MixedStreamAudioCodecType](https://docs.byteplus.com/en/docs/12/14199#mixedstreamaudiocodectype) |Value: `0`<br><br>Audio codec. Defaults to `0`. |

## MixedStreamAudioProfile

* **Type**: `enum`

* **Description**: Advanced Audio Coding (AAC) profile.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamAudioProfileLC |`0` |(Default) AAC Low\-Complexity profile (AAC\-LC). |
   |kMixedStreamAudioProfileHEv1 |`1` |HE\-AAC v1 profile (AAC LC with SBR). |
   |kMixedStreamAudioProfileHEv2 |`2` |HE\-AAC v2 profile (AAC LC with SBR and Parametric Stereo). |

## MixedStreamVideoConfig

* **Type**: `interface`

* **Description**: Video mix stream configurations. With invalid or empty input, the configurations will be set as the default values.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |The width (pixels) to be set. The range is [2, 1920], and must be an even number. The default value is 360 pixels.<br><br>If an odd number is set, the width will be adjusted to the next larger even number. |
   |height |number |The height (pixels) to be set. The range is [2, 1920], and must be an even number. The default value is 640 pixels.<br><br>If an odd number is set, the height will be adjusted to the next larger even number. |
   |fps |number |The frame rate (FPS) in range of [1, 60]. The default value is 15 FPS. |
   |gop |number |The time interval between I\-frames (second) in range of [1, 5]. The default value is 2 seconds.<br><br>This parameter cannot be updated while pushing stream to the CDN. |
   |bitrate |number |The bitrate (Kbps) in range of [1, 10000]. The default value is self\-adaptive. |
   |video_codec |[MixedStreamVideoCodecType](https://docs.byteplus.com/en/docs/12/14199#mixedstreamvideocodectype) |The video codec. The default value is `0`.<br><br>This parameter cannot be updated while pushing stream to the CDN. |
   |enable_bframe |boolean |Whether to push streams with B frame, only supported by server mix:<br><br><br>* true: Yes<br><br>* false: No. |

## MixedStreamVideoCodecType

* **Type**: `enum`

* **Description**: The video codec.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamVideoCodecTypeH264 |`0` |(Default) H.264 format. |
   |kMixedStreamVideoCodecTypeByteVC1 |`1` |ByteVC1 format. |

## MixedStreamLayoutRegionConfig

* **Type**: `interface`

* **Description**: Layout information for one of the video streams to be mixed.

   After starting to push streams to CDN and mixing multiple video streams, you can set the layout information for each of them.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |user_id |string |The user ID of the user who publishes the video stream. Set this field for a video stream region. |
   |room_id |string |The room ID of the media stream. Set this field for a video stream region.<br><br>If the media stream is the stream forwarded by [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms), you must set the roomID to the room ID of the target room. |
   |location_x |number |The X coordinate (pixel) of the top left corner of the user's view. The default value is 0. |
   |location_y |number |The Y coordinate (pixel) of the top left corner of the user's view. The default value is 0. |
   |width |number |The width of the user's view in pixels. The default value is 360. |
   |height |number |The height of the user's view in pixels. The default value is 640. |
   |alpha |number |The opacity in the range `[0.0, 1.0]`. `0.0` is fully transparent. The default value is `1.0`. |
   |corner_radius |number |The proportion of the radius to the width of the canvas. `0.0` by default.<br><br>**Notes**:<br><br>After you set the value, `width_px`, `height_px`, and `corner_radius_px` are calculated based on `width`, `height`, `corner_radius`, and the width of the canvas. If `corner_radius_px < min(width_px/2, height_px/2)` is met, the value of `corner_radius` is set valid; if not, `corner_radius_px` is set to `min(width_px/2, height_px/2)`, and `corner_radius` is set to the proportion of `corner_radius_px` to the width of the canvas. |
   |z_order |number |The layer on which the video is rendered. The range is [0, 100]. 0 for the bottom layer, and 100 for the top layer. The default value is 0. |
   |is_local_user |boolean |Whether the source user of the stream is a local user:<br><br><br>* true: Yes<br><br>* false: No. This is the default value. |
   |media_type |[MixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14199#mixedstreammediatype) |The stream mixing content type. The default value is `kMixedStreamMediaTypeAudioAndVideo`. |
   |render_mode |[MixedStreamRenderMode](https://docs.byteplus.com/en/docs/12/14199#mixedstreamrendermode) |The render mode. The default value is `kMixedStreamRenderModeHidden`. |
   |region_content_type |[MixedStreamLayoutRegionType](https://docs.byteplus.com/en/docs/12/14199#mixedstreamlayoutregiontype) |Stream mixing region type. The default value is `kMixedStreamLayoutRegionTypeVideoStream`. |
   |image_water_mark |Uint8Array |The RGBA data of the mixing image. Put in null when mixing video streams. |
   |image_water_mark_param |[MixedStreamLayoutRegionImageWaterMarkConfig](https://docs.byteplus.com/en/docs/12/14199#mixedstreamlayoutregionimagewatermarkconfig) |Image parameters for stream mixing. Put in null when mixing video streams. |
   |source_crop |[SourceCrop](https://docs.byteplus.com/en/docs/12/14199#sourcecrop) \| undefined |Crops the source video for WTN streams. This field is not supported for mixed\-stream pushing tasks. |
   |spatial_position |[Position](https://docs.byteplus.com/en/docs/12/14199#position) |spatial position. |
   |apply_spatial_audio |boolean |Whether to apply spatial audio. The default value is `true`. |
   |alternate_image_fill_mode |[MixedStreamAlternateImageFillMode](https://docs.byteplus.com/en/docs/12/14199#mixedstreamalternateimagefillmode) |Fill mode of the alternate image after a user stops publishing video and the alternate image is restored. The default value is `kMixedStreamAlternateImageFillModeFit`. |
   |alternate_image_url |string |URL of the alternate image. The length must be less than 1024 characters. |

## MixedStreamMediaType

* **Type**: `enum`

* **Description**: Types of streams to be mixed.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamMediaTypeAudioAndVideo |`0` |Audio and video. |
   |kMixedStreamMediaTypeAudioOnly |`1` |Audio only. |

## MixedStreamRenderMode

* **Type**: `enum`

* **Description**: The render mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamRenderModeHidden |`1` |(Default) Fill and Crop.<br><br>The video frame is scaled with fixed aspect ratio, until it completely fills the canvas. The region of the video exceeding the canvas will be cropped. |
   |kMixedStreamRenderModeFit |`2` |Fit.<br><br>The video frame is scaled with fixed aspect ratio, until it fits just within the canvas. Other part of the canvas is filled with the background color. |
   |kMixedStreamRenderModeAdaptive |`3` |Fill the canvas.<br><br>The video frame is scaled to fill the canvas. During the process, the aspect ratio may change. |

## MixedStreamLayoutRegionType

* **Type**: `enum`

* **Description**: Stream mixing region type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamLayoutRegionTypeVideoStream |`0` |The region type is a video stream. |
   |kMixedStreamLayoutRegionTypeImage |`1` |The region type is an image. |

## MixedStreamLayoutRegionImageWaterMarkConfig

* **Type**: `interface`

* **Description**: Image parameters for stream mixing.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |image_width |number |Width of the original image in px. |
   |image_height |number |Height of the original image in px. |

## SourceCrop

* **Type**: `interface`

* **Description**: Cropping configurations for WTN source video.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |location_x |number |Normalized X coordinate of the top\-left corner after cropping, in the range `[0.0, 1.0)`. The default value is `0.0`. |
   |location_y |number |Normalized Y coordinate of the top\-left corner after cropping, in the range `[0.0, 1.0)`. The default value is `0.0`. |
   |width_proportion |number |Normalized width after cropping, in the range `(0.0, 1.0]`. The default value is `1.0`. |
   |height_proportion |number |Normalized height after cropping, in the range `(0.0, 1.0]`. The default value is `1.0`. |

## MixedStreamAlternateImageFillMode

* **Type**: `enum`

* **Description**: Fill mode for the alternate image in server\-side stream mixing.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamAlternateImageFillModeFit |`0` |The alternate image is scaled to the same proportion as the user's original video frame, by default. |
   |kMixedStreamAlternateImageFillModeFill |`1` |The alternate image does not scale with the same ratio as the user's original video frame, but maintains the original proportions of the image. |

## MixedStreamServerControlConfig

* **Type**: `interface`

* **Description**: Server\-side stream mixing control configuration.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |enable_volume_indication |boolean |Whether to send a separate volume indication SEI message.<br><br><br>* true: Enable the feature.<br><br>* false: Disable the feature. This is the default.<br><br><br>After enabling it, use `sei_content_mode` to control whether SEI contains only volume information. |
   |volume_indication_interval |number |Volume indication interval in seconds. The range is [0.3, +infinity), and the default is 2.<br><br>The value is rounded to one decimal place. For example, 0.36 is rounded to 0.4. |
   |talk_volume |number |Effective volume threshold in the range [0, 255]. The default is 0.<br><br>Values outside the range are reset to 0. |
   |is_add_volume_value |boolean |Whether volume indication SEI contains the volume value.<br><br><br>* true: Include the volume value.<br><br>* false: Do not include it. This is the default. |
   |sei_content_mode |[MixedStreamSEIContentMode](https://docs.byteplus.com/en/docs/12/14199#mixedstreamseicontentmode) |SEI content mode. |
   |sei_payload_type |number |SEI payload type.<br><br>**Notes**:<br><br><br>* The default is 100. Only 5 and 100 are supported.<br><br>* This setting cannot be changed while a mixed\-stream pushing task is running. |
   |sei_payload_uuid |string \| undefined |SEI payload UUID.<br><br>**Notes**:<br><br><br>* This field is required when `sei_payload_type` is 5. Otherwise, an error callback is triggered.<br><br>* When `sei_payload_type` is not 5, this field is ignored.<br><br>* The value must contain exactly 32 hexadecimal characters and must not contain hyphens.<br><br>* This setting cannot be changed while a mixed\-stream pushing task is running. |
   |media_type |[MixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14199#mixedstreammediatype) |Media content pushed to CDN after stream mixing.<br><br>**Notes**:<br><br>The default is audio and video. Audio\-only output is supported, but video\-only output is not. |
   |push_stream_mode |[MixedStreamPushMode](https://docs.byteplus.com/en/docs/12/14199#mixedstreampushmode) |Push mode for the mixed\-stream task.<br><br>**Notes**:<br><br>By default, the task can start when audio or video is published. It can also be configured to start with an alternate image when no user is publishing. |

## MixedStreamSEIContentMode

* **Type**: `enum`

* **Description**: SEI content mode for server\-side mixed\-stream pushing.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamSEIContentModeDefault |`0` |Include all SEI information in the video stream. This is the default. |
   |kMixedStreamSEIContentModeEnableVolumeIndication |`1` |Include only volume information in SEI data sent with non\-key frames.<br><br>This setting takes effect when `MixedStreamServerControlConfig.enable_volume_indication` is true. |

## MixedStreamPushMode

* **Type**: `enum`

* **Description**: Push mode for server\-side mixed\-stream tasks.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamPushModeOnStream |`0` |The mixed stream task can only be initiated when there is a user pushing the stream. |
   |kMixedStreamPushModeOnStartRequest |`1` |When there is no user push stream, enabling stream mixing can use the alternate image to initiate the mixed stream task. |

## LocalProxyConfiguration

* **Type**: `interface`

* **Description**: Detailed information of local proxy configurations.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |local_proxy_type |[LocalProxyType](https://docs.byteplus.com/en/docs/12/14199#localproxytype) |Types of local proxies. |
   |local_proxy_ip |string |Local proxy IP. |
   |local_proxy_port |number |Local proxy port. |
   |local_proxy_username |string |The username of the local proxy. |
   |local_proxy_password |string |The password of the local proxy. |

## LocalProxyType

* **Type**: `enum`

* **Description**: Types of local proxies.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalProxyTypeSocks5 |`1` |Socks5 proxy. If you choose Socks5 as the local proxy, you need to make sure all requirements listed in the Socks5 document are satisfied. |
   |kLocalProxyTypeHttpTunnel |`2` |Http tunnel proxy. |

## EarMonitorMode

* **Type**: `enum`

* **Description**: Whether to turn on the earphone monitoring function.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kEarMonitorModeOff |`0` |Not open. |
   |kEarMonitorModeOn |`1` |Open. |

## AudioFrameCallbackMethod

* **Type**: `enum`

* **Description**: Audio data callback method.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRecord |`0` |The callback of the audio data recorded by local microphone. |
   |kPlayback |`1` |The callback of the mixed audio data of all remote users subscribed by the local user. |
   |kMixed |`2` |The callback of the mixed audio data including the data recorded by local microphone and that of all remote users subscribed by the local user. |
   |kRemoteUser |`3` |The callback of the audio data before mixing of each remote user subscribed by the local user. |
   |kRecordScreen |`4` |The callback of screen audio data captured locally. |
   |kCaptureMixed |`5` |The callback of the audio data recorded by local microphone and audio data of MediaPlayer, EffectPlayer. |

## AudioFormat

* **Type**: `interface`

* **Description**: Audio format.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |sample_rate |[AudioSampleRate](https://docs.byteplus.com/en/docs/12/14199#audiosamplerate) |Audio sample rate. |
   |channel |[AudioChannel](https://docs.byteplus.com/en/docs/12/14199#audiochannel) |Audio channels. |
   |samples_per_call |number |Samples per audio frame returned by callback. You can set the length of the audio frame by setting the three parameters: `sample_rate`, `samples_per_call`, and `channel`.<br><br>`0` by default, which is the minimum value. The minimum value is the value when audio frame length is `0.01s`.<br><br>The maximum value is `2048`. If the value is invalid, the samples per callback uses the default value. |

## AudioAlignmentMode

* **Type**: `enum`

* **Description**: The alignment mode of remote audio streams.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioAlignmentModeOff |`0` |Disabled. |
   |kAudioAlignmentModeAudioMixing |`1` |All subscribed audio streams are aligned based on the process of the background music. |

## VideoEnhancementMode

* **Type**: `enum`

* **Description**: Low\-light video enhancement mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoEnhancementModeDisabled |`0` |Disable low\-light video enhancement. |
   |kVideoEnhancementModeAuto |`1` |Enable automatic low\-light video enhancement. |

## StreamInfo

* **Type**: `interface`

* **Description**: Information about the stream.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |room_id |string |The room ID of the media stream.<br><br>If the media stream is the stream forwarded by [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms), you must set the roomID to the room ID of the target room. |
   |user_id |string |The ID of the user who published the stream. |
   |is_screen |boolean |Reserved parameter. |

## LogConfig

* **Type**: `interface`

* **Description**: Local log configuration.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |log_path |string |Local log directory. |
   |log_level |[LocalLogLevel](https://docs.byteplus.com/en/docs/12/14199#localloglevel) |The logging level. The default is warning level. |
   |log_file_size |number |The maximum cache space available for logs in MB. The range is 1 to 100 MB, and the default value is 10 MB. |
   |log_filename_prefix |string \| undefined |Optional log file name prefix. The value must match `[a-zA-Z0-9_@\-\.]{1,128}`.<br><br>The final file name is the prefix, creation time, and `_rtclog.log`, for example `logPrefix_2023-05-25_172324_rtclog.log`. |

## LocalLogLevel

* **Type**: `enum`

* **Description**: Local log parameters.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kInfo |`0` |Info level. |
   |kWarning |`1` |(Default) Warning level. |
   |kError |`2` |Error level. |
   |kNone |`3` |Turn off logging. |

## RenderType

* **Type**: `enum`

* **Description**: rendering type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRenderTypeWebGL |`1` |WebGL render. |
   |kRenderTypeSoftware |`2` |Software render. |

## RtcRoomStats

* **Type**: `interface`

* **Description**: Call related statistics.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |tx_lostrate |number |Current Tx packet loss rate. The range is [0,1]. |
   |rx_lostrate |number |Current Rx packet loss rate. The range is [0,1]. |
   |rtt |number |Round\-trip time (in ms) from client side to server side. |
   |duration |number |The duration that the local user has spent in the room, measured in seconds. |
   |tx_bytes |number |Cumulative data sent by the user in bytes. |
   |rx_bytes |number |Cumulative data received by the user in bytes. |
   |tx_kbitrate |number |The instantaneous value of Tx bitrate in kbps. |
   |rx_kbitrate |number |The instantaneous value of Rx bitrate in kbps. |
   |rx_audio_kbitrate |number |The instantaneous value of audio Rx bitrate in kbps. |
   |tx_audio_kbitrate |number |The instantaneous value of audio Tx bitrate in kbps. |
   |rx_video_kbitrate |number |The instantaneous value of video Rx bitrate in kbps. |
   |tx_video_kbitrate |number |The instantaneous value of video Tx bitrate in kbps. |
   |rx_screen_kbitrate |number |The instantaneous RX bitrate of screen\-sharing video in Kbps. |
   |tx_screen_kbitrate |number |The instantaneous TX bitrate of screen\-sharing video in Kbps. |
   |user_count |number |Number of visible users in the current room. |
   |cpu_app_usage |number |CPU usage (%) of the application. |
   |tx_cellular_kbitrate |number |Cellular Link Send bit rate (kbps), get the instantaneous value of the data. |
   |rx_cellular_kbitrate |number |Cellular Link Receive bit rate (kbps), get the instantaneous value of the data. |

## UserOfflineReasonType

* **Type**: `enum`

* **Description**: Reason to leave the room.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kUserOfflineReasonQuit |`0` |The remote client calls [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-leaveroom) to leave the room. |
   |kUserOfflineReasonDropped |`1` |The remote client is disconnected because of poor network connection or expired Token. |
   |kUserOfflineReasonSwitchToInvisible |`2` |The remote client calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) to turn invisible. |
   |kUserOfflineReasonKickedByAdmin |`3` |The remote user has been removed from the room by the administrator via an OpenAPI call. |

## AVSyncState

* **Type**: `enum`

* **Description**: A/V synchronization states.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAVSyncStateAVStreamSyncBegin |`0` |A/V synchronization begins. |
   |kAVSyncStateAudioStreamRemove |`1` |The publisher stops publishing the audio stream during synchronization, which does not affect the sync relationship. |
   |kAVSyncStateVdieoStreamRemove |`2` |The publisher stops publishing the video stream during synchronization, which does not affect the sync relationship. |

## LocalStreamStats

* **Type**: `interface`

* **Description**: Local audio/video stream statistics and network status, the reference period is 2s.

   After the local user publishes the audio/video stream successfully, the SDK will periodically notify the local user through [onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onlocalstreamstats)

   The transmission status of the published audio/video stream during this reference period. This data structure is the type of parameter that is called back to the user.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |audio_stats |[LocalAudioStats](https://docs.byteplus.com/en/docs/12/14199#localaudiostats) |For statistics on audio streams sent by local devices. |
   |video_stats |[LocalVideoStats](https://docs.byteplus.com/en/docs/12/14199#localvideostats) |For statistics on video streams sent by local devices. |
   |local_tx_quality |[NetworkQuality](https://docs.byteplus.com/en/docs/12/14199#networkquality) |For the media stream uplink network quality of the local user.<br><br><br>* **Deprecated**<br><br><br>since 336.1, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onnetworkquality) instead. |
   |local_rx_quality |[NetworkQuality](https://docs.byteplus.com/en/docs/12/14199#networkquality) |The downlink network quality of the media stream belonging to the user.<br><br><br>* **Deprecated**<br><br><br>since 336.1, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onnetworkquality) instead. |
   |is_screen |boolean |Reserved parameter. |

## LocalAudioStats

* **Type**: `interface`

* **Description**: Local audio stream statistics, reference period 2s.

   After the local user publishes the audio stream successfully, the SDK will periodically notify the user through [onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onlocalstreamstats)

   The transmission status of the published audio stream during this reference period. This data structure is the type of parameter that is called back to the user.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |audio_loss_rate |number |Audio uplink packet loss rate in this reference period. The value range is [0, 1]. |
   |send_kbitrate |number |Send rate. The audio transmission rate in the reference period is kbps. |
   |record_sample_rate |number |Acquisition sampling rate. Audio sampling rate information collected in the reference period, in units of Hz. |
   |stats_interval |number |Statistical interval. The interval of this reference period is in ms.<br><br>This field is used to set the reference period for the callback. The default setting is 2s. |
   |rtt |number |Round\-trip time. The unit is ms. |
   |num_channels |number |Number of audio channels. |
   |sent_sample_rate |number |Audio transmission sampling rate. Audio transmission sampling rate information in the reference period, in Hz. |
   |jitter |number |Audio uplink network jitter in ms. |
   |encode_frame_rate |number |Audio encode frame rate. |

## LocalVideoStats

* **Type**: `interface`

* **Description**: Local video stream statistics, reference period 2s.

   After a local user publishes a video stream successfully, the SDK will periodically notify the user through [onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onlocalstreamstats)

   The delivery status of the published video stream during this reference period. This data structure is the type of parameter that is called back to the user.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |sent_kbitrate |number |TX bitrate in Kbps of the video stream with the highest resolution within the reference period. |
   |input_frame_rate |number |Sampling frame rate in fps of video capture during this reference period. |
   |sent_frame_rate |number |TX frame rate in fps of the video stream with the highest resolution within the reference period. |
   |encoder_output_frame_rate |number |Encoder\-output frame rate in fps of the video stream with the highest resolution within the reference period. |
   |renderer_output_frame_rate |number |Local\-rendering frame rate in fps during this reference period. |
   |stats_interval |number |Statistical interval. The interval of this reference period is in ms.<br><br>This field is used to set the reference period for the callback. The default setting is 2s. |
   |video_loss_rate |number |Video packet loss rate. The video uplink packet loss rate in this reference period ranges from [0,1]. |
   |rtt |number |Round\-trip time in ms. |
   |encoded_bitrate |number |Video encoding bitrate in Kbps of the video stream with the highest resolution within the reference period. |
   |encoded_frame_width |number |Video encoding width in px of the video stream with the highest resolution within the reference period. |
   |encoded_frame_height |number |Video encoding height in px of the video stream with the highest resolution within the reference period. |
   |encoded_frame_count |number |The total number of the video stream with the highest resolution within the reference period sent in the reference period. |
   |codec_type |[VideoCodecType](https://docs.byteplus.com/en/docs/12/14199#videocodectype) |For the encoding type of the video. |
   |is_screen |boolean |Reserved parameter. |
   |jitter |number |Video uplink network jitter in ms. |
   |codec_elapse_per_frame |number |Average video encoding time per frame in milliseconds. |

## VideoCodecType

* **Type**: `enum`

* **Description**: Video encoder type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kVideoCodecUnknown |`0` |Unknown. |
   |kVideoCodecH264 |`1` |H264. |
   |kVideoCodecByteVC1 |`2` |ByteVC1. |

## NetworkQuality

* **Type**: `enum`

* **Description**: Media streaming network quality.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kNetworkQualityUnknown |`0` |Network quality unknown. |
   |kNetworkQualityExcellent |`1` |The network quality is excellent. |
   |kNetworkQualityGood |`2` |The subjective feeling is similar to kNetworkQualityExcellent, but the bit rate may be slightly lower. |
   |kNetworkQualityPoor |`3` |Subjective feelings are flawed but do not affect communication. |
   |kNetworkQualityBad |`4` |Can barely communicate but not smoothly. |
   |kNetworkQualityVbad |`5` |The quality of the network is very poor and communication is basically impossible. |

## RemoteStreamStats

* **Type**: `interface`

* **Description**: The remote audio/video stream statistics and network status subscribed by the user, with a reference period of 2s.

   After the remote user subscribed to successfully publish the audio/video stream, the SDK will periodically notify local users through [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onremotestreamstats)

   The reception status of the remote audio/video stream subscribed during this reference period. This data structure is the type of parameter that is called back to the local user.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |uid |string |User ID of the remote stream publisher. |
   |audio_stats |[RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14199#remoteaudiostats) |Statistics for the remote audio stream. |
   |video_stats |[RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14199#remotevideostats) |Statistics for the remote video stream. |
   |remote_tx_quality |[NetworkQuality](https://docs.byteplus.com/en/docs/12/14199#networkquality) |For the media stream uplink network quality of the user you belong to.<br><br><br>* **Deprecated**<br><br><br>since 336.1, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onnetworkquality) instead. |
   |remote_rx_quality |[NetworkQuality](https://docs.byteplus.com/en/docs/12/14199#networkquality) |The downlink network quality of the media stream belongs to the user.<br><br><br>* **Deprecated**<br><br><br>since 336.1, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onnetworkquality) instead. |
   |is_screen |boolean |Reserved parameter. |

## RemoteAudioStats

* **Type**: `interface`

* **Description**: Remote audio stream statistics, reference period 2s.

   After a local user subscribes to a remote audio stream successfully, the SDK periodically notifies the local user of the reception status of the subscribed audio stream during this reference period through [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onremotestreamstats). This data structure is the type of parameter that is called back to the local user.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |audio_loss_rate |number |Audio packet loss rate. The audio downlink packet loss rate in the reference period, the value range is [0,1]. |
   |received_kbitrate |number |Receiving bit rate. The audio reception rate in the reference period in kbps. |
   |stall_count |number |Number of audio stalls. Number of stalls in the reference period. |
   |stall_duration |number |Audio stall Duration. Stall duration in the reference period in ms. |
   |e2e_delay |number |End\-to\-end latency at the user experience level. The delay from the start of encoding at the sending end to the start of decoding at the receiving end, in units of ms. |
   |playout_sample_rate |number |Play sample rate. Audio playback sample rate information within the reference period in Hz. |
   |stats_interval |number |Statistical interval. The interval of this reference period is in ms. |
   |rtt |number |Round\-trip time for client side to server level data transfer in ms. |
   |total_rtt |number |The sender\-server level\-the receiver\-link data transmission round\-trip time. The unit is ms. |
   |quality |number |The quality of the audio stream sent by the remote user.<br><br><br>* `0`: Network quality unknown.<br><br>* `1`: The network quality is excellent.<br><br>* `2`: The subjective feeling is similar to kNetworkQualityExcellent, but the bit rate may be slightly lower.<br><br>* `3`: Subjective feelings are flawed but do not affect communication.<br><br>* `4`: Can barely communicate but not smoothly.<br><br>* `5`: The quality of the network is very poor and communication is basically impossible. |
   |jitter_buffer_delay |number |The delay caused by the introduction of the jitter buffer mechanism. The unit is ms. |
   |num_channels |number |Number of audio channels. |
   |received_sample_rate |number |Audio reception sampling rate. Remote audio sampling rate information received within the reference period, in Hz. |
   |frozen_rate |number |The accumulated length of the audio card occurs after the remote user joins the room as a percentage of the total effective length of the audio. The effective duration of audio refers to the duration of audio other than stopping sending audio streams and disabling audio modules after remote users enter the room to publish audio streams. |
   |concealed_samples |number |Audio packet loss compensation (PLC) total number of sample points. |
   |concealment_event |number |Audio packet loss compensation (PLC) cumulative times. |
   |dec_sample_rate |number |Audio decoding sample rate. Audio decoding sample rate information in the reference period in Hz. |
   |dec_duration |number |Decoding duration. The total time\-consuming decoding of the remote audio stream received within this reference period, in seconds. |
   |jitter |number |Audio downlink network jitter in ms. |
   |decode_frame_rate |number |Audio decode frame rate. |
   |is_muted |Boolean |Whether the audio stream is muted. |

## RemoteVideoStats

* **Type**: `interface`

* **Description**: Remote video stream statistics, reference period 2s.

   After the local user subscribes to the remote video stream successfully, the SDK will periodically notify the local user of the reception status of the remote video stream subscribed to during this reference period through [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onremotestreamstats). This data structure is the type of parameter that is called back to the local user.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |Video Width. |
   |height |number |Video height. |
   |video_loss_rate |number |Video packet loss rate. Video downlink packet loss rate in the reference period, in units of %, and in the range of [0,1]. |
   |received_kbitrate |number |Receiving bit rate. Video reception rate within the reference period, in kbps. |
   |decoder_output_frame_rate |number |The decoder outputs the frame rate. Video decoder output frame rate within the reference period, in fps. |
   |renderer_output_frame_rate |number |Render frame rate. The video rendering frame rate in the reference period, in fps. |
   |stall_count |number |Number of stalls. Number of stalls in the reference period. |
   |stall_duration |number |Stall duration. The total duration of the video stall in the reference period. Unit ms. |
   |e2eDelay |number |End\-to\-end latency at the user experience level. The delay from the start of encoding at the sending end to the start of decoding at the receiving end, in units of ms. |
   |is_screen |number |Reserved parameter. |
   |stats_interval |number |Statistical interval, the interval of this reference period, in ms.<br><br>This field is used to set the reference period for the callback, currently set to 2s. |
   |rtt |number |Round\-trip time in ms. |
   |frozen_rate |number |The cumulative duration of the video card of the remote user accounts for the percentage (%) of the total effective duration of the video after entering the room. The effective duration of the video refers to the duration of the video other than stopping sending the video stream and disabling the video module after the remote user enters the room to publish the video stream. |
   |codec_type |[VideoCodecType](https://docs.byteplus.com/en/docs/12/14199#videocodectype) |For the encoding type of the video. |
   |video_index |number |For subscripts of streams with multiple resolutions. |
   |jitter |number |Video downlink network jitter in ms. |
   |codec_elapse_per_frame |number |Average video decoding time per frame in milliseconds. |
   |cap_to_render_delay |number |End\-to\-end latency at the user experience level. The delay from the start of capturing at the sending end to the completion of rendering at the receiving end, in units of ms. |
   |av_sync_diff_ms |number |Audio/video synchronization diff in ms. |
   |is_muted |Boolean |Whether the video stream is muted. |

## ForwardStreamStateInfo

* **Type**: `interface`

* **Description**: State and error for each room during relaying.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_id |string |ID of the room where the media stream aims to relay to<br><br>An Empty string is for all rooms. |
   |state |[ForwardStreamState](https://docs.byteplus.com/en/docs/12/14199#forwardstreamstate) |State of the room during relaying. |
   |error |[ForwardStreamError](https://docs.byteplus.com/en/docs/12/docs-85534#forwardstreamerror) |Error code from the room during relaying. |

## ForwardStreamState

* **Type**: `enum`

* **Description**: The state of the relaying for each room.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kForwardStreamStateIdle |`0` |Idle<br><br><br>* States of all the rooms turns to idle after you call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-stopforwardstreamtorooms).<br><br>* States of the rooms turns to idle that you call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms) to remove. |
   |kForwardStreamStateSuccess |`1` |Start relaying.<br><br><br>* State of the rooms turn to this state after the relaying starts successfully by calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms).<br><br>* State of the rooms added by calling [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms) turn to this state after the relaying start successfully. |
   |kForwardStreamStateFailure |`2` |Relay fails. Refer to [ForwardStreamError](https://docs.byteplus.com/en/docs/12/docs-85534#forwardstreamerror) for more information for more information.<br><br>Once the relaying fails, state of the room turns to this state after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms) or [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms). |

## ForwardStreamEventInfo

* **Type**: `interface`

* **Description**: Event from each room during relaying.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |room_id |string |ID of the room where the media stream aims to relay to<br><br>An Empty string is for all rooms. |
   |event |[ForwardStreamEvent](https://docs.byteplus.com/en/docs/12/14199#forwardstreamevent) |Event from the room during relaying. |

## ForwardStreamEvent

* **Type**: `enum`

* **Description**: Events during the relaying.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kForwardStreamEventDisconnected |`0` |Relaying pauses for the reason of network disconnecting. |
   |kForwardStreamEventConnected |`1` |Relaying recovers from the disconnecting. |
   |kForwardStreamEventInterrupt |`2` |Relaying aborts for the reason of that a User with the same user ID as that of the publisher joins. |
   |kForwardStreamEventDstRoomUpdated |`3` |Target room list updates after you call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms). |
   |kForwardStreamEventUnExpectAPICall |`4` |Wrong API\-calling order. For example, call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms) before calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms). |

## NetworkQualityStats

* **Type**: `interface`

* **Description**: Tx/Rx network quality.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |uid |string |User ID. |
   |fraction_lost |number |Packet loss ratio of the local client, ranging [0.0,1.0]<br><br>For a local user, it is the sent\-packet loss ratio.<br><br>For a remote user, it is the loss ratio of all the packets received. |
   |rtt |number |Round\-trip time (RTT) from client to server. Effective for the local user. Unit: ms. |
   |rx_quality |[NetworkQuality](https://docs.byteplus.com/en/docs/12/14199#networkquality) |Rx network quality grade. The range is `[0, 5]`; a higher score indicates poorer network quality. |
   |total_bandwidth |number |Average transmission rate of the media RTP packages in 2s. unit: bps<br><br>For a local user, it is the packet\-transmitting speed.<br><br>For a remote user, it is the speed of receiving all subscribed media. |
   |tx_quality |[NetworkQuality](https://docs.byteplus.com/en/docs/12/14199#networkquality) |Tx network quality grade. The range is `[0, 5]`; a higher score indicates poorer network quality. |

## SetRoomExtraInfoResult

* **Type**: `enum`

* **Description**: Extra information setting result.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSetRoomExtraInfoResultSuccess |`0` |Success. |
   |kSetRoomExtraInfoResultErrorNotJoinRoom |`-1` |Failure. You are not in the room. |
   |kSetRoomExtraInfoResultErrorKeyIsNull |`-2` |Failure. The key pointer is null. |
   |kSetRoomExtraInfoResultErrorValueIsNull |`-3` |Failure. The value pointer is null. |
   |kSetRoomExtraInfoResultResultUnknow |`-99` |Failure. Unknown error. |
   |kSetRoomExtraInfoResultErrorKeyIsEmpty |`-400` |Failure. The key length is 0. |
   |kSetRoomExtraInfoResultErrorTooOften |`-406` |Failure. Excessively frequent setting. 10 times per second is preferable. |
   |kSetRoomExtraInfoResultErrorSilentUser |`-412` |Failure. Invisible users are not allowed to call [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo). |
   |kSetRoomExtraInfoResultErrorKeyTooLong |`-413` |Failure. Key length exceeds 10 bytes. |
   |kSetRoomExtraInfoResultErrorValueTooLong |`-414` |Failure. Value length exceeds 128 bytes. |
   |kSetRoomExtraInfoResultErrorServer |`-500` |Failure. Server error. |

## FaceDetectResult

* **Type**: `interface`

* **Description**: The encoding modes for shared\-screen streams. The default mode is the high\-resolution mode. If you exclude specific windows by setting `filter_config`, the frame rate of the shared\-screen stream will be slower than 30fps.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |detect_result |number |Face Detection Result<br><br><br>* 0: Success<br><br>* !0: Failure. See [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table). |
   |face_count |number |Number of the detected face. |
   |rect |[Rectangle](https://docs.byteplus.com/en/docs/12/14199#rectangle)[] |The face recognition rectangles. The length of the array is the same as the number of detected faces. |
   |image_width |number |Width of the original image (px). |
   |image_height |number |Height of the original image (px). |
   |frame_timestamp_us |number |The time stamp of the video frame using face detection. |

## RTCAudioDeviceType

* **Type**: `enum`

* **Description**: Type of audio device.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRTCAudioDeviceTypeUnknown |`-1` |Unknown device. |
   |kRTCAudioDeviceTypeRenderDevice |`0` |Speaker or headphone. |
   |kRTCAudioDeviceTypeCaptureDevice |`1` |Microphone. |
   |kRTCAudioDeviceTypeScreenCaptureDevice |`2` |Screen capturing audio device. |

## AudioRecordingState

* **Type**: `enum`

* **Description**: Audio recording config.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioRecordingStateError |`0` |Recording exception. |
   |kAudioRecordingStateProcessing |`1` |Recording in progress. |
   |kAudioRecordingStateSuccess |`2` |The recording task ends, and the file is saved. |

## HardwareEchoDetectionResult

* **Type**: `enum`

* **Description**: Result of the detection inited before joining a room.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kHardwareEchoDetectionResultCanceled |`0` |Detection is stopped by the call of [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stophardwareechodetection) before the SDK reports the detection result. |
   |kHardwareEchoDetectionResultUnknown |`1` |Unknown state<br><br>Contact us if you retry several times but keep failing. |
   |kHardwareEchoDetectionResultNormal |`2` |Excellent<br><br>No echo issue is detected. |
   |kHardwareEchoDetectionResultPoor |`3` |Echo<br><br>Echo issue is detected. Recommend the user join the call with a headset through the interface. |

## LocalProxyState

* **Type**: `enum`

* **Description**: The states of local proxy connection.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalProxyStateInited |`0` |TCP proxy server is connected. |
   |kLocalProxyStateConnected |`1` |The local proxy is connected. |
   |kLocalProxyStateError |`2` |Errors occurred when connecting to the local proxy. |

## MixedStreamTaskInfo

* **Type**: `interface`

* **Description**: Mixed stream task info.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |task_id |string |Task ID. For WTN tasks, this value is the WTN stream ID. |
   |push_target_type |[MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/14199#mixedstreampushtargettype) |Push target type. See `MixedStreamPushTargetType`. |

## MixedStreamTaskEvent

* **Type**: `enum`

* **Description**: Mixed stream task events.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamTaskEventStartSuccess |`1` |The mixed\-stream push task started successfully. |
   |kMixedStreamTaskEventStartFailed |`2` |The mixed\-stream push task failed to start. |
   |kMixedStreamTaskEventUpdateSuccess |`3` |The mixed\-stream push task was updated successfully. |
   |kMixedStreamTaskEventUpdateFailed |`4` |The mixed\-stream push task failed to update. |
   |kMixedStreamTaskEventStopSuccess |`5` |The mixed\-stream push task stopped successfully. |
   |kMixedStreamTaskEventStopFailed |`6` |The mixed\-stream push task failed to stop. |
   |kMixedStreamTaskEventWarning |`7` |A warning occurred during the mixed\-stream push task. |

## IVideoFrame

* **Type**: `interface`

* **Description**: Sets the video frame.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |channel_id |string |Room ID. |
   |user_id |string |User ID. |
   |is_screen |boolean |Reserved parameter. |
   |plane_y |Uint8Array |Video data buffer in plane Y. |
   |plane_u |Uint8Array |Video data buffer in plane U. |
   |plane_v |Uint8Array |Video data buffer in plane V. |
   |width |number |Pixel of the width of the video. |
   |height |number |Pixel of the height of the video. |
   |plane_size_y |number |Size of Plane Y of the video data buffer. |
   |plane_size_u |number |Size of Plane U of the video data buffer. |
   |plane_size_v |number |Size of Plane V of the video data buffer. |
   |format |[VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14199#videopixelformat) |Format of the video frames. |
   |rotation |number |Rotation angles of the video frame. |
   |rgba |Uint8Array |Video data buffer RGBA. |
   |rgba_size |number |Video data buffer RGBA size. |
   |stream_id |string \| undefined |WTN stream ID. |
   |task_id |string |Stream\-mixing task ID. |

## ConnectionState

* **Type**: `enum`

* **Description**: SDK Connection status with the signaling server.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kConnectionStateDisconnected |`1` |Disconnected for 12s, SDK will try to reconnect automatically. |
   |kConnectionStateConnecting |`2` |The first request to connect to the server. Connecting. |
   |kConnectionStateConnected |`3` |The first connection was successful. |
   |kConnectionStateReconnecting |`4` |The code includes the following status:<br><br><br>* The first connection is not successful for 10s.<br><br>* The connection has been lost for 10s. Auto reconnecting. |
   |kConnectionStateReconnected |`5` |Successful reconnection after disconnection. |
   |kConnectionStateLost |`6` |In status `kConnectionStateDisconnected` for more than 10s without a successful reconnection. SDK will still continue to try to reconnect. |

## NetworkType

* **Type**: `enum`

* **Description**: SDK Network connection type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kNetworkTypeUnknown |`-1` |Network connection type unknown. |
   |kNetworkTypeDisconnected |`0` |The network connection has been disconnected. |
   |kNetworkTypeLAN |`1` |The network connection type is LAN. |
   |kNetworkTypeWIFI |`2` |The network connection type is Wi\-Fi (including hotspots). |
   |kNetworkTypeMobile2G |`3` |The network connection type is 2G mobile network. |
   |kNetworkTypeMobile3G |`4` |The network connection type is 3G mobile network. |
   |kNetworkTypeMobile4G |`5` |The network connection type is 4G mobile network. |
   |kNetworkTypeMobile5G |`6` |The network connection type is 5G mobile network. |

## PerformanceAlarmMode

* **Type**: `enum`

* **Description**: Whether to turn on release performance fallback.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPerformanceAlarmModeNormal |`0` |Not enabled Release performance fallback. |
   |kPerformanceAlarmModeSimulcast |`1` |Enable publish performance fallback. |

## PerformanceAlarmReason

* **Type**: `enum`

* **Description**: Reasons of performance\-related alarms.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPerformanceAlarmReasonBandwidthFallbacked |`0` |The poor network causes the transmission performance to fall back. This reason is only received when sending performance fallback is turned on. |
   |kPerformanceAlarmReasonBandwidthResumed |`1` |Network performance recovery, transmission performance rollback recovery. This reason is only received when sending performance fallback is turned on. |
   |kPerformanceAlarmReasonPerformanceFallbacked |`2` |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance is insufficient;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance is insufficient and the send performance fallback has occurred. |
   |kPerformanceAlarmReasonPerformanceResumed |`3` |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance shortage has been restored;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance shortage has been restored and the send performance fallback has occurred. Recovery. |

## SourceWantedData

* **Type**: `interface`

* **Description**: Performance fallback related data.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |When the release rollback is not turned on, this value represents the recommended video input width. When the rollback mode is the large and small stream mode, it represents the maximum width of the current push stream<br><br>If the send performance rollback is not turned on, this value represents the recommended Video input width;<br><br>If the send performance rollback is turned on, this value represents the maximum width of the current push stream. |
   |heigth |number |If send performance fallback is not turned on, this value represents the recommended video input height;<br><br>If send performance fallback is turned on, this value represents the maximum height of the current push stream. |
   |frame_rate |number |If send performance fallback is not turned on, this value represents the recommended video input frame rate in fps;<br><br>If send performance fallback is turned on, this value represents the maximum frame rate of the current push stream in fps. |

## SysStats

* **Type**: `interface`

* **Description**: The cpu and memory information used by App .

   The information is periodically (2s) notified to the user by the SDK via [onSysStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onsysstats) callback.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |cpu_cores |number |Current system CPU cores. |
   |cpu_app_usage |number |The cpu usage rate of the current application, the value range is [0,1]. |
   |memory_usage |number |The memory usage of the current application (in MB). |
   |full_memory |number |Full memory (in MB). |
   |total_memory_usage |number |System used memory (in MB). |
   |free_memory |number |Free allocable memory (in MB). |
   |memory_ratio |number |Memory usage of the current application (in %). |
   |total_memory_ratio |number |System memory usage (in %). |

## RemoteStreamSwitch

* **Type**: `interface`

* **Description**: Information of stream switching due to a Fallback.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |uid |string |User ID of the publisher of the subscribed media stream. |
   |is_screen |boolean |Reserved parameter. |
   |before_video_index |number |The quality index of the subscribed stream before the stream switching. |
   |after_video_index |number |The quality index of the subscribed stream after the stream switching. |
   |before_enable |boolean |Whether a video stream before the stream switching. |
   |after_enable |boolean |Whether a video stream after the stream switching. |
   |reason |[FallbackOrRecoverReason](https://docs.byteplus.com/en/docs/12/14199#fallbackorrecoverreason) |Reason of the Fallback or reverting from the Fallback of the subscribed stream. |

## FallbackOrRecoverReason

* **Type**: `enum`

* **Description**: Reason of the Fallback or reverting from a Fallback of the subscribed stream or the publishing stream.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kFallbackOrRecoverReasonUnknown |`-1` |The default: Fallback due to an unknown reason that is neither insufficient bandwidth of the network nor poor\-performance of the device. |
   |kFallbackOrRecoverReasonSubscribeFallbackByBandwidth |`0` |Fallback of the subscribed stream due to insufficient bandwidth of the network. |
   |kFallbackOrRecoverReasonSubscribeFallbackByPerformance |`1` |Fallback of the subscribed stream for poor\-performance of the device. |
   |kFallbackOrRecoverReasonSubscribeRecoverByBandwidth |`2` |Reverting from a Fallback of the subscribed stream due to the recovery of the network bandwidth. |
   |kFallbackOrRecoverReasonSubscribeRecoverByPerformance |`3` |Reverting from a Fallback of the subscribed stream due to the amelioration of the device performance. |
   |kFallbackOrRecoverReasonPublishFallbackByBandwidth |`4` |Fallback of the publishing stream due to Insufficient bandwidth of the network. |
   |kFallbackOrRecoverReasonPublishFallbackByPerformance |`5` |Fallback of the publishing stream due to poor\-performance of the device. |
   |kFallbackOrRecoverReasonPublishRecoverByBandwidth |`6` |Reverting from a Fallback of the publishing stream due to the recovery of the network bandwidth. |
   |kFallbackOrRecoverReasonPublishRecoverByPerformance |`7` |Reverting from a Fallback of the publishing stream due to the amelioration of the device performance. |

## VideoFrameInfo

* **Type**: `interface`

* **Description**: Video frame information.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |width |number |Width (pixels). |
   |height |number |High (pixels). |
   |rotation |[VideoRotation](https://docs.byteplus.com/en/docs/12/14199#videorotation) |Video frame clockwise rotation angle. |

## LocalAudioStreamState

* **Type**: `enum`

* **Description**: Local audio stream status.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalAudioStreamStateStopped |`0` |The default initial state of the local audio.<br><br>Callback to this state when the microphone stops working, corresponding to the error code kLocalAudioStreamErrorOk. |
   |kLocalAudioStreamStateRecording |`1` |The local audio recording device started successfully.<br><br>Callback to the state when the first frame of audio is collected, corresponding to the error code kLocalAudioStreamErrorOk. |
   |kLocalAudioStreamStateEncoding |`2` |The first frame of the local audio was successfully encoded.<br><br>Callback to the state when the audio first frame encoding is successful, corresponding to the error code kLocalAudioStreamErrorOk. |
   |kLocalAudioStreamStateFailed |`3` |The local audio startup failed, and the status is called back at the following times:<br><br><br>* The local recording device failed to start, corresponding to the error code kLocalAudioStreamErrorRecordFailure<br><br>* No recording device permission was detected, corresponding to the error code kLocalAudioStreamErrorDeviceNoPermission<br><br>* The audio encoding failed, corresponding to the error code kLocalAudioStreamErrorEncodeFailure. |
   |kLocalAudioStreamStateMute |`4` |The local audio stream is muted successfully.<br><br>This state is reported after [setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevicemute) succeeds, with kLocalAudioStreamErrorOk from [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-85534#localaudiostreamerror). |
   |kLocalAudioStreamStateUnmute |`5` |The local audio stream is unmuted successfully.<br><br>This state is reported after [setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevicemute) succeeds, with kLocalAudioStreamErrorOk from [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-85534#localaudiostreamerror). |

## RemoteAudioState

* **Type**: `enum`

* **Description**: Remote audio stream state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRemoteAudioStateStopped |`0` |The remote audio stream is not received. |
   |kRemoteAudioStateStarting |`1` |Start receiving the remote audio stream header. |
   |kRemoteAudioStateDecoding |`2` |The remote audio stream is decoding and playing normally. |
   |kRemoteAudioStateFrozen |`3` |Remote audio stream freezes. |

## RemoteAudioStateChangeReason

* **Type**: `enum`

* **Description**: Receives the cause of the remote audio stream state change.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRemoteAudioStateChangeReasonInternal |`0` |Internal reasons. |
   |kRemoteAudioStateChangeReasonNetworkCongestion |`1` |Network blocking. |
   |kRemoteAudioStateChangeReasonNetworkRecovery |`2` |Network back to normal. |
   |kRemoteAudioStateChangeReasonLocalMuted |`3` |Local user stops receiving remote audio stream. |
   |kRemoteAudioStateChangeReasonLocalUnmuted |`4` |Local users resume receiving remote audio streams. |
   |kRemoteAudioStateChangeReasonRemoteMuted |`5` |Remote user stops sending audio stream. |
   |kRemoteAudioStateChangeReasonRemoteUnmuted |`6` |Remote user resumes sending audio stream. |
   |kRemoteAudioStateChangeReasonRemoteOffline |`7` |Remote user leaves room. |

## LocalVideoStreamState

* **Type**: `enum`

* **Description**: Local video stream status.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalVideoStreamStateStopped |`0` |Local video capture stop state. |
   |kLocalVideoStreamStateRecording |`1` |Local video capture device activated. |
   |kLocalVideoStreamStateEncoding |`2` |After local video capture, the first frame is encoded successfully. |
   |kLocalVideoStreamStateFailed |`3` |Local video capture device failed to start. |

## RemoteVideoState

* **Type**: `enum`

* **Description**: Remote video stream status.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRemoteVideoStateStopped |`0` |The remote video stream defaults to the initial state, and the video has not yet started playing. |
   |kRemoteVideoStateStarting |`1` |Local user has received remote video stream header packet. |
   |kRemoteVideoStateDecoding |`2` |The remote video stream is decoding and playing normally. |
   |kRemoteVideoStateFrozen |`3` |Remote video streaming card, there may be network and other reasons. |
   |kRemoteVideoStateFailed |`4` |The remote video stream failed to play. |

## RemoteVideoStateChangeReason

* **Type**: `enum`

* **Description**: Cause of remote video stream state change.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kRemoteVideoStateChangeReasonInternal |`0` |Internal reasons. |
   |kRemoteVideoStateChangeReasonNetworkCongestion |`1` |Network blocking. |
   |kRemoteVideoStateChangeReasonNetworkRecovery |`2` |Network back to normal. |
   |kRemoteVideoStateChangeReasonLocalMuted |`3` |Local user stops receiving remote video stream or local user disables video module. |
   |kRemoteVideoStateChangeReasonLocalUnmuted |`4` |Local user resumes receiving remote video streams or local user enables video modules. |
   |kRemoteVideoStateChangeReasonRemoteMuted |`5` |The remote user stops sending the video stream or the remote user disables the video module. |
   |kRemoteVideoStateChangeReasonRemoteUnmuted |`6` |Remote user resumes sending video stream or remote user enables video module. |
   |kRemoteVideoStateChangeReasonRemoteOffline |`7` |The remote user leaves the channel. |

## RtcUser

* **Type**: `interface`

* **Description**: User information.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |user_id |string |User ID. |
   |meta_data |string |Meta data. |

## FirstFrameSendState

* **Type**: `enum`

* **Description**: First frame sending state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kFirstFrameSendStateSending |`0` |Sending. |
   |kFirstFrameSendStateSent |`1` |Sent. |
   |kFirstFrameSendStateEnd |`2` |Failed. |

## FirstFramePlayState

* **Type**: `enum`

* **Description**: First frame playback state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kFirstFramePlayStatePlaying |`0` |Playing. |
   |kFirstFramePlayStatePlayed |`1` |Play started. |
   |kFirstFramePlayStateEnd |`2` |Failed. |

## SingleStreamTaskEvent

* **Type**: `enum`

* **Description**: Single stream push task events.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSingleStreamTaskEventStartSuccess |`1` |The task starts successfully. |
   |kSingleStreamTaskEventStartFailed |`2` |The task fails to start. |
   |kSingleStreamTaskEventStopSuccess |`3` |The task stops successfully. |
   |kSingleStreamTaskEventStopFailed |`4` |The task fails to stop. |
   |kSingleStreamTaskEventWarning |`5` |Warning event. |

## RecordingInfo

* **Type**: `interface`

* **Description**: Details of local recording.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |file_path |string |The absolute path of the recorded file, including the file name and file suffix. |
   |video_codec_type |[VideoCodecType](https://docs.byteplus.com/en/docs/12/14199#videocodectype) |For the video encoding type of the recorded file. |
   |width |number |The width of the recorded video, in pixels. Please ignore this field for audio\-only recording. |
   |height |number |The height of the recorded video, the unit: pixels. Please ignore this field for audio\-only recording. |

## RecordingProgress

* **Type**: `interface`

* **Description**: Local recording progress.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |duration |number |The cumulative recording time of the current file, in milliseconds. |
   |file_size |number |The size of the currently recorded file in bytes. |

## LogoutReason

* **Type**: `enum`

* **Description**: Reason for logout.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLogoutReasonLogout |`0` |The user logs out by calling [logout](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-logout) or destroying the engine. |
   |kLogoutReasonDuplicateLogin |`1` |The user is logged out because another client logs in with the same user ID. |

## IAudioFrame

* **Type**: `interface`

* **Description**: Audio frame.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |frame_type |[AudioFrameType](https://docs.byteplus.com/en/docs/12/14199#audioframetype) |Value: `0`<br><br>Audio frame type. |
   |channels |number |Audio channel.<br><br>For dual channels, the audio frames are interleaved. |
   |sample_rate |number |Audio sample rate in Hz. |
   |buffer |Uint8Array |Address of the audio data buffer. |
   |render_time_ms |number |Audio frame timestamp in milliseconds. |
   |mute |boolean |Gets audio mute state identifier. |

## LocalAudioPropertiesInfo

* **Type**: `interface`

* **Description**: Local audio properties.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |audio_properties_info |[AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14199#audiopropertiesinfo) |Audio properties information. |

## AudioPropertiesInfo

* **Type**: `interface`

* **Description**: Audio properties.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |linear_volume |number |linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].<br><br><br>* [0, 25]: Silence<br><br>* [26, 75]: Low volume<br><br>* [76, 204]: Medium volume<br><br>* [205, 255]: High volume. |
   |nonlinear_volume |number |non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].<br><br><br>* [\-127, \-60]: Silence<br><br>* [\-59, \-40]: Low volume<br><br>* [\-39, \-20]: Medium volume<br><br>* [\-19, 0]: High volume. |
   |vad |number |Voice Activity Detection (VAD) result<br><br><br>* 1: Voice activity detected.<br><br>* 0: No voice activity detected.<br><br>* \-1: VAD not activated. |
   |spectrum |number[] |Spectrum array. The default length is 257. |
   |voice_pitch |number |Fundamental frequency of the local user's voice in Hz.<br><br>The value is returned when voice pitch reporting is enabled and the locally captured audio contains speech. Otherwise, the value is 0. |

## RemoteAudioPropertiesInfo

* **Type**: `interface`

* **Description**: Remote audio properties.

* **Properties**

   |Property |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/14199#streaminfo) |Stream information. |
   |audio_properties_info |[AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14199#audiopropertiesinfo) |Audio properties information. |

## EchoTestResult

* **Type**: `enum`

* **Description**: Call test result.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kTestSuccess |`0` |The playback of captured audio/video is received, test succeeds. |
   |kTestTimeout |`1` |Test is not completed after 60 seconds and has been stopped automatically. |
   |kTestIntervalShort |`2` |Less than 5s between the end of the last test and the start of the next test. |
   |kAudioDeviceError |`3` |Audio capture error. |
   |kVideoDeviceError |`4` |Video capture error. |
   |kAudioReceiveError |`5` |Audio reception error. |
   |kVideoReceiveError |`6` |Video reception error. |
   |kInternalError |`7` |Unrecoverable internal error. |

## MediaDeviceWarning

* **Type**: `enum`

* **Description**: Media device warning.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMediaDeviceWarningOK |`0` |No warning. |
   |kMediaDeviceWarningOperationDenied |`1` |Illegal device operation. Calls the API for internal device when using the external device. |
   |kMediaDeviceWarningCaptureSilence |`2` |No audio is captured. |
   |kMediaDeviceWarningDetectLeakEcho |`11` |Echoes between mics and speakers are detected during a call.<br><br>[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicewarning) notifies you with this enum of echo issue. During a call, SDK will detect echo<br><br>issue only when [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85535#roomprofiletype) is set to `kRoomProfileTypeMeeting` or<br><br>`kRoomProfileTypeMeetingRoom` and AEC is disabled. |
   |kMediaDeviceWarningCaptureDetectHowling |`16` |Howling detected.<br><br>You will receive this callback in the following scenarios: 1) Howling is detected under the room profiles<br><br>that do not support howling suppression; 2) Detect howling that is not suppressed under the room profiles that<br><br>support howling suppression. You can only enable howling suppression by calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) to set your room profile as kRoomProfileTypeCommunication, kRoomProfileTypeMeeting, and<br><br>kRoomProfileTypeMeetingRoom. We recommend that you remind your users to adjust the physical distance between two<br><br>devices or disable all unused devices except the connecting one. |
   |kMediaDeviceWarningPlayoutUseSilentDevice |`28` |use silent record device. |
   |kMediaDeviceWarningRecordingAllProcess |`29` |Unable to exclude current process from audio capture. Currently capturing audio from all system processes. |
   |kMediaDeviceWarningRecordingAllProcessFailed |`30` |recording all process failed. |

## SEIStreamEventType

* **Type**: `enum`

* **Description**: State of the black frame video stream.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSEIStreamEventTypeStreamAdd |`0` |A black frame video stream is published from the remote user.<br><br>In a voice call, when the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendseimessage) to send SEI data, SDK will automatically publish a black frame video stream, and trigger this callback. |
   |kSEIStreamEventTypeStreamRemove |`1` |The black frame video stream is removed. The timing this callback will be triggered is as following:<br><br><br>* The remote user turns on their camera, switching from a voice call to a video call.<br><br>* No SEI data is sent within 1min after the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendseimessage).<br><br>* The black frame video stream stops when the remote user switch to custom video capture. |

## WTNSubscribeState

* **Type**: `enum`

* **Description**: WTN subscription states.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kWTNSubscribeStateSubscribed |`0` |The WTN stream is subscribed. |
   |kWTNSubscribeStateUnsubscribed |`1` |The WTN stream is unsubscribed. |

## WTNSubscribeStateChangeReason

* **Type**: `enum`

* **Description**: Reasons for WTN subscription state changes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kWTNSubscribeStateChangeReasonSubscribe |`0` |The subscription succeeds. |
   |kWTNSubscribeStateChangeReasonUnsubscribe |`1300` |The subscription is canceled or fails for other reasons. |
   |kWTNSubscribeStateChangeReasonRemoteUnpublish |`1301` |Subscription fails because the remote stream is not published. |
   |kWTNSubscribeStateChangeReasonOverClientSubscribeStreamLimit |`1310` |Subscription fails because the client exceeds the maximum simultaneous subscription limit. |
   |kWTNSubscribeStateChangeReasonOverStreamSubscribeUserLimit |`1311` |Subscription fails because the number of subscribers to the same stream exceeds the server\-side limit. |
   |kWTNSubscribeStateChangeReasonOverStreamSubscribeRequestLimit |`1312` |Subscription fails because the QPS of subscription requests for the same stream exceeds the server\-side limit. |

## DataMessageSourceType

* **Type**: `enum`

* **Description**: SEI data source type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kDataMessageSourceTypeDefault |`0` |Custom message inserted by the client or server. |
   |kDataMessageSourceTypeSystem |`1` |System data that contains volume indication information. |

## PlayerState

* **Type**: `enum`

* **Description**: Player state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPlayerStateIdle |`0` |Not started. |
   |kPlayerStatePreloaded |`1` |Preloaded. |
   |kPlayerStateOpened |`2` |Opened. |
   |kPlayerStatePlaying |`3` |Playing. |
   |kPlayerStatePaused |`4` |Paused. |
   |kPlayerStateStopped |`5` |Stopped or finished. |
   |kPlayerStateFailed |`6` |Failed. |
   |kPlayerStateFinished |`7` |finished. |

## StreamSubscribeState

* **Type**: `enum`

* **Description**: Subscription status of media streams.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kStreamSubscribeStateSuccess |`0` |Successfully changed the subscription status. |
   |kStreamSubscribeStateFailedNotInRoom |`1` |Failed to change the subscription status, because you were not in the room. |
   |kStreamSubscribeStateFailedStreamNotFound |`2` |Failed to change the subscription status, because the target audio/video stream was not found. |
   |kStreamSubscribeStateFailedOverLimit |`3` |Failed to change the subscription status, because the number of streams you have subscribed to has exceeded the limit. |

## PublishState

* **Type**: `enum`

* **Description**: Stream publishing state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPublishStatePublished |`0` |Successfully published. |
   |kPublishStateUnpublished |`1` |Failed to publish. |

## SubscribeState

* **Type**: `enum`

* **Description**: Stream subscription state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSubscribeStateSubscribed |`0` |Successfully subscribed. |
   |kSubscribeStateUnsubscribed |`1` |Failed to subscribe. |

## PublishStateChangeReason

* **Type**: `enum`

* **Description**: Reason to change the publishing state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPublishStateChangeReasonPublish |`0` |Requested to publish. |
   |kPublishStateChangeReasonUnpublish |`1` |Requested to remove. |
   |kPublishStateChangeReasonNoPublishPermission |`2` |The token the user used was not permitted to publish. |
   |kPublishStateChangeReasonOverStreamPublishLimit |`3` |The number of streams the user has published has exceeded the limit. |
   |kPublishStateChangeReasonMultiRoomUnpublishFailed |`4` |The stream failed to remove from a room when you are publishing the stream in two or more rooms. |
   |kPublishStateChangeReasonPublishStreamFailed |`5` |Failed to publish due to the server error. |
   |kPublishStateChangeReasonPublishStreamForbidden |`6` |The user who tried to publish a stream is not a host. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) to change the user role. |
   |kPublishStateChangeReasonUserInPublish |`7` |The user who tried to publish a stream has already published a stream in a room. |

## SubscribeStateChangeReason

* **Type**: `enum`

* **Description**: Reason to change the subscription state.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSubscribeStateChangeReasonSubscribe |`0` |Requested to subscribe. |
   |kSubscribeStateChangeReasonUnsubscribe |`1` |Requested to unsubscribe. |
   |kSubscribeStateChangeReasonRemotePublish |`2` |The remote user published a stream. |
   |kSubscribeStateChangeReasonRemoteUnpublish |`3` |The remote user removed a stream. |
   |kSubscribeStateChangeReasonStreamFailed5xx |`4` |Failed to subscribe due to the server error. The SDK will automatically retry. |
   |kSubscribeStateChangeReasonStreamFailed404 |`5` |Failed to subscribe since the stream to be subscribed to was not found in the room. The SDK will automatically retry the subscription. If the subscription still fails, we recommend you exit and retry. |
   |kSubscribeStateChangeReasonOverStreamSubscribeLimit |`6` |The number of streams the user has subscribed to has exceeded the limit. |
   |kSubscribeStateChangeReasonNoSubscribePermission |`7` |The user was not permitted to subscribe to the stream. |

## AudioFrameType

* **Type**: `enum`

* **Description**: Audio frame type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioFrameTypePCM16 |`0` |PCM 16bit. |

## AVSyncEvent

* **Type**: `enum`

* **Description**: A/V synchronization event type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAVSyncEventInvalidAudioSyncUidRepeated |`0` |A/V synchronization failed.<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |

## SyncInfoStreamType

* **Type**: `enum`

* **Description**: Stream type for media stream information synchronization.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSyncInfoStreamTypeAudio |`0` |Audio stream. |

## MixedStreamAudioCodecType

* **Type**: `enum`

* **Description**: The audio codec.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamAudioCodecTypeAAC |`0` |AAC format. |

## ReturnStatus

* **Type**: `enum`

* **Description**: API return status.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kReturnStatusSuccess |`0` |Success. |
   |kReturnStatusFailure |`-1` |Failure. |
   |kReturnStatusParameterErr |`-2` |Invalid parameter. |
   |kReturnStatusWrongState |`-3` |Invalid API state. |
   |kReturnStatusHasInRoom |`-4` |Failure. The user is already in a room. |
   |kReturnStatusHasInLogin |`-5` |Failure. The user is already logged in. |
   |kReturnStatusHasInEchoTest |`-6` |Failure. The user is already running an audio/video call loop test. |
   |kReturnStatusNeitherVideoNorAudio |`-7` |Failure. Neither audio nor video is being captured. |
   |kReturnStatusRoomIdInUse |`-8` |Failure. The room ID is already in use. |
   |kReturnStatusScreenNotSupport |`-9` |Failure. Screen streams are not supported. |
   |kReturnStatusNotSupport |`-10` |Failure. The operation is not supported. |
   |kReturnStatusResourceOverflow |`-11` |Failure. The resource is already in use. |
   |kReturnStatusVideoNotSupport |`-12` |Failure. Video API calls are not supported. |
   |kReturnStatusAudioNoFrame |`-101` |Failure. No audio frame is available. |
   |kReturnStatusAudioNotImplemented |`-102` |Failure. The feature is not implemented. |
   |kReturnStatusAudioNoPermission |`-103` |Failure. Microphone permission is denied and the capture device cannot be initialized. |
   |kReturnStatusAudioDeviceNotExists |`-104` |Failure. No audio device exists, or the device has been removed. |
   |kReturnStatusAudioDeviceFormatNotSupport |`-105` |Failure. The device audio format is not supported. |
   |kReturnStatusAudioDeviceNoDevice |`-106` |Failure. No system audio device is available. |
   |kReturnStatusAudioDeviceCannotUse |`-107` |Failure. The current device is unavailable and must be replaced. |
   |kReturnStatusAudioDeviceInitFailed |`-108` |System error. Device initialization fails. |
   |kReturnStatusAudioDeviceStartFailed |`-109` |System error. The device fails to start. |
   |kReturnStatusAudioDeviceProcessNotExist |`-110` |Capture failed. The specified audio process does not exist. |
   |kReturnStatusAudioDeviceSpecifyingProcessUnsupport |`-111` |The current system does not support audio capture for the specified process. |
   |kReturnStatusNativeInvalid |`-201` |Failure. The native object is invalid. |
   |kReturnStatusVideoTimeStampWarning |`-202` |Warning. When pushing video frames to the RTC SDK, the timestamp difference between adjacent frames should match the interval at which frames are pushed. |
   |kReturnStatusAecSceneError |`-302` |Failure. The configuration delivers an invalid aec scene. |
   |kReturnStatusAecTypeWarning |`-303` |Warning. The configuration delivers an invalid aec type. |
