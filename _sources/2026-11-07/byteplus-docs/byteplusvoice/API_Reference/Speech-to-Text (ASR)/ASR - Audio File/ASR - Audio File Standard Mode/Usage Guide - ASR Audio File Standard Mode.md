---
title: "Usage Guide - ASR Audio File Standard Mode"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asraucstandardusageguide"
---

<span id="GR91ISOy"></span>
# Introduction

The Audio File Speech Recognition API converts audio files into text through **asynchronous processing**, supporting multiple audio formats and delivering accurate transcription results. It is ideal for batch or offline speech recognition scenarios, providing reliable and efficient transcription for various applications such as voice analysis, content indexing, and automated subtitles.

<span id="twyQQv8I"></span>
# Usage Limitations


|**Item** |**Description** |
|---|---|
|Audio Duration |< 5 hours |
|File Size |< 512MB |
|Audio Encoding |Supports OPUS, WAV, MP3, SPX, OGG, AMR, AAC and M4A formats |
|Multi\-Channel Audio |Both mono and stereo are supported; However, stereo files require longer processing time compared to mono |
|Response Time |Transcription results will be returned within 3 hours. After submission, the results must be queried within 7 days. |
|Concurrency Limit |The activated version supports a maximum of 10 QPS by default, with a total audio duration of no more than 500 hours submitted within a 30\-minute period. |


<span id="sn4OLWgf"></span>
# Processing Workflow

The processing flow of the large model recording file recognition service is divided into two stages: **task submission** and ** result query**.


1. **Task Submission**

   Call the **Submit Task API** to create a recognition task. When sending the request, the client must provide a unique request identifier through the `X-Api-Request-Id` header. This ID is used as the **task identifier** for the recognition job.

   The client should store this ID and use it when querying the task result.

2. **Result Query**

   Call the **Query Result API** using the same `X-Api-Request-Id`  to check the task status and retrieve the transcription result.

   Because the service processes audio asynchronously, the recognition result may not be available immediately after submission.


<span id="g45IrAbk"></span>
## Best Practice

The recommended integration pattern is:


1. Generate a unique `X-Api-Request-Id` for each recognition task.

2. Submit the recognition request using this ID.

3. Periodically call the **Query API** with the same ID to check the task status.

4. Continue polling until the task reaches a **final state**.


When the `X-Api-Status-Code` in the Query API response header is `20000000`, the recognition task has finished and the transcription result can be obtained from the response body.

Typical status codes returned in the response header:


|**Status Code** |**Meaning** |
|---|---|
|20000000 |Task completed successfully |
|20000001 |Task is being processed |
|20000002 |Task is queued |


```Plain Text
Client
   │
   │ Submit audio URL
   ▼
Submit API
   │
   │ record task_id （X-Api-Request-Id）
   ▼
Client polls Query API
   │
   ├─ 20000001 / 20000002 → processing
   │
   └─ 20000000 → result ready
```


<span id="PlhFkNVT"></span>
# **Status Code**


|Error Code |Meaning |Description |
|---|---|---|
|20000000 |Success | |
|20000001 |Processing | |
|20000002 |Task in queue | |
|20000003 |Mute audio |There is no need to query again when this error code is returned. Just submit again directly. |
|45000001 |Invalid request parameters |The request parameters are missing required fields / the field values are invalid / repeated requests. |
|45000002 |Empty audio | |
|45000151 |Incorrect audio format | |
|550xxxx |Service internal processing error | |
|55000031 |Server busy |The service is overloaded and cannot process the current request. |


<span id="s5lXQfXe"></span>
#
