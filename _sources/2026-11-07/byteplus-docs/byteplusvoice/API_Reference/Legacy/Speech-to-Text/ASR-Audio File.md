---
title: "ASR-Audio File"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofile"
---

<span id="aYHcXoEE"></span>
# Introduction

The Audio File Speech Recognition API converts audio files into text through **asynchronous processing**, supporting multiple audio formats and delivering accurate transcription results. It is ideal for batch or offline speech recognition scenarios, providing reliable and efficient transcription for various applications such as voice analysis, content indexing, and automated subtitles.

<span id="qchECQYL"></span>
# Usage Limitations


|**Item** |**Description** |
|---|---|
|Audio Duration |< 5 hours |
|File Size |< 512MB |
|Audio Encoding |Supports OPUS, WAV, MP3, SPX, OGG, AMR, AAC and M4A formats |
|Multi\-Channel Audio |Both mono and stereo are supported; However, stereo files require longer processing time compared to mono |
|Response Time |Transcription results will be returned within 3 hours. After submission, the results must be queried within 7 days. |
|Concurrency Limit |The activated version supports a maximum of 10 QPS by default, with a total audio duration of no more than 500 hours submitted within a 30\-minute period. |


<span id="aYHcXoEE"></span>
# Processing Workflow

The processing flow of the large model recording file recognition service is divided into two stages: **task submission** and ** result query**.


1. **Task Submission**

   Call the **Submit API** to create a recognition task. When sending the request, the client must provide a unique request identifier through the `X-Api-Request-Id` header. This ID is used as the **task identifier** for the recognition job.

   The client should store this ID and use it when querying the task result.

2. **Result Query**

   Call the **Query API** using the same `X-Api-Request-Id`  to check the task status and retrieve the transcription result.

   Because the service processes audio asynchronously, the recognition result may not be available immediately after submission.


<span id="9fo2HNnv"></span>
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
   │ record task_id
   ▼
Client polls Query API
   │
   ├─ 20000001 / 20000002 → processing
   │
   └─ 20000000 → result ready
```


<span id="tACBDw93"></span>
# Authentication

The API supports two authentication methods. Due to the console upgrade, we recommend using the **simplified X\-Api\-Key authentication**.


|**Method** |**Header** |**Description** |
|---|---|---|
|**Recommended** |X\-Api\-Key |A single API Key generated from the [BytePlus console](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide). |
|**Legacy (compatible)**  |X\-Api\-App\-Key + X\-Api\-Access\-Key |The previous authentication method using an [App ID and Access Token](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide) pair. |


**Example (Recommended)** 

```Python
    headers = {
        "X-Api-Key": "xxxxxxxx", # your API key obtained from the new console
        "X-Api-Resource-Id": "volc.seedasr.auc", # ASR 2.0 resource ID
        "X-Api-Request-Id": str(uuid.uuid4()),
        "X-Api-Sequence": "-1"
    }
```


**Example (Legacy)** 

```Python
   headers = {
        "X-Api-App-Key": "xxxxxx", # APP ID obtained using the legacy console
        "X-Api-Access-Key": "xxxxxxxxxxxxxxx", # Access Token obtained using the legacy console
        "X-Api-Resource-Id": "volc.bigasr.auc" # ASR 1.0 resource ID
        "X-Api-Request-Id": str(uuid.uuid4()),
        "X-Api-Sequence": "-1"
    }
```


<span id="APpYZEKk"></span>
# Task Submission

<span id="7LZ0uRH1"></span>
## **Interface Address**

BytePlus address: `https://voice.ap-southeast-1.bytepluses.com/api/v3/auc/bigmodel/submit`

Request method: `HTTP POST`

<span id="5uBOVtO5"></span>
## Request

**Request Headers**


