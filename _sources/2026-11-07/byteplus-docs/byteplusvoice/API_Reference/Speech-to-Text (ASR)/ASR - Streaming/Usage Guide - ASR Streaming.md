---
title: "Usage Guide - ASR Streaming"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asrstreamingguide"
---

<span id="Bq6zTBA2"></span>
# Introduction

To integrate real\-time large model streaming speech recognition (ASR) into your application using the WebSocket protocol, this guide provides complete coverage of authentication requirements, detailed protocol specifications, troubleshooting guidance, and ready\-to\-use code demos. You can select between bi\-directional streaming mode for low\-latency results or streaming input mode for enhanced accuracy, with optimized packet sizing recommendations to maximize performance.

<span id="Wur3eOc9"></span>
# API Endpoints Overview

**Base URL**

`wss://voice.ap-southeast-1.bytepluses.com/api/v3/sauc/{mode}`


|Mode |Path |Characteristics |Recommended Use Case |
|---|---|---|---|
|**Unidirectional** |`bigmodel_nostream` |Returns a response for each input packet; <br><br>Recognition results are returned after the input audio exceeds 15 seconds, or after the final packet (a negative packet) is sent. |Accuracy\-sensitive scenarios |
|**Bi\-directional** |`bigmodel_async` |Returns a response **only when the recognition result changes**;<br><br>Provides better performance and supports dual\-pass recognition |**Recommended for most scenarios** |


<span id="4g3GR6qK"></span>
## Key Differences


* **Real\-time vs Accuracy Trade\-off**

   * Bi\-directional Streaming mode prioritizes **low latency**

   * Unidirectional Streaming mode prioritizes **higher accuracy**

   * Bi\-directional Streaming mode + Dual\-pass parameter delivers **both low\-latency real\-time transcription and high final recognition accuracy**


<span id="fTReBwXp"></span>
## Performance Reference


* Bi\-directional Streaming (including optimized version):

   * Time to first character:  **~600 ms**

* Streaming input mode:

   * ~5 seconds audio → **300–400 ms** average response latency (**RTF ≈ 0.07**)


<span id="kOYbvhbE"></span>
## Audio Streaming Best Practices


* **Packet duration**: 100–200ms

* **Sending interval**: 100–200ms

* Avoid overly large or small packets to ensure optimal performance


<span id="AmB26rex"></span>
## Interaction Process

```JSON
Client
 │
 │ Send full request (parameters)
 ▼
Server
 │
 └─ Acknowledge request
 │
 ▼
Streaming
 │
 │ Send audio packet (chunks)
 ▼
 Server
 │
 ├─ Bi-directional Streaming Mode
 │ │
 │ └─ Return real-time results （faster response）
 │ 
 │
 ├─ Non-streaming Mode
 │ │
 │ ├─ Process full audio or each time when the input audio exceeds 15 seconds
 │ │
 │ └─ Return final result (higher accuracy)
 │
 │
 ├─ Bi-directional Streaming (Optimized) + Dual-pass Mode (Streaming + Non-streaming) 
 │ │
 │ ├─ Return streaming results (fast display)
 │ │
 │ ├─ VAD detects end of utterance
 │ │
 │ └─ Trigger second-pass (non-streaming)
 │ │
 │ └─ Return refined result ("definite": true)
 │
 │
 ▲
 │ (loop until audio ends)
 │
 │ ...
 │
 │ Send final packet
 ▼
Server
 │
 └─ Return final result 
```


<span id="wtXeTfxq"></span>
##
