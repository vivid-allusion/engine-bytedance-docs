---
title: "Streaming ASR - Android SDK"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/saucandroidsdk"
---

Based on the [Seed Speech Streaming ASR model](https://docs.byteplus.com/en/docs/byteplusvoice/asrstreaming), this SDK supports streaming audio input and streaming recognition result output with low latency. It is suitable for real\-time speech recognition scenarios, covering multiple languages and dialects. Below is the Android SDK integration guide for developers.

# SDK Version

**Android:**  `com.bytedance.speechengine:speechengine_tob: 0.0.15.0`

```Java
// Speech Engine
implementation 'com.bytedance.speechengine:speechengine_tob:0.0.15.0'
// Net: okhttp:4.9.1 is the default network library dependency version.
// If you need a different version, reference the corresponding okhttp version.
implementation("com.squareup.okhttp3:okhttp:4.9.1")
```

# Demo

Main reference: `BigAsrActivity`

[SpeechDemoAndroid_bp.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260727111228-1211701161988.zip)

# Compatibility

|**Category** |**Compatible Range** |
|---|---|
|System |Minimum supported: Android 4.4 and above, API LEVEL 19 |
|Architecture |armeabi\-v7a, arm64\-v8a |
|Network |Mobile data and Wi\-Fi |

# AndroidManifest.xml

```XML
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

# ProGuard Rules

```Plain Text
-keep class com.bytedance.speech.speechengine.SpeechEngineImpl {*;}
```

# Integration flow

## Initialize Environment Dependencies

Call this before creating the Speech SDK engine instance to complete network environment and related dependency configuration. This initialization only needs to be performed once during the app lifecycle.

```Java
SpeechEngineGenerator.PrepareEnvironment(getApplicationContext(), getApplication());
```

## Create Engine Instance

```Java
mSpeechEngine = SpeechEngineGenerator.getInstance();
mSpeechEngine.createEngine();
mSpeechEngine.setContext(getApplicationContext());
```

## Parameter Configuration

### Required Configuration

```Java
// [Required] Engine Name
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_ENGINE_NAME_STRING, SpeechEngineDefines.ASR_ENGINE);

// [Required] Authentication. If using the new console, this configuration is required.
// API Key can be obtained from the console.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_API_KEY_STRING, "your-api-key");

// [Required] Authentication: AppId. For authentication method details, see the documentation.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_APP_ID_STRING, "APPID");

// [Required] Authentication: Token. For authentication method details, see the documentation.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_APP_TOKEN_STRING, "ACCESS TOKEN");

// [Required] Speech recognition service domain
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_ASR_ADDRESS_STRING, "wss://voice.ap-southeast-1.bytepluses.com");

// [Required] Recognition service URI
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_ASR_URI_STRING, "/api/v3/sauc/bigmodel_async");

// [Required] Speech recognition model service Resource ID.
// Options:
//   volc.bigasr.sauc.duration: Seed Speech Streaming ASR Model 1.0 
//   volc.seedasr.sauc.duration: Seed Speech Streaming ASR Model 2.0 
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_RESOURCE_ID_STRING, "RESOURCE ID");

// [Required] Protocol type. BigAsr protocol must be set to Seed.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_PROTOCOL_TYPE_INT, SpeechEngineDefines.PROTOCOL_TYPE_SEED);

// [Required] Configure audio source
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_RECORDER_TYPE_STRING, SpeechEngineDefines.RECORDER_TYPE_RECORDER);
```

#### Audio Source

The Speech Recognition SDK supports the built\-in recorder, external PCM audio stream, or audio file as input. The configuration values are:

* `SpeechEngineDefines.RECORDER_TYPE_RECORDER` — SDK Built\-in recorder

* `SpeechEngineDefines.RECORDER_TYPE_STREAM` — External PCM audio stream

* `SpeechEngineDefines.RECORDER_TYPE_FILE` — PCM format audio file

```Java
// [Required] Default: use system built-in recorder
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_RECORDER_TYPE_STRING, SpeechEngineDefines.RECORDER_TYPE_RECORDER);
 
