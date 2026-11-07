---
title: "Submit Task - HTTP"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilesubmittask"
---

This API **asynchronously** transcribes audio files into text. Uploaded files must be smaller than 512 MB and no longer than 5 hours. After uploading a file, use the **Query Result API ** to retrieve the transcription results.

&nbsp;

<span data-label="purple">POST</span> https://voice.ap\-southeast\-1.bytepluses.com/api/v3/auc/bigmodel/submit

&nbsp;


<span id="ULAS3Id9"></span>
### Request Headers


**X\-Api\-Key ** `string` <span data-api-tag="require|1RbFw3">必选</span>

API Key can be retrieved from [Speech Console > API Key ](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default) 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported, check <a href="https://docs.byteplus.com/en/docs/byteplusvoice/legacyconsoleauth?lang=en">Legacy Console Authentication Reference</a> for details.</div>




**X\-Api\-Resource\-Id ** `string` <span data-api-tag="require|W2vM70">必选</span>

Represents the resource information ID for calling the service：


* `volc.seedasr.auc`：Seed ASR 2.0 model

* `volc.bigasr.auc`：Seed ASR 1.0 model



**X\-Api\-Request\-Id ** `string` <span data-api-tag="require|W2vM70">必选</span>

Used for the **task ID ** of submitting and querying tasks. It is recommended to pass in a randomly generated UUID.



**X\-Api\-Sequence ** `string` <span data-api-tag="require|W2vM70">必选</span>

Packet sequence number. The fixed value is: `-1`




<span id="OG7QrhRG"></span>
### Request Body


**audio ** `dict` <span data-api-tag="require|WnVo1B">必选</span>


**url ** `string` <span data-api-tag="require|1zS7c2">必选</span>

Audio link



**language ** `string`

Specify the language for speech recognition. The following languages are currently supported:


* English: `en-US`

* Mandarin Chinese: `zh-CN`

* Cantonese: `yue-CN`

* Japanese: `ja-JP`

* Indonesian Bahasa: `id-ID`

* Spanish: `es-MX`

* Portuguese: `pt-BR`

* German: `de-DE`

* French: `fr-FR`

* Korean: `ko-KR`

* Filipino: `fil-PH`

* Malay: `ms-MY`

* Thai: `th-TH`

* Arabic: `ar-SA`

* Italian: `it-IT`

* Bengali: `bn-BD`

* Greek: `el-GR`

* Dutch: `nl-NL`

* Russian: `ru-RU`

* Turkish: `tr-TR`

* Vietnamese: `vi-VN`

* Polish: `pl-PL`

* Romanian: `ro-RO`

* Ukrainian: `uk-UA`

* Azerbaijani: `az-AZ`

* Bulgarian: `bg-BG`

* Czech: `cs-CZ`

* Danish: `da-DK`

* Finnish: `fi-FI`

* Hindi: `hi-IN`

* Hungarian: `hu-HU`

* Kazakh: `kk-KZ`

* Khmer: `km-KH`

* Burmese: `my-MM`

* Norwegian: `no-NO`

* Punjabi: `pa-PK`

* Swedish: `sv-SE`

* Swahili: `sw-KE`

* Urdu: `ur-PK`

* Slovak: `sk-SK`

* Slovenian: `sl-SI`

* Croatian: `hr-HR`

* Serbian: `sr-RS`

* Lithuanian: `lt-LT`

* Latvian: `lv-LV`

* Estonian: `et-EE`

* Persian: `fa-IR`

* Afrikaans: `af-ZA`

* Icelandic: `is-IS`

* Albanian: `sq-AL`

* Catalan: `ca-ES`

* Cebuano: `ceb-PH`

* Irish: `ga-IE`

* Javanese: `jv-ID`

* Uzbek: `uz-UZ`


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">When <code>language</code> is empty, the model supports <strong>Mandarin Chinese, English, Cantonese, Shanghainese, Minnan, Sichuan, Shaanxi dialect </strong>recognition. </div>




**format ** `string` <span data-api-tag="require|7sHXWE">必选</span>

Audio container format

Options: `raw` / `wav` / `mp3` / `ogg `/ `pcm` /` spx` / `amr` /` aac` / `m4a`



**codec** `string`

Audio encoding format, the default is raw（pcm）

Options: `raw` / `opus`



**rate** `int`

Audio sampling rate, the default is `16000`



