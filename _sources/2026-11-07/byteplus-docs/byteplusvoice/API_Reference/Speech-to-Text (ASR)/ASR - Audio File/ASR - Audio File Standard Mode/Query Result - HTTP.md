---
title: "Query Result - HTTP"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilequeryresult"
---

Queries the transcription results from the Standard Audio File Transcription API using the "`Task ID`".

&nbsp;

<span data-label="purple">POST</span> https://voice.ap\-southeast\-1.bytepluses.com/api/v3/auc/bigmodel/query

&nbsp;


<span id="U2dCXzkM"></span>
### Request Headers


**X\-Api\-Key ** `string` <span data-api-tag="require|g9zFYw">必选</span>

API Key can be retrieved from [Speech Console > API Key ](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default) 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported, check <a href="https://docs.byteplus.com/en/docs/byteplusvoice/legacyconsoleauth?lang=en">Legacy Console Authentication Reference</a> for details.</div>




**X\-Api\-Resource\-Id ** `string` <span data-api-tag="require|g9zFYw">必选</span>

Represents the resource information ID for calling the service：


* `volc.seedasr.auc`：Seed ASR 2.0 model

* `volc.bigasr.auc`：Seed ASR 1.0 model



**X\-Api\-Request\-Id ** `string` <span data-api-tag="require|g9zFYw">必选</span>

The X\-Api\-Request\-Id request header **must use the same** UUID as the one provided in the Submit API request. It can also referred to as the "`Task ID`".




<span id="12GqAfW0"></span>
### Request Body 

The body is an empty json:

```JSON
{}
```






<span id="WtD1SAXn"></span>
### Response Headers


**X\-Tt\-Logid ** `string`

The logid returned by the server. It is recommended that users obtain and print it to facilitate problem location.



**X\-Api\-Status\-Code ** `string`

The status code returned by the server after submitting the task. For specific error codes, refer to the following error code list.



**X\-Api\-Message ** `string`

The information returned by the server after submitting the task. OK indicates success, and others indicate failure.




<span id="WtD1SAXn"></span>
### Response Body


**audio_info ** `list`

Audio information


**duration ** `int`

Audio duration in milliseconds.




**result** `list`

Transcription result


**additions ** `object`

Additional information about the transcription result. 



**text ** `string`

Complete transcription of the audio.



**utterances ** `list`

List of segmented utterances.

&nbsp;


**additions ** `list`

Additional information about the utterance, such as the channel and speaker IDs.



**text ** `string`

Transcription of the utterance.



**start_time ** `int`

Start time of the utterance in milliseconds.



**end_time ** `int`

End time of the utterance in milliseconds.



**words ** `list`

Word\-level recognition results with timestamps.


**Confidence ** `int`

Confidence score of the recognized word. This field is currently reserved and is not populated by the API.



**text ** `string`

Recognized word or character.



**start_time ** `int`

Start time of the word in milliseconds.



**end_time ** `int`

End time of the word in milliseconds.
