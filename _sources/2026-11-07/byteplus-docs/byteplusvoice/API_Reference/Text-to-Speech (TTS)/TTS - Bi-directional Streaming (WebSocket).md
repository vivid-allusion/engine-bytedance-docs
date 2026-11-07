---
title: "TTS - Bi-directional Streaming (WebSocket)"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts"
---

The streaming Text\-to\-Speech WebSocket API is designed to generate audio from streaming while maintaining consistency across the output. It is suited for:


* Real\-time text streaming or dynamically generated input

* Scenarios requiring word\-level audio alignment data


<span id="interface-description"></span>
# Interface Description

<span id="request"></span>
## Request

<span id="request-path"></span>
### Request path


* The request path is: `wss://voice.ap-southeast-1.bytepluses.com/api/v3/tts/bidirection`


<span id="connection-authentication"></span>
### Connection & Authentication

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
        "X-Api-Connect-Id": str(uuid.uuid4()),
    }
    
    ## Response Header
    ## Provide this logID to Techinical Support if needed
    X-Tt-Logid: 202407261553070FACFE6D19421815D605 
```


**Example (Legacy)** 

```Python
   headers = {
        "X-Api-App-Key": "xxxxxx", # APP ID obtained using the legacy console
        "X-Api-Access-Key": "xxxxxxxxxxxxxxx", # Access Token obtained using the legacy console
        "X-Api-Resource-Id": "volc.service_type.1000009" # TTS 1.0 resource ID
        "X-Api-Connect-Id": str(uuid.uuid4()),
    }
    
    ## Response Header
    ## Provide this logID to Techinical Support if needed
    X-Tt-Logid: 202407261553070FACFE6D19421815D605 
