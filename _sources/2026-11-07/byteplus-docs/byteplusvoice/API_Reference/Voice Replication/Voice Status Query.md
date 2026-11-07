---
title: "Voice Status Query"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-status-query"
---

Queries the training status of a cloned voice

## Request

**Request Path**

POST `https://voice.ap-southeast-1.bytepluses.com/api/v3/tts/get_voice`

### **Header**

**Content\-Type ** `string` 必选

The media type of the request body. Must be set to `application/json`

**X\-Api\-Key ** `string`  必选

API Key can be obtained from [Byteplus Console](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default).

**X\-Api\-Request\-Id ** `string` 必选

Client\-generated request ID, a random UUID string

### **Body**

**custom_speaker_id ** `string` ** ** 新增

Custom voice ID. Only **post\-paid** voices are supported. For information about ordering and using post\-paid voices, see: [Voice Clone Order and Usage Guide](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication)

```JSON
{
  "speaker_id": "custom_speaker_id",    // Must be the fixed value
  "custom_speaker_id": "custom_zh_xxx"  // Custom voice ID
}
```

**speaker_id ** `string` 必选

Unique voice identifier. See [Obtain Speaker ID](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication#1en9gleI) for details

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
