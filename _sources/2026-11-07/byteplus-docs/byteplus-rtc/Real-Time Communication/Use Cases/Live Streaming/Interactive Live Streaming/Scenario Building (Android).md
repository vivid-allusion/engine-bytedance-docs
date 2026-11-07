---
title: "Scenario Building (Android)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-152726"
---

<span id="sdk-integration"></span>
## SDK Integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/intergration.png) </span>

<span id="implementation-flowchart"></span>
## Implementation flowchart


* Battle between host and co\-host

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/livestreaming/image.jpg) </span>

* Co\-host between host and guest

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/livestreaming/b6c60d1c-511b-4bb6-b15e-cf4ffdd89cd3.png) </span>


<span id="core-feature-implementation"></span>
## Core feature implementation

<span id="host-starts-a-live-stream-and-the-audience-joins-the-room"></span>
### Host Starts a Live Stream and the Audience Joins the Room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/352usecase/016e4848-6bd1-4e45-bbcd-ebfa7fb56a89.png) </span>

<span id="sample-code"></span>
#### Sample Code

```Java
public void joinRoom(String roomId, String userId, String token) {
    Log.d(TAG, String.format("joinRoom: %s %s %s", roomId, userId, token));
    // Initialize the RTCVideo object
    mRTCVideo = RTCVideo.createRTCVideo(Utilities.getApplicationContext(), appId, mRTCVideoEventHandler, null, null);
 
    // Initialize the RTCRoom object
    mRTCRoom = mRTCVideo.createRTCRoom(roomId);
    mRTCRoom.setRTCRoomEventHandler(mRTCRoomEventHandler);
    mRTCRoomEventHandler.setBaseClient(mRTSClient);
    
    // join the RTC room
    UserInfo userInfo = new UserInfo(userId, null);
    RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_COMMUNICATION,
            true, true, true);
    mRTCRoom.joinRoom(token, userInfo, roomConfig);
    
    // Set the video capture config
    VideoCaptureConfig captureConfig = new VideoCaptureConfig(720, 1280, 15);
    mRTCVideo.setVideoCaptureConfig(captureConfig);
   
    // Set the video encoder config
    VideoEncoderConfig config = new VideoEncoderConfig();
    config.width = 720;
    config.height = 1280;
    config.frameRate = 15;
    mRTCVideo.setVideoEncoderConfig(config);
    
    // Start video and audio capture
    mRTCVideo.startVideoCapture();
    mRTCVideo.startAudioCapture();
}

/**
 * RTC business room-related event callbacks
 */
private final RTCRoomEventHandlerWithRTS mRTCRoomEventHandler = new RTCRoomEventHandlerWithRTS() {
    @Override
    public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
        super.onRoomStateChanged(roomId, uid, state, extraInfo);
        Log.d(TAG, String.format("onRoomStateChanged: %s, %s, %d, %s", roomId, uid, state, extraInfo));
        mRoomId = roomId;
        if (isFirstJoinRoomSuccess(state, extraInfo)) {
            // mSingleLiveInfo records the host's live streaming information.
            if (mSingleLiveInfo != null) {
                startLiveTranscoding(roomId, uid, mSingleLiveInfo.pushUrl);
            }
        }
    }

    /**
     * Checks if the user has successfully joined the room for the first time
     *
     * @param extraInfo Extra information
     * @return true if the user joined the room successfully; false otherwise.
     */
    protected boolean isFirstJoinRoomSuccess(int state, String extraInfo) {
        int joinType = -1;
        try {
            JSONObject json = new JSONObject(extraInfo);
            joinType = json.getInt("join_type");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return joinType == 0 && state == 0;
     }
}

/**
 * Mix streams and push to CDN
 * @param roomId Room ID
 * @param userId User ID
 * @param liveUrl RTMP push URL
 */
private void startLiveTranscoding(String roomId, String userId, String liveUrl,String taskId) {
    MixedStreamConfig config = MixedStreamConfig.defaultMixedStreamConfig();
    config.setRoomID(roomId);
    config.setUserID(userId);
    config.setPushURL(liveUrl);
    config.setExpectedMixingType(ByteRTCStreamMixingType.STREAM_MIXING_BY_SERVER);
    
    //Set video config
    MixedStreamVideoConfig videoConfig = config.getVideoConfig();
    videoConfig.setWidth(mHostConfig.width);
    videoConfig.setHeight(mHostConfig.height);
    videoConfig.setFps(mHostConfig.frameRate);
    videoConfig.setBitrate(mHostConfig.bitRate);
    config.setVideoConfig(videoConfig);
    
    //Set audio config
    MixedStreamAudioConfig audioConfig = config.getAudioConfig();
    audioConfig.setSampleRate(44100);
    audioConfig.setChannels(2);
    config.setAudioConfig(audioConfig);
    
    //Set the layout
    MixedStreamLayoutRegionConfig localRegionConfig = new MixedStreamLayoutRegionConfig();
    localRegionConfig.setUserID(userId);
    localRegionConfig.setIsLocalUser(true);
    localRegionConfig.setRoomID(roomId);
    localRegionConfig.setLocationX(0);
    localRegionConfig.setLocationY(0);
    localRegionConfig.setWidth(mHostConfig.width);
    localRegionConfig.setHeight(mHostConfig.height);
    localRegionConfig.setAlpha(1);
    localRegionConfig.setZOrder(0);
    localRegionConfig.setRenderMode(MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
    
    MixedStreamLayoutRegionConfig[] regions = new MixedStreamLayoutRegionConfig[]{localRegionConfig};
    MixedStreamLayoutConfig layoutConfig = new MixedStreamLayoutConfig();
    layoutConfig.setRegions(regions);
    JsonObject json = new JsonObject();
    json.addProperty(KEY_SEI_KEY_SOURCE, KEY_SEI_VALUE_SOURCE_NONE);
    //Set SEI message
    layoutConfig.setUserConfigExtraInfo(json.toString());
    config.setLayout(layoutConfig);
    //start Pushing Mixed-Stream to CDN
    mRTCVideo.startPushMixedStreamToCDN(taskId, config, mMixedStreamObserver);
   }
```


