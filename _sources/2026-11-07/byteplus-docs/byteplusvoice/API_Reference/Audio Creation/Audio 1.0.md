---
title: "Audio 1.0"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01"
---

A non\-streaming audio generation API based on HTTP. It supports uploading multiple reference audio clips or images to generate audio, and lets you describe the desired sound effects, timbre, and more in natural language. Ideal for audiobooks, voiceovers, gaming, and similar scenarios. Currently supports audio output up to 120 seconds.

<span id="hR1Aoi6r"></span>
## Request

**Request Path**

`https://voice.ap-southeast-1.bytepluses.com/api/v3/tts/create`


**Header**


**X\-Api\-Key** `string` <span data-api-tag="require|iLAr2X">必选</span>

API Key can be obtained from [Byteplus Console](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default).



**X\-Api\-Request\-Id** `string`

Client\-generated request ID, a random UUID string




**Body**


**model** `string` <span data-api-tag="require|oZCI3H">必选</span>

Model version identifier.

Value:


`seed-audio-1.0` <span data-label="purple">Upgraded</span>


* Supports `English` `Chinese` `Japanese` `Korean` `Mexican Spanish` `Indonesian` `German` `Brazilian` `Portuguese` `French` `Thai` `Vietnamese` `Malay` `Filipino` `Italian` `Russian` `Dutch` `Polish` `Turkish` `Swedish` `Castilian Spanish`

* Supports timing control




**text_prompt** `string` <span data-api-tag="require|xbMpCI">必选</span>

The prompt used to synthesize audio, or the text to be synthesized. Up to 3000 characters.


* **Text\-only generation**: Audio is generated from the prompt in `text_prompt`.

* **Reference\-audio generation**: Use `@AudioN` to reference the audio at the corresponding position in references. Numbering starts at 1 in upload order, i.e. the first reference audio is `@Audio1`, the second is `@Audio2`, and so on.

* **Reference\-image generation**: When using an image reference, `text_prompt` can contain only the text to be synthesized.



**references** `array`

List of reference resources. The generation mode is matched automatically based on what you pass in:

**Notes:** 


* **Text\-only generation**: Pass no reference resources; audio is generated from the prompt in `text_prompt`.

* **Reference\-audio generation**: Pass audio references to generate audio from both the reference audio and the prompt in `text_prompt`. The audio can be specified by a `Speaker` ID.

* **Reference\-image generation**: Pass an image reference to generate audio from the text to be synthesized in `text_prompt`.

* The order of the audio clips corresponds to the `@AudioN` numbering in the prompt: the first clip is `@Audio1`, and so on.

* Up to three reference audio clips are supported. Each clip can be up to 30 seconds and no larger than 10 MB. Supported formats: `wav`/`mp3`/`pcm`/`ogg_opus`.

* Only one reference image is supported, no larger than 10 MB. Supported formats: `jpeg`/`png`/`webp`.



**speaker** `string`

Speaker ID. You can use a [TTS2.0](https://docs.byteplus.com/en/docs/byteplusvoice/voicelist) voice or a cloned voice.

**Note**: Provide exactly one of `speaker`, `audio_data`, or `audio_url`.



**audio_data** `string`

Base64\-encoded reference audio.

**Note**: Provide exactly one of `audio_data`, `speaker`, or `audio_url`.



**audio_url** `string`

Reference audio URL. Use this to reference remote audio.

**Note**: Provide exactly one of `audio_url`, `speaker`, or `audio_data`.



**image_data** `string`

Base64\-encoded reference image.

**Note**:


* Provide either this parameter or `image_url`, but not both.

* Image references cannot be mixed with audio references, i.e. `image_data` cannot be used together with `audio_data`, `audio_url`, or `speaker`.



**image_url** `string`

Reference image URL.

**Note**:


* Provide either this parameter or `image_data`, but not both.

* Image references cannot be mixed with audio references, i.e. `image_url` cannot be used together with `audio_data`, `audio_url`, or `speaker`.




**audio_config** `object`

Output audio configuration.


**format** `string`

Output format: `wav`/`mp3`/`pcm`/`ogg_opus`.

Default `wav`.



**sample_rate** `int`

Output sample rate.

Default: wav,pcm:`40000`; mp3: `44100`

Values: [`8000`, `16000`, `24000`, `32000`, `44100`, `48000`].



**speech_rate** `int`

Speech rate.

Range [`-50`, `100`]: `100` means 2.0x speed, `-50` means 0.5x speed.

Default：`0` (rate unchanged).



**loudness_rate** `int`

Volume.

Range [`-50`, `100`]: `100`

means 2.0x volume, `-50` means 0.5x volume.

Default: `0` (volume unchanged).



**pitch_rate** `int`

Pitch.Higher values result in a higher pitch.

Range [`-12`, `12`].

Default `0` (pitch unchanged).



**enable_subtitle** `bool`

**Whether to enable the subtitle service.**  When enabled, the response includes word\-level timestamps.

Values: `true`, `false`

Default: `false`




**watermark** `object`

Watermark configuration


**aigc_watermark** `bool`

Explicit watermark switch. Adds an audio rhythm marker at the end of the synthesized audio.

Default: `False`



**aigc_metadata** `object`

Implicit watermark. Adds metadata to the synthesized audio header.


**enable** `bool`

Whether to enable the implicit watermark.

Default: `False`.



**content_producer** `string`

Name or code of the synthesis service provider.



**produce_id** `string`

Content production ID.



**content_propagator** `string`

Name or code of the content distribution service provider.



**propagate_id** `string`

Content distribution ID.






**Response**


**code** `int`

Status code of the request



**message** `string`

Status message of the request.



**audio** `string`

Synthesized audio data, Base64\-encoded.



**duration** `float`

Duration of the post\-processed audio (in seconds).

Notes:


* It may differ from `original_duration` when speed adjustment or post\-processing is applied;

* billing is based on `original_duration`.



**original_duration** `float`

Duration of the model's original output audio (in seconds). This is also the duration used for billing, with a maximum of 120s.



**url** `string`

Audio URL with an expiration time.Valid for 2 hours.



**subtitle** `object`

**Subtitle information for the audio.**  This field is present only when audio_config.enable_subtitle is set to true.


**text** `string`

Subtitle text corresponding to the audio.



**sentences** `object list`

Utterance\-level subtitle information.


**start_time** `int`

The start time of the utterance, in milliseconds from the beginning of the audio.



**end_time** `int`

The end time of the utterance, in milliseconds from the beginning of the audio.



**text** `string`

The complete text of the utterance.



**words** `object list`

Word\-level subtitle information.


**start_time** `int`

The start time of the word, in milliseconds from the beginning of the audio.



**end_time** `int`

The end time of the word, in milliseconds from the beginning of the audio.



**text** `string`

The complete text of the word.
