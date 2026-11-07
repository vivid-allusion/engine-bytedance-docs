---
title: "ASR - Unidirectional Streaming - WebSocket"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/asrunidirect"
---

Supports **streaming audio input** and returns the complete recognition result for each utterance. It provides higher recognition accuracy than the bidirectional streaming API and is suitable for **non\-realtime scenarios**.

> Runtime Dependencies

> 
<Tabs>
<Tab zoneid="E7WzEgW1" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_084f2effab285cf82e5196388e0bd354.zip" name="sauc_python.zip">sauc_python.zip</Attachment>



</Tab>
<Tab zoneid="bV0No9ON" title="Go">
<TabTitle>Go</TabTitle>

&nbsp;

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25e3ec23373a78508cf36cb446a4141f.zip" name="sauc_go.zip">sauc_go.zip</Attachment>



</Tab>
</Tabs>




---



<span data-label="purple">POST</span> wss://voice.ap\-southeast\-1.bytepluses.com/api/v3/sauc/bigmodel_nostream

&nbsp;


<span id="ULAS3Id9"></span>
### Request Headers


**X\-Api\-Key ** `string` <span data-api-tag="require|1RbFw3">必选</span>

API Key can be retrieved from [Speech Console > API Key ](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default) 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported, check <a href="https://docs.byteplus.com/en/docs/byteplusvoice/legacyconsoleauth?lang=en">Legacy Console Authentication Reference</a> for details.</div>




**X\-Api\-Resource\-Id ** `string` <span data-api-tag="require|W2vM70">必选</span>

Represents the resource information ID for calling the service：


* Seed ASR Model 2.0 <span data-label="purple">推荐</span>: `volc.seedasr.sauc.duration`

* Seed ASR Model 1.0: `volc.bigasr.sauc.duration` 



**X\-Api\-Request\-Id ** `string` <span data-api-tag="require|W2vM70">必选</span>

Client request ID, a UUID random string.




<span id="OG7QrhRG"></span>
### Request Body


**audio ** `dict` <span data-api-tag="require|WnVo1B">必选</span>


**format ** `string` <span data-api-tag="require|7sHXWE">必选</span>

Audio container format

Options: `wav` / `mp3` / `ogg `/ `pcm` 



**codec** `string`

Audio encoding format, the default is `raw`(pcm)

Options: `raw` / `opus`



**rate** `int`

Audio sampling rate, the default is `16000`



**bits** `int`

Audio sampling point bit number, the default is `16`



**channel** `int`

Number of audio channels, the default is `1`

Options:

`1`：mono

`2`：stereo



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





**request** `dict`


**model_name** `string` <span data-api-tag="require|tXLKeG">必选</span>

Model name, currently only `bigmodel` 



**enable_auto_lang** `bool`

Enable language auto\-detection capability, the default is `false`.

When `enable_auto_lang=true`, a multilingual ASR model is used to automatically detect the language of the input audio and dynamically routes the request to the corresponding NLU (Natural Language Understanding) cluster based on the detection result. The caller does not need to specify the language in advance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">If both <code>language</code> and <code>enable_auto_lang=true</code> are provided, the automatically detected language will take precedence.</div>




**enable_nonstream ** `bool`

Enable **dual\-pass recognition mode**, the default is ** ** `false`。

This mode supports **bidirectional streaming** for real\-time, word\-by\-word transcription output, while also leveraging a **non\-streaming re\-recognition** of segmented audio utterances to improve accuracy. This approach satisfies both **real\-time display requirements (low latency)**  and **high accuracy in final results**.

**When enabled:** 


* **Automatically enables Voice Activity Detection (VAD) for utterance segmentation.**  By default, an utterance is considered complete when continuous silence reaches **800 ms**. This threshold can be adjusted using the `end_window_size` parameter.

* **Re\-recognizes each utterance using the non\-streaming model** whenever VAD detects the end of an utterance.

