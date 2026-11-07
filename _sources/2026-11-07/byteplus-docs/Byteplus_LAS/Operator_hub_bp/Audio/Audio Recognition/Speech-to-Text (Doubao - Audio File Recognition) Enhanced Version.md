---
title: "Speech-to-Text (Doubao - Audio File Recognition) Enhanced Version"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/las_asr_pro"
---

<span id="0d35e679"></span>
# **Operator introduction**

<span id="f50ce8e4"></span>
## Description

The LAS speech\-to\-text (ByteDance\-audio file recognition) enhanced operator is based on the ByteDance large audio file recognition model and can transcribe speech from input audio or video files into text output. Supports multiple audio and video formats, multiple languages, audio noise reduction, and large file processing. Suitable for content quality inspection and review, audio and video subtitle generation, speech search, classroom content analysis, and more.

<span id="62d75f31"></span>
## Limitations


* Currently, only a single audio file can be processed at a time.

* For languages beyond the 13 supported by ByteDance speech, only recording transcription capability is available. Automatic punctuation, semantic smoothing, speaker identification, number normalization (ITN), hotword correction, multimodal visual recognition, and other features are not currently supported.

* The currently supported audio formats are raw, wav, mp3, and ogg.

* The system currently provides full capability support only for the following target languages:

   * English (en), Japanese (ja), Indonesian (id), Spanish (es), Portuguese (pt), German (de), French (fr), Korean (ko), Filipino (fil), Malay (ms), Thai (th), Arabic (ar).

   * If the target language is not listed above, only basic transcription functionality is supported. Advanced features such as speaker separation and emotion recognition are not currently available.


<span id="5690619d"></span>
## Key features


