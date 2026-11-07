---
title: "Live Interpretation - API guide"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/liveinterpretationapi"
---

<span id="wlWMWKlP"></span>
# Overview

This document describes how to access the Seed Live Interpretation large model service over WebSocket in real time. The API supports speech\-to\-text translation (S2T) and speech\-to\-speech translation (S2S) modes. 

<span id="8zfy8ssr"></span>
## Supported modes and language codes


|**Mode** |**Notes** |**Language configuration** |**Supported languages** |**Count** |
|---|---|---|---|---|
|Speech\-to\-Text (S2T) |Returns translated text only. |* Specify both source and target languages.<br><br>* One side of the language pair must be Chinese (`zh`) or English (`en`): <br><br>   * supported language → `zh`/`en`<br><br>   * `zh`/`en `→ supported language<br><br>* Dialects are supported **only as source** languages.<br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260701072031-273938574057.png) </span><br><br> |* Languages:<br><br><br>`zh` Chinese<br><br>`en` English <br><br>`pt` Portuguese<br><br>`es` Spanish<br><br>`ja` Japanese<br><br>`id` Indonesian<br><br>`de` German<br><br>`fr` French<br><br>`ru` Russian<br><br>`it` Italian<br><br>`ko` Korean<br><br>`ar` Arabic<br><br>`tr` Turkish<br><br>`ms` Malay<br><br>`vi` Vietnamese<br><br>`th` Thai<br><br>`nl` Dutch<br><br>`ro` Romanian<br><br>`pl` Polish<br><br>`cs` Czech<br><br><br>* Dialects: <br><br><br>`yue-CN` Cantonese <br><br>`sh-CN` Shanghainese |20  languages<br><br>2 dialects<br><br> |
|Speech\-to\-Speech (S2S) |The target language can be broadcasted with supported TTS voices or ICL voices. ||||


<span id="Y8QrpLQI"></span>
## Request path


* The request path is: `voice.ap-southeast-1.bytepluses.com/api/v4/ast/v2/translate`


<span id="4L1tkwww"></span>
# Authentication

The API supports two authentication methods. Due to the console upgrade, we recommend using the **simplified X\-Api\-Key authentication**.


|**Header** |**Description** |**Type** |**Required** |**Example** |
|---|---|---|---|---|
|X\-Api\-Key |API key obtained from the [BytePlus console](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide). |string |Yes |your\-api\-key |
|X\-Api\-Resource\-Id |Fixed resource ID for this service. |string |Yes |volc.service_type.1000025 |


**Example (Recommended)** 

```Python
headers = {
    "X-Api-Key": "your-api-key",
    "X-Api-Resource-Id": "volc.service_type.1000025"
}
```


**Example (Legacy)** 

```Python
headers = {
    "X-Api-App-Id": "123456789",
    "X-Api-Access-Key": "your-access-key",  
    # the AppID and AccessToken can be retrieved following this console guide. 
    "X-Api-Resource-Id": "volc.service_type.1000025"
}
```


After the WebSocket handshake succeeds, the response headers include `X-Tt-Logid`. Log this value on the client side because it is useful for troubleshooting.


|**Header** |**Description** |**Example** |
|---|---|---|
|X\-Tt\-Logid |Server\-side log ID returned after the handshake. |202407261553070FACFE6D19421815D605 |


<span id="ZE5bxR4t"></span>
# Sample code

<span id="2uLG9Ux5"></span>
## Protobuf

<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260727032018-685838112148.gz" name="protos.tar.gz">protos.tar.gz</Attachment>


The WebSocket connection uses protobuf binary messages.

"protos.tar.gz" contains the original ".proto" protocol definitions. It is language\-neutral. The demos below already contain generated protobuf code, you only need "protos.tar.gz" if you want to regenerate client code, inspect the protocol messages, or create a client for another language.

<span id="sLxpy6iA"></span>
### Client Demo


<Tabs>
<Tab zoneid="ou18GJd0jV" title="Go">
<TabTitle>Go</TabTitle>

1. Download the demo package here. 


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260701035218-672051598812.zip" name="ast_go_bp_demo.zip">ast_go_bp_demo.zip</Attachment>



2. Follow the readme.md file to quickly run a S2T mode zh\-\>en test.


</Tab>
<Tab zoneid="GpRoFpV4aO" title="Python">
<TabTitle>Python</TabTitle>

1. Download the demo package here. 


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260701035319-1666194289774.zip" name="ast_python_bp_demo.zip">ast_python_bp_demo.zip</Attachment>



2. Follow the readme.md file to quickly run a S2T mode zh\-\>en test.


</Tab>
<Tab zoneid="h91r7i6bc3" title="Java">
<TabTitle>Java</TabTitle>

