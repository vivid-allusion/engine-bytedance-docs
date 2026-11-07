---
title: "Text to Speech (Doubao Speech 2.0)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/text-to-speech-doubao-speech-2-0"
---

`las_tts` is a synchronous streaming text\-to\-speech operator. After the caller submits the complete text, the API returns audio frames, subtitle frames, and a finish event through `text/event-stream`. The default resource is Doubao Text\-to\-Speech 2.0.

# Operator introduction

> Operator ID: `las_tts`

## Application scenarios

* Narration, customer\-service announcements, course audio, and content dubbing.

* Online synthesis scenarios that need low\-latency audio frames.

## Core capabilities

* Text to speech: synthesize speech from input text.

* Multiple resource versions: supports `seed-tts-2.0` (default) and `seed-tts-1.0` for text\-to\-speech, and `seed-icl-2.0` and `seed-icl-1.0` for voice cloning. The selected speaker must match the resource version.

* Audio controls: configure format, sample rate, bitrate, speed, and volume.

* Subtitles and timestamps: return sentence\-level subtitles or word\-level timestamps on supported resources.

## Effect display

The following examples are intended for short\-drama narration. They use the same English narration and male voice, add dramatic pauses through SSML, and adjust speech rate, volume, and pitch to generate narration for different editing rhythms. All four examples output MP3 audio and enable subtitle timestamps.

* Actual input SSML text

   ```xml
   <speak>
   Last night, the Sterling mansion went dark for exactly nine minutes.
   <break time="700ms"/>
   When the lights came back, the family heirloom was gone, and every security camera had been wiped clean.
   <break time="900ms"/>
   Emily was the only one who stayed in the east wing.
   <break time="500ms"/>
   She said she heard footsteps behind the locked gallery door, then a voice whispering her name.
   <break time="800ms"/>
   But the old butler noticed something no one else did.
   <break time="600ms"/>
   The broken window was staged from the inside, and the muddy footprints led back into the house.
   <break time="900ms"/>
   Now, as the family gathers for the reading of the will, Emily must decide whether to expose the truth, or protect the person who betrayed her first.
   <break time="800ms"/>
   Outside, the rain begins again. In the reflection of the dining room glass, Emily sees a second envelope hidden beneath her father portrait.
   <break time="600ms"/>
   It carries no signature, only a warning written in silver ink: tell the truth tonight, or the next disappearance will not be a jewel.
   <break time="900ms"/>
   The room falls silent as she reaches for the envelope. Every guest watches her hand, but only one of them already knows what is inside.
   </speak>
   ```

* **Standard narration**

   * Use case: Standard short\-drama narration

   * Parameters: Speech rate `0`, volume `0`, pitch `0`

   * Duration: Approximately 67 seconds

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/c252cd91-164d-4c00-adba-dd0a2a853be8.mp3)

* **Quick preview**

   * Use case: Fast\-paced short videos

   * Parameters: Speech rate `20`, volume `0`, pitch `0`

   * Duration: Approximately 53 seconds

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/e0de2545-0f8e-4d49-ad71-c88c216fc143.mp3)

* **Gentle suspense**

   * Use case: Suspenseful openings or emotional buildup

   * Parameters: Speech rate `-10`, volume `-15`, pitch `-2`

   * Duration: Approximately 70 seconds

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/a5ab0475-0294-4a08-8444-c2f9e8a54344.mp3)

* **Dramatic trailer**

   * Use case: Trailer\-style highlight edits

   * Parameters: Speech rate `5`, volume `15`, pitch `2`

   * Duration: Approximately 57 seconds

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/74186647-4795-42df-8bb6-f55240823b14.mp3)

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Breakdown item |Performance impact |
|---|---|
|Response mode |The Process API streams audio frames, subtitle or timestamp frames, and a finish event through SSE. |

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |Text |
|Input format: Text |* Content: `req_params.text` is required.<br><br>* SSML: The current BytePlus unidirectional HTTP API does not support SSML.<br><br>* Voice configuration: `req_params.speaker` and `req_params.audio_params` are required. The selected speaker must match `resource_id`. |
|Input path requirements |No file path is required. Submit the text through `POST /api/v1/process`, set `data.stream=true`, and continue reading the SSE response until `[DONE]`. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |* Audio<br><br>* Text (subtitles or timestamps on supported resources) |
|Output format: Audio |* Format: `mp3`, `ogg_opus`, `pcm`, or `wav`.<br><br>* Sample rate: 8,000, 16,000, 22,050, 24,000, 32,000, 44,100, or 48,000 Hz.<br><br>* Streaming: PCM is recommended because WAV chunks contain repeated file headers. Base64\-decode audio chunks and concatenate them in arrival order. |
|Output format: Text |Subtitle or timestamp frames are returned when supported by the selected resource. |
|Output path requirements |No output storage path is required. The Process API returns audio frames, subtitle or timestamp frames, and a finish event through an SSE stream. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Synthesized text characters. |
   |Billing type |Usage\-based billing in `USD/10K characters`. |
   |Unit price |4.5 USD/10K characters. |

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Process

