---
title: "Bi-directional Streaming TTS - Android SDK"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/bi-ttsandroidsdk"
---

The [WebSocket-based bidirectional streaming TTS API](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts) enables **low\-latency, real\-time text\-to\-speech synthesis** through streaming text input and streaming audio output. It supports multiple languages and dialects, making it suitable for real\-time interactive scenarios. This guide describes how to integrate the **Android SDK**.

# SDK Version

**Android: ** `com.bytedance.speechengine:speechengine_tob: 0.0.15.0`

```Java
// Speech Engine
implementation 'com.bytedance.speechengine:speechengine_tob:0.0.15.0'
// Net  The SDK depends on OkHttp 4.9.1 by default. If your project uses a different version of OkHttp, simply update the dependency to the appropriate version.
implementation("com.squareup.okhttp3:okhttp:4.9.1")
```

# Demo

Mainly refer to `BiTtsActivity`.

[SpeechDemoAndroid_bp.zip](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260727120936-248236830720.zip)

# Compatibility

|Category |Compatible Range |
|---|---|
|System |Minimum supported: Android 4.4 and above, API LEVEL 19 |
|Architecture |armeabi\-v7a，arm64\-v8a |
|Network |Mobile data and Wi\-Fi |

# AndroidManifest.xml

```Java
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

# ProGuard Rules

```Java
-keep class com.bytedance.speech.speechengine.SpeechEngineImpl {*;}
```

# Integration Flow

## Prepare Environment Dependencies

Call this before creating the Speech SDK engine instance to set up dependencies such as the network environment. You only need to do this **once** during the app lifecycle.

```Java
SpeechEngineGenerator.PrepareEnvironment(getApplicationContext(), getApplication());
```

## Create an Engine Instance

```Java
mSpeechEngine = SpeechEngineGenerator.getInstance();
mSpeechEngine.createEngine();
```

## Configure Parameters

#### Required Configuration

#### ```Java
// [Optional] Engine Name
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_ENGINE_NAME_STRING,SpeechEngineDefines.BITTS_ENGINE);
// [Optional] Local log file path. The SDK will generate a log file named speech_sdk.log
// in this folder path. Set during development, disable in production.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_DEBUG_PATH_STRING, "existing_folder_path_or_empty_string");
// [Optional] Log level. Set to TRACE (lowest level) during development, set to WARN in production.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_LOG_LEVEL_STRING, SpeechEngineDefines.LOG_LEVEL_TRACE);
// [Required] Authentication. If using the new console, this configuration is required.
// API Key can be obtained from the console.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_API_KEY_STRING, "your-api-key");
// [Required] Authentication: AppId. For authentication method details, see the documentation.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_APP_ID_STRING, "APPID");
// [Required] Authentication: Token. For authentication method details, see the documentation.
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_APP_TOKEN_STRING, "ACCESS TOKEN");
// [Required] TTS service domain
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_TTS_ADDRESS_STRING, "wss://voice.ap-southeast-1.bytepluses.com");
// [Required] TTS service URI
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_TTS_URI_STRING, "/api/v3/tts/bidirection");
// [Required] TTS model service Resource ID.
// Options:
//   seed-tts-2.0: Seed Speech TTS Model 2.0, supports using preset voices
//   seed-icl-2.0: Seed Speech Voice Cloning Model 2.0, supports voices cloned via the Voice Cloning API
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_RESOURCE_ID_STRING, "RESOURCE ID");
// [Required] Audio-related parameters passed during StartSession for the TTS service, in JSON string format
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_START_ENGINE_PAYLOAD_STRING,startSessionPayload);
```


<span id="h1HA6C5V"></span>
#### Optional Configuration

```Java
// [Optional] TTS service connection timeout
mSpeechEngine.setOptionInt(SpeechEngineDefines.PARAMS_KEY_TTS_CONN_TIMEOUT_INT,100000);
// [Optional] Whether to save synthesized audio to device.
// When set to true, PARAMS_KEY_TTS_AUDIO_PATH_STRING must be correctly configured.
mSpeechEngine.setOptionBoolean(SpeechEngineDefines.PARAMS_KEY_TTS_ENABLE_DUMP_BOOL,true);
// [Optional] TTS audio file save directory.
// Must be created before synthesis and the APP must have access permissions.
// Saved audio file name format: tts_{reqid}.wav, where {reqid} is the request ID for this synthesis.
// [Required] when PARAMS_KEY_TTS_ENABLE_DUMP_BOOL is set to true, otherwise [Optional].
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_TTS_AUDIO_PATH_STRING, mDebugPath);
// [Optional] Additional parameters for the Header section of TTS service requests
mSpeechEngine.setOptionString(SpeechEngineDefines.PARAMS_KEY_REQUEST_HEADERS_STRING,"{}");
// [Optional] Whether to use the built-in player to play TTS audio
mSpeechEngine.setOptionBoolean(SpeechEngineDefines.PARAMS_KEY_TTS_ENABLE_PLAYER_BOOL,true);
// [Optional] Whether to enable the player's data callback
mSpeechEngine.setOptionBoolean(SpeechEngineDefines.PARAMS_KEY_ENABLE_PLAYER_AUDIO_CALLBACK_BOOL,true);
```

## Initialize the Engine Instance

Initialize the engine object and register callbacks.

```Java
// Initialize engine instance
int ret = engine.initEngine();
if (ret != SpeechEngineDefines.ERR_NO_ERROR) {
    Log.e(SpeechDemoDefines.TAG, "Initialization Failed: " + ret);
    return;
}
engine.setContext(getApplicationContext());
engine.setListener(this);
```

## Send Directives

The Speech SDK triggers various operations through the `sendDirective` interface. Note that it is **not recommended** to call this interface from the SDK's callback thread.

### Start Engine

For StartEngine parameters, refer to the upstream event \-\> StartSession parameter description in the protocol [documentation](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts).

```Java
// Note: call synchronous stop first to avoid issues with SDK internal asynchronous threads
engine.sendDirective(SpeechEngineDefines.DIRECTIVE_SYNC_STOP_ENGINE, "");
// Start BiTTS engine
int ret = engine.sendDirective(SpeechEngineDefines.DIRECTIVE_START_ENGINE, startSessionPayload);
if (ret != SpeechEngineDefines.ERR_NO_ERROR) {
    Log.e(SpeechDemoDefines.TAG, "Start failed, return value: " + ret);
    return;
}
```

An example of `startSessionPayload` (including speaker and audio generation parameters):

```Java
"{\"user\":{\"uid\":\"YOURUID\"},\"req_params\":{\"speaker\":\"zh_female_vv_uranus_bigtts\",\"audio_params\":{\"loudness_rate\":50}}}"
```

### Start Synthesis Service\-StartSession

Bidirectional Streaming TTS supports calling `StartSession` and `FinishSession` multiple times within a single connection. Each call represents starting and ending the synthesis service. However, you must wait for the `SessionFinished` callback before calling `StartSession` again (StartEngine \-\> [FinishSession \-\> StartSession] (can be called in a loop) \-\> StopEngine).

The `data` field of `StartSession` can be set in two ways:

* Empty string: use the startSessionPayload provided when starting the engine.

* A new JSON session payload: update synthesis parameters and synthesize with the new parameters.

```Java
int ret = 0;
ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_EVENT_START_SESSION,"");
// Or pass updated new parameters
//ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_EVENT_START_SESSION,startSessionPayload);
if(ret!=0){
    Log.e(SpeechDemoDefines.TAG, "Send StartSession failed: " + ret);
    String message = "Failed to send StartSession directive, " + ret;
    sendSynthesisDirectiveFailed(message);
}
```

### End Synthesis Service\-FinishSession

If there is no more text to synthesize, or you need to force an end, call FinishSession to have the server complete audio synthesis based on the received text and return it.

> **Note**

> If the transmitted text does not end with punctuation, the server will wait for subsequent text before triggering synthesis. If no subsequent text is received within 4 seconds, synthesis will also be triggered. If you want the server to start synthesis immediately, call FinishSession.

```Java
int ret = 0;
ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_EVENT_FINISH_SESSION, "");
if(ret!=0){
    Log.e(SpeechDemoDefines.TAG, "Send FinishSession failed: " + ret);
    String message = "Failed to send FinishSession directive, " + ret;
    sendSynthesisDirectiveFailed(message);
}
```

### Send Text to Synthesize

The text must be assembled into a JSON\-formatted string.

```Java
String result = "{\"req_params\":{\"text\":\"" + text + "\"}}";
int ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_EVENT_TASK_REQUEST, result);
if (ret != 0) {
    Log.e(SpeechDemoDefines.TAG, "Synthesis failed: " + ret);
    String message = "Failed to send synthesis directive, " + ret;
    sendSynthesisDirectiveFailed(message);
}
```

You can call DIRECTIVE_EVENT_TASK_REQUEST multiple times to send text content to be synthesized to the server. The server will segment and return results one by one. If you need audio content returned immediately, call StartSession and FinishSession before and after sending DIRECTIVE_EVENT_TASK_REQUEST to ensure audio is returned right away.

### Cancel Synthesis Service\-CancelSession

To cancel the current synthesis service and stop the server from returning audio, call CancelSession.

```Java
int ret = 0;
ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_EVENT_CANCEL_SESSION, "");
if(ret!=0){
    Log.e(SpeechDemoDefines.TAG, "Send CancelSession failed: " + ret);
    String message = "Failed to send CancelSession directive, " + ret;
    sendSynthesisDirectiveFailed(message);
}
```

### Pause Playback

Send the DIRECTIVE_PAUSE_PLAYER directive during audio playback to pause TTS audio playback.

```Java
int ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_PAUSE_PLAYER, "");
Log.d(SpeechDemoDefines.TAG, "Pause playback status:" + ret);
```

### Resume Playback

Send the DIRECTIVE_RESUME_PLAYER directive during audio playback to resume TTS audio playback.

```Java
int ret = mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_RESUME_PLAYER, "");
Log.d(SpeechDemoDefines.TAG, "Resume playback status:" + ret);
```

### Stop Engine

```Java
// Will wait for callback function to complete execution. Must not be executed in the callback thread.
mSpeechEngine.sendDirective(SpeechEngineDefines.DIRECTIVE_SYNC_STOP_ENGINE, "");
```

## Handle Callbacks

After starting the engine, the SDK will continuously callback messages. For callback message content, refer to the protocol [documentation](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts).

```Java
@Override
public void onSpeechMessage(int type, byte[] data, int len) {
    String stdData = "";
    stdData = new String(data);

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
        case SpeechEngineDefines.MESSAGE_TYPE_EVENT_TTS_SENTENCE_START:
            // Callback: Synthesis started
            Log.e(SpeechDemoDefines.TAG, "Callback: TTS_SENTENCE_START: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_EVENT_TTS_SENTENCE_END:
            // Callback: Synthesis ended
            Log.e(SpeechDemoDefines.TAG, "Callback: TTS_SENTENCE_END: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_EVENT_TTS_RESPONSE:
            Log.e(SpeechDemoDefines.TAG, "Callback: TTS_RESPONSE: data len " + stdData.length());
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_EVENT_TTS_ENDED:
            Log.e(SpeechDemoDefines.TAG, "Callback: TTSEnded: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_PLAYER_AUDIO_DATA:
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_PLAYER_START_PLAY_AUDIO:
            // Callback: Playback started
            Log.e(SpeechDemoDefines.TAG, "Callback: Playback started: " + stdData);
            break;
        case SpeechEngineDefines.MESSAGE_TYPE_PLAYER_FINISH_PLAY_AUDIO:
            // Callback: Playback ended
            Log.e(SpeechDemoDefines.TAG, "Callback: Playback ended: " + stdData);
            break;
        default:
            break;
    }
}
```

## Destroy the Engine Instance

When the Speech SDK is no longer needed, it is recommended to destroy the engine instance to release memory resources.

> **Important**

> *Make sure to call StopEngine before calling destroyEngine.*

```Java
// Will execute SYNC_STOP internally. Must not be executed in the callback thread.
mSpeechEngine.destroyEngine();
mSpeechEngine = null;
```