* **Only the results from the non\-streaming model's second\-pass recognition** include "definite": true, indicating that the utterance has been finalized.



**enable_itn** `bool`

Enable Inverse Text Normalization, the default is `true`

Inverse Text Normalization (ITN) is a part of the automatic speech recognition (ASR) post\-processing pipeline. The task of ITN is to convert the original speech output of the ASR model into a written form to improve the readability of the text.

For example, "一九七零年" \-\> "1970 年" and "一百二十三美元" \-\> "$123".



**enable_punc** `bool`

Enable punctuation, the default is `true`

When enabled, the system automatically adds punctuation marks such as commas, periods, and question marks to the recognition results, improving text readability.



**enable_ddc** `bool`

Enable Disfluency Detection and Correction, the default is `false`

When enabled, the system removes or corrects disfluencies in the recognition results, such as filler words, interjections, and repeated words, making the text more coherent and readable.



**output_zh_variant ** `string`

Enable Traditional Chinese output

Specifies the target Traditional Chinese variant for output conversion.


* `traditional`: Simplified Chinese to Traditional Chinese (Mainland convention)

* `tw`: Simplified Chinese to Traditional Chinese (Taiwan variant)

* `hk`: Simplified Chinese to Traditional Chinese (Hong Kong variant)



**show_utterances** `bool`

The default value is `false`

Enables the output of sentence segmentation, word segmentation, speaker, and speech pause information. 



**show_speech_rate** `bool`

Include speech rate in utterance metadata, the default is `false`

If set to `"true"`, the `speech_rate` field (unit: tokens/s) will be included in the `additions` of each segmented utterance. Default is `"false"`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Enabling this parameter will automatically enable VAD\-based segmentation (default endpointing timeout: 800 ms, configurable via <code>end_window_size</code>).</div>


<div data-tips="true" data-tips-type="default">The <code>speech_rate</code> field is included in the <code>additions</code> of utterances where <code>"definite": true</code> in the recognition result.</div>




**show_volume** `bool`

Include speech volume in utterance metadata, the default is `false`

If set to `"true"`, the `volume` field (unit: dB) will be included in the `additions` of each segmented utterance. Default is `"false"`.

<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">Enabling this parameter will automatically enable VAD\-based segmentation (default endpointing timeout: 800 ms, configurable via <code>end_window_size</code>).</div>


<div data-tips="true" data-tips-type="default">The <code>volume</code> field is included in the <code>additions</code> of utterances where <code>"definite": true</code> in the recognition result.</div>




**enable_lid** `bool`

Enable language identification (LID). The default is `false`

When set to `true`, the recognition result includes the `lid_lang` field in additions, which indicates the detected language label. 

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


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Enabling <code>enable_lid</code> at this endpoint will automatically enable VAD\-based segmentation (default endpointing timeout: 800 ms, configurable via <code>end_window_size</code>).</div>


<div data-tips="true" data-tips-type="default">The <code>lid_lang </code> label is included in the <code>additions</code> of utterances where <code>"definite": true</code> is returned.</div>




**result_type ** `string`

Result return method, the default is `full`

Options:


* `full`: full result return.

* `single`: incremental result return, that is, the results of previous sentence segments are not returned.



**enable_accelerate_text ** `bool`

Enables first\-character latency optimization. The default value is `false`

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">When enabled, the system prioritizes faster first\-character output, which may slightly reduce the recognition accuracy of the initial characters. </div>




**accelerate_score** `int`

Specifies the first\-character acceleration level. The default value is `0`, which disables acceleration. The maximum value is `20`. A higher value results in faster first\-character output.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">This parameter takes effect only when <code>enable_accelerate_text</code> is enabled.</div>




**vad_segment_duration** `int`

Maximum mute threshold for semantic sentence segmentation, the default is `3000` in milliseconds. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">When the mute time exceeds this value, the text will be divided into two sentences. It does not determine the pause, so it will not modify the position where definite appears. After the <code>end_window_size</code> configuration, this parameter becomes invalid.</div>




