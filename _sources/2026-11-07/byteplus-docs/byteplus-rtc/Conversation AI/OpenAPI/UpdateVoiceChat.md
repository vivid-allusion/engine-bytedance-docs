---
title: "UpdateVoiceChat"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404671"
---

In real\-time audio and video interaction, if you need to change behaviors of the AI agent, such as interrupting it during voice output, you can achieve this by calling this interface.

## HTTP request

* Method：POST

* Endpoint：[https://open.byteplusapi.com?Action=UpdateVoiceChat&Version=2025-05-01](https://open.byteplusapi.com?Action=UpdateVoiceChat&Version=2025-05-01)

## Request parameters

### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

### Query

**Action** String 必选 `Example: UpdateVoiceChat`

Interface name. The value of this interface: `UpdateVoiceChat`

**Version** String 必选 `Example: 2025-05-01`

OpenAPI version. The value of this interface: `2025-05-01`

### Body

**AppId** String 必选 `Example: 661e****543cf`

The AppId for your application.

Must be the same AppId that was used to start the task with `StartVoiceChat`. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid).

**RoomId** String 必选 `Example: Room1`

The ID of the call room.

Must be the same `RoomId` that was used to start the task with `StartVoiceChat`.

**TaskId** String 必选 `Example: task1`

The ID of the target agent task.

Must be the same `TaskId` that was defined when starting the task with `StartVoiceChat`.

**Command** String 必选 `Example: interrupt`

Update instructions:

* `interrupt`: Interrupts the agent's current speech.  See [Interrupt AI Agent](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1511927).

* `function`: Return tool invocation messages to RTC Server

* `ExternalTextToSpeech`: Pass in text information for TTS audio playback.

* `ExternalPromptsForLLM`: Pass in custom text combined with the user's question to the LLM.

* `ExternalTextToLLM`: Pass in an external question to the LLM.

* `FinishSpeechRecognition`：Trigger a new round of conversation.

* `UpdateParameters`: Updates the agent's configuration. Requires the `Parameters` field.

* `AudioCtrl`: Controls the playback state (e.g., pause or resume) of the TTS audio in the current conversation turn. Must be used in conjunction with the `AudioConfig` field.

* `SetTTSContext`: Dynamically sets TTS instruction tags for the next round of conversation to make the broadcast emotional. It needs to be used in conjunction with the Message field. For specific usage methods, please refer to [Using Instruction Tags to Control AI Emotion](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-2139328).

> **说明**

> The `SetTTSContext` command only takes effect when using the BytePlus TTS and when `Context.TagParse` is configured to true in `StartVoiceChat`.

**Message** String `Optional` `Example: {\"ToolCallID\":\"call_cx\",\"Content\":\"The weather in London is sunny.\"}`

The content of the command. Whether this field is required and its format depend on the Command value.

* **When** **`Command`** ** is ** **`function`**: **Required**. The tool's execution result as an escaped JSON string. Sample: `"{\"ToolCallID\":\"call_cx\",\"Content\":\"The weather in Shanghai is typhoon\"}"`.

* **When** **`Command`** ** is ** **`ExternalTextToSpeech`**: **Required**. The plain text for the agent to speak. Recommended length is under 200 characters to avoid high synthesis latency.

* **When** **`Command`** ** is ** **`ExternalPromptsForLLM`**: **Required**. The background context or prompt text to inject into the LLM.

* **When** **`Command`** ** is ** **`ExternalTextToLLM`**:

   * **For text\-only prompts**: **Required**. The text of the question.

   * **For image understanding**: **Conditional**.

      * If `Message` is provided: It serves as the text prompt associated with the image (e.g., "What is in this picture?"). The system sends both the image and text to the LLM to trigger a response.

      * If `Message` is omitted: The system only caches the image in the current turn's context (GroupID) without triggering a response. This is useful for multi\-image or chunked uploads.

* **When Command is SetTTSContext**: **Required**. Fill in the TTS tag to be set (must be a JSON escaped string). This tag only takes effect for the next turn of the response. The Message format depends on the TTS model version you specified via ResourceId in StartVoiceChat:

   * BytePlus TTS 2.0: `"{\"Tag\":{\"additions\":{\"context_texts\":[\"Make your tone a bit more cheerful\"]}}}"`

   * BytePlus TTS 1.0: `"{\"Tag\":{\"audio_params\":{\"emotion\":\"happy\",\"emotion_scale\":5}}}"`

