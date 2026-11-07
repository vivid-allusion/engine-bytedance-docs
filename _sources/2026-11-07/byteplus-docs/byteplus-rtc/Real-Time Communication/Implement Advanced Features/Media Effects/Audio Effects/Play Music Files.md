---
title: "Play Music Files"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70141"
---

To enhance interactive entertainment scenarios like 'Watch Together' or 'Listen Together', you can play music files for all participants in a room to hear.

In this context, "music" refers to audio files or PCM data streams longer than 20 seconds, such as background music or accompaniments. Only 4 music files can be played simultaneously.

> Audio shorter than 20 seconds is generally considered a sound effect. For these files, use the sound\-playing interface. Please refer to Sound Playing for more information.

## Prerequisite

You have already integrated RTC SDK and are able to implement basic audio and video calls.

For details about which SDKs support music playback, see API and Callback.

## Step 1: Create an engine

After creating the audio and video engine instance, call `getMediaPlayer` and pass a player ID to create a music player instance.

**java**

```java
EngineConfig config = new EngineConfig();
config.appID = appId;
config.context = applicationContext;
rtcVideo = RTCEngine.createRTCEngine(config, rtcVideoEventHandler);
// Enable local audio capture
rtcVideo.startAudioCapture();
// Play non-PCM files
mediaPlayer = rtcVideo.getMediaPlayer(PLAYER_ID);
```

**swift**

```swift
let engineCfg = ByteRTCEngineConfig.init()
engineCfg.appID = appId
engineCfg.parameters = [:]
self.rtcVideo = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)
// Enable local audio capture
self.rtcVideo?.startAudioCapture()
// Play non-PCM files
self.mediaPlayer = self.rtcVideo?.getMediaPlayer(audioPlayerId)
```

**cpp**

```cpp
// Create engine
    m_handler.reset(new ByteRTCEventHandler());
    bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    m_video = bytertc::IRTCEngine::createRTCEngine(conf, m_handler.get());

// Enable local audio capture
m_video->startAudioCapture();
// Play non-PCM files
player_audio = m_video->getMediaPlayer(id1); 
```

### Step 2: Set the event handler

You can use callbacks to monitor the playback status and progress of the music.

**java**

```java
// It is recommended to use strong reference for handler
    mediaPlayer.setEventHandler(playerEventHandler);
```

**swift**

```swift
// It is recommended to use strong reference for handler
    self.mediaPlayer?.setEventHandler(self)
    // Set playback progress callback interval, e.g., callback every 1s
    self.mediaPlayer?.setProgressInterval(1000)
    
    // MARK: - ByteRTCMediaPlayerEventDelegate
    func onMediaPlayerStateChanged(_ playerId: Int32, state: ByteRTCPlayerState, error: ByteRTCPlayerError) {
        // Playback state change callback
    }
    
    func onMediaPlayerPlayingProgress(_ playerId: Int32, progress: Int64) {
        // Playback progress callback
    }
```

**cpp**

```cpp
// It is recommended to use strong reference for handler
m_player_audio->setEventHandler(m_handler.get());
// Set playback progress callback interval, e.g., callback every 1s
m_player_audio->setProgressInterval(1000);

class EventHandler : public bytertc::IMediaPlayerEventHandler {
public:
    void onMediaPlayerStateChanged(int playerId, bytertc::PlayerState state, bytertc::PlayerError error) override {
        // Playback state change callback
    }
    
    void onMediaPlayerPlayingProgress(int playerId, int64_t progress) override {
        // Playback progress callback
    }
};
```

## Play PCM audio

### Enable audio mixing

Before calling `openWithCustomSource` to enable audio mixing, you can initialize settings such as auto\-play, the number of playbacks, and other configurations.

**java**

```java
private void startPlayPCM() {
    openFile(pcmPath);

    MediaPlayerCustomSource source = new MediaPlayerCustomSource();
    source.mode = MediaPlayerCustomSourceMode.PUSH;
    source.type = MediaPlayerCustomSourceStreamType.RAW;
    source.provider = null;

    MediaPlayerConfig playerConfig = new MediaPlayerConfig();
    playerConfig.startPos = 0;
    playerConfig.autoPlay = true;
    playerConfig.playCount = 1;
    playerConfig.type = AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH;
    playerConfig.callbackOnProgressInterval = 500;

    pcmPlayer.openWithCustomSource(source, playerConfig);
    startPushPCM();
}
```