<span id="host-interacts-with-audience"></span>
### Host Interacts with Audience

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/livestreaming/13c9bda3-9afc-426e-a741-cd0faf9736dd.png) </span>

<span id="sample-code"></span>
#### Sample Code


* Audience becomes guest


```Java
public void audienceOnMic(String roomId, String userId, String token) {
   // Initialize the RTCVideo object
   mRTCVideo = RTCVideo.createRTCVideo(Utilities.getApplicationContext(), appId, mRTCVideoEventHandler, null, null);

     // Initialize the RTCRoom object  
   mRTCRoom = mRTCVideo.createRTCRoom(roomId);
   mRTCRoom.setRTCRoomEventHandler(mRTCRoomEventHandler);
   mRTCRoomEventHandler.setBaseClient(mRTSClient);
   
   // Set the video encoder config      
   VideoEncoderConfig config = new VideoEncoderConfig();
   config.width = 250;
   config.height = 250;
   config.frameRate = 15;
   mRTCVideo.setVideoEncoderConfig(config);
   
   // join the RTC room
   UserInfo userInfo = new UserInfo(userId, null);
   RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_COMMUNICATION,
           true, true, true);
   mRTCRoom.joinRoom(token, userInfo, roomConfig);
   
   // Start video and audio capture
   mRTCVideo.startVideoCapture();
   mRTCVideo.startAudioCapture();
}
```



* Guest is removed


```Java
public void audienceLeaveMic() {
    Log.d(TAG, "audienceLeaveMic");
    if (mRTCRoom != null) {
        // Leave the RTC room
        mRTCRoom.leaveRoom();
        // Destroy the mRTCRoom object.
        mRTCRoom.destroy();
        mRTCRoom = null;
    }
    if (mRTCVideo != null) {
        // Stop video and audio capture
        mRTCVideo.stopVideoCapture();
        mRTCVideo.stopAudioCapture();
        mRTCVideo = null;
    }
}
```


<span id="host-vs-co-host-interaction"></span>
### Host vs. Co\-host Interaction

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/352usecase/cf08ceef-d744-4b01-b0dc-5bafd67ddd30.png) </span>

<span id="sample-code"></span>
#### Sample Code

