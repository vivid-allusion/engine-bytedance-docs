---
title: "Group Video Call Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-154376"
---

Group video call is one of the most common use cases in social interactions where it's better to eliminate role distinctions among relatives, friends, and strangers. This use case supports multi\-ends intercommunication including mobile phone, PC, and web. Users type in the same room number to create or enter the same online real\-time interactive room where they can chat in real time, creating a completely equal high\-quality audio and video chatting room for users. This use case also supports adding beauty effects and enabling screen sharing.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/docs/12/docs-257549). There is usually 1 role in a video call room:


|Role |Description |
|---|---|
|Callers |Users participating in audio and video calls in the room. They can manage their own audio and video devices and parameters, and view real\-time audio and video quality statistics for all callers in the room. Additionally, on PC and web clients, they can share their screen for other callers to watch. |


<span id="how-to-play"></span>
# **Example Scenarios**


* Socializing with acquaintances

   By removing role\-based features like seat control, all participants in a call with friends have an equal experience.

* Socializing with strangers

   Removing role privileges creates a level playing field for all participants, which is ideal for social applications that connect strangers.

* Screen sharing

   Users can share their screens during calls, which is useful for scenarios like technical consultations or educational sessions.


<span id="technical-structure"></span>
## Technical Structure

Users with publishing permissions (speakers) can publish audio streams to the RTC room. Other users in the room can only subscribe to and receive these streams.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/videocall/79cca7db-8d17-4732-8f73-9d53b4a8465e.png) </span>

<span id="feature-list"></span>
## Feature List


|Feature |Description |
|---|---|
|Real\-time voice interaction |The room owner and guests can have real\-time audio interactions in the voice chat room. |
|Audio live streaming |Audiences can listen to real\-time audio interactions between users on the mic. |
|Invite to be a guest |The room owner can invite audiences to be a guest. After accepting the invitation, such audiences become guests so they can have real\-time audio interactions with the room owner and other guests. |
|Apply to be a guest |Audiences can apply to be guests. After being accepted by the room owner, such audiences become guests so they can have real\-time audio interactions with the room owner and other guests. |
|Background music |Music can be played in the room for all users, helping to create an atmosphere that suits the room's theme. |
|Guest Seat Management |The room owner can manage guest seats with actions such as inviting users to become guests, removing guests, muting or unmuting guests, and locking or unlocking guest seats. |
|Real\-time signaling |Users in the voice chat room can communicate in real\-time by sending texts or images. |
|Comments/Gifts |Users in voice chat rooms can post live comments or send gifts to their favorite guests/streamers. |
