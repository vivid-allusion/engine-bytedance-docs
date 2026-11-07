---
title: "Spatial Audio"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-93903"
---

<span id="introduction"></span>
## Introduction

Spatial audio is a powerful 3D audio technology that enables a more immersive and realistic audio experience by accurately reproducing sound in three\-dimensional space. It allows audio to be positioned and moved around the listener, creating a sense of location and depth that can enhance the overall impact of audio content. It is becoming increasingly popular in a variety of applications, including:


* Online multiplayer gaming events like *PUBG* in which players can locate their teammates based on proximity\-based sensing;

* VR applications in which users can perceive full\-sphere surround sound.

* Virtual meetings in which participants can locate other members by sound.


This document describes how to implement the spatial audio effect.

<span id="prerequisites"></span>
## Prerequisites

Before implementing spatial audio, ensure you meet the following requirements:


* Integrate SDK v3.45 or later into your project.

* Use stereo\-capable devices.


This table shows the stereo capability of different audio routes.


|**Audio Route** |**Stereo Capability** |
|---|---|
|Wired Headphones |Yes |
|Bluetooth Headphones |* Mic on: No<br><br>* Mic off: Yes |
|Speakers |No |



* Ensure network stability. Avoid using spatial audio under challenging network conditions.

* Use high\-performance devices. Low\-end devices may cause audio stuttering or dropouts.

* Use RTC to render audio. Avoid using your custom audio renderer.


<span id="enable-spatial-audio"></span>
## Enable spatial audio

To implement the spatial audio effect, follow these steps:


1. Call `getSpatialAudio` to create a spatial audio instance.

2. Call `enableSpatialAudio` to enable the spatial audio effect;

3. Call `updatePosition` to update the three\-dimensional coordinate of the local user when they speak;

> You can repeatedly call this API to update the coordinates in real time.

> When you use Range Voice, use the same coordinates of the user.


4. (Optional) Call `updateListenerPosition` to update the three\-dimensional coordinate of the local user when they are listening.

> If you don't call this API, the coordinates of the local user will be the same when they speak and listen.


5. Call `updateSelfOrientation` to update the orientation of the local user when they speak.

6. (Optional) Call `updateListenerOrientation` to update the orientation of the local user when they listen.

> Notes:

> * The room size limits the voice reception range. Users can hear only 40 closest voices when more than 30 players speak nearby.

> * The spatial audio effect does not support screen\-captured audio streams.


<span id="disable-remote-user-orientation"></span>
## Disable remote user orientation

In some cases, it may be more important to perceive the distance of the speaker rather than their orientation. For example, during online meetings, the speaker's orientation must remain unchanged to provide high\-quality, real\-time audio call experience.

Call `disableRemoteOrientation` to disable remote user orientation.

> Notes:

> * After you disable this feature, you can still call `updateSelfOrientation` to update the local orientation. This will affect the local listening experience.

> * Ensure all users in a room have the same setting for this feature.


<span id="api-reference"></span>
## API Reference

See the links below for API details and parameters.


* Android

   * [getSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70080#getspatialaudio)

   * [enableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70080#enablespatialaudio)

   * [updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-70080#updateselfposition)

   * [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#updateremoteposition)

   * [removeRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#removeremoteposition)

* iOS

   * [getSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70086#getspatialaudio)

   * [enableSpatialAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#enablespatialaudio)

   * [updateSelfPosition:](https://docs.byteplus.com/en/docs/12/docs-70086#updateselfposition)

   * [updateRemotePosition:](https://docs.byteplus.com/en/docs/12/docs-70086#updateremoteposition)

   * [removeRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70086#removeremoteposition)

* Windows

   * [getSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70095#getspatialaudio)

   * [enableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70095##enablespatialaudio)

   * [updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-70095##updateselfposition)

   * [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095##updateremoteposition)

   * [removeRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095##removeremoteposition)