**bits** `int`

Audio sampling point bits, the default is `16`



**channel** `int`

Number of audio channels, the default is `1`

Options：

`1`: mono

`2`: stereo




**request** `dict`


**model_name** `string` <span data-api-tag="require|tXLKeG">必选</span>

Model name, use fixed value: `bigmodel`



**enable_speaker_info** `bool`

Enable Speaker Diarization, the default is `false`

When enabled, speaker information can be returned. Best performance is achieved when the number of speakers is **10 or fewer**.

If the audio contains significant variations in volume, distance, or other acoustic conditions, speaker differentiation accuracy **cannot be guaranteed**.



**output_zh_variant** `string`

Specifies the target Traditional Chinese variant for output conversion.


* `traditional`: Simplified Chinese to Traditional Chinese (Mainland convention)

* `tw`: Simplified Chinese to Traditional Chinese (Taiwan variant)

* `hk`: Simplified Chinese to Traditional Chinese (Hong Kong variant)



**enable_itn** `bool`

Enable Inverse Text Normalization, the default is `true`

Inverse Text Normalization (ITN) is a part of the automatic speech recognition (ASR) post\-processing pipeline. The task of ITN is to convert the original speech output of the ASR model into a written form to improve the readability of the text.

For example, "一九七零年" \-\> "1970 年" and "一百二十三美元" \-\> "$123".



**enable_punc** `bool`

Enable punctuation, the default is `false`

When enabled, the system automatically adds punctuation marks such as commas, periods, and question marks to the recognition results, improving text readability.



**enable_ddc** `bool`

Enable Disfluency Detection and Correction, the default is `false`

When enabled, the system removes or corrects disfluencies in the recognition results, such as filler words, interjections, and repeated words, making the text more coherent and readable.



**enable_channel_split** `bool`

Enable dual\-channel recognition, the default is `false`

When enabled, the returned results include a channel_id field to identify the audio channel.

`1`: Left channel

`2`: Right channel



**show_utterances** `bool`

The default value is `false`

Enables the output of sentence segmentation, word segmentation, speaker, and speech pause information. 



**enable_auto_lang** `bool`

Enable language auto\-detection capability, the default is `false`.

When `enable_auto_lang=true`, a multilingual ASR model is used to automatically detect the language of the input audio and dynamically routes the request to the corresponding NLU (Natural Language Understanding) cluster based on the detection result. The caller does not need to specify the language in advance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">If both <code>language</code> and <code>enable_auto_lang=true</code> are provided, the automatically detected language will take precedence.</div>




**enable_lid** `bool`

Enable language identification (LID), the default is `false`

When set to `true`, the recognition result includes the `lid_lang` field in `additions`, which indicates the detected language label. 

For example:


* `singing_en`: English singing

* `singing_mand`: Mandarin singing

* `singing_dia_cant`: Cantonese singing

* `speech_en`: English speech

* `speech_mand`: Mandarin speech

* `other_langs`: Other human languages

* `others`: Non\-semantic voice or non\-human audio

* `"(blank)"`: Unable to determine (for example, audio is too short)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">The languages supported for language identification (<code>enable_lid</code>) are not identical to the transcription languages supported by the <code>language</code> parameter. </div>




**vad_segment** `bool`

Use Voice Activity Detection (VAD) to perform sentence segmentation.

The default is `false`, and the default is semantic sentence segmentation.

When dual\-channel recognition is turned on, VAD sentence segmentation is usually required, and this parameter can be turned on at the same time.



**end_window_size** `int`

Sets the silence threshold for Voice Activity Detection (VAD), in milliseconds. When the detected continuous silence reaches this threshold, the system considers the utterance complete and triggers sentence segmentation.

**Default**: `800` ms

**Range: ** [`300`, `5000`] ms

**Recommended value: ** `800` or `1000` ms

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">If the value is set too low, sentences may be segmented too frequently, resulting in fragmented output. If the value is set too high, it may be difficult to accurately separate individual utterances. We recommend adjusting this value based on your specific use case.</div>




**sensitive_words_filter** `string`

Enables sensitive word filtering. When enabled, sensitive words in the recognition results can be masked or replaced.

This parameter supports three processing modes: no processing (default, displaying the original text), filtering by removing sensitive words, and masking sensitive words with `*`.

Example:

