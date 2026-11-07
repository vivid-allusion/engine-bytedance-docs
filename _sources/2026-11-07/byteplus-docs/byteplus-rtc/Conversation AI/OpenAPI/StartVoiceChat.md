---
title: "StartVoiceChat"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163"
---

In real\-time audio and video interaction, if you want to activate an AI agent to provide voice chat services, you can achieve this by calling this interface.

You can set the application identifier, RoomId, TaskId, as well as advanced configurations related to ASR, TTS, and LLM according to your need to customize the agent's behavior and interaction methods.

## Usage scenario

* **How to call the API**: When sending an HTTP(S) request, follow the BytePlus API specifications. For details about the request structure, common parameters, signature mechanism, and response structure, see [Call OpenAPI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828).

* **Request rate**: The QPS for a single account must not exceed 60.

## HTTP request

* Method：POST

* Endpoint：[https://open.byteplusapi.com?Action=StartVoiceChat&Version=2025-05-01](https://open.byteplusapi.com?Action=StartVoiceChat&Version=2025-05-01)

## Request parameters

### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

### Query

**Action** String 必选 `Example: StartVoiceChat`

Interface name. The value of this interface: `StartVoiceChat`

**Version** String 必选 `Example: 2025-05-01`

OpenAPI version. The value of this interface: `2025-05-01`

### Body

**AppId** String 必选 `Example: 661e****543cf`

The AppId for your application.

Must be the same AppId that was used to start the task with `StartVoiceChat`. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid).

**RoomId** String 必选 `Example: Room1`

The room ID for the conversation between the agent and the real person. This value must be consistent with that used when the real person user enters the room using the client SDK.

**TaskId** String 必选 `Example: Task1`

Task Id. You need to define the `TaskId` for each agent task, and also use this `TaskId` when updating and ending the task later.

It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.

The `TaskId` is the identifier of the task. Under a `RoomId` of an AppId, the `TaskId` is unique. The `TaskId` can be repeated under different `AppId` or different `RoomId`. Therefore, `AppId` + `RoomId` + `TaskId` is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified `AppId`, so that this task can be updated or stopped during the running of this task.

**Config** Object 必选 `Example: -`

Agent interaction configuration, including Automatic Speech Recognition (ASR), Text\-to\-Speech (TTS), Large Language Model (LLM), subtitle, and Function Calling.

**ASRConfig** Object 必选 `Example: -`

Config for ASR.

**Provider** String 必选 `Example: amazon`

ASR provider. Supported ASR services and their values are listed below:

* `Amazon`: Amazon ASR

* `BytePlus`: BytePlus ASR（Speech\-to\-Text (ASR) \- Streaming）

* `Google`: Google ASR (Cloud Speech\-to\-Text V1)

* `GoogleV2`: Google ASR (Cloud Speech\-to\-Text V2)

* `ai_gateway`: Self\-hosted ASR

**ProviderParams** Object 必选 `Example: -`

Configuration for ASR. Parameters of different ASR providers vary:

Amazon ASR

**ID** String 必选 `Example: 123****214`

Amazon Access key ID. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**Secret** String 必选 `Example: 32****dad`

Amazon Secret access key. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**Region** String 必选 `Example: us-west-2`

