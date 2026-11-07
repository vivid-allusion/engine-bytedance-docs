---
title: "OpenAPI"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-116363"
---

<span id="_2026"></span>
## 2026


* 2026\-09

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Subtitles |Added subtitle OpenAPIs, including [StartSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402681), [UpdateSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402683), and [StopSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402682), to let you start, update, and stop real\-time subtitle tasks on the server side. Added the [Real-time Call Subtitles and Translation](https://docs.byteplus.com/docs/byteplus-rtc/real-time-call-subtitles-and-translation-server-side) guide to describe how to receive and parse subtitle results on the client or server. |2026\-09\-11 |
   

* 2026\-07

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Audio Segmentation |A new `Control.VadConfig` parameter has been added to the `StartSegment` API to support Voice Activity Detection (VAD). When enabled, it automatically filters out audio segments that do not contain human speech, thereby saving storage and downstream processing costs. |2026\-07\-27 |
   |Snapshot |The data type of the `ImageConfig.Interval`parameter is changed from `int` to `float` to support millisecond precision. The interval is specified in milliseconds, with the valid range updated to `[0.1, 600]`. |2026\-07\-23 |
   

* 2026\-04

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Relay online media stream |Added `Volume` parameter to support adjusting the volume during and before relaying the stream, and supported MP3 format. |2026\-04\-10 |
   


<span id="_2025"></span>
## 2025


* 2025\-04

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |Added `Duration` to the `UserLeaveRoom` and `InvisibleUserLeaveRoom` callbacks to show the duration of the user in the room. |2025\-04\-11 |
   

* 2025\-03

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |Added `IP` in [BanRoomUser](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188353) to support banning users using specified public IP address. |2025\-03\-24 |
   

* 2025\-02

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Cloud Recording |Supported TOS storage for cloud recording, segment and snapshot. |2025\-02\-25 |
   


<span id="_2024"></span>
## 2024


* 2024\-12

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |Add [Conversational AI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1315560) related APIs, you can call them to engage an AI agent to interact with the user in the room. |2024\-12\-30 |
   |Cloud Recording |Cloud recording supports recording video at up to 4K resolution. |2024\-12\-18 |
   

* 2024\-11

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Cloud Recording |Added `SecurityToken` (temporary security token) in Cloud Recording (including for WTN). You can use temporary security tokens for authenticating with third\-party cloud storage platforms, enhancing system security. See details in [StartRecord](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115526) and [StartRecord (WTN)](https://docs.byteplus.com/en/docs/byteplus-rtc/startrecord-wtn). |2024\-11\-29 |
   |Stream Management |Added [ListRealTimePublicStreamInfo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1391228). You can query public streams' subscription data of an application over a period of time. |2024\-11\-29 |
   

* 2024\-08

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Cloud Recording |* Added `MaxSilenceSeconds` in Cloud Recording. You can set the maximum silence time to pause cloud recording, but not stop the recording task.<br><br>* Supported setting audio parameters in cloud recording. |2024\-08\-26 |
   |Cloud Recording |Cloud recording has added a new feature of recording and uploading simultaneously, which is only effective for files stored in `HLS` format.<br><br><br>* Added RecordSyncUploadStarted callback to show an m3u8 file was generated and uploaded successfully.<br><br>* Added RecordSyncUploadFailed callback to show an m3u8 file was generated but failed to be uploaded. |2024\-08\-23 |
   

* 2024\-07

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Push to CDN |Add enumeration value `1` to `Status` in `PushPublicStream`, which means public stream is pushed successfully. |2024\-07\-17 |
   

* 2024\-06

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |**Deprecated:** <br><br><br>* `UserExtraInfo` in `UserJoinRoom` has been deprecated. Use `ExtraInfo` instead.<br><br>* `UserExtraInfo` in `InvisibleUserJoinRoom` has been deprecated. Use `ExtraInfo` instead.<br><br><br>**Added**:<br><br><br>* Added `ExtraInfo` in [UserAudioStreamStart](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#useraudiostreamstart) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserAudioStreamStop](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#useraudiostreamstop) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserVideoStreamStart](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#uservideostreamstart) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserVideoStreamStop](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#uservideostreamstop) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserScreenAudioStreamStart](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userscreenaudiostreamstart) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserScreenAudioStreamStop](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userscreenaudiostreamstop) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserScreenVideoStreamStart](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userscreenvideostreamstart) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserScreenVideoStreamStop](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userscreenvideostreamstop) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserJoinRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userjoinroom) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [UserLeaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userleaveroom) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [InvisibleUserJoinRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#invisibleuserjoinroom) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [InvisibleUserLeaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#invisibleuserleaveroom) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [RoleChangeInvisible2Visible](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#rolechangeinvisible2visible) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server.<br><br>* Added `ExtraInfo` in [RoleChangeVisible2Invisible](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#rolechangevisible2invisible) callback to show user's extra information passed in by `joinRoom` and user's extra information returned by the RTC server. |2024\-06\-03 |
   

* 2024\-05

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |`2023-11-01` version for acquiring data index added. Under this version:<br><br><br>* When the HTTP response status code is equal to `200`, it indicates a successful call.<br><br>* When the HTTP response status code is not equal to `200`, it indicates a failed call. You can parse the error reason based on the `Code` and `Message` fields in `BaseResponse.ResponseMetaData` and `BaseResponse.Result` field.<br><br><br>**Interface Changes**<br><br><br>* Added [BanUserStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188354). You can block the audio/video stream published by the user in a room.<br><br>* Added [UnbanUserStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188356). You can unblock the audio/video stream published by the user in a room.<br><br>* Added [BanRoomUser](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188353). You can ban a room or specific user in the room to dismiss the room or remove specific user.<br><br>* Added [UpdateBanRoomUserRule](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188351). You can update `ForbiddenInterval` of a room or user.<br><br>* Added [GetRoomOnlineUsers](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188355). You can get a real\-time list of users in a room.<br><br>* Added [LimitTokenPrivilege](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188352). You can restrict the publishing permissions of a user's Token. |2024\-05\-11 |
   

* 2024\-01

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Cloud Recording |Cloud recording supports Google Cloud storage platform. |2024\-01\-05 |
   


<span id="_2023"></span>
## 2023


* 2023\-11

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Callbacks |**Deprecated:** <br><br>`GetUserStreamState` has been deprecated. Use [callbacks about the status of audio and video streams](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125) to get the real\-time status of a specified user's streams. |2023\-11\-08 |
   |Room Management |* Added `UserExtraInfo` in `UserJoinRoom` callback to show user's extra information passed in by the SDK<br><br>* Added `UserExtraInfo` in `InvisibleUserJoinRoom` callback to show user's extra information passed in by the SDK |2023\-11\-07 |
   

* 2023\-07

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Push to CDN |* Added Enumerated value `4` for `TaskState` of `TranscodeStateChanged` callback. It means the address of pushed stream has changed.<br><br>* Added `IsUpdatePartialParam` request parameter in `UpdatePushMixedStreamToCDN` to support updating partial parameters.<br><br>* Added `SequenceNumber` request parameter in `UpdatePushMixedStreamToCDN` to flag a request to ensure the server updates according to the latest configuration.<br><br>* Added `PushStreamState` return parameter in `GetPushSingleStreamToCDNTask` to query the status of pushed stream.<br><br>* Added `PushStreamState` return parameter in `GetPushMixedStreamToCDNTask` to query the status of pushed stream. |2023\-07\-27 |
   |General |Added [Layout.CustomLayout.Regions.Region.ApplySpatialAudio](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69835#region). You can use it to choose whether to enable spatial audio mode. |2023\-07\-11 |
   

* 2023\-06

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Cloud Recording |* Added [GetPushMixedStreamToCDNTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-w5q4dtjbde). You can use this API to query a started mixed\-stream task.<br><br>* Added [GetPushSingleStreamToCDNTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-3w06olaa6w).You can use this interface to query a started single\-stream task.<br><br>* Added [GetSnapshotTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-7oypi02iom). You can use this interface to query a started snapshot task.<br><br>* Added [GetSegmentTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-zixcxrzfsy). You can use this interface to query a started segment task.<br><br><br>Supported WebRecord:<br><br><br>* [StartWebCast](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-119513): You can relay the content of the specified webpage to the RTC room.<br><br>* [StopWebCast](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-119514): You can stop the relaying task.<br><br>* [GetWebCastTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-zq385antnd): you can query a started webrecord task. |2023\-06\-20 |
   |Room Management |Optimized the logic for [mutual kick-out](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#userjoinroom) when entering the room |2023\-06\-15 |
   |Cloud Recording |Changed `Layout.CustomLayout.Regions.Region` to an optional parameter in `StartPushMixedStreamToCDN` and `StartPushSingleStreamToCDN`.<br><br><br>* Added `PushUrl` in `TranscodeStarted`, `TranscodeUpdated`, `TranscodeStateChanged` and `TranscodeStopped` callbacks to show the CDN address of pushed Url.<br><br>* Added [Layout.CustomLayout.Regions.Region.MediaType](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69835#region). You can use it to set the media type of a stream when pushing to CDN.<br><br>* Added [Layout.CustomLayout.Regions.Region.MediaType](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115995#region). You can use it to set the media type of a stream in cloud recording.<br><br>* Added [Layout.CustomLayout.Regions.Region.AlternateImageRenderMode](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69835#region). You can use it to set the rendering mode of the alternate image when pushing to CDN.<br><br>* Added [Layout.CustomLayout.Regions.Region.AlternateImageRenderMode](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115995#region). You can use it to set the rendering mode of the alternate image in cloud recording.<br><br>* Changed the rule of slicing in cloud recording. |2023\-06\-02 |
   

* 2023\-04

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |Added [ListCallDetail](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-172151) . You can call this interface to query the uplink and downlink data of a user in a specified room under a certain application within a certain period of time. |2023\-04\-12 |
   |Room Management |* Added [BanRoomUser](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-336038) . You can call this interface to ban a room or specific user in the room to dismiss the room or remove specific user.<br><br>* Added [UpdateBanRoomUserRule](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-336039) . You can call this API to update ban length set by calling `BanRoomUser`.<br><br><br>**Deprecated:** <br><br><br>* `DismissRoom` has been deprecated. Call [BanRoomUser](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-336038) to dismiss a room instead.<br><br>* `KickUser` has been deprecated. Call [BanRoomUser](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-336038) to kick a user out of a room instead. |2023\-04\-11 |
   

* 2023\-03

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Relay Stream |In Relaying online media stream, the range of `StreamControl.FrameRate` was changed to `[1,30]`. |2023\-03\-13 |
   |Room Management |* Added [StartPushSingleStreamToCDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153583). You can call this API to push a single stream to the specified CDN address through the RTMP protocol<br><br>* Supported **Relay online media stream**<br><br>* [StartRelayStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-105188): You can relay online media streams into the RTC room for remote users to enjoy<br><br>* [StopRelayStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-105190): You can stop relaying this media stream<br><br>* [UpdateRelayStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-105189):You can update the URL address of this media stream to relay a new media stream<br><br>* [ListRelayStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-121958):You can query all tasks of relaying media streams in a room under an `AppId` |2023\-03\-06 |
   

* 2023\-02

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Cloud Recording |* Snapshot supports more S3 storage platforms, including HUAWEI CLOUD OBS, Tencent Cloud COS, Qiniu Cloud Kodo.<br><br>* Segment supports more S3 storage platforms, including HUAWEI CLOUD OBS, Tencent Cloud COS, Qiniu Cloud Kodo.<br><br>* Cloud recording supports more S3 storage platforms, including HUAWEI CLOUD OBS, Tencent Cloud COS, Qiniu Cloud Kodo. |2023\-02\-07 |
   |Room Management |A task of pushing to CDN can be started when there is no user pushing a stream in the room. For details, see [Control](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69835#control). |2023\-02\-03 |
   |Room Management |* Added [ListUserInfo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-156027). You can call this interface to query the information of specific or all users in a room over a period of time.<br><br>* Added [ListRoomInfo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-156026). You can call this interface to query the list of the rooms where audio or video calls are being made and related information of these rooms. |2023\-02\-02 |
   

* 2023\-01

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |Added GetUserStreamState. You can call this interface to query the real\-time status of a specified user's streams in the specific room. |2023\-01\-19 |
   |Data Index |Added [ListQuality](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-124667). You can call this interface to query the offline quality of audio and video calls of an application within a certain period of time. |2023\-01\-18 |
   |Data Index |* Added [ListOperationDistribution](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-163727). You can call this interface to query the geographical distribution (first\-level administrative divisions/countries) of your operating activities (the user count).<br><br>* Added [ListQualityDistribution](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-163728). You can call this interface to track the performance of your App across a range of dimensions, including first\-level administrative divisions, countries, operating systems, and network types.<br><br>* Added [ListRealTimeQualityDistribution](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-163729). You can call this interface to track the performance of your App in real time across a range of dimensions, including first\-level administrative divisions, countries, operating systems, and network types. |2023\-01\-05 |
   


<span id="_2022"></span>
## 2022


* 2022\-08

   
   |Feature |Description |Release Date |
   |---|---|---|
   |Room Management |* Supported **room management**. You can manage the room and users in the room, including kicking them out and banning the user's stream. In addition, you can acquire related information about the room and users.<br><br>* Supported **pushing streams to CDN**. You can mix multiple audio & video streams into one, and push the mixed audio & video stream to the specified address.<br><br>* Supported **acquiring data index**. You can query the call duration of an application over a period of time.<br><br>* Supported **App Management**. You can manage AppId including creating an AppId, modifying its status and querying it.<br><br>* Supported **real\-time signaling**. You can send peer\-to\-peer messages and broadcast messages in the room and out of the room. |2022\-08\-26 |
