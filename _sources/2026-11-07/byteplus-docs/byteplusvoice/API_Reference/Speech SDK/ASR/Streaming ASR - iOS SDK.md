---
title: "Streaming ASR - iOS SDK"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/sauciossdk"
---

Based on the [Seed Speech Streaming ASR model](https://docs.byteplus.com/en/docs/byteplusvoice/asrstreaming), this SDK supports streaming audio input and streaming recognition result output with low latency. It is suitable for real\-time speech recognition scenarios, covering multiple languages and dialects. Below is the iOS SDK integration guide for developers.

# SDK Version

**iOS：** `pod 'SpeechEngineToB', '0.0.15.0'`

```Objective-C
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'

# Net: 0.6.1 is the default network library dependency version.
# If you need a different version, reference the corresponding SocketRocket version.
pod 'SocketRocket', '0.6.1'
pod 'SpeechEngineToB', '0.0.15.0'
```

# Demo

Main reference: `BigAsrViewController`

[SpeechDemoiOS_bp.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260727114435-1492097833443.zip)

# Compatibility

|**Category** |**Compatible Range** |
|---|---|
|System |Minimum supported: iOS 12.0 |
|Architecture |armv7, arm64, x86_64 |
|Network |Mobile data and Wi\-Fi |

# Integration Flow

## Initialize Environment Dependencies

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
self.curEngine = [[SpeechEngine alloc] init];
// Add engine delegate, callback methods need to be implemented
[self.curEngine createEngineWithDelegate:self];
```

## Parameter Configuration

### Required Configuration

```Objective-C
// [Required] Engine Name
[self.curEngine setStringParam:SE_ASR_ENGINE forKey:SE_PARAMS_KEY_ENGINE_NAME_STRING];

// [Required] Authentication. If using the new console, this configuration is required.
// API Key can be obtained from the console.
[self.curEngine setStringParam:@"your-api-key" forKey:SE_PARAMS_KEY_API_KEY_STRING];

// [Required] Authentication: AppId. For authentication method details, see the documentation.
[self.curEngine setStringParam:self.ttsAppId forKey:SE_PARAMS_KEY_APP_ID_STRING];

// [Required] Authentication: Token. For authentication method details, see the documentation.
[self.curEngine setStringParam:ttsAppToken forKey:SE_PARAMS_KEY_APP_TOKEN_STRING];

// [Required] Recognition service domain
[self.curEngine setStringParam:@"wss://voice.ap-southeast-1.bytepluses.com" forKey:SE_PARAMS_KEY_ASR_ADDRESS_STRING];

// [Required] Recognition service URI
[self.curEngine setStringParam:@"/api/v3/sauc/bigmodel_nostream" forKey:SE_PARAMS_KEY_ASR_URI_STRING];

// [Required] Speech recognition model service Resource ID.
// Options:
//   volc.bigasr.sauc.duration: Seed Speech Streaming ASR Model 1.0 
//   volc.seedasr.sauc.duration: Seed Speech Streaming ASR Model 2.0 
[self.curEngine setStringParam:[self.settings getString:SETTING_RESOURCE_ID] forKey:SE_PARAMS_KEY_RESOURCE_ID_STRING];

// [Required] Protocol type. BigAsr protocol must be set to Seed.
[self.curEngine setIntParam:SEProtocolTypeSeed forKey:SE_PARAMS_KEY_PROTOCOL_TYPE_INT];

// [Required] Configure audio source
[self.curEngine setStringParam:[self getRecorderType] forKey:SE_PARAMS_KEY_RECORDER_TYPE_STRING];
```

#### Audio Source

The Speech Recognition SDK supports the built\-in recorder, external PCM stream, or audio file as input. The configuration values are:

* `SE_RECORDER_TYPE_RECORDER` — Built\-in recorder

* `SE_RECORDER_TYPE_STREAM` — External PCM stream

* `SE_RECORDER_TYPE_FILE` — PCM format audio file

```Objective-C
// [Required] Use built-in recorder. Default: mono, 16K sample rate, 16-bit depth.
[self.curEngine setStringParam:SE_RECORDER_TYPE_RECORDER forKey:SE_PARAMS_KEY_RECORDER_TYPE_STRING];

// [Optional] External PCM stream.

[self.curEngine setStringParam:SE_RECORDER_TYPE_STREAM
                        forKey:SE_PARAMS_KEY_RECORDER_TYPE_STRING];

[self.curEngine setBoolParam:TRUE
                      forKey:SE_PARAMS_KEY_ENABLE_RESAMPLER_BOOL];
[self.curEngine setIntParam:[self.streamRecorder getSampleRate]
                     forKey:SE_PARAMS_KEY_CUSTOM_SAMPLE_RATE_INT];
[self.curEngine setIntParam:[self.streamRecorder getChannel]
                     forKey:SE_PARAMS_KEY_CUSTOM_CHANNEL_INT];
                     
// [Optional] File input.
NSString *filePath = [self.debugPath stringByAppendingPathComponent:@"asr_rec_file.pcm"];
[self.curEngine setStringParam:filePath
                        forKey:SE_PARAMS_KEY_RECORDER_FILE_STRING];
```

```Objective-C
// [Optional] Whether to return recording volume
[self.curEngine setBoolParam:TRUE forKey:SE_PARAMS_KEY_ENABLE_GET_VOLUME_BOOL];
```

Set the maximum recording duration. When the set time is reached, the audio end packet will be sent and the system will wait for the ASR result:

```Objective-C
// [Optional] Maximum recording duration. Default: 60000ms.
// If your usage scenario exceeds 60s, modify this value. -1 means no limit on recording duration.
[self.curEngine setIntParam:60000 forKey:SE_PARAMS_KEY_VAD_MAX_SPEECH_DURATION_INT];
```

### Optional Configuration

```Objective-C
// [Optional] Debug & Log: Local log file path. The SDK will generate a log file named
// speech_sdk.log in this folder path. Set during development, disable in production.
[self.curEngine setStringParam:self.debugPath forKey:SE_PARAMS_KEY_DEBUG_PATH_STRING];

// [Optional] Log level. Set to DEBUG during development, set to WARN in production.
[self.curEngine setStringParam:SE_LOG_LEVEL_DEBUG forKey:SE_PARAMS_KEY_LOG_LEVEL_STRING];

// [Optional] UID & deviceID: Used for troubleshooting online issues.
[self.curEngine setStringParam:SDEF_UID forKey:SE_PARAMS_KEY_UID_STRING];
[self.curEngine setStringParam:self.deviceID forKey:SE_PARAMS_KEY_DEVICE_ID_STRING];

// [Optional] Recording file save path. If configured, the SDK will save recordings
// to this path in .wav format.
[self.curEngine setStringParam:self.debugPath forKey:SE_PARAMS_KEY_ASR_REC_PATH_STRING];

// [Optional] Connection and receive timeout for online requests.
// Generally no need to configure, default values are sufficient. Unit: milliseconds.
[self.curEngine setIntParam:3000 forKey:SE_PARAMS_KEY_ASR_CONN_TIMEOUT_INT];
[self.curEngine setIntParam:5000 forKey:SE_PARAMS_KEY_ASR_RECV_TIMEOUT_INT];

// [Optional] Number of reconnection attempts after disconnection.
// Default is 0. Set to a value greater than 0 to enable reconnection.
[self.curEngine setIntParam:[self.settings getInt:SETTING_ASR_MAX_RETRY_TIMES] forKey:SE_PARAMS_KEY_ASR_MAX_RETRY_TIMES_INT];

// [Optional] Audio sample rate. Default: 16000
[self.curEngine setIntParam:[self.settings getInt:SETTING_SAMPLE_RATE] forKey:SE_PARAMS_KEY_SAMPLE_RATE_INT];

// [Optional] Audio channel count. Default: 1. Options: 1 or 2.
[self.curEngine setIntParam:[self.settings getInt:SETTING_CHANNEL] forKey:SE_PARAMS_KEY_CHANNEL_NUM_INT];

// [Optional] Audio channel count uploaded to server. Default: 1. Options: 1 or 2.
// Generally keep consistent with SE_PARAMS_KEY_CHANNEL_NUM_INT.
[self.curEngine setIntParam:[self.settings getInt:SETTING_CHANNEL] forKey:SE_PARAMS_KEY_UP_CHANNEL_NUM_INT];

// [Optional] When audio source is RECORDER_TYPE_STREAM and input audio sample rate
// is not 16K, enable SDK internal resampling.
[self.curEngine setBoolParam:TRUE forKey:SE_PARAMS_KEY_ENABLE_RESAMPLER_BOOL];

// [Optional] Set resampling input sample rate to the actual sample rate of the APP layer input audio.
[self.curEngine setIntParam:[self.streamRecorder getSampleRate] forKey:SE_PARAMS_KEY_CUSTOM_SAMPLE_RATE_INT];
[self.curEngine setIntParam:[self.streamRecorder getChannel] forKey:SE_PARAMS_KEY_CUSTOM_CHANNEL_INT];

// [Optional] Whether to return recording volume. Enable when APP needs to display audio waveform.
[self.curEngine setBoolParam:[self.settings getBool:SETTING_GET_VOLUME] forKey:SE_PARAMS_KEY_ENABLE_GET_VOLUME_BOOL];

// [Optional] Enable system built-in Acoustic Echo Cancellation (AEC).
// When enabled, ASR recognition will not pick up TTS audio.
// Note: This is not an SDK-provided feature; effectiveness depends on the underlying system and hardware.
[self.curEngine setBoolParam:TRUE forKey:SE_PARAMS_KEY_ENABLE_AEC_BOOL];

// [Optional] Set recognition language (audio-level parameter), e.g., zh-CN, en-US, etc.
[self.curEngine setStringParam:@"zh-CN" forKey:SE_PARAMS_KEY_ASR_LANGUAGE_STRING];

// [Optional] Whether to output speech pause, sentence segmentation, and word segmentation
// information (utterance info). Default: disabled.
// Note: When enabled, you also need to set show_utterances to True in the
// Large Model ASR request parameters for it to take effect.
[self.curEngine setBoolParam:TRUE forKey:SE_PARAMS_KEY_ASR_SHOW_UTTER_BOOL];
```

## Large Model ASR Parameter Configuration

Large Model ASR related parameters need to be passed via SE_PARAMS_KEY_ASR_REQ_PARAMS_STRING. Below is an example of setting VAD sentence segmentation and hotword table; other parameters follow the same pattern. Details can be found in the [API documentation](https://docs.byteplus.com/en/docs/byteplusvoice/asrstreaming).

```Objective-C
// The final value passed to the SDK should be a JSON string like this:

{
  "model_name": "bigmodel",
  "output_zh_variant": "traditional",
  "enable_channel_split": true,
  "enable_ddc": true,
  "enable_speaker_info": false,
  "enable_punc": true,
  "enable_itn": false,
  "show_utterances": true,
  "sensitive_words_filter": "{\"system_reserved_filter\":true,\"filter_with_empty\":[\"八\"],\"filter_with_signed\":[\"岭\"]}",
  "corpus": {
    "context": "{\"hotwords\":[{\"word\":\"one\"},{\"word\":\"two\"}],\"context_type\":\"dialog_ctx\",\"context_data\":[{\"text\":\"text1\"},{\"image_url\":\"image_url\"},{\"text\":\"text2\"},{\"text\":\"text3\"},{\"text\":\"text4\"}]}"
  }
}

// If this value is written directly as an Objective-C string, quotes must be escaped:
NSString *reqParamsJsonString = @"{\"model_name\":\"bigmodel\",\"output_zh_variant\":\"traditional\",\"enable_channel_split\":true,\"enable_ddc\":true,\"enable_speaker_info\":false,\"enable_punc\":true,\"enable_itn\":false,\"show_utterances\":true,\"sensitive_words_filter\":\"{\\\"system_reserved_filter\\\":true,\\\"filter_with_empty\\\":[\\\"八\\\"],\\\"filter_with_signed\\\":[\\\"岭\\\"]}\",\"corpus\":{\"context\":\"{\\\"hotwords\\\":[{\\\"word\\\":\\\"one\\\"},{\\\"word\\\":\\\"two\\\"}],\\\"context_type\\\":\\\"dialog_ctx\\\",\\\"context_data\\\":[{\\\"text\\\":\\\"text1\\\"},{\\\"image_url\\\":\\\"image_url\\\"},{\\\"text\\\":\\\"text2\\\"},{\\\"text\\\":\\\"text3\\\"},{\\\"text\\\":\\\"text4\\\"}]}\"}}";
[self.curEngine setStringParam:reqParamsJsonString
                        forKey:SE_PARAMS_KEY_ASR_REQ_PARAMS_STRING];
                        
// Note: `SE_PARAMS_KEY_ASR_REQ_PARAMS_STRING` receives the request parameter object itself. Do not wrap this example with another `"request"` object unless the SDK page explicitly requires it. Fields such as `sensitive_words_filter`, `correct_words`, `context`, and other nested JSON fields are passed as JSON strings. Convert the inner JSON to a string first, then escape it when writing an Objective-C string literal.
 
```

> **Note**: To output speech pause, sentence segmentation, and word segmentation information, you must first set SE_PARAMS_KEY_ASR_SHOW_UTTER_BOOL to true.

## Initialize Engine Instance

Initialize the engine object and set callback listeners.

```Objective-C
// Initialize engine instance
SEEngineErrorCode ret = [self.curEngine initEngine];
if (ret == SENoError) {
    NSLog(@"Initialization successful");
} else {
    NSLog(@"Initialization failed, return value: %d", ret);
}
```

## Send Directives

The Speech SDK triggers various operations through the sendDirective interface. Note that it is not recommended to call this interface from the SDK's callback thread.

### Start Engine

Call the SYNC_STOP directive before starting the engine to ensure the previous request has ended.

```Objective-C
// Note: call synchronous stop first to avoid issues with SDK internal asynchronous threads
SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveSyncStopEngine];
if (ret != SENoError) {
    NSLog(@"Send directive syncstop failed: %d", ret);
} else {
    // Start ASR engine
    NSLog(@"Starting engine.");
    SEEngineErrorCode ret = [self.curEngine sendDirective:SEDirectiveStartEngine];
    if (ret == SERecCheckEnvironmentFailed) {
        NSLog(@"No recording permission");
    }
}
```

> **Note**: When the audio source is RECORDER_TYPE_STREAM, you need to start the APP layer recorder yourself before starting the engine. When the audio source is FILE, you need to set the audio file path:

```Objective-C
// [Required] when using audio file recognition, otherwise not needed.
NSString *file_path = [NSString stringWithFormat:@"%@/%@", self.debugPath, @"asr_rec_file.pcm"];
NSLog(@"Input audio file path: %@", file_path);
[self.curEngine setStringParam:file_path forKey:SE_PARAMS_KEY_RECORDER_FILE_STRING];
```

### End Audio Input\-FinishTalking

For press\-to\-talk mode, call FinishTalking after release to end audio input and wait for the final recognition result.

```Objective-C
// Directive: End user audio input
[self.curEngine sendDirective:SEDirectiveFinishTalking];
```

### Stop Engine

```Objective-C
// Stop engine (asynchronous)
[self.curEngine sendDirective:SEDirectiveStopEngine];
```

## Handle Callbacks

After starting the engine, the SDK will continuously return messages via callbacks.

```Objective-C
- (void)onMessageWithType:(SEMessageType)type andData:(NSData *)data {
    NSLog(@"Message Type: %d.", type);
    switch (type) {
        case SEEngineStart:
            // Callback: Engine started successfully
            NSLog(@"Callback: Engine started successfully");
            break;
        case SEEngineStop:
            // Callback: Engine stopped
            NSLog(@"Callback: Engine stopped");
            break;
        case SEEngineError:
            // Callback: Error message
            NSLog(@"Callback: Error: %@", data);
            break;
        case SEConnectionConnected:
            // Callback: Connection established successfully
            NSLog(@"Callback: Connection established successfully");
            break;
        case SEAsrPartialResult:
            // Callback: Partial result for current ASR request
            NSLog(@"Callback: Partial result for current ASR request");
            [self speechEngineResult:data isFinal:FALSE];
            break;
        case SEFinalResult:
            // Callback: Final result for current ASR request
            NSLog(@"Callback: Final result for current ASR request");
            [self speechEngineResult:data isFinal:TRUE];
            break;
        case SEVolumeLevel:
            // Callback: Recording volume
            NSLog(@"Callback: Recording volume，%.3f", [[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding] floatValue]);
            break;
        default:
            break;
    }
}

// Callback: Server logid when connection is established, useful for troubleshooting
- (void)onSpeechLogid:(NSString *)logid {
    NSLog(@"Callback: logid: %@", logid);
}
```

### Callback Message Reference

|**Message Type** |**Description** |
|---|---|
|SEEngineStart |Engine started successfully |
|SEEngineStop |Engine stopped |
|SEEngineError |Error message |
|SEConnectionConnected |Connection established successfully |
|SEAsrPartialResult |Partial result for current ASR request (during real\-time recognition) |
|SEFinalResult |Final result for current ASR request |
|SEVolumeLevel |Recording volume. Requires `SE_PARAMS_KEY_ENABLE_GET_VOLUME_BOOL` to be enabled |
|onSpeechLogid |Server logid when connection is established, useful for troubleshooting |

## Destroy Engine Instance

When speech recognition is no longer needed, it is recommended to destroy the engine instance to release memory resources.

```Objective-C
// Will execute SYNC_STOP internally. Must not be executed in the callback thread.
[self.curEngine destroyEngine];
self.curEngine = nil;
```