```



* Add the following information to the HTTP request header of a WebSocket connection.



|Key |Description |Required |Example |
|---|---|---|---|
|X\-Api\-Key |Please obtain the **API Key** from the BytePlus console, refer to [Console Guide](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Due to the console upgrade, authentication can now be completed using <code>X-Api-Key</code>.</div><br><br><br><div data-tips="true" data-tips-type="default">The legacy <code>X-Api-App-Key</code> + <code>X-Api-Access-Key</code> pair is still supported for backward compatibility.</div><br><br><br><div data-tips="true" data-tips-type="default">For new integrations, <code>X-Api-Key</code> is recommended.</div><br> |Yes |your\-api\-key |
|X\-Api\-Resource\-Id |Specifies the service resource ID used to select different model versions and synthesis effects.<br><br><br>* **TTS 1.0:** <br><br>   * `seed-tts-1.0` or `volc.service_type.1000009`<br><br>* **TTS 2.0:** <br><br>   * `seed-tts-2.0`<br><br>* **Voice Replication 1.0：** <br><br>   * `seed-icl-1.0` or `volc.megatts.default` <br><br>* **Voice Replication 2.0:** <br><br>   * `seed-icl-2.0` |Yes |* **TTS 1.0:** <br><br>   * `seed-tts-1.0` or `volc.service_type.1000009`<br><br>* **TTS 2.0:** <br><br>   * `seed-tts-2.0`<br><br>* **Voice Replication 1.0：** <br><br>   * `seed-icl-1.0` or `volc.megatts.default` <br><br>* **Voice Replication 2.0:** <br><br>   * `seed-icl-2.0` |
|X\-Api\-Connect\-Id |Flag ID used to track the current connection information.<br><br>We recommend that you specify this key to facilitate connection troubleshooting. | |67ee89ba\-7050\-4c04\-a3d7\-ac61a63499b3 |



* The following response header is returned upon a successful WebSocket handshake.



|Key |Description |Example |
|---|---|---|
|X\-Tt\-Logid |Log ID returned by the server. We recommend that you obtain and print the log ID to facilitate troubleshooting. |202407261553070FACFE6D19421815D605 |


<span id="websocket-binary-protocol"></span>
### 

<span id="wmHEJZGn"></span>
### Websocket Binary Protocol

WebSocket uses a binary protocol to transmit data.

The protocol consists of three parts: the variable\-length header part with at least 4 bytes, the payload size part, and the payload part.


* The header part describes the message type, serialization method, and compression format.

* The header may include the following optional fields:

   * **event**: describes predefined events for status management during the connection process.

   * **connect id size/connect id**: provides additional information for connection\-related events.

   * **session id size/session id**: provides additional information for session\-related events.

   * **error code**: used only for error frames, describing error information.

* The payload size part indicates the size of the payload.

* The payload part indicates the actual content of the payload, which varies based on the message type.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Integer fields in the protocol are in <strong>big\-endian</strong> form.</div>


**Binary** **frame**


|Byte |Left 4\-bit |Right 4\-bit |Description |
|---|---|---|---|
|0 \- Left half |Protocol version | |Only v1 is supported. The value is fixed to `0b0001` |
|0 \- Right half | |Header size (4x) |Only 4\-byte is supported. The value is fixed to `0b0001` |
|1 |Message type |Message type\-specific flag |For more information, see Message type\-specific flags below |
|2 \- Left half |Serialization method | |* `0b0000`: Raw (with no special serialization method, mainly for binary audio data)<br><br>* `0b0001`: JSON (mainly for text messages) |
|2 \- Right half | |Compression method |* `0b0000`: not compressed<br><br>* `0b001`: gzip |
|3 |Reserved ||Reserved for future use (`0b0000 0000`) |
|[4 ~ 7] |[Optional field,like event number,...] ||Optional fields depending on message type\-specific flags |
|... |Payload ||Audio data, text data, or audio\-text mixed data. |


**Message type\-specific flags**

Message type\-specific flags provide an extended structure, which is described in detail as follows.


|Message type |Description |Message type\-specific flag |Includes an event number |Remarks |
|---|---|---|---|---|
|`0b0001` |Full\-client request |0 |Yes |A complete request body to initiate a session on the server |
|`0b1001` |Full\-server response |0 |Yes |Text\-to\-speech: includes frontend information and audio\-text mixed data (Serialization=JSON) |
|`0b1011` |Audio\-only response |0 |Yes | |
|`0b1111` |Error information |None |No | |


**Request payload parameters**

The text\-to\-speech service has the following request parameters. Most of the settings will only take effect during the StartSession operation, while the text sent each time will take effect in the TaskRequest.


|Parameter |Description |Required |Type |Default value |
|---|---|---|---|---|
|user |User information | | | |
|user.uid |User UID | | | |
|event |Requested event |✓ | | |
|namespace |Request method | |string |BidirectionalTTS |
|req_params.text |Input text<br><br>(SSML is not currently supported in Bi\-directional scenario) |✓ |string | |
|req_params.speaker |Voice<br><br>For more information, see [Voice List](https://docs.byteplus.com/en/docs/byteplusvoice/voicelist) |✓ |string | |
|req_params.audio_params |Audio parameters, which facilitate audio decoding |✓ |object | |
|req_params.audio_params.format |Audio encoding format<br><br>Valid value: `mp3`, `ogg_opus`, and `pcm`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">WAV input is accepted, but in streaming scenarios, multiple WAV headers returned may affect the result. PCM is recommended.</div><br> | |string |mp3 |
|req_params.audio_params.sample_rate |Audio sampling rate. Valid values: [`8000`,`16000`,`22050`,`24000`,`32000`,`44100`,`48000`] | |number |24000 |
|req_params.audio_params.bit_rate |The audio bit\-rate can be set to values such as `16000`, `32000`, etc.<br><br>The default range is 64k~160k, it's a must to pass parameter `disable_default_bit_rate` as `true` if you want to set the rate lower than 64k.<br><br>Golang sample: <br><br>`additions = fmt.Sprintf("{\"disable_default_bit_rate\":true}")`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">For MP3 and OGG formats, it is recommended to manually set the <code>bit_rate</code>. Using the default value (8k) may cause significant audio quality loss. For WAV files, the bitrate is calculated the same way as PCM:</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>bitrate (bps) = sample rate × bit depth × number of channels</strong>.</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, the large TTS model can only modify the sample rate, so for WAV format, the bitrate can only be changed by adjusting the sample rate.</div><br> | |number | |
|req_params.audio_params.emotion |Set the emotion of the voice timbre. Example: `"emotion": "angry"`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only<a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist"> some voices</a> support emotion setting, and the supported emotion ranges vary among different voices.</div><br> | |string | |
|req_params.audio_params.emotion_scale |After calling the emotion to set the emotion parameters, you can use emotion_scale to further set the emotion value, which ranges from 1 to 5. If not set, the default value is 4.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Theoretically, the larger the emotion value, the more obvious the emotion. However, the actual emotion values from 1 to 5 are non\-linearly increasing, and the emotion may not increase significantly after exceeding a certain value. For example, the emotion values set to 3 and 5 may be close.</div><br> | |number |4 |
|req_params.audio_params.speech_rate |Speech speed.<br><br>Valid values: [`-50`,`100`]. A value of `100` indicates the 2.0x speed. A value of `-50 `indicates the 0.5x speed. | |number |0 |
|req_params.audio_params.loudness_rate |Volume. <br><br>The value range is [`-50`, `100`]. `100` represents 2.0x volume, and `-50` represents 0.5x volume. | |number |0 |
|req_params.audio_params.enable_timestamp |Whether to return both word and phoneme timestamps.<br><br>The timestamp information will be included in `event=TTSSentenceEnd`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only works on TTS1.0 and ICL1.0 <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist">voices</a> and only Chinese & English are supported. </div><br> | |bool |FALSE |
|req_params.audio_params.enable_subtitle |Whether to return both word and phoneme timestamps.<br><br>The timestamp information will be returned in a new event `event=TTSSubtitle` after each `event=TTSSentenceEnd`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only works on TTS2.0 and ICL2.0 <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist">voices</a> and only Chinese & English are supported. </div><br> | |bool |FALSE |
|req_params.additions |User\-defined parameters | |jsonstring | |
|req_params.additions.silence_duration |Setting this parameter can add a mute duration at the end of the sentence, with a range of 0 to 30000 milliseconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The added mute at the end of the sentence mainly applies to the end of the last sentence of the input text, not the end of each individual sentence.</div><br> | |number |0 |
|req_params.additions.enable_language_detector |Automatic Language Detection | |bool |FALSE |
|req_params.additions.disable_markdown_filter |Whether to enable markdown parsing and filtering.<br><br>When it is **true**, parse and filter markdown syntax. For example, `**Hello**` will be read as  **"Hello"** .<br><br>When it is **false**, **do not parse** **or filter**. For example, `**Hello**`  will be read as  **"star 'Hello' star"** . | |bool |FALSE |
|req_params.additions.disable_emoji_filter |Whether to enable emoji parsing and filtering.<br><br> When set to **true**, emojis will **not be parsed or filtered** and will be displayed in the text to be synthesized.<br><br> When set to **false**, emojis will be **parsed and filtered out** and will **not** be displayed in the text to be **synthesized**. | |bool |FALSE |
|req_params.additions.enable_latex_tn |Whether it is possible to broadcast LaTeX formulas depends on setting `disable_markdown_filter` to `true`. When this parameter is set to `true`, it enables the functionality to broadcast LaTeX formulas; otherwise, such formulas may not be properly handled. | |bool |FALSE |
|req_params.additions.max_length_to_filter_parenthesis |Whether to filter the content within parentheses. Set it to `0` if you don't want to filter, and set it to `100` if you want to filter. | |int |100 |
|req_params.additions.explicit_language |Only read the text in the specified language.<br><br><br>* If no parameter is given, it will work normally for a mixture of Chinese and English.<br><br>* `zh-cn`: Mainly Chinese, supports a mixture of Chinese and English.<br><br>* `en`: Only English.<br><br>* `ja`: Only Japanese.<br><br>* `es-mx`: Only Mexican Spanish.<br><br>* `es`: Only Spanish.<br><br>* `id`: Only Indonesian.<br><br>* `pt-br`: Only Brazilian Portuguese.<br><br>* `pt`: Only Portuguese.<br><br>* `ko`: Only Korean.<br><br>* `it`: Only Italian. <br><br>* `de`: Only German.<br><br>* `fr`: Only French.<br><br>* `th`: Only Thai.<br><br>* `vi`: Only Vietnamese.<br><br>* `ru`: Only Russian.<br><br>* `fil`: Only Filipino.<br><br>* `ms`: Only Malay.<br><br>* `ar`: Only Arabic.<br><br>* `pl`: Only Polish.<br><br>* `tr`: Only Turkish.<br><br>* `sv`: Only Swedish.<br><br><br>Sample (Go): <br><br>`additions = fmt.Sprintf("{\"explicit_language\":\"zh-cn\"}")` | |string | |
|req_params.additions.unsupported_char_ratio_thresh |Default: `0.3`, Maximum value: `1.0`<br><br>If the proportion of detected unsupported languages exceeds the set ratio, an error code or fallback audio will be returned. | |float |0.3 |
|req_params.additions.context_language |Provide the model with the reference language.<br><br><br>* If not specified, for Western European languages, English will be used.<br><br>* "`id`", for Western European languages, Indonesian will be used.<br><br>* "`es`", for Western European languages, Spanish (Mexican variety) will be used.<br><br>* "`pt`", for Western European languages, Portuguese (Brazilian variety) will be used. | |string | |
|req_params.additions.context_texts<br><br>([TTS 2.0 only](https://docs.byteplus.com/en/docs/byteplusvoice/voicelist)) |Auxiliary information for speech synthesis, used for conversational\-style synthesis to better convey vocal emotion.<br><br>This field can be explored in various ways. Common examples include the following:<br><br><br>1. **Speech rate adjustment**<br><br>   1. Example: context_texts: ["Could you speak a bit slower?"]<br><br>2. **Emotion / tone adjustment**<br><br>   1. Example: context_texts: ["Could you speak in a very, very heartbroken tone?"]<br><br>   2. Example: context_texts: ["Hmm, make your tone a bit more cheerful."]<br><br>3. **Volume adjustment**<br><br>   1. Example: context_texts: ["Lower your voice a bit."]<br><br>4. **Vocal style / timbre adjustment**<br><br>   1. Example: context_texts: ["Could you speak in a proud tone?"]<br><br><br><div data-tips="true" data-tips-type="default"><strong>Note:</strong></div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">This field is only applicable to voices of <strong>“</strong><a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist"><strong>TTS 2.0</strong></a><strong>”</strong>.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Only the <strong>first value</strong> in the string list is effective.</div><br><br><br>3. <div data-tips="true" data-tips-type="default">The text in this field is <strong>not included in billing</strong>.</div><br> |No |string list |null |
|req_params.additions.section_id<br><br>([TTS 2.0 only](https://docs.byteplus.com/en/docs/byteplusvoice/voicelist)) |The ID of other speech synthesis conversations, used to assist the current speech synthesis by providing additional contextual information.<br><br>**Example:** <br><br>section_id = "bf5b5771\-31cd\-4f7a\-b30c\-f4ddcbf2f9da"<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">This field is only applicable to voices of <strong>“</strong><a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicelist"><strong>TTS 2.0</strong></a><strong>”</strong>.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">A maximum of 30 rounds or 10 minutes of previous synthesis conversations can be linked as historical context. </div><br> |No |string |null |


<span id="LOVZ7jXO"></span>
### Request parameters sample code

```Python
{
    "user": {
        "uid": "123123"
    },
    "req_params": {
        "text": "Welcome to use Bytedance's speech service.",
        "speaker": "zh_female_vv_uranus_bigtts",
        "audio_params": {
            "format": "mp3",
            "sample_rate": 24000,
            # "emotion": "neutral",
            # "speech_rate": 100,
            # "enable_timestamp": True
        },
        # additions needs to be an escaped JSON string
        # "additions": "{\"explicit_language\":\"zh\",\"disable_markdown_filter\":true,\"disable_emoji_filter\":true,\"section_id\":\"550e8400-e29b-41d4-a716-446655440000\",\"context_texts\":[\"Make your tone a bit more cheerful.\"]}"
        "additions": json.dumps({
            # "silence_duration": 100,
            # "enable_language_detector": True,
            "explicit_language": "zh",
            # "context_language": "",
            "disable_markdown_filter": True,
            "disable_emoji_filter": True,
            "section_id": "550e8400-e29b-41d4-a716-446655440000",  # Custom section ID to link other speech synthesis conversations
            # "enable_timestamp": True,
            # "enable_latex_tn": True,
            # "max_length_to_filter_parenthesis": "100",
            # "unsupported_char_ratio_thresh": "0.3",
            # "cache_config": {
            #    "text_type": 1,
            #    "use_cache": True
            # },
            # "post_process": {
            #     "pitch": 0
            # },
            "context_texts": [
                "Make your tone a bit more cheerful."
            ]
        }, ensure_ascii=False)
    }
}
```


<span id="response"></span>
## Response

<span id="response-to-connection-establishment"></span>
### Response to connection establishment

The main focus is on the status code and body of the HTTP response returned during the connection process.


* For a successful connection, the status code is 200.

* For a failed connection, the status code is not 200, and the response body provides the cause of failure.


<span id="response-to-websocket-transmission"></span>
### Response to WebSocket transmission

**Text frame**


* Returns error information through text.


**Binary** **frame**


* Returns structured normal responses and general error information based on the binary protocol.


**Success response frame**


|Byte |Left 4\-bit |Right 4\-bit |Description |
|---|---|---|---|
|0 \- Left half |Protocol version | |Only v1 is supported. The value is fixed to `0b0001` |
|0 \- Right half | |Header size (4x) |Only 4\-byte is supported. The value is fixed to `0b0001` |
|1 |Message type |Message type\-specific flag |For more information, see Message type\-specific flags below |
|2 \- Left half |Serialization method | |* `0b0000`: Raw (with no special serialization method, mainly for binary audio data)<br><br>* `0b0001`: JSON (mainly for text messages) |
|2 \- Right half | |Compression method |* `0b0000`: not compressed<br><br>* `0b0001`: gzip |
|3 |Reserved ||Reserved for future use (`0b0000 0000`) |
|[4 ~ 7] |[Optional field, like event number,...] ||Optional fields depending on message type\-specific flags |
|... |Payload ||Audio data, text data, or audio\-text mixed data |


**Payload response parameters**


|Parameter |Description |Type |Default value |
|---|---|---|---|
|data |Binary packet returned |[]byte | |
|event |Event type returned |number | |
|res_params.text |Sentence after being segmented |string | |
|res_params.duration |Audio duration of the sentence |number | |


**Error response frame**


|Byte |Left 4\-bit |Right 4\-bit |Description |
|---|---|---|---|
|0 \- Left half |Protocol version | |Only v1 is supported. The value is fixed to `0b0001` |
|0 \- Right half | |Header size (4x) |Only 4\-byte is supported. The value is fixed to `0b0001` |
|1 |Message type |Message type\-specific flag |The value is fixed to `0b11110000` |
|2 \- Left half |Serialization method | |`0b0001`: JSON (mainly for text messages) |
|2 \- Right half | |Compression method |`0b0000`: not compressed |
|3 |Reserved ||Reserved for future use (`0b0000 0000`) |
|[4 ~ 7] |Error code ||The error code |
|... |Payload ||The error message object |


<span id="event-definition"></span>
### Event definition

In text\-to\-speech scenarios, Event is a critical field in normal data frames (both upstream and downstream). It defines necessary state transitions during the request process. For more information, see Interaction example below.


|Event code |Description |Event type |Applicable scope (upstream/downstream) |
|---|---|---|---|
|1 |StartConnection:<br><br>declaration of the initiation of a WebSocket connection<br><br>( after the HTTP connection has been upgraded ) |Connection |Upstream |
|2 |FinishConnection:<br><br>the end of a connection |Connection |Downstream |
|50 |ConnectionStarted:<br><br>successful creation of a connection |Connection |Downstream |
|51 |ConnectionFailed:<br><br>failed creation of a connection |Connection |Downstream |
|100 |StartSession:<br><br>declaration of the initiation of a WebSocket session |Connection |Upstream |
|101 |CancelSession:<br><br>declaration of the cancellation of an upstream session |Session |Upstream |
|102 |FinishSession:<br><br>declaration of the termination of an upstream session |Session |Upstream |
|150 |SessionStarted:<br><br>successful start of a session |Session |Downstream |
|151 |SessionCanceled:<br><br>cancellation of a session |Session |Downstream |
|152 |SessionFinished:<br><br>termination of an upstream or downstream session |Session |Downstream |
|153 |SessionFailed:<br><br>failed session |Session |Downstream |
|200 |TaskRequest:<br><br>transmission of the requested content |Data |Upstream |
|350 |TTSSentenceStart:<br><br>beginning of the content returned by the text\-to\-speech service |Data |Downstream |
|351 |TTSSentenceEnd:<br><br>end of the content returned by the text\-to\-speech service |Data |Downstream |
|352 |TTSResponse:<br><br>audio content returned by the text\-to\-speech service |Data |Downstream |


<span id="interaction-example"></span>
# Interaction Example

```Plain Text
Client
   │
   │ Establish WebSocket connection
   ▼
