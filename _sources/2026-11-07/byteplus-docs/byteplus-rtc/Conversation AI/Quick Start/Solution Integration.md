---
title: "Solution Integration"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1310560"
---

This document describes how to integrate a basic conversational AI solution with BytePlus RTC and enable real\-time interaction between a user and an AI agent.

## Preparations

Before integration, complete the following preparations:

1. Activate BytePlus RTC, create an RTC application, and obtain its `AppId`. For details, see [Preparations for Solution Integration](https://docs.byteplus.com/docs/byteplus-rtc/docs-1315561).

2. Activate the ASR, LLM, and TTS services required by your selected model combination and obtain their credentials. Available model and preparation instructions are listed in [Preparations for Solution Integration](https://docs.byteplus.com/docs/byteplus-rtc/docs-1315561).

3. Generate an RTC Token on your application server for the human user to join the room. For details, see [Authentication with Token](https://docs.byteplus.com/docs/byteplus-rtc/docs-70121).

4. Obtain an Access Key ID and Secret Access Key for your application server. Use them to sign BytePlus OpenAPI requests. For details, see [API Call](https://docs.byteplus.com/docs/byteplus-rtc/docs-69828).

## Quickly build a web application

You can download [RTC_AIGC_Demo](https://github.com/byteplus-sdk/RTC_AIGC_Demo) to quickly build a web application for AI\-powered audio and video interaction.

## Integrate

### Step 1: Implement audio and video calls

Integrate the BytePlus RTC SDK into your client application and implement the basic RTC call.

##### Implementation

* **Quick test**: Run the [Sample Project](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1163793) to verify the basic RTC call flow before integrating it into your application.

* **Integrate into your application**: Download the required SDK from [Download SDK](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75707), then follow the platform\-specific guide:

   * [Android](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70134)

   * [iOS (Objective-C)](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133)

   * [macOS (Objective-C)](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70131)

   * [Windows](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70130)

   * [Web](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-106914)

   * [Electron](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-108795)

   * [Flutter](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-132236)

   * [Unity](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-108610)

   * [React Native](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1455709)

##### Key configurations

* **Create the engine and join the room**: In Native SDK 3.60 and Electron SDK 3.60.1, use `createRTCEngine`. In the Web SDK, use `createEngine`. Create a room instance, then call `joinRoom` with the RTC Token, `RoomId`, and the human user's `UserId`.

* **Publish and subscribe to audio**: Keep automatic audio publishing and subscription enabled unless your application requires manual control. To use manual control, set `isAutoPublish` and `isAutoSubscribeAudio` to `false` when calling `joinRoom`. Then use `publishStreamAudio` and `subscribeStreamAudio` in Native SDK 3.60 and Electron SDK 3.60.1, or `publishStream` and `subscribeStream` in the Web SDK.

* **Optimize audio**: For Native SDK 3.60, include `"rtc.fg_config":"aigc_media_360=true"` in the `parameters` field when calling `createRTCEngine`. Call `setAudioScenario` and select the Conversation AI scenario supported by the platform. For example, use `AICLIENT` on Android.

* **Mute the user**: To mute the user's microphone with the lowest switching latency, use `muteAudioCapture`. Do not use `stopAudioCapture` to implement mute, because stopping and restarting audio capture may cause audio stuttering or voice distortion.

### Step 2: Start the AI conversation

After the human user has joined the room and published audio, call [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163) from your application server.

* How to call: see [API Call](https://docs.byteplus.com/docs/byteplus-rtc/docs-69828).

* Examples:

   * `AppId` and `RoomId`: Replace them with the `AppId` and `RoomId` used when generating the RTC token.

   * `TaskId`: Define this value yourself to uniquely identify the AI conversation task.

   * `AgentConfig.TargetUserID`: Set to the actual human `UserId` used to join the room. Only one target user is supported.

   * `AgentConfig.UserID`: Set to a different value from the target user. Avoid reusing an AI agent user ID within the same RTC application.

   **Use BytePlus models**

This example uses BytePlus ASR, BytePlus ModelArk, and BytePlus TTS.

   ```JSON
   {
     "AppId": "<RTC_APP_ID>",
     "RoomId": "<ROOM_ID>",
     "TaskId": "<TASK_ID>",
     "AgentConfig": {
       "TargetUserID": ["<HUMAN_USER_ID>"],
       "UserID": "<AI_AGENT_USER_ID>",
       "WelcomeMessage": "Hello, how can I help you?"
     },
     "Config": {
       "ASRConfig": {
         "Provider": "BytePlus",
         "ProviderParams": {
           "Mode": "SeedASR",
           "Language": "en-US",
           "ApiKey": "<ASR_API_KEY>",
           "ApiResourceId": "volc.seedasr.sauc.duration",
           "StreamMode": 2,
           "enable_nonstream": true
         }
       },
       "LLMConfig": {
         "Provider": "BytePlus",
         "APIKey": "<MODELARK_API_KEY>",
         "EndPointId": "<MODELARK_ENDPOINT_ID>"
       },
       "TTSConfig": {
         "Provider": "BytePlus",
         "ProviderParams": {
           "app": {
             "apikey": "<TTS_API_KEY>"
           },
           "audio": {
             "voice_type": "<TTS_VOICE_TYPE>"
           },
           "ResourceId": "seed-tts-2.0"
         }
       }
     }
   }
   ```

   **Use self-hosted models**

* If you need to connect a self\-hosted LLM, see [Integrate Third-Party Model](https://docs.byteplus.com/docs/byteplus-rtc/docs-1399966).

      * If you need to connect a self\-hosted ASR or TTS service, see [Integrate Self-hosted ASR or TTS Model](https://docs.byteplus.com/docs/byteplus-rtc/docs-1798100).

   ```JSON
   {
     "AppId": "<RTC_APP_ID>",
     "RoomId": "<ROOM_ID>",
     "TaskId": "<TASK_ID>",
     "AgentConfig": {
       "TargetUserID": ["<HUMAN_USER_ID>"],
       "UserID": "<AI_AGENT_USER_ID>",
       "WelcomeMessage": "Hello, how can I help you?"
     },
     "Config": {
       "ASRConfig": {
         "Provider": "ai_gateway", // required, must be set to `ai_gateway`
         "ProviderParams": {
           "URL": "<AI Gateway endpoint URL>", // required, the service endpoint URL obtained from AI Gateway
           "APIKey": "sk-xxxxxx", // required, the access key for AI Gateway
           "ExtraData": {
             "language": "zh-cn",
             "enable_punctuation": true,
             "domain": "medical"
           },
           "ExtraHeader": {
             "custom_header": "value"
           }
         }
       }
     },
     "LLMConfig": {
       "Mode": "CustomLLM",
       "Url": "https://api.example.com/v1/chat-stream",
       "ModelName": "<MODEL_NAME>",
       "APIKey": "<THIRD_PARTY_LLM_API_KEY>"
     },
     "TTSConfig": {
       "Provider": "ai_gateway", // required, must be set to `ai_gateway`
       "ProviderParams": {
         "URL": "<AI Gateway endpoint URL>", // required, the service endpoint URL obtained from AI Gateway
         "APIKey": "sk-xxxxxx", // required, the access key for AI Gateway
         "Voice": "<your_custom_voice>", // required, your self-hosted voice
         "ExtraData": {
           "language": "zh-cn",
           "enable_punctuation": true,
           "domain": "medical"
         },
         "ExtraHeader": {
           "custom_header": "value"
         },
         "OutputAudioSpeedRate": 1.0,
         "OutputAudioVolume": 1.0,
         "OutputAudioPitchRate": 1.0
       }
     }
   }
   ```

After the AI agent joins the room, the client can hear the welcome message and start a real\-time conversation. To verify the integration, complete one full conversation round and confirm that the agent can receive the user's audio, generate a response, and publish response audio back to the RTC room.

* If you enable callbacks, use [Obtain AI Status](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216) and [Obtain Conversation AI Task Events](https://docs.byteplus.com/docs/byteplus-rtc/docs-1798101) to check task status, stage latency, usage, and error events.

* If the request succeeds but the AI agent does not join the room or cannot respond, see [Agent Failed to Join the Room or Not Working Properly](https://docs.byteplus.com/docs/byteplus-rtc/docs-1557772).

### Step 3: End the conversation and release resources

By default, if the target user leaves the room without stopping the task, the AI agent task stops after 180 seconds. Billing continues during this period. To avoid unnecessary resource consumption, clean up resources in the following order when the conversation ends:

1. From your application server, call [StopVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1404672). Pass the same `AppId`, `RoomId`, and `TaskId` used at startup.

2. After the stop request succeeds or your application has handled the failure according to its retry policy, call `leaveRoom` on the client.

3. Destroy the client engine and release its resources. Use `destroyRTCEngine` for Native SDK 3.60 and Electron SDK 3.60.1, or `destroyEngine` for the Web SDK.

### Advanced features

After the basic conversation flow works, you can add the following capabilities:

* **Real\-time subtitles**: Display the recognized conversation as text.

* **Conversation interruption**: Allow the user to interrupt the AI while it is speaking.

* **Visual understanding**: Send video frames or images to a vision\-capable model.

* **Status monitoring**: Receive AI agent status changes and handle task exceptions.

For more supported features and implementation methods, see [Development](https://docs.byteplus.com/docs/byteplus-rtc/docs-1350595).
