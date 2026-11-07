---
title: "ASR-Streaming"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asrstreaming"
---

<span id="PHNDGEJv"></span>
# Introduction

To integrate real\-time large model streaming speech recognition (ASR) into your application using the WebSocket protocol, this guide provides complete coverage of authentication requirements, detailed protocol specifications, troubleshooting guidance, and ready\-to\-use code demos. You can select between bi\-directional streaming mode for low\-latency results or streaming input mode for enhanced accuracy, with optimized packet sizing recommendations to maximize performance.

<span id="08f16525"></span>
# API Endpoints Overview

**Base URL**

`wss://voice.ap-southeast-1.bytepluses.com/api/v3/sauc/{mode}`


|Mode |Path |Characteristics |Recommended Use Case |
|---|---|---|---|
|**Bi\-directional Streaming (Legacy)**  |`bigmodel` |Returns a response for each input packet; <br><br>Recognition resultsare returned as soon as possible.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only ASR 1.0</strong> is supported in this mode. </div><br> |Real\-time display scenarios |
|**Streaming Input (Non\-Streaming Recognition)**  |`bigmodel_nostream` |Returns a response for each input packet; <br><br>Recognition results are returned after the input audio exceeds 15 seconds, or after the final packet (a negative packet) is sent. |Accuracy\-sensitive scenarios |
|**Bi\-directional Streaming (Optimized)**   |`bigmodel_async` |Returns a response **only when the recognition result changes**;<br><br>Provides better performance and supports dual\-pass recognition |**Recommended for most scenarios** |


<span id="63eaea48"></span>
## Key Differences


* **Real\-time vs Accuracy Trade\-off**

   * Bi\-directional Streaming mode prioritizes **low latency**

   * Non\-Streaming mode prioritizes **higher accuracy**

   * Optimized Bi\-directional Streaming mode + Dual\-pass parameter delivers **both low\-latency real\-time transcription and high final recognition accuracy**


<span id="c128e7a3"></span>
## Performance Reference


* Bi\-directional Streaming (including optimized version):

   * Time to first character:  **~600 ms**

* Streaming input mode:

   * ~5 seconds audio → **300–400 ms** average response latency (**RTF ≈ 0.07**)


<span id="a212cd65"></span>
## Audio Streaming Best Practices


* **Packet duration**: 100–200ms

* **Sending interval**: 100–200ms

* Avoid overly large or small packets to ensure optimal performance


<span id="BBPPkp3R"></span>
# Authentication

The API supports two authentication methods. Due to the console upgrade, we recommend using the **simplified X\-Api\-Key authentication**.


|**Method** |**Header** |**Description** |
|---|---|---|
|**Recommended** |`X-Api-Key` |A single API Key generated from the [BytePlus console](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide). |
|**Legacy (compatible)**  |`X-Api-App-Key` + `X-Api-Access-Key` |The previous authentication method using an [App ID and Access Token](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide) pair. |


**Example (Recommended)** 

```Python
    headers = {
        "X-Api-Key": "xxxxxxxx", # your API key obtained from the new console
        "X-Api-Resource-Id": "volc.seedasr.sauc.duration", # ASR 2.0 resource ID
        "X-Api-Connect-Id": str(uuid.uuid4()),
    }
    
    ## Response Header
    X-Tt-Logid: 202407261553070FACFE6D19421815D605 
```


**Example (Legacy)** 

```Python
   headers = {
        "X-Api-App-Key": "xxxxxx", # APP ID obtained using the legacy console
        "X-Api-Access-Key": "xxxxxxxxxxxxxxx", # Access Token obtained using the legacy console
        "X-Api-Resource-Id": "volc.bigasr.sauc.duration" # ASR 1.0 resource ID
        "X-Api-Connect-Id": str(uuid.uuid4()),
    }
    
    ## Response Header
    X-Tt-Logid: 202407261553070FACFE6D19421815D605 
```