Server
   │
   └─ Connection established
   │
   ▼
Session
   │
   │ Send StartSession (TTS config, voice, etc.)
   ▼
Server
   │
   └─ Session started
   │
   ▼
Synthesis (Streaming)
   │
   │ Send TaskRequest (text)
   ▼
Server
   │
   ├─ Start TTS processing
   │
   ├─ Return TTS Sentence Start
   │
   ├─ Stream audio chunks (TTSResponse)
   │
   ▼
Client
   │
   └─ Play audio in real time
   │
   ▲
   │ (loop: continue sending text)
   │
   │ ...
   │
   ▼
Server
   │
   └─ Return TTS Sentence End
   │
   ▼
Completion
   │
   │ Send FinishSession (no more text)
   ▼
Server
   │
   ├─ Complete remaining synthesis
   │
   ├─ Return final TTS Sentence End
   │
   └─ Session finished
   │
   ▼
Connection Close
   │
   │ Close connection
   ▼
Server
   │
   └─ Connection closed
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



1. <div data-tips="true" data-tips-type="tip"><code>CancelSession</code> allows the client to proactively terminate the current session, end synthesis, and release server resources.</div>


2. <div data-tips="true" data-tips-type="tip">The best time window to send the <code>CancelSession</code> packet is after receiving <code>SessionStarted</code> but before sending <code>FinishSession</code>.</div>


