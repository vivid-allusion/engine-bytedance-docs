---
title: "Scenario Building (Android)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153604"
---

<span id="sdk-integration"></span>
## SDK Integration

To ensure the best experience, this use case requires the integration of RTC SDK and MediaLive Player (recommended). You need to activate the service in the console of RTC and MediaLive. Activation instructions are as follows:


1. For details of the overall access process of RTC SDK, see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/intergration.png) </span>

2. For details of the access procedure of MediaLive player, see [Getting started with BytePlus MediaLive](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)

> You can do so by using the same third\-party live player. To ensure the best experience, however, you must implement the audio hosting feature. For details, contact our technical support team;


<span id="implementation-flows"></span>
## Implementation Flows


* High\-level workflow diagram


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/watchlivetogether/f6877cc6-3604-49f1-8221-326b39b3d98f.png) </span>

<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="join-room"></span>
### Join room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/watchlivejoinroom.jpg) </span>

<span id="sample-code"></span>
#### Sample code

```Java
/**
  Join the RTC room and initialize parameters
  @param token The token for joining the RTC room
  @param roomId The ID of the RTC room to join
  @param userId The user ID for joining the RTC room
 */
public void joinRTCRoom(String token, String roomId, String userId) {
    // Initialize the RTCVideo object
    mRTCVideo = RTCVideo.createRTCVideo(applicationContext, appId, mIRTCVideoEventHandler, null, null);

    // Initialize the RTCRoom object
    mRTCRoom = mRTCVideo.createRTCRoom(roomId);
    mRTCRoom.setRTCRoomEventHandler(mIRTCRoomEventHandler);

    // Set visibility
    mRTCRoom.setUserVisibility(true);

    // Enable the microphone and camera for the host. Audience members should join with their microphone and camera disabled
    mRTCVideo.startVideoCapture();
    mRTCVideo.startAudioCapture();

    // Set local video rendering and encoding mirror
    mRTCVideo.setLocalVideoMirrorType(MirrorType.MIRROR_TYPE_RENDER_AND_ENCODER);

    // Bind the local preview view
    TextureView view = new TextureView(Utilities.getApplicationContext());
    VideoCanvas videoCanvas = new VideoCanvas(view, VideoCanvas.RENDER_MODE_HIDDEN);
    mRTCVideo.setLocalVideoCanvas(StreamIndex.STREAM_INDEX_MAIN, videoCanvas);

    // Set audio scenario type
    mRTCVideo.setAudioScenario(AudioScenarioType.AUDIO_SCENARIO_COMMUNICATION);

    // Enable speaker volume monitoring
    AudioPropertiesConfig audioPropertiesConfig = new AudioPropertiesConfig(300);
    mRTCVideo.enableAudioPropertiesReport(audioPropertiesConfig);

    // Join the room to start the interaction. An AppId and a valid token are required
    UserInfo userInfo = new UserInfo(userId, null);
    RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_LW_TOGETHER,
            true, true, true);
    mRTCRoom.joinRoom(token, userInfo, roomConfig);
}

```


```Java
private final IRTCVideoEventHandler mIRTCVideoEventHandler = new IRTCVideoEventHandler() {
    /**
      Callback for local user audio properties
     */
    @Override
    public void onLocalAudioPropertiesReport(LocalAudioPropertiesInfo[] audioPropertiesInfos) {
        super.onLocalAudioPropertiesReport(audioPropertiesInfos);
    }
    /
      Callback for remote user audio properties
     /
    @Override
    public void onRemoteAudioPropertiesReport(RemoteAudioPropertiesInfo[] audioPropertiesInfos, int totalRemoteVolume) {
        super.onRemoteAudioPropertiesReport(audioPropertiesInfos, totalRemoteVolume);
    }
};

private final IRTCRoomEventHandler mIRTCRoomEventHandler = new IRTCRoomEventHandler() {
    /**
      Callback for receiving RTC room state changes
     /
    @Override
    public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
        super.onRoomStateChanged(roomId, uid, state, extraInfo);
    }

    /**
      Callback for remote user joining the room
     /
    @Override
    public void onUserJoined(UserInfo userInfo, int elapsed) {
        super.onUserJoined(userInfo, elapsed);
    }

    /**
      Callback for new media streams published by remote users
     /
    @Override
    public void onUserPublishStream(String uid, MediaStreamType type) {
        super.onUserPublishStream(uid, type);
        if (type == MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO) {
            return;
        }
        // Bind the remote user's video view
        TextureView view = new TextureView(Utilities.getApplicationContext());
        VideoCanvas videoCanvas = new VideoCanvas(view, VideoCanvas.RENDER_MODE_HIDDEN);
        RemoteStreamKey streamKey = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
        mRTCVideo.setRemoteVideoCanvas(streamKey, videoCanvas);
    }
};
```


<span id="watch-live-together"></span>
### Watch LIVE together

