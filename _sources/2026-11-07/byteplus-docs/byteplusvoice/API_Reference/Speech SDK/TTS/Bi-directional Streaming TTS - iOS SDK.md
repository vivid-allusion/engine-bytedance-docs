---
title: "Bi-directional Streaming TTS - iOS SDK"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/bi-ttsiossdk"
---

The [WebSocket-based bidirectional streaming TTS API](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts) enables **low\-latency, real\-time text\-to\-speech synthesis** through streaming text input and streaming audio output. It supports multiple languages and dialects, making it suitable for real\-time interactive scenarios. This guide describes how to integrate the **iOS SDK**.

# SDK Version

**iOS：** `pod 'SpeechEngineToB', '0.0.15.0'`

```Objective-C
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'

//Net The SDK depends on SocketRocket 0.6.1 by default. If your project uses a different version of SocketRocket, simply update the dependency to the appropriate version.
pod 'SocketRocket', '0.6.1'
pod 'SpeechEngineToB', '0.0.15.0'
```

# Demo

Mainly refer to `BiTTSViewController`.

[SpeechDemoiOS_bp.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260727120241-882014018141.zip)

# Compatibility

|Category |Compatible Range |
|---|---|
|System |iOS 12.0 and above |
|Architecture |armv7，arm64，x86_64 |
|Network |Mobile data and Wi\-Fi |

# Integration Flow

## Prepare Environment Dependencies

Call this before creating the Speech SDK engine instance to complete network environment and related dependency configuration. Only needs to be executed once within the APP lifecycle.

```Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    return [SpeechEngine prepareEnvironment];
}
```

## Create Engine Instance

The Speech SDK obtains instances in the following way:

```Objective-C
// Create instance
self.engine = [[SpeechEngine alloc] init];
// Add engine delegate, callback methods need to be implemented
[self.engine createEngineWithDelegate:self];
```

## Parameter Configuration

### Required Configuration

```Objective-C
// [Required] Engine Name
[self.curEngine setStringParam:SE_BITTS_ENGINE forKey:SE_PARAMS_KEY_ENGINE_NAME_STRING];
// [Required] Authentication. If using the new console, this configuration is required.
// API Key can be obtained from the console.
[self.curEngine setStringParam:@"your-api-key" forKey:SE_PARAMS_KEY_API_KEY_STRING];
// [Required] Authentication: AppId. For authentication method details, see the documentation.
[self.curEngine setStringParam:self.ttsAppId forKey:SE_PARAMS_KEY_APP_ID_STRING];
// [Required] Authentication: Token. For authentication method details, see the documentation.
[self.curEngine setStringParam:ttsAppToken forKey:SE_PARAMS_KEY_APP_TOKEN_STRING];
// [Required] TTS service domain
[self.curEngine setStringParam:@"wss://voice.ap-southeast-1.bytepluses.com"
                        forKey:SE_PARAMS_KEY_TTS_ADDRESS_STRING];
// [Required] TTS service URI
[self.curEngine setStringParam:@"/api/v3/tts/bidirection"
                        forKey:SE_PARAMS_KEY_TTS_URI_STRING];
// [Required] TTS model service Resource ID.
// Options:
//   seed-tts-2.0: Seed Speech TTS Model 2.0, supports using preset voices
//   seed-icl-2.0: Seed Speech Voice Cloning Model 2.0, supports voices cloned via the Voice Cloning API
[self.curEngine setStringParam:resourceId forKey: SE_PARAMS_KEY_RESOURCE_ID_STRING];
// [Required] StartSession payload, specifying audio generation parameters (excluding the text to be synthesized)
[self.curEngine setStringParam:startPayload forKey:SE_PARAMS_KEY_START_ENGINE_PAYLOAD_STRING];
```

### Optional Configuration