1. Download the demo package here. 


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260701035337-1125658323965.zip" name="ast_java_bp_demo.zip">ast_java_bp_demo.zip</Attachment>



2. Follow the readme.md file to quickly run a S2T mode zh\-\>en test.


</Tab>
</Tabs>


<span id="TbcSxeFv"></span>
# End\-to\-end streaming example

The following example is based on the typical interaction sequence between the client and the live interpretation service.

<span id="kUNDdNgB"></span>
## Sequence diagram

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260701035800-531480825716.png) </span>

<span id="xWcVRmlv"></span>
## Step\-by\-step flow


1. Establish the WebSocket connection with the authentication headers.

2. Send `StartSession` with `request_meta.session_id`, source audio parameters, target audio parameters if `mode=s2s`, source language, target language, and optional glossary or replacement rules.

3. Wait for `SessionStarted`.

4. After `SessionStarted` is received, send `TaskRequest` audio packets continuously. The recommended packet size is about 80 ms of audio.

5. Read service events asynchronously. Source subtitle events, translation subtitle events, and TTS events may arrive interleaved.

6. Optionally send `UpdateConfig` if supported runtime parameters need to be changed during the session.

7. After all audio has been sent, send `FinishSession`.

8. Wait for `SessionFinished` or `SessionFailed`.


<span id="VafIgMXx"></span>
## Event types sent by the client


|**Event** |**Value** |**Description** |
|---|---|---|
|StartSession |100 |Starts a new interpretation session. This must be the first business message after the WebSocket connection is established. |
|TaskRequest |200 |Sends one audio packet. |
|UpdateConfig |201 |Updates configurable parameters during an active session. |
|FinishSession |102 |Ends the current session after all audio has been sent. |


<span id="KMAh5TCb"></span>
## Event types returned by the service


|**Event** |**Value** |**Description** |
|---|---|---|
|SessionStarted |150 |The session has been created successfully. The client can start sending audio only after receiving this event. |
|SourceSubtitleStart |650 |Source subtitle segment starts. |
|SourceSubtitleResponse |651 |Partial or incremental source subtitle text. |
|SourceSubtitleEnd |652 |Source subtitle segment ends. |
|TranslationSubtitleStart |653 |Translation subtitle segment starts. |
|TranslationSubtitleResponse |654 |Partial or incremental translated subtitle text. |
|TranslationSubtitleEnd |655 |Translation subtitle segment ends. |
|TTSSentenceStart |350 |TTS sentence starts. Returned in S2S mode. |
|TTSSentenceEnd |351 |TTS sentence ends. Returned in S2S mode. |
|TTSResponse |352 |TTS audio data. Returned in S2S mode. |
|UsageResponse |154 |Usage and billing information. |
|SessionFinished |152 |The session ended normally. |
|SessionFailed |153 |The session failed. Check response_meta.status_code and response_meta.message. |
|AudioMuted |250 |Silence detected by VAD. |


<span id="t8ZgqvbY"></span>
# Client requests details

<span id="O0r9FDLo"></span>
## Start a session: `StartSession`

After the WebSocket handshake is complete, send `StartSession` as the first business message. The request defines the session ID, user metadata, audio format, translation mode, languages, output audio format, and optional corpus settings.

<span id="lM2xrUbJ"></span>
### Request fields