* **For other Commands**: This field is ignored.

**InterruptMode** Integer `Optional` `Example: 1`

The processing priority when text information or external questions are passed in. Required if `Command` is set to `ExternalTextToSpeech` or `ExternalTextToLLM`. For other Commands, this field is ignored.

* `1`: High priority. The incoming information directly interrupts the interaction and is processed.

* `2`: Medium priority. Wait until the current interaction ends and then process.

* `3`: Low priority. If an interaction is currently occurring, directly discard the information passed in by `Message`.

> **warning**

> Under the Function Calling function, this parameter is defined differently. See [Function Calling](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1554654)for details.

**ImageConfig** Object `Optional` `Example: -`

Send images (URL) to the LLM for visual question answering.

> **warning**

> Required if `Command` is set to `ExternalTextToLLM`and need to send image.

**Action** String 必选 `Example: insert`

Defines the operation for the current set of images. Supported values are:

* `insert`: Submits images for the current conversation turn (identified by `GroupID`). The images are cached and associated with any following text prompts in the same turn.

* `delete`: Clears the image cache for a specific `GroupID`.

**GroupID** Integer 必选 `Example: 2`

A user\-defined ID that groups a set of images and text prompts into a single conversational turn. **Must be monotonically increasing.**

* For insert: The ID of the current turn.

* For delete: The ID of the turn whose image cache you want to clear.

**ImageType** String `Optional` `Example: url`

Specifies the image format. Currently, only `url` is supported.

> **warning**

> Required if `Action` is set to `insert`.

**Images** String[] `Optional` `Example: ["https://your-tos-bucket.volces.com/path/to/image.jpg"]`

An array of public URLs for the images to be processed. The LLM must be able to access these URLs.

> **warning**

> Required if `Action` is set to `insert`.

**Parameters** Object `Optional` `Example: -`

Configuration parameters for the agent.

> **warning**

> Required if `Command` is set to `UpdateParameters`.

**Config** Object `Optional` `Example: -`

Configuration parameters for the agent.

**LLMConfig** Object `Optional` `Example: -`

Configuration for the LLM.

**SystemMessages** String[] `Optional` `Example: ["You are Xiao Ning..."]`

The system prompt, used to define the agent's role, persona, response style, and output format.

* **To update**: Provide a new array of strings to overwrite the existing configuration.

* **To clear**: Provide an empty array [] or `null`.

**UserPrompts** Object[] `Optional` `Example: [ { "Role": "user", "Content": "Hello" }... ]`

Pre\-defined user inputs and assistant replies used to guide the model's behavior or set the dialogue context.

* **To update**: Provide a new array of objects (each with Role and Content) to completely overwrite the old configuration.

* **To clear**: Provide an empty array [] or `null`.

> **warning**

* > **Format Constraints**: Role only supports system, user, and assistant. The user and assistant roles must appear in pairs, otherwise it may lead to undefined behavior from the LLM.

* > **Context Limit**: The number of turns occupied by `UserPrompts` is limited by the `HistoryLength` parameter. For example, if `UserPrompts` contains 2 turns and `HistoryLength`is 3, after 3 live turns with the user, the pre\-set prompts will be pushed out of the context window.

**Tools** Object[] `Optional` `Example: null`

Updates the list of tools for Function Calling or disables the feature.

* **To update tools**: Provide an array with the new tool definitions to overwrite the old configuration.

* **To disable Function Calling**: Set the value to `null` or `[]` (e.g., `{"Tools": null}`).

**type** String `Optional` `Example: function`

The tool type. Currently, only `function` is supported.

**function** Object `Optional` `Example: -`

Defines a function the model can call.

**name** String `Optional` `Example: get_current_weather`

The name of the function.

**description** String `Optional` `Example: Get weather info for a city`

A description of what the function does, used by the model to decide when and how to call it.

**parameters** JSONMap `Optional` `Example: -`

The function's request parameters, described in JSON Schema format. See details in [JSON Schema](https://json-schema.org/understanding-json-schema).

```json
{ "type": "object", "properties": { ... }, "required": ["location"] }
```

**VisionConfig** Object `Optional` `Example: -`

Configuration for visual understanding capabilities.

