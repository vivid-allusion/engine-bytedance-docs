---
title: "Live Streaming Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113690"
---

Video interaction is common in pan\-entertainment socializing, including interactive live streaming in big showrooms, interactive live streaming for e\-commerce, and live streaming of cultural and artistic events. After the host creates a live streaming room, they can conduct talent shows, instructional programs, etc. in the room to attract audiences and receive gifts and rewards from audiences. The host can also initiate co\-hosting with other hosts online for "Player Killing" (PK) interaction across live streaming rooms, or with the audiences in the room. In addition, the host can open a video chat room to engage audiences through real\-time audio and video interaction. During the interaction, adding beautification effects, playing background music, or doing karaoke to make interactions more entertaining are supported. In addition, texts and emojis in live chat can be sent.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/docs/12/docs-257549). There are usually the following 3 roles in a video interaction during live streaming:


* Host: The user who creates the live streaming room. They can do a live stream by themselves or initiate live interaction with other hosts or audiences.

* Audience: The user who enters the room to watch live streaming. They can request to join the stream as a guest.

* Guest: When an audience member becomes a guest, they can be seen and heard by everyone else in the room.


<span id="how-to-play"></span>
## How to Play


* PK across rooms: After a live streaming has started, the host initiates a cross\-room PK with the hosts in other rooms. The number of gifts from audiences will be tied to a PK health bar. This feature is designed to boost the overall revenue of the live streaming room.

* Co\-hosting —make friends or find a date: After an audience member becomes a guest, they can interact with the host or other guests. The setting can be modified to create a room for making friends or finding a date by configuring guest permissions and adjusting the UI layout.

* Mini\-games: The host can load various mini\-games (such as whack\-a\-mole, draw\-and\-guess) into the live streaming room to increase appeal, enrich the interaction with the audiences, and increase the time audiences spend in the room.

* Music: The host can use the music widget to showcase talents in the room or entertain audiences through song requests, which enhances revenue. Background music can also be played to enhance the atmosphere in the live stream room.

* Smart beautification effects: Not only can users try out various beautification effects, filters, and stickers, but the host or guest can also use the recognition feature to trigger a wide variety of video effects through expressions and gestures such as blinking, pouting, making the heart gesture or OK gesture, arm swinging, and squatting. This allows users to enhance their appearance and makes video interaction more fun.


<span id="technical-structure"></span>
## Technical structure

RTC provides two solutions for live streaming:


* [Interactive Live Streaming](https://docs.byteplus.com/en/docs/12/docs-152574):This use case uses RTC to achieve features of live streaming and co\-hosting, but audiences traditionally subscribe to streams from CDN to watch a live stream.

* [Interactive Video Streaming](https://docs.byteplus.com/en/docs/12/docs-113691): This solution uses RTC to achieve features of live streaming and co\-hosting instead of using CDN. Synchronization between the audience and the host is optimal and there is minimal delay, ensuring a smooth transition when an audience member becomes a guest or returns to being an audience member.


<span id="feature-list"></span>
## Feature list


|Main feature |Description |
|---|---|
|Live streaming |After the host creates a live streaming room, they can start a solo live stream. |
|Live PK between hosts |Host A and host B connect for live PK interaction. Audiences can watch the real\-time interaction of multiple hosts in the original live room. During the connection, a host can mute other guests so that audiences in that room cannot hear them. |
|Guest |The host invites audiences to be guests, or audience members can apply to become guests. After an audience becomes a guest, they can interact with the host through audio and video. |
|Guest seat management |The host can manage the guest seats in their room, such as inviting an audience to be a guest, removing a guest from the stream, and blocking a user. |
|Smart beautification effects |Including skin smoothing, big eyes and other beautification effects, AR effects, 2D/3D stickers, gesture recognition, expression recognition, and motion recognition for triggering video effects. |
|Device management |In the room, users can turn on/off the camera and microphone, and switch between the front and rear lenses. |
|Network status detection |Check the network quality of the host and guest during live streaming. If network quality is poor, a prompt is sent to the user. |


<span id="advantages"></span>
## Advantages


* **Ultra\-low latency for smooth transitions between audience and co\-host roles**

   Compared with CDN live streaming, this solution offers an ultra\-low latency video experience for live audiences. The video streamed by a host is synchronized with audiences' screens at the millisecond level, outperforming the second\-level latency experience offered by CDN live streaming. In addition, the audience enjoys a smooth video experience without the video skipping forward or backward when transitioning between audience and co\-host roles.

* **Optimized for this Business Scenario**

   With advanced video capabilities, we support 48 kHz full\-band sampling, providing 3A\-specific optimization for real\-time scenarios and Ultra HD videos. The solution uses advanced codec policies and algorithms such as Simulcast, SVC, ROI, and super resolution.

   The solution supports multiple adaptation strategies, including distributing parameter configurations for different scenarios, segmenting users by room size, and adapting to various devices, regions, and network conditions to ensure a high\-quality experience.

* **Global High\-quality Network Coverage with High Concurrent Capacity**

   Our network has over 300 nodes worldwide, providing a global latency of 400 ms with a compliance rate of 99.5% or higher. In Southeast Asia, the Middle East, South Africa, and other overseas areas with poor infrastructure, dedicated network access and scheduling optimization are provided. Within China, full coverage of small\- and medium\-sized carriers as well as third\-tier and fourth\-tier cities.

   The network features an elastic and scalable design, 100% traffic redundancy, automatic expansion within minutes, and theoretically unlimited concurrency.

* **Smooth Experience for Weak Networks, 80% Anti\-packet Loss Capability**

   The real\-time, accurate network prediction and adaptive congestion control strategy ensures seamless recovery from up to 50% packet loss. A smooth audio and video experience can be maintained even with packet loss of up to 80%. Through the application of weak network strategies such as FEC, ARQ, HARQ, adaptive jitter buffer, and adaptive bitrate delivery, the end\-to\-end audio and video QoE can be optimized.