|**Field** |**Description** |**Level** |**Type** |**Required** |**Notes** |
|---|---|---|---|---|---|
|request_meta |Request metadata. |1 |object |Yes |Contains session\-level metadata. |
|session_id |Session ID. |2 |string |Yes |A UUID is recommended. |
|event |Request event. |1 |enum/int32 |Yes |Use `100` for `StartSession`. |
|user |User metadata. |1 |object |No |Useful for server\-side log filtering. |
|uid |User ID. |2 |string |No |Use a stable user identifier when available. |
|did |Device ID or device name. |2 |string |No |Optional. |
|platform |Operating system and API version. |2 |string |No |Examples: `iOS`, `Android`, `Linux`. |
|sdk_version |SDK version. |2 |string |No |Optional. |
|request |Session configuration. |1 |object |Yes |Translation and TTS settings. |
|mode |Output mode. |2 |string |No |Use `s2t` or `s2s`. |
|speaker_id |Speaker voice ID. |2 |string |Required when `mode=s2s` |Overseas S2S requires a valid speaker ID. Use a supported TTS voice or a cloned voice for output audio. |
|is_custom_speaker |Whether the external voice is a cloned voice. |2 |bool |No |Default: `false`. <br><br>Cloned voices trigger authorization checks. |
|tts_resource_id |TTS resource ID for external voices. |2 |string |Required for TTS or cloned voice paths |Supported values include: <br><br>`seed-tts-1.0`<br><br>`seed-tts-2.0`<br><br>`seed-icl-1.0`<br><br>`seed-icl-2.0` |
|speech_rate |Speech rate. |2 |number |No |Range: `[-50, 100]`. <br><br>`100` means 2.0x speed; `-50 `means 0.5x speed. |
|source_language |Source language code. |2 |string |Yes |See Language codes. |
|target_language |Target language code. |2 |string |Yes |See Language codes. |
|corpus |Custom corpus and intervention terms. |2 |object |No |Only `correct_words `is supported for now. |
|correct_words |Replacement dictionary. |3 |JSON string |No |Used for source and translated subtitle recognition.<br><br>Example:<br><br>`"{\"接受\":\"接收\",\"Accept\":\"Receive\"}"` |
|source_audio |Source audio configuration. |1 |object |Yes |Input audio format. |
|format |Source audio container format. |2 |string |Yes |`wav` only. |
|codec |Source audio codec. |2 |string |No |`raw` only, which means PCM encoding. |
|rate |Source audio sample rate. |2 |int |Yes |Must be `16000`. |
|bits |Source audio bit depth. |2 |int |Yes |Must be `16`. |
|channel |Source audio channel count. |2 |int |Yes |Must be `1` for mono. |
|target_audio |Target audio configuration. |1 |object |Required for S2S |Output audio format. |
|format |Target audio container format. |2 |string |Required for S2S |`pcm` or `ogg_opus` |
|rate |Target audio sample rate. |2 |int |Required for S2S |Default: `24000`. <br><br>Supported values: `16000`, `24000`. <br><br>For ogg_opus, output sample rate is fixed at 48000 regardless of this field. |


<span id="wXFnWElQ"></span>
### Example

```JSON
// request_meta.session_id must be provided
{
  "request_meta": {
    "session_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  },
  "event": "StartSession",
  "user": {
    "uid": "388808088185088",
    "did": "device-id"
  },
  "source_audio": {
    "format": "wav",
    "codec": "raw",
    "rate": 16000,
    "bits": 16,
    "channel": 1
  },
  "target_audio": {
    "format": "pcm",
    "rate": 24000
  },
  "request": {
    "mode": "s2s",
    "speaker_id": "your-valid-speaker-id",
    "is_custom_speaker": false,
    "tts_resource_id": "seed-tts-2.0",
    "speech_rate": 0,
    "source_language": "zh",
    "target_language": "en",
    "corpus": {
      "correct_words": "{\"Accept\":\"Receive\"}",
      }
    }
  }
}
```


<span id="eO6xAzxf"></span>
## Send audio: `TaskRequest`

After the client sends `StartSession`, it must wait for `SessionStarted`. Then the client can send `TaskRequest` messages with audio data.

The audio packet must follow the format declared in `source_audio`. The binary audio data is carried in the protobuf request body. For example, if the client sends 80 ms of audio per packet, the `data` field contains the bytes for that 80 ms chunk.


|**Field** |**Description** |**Level** |**Type** |**Required** |**Notes** |
|---|---|---|---|---|---|
|event |Request event. |1 |enum/int32 |Yes |Use `200` for `TaskRequest`. |
|source_audio |Source audio payload. |1 |object |Yes |Contains audio bytes. |
|data |Audio bytes. |2 |bytes |Yes |16 kHz, 16\-bit, mono WAV/PCM. About 80 ms per packet is recommended. |


```JSON
{
  "event": "TaskRequest",
  "source_audio": {
    "data": "<binary-audio-bytes>"
  }
}
```


<span id="GtsIAH68"></span>
## Finish a session: `FinishSession`

After all audio has been sent, send `FinishSession`. This message does not carry audio data.

```JSON
{
  "event": "FinishSession"
}
```


<span id="i02jRm7l"></span>
# Server responses details

Every client request produces one or more server responses. The response format is defined in protobuf. Important fields are listed below.


|**Field** |**Description** |**Level** |**Type** |**Required** |**Notes** |
|---|---|---|---|---|---|
|response_meta |Response metadata. |1 |object |No |Contains status and billing fields. |
|status_code |Status code. |2 |int |No |Present when status information is returned. |
|message |Error or status message. |2 |string |No |Present when status information is returned. |
|billing |Usage and billing information. |2 |object |No |Returned with `UsageResponse`. |
|duration_msec |Audio duration. |3 |int |No |Unit: milliseconds. |
|items |Usage details. |3 |array |No |Usage item list. |
|unit |Token category. |4 |string |No |Possible values: `output_text_tokens`<br><br>`output_audio_tokens`<br><br>`input_audio_tokens` |
|quantity |Consumed token quantity. |4 |float |No |Usage quantity. |
|event |Response event. |1 |int |No |For example, `SessionStarted` is `150`. |
|text |Recognition or translation text. |1 |string |No |Source text or translated text. |
|data |Binary response data. |1 |bytes |No |TTS audio bytes. |
|start_time |Start timestamp. |1 |int |No |Unit: milliseconds. |
|end_time |End timestamp. |1 |int |No |Unit: milliseconds. |
|spk_chg |Speaker\-change flag. |1 |bool |No |Default: `false`. Set to true when speaker change is detected in `SourceSubtitleStart` or `TranslationSubtitleStart`. |
|muted_duration_ms |Silence duration. |1 |int |No |Unit: milliseconds. Approximate value. |


