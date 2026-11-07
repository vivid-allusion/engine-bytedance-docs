---
title: "Billing of Conversational AI"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392584"
---

RTC Conversational AI is a composite service. Its total cost is composed of two main categories:


* **RTC\-Related Fees**: Charges for **Audio/Video Calls** and **Audio/Video Processing**.

* **AI Service Fees**: Charges for the AI services you select, such as **LLM, ASR,**  and **TTS**.


<span id="billing-rules"></span>
## Billing Rules

<span id="audio-video-call-charges"></span>
### Audio/Video Call Charges

When a user makes a call with an AI agent, you are charged for both the user's and the agent's audio/video stream subscriptions. These charges follow the same rules as standard audio/video calls. For detailed rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).


* **Specific charges incurred**:

> * Billing for audio duration occurs even if only one participant is in the room.

> * If you subscribe to both audio and video streams simultaneously, you are only charged for the video duration.


&nbsp;


|Scenario |Generated Audio/Video Call Fees |
|---|---|
|**Visual Understanding & Digital Human disabled** |Audio call charges (user and AI agent subscribe to each other’s audio streams) |
|**Only Visual Understanding enabled** |* Audio call charges (user subscribes to AI agent’s audio)<br><br>* Video call charges (AI agent subscribes to user’s audio/video stream) |
|**Only Digital Human enabled** |* Audio call charges (AI agent subscribes to user’s audio)<br><br>* Video call charges (user subscribes to AI agent’s audio/video stream) |
|**Visual Understanding & Digital Human enabled** |Video call charges (user and AI agent subscribe to each other’s audio/video streams) |



* **Audio/Video Billing Rules**: The cost calculation method is identical to that of regular audio/video calls. For specific rules, refer to [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).


<span id="audio-video-processing-fee"></span>
### Audio/Video Processing Fee


* **Billing formula**

   Audio processing fee = Audio processing unit price × Billing duration

   Video processing fee = Video processing unit price × Billing duration

* **Pricing**


&nbsp;


|Service |Unit price (USD / 1000 minutes) |
|---|---|
|ConversationalAI_Audio (Audio processing) |1.29 |
|ConversationalAI_Video (Video processing) |13.99 |



* **Calculating billing duration**

   The total billing duration is calculated on a per\-task, per\-day basis.

   * **Task Duration**: The total time from when the Conversational AI task is initiated on the server until it ends.

   * **Video Processing Duration**: The cumulative time that video frames are actively processed during a task. If a task involves multiple, separate periods of video processing, the duration of each period is measured and then added together.

   * **Audio Processing Duration**: This is calculated by subtracting the Video Processing Duration from the total Task Duration.

> Audio Processing Duration = Task Duration \- Video Processing Duration


* **Rounding Rule**:

   Durations for audio and video processing are calculated independently for each calendar day. The total usage for each service is rounded up to the nearest minute. For example, any usage on a given day that is less than one minute is billed as one minute.

* **Payment method**

   Pay\-as\-you\-go: You are billed for your usage after it occurs. Charges are settled monthly and deducted from your account balance.


<span id="llm-service-fee"></span>
### LLM Service Fee

This fee covers the inference services provided by the Large Language Model (LLM). Specific billing items and rates depend on the actual model used.

<span id="asr-service-fee"></span>
### ASR service fee

This fee is for the real\-time speech\-to\-text (ASR) conversion of the user’s voice during the conversation. Billing details depend on the specific ASR service used.

<span id="tts-service-fee"></span>
### TTS service fee

This fee is for the real\-time text\-to\-speech (TTS) synthesis of the AI agent’s responses. Billing details depend on the specific TTS service used.

<span id="how-to-stop-billing"></span>
## How to Stop Billing

To stop charges for RTC Conversational AI, follow these steps:

> For API descriptions for each client, see [Client API Reference](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-client-api).


1. Call the server\-side API [StopVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404672) to end the conversation.

   After this call, the AI agent leaves the room, the ASR, LLM, and TTS services stop running, and billing for these services ceases. If the human user remains in the room, RTC audio subscription fees will continue to accrue.

2. Call the client\-side API `leaveRoom` for the human user to exit the room.

   Once the user leaves, RTC audio subscription billing stops.

3. Call the client\-side API `destroyRTCEngine` to destroy the RTC engine and release resources.


<span id="billing-example"></span>
## Billing Example

Suppose a user enters a room and initiates a 1v1 real\-time voice conversation with an AI agent, which lasts for 10 minutes, after which both participants leave the room. The costs for this real\-time call between the user and the AI are as follows:


* User's audio call fee = 0.99/1000 × 10 = 0.0099 USD

* AI agent's audio call fee = 0.99/1000 × 10 = 0.0099 USD

* Audio processing fee = 1.29/1000 × 10 = 0.0129 USD


Total RTC\-related cost is 0.0327 USD (excluding AI service fees).