3. <div data-tips="true" data-tips-type="tip">After receiving the <code>SessionCanceled</code> packet, if the client wants to continue synthesis, it must create a new session by executing <code>StartSession</code> again.</div>



**Connection:** 


* `StartConnection` packet (RequestMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_StartConnection`) ||event type ||
|8–11 |uint32(`2`) ||len(`<payload_json>`) ||
|12–93 |`{}` ||`payload_json`<br><br>Reserved for extension ||



* `FinishConnection` packet (RequestMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_FinishConnection`) ||event type ||
|8–11 |uint32(`2`) ||len(`<payload_json>`) ||
|12–13 |`{}` ||`payload_json`<br><br>Reserved for extension ||



* `ConnectionStarted` packet:



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`1001` |`0100` |Full\-server response |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_ConnectionStarted`) ||event type ||
|8–11 |uint32(`7`) ||len(`<connection_id>`) ||
|12–18 |`bxnweiu` ||connection_id ||
|19–22 |uint32(`2`) ||len(`<payload_json>`) ||
|23–24 |`{}` ||`payload_json`<br><br>Reserved for extension ||


You can leave `connection_id` **unspecified** on the client. In this case, the gateway will issue a unique connection ID.


* `ConnectionFailed` packet (ResponseMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`1001` |`0100` |Full\-server response |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_ConnectionFailed`) ||event type ||
|8–11 |uint32(`7`) ||len(`<connection_id>`) ||
|12–15 |uint32(`58`) ||len(`<response_meta_json>`) ||
|16–73 |`{"status_code": 4xxxxxxx,"message": "unauthorized"}` ||`response_meta_json`<br><br><br>* may indicate either a client\-side error or a server\-side error, it includes only the `status_code` and `message` fields. ||


