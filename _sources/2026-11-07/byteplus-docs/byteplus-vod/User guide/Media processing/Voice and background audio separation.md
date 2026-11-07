---
title: "Voice and background audio separation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-voice-background-audio-separation"
---

BytePlus VOD voice and background audio separation, also known as audio separation or vocal and accompaniment separation, uses deep learning algorithms to accurately process the audio or video files that you provide. It outputs two independent audio files: clean vocal audio and complete background accompaniment. This feature is suitable for karaoke accompaniment production, voice enhancement in noisy environments, music replacement during video secondary creation, and similar scenarios.

This guide describes how to separate voice and background audio by calling the BytePlus VOD OpenAPI.

<span id="feature-introduction"></span>
## Feature introduction

Voice and background audio separation is based on advanced audio processing algorithms, such as deep learning and spectral analysis. The system analyzes audio signals across multiple dimensions, identifies and captures differences between voice and background audio in spectrum, time domain, timbre, and other aspects, and uses intelligent algorithm models to separate the two. During separation, the system preserves the integrity and audio quality of both voice and background audio as much as possible, ensuring that the separated vocal track is clear and intelligible and the background audio remains natural and smooth. This provides high\-quality audio materials for subsequent audio and video processing and applications.

<span id="use-cases"></span>
## Use cases


* **Voice enhancement and optimization**: For videos from complex sources, such as mobile phone life recordings, on\-site lecture recordings, and non\-professional podcast recordings, you can separate the voice track and then process it independently, such as increasing volume, improving audio quality, and reducing noise. This significantly improves voice clarity in the audio.

* **Voice cloning in video translation**: During video translation, you can use this feature to extract the original voice separately for voice cloning, preserving characteristics such as timbre and intonation. Combined with TTS technology, the translated text can then be converted into speech in the target language.

* **ASR optimization**: After extracting clean voice audio, you can use it for automatic speech recognition. This effectively reduces interference from background noise and other factors, improving overall ASR accuracy.

* **Video editing and secondary creation**: In video editing and secondary creation workflows, the separated voice and background audio can be processed independently, such as adjusting the volume of a dialogue segment or replacing the background music, making secondary creation more flexible and efficient.


<span id="capabilities-and-limits"></span>
## Capabilities and limits


|Item |Description |
|---|---|
|Input file formats |* Video formats: Mainstream video formats, including MP4, FLV, RM, RMVB, MPEG, MOV, AVI, MPEGTS, WMV, 3GP, TS, MPG, WEBM, MKV, WM, MP4V, M4V, F4V, and MXF.<br><br>* Audio formats: Mainstream audio formats, including MP3, M4A, WAV, ACC, WMA, AMR, OGG, and FLAC. |
|Output artifacts |* Vocal audio file in AAC format<br><br>* Background audio file in AAC format |


<span id="pricing"></span>
## Pricing

Using voice and background audio separation incurs the following fees:


