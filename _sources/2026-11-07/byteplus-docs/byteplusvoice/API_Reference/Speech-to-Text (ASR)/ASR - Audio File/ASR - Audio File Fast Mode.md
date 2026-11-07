---
title: "ASR - Audio File Fast Mode"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofile-flash"
---

<span id="VEQaTFJX"></span>
## Introduction

This API is designed for **fast audio file recognition**. Powered by the latest large speech model, it delivers higher accuracy and faster response. The interface follows a **single\-request, single\-response** pattern — recognition results are returned directly, with no need for the submit/query polling used by the standard version.


---



<span id="351XT4XH"></span>
## Request

**Request Path:** `https://voice.ap-southeast-1.bytepluses.com/api/v3/auc/bigmodel/recognize/flash`

**Request Method:** `HTTP POST`


**Header**


**X\-Api\-Key** `string` <span data-api-tag="require|uxJNXR">必选</span>

A single API Key generated from the [BytePlus console](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide).



**X\-Api\-Resource\-Id** `string` <span data-api-tag="require|K2Vo5Y">必选</span>

Represents the resource information ID for calling the service.Fixed value:`volc.seedasr.auc_turbo`



**X\-Api\-Request\-Id** `string` <span data-api-tag="require|IPSWGh">必选</span>

Used for the **task ID** of submitting and querying tasks. It is recommended to pass in a randomly generated UUID.



**X\-Api\-Sequence** `string`

Packet sequence number. The fixed value is \-1.




**Body**


**audio**


**url** `string` <span data-api-tag="require|4Zr5ZQ">必选</span>

Publicly accessible HTTP(S) URL of the audio file.

Max duration: 2 hours

Max file size: 100MB

**Note**: For **audio longer than 2 hours**, please use [ASR Audio File](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofile) \*\*\*\*\*\* *API.* 



**data** `string`

Base64\-encoded audio content. Either this or `url` must be provided.



**format** `string`

Audio container format.

Supported values: `raw` / `wav` / `mp3` / `ogg`



**codec** `string`

Audio encoding format.

Supported values: `raw` / `opus`

Default: `raw` (PCM)



**rate** `int`

Audio sample rate (Hz)

Default: `16000`



**bits** `int`

Audio sample bit depth

Default: `16`



**channel** `int`

Number of audio channels

`1`: mono

`2`: stereo

Default: `1`



**language** `string`

Recognition language.

When empty, the model recognizes **Mandarin Chinese, English, Cantonese, Shanghainese, Minnan, Sichuan, and Shaanxi dialect**. When set to one of the keys below, it can recognize below languages.

• English: `en-US`

• Mandarin Chinese: `zh-CN`

• Cantonese: `yue-CN`

• Japanese: `ja-JP`

• Indonesian Bahasa: `id-ID`

• Spanish: `es-MX`

• Portuguese: `pt-BR`

• German: `de-DE`

• French: `fr-FR`

• Korean: `ko-KR`

• Filipino: `fil-PH`

• Malay: `ms-MY`

• Thai: `th-TH`

• Arabic: `ar-SA`

• Italian: `it-IT`

• Bengali: `bn-BD`

• Greek: `el-GR`

• Dutch: `nl-NL`

• Russian: `ru-RU`

• Turkish: `tr-TR`

• Vietnamese: `vi-VN`

• Polish: `pl-PL`

• Romanian: `ro-RO`

• Ukrainian: `uk-UA`

• Azerbaijani: `az-AZ`

• Bulgarian: `bg-BG`

• Czech: `cs-CZ`

• Danish: `da-DK`

• Finnish: `fi-FI`

• Hindi: `hi-IN`

• Hungarian: `hu-HU`

• Kazakh: `kk-KZ`

• Khmer: `km-KH`

• Burmese: `my-MM`

• Norwegian: `no-NO`

• Punjabi: `pa-PK`

• Swedish: `sv-SE`

• Swahili: `sw-KE`

• Urdu: `ur-PK`

**Note**: For languages such as Chinese, Japanese, and Korean, the returned text may contain Unicode escape sequences. Ensure your client correctly decodes Unicode for proper display.




**request**


**model_name** `string` <span data-api-tag="require|9XQ4jp">必选</span>

Currently, only `bigmodel`is available.



**output_zh_variant** `string`

Specifies the target Traditional Chinese variant for output conversion.

• `traditional`: Simplified → Traditional (Mainland convention)

• `tw`: Simplified → Traditional (Taiwan variant)

• `hk`: Simplified → Traditional (Hong Kong variant)



**enable_auto_lang** `bool`