|Key |Description |Value Example |
|---|---|---|
|X\-Api\-Key |Please obtain the **API Key** from the BytePlus console, refer to [Console Guide](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Due to the console upgrade, authentication can now be completed using <code>X-Api-Key</code>.</div><br><br><br><div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported for backward compatibility.</div><br><br><br><div data-tips="true" data-tips-type="default">For new integrations, <code>X-Api-Key</code> is recommended.</div><br> |your\-api\-key |
|X\-Api\-Resource\-Id |Represents the resource information ID for calling the service. <br><br>**Seed ASR 1.0 model:** <br><br><br>* `volc.bigasr.auc`<br><br><br>**Seed ASR 2.0 model:** <br><br><br>* `volc.seedasr.auc` |* ASR 1.0<br><br>   * `volc.bigasr.auc`<br><br>* ASR 2.0<br><br>   * `volc.seedasr.auc` |
|X\-Api\-Request\-Id |Used for the **task ID ** of submitting and querying tasks. It is recommended to pass in a randomly generated UUID. |67ee89ba\-7050\-4c04\-a3d7\-ac61a63499b3 |
|X\-Api\-Sequence |Packet sequence number. The fixed value is \-1. | |


**Request Body**


|Field |Description |Level |Format |Required |Remarks |
|---|---|---|---|---|---|
|user |User\-related configuration |1 |dict | | |
|uid |User identifier |2 |string | |It is recommended to use IMEI or MAC. |
|audio |Audio\-related configuration |1 |dict |✓ | |
|url |Audio link |2 |string |✓ | |
|format |Audio container format | | | |raw / wav / mp3 / ogg |
|language |Designate recognized language |2 |string | |When it's empty, the model supports **Mandarin Chinese, English, Cantonese, Shanghainese, Minnan, Sichuan, Shaanxi dialect ** recognition. When it's set to the specific key below, then it can recognize below languages.<br><br><br>* English set to: **en\-US** <br><br>* Mandarin Chinese set to: **zh\-CN**<br><br>* Cantonese set to: **yue\-CN**<br><br>* Japanese set to: **ja\-JP**<br><br>* Indonesian Bahasa set to: **id\-ID**<br><br>* Spanish set to: **es\-MX**<br><br>* Portuguese set to: **pt\-BR**<br><br>* German set to: **de\-DE**<br><br>* French set to: **fr\-FR**<br><br>* Korean set to: **ko\-KR**<br><br>* Filipino set to: **fil\-PH**<br><br>* Malay set to: **ms\-MY**<br><br>* Thai set to: **th\-TH**<br><br>* Arabic set to: **ar\-SA**<br><br>* Italian set to: **it\-IT**<br><br>* Bengali set to: **bn\-BD**<br><br>* Greek set to: **el\-GR**<br><br>* Dutch set to: **nl\-NL**<br><br>* Russian set to: **ru\-RU**<br><br>* Turkish set to: **tr\-TR**<br><br>* Vietnamese set to: **vi\-VN**<br><br>* Polish set to: **pl\-PL**<br><br>* Romanian set to: **ro\-RO**<br><br>* Ukrainian set to: **uk\-UA**<br><br>* Azerbaijani set to: **az\-AZ**<br><br>* Bulgarian set to: **bg\-BG**<br><br>* Czech set to: **cs\-CZ**<br><br>* Danish set to: **da\-DK**<br><br>* Finnish set to: **fi\-FI**<br><br>* Hindi set to: **hi\-IN**<br><br>* Hungarian set to: **hu\-HU**<br><br>* Kazakh set to: **kk\-KZ**<br><br>* Khmer set to: **km\-KH**<br><br>* Burmese set to: **my\-MM**<br><br>* Norwegian set to: **no\-NO**<br><br>* Punjabi set to: **pa\-PK**<br><br>* Swedish set to: **sv\-SE**<br><br>* Swahili set to: **sw\-KE**<br><br>* Urdu set to: **ur\-PK** |
|codec |Audio encoding format |2 |string | |raw / opus, default is raw(pcm). |
|rate |Audio sampling rate |2 |int | |The default is 16000. |
|bits |Audio sampling point bits |2 |int | |The default is 16. |
|channel |Number of audio channels |2 |int | |1(mono) / 2(stereo), default is 1. |
|request |Request\-related configuration |1 |dict |✓ | |
|model_name |Model name |2 |string |✓ |Currently, only bigmodel is available. |
|output_zh_variant |Enable Traditional Chinese output |2 |string | |Specifies the target Traditional Chinese variant for output conversion.<br><br>`traditional`: Simplified Chinese to Traditional Chinese (Mainland convention)<br><br>`tw`: Simplified Chinese to Traditional Chinese (Taiwan variant)<br><br>`hk`: Simplified Chinese to Traditional Chinese (Hong Kong variant) |
|enable_auto_lang |Add language auto\-detection capability |2 |bool | |Default is false.<br><br>When `enable_auto_lang=true`, a multilingual ASR model is used to automatically detect the language of the input audio and dynamically routes the request to the corresponding NLU (Natural Language Understanding) cluster based on the detection result. The caller does not need to specify the language in advance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">If both <code>language</code> and <code>enable_auto_lang=true</code> are provided, the automatically detected language will take precedence.</div><br> |
|enable_lid |Enable language identification (LID) |2 |bool | |Default is `false`.<br><br>When set to `true`, the recognition result includes the `lid_lang` field in additions, which indicates the detected language label. <br><br>For example:<br><br><br>* `singing_en`: English singing<br><br>* `singing_mand`: Mandarin singing<br><br>* `singing_dia_cant`: Cantonese singing<br><br>* `speech_en`: English speech<br><br>* `speech_mand`: Mandarin speech<br><br>* `other_langs`: Other human languages<br><br>* `others`: Non\-semantic voice or non\-human audio<br><br>* `"(blank)"`: Unable to determine (for example, audio is too short)<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default">The languages supported for language identification (<code>enable_lid</code>) are not identical to the transcription languages supported by the <code>language</code> parameter. </div><br> |
|enable_itn |Enable ITN |2 |bool | |The default is true.<br><br>Text Normalization (ITN) is a part of the automatic speech recognition (ASR) post\-processing pipeline. The task of ITN is to convert the original speech output of the ASR model into a written form to improve the readability of the text.<br><br>For example, "一九七零年" \-\> "1970 年" and "一百二十三美元" \-\> "$123". |
|enable_punc |Enable punctuation |2 |bool | |The default is false. |
|enable_ddc |Enable smoothing |2 |bool | |The default is false.<br><br>Semantic Smoothing is a technology designed to improve the text readability and fluency of automatic speech recognition (ASR) results. This technology makes the text easier to read and understand by deleting or modifying the unsmooth parts in the ASR results, such as pauses, modal particles, and semantic repetitions. |
|enable_speaker_info |Enable Speaker Diarization |2 |bool | |The default is false.<br><br>When enabled, speaker information can be returned. Best performance is achieved when the number of speakers is **10 or fewer**.<br><br>If the audio contains significant variations in volume, distance, or other acoustic conditions, speaker differentiation accuracy **cannot be guaranteed**. |
|enable_channel_split |Enable dual\-channel recognition |2 |bool | |If set to "True", it will be marked with channel_id in the return result, 1 for the left channel and 2 for the right channel. The default is false. |
|show_utterances |Output speech pause, sentence segmentation, and word segmentation information |2 |bool | | |
|vad_segment |Use VAD to segment sentences |2 |bool | |The default is false, and the default is semantic sentence segmentation.<br><br>When dual\-channel recognition is turned on, VAD sentence segmentation is usually required, and this parameter can be turned on at the same time. |
|end_window_size |Forced pause time |2 |int | |The range is 300\-5000ms. It is recommended to set 800ms or 1000ms. For sensitive scenarios, 500ms or smaller can be configured. (If the configuration is too small, it will cause the sentence segmentation to be too broken. If the configuration is too large, it will be difficult to separate the speaking content. It is recommended to configure according to your own scenario.)<br><br>When this value is configured, semantic sentence segmentation is not used, and sentence segmentation is performed according to the mute duration. |
|sensitive_words_filter |Sensitive word filtering |2 |string | |Sensitive word filtering function, supporting on or off, and custom sensitive words. This parameter can achieve: no processing (default, that is, display the original text), filtering, and replacement with \*.<br><br>Example:<br><br>system_reserved_filter // Whether to use system sensitive words, which will be replaced with \* (the default system sensitive words mainly include some restricted vocabulary)<br><br>filter_with_empty // Sensitive words to be replaced with empty<br><br>filter_with_signed // Sensitive words to be replaced with \*<br><br>"sensitive_words_filter":{"system_reserved_filter":true,"filter_with_empty":["敏感词"],"filter_with_signed":["敏感词"]} |
|corpus |Corpus/intervention words, etc. |2 |dict | | |
|context |Hotword or Context function |3 |string | |Hotword direct transmission, limited to 5000 words.<br><br>```JSON```<br>```"context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}"```<br><br><br>Context, limited to 800 tokens and within 20 rounds (inclusive). If exceeded, it will be truncated in chronological order from new to old, and the updated dialogues will be preferentially retained.<br><br>The context_data field is arranged in the order from new to old. The following is an example after deserialization. It needs to be serialized into a jsonstring (escape quotes) when passing in.<br><br>**Seed ASR 2.0 extends the scope of contextual understanding from pure text to the visual dimension.** <br><br>By comprehending image content, it helps the model achieve more accurate speech transcription.<br><br>Images are passed via `image_url`, with a limit of **1 image per request** and a **maximum size of 500KB (supported formats: JPEG, JPG, PNG).** <br><br>```JSON```<br>```// Context: Can include dialogue history, bot information, personalization details, business scenario info, etc., such as:```<br>```// a. Dialogue history: Pass in the most recent rounds of conversation```<br>```// b. Bot information: e.g., "I'm chatting with Lin Daiyu", "I'm talking to my phone using Assistant A"```<br>```// c. Personalization info: "I'm currently in Haidian District, Beijing", "I have a Sichuan accent", "I like music"```<br>```// d. Business scenario info: "This is a recording of an external customer interview by a Ping An salesman, which may involve..."```<br>``````<br>```{```<br>```    \"context_type\": \"dialog_ctx\",```<br>```    \"context_data\":[```<br>```        {\"text\": \"text1\"},```<br>```        {\"image_url\": \"image_url\"},```<br>```        {\"text\": \"text2\"},```<br>```        {\"text\": \"text3\"},```<br>```        {\"text\": \"text4\"},```<br>```        ...```<br>```    ]```<br>```}```<br> |
|callback |Callback address |1 |string | |Example:<br><br>```Plain Text```<br>```"callback": "http://xxx"```<br><br><br> |
|callback_data |Callback information |1 |string | |Example:<br><br>```Plain Text```<br>```"callback_data":"$Request-Id"```<br><br><br> |


**Request Body Example**

```JSON
{
    "user": {
        "uid": "6F832CCB-F586-4FDB-8A77-B26AAECCD3CF"
    },
    //"callback": "https://customcallback/site1",
    "audio": {
        "url": "https://xxx.com/obj/sample.mp3",
        "format": "mp3"
        // "language": "ja-JP",
        // "channel": 2
    },
    //"callback_data": "testcallbackdatamark1",
    "request": {
        "model_name": "bigmodel",
        "output_zh_variant": "traditional",   // one of traditional/tw/hk
        "enable_channel_split": true,
        "enable_ddc": true,
        "enable_speaker_info": false,
        "enable_punc": true,
        "enable_itn": false,
        "show_utterances": true
        //"sensitive_words_filter": "{\"system_reserved_filter\":true,\"filter_with_empty\":[\"八\"],\"filter_with_signed\":[\"岭\"]}",
        // "corpus": {
        //     "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}],\"context_type\":\"dialog_ctx\",\"context_data\":[{\"text\":\"text1\"},{\"image_url\":\"image_url\"},{\"text\":\"text2\"},{\"text\":\"text3\"},{\"text\":\"text4\"}]}"
        // }
    }
}
```


<span id="mBmsG0ro"></span>
## Response

**Response Headers**


|Key |Description |Value Example |
|---|---|---|
|X\-Tt\-Logid |The logid returned by the server. It is recommended that users obtain and print it to facilitate problem location. |202407261553070FACFE6D19421815D605 |
|X\-Api\-Status\-Code |The status code returned by the server after submitting the task. 20000000 indicates successful submission, and others indicate failure. | |
|X\-Api\-Message |The information returned by the server after submitting the task. OK indicates success, and others indicate failure. | |


**Response Body**

The response body of a successful **Submit API** request is empty.

```JSON
{}
```


<span id="Y9TWBW3I"></span>
# Query Results

<span id="6LLwgAKA"></span>
## **Interface Address**

BytePlus address: `https://voice.ap-southeast-1.bytepluses.com/api/v3/auc/bigmodel/query`

Request method: `HTTP POST`

<span id="B0nRmbji"></span>
## Request

**Request Headers**


|Key |Description |Value Example |
|---|---|---|
|X\-Api\-Key |Please obtain the **API Key** from the BytePlus console, refer to [Console Guide](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Due to the console upgrade, authentication can now be completed using <code>X-Api-Key</code>.</div><br><br><br><div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported for backward compatibility.</div><br><br><br><div data-tips="true" data-tips-type="default">For new integrations, <code>X-Api-Key</code> is recommended.</div><br> |your\-api\-key |
|X\-Api\-Resource\-Id |Represents the resource information ID for calling the service. <br><br>**Seed ASR 1.0 model:** <br><br><br>* `volc.bigasr.auc`<br><br><br>**Seed ASR 2.0 model:** <br><br><br>* `volc.seedasr.auc` |* ASR 1.0<br><br>   * `volc.bigasr.auc`<br><br>* ASR 2.0<br><br>   * `volc.seedasr.auc` |
|X\-Api\-Request\-Id |Used for the **task ID ** of submitting and querying tasks. It is recommended to pass in a randomly generated UUID. |67ee89ba\-7050\-4c04\-a3d7\-ac61a63499b3 |
|X\-Api\-Sequence |Packet sequence number. The fixed value is \-1. | |


**Request Body**

The body is an empty json:

```JSON
{}
```


<span id="cuV19i0D"></span>
## Response

**Response Headers**


|Key |Description |Value Example |
|---|---|---|
|X\-Tt\-Logid |The logid returned by the server. It is recommended that users obtain and print it to facilitate problem location. |202407261553070FACFE6D19421815D605 |
|X\-Api\-Status\-Code |The status code returned by the server after submitting the task. For specific error codes, refer to the following error code list. | |
|X\-Api\-Message |The information returned by the server after submitting the task. OK indicates success, and others indicate failure. | |


**Response Body**


|Field |Description |Level |Format |Remarks |
|---|---|---|---|---|
|result |Recognition result |1 |list |Only filled in when the recognition is successful. |
|text |The recognition result text of the entire audio |2 |string |Only filled in when the recognition is successful. |
|utterances |Speech sentence segmentation information of the recognition result |2 |list |Only filled in when the recognition is successful and show_utterances is enabled. |
|text |Text content at the utterance level |3 |string |Only filled in when the recognition is successful and show_utterances is enabled. |
|start_time |Start time (milliseconds) |3 |int |Only filled in when the recognition is successful and show_utterances is enabled. |
|end_time |End time (milliseconds) |3 |int |Only filled in when the recognition is successful and show_utterances is enabled. |


**Response Body Example**

The response body is returned in **JSON format** and contains the recognition result.

```JSON
{
    "audio_info": {
        "duration": 2927
    },
    "result": {
        "additions": {
            "duration": "2927"
        },
        "text": "To be or not to be, that is the question.",
        "utterances": [
            {
                "additions": {
                    "channel_id": "1",
                    "speaker": "1"
                },
                "end_time": 2430,
                "start_time": 80,
                "text": "To be or not to be, that is the question.",
                "words": [
                    {
                        "confidence": 0,
                        "end_time": 350,
                        "start_time": 80,
                        "text": "To"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 550,
                        "start_time": 350,
                        "text": "be"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 830,
                        "start_time": 630,
                        "text": "or"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 1030,
                        "start_time": 830,
                        "text": "not"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 1190,
                        "start_time": 1030,
                        "text": "to"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 1390,
                        "start_time": 1190,
                        "text": "be"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 1830,
                        "start_time": 1630,
                        "text": "that"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 1990,
                        "start_time": 1830,
                        "text": "is"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 2150,
                        "start_time": 1990,
                        "text": "the"
                    },
                    {
                        "confidence": 0,
                        "end_time": -1,
                        "start_time": -1,
                        "text": " "
                    },
                    {
                        "confidence": 0,
                        "end_time": 2430,
                        "start_time": 2150,
                        "text": "question"
                    }
                ]
            }
        ]
    }
}
```


<span id="RD4FOp4x"></span>
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


<span id="ZP4kdveL"></span>
# Demo


<Tabs>
<Tab zoneid="bX2jTKTlpB" title="Python Example">
<TabTitle>Python Example</TabTitle>

<span id="QpzZPA1s"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.


<span id="3g3qmIMm"></span>
## Python env


* Python：Version 3.9 and above.

* Pip：Version 25.1.1 and above. You can use the following command to install it.


```Bash
python3 -m pip install --upgrade pip
```


<span id="YHDRAhvG"></span>
## Download code example 

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_63d8188c90471c5d902c76f78903454d.zip" name="Byteplus_ASR_AUC_http_python.zip">Byteplus_ASR_AUC_http_python.zip</Attachment>


<span id="IbaEerBu"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_ASR_AUC_http_python
tar xvzf Byteplus_ASR_AUC_http_python.zip -C ./Byteplus_ASR_AUC_http_python
cd Byteplus_ASR_AUC_http_python
cd auc_python
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
pip install requests
```


<span id="PmOS0hU1"></span>
## Invoke

> At the end of the python scirpt `auc_http_demo.py`:


> * `<appid>`Replace with your APP ID.

> * `<token>`Replace with your Access Token.

> * `<file_url>` Replace with your online audio recording url, it's recommended to use [Byteplus TOS service](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos). 


```Bash
python3 auc_http_demo.py
```





</Tab>
<Tab zoneid="pCYGtNRYe5" title="Go Example">
<TabTitle>Go Example</TabTitle>

<span id="U8dnTJYc"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

* Detailed information on environment setup is available in the README.md file located in the sample package.


<span id="UQW6mOK9"></span>
### Download code example 

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4e980e6fb839fd7048f016aca092990f.zip" name="Byteplus_ASR_AUC_http_go.zip">Byteplus_ASR_AUC_http_go.zip</Attachment>


<span id="krQoigg6"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_ASR_AUC_http_go
tar xvzf Byteplus_ASR_AUC_http_go.zip -C ./Byteplus_ASR_AUC_http_go
cd Byteplus_ASR_AUC_http_go
cd auc
go mod tidy
```


<span id="Q7IWzAED"></span>
### Invoke 

> In the config.toml file:


> * `<appid>`Replace with your APP ID.

> * `<access_token>`Replace with your Access Token.


```Bash
go run main.go -fileurl="https://example.com/audio.wav"
```





</Tab>
<Tab zoneid="cz7uCPsP9j" title="Java Example">
<TabTitle>Java Example</TabTitle>

<span id="dgQameWl"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

* Detailed information on environment setup is available in the README.md file located in the sample package.


<span id="wOrPRhAx"></span>
### Download code example 

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_35696b6301222e8a109e195308ace5e8.zip" name="Byteplus_ASR_AUC_http_java.zip">Byteplus_ASR_AUC_http_java.zip</Attachment>


<span id="vVDkGtSF"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_ASR_AUC_http_java
tar xvzf Byteplus_ASR_AUC_http_java.zip -C ./Byteplus_ASR_AUC_http_java
cd Byteplus_ASR_AUC_http_java
cd auc
mvn clean install
```


<span id="2AHrdt7f"></span>
### Invoke 

> In the mvn command:


> * `<YOUR_APP_KEY>`Replace with your APP ID.

> * `<YOUR_ACCESS_KEY>`Replace with your Access Token.

> * `<AUDIO_FILE_URL>` Replace with your audit URL.


```Bash
mvn exec:java -Dexec.mainClass="com.example.auc.AucWebSocketDemo" -Dexec.args="<YOUR_APP_KEY> <YOUR_ACCESS_KEY> <AUDIO_FILE_URL>"
```





</Tab>
</Tabs>