**end_window_size** `int`

Sets the silence threshold for Voice Activity Detection (VAD), in milliseconds. When the detected continuous silence reaches this threshold, the system considers the utterance complete and triggers sentence segmentation.

**Range: ** [`300`, `5000`] ms

**Recommended value: ** `800` or `1000` ms

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">If the value is set too low, sentences may be segmented too frequently, resulting in fragmented output. If the value is set too high, it may be difficult to accurately separate individual utterances. We recommend adjusting this value based on your specific use case.</div>




**force_to_speech_time ** `int`

Specifies the minimum audio duration required to trigger VAD\-based utterance termination. The minimum value is **1 ms**. VAD\-based termination is only performed after the audio duration exceeds this threshold;

Default: `0` ms

**Recommended value: ** `100` ms.



**sensitive_words_filter** `string`

Enables sensitive word filtering. When enabled, sensitive words in the recognition results can be masked or replaced.

This parameter supports three processing modes: no processing (default, displaying the original text), filtering by removing sensitive words, and masking sensitive words with `*`.

Example:

```Python
"sensitive_words_filter":"{\"system_reserved_filter\":true,\"filter_with_empty\":[\"Sensitive Word\"],\"filter_with_signed\":[\"Sensitive Word\"],\"wrap_with_marks\": false}"
```



**system_reserved_filter ** `bool`

Whether to enable the system\-defined sensitive word list. When enabled, matched sensitive words are replaced with `*`. The system\-defined list mainly includes restricted or sensitive terms.



**filter_with_empty ** `string`

Specifies custom sensitive words to be removed and replaced with an empty string. 



**filter_with_signed ** `string`

Specifies custom sensitive words to be masked with `*`.



**wrap_with_marks ** `bool`

Whether to wrap sensitive words with ```. Once enabled, system\-reserved words, words configured for empty\-string replacement, and words configured for asterisk replacement will all be returned in the format ``sensitive word``.




**corpus** `object`

Configures a context\-specific vocabulary dictionary, allowing you to customize hotwords and replacement words. This can improve recognition accuracy for specific terms in a given context.


**context ** `string`

**Contextual Information:**  Provides auxiliary information before recognition to help the model achieve more accurate results. Supports directly specifying hotwords, conversation history, scenario information, and other contextual data. 

<div data-tips="true" data-tips-type="default">Note:</div>


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



**hotwords**`string`

Directly specifies a list of hotwords to improve recognition accuracy for specific terms. **Limited to 5000 words.** 


**word**`string`

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








<span id="pF6mxalL"></span>
### Response


**code ** `int`

Request status code. `0` indicates a successful recognition, while a non\-zero value indicates that the recognition failed.



**event** `int`

Session event type identifier.



**is_last_package ** `bool`

Indicates whether this is the last response packet. true means that all recognition results have been returned.



**payload_sequence ** `int`

Sequence number of the response packet.



**payload_size ** `int`

Size of the response payload in bytes.



**payload_msg ** `object`

Response payload containing audio information and recognition results.


**audio_info ** `object`

Audio information


**duration ** `int`

Audio duration in milliseconds (ms).




**result ** `list`

Recognition result returned upon successful recognition.


**additions ** `object`


**log_id** `string`

Server\-generated log ID used for troubleshooting and issue tracking.




**text ** `string`

Transcribed text returned upon successful recognition.



**utterances ** `list`

List of segmented utterances.


**fixed_prefix_result ** `string`

Confirmed prefix of the recognition result.



**source ** `string`

Source of the utterance segmentation result.



**definite ** `bool`

Indicates whether the current utterance is a finalized result. `true` means the utterance will not be updated further.



**words** `list`

Word\-level recognition results with timestamps.


**start_time ** `int`

Start time of the word in milliseconds.



**end_time ** `int`

End time of the word in milliseconds.



**text ** `string`

Recognized word or character.







 &nbsp;

&nbsp;