```Python
"sensitive_words_filter":"{\"system_reserved_filter\":true,\"filter_with_empty\":[\"Sensitive Word\"],\"filter_with_signed\":[\"Sensitive Word\"],\"wrap_with_marks\": false}"
```



**system_reserved_filter ** `bool`

Whether to enable the system\-defined sensitive word list. When enabled, matched sensitive words are replaced with `*`. The system\-defined list mainly includes restricted or sensitive terms.

Default: `false`



**filter_with_empty ** `string`

Specifies custom sensitive words to be removed and replaced with an empty string. 



**filter_with_signed ** `string`

Specifies custom sensitive words to be masked with `*`.



**wrap_with_marks ** `bool`

Whether to wrap sensitive words with ```. Once enabled, system\-reserved words, words configured for empty\-string replacement, and words configured for asterisk replacement will all be returned in the format ``sensitive word``.

Default: `false`




**corpus** `object`

Configures a context\-specific vocabulary dictionary, allowing you to customize hotwords and replacement words. This can improve recognition accuracy for specific terms in a given context.


**context ** `string`

**Contextual Information:**  Provides auxiliary information before recognition to help the model achieve more accurate results. Supports directly specifying hotwords, conversation history, scenario information, and other contextual data. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">The hotword and context features are currently supported only by the Chinese\-English hybrid model. The language parameter must either be omitted or set to <code>zh-CN</code>. And the <code>enable_auto_lang</code> parameter cannot be enabled at the same time.</div>


<div data-tips="true" data-tips-type="default">For best practices, see <a href="https://docs.volcengine.com/docs/6561/2604976?lang=zh">Hotwords and Context</a>.</div>


Example:

```Python
## When passing the parameter, context must be serialized as a JSON string, for example:
"corpus": {
    "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}],\"context_type\":\"dialog_ctx\",\"context_data\":[{\"text\":\"The most recent answer from the assistant\"},{\"image_url\":\"image_url\"},{\"text\":\"The most recent query from the user\"},{\"text\":\"Earlier assistant response\"},{\"text\":\"Earlier user query\"}]}"
}

## a sample code before serialization
{
  "hotwords": [
    { "word": "custom word A" },
    { "word": "custom word B" },
    { "word": "custom word C" }
  ],
  "context_type": "dialog_ctx",
  "context_data": [
    {
      "speaker": "bot",
      "text": "Sure. I'm looking up the latest automotive news for you."
    },
    {
      "speaker": "user",
      "text": "Please look up the latest automotive news."
    },
    {
      "speaker": "bot",
      "text": "Of course. What information would you like me to look up?"
    },
    {
      "speaker": "user",
      "text": "Could you help me look up some information?"
    }
  ]
}
```



**hotwords ** `list`

Directly specifies a list of hotwords to improve recognition accuracy for specific terms. **Limited to 5000 words.** 


**word** `string`

Content of the hotword




**context_type** `string`

Context type. Currently, only the following type is supported: `dialog_ctx`



**context_data** `object`

A list of contextual data used to provide information such as conversation history. This parameter must be configured together with `context_type`.

**Limited to 800 tokens and within 20 rounds (inclusive).** 


**text ** `string`

Historical conversation text used to provide context and help the model improve recognition accuracy. The `speaker` field is optional and can be used to help the model better understand the dialogue context.



**image_url ** `string`

Image URL used to provide visual context and help the model better understand the audio content.

Limit to **1 image per request** and a **maximum size of 500KB (supported formats: JPEG, JPG, PNG).** 







**callback  ** `string`

Callback address.

Example:

```Python
"callback": "http://xxx"
```




**callback_data** `string`

Callback information.

```Python
"callback_data":"$Request-Id"
```





<span id="pF6mxalL"></span>
### Response Headers


**X\-Api\-Request\-Id ** `string`

Used for the **task ID ** of querying tasks, same as the one in the request header.



**X\-Api\-Status\-Code ** `string`

The status code returned by the server after submitting the task. `20000000` indicates successful submission, and others indicate failure.



**X\-Api\-Message ** `string`

The information returned by the server after submitting the task. `OK` indicates success, and others indicate failure.



**X\-Tt\-Logid ** `string`

The logid returned by the server. It is recommended that users obtain and print it to facilitate problem location.




<span id="2J2ztPIG"></span>
### Response Body

The response body of a successful **Submit API** request is empty.