Region. Acquire on [Amazon console](https://console.aws.amazon.com/iam/).

**Language** String `Optional` `Example: zh-CN`

Language code. Acquire on [Supported languages and language-specific features](https://docs.aws.amazon.com/transcribe/latest/dg/supported-languages.html).

BytePlus ASR (Parameter Pass\-through)

This method supports all configuration parameters of the BytePlus ASR, offering greater flexibility and more comprehensive features compared to direct parameter passing.

**Mode** String 必选 `Example: SeedASR`

The model type. This parameter must be SeedASR, indicating the BytePlus ASR model (Speech\-to\-Text (ASR) \- Streaming).

**Credential** Object 必选 `Example: -`

Authentication parameters for BytePlus ASR service.

**ApiKey** String 必选 `Example: bpAK****21`

API key used for BytePlus Seed ASR authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys).

> **tip**

> The existing `AppId` and `AccessToken` authentication method remains supported for backward compatibility.

**ApiResourceId** String 必选 `Example: volc.bigasr.sauc.duration`

Choose the BytePlus Seed Speech ASR Model:

* `volc.bigasr.sauc.duration`: Seed Speech ASR 1.0

* `volc.seedasr.sauc.duration`: Seed Speech ASR 2.0

For the differences between the two models, see [ASR 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/speechtotextv2) and [ASR 1.0](https://docs.byteplus.com/en/docs/byteplusvoice/speechtotextv_1).

**SeedASRParameters** String 必选 `Example: "{\"request\":{\"enable_ddc\":true,\"end_window_size\":800}}"`

A single\-line, minified, and escaped JSON string for passing custom parameters to the BytePlus ASR service.

**How to Configure This Field**:

* **If no custom parameters are needed**: Provide an empty JSON object string: "{}". E.g., `SeedASRParameters: "{}"`.

* **To send custom parameters**：

   * **Allowed Parameters**: Parameter from the Payload section of the [ASR Streaming API documentation](https://docs.byteplus.com/en/docs/byteplusvoice/asrstreaming), **excluding the fields listed under Forbidden Parameters below**.

   * **How to Format:**  Construct a JSON object with your chosen parameters, then convert it into a single\-line, minified, and escaped string.

   * **Forbidden Parameters:**  The following parameters must not be included in your JSON object:

      * user

      * request.show_speech_rate

      * request.show_volume

      * request.enable_lid

      * request.enable_emotion_detection

      * request.enable_gender_detection

      * request.show_utterances

      * request.result_type

      * request.mode_name

      * request.force_to_speech_time

      * audio.format

      * audio.codec

      * audio.rate

      * audio.bits

      * audio.channel

**StreamMode** Integer `Optional` `Example: 0`

The output mode for ASR results:

* `0` (defalut): Streaming output. The recognition results are returned in segments in real\-time. This mode offers faster speed and is suitable for real\-time captioning scenarios.

* `1`: Non\-streaming output. The final recognition result is returned once after the entire audio segment is received and processed. This mode provides higher accuracy and is suitable for offline transcription scenarios (e.g., meeting recordings) where immediate feedback is not required.

* `2` (Recommended): Bidirectional streaming. Building on both streaming input and output, this mode supports a dual\-pass recognition for detected complete sentence segments, striking a balance between real\-time performance and accuracy.

> **warning**

* > When using the Seed Speech ASR 2.0, the `StreamMode`can only be set to 1 or 2.

* > To enable the dual\-pass recognition, you must pass `"enable_nonstream": true` in the `VolcanoASRParameters`.

**ContextHistoryLength** Integer `Optional` `Example: 0`

The number of recent conversation turns to use as context for improving ASR accuracy.

* Valid Range: `[0, 20]`.

* The default is `0`.

BytePlus ASR (Direct Parameter Forwarding)

This method encapsulates some of the common parameters for the the BytePlus ASR. It simplifies integration but does not provide access to the service's full range of features.

**Mode** String 必选 `Example: SeedASR`

The model type. This parameter must be `SeedASR`, indicating the BytePlus ASR model (Speech\-to\-Text (ASR) \- Streaming).

**Language** String 必选 `Example: zh-CN`

Language code, supported values:

* `zh-CN`: Chinese (Simplified)

* `en-US`: English (United States)

**ApiKey** String 必选 `Example: bpAK****21`

API key used for BytePlus Seed ASR authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys).

> **tip**

> The existing `AppId` and `AccessToken` authentication method remains supported for backward compatibility.

**ApiResourceId** String 必选 `Example: volc.bigasr.sauc.duration`

Choose the BytePlus Seed Speech ASR Model:

* `volc.bigasr.sauc.duration`: Seed Speech ASR 1.0

* `volc.seedasr.sauc.duration`: Seed Speech ASR 2.0

For the differences between the two models, see [ASR 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/speechtotextv2) and [ASR 1.0](https://docs.byteplus.com/en/docs/byteplusvoice/speechtotextv_1).

**StreamMode** Integer `Optional` `Example: 0`

The output mode for ASR results:

* `0` (default): Streaming output. The recognition results are returned in segments in real\-time. This mode offers faster speed and is suitable for real\-time captioning scenarios.

* `1`: Non\-streaming output. The final recognition result is returned once after the entire audio segment is received and processed. This mode provides higher accuracy and is suitable for offline transcription scenarios (e.g., meeting recordings) where immediate feedback is not required.

* `2` (Recommended): Bidirectional streaming. Building on both streaming input and output, this mode supports a dual\-pass recognition for detected complete sentence segments, striking a balance between real\-time performance and accuracy.

> **warning**

* > When using the Seed Speech ASR 2.0, the `StreamMode`can only be set to 1 or 2.

* > To enable the dual\-pass recognition, you must set `enable_nonstream` to true.

**enable_nonstream** Boolean `Optional` `Example: true`

Whether to enable dual\-pass recognition based on the bidirectional streaming mode (`StreamMode: 2`).

* **false** (default): Disabled.

* **true**: Enabled. When enabled, if the user's speaking pause exceeds the duration specified by `ASRConfig.VADConfig.SilenceTime`, the system will perform a dual\-pass recognition on the audio of that sentence segment (using streaming input and non\-streaming output).

> **warning**

> Setting `enable_nonstream` to `true` only takes effect when `StreamMode` is set to `2`.

Google ASR (Speech\-to\-Text V1)

**Language** String 必选 `Example: en-US`

Code of the language to be recognized. See [Speech-to-Text V1 supported languages](https://cloud.google.com/speech-to-text/docs/v1/speech-to-text-supported-languages) for all valid codes.

**CredentialsJSON** String 必选 `Example: "{\"type\": \"service_account\", \"private_key\": \"-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n\"}"`

Provide the service account key as a JSON string (downloaded from Google Cloud Console).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89d3385eb7f0fad18ff0b10464b41091.png)

**How to obtain the key**: see [Creating service account keys](https://docs.cloud.google.com/iam/docs/keys-create-delete#iam-service-account-keys-create-console).

> The Google service account must have permissions to use the Cloud Speech\-to\-Text V1.

**Model** String `Optional` `Example: latest_short`

Google ASR model type. Defaults to empty. For supported types, see [Introduction to Latest Models](https://cloud.google.com/speech-to-text/docs/v1/latest-models).

> **tip**

> For low\-latency scenarios, it is recommended to use `latest_short`or the default model.

Google ASR (Speech\-to\-Text V2)

**RecognizerPath** String 必选 `Example: projects/{PROJECT_ID}/locations/{LOCATION}/recognizers/{RECOGNIZER_ID}`

The full resource name of the "Recognizer" which stores your ASR configuration.

> **warning**

> If a custom `RecognizerPath` is provided, the `LanguageCodes` and `Model`parameters become optional. However, if you do provide them manually, they will override the settings stored within the Recognizer.

**CredentialsJSON** String 必选 `Example: "{\"type\": \"service_account\", \"private_key\": \"-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n\"}"`

Provide the service account key as a JSON string (downloaded from Google Cloud Console).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89d3385eb7f0fad18ff0b10464b41091.png)

**How to obtain the key**: see [Creating service account keys](https://docs.cloud.google.com/iam/docs/keys-create-delete#iam-service-account-keys-create-console).

> The Google service account must have permissions to use the Cloud Speech\-to\-Text V2.

**LanguageCodes** String[] `Optional` `Example: ["en-US", "fr-FR"]`

A list of BCP\-47 language codes for speech recognition.

V2 allows simultaneous recognition of up to two languages for Chirp models.  Other models support only one language. See [Cloud Speech-to-Text V2 supported languages](https://docs.cloud.google.com/speech-to-text/docs/speech-to-text-supported-languages) for all valid codes.

**Model** String `Optional` `Example: chirp-3`

The specific speech recognition model to be used. Must be compatible with the geographic location in `RecognizerPath` or the selected `LanguageCodes`.

Check the [Cloud Speech-to-Text V2 supported languages](https://docs.cloud.google.com/speech-to-text/docs/speech-to-text-supported-languages) documentation for valid combinations.

Self\-hosted ASR

**URL** String 必选 `Example: YourOpenAIURL`

> **warning**

> Before configuration, make sure that you have completed the following:

1. > Prepare your self\-hosted ASR service API. The API must comply with the [Self\-hosted model interface protocol spec](https://docs.byteplus.com/en/docs/iga/ai-gateway-self-hosted-protocol).

2. > [Submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000762&FlowKey=hooomjXXojvNpHrZdAQT&aiSearchQuestion=&aiID=) to request onboarding your self\-hosted ASR service to AI Gateway. Then follow [Onboard and call a self\-hosted model](https://docs.byteplus.com/en/docs/iga/ai-gateway-self-hosted)to complete the integration.

AI Gateway endpoint URL. StartVoiceChat connects to AI Gateway through this URL, and AI Gateway then forwards requests to your self\-hosted ASR service.

* URL format:`wss://ai-gateway.vei.volces.com/v1/realtime?model=<ASR invocation name>`

* `<ASR invocation name>`: Replace this value with the custom model invocation name configured in the AI Gateway console.

**APIKey** String 必选 `Example: YourOpenAIAPIKey`

AI Gateway access key. This is configured when onboarding your self\-hosted ASR service to AI Gateway.

**ExtraData** JSONMap `Optional` `Example: {"custom_param": "value1"}`

Custom parameters passed through to your self\-hosted ASR service in JSON format. If this parameter is not passed, no custom parameters are passed through.

**ExtraHeader** JSONMap `Optional` `Example: {"custom_header": "value"}`

Custom pass\-through headers. This parameter is a JSON object. Its key\-value pairs are passed as additional HTTP headers in requests to your self\-hosted ASR service. You can use them for authentication or other custom logic. If this parameter is not passed, no custom headers are passed through.

**VADConfig** Object `Optional` `Example: -`

VAD Configuration.

**SilenceTime** Integer `Optional` `Example: 600`

Duration of silence to detect speech stop (in milliseconds).

* Limited to `[500, 3000)`.

* Default to `600`.

   Shorter values result in faster responses, but the model might interrupt the user during brief pauses.

**VolumeGain** Float `Optional` `Example: 0.3`

Volume gain. Reduce the collection volume by this parameter to reduce ASR misrecognition caused by noise.

The default value is `1.0`, and the recommended value is `0.3`.

**TurnDetectionMode** Integer `Optional` `Example: 0`

Trigger method for a new round of conversation. For the usage method of this function, see [Configure Conversation Trigger Modes](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245).

* `0` (default): After the server detects a complete sentence, it automatically triggers a new round of conversation.

* `1`: After receiving the input end signal or the speech caption result, you decide whether to trigger a new round of conversation by yourself.

**LLMConfig** Object 必选 `Example: -`

Config for LLM. Parameters of different LLM providers vary:

BytePlus\-ModelArk

**AutoActive** Boolean `Optional` `Example: true`

Whether to enable LLMConfig configuration.

* `true` (default): Enable.

* `false`: Disable. After disabling, `LLMConfig` and `TTSConfig` will take no effect.

**Provider** String 必选 `Example: BytePlus`

Provider name. Must be `BytePlus`.

**EndPointId** String 必选 `Example: epid****212`

Online Inference EndPointId. Acquire on [ModelArk Console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint?config=%7B%7D).

**APIKey** String 必选 `Example: a12******31`

APIKey. Acquire on [View API Key](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint?config=%7B%7D).

**SystemMessages** String[] `Optional` `Example: ["You are an assistant, with a humorous and understanding personality."]`

System messages, used to input instructions that control the behavior of large language models, defining the model's role, behavioral guidelines, specific output formats, etc.

**UserPrompts** Object[] `Optional` `Example: [ { "Role": "user", "Content": "hello" }, { "Role": "assistant", "Content": "What can I do for you？" }]`

User prompts, used to enhance the quality of the model's responses. When the model generates responses, it will preferentially refer to the content here to guide the model to generate specific outputs or perform specific tasks.

The conversation content stored in `UserPrompts` is controlled by `HistoryLength`. For example, if two rounds of conversations are pre\-stored in `UserPrompts`, `HistoryLength` is set to 3, and the user has already had three rounds of conversations, when the fourth round of conversation starts, all the content stored in `UserPrompts` will be deleted.

**HistoryLength** Integer `Optional` `Example: 3`

Number of historical question rounds. The default value is `3`.

When calling this interface, it is necessary to ensure that the total length of all `UserPrompts` and `SystemMessage` text does not exceed the context length of the large language model.

For example, if the number of historical question rounds is `3`, and the `Skylark2-lite-8k` large language model with a length limit of 8k is used, and two rounds of conversations are pre\-stored in `UserPrompts`. When the user inputs the question of the first round of conversation, the total length of the `SystemMessage`, `UserPrompts`, and the question of the first round of conversation should not exceed 8k.

**TopP** Float `Optional` `Example: 0.3`

An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered.

Limited to `[0, 1]`, default to `0.3`。

**Temperature** Float `Optional` `Example: 0.1`

The sampling temperature, limited to `(0, 1]`, default to `0.1`.

Higher values like `0.8` will make the output more random, while lower values like `0.2` will make it more focused and deterministic.

**MaxTokens** Integer `Optional` `Example: 1024`

The maximum token limit of the output text, does not include chain\-of\-thought content.

* Default to `1024`.

* The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

> When `ThinkingType=enabled` or `auto` and you want to control the total output budget (including reasoning tokens), use `MaxCompletionTokens` instead.

**MaxCompletionTokens** Integer `Optional` `Example: 4096`

The maximum number of tokens the model can generate in its completion, including both the visible response and any internal reasoning tokens (chain\-of\-thought).

* Value range: A positive integer (\> 0). The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

* When not set, the field is not passed to the model, and `MaxTokens` remains in effect.

**ThinkingType** String `Optional` `Example: null`

Disables or enables the deep thinking capability of the large model. If you are using a model with deep thinking capabilities, it is strongly recommended to disable this feature to prevent long agent response times and ensure a smooth conversation.

Available values:

* `null`: The model uses its own default behavior. `null` is a keyword and must be passed without quotes when constructing the JSON request. Example: `{"ThinkingType": null}`.

* `disabled` (**Recommended**): Disables the deep thinking capability.

* `enabled`: Enables the deep thinking capability. When enabled, this will increase inference latency, and the model's intermediate thoughts will be discarded and not be part of the output.

   When not set, the field is not passed to the model, and the model uses its own default behavior.

> **warning**

> The `ThinkingType` field and the `auto` value are only supported by some models with deep thinking capabilities. For a list of supported models, refer to [Enable/disable deep reasoning](https://docs.byteplus.com/en/docs/modelark/deep-thinking#fa3f44fa).

**ReasoningEffort** String `Optional` `Example: low`

Controls the intensity of the model's reasoning process. Higher values produce better answer quality but increase latency and token consumption.

* Available values: `minimal`, `low`, `medium`, `high`.

* If not set, the parameter is not passed to the model, and the model uses its own default behavior.

> **warning**

* > When both `ThinkingType` and `ReasoningEffort` are provided, `ReasoningEffort` takes precedence.

* > When `ThinkingType=disabled`: `ReasoningEffort` can only be `minimal` or omitted.

* > When `ThinkingType=enabled` or `auto`: `ReasoningEffort` cannot be set to `minimal`.

**VisionConfig** Object `Optional` `Example: -`

Vision Config. Refer to [Vision Understanding](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245) for how to use this feature.

**Enable** Boolean `Optional` `Example: true`

Whether to enable.

* `false` (default): Disable.

* `true`: Enable.

**SnapshotConfig** Object `Optional` `Example: -`

Snapshot configuration.

**StreamType** Integer `Optional` `Example: 0`

Screenshot stream types:

* `0` (default): Main stream.

* `1`: Screen stream.

**ImageDetail** String `Optional` `Example: auto`

Image processing modes.

* `high`: High\-detail mode. It is suitable for scenarios that require understanding of detailed image information, such as extracting multiple local information/features from images and understanding images with complex/rich details. It provides a more comprehensive understanding.

* `low`: Low\-detail mode. It is suitable for simple image classification/recognition, overall content understanding/description, and other scenarios. It enables faster understanding.

* `auto` (default): Auto mode. It automatically selects an appropriate mode based on the image resolut

**Height** Integer `Optional` `Example: 640`

The height of the video frame captured for the large model. The value range is `[0, 1792]`, and the unit is pixel.

If this parameter is not provided or is set to `0`, it defaults to `360`.

The frame width is automatically calculated to maintain the aspect ratio based on the provided height.

**Interval** Integer `Optional` `Example: 1000`

The interval between adjacent screenshots. The value range is `[100, 5000]` in milliseconds. The default value is `1000`.

**ImagesLimit** Integer `Optional` `Example: 2`

The number of screenshots sent to the large model at a time. The value range is `[0, 50]`.

If this parameter is not provided or is set to `0`, it defaults to `2`.

**StorageConfig** Object `Optional` `Example: -`

Storage configuration.

**Type** Integer `Optional` `Example: 0`

Storage type.

* `0` (default): Store in the server cache in Base 64 encoding and automatically delete it after the session ends.

* `1`: Store on the TOS platform. Before using TOS storage, you need to go to the [console](https://console.byteplus.com/tos/bucket) to enable this service.

**TosConfig** Object `Optional` `Example: -`

TOS storage configuration.

**AccountId** String 必选 `Example: acc****_id`

BytePlus AccountId.You can find it by clicking the account icon in the top\-right corner.

Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID.

**Region** Integer `Optional` `Example: 0`

Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1167931).

The default value is `0`.

**Bucket** String 必选 `Example: b****t`

Name of bucket you created on TOS platform.

**Tools** Object[] `Optional` `Example: -`

List of tools that the model can call, when using Function Calling.

Only functions are supported as tools, and a list of functions with JSON inputs generated by the model is provided. Refer to [Function Calling](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1554654) for how to use this feature.

> **tip**

> If you need to use this feature, all parameters in this structure are required.

**type** String `Optional` `Example: function`

Tool type. Must be `function`.

**function** Object `Optional` `Example: -`

The list of tools that the model can call.

**name** String 必选 `Example: get_current_weather`

Name of function.

**description** String `Optional` `Example: Get weather information for a specified city.`

Description of the function's purpose for the model to determine when and how to call this tool function.

**parameters** JSONMap `Optional` `Example: {"type": "object","properties": {"location": {"type": "string","description": "City, such as: London"},},"required": ["location"]}`

Function request parameters are described in JSON Schema format. For specific format, please refer to the [JSON Schema](https://json-schema.org/understanding-json-schema) document.

**EnableToolCallHistory** Boolean `Optional` `Example: false`

Whether to retain the tool call instructions and tool return results generated during Function Calling in the conversation history of subsequent LLM requests.

* `false` (default): Do not retain them.

* `true`: Retain them. If Function Calling is triggered in a given turn, the conversation history for that turn will include not only the user's input and the final response, but also the intermediate tool call instructions and tool return results. If Function Calling is not triggered in that turn, only the user's input and the final response will be retained.

> **warning**

* > This parameter takes effect only when `Tools` is configured and Function Calling is actually triggered.

* > Tool call instructions and tool return results do not count as an additional turn toward `HistoryLength`. Instead, they are retained and evicted together with the dialog turn to which they belong.

**MCP** Object[] `Optional` `Example: -`

Configure MCP for connecting to knowledge bases and other external tool services. For detailed configuration instructions, refer to [Integrate MCP](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856160).

> **warning**

* > This feature is only supported by BytePlus ModelArk models that support Function Calling. For best results, we recommend using the `seed-1.6` model. For a detailed list, see [Model List\-Tool use](https://docs.byteplus.com/en/docs/modelark/model-list#f44ceef7).

* > Your MCP Server's response format must be Server\-Sent Events (SSE).

**URL** String 必选 `Example: https://knowledge-mcp-server.com/test/123`

The endpoint URL of your remote MCP Server.

**Name** String 必选 `Example: knowledge`

A custom, unique identifier for this MCP service.

This name is used by the LLM to distinguish the tool's origin and by the system to route the invocation request to the correct MCP Server.

> **warning**

> This name must not conflict with any tool names defined in the AskEcho Search Agent (`WebSearchAgentConfig.FunctionName`) or in Function Calling (`Tools.function.name`).

**ComfortWords** String `Optional` `Example: "Processing your request..."`

A user\-facing message played via TTS when the agent invokes an MCP tool. This message improves the user experience during the wait.

If empty or not provided, no message is played.

**InterestedTools** String[] `Optional` `Example: ["search_knowledge"]`

Specifies a list of tools to load into the LLM's context, making them available for the LLM to decide on and invoke.

* **If empty or not provided**: All tools from this MCP Server will be loaded into the LLM's context.

* **If populated**: Only the specified tools will be loaded into the LLM's context.

Amazon LLM

**AutoActive** Boolean `Optional` `Example: true`

Whether to enable LLMConfig configuration.

* `true` (default): Enable.

* `false`: Disable. After disabling, `LLMConfig` and `TTSConfig` will take no effect.

**Provider** String 必选 `Example: Amazon`

Provider name. Must be `Amazon`.

**ModelName** String 必选 `Example: arn:aws:bedrock:us-west-2:******:inference-profile/us.amazon.nova-pro-v1:0`

Amazon model.

**Region** String 必选 `Example: us-west-2`

Region. Acquire on [Amazon console](https://console.aws.amazon.com/iam/).

**AccessKeyId** String 必选 `Example: 123****214`

Amazon Access key ID. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**SecretAccessKey** String 必选 `Example: 32****dad`

Amazon Secret Access Key. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**SystemMessages** String[] `Optional` `Example: ["You are an assistant, with a humorous and understanding personality."]`

System messages, used to input instructions that control the behavior of large language models, defining the model's role, behavioral guidelines, specific output formats, etc.

**UserPrompts** Object[] `Optional` `Example: [ { "Role": "user", "Content": "hello" }, { "Role": "assistant", "Content": "What can I do for you？" }]`

User prompts, used to enhance the quality of the model's responses. When the model generates responses, it will preferentially refer to the content here to guide the model to generate specific outputs or perform specific tasks.

The conversation content stored in `UserPrompts` is controlled by `HistoryLength`. For example, if two rounds of conversations are pre\-stored in `UserPrompts`, `HistoryLength` is set to 3, and the user has already had three rounds of conversations, when the fourth round of conversation starts, all the content stored in `UserPrompts` will be deleted.

**HistoryLength** Integer `Optional` `Example: 3`

Number of historical question rounds. The default value is `3`.

When calling this interface, it is necessary to ensure that the total length of all `UserPrompts` and `SystemMessage` text does not exceed the context length of the large language model.

For example, if the number of historical question rounds is `3`, and the `Skylark2-lite-8k` large language model with a length limit of 8k is used, and two rounds of conversations are pre\-stored in `UserPrompts`. When the user inputs the question of the first round of conversation, the total length of the `SystemMessage`, `UserPrompts`, and the question of the first round of conversation should not exceed 8k.

**TopP** Float `Optional` `Example: 0.3`

An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered.

Limited to `[0, 1]`, default to `0.3`。

**Temperature** Float `Optional` `Example: 0.1`

The sampling temperature, limited to `(0, 1]`, default to `0.1`.

Higher values like `0.8` will make the output more random, while lower values like `0.2` will make it more focused and deterministic.

**MaxTokens** Integer `Optional` `Example: 1024`

The maximum token limit of the output text, does not include chain\-of\-thought content.

* Default to `1024`.

* The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

> When `ThinkingType=enabled` or `auto` and you want to control the total output budget (including reasoning tokens), use `MaxCompletionTokens` instead.

**MaxCompletionTokens** Integer `Optional` `Example: 4096`

The maximum number of tokens the model can generate in its completion, including both the visible response and any internal reasoning tokens (chain\-of\-thought).

* Value range: A positive integer (\> 0). The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

* When not set, the field is not passed to the model, and `MaxTokens` remains in effect.

**ReasoningEffort** String `Optional` `Example: low`

Controls the level of reasoning effort (depth of thinking) for the large model. Use this parameter to balance response quality, latency, and token cost.

* Available values: `minimal`, `low`, `medium`, `high`.

* If not set, the parameter is not passed to the model, and the model uses its own default behavior.

**VisionConfig** Object `Optional` `Example: -`

Vision Config. Refer to [Vision Understanding](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245) for how to use this feature.

**Enable** Boolean `Optional` `Example: true`

Whether to enable.

* `false` (default): Disable.

* `true`: Enable.

**SnapshotConfig** Object `Optional` `Example: -`

Snapshot configuration.

**StreamType** Integer `Optional` `Example: 0`

Screenshot stream types:

* `0` (default): Main stream.

* `1`: Screen stream.

**ImageDetail** String `Optional` `Example: auto`

Image processing modes.

* `high`: High\-detail mode. It is suitable for scenarios that require understanding of detailed image information, such as extracting multiple local information/features from images and understanding images with complex/rich details. It provides a more comprehensive understanding.

* `low`: Low\-detail mode. It is suitable for simple image classification/recognition, overall content understanding/description, and other scenarios. It enables faster understanding.

* `auto` (default): Auto mode. It automatically selects an appropriate mode based on the image resolution.

**Height** Integer `Optional` `Example: 640`

The height of the video frame captured for the large model. The value range is `[0, 1792]`, and the unit is pixel.

If this parameter is not filled in or `0` is passed, it will be automatically modified to `360`.

The width of the video frame captured for the large model will be automatically calculated proportionally based on the passed\-in height.

**Interval** Integer `Optional` `Example: 1000`

The interval between adjacent screenshots. The value range is `[100, 5000]` in milliseconds. The default value is `1000`.

**ImagesLimit** Integer `Optional` `Example: 2`

The number of screenshots sent to the large model at a time. The value range is `[0, 50]`.

If this parameter is not passed or `0` is passed, it will be automatically modified to `2`.

**StorageConfig** Object `Optional` `Example: -`

Storage configuration.

**Type** Integer `Optional` `Example: 0`

Storage type.

* `0` (defalut): Store in the server cache in Base 64 encoding and automatically delete it after the session ends.

* `1`: Store on the TOS platform. Before using TOS storage, you need to go to the [console](https://console.byteplus.com/tos/bucket) to enable this service.

**TosConfig** Object `Optional` `Example: -`

TOS storage configuration.

**AccountId** String 必选 `Example: acc****_id`

BytePlus AccountId.You can find it by clicking the account icon in the top\-right corner.

Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID.

**Region** Integer `Optional` `Example: 0`

Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1167931).

The default value is `0`.

**Bucket** String 必选 `Example: b****t`

Name of bucket you created on TOS platform.

Google LLM

**AutoActive** Boolean `Optional` `Example: true`

Whether to enable LLMConfig configuration.

* `true` (default): Enable.

* `false`: Disable. After disabling, `LLMConfig` and `TTSConfig` will take no effect.

**Provider** String 必选 `Example: Google`

Provider name. Must be `Google`.

**Url** String 必选 `Example: https://generativelanguage.googleapis.com/v1beta/models`

Google LLM server endpoint. Must be `https://generativelanguage.googleapis.com/v1beta/models`.

**ModelName** String 必选 `Example: gemini-2.0-flash`

Google model name, see [Supported models](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-garden/available-models).

**APIKey** String 必选 `Example: a****31`

API Key. [How to get a Google Cloud API key?](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/start/api-keys)

**SystemMessages** String[] `Optional` `Example: ["You are an assistant, with a humorous and understanding personality."]`

System messages, used to input instructions that control the behavior of large language models, defining the model's role, behavioral guidelines, specific output formats, etc.

**UserPrompts** Object[] `Optional` `Example: [ { "Role": "user", "Content": "hello" }, { "Role": "assistant", "Content": "What can I do for you？" }]`

User prompts, used to enhance the quality of the model's responses. When the model generates responses, it will preferentially refer to the content here to guide the model to generate specific outputs or perform specific tasks.

The conversation content stored in `UserPrompts` is controlled by `HistoryLength`. For example, if two rounds of conversations are pre\-stored in `UserPrompts`, `HistoryLength` is set to 3, and the user has already had three rounds of conversations, when the fourth round of conversation starts, all the content stored in `UserPrompts` will be deleted.

**HistoryLength** Integer `Optional` `Example: 3`

Number of historical question rounds. The default value is `3`.

When calling this interface, it is necessary to ensure that the total length of all `UserPrompts` and `SystemMessage` text does not exceed the context length of the large language model.

For example, if the number of historical question rounds is `3`, and the `Skylark2-lite-8k` large language model with a length limit of 8k is used, and two rounds of conversations are pre\-stored in `UserPrompts`. When the user inputs the question of the first round of conversation, the total length of the `SystemMessage`, `UserPrompts`, and the question of the first round of conversation should not exceed 8k.

**Temperature** Float `Optional` `Example: 0.1`

The sampling temperature, limited to `(0, 1]`, default to `0.1`.

Higher values like `0.8` will make the output more random, while lower values like `0.2` will make it more focused and deterministic.

**TopP** Float `Optional` `Example: 0.3`

An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered.

Limited to `[0, 1]`, default to `0.3`。

**MaxTokens** Integer `Optional` `Example: 1024`

The maximum token limit of the output text, does not include chain\-of\-thought content.

* Default to `1024`.

* The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

> When `ThinkingType=enabled` or `auto` and you want to control the total output budget (including reasoning tokens), use `MaxCompletionTokens` instead.

**MaxCompletionTokens** Integer `Optional` `Example: 4096`

The maximum number of tokens the model can generate in its completion, including both the visible response and any internal reasoning tokens (chain\-of\-thought).

* Value range: A positive integer (\> 0). The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

* When not set, the field is not passed to the model, and `MaxTokens` remains in effect.

**ReasoningEffort** String `Optional` `Example: low`

Controls the level of reasoning effort (depth of thinking) for the large model. Use this parameter to balance response quality, latency, and token cost.

* Available values: `minimal`, `low`, `medium`, `high`.

* If not set, the parameter is not passed to the model, and the model uses its own default behavior.

**VisionConfig** Object `Optional` `Example: -`

Vision Config. Refer to [Vision Understanding](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245) for how to use this feature.

**Enable** Boolean `Optional` `Example: true`

Whether to enable.

* `false` (default): Disable.

* `true`: Enable.

**SnapshotConfig** Object `Optional` `Example: -`

Snapshot configuration.

**StreamType** Integer `Optional` `Example: 0`

Screenshot stream types:

* `0` (default): Main stream.

* `1`: Screen stream.

**ImageDetail** String `Optional` `Example: auto`

Image processing modes.

* `high`: High\-detail mode. It is suitable for scenarios that require understanding of detailed image information, such as extracting multiple local information/features from images and understanding images with complex/rich details. It provides a more comprehensive understanding.

* `low`: Low\-detail mode. It is suitable for simple image classification/recognition, overall content understanding/description, and other scenarios. It enables faster understanding.

* `auto` (default): Auto mode. It automatically selects an appropriate mode based on the image resolution.

**Height** Integer `Optional` `Example: 640`

The height of the video frame captured for the large model. The value range is `[0, 1792]`, and the unit is pixel.

If this parameter is not provided or is set to `0`, it defaults to `360`.

The frame width is automatically calculated to maintain the aspect ratio based on the provided height.

**Interval** Integer `Optional` `Example: 1000`

The interval between adjacent screenshots. The value range is `[100, 5000]` in milliseconds. The default value is `1000`.

**ImagesLimit** Integer `Optional` `Example: 2`

The number of screenshots sent to the large model at a time. The value range is `[0, 50]`.

If this parameter is not provided or is set to `0`, it defaults to `2`.

**StorageConfig** Object `Optional` `Example: -`

Storage configuration.

**Type** Integer `Optional` `Example: 0`

Storage type.

* `0`: Store in the server cache in Base 64 encoding and automatically delete it after the session ends.

OpenAI LLM

**AutoActive** Boolean `Optional` `Example: true`

Whether to enable LLMConfig configuration.

* `true` (default): Enable.

* `false`: Disable. After disabling, `LLMConfig` and `TTSConfig` will take no effect.

**Provider** String 必选 `Example: OpenAI`

Provider name. Must be `OpenAI`.

**Url** String 必选 `Example: https://api.openai.com/v1/chat/completions`

URL. Must be `https://api.openai.com/v1/chat/completions`.

**ModelName** String 必选 `Example: gpt-4o-2024-05-13`

OpenAPI model. Acquire on [models](https://platform.openai.com/docs/models#tts).

**APIKey** String 必选 `Example: a****31`

APIKey. Acquire on [api-keys](https://platform.openai.com/api-keys).

**SystemMessages** String[] `Optional` `Example: ["You are an assistant, with a humorous and understanding personality."]`

System messages, used to input instructions that control the behavior of large language models, defining the model's role, behavioral guidelines, specific output formats, etc.

**UserPrompts** Object[] `Optional` `Example: [ { "Role": "user", "Content": "hello" }, { "Role": "assistant", "Content": "What can I do for you？" }]`

User prompts, used to enhance the quality of the model's responses. When the model generates responses, it will preferentially refer to the content here to guide the model to generate specific outputs or perform specific tasks.

The conversation content stored in `UserPrompts` is controlled by `HistoryLength`. For example, if two rounds of conversations are pre\-stored in `UserPrompts`, `HistoryLength` is set to 3, and the user has already had three rounds of conversations, when the fourth round of conversation starts, all the content stored in `UserPrompts` will be deleted.

**HistoryLength** Integer `Optional` `Example: 3`

Number of historical question rounds. The default value is `3`.

When calling this interface, it is necessary to ensure that the total length of all `UserPrompts` and `SystemMessage` text does not exceed the context length of the large language model.

For example, if the number of historical question rounds is `3`, and the `Skylark2-lite-8k` large language model with a length limit of 8k is used, and two rounds of conversations are pre\-stored in `UserPrompts`. When the user inputs the question of the first round of conversation, the total length of the `SystemMessage`, `UserPrompts`, and the question of the first round of conversation should not exceed 8k.

**Temperature** Float `Optional` `Example: 0.1`

The sampling temperature, limited to `(0, 1]`, default to `0.1`.

Higher values like `0.8` will make the output more random, while lower values like `0.2` will make it more focused and deterministic.

**TopP** Float `Optional` `Example: 0.3`

An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered.

Limited to `[0, 1]`, default to `0.3`。

**MaxTokens** Integer `Optional` `Example: 1024`

The maximum token limit of the output text, does not include chain\-of\-thought content.

* Default to `1024`.

* The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

> When `ThinkingType=enabled` or `auto` and you want to control the total output budget (including reasoning tokens), use `MaxCompletionTokens` instead.

**MaxCompletionTokens** Integer `Optional` `Example: 4096`

The maximum number of tokens the model can generate in its completion, including both the visible response and any internal reasoning tokens (chain\-of\-thought).

* Value range: A positive integer (\> 0). The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

* When not set, the field is not passed to the model, and `MaxTokens` remains in effect.

**ReasoningEffort** String `Optional` `Example: low`

Controls the level of reasoning effort (depth of thinking) for the large model. Use this parameter to balance response quality, latency, and token cost.

* Available values: `minimal`, `low`, `medium`, `high`.

* If not set, the parameter is not passed to the model, and the model uses its own default behavior.

ThirdParty LLM

**AutoActive** Boolean `Optional` `Example: true`

Whether to enable LLMConfig configuration.

* `true` (default): Enable.

* `false`: Disable. After disabling, `LLMConfig` and `TTSConfig` will take no effect.

**Mode** String 必选 `Example: CustomLLM`

Mode of LLM platform. Must be `CustomLLM`.

**Url** String 必选 `Example: https://api.openai.com/v1/chat/completions`

API endpoint.

**ModelName** String 必选 `Example: gpt-4o-2024-05-13`

Model name.

**APIKey** String 必选 `Example: a****31`

APIKey for authentication.

**SystemMessages** String[] `Optional` `Example: ["You are an assistant, with a humorous and understanding personality."]`

System messages, used to input instructions that control the behavior of large language models, defining the model's role, behavioral guidelines, specific output formats, etc.

**UserPrompts** Object[] `Optional` `Example: [ { "Role": "user", "Content": "hello" }, { "Role": "assistant", "Content": "What can I do for you？" }]`

User prompts, used to enhance the quality of the model's responses. When the model generates responses, it will preferentially refer to the content here to guide the model to generate specific outputs or perform specific tasks.

The conversation content stored in `UserPrompts` is controlled by `HistoryLength`. For example, if two rounds of conversations are pre\-stored in `UserPrompts`, `HistoryLength` is set to 3, and the user has already had three rounds of conversations, when the fourth round of conversation starts, all the content stored in `UserPrompts` will be deleted.

**HistoryLength** Integer `Optional` `Example: 3`

Number of historical question rounds. The default value is `3`.

When calling this interface, it is necessary to ensure that the total length of all `UserPrompts` and `SystemMessage` text does not exceed the context length of the large language model.

For example, if the number of historical question rounds is `3`, and the `Skylark2-lite-8k` large language model with a length limit of 8k is used, and two rounds of conversations are pre\-stored in `UserPrompts`. When the user inputs the question of the first round of conversation, the total length of the `SystemMessage`, `UserPrompts`, and the question of the first round of conversation should not exceed 8k.

**MaxTokens** Integer `Optional` `Example: 1024`

The maximum token limit of the output text, does not include chain\-of\-thought content.

* Default to `1024`.

* The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

> When `ThinkingType=enabled` or `auto` and you want to control the total output budget (including reasoning tokens), use `MaxCompletionTokens` instead.

**MaxCompletionTokens** Integer `Optional` `Example: 4096`

The maximum number of tokens the model can generate in its completion, including both the visible response and any internal reasoning tokens (chain\-of\-thought).

* Value range: A positive integer (\> 0). The actual upper limit depends on the output window size of the model being used.

* Mutually exclusive with `MaxTokens`: The two parameters **cannot be set at the same time**. If both are provided, the API returns a parameter error.

* When not set, the field is not passed to the model, and `MaxTokens` remains in effect.

**ReasoningEffort** String `Optional` `Example: low`

Controls the level of reasoning effort (depth of thinking) for the large model. Use this parameter to balance response quality, latency, and token cost.

* Available values: pass\-through; accepted values depend on the third\-party model.

* If not set, the parameter is not passed to the model, and the model uses its own default behavior.

**Custom** String `Optional` `Example: -`

Customize JSON string. You can pass in business\-specific custom parameters.

**Tools** Object[] `Optional` `Example: -`

List of tools that the model can call, when using Function Calling.

Only functions are supported as tools, and a list of functions with JSON inputs generated by the model is provided. Refer to [Function Calling](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1554654) for how to use this feature.

> **tip**

> If you need to use this feature, all parameters in this structure are required.

**type** String 必选 `Example: function`

Tool type. Must be `function`.

**function** Object 必选 `Example: -`

The list of tools that the model can call.

**name** String 必选 `Example: get_current_weather`

Name of function.

**description** String `Optional` `Example: Get weather information for a specified city.`

Description of the function's purpose for the model to determine when and how to call this tool function.

**parameters** JSONMap `Optional` `Example: {"type": "object","properties": {"location": {"type": "string","description": "City, such as: London"},},"required": ["location"]}`

Function request parameters, described in JSON Schema format. For the specific format, please refer to the [JSON Schema](https://json-schema.org/understanding-json-schema) documentation.

**EnableToolCallHistory** Boolean `Optional` `Example: false`

Whether to retain the tool call instructions and tool return results generated during Function Calling in the conversation history of subsequent LLM requests.

* `false` (default): Do not retain them.

* `true`: Retain them. If Function Calling is triggered in a given turn, the conversation history for that turn will include not only the user's input and the final response, but also the intermediate tool call instructions and tool return results. If Function Calling is not triggered in that turn, only the user's input and the final response will be retained.

> **warning**

* > This parameter takes effect only when `Tools` is configured and Function Calling is actually triggered.

* > Tool call instructions and tool return results do not count as an additional turn toward `HistoryLength`. Instead, they are retained and evicted together with the dialog turn to which they belong.

**MCP** Object[] `Optional` `Example: -`

Configure MCP for connecting to knowledge bases and other external tool services. For detailed configuration instructions, refer to [Integrate MCP](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856160).

> **warning**

> Your MCP Server's response format must be Server\-Sent Events (SSE).

**URL** String 必选 `Example: https://knowledge-mcp-server.com/test/123`

The endpoint URL of your remote MCP Server.

**Name** String 必选 `Example: knowledge`

A custom, unique identifier for this MCP service. This name is used by the LLM to distinguish the tool's origin and by the system to route the invocation request to the correct MCP Server.

> **warning**

> This name must not conflict with any tool names defined in the AskEcho Search Agent (`WebSearchAgentConfig.FunctionName`) or in Function Calling (`Tools.function.name`).

**ComfortWords** String `Optional` `Example: Processing your request...`

A user\-facing message played via TTS when the agent invokes an MCP tool. This message improves the user experience during the wait. If empty or not provided, no message is played.

**InterestedTools** String[] `Optional` `Example: ["search_knowledge"]`

Specifies a list of tools to load into the LLM's context, making them available for the LLM to decide on and invoke.

* **If empty or not provided**: All tools from this MCP Server will be loaded into the LLM's context.

* **If populated**: Only the specified tools will be loaded into the LLM's context.

**VisionConfig** Object `Optional` `Example: -`

Vision Config. Refer to [Vision Understanding](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245) for how to use this feature.

**Enable** Boolean `Optional` `Example: true`

Whether to enable.

* `false`: Disable.

* `true`: Enable.

   Defauls to `false`.

**SnapshotConfig** Object `Optional` `Example: -`

Snapshot configuration.

**StreamType** Integer `Optional` `Example: 0`

Screenshot stream types:

* `0` (default): Main stream.

* `1`: Screen stream.

**ImageDetail** String `Optional` `Example: auto`

Image processing modes.

* `high`: High\-detail mode. It is suitable for scenarios that require understanding of detailed image information, such as extracting multiple local information/features from images and understanding images with complex/rich details. It provides a more comprehensive understanding.

* `low`: Low\-detail mode. It is suitable for simple image classification/recognition, overall content understanding/description, and other scenarios. It enables faster understanding.

* `auto` (default): Auto mode. It automatically selects an appropriate mode based on the image resolution.

**Height** Integer `Optional` `Example: 640`

The height of the video frame captured for the large model. The value range is `[0, 1792]`, and the unit is pixel.

If this parameter is not provided or is set to `0`, it defaults to `360`.

The frame width is automatically calculated to maintain the aspect ratio based on the provided height.

**Interval** Integer `Optional` `Example: 1000`

The interval between adjacent screenshots. The value range is `[100, 5000]` in milliseconds. The default value is `1000`.

**ImagesLimit** Integer `Optional` `Example: 2`

The number of screenshots sent to the large model at a time. The value range is `[0, 50]`.

If this parameter is not provided or is set to `0`, it defaults to `2`.

**StorageConfig** Object `Optional` `Example: -`

Storage configuration.

**Type** Integer `Optional` `Example: 0`

Storage type.

* `0` (defalut): Store in the server cache in Base 64 encoding and automatically delete it after the session ends.

* `1`: Store on the TOS platform. Before using TOS storage, you need to go to the [console](https://console.byteplus.com/tos/bucket) to enable this service.

**TosConfig** Object `Optional` `Example: -`

TOS storage configuration.

**AccountId** String 必选 `Example: acc****_id`

BytePlus AccountId.You can find it by clicking the account icon in the top\-right corner.

Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID.

**Region** Integer `Optional` `Example: 0`

Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1167931).

The default value is `0`.

**Bucket** String 必选 `Example: b****t`

Name of the bucket you created on TOS platform.

**TTSConfig** Object 必选 `Example: -`

Config for TTS.

**AutoActive** Boolean `Optional` `Example: true`

Whether to enable `TTSConfig`.

* `true` (default): Enable.

* `false`: Disable. After disabling, `TTSConfig` becomes invalid, and `SubtitleMode: 0` (timestamp\-aligned subtitles) and `SubtitleMode: 1` (fast subtitles) are also unavailable. This does not affect `ASRConfig` and `LLMConfig`.

**Provider** String 必选 `Example: OpenAI`

TTS provider.

* `OpenAI`: OpenAI TTS

* `Amazon`: Amazon TTS

* `BytePlus`: BytePlus TTS

* `Google`: Google TTS

* `Elevenlabs`: ElevenLabs TTS

* `minimax_bidirection`: MiniMax bidirectional streaming TTS

* `ai_gateway`: Self\-hosted TTS

**ProviderParams** Object `Optional` `Example: -`

Configuration parameters of different TTS providers:

OpenAI TTS

**URL** String 必选 `Example: https://api.openai.com/v1/audio/speech`

URL. Must be the value: `https://api.openai.com/v1/audio/speech`.

**APIKey** String 必选 `Example: 234****2nd`

APIKey. Acquire on [api-keys](https://platform.openai.com/api-keys).

**Model** String 必选 `Example: tts-1`

OpenAPI model. Acquire on [models](https://platform.openai.com/docs/models#tts).

**Voice** String 必选 `Example: alloy`

Voice type. Acquire on [Voice options](https://platform.openai.com/docs/guides/text-to-speech#voice-options).

**Speed** String 必选 `Example: 1`

Voice's speed. Must be the value: `1.0`.

Amazon TTS

**ID** String 必选 `Example: 13****413`

Amazon Access key ID. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**Secret** String 必选 `Example: 13****a12`

Amazon Secret access key. For detail, see [Create new access keys for an IAM user](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html).

**VoiceID** String 必选 `Example: Celine`

Voice ID. Acquire on [Available voice](https://docs.aws.amazon.com/polly/latest/dg/available-voices.html).

**Region** String 必选 `Example: us-west-2`

Region. Acquire on [Amazon console](https://console.aws.amazon.com/iam/).

**Language** String 必选 `Example: zh-CN`

Language code. Acquire on [Supported languages and language-specific features](https://docs.aws.amazon.com/transcribe/latest/dg/supported-languages.html).

BytePlus TTS_Text\-to\-Speech (Parameter Pass\-through)

This method supports all configuration parameters of the BytePlus TTS, offering greater flexibility and more comprehensive features compared to direct parameter passing.

**Credential** Object 必选 `Example: -`

Authentication parameters for BytePlus TTS (Text\-to\-Speech) service.

**ApiKey** String 必选 `Example: bpAK****11`

API key used for BytePlus Seed TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys).

> **tip**

> The existing `AppId` and `Token` authentication method remains supported for backward compatibility.

**ResourceId** String 必选 `Example: seed-tts-2.0`

Choose the BytePlus TTS (Text\-to\-Speech) version:

* `volc.service_type.1000009`: BytePlus TTS (Text\-to\-Speech) 1.0

* `seed-tts-2.0`: BytePlus TTS (Text\-to\-Speech) 2.0

   For the differences between the two versions, see [TTS 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/texttospeechv2) and [TTS 1.0](https://docs.byteplus.com/en/docs/byteplusvoice/texttospeechv_1).

**SeedTTSParameters** String `Optional` `Example: "{\"req_params\":{\"speaker\":\"zh_female_cancan_mars_bigtts\"}}"`

A single\-line, minified, and escaped JSON string for passing custom parameters to the BytePlus TTS (Text\-to\-Speech) service.

**How to Configure This Field:**  Construct a JSON object based on the Payload request parameters from the documentation [TTS - Bi-directional Streaming (WebSocket)](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts), following the rules below. Once built, convert it into a single\-line, escaped string.

* **Required parameters:**  Must include the parameter `req_params.speaker`, which can be obtained on [BytePlus Text-to-Speech Console](https://console.byteplus.com/voice/service/1000014?).

* **Forbidden parameters:**  Do not include the following parameters:

   * user

   * event

   * namespace

   * req_params.text

   * req_params.audio_params.format

   * req_params.audio_params.enable_timestamp

   * req_params.additions.max_length_to_filter_parenthesis

   * req_params.additions.cache_config, req_params.additions.enable_latex_tn: When using TTS 2.0 (ResourceId is `seed-tts-2.0`), this field cannot be passed if `SubtitleMode` is set to 0.

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

This method encapsulates some of the common parameters for the the BytePlus TTS. It simplifies integration but does not provide access to the service's full range of features.

**app** Object 必选 `Example: -`

BytePlus TTS (Text\-to\-Speech) application configuration.

**apikey** String 必选 `Example: bpAK****11`

API key used for BytePlus Seed TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys).

> **tip**

> The existing `appid` and `token` authentication method remains supported for backward compatibility.

**audio** Object 必选 `Example: -`

BytePlus TTS (Text\-to\-Speech) audio configuration.

**voice_type** String 必选 `Example: zh_female_cancan_mars_bigtts`

Voice_type of purchased timbre on [BytePlus Text-to-Speech Console](https://console.byteplus.com/voice/service/1000014?).

**pitch_rate** Float `Optional` `Example: 0`

Pitch, limited to `[-12,12]`. Defaults to `0`.

**speech_rate** Integer `Optional` `Example: 0`

Speech speed, limited to `[-50, 100]`. Default to `0`.

`100` represents 2.0x speed, and `-50` represents 0.5x speed.

**ResourceId** String 必选 `Example: seed-tts-2.0`

Choose the BytePlus TTS (Text\-to\-Speech) versions:

* `volc.service_type.1000009`: BytePlus TTS (Text\-to\-Speech) 1.0

* `seed-tts-2.0`: BytePlus TTS (Text\-to\-Speech) 2.0

   For the differences between the two versions, see [TTS 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/texttospeechv2) and [TTS 1.0](https://docs.byteplus.com/en/docs/byteplusvoice/texttospeechv_1).

**additions** Object `Optional` `Example: -`

BytePlus Text\-to\-Speech advanced configuration.

**enable_latex_tn** Boolean `Optional` `Example: false`

Read LaTeX formulas aloud.

When enabled, the agent will read LaTeX\-formatted mathematical formulas using natural language instead of just speaking the raw characters.

* `false` (default): Disable.

* `true`: Enable. For this to take effect, `disable_markdown_filter` must also be true.

**Example**:

* LLM Response: `According to the formula a^2 + b^2 = c^2...`

* Agent Speaks: `According to the formula a squared plus b squared equals c squared...`

* Subtitles Show: `According to the formula a^2 + b^2 = c^2...`

> **warning**

* > When using BytePlus TTS (Text\-to\-Speech) 2.0 (`ResourceId` is `seed-tts-2.0`), this field cannot be passed if `SubtitleMode` is set to 0.

* > When using the Voice Replication 2.0, if you need to set `SubtitleMode: 0`, you must disable the `enable_latex_tn` (broadcast LaTeX formulas) feature.

* > When `SubtitleMode` is 1, it is expected behavior for the subtitle to receive the following italicized content: `{"definite": true, "paragraph": true, "roundId": 4, "text": ""}`.

**disable_markdown_filter** Boolean `Optional` `Example: false`

Filters Markdown formatting from the LLM's text before speech synthesis.

* `true`: Enable filtering. For example, `**hello**` will be pronounced as hello.

* `false` (Default): No filtering.

**Example:**

* LLM Response: `Please run the **grep** command to view the logs.`

* Agent Speaks: `Please run the grep command to view the logs.`

* Subtitles Show: `Please run the **grep** command to view the logs.`

**enable_language_detector** Boolean `Optional` `Example: false`

Whether to automatically recognize the language.

* `true`: Enable to automatically recognize.

* `false` (default): Disable to automatically recognize.

BytePlus TTS_Voice Replication (Parameter Pass\-through)

This method supports all configuration parameters of the BytePlus TTS (Voice Replication), offering greater flexibility and more comprehensive features compared to direct parameter passing.

**Credential** Object 必选 `Example: -`

Authentication parameters for BytePlus TTS (Voice Replication) service.

**ApiKey** String 必选 `Example: bpAK****11`

API key used for BytePlus Seed TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys).

> **tip**

> The existing `AppId` and `Token` authentication method remains supported for backward compatibility.

**ResourceId** String 必选 `Example: seed-icl-2.0`

Choose the BytePlus TTS (Voice Replication) version:

* `seed-icl-1.0` or `volc.megatts.defaul`: BytePlus TTS (Voice Replication) 1.0

* `seed-icl-2.0`: BytePlus TTS (Voice Replication) 2.0

For the differences between the two versions, see [Voice Replication 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplicationv2).

**SeedTTSParameters** String 必选 `Example: {\"req_params\":{\"speaker\":\"zh_female_cancan_mars_bigtts\"}}"`

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

This method encapsulates some of the common parameters for the the BytePlus TTS (Voice Replication ). It simplifies integration but does not provide access to the service's full range of features.

**app** Object 必选 `Example: -`

BytePlus TTS (Voice Replication) application configuration.

**apikey** String 必选 `Example: bpAK****11`

API key used for BytePlus Seed TTS authentication. Create or obtain an API key in the [Seed Speech console](https://console.byteplus.com/voice/new/setting/apikeys).

> **tip**

> The existing `AppId` and `Token` authentication method remains supported for backward compatibility.

**audio** Object 必选 `Example: -`

BytePlus TTS (Voice Replication) audio configuration.

**voice_type** String 必选 `Example: S_N****7k1`

Speaker ID for the BytePlus TTS (Voice Replication) service. You need to purchase and train the voice in the [BytePlus Voice Replication Console](https://console.byteplus.com/voice/service/1000016?) first. For detailed instructions, refer to the [Voice Replication Order and Usage Guide](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication).

**pitch_rate** Float `Optional` `Example: 0`

Pitch, limited to `[-12, 12]`. Defaults to `0`.

**speech_rate** Integer `Optional` `Example: 0`

Speech speed, limited to `[-50, 100]`. Default to `0`.

`100` represents 2.0x speed, and `-50` represents 0.5x speed.

**ResourceId** String 必选 `Example: seed-icl-2.0`

Choose the BytePlus TTS (Voice Replication) version:

* `seed-icl-1.0` or `volc.megatts.defaul`: BytePlus TTS (Voice Replication) 1.0

* `seed-icl-2.0`: BytePlus TTS (Voice Replication) 2.0

   For the differences between the two versions, see [Voice Replication 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplicationv2).

**additions** Object `Optional` `Example: -`

BytePlus Voice Replication advanced configuration.

**enable_latex_tn** Boolean `Optional` `Example: false`

Read LaTeX formulas aloud.

When enabled, the agent will read LaTeX\-formatted mathematical formulas using natural language instead of just speaking the raw characters.

* `false` (default): Disable.

* `true`: Enable. For this to take effect,`disable_markdown_filter` must also be true.

   **Example**:

* LLM Response: `According to the formula a^2 + b^2 = c^2...`

* Agent Speaks: `According to the formula a squared plus b squared equals c squared...`

* Subtitles Show: `According to the formula a^2 + b^2 = c^2...`

> **warning**

* > When using Voice Replication 2.0 (`ResourceId` is `seed-icl-2.0`), this field cannot be passed if `SubtitleMode` is set to 0.

* > When using the Voice Replication 2.0, if you need to set `SubtitleMode: 0`, you must disable the `enable_latex_tn` (broadcast LaTeX formulas) feature.

* > When `SubtitleMode` is 1, it is expected behavior for the subtitle to receive the following italicized content: `{"definite": true, "paragraph": true, "roundId": 4, "text": ""}`.

**disable_markdown_filter** Boolean `Optional` `Example: false`

Filters Markdown formatting from the LLM's text before speech synthesis.

* `true`: Enable filtering. For example, `**hello**` will be pronounced as hello.

* `false` (Default): No filtering.

   **Example:**

* LLM Response: `Please run the **grep** command to view the logs.`

* Agent Speaks: `Please run the grep command to view the logs.`

* Subtitles Show: `Please run the **grep** command to view the logs.`

**enable_language_detector** Boolean `Optional` `Example: false`

Whether to automatically recognize the language.

* `true`: Enable to automatically recognize.

* `false`: Disable to automatically recognize.

   Default to `false`.

Google TTS

**CredentialsJSON** String 必选 `Example: "{\"type\": \"service_account\", \"private_key\": \"-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n\"}"`

Provide the service account key as a JSON string (downloaded from Google Cloud Console).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89d3385eb7f0fad18ff0b10464b41091.png)

**How to obtain the key**: see [Creating service account keys](https://docs.cloud.google.com/iam/docs/keys-create-delete#iam-service-account-keys-create-console).

> The Google service account must have permissions to use the [Cloud Chirp 3: HD voices](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd).

> **warning**

> This key grants full access to your Google Cloud project. Store it securely and avoid hardcoding in source code.

**VoiceSelection** Object 必选 `Example: -`

Specifies the voice and language for speech synthesis.

**LanguageCode** String 必选 `Example: cmn-CN`

The BCP\-47 language code for the desired voice. Supported languages: [Language availability](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd#language_availability).

**Name** String 必选 `Example: cmn-CN-Chirp3-HD-Achernar`

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

ElevenLabs TTS

**APIKey** String 必选 `Example: YourOpenAIAPIKey`

ElevenLabs API key. Obtain it from the ElevenLabs console. See detials in [ElevenLabs API Keys](https://elevenlabs.io/docs/overview/administration/workspaces/api-keys).

**VoiceID** String 必选 `Example: pU9N****3uKz`

ID of the ElevenLabs voice used to synthesize speech. You can also call the ElevenLabs [List Voices API](https://elevenlabs.io/docs/api-reference/voices/search) and use the `voice_id` of the required voice.

**ModelID** String 必选 `Example: eleven_flash_v2_5`

ID of the ElevenLabs TTS model used to synthesize speech, such as `eleven_flash_v2_5` or `eleven_v3`. Call the ElevenLabs [List models API](https://elevenlabs.io/docs/api-reference/models/list) (`GET /v1/models`) and use the `model_id` of the required TTS model.

Before selecting a model, check [ElevenLabs models](https://elevenlabs.io/docs/overview/models) to confirm that it supports the required voice, language, and capabilities.

**URL** String `Optional` `Example: YourOpenAIURL`

ElevenLabs WebSocket endpoint. The default value is `wss://api.elevenlabs.io/v1/text-to-speech`.

**Speed** Float `Optional` `Example: 1.0`

Speech speed. Valid range: `[0.7, 1.2]`. The default value is `1.0`.

**Language** String `Optional` `Example: en`

Language code passed through to ElevenLabs as `language_code`. It specifies the language used by the model and text normalization. For supported values and default behavior, see detaisl in the `language_code` parameter in [ElevenLabs documentation](https://elevenlabs.io/docs/api-reference/text-to-speech/v-1-text-to-speech-voice-id-multi-stream-input).

MiniMax TTS

**APIKey** String 必选 `Example: YourOpenAIAPIKey`

MiniMax API key. See details in [API Overview](https://platform.minimax.io/docs/api-reference/api-overview).

**Model** String 必选 `Example: speech-2.8-turbo`

The model version to request. Available options: See the `model` parameter in the [MiniMax official documentation](https://platform.minimax.cn/docs/api-reference/speech-t2a-websocket-bidi).

**VoiceID** String 必选 `Example: English_expressive_narrator`

The ID of the target voice. The full list of available voices can be viewed on the [System Voice ID List](https://platform.minimax.io/docs/faq/system-voice-id) or retrieved programmatically using the [Get Voice API](https://platform.minimax.io/docs/api-reference/voice-management-get).

**URL** String `Optional` `Example: wss://api.minimax.io/ws/v1/t2a_v2_bidi`

MiniMax bidirectional streaming endpoint. The default value is `wss://api.minimax.io/ws/v1/t2a_v2_bidi`.

**Speed** Float `Optional` `Example: 1.0`

Speech speed. Higher values result in faster speech. Range: `[0.5, 2]` (default: `1.0`).

**Language** String `Optional` `Example: English`

Controls whether recognition for specific minority languages and dialects is enhanced. Default is `null`. If the language type is unknown, set to `"auto"` and the model will automatically detect it.

Supported values: See the `language_boost` parameter in the [MiniMax official documentation](https://platform.minimax.cn/docs/api-reference/speech-t2a-websocket-bidi).

Self\-hosted TTS

**URL** String 必选 `Example: YourOpenAIURL`

> **warning**

> Before configuration, make sure that you have completed the following:

1. > Prepare your self\-hosted TTS service API. The API must comply with the [Self\-hosted model interface protocol spec](https://docs.byteplus.com/en/docs/iga/ai-gateway-self-hosted-protocol).

2. > [Submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000762&FlowKey=hooomjXXojvNpHrZdAQT&aiSearchQuestion=&aiID=) to request onboarding your self\-hosted TTS service to AI Gateway. Then follow [Onboard and call a self\-hosted model](https://docs.byteplus.com/en/docs/iga/ai-gateway-self-hosted)to complete the integration.

AI Gateway endpoint URL. StartVoiceChat connects to AI Gateway through this URL, and AI Gateway then forwards requests to your self\-hosted ASR service.

* URL format:`wss://ai-gateway.vei.volces.com/v1/realtime?model=<ASR invocation name>`

* `<ASR invocation name>`: Replace this value with the custom model invocation name configured in the AI Gateway console.

**APIKey** String 必选 `Example: YourOpenAIAPIKey`

AI Gateway access key. This is configured when onboarding your self\-hosted ASR service to AI Gateway.

**Voice** String 必选 `Example: alloy`

Voice. Enter a voice name supported by your self\-hosted TTS service.

**OutputAudioPitchRate** Float `Optional` `Example: 1.0`

Pitch.

> Pass\-through field. The limit and default behavior are determined by your self\-hosted model.

**OutputAudioSpeedRate** Float `Optional` `Example: 1.0`

Speech rate.

> Pass\-through field. The limit and default behavior are determined by your self\-hosted model.

**OutputAudioVolume** Float `Optional` `Example: 1.0`

Volume.

> Pass\-through field. The limit and default behavior are determined by your self\-hosted model.

**ExtraData** JSONMap `Optional` `Example: {"custom_param": "value1"}`

Custom parameters passed through to your self\-hosted TTS service in JSON format. If this parameter is not passed, no custom parameters are passed through.

**ExtraHeader** JSONMap `Optional` `Example: {"custom_header": "value"}`

Custom pass\-through headers. This parameter is a JSON object. Its key\-value pairs are passed as additional HTTP headers in requests to your self\-hosted TTS service. You can use them for authentication or other custom logic.

If this parameter is not passed, no custom headers are passed through.

**IgnoreBracketText** Integer[] `Optional` `Example: [1,2]`

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

> **tip**

> Filtered content will typically still appear in the subtitles. However, it will be excluded from subtitles if it appears at the very end of a response and is treated as a separate sentence.

**Context** Object `Optional` `Example: -`

Configure TTS context and tag parsing to control the AI broadcast's tone (e.g., cheerful, sad), speech rate, and volume, making the AI broadcast more emotional and expressive.

> **warning**

> This feature only takes effect when using the BytePlus TTS service.

**TagParse** Boolean `Optional` `Example: true`

Whether to enable `{{...}}` tag parsing:

* `true`: Enable. After enabling, you also need to guide the LLM in the system prompt to automatically generate standard format instruction tags based on the context. The tags and their content will not be read aloud or displayed in subtitles. For tag format and Prompt writing methods, please refer to to [Using Instruction Tags to Control AI Emotion](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-2139328).

* `false` (Default): Disable. `{{...}}` and its content will be treated as plain text; if `IgnoreBracketText` is configured to filter `{}`, the tags and content will be filtered out.

**QuoteUserQuestion** Boolean `Optional` `Example: true`

Whether to pass the user's question as context to the TTS, allowing the TTS model to automatically match an appropriate reply tone based on the conversation context.

* `true` (Default): Yes.

* `false`: No.

> **warning**

> This field only takes effect when using the BytePlus TTS 2.0, and its priority is lower than instruction tags.

**SubtitleConfig** Object `Optional` `Example: -`

Subtitle callback configuration.

Callbacks can be received through the client or server. The message format is binary and needs to be parsed before use. For detailed instructions, see [Real-time Subtitles](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1337284).

**DisableRTSSubtitle** Boolean `Optional` `Example: false`

Whether to turn off the client subtitle callback in the room.

* `true`: Turn off the client subtitle callback.

* `false`: Turn on the client subtitle callback.After turning it on, you can listen [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onroombinarymessagereceived) on the client side to receive the subtitle callback message.

   Default to `false`.

> **tip**

> If you need to receive the subtitle callback through the server side, please configure `AgentConfig.ServerMessageURLForRTS` and `AgentConfig.ServerMessageSignatureForRTS`.

**SubtitleMode** Integer `Optional` `Example: 0`

Subtitle Type. Different type determine the source of the subtitles, synchronization with audio, and reception speed. The reception speeds of the modes are ranked as follows: 3 \> 1 \> 0 ≈ 2.

* `0`: **Timestamp\-Aligned Subtitles**. Subtitles are sourced from TTS and aligned with the AI’s actual audio output at the sentence level using timestamps. **Note**: This mode is unavailable when `TTSCofing.AutoActive` is false.

* `1`: **Fast Subtitles.**  Subtitles originate from the LLM's raw response, but special characters like spaces and carriage returns are filtered out. Upon return, the system returns identified clauses or full sentences in one go. Subtitles are not aligned with audio timestamps, enabling rapid subtitle callbacks. **Note**: This mode is unavailable when `TTSCofing.AutoActive` is false.

* `2`: **Audio Frame\-Aligned Subtitles**. Subtitles originate from TTS. Audio frames are precisely synchronized with subtitles to achieve a karaoke\-like, character\-by\-character highlighting effect. For implementation details, refer to Using Audio Frame\-Aligned Subtitles.

* `3`: **LLM raw subtitles**. Subtitles originate from the LLM's raw output without any content processing, fully preserving formats such as line breaks. Suitable for scenarios requiring content fidelity and rapid subtitle callbacks.

   Default to `0`.

> **warning**

* > When the digital human service is enabled, this field only supports a value of 1. If set to 0, subtitles will not take effect.

* > When using the BytePlus TTS 2.0, if you need to set `SubtitleMode: 0` (align audio timestamps), you must disable the `enable_latex_tn` (broadcast LaTeX formulas) feature.

* > When `SubtitleMode` is 1, it is expected behavior for the subtitle to receive the following italicized content: `{"definite": true, "paragraph": true, "roundId": 4, "text": ""}`.

**FunctionCallingConfig** Object `Optional` `Example: -`

Tool Invocation Messages configuration when using Function calling on the server\-side.

For details about the Function calling function, see the [Function Calling](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1554654).

> **tip**

> This function is only valid when using ModelArk platform.

**ServerMessageUrl** String `Optional` `Example: https://example-domain.com/vertc/fc`

The URL address of receiving the tool invocation messages returned.

The URL for receiving the result must start with a domain name. If the URL is an HTTPS domain name, please ensure that the SSL certificate of the domain name is legal and complete.

> **tip**

> Both ServerMessageUrl and ServerMessageSignature must be filled in correctly to enable this function.

**ServerMessageSignature** String `Optional` `Example: TestSignature`

Authentication signature.

You can pass in this authentication parameter, and after receiving tool invocation messages, compare it with the value of the signature field in the result for authentication verification.

**InterruptMode** Integer `Optional` `Example: 0`

The voice interruption mode for the AI agent. Supported values and their meanings are as follows.

* `0`: Automatic voice interruption (default). User's voice input will interrupt the AI agent's speech.

* `1`: Disable voice interruption. User's voice input during the AI agent's speech will be ignored.

**AvatarConfig** Object `Optional` `Example: -`

Configure the avatar. Only support Akool avatar.

**Enabled** Boolean `Optional` `Example: true`

Whether to enable the avatar service.

* `true`: Enable.

* `false` (default): Disable.

> **warning**

> Before enabling, please ensure that you have created an Akool API key and got the Akool avatar ID. See details in [Prepare Akool Avatar Resources](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1848567).

**Provider** String `Optional` `Example: Akool`

Avatar service provider. Supported values: `Akool` (Akool avatar).

**ProviderParams** Object `Optional` `Example: -`

Akool avatar configuration.

**ApiKey** String 必选 `Example: your_akool_api_key`

Akool API Key. You can obtain from the [Akool console](https://akool.com/workspace/6a5f1cca5481c8661d6da24c/api/credentials).

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261104033932-434147883471.png)

**AvatarId** String 必选 `Example: djn****nZk`

Akool avatar ID. You can obtain from the [Akool console](https://akool.com/workspace/6a5f1cca5481c8661d6da24c/avatars).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0022b88faa124b8fd640a5acf0ea678a.png)

**AvatarUserID** String `Optional` `Example: avatar_user`

User ID of the avatar in the RTC room, used for identification. This field is user\-defined.

* **Default Value**: `AgentConfig.UserId` + _`Avatar`.

* **Naming Rules**:

   * Supports uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.), and the @ symbol. The maximum length is 128 characters.

   * The value of AvatarUserID must not be the same as `AgentConfig.UserId` (Agent ID) or `TargetUserId` (Real user ID).

> **warning**

> When sending control commands—such as manually interrupting a response or updating conversation context via the sendUserBinaryMessage interface, the target userId must be the **AI Agent ID (AgentConfig.UserId)**.

**WebSearchAgentConfig** Object `Optional` `Example: -`

Configuration of the BytePlus AskEcho Search Agent, see [Integrate AskEcho Search Agent](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856161).

> **warning**

> It is only compatible with BytePlus ModelArk models or third\-party LLMs that support Function Calling. For a comprehensive list of supported ModelArk models, refer to the [Model List\-Tool use](https://docs.byteplus.com/en/docs/modelark/model-list#f44ceef7).

**Enable** Boolean `Optional` `Example: true`

Whether to enable the AskEcho Search Agent.

* `true`: Enable.

* `false` (default): Disable.

**APIKey** String `Optional` `Example: oHdJ****Lc8Z`

The API Key for the AskEcho Search Agent service. You can create and obtain it on the [AskEcho Search Agent Console](https://console.byteplus.com/bp-ask-echo/api-key).

> Required only when `Enable` is set to `true`.

**ParamsString** String `Optional` `Example: {"bot_id": "742..."}`

Pass\-through parameters for the AskEcho Search Agent service, sent as a compressed and escaped JSON string.

> Required only when `Enable` is `true`.

How to generate this value:

1. Build a JSON object based on the `ChatCompletionRequest` parameters from [AskEcho Search Agent API](https://docs.byteplus.com/en/docs/askecho/Agent_API_Reference).

   * `bot_id`: Required. Set this to your Agent ID, which can be obtained on the [AskEcho Search Agent Console](https://console.byteplus.com/bp-ask-echo/my-agent).

   * `stream`: Required. Must be set to `true`.

   * Other parameters like `messages` can be included as needed.

2. Compress and escape the JSON object into a single\-line string.

**FunctionName** String `Optional` `Example: WebSearch`

Your custom name for the search agent tool, which is used to internally identify this tool.

> **warning**

* > Required only when `Enable` is `true`.

* > The name must be unique and cannot be the same as any tool name defined in Function calling (`LLMConfig.Tools`).

**FunctionDescription** String `Optional` `Example: Query real-time information, such as today's weather, the latest news, the current price of A-shares.`

Description for the tool. This will be used as part of the prompt to help the LLM more accurately determine whether to trigger an online search.

> Required only when `Enable` is `true`.

**ComfortWords** String `Optional` `Example: Connecting ...`

Comfort message. When the agent triggers an online search, this comfort message will be played via TTS first to improve the user experience while waiting for search results. If left blank, it will not be played.

> **warning**

> The comfort message must end with punctuation.

**AgentConfig** Object 必选 `Example: -`

Agent configuration, including welcome messages and task status callbacks.

**TargetUserID** String[] 必选 `Example: ["User1"]`

Real user's ID. That is, the `UserId` of the real user who enters the room using the client SDK.

Only one `UserId` can be set.

**UserID** String 必选 `Example: voiceChat_task1_1611736812853`

AI Agent's ID, used to identify the agent.

It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.

> **tip**

* > It is recommended that the `UserId` be globally unique under the same `AppId`. If the names of agents in different rooms under the same AppId are the same, it will cause features that rely on server callbacks to malfunction, such as subtitle, Function Calling, and task status callback functions.

* > The value of `UserId` cannot be repeated with that of `TargetUserId` or `AvatarUserID`.

**WelcomeMessage** String `Optional` `Example: Hi, how can I help you today.`

AI agent's welcome message.

**EnableConversationStateCallback** Boolean `Optional` `Example: false`

Whether to receive the callback of the status change of the agent and obtain the key status of the agent, such as "listening", "speaking", etc. For detailed function description, see [Receive Status Change Messages](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1415216).

* `true`: Enable to receive. The callback of the status change of the agent can be received through the client or the server.

   * Receiving through the client: Listening callback [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onroombinarymessagereceived) in the client.

   * Receiving through the server: Configure the fields `ServerMessageURLForRTS` and `ServerMessageSignatureForRTS`.

* `false`: Disable to receive.

Default to `false`.

**ServerMessageURLForRTS** String `Optional` `Example: https://example-domain.com/vertc/callback`

The URL address for the your server to receive AI bot status changes or subtitles.

The URL for receiving results must start with a domain name. If the URL is an HTTPS domain, please ensure that the SSL certificate of the domain is legal and complete.

**ServerMessageSignatureForRTS** String `Optional` `Example: b46ab****d6a`

Authentication signature.

You can pass in this authentication parameter, and after receiving status change messages or subtitles, compare it with the value of the signature field in the result for authentication verification.

**AnsMode** Integer `Optional` `Example: 0`

AI noise suppression.

Suppresses ambient noise other than human voices, such as air conditioners, fans, and keyboard clicks, to enhance speech clarity.

> This feature is available on both client and server sides. Server\-side noise suppression is recommended when terminal devices (e.g., IoT, smart hardware) are unable to enable the client\-side feature due to limited computing power or other constraints.

Supported values:

* `0` (Default): Disables AI noise suppression.

* `1`: Mild suppression. Suitable for suppressing faint, steady background noise.

* `2`: Medium suppression. Suitable for suppressing moderate steady noise, such as air conditioners and fans.

* `3`: Heavy suppression. Suitable for suppressing loud, non\-stationary dynamic noise, such as keyboard clicks, object collisions, animal sounds, etc.

## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

On success, the `Result` field in the response is "success".