```Objective-C
// [Optional] Local log file path. The SDK will generate a log file named speech_sdk.log
// in this folder path. Set during development, disable in production.
[self.engine setStringParam:@"existing_folder_path_or_empty_string" forKey:SE_PARAMS_KEY_DEBUG_PATH_STRING];
// [Optional] Log level. Set to TRACE (lowest level) during development, set to WARN in production.
[self.engine setStringParam:SE_LOG_LEVEL_TRACE forKey:SE_PARAMS_KEY_LOG_LEVEL_STRING];
// [Optional] Custom request headers
[self.curEngine setStringParam:headerStr forKey:SE_PARAMS_KEY_REQUEST_HEADERS_STRING];
// [Optional] Whether to use the SDK built-in player to play synthesized audio. Default is true.
[self.curEngine setBoolParam:[self.settings getBool:SETTING_TTS_ENABLE_PLAYER]
                          forKey:SE_PARAMS_KEY_TTS_ENABLE_PLAYER_BOOL];
// [Optional] Whether to have the SDK return player PCM audio data via callback. Default is disabled.
// When enabled, the SDK will stream audio data back.
// SEPlayerStartPlayAudio / SEPlayerFinishPlayAudio indicate playback start/end for the current sentence.
// SEPlayerAudioData indicates streaming PCM audio data.
[self.curEngine setBoolParam:[self.settings getBool:SETTING_ENABLE_PLAYER_AUDIO_CALL_BACK] ? SETtsDataCallbackModeAll : SETtsDataCallbackModeNone forKey:SE_PARAMS_KEY_ENABLE_PLAYER_AUDIO_CALLBACK_BOOL];
// [Optional] Whether to save synthesized audio to device.
// When set to true, PARAMS_KEY_TTS_AUDIO_PATH_STRING must be correctly configured.
[self.curEngine setBoolParam:[self.settings getBool:SETTING_TTS_ENABLE_DUMP] forKey:SE_PARAMS_KEY_TTS_ENABLE_DUMP_BOOL];
// [Optional] TTS audio file save path. If not empty, the SDK will save player audio to this path in .wav format.
[self.curEngine setStringParam:self.debugPath forKey:SE_PARAMS_KEY_TTS_AUDIO_PATH_STRING];
// [Optional] TTS connection timeout
[self.curEngine setIntParam:10000 forKey:SE_PARAMS_KEY_TTS_CONN_TIMEOUT_INT];
```

## Initialize Engine Instance

Initialize the engine object and set callback listeners.

```Objective-C
// Initialize engine instance
SEEngineErrorCode ret = [self.engine initEngine];
if (ret != SENoError) {
    NSLog(@"Initialization failed, return value: %d", ret);
    return;
}
```

## Send Directives

The Speech SDK triggers various operations through the `sendDirective` interface. Note that it is not recommended to call this interface from the SDK's callback thread.

### Start Engine

For StartEngine parameters, refer to the StartSession command parameters in the protocol [documentation](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts).

```Objective-C
// Note: call synchronous stop first to avoid issues with SDK internal asynchronous threads
[self.engine sendDirective:SEDirectiveSyncStopEngine];

// Start BiTTS engine
SEEngineErrorCode ret = [self.engine sendDirective:SEDirectiveStartEngine data: startSessionPayload];
if (ret != SENoError) {
    NSLog(@"Send directive say hello failed: %d", ret);
    return;
}
```

**startSessionPayload parameter example**, including voice and audio synthesis parameters:

```JSON
"{\"user\":{\"uid\":\"YOURUID\"},\"req_params\":{\"speaker\":\"zh_female_vv_uranus_bigtts\",\"audio_params\":{\"loudness_rate\":50}}}"
```

> **Note**

> Starting the BiTTS engine only completes the connection. It does not initiate StartSession. Before starting synthesis, you must first call `[self.curEngine sendDirective:SEDirectiveEventStartSession data:@""]`

### Start Synthesis\-StartSession

Bidirectional Streaming TTS supports calling `StartSession` and `FinishSession` multiple times within a single connection. Each call represents starting and ending the synthesis service. However, you must wait for the `SessionFinished` callback before calling `StartSession` again (StartEngine \-\> [FinishSession \-\> StartSession] (can be called in a loop) \-\> StopEngine).

When calling `StartSession`, the `data` field can be set in two ways:

* **Pass an empty string**: Uses the startSessionPayload parameters passed during SEDirectiveStartEngine for synthesis.

* **Pass new JSON\-formatted session payload parameters**: Updates synthesis parameters and synthesizes text with the new parameters.

```Objective-C
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveEventStartSession data:@""];
// Or pass updated new parameters
//SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveEventStartSession data:startSessionPayload];
if (ret != SENoError) {
    NSLog(@"Send directive say Start Session failed: %d", ret);
    return;
}
```

### End Synthesis\-FinishSession

If there is no more text to synthesize, or you need to force an end, call FinishSession to have the server complete audio synthesis based on the received text and return it.

> **Note**

> If the transmitted text does not end with punctuation, the server will wait for subsequent text before triggering synthesis. If no subsequent text is received within 4 seconds, synthesis will also be triggered. If you want the server to start synthesis immediately, call FinishSession.

