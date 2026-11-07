---
title: "Diagnostic Tool"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-125643"
---

[Diagnostic Tool](https://console.byteplus.com/rtc/callQualityRTC/diagnosis) analyzes and helps troubleshoot quality issues of RTC calls by recording key events and monitoring metrics of each RTC call. Diagnostic Tool lists related metrics such as devices and network states.

When users report audio & video quality issues, such as silence or stall, you can use Diagnostic Tool to locate the time period during which the issue happened. To maintain call quality for critical events, you can use the Diagnostic Tool to promptly resolve issues by consulting the diagnosis report and related metrics.

<span id="features"></span>
## Features

The diagnostic tool has the following features:


* Locate important calls quickly

   You can locate the target RTC room by searching in the Filters under the Calls tab, based on metrics such as the number of online users and video stall rate.

* Monitor metrics of important calls

   To get a quick overview of an RTC room, check the Overview tab in Room Details. It shows room\-level events, such as users experiencing stalls. You can also view user statistics on the Dashboard tab.

* Call investigation

   In the Users tab in Room Details, you can view the events and key quality data of the call from the publisher's and the subscriber's perspective.

* Call diagnosis

   Diagnose problems at the user level and provide analysis reports.


<span id="user-details-and-metrics"></span>
## User details and metrics

Click on Details in the Users tab to troubleshoot and locate anomalies based on user events and metrics of devices and networks. Refer to the following section to understand how the events and data help you with troubleshooting.

<span id="user-details"></span>
### User Details

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a7a98396aea338689847023ac1f2f97a.png) </span>

Hover over the diagram to see the list of user events at that point. The events and related issues are described below:


* Getting device permissions: Users cannot start audio or video capture without obtaining access permission.

* Joining/Leaving the room: Users need to join a room before sending/receiving audio & video.

* User role: A user can publish audio and video streams only after joining the room.

* The first frame of audio/video sent: Start publishing the media stream.

* Audio route switching: When a headset is connected, the audio output automatically switches to it, and the device's speaker or earpiece is muted.

* Network switching: When the network drops to 3G or 2G, the quality of audio & video calls may be affected due to insufficient bandwidth.

* Pausing/resuming receiving remote audio/video: During the pause, the remote audio & video cannot be received.

* Pausing/resuming sending local audio/video: During the pause, the local audio & video cannot be sent.


<span id="device-status"></span>
### Device Status

The relevant metrics are described below:


* CPU usage: If the CPU usage exceeds 80%, it means that the device may not be able to provide enough resources for the application. Try to restart or replace the device.

* Audio volume: Low capture/playback volume may be reported as silence.

* Video resolution: The resolution can help troubleshoot video blurring.

* Bit rate: Bit rate is the amount of data transmitted per unit of time. Generally, the higher the bit rate, the higher the media quality. The bit rate will fluctuate within a certain range. If the bit rate suddenly experiences significant drops, it indicates that the network may be congested. If the bit rate fluctuates abnormally within a certain period of time, it may indicate large network jitter, which may affect the call quality.

* Video frame rate: Frame rate is the number of frames displayed per second, also known as FPS. Generally, the higher the frame rate, the smoother the video. But higher frame rates will take up more internet bandwidth and device CPU. When the frame rate is low, for example, below 5 fps, it will cause stall or blurring.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a20b11edc3d7b6dea35bb5f3e874b4c.png) </span>

<span id="network-status"></span>
### Network Status

Poor network metrics usually result in lower call quality, which can manifest as audio/video stalls, dropped frames, and blurring.


* Packet Loss Rate: Packet loss refers to the situation where some packets are not received during the uplink/downlink data transmission. Generally, low packet loss rates will not affect the call experience.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3197636945f080c7c75a1bb48c993d0.png) </span>


* Latency: Uplink/downlink network round\-trip time (RTT). When RTT exceeds 250 ms, it may affect the call experience.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5fd512efa1d9d22bcd2be17e60704b3c.png) </span>


* Stall: A video stall is recorded when no video frames are received from a remote stream for more than 500 ms continuously.
