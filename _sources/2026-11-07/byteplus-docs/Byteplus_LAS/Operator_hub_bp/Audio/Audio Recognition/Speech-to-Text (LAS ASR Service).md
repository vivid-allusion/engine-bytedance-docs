---
title: "Speech-to-Text (LAS ASR Service)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/las_asr"
---

<span id="d4caf38f"></span>
# **Operator introduction**

<span id="d5056cce"></span>
## Description

**Speech recognition module \- a recording transcription solution based on the LAS ASR service**

<span id="3bd3abc9"></span>
## **Limitations**


* Currently, only a single audio file is supported for input

* Speech recognition is an asynchronous interface. You need to first create a speech recognition task, then query the speech recognition result using the task ID

* The currently supported audio formats are raw, wav, mp3, and ogg.


<span id="c602b991"></span>
## Key features


* Integrate the BytePlus LAS ASR interface

* Supports automatic sentence segmentation, number normalization, and speaker or channel separation (optional)

* Processes multiple audio files concurrently and provides both structured JSON and readable text outputs

* Suitable for transcribing recording files up to 2 hours in length, supporting advanced features such as punctuation completion, intelligent sentence segmentation, and speaker separation.


<span id="0a37462e"></span>
# Rest API invocation

<span id="3c4273e1"></span>
## API usage instructions


* This operator's API is an asynchronous task interface. You need to submit a task through the `Submit` interface to obtain a `task_id`, then use the `Poll` interface to check the status of the corresponding task (`task_id`) and obtain the processing result.

* Caution: After a task is submitted, the `task_id` is valid for one day. After one day, you will no longer be able to use this `task_id` to obtain the processing result.


<span id="d4896613"></span>
## Submit

<span id="1791b648"></span>
### Interface description

Submit an ASR recognition task.

<span id="659e5d64"></span>
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
      "column_3": "las_asr",