**Session:** 


* `StartSession` packet (RequestMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_StartSession`) ||event type ||
|8–11 |uint32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`...`) ||len(`tts_session_meta`) ||
|28–... |`{"user": ...,"req_params": ... }` ||tts_session_meta ||


`session_id` is **required** on the client.


* `FinishSession` packet (RequestMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_FinishSession`) ||event type ||
|8–11 |int32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`2`) ||len(`<payload_json>`) ||
|28–29 |`{}` ||`payload_json`<br><br>Reserved for extension ||



* `CancelSession` packet (RequestMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_CancelSession`) ||event type ||
|8–11 |int32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`2`) ||len(`<payload_json>`) ||
|28–29 |`{}` ||`payload_json`<br><br>Reserved for extension ||



* `SessionStarted` packet (ResponseMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_SessionStarted`) ||event type ||
|8–11 |int32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`2`) ||len(`<payload_json>`) ||
|28–29 |`{}` ||`payload_json`<br><br>Reserved for extension ||



* `SessionFinished` packet (ResponseMeta):



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`1001` |`0100` |Full\-server response |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_SessionFinished`) ||event type ||
|8–11 |uint32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`48`) ||len(`<response_meta_json>`) ||
|28–75 |`{"status\_code": 20000000,"message": "ok"}` ||`response_meta_json`<br><br>includes only the `status_code` and `message` fields. ||



* `SessionFailed` packet (ResponseMeta): similar to`SessionFinished`

* `SessionCanceled` packet (ResponseMeta): similar to `SessionFinished`


**Data:** 


* Audio, including Event (with upstream event `Event_TaskRequest` used as an example)



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0010` |`0100` |Audio\-only request |with event number |
|2 |`0000` |`0000` |raw |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_TaskRequest`) ||event type ||
|8–11 |uint32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`...`) ||len(`<audios_binary>`) ||
|28–... |`...` ||audio_binary ||



* Text, including Event (with upstream event `Event_TaskRequest` used as an example)



|Byte |Left 4\-bit |Right 4\-bit |Remarks ||
|---|---|---|---|---|
|0 |`0001` |`0001` |v1 |4\-byte header |
|1 |`0001` |`0100` |Full\-client request |with event number |
|2 |`0001` |`0000` |JSON |no compression |
|3 |`0000` |`0000` | | |
|4–7 |int32(`Event_TaskRequest`) ||event type ||
|8–11 |uint32(`12`) ||len(`<session_id>`) ||
|12–23 |`nxckjoejnkegf` ||session_id ||
|24–27 |uint32(`...`) ||len(`<payload_json>`) ||
|28–... |`{...}` ||`payload_json` ||


<span id="error-code"></span>
# Error Code

```json
CodeOK Code = 20000000 //Success
CodeClientError Code = 45000000 //Common client error
CodeServerError Code = 55000000 //Common server error
CodeSessionError      Code = 55000001 //Server session error
CodeInvalidReqError   Code = 45000001 //Client request parameter error
```


<span id="sample"></span>
# Sample


<Tabs>
<Tab zoneid="seZ6xhiqAt" title="Python Example">
<TabTitle>Python Example</TabTitle>

<span id="760142c1"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the legacy console.

   * `<access_token>`: Access Token obtained using the legacy console.

   * `<api_key>`: API key obtained using the new console. 

   * `<voice_type>`: The timbre ID you expect to use.


<span id="rZxuAJMF"></span>
### Authentication

The API supports two authentication methods. Due to the console upgrade, we recommend using the **simplified X\-Api\-Key authentication**.


|**Method** |**Header** |**Description** |
|---|---|---|
|**Recommended** |X\-Api\-Key |A single API Key generated from the BytePlus console. |
|**Legacy (compatible)**  |X\-Api\-App\-Key + X\-Api\-Access\-Key |The previous authentication method using an App ID and Access Token pair. |


<span id="c8Oi0oJz"></span>
#### Example (Recommended)

```Python
    headers = {
        "X-Api-Key": "xxxxxxxx", # your API key obtained from the new console
        "X-Api-Resource-Id": "seed-tts-2.0", # TTS 2.0 resource ID
        "X-Api-Connect-Id": str(uuid.uuid4()),
    }