### Interface description

Synchronously submit a text\-to\-speech request and receive audio frames, subtitle frames, and a finish event through SSE. Callers should set `data.stream=true` and keep consuming events until `[DONE]`.

The response example lists SSE events in arrival order as an array, with each `data` JSON string decoded and expanded into an object, followed by the `[DONE]` marker. The API sends individual SSE messages, and the actual `data` field is a string that the client parses a second time.

Encode extension fields inside the JSON string `req_params.additions`. Common fields are listed below; availability depends on the voice and resource. See the [BytePlus HTTP reference](https://docs.byteplus.com/en/docs/byteplusvoice/unidirectional_tts_http) for the full specification.

|Field inside additions |Type |Description |
|---|---|---|
|silence_duration |integer |Trailing silence in milliseconds; default 0, range 0 to 30000. |
|disable_default_bit_rate |boolean |Set true to use bit rates below 64000 bit/s, such as 16000 or 32000. |
|disable_markdown_filter |boolean |Default false. When true, parse and filter Markdown syntax. |
|explicit_language |string |Synthesis language, such as zh\-cn or en; must match the input text and voice language support. |
|context_texts |array |Voice\-style instructions for TTS 2.0 voices only. The instruction text is not billed. Only the first instruction in the array is effective. |
|tone_fidelity |boolean |Default false. ICL 2.0 only: reproduce the reference voice and speaking style. Input text must use the reference audio language. |
|post_process.pitch |integer |Pitch adjustment; default 0, range \-12 to 12. |
|enable_language_detector |boolean |Automatic language detection; default false. |
|enable_latex_tn |boolean |Set true to enable LaTeX reading. Also set disable_markdown_filter=true. |

Each SSE message has a data field containing a JSON string. Parse it a second time, Base64\-decode audio chunks separately, and concatenate the bytes in arrival order. Process sentence as subtitle/timestamp information; if a frame contains both audio and subtitles, handle both. An inner code=20000000 followed by [DONE] confirms complete synthesis.

### Request parameters

**operator_id** string 必选 `Example value: las_tts`

Operator ID, fixed to las_tts.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed to v1.

**data** tts_data 必选

Text, voice, and audio configuration.

**stream** boolean `Optional` `Example value: true`

Defaults to false. Set true to receive complete audio, subtitles, and the finish frame. Omitted or false returns only the first frame.

**resource_id** string `Optional` `Example value: seed-tts-2.0`

Defaults to seed\-tts\-2.0. Values: seed\-tts\-1.0 (TTS 1.0), seed\-tts\-2.0 (TTS 2.0), seed\-icl\-1.0 (ICL 1.0), or seed\-icl\-2.0 (ICL 2.0). Must match speaker. LAS currently does not accept the upstream legacy aliases volc.service_type.1000009 and volc.megatts.default; use the corresponding seed resource ID.

**user** tts_user `Optional`

Optional caller information; uid is defined by the caller.

**uid** string `Optional` `Example value: user_001`

Caller user identifier.

**req_params** tts_req_params 必选

Synthesis parameters, including text, voice, and audio settings.

**text** string 必选 `Example value: Welcome to Doubao Text-to-Speech.`

Input text. The current BytePlus unidirectional HTTP API does not support SSML.

**speaker** string 必选 `Example value: en_female_stokie_uranus_bigtts`

Voice ID; must match the resource version and input language. See the [BytePlus voice list](https://docs.byteplus.com/en/docs/byteplusvoice/tts-voice-list).

**audio_params** tts_audio_params 必选

Output audio settings, nested inside req_params. Missing values produce Parameter.Invalid.

**format** string `Optional` `Example value: mp3`

Defaults to mp3; choices are mp3, ogg_opus, and pcm. Use pcm for streaming. wav is accepted but may return repeated WAV headers, making direct concatenation unsuitable.

**sample_rate** integer `Optional` `Example value: 24000`

Sample rate in Hz; default 24000. Values: 8000, 16000, 22050, 24000, 32000, 44100, 48000.

**bit_rate** integer `Optional` `Example value: 64000`

Bit rate in bit/s; explicitly set it for MP3 and OGG. The default allowed range is 64000 to 160000. Values below 64000, such as 16000 or 32000, require disable_default_bit_rate=true in additions. For pcm/wav, bitrate depends on sample rate, bit depth, and channel count.

**emotion** string `Optional` `Example value: angry`

Supported by some voices only; values depend on the voice list, for example angry.

**emotion_scale** integer `Optional` `Example value: 4`

Used with emotion. Range 1 to 5, default 4; intensity does not necessarily increase linearly.

**speech_rate** integer `Optional` `Example value: 0`

Speech rate; default 0, range \-50 to 100. \-50 means 0.5x speed; 100 means 2x speed.

**loudness_rate** integer `Optional` `Example value: 0`

Volume; default 0, range \-50 to 100. \-50 means 0.5x volume; 100 means 2x volume.

**enable_subtitle** boolean `Optional` `Example value: true`

Default false. Returns word and phoneme timestamps in sentence for Chinese/English TTS 2.0 and ICL 2.0 voices.

**enable_timestamp** boolean `Optional` `Example value: false`

Default false. Returns word and phoneme timestamps for Chinese/English TTS 1.0 and ICL 1.0 voices.

**additions** string 必选 `Example value: {"silence_duration":500}`

A JSON string for extensions, for example "{"silence_duration":500}". Use "{}" when no extensions are needed. Do not pass a JSON object.

### Response parameters

**metadata** tts_metadata

Common metadata for each SSE response object.

**task_status** string `Example value: RUNNING`

Always RUNNING for normal frames, including the finish frame. Detect completion through the inner finish event and SSE [DONE].

**business_code** string `Example value: 0`

0 for normal frames. See the error table for failures.

**error_msg** string

Empty for normal frames; contains error details on failure.

**request_id** string `Example value: <request-id>`

Request identifier for troubleshooting.

**data** string `Example value: {"code":0,"data":"<base64-audio-chunk>"}`

JSON string containing the inner event; parse it a second time. For code=0, data may contain Base64 audio and sentence may contain subtitles and timestamps. data is null when no audio is present. Finish: code=20000000; usage.text_words is the character usage measurement when returned.

### Examples

#### Request example

```bash
curl -N --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/process" \
--header "Content-Type: application/json" \
--header "Accept: text/event-stream" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_tts",
  "operator_version": "v1",
  "data": {
    "stream": true,
    "resource_id": "seed-tts-2.0",
    "req_params": {
      "text": "Welcome to Doubao Text-to-Speech.",
      "speaker": "en_female_stokie_uranus_bigtts",
      "audio_params": {
        "format": "mp3",
        "sample_rate": 24000,
        "bit_rate": 64000
      },
      "additions": "{\"silence_duration\":500}"
    }
  }
}'
```

#### Response example

The response example lists SSE events in arrival order as an array, with each `data` JSON string decoded and expanded into an object, followed by the `[DONE]` marker. The API sends individual SSE messages, and the actual `data` field is a string that the client parses a second time.

```json
[
  {
    "metadata": {
      "task_status": "RUNNING",
      "business_code": "0",
      "error_msg": "",
      "request_id": "<request-id>"
    },
    "data": {
      "code": 0,
      "message": "",
      "data": "<base64-audio-chunk>"
    }
  },
  {
    "metadata": {
      "task_status": "RUNNING",
      "business_code": "0",
      "error_msg": "",
      "request_id": "<request-id>"
    },
    "data": {
      "code": 20000000,
      "message": "OK",
      "data": null,
      "usage": {
        "text_words": 33
      }
    }
  },
  "[DONE]"
]
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |The request parameters are invalid. |
|400 |Tts.TextLimitExceeded |The text length exceeds the limit. |The submitted text is too long. |
|400 |Tts.SpeakerPermissionDenied |Speaker permission denied. |The voice is invalid or unauthorized. |
|401 |Authorization.Missing |Missing Authorization. |Authorization is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The API key is invalid. |
|429 |Server.Busy |Server is Busy, please try again later. |The service is busy or rate limited. |
|500 |Server.InternalError |General Internal Error |Internal server error. |
|500 |Tts.InternalError |TTS Internal Error |TTS service error. |