// [Optional] External PCM stream:
mSpeechEngine.setOptionString(
        SpeechEngineDefines.PARAMS_KEY_RECORDER_TYPE_STRING,
        SpeechEngineDefines.RECORDER_TYPE_STREAM);

// If the input stream is not 16 kHz mono, enable resampling.
mSpeechEngine.setOptionBoolean(
        SpeechEngineDefines.PARAMS_KEY_ENABLE_RESAMPLER_BOOL,
        true);
mSpeechEngine.setOptionInt(
        SpeechEngineDefines.PARAMS_KEY_CUSTOM_SAMPLE_RATE_INT,
        customSampleRate);
mSpeechEngine.setOptionInt(
        SpeechEngineDefines.PARAMS_KEY_CUSTOM_CHANNEL_INT,
        customChannelCount);

// Start your APP-layer recorder before START_ENGINE.

// [Optional] File input
mSpeechEngine.setOptionString(
        SpeechEngineDefines.PARAMS_KEY_RECORDER_TYPE_STRING,
        SpeechEngineDefines.RECORDER_TYPE_FILE);
mSpeechEngine.setOptionString(
        SpeechEngineDefines.PARAMS_KEY_RECORDER_FILE_STRING,
        "/absolute/path/to/asr_rec_file.pcm");
```

```Java
// [Optional] Whether to return recording volume
engine.setOptionBoolean(engineHandler, SpeechEngineDefines.PARAMS_KEY_ENABLE_GET_VOLUME_BOOL, mEnableGetVolume);
```

Set the maximum recording duration. When the set time is reached, the audio end packet will be sent and the system will wait for the ASR result:

```Java
// [Optional] Maximum recording duration. Default: 60000ms.
// If your usage scenario exceeds 60s, modify this value. -1 means no limit on recording duration.
engine.setOptionInt(engineHandler, SpeechEngineDefines.PARAMS_KEY_VAD_MAX_SPEECH_DURATION_INT, 60000);
```

### Optional Configuration

```Java
// [Optional] Local log file path. The SDK will generate a log file named speech_sdk.log
// in this folder path. Set during development, disable in production.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_DEBUG_PATH_STRING, "existing_folder_path_or_empty_string");

// [Optional] Log level. Set to DEBUG during development, set to WARN in production.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_LOG_LEVEL_STRING, SpeechEngineDefines.LOG_LEVEL_DEBUG);

// [Optional] User ID (to assist in troubleshooting online user issues)
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_UID_STRING, "YOUR_UID");

// [Optional] Recording file save path. If configured, the SDK will save recordings
// to this path in .wav format.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_ASR_REC_PATH_STRING, mDebugPath);

// [Optional] Connection and receive timeout for online requests.
// Generally no need to configure, default values are sufficient. Unit: milliseconds.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_ASR_CONN_TIMEOUT_INT, 3000);
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_ASR_RECV_TIMEOUT_INT, 5000);

// [Optional] Number of reconnection attempts after disconnection.
// Default is 0. Set to a value greater than 0 to enable reconnection.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_ASR_MAX_RETRY_TIMES_INT, 0);

// [Optional] Audio sample rate. Default: 16000
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_SAMPLE_RATE_INT, 16000);

// [Optional] Audio channel count. Default: 1. Options: 1 or 2.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_CHANNEL_NUM_INT, 1);

// [Optional] Audio channel count uploaded to server. Default: 1. Options: 1 or 2.
// Generally keep consistent with PARAMS_KEY_CHANNEL_NUM_INT.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_UP_CHANNEL_NUM_INT, 1);

// [Optional] When audio source is RECORDER_TYPE_STREAM and input audio sample rate
// is not 16K, enable SDK internal resampling.
mSpeechEngine.setOptionBoolean(SpeechEngineDefines.PARAMS_KEY_ENABLE_RESAMPLER_BOOL, true);

// [Optional] Set resampling input sample rate to the actual sample rate of the APP layer input audio.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_CUSTOM_SAMPLE_RATE_INT, customSampleRate);
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_CUSTOM_CHANNEL_INT, customChannelCount);