* Multi\-format audio and video input recognition:

   * In addition to audio, video file input is now supported. The LAS operator can automatically extract the audio track from video files for recognition.

   * In addition to raw, wav, mp3, and ogg, the operator now supports container formats such as mp4, mov, mkv, and flac.

   * The LAS operator imposes no file size or duration limits on input audio or video files.

   * In addition to public HTTPS URL access, TOS internal network path access is also supported (tos://bucket\-name/path\-name/file\-name).

* Enhanced audio preprocessing to improve model performance:

   * The built\-in audio noise reduction module effectively reduces the impact of background noise on recognition, improving the accuracy of audio file transcription.

* Multilingual support:

   * Languages can be automatically detected or specified by the user for recognition.

   * Expanded language recognition to 99 languages, meeting the needs of audio data processing across multiple languages and regions.


<span id="85736531"></span>
## Application scenarios


* Content review and quality inspection: Transcribe recordings into text, analyze the text using quality inspection rules to promptly detect and take action on violations, or monitor and analyze content to uncover potential business opportunities.

* Audio and video subtitles: Supports automatic transcription of speech and lyrics in audio or video to text, enabling one\-click generation of subtitles corresponding to the audio and video. Applicable to various scenarios such as video editing, video viewing, and video conferencing.

* Classroom content analysis: Transcribe classroom recordings to restore classroom scenarios through text, analyze teaching content, and improve teaching quality.

* Meeting and interview transcription: Asynchronously transcribe meeting and interview audio to text, automatically segment and recognize speech parts to reduce costs and improve efficiency; automatic segmentation also effectively enhances the efficiency of meeting content recording.


<span id="bdaf2dea"></span>
# Rest API invocation

<span id="bd2c8749"></span>
## API usage instructions


* The API for this operator is an asynchronous task interface. You need to submit a task through the `Submit` interface to obtain the task's `task_id`, then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After submitting a task, the `task_id` is valid for 3 days. After 3 days, you will not be able to use this `task_id` to retrieve the operator's processing result.


<span id="85eccde2"></span>
## Submit (submit task)

<span id="3ba57910"></span>
### Interface description

Submit the audio link and obtain the task ID assigned by the server.

<span id="b88cc7fe"></span>
### Request parameters

```mixin-react
const properties = ({
  "columns": [
    { "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
    { "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
    { "title": "Required", "dataIndex": "column_2", "key": "column_2", "width": 80 },
    { "title": "Example value", "dataIndex": "column_3", "key": "column_3", "width": 150 },
    { "title": "Description", "dataIndex": "column_4", "key": "column_4" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "operator_id",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "las_asr_pro",
      "column_4": "Operator ID"
    },
    {
      "key": "2",
      "column_0": "operator_version",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "v1",
      "column_4": "Operator version"
    },
    {
      "key": "3",
      "column_0": "data",
      "column_1": "SpeechRecognition",
      "column_2": "Yes",
      "column_3": "",
      "column_4": "Request data",
      "children": [
        {
          "key": "3-1",
          "column_0": "user",
          "column_1": "UserConfig",
          "column_2": "No",
          "column_3": "",
          "column_4": "User-related configuration",
          "children": [
            {
              "key": "3-1-1",
              "column_0": "uid",
              "column_1": "string",
              "column_2": "No",
              "column_3": "",
              "column_4": "User identifier; it is recommended to use IMEI or MAC."
            }
          ]
        },
        {
          "key": "3-2",
          "column_0": "audio",
          "column_1": "Audio",
          "column_2": "Yes",
          "column_3": "",
          "column_4": "Audio-related configuration",
          "children": [
            {
              "key": "3-2-1",
              "column_0": "url",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "",
              "column_4": "Audio link"
            },
            {
              "key": "3-2-2",
              "column_0": "language",
              "column_1": "string",
              "column_2": "No",
              "column_3": "en-US",
              "column_4": <div>When this key is empty, the model supports recognition of<b>Chinese and English, Shanghainese, Minnan, Sichuanese, Shaanxi, and Cantonese</b>.<br/>When set to the specific keys below, it can recognize the specified language.<br/>English: en-US<br/>Japanese: ja-JP<br/>Indonesian: id-ID<br/>Spanish: es-MX<br/>Portuguese: pt-BR<br/>German: de-DE<br/>French: fr-FR<br/>Korean: ko-KR<br/>Filipino: fil-PH<br/>Malay: ms-MY<br/>Thai: th-TH<br/>Arabic: ar-SA</div>
            },
            {
              "key": "3-2-3",
              "column_0": "format",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "mp3",
              "column_4": "Audio container format. Currently supports raw/wav/mp3/ogg formats."
            },
            {
              "key": "3-2-4",
              "column_0": "codec",
              "column_1": "string",
              "column_2": "Optional",
              "column_3": "raw",
              "column_4": "Audio encoding format. Currently supports raw / opus. Default is raw (pcm)."
            },
            {
              "key": "3-2-5",
              "column_0": "rate",
              "column_1": "integer",
              "column_2": "Optional",
              "column_3": "",
              "column_4": "Audio sampling rate. Default is 16000."
            },
            {
              "key": "3-2-6",
              "column_0": "bits",
              "column_1": "integer",
              "column_2": "Optional",
              "column_3": "",
              "column_4": "Audio sample bit depth. Default is 16. Currently only 16 bits are supported."
            },
            {
              "key": "3-2-7",
              "column_0": "channel",
              "column_1": "integer",
              "column_2": "Optional",
              "column_3": "",
              "column_4": "Number of audio channels: 1 (mono) / 2 (stereo). Default is 1."
            }
          ]
        },
        {
          "key": "3-3",
          "column_0": "request",
          "column_1": "RequestConfig",
          "column_2": "Yes",
          "column_3": "",
          "column_4": "Request-related configuration.",
          "children": [
            {
              "key": "3-3-1",
              "column_0": "model_name",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "bigmodel",
              "column_4": "Model name. Currently only 'bigmodel' is available."
            },
            {
              "key": "3-3-2",
              "column_0": "enable_itn",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "true",
              "column_4": <div>Default is true.<br/>Text normalization (ITN) is part of the post-processing pipeline for automatic speech recognition (ASR). The task of ITN is to convert the raw speech output of the ASR model into written form to improve the readability of the text.<br/>For example, "一九七零年"-&gt;"1970年" and "一百二十三美元"-&gt;"$123".</div>
            },
            {
              "key": "3-3-3",
              "column_0": "enable_punc",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "false",
              "column_4": "Default is false. Enables punctuation."
            },
            {
              "key": "3-3-4",
              "column_0": "enable_ddc",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "false",
              "column_4": <div>Default is false.<br/><b>Semantic smoothing</b> is a technique designed to improve the readability and fluency of the text results from automatic speech recognition (ASR). This technique makes the text easier to read and understand by removing or modifying disfluent parts in the ASR results, such as filler words, interjections, semantic repetitions, and so on.</div>
            },
            {
              "key": "3-3-5",
              "column_0": "enable_speaker_info",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "false",
              "column_4": <div>Default is false. When enabled, speaker information can be returned. Works best for up to 10 speakers.<br/>(If there are significant changes in volume or distance in the audio, differentiation cannot be guaranteed.)</div>
            },
            {
              "key": "3-3-6",
              "column_0": "enable_channel_split",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "false",
              "column_4": <div>Default is false.<br/>If set to true, channel_id will be used in the returned results: 1 for left channel, 2 for right channel.</div>
            },
            {
              "key": "3-3-7",
              "column_0": "show_utterances",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "false",
              "column_4": "Outputs information on speech pauses, sentence segmentation, and word segmentation."
            },
            {
              "key": "3-3-8",
              "column_0": "vad_segment",
              "column_1": "boolean",
              "column_2": "Optional",
              "column_3": "false",
              "column_4": <div>Default is false. Semantic segmentation is used by default.<br/>When enabling dual-channel recognition, vad segmentation is usually required. This parameter can be enabled simultaneously.</div>
            },
            {
              "key": "3-3-9",
              "column_0": "end_window_size",
              "column_1": "integer",
              "column_2": "Optional",
              "column_3": "800",
              "column_4": <div>Range: 300 - 5000 ms. It is recommended to set 800 ms or 1000 ms. For more sensitive scenarios, configure 500 ms or less. (If the value is set too low, it will result in overly fragmented sentences; if set too high, it will make it difficult to separate spoken content. It is recommended to configure this value as needed based on your specific scenario.)<br/>Configure this value to segment sentences based on silence duration, without using semantic segmentation.</div>
            },
            {
              "key": "3-3-10",
              "column_0": "sensitive_words_filter",
              "column_1": "string",
              "column_2": "No",
              "column_3": "",
              "column_4": <div>Sensitive word filtering functionality, supports enabling or disabling, and allows custom sensitive words. This parameter can be used to: No processing (default, that is, display the original text), filter, or replace with *.  Example: system_reserved_filter // Whether to use system sensitive words, will be replaced with * (default system sensitive words mainly include some restricted vocabulary) filter_with_empty // Sensitive words to be replaced with an empty string filter_with_signed // Sensitive words to be replaced with *<br/><pre style={{background: "#eee", borderRadius: "4px"}}><code>"sensitive_words_filter":&#123;"system_reserved_filter":true,"filter_with_empty":&#91;"敏感词"&#93;,"filter_with_signed":&#91;"敏感词"&#93;&#125;</code></pre></div>
            },
            {
              "key": "3-3-11",
              "column_0": "enable_denoise",
              "column_1": "boolean",
              "column_2": "No",
              "column_3": "",
              "column_4": "Whether to enable noise reduction"
            },
            {
              "key": "3-3-12",
              "column_0": "enable_multi_language",
              "column_1": "boolean",
              "column_2": "No",
              "column_3": "",
              "column_4": <div>Default is true<br/>Whether to enable language identification and multi-language support</div>
            },
            {
              "key": "3-3-13",
              "column_0": "corpus",
              "column_1": "Corpus",
              "column_2": "No",
              "column_3": "",
              "column_4": "Corpora/intervention words, etc.",
              "children": [
                {
                  "key": "3-3-13-1",
                  "column_0": "context",
                  "column_1": "string",
                  "column_2": "No",
                  "column_3": "",
                  "column_4": <div>Direct hotword transmission, supports up to 5000 hotwords "context":"&#123;"hotwords":&#91;&#123;"word":"Hotword No. 1"&#125;, &#123;"word":"Hotword No. 2"&#125;&#93;&#125;" Context is limited to 800 tokens and within 20 rounds (inclusive). If exceeded, it will be truncated from newest to oldest based on chronological order, prioritizing retention of updated conversations. The context_data field is arranged from newest to oldest. The following is an example after deserialization; input needs to be serialized as a jsonstring (escape quotation marks).<br/><pre style={{background: "#eee", borderRadius: "4px"}}><code>Context: You can include conversation history, bot information for the chat, personalized information, business scenario information, and more, such as:<br/>a. Conversation history: Pass in the recent rounds of conversation history<br/>b. Bot information for the chat: For example, "I am chatting with Lin Daiyu", "I am using Assistant A to talk with my phone"<br/>c. Personalized information: "I am currently in Haidian District, Beijing", "I have a Sichuan accent", "I like music"<br/>d. Business scenario information: "This is a recording of Ping An's marketing staff interviewing external customers, which may involve..."<br/>&#123;<br/>    "context_type": "dialog_ctx",<br/>    "context_data":&#91;<br/>        &#123;"text": "text1"&#125;,<br/>        &#123;"text": "text2"&#125;,<br/>        &#123;"text": "text3"&#125;,<br/>        &#123;"text": "text4"&#125;,<br/>        ...<br/>    &#93;<br/>&#125;</code></pre></div>
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="57d1e08f"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
{ "title": "Example value", "dataIndex": "column_2", "key": "column_2", "width": 150 },
{ "title": "Description", "dataIndex": "column_3", "key": "column_3" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "Metadata",
      "column_2": "",
"column_3": "Request metadata",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_2": "",
"column_3": "Task ID in asynchronous mode."
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_2": "",
"column_3": "Task status in asynchronous mode."
        },
        {
          "key": "1-3",
          "column_0": "business_code",
          "column_1": "string",
          "column_2": "",
"column_3": "Business code"
        },
        {
          "key": "1-4",
          "column_0": "error_msg",
          "column_1": "string",
          "column_2": "",
"column_3": "If there is an exception, detailed exception information will be returned."
        },
        {
          "key": "1-5",
          "column_0": "request_id",
          "column_1": "string",
          "column_2": "",
"column_3": "Request ID"
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="d9471d5b"></span>
### Example

<span id="d6ddd1cf"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: $LAS_API_KEY" \
--data '
{
    "operator_id": "las_asr_pro",
    "operator_version": "v1",
    "data": {
        "resource": "bigasr",
        "audio": {
            "url": "https://las-ai-cn-beijing-online.tos-cn-beijing.volces.com/operator_cards_serving/public/online/las_asr/badaling.wav",
            "format": "wav"
        },
        "request": {
            "model_name": "bigmodel"
        }
    }
}'
```


<span id="5146cafd"></span>
#### Response example

```JSON
{
    "metadata": {
        "task_id": "xxxxx123ef24ea40546c",
        "task_status": "PENDING",
        "business_code": "0",
        "error_msg": "",
        "request_id": "494022a8a0fc3eadb758cf8b0e8b20ef"
    }
}
```


<span id="a2e8248e"></span>
## Poll (query results)

<span id="afe202be"></span>
### Interface description

Query the transcription result of the recording using the task ID.

<span id="9e03f312"></span>
### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_asr_pro |Operator ID |
|operator_version |string |Yes |v1 |Operator version |
|task_id |string |Yes | |Asynchronous task ID |


<span id="99c9b9f0"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
{ "title": "Example value", "dataIndex": "column_2", "key": "column_2", "width": 150 },
{ "title": "Description", "dataIndex": "column_3", "key": "column_3" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "Metadata",
      "column_2": "",
"column_3": "The metadata of the request; the ID of the asynchronous task is located under the task_id field within it.",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_2": "",
"column_3": "Task ID in asynchronous mode."
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_2": "",
"column_3": "The task status in asynchronous mode."
        },
        {
          "key": 1-3,
          "children": [],
          "column_0": "submit_time",
          "column_1": "string",
          "column_2": "2026-07-21T16:04:06+08:00",
"column_3": "Task submission time, in ISO 8601 timestamp format."
        },
        {
          "key": 1-4,
          "children": [],
          "column_0": "end_time",
          "column_1": "string",
          "column_2": "2026-07-21T16:04:06+08:00",
"column_3": "Task end time, in ISO 8601 timestamp format."
        },
        {
          "key": "1-5",
          "column_0": "business_code",
          "column_1": "string",
          "column_2": "",
"column_3": < div> Business code < br/>- PENDING, task submitted and queued< br/>- RUNNING, running< br/>- COMPLETED, completed< br/>- FAILED, failed< br/>- TIMEOUT, timed out</ div>
        },
        {
          "key": "1-6",
          "column_0": "error_msg",
          "column_1": "string",
          "column_2": "",
"column_3": "If an exception occurs, detailed exception information will be returned."
        },
        {
          "key": "1-7",
          "column_0": "request_id",
          "column_1": "string",
          "column_2": "",
"column_3": "request ID"
        }
      ]
    },
    {
      "key": "2",
      "column_0": "data",
      "column_1": "AudioResponse",
      "column_2": "",
"column_3": "The returned audio recognition result.",
      "children": [
        {
          "key": "2-1",
          "column_0": "audio_info",
          "column_1": "AudioInfo",
          "column_2": "",
"column_3": "audio information",
          "children": [
            {
              "key": "2-1-1",
              "column_0": "duration",
              "column_1": "integer",
              "column_2": "",
"column_3": "audio duration, in milliseconds"
            }
          ]
        },
        {
          "key": "2-2",
          "column_0": "result",
          "column_1": "AudioResult",
          "column_2": "",
"column_3": "audio recognition result",
          "children": [
            {
              "key": "2-2-1",
              "column_0": "text",
              "column_1": "string",
              "column_2": "",
"column_3": "recognized text content"
            },
            {
              "key": "2-2-2",
              "column_0": "utterances",
              "column_1": "list of Utterance",
              "column_2": "",
"column_3": "speech pause, sentence segmentation, and word segmentation information",
              "children": [
                {
                  "key": "2-2-2-1",
                  "column_0": "additions",
                  "column_1": "Additions",
                  "column_2": "",
                  "column_3": "Additional information, such as speaker and others",
                  "children": [
                    {
                      "key": "2-2-2-1-1",
                      "column_0": "speaker",
                      "column_1": "string",
                      "column_2": "",
"column_3": "Speaker"
                    },
                    {
                      "key": "2-2-2-1-2",
                      "column_0": "channel_id",
                      "column_1": "string",
                      "column_2": "",
                      "column_3": "channel number"
                    }
                  ]
                },
                {
                  "key": "2-2-2-2",
                  "column_0": "confidence",
                  "column_1": "integer",
                  "column_2": "",
                  "column_3": "confidence level"
                },
                {
                  "key": "2-2-2-3",
                  "column_0": "end_time",
                  "column_1": "integer",
                  "column_2": "",
                  "column_3": "End time"
                },
                {
                  "key": "2-2-2-4",
                  "column_0": "start_time",
                  "column_1": "integer",
                  "column_2": "",
                  "column_3": "Start time"
                },
                {
                  "key": "2-2-2-5",
                  "column_0": "text",
                  "column_1": "string",
                  "column_2": "",
"column_3": "The content of this section"
                },
                {
                  "key": "2-2-2-6",
                  "column_0": "words",
                  "column_1": "list of Word",
                  "column_2": "",
                  "column_3": "word-related information",
                  "children": [
                    {
                      "key": "2-2-2-6-1",
                      "column_0": "confidence",
                      "column_1": "integer",
                      "column_2": "",
                      "column_3": "Confidence"
                    },
                    {
                      "key": "2-2-2-6-2",
                      "column_0": "blank_duration",
                      "column_1": "integer",
                      "column_2": "",
                      "column_3": "blank duration"
                    },
                    {
                      "key": "2-2-2-6-3",
                      "column_0": "end_time",
                      "column_1": "integer",
                      "column_2": "",
                      "column_3": "word end time"
                    },
                    {
                      "key": "2-2-2-6-4",
                      "column_0": "start_time",
                      "column_1": "integer",
                      "column_2": "",
                      "column_3": "word start time"
                    },
                    {
                      "key": "2-2-2-6-5",
                      "column_0": "text",
                      "column_1": "string",
                      "column_2": "",
"column_3": "Word"
                    }
                  ]
                }
              ]
            },
            {
              "key": "2-2-3",
              "column_0": "additions",
              "column_1": "RequestAdditions",
              "column_2": "",
              "column_3": "additional information",
              "children": [
                {
                  "key": "2-2-3-1",
                  "column_0": "duration",
                  "column_1": "string",
                  "column_2": "",
                  "column_3": "audio duration"
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="b770e28a"></span>
### Example

<span id="ad1b45e7"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: $LAS_API_KEY" \
--data '
{
    "operator_id": "las_asr_pro",
    "operator_version": "v1",
    "task_id": "xxxxx123ef24ea40546c"
}'
```


<span id="4d0d4a34"></span>
#### Response example

```JSON
{
    "metadata": {
        "task_id": "xxxxx123ef24ea40546c",
        "task_status": "COMPLETED",
        "submit_time": "2026-07-21T16:04:06+08:00",
        "end_time": "2026-07-21T16:04:06+08:00",
        "business_code": "0",
        "error_msg": "",
        "request_id": "d204c21f5c7c8f8cfeb85d211b9c20ac"
    },
    "data": {
        "audio_info": {
            "duration": 3575
        },
        "result": {
            "additions": {
                "duration": "3575"
            },
            "text": "参观达*长城。",
            "utterances": [
                {
                    "additions": {
                        "channel_id": "1"
                    },
                    "end_time": 2320,
                    "start_time": 640,
                    "text": "参观达*长城。",
                    "words": [
                        {
                            "confidence": 0,
                            "end_time": 920,
                            "start_time": 640,
                            "text": "参"
                        },
                        {
                            "confidence": 0,
                            "end_time": 1120,
                            "start_time": 920,
                            "text": "观"
                        },
                        {
                            "confidence": 0,
                            "end_time": 1480,
                            "start_time": 1440,
                            "text": "达"
                        },
                        {
                            "confidence": 0,
                            "end_time": 1720,
                            "start_time": 1680,
                            "text": "*"
                        },
                        {
                            "confidence": 0,
                            "end_time": 2080,
                            "start_time": 1880,
                            "text": "长"
                        },
                        {
                            "confidence": 0,
                            "end_time": 2320,
                            "start_time": 2080,
                            "text": "城"
                        }
                    ]
                }
            ]
        }
    }
}
```