When set to `true` , the multilingual ASR model auto\-detects the input language and routes the request to the matching NLU cluster, so you don't need to set language manually.

Default: `false`

***Note:* **  \*\* When both `language` and `enable_auto_lang=true` are set, the auto\-detected result takes precedence.



**enable_itn** `bool`

Enable Inverse Text Normalization (ITN).

ITN converts spoken\-form ASR output into written form to improve readability.

Default: `true`



**enable_punc** `bool`

Enable punctuation

Default: `false`



**enable_ddc** `bool`

Enable semantic smoothing (DDC).

Removes or rewrites disfluencies in ASR output (pauses, filler words, repetitions) to improve text readability.

Default: `false`



**enable_speaker_info** `bool`

Enable speaker diarization.

When enabled, speaker labels are returned. Best performance is achieved when the number of speakers is **10 or fewer**. Accuracy **cannot be guaranteed** when the audio contains significant variations in volume, distance, or other acoustic conditions.

Default: `false`



**enable_channel_split** `bool`

Enable dual\-channel recognition.

When `true`, results are tagged with `channel_id: 1` for the left channel and `2` for the right channel.

Default: `false`



**show_utterances** `bool`

Output utterance\- and word\-level segmentation information.

Dedault: `false`



**vad_segment** `bool`

Use VAD for sentence segmentation.

When dual\-channel recognition is enabled, VAD\-based segmentation is usually required and can be turned on at the same time.

Default: `false`



**end_window_size** `int`

Forced pause duration (ms).The minimum silence duration used to determine the end of a sentence.

Default: `800` ms

Range: `300–5000` ms

Recommended: `800–1000` ms.

Use `≤500` ms for latency\-sensitive scenarios.

**Note:**  Setting this value disables semantic segmentation; silence duration drives segmentation instead.



**sensitive_words_filter** `string`

Filters sensitive words from the recognition output. If none is set, the original text is returned unchanged.


**system_reserved_filter** `bool`

When set to `true`, applies the built\-in sensitive\-word list (mainly restricted vocabulary); matches are replaced with `*`

Default: `false`



**filter_with_empty** `string`

Custom words to be removed from the output (replaced with an empty string).



**filter_with_signed** `string`

Custom words to be replaced with `*` in the output.




**corpus** `dict`

Corpus / intervention configuration


**context** `string`

A JSON\-encoded string that passes hotwords, dialogue context, and (optionally) visual context to the model to improve transcription accuracy.

**Capabilities**

```JSON
"context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}"
```


```JSON
// Context: Can include dialogue history, bot information, personalization details, business scenario info, etc., such as:
// a. Dialogue history: Pass in the most recent rounds of conversation
// b. Bot information: e.g., "I'm chatting with Lin Daiyu", "I'm talking to my phone using Assistant A"
// c. Personalization info: "I'm currently in Haidian District, Beijing", "I have a Sichuan accent", "I like music"
// d. Business scenario info: "This is a recording of an external customer interview by a Ping An salesman, which may involve..."

{
    \"context_type\": \"dialog_ctx\",
    \"context_data\":[
        {\"text\": \"text1\"},
        {\"image_url\": \"image_url\"},
        {\"text\": \"text2\"},
        {\"text\": \"text3\"},
        {\"text\": \"text4\"},
        ...
    ]
}
```



* **Hotwords:**  Pass domain\-specific or rare words to bias recognition. Up to **5,000 words** per request.

* **Dialogue context:**  Pass prior dialogue turns to leverage conversational context. Up to **800 tokens across 20 turns** (inclusive); when the limit is exceeded, the oldest turns are truncated first so that the most recent dialogue is preserved. The context_data field is ordered from **newest to oldest**.



**Visual context**  *(Seed ASR 2.0)*  : Pass an image via image_url so the model can interpret visual content alongside audio for more accurate transcription. Limits: **1 image per request**,  **≤500 KB**, formats JPEG / JPG/ PNG.

**Example:** 







**Response**


**audio_info** `object`


**duration** `int`

Total audio duration in ms




**result**


**additions**


**duration** `int`

Total audio duration in ms




**text** `string`

Full transcript of the audio.



**utterances** `object list`


**additions** `object`


**channel_id** `string`

Audio channel index the utterance belongs to.



**speaker** `string`

Speaker label assigned by diarization.




**end_time** `int`

Utterance end offset in milliseconds.



**start_time** `int`

Utterance start offset in milliseconds.



**text** `string`

Transcript text of the utterance.



**words** `object list`


**confidence** `float`

Recognition confidence score.



**end_time** `int`

Utterance end offset in milliseconds.



**start_time** `int`

Utterance start offset in milliseconds.



**text** `string`

The word token