```


<span id="htOxSt8i"></span>
#### Example (Legacy)

```Python
   headers = {
        "X-Api-App-Key": "xxxxxx", # APP ID obtained using the legacy console
        "X-Api-Access-Key": "xxxxxxxxxxxxxxx", # Access Token obtained using the legacy console
        "X-Api-Resource-Id": "volc.service_type.1000009" # TTS 1.0 resource ID
        "X-Api-Connect-Id": str(uuid.uuid4()),
    }
```


<span id="eGWlG0yn"></span>
### Python Env


* Python：Version 3.9 and above.

* Pip：Version 25.1.1 and above. You can use the following command to install it.


```Bash
python3 -m pip install --upgrade pip
```


<span id="3ebd8c77"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7f8f4cde0df7ecb7c1bfc8020aa20ff6.gz" name="byteplus_bidirection_demo.tar.gz">byteplus_bidirection_demo.tar.gz</Attachment>


&nbsp;

<span id="16de5fc6"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p byteplus_bidirection_demo
tar xvzf byteplus_bidirection_demo.tar.gz -C ./byteplus_bidirection_demo
cd byteplus_bidirection_demo
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
pip3 install -e .
```


<span id="4993939e"></span>
### Invoke

> `<appid>`Replace with your APP ID.

> `<access_token>`Replace with your Access Token.