// [Optional] Whether to return recording volume. Enable when APP needs to display audio waveform.
mSpeechEngine.setOptionBoolean(SpeechEngineDefines.PARAMS_KEY_ENABLE_GET_VOLUME_BOOL, false);

// [Optional] Recording preset mode. Set to VOICE_COMMUNICATION to enable
// system built-in Acoustic Echo Cancellation (AEC).
// Note: This is not an SDK-provided feature; effectiveness depends on the underlying system and hardware.
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_RECORDER_PRESET_INT, SpeechEngineDefines.RECORDER_PRESET_VOICE_COMMUNICATION);

// [Optional] Set recognition language (audio-level parameter), e.g., zh-CN, en-US, etc.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_ASR_LANGUAGE_STRING, "zh-CN");

// [Optional] Whether to output speech pause, sentence segmentation, and word segmentation
// information (utterance info). Default: disabled.
// Note: When enabled, you also need to set show_utterances to True in the
// Large Model ASR request parameters for it to take effect.
mSpeechEngine.setOptionBoolean(SpeechEngineDefines.PARAMS_KEY_ASR_SHOW_UTTER_BOOL, true);
```

## Large Model ASR Parameter Configuration

Large Model ASR related parameters need to be passed via `PARAMS_KEY_ASR_REQ_PARAMS_STRING`. Below is an example of setting VAD sentence segmentation and hotword table; other parameters follow the same pattern. Details can be found in the [API documentation](https://docs.byteplus.com/en/docs/byteplusvoice/asrstreaming).

```Java
// The final value passed to the server should be a JSON string like this:

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

// If this value is written directly as a Java string, quotes must be escaped:

String reqParamsJsonString = "{\"model_name\":\"bigmodel\",\"output_zh_variant\":\"traditional\",\"enable_channel_split\":true,\"enable_ddc\":true,\"enable_speaker_info\":false,\"enable_punc\":true,\"enable_itn\":false,\"show_utterances\":true,\"sensitive_words_filter\":\"{\\\"system_reserved_filter\\\":true,\\\"filter_with_empty\\\":[\\\"八\\\"],\\\"filter_with_signed\\\":[\\\"岭\\\"]}\",\"corpus\":{\"context\":\"{\\\"hotwords\\\":[{\\\"word\\\":\\\"one\\\"},{\\\"word\\\":\\\"two\\\"}],\\\"context_type\\\":\\\"dialog_ctx\\\",\\\"context_data\\\":[{\\\"text\\\":\\\"text1\\\"},{\\\"image_url\\\":\\\"image_url\\\"},{\\\"text\\\":\\\"text2\\\"},{\\\"text\\\":\\\"text3\\\"},{\\\"text\\\":\\\"text4\\\"}]}\"}}";
mSpeechEngine.setOptionString(
        SpeechEngineDefines.PARAMS_KEY_ASR_REQ_PARAMS_STRING,
        reqParamsJsonString);

// Note: `PARAMS_KEY_ASR_REQ_PARAMS_STRING` receives the request parameter object itself. Do not wrap this example with another `"request"` object unless the SDK page explicitly requires it. Fields such as `sensitive_words_filter`, `correct_words`, `context`, and other nested JSON fields are passed as JSON strings. Convert the inner JSON to a string first, then escape it when writing a Java string literal.
```

> **Note:**  To output speech pause, sentence segmentation, and word segmentation information, you must first set PARAMS_KEY_ASR_SHOW_UTTER_BOOL to true.

## Initialize Engine Instance

Initialize the engine object and set callback listeners.

```Java
// Initialize engine instance
int ret = mSpeechEngine.initEngine();
if (ret != SpeechEngineDefines.ERR_NO_ERROR) {
    Log.e(SpeechDemoDefines.TAG, "Initialization failed, return value: " + ret);
    return;
}
mSpeechEngine.setListener(this);
```

## Send Directives

The Speech SDK triggers various operations through the sendDirective interface. Note that it is not recommended to call this interface from the SDK's callback thread.

### Start Engine

Call the SYNC_STOP directive before starting the engine to ensure the previous request has ended.

```Java
// Note: call synchronous stop first to avoid issues with SDK internal asynchronous threads
mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_SYNC_STOP_ENGINE, "");

