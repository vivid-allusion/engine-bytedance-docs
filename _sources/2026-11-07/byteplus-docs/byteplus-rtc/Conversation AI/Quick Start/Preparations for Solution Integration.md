---
title: "Preparations for Solution Integration"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1315561"
---

This document provides an integration preparation guide for integrating real\-time conversational AI scenarios.

RTC offers two integration solutions: a one\-stop integration of ASR, LLM, and TTS services, and direct integration via OpenAI RealtimeAPI. The access preparations differ between the two solutions.

## One\-Stop Integration

### Step 1: Activate RTC Service

To activate the RTC service and create an application, refer to the [activation tutorial](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865).

### Step 2: Activate ASR Service

BytePlus RTC supports the following ASR vendors:

* [Amazon Streaming transcriptions](https://docs.aws.amazon.com/transcribe/latest/dg/getting-started-console.html)

* [BytePlus ASR (Speech-to-Text (ASR))](https://docs.byteplus.com/en/docs/byteplusvoice/speechtotext)

* [Google ASR (Cloud Speech-to-Text V1)](https://cloud.google.com/speech-to-text)

### Step 3: Activate TTS Service

BytePlus RTC supports the following TTS vendors:

* [Amazon](https://docs.aws.amazon.com/polly/latest/dg/signup.html)

* [BytePlus (Text-to-Speech (TTS))](https://docs.byteplus.com/en/docs/byteplusvoice/texttospeech)

* [ElevenLabs](https://elevenlabs.io/docs/overview/administration/workspaces/api-keys)

* [Google (Chirp 3: HD voices)](https://docs.cloud.google.com/text-to-speech/docs)

* [MiniMax](https://platform.minimax.io/docs/guides/quickstart-preparation)

* [OpenAI](https://platform.openai.com/docs/overview)

### Step 4: Activate LLM Service

BytePlus RTC supports the following LLM vendors:

* [BytePlus-ModelArk](https://docs.byteplus.com/en/docs/ModelArk/1099455)

* [OpenAI](https://platform.openai.com/docs/overview)

* Third\-Party

* [Google LLM](https://docs.cloud.google.com/vertex-ai/generative-ai/docs)

* [Amazon LLM](https://docs.aws.amazon.com/polly/latest/dg/signup.html)

## OpenAI RealtimeAPI Integration

Refer to [Realtime API](https://platform.openai.com/docs/guides/realtime).
