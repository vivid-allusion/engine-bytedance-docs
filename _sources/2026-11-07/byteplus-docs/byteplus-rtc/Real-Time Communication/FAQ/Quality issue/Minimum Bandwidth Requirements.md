---
title: "Minimum Bandwidth Requirements"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1155371"
---

<span id="question"></span>
## Question

What's the requirements on network bandwidth for an audio/video call?

<span id="answer"></span>
## Answer

<span id="calculation-of-the-minimum-bandwidth"></span>
### Calculation of the minimum bandwidth

We only provide the calculation method without considering any other factors that may consume the bandwidth. In actual use, the same network may be used by other users, resulting in the requirement of a larger network bandwidth. Therefore, it is recommended to leave a certain amount of bandwidth margin to ensure a better audio/video call experience.


* The minimum upstream bandwidth = Bitrate of locally sent audio + Bitrate of locally sent video

* The minimum downstream bandwidth = Bitrate of audio sent from the remote user 1 + Bitrate of video sent from the remote user 1 + … + Bitrate of audio sent from the remote user N + Bitrate of video sent from the remote user N


<span id="value-of-audio-video-bitrate-in-the-calculation"></span>
### Value of audio/video bitrate in the calculation

The **audio** bitrate is determined by the parameter set in [setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70095#setaudioprofile), which is typically between 16kbps and 48kbps.

The **video** bitrate is determined by the parameter set in [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideoencoderconfig-2), or refers to the default bitrate corresponding to each resolution level in [Setting Video Encoder Configuration](https://docs.byteplus.com/en/docs/12/docs-70122).

<span id="example"></span>
### Example


* **1v1 audio/video call**: If both parties in the call are using the default audio profile with the bitrate being 16kbps, and setting the resolution to 1280\*720 and the bitrate to 1200kbps, the recommended upstream/downstream bandwidth should be at least:

   (1200+16)kbps/1024 = 1.19mbps

* **1vN audio/video call**: The upstream bandwidth requirement remains essentially unchanged, while the downstream bandwidth needs to be increased exponentially based on the 1v1 requirement.