* **To enable/update**: Configure Enable and SnapshotConfig. See [How to use visual understanding](https://docs.byteplus.com/en/docs/12/docs-1408245).

* **To disable**: Set VisionConfig to null, or set VisionConfig.Enable to false.

**Enable** Boolean `Optional` `Example: false`

Enables or disables the visual understanding feature.

* `false`: Disable.

* `true`: Enable.

   Defaults to `false`.

**SnapshotConfig** Object `Optional` `Example: -`

Snapshot configuration.

The agent will capture frames from a video stream according to this policy and send them to the LLM.

**StreamType** Integer `Optional` `Example: 0`

The type of stream to capture from.

* `0`: Main stream (camera feed).

* `1`: Screen sharing stream.

   Defaults to `0`.

**TTSConfig** Object `Optional` `Example: -`

Configuration for TTS. You can perform the following actions:

* **Modify current TTS settings**: If keeping the same TTS provider, you only need to send the fields you want to change (e.g., just `speed_ratio`).

* **Switch TTS provider**: To switch from one provider to another, you must provide both the new `Provider` and a `ProviderParams` object with the fields required by the new provider to ensure the old configuration is fully overwritten.

**Provider** String `Optional`

TTS provider.

* `OpenAI`: OpenAI TTS

* `Amazon`: Amazon TTS

* `BytePlus`: BytePlus TTS

* `Google`: Google TTS

* `Elevenlabs`: ElevenLabs TTS

* `minimax_bidirection`: MiniMax bidirectional streaming TTS

**ProviderParams** Object `Optional` `Example: -`

Configuration parameters of different TTS providers vary:

OpenAI TTS

**URL** String `Optional` `Example: https://api.openai.com/v1/audio/speech`

URL. Must be the value: `https://api.openai.com/v1/audio/speech`.

**APIKey** String `Optional` `Example: 234****2nd`

APIKey. Acquire on [api-keys](https://platform.openai.com/api-keys).

**Model** String `Optional` `Example: tts-1`

OpenAPI model. Acquire on [models](https://platform.openai.com/docs/models#tts).

**Speed** String `Optional` `Example: 1.0`

Voice's speed. Must be the value: `1.0`.

**Voice** String `Optional` `Example: alloy`

Voice type. Acquire on [Voice options](https://platform.openai.com/docs/guides/text-to-speech#voice-options).

Amazon TTS

**ID** String `Optional` `Example: 13****413`

Amazon Access key ID. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**Secret** String `Optional` `Example: 13****a12`

Amazon Secret access key. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**VoiceID** String `Optional` `Example: Celine`

Voice ID. Acquire on [Available voice](https://docs.aws.amazon.com/polly/latest/dg/available-voices.html).

**Region** String `Optional` `Example: us-west-2`

Region. Acquire on [Amazon console](https://console.aws.amazon.com/iam/).

**Language** String `Optional` `Example: zh-CN`

Language code. Acquire on [Supported languages and language-specific features](https://docs.aws.amazon.com/transcribe/latest/dg/supported-languages.html).

BytePlus TTS_Text\-to\-Speech (Parameter Pass\-through)

This method supports all configuration parameters of the BytePlus TTS, offering greater flexibility and more comprehensive features compared to direct parameter passing.

**Credential** Object `Optional` `Example: -`

Authentication parameters for BytePlus TTS service.

**ApiKey** String `Optional` `Example: bpAK****11`

API key for BytePlus TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys). The existing `AppId` and `Token` authentication method remains supported for backward compatibility.

**ResourceId** String `Optional` `Example: volc.service_type.1000009`

The resource information ID. Must be `volc.service_type.1000009`.

**SeedTTSParameters** String `Optional`

A single\-line, minified, and escaped JSON string for passing custom parameters to the BytePlus TTS (Text\-to\-Speech) service.

**How to Configure This Field**: Construct a JSON object based on the Payload request parameters from the documentation [TTS - Bi-directional Streaming (WebSocket)](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts), following the rules below. Once built, convert it into a single\-line, escaped string.

* **Required parameters**: Must include the parameter `req_params.speaker`, which can be obtained on [BytePlus Text-to-Speech Console](https://console.byteplus.com/voice/service/1000014?).

* **Forbidden parameters:**  Do not include the following parameters:

   * user

   * event

   * namespace

   * req_params.text

   * req_params.audio_params.format

   * req_params.audio_params.enable_timestamp

   * req_params.additions.max_length_to_filter_parenthesis

   * req_params.additions.cache_config, req_params.additions.enable_latex_tn: When using TTS 2.0 (`ResourceId` is `seed-tts-2.0`), this field cannot be passed if `SubtitleMode` is set to 0.

* **Other parameters:**  As you needed to customize the output (e.g., req_params.audio_params.speech_rate).

   **Example:**  To set the required speaker voice.

1. Construct this JSON:

   ```Plain Text
   {
   "req_params": {
         "speaker": "zh_female_cancan_mars_bigtts"
      }
   }
   ```

2. Convert it into a single\-line, escaped string: `{\"req_params\":{\"speaker\":\"zh_female_cancan_mars_bigtts\"}}`.

BytePlus TTS_Text\-to\-Speech (Direct Parameter Forwarding)

This method encapsulates some of the common parameters for the BytePlus TTS. It simplifies integration but does not provide access to the service's full range of features.

**app** Object `Optional` `Example: -`

BytePlus Text\-to\-Speech application configuration.

**apikey** String `Optional` `Example: bpAK****11`

API key for BytePlus TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys). The existing `appid` and `token` authentication method remains supported for backward compatibility.

**audio** Object `Optional` `Example: -`

BytePlus Text\-to\-Speech audio configuration.

**voice_type** String `Optional` `Example: zh_female_cancan_mars_bigtts`

Voice_type of purchased timbre on [BytePlus Text-to-Speech Console](https://console.byteplus.com/voice/service/1000014?).

**pitch_rate** Float `Optional` `Example: 0.0`

Pitch, limited to `[-12,12]`. Defaults to `0.8`.

**speech_rate** Integer `Optional` `Example: 0`

Speech speed, limited to `[-50, 100]`. Default to `0`.

`100` represents 2.0x speed, and `-50` represents 0.5x speed.

**ResourceId** String `Optional` `Example: volc.service_type.1000009`

The resource information ID. Must be `volc.service_type.1000009`.

**Additions** Object `Optional` `Example: -`

BytePlus Text\-to\-Speech advanced configuration.

**enable_latex_tn** Boolean `Optional` `Example: true`

Read LaTeX formulas aloud.

When enabled, the agent will read LaTeX\-formatted mathematical formulas using natural language instead of just speaking the raw characters.

* `false` (default): Disable.

* `true`: Enable. For this to take effect, `disable_markdown_filter` must also be true.

> **Example**:

* LLM Response: `According to the formula a^2 + b^2 = c^2...`

* Agent Speaks: `According to the formula a squared plus b squared equals c squared...`

* Subtitles Show: `According to the formula a^2 + b^2 = c^2...`

**disable_markdown_filter** Boolean `Optional` `Example: true`

Filters Markdown formatting from the LLM's text before speech synthesis.

* `true`: Enable filtering. For example, `**hello**` will be pronounced as `hello`.

* `false` (Default): No filtering.

> **Example:**

* LLM Response: `Please run the **grep** command to view the logs.`

* Agent Speaks: `Please run the grep command to view the logs.`

* Subtitles Show: `Please run the **grep** command to view the logs.`

**enable_language_detector** Boolean `Optional` `Example: false`

Whether to automatically recognize the language.

* `true`: Enable to automatically recognize.

* `false`: Disable to automatically recognize.

   Default to `false`.

BytePlus TTS_Voice Replication (Parameter Pass\-through)

This method supports all configuration parameters of the BytePlus TTS (Voice Replication), offering greater flexibility and more comprehensive features compared to direct parameter passing.

**Credential** Object `Optional` `Example: -`

Authentication parameters for BytePlus TTS (Voice Replication) service.

**ApiKey** String `Optional` `Example: bpAK****11`

API key for BytePlus TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys). The existing `AppId` and `Token` authentication method remains supported for backward compatibility.

**ResourceId** String `Optional` `Example: seed-icl-2.0`

Choose the BytePlus TTS (Voice Replication) version:

* `seed-icl-1.0` or `volc.megatts.default`: BytePlus TTS (Voice Replication) 1.0

* `seed-icl-2.0`: BytePlus TTS (Voice Replication) 2.0

   For the differences between the two versions, see [Voice Replication 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplicationv2).

**SeedTTSParameters** String `Optional` `Example: "{\"req_params\":{\"speaker\":\"zh_female_cancan_mars_bigtts\"}}"`

A single\-line, minified, and escaped JSON string for passing custom parameters to the BytePlus TTS (Voice Replication) service.

**How to Configure This Field**: Construct a JSON object based on the Payload request parameters from the documentation [TTS - Bi-directional Streaming (WebSocket)](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts), following the rules below. Once built, convert it into a single\-line, escaped string.

* **Required parameters**: Must include the parameter `req_params.speaker`. You need to purchase and train the voice in the [BytePlus Voice Replication Console](https://console.byteplus.com/voice/service/1000016?) first. For detailed instructions, refer to the [Voice Replication Order and Usage Guide](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication).

* **Forbidden parameters:**  Do not include the following parameters:

   * user

   * event

   * namespace

   * req_params.text

   * req_params.audio_params.format

   * req_params.audio_params.enable_timestamp

   * req_params.additions.max_length_to_filter_parenthesis

   * req_params.additions.cache_config, req_params.additions.enable_latex_tn: When using TTS 2.0 (`ResourceId` is `seed-tts-2.0`), this field cannot be passed if `SubtitleMode` is set to 0.

* **Other parameters:**  As you needed to customize the output (e.g., req_params.audio_params.speech_rate).

   **Example:**  To set the required speaker voice.

1. Construct this JSON:

   ```Plain Text
   {
   "req_params": {
         "speaker": "zh_female_cancan_mars_bigtts"
      }
   }
   ```

2. Convert it into a single\-line, escaped string: `{\"req_params\":{\"speaker\":\"zh_female_cancan_mars_bigtts\"}}`.

BytePlus TTS_Voice Replication (Direct Parameter Forwarding)

This method encapsulates some of the common parameters for the BytePlus TTS (Voice Replication). It simplifies integration but does not provide access to the service's full range of features.

**app** Object `Optional` `Example: -`

BytePlus TTS (Voice Replication) application configuration.

**apikey** String `Optional` `Example: bpAK****11`

API key for BytePlus TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys). The existing `appid` and `token` authentication method remains supported for backward compatibility.

**audio** Object `Optional` `Example: -`

BytePlus TTS (Voice Replication) audio configuration.

**voice_type** String `Optional` `Example: S_N****7k1`

Speaker ID for the BytePlus TTS (Voice Replication) service. You need to purchase and train the voice in the [BytePlus Voice Replication Console](https://console.byteplus.com/voice/service/1000016?) first. For detailed instructions, refer to the [Voice Replication Order and Usage Guide](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication).

**pitch_rate** Float `Optional` `Example: 0.0`

Pitch, limited to `[-12, 12]`. Defaults to `0.0`.

**speech_rate** Integer `Optional` `Example: 0`

Speech speed, limited to `[-50, 100]`. Default to `0`.

`100` represents 2.0x speed, and `-50` represents 0.5x speed.

**ResourceId** String `Optional` `Example: seed-icl-2.0`

Choose the BytePlus TTS (Voice Replication) version:

* `seed-icl-1.0` or `volc.megatts.defaul`: BytePlus TTS (Voice Replication) 1.0

* `seed-icl-2.0`: BytePlus TTS (Voice Replication) 2.0

   For the differences between the two versions, see [Voice Replication 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplicationv2).

**Additions** Object `Optional` `Example: -`

BytePlus TTS (Voice Replication) advanced configuration.

**enable_latex_tn** Boolean `Optional` `Example: true`

Read LaTeX formulas aloud.

When enabled, the agent will read LaTeX\-formatted mathematical formulas using natural language instead of just speaking the raw characters.

* `false` (default): Disable.

* `true`: Enable. For this to take effect, `disable_markdown_filter` must also be true.

> **Example**:

* LLM Response: According to the formula a2 + b2 = c^2...

* Agent Speaks: According to the formula a squared plus b squared equals c squared...

* Subtitles Show: According to the formula a2 + b2 = c^2...

> **warning**

* > When using Voice Replication 2.0 (`ResourceId` is `seed-icl-2.0`), this field cannot be passed if `SubtitleMode` is set to 0.

* > When using the Voice Replication 2.0, if you need to set `SubtitleMode: 0`, you must disable the `enable_latex_tn` (broadcast LaTeX formulas) feature.

* > When `SubtitleMode` is 1, it is expected behavior for the subtitle to receive the following italicized content: `{"definite": true, "paragraph": true, "roundId": 4, "text": ""}`.

**disable_markdown_filter** Boolean `Optional` `Example: true`

Filters Markdown formatting from the LLM's text before speech synthesis.

* true: Enable filtering. For example, **hello** will be pronounced as hello.

* false (Default): No filtering.

> **Example:**

* LLM Response: Please run the **grep** command to view the logs.

* Agent Speaks: Please run the grep command to view the logs.

* Subtitles Show: Please run the **grep** command to view the logs.

**enable_language_detector** Boolean `Optional` `Example: false`

Whether to automatically recognize the language.

* `true`: Enable to automatically recognize.

* `false`: Disable to automatically recognize.

   Default to `false`.

Google TTS

**CredentialsJSON** String `Optional` `Example: "{\"type\": \"service_account\", \"private_key\": \"-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n\"}"`

Provide the service account key as a JSON string (downloaded from Google Cloud Console).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89d3385eb7f0fad18ff0b10464b41091.png)

**How to obtain the key**: see [Creating service account keys](https://docs.cloud.google.com/iam/docs/keys-create-delete#iam-service-account-keys-create-console).

> The Google service account must have permissions to use the [Cloud Chirp 3: HD voices](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd).

> **warning**

> This key grants full access to your Google Cloud project. Store it securely and avoid hardcoding in source code.

**VoiceSelection** Object `Optional` `Example: -`

Specifies the voice and language for speech synthesis.

**LanguageCode** String `Optional` `Example: cmn-CN`

The BCP\-47 language code for the desired voice. Supported languages: [Language availability](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd#language_availability).

**Name** String `Optional` `Example: cmn-CN-Chirp3-HD-Achernar`

The full name of the voice model, formatted as: `<Language code>-Chirp3-HD-<Voice name>`.

* `<Language code>`: Must be identical to the value specified in `LanguageCode`.

* `<Voice name>`: The specific voice to use. See [Voice options](https://docs.cloud.google.com/text-to-speech/docs/gemini-tts#voice_options) for a complete list.

   Example: `cmn-CN-Chirp3-HD-Achernar` (a male Mandarin voice).

**StreamingAudioConfig** Object `Optional` `Example: -`

Configuration settings for the output audio stream.

**SpeakingRate** Float `Optional` `Example: 1.0`

Controls speech speed relative to the voice’s original speaking rate.

* Valid range: `[0.25, 2.0]`.

   * `0.5`: half speed.

   * `2.0`: double speed.

* Defaults to `1.0`, representing original speed.

**IgnoreBracketText** Integer[] `Optional`

Filters out content within specified types of brackets from the LLM's response before sending it to TTS.

This is useful for removing non\-verbal cues like emotion tags (e.g., (happy)) or action descriptions (e.g., [nods]) from the audio playback to create a more immersive experience.

> This should be used in conjunction with LLM prompts that instruct the model to place such cues within brackets. See [Filter specific content](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1350596).

* **Supported values:**

   * `1`: Chinese parentheses `（）`

   * `2`: English parentheses `()`

   * `3`: Chinese square brackets `【】`

   * `4`: English square brackets `[]`

   * `5`: English curly braces `{}`

The default value is empty, indicating that no filtering is performed.

* **How to update:**

   * **To set/update**: Provide an array of values (e.g., [1, 2]) to **overwrite** the previous setting.

   * **To disable**: Provide null or an empty array [].

> **tip**

> Filtered content will typically still appear in the subtitles. However, it will be excluded from subtitles if it appears at the very end of a response and is treated as a separate sentence.

**InterruptMode** Integer `Optional` `Example: 0`

Enables or disables barge\-in (speak to interrupt).

* `0`: Enabled. The agent will stop speaking as soon as the user starts talking.

* `1`: Disabled. The agent will not be interrupted, and any user speech during the agent's playback will be ignored.

   Defaults to 0.

**AudioConfig** Object `Optional` `Example: -`

Audio control parameters.

> **warning**

> This field takes effect and is required only when `Command` is set to `AudioCtrl`.

**Action** String 必选 `Example: pause`

Audio playback operations:

* `pause`: Pause playback.

* `play`: Resume playback.

> **warning**

> This control applies only to the current conversation turn. If the agent is interrupted or a new conversation turn begins, the control state is automatically invalidated.

## Response parameters {#Response parameters}

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

Result returns "success" only when the request succeeds and null when it fails.