> `<voice_type>`Replace with your timbre ID, eg.`zh_female_cancan_mars_bigtts`.


```Bash
python3 examples/byteplus/bidirection.py --appid <appid> --access_token <access_token> --voice_type <voice_type> --text "To be, or not to be, that is the question" 
```



</Tab>
<Tab zoneid="HyMbeBMQRs" title="Java Example">
<TabTitle>Java Example</TabTitle>

<span id="02f52980"></span>
### precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

   * `<voice_type>`: The timbre ID you expect to use.


<span id="4b471d3a"></span>
### Java env


* Java：Version 21 and above.

* Maven：Version 3.9.10 and above.


<span id="1c6d128d"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7dcc4f57225d86c9aab69c0d1f690340.gz" name="byteplus_bidirection_demo.tar.gz">byteplus_bidirection_demo.tar.gz</Attachment>


&nbsp;

<span id="7e37cd1a"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p byteplus_bidirection_demo
tar xvzf byteplus_bidirection_demo.tar.gz -C ./byteplus_bidirection_demo
cd byteplus_bidirection_demo
```


<span id="216ef09f"></span>
### Invoke

> `<appid>`Replace with your APP ID.

> `<access_token>`Replace with your Access Token.

> `<voice_type>`Replace with your timbre ID, eg.`zh_female_cancan_mars_bigtts`.


```Bash
mvn compile exec:java -Dexec.mainClass=com.speech.byteplus.Bidirection -DappId=<appid> -DaccessToken=<access_token> -Dvoice=<voice_type> -Dtext="To be, or not to be, that is the question"
```



</Tab>
<Tab zoneid="v0bs5joS8F" title="Go Example">
<TabTitle>Go Example</TabTitle>

<span id="4b8f00a1"></span>
### precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

   * `<voice_type>`: The timbre ID you expect to use.


<span id="d9db4951"></span>
### Go env


* Go：Version 1.21.0 and above.


<span id="e02a532a"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0b171af9f3507ec98ca4695a5da708c7.gz" name="byteplus_bidirection_demo.tar.gz">byteplus_bidirection_demo.tar.gz</Attachment>


&nbsp;

<span id="d5ba0d7d"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p byteplus_bidirection_demo
tar xvzf byteplus_bidirection_demo.tar.gz -C ./byteplus_bidirection_demo
cd byteplus_bidirection_demo
```


