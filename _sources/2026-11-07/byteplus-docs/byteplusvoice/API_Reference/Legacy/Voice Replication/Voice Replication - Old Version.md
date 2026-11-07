---
title: "Voice Replication - Old Version"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v1"
---

<span id="CL57DtV2"></span>
# Upload audio for voice replication training

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Starting from 2024.07.10, the Voice Replication ICL 1.0 effect is available. When calling the API, make sure to pass <code>model_type=1</code>. Additionally, if the original audio is not in Chinese, the <code>language</code> parameter must be specified.</div>


<div data-tips="true" data-tips-type="warning">Starting from 2025.04.30, the DiT (Diffusion Transformers) replication effect is available. It is better suited for non\-real\-time scenarios. Use <code>model_type=2</code> for the DiT Standard Edition Effect (voice tone does not preserve the user’s original style) and <code>model_type=3</code> for the DiT Restoration Edition Effect (voice tone preserves the user’s accent, speaking speed, and other speech characteristics).</div>


<span id="JJg8Em0W"></span>
## Training (Upload Interface)

**Domain:**  `https://voice.ap-southeast-1.bytepluses.com`

**Interface Path:**  `POST` `/api/v1/mega_tts/audio/upload`

**Interface Description:**  Submit audio for voice replication training.

**Authentication Method:**  Bearer Token; Add `"Authorization": "Bearer; {token}"` to the request header and fill in the corresponding appid in the request JSON.

Tip

Separate Bearer and the token value with a single space

Do not keep {} when replacing token