**swift**

```swift
@objc func startPcmMix() {
    let source = ByteRTCMediaPlayerCustomSource.init()
    source.mode = .push
    source.type = .raw
    
    let config  = ByteRTCMediaPlayerConfig.init()
    config.type = .playoutAndPublish
    config.playCount = 1
    config.autoPlay = true
    
    self.mediaPlayerPCM?.open(with: source, config: config)
};
```

**cpp**

```cpp
bytertc::MediaPlayerCustomSource source;
source.mode = bytertc::kMediaPlayerCustomSourceModePush;
source.provider = nullptr;
source.type = bytertc::kMediaPlayerCustomSourceStreamTypeRaw;
bytertc::MediaPlayerConfig config;
// If auto_play=true, playback starts automatically without a call to start().
// When auto_play=false, it does not play automatically and requires calling the start interface
config.auto_play = true; 
config.callback_on_progress_interval = 1000;
config.play_count = 1;
config.start_pos = 0;
config.sync_progress_to_record_frame = true;
config.type = bytertc::kAudioMixingTypePlayoutAndPublish;

int ret = player->openWithCustomSource(source, config);
```

### Play

Before pushing audio data to RTC by calling `pushExternalAudioFrame`, you need to process the data according to the RTC SDK requirements. The following code segments take the PCM audio file provided in the sample project as an example to specify the data format requirements.

**java**

```java
Runnable pushAudioFrameTask = new Runnable() {
    @Override
    public void run() {
        int size = 16 * 10;
        if (isFirstPush) {
            size = size * 20;
            isFirstPush = false;
        }
        ByteBuffer pushBuffer = ByteBuffer.allocate(size * 2);
        AudioFrame audioFrame = new AudioFrame();
        audioFrame.channel = AudioChannel.AUDIO_CHANNEL_MONO;
        audioFrame.sampleRate = AudioSampleRate.AUDIO_SAMPLE_RATE_16000;
        audioFrame.samples = size;

        int nRead = 0;
        if (fileData != null) {
            nRead = Integer.min(size * 2, fileDataBufferSize - fileDataOffset);
            pushBuffer.put(fileData, fileDataOffset, nRead);
            fileDataOffset += nRead;
        }
        Log.i(TAG, "offset:" + fileDataOffset + " read:" + nRead);
        if (nRead == 0) {
            stopPlayPCM();
            return;
        }
        audioFrame.buffer = pushBuffer.array();
        pcmPlayer.pushExternalAudioFrame(audioFrame);
    }
};
```

**swift**

```swift
func pushPCMData() {
    if let mediaPlayerPCM = self.mediaPlayerPCM {
        var size = 160 * 1 * 2 
        
        if self.firstPush {
            size = size * 20 
            self.firstPush = false
        }
        
        let filePath = Bundle.main.path(forResource: "pcmFileName", ofType: "pcm")!
        let url = URL(fileURLWithPath: filePath)
        
        guard let fileData = try? Data(contentsOf: url) else {
            print("Failed to read PCM file data.")
            return
        }
        
        var endOffset = self.startOffset + size
        if endOffset >= fileData.count {
            self.startOffset = 0
            endOffset = self.startOffset + size
        }
        
        let audioData: Data = fileData.subdata(in: startOffset..<endOffset)
        self.startOffset = endOffset
        
        let audioFrame = ByteRTCAudioFrame()
        audioFrame.channel = .mono
        audioFrame.sampleRate = .rate16000
        audioFrame.samples = Int32(size) / 2 
        audioFrame.buffer = audioData
        
        mediaPlayerPCM.pushExternalAudioFrame(audioFrame)
    }
}
```

**cpp**