|Key |Description |Value Example |
|---|---|---|
|X\-Api\-Key |Please obtain the **API Key** from the BytePlus console, refer to [Console Guide](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default">Due to the console upgrade, authentication can now be completed using <code>X-Api-Key</code>.</div><br><br><br><div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported for backward compatibility.</div><br><br><br><div data-tips="true" data-tips-type="default">For new integrations, <code>X-Api-Key</code> is recommended.</div><br> |your\-api\-key |
|X\-Api\-Resource\-Id |Represents the resource information ID for calling the service. <br><br>**Seed ASR 1.0 model:** <br><br><br>* `volc.bigasr.sauc.duration`<br><br><br>**Seed ASR 2.0 model:** <br><br><br>* `volc.seedasr.sauc.duration` |**ASR 1.0:** <br><br><br>* `volc.bigasr.sauc.duration`<br><br><br>**ASR 2.0:** <br><br><br>* `volc.seedasr.sauc.duration` |
|X\-Api\-Connect\-Id |Used to track the flag ID of the current connection, and UUID is recommended |67ee89ba\-7050\-4c04\-a3d7\-ac61a63499b3 |


After the websocket handshake is successful, these response headers will be returned. It is strongly recommended to record **X\-Tt\-Logid (logid)**  as a troubleshooting clue.


|Key |Description |Value Example |
|---|---|---|
|X\-Api\-Connect\-Id |Used to track the flag ID of the current call information, and UUID is recommended |67ee89ba\-7050\-4c04\-a3d7\-ac61a63499b3 |
|X\-Tt\-Logid |The logid returned by the server. It is recommended that users obtain and print it to facilitate problem location |202407261553070FACFE6D19421815D605 |


<span id="wyJgANV0"></span>
# Protocol Details

<span id="gbpf5bW6"></span>
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


<span id="N6cXO6NJ"></span>
## WebSocket Binary Protocol

WebSocket uses a binary protocol to transmit data. The protocol consists of at least 4 bytes of **variable header**, **payload size**, and **payload**. The header describes the message type, serialization method, compression format, etc. The payload size is the length of the payload, and the payload is the specific content of the load, which varies according to the message type.

> **Note:**  Integer fields in the protocol are all represented in big\-endian.


<span id="8fkfTrwr"></span>
### Header Data Format


|Byte \ Bit |7 |6 |5 |4 |3 |2 |1 |0 |
|---|---|---|---|---|---|---|---|---|
|0 |Protocol version ||||Header size ||||
|1 |Message type ||||Message type specific flags ||||
|2 |Message serialization method ||||Message compression ||||
|3 |Reserved ||||||||
|4 |[Optional header extensions] ||||||||
|5 |[Payload, depending on the Message Type] ||||||||
|6 |... ||||||| |


<span id="gWK8S5Xx"></span>
### Header Field Description


|Field (size in bits) |Description |Value |
|---|---|---|
|Protocol version (4) |It may determine the use of different protocol versions in the future, so this field is used to make the client and server reach a consensus on the version. |0b0001 \- version 1 (only this version is currently available) |
|Header (4) |Header size. The actual header size (in bytes) is header size value x 4. |0b0001 \- header size = 4 (1 x 4) |
|Message type (4) |Message type. |0b0001 \- full client request containing request parameters sent by the client<br><br>0b0010 \- audio only request containing audio data sent by the client<br><br>0b1001 \- full server response containing recognition results sent by the server<br><br>0b1111 \- message type sent by the server when an error occurs in processing (such as invalid message format, unsupported serialization method, etc.) |
|Message type specific flags (4) |Supplementary information of Message type. |Request:<br><br>0b0000 \- set in full client request or audio only request containing non\-last audio packet<br><br>0b0010 \- set in audio only request containing last audio packet<br><br>Response:<br><br>0b0001 \- set in full client response or audio only response containing non\-last audio packet<br><br>0b0011 \- set in audio only response containing last audio packet<br><br>Bit meaning description:<br><br>bit0 (far right): indicates whether the sequence value information is encoded in the data frame<br><br>bit1: indicates whether the current data frame is the last packet |
|Message serialization method (4) |Payload serialization method of full client request;<br><br>The server will use the same serialization method as the client. |0b0000 \- no serialization<br><br>0b0001 \- JSON format |
|Message Compression (4) |Define the compression method of the payload;<br><br>The server will use the compression method of the client. |0b0000 \- no compression<br><br>0b0001 \- Gzip compression |
|Reserved (8) |Reserved for future use and also used as padding (so that the entire header totals 4 bytes). | |


<span id="KDhq7GyN"></span>
## Request Process

<span id="TTbkrJKV"></span>
### Establish Connection

According to the mechanism of the WebSocket protocol itself, the client will send an HTTP GET request to establish a connection with the server for protocol upgrade.

It is necessary to add an authentication signature header according to the identity authentication protocol. For the setting method, please refer to Authentication.

<span id="buX2xIT0"></span>
### Send full client request

After the WebSocket connection is established, the first request sent is a full client request. The format is:


|31 ... 24 |23 ... 16 |15 ... 8 |7 ... 0 |
|---|---|---|---|
|Header ||||
|Payload size (4B, unsigned int32) ||||
|Payload ||||



* **Header**: The 4\-byte header described above.

* **Payload size**: The length of the payload compressed according to the compression method specified in the Header, represented in big\-endian.

* **Payload**: Contains audio metadata and relevant parameters required by the server, generally in JSON format. The specific parameter fields are as follows:



|Field |Description |Level |Format |Required |Remarks |
|---|---|---|---|---|---|
|user |User\-related configuration |1 |dict | |Provided for the server to filter logs |
|uid |User identifier |2 |string | |It is recommended to use IMEI or MAC. |
|did |Device name |2 |string | | |
|platform |Operating system and API version number |2 |string | |iOS/Android/Linux |
|sdk_version |SDK version |2 |string | | |
|app_version |App version |2 |string | | |
|audio |Audio\-related configuration |1 |dict |✓ | |
|format |Audio container format |2 |string |✓ |pcm(pcm_s16le) / wav(pcm_s16le) / ogg |
|language |Designate recognized language<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only for streaming input mode </strong><strong><code>/api/v3/sauc/bigmodel_nostream</code></strong> , not for bi\-directional streaming mode. </div><br> |2 |string | |When it's empty, the model supports **Mandarin Chinese, English, Cantonese, Shanghainese, Minnan, Sichuan, Shaanxi dialect ** recognition. When it's set to the specific key below, then it can recognize below languages.<br><br><br>* English set to: **en\-US** <br><br>* Mandarin Chinese set to: **zh\-CN**<br><br>* Cantonese set to: **yue\-CN**<br><br>* Japanese set to: **ja\-JP**<br><br>* Indonesian Bahasa set to: **id\-ID**<br><br>* Spanish set to: **es\-MX**<br><br>* Portuguese set to: **pt\-BR**<br><br>* German set to: **de\-DE**<br><br>* French set to: **fr\-FR**<br><br>* Korean set to: **ko\-KR**<br><br>* Filipino set to: **fil\-PH**<br><br>* Malay set to: **ms\-MY**<br><br>* Thai set to: **th\-TH**<br><br>* Arabic set to: **ar\-SA**<br><br>* Italian set to: **it\-IT**<br><br>* Bengali set to: **bn\-BD**<br><br>* Greek set to: **el\-GR**<br><br>* Dutch set to: **nl\-NL**<br><br>* Russian set to: **ru\-RU**<br><br>* Turkish set to: **tr\-TR**<br><br>* Vietnamese set to: **vi\-VN**<br><br>* Polish set to: **pl\-PL**<br><br>* Romanian set to: **ro\-RO**<br><br>* Ukrainian set to: **uk\-UA**<br><br>* Azerbaijani set to: **az\-AZ**<br><br>* Bulgarian set to: **bg\-BG**<br><br>* Czech set to: **cs\-CZ**<br><br>* Danish set to: **da\-DK**<br><br>* Finnish set to: **fi\-FI**<br><br>* Hindi set to: **hi\-IN**<br><br>* Hungarian set to: **hu\-HU**<br><br>* Kazakh set to: **kk\-KZ**<br><br>* Khmer set to: **km\-KH**<br><br>* Burmese set to: **my\-MM**<br><br>* Norwegian set to: **no\-NO**<br><br>* Punjabi set to: **pa\-PK**<br><br>* Swedish set to: **sv\-SE**<br><br>* Swahili set to: **sw\-KE**<br><br>* Urdu set to: **ur\-PK** |
|codec |Audio encoding format |2 |string | |raw / opus, default is raw(pcm). |
|rate |Audio sampling rate |2 |int | |Default is 16000, currently only 16000 is supported |
|bits |Audio sampling point bit number |2 |int | |Default is 16. |
|channel |Number of audio channels |2 |int | |1(mono) / 2(stereo), default is 1. |
|request |Request\-related configuration |1 |dict |✓ | |
|model_name |Model name |2 |string |✓ |Currently only bigmodel |
|output_zh_variant |Enable Traditional Chinese output<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Supported in optimized Bi\-direction streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_async</code></strong></div><br><br><br><div data-tips="true" data-tips-type="default"><strong>and</strong> <strong>streaming input mode </strong><strong><code>/api/v3/sauc/bigmodel_nostream</code></strong></div><br> |2 |string | |Specifies the target Traditional Chinese variant for output conversion.<br><br>`traditional`: Simplified Chinese to Traditional Chinese (Mainland convention)<br><br>`tw`: Simplified Chinese to Traditional Chinese (Taiwan variant)<br><br>`hk`: Simplified Chinese to Traditional Chinese (Hong Kong variant) |
|enable_auto_lang |Add language auto\-detection capability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only supported</strong> in streaming input mode <strong><code>/api/v3/sauc/bigmodel_nostream</code></strong>. <strong>Must be used together</strong> with the <strong><code>end_window_size</code></strong> parameter; otherwise, recognition accuracy may be affected.</div><br> |2 |bool | |Default is false.<br><br>When `enable_auto_lang=true`, a multilingual ASR model is used to automatically detect the language of the input audio and dynamically routes the request to the corresponding NLU (Natural Language Understanding) cluster based on the detection result. The caller does not need to specify the language in advance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">If both <code>language</code> and <code>enable_auto_lang=true</code> are provided, the automatically detected language will take precedence.</div><br> |
|enable_lid |Enable language identification (LID).<br><br><div data-tips="true" data-tips-type="default">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only for optimized Bi\-direction streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_async</code></strong><strong> and non\-streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_nostream</code></strong></div><br> |2 |bool | |Default is `false`.<br><br>When set to `true`, the recognition result includes the `lid_lang` field in additions, which indicates the detected language label. <br><br>For example:<br><br><br>* `singing_en`: English singing<br><br>* `singing_mand`: Mandarin singing<br><br>* `singing_dia_cant`: Cantonese singing<br><br>* `speech_en`: English speech<br><br>* `speech_mand`: Mandarin speech<br><br>* `other_langs`: Other human languages<br><br>* `others`: Non\-semantic voice or non\-human audio<br><br>* `"(blank)"`: Unable to determine (for example, audio is too short)<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default">The languages supported for language identification (<code>enable_lid</code>) are not identical to the transcription languages supported by the <code>language</code> parameter. </div><br><br><br>In the optimized bi\-directional streaming mode  **`/api/v3/sauc/bigmodel_async`**, enabling enable_lid automatically enables VAD\-based segmentation (default endpointing timeout: 800 ms, configurable via `end_window_size`).<br><br>The `lid_lang `label is included in the additions of utterances where `"definite": true` is returned. |
|enable_itn |Enable itn |2 |bool | |Default is true.<br><br>Text Normalization (ITN) is a part of the automatic speech recognition (ASR) post\-processing pipeline. The task of ITN is to convert the original speech output of the ASR model into a written form to improve the readability of the text.<br><br>For example, "一九七零年" \-\> "1970 年" and "一百二十三美元" \-\> "$123". |
|enable_punc |Enable punctuation |2 |bool | |Default is true. |
|enable_ddc |Enable smoothing |2 |bool | |Default is false.<br><br>Semantic Smoothing is a technology designed to improve the text readability and fluency of automatic speech recognition (ASR) results. This technology makes the text easier to read and understand by deleting or modifying the unsmooth parts in the ASR results, such as pauses, modal particles, and semantic repetitions. |
|enable_nonstream |Enable dual\-pass recognition<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only for optimized Bi\-direction streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_async</code></strong></div><br><br><br> |2 |bool | |Enable **streaming + non\-streaming dual\-pass recognition mode**: within a single interface, this mode supports **bidirectional streaming** for real\-time, word\-by\-word transcription output, while also leveraging a **non\-streaming re\-recognition** of segmented audio utterances to improve accuracy. This approach satisfies both **real\-time display requirements (low latency)**  and **high accuracy in final results**.<br><br>Currently, dual\-pass recognition is only supported in the **optimized bidirectional streaming version （** `/api/v3/sauc/bigmodel_async` **）**  and is **not available in the legacy pipeline**.<br><br>When dual\-pass recognition is enabled, **VAD\-based segmentation** is automatically activated (default endpointing timeout: 800 ms, configurable via the `end_window_size` parameter). Once VAD detects the end of an utterance, the segmented audio is reprocessed using the **non\-streaming model**.<br><br>Note that the `"definite": true` flag, indicating finalized utterances, is **only included in the recognition results returned by the non\-streaming model**. |
|show_speech_rate |Include speech rate in utterance metadata<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only for optimized Bi\-direction streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_async</code></strong><strong> and non\-streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_nostream</code></strong></div><br> |2 |bool | |If set to `"true"`, the `speech_rate` field (unit: tokens/s) will be included in the `additions` of each segmented utterance. Default is `"false"`.<br><br>In the **optimized bidirectional streaming version**, enabling this feature will automatically activate **VAD\-based segmentation** (default endpointing timeout: 800 ms, configurable via the `end_window_size` parameter). The `speech_rate` field is included in the `additions` of utterances where `"definite": true` in the recognition result. |
|show_volume |Include speech volume in utterance metadata<br><br><div data-tips="true" data-tips-type="default">Note:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Only for optimized Bi\-direction streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_async</code></strong><strong> and non\-streaming mode </strong><strong><code>/api/v3/sauc/bigmodel_nostream</code></strong></div><br> |2 |bool | |If set to `"true"`, the `volume` field (unit: dB) will be included in the `additions` of each segmented utterance. Default is `"false"`.<br><br>In the **optimized bidirectional streaming version**, enabling this feature will automatically activate **VAD\-based segmentation** (default endpointing timeout: 800 ms, configurable via the `end_window_size` parameter). The `volume` field is included in the `additions` of utterances where `"definite": true` in the recognition result. |
|show_utterances |Output speech pause, sentence segmentation, and word segmentation information |2 |bool | | |
|result_type |Result return method |2 |string | |Default is "full", which returns the full amount.<br><br>Setting it to "single" means incremental result return, that is, the results of previous sentence segments are not returned. |
|vad_segment_duration |Maximum mute threshold for semantic sentence segmentation |2 |int | |Unit ms, default is 3000. When the mute time exceeds this value, the text will be divided into two sentences. It does not determine the pause, so it will not modify the position where definite appears. After the end_window_size configuration, this parameter becomes invalid. |
|end_window_size |Forced pause time |2 |int | |Unit ms, default is 800, minimum 200. If the mute duration exceeds this value, it will directly pause and output finalized recognition results based on the silence duration. Configuring this value does not use semantic sentence segmentation, but divides sentences according to the mute duration. It is used in scenarios with high real\-time requirements and can obtain finalized sentences in advance |
|force_to_speech_time |Forced speech time |2 |int | |Unit ms, default is 10000, minimum 1. After the audio duration exceeds this value, it will pause, and output definite according to the mute duration. It needs to be used with end_window_size.<br><br>It is used to solve the scenario of short audio + high real\-time requirements. When this parameter is not configured and only end_window_size is used, there will be no pause in the first 10s. It is recommended to set 1000, which may affect the recognition accuracy. |
|sensitive_words_filter |Sensitive word filtering |2 |string | |Sensitive word filtering function, supporting on or off, and custom sensitive words. This parameter can achieve: no processing (default, that is, display the original text), filtering, and replacement with \*.<br><br>Example:<br><br>system_reserved_filter // Whether to use system sensitive words, which will be replaced with \* (the default system sensitive words mainly include some restricted vocabulary)<br><br>filter_with_empty // Sensitive words to be replaced with empty<br><br>filter_with_signed // Sensitive words to be replaced with \*<br><br>```Python```<br>```"sensitive_words_filter":{"system_reserved_filter":true,"filter_with_empty":["敏感词"],"filter_with_signed":["敏感词"]},```<br><br><br> |
|corpus |Corpus/intervention words, etc. |2 |dict | | |
|context |Hotword or Context function |3 |string | |Hotword direct transmission, limited to 5000 words.<br><br>```Plain Text```<br>```"context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}"```<br><br><br>Context, limited to 800 tokens and within 20 rounds (inclusive). If exceeded, it will be truncated in chronological order from new to old, and the updated dialogues will be preferentially retained.<br><br>The context_data field is arranged in the order from new to old. The following is an example after deserialization. It needs to be serialized into a jsonstring (escape quotes) when passing in.<br><br>**Seed ASR 2.0 extends the scope of contextual understanding from pure text to the visual dimension.** <br><br>By comprehending image content, it helps the model achieve more accurate speech transcription.<br><br>Images are passed via image_url, with a limit of **1 image per request** and a **maximum size of 500KB (supported formats: JPEG, JPG, PNG).** <br><br>```JSON```<br>```// Context: Can include dialogue history, bot information, personalization details, business scenario info, etc., such as:```<br>```// a. Dialogue history: Pass in the most recent rounds of conversation```<br>```// b. Bot information: e.g., "I'm chatting with Lin Daiyu", "I'm talking to my phone using Assistant A"```<br>```// c. Personalization info: "I'm currently in Haidian District, Beijing", "I have a Sichuan accent", "I like music"```<br>```// d. Business scenario info: "This is a recording of an external customer interview by a Ping An salesman, which may involve..."```<br>```{```<br>```    \"context_type\": \"dialog_ctx\",```<br>```    \"context_data\":[```<br>```        {\"text\": \"text1\"},```<br>```        {\"image_url\": \"image_url\"},```<br>```        {\"text\": \"text2\"},```<br>```        {\"text\": \"text3\"},```<br>```        {\"text\": \"text4\"},```<br>```        ...```<br>```    ]```<br>```}```<br><br><br> |


<span id="7JB9ZgiR"></span>
### Request parameter sample:

<span id="zXoQnu1e"></span>
### ```Python
{
            "user": {
                "uid": "demo_uid",
            },
            "audio": {
                "format": "wav",
                "codec": "raw",
                "rate": 16000,
                "bits": 16,
                "channel": 1,
                # "language": "yue-CN"
            },
            "request": {
                "model_name": "bigmodel",
                # "output_zh_variant": "traditional",   // one of traditional/tw/hk
                "enable_itn": True,
                "enable_punc": True,
                "enable_ddc": True,
                "show_utterances": True,
                "enable_nonstream": True,
                "result_type": "full",
                "end_window_size":800,
                "show_speech_rate": True,
                "show_volume": True, 
               #"sensitive_words_filter": "{\"system_reserved_filter\":true,\"filter_with_empty\":[\"word1\"],\"filter_with_signed\":[\"word2\"]}",
               #"corpus": {
               #"context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}],\"context_type\":\"dialog_ctx\",\"context_data\":[{\"text\":\"text1\"},{\"image_url\":\"image_url\"},{\"text\":\"text2\"},{\"text\":\"text3\"},{\"text\":\"text4\"}]}"
               # }
            }
}
```


<span id="NAnougLw"></span>
### Send audio only request

After the client sends a full client request, it then sends an audio\-only client request containing audio data. The audio should adopt the format (audio format, codec, sampling rate, channel) specified in the full client request. The format is as follows:


|31 ... 24 |23 ... 16 |15 ... 8 |7 ... 0 |
|---|---|---|---|
|Header ||||
|Payload size (4B, unsigned int32) ||||
|Payload ||||


The payload is the compressed audio data using the specified compression method. You can send audio only request multiple times. For example, in streaming speech recognition, if 100ms of audio data is sent each time, the payload in the audio only request is 100ms of audio data.

<span id="nNa5Ao30"></span>
### Full server response

The server will return a full server response for both the full client request and the audio only request sent by the client. The format is as follows:


|31 ... 24 |23 ... 16 |15 ... 8 |7 ... 0 |
|---|---|---|---|
|Header ||||
|Sequence ||||
|Payload size (4B, unsigned int32) ||||
|Payload ||||


The payload content is in JSON format containing recognition results. The field description is as follows:


|Field |Description |Level |Format |Required |Remarks |
|---|---|---|---|---|---|
|result |Recognition result |1 |list | |Only filled in when the recognition is successful |
|text |Recognition result text of the entire audio |2 |string | |Only filled in when the recognition is successful. |
|utterances |Speech sentence segmentation information of the recognition result |2 |list | |Only filled in when the recognition is successful and show_utterances is activated |
|text |Utterance\-level text content |3 |string | |Only filled in when the recognition is successful and show_utterances is activated |
|start_time |Start time (ms) |3 |int | |Only filled in when the recognition is successful and show_utterances is activated |
|end_time |End time (ms) |3 |int | |Only filled in when the recognition is successful and show_utterances is activated |
|definite |Whether is a definite clause |3 |bool | |Only filled in when the recognition is successful and show_utterances is activated |


<span id="Yhmh9T3S"></span>
### Response playload sample:

<span id="ahNB4LNO"></span>
### ```JSON
{
  "code": 0,
  "event": 0,
  "is_last_package": true,
  "payload_sequence": 16,
  "payload_size": 1883,
  "payload_msg": {
    "audio_info": {
      "duration": 5280
    },
    "result": {
      "additions": {
        "log_id": "20260318182953635E72C86CE703AA8622"
      },
      "text": "Hello, if you want to use ByteDance's speech service, please contact ByteDance's customer service.",
      "utterances": [
        {
          "additions": {
            "all_matched_hotwords": "",
            "fixed_prefix_result": "",
            "invoke_type": "hard_vad",
            "source": "two_pass",
            "speech_rate": "2.6666666666666665",
            "use_bigasr_post_process": "true",
            "volume": "80.1030682447440938"
          },
          "definite": true,
          "end_time": 5282,
          "start_time": 32,
          "text": "Hello, if you want to use ByteDance's speech service, please contact ByteDance's customer service.",
          "words": [
            {
              "end_time": 552,
              "start_time": 312,
              "text": "Hello"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 992,
              "start_time": 792,
              "text": "if"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 1112,
              "start_time": 992,
              "text": "you"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 1272,
              "start_time": 1112,
              "text": "want"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 1392,
              "start_time": 1272,
              "text": "to"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 1512,
              "start_time": 1392,
              "text": "use"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 2192,
              "start_time": 1632,
              "text": "ByteDance's"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 2392,
              "start_time": 2232,
              "text": "speech"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 2672,
              "start_time": 2552,
              "text": "service"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 3152,
              "start_time": 2952,
              "text": "please"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 3552,
              "start_time": 3312,
              "text": "contact"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 4312,
              "start_time": 3752,
              "text": "ByteDance's"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 4592,
              "start_time": 4352,
              "text": "customer"
            },
            {
              "end_time": -1,
              "start_time": -1,
              "text": " "
            },
            {
              "end_time": 4952,
              "start_time": 4792,
              "text": "service"
            }
          ]
        }
      ]
    }
  }
}
```


<span id="b18I9rt8"></span>
### Error message from server

When the server encounters unsolvable binary/transport protocol issues (for example, the client sends messages in a serialization format not supported by the server), it will send an "Error message from server". The format is as follows:


|**31 ... 24** |**23 ... 16** |**15 ... 8** |**7 ... 0** |
|---|---|---|---|
|Header ||||
|Error message code (4B, unsigned int32) ||||
|Error message size (4B, unsigned int32) ||||
|Error message (UTF8 string) ||||


`Header`: The 4\-byte header described in the preceding text.

`Error message code`: Error code, represented in **big\-endian** format.

`Error message size`: Length of the error message, represented in **big\-endian** format.

`Error message`: The error message content.

<span id="b18I9rt8"></span>
### Sample Message Flow

Example: The client sends 3 requests.

The following message flow will send multiple messages, each containing the version, header size, and reserved data. Since the values of these fields are the same in each message, they are omitted in some messages.

**The client sends a "Full client request"** 

version: `b0001` (4 bits)

header size: `b0001` (4 bits)

message type: `b0001` (Full client request) (4bits)

message type specific flags: `b0000` (use_specific_pos_sequence) (4bits)

message serialization method: `b0001` (JSON) (4 bits)

message compression: `b0001` (Gzip) (4bits)

reserved data: `0x00` (1 byte)

payload size = The length after Gzip compression

payload: Data obtained by compressing the JSON\-formatted request fields using Gzip

**The server responds a "Full server response"** 

version: `b0001`

header size: `b0001`

message type: `b1001` (Full server response)

message type specific flags: `b0001` (none)

message serialization method: `b0001` (JSON 和请求相同)

message compression: `b0001` (Gzip 和请求相同)

reserved data: `0x00`

sequence: `0x00` `0x00` `0x00` `0x01` (4 byte) sequence=1

payload size = The length after Gzip compression

payload: Response data after Gzip compression

**The client sends an "Audio only client request" containing the first packet of audio data.** 

version: `b0001`

header size: `b0001`

message type: `b0010` (audio only client request)

message type specific flags: `b0000` (The user sets a positive sequence number)

message serialization method: b0000 (none \- raw bytes)

message compression: b0001 (Gzip)

reserved data: 0x00

payload size = The length after Gzip compression

payload: Response data after Gzip compression

**The server responds a "Full server response"** 

message type: `0b1001` \- Full server response

message specific flags: `0b0001` (none)

message serialization: `0b0001` (JSON, same as the request)

message compression `0b0001` (Gzip, same as the request)

reserved data: `0x00`

sequence data: `0x00` `0x00` `0x00` `0x02` (4 byte) sequence=2

payload size = The length after Gzip compression

payload: Response data after Gzip compression

**The client sends an "Audio\-only client request" containing the last packet of audio data (via message type specific flags)** 

message type: `b0010` (audio only client request)

message type specific flags: **`b0010`** (the **last packet** of audio data request)

message serialization method: `b0000` (none \- raw bytes)

message compression: `b0001` (Gzip)

reserved data: `0x00`

payload size = The length after Gzip compression

payload: Response data after Gzip compression

**The server responds with a "Full server response" — the final reply and processing result**

message type: `b1001` (Full server response)

message type specific flags: **`b0011`** (the **last packet** of audio data request)

message serialization method: `b0001` (JSON)

message compression: `b0001` (Gzip)

reserved data: `0x00`

sequence data: `0x00` `0x00` `0x00` `0x03` (4byte) sequence=3

payload size = The length after Gzip compression

payload: Response data after Gzip compression

**If an error message occurs during processing, the following error frames may be returned**

message type: `b1111` (error response)

message type specific flags: `b0000` (none)

message serialization method: `b0001` (JSON)

message compression: `b0000` (none)

reserved data: `0x00`

Error code data: `0x2A` `0x0D` `0xA2` `0xff` (4byte) 错误码

payload size = The JSON length of the error message object

payload: The JSON data of the error message object

<span id="DwPzL2UC"></span>
## Error codes


|Error Code |**Meaning** |**Description** |
|---|---|---|
|20000000 |Success | |
|45000001 |Invalid request parameters |Missing required fields in request parameters / invalid field values / duplicate requests |
|45000002 |Empty audio | |
|45000081 |Packet waiting timeout | |
|45000151 |Incorrect audio format | |
|550xxxxx |Internal server error | |
|55000031 |Server busy |Service overloaded and unable to process the current request. |


<span id="CQCzkOCq"></span>
# Demo


<Tabs>
<Tab zoneid="HWXc36oRjj" title="Python Example">
<TabTitle>Python Example</TabTitle>

<span id="Mwdy4TLH"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * : APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.


<span id="kMsH6RtC"></span>
## Python env


* Python：Version 3.9 and above.

* Pip：Version 25.1.1 and above. You can use the following command to install it.


```Bash
python3 -m pip install --upgrade pip
```


<span id="ds4P1OGq"></span>
## Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_44f3938ed393aefa432770a1e8a0b636.zip" name="Byteplus_ASR_SAUC_bidirection_python.zip">Byteplus_ASR_SAUC_bidirection_python.zip</Attachment>


&nbsp;

<span id="k2mYESOP"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_ASR_SAUC_bidirection_python
tar xvzf Byteplus_ASR_SAUC_bidirection_python.zip -C ./Byteplus_ASR_SAUC_bidirection_python
cd Byteplus_ASR_SAUC_bidirection_python
cd sauc_python
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
pip install requests
pip install aiohttp
```


<span id="PcB3FHnr"></span>
## Invoke

> In the `Config` class of the python script `sauc_websocket_demo.py`:

> * Replace with your APP ID.

> * `<access_token>`Replace with your Access Token.


```Bash
python3 sauc_websocket_demo.py --url wss://voice.ap-southeast-1.bytepluses.com/api/v3/sauc/bigmodel --file /path/to/your/audio.wav
```



</Tab>
<Tab zoneid="Sb7NnzEWAh" title="Go Example">
<TabTitle>Go Example</TabTitle>

<span id="5RYaB1lb"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * : APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

* Detailed information on environment setup is available in the README.md file located in the sample package.


<span id="4M9UlLd7"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_18e6c3812ca16d4819657a61af4f1fcb.zip" name="Byteplus_ASR_SAUC_bidirection_go.zip">Byteplus_ASR_SAUC_bidirection_go.zip</Attachment>


&nbsp;

<span id="sFqftcPS"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_ASR_SAUC_bidirection_go
tar xvzf Byteplus_ASR_SAUC_bidirection_go.zip -C ./Byteplus_ASR_SAUC_bidirection_go
cd Byteplus_ASR_SAUC_bidirection_go
cd sauc_go
go mod tidy
```


<span id="KPbc9SUs"></span>
### Invoke

> In the config.toml file:

> * Replace with your APP ID.

> * `<access_token>`Replace with your Access Token.


```Bash
go run main.go -file="/path/to/your/audio.wav" -url="wss://voice.ap-southeast-1.bytepluses.com/api/v3/sauc/bigmodel"
```



</Tab>
<Tab zoneid="vbZsKY7716" title="Java Example">
<TabTitle>Java Example</TabTitle>

<span id="cVhMJI2k"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * : APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

* Detailed information on environment setup is available in the README.md file located in the sample package.


<span id="3222E0dQ"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ff417ba5e89f71bdb965e9a0631d042f.zip" name="Byteplus_ASR_SAUC_bidirection_java.zip">Byteplus_ASR_SAUC_bidirection_java.zip</Attachment>


&nbsp;

<span id="ZtiwdPGe"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_ASR_SAUC_bidirection_java
tar xvzf Byteplus_ASR_SAUC_bidirection_java.zip -C ./Byteplus_ASR_SAUC_bidirection_java
cd Byteplus_ASR_SAUC_bidirection_java
cd sauc
```


<span id="4f6abSUN"></span>
### Invoke

> In the mvn command:

> * `your_app_id`Replace with your APP ID.

> * `your_token`Replace with your Access Token.


```Bash
mvn clean compile exec:java -Dexec.args="wss://openspeech.bytedance.com/api/v3/sauc/bigmodel your_app_id your_token /path/to/your/audio.wav"
```



</Tab>
</Tabs>