Information such as AppID/Token/Cluster can be found in the [Console Guide](https://docs.byteplus.com/en/docs/byteplusvoice/Speech_Console_Guide)

<span id="tYXorfu2"></span>
### Request Parameters

**Header:** 


|Parameter |Type |Required |Remarks |
|---|---|---|---|
|Authorization |string |✓ |Bearer;$ |
|Resource\-Id |string |✓ |volc.megatts.voiceclone |


**Body:** 


|Parameter |Level |Type |Required |Remarks |
|---|---|---|---|---|
|appid |1 |string |✓ | |
|speaker_id |1 |string |✓ |unique Speaker ID (voice replica identifier) |
|audios |1 |list |✓ |Supported audio formats: wav, mp3, ogg, m4a, aac, pcm.<br><br>pcm only supports 24k single\-channel.<br><br>Currently, the maximum single file upload size is 10MB, and only 1 audio file can be uploaded each time. |
|audio_bytes |2 |string |✓ |Binary audio bytes, which need to be base64 \- encoded |
|audio_format |2 |string | |Audio format. pcm and m4a must be passed, while others are optional |
|text |2 |string | |Allows users to recite according to this text. The service will compare the difference between the audio and the text. If the difference is too large, a 1109 WERError will be returned. |
|source |1 |int |✓ |Fixed value: 2 |
|language |1 |int | |When `model_type` is 1, the following languages are supported:<br><br><br>* cn = 0 Chinese (Default)<br><br>* en = 1 English<br><br>* ja = 2 Japanese<br><br>* es = 3 Spanish<br><br>* id = 4 Indonesian<br><br>* pt = 5 Portuguese<br><br><br>When `model_type` is 2 or 3, only the following languages are supported:<br><br><br>* cn = 0 Chinese (Default)<br><br>* en = 1 English |
|model_type |1 |int | |0 for mega effect (default, not recommended)<br><br>1 for ICL 1.0 effect<br><br>2 for DiT standard version effect (timbre, does not restore user style).<br><br>3 for DiT restoration version effect (timbre, restores user accent, speaking speed, etc.). |
|extra_params |1 |jsonstring | |Extra parameters<br><br>Default as "{}", which is a JSON string. |
|enable_audio_denoise |2 |bool | |Whether to enable noise reduction: enabling it may affect some voice details.<br><br>It is recommended to enable noise reduction for audio samples with high noise levels, and to disable it for high\-quality audio samples.<br><br>Default is `true` when `model_type` is 1, 2, or 3.<br><br>Python example:<br><br>`"extra_params": json.dumps({"enable_audio_denoise": False})` |
|voice_clone_denoise_model_id |2 |string | |Selection of the voice enhancement model: removes noise from the audio sample (may affect some voice details).<br><br>If the cloned result contains noticeable noise, you can try switching to different models to test for varying effects.<br><br>Default: `""` (`SpeechInpaintingV2` is the default when it's empty)<br><br>Options:<br><br><br>* `SpeechInpaintingV2` (default)<br><br>* `VocalDiffusionV2`<br><br>* `VocalDiffusionV2_44k`<br><br><br>Python example：<br><br>`"extra_params": json.dumps({"voice_clone_denoise_model_id": "SpeechInpaintingV2"})` |
|voice_clone_enable_mss |2 |bool | |Whether to use audio source separation to remove background sounds.<br><br>Default value: `false`<br><br>Python example:<br><br>`"extra_params": json.dumps({"voice_clone_enable_mss": False})` |
|enable_crop_by_asr |2 |bool | |Whether to use ASR\-based cropping.<br><br>ASR\-based cropping can prevent the pronunciation of a single character from being cut off. The core reason is that it can accurately locate the position of each character in the audio. In contrast, the default audio duration\-based cropping (with a duration of 25s) may result in the pronunciation of a single character being cut off.<br><br>Default value: `false`<br><br>Python example:<br><br>`"extra_params": json.dumps({"enable_crop_by_asr": True})` |


**JSON Sample**

```JSON
{
    "speaker_id": "S_*******", // Obtained from the console, refer to the Console Guide
    "appid": "your appid",
    "audios": [{
            "audio_bytes": "base64 - encoded audio",
            "audio_format": "wav"
    }],
    "source": 2,
    "language": 0,
    "model_type": 1,
    "extra_params": "{\"voice_clone_denoise_model_id\": \"\"}"
}
```


<span id="fiI5RLsK"></span>
### Return Data

**Body:** 


|Parameter |Level |Type |Required |Remarks |
|---|---|---|---|---|
|BaseResp |1 |object |✓ | |
|StatusCode |2 |int |✓ |Success: 0 |
|StatusMessage |2 |string | |Error message |
|speaker_id |1 |string |✓ |unique Speaker ID (voice replica identifier) |


**JSON Sample:** 

```JSON
{
    "BaseResp": {
        "StatusCode": 0,
        "StatusMessage": ""
    },
    "speaker_id": "S_*******"
}
```


<span id="vdDU337S"></span>
### **Return Code**


|**Message** |**Code** |**Remark** |
|---|---|---|
|Success |0 |Success |
|BadRequestError |1001 |Invalid request parameters |
|AudioUploadError |1101 |Audio upload failed |
|ASRError |1102 |ASR (speech\-to\-text) transcription failed |
|SIDError |1103 |SID voiceprint detection failed |
|SIDFailError |1104 |Voiceprint detection failed, voiceprint is too similar to a celebrity's |
|GetAudioDataError |1105 |Failed to obtain audio data |
|SpeakerIDDuplicationError |1106 |SpeakerID duplicate |
|SpeakerIDNotFoundError |1107 |SpeakerID not found |
|AudioConvertError |1108 |Audio transcoding failed |
|WERError |1109 |WER detection error, the word error rate between the uploaded audio and the request text is too high |
|AEDError |1111 |AED detection error, usually due to no speech in the audio |
|SNRError |1112 |SNR detection error, usually due to too low signal\-to\-noise ratio (poor audio quality from excessive background noise) |
|DenoiseError |1113 |Noise reduction failed |
|AudioQualityError |1114 |Low audio quality, noise reduction failed |
|ASRNoSpeakerError |1122 |No human voice detected |
|UploadCountLimitExceeded |1123 |Upload interface call limit reached. Currently, the same timbre supports 10 uploads. |


<span id="QqH65l00"></span>
## Status Query (Status Interface)

**Domain:**  `https://voice.ap-southeast-1.bytepluses.com`

**Interface Path:**  `POST` `/api/v1/mega_tts/status`

**Interface Description:**  Query the voice replication training status.

<span id="JAmwe8Ye"></span>
### Request Parameters

**Header:** 


|Parameter |**Type** |Required |Remarks |
|---|---|---|---|
|Authorization |string |✓ |Bearer;$ |
|Resource\-Id |string |✓ |volc.megatts.voiceclone |


**Body:** 


|Parameter |Level |Type |Required |Remarks |
|---|---|---|---|---|
|appid |1 |string |✓ | |
|speaker_id |1 |string |✓ |Unique voice identifier |


**JSON Sample:** 

```JSON
{
    "appid": "your appid",
    "speaker_id": "S_*******" // Obtained from the console, refer to the Console Guide
}
```


<span id="15KjNRNo"></span>
### Return Data

**Body:** 


|Parameter Name |Level |**Type** |Required |Remarks |
|---|---|---|---|---|
|BaseResp |1 |object |Required | |
|StatusCode |2 |int |Required |Success: 0 |
|StatusMessage |2 |string |Optional |Error message |
|speaker_id |1 |string |Required |Unique timbre identifier |
|status |1 |enum |Required |Training status.<br><br>When the status is 2 or 4, TTS can be called.<br><br><br>* NotFound = 0<br><br>* Training = 1<br><br>* Success = 2<br><br>* Failed = 3<br><br>* Active = 4 |
|create_time |1 |int |Required |Creation time |
|version |1 |string |Optional |Training version |
|demo_audio |1 |string |Optional |Returned when the status is Success; valid for 1 hour. Download and use it if needed. |


**JSON Sample:** 

```JSON
{
    "BaseResp": {
        "StatusCode": 0,
        "StatusMessage": ""
    },
    "create_time": 1701055304000,
    "version": "V1",
    "demo_audio": "http://**********.wav",
    "speaker_id": "S_*******",
    "status": 2
}
```


<span id="1v5Zm6lK"></span>
# Demo


<Tabs>
<Tab zoneid="Ka0sy0k1" title="Python Example">
<TabTitle>Python Example</TabTitle>

<span id="Zh1fI9Wx"></span>
### Precondition


* Before invoking, you need to obtain the following information:

   * : APP ID obtained using the console.

   * `<access_token>`: Access Token obtained using the console.


<span id="N4bj2yXU"></span>
## Download code example

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dfb6c4c6cbdb05d16366a1150ddbcc61.zip" name="Byteplus_TTS_VoiceReplication_python.zip">Byteplus_TTS_VoiceReplication_python.zip</Attachment>


&nbsp;

<span id="CaAXm7tq"></span>
### Unzip the code package and install dependencies

```Bash
mkdir -p Byteplus_TTS_VoiceReplication_python
tar xvzf Byteplus_TTS_VoiceReplication_python.zip -C ./Byteplus_TTS_VoiceReplication_python
cd Byteplus_TTS_VoiceReplication_python
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
pip install requests
```


<span id="fFQNuaGs"></span>
## Invoke

> At the end of the Python script `uploadAndStatus.py`:

> * `appid`: Your Byteplus application ID

> * `token`: Your access token

> * `spk_id`: Speaker ID for the timbre

> * `audio_path`: Path to your audio file


```Bash
python uploadAndStatus.py
```



</Tab>
</Tabs>
