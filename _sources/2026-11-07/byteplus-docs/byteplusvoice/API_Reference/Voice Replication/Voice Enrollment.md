---
title: "Voice Enrollment"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-training"
---

Uploads a voice sample to train a custom voice model for TTS synthesis.

## Request

**Request Path**

POST `https://voice.ap-southeast-1.bytepluses.com/api/v3/tts/voice_clone`

### **Header**

**Content\-Type ** `string` 必选

The media type of the request body. Must be set to `application/json`

**X\-Api\-Key ** `string`  必选

API Key can be obtained from [Byteplus Console](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default).

**X\-Api\-Request\-Id ** `string` 必选

Client\-generated request ID, a random UUID string

### **Body**

**custom_speaker_id ** `string` 新增

Custom voice ID. Only **post\-paid** voices are supported. For information about ordering and using post\-paid voices, see: [Voice Clone Order and Usage Guide](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication)

> **Important**

> The first call to the TTS synthesis API is considered the point at which the custom voice ID is officially activated, and the **voice slot fee will be charged**. Please make sure you are satisfied with the voice quality **before proceeding with actual synthesis**.

1. **Parameter Format**

When using a custom voice, `speaker_id` must be set to the fixed value `custom_speaker_id`. The actual custom voice ID should be specified in `custom_speaker_id`:

```JSON
{
  "speaker_id": "custom_speaker_id",    // Must be the fixed value
  "custom_speaker_id": "custom_zh_xxx"  // Custom voice ID
}
```

2. **Naming Requirements**

* **Character and length:**  8\-256 characters. Only digits, uppercase and lowercase letters, hyphens (`-`), and underscores (`_`) are supported.

* **Start and end characters:**  The ID must start with an English letter. Neither the first nor the last character can be a hyphen (`-`) or underscore (`_`).

* **Uniqueness:**  The ID must be unique within the same accountID.

* **Conflict prevention:**  The ID must not conflict with official system voice IDs. The system automatically blocks certain reserved prefixes, such as `S_` and `MIX_`, and suffixes, such as `_tob` and `_streaming`.

* **Regular expression validation:**  If your custom voice ID matches any of the following regular expressions on a regex validation website, it will be rejected by the system, indicating that it either conflicts with an official voice ID or does not meet the required format:

```Go
`^((?i:S_|ICL_|MIX_|DiT_|BV)|[a-z]{2}_|(?i:(wvae|moon|mercury|venus|earth|mars|jupiter|saturn|uranus|neptune|pluto|umm)_)).*|.*_(?i:bigtts|bigtts_cc|tob|cs_tob|streaming)$|^[^a-zA-Z]|.*[-_]$|^.{0,7}$|^.{257,}$|.*[^a-zA-Z0-9_-].*`
```

**speaker_id ** `string` 必选

Unique voice ID. See [Obtain Speaker ID](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication#1en9gleI) for details

**audio ** `objct` 必选

Supported audio formats: `wav`, `mp3`, `ogg`, `m4a`, `aac`, and `pcm`.

Maximum file size: 10 MB.

**Note**：

* Suggested audio duration: 10–15 seconds.

* `pcm` supports 24 kHz, mono only

**data ** `string` 必选

Raw audio bytes encoded as base64.

**format ** `string`

Audio format. Required when the input is `pcm` or `m4a`. Optional for other formats

**text ** `string`

Optional reference text. The user is expected to read this text aloud, and the service compares the audio against it. An error will be returned if the discrepancy is too large.

**Note:**  The prompt must be in the same language as the text. Cross\-lingual voice cloning and synthesis are not supported.

**language ** `int`

We recommend setting this field, as it determines the language of the demo audio. A voice registered through this API can be reused across multiple products, each supporting a different set of languages.

**Voice Replication 2.0 ** supports the following languages. The audio content must match the selected language.

* `zh = 0`: Chinese (default)

* `en = 1`: English

* `ja = 2`: Japanese

* `es = 3`: Spanish

* `id = 4`: Indonesian

* `pt = 5`: Portuguese

* `de = 6`: German

* `fr = 7`: French

* `ko = 8`: Korean

* `it = 9`: Italian

* `th = 10`: Thai

* `vi = 11`: Vietnamese

* `ru = 12`: Russian

* `fil = 13`: Filipino

* `ms = 14`: Malay

* `ar = 15`: Arabic

* `mx = 16`: Mexican Spanish

* `pt-br = 17`: Brazilian Portuguese

* `pl = 19`: Polish

* `tr = 20`: Turkish

* `sv = 21`: Swedish

**extra_params** `object`

**disable_volume_normalization ** `bool`

Whether to disable volume normalization. `false`: keeps the synthesized audio at a consistent volume.

`true`:the output more closely matches the volume of the prompt audio, improving prompt similarity.

Default: `false`

**demo_text ** `string`

Text used to generate the demo (preview) clip.

If `language` is specified, this text must be written in that language, otherwise synthesis will fail.

Length: 4–80 characters.

### **Response**

**X\-Tt\-Logid ** `string`

The logid is returned by the server. We recommend reading and logging this value to make troubleshooting easier.

**code** `int`

Status code of the request.On failure, the HTTP status will be non\-200.

See the [error code reference](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-error-code-reference) for details.

**message ** `string`

Status message of the request. When training fails, a description on failure will be returned.

**available_training_times** `int`

Remaining training quota.

**create_time ** `int`

Creation timestamp.

**language ** `int`

Language enum value:

* `zh = 0`: Chinese (default)

* `en = 1`: English

* `ja = 2`: Japanese

* `es = 3`: Spanish

* `id = 4`: Indonesian

* `pt = 5`: Portuguese

* `de = 6`: German

* `fr = 7`: French

* `ko = 8`: Korean

* `it = 9`: Italian

* `th = 10`: Thai

* `vi = 11`: Vietnamese

* `ru = 12`: Russian

* `fil = 13`: Filipino

* `ms = 14`: Malay

* `ar = 15`: Arabic

* `mx = 16`: Mexican Spanish

* `pt-br = 17`: Brazilian Portuguese

* `pl = 19`: Polish

* `tr = 20`: Turkish

* `sv = 21`: Swedish

**speaker_id ** `string`

Unique voice identifier.

**status ** `int`

Training status. TTS can be invoked when status is `2` or `4`.

**speaker_status**`object list`

**model_type ** `int`

For Voice Replication 2.0：`model_type = 5`

**demo_audio ** `string`

Returned when the status is Success. The URL is valid for one hour, download the audio if you need it.
