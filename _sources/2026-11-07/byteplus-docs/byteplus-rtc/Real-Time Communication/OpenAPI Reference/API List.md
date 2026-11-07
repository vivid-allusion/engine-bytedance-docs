---
title: "API List"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1197615"
---

## Room Management

|API |Description |Related Version |
|---|---|---|
|[BanUserStream](https://docs.byteplus.com/en/docs/12/docs-1188354) |You can call the BanUserStream interface, specify the AppId, and block the audio/video stream published by the user with the specified userId in a room. |2023\-11\-01 |
|[UnbanUserStream](https://docs.byteplus.com/en/docs/12/docs-1188356) |You can call the UnbanUserStream interface, specify the AppId you belong to, and unblock the user audio/video stream of blocked users in the specified room. |2023\-11\-01 |
|[BanRoomUser](https://docs.byteplus.com/en/docs/12/docs-1188353) |You can call the BanRoomUser API, specify your AppId and RoomId to ban a room, or specify AppId, RoomId and UserId to remove a specific user in the room. |2023\-11\-01 |
|[UpdateBanRoomUserRule](https://docs.byteplus.com/en/docs/12/docs-1188351) |After you ban a room or specific user in the room, you can call the UpdateBanRoomUserRule OpenAPI to update the set rule. |2023\-11\-01 |
|[GetRoomOnlineUsers](https://docs.byteplus.com/en/docs/12/docs-1188355) |You can use this interface to get a real\-time list of users in a room by specifying your AppId and RoomId. |2023\-11\-01 |
|[LimitTokenPrivilege](https://docs.byteplus.com/en/docs/12/docs-1188352) |You can use this interface to restrict the publishing permissions of a user's Token by specifying your AppId and RoomId. |2023\-11\-01 |

## Cloud Recording

|API |Description |Related Version |
|---|---|---|
|[StartRecord](https://docs.byteplus.com/en/docs/12/docs-115526) |In an audio and video application, you can use cloud recording to record audio or video files. |2022\-06\-01 |
|[UpdateRecord](https://docs.byteplus.com/en/docs/12/docs-116406) |After you enable Cloud Recording and make a custom layout in mixing\-stream recording mode, you can update configuration parameters relevant to recording. You can use the UpdateRecord OpenAPI to do this. |2022\-06\-01 |
|[StopRecord](https://docs.byteplus.com/en/docs/12/docs-116407) |After you start cloud recording by calling StartRecord, you can use StopRecord to stop it. |2022\-06\-01 |
|[GetRecordTask](https://docs.byteplus.com/en/docs/12/docs-116408) |You can call this interface to query information about a recording task. |2022\-06\-01 |

## Push to CDN

|API |Description |Related Version |
|---|---|---|
|[StartPushMixedStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-69850) |In an audio and video application, you can mix multiple audio & video streams into one, and push the mixed audio & video stream to the specified address (usually CDN address) through the RTMP protocol. |2020\-12\-01 |
|[StartPushSingleStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-153583) |In an audio and video application, you can push a stream to the specified CDN address through the RTMP protocol. |2020\-12\-01 |
|[UpdatePushMixedStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-69849) |If you have started a task, you can call UpdatePushMixedStreamToCDN to update the task's parameters. |2020\-12\-01 |
|[StopPushStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-153582) |After you start a single\-stream or mixed\-stream task of pushing to CDN, you can stop it by calling this interface. |2020\-12\-01 |
|[GetPushMixedStreamToCDNTask](https://docs.byteplus.com/en/docs/12/docs-w5q4dtjbde) |After you start a mixed\-stream task to push to CDN, you can use this interface to query the task. |2020\-12\-01 |
|[GetPushSingleStreamToCDNTask](https://docs.byteplus.com/en/docs/12/docs-3w06olaa6w) |After you start a single\-stream task to push to CDN, you can use this interface to query the task. |2020\-12\-01 |

## Public Stream

|API |Description |Related Version |
|---|---|---|
|[StartPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-113680) |A public stream refers to an audio & video stream that users can subscribe to and receive without entering a room. In usual cases, users need to enter a room to subscribe and receive media streams. You can use the OpenAPI StartPushPublicStream to use this feature. |2022\-06\-01 |
|[UpdatePublicStreamParam](https://docs.byteplus.com/en/docs/12/docs-113681) |If you have started pushing a public stream using StartPushPublicStream, you can call UpdatePublicStreamParam to update some parameters of the task. |2022\-06\-01 |
|[StopPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-113682) |If you have already pushed a public stream, you can call StopPushPublicStream to stop pushing. |2022\-06\-01 |

## Query Real\-time Data

|API |Description |Related Version |
|---|---|---|
|[ListRealTimeQualityDistribution](https://docs.byteplus.com/en/docs/12/docs-163729) |Call ListRealTimeQualityDistribution to track the performance of your App in real time across a range of dimensions, including first\-level administrative divisions, countries, operating systems, and network types. |2020\-12\-01 |
|[ListCallDetail](https://docs.byteplus.com/en/docs/12/docs-1186717) |You can use this interface to query the uplink and downlink data of a user in a specified room under a certain application within a certain period of time. |2020\-12\-01 |
|[ListRealTimePublicStreamInfo](https://docs.byteplus.com/en/docs/12/docs-1391228) |In real\-time audio and video calling, you can use this interface to query public streams' subscription data of an application over a period of time. |2020\-12\-01 |

## Query Historical Data

|API |Description |Related Version |
|---|---|---|
|[ListQuality](https://docs.byteplus.com/en/docs/12/docs-71234) |You can call this interface to query the call duration of an application over a period of time. |2023\-11\-01 |
|[ListOperationDistribution](https://docs.byteplus.com/en/docs/12/docs-163727) |Call ListOperationDistribution to query the geographical distribution (first\-level administrative divisions/countries) of your operating activities (the user count). |2023\-11\-01 |
|[ListQualityDistribution](https://docs.byteplus.com/en/docs/12/docs-163728) |Call ListQualityDistribution to track the performance of your App across a range of dimensions, including first\-level administrative divisions, countries, operating systems, and network types. |2023\-11\-01 |
|[ListQuality](https://docs.byteplus.com/en/docs/12/docs-124667) |You can use this interface to query the offline quality of audio and video calls of an application within a certain period of time. |2023\-11\-01 |
|[ListRoomInfo](https://docs.byteplus.com/en/docs/12/docs-1186715) |In an audio & video application, you may need to query the list of the rooms where audio or video calls are being made and related information of these rooms. |2023\-11\-01 |
|[ListUserInfo](https://docs.byteplus.com/en/docs/12/docs-1186716) |In an audio & video application, you may need to query the information of specific or all users in a room over a period of time. You can use ListUserInfo to do this. |2023\-11\-01 |

## App Management

|API |Description |Related Version |
|---|---|---|
|[CreateApp](https://docs.byteplus.com/en/docs/12/docs-74487) |You have two options for managing AppIDs: using the console or calling the OpenAPI. To create an AppID, you can use the CreateApp API. |2020\-12\-01 |
|[ModifyAppStatus](https://docs.byteplus.com/en/docs/12/docs-74488) |After you have created an app, you can enable or disable the app. You can call the ModifyAppStatus OpenAPI to do this. |2020\-12\-01 |
|[ListApps](https://docs.byteplus.com/en/docs/12/docs-74489) |After you create an app, you can query for information about the app that corresponds to an AppId. You can call ListApps to do this. |2020\-12\-01 |

## Real\-time Signaling

|API |Description |Related Version |
|---|---|---|
|[SendUnicast](https://docs.byteplus.com/en/docs/12/docs-1164061) |In your audio & video applications, when you need to send out\-of\-room peer\-to\-peer messages from the business server to a client, you can call the OpenAPI of SendUnicast to do this. |2023\-07\-20 |
|[SendRoomUnicast](https://docs.byteplus.com/en/docs/12/docs-1164062) |In your audio & video applications, when you need to send messages from the business server to a client in a specified RTC room, you can call the OpenAPI of SendRoomUnicast to do this. |2023\-07\-20 |
|[SendBroadcast](https://docs.byteplus.com/en/docs/12/docs-1164063) |In your audio & video application, when you need to broadcast messages from the business server to all users in a specified RTC room, you can call the OpenAPI of SendBroadcast to do this. |2023\-07\-20 |
|[BatchSendRoomUnicast](https://docs.byteplus.com/en/docs/12/docs-1164064) |In your audio & video application, when you need to send peer\-to\-peer messages from the business server level to a number of users in a specified RTC room simultaneously, you can use the OpenAPI BatchSendRoomUnicast to do this. |2023\-07\-20 |

## Segment

|API |Description |Related Version |
|---|---|---|
|[StartSegment](https://docs.byteplus.com/en/docs/12/docs-155129) |In an audio & video application, you can segment audio streams in the room for processing later including moderating the content. |2022\-06\-01 |
|[UpdateSegment](https://docs.byteplus.com/en/docs/12/docs-155130) |If you have started a segmenting task, you can use UpdateSegment to update the parameters of the task. |2022\-06\-01 |
|[StopSegment](https://docs.byteplus.com/en/docs/12/docs-155131) |After starting a segmenting task, you can use StopSegment to stop the task. | |
|[GetSegmentTask](https://docs.byteplus.com/en/docs/12/docs-zixcxrzfsy) |After you start a segment task, you can use this interface to query the task. |2022\-06\-01 |

## Subtitles

|API |Description |Related Version |
|---|---|---|
|[StartSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402681) |Start a real\-time subtitle task for an RTC room or WTN stream. |2024\-06\-01 |
|[UpdateSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402683) |Update the language settings of an ongoing real\-time subtitle task for an RTC room or WTN stream. |2024\-06\-01 |
|[StopSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402682) |Stop an ongoing real\-time subtitle task for an RTC room or WTN stream. |2024\-06\-01 |

## Snapshot

|API |Description |Related Version |
|---|---|---|
|[StartSnapshot](https://docs.byteplus.com/en/docs/12/docs-155125) |In an audio & video application, you may need to take snapshots of streams in the room at certain intervals for processing later, including storing and identifying illegal information. |2022\-06\-01 |
|[UpdateSnapshot](https://docs.byteplus.com/en/docs/12/docs-147060) |If you start a snapshotting task, you can use UpdateSnapshot to update set parameters. |2022\-06\-01 |
|[StopSnapshot](https://docs.byteplus.com/en/docs/12/docs-155157) |After starting a snapshot task, you can call StopSnapshot to stop it. |2022\-06\-01 |
|[GetSnapshotTask](https://docs.byteplus.com/en/docs/12/docs-7oypi02iom) |After you start a snapshot task, you can use this interface to query the task. |2022\-06\-01 |

## Relay online Media Stream

|API |Description |Related Version |
|---|---|---|
|[StartRelayStream](https://docs.byteplus.com/en/docs/12/docs-105188) |In an audio and video application, you may need to relay online media streams into the RTC room for remote users to enjoy. |2020\-12\-01 |
|[UpdateRelayStream](https://docs.byteplus.com/en/docs/12/docs-105189) |After you relay an online media stream, you can update the URL address of this media stream to relay a new media stream. |2020\-12\-01 |
|[StopRelayStream](https://docs.byteplus.com/en/docs/12/docs-105190) |After relaying an online media stream, you can use StopRelayStream to stop relaying this media stream. |2020\-12\-01 |
|[ListRelayStream](https://docs.byteplus.com/en/docs/12/docs-121958) |If you have relayed online media streams, you can query all tasks of relaying media streams in a room under an AppId. |2020\-12\-01 |

## WebRecord

|API |Description |Related Version |
|---|---|---|
|[StartWebcast](https://docs.byteplus.com/en/docs/12/docs-119513) |In online classrooms, video conferences, and other scenarios, you may need to relay the content of a specified webpage to the RTC room for users to watch. You can use this interface to do this. |2022\-06\-01 |
|[StopWebcast](https://docs.byteplus.com/en/docs/12/docs-119514) |After relaying the content of a specified webpage to the RTC room, you can use this interface to end the task. |2022\-06\-01 |
|[GetWebCastTask](https://docs.byteplus.com/en/docs/12/docs-zq385antnd) |After you start a webrecord task, you can use this interface to query the task. |2022\-06\-01 |

## Push Media Stream to WTN

|API |Description |Related Version |
|---|---|---|
|[RtmpAccessInfo](https://docs.byteplus.com/en/docs/12/docs-1392589) |You can use this interface to obtain an RTMP push stream address, so that you can push RTMP streams such as local media files and audio and video captured by audio and video devices to WTN and play them in the RTC room. |2023\-11\-01 |

## Query WTN Stream

|API |Description |Related Version |
|---|---|---|
|[GetStreamProperty](https://docs.byteplus.com/en/docs/12/docs-139261) |You can use this interface to query the information of the specified WTN stream. |2023\-11\-01 |
|[GetOnlineStreams](https://docs.byteplus.com/en/docs/12/docs-139262) |You can use this interface to query the list of online WTN streams. |2023\-11\-01 |