```cpp
m_pcm_file = new QFile(name);
m_pcm_file->seek(0); // Seek PCM audio file to initial position

m_timer.start(10); // Start timer

connect(m_timer, &QTimer::timeout, [](){
// Data size for every 10ms = sample count * channel count * bytes per sample, this PCM file is 16000 sample rate, mono, 2 bytes per sample
    int size = 160 * 1 * 2; 
    if (m_first_push) {
        size = 20 * size; // It is recommended to pass 200ms buffer data for the first time to avoid noise
        m_first_push = false;
    }

    if (m_pcm_file) {
        QByteArray data = m_pcm_file->read(size);
        if (data.size() == 0) {
            return;
        }
        bytertc::AudioFrameBuilder builder;
        builder.channel = bytertc::kAudioChannelMono; // Specify according to the channel count of PCM file
        builder.sample_rate = bytertc::kAudioSampleRate16000; // Specify according to the sample rate of PCM file
        builder.data = (uint8_t*)data.data();
        builder.data_size = size;
        auto frame = bytertc::buildAudioFrame(builder);

        int ret = player_pcm->pushExternalAudioFrame(frame);
}});
```

### Stop

Call `stop` to stop playback.

**java**

```java
pcmPlayer.stop();
```

**swift**

```swift
@objc func stopPcmMix()  {
    self.mediaPlayerPCM?.stop()
    self.timer?.cancel()
}
```

**cpp**

```cpp
int ret = player_pcm->stop();
m_timer.stop(); 
```

### Adjust audio mixing volume

Volume settings only take effect after playback starts and before it stops.

Batch volume setting for all mixed audio is available via the `setVolumeAll` interface for mobile. As for PC, you can only specify the volume of each mixed audio one by one with the `setVolume` interface.

**java**

```java
pcmPlayer.setVolume(volume, AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH);
```

**swift**

```swift
self.mediaPlayer?.setVolume(volume, type: .playoutAndPublish)
```

**cpp**

```cpp
int ret = player_pcm->setVolume(volume, type);
```

## Play other media files (non\-PCM audio)

> The audio mixing IDs should be consistent if the same audio file is being processed.

### Open a media file

**java**

```java
private void openMedia(String filePath) {
    MediaPlayerConfig playerConfig = new MediaPlayerConfig();
    playerConfig.startPos = 0;
    playerConfig.autoPlay = false;
    playerConfig.playCount = 1; 
    playerConfig.type = AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH;
    playerConfig.callbackOnProgressInterval = 500;
    mediaPlayer.open(filePath, playerConfig);
}
```

**swift**

```swift
let config = ByteRTCMediaPlayerConfig.init()
    config.type = .playoutAndPublish
    config.playCount = 1 
    config.autoPlay = true
    self.mediaPlayer?.open(filePath, config: config)
```

**cpp**

```cpp
bytertc::MediaPlayerConfig config;
config.auto_play = true; 
config.callback_on_progress_interval = 500;
config.play_count = 1;
config.start_pos = 0;
config.sync_progress_to_record_frame = true; 
config.type = bytertc::kAudioMixingTypePlayoutAndPublish;
int ret = player_audio->open(url, config);
```

### Start playback manually

If `open` is already called and `auto_play = false`, you need to call `start` to play music.

**java**

```java
mediaPlayer.start();
```

**swift**

```swift
self.mediaPlayer?.start()
```

**cpp**

```cpp
int ret = player_audio->start();
```

### Stop

Call `stop` to stop playback.

**java**

```java
mediaPlayer.stop()
```

**swift**

```swift
self.mediaPlayer?.stop()
```

**cpp**

```cpp
int ret = player_audio->stop();
```

### Pause/resume

**java**

```java
mediaPlayer.pause()
mediaPlayer.resume()
```

**swift**

```swift
self.mediaPlayer?.pause()
    self.mediaPlayer?.resume()
```

**cpp**

```cpp
int ret = player_audio->pause();
int ret = player_audio->resume();
```

### Get and set media file properties

All settings related to audio mixing, including but not limited to volume setting and starting point setting, are valid only after the music starts and before it stops.

**java**

```java
// Get volume
float volume = mediaPlayer.getVolume();
// Set volume
mediaPlayer.setVolume(value, type);

// Get total duration
    int totalTime = mediaPlayer.getTotalDuration();
// Get playback duration
    int playbackDuration = mediaPlayer.getPlaybackDuration();
    // Get position
    int currentPosition = mediaPlayer.getPosition();
    // Set position
    mediaPlayer.setPosition(position);
    
    // Get audio trackCount
    int trackCount = mediaPlayer.getAudioTrackCount();
    // Select audio track
    mediaPlayer.selectAudioTrack(trackIndex);
    
    // Set playback speed
    mediaPlayer.setPlaybackSpeed(speed);
```

**swift**