```Java
public void startForwardStreamToRooms(String coHostRoomId, String coHostUserId, String token,
                                      String selfRoomId, String selfUserId, String pushUrl) {
    // Enable cross-room relaying
    mCoHostInfo = new LiveTranscodingInfo(pushUrl, selfRoomId, selfUserId, coHostRoomId, coHostUserId);
    ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(coHostRoomId, token);
    if (mRTCRoom != null) {
        mRTCRoom.startForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
    }
}

/**
 * RTC business callbacks of joining room
 */
private final RTCRoomEventHandlerWithRTS mRTCRoomEventHandler = new RTCRoomEventHandlerWithRTS() {
    @Override
    public void onUserPublishStream(String uid, MediaStreamType type) {
        super.onUserPublishStream(uid, type);
        if (type == MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO) {
            return;
        }
        // CO-host
        if (mCoHostInfo != null && TextUtils.equals(uid, mCoHostInfo.coHostUserId)) {
            updateLiveTranscodingWithHost(mCoHostInfo.pushUrl, mCoHostInfo.selfRoomId, mCoHostInfo.selfUserId,
                                          mCoHostInfo.coHostUserId);
        }
    }
};

/**
 * Update the layout of the mixed stream
 * @param selfRoomId Room ID
 * @param selfUserId Your User ID
 * @param coHostRoomId Co-host's Room ID
 * @param coHostUserId Co-host's User ID
 */
public void updateLiveTranscodingWithHost( String liveUrl, 
                                           String selfRoomId,
                                           String selfUserId, 
                                           String coHostUserId,
                                           String taskId) {
    if (mRTCVideo == null) {
        return;
    }
    MixedStreamConfig config = MixedStreamConfig.defaultMixedStreamConfig();
     // Set Room ID
    liveTranscoding.setRoomId(selfRoomId);
    // Set push live streaming url
    liveTranscoding.setUrl(liveUrl);
    // Set mixing-stream mode
    liveTranscoding.setMixType(ByteRTCStreamMixingType.STREAM_MIXING_BY_SERVER);

   // Sets the video parameters for the mixed stream. Adjust these values based on your use case.
    MixedStreamVideoConfig videoConfig = config.getVideoConfig();
    videoConfig.setWidth(mHostConfig.width);
    videoConfig.setHeight(mHostConfig.height);
    videoConfig.setFps(mHostConfig.frameRate);
    videoConfig.setBitrate(mHostConfig.bitRate);

    // Set audio parameters of mixed-streams, with the specific parameters depending on the situation
    MixedStreamAudioConfig audioConfig = config.getAudioConfig();
    audioConfig.setSampleRate(44100);
    audioConfig.setChannels(2);
    
    MixedStreamLayoutConfig layoutConfig = new MixedStreamLayoutConfig();

    LiveTranscoding.Layout.Builder layoutBuilder = new LiveTranscoding.Layout.Builder();
    MixedStreamLayoutRegionConfig localRegion = new MixedStreamLayoutRegionConfig();
    localRegion.setUserID(selfUserId);
    localRegion.setIsLocalUser(true);
    localRegion.setRoomID(selfRoomId);
    localRegion.setLocationX(0);
    localRegion.setLocationY((int)(0.25 * mHostConfig.height));
    localRegion.setWidth((int)(0.5 * mHostConfig.width));
    localRegion.setHeight((int)(0.5 * mHostConfig.height));
    localRegion.setAlpha(1); 
    localRegion.setZorder(0); 

    MixedStreamLayoutRegionConfig hostRegion = new MixedStreamLayoutRegionConfig();
    hostRegion.setUserID(coHostUserId);
    hostRegion.setRoomID(selfRoomId);
    hostRegion.setLocationX((int)(0.5 * mHostConfig.width));
    hostRegion.setLocationY((int)(0.25 * mHostConfig.height));
    hostRegion.setWidth((int)(0.5 * mHostConfig.width));
    hostRegion.setHeight((int)(0.5 * mHostConfig.height));
    hostRegion.setAlpha(1);
    hostRegion.setZorder(0);
    JsonObject json = new JsonObject();
    json.addProperty(KEY_SEI_KEY_SOURCE, KEY_SEI_VALUE_SOURCE_NONE);
    //Set SEI message
    layoutConfig.setUserConfigExtraInfo(json.toString());
    layoutConfig.setRegions(new MixedStreamLayoutRegionConfig[]{localRegion,hostRegion});
    config.setLayout(layoutConfig);
    mRTCVideo.updatePushMixedStreamToCDN(taskId, config);
    }
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create ByteRTCVideo instance |createRTCVideo |
|Create ByteRTCRoom instance |[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcroom) |
|Set camera capture parameters |[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setvideocaptureconfig) |
|Set video publishing parameters |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setvideoencoderconfig) |
|Set mirroring |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideomirrortype) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |
|Leave RTC room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#leaveroom) |
|Destroy room object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#destroy) |
|Get the default configuration parameters of Live transcoding |MixedStreamConfig.defaultMixedStreamConfig |
|Start pushing mixed\-stream to CDN |startPushMixedStreamToCDN |
|Update parameters of pushing mixed\-stream to CDN |updatePushMixedStreamToCDN |
|Stop Pushing mixed\-stream to CDN |stopPushStreamToCDN |
|Start forwarding stream to rooms |[startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/docs-70080#startforwardstreamtorooms) |
|Stop forwarding stream to rooms |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#stopforwardstreamtorooms) |
|Start video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopvideocapture) |
|start audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startaudiocapture) |
|stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopaudiocapture) |
|Switch camera |[switchCamera](https://docs.byteplus.com/en/docs/12/docs-70080#switchcamera) |
|pause all subscribed stream |pauseAllSubscribedStream |
|Resume all subscribed stream |resumeAllSubscribedStream |


<span id="callback"></span>
### callback


|Function |Callback |
|---|---|
|Local user joins RTC room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onroomstatechanged) |
|Remote user joins RTC room |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
|Receiving the remote user's audio and video stream |onuserpublishstream |
|Local stream statistics and network quality |onLocalStreamStats |
|Remote stream statistics and network quality |onRemoteStreamStats |