"column_4": "Operator ID"
    },
    {
      "key": "2",
      "column_0": "operator_version",
      "column_1": "string",
"column_2": "Yes",
      "column_3": "v2",
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
"column_4": "User identifier. It is recommended to use IMEI or MAC."
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
"column_4": "Audio URL"
            },
            {
              "key": "3-2-2",
              "column_0": "language",
              "column_1": "string",
"column_2": "No",
              "column_3": "en-US",
"column_4": < div> When this key is empty, the model supports< b> Chinese and English, Shanghainese, Hokkien (Min Chinese), Sichuanese, Shaanxi dialect, and Cantonese</ b> recognition. When set to the specific keys below, it can recognize the specified language.  English: en-US, Japanese: ja-JP, Indonesian: id-ID, Spanish: es-MX, Portuguese: pt-BR, German: de-DE, French: fr-FR, Korean: ko-KR, Filipino: fil-PH, Malay: ms-MY, Thai: th-TH, and Arabic: ar-SA</ div>
            },
            {
              "key": "3-2-3",
              "column_0": "format",
              "column_1": "string",
"column_2": "Yes",
              "column_3": "mp3",
"column_4": "Audio container format. Currently supports raw/wav/mp3/ogg formats"
            },
            {
              "key": "3-2-4",
              "column_0": "codec",
              "column_1": "string",
"column_2": "No",
              "column_3": "raw",
"column_4": "Audio encoding format. Currently supports raw / opus, default is raw (pcm)"
            },
            {
              "key": "3-2-5",
              "column_0": "rate",
              "column_1": "integer",
"column_2": "No",
              "column_3": "",
"column_4": "Audio sample rate. Default is 16000"
            },
            {
              "key": "3-2-6",
              "column_0": "bits",
              "column_1": "integer",
"column_2": "No",
              "column_3": "",
"column_4": "Audio sample bit depth. Default is 16. Currently only 16 bits are supported"
            },
            {
              "key": "3-2-7",
              "column_0": "channel",
              "column_1": "integer",
"column_2": "No",
              "column_3": "",
"column_4": "Number of audio channels, 1 (mono) / 2 (stereo), default is 1."
            }
          ]
        },
        {
          "key": "3-3",
          "column_0": "request",
          "column_1": "RequestConfig",
"column_2": "Required",
          "column_3": "",
"column_4": "Request-related configuration",
          "children": [
            {
              "key": "3-3-1",
              "column_0": "model_name",
              "column_1": "string",
"column_2": "Required",
              "column_3": "bigmodel",
"column_4": "Model name; currently only 'bigmodel' is supported."
            },
            {
              "key": "3-3-2",
              "column_0": "enable_itn",
              "column_1": "boolean",
"column_2": "Optional",
              "column_3": "true",
"column_4": < div> Default is true. < br/> Text normalization (ITN) is part of the automatic speech recognition (ASR) post-processing pipeline. The task of ITN is to convert the raw speech output of the ASR model into written form to improve text readability. < br/> For example, "一九七零年"-&gt;"1970年" and "一百二十三美元"-&gt;"$123". </div>
            },
            {
              "key": "3-3-3",
              "column_0": "enable_punc",
              "column_1": "boolean",
"column_2": "Optional",
              "column_3": "false",
"column_4": "Default is false."
            },
            {
              "key": "3-3-4",
              "column_0": "enable_ddc",
              "column_1": "boolean",
"column_2": "Optional",
              "column_3": "false",
"column_4": < div> Default is false. < br/>< b> Semantic smoothing</ b> is a technique designed to improve the readability and fluency of automatic speech recognition (ASR) results. This technique makes the text easier to read and understand by removing or modifying disfluent parts in ASR results, such as filler words, interjections, semantic repetitions, and so on. </div>
            },
            {
              "key": "3-3-5",
              "column_0": "enable_channel_split",
              "column_1": "boolean",
"column_2": "Optional",
              "column_3": "false",
"column_4": < div> Default is false. < br/> If set to "True", channel_id tags will be used in the returned results: 1 for the left channel, 2 for the right channel. Default is "False". </div>
            },
            {
              "key": "3-3-6",
              "column_0": "show_utterances",
              "column_1": "boolean",
"column_2": "Optional",
              "column_3": "false",
"column_4": "Outputs information on speech pauses, sentence segmentation, and word segmentation."
            },
            {
              "key": "3-3-7",
              "column_0": "vad_segment",
              "column_1": "boolean",
"column_2": "Optional",
              "column_3": "false",
"column_4": < div> Default is false; semantic segmentation is used by default. < br/> When dual-channel recognition is enabled, VAD segmentation is usually required; this parameter can be enabled at the same time</ div>
            },
            {
              "key": "3-3-8",
              "column_0": "end_window_size",
              "column_1": "integer",
"column_2": "Optional",
              "column_3": "800",
"column_4": < div> Range: 300 - 5000 ms. It is recommended to set 800 ms or 1000 ms; for more sensitive scenarios, 500 ms or less can be configured. (If the value is set too small, sentence segmentation will be too fragmented; if set too large, it will be difficult to separate spoken content. It is recommended to configure as needed for your scenario.)< br/> When this value is configured, semantic segmentation is not used; segmentation is based on silence duration. </div>
            },
            {
              "key": "3-3-9",
              "column_0": "sensitive_words_filter",
              "column_1": "string",
"column_2": "Optional",
              "column_3": "",
"column_4": <div>Sensitive word filtering function; supports enabling or disabling, and custom sensitive words. This parameter can be used for: no processing (default, that is, displaying the original text), filtering, or replacing with *.  Example: system_reserved_filter // Whether to use system sensitive words, which will be replaced with * (the default system sensitive words mainly include some restricted vocabulary) filter_with_empty // Replace sensitive words with empty filter_with_signed // Replace sensitive words with *<br/><pre style={{background: "#eee", borderRadius: "4px"}}><code>"sensitive_words_filter":&#123;"system_reserved_filter":true,"filter_with_empty":&#91;"敏感词"&#93;,"filter_with_signed":&#91;"敏感词"&#93;&#125;</code></pre></div>            },
            {
              "key": "3-3-10",
              "column_0": "corpus",
              "column_1": "Corpus",
"column_2": "Optional",
              "column_3": "",
"column_4": "Corpora/intervention words and more.",
              "children": [
                {
                  "key": "3-3-10-1",
                  "column_0": "context",
                  "column_1": "string",
"column_2": "Optional",
                  "column_3": "",
"column_4": <div>Direct transmission of hotwords, supports up to 5000 hotwords "context":"&#123;"hotwords":&#91;&#123;"word": "Hotword No. 1"&#125;, &#123;"word": "Hotword No. 2"&#125;&#93;&#125;" Context: limited to 800 tokens and within 20 rounds (inclusive). If exceeded, truncation will occur in chronological order from newest to oldest, prioritizing retention of updated conversations. The context_data field is arranged in order from newest to oldest. Below is an example after deserialization. Input needs to be serialized as a jsonstring (escape quotation marks).<br/><pre style={{background: "#eee", borderRadius: "4px"}}><code>Context: You can include conversation history, information about the bot in which the chat takes place, personalized information, business scenario information, and more, for example:<br/>a. Conversation history: Pass in the conversation history from the most recent rounds<br/>b. Information about the bot in which the chat takes place: For example, "I am chatting with Lin Daiyu", "I am using Assistant A to converse with my phone"<br/>c. Personalized information: "I am currently in Haidian District, Beijing", "I have a Sichuan accent", "I like music"<br/>d. Business scenario information: "Currently, this is a recording of an interview by a Ping An Insurance salesperson with an external customer, which may involve..."<br/>&#123;<br/>    "context_type": "dialog_ctx",<br/>    "context_data":&#91;<br/>        &#123;"text": "text1"&#125;,<br/>        &#123;"text": "text2"&#125;,<br/>        &#123;"text": "text3"&#125;,<br/>        &#123;"text": "text4"&#125;,<br/>        ...<br/>    &#93;<br/>&#125;</code></pre></div>
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


<span id="3a5f71d7"></span>
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
"column_3": "If an exception occurs, detailed exception information will be returned."
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


<span id="4343cb78"></span>
### Examples

<span id="67139228"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: $LAS_API_KEY" \
--data '
{
    "operator_id": "las_asr",
    "operator_version": "v2",
    "data": {
        "audio": {
            "url": "https://las-ai-cn-beijing-baseline.tos-cn-beijing.volces.com/operator_cards_serving/public/baseline/las_asr/badaling.wav",
            "format": "mp3"
        },
        "request": {
            "model_name": "bigmodel"
        }
    }
}'
```


<span id="dc788feb"></span>
#### Response example

```JSON
{
    "metadata": {
        "task_id": "xxxxx123ef24ea40546c-las-asr",
        "task_status": "ACCEPTED",
        "business_code": "0",
        "error_msg": "",
        "request_id": "494022a8a0fc3eadb758cf8b0e8b20ef"
    }
}
```


<span id="cefaa140"></span>
## Poll

<span id="eac2568a"></span>
### Interface description

Query the status of an ASR recognition task.

<span id="da5a8413"></span>
### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_asr |Operator ID |
|operator_version |string |Yes |v2 |Operator version |
|task_id |string |Yes | |Asynchronous task ID |


<span id="f1a81b72"></span>
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
"column_3": "Request metadata. The asynchronous task ID is under the task_id field.",
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
"column_3": "Business code"
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
"column_3": "Request ID"
        }
      ]
    },
    {
      "key": "2",
      "column_0": "data",
      "column_1": "AudioResponse",
      "column_2": "",
"column_3": "Returned audio recognition result.",
      "children": [
        {
          "key": "2-1",
          "column_0": "audio_info",
          "column_1": "AudioInfo",
          "column_2": "",
"column_3": "Audio information",
          "children": [
            {
              "key": "2-1-1",
              "column_0": "duration",
              "column_1": "integer",
              "column_2": "",
"column_3": "Audio duration, in milliseconds"
            }
          ]
        },
        {
          "key": "2-2",
          "column_0": "result",
          "column_1": "AudioResult",
          "column_2": "",
"column_3": "Audio recognition result",
          "children": [
            {
              "key": "2-2-1",
              "column_0": "text",
              "column_1": "string",
              "column_2": "",
"column_3": "Recognized text content"
            },
            {
              "key": "2-2-2",
              "column_0": "utterances",
              "column_1": "list of Utterance",
              "column_2": "",
"column_3": "Speech pause, sentence segmentation, and word segmentation information",
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
"column_3": "Channel ID"
                    }
                  ]
                },
                {
                  "key": "2-2-2-2",
                  "column_0": "confidence",
                  "column_1": "integer",
                  "column_2": "",
"column_3": "Confidence"
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
"column_3": "Text content of this part"
                },
                {
                  "key": "2-2-2-6",
                  "column_0": "words",
                  "column_1": "list of Word",
                  "column_2": "",
"column_3": "Word-related information",
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
"column_3": "Blank duration"
                    },
                    {
                      "key": "2-2-2-6-3",
                      "column_0": "end_time",
                      "column_1": "integer",
                      "column_2": "",
"column_3": "Word end time"
                    },
                    {
                      "key": "2-2-2-6-4",
                      "column_0": "start_time",
                      "column_1": "integer",
                      "column_2": "",
"column_3": "Word start time"
                    },
                    {
                      "key": "2-2-2-6-5",
                      "column_0": "text",
                      "column_1": "string",
                      "column_2": "",
"column_3": "Word text"
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
"column_3": "Additional information",
              "children": [
                {
                  "key": "2-2-3-1",
                  "column_0": "duration",
                  "column_1": "string",
                  "column_2": "",
"column_3": "Audio duration"
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


<span id="b72f1645"></span>
### Examples

<span id="23ed65e1"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: $LAS_API_KEY" \
--data '
{
    "operator_id": "las_asr",
    "operator_version": "v2",
    "task_id": "xxxxx123ef24ea40546c-las-asr"
}'
```


<span id="5a5d51db"></span>
#### Response example

```JSON
{
    "metadata": {
        "task_id": "xxxxx123ef24ea40546c-las-asr",
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


<span id="a0a98276"></span>
## Error codes


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameter |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API |
|429 |Server.Busy |Server is Busy, please try again later. |Server busy, rate limiting |
|500 |Server.InternalError |Depends on the specific exception |Business exception |


<span id="00cc255f"></span>
# **Daft invocation**

<span id="c0c7b1a2"></span>
## Operator parameters

<span id="6e75de2f"></span>
### Input


|Input column name |Note |
|---|---|
|audio_urls |Column for storing audio paths |
|audio_metas |Column for storing audio metadata in dictionary format; supports parameters such as language, codec, rate, bits, channel, format, corpus, and similar words |


<span id="c1ed7577"></span>
### Output

<span id="ed4ccde4"></span>
### Parameters

If a parameter does not have a default value, it is required


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|api_key |str | |LAS service API Key. |
|endpoint |str or None | |LAS service API Endpoint. |
|version |str |v1 |LAS service API Version. Default value: "v1". |
|operator_id |str |las_asr |LAS ASR service ID. Default value: "las_asr". |
|resource |str |bigasr |Resource type for ASR. Default value: "bigasr". Optional values: "bigasr", "seedasr". |
|operator_version |str |v1 |LAS ASR service version. Default value: "v1". |
|num_coroutines |int |20 |Maximum number of concurrent audio processing per instance. Default value: 20. |
|max_retries |int |3 |Maximum number of retries for a single API request. Default value: 3. |
|enable_idempotent |bool |False |Used to determine whether to retry data processing. When True, each time will be reprocessed. Default value: False. |
|enable_punc |bool |False |Text punctuation. Converts original speech output to a punctuated form to improve text readability. Default value: False. |
|enable_ddc |bool |False |Semantic smoothing, designed to improve the readability and fluency of automatic speech recognition (ASR) results. This technology removes or modifies disfluent parts in ASR results, such as filler words, interjections, semantic repetitions, and similar words, making the text easier to read and understand. Default value: False. |
|enable_speaker_info |bool |False |Speaker information. When enabled, can return speaker information for up to 10 people with good accuracy. Default value: False. |
|enable_itn |bool |True |Text normalization. Converts original speech output to written form to improve text readability. Default value: True. |
|enable_channel_split |bool |False |Channel splitting. When enabled, channel_id will be used in the returned result: 1 for left channel, 2 for right channel. Default value: False. |
|enable_lid |bool |False |Language identification. Currently supports the following languages: Chinese, English, Shanghainese, Minnan, Sichuanese, Shaanxi dialect, and Cantonese. When enabled, lid_lang will be used in the additions information to return the corresponding language tag. Default value: False. |
|show_speech_rate |bool |False |Speech rate information. When enabled, speech_rate will be used in the additions information for each sentence. Unit: tokens/s. Default value: False. |
|show_volume |bool |False |Volume information. When enabled, volume will be used in the additions information for each sentence. Unit: decibels. Default value: False. |


<span id="fbc21b66"></span>
## Examples

The following code demonstrates how to use Daft to run the operator and convert speech to text.

```Python
from __future__ import annotations

import logging
import os

import daft
from daft import col
from daft.las.functions.audio.audio_asr_las import LasAsrPoller, LasAsrSubmitter
from daft.las.functions.udf import las_udf

def configure_logging():
    logging.basicConfig(
        level=logging.INFO,
        format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
        datefmt="%Y-%m-%d %H:%M:%S.%s".format(),
    )
    logging.getLogger("tracing.span").setLevel(logging.WARNING)
    logging.getLogger("daft_io.stats").setLevel(logging.WARNING)
    logging.getLogger("DaftStatisticsManager").setLevel(logging.WARNING)
    logging.getLogger("DaftFlotillaScheduler").setLevel(logging.WARNING)
    logging.getLogger("DaftFlotillaDispatcher").setLevel(logging.WARNING)

configure_logging()

if __name__ == "__main__":
    # Need to configure the environment variable LAS_API_KEY: LAS_API_KEY is obtained by creating it on the LAS service page
    las_api_key = os.getenv("LAS_API_KEY")
    endpoint = os.getenv("LAS_SERVICE_ENDPOINT", "https://operator.las.cn-beijing.volces.com")
    TOS_INPUT_DIR_URL = os.getenv("TOS_INPUT_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {"audio_path": [os.path.join(f"https://{TOS_INPUT_DIR_URL}", "public/shared_audio_dataset/参观八达岭长城。.wav")]}

    df = daft.from_pydict(samples)
    df = df.with_column(
        "task_id",
        las_udf(
            LasAsrSubmitter,
            construct_args={
                "api_key": las_api_key,
                "max_retries": 10,
                "endpoint": endpoint,
            },
            num_cpus=1,
            concurrency=1,
            batch_size=2,
        )(col("audio_path")),
    )

    df = df.with_column(
        "asr_result",
        las_udf(
            LasAsrPoller,
            construct_args={
                "api_key": las_api_key,
                "endpoint": endpoint,
            },
            num_cpus=1,
            concurrency=1,
            batch_size=2,
        )(col("audio_path"), col("task_id")),
    ).exclude("task_id")

    df = df.with_columns(
        {
            "asr_result_raw": col("asr_result")["asr_result_raw"],
            "asr_result_text": col("asr_result")["asr_result_text"],
            "failed_reason": col("asr_result")["failed_reason"],
        }
    ).exclude("asr_result")

    df.show()
    # ╭────────────────────────────────┬────────────────────────────────┬──────────────────┬───────────────╮
    # │ audio_path                     ┆ asr_result_raw                 ┆ asr_result_text  ┆ failed_reason │
    # │ ---                            ┆ ---                            ┆ ---              ┆ ---           │
    # │ String                         ┆ String                         ┆ String           ┆ String        │
    # ╞════════════════════════════════╪════════════════════════════════╪══════════════════╪═══════════════╡
    # │ https://las-cn-beijing-public… ┆ {"additions": {"duration": "3… ┆ Visit the Badaling Great Wall.     ┆ None          │
    # ╰────────────────────────────────┴────────────────────────────────┴──────────────────┴───────────────╯
```
