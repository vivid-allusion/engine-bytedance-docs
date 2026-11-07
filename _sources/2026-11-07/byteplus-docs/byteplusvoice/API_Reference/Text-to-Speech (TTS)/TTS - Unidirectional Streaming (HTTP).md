---
title: "TTS - Unidirectional Streaming (HTTP)"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/unidirectional_tts_http"
---

<span id="MHovHG9e"></span>
# Interface Function

The BytePlus unidirectional streaming TTS API converts text to natural\-sounding speech in multiple languages and dialects with low\-latency HTTP streaming output. This document provides complete integration guidance, including request and response specifications, best practices for streaming audio handling, sample code, and error troubleshooting steps to help you quickly implement high\-quality text\-to\-speech functionality in your applications.

<span id="Qsu1IEmV"></span>
## Best Practices


* The client reads the JSON data returned by the server in a streaming manner and extracts the corresponding audio from it.

* The returned audio is in base64 format, which needs to be parsed and concatenated into a byte array to assemble the audio for playback.

* You can use connection\-reuse components in the corresponding programming language to avoid repeatedly creating TCP connections (the Byteplus server’s keep\-alive time is 1 minute), such as Python’s `session` component:


```JSON
session = requests.Session()
response = session.post(url, headers=headers, json=payload, stream=True)
```


<span id="Kh7YMhd3"></span>
# Interface Description

<span id="wNitEmSP"></span>
## Request

<span id="tJqx5XDv"></span>
#### Request Path

The request path is: `https://voice.ap-southeast-1.bytepluses.com/api/v3/tts/unidirectional`

<span id="vdDeXveF"></span>
#### Connection & Authentication

The API supports two authentication methods. Due to the console upgrade, we recommend using the **simplified X\-Api\-Key authentication**.


|**Method** |**Header** |**Description** |
|---|---|---|
|**Recommended** |`X-Api-Key` |A single API Key generated from the [BytePlus console](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide). |
|**Legacy (compatible)**  |`X-Api-App-Key` + `X-Api-Access-Key` |The previous authentication method using an [App ID and Access Token](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide) pair. |


**Example (Recommended)** 

```Python
    headers = {
        "X-Api-Key": "xxxxxxxx", # your API key obtained from the new console
        "X-Api-Resource-Id": "seed-tts-2.0", # TTS 2.0 resource ID
        "X-Api-App-Key": "aGjiRDfUWi",
        "Content-Type": "application/json",
        "Connection": "keep-alive"
    }
    
    ## Response Header
    ## Provide this logID to Techinical Support if needed
    X-Tt-Logid: 202407261553070FACFE6D19421815D605 
```


<span id="aSR5S5dy"></span>
#### **Example (Legacy)** 

```Python
    headers = {
        "X-Api-App-Id": "xxxxxx", # APP ID obtained using the legacy console
        "X-Api-Access-Key": "xxxxxxxxxxxxxxx", # Access Token obtained using the legacy console
        "X-Api-Resource-Id": "volc.service_type.1000009", # TTS 1.0 resource ID
        "X-Api-App-Key": "aGjiRDfUWi",
        "Content-Type": "application/json",
        "Connection": "keep-alive"
    }
    
    ## Response Header
    ## Provide this logID to Techinical Support if needed
    X-Tt-Logid: 202407261553070FACFE6D19421815D605 
```


<span id="v5sLqvDL"></span>
#### Request Headers


