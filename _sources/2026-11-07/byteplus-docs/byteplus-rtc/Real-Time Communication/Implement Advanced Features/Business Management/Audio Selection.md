---
title: "Audio Selection"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113547"
---

Audio selection is a feature that intelligently manages audio subscriptions in large\-scale RTC rooms. When enabled, the RTC server automatically selects and delivers audio streams from the loudest participants, which improves user experience and increases the room's capacity. This document explains the feature details, how to enable it, and the resulting changes in API and callback behavior.


* **Online conference.**  Join an RTC room with thousands of participants who can turn on their microphone and camera and watch other participants’ videos.

* **Interactive entertainment.**  Join an RTC room with tens of thousands of participants who can request to interact with guests.


<span id="feature-details"></span>
## Feature Details


* Enabling Audio selection will increase the capacity of an RTC room. For your reference, see [Capacity of Users and Media Streams](https://docs.byteplus.com/en/docs/12/docs-257549) for the capacity before and after the Audio selection is enabled.

* After audio selection is enabled, you still need to manage your video subscription.

* When audio selection is enabled, you have the option to unsubscribe from a selected audio, except when using the Web SDK. For example, if user A unsubscribes from user B's audio, user A won't hear user B even if user B is selected as an active speaker.

* Enabling audio selection only affects rooms created after the feature is enabled; it does not impact existing rooms.


<span id="enable-audio-selection"></span>
## Enable Audio Selection


> * By default, the Audio selection is disabled for each application.

> * Use different appIDs for audio and video apps in different scenarios. Do not toggle Audio selection within a single app, because the scenarios that require this feature vary significantly.

1. Navigate to **Settings** \> **Audio selection**, on the [BytePlus RTC Console](https://console.byteplus.com/rtc/cloudRTC?tab=roomMode)

2. Turn on Audio selection.

> * You can disable Audio selection by following the same steps.


<span id="api-reference"></span>
## API Reference

When over 5 users are in an RTC room, the expected behavior of the following APIs and callbacks differs before and after the Audio selection is enabled.

> Note: The steps are the same in different platforms, but interface and parameter names may be slightly different. The following guide takes the Windows RTC SDK as an example. You can refer to the API reference of the corresponding platform for more information.


<span id="api"></span>
### API


|API |Audio selection disabled |Audio selection enabled |
|---|---|---|
|joinRoom ([isAutoSubscribeAudio](https://docs.byteplus.com/en/docs/12/docs-70098#is-auto-subscribe-audio-2) = true) |Automatically subscribe to audio |Invalid. Audio subscription relationships are automatically managed by the RTC server. |
|subscribeStream |Subscribe to media stream of specified user |Video: Same as when Audio selection is disabled |


<span id="callback"></span>
### Callback

The behavior of some callbacks will change when Audio selection is enabled, as shown in the table below. You must adjust the corresponding application\-side logic according to these changes.


|Callback |Audio selection disabled |Audio selection enabled |
|---|---|---|
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#onuserjoined) |Callbacks for remote visible users joining the room, or for invisible users in the room switching to visible. |The callback is not triggered after the number of visible users in the room exceeds 500. If you need a complete list of users in the room, you need to maintain your own user list. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70096#onuserleave) |Triggered when a remote user goes offline or becomes invisible |The callback is not triggered after the number of visible users in the room exceeds 500 |
|[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-70096#onroomstats)<br><br>This interface is not available on Web. |Report in\-room call statistics every 2s |The RtcRoomStats{user_count} value of the callback is invalid after the number of visible users in the room exceeds 500 |
|[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#onuserpublishstreamvideo)/[onUserUnpublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#onuserpublishstreamaudio) |Triggered when media streams captured by remote cameras/microphones are added to the room |Only receive callbacks related to video stream |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#onnetworkquality) |Reports the network quality score of the user(s) in the room |Report information about users with video streams or network quality scores of remote active users |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#onremotestreamstats) |Reports the network quality statistics of the subscribed remote user in the reported interval | **(Native)**  Report information about users with video streams published or audio stream information from remote active users.<br><br> **(Web)**  Audio stream information will not be reported. |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#onremoteaudiopropertiesreport) |Reports the audio information of the subscribed remote user. |Reports the audio information of the remote active users |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#onuserstartaudiocapture) |A remote user has started audio capture. |You won't receive this callback after enabling Audio selection, regardless of the number of users in the room. |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#onuserstopaudiocapture) |A remote user has stopped audio capture. |You won't receive this callback after enabling Audio selection, regardless of the number of users in the room. |
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#onuserstartvideocapture) |A remote user has started video capture. |You will receive this callback only when the remote user has published their video stream. It is triggered once, along with `onUserPublishStream`. Receiving both callbacks confirms that the user has started video capture. |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#onuserstopvideocapture) |A remote user has stopped video capture. |You won't receive this callback after enabling Audio selection. When the remote user has stopped the video capture, you receive `onUserUnpublishStream`. Receiving the `onUserUnpublishStream` callback confirms that the remote user has stopped video capture. |


> **Notes**

> * Calling `PublishStream` or `PublishScreen` will return a `-1080` error code when the number of media streams in the room reaches the [maximum number](https://docs.byteplus.com/en/docs/12/docs-257549). There is no corresponding error code on Web, but it will also trigger a publishing failure.

> * Calling `SubscribeStream` or `SubscribeScreen` will return a `-1070` error code when the number of streams subscribed to by the current user reaches the [maximum number](https://docs.byteplus.com/en/docs/12/docs-257549). There is no corresponding error code on Web, but it will also trigger a subscription failure.


If you have any other questions, contact our pre\-sales or technical support team.

<span id="changelog"></span>
## Changelog


* This feature is available on Native, Electron and Flutter since RTC SDK v3.45.

* This feature is available on Web since RTC SDK v4.49.

* Starting from June 8th 2023, BytePlus RTC uses Audio selection instead of Room mode. If you previously enabled and selected a mode, we have migrated your settings to the latest version without modifying the features and capacity. For your reference, see the table below for the settings before and after the change.



|Previous |Current |
|---|---|
|Default mode with Audio selection disabled |Audio selection disabled |
|Default mode with Audio selection enabled |Audio selection enabled |
|Conference Mode |Audio selection enabled |
|Conference mode for games |Audio selection disabled |