// Start ASR engine
int ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_START_ENGINE, "");
if (ret == SpeechEngineDefines.ERR_REC_CHECK_ENVIRONMENT_FAILED) {
    Log.e(SpeechDemoDefines.TAG, "No recording permission");
} else if (ret != SpeechEngineDefines.ERR_NO_ERROR) {
    Log.e(SpeechDemoDefines.TAG, "Start failed, return value: " + ret);
    return;
}
```

> **Note**: When the audio source is RECORDER_TYPE_STREAM, you need to start the APP layer recorder yourself before starting the engine. When the audio source is FILE, you need to set the audio file path:

```Java
// [Required] when using audio file recognition, otherwise not needed.
String test_file_path = mDebugPath + "/asr_rec_file.pcm";
Log.d(SpeechDemoDefines.TAG, "Input audio file path: " + test_file_path);
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_RECORDER_FILE_STRING, test_file_path);
```

### End audio input\-FinishTalking

For press\-to\-talk mode, call FinishTalking after release to end audio input and wait for the final recognition result.

```Java
// Directive: End user audio input
mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_FINISH_TALKING, "");
```

### Stop Engine

```Java
// Stop engine (asynchronous)
mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_STOP_ENGINE, "");
```

## Handle Callbacks

After starting the engine, the SDK continuously delivers messages through the callback.

```Java
@Override
public void onSpeechMessage(int type, byte[] data, int len) {
    String stdData = new String(data);
    switch (type) {
        case SpeechEngineDefines.MESSAGE_TYPE_ENGINE_START:
            // Callback: Engine started successfully
            Log.i(SpeechDemoDefines.TAG, "Callback: Engine started: data: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_ENGINE_STOP:
            // Callback: Engine stopped
            Log.i(SpeechDemoDefines.TAG, "Callback: Engine stopped: data: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_ENGINE_ERROR:
            // Callback: Error message
            Log.e(SpeechDemoDefines.TAG, "Callback: Error: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_CONNECTION_CONNECTED:
            // Callback: Connection established successfully
            Log.i(SpeechDemoDefines.TAG, "Callback: Connection established: data: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_PARTIAL_RESULT:
            // Callback: Partial result for current ASR request
            Log.d(SpeechDemoDefines.TAG, "Callback: ASR partial result: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_FINAL_RESULT:
            // Callback: Final result for current ASR request
            Log.i(SpeechDemoDefines.TAG, "Callback: ASR final result: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_VOLUME_LEVEL:
            // Callback: Recording volume
            Log.d(SpeechDemoDefines.TAG, "Callback: Recording volume");
            break;
        default:
            break;
    }
}

// Callback: Server logid when connection is established, useful for troubleshooting
@Override
public void onSpeechLogid(String logid) {
    Log.d(SpeechDemoDefines.TAG, "Callback: logid: " + logid);
}
```

### Callback Message Reference

|**Message Type** |**Description** |
|---|---|
|MESSAGE_TYPE_ENGINE_START |Engine started successfully |
|MESSAGE_TYPE_ENGINE_STOP |Engine stopped |
|MESSAGE_TYPE_ENGINE_ERROR |Error message |
|MESSAGE_TYPE_CONNECTION_CONNECTED |Connection established successfully |
|MESSAGE_TYPE_PARTIAL_RESULT |Partial result for current ASR request (during real\-time recognition) |
|MESSAGE_TYPE_FINAL_RESULT |Final result for current ASR request |
|MESSAGE_TYPE_VOLUME_LEVEL |Recording volume. Requires PARAMS_KEY_ENABLE_GET_VOLUME_BOOL to be enabled |
|onSpeechLogid |Server logid when connection is established, useful for troubleshooting |

## Destroy Engine Instance

When speech recognition is no longer needed, it is recommended to destroy the engine instance to release memory resources.

```Java
// Will execute SYNC_STOP internally. Must not be executed in the callback thread.
mSpeechEngine.destroyEngine();
mSpeechEngine = null;
```
