---
title: "What is BytePlus RTC？"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-66812"
---

BytePlus Real\-Time Communication (RTC) is a global service that provides highly reliable, low\-latency audio and video capabilities for your applications.

By integrating the BytePlus RTC SDK, you can quickly build features like one\-to\-one or group video calls, interactive live streaming, online classes, and virtual meetings, supporting scenarios from social entertainment to cloud gaming.

<span id="product-architecture"></span>
## Product Architecture

You can easily integrate the RTC service provided by BytePlus RTC in both your client application and your server\-side application:


* Client side: [Integrate Client SDKs](https://docs.byteplus.com/en/docs/12/docs-70019) on platforms including Android, iOS, macOS, Windows, Web, mini programs and Electron to enable various types of audio & video functions.

* Server side:

   * Call [OpenAPI](https://docs.byteplus.com/en/docs/12/docs-overview) to launch HTTP requests, which allows you to create a room, query room status, start cloud recording, and distribute configuration from the backend server. The audio & video streams and signaling are transmitted via the WTN real\-time transmission network.

   * The [Console](https://docs.byteplus.com/en/docs/12/docs-70065) is both a control center and a dashboard that enables full\-lifecycle quality monitoring, tracing, and analysis of audio & video calls. It can help troubleshoot, identify and locate issues and provide timely solutions. In addition, the console offers client application management, cloud media processing configuration, and shows usage statistics.


You can use BytePlus RTC alongside other products like [BytePlus MediaLive](https://docs.byteplus.com/en/byteplus-media-live) and [BytePlus VOD](https://docs.byteplus.com/en/byteplus-vod). The architecture is shown in the following picture:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b28d1c48a420fb7b432341ad878d7e83.png) </span>

<span id="basic-concepts"></span>
## Basic Concepts

<span id="room"></span>
### Room

Users can only participate in the same audio or video call and interact with each other after joining the same room.

<span id="user"></span>
### User

Users are participants of the audio & video calls.


* Users inside a room belong to different roles according to business scenarios. Roles define what users can do in the room. For example, the room owner can start a call and have control over the room, while other users can speak and interact.

* Users in a room can switch their roles according to their needs.


<span id="stream"></span>
### Stream

A stream is a continuous flow of audio and video data that is collected, encoded, and transmitted over a network for playback.

<span id="push"></span>
### Push

To push local audio & video streams to the remote end. Refer to [Publish](https://docs.byteplus.com/en/docs/12/docs-70120#publish).

<span id="pull"></span>
### Pull

To pull remote audio & video streams to the local end. Refer to [Subscribe](https://docs.byteplus.com/en/docs/12/docs-70120#subscribe).

<span id="push-to-cdn"></span>
### Push to CDN

Mix the audio & video streams from one or multiple rooms into a single stream, push it to an RTMP server via a real\-time messaging protocol, and then distribute it through CDN.

<span id="peer-to-peer-message"></span>
### Peer\-to\-peer Message

Messages sent and received from one user to another.

<span id="broadcasting-message"></span>
### Broadcasting Message

Messages sent from the server to all users in a room.

You can learn more in [Glossary](https://docs.byteplus.com/en/docs/12/docs-70120).

<span id="compatibility"></span>
## Compatibility


|Platform |Environment requirement |Architecture |
|---|---|---|
|iOS |* iPhone or iPad running iOS 11.0+<br><br>* Xcode 14.1+ |iOS Simulator x86_64<br><br>arm64 real iOS device |
|Android |* Android 4.4 (API level 19)<br><br>* Android Studio 3.5+ (recommended) |arm64\-v8a real Android device<br><br>armeabi\-v7a real Android device<br><br>x86 Android Emulator<br><br>x86_64 Android Emulator |
|macOS |* macOS 10.13+<br><br>* Xcode 9.0+ |arm64<br><br>x86_64<br><br>Simulators are not supported. |
|Windows |* Windows 7+<br><br>* Visual Studio 2017<br><br>* .NET Framework 4.0+ |x86<br><br>x86_64 |
|Linux |* glibc 2.27+ |arm64<br><br>armhf<br><br>x86_64 |
|Web |See [Compatibility for RTC Web SDK](https://docs.byteplus.com/en/docs/12/docs-111854) |<br>---<br><br> |
|Flutter |* Flutter 2.0.0+<br><br>* Dart 2.12.0+<br><br>* Android 4.4+ (SDK API Level 19+), iOS 11.0+ |Simulators are not supported. |


<span id="why-byteplus-rtc"></span>
## Why BytePlus RTC

<span id="audio-processing"></span>
### Audio Processing

BytePlus RTC has an industry\-leading 3A algorithm that can achieve 48kHz high\-quality full\-duplex echo cancellation. With automatic noise suppression and automatic gain control using ultra\-low computational machine learning algorithms, it can achieve better results with lower power consumption.

<span id="device-adaptation"></span>
### Device Adaptation

BytePlus RTC adapts to over 40,000 device models and implements differentiated video capture/encoding strategies according to device performance. Over 90% of devices support RTC hardware encoding and decoding (calculated by actual call duration).

<span id="video-quality"></span>
### Video Quality

BytePlus RTC uses the H.265 encoder and supports advanced encoding strategies like Simulcast, SVC, ROI, and automatic bitrate. It also features advanced image quality enhancement algorithms, including super\-resolution, video noise reduction, and low\-light enhancement. The service can provide different video resolutions to match device performance. Mobile devices support up to 1080p, PCs support up to 4K, and VR devices support up to 8K.

<span id="accessibility-and-usability"></span>
### Accessibility and Usability

BytePlus RTC supports unitized deployment that enables rapid expansion within minutes. Each city has two data centers with multiple redundant routes to ensure reliable transmission. It complies with the SLA service level agreement, with a service availability of no less than 99.9%.

<span id="low-latency"></span>
### Low Latency

BytePlus RTC is based on a global transmission network that ensures an end\-to\-end latency of less than 400 ms for over 99.5% of users, with an average server\-side latency under 50 ms.

<span id="automatic-adaptation"></span>
### Automatic Adaptation

BytePlus RTC implements strategies such as FEC, ARQ, HARQ, Jitter Buffer, and adaptive bitrate distribution, allowing for imperceptible recovery from 50% packet loss and resistance to up to 80% packet loss. It supports content\-adaptive encoding, which can automatically adjust the bitrate based on real\-time feedback on online video clarity. Additionally, it uses the VICC intelligent congestion control algorithm to automatically adapt to different network conditions, business preferences, and bitrates.

<span id="dynamic-adaptation"></span>
### Dynamic Adaptation

BytePlus RTC supports an intelligent flow control protocol, which can meet the personalized needs of audio & video subscribers. It automatically adjusts audio and video stream configurations in response to changing network conditions and device performance.

<span id="use-cases"></span>
### Use Cases

BytePlus RTC supports the distribution of parameter configurations for different use cases, and takes various strategies based on user scales, devices, regions, and networks.

<span id="effective-integration"></span>
### Effective Integration

BytePlus RTC provides a set of well\-designed APIs that are ready and easy for developers to adopt. RTC can be integrated into new projects within two weeks on average. The streamlined SDK packages have a low memory footprint and CPU usage, and can be used to build applications across multiple platforms.

<span id="scale-and-capacity"></span>
### Scale and Capacity

BytePlus RTC allows 1000+ concurrent speakers in one single room, over 20 times higher than that of traditional RTC providers, and has no limits on the number of viewers.

<span id="edge-cloud-integration-in-pushing"></span>
### Edge\-cloud Integration in Pushing

BytePlus RTC is one of the first providers to apply edge\-cloud integration in pushing live streams. It will automatically switch to the suitable pushing strategies according to the devices, scenarios and network status, thus making videos clearer and more stable.

<span id="integration-with-various-products"></span>
### Integration with Various Products

BytePlus RTC integrates with other products including BytePlus VOD, BytePlus MediaLive and functions including beauty effects, ASR and AI technology to provide customers with comprehensive solutions for various RTC scenarios.

<span id="security-regulations"></span>
### Security Regulations

BytePlus RTC provides end\-to\-end encryption and data isolation. It operates in compliance with the General Data Protection Regulation (GDPR) and the California Consumer Privacy Act (CCPA).

<span id="features-and-scenarios"></span>
## Features and Scenarios

<span id="basic-features"></span>
### Basic Features


|Features |Description |Scenarios |
|---|---|---|
|Audio Calls |One\-on\-one voice calls and group audio calls with 48kHz full\-bandwidth sampling and advanced 3A processing algorithm |* [Chatting Room](https://docs.byteplus.com/en/docs/12/docs-117919)<br><br>* [Game Room](https://docs.byteplus.com/en/docs/12/docs-136527) |
|Video Calls |One\-on\-one video calls and [group video calls](https://docs.byteplus.com/en/docs/12/docs-154376) with a video resolution of up to 1080p and leading encoding and decoding algorithms |Online conference |
|Live Streaming |Allows for 1,000 broadcasters and 100,000 viewers in a single room, with a median first frame duration of less than 300ms |* [Watch LIVE Together](https://docs.byteplus.com/en/docs/12/docs-153586)<br><br>* Online class |


<span id="advanced-features"></span>
### Advanced Features


|Features |Description |Scenarios |
|---|---|---|
|Interactive Livestreaming |Hosts interact with the audience or other hosts smoothly |* [Chatting Room](https://docs.byteplus.com/en/docs/12/docs-117919)<br><br>* [Game Room](https://docs.byteplus.com/en/docs/12/docs-136527)<br><br>* Online class |
|[Push to CDN](https://docs.byteplus.com/en/docs/12/docs-69821) |Mix multiple media streams from one or more rooms into a single stream, push it to an RTMP server, and then distribute it through a CDN |Scenarios that require audiences outside the room to watch the audio & video interaction:<br><br><br>* Interactive livestreaming<br><br>* Sharing online class |
|Room Background Music |Play background music in the live room |Online KTV |
|Audio Effects |Send some special audio effects, such as laughter, cheers and applause to enhance the audio experience |Online KTV |
|[AI Noise Cancellation](https://docs.byteplus.com/en/docs/12/docs-148647) |Use AI algorithms to reduce non\-static noise |Noise\-sensitive scenarios:<br><br><br>* Online conference<br><br>* Online class |
|[Simulcasting](https://docs.byteplus.com/en/docs/12/docs-70139) |Encode and transmit both high\- and low\-definition streams, which the receiving end automatically subscribes to based on network conditions |* Live streaming<br><br>* Online class |
|[Screen Sharing](https://docs.byteplus.com/en/docs/12/docs-70144) |Share certain areas of the screen, a designated tab, or a whiteboard with remote users while the camera is on |* Online conference<br><br>* Online class |
|[Custom Video Capturing and Rendering](https://docs.byteplus.com/en/docs/12/docs-96197) |Set customized devices to capture and render videos to meet diversified needs |Audio capture and rendering modules already exist in your audio & video applications<br><br><br>* You want to do some pre\-transmission processing on the captured audio & video data<br><br>* Your audio capture device is already in use. |
|[Cloud Recording](https://docs.byteplus.com/en/docs/12/docs-115526) |Start cloud recording with OpenAPI and upload the recorded videos to designated platforms for storage |Scenarios that require preserving audio & video calls |


<span id="extended-features"></span>
### Extended Features


|Features |Description |Scenarios |
|---|---|---|
|[Beauty Effects](https://docs.byteplus.com/en/docs/12/docs-372605) |Integrate with BytePlus Effects to enable basic and advanced effects |* [Watch LIVE Together](https://docs.byteplus.com/en/docs/12/docs-153586)<br><br>* Live streaming |
|[Spatial Audio](https://docs.byteplus.com/en/docs/12/docs-93903) |A powerful 3D audio technology that enables a more immersive and realistic audio experience by accurately reproducing sound in three\-dimensional space |Scenarios that prefer 3D sound effects:<br><br><br>* Gaming<br><br>* VR application |
|Sound Attenuation |Adjust the sound output based on the listener's position |Games like PUBG or other battle royale titles. |
|[Virtual Background](https://docs.byteplus.com/en/docs/12/docs-97293) |Separate the user from their background using AI algorithms. |Scenarios that require virtual backgrounds:<br><br><br>* Live streaming<br><br>* Online conference<br><br>* Online class |
|[Supplemental Enhancement Information (SEI)](https://docs.byteplus.com/en/docs/12/docs-70140) |Send SEI with audio & video frames so that the information can be presented with the frames without latency |* Present lyrics in online KTV<br><br>* Position the PK progress bars |
|AI Technology |One\-stop solutions for AI implementation. Recognition of facial expressions, hand gestures, attention, and speaking durations can empower online education and entertainment. |* Live streaming<br><br>* Audio & video calls |