```swift
// Get volume
    self.mediaPlayer?.getVolume(.playoutAndPublish)
    // Set volume
    self.mediaPlayer?.setVolume(volume, type: .playoutAndPublish)
    
    // Total file duration in ms
    let totalTime = self.mediaPlayer?.getTotalDuration()
    // Playback duration in ms
    self.mediaPlayer?.getPlaybackDuration()
    // Playback position in ms
    self.mediaPlayer?.getPosition()
    // Set starting playback position in ms
    self.mediaPlayer?.setPosition(position)
    
    // Pitch adjustment, value range [-12, 12]
    self.mediaPlayer?.setAudioPitch(pitch)
    
    // Channel mode
    self.mediaPlayer?.setAudioDualMonoMode(mode)
    
    // Audio tracks
    let tracks = self.mediaPlayer?.getAudioTrackCount()
    
    // Select audio track
    self.mediaPlayer?.selectAudioTrack(trackIndex)
    
    // Set playback speed
    self.mediaPlayer?.setPlaybackSpeed(speed)
```

**cpp**

```cpp
// Get volume
int volume = player_audio->getVolume(type);
// Set volume
int ret = player_audio->setVolume(vol);

// Total file duration in ms
int length = player_audio->getTotalDuration();
// Playback duration in ms
int playback_length = player_audio->getPlaybackDuration();
// Playback position in ms
int pos = player_audio->getPosition(); 
// Set starting playback position in ms
ret = player_audio->setPosition();

// Pitch adjustment, value range [-12, 12]
ret = player_audio->setAudioPitch(pitch);

// Channel mode
ret = player_audio->setAudioDualMonoMode(mode);

// Get audio track count
int count = player_audio->getAudioTrackCount(); 
// Select to play specified audio track
ret = player_audio->selectAudioTrack(index);

// Playback speed in %, value range [50, 200], default value is 100
ret = player_audio->setPlaybackSpeed(speed);
```

## Sample project

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/audio/mixing/AudioMediaMixingActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/AudioManager/AudioMediaMixing/AudioMediaMixingViewController.swift)

## API reference

> Note: The macOS API in the table is for Objective\-C, while the sample project uses the C++ API, which is shared with the Windows SDK.

|Platform |Android |iOS |macOS |Windows |Linux |Electron |Web |
|---|---|---|---|---|---|---|---|
|Initialize music player |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70095#getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getmediaplayer) |[getAudioMixingManager](https://docs.byteplus.com/en/docs/12/docs-104478#getaudiomixingmanager) |
|Music mixing management class |[IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#imediaplayer) |[ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#bytertcmediaplayer) |[ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70092#bytertcmediaplayer) |[IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-imediaplayer) |[MediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#imediaplayer) |[RTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer) |[AudioMixingManager](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager) |
|Music player state callback |[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerstatechanged) |[onMediaPlayerStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCMediaPlayerEventHandler-onmediaplayerstatechanged-state-error) |[onMediaPlayerStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCMediaPlayerEventHandler-onmediaplayerstatechanged-state-error) |[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerstatechanged) |[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerstatechanged) |[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerstatechanged) |Not supported |
|Music playback progress callback |[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |[onMediaPlayerPlayingProgress:progress:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCMediaPlayerEventHandler-onmediaplayerplayingprogress-progress) |[onMediaPlayerPlayingProgress:progress:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCMediaPlayerEventHandler-onmediaplayerplayingprogress-progress) |[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) |Not supported |

## Change log

1. From client\-side SDK 3.32, channel settings of music files are supported.

2. From client\-side SDK 3.36, mixing of online audio files is supported across the platform.

3. From client\-side SDK 3.38, playing speed adjustment of audio files used during audio and video calls is supported.

4. Starting with client\-side SDK v3.45.4, you can get the actual playback duration of mixed audio files, which excludes time spent paused, skipped, or stalled.

5. From client\-side SDK 3.52, mixed audio files of 24 kHz mp3 are supported. For versions previous to 3.52, only audio files of the following sampling rates are supported: 8 kHz, 16 kHz, 22.05 kHz, 32 kHz, 44.1 kHz, 48 kHz, 64 kHz, 96 kHz, and 192 kHz.

6. From client\-side SDK 3.54, all original audio mixing classes on the Native platform are deprecated, replaced by separate sound and music mixing classes, which can be controlled independently.