<span id="X1CHawzL"></span>
## SessionStarted

```JSON
{
  "event": "SessionStarted"
}
```


<span id="4GMQLhQN"></span>
## SourceSubtitleStart

Marks the start of a source subtitle segment.

```JSON
{
  "event": "SourceSubtitleStart",
  "start_time": 1200,
  "spk_chg": false
}
```


<span id="zcV3HPBQ"></span>
## SourceSubtitleResponse

Returns partial or incremental source subtitle text.

```JSON
{
  "event": "SourceSubtitleResponse",
  "text": "Hello, everyone"
}
```


<span id="lAQgYzRV"></span>
## SourceSubtitleEnd

Marks the end of a source subtitle segment.

```JSON
{
  "event": "SourceSubtitleEnd",
  "start_time": 1200,
  "end_time": 2600,
  "text": "Hello, everyone"
}
```


<span id="85eLYS88"></span>
## TranslationSubtitleStart

```JSON
{
  "event": "TranslationSubtitleStart",
  "start_time": 1200,
  "spk_chg": false
}
```


<span id="yspX0PVX"></span>
## TranslationSubtitleResponse

```JSON
{
  "event": "TranslationSubtitleResponse",
  "text": "大家好"
}
```


<span id="pWNbAusp"></span>
## TranslationSubtitleEnd

```JSON
{
  "event": "TranslationSubtitleEnd",
  "start_time": 1200,
  "end_time": 2600,
  "text": "大家好"
}
```


<span id="gEfgbZXi"></span>
## TTSSentenceStart

```JSON
{
  "event": "TTSSentenceStart",
  "start_time": 1200
}
```


<span id="rClZxwhH"></span>
## TTSResponse

Returns TTS audio bytes according to the target_audio configuration.

```JSON
{
  "event": "TTSResponse",
  "data": "<binary-audio-bytes>"
}
```


<span id="oYyMrBuq"></span>
## TTSSentenceEnd

```JSON
{
  "event": "TTSSentenceEnd",
  "start_time": 1200,
  "end_time": 2600
}
```


<span id="NjEHxnWI"></span>
## UsageResponse

```JSON
{
  "event": "UsageResponse",
  "response_meta": {
    "session_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "status_code": 20000000,
    "message": "OK",
    "billing": {
      "items": [
        {
          "unit": "output_text_tokens",
          "quantity": 15.0
        },
        {
          "unit": "output_audio_tokens",
          "quantity": 11.0
        },
        {
          "unit": "input_audio_tokens",
          "quantity": 4.0
        }
      ],
      "duration_msec": 640
    }
  }
}
```


<span id="5sm2VVwF"></span>
## SessionFinished

```JSON
{
  "event": "SessionFinished"
}
```


<span id="CASH5v1L"></span>
## SessionFailed

```JSON
{
  "event": "SessionFailed",
  "response_meta": {
    "status_code": 45000001,
    "message": "Invalid request parameters"
  }
}
```


<span id="5qxgVP6f"></span>
## AudioMuted

When VAD detects silence, the service returns AudioMuted. The first event is usually returned after about 2 seconds of silence. Subsequent events may be returned about once per second while silence continues.

```JSON
{
  "event": "AudioMuted",
  "muted_duration_ms": 2000
}
```


<span id="x69RPk71"></span>
# Error message from server

If the server cannot parse or process the binary or transport protocol, it sends an error message. For example, this can happen if the client uses an unsupported serialization format. Check `response_meta.status_code` and `response_meta.message`for details.

<span id="fPtKj7VK"></span>
## Error codes


|**Code** |**Meaning** |**Description** |
|---|---|---|
|20000000 |Success |The request succeeded. |
|45000001 |Invalid request parameters |Required fields are missing, field values are invalid, or the request is duplicated. |
|45000002 |Empty audio |The request contains no valid audio. |
|45000081 |Packet timeout |The service timed out while waiting for audio packets. |
|45000151 |Invalid audio format |The audio format does not meet the required format. |
|550xxxxx |Internal service error |Internal service processing error. |
|55000031 |Server busy |The service is overloaded and cannot process the request. |
