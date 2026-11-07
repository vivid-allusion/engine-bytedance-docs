---
title: "Show Call Statistics"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-106866"
---

BytePlus RTC SDK provides rich in\-call statistics via callbacks, including network quality, audio & video stream quality and states, device performance, and call statistics. This will help you optimize your project and you can also use this information to further analyze call statistics.

> Note:

> The steps are the same in different platforms, but the names of interface and parameter may be slightly different. The following guide takes the Android RTC SDK as an example. You can refer to the API doc of the corresponding platform for more information.


<span id="prerequisite"></span>
## Prerequisite

You have integrated the RTC SDK to implement basic real\-time functions.

<span id="network-quality-rating"></span>
## Network quality rating

After users enter the room, the `onNetworkQuality` callback reports the uplink and downlink network quality score of the local user and the remote subscribed user every 2 seconds. You can determine the network quality from the `NetworkQuality` score.

> Note:

> Web SDK only supports getting the upstream and downstream network quality scores of local users, but not those of remote users.


* `NETWORK_QUALITY_BAD`: Network quality is poor and the communication quality is poor. It is recommended to lower the sampling rate, bit rate or to notify users through the UI to switch to a voice call.

* `NETWORK_QUALITY_VERY_BAD`: Network quality is very poor. It is recommended to notify users of the poor connection through the UI.


<span id="audio-and-video-quality-report"></span>
## Audio and video quality report

The following callbacks report statistics of audio & video streams sent and received.


* `onLocalStreamStats`: triggered every 2 seconds after a local media stream is published.

* `onRemoteStreamStats`: triggered every 2 seconds after the local device subscribes to a remote media stream.


<span id="network-conditions"></span>
### Network conditions


|Parameter |Description |Comment |
|---|---|---|
|sendKBitrate |The average bitrate of audio sent in the reported interval |The closer the actual bitrate is to the target bitrate, the better the network quality |
|e2eDelay |The time taken for audio/video encoding on the sending side to rendering on the receiving side. | |
|rtt |The round\-trip time of data transmission from client side to server side. | |
|total_rtt |The round\-trip time for data transmission from the sender to the receiver via the server. | |


<span id="freeze"></span>
### Freeze

> Note:

> You can get more statistics on the console.



|Parameter |Description |Comment |
|---|---|---|
|stallCount |Frequency of freeze |Video freeze occurs when the time interval between two adjacent renderable video frames is more than 500 ms. Audio freeze occurs when the time interval between two adjacent renderable audio frames is more than 80 ms. |
|stallDuration |Freeze duration |freeze duration refers to the total time freeze occurs in a reported interval. |
|frozenRate |The ratio of total freeze duration to the total time when the audio/video is available in the room |Audio/video is considered available when the user has not stopped sending the stream or disabled the audio/video module. |


Before attempting to fix a freeze, determine if it is an intermittent issue caused by poor network or device performance. Such freezes might have a negligible impact on the user experience and may not require intervention.


* Use the data in the callback to check if the network is stable and in good condition.

* If the network is good (for example, the `NetworkQuality` is `NETWORK_QUALITY_EXCELLENT` or `NETWORK_QUALITY_GOOD`), check the CPU usage of devices through the `onSysStats` callback


If there is still a problem, please contact technical support.

<span id="room-and-device-statistics-report"></span>
## Room and device statistics report

After the user enters the room, the `onRoomStats` and `onSysStats` callbacks report local call statistics every 2 seconds, including call duration, the number of participants in the room, current CPU usage, current memory usage of the app, and other important parameters.

<span id="media-stream-state-changes"></span>
## Media stream state changes


* When the state of a local audio stream changes, the `onLocalAudioStateChanged` callback is triggered. When the state of a local video stream changes, the `onLocalVideoStateChanged` callback is triggered. When there is a problem with local audio & video, you can troubleshoot it using error codes.

* Similarly, when the state of a remote audio or video stream changes, the corresponding `onRemoteAudioStateChanged` or `onRemoteVideoStateChanged` callback is triggered.


<span id="api-reference"></span>
## API reference


|Callback |Android |iOS |macOS |Windows |Web |
|---|---|---|---|---|---|
|Network quality rating |[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onnetworkquality) |[rtcRoom:onNetworkQuality:remoteQualities:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcroom-onnetworkquality-remotequalities) |[rtcRoom:onNetworkQuality:remoteQualities](https://docs.byteplus.com/en/docs/12/docs-70093#rtcroom-onnetworkquality-remotequalities) |[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onnetworkquality) |[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onnetworkquality) |
|Room statistics report |[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstats) |[rtcRoom:onRoomStats:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcroom-onroomstats) |[rtcRoom:onRoomStats:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcroom-onroomstats) |[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onroomstats) | |
|Device statistics report |[onSysStats](https://docs.byteplus.com/en/docs/12/docs-70081#onsysstats) |[rtcEngine:onSysStats:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onsysstats) |[rtcEngine:onSysStats:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onsysstats) |[onSysStats](https://docs.byteplus.com/en/docs/12/docs-70096#onsysstats) | |
|Local audio&video quality report |[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onlocalstreamstats) |[rtcRoom:onLocalStreamStats:info:stats:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcroom-onlocalstreamstats-info-stats) |[rtcRoom:onLocalStreamStats:info:stats:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcroom-onlocalstreamstats-info-stats) |[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onlocalstreamstats) |[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalstreamstats) |
|Remote audio&video quality report |[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onremotestreamstats) |[rtcRoom:onRemoteStreamStats:info:stats:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcroom-onremotestreamstats-info-stats) |[rtcRoom:onRemoteStreamStats:info:stats:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcroom-onremotestreamstats-info-stats) |[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onremotestreamstats) |[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotestreamstats) |
|State changes of local audio stream |[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalaudiostatechanged) |[rtcEngine:onLocalAudioStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onlocalaudiostatechanged-state-error) |[rtcEngine:onLocalAudioStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onlocalaudiostatechanged-state-error) |[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onlocalaudiostatechanged) | |
|State changes of local video stream |[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalvideostatechanged) |[rtcEngine:onLocalVideoStateChanged:withStreamState:withStreamError:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onlocalvideostatechanged-withstreamstate-withstreamerror) |[rtcEngine:onLocalVideoStateChanged:withStreamState:withStreamError:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onlocalvideostatechanged-withstreamstate-withstreamerror) |[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onlocalvideostatechanged) | |
|State changes of remote audio stream |[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onremoteaudiostatechanged) |[rtcEngine:onRemoteAudioStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onremoteaudiostatechanged-info-state-reason) |[rtcEngine:onRemoteAudioStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onremoteaudiostatechanged-info-state-reason) |[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onremoteaudiostatechanged) | |
|State changes of remote video stream |[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onremotevideostatechanged) |[rtcEngine:onRemoteVideoStateChanged:info:withVideoState:withVideoStateReason:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onremotevideostatechanged-info-withvideostate-withvideostatereason) |[rtcEngine:onRemoteVideoStateChanged:info:withVideoState:withVideoStateReason:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onremotevideostatechanged-info-withvideostate-withvideostatereason) |[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onremotevideostatechanged) | |