<span id="0208ef90"></span>
### Invoke

> `<appid>`Replace with your APP ID.

> `<access_token>`Replace with your Access Token.

> `<voice_type>`Replace with your timbre ID, eg.`zh_female_cancan_mars_bigtts`.


```Bash
go run byteplus/bidirection/main.go --appid <appid> --access_token <access_token> --voice_type <voice_type> --text "To be, or not to be, that is the question"
```



</Tab>
<Tab zoneid="aVFSAfqxka" title="C# Example">
<TabTitle>C# Example</TabTitle>

<span id="0a99bf3b"></span>
### precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.

   * `<voice_type>`: The timbre ID you expect to use.


<span id="c09bcb89"></span>
### C# env


* .Net Version 9.0.


<span id="b38492eb"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1641bcfc05c6caaa7ed1bd903eb0a3be.gz" name="byteplus_bidirection_demo.tar.gz">byteplus_bidirection_demo.tar.gz</Attachment>


&nbsp;

<span id="2cc841a1"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p byteplus_bidirection_demo
tar xvzf byteplus_bidirection_demo.tar.gz -C ./byteplus_bidirection_demo
cd byteplus_bidirection_demo
```


<span id="7c4ef117"></span>
### Invoke

> `<appid>`Replace with your APP ID.

> `<access_token>`Replace with your Access Token.

> `<voice_type>`Replace with your timbre ID, eg.`zh_female_cancan_mars_bigtts`.


```Bash
dotnet run --project Byteplus/Bidirection/Byteplus.Speech.Bidirection.csproj -- --appid <appid> --access_token <access_token> --voice_type <voice_type> --text "To be, or not to be, that is the question"
```



</Tab>
<Tab zoneid="dxwBPZmhzb" title="TypeScript Example">
<TabTitle>TypeScript Example</TabTitle>

<span id="d1ff3169"></span>
### precondition


* Before invoking, you need to obtain the following information:

   * `<appid>`: APP ID obtained from the console.

   * `<access_token>`: Access Token obtained from the console.

   * `<voice_type>`: The timbre ID you expect to use.


<span id="9d33c003"></span>
### node env


* node：Version 24.0 and above.


<span id="7e88d56e"></span>
### Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ef6127dde420a8a073dec13c83974bb8.gz" name="byteplus_bidirection_demo.tar.gz">byteplus_bidirection_demo.tar.gz</Attachment>


&nbsp;

<span id="e6abc9f3"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p byteplus_bidirection_demo
tar xvzf byteplus_bidirection_demo.tar.gz -C ./byteplus_bidirection_demo
cd byteplus_bidirection_demo
npm install
npm install -g typescript
npm install -g ts-node
```


<span id="da29b1f5"></span>
### Invoke

> `<appid>`Replace with your APP ID.

> `<access_token>`Replace with your Access Token.

> `<voice_type>`Replace with your timbre ID, eg.`zh_female_cancan_mars_bigtts`.


```Bash
npx ts-node src/byteplus/bidirection.ts --appid <appid> --access_token <access_token> --voice_type <voice_type> --text "To be, or not to be, that is the question"
```



</Tab>
</Tabs>
