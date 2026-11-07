---
title: "Release Notes"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/81145"
---

## 2026

* November 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |ASR and TTS |BytePlus Seed ASR and TTS support API key authentication. |`2025-05-01` |2026\-11\-05 |[StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163), [UpdateVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1404671) |

* October 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |TTS |Added direct integration with ElevenLabs TTS and MiniMax bidirectional streaming TTS. |`2025-05-01` |2026\-10\-23 |[StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163) |
   |LLM |Added the `llmIncomplete` server\-side event. When an LLM response triggers content filtering, Conversation AI removes the affected round from the context used in subsequent LLM requests to prevent repeated filtering. The event also reports responses stopped by model output or context length limits through `ExtraInfo.FinishReason`. |`2025-05-01` |2026\-10\-23 |* [Obtain Conversation AI Task Events](https://docs.byteplus.com/docs/byteplus-rtc/docs-1798101)<br><br>* [Events and Error Codes](https://docs.byteplus.com/docs/byteplus-rtc/docs-1928198) |

* September 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |TTS |Added direct integration with ElevenLabs TTS and MiniMax bidirectional streaming TTS. |`2025-05-01` |2026\-09\-04 |[StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163) |
   |Function Calling |Added the `LLMConfig.EnableToolCallHistory` parameter. When enabled, if a round triggers Function Calling, the system includes that round's tool call instructions and tool return results in subsequent LLM requests together with the round history, so the model can continue multi\-turn conversations based on previous tool execution results. |`2025-05-01` |2026\-09\-01 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |
   |Transparent passthrough of custom external text information |When you pass external text through the `ExternalTextToSpeech` instruction of the `UpdateVoiceChat` API, you can include custom business information in `AdvanceConfig.CustomInfo`. The system then returns it unchanged in the `customInfo` field of the subtitles for the corresponding round. |`2025-05-01` |2026\-09\-01 |[UpdateVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404671) |
   |Real\-time subtitles |Added the `voiceprintScore` field to subtitle callbacks to return the voiceprint similarity score. |`2025-05-01` |2026\-09\-01 |[Real-time Subtitles (Dialog Records)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284) |

* July 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |LLM |Added `ReasoningEffort` and `MaxCompletionTokens` parameters to control the model's reasoning intensity and total output token budget (including chain\-of\-thought tokens). Supported across all LLM providers (BytePlus ModelArk, OpenAI, Amazon Bedrock, Google Gemini, ThirdParty). |`2025-05-01` |2026\-07\-28 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |
   |Avatar |Akool Avatar integration is supported. |`2025-05-01` |2026\-07\-21 |* [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163)<br><br>* [Integrate Akool Avatar](https://docs.byteplus.com/docs/byteplus-rtc/docs-1848567) |
   |Visual understanding |Function calling is now supported when visual understanding is enabled. |`2025-05-01` |2026\-07\-21 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |

* June 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |Real\-time Subtitles |Added `SubtitleMode=3` (LLM Raw Subtitles). Subtitles originate from the LLM's raw output without any content processing, fully retaining formatting such as newlines. Suitable for scenarios requiring content fidelity and rapid subtitle callbacks. |`2025-05-01` |2026\-06\-18 |* [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163)<br><br>* [Real-time Subtitles (Dialog Records)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284) |
   |ASR and LLM |Added `LLMConfig.AutoActive` and `TTSConfig.AutoActive` parameters to enable pure ASR or ASR+LLM modes, allowing for atomic combination control of ASR, LLM, and TTS modules. ||||
   |TTS and ASR |* Added support for [BytePlus Seed Speech ASR 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/speechtotextv2) and [TTS 2.0](https://docs.byteplus.com/en/docs/byteplusvoice/texttospeechv2).<br><br>* You can control the AI's speaking tone (e.g., cheerful, sad), speech rate, and volume using instruction tags (automatically generated by the LLM or injected by your business logic in real time). Additionally, passing the user's question as context to the TTS enables the AI to deliver replies with emotions that better fit the conversation scenario, achieving more empathetic and human\-like interaction. **This function only takes effect when using BytePlus TTS.**  |`2025-05-01` |2026\-06\-10 |* [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163)<br><br>* [UpdateVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404671)<br><br>* [Control AI Emotion with Instruction Tags](https://docs.byteplus.com/docs/byteplus-rtc/docs-2139328) |

* May 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |Real\-Time Subtitles |The StartVoiceChat API now supports SubtitleMode=2 (Audio Frame\-Aligned Subtitles). In this mode, each audio frame carries subtitle position metadata, enabling character\-level precise alignment (e.g., karaoke\-style highlighting). |`2025-05-01` |2026\-05\-09 |* [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163)<br><br>* [Real-time Subtitles (Dialog Records)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284) |
   |Pause/Resume AI Playback |While the AI is speaking, you can use a server\-side API or send a command from the client side to pause or resume AI playback. |`2025-05-01` |2026\-05\-09 |* [UpdateVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404671)<br><br>* [Pause or Resume AI Playback](https://docs.byteplus.com/docs/byteplus-rtc/docs-2389913) |

* March 2026

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |Digital Human |Introduced the `AvatarUserID` parameter within `AvatarConfig` to support custom, independent UserIDs. This resolves the issue where clients were unable to send commands to the AI Agent in digital human scenarios. |`2025-05-01` |2026\-03\-19 |* [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163)<br><br>* [Digital Human](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1848567) |

## 2025

* December 2025

   |Feature |Description |API Version |Release date |References |
   |---|---|---|---|---|
   |ASR |Added support for Google ASR (Cloud Speech\-to\-Text V2) |`2025-05-01` |2025\-12\-31 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |
   |MCP Integration |Added support for MCP (Model Context Protocol) integration, allowing you to integrate external services—such as knowledge base Q&A (RAG), web search, or business API calls—as standardized tools.<br><br>> This feature is currently available when using the BytePlus ModelArk LLM or Third\-party LLM. |`2025-05-01` |2025\-12\-09 |[Integrate MCP](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856160) |
   |AskEcho Search Agent |Added support for the AskEcho Search Agent, enabling the agent to perform real\-time web searches and provide summarized answers. |`2025-05-01` |2025\-12\-09 |[Integrate AskEcho Search Agent](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856161) |
   |Visual understanding |Added support for visual understanding, enabling the agent to analyze one or more images sent during a conversation and answer related questions. |`2025-05-01` |2025\-12\-09 |[Video and image understanding](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245) |
   |Update agent |Added support for dynamically updating agent configurations during a session via the `UpdateVoiceChat` interface (using the `Parameters` field). |`2025-05-01` |2025\-12\-09 |[UpdateVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404671) |
   |BytePlus TTS/ASR |Added support for parameter pass\-through for BytePlus TTS/ASR, allowing for more granular control. |`2025-05-01` |2025\-12\-09 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |
   |Google TTS |Added support for Google TTS integration. Only the "Chirp 3: HD voices" model is supported. |`2025-05-01` |2025\-12\-09 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |
   |AI noise suppression |Added support for AI noise suppression to intelligently reduce background noise. Different suppression levels can be selected via the `AgentConfig.AnsMode` field. |`2025-05-01` |2025\-12\-09 |[StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163) |