```Objective-C
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveEventFinishSession data:@""];
if (ret != SENoError) {
    NSLog(@"Send directive Finish Session failed: %d", ret);
    return;
}
```

### Send text to synthesis

Text content needs to be assembled into a JSON\-formatted string before passing in. Additional parameters can be forwarded to the server.

```Objective-C
NSString* taskRequestJson = [NSString stringWithFormat: @"{\"req_params\":{\"text\":\"%@\"}}", text];
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveEventTaskRequest data:taskRequestJson];
if (ret != SENoError) {
    NSLog(@"Send directive Task Request failed: %d", ret);
    return;
}
```

You can call SEDirectiveEventTaskRequest multiple times to send text content to be synthesized to the server. The server will segment and return results one by one. If you need audio content returned immediately, call StartSession and FinishSession before and after sending SEDirectiveEventTaskRequest to ensure audio is returned right away.

### Cancel Synthesis\-CancelSession

To cancel the current synthesis service and stop the server from returning audio, call CancelSession.

```Objective-C
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveEventCancelSession data:@""];
if (ret != SENoError) {
    NSLog(@"Send directive Finish Session failed: %d", ret);
    return;
}
```

### Pause Playback

Send the SEDirectivePausePlayer directive during audio playback to pause TTS audio playback.

```Objective-C
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectivePausePlayer];
NSLog(@"Pause playback status: %d", ret);
```

### Resume Playback

Send the SEDirectiveResumePlayer directive during audio playback to resume TTS audio playback.

```Objective-C
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveResumePlayer];
NSLog(@"Resume playback status: %d", ret);
```

### Stop Engine

```Objective-C
// Will wait for callback function to complete execution. Must not be executed in the callback thread.
[self.engine sendDirective:SEDirectiveSyncStopEngine];
```

## Handle Callbacks

After starting the engine, the SDK will continuously callback messages. For callback message content, refer to the protocol [documentation](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts).

```Objective-C
- (void)onMessageWithType:(SEMessageType)type andData:(NSData *)data {
    NSLog(@"Message Type: %d.", type);
    NSString *strData = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
    switch (type) {
        case SEEngineStart:
            // Callback: Engine started successfully
            NSLog(@"Callback: Engine started: %@", strData);
            break;
        case SEEngineStop:
            // Callback: Engine stopped. After engine starts successfully,
            // this message is guaranteed to occur and is the last callback message.
            NSLog(@"Callback: Engine stopped: %@", strData);
            break;
        case SEEngineError:
            // Callback: Error message
            NSLog(@"Callback: Error: %d, data: %@", type, strData);
            break;
        case SEEventConnectionStarted:
            NSLog(@"Callback: SEEventConnectionStarted");
            break;
        case SEEventConnectionFailed:
            NSLog(@"Callback: SEEventConnectionFailed");
            break;
        case SEEventConnectionFinished:
            NSLog(@"Callback: SEEventConnectionFinished");
            break;
        case SEEventSessionStarted:
            NSLog(@"Callback: SEEventSessionStarted");
            break;
        case SEEventSessionCanceled:
            NSLog(@"Callback: SEEventSessionCanceled");
            break;
        case SEEventSessionFinished:
            NSLog(@"Callback: SEEventSessionFinished");
            break;
        case SEEventSessionFailed:
            NSLog(@"Callback: SEEventSessionFailed");
            break;
        case SEEventTTSSentenceStart:
            NSLog(@"Callback: Synthesis SentenceStart: %@", data);
            break;
        case SEEventTTSSentenceEnd:
            NSLog(@"Callback: Synthesis SentenceEnd: %@", data);
        case SEEventTTSResponse:
            NSLog(@"Callback: Received synthesized audio TTSResponse: %@", data);
        case SEEventTTSEnded:
            NSLog(@"Callback: TTSEnd: %@", data);
        case SEPlayerAudioData:
            NSLog(@"Callback: Player PCM audio: %@", data);
            break;
        case SEPlayerStartPlayAudio:
            NSLog(@"Callback: Started playing current sentence TTS audio");
            break;
        case SEPlayerFinishPlayAudio:
            NSLog(@"Callback: Finished playing current sentence TTS audio");
            break;        
        default:
            break;
    }
}
```

## Destroy Engine Instance

When voice interaction is no longer needed, it is recommended to destroy the engine instance to release memory resources.

> **Important**

> Be sure to call StopEngine before destroyEngine.

```Objective-C
// Will execute SYNC_STOP internally. Must not be executed in the callback thread.
[self.engine destroyEngine];
self.engine = nil;
```
