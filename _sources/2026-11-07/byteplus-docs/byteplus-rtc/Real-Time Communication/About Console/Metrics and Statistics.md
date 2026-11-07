---
title: "Metrics and Statistics"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70063"
---

You can view the data and statistics of some period by app or business ID. The statistics include [call quality](https://docs.byteplus.com/6uofwzl3/14292), [operation data](https://docs.byteplus.com/6uofwzl3/14292), and [usage data](https://docs.byteplus.com/6uofwzl3/14292).

<span id="quality-overview"></span>
##   Quality Overview

Go to [BytePlus RTC Console](https://console.byteplus.com/rtc/workplaceRTC) \> [Quality Overview](https://console.byteplus.com/rtc/callQualityRTC/qos) and then select a time range to view the statistical data by application or business ID.


> * This page shows Native's quality data by default. Switch to Web's data by selecting Web in the list next to the page title.

> * The quality statistics have been generated based on the data before 24:00 yesterday. If you need the more recent data, go to [BytePlus RTC Console](https://console.byteplus.com/rtc/workplaceRTC) \> [Realtime Monitor](https://console.byteplus.com/rtc/callQualityRTC/qos) .


<span id="room-ranking"></span>
### Room Ranking

Click a data point on the chart to view the top 5 rooms that have the greatest impact on the metrics. Both the metrics and the user numbers of the room affect the ranking.

Click Diagnose to view the analysis of the room. Click User Ranking for a more detailed, user\-level analysis.

<span id="analysis-tool"></span>
### Analysis Tool

If you find abnormal data in the chart, use this tool to analyze it.

When data granularity is set to By day, click a data dot and select Analysis in All Dimensions to view its analysis by Area, Operating System, and SDK version.

> Analysis Tool does not support Web's data.


The following table describes each item and its calculation method.


|Item |Description |
|---|---|
|Success rate of joining rooms in 5 seconds |Count of joining a room in 5 s / Count of attempts to join a room<br><br>Receiving the joining room ACK in 5 s after calling joinRoom API is counted as a successful join. |
|Audio stall rate |The duration of audio stalls / total audio duration<br><br>An audio stall lasting over a specific amount of time, such as 80 ms, will be counted as one audio stall issue.<br><br><br>* For mobile and PC clients: 80 ms<br><br>* For web: 200 ms |
|Video stall rate |The duration of video stalls / total video duration<br><br>A video stall lasting over a specific amount of time, such as 500 ms, will be counted as one video stall issue.<br><br><br>* For mobile and PC clients: 500 ms (default) / 200 ms / 100 ms<br><br>* For web: 500 ms |
|Compliance percentage of 400 ms transmission delay |Count of transmission delays lower than 400 ms / Count of total reports of transmission delay<br><br>The transmission link for statistics begins from the sender and ends at the receiver. The delay does not include the delay introduced by jitter buffers. |
|Success rate of sending the first audio frame |The count of sending the first audio frame successfully / The count of API calls to start sending media frames<br><br>Sending media frames begins when the sending status changes from idle to active.<br><br>Sending the first audio frame successfully will trigger the callback of the first frame sent. The silent packets have been excluded. |
|Success rate of decoding the first audio frame |The count of successfully decoding the first audio frame / The count of decoding audio frames<br><br>The client receives and decodes the first valid audio frame which is not a silent packet. |
|Success rate of decoding the first video frame |The count of successfully decoding the first video frame / The count of decoding video frames<br><br>The client receives and decodes the first valid video frame. |


If you need statistics with different criteria, contact our technical specialists. For example, replace the Success rate of Joining Rooms in 5 Seconds with the Success rate of Joining Rooms in 3 Seconds.

You can view data aggregated by each dimension. Refer to [Dimension](https://docs.byteplus.com/6uofwzl3/14292) for help.

<span id="operation-data"></span>
##   Operation Data

Go to [BytePlus RTC Console](https://console.byteplus.com/rtc/workplaceRTC) \> [Operation Data](https://console.byteplus.com/rtc/callQualityRTC/operation) and then select a time range to view the statistical data by application or business ID.

> The operation data statistics include data up to the end of the previous day. If you need the more recent data, go to [BytePlus RTC Console](https://console.byteplus.com/rtc/workplaceRTC) \> [Realtime Monitor](https://console.byteplus.com/rtc/callQualityRTC/qos) .


The following table describes each item and its calculation method.


|Item |Description |
|---|---|
|Number of users |This count includes normal and invisible users, and excludes duplicates. |
|Number of room joins |A user joining a room for the first time is counted once. The same user joining and leaving the same room repeatedly will only be counted once. |
|Number of rooms |The lifecycle of a room begins when the first user joins and ends when the last user leaves. |
|Number of high\-concurrency rooms |When the number of online users in a room reaches 100, it will be counted as one high concurrent room. This count excludes duplicate room IDs. |
|Peak Number of concurrent rooms |A room with at least one online user is considered an online room. |
|Number of calls per user |Count of user joining rooms / Number of Active Users |
|Average call duration |Call duration / Count of User Joining Rooms<br><br>Total duration of calls include video and audio calls using the RTC SDK |
|Average call duration per user |Call Duration / Number of Active Users<br><br>Total duration of calls include video and audio calls using the RTC SDK |


<span id="dimension"></span>
## Dimension

In [Quality Overview](https://console.byteplus.com/rtc/callQualityRTC/qos) and [Operation Data](https://console.byteplus.com/rtc/callQualityRTC/operation), you can view aggregated data by dimension.


|Dimension |Description |
|---|---|
|Area |The area or country where the user is located |
|Network |The user's network type during the call, including Wi\-Fi, 4G, 5G, and so on. |
|Operation system |The operating system of the device, including Android, iOS, Windows, and so on. |
|SDK version |The version of the RTC SDK |
|Number of users in a call |Only available in [Operation Data](https://console.byteplus.com/rtc/callQualityRTC/operation) |


> The size of a bubble in the chart represents the volume of the sample. A larger sample size is represented by a larger bubble.

> Web data can be displayed by Area, Operating System, and SDK version.


<span id="usage-statistics"></span>
##   Usage Statistics

<span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/cd824798735444e9b1eb851db3ab3021~tplv-k9wyc2ijk0-image.image) </span>

Go to [BytePlus RTC Console](https://console.byteplus.com/rtc/workplaceRTC) \> [Usage Statistics](https://console.byteplus.com/rtc/statisticsRTC) and then select a time range to view the statistical data by app or business ID.


> * You can also get the duration data by calling OpenAPI [ListUsages](https://docs.byteplus.com/en/docs/12/docs-71234).

> * The usage statistics are only for your reference. They are not used for billing purposes. Refer to the bill for billing details.



|Item |Description |
|---|---|
|Duration of video calls |Total minutes of the video calls made by all users through the selected appID, including 360P, 720P, and 1080P. |
|Duration of audio calls |Total minutes of the voice calls made by all users through the selected appID. |
