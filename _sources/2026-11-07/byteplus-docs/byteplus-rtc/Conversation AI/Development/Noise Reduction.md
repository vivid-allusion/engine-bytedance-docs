---
title: "Noise Reduction"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1806620"
---

Background noise, such as air conditioners or background conversations, can interfere with voice activity detection and lower recognition accuracy. To mitigate these issues in noisy environments, you can either adjust the audio gain or enable AI noise suppression.

<span id=".6LCD5pW06Z-z6YeP5aKe55uK"></span>
## Adjust Audio Gain

Adjusting the gain of the audio sent to the server affects the signal\-to\-noise ratio. Lowering the gain reduces the overall captured volume, which can help filter out low\-level ambient noise. This method is best suited for environments with only faint, consistent background noise.

**How to configure:** 

When calling the [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163) API, set the `ASRConfig.VolumeGain` parameter.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Setting <code>VolumeGain</code> too low may cause the user's voice to be too quiet for accurate recognition.</div>


```json
  "ASRConfig": {
     "VolumeGain": 0.3 // Recommended value, default is 1.0
}
```


<span id=".YWkt6ZmN5Zmq"></span>
## Enable AI Noise Suppression

When background noise is more pronounced (e.g., air conditioners, fans, or keyboard clicks), enabling AI noise suppression is recommended. You can enable this feature either on the server or on the client.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Do not enable AI noise suppression on both the server and client simultaneously, as over\-processing can degrade audio quality.</div>


<span id=".5pa55byP5LiA77ya5pyN5Yqh56uvLWFpLemZjeWZqg=="></span>
### Method 1: Server\-Side Suppression

With this method, noise suppression is applied on the server. It is ideal for client devices with limited computing power (such as IoT or smart hardware) that cannot run suppression locally.

When calling the [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163) API, set the `AgentConfig.AnsMode` parameter.

```json
"AgentConfig": {
    "AnsMode": 2 // Select a mode based on the noise type
}
```


**Available Modes**


* `1`: **Mild**. Suitable for suppressing faint, steady background noise.

* `2`: **Medium**. Suitable for suppressing moderate steady noise, such as air conditioners and fans.

* `3`: **Heavy**. Suitable for suppressing loud, non\-stationary dynamic noise, such as keyboard clicks, object collisions, and animal sounds.


<span id=".5pa55byP5LqM77ya5a6i5oi356uvLWFpLemZjeWZqg=="></span>
### Method 2: Client\-Side Suppression

This method uses the noise suppression API built into the ByteRTC client\-side SDK. Note that the algorithm's effectiveness depends on the room profile you set when calling `joinRoom`.

For more information, see:


* Native: [4. Set noise cancellation mode](https://docs.byteplus.com/docs/byteplus-rtc/docs-1178327#_4-set-noise-cancellation-mode)

* Web: [AI Noise-Canceling Extension (Web)](https://docs.byteplus.com/docs/byteplus-rtc/docs-148647)