* **Voice and background audio separation fees**: Charged based on the duration of the input source file. For details, see [Voice and background audio separation pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#voice-background-audio-separation-pricing).

* **Media asset storage fees**: The original video file that you upload for processing and the generated segment files are stored in your BytePlus VOD space. Storage fees are charged based on storage volume and duration. For details, see [Storage pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#storage-pricing).

* **Video distribution fees**: If you use BytePlus VOD CDN distribution acceleration to play or download generated videos, distribution acceleration fees are incurred. For details, see [Distribution acceleration pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#distribution-acceleration).


<span id="prerequisites"></span>
## Prerequisites


* Create a [BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console.

* Enable the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started) and create a space.

* [Upload audio or video files](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to the VOD space and obtain the Vid or FileName.


<span id="procedure"></span>
## Procedure

<span id="step-1-submit-a-voice-and-background-audio-separation-task"></span>
### Step 1: Submit a voice and background audio separation task

Call the [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-audio-separation) API to submit a voice and background audio separation task. The following are the key task parameters. For the complete request parameter list and detailed descriptions, see [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-audio-separation).


* `Input`: Specifies the input file.

   * `Type`: Set to `Vid` or `DirectUrl`.

   * `Vid` / `DirectUrl`: Provides the Vid or DirectUrl information of the file to process.

* `Operation.Task`: Defines the task to execute.

   * `Type`: Must be set to `AudioExtract`, indicating a voice and background audio separation task.

   * `AudioExtract.Voice`: Must be set to `true`, indicating that voice audio is extracted.


Request example:

```JSON
POST https://vod.byteplusapi.com?Action=StartExecution&Version=2025-07-01
{
  "Input": {
    "Type": "Vid",
    "Vid": "v006f2g00018***9k373ksl1sm3isoeg"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "AudioExtract",
      "AudioExtract": {
        "Voice": true,
        "AudioOption": {
          "Format": "aac"
        }
      }
    }
  }
}
```


After the task is submitted successfully, the system returns the unique task identifier `RunId`. Save this ID for later result queries.

<span id="step-2-get-the-task-result"></span>
### Step 2: Get the task result

After the task is submitted, the system processes it asynchronously in the background. You can get the result in either of the following ways:


* **Active query**: Call the [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution) API and pass in the `RunId` obtained in step 1.

   ```HTTP
   GET https://vod.byteplusapi.com?Action=GetExecution&Version=2025-07-01&RunId=hb:ebd05bee1f3873***f7316c742b5f
   ```
   

* **Event notification**:

   1. Refer to [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-) to configure a service address for receiving callbacks. When subscribing to events, select [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete).

   2. When the task is complete, your service receives an HTTP POST request whose `EventType` is `ExecutionComplete`.


When the returned `Status` value is `Success`, the task has completed successfully. You can find separated artifact information in `Output.Task.AudioExtract`. The following table describes the key artifact fields.


|Field |Type |Description |
|---|---|---|
|`Duration` |Float |The duration of the input file, in seconds. |
|`Voice` |Object |Information about the **vocal audio file**. |
|`Voice.FileName` |String |The storage path of the vocal audio file. |
|`Voice.Size` |String |The size of the vocal audio file, in bytes. |
|`Background` |Object |Information about the **background audio file**. |
|`Background.FileName` |String |The storage path of the background audio file. |
|`Background.Size` |String |The size of the background audio file, in bytes. |


The following is an example of a successful voice and background audio separation result:

```JSON
{
  "ResponseMetadata": {
    // ... Common metadata omitted
  },
  "Result": {
    "Input": {
      "Type": "Vid",
      "Vid": "v006f2g00018***9k373ksl1sm3isoeg"
    },
    "Operation": {
      "Type": "Task",
      "Task": {
        "Type": "AudioExtract",
        "AudioExtract": {
          "Voice": true,
          "AudioOption": {
            "Format": "aac"
          }
        }
      }
    },
    "Output": {
      "Type": "Task",
      "Task": {
        "Type": "AudioExtract",
        "AudioExtract": {
          "Duration": 107.90168,
          "Voice": {
            "Size": "1787924",
            "FileName": "2aa5293f1f83405b9c5efbf74647aaa5_audiospeech.aac"
          },
          "Background": {
            "Size": "1787924",
            "FileName": "2aa5293f1f83405b9c5efbf74647aaa5_background.aac"
          }
        }
      }
    },
    "RunId": "p0:e1a800c85b9b5***1b3e12f39bafee0f",
    "Status": "Success"
  }
}
```


<span id="step-3-get-audio-urls-based-on-filename"></span>
### Step 3: Get audio URLs based on FileName

In [Step 2: Get the task result](https://docs.byteplus.com/en/docs/25/112791#step-2-get-the-task-result), you obtained the FileName values of the output audio files. Next, convert them to public URLs for playback or download.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Before obtaining a public URL for a file, you <strong>must</strong> add and configure an acceleration domain name for the VOD space where the artifact is stored. All URLs are generated based on this domain name.</div>


A basic access URL consists of the following parts: `[Protocol]://[PlaybackDomain]/[FileName]`


* `[Protocol]`: Usually `https` or `http`, depending on whether you have configured an SSL certificate.

* `[PlaybackDomain]`: The acceleration domain name that you configured in the VOD console.

* `[FileName]`: The artifact `FileName` obtained from the `GetExecution` result.


Concatenation example: Assume that your acceleration domain name is `play.example.com` and the obtained vocal file `FileName` is `speech.aac`. The concatenated URL is `https://play.example.com/speech.aac`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To prevent hotlinking, BytePlus VOD supports URL signing. If URL signing is enabled in the VOD console, the basic URL cannot be accessed directly. You must append a dynamically calculated authentication parameter, such as <code>auth_key</code>.</div>



* <div data-tips="true" data-tips-type="tip"><strong>Generate authentication parameters</strong>: URL signing must follow a strict signature algorithm. For calculation methods and examples in different languages, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication">URL signing</a>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Complete URL example with authentication</strong>: <code>https://play.example.com/speech.aac?auth_key=1732529334-0-0-a1b2c3d4e5f6...</code></div>



<span id="related-api-documentation"></span>
## Related API documentation


* [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-audio-separation)

* [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution)

* [ExecutionComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-executioncomplete)