When the room owner starts a "Watch LIVE together" session, all audience members join the live room synchronously. The room owner and audience can then watch the same live stream using the player.

For player integration and detailed instructions, see the Player SDK for Android documentation

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/watchlive.jpg) </span>

<span id="code-sample"></span>
#### Code sample

```Java
/**
 * Start PCM audio mixing
 */
public void startAudioMixing() {
    // Get the RTC audio mixing manager
    IMediaPlayer mixAudioManager = mRTCVideo.getMediaPlayer(0);
    // Start mixing PCM audio data
    MediaPlayerCustomSource source = new MediaPlayerCustomSource();
    source.provider = null;
    source.mode = MediaPlayerCustomSourceMode.PUSH;
    source.type = MediaPlayerCustomSourceStreamType.RAW;

    MediaPlayerConfig config = new MediaPlayerConfig(AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT, 0);
    config.startPos = 0;
    config.syncProgressToRecordFrame = false;
    config.autoPlay = true;

    mixAudioManager.openWithCustomSource(source, config);
}

/**
 * Audio player data callback for pushing audio data to the RTC engine
 */
public void pushAudioMixingFrame(byte[] pcm, int samples, AudioSampleRate sampleRate, AudioChannel channel) {
    // Get the RTC audio mixing manager
    IMediaPlayer mixAudioManager = mRTCVideo.getMediaPlayer(0);
    // Construct audio frame
    AudioFrame frame = new AudioFrame(pcm, samples, sampleRate, channel);
    // Push the audio data from the player callback to the RTC engine for playback
    mixAudioManager.pushExternalAudioFrame(frame);
}

/**
 * Stop PCM audio mixing
 */
public void stopAudioMixing() {
    // Get the RTC audio mixing manager
    IMediaPlayer mixAudioManager = mRTCVideo.getMediaPlayer(0);
    // Stop mixing
    mixAudioManager.stop();
}
```


<span id="console"></span>
### Console

<span id="code-sample"></span>
#### Code sample

```Java
/**
 * Enable/disable playback ducking.
 * When enabled, this feature automatically lowers the local media playback volume when a remote user speaks. The volume returns to its original level after the remote user stops speaking, ensuring remote voices are clearly audible
 * @param enable Whether to enable playback ducking
 */
public void enablePlaybackDucking(boolean enable) {
    mRTCVideo.enablePlaybackDucking(enable);
}

/**
  * Adjust the volume of the audio mixing, including audio file mixing and PCM mixing.
  * @param volume The ratio of the mixing volume to the original volume. The range is [0, 400], and the recommended range is [0, 100].
  */
public void setAudioMixingVolume(int volume) {
    IMediaPlayer mixAudioManager = mRTCVideo.getMediaPlayer(0);
    mixAudioManager.setVolume(volume, AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT);
}

/**
 * Adjust the playback volume of all mixed remote audio streams. You can use this interface to set the playback volume before or during audio playback.
 * @param volume The playback volume as a ratio of the original volume, expressed as a percentage. The value ranges from 0 to 400. Values outside this range are automatically capped.
 */
public void setPlaybackVolume(int volume) {
    mRTCVideo.setPlaybackVolume(volume);
}
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create RTCVideo object |createRTCVideo |
|Create RTCRoom object |[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcroom) |
|Set user visibility |[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#setuservisibility) |
|Set local rendering and encoding mirroring |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideomirrortype) |
|Set local video rendering view |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideocanvas) |
|Set audio scenario type |[setAudioScenario](https://docs.byteplus.com/en/docs/12/docs-70080#setaudioscenario) |
|Enable audio properties report |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#enableaudiopropertiesreport) |
|Create a mixing management interface |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#getmediaplayer) |
|Start local audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startaudiocapture) |
|Start local video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |
|Set the remote user video rendering view |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setremotevideocanvas) |
|Enable PCM audio data mixing |enableAudioMixingFrame |
|Push PCM audio frame data for mixing |pushAudioMixingFrame |
|Adjust the volume of mixed audio |setAudioMixingVolume |
|Disable audio mixing |disableAudioMixingFrame |
|Adjust the playback volume of remote users |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#setplaybackvolume) |
|Enable volume ducking |[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/docs-70080#enableplaybackducking) |
|Leave Room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#leaveroom) |
|Destroy the RTCRoom object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#destroy) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopaudiocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopvideocapture) |
|Destroy the RTCVideo object |destroyRTCVideo |


<span id="callback"></span>
### Callback


|Function |Callback |
|---|---|
|Local user joins RTC room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onroomstatechanged) |
|Audio playback route changes |[onAudioRouteChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onaudioroutechanged) |
|Local audio information |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalaudiopropertiesreport) |
|Audio information of the subscribed remote user |onRemoteAudioPropertiesReport |
|Remote user joins RTC room |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
|A new media stream from a remote user is available |onuserpublishstream |