|Key |Description |Required |Value Example |
|---|---|---|---|
|X\-Api\-Key |Please obtain the **API Key** from the BytePlus console, refer to [Console Guide](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Due to the console upgrade, authentication can now be completed using <code>X-Api-Key</code>.</div><br><br><br><div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Id</code> + <code>X-Api-Access-Key</code> pair is still supported for backward compatibility.</div><br><br><br><div data-tips="true" data-tips-type="default">For new integrations, <code>X-Api-Key</code> is recommended.</div><br> |Yes |your\-api\-key |
|X\-Api\-Resource\-Id |Specifies the service resource ID used to select different model versions and synthesis effects.<br><br><br>* **TTS 1.0:** <br><br>   * `seed-tts-1.0` or `volc.service_type.1000009`<br><br>* **TTS 2.0:** <br><br>   * `seed-tts-2.0`<br><br>* **Voice Replication 1.0：** <br><br>   * `seed-icl-1.0` or `volc.megatts.default` <br><br>* **Voice Replication 2.0:** <br><br>   * `seed-icl-2.0` |Yes |* **TTS 1.0:** <br><br>   * `seed-tts-1.0` or `volc.service_type.1000009`<br><br>* **TTS 2.0:** <br><br>   * `seed-tts-2.0`<br><br>* **Voice Replication 1.0：** <br><br>   * `seed-icl-1.0` or `volc.megatts.default` <br><br>* **Voice Replication 2.0:** <br><br>   * `seed-icl-2.0` |
|X\-Api\-App\-Key |Fixed value |Yes |aGjiRDfUWi |
|X\-Api\-Request\-Id |Identifies the client request ID, a UUID random string |No |67ee89ba\-7050\-4c04\-a3d7\-ac61a63499b3 |


<span id="8Z6MY083"></span>
#### Response Headers


|Key |Description |Value Example |
|---|---|---|
|X\-Tt\-Logid |The logid returned by the server. It is recommended that users obtain and print it for troubleshooting purpose. |2025041513355271DF5CF1A0AE0508E78C |


<span id="EZ5JOriE"></span>
## Request Body


|Field |Description |Required |Type |Default Value |
|---|---|---|---|---|
|user |User information |No |object |—— |
|user.id |User uid |No |string |—— |
|req_params.text |Input text <br><br>(SSML is not currently supported) |Yes |string |—— |
|req_params.speaker |Voice ID. <br><br>For details, see the [Voice List](https://docs.byteplus.com/en/docs/byteplusvoice/voicelist) |Yes |string |—— |
|req_params.audio_params |Audio parameters, used to reduce server\-side audio decoding time |Yes |object |—— |
|req_params.audio_params.format |Audio encoding format:`mp3`, `ogg_opus` and `pcm`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Passing WAV to the API will not cause an error, but in streaming scenarios it will return multiple WAV headers. PCM is recommended in such cases.</div><br> |No |string |mp3 |
|req_params.audio_params.sample_rate |Audio sampling rate. Optional values: [`8000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`] |No |number |24000 |
|req_params.audio_params.bit_rate |The audio bit\-rate can be set to values such as `16000`, `32000`, etc.<br><br>The default range is 64k~160k, it's a must to pass parameter `disable_default_bit_rate` as `true` if you want to set the rate lower than 64k.<br><br>Golang sample: `additions = fmt.Sprintf({\"disable_default_bit_rate\":true}")`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">For MP3 and OGG formats, it is recommended to manually set the <code>bit_rate</code>. </div><br><br><br><div data-tips="true" data-tips-type="tip">Using the default value (8k) may cause significant audio quality loss. For WAV files, the bitrate is calculated the same way as PCM:</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>bitrate (bps) = sample rate × bit depth × number of channels</strong></div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, the large TTS model can only modify the sample rate, so for WAV format, the bitrate can only be changed by adjusting the sample rate.</div><br> |No |number |—— |
|req_params.audio_params.emotion |Set the emotion of the timbre. Example: `"emotion": "angry"`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist">some voices</a> support emotion setting, and the supported emotion ranges vary among different voices.</div><br> |No |string |—— |
|req_params.audio_params.emotion_scale |After calling the emotion to set the emotion parameters, you can use emotion_scale to further set the emotion value, which ranges from 1 to 5. If not set, the default value is 4.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Theoretically, the larger the emotion value, the more obvious the emotion. However, the actual emotion values from 1 to 5 are non\-linearly increasing, and the emotion may not increase significantly after exceeding a certain value. For example, the emotion values set to 3 and 5 may be close.</div><br> |No |number |4 |
|req_params.audio_params.speech_rate |Speech rate. The value range is [`-50`, `100`]. <br><br>A value of `100` indicates the 2.0x speed. A value of `-50 `indicates the 0.5x speed. |No |number |0 |
|req_params.audio_params.loudness_rate |Volume. The value range is [`-50`, `100`]. <br><br>A value of `100` represents 2.0x volume, and `-50` represents 0.5x volume. |No |number |0 |
|req_params.audio_params.enable_timestamp |Whether to return both word and phoneme timestamps.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only works on TTS1.0 and ICL1.0 <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist">voices</a> and only Chinese & English are supported. </div><br> |No |bool |FALSE |
|req_params.audio_params.enable_subtitle |Whether to return both word and phoneme timestamps.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only works on TTS2.0 and ICL2.0 <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist">voices</a> and only Chinese & English are supported. </div><br> |No |bool |FALSE |
|req_params.additions |User\-defined parameters |Yes |jsonstring |—— |
|req_params.additions.post_process.pitch |It needs to be passed in additions and set in post_process. The pitch range is [\-12, 12].<br><br>Golang sample:`additions = fmt.Sprintf("{"post_process":{"pitch":12}}")`<br><br>Note: If the pitch is the default 0, adjusting the speech_rate will not take effect; If the pitch is not the default 0, then the pitch can take effect, and at this time, the speech_rate can also take effect. |No |number |0 |
|req_params.additions.silence_duration |Setting this parameter can add a mute duration at the end of the sentence, ranging from 0 to 30000ms.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The added mute at the end of the sentence is mainly for the end of the last sentence in the input text, not the end of each sentence.</div><br> |No |number |0 |
|req_params.additions.enable_language_detector |Automatically identify the language |No |bool |FALSE |
|req_params.additions.disable_markdown_filter |Whether to enable markdown parsing and filtering.<br><br>When it is **true**, parse and filter markdown syntax. For example, `**Hello**` will be read as  **"Hello"** .<br><br>When it is **false**, **do not parse** **or filter**. For example, `**Hello**`  will be read as  **"star 'Hello' star"** . |No |bool |FALSE |
|req_params.additions.disable_emoji_filter |Whether to enable emoji parsing and filtering.<br><br> When set to **true**, emojis will **not be parsed or filtered** and will be displayed in the text to be synthesized.<br><br> When set to **false**, emojis will be **parsed and filtered out** and will **not** be displayed in the text to be **synthesized**. |No |bool |FALSE |
|req_params.additions.enable_latex_tn |Whether it is possible to broadcast LaTeX formulas depends on setting `disable_markdown_filter` to `true`. When this parameter is set to `true`, it enables the functionality to broadcast LaTeX formulas; otherwise, such formulas may not be properly handled. |No |bool |FALSE |
|req_params.additions.max_length_to_filter_parenthesis |Whether to filter the content within parentheses. Set it to `0` if you don't want to filter, and set it to `100` if you want to filter. |No |int |100 |
|req_params.additions.explicit_language |Only read the text in the specified language.<br><br><br>* If no parameter is given, it will work normally for a mixture of Chinese and English.<br><br>* `zh-cn`: Mainly Chinese, supports a mixture of Chinese and English.<br><br>* `en`: Only English.<br><br>* `ja`: Only Japanese.<br><br>* `es-mx`: Only Mexican Spanish.<br><br>* `es`: Only Spanish.<br><br>* `id`: Only Indonesian.<br><br>* `pt-br`: Only Brazilian Portuguese.<br><br>* `pt`: Only Portuguese.<br><br>* `ko`: Only Korean.<br><br>* `it`: Only Italian. <br><br>* `de`: Only German.<br><br>* `fr`: Only French.<br><br>* `th`: Only Thai.<br><br>* `vi`: Only Vietnamese.<br><br>* `ru`: Only Russian.<br><br>* `fil`: Only Filipino.<br><br>* `ms`: Only Malay.<br><br>* `ar`: Only Arabic.<br><br>* `pl`: Only Polish.<br><br>* `tr`: Only Turkish.<br><br>* `sv`: Only Swedish.<br><br><br>Sample (Go): <br><br>`additions = fmt.Sprintf("{\"explicit_language\":\"zh-cn\"}")` |No |jsonstring |—— |
|req_params.additions.unsupported_char_ratio_thresh |Default: `0.3`, Maximum value: `1.0`<br><br>If the proportion of detected unsupported languages exceeds the set ratio, an error code or fallback audio will be returned. |No |float |0.3 |
|req_params.additions.context_language |Provide reference language for the model<br><br><br>* If not given, Western European languages use English.<br><br>* `id`: Western European languages use Indonesian.<br><br>* `es`: Western European languages use Mexican Spanish.<br><br>* `pt`: Western European languages use Brazilian Portuguese. |No |string |—— |
|req_params.additions.cache_config |Enable Caching<br><br>When caching is enabled, the service will directly read the cache and return the audio synthesized for the same text in the previous synthesis when synthesizing identical text. This can significantly accelerate the synthesis speed for the same text. The cached data is retained for 1 hour.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Data returned via the cache will not include timestamps.</div><br><br><br>Golang sample: `additions := fmt.Sprintf("{\"disable_default_bit_rate\":true, \"cache_config\": {\"text_type\": 1,\"use_cache\": true}}")` |No |object | |
|req_params.additions.cache_config.text_type |When used together with the `use_cache` parameter, set it to `1`when enabling caching. |No |int |1 |
|req_params.additions.cache_config.use_cache |When used in conjunction with the `text_type` parameter, set `use_cache` to `true` when enabling caching. |No |bool |TRUE |
|req_params.additions.context_texts<br><br>([TTS 2.0 only](https://docs.byteplus.com/en/docs/byteplusvoice/voicelist))<br><br> |Auxiliary information for speech synthesis, used for conversational\-style synthesis to better convey vocal emotion.<br><br>This field can be explored in various ways. Common examples include the following:<br><br><br>1. **Speech rate adjustment**<br><br>   1. Example: context_texts: ["Could you speak a bit slower?"]<br><br>2. **Emotion / tone adjustment**<br><br>   1. Example: context_texts: ["Could you speak in a very, very heartbroken tone?"]<br><br>   2. Example: context_texts: ["Hmm, make your tone a bit more cheerful."]<br><br>3. **Volume adjustment**<br><br>   1. Example: context_texts: ["Lower your voice a bit."]<br><br>4. **Vocal style / timbre adjustment**<br><br>   1. Example: context_texts: ["Could you speak in a proud tone?"]<br><br><br><div data-tips="true" data-tips-type="default"><strong>Note:</strong></div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">This field is only applicable to voices of <strong>“</strong><a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist"><strong>TTS 2.0</strong></a><strong>”</strong>.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Only the <strong>first value</strong> in the string list is effective.</div><br><br><br>3. <div data-tips="true" data-tips-type="default">The text in this field is <strong>not included in billing</strong>.</div><br> |No |string list |null |
|req_params.additions.tone_fidelity |**Whether to enable tone fidelity mode.**  When enabled, the model will attempt to reproduce the voice characteristics and speaking style of the prompt audio used for training **as closely as possible**, including emotion, prosody, and accent.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><div data-tips="true" data-tips-type="default">This option is <strong>only applicable </strong>to <strong>Voice Replication 2.0 </strong>cloned<strong> </strong>voices (with resourceID <code>seed-icl-2.0</code>). </div><br><br><br><div data-tips="true" data-tips-type="default">It only supports synthesis of text in the same language as the training audio. <strong>Cross\-language synthesis is not supported</strong>. </div><br><br><br><div data-tips="true" data-tips-type="default">This option is also <strong>not supported by the bi\-directional streaming</strong> synthesis API.</div><br> |No |bool |FALSE |


<span id="465VwMhY"></span>
#### Request parameters sample code

```JSON
{
  "user": {
    "uid": "123123"
  },
  "req_params": {
    "text": "Welcome to use ByteDance text-to-speech services.",
    "speaker": "en_female_skye_emo_v2_mars_bigtts",
    "audio_params": {
      "format": "mp3",
      "sample_rate": 24000
    },
    "additions": "{\"tone_fidelity\":false,\"silence_duration\":100,\"enable_language_detector\":true,\"explicit_language\":\"zh\",\"context_language\":\"\",\"disable_markdown_filter\":true,\"disable_emoji_filter\":true,\"enable_timestamp\":true,\"enable_latex_tn\":true,\"max_length_to_filter_parenthesis\":100,\"unsupported_char_ratio_thresh\":0.3,\"ache_config\":{\"text_type\":1,\"use_cache\":true},\"post_process\":{\"pitch\":0},\"context_texts\":[\"Could you speak a bit slower?\"]}"
  }
}
```


<span id="7GevX2tU"></span>
## Response

Audio response data, where data corresponds to the synthesized base64 audio:

```Plain
{
    "code": 0,
    "message": "",
    "data" : {{STRING}}
}
```


Successful response corresponding to the end of audio synthesis:

```Plain
{
    "code": 20000000,
    "message": "ok",
    "data": null
}
```


<span id="nYfG0rlD"></span>
## Error Code


|Code |Message |Description |
|---|---|---|
|20000000 |ok |Success status code for the end of audio synthesis |
|40402003 |TTSExceededTextLimit: exceed max limit |The submitted text length exceeds the limit |
|45000000 |speaker permission denied: get resource id: access denied |Speaker authentication failed, usually because the speaker specified timbre is not authorized or is incorrect |
||quota exceeded for types: concurrency |Concurrency limit, usually because the number of concurrent requests exceeds the limit |
|55000000 |Some server errors |General server error |


<span id="h5DX67XD"></span>
## Samples


<Tabs>
<Tab zoneid="FroHOBLSCK" title="Python Example">
<TabTitle>Python Example</TabTitle>

<span id="Q2hzvrJw"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

   * `<voice_type>`: The timbre ID you expect to use.


<span id="SOlx6sCe"></span>
### Authentication

The API supports two authentication methods. Due to the console upgrade, we recommend using the **simplified X\-Api\-Key authentication**.


|**Method** |**Header** |**Description** |
|---|---|---|
|**Recommended** |X\-Api\-Key |A single API Key generated from the BytePlus console. |
|**Legacy (compatible)**  |X\-Api\-App\-Id + X\-Api\-Access\-Key |The previous authentication method using an App ID and Access Token pair. |


<span id="adzG3Knd"></span>
#### Example (Recommended)

```Python
    headers = {
        "X-Api-Key": "xxxxxxxx", # your API key obtained from the new console
        "X-Api-Resource-Id": "seed-tts-2.0", # TTS 2.0 resource ID
        "X-Api-App-Key": "aGjiRDfUWi",
        "Content-Type": "application/json",
        "Connection": "keep-alive"
    }
```


<span id="RjKGImcT"></span>
#### Example (Legacy)

```Python
    headers = {
        "X-Api-App-Id": "xxxxxx", # APP ID obtained using the legacy console
        "X-Api-Access-Key": "xxxxxxxxxxxxxxx", # Access Token obtained using the legacy console
        "X-Api-Resource-Id": "volc.service_type.1000009", # TTS 1.0 resource ID
        "X-Api-App-Key": "aGjiRDfUWi",
        "Content-Type": "application/json",
        "Connection": "keep-alive"
    }
```


<span id="JwN1HzYO"></span>
### Python env


* Python：Version 3.9 and above.

* Pip：Version 25.1.1 and above. You can use the following command to install it.


```Bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
pip3 install requests
```


<span id="cJ8dPFDM"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_073603f4408ab661e8a1e19d81ebae6b.zip" name="tts_unidirectional_http_demo.py.zip">tts_unidirectional_http_demo.py.zip</Attachment>


<span id="oJ4hWZC6"></span>
### Invoke

> `appID`: Replace with your APP ID.

> `accessKey`: Replace with your Access Token.

> `speaker`: Replace with your timbre ID, eg.`zh_female_cancan_mars_bigtts`.


```Bash
python3 tts_http_demo.py
```





</Tab>
</Tabs>
