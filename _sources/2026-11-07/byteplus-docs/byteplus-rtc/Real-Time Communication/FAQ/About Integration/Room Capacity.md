---
title: "Room Capacity"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-257549"
---

<span id="how-many-visible-users-can-an-rtc-room-accommodate"></span>
## How many visible users can an RTC room accommodate?

> Note: All users are visible who can publish and subscribe to media streams. While an invisible user can only subscribe to media streams. To change the visibility of a user, call setUserVisibility.


* Audio selection disabled: 50

* Audio selection enabled: 1000


<span id="how-many-media-streams-can-users-publish-at-the-same-time-in-an-rtc-room"></span>
## How many media streams can users publish at the same time in an RTC room?

> Note: A user can publish up to 2 streams in an RTC room, that one Main stream and one Screen\-sharing stream. Each stream can be a video\-only, audio\-only, or video\-and\-audio stream.


* Audio selection disabled: 30

* Audio selection enabled: 1000


<span id="how-many-media-streams-can-a-user-subscribe-to-at-the-same-time"></span>
## How many media streams can a user subscribe to at the same time?


* Audio selection disabled: 30 video streams + 30 audio streams

* Audio selection enabled: 50 video streams. The capacity of audio streams is up to the audio selection settings which are 4 audio streams by default.
