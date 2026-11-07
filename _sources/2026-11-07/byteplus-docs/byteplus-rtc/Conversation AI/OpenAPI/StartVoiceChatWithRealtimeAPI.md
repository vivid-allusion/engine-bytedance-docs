---
title: " StartVoiceChatWithRealtimeAPI"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1316257"
---

If you want to initiate an agent to provide voice chat services using the Realtime API, you can call this interface.

Realtime API enables you to build low\-latency, multimodal experiences, without the need for additional ASR and TTS integration.

<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://open.byteplusapi.com?Action=StartVoiceChatWithRealtimeAPI&Version=2025\-05\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters).

<span id="Query"></span>
### Query



**Action** `String` <span data-api-tag="require|2FeJ2n">必选</span> Example: `StartVoiceChatWithRealtimeAPI`

Interface name. The value of this interface: `StartVoiceChatWithRealtimeAPI`



**Version** `String` <span data-api-tag="require|e2HDT0">必选</span> Example: `2025-05-01`

OpenAPI version. The value of this interface: `2025-05-01`



<span id="Body"></span>
### Body



**AppId** `String` <span data-api-tag="require|nUPE3Q">必选</span> Example: `661e****543cf`

The only identifier for your audio & video app.



**RoomId** `String` <span data-api-tag="require|x2oByf">必选</span> Example: `Room1`

The room ID for the conversation between the agent and the real person. This value must be consistent with that used when the real person user enters the room using the client SDK.



**TaskId** `String` `Optional` Example: `Task1`

Task Id. You need to define the `TaskId` for each agent task, and also use this `TaskId` when updating and ending the task later.

It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.

The `TaskId` is the identifier of the task. Under a `RoomId` of an AppId, the `TaskId` is unique. The `TaskId` can be repeated under different `AppId` or different `RoomId`. Therefore, `AppId` + `RoomId` + `TaskId` is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified `AppId`, so that this task can be updated or stopped during the running of this task.



**AgentConfig** `Object` <span data-api-tag="require|ZyqC6n">必选</span> Example: `-`

Config for chat agent.


**UserId** `String` `Optional` Example: `bot1`

AI Agent ID, used to identify the agent.

It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.

If not filled, the default value is `voiceChat_$(UserId)_$(timestamp_now)`.



**TargetUserID** `String[]` <span data-api-tag="require|Lrcnnf">必选</span> Example: `["User1"]`

UserId of the client.

Only one client is supported.



**WelcomeMessage** `String` `Optional` Example: `Hi, how can I help you today.`

The chat agent's welcome message.




**LLMConfig** `Object` <span data-api-tag="require|Aw5gOo">必选</span> Example: `-`

Config for OpenAI LLM.


**Provider** `String` <span data-api-tag="require|ixuhjV">必选</span> Example: `openai`

The service provider. The value of this interface takes `openapi`.



**Token** `String` <span data-api-tag="require|TM_ju0">必选</span> Example: `yJhbGciO****zI1NiIsI`

API key of OpenAI. Acquire on [OpenAI's dashboard](https://platform.openai.com/api-keys).



**Voice** `String` `Optional` Example: `alloy`

The voice the model uses to respond,defaults to `alloy`.

Supported voices are:


* `alloy`

* `ash`

* `ballad`

* `coral`

* `echo`

* `sage`

* `shimmer`

* `verse`



**Instructions** `String` `Optional` Example: `You are a helpful, witty, and friendly AI.Talk quickly. You should always call a function if you can.`

System message.



**Temperature** `Float` `Optional` Example: `0.8`

Sampling temperature for the model, limited to `[0.6, 1.2]`. Defaults to `0.8`.



**TurnDetection** `Object` `Optional` Example: `-`

Config of turn detection.


**Type** `String` `Optional` Example: `server_vad`

Type of turn detection, only `server_vad` is supported.

`server_vad`means that the model will detect the start and end of speech based on audio volume and respond at the end of user speech.



**Threshold** `Float` `Optional` Example: `0.5`

Activation threshold for VAD, limited to `[0.0, 1.0]`. Defaults to `0.5`.

A higher threshold will require louder audio to activate the model, and thus might perform better in noisy environments.



**PrefixPaddingMs** `Integer` `Optional` Example: `300`

Amount of audio to include before the VAD detected speech in milliseconds. Defaults to `300`.



**SilenceDurationMs** `Integer` `Optional` Example: `200`

Duration of silence to detect speech stop in milliseconds. Defaults to `200`.

With shorter values, the model will respond more quickly, but may jump in on short pauses from the user.





**AvatarConfig** `Object` `Optional`


**Enabled** `Boolean` `Optional` Example: `true`

Whether to enable BytePlus digital human service.


* `true`: Enable.

* `false` (default): Disable.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before enabling, please ensure that you have applied for BytePlus digital human resources. See details in <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1848567#step-1-apply-for-digital-human-resources">Apply for Digital Human Resources</a>.</div>




**AvatarAppID** `String` `Optional` Example: `zOpP1FFZ****ZQi9GHn`

The AppID of the BytePlus digital human service.


> * This field is required when `Enabled` is set to `true`.

> * After applying for digital human resources, the technical support will provide this information.



**AvatarToken** `String` `Optional` Example: `250623-****-linyunzhi`

The token for the BytePlus digital human service.


> * This field is required when `Enabled` is set to `true`.

> * After applying for digital human resources, the technical support will provide this information.



**AvatarType** `String` `Optional` Example: `3min`

The type of digital human. Currently, the only supported value is `3min`, which represents a 3\-minute cloned digital human.

> This field is required when `Enabled` is set to `true`.



**AvatarRole** `String` `Optional` Example: `250623-zhibo-linyunzhi`

The ID of the digital human role.


> * This field is required when `Enabled` is set to `true`.

> * After applying for digital human resources, the technical support will provide this information.



**BackgroundUrl** `String` `Optional` Example: `https://example.com/background.png`

The URL of the digital human background image. The URL must be publicly accessible and include an image format suffix such as `.png` or `.jpg`.



**VideoBitrate** `Integer` `Optional` Example: `3000`

The video bitrate of the digital human video stream, in kbps. The value range is `[100, 8000]`. The default value is `2000`.




<span id="Response parameters"></span>
## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)for returned common parameters.

Result returns "success" only when the request succeeds and null when it fails.
