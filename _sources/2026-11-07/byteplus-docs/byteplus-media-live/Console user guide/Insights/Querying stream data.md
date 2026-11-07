---
title: "Querying stream data"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-querying-stream-data"
---

Use **Stream data query** to access comprehensive data related to your live streaming services, enabling efficient monitoring, analysis, and troubleshooting of your streams. This module provides detailed insights into push\-stream performance, pull\-stream metrics, and various callback events.

<span id="1ab3a720"></span>
## Module Overview

The **Stream data query** module offers the following key capabilities to help you manage and analyze your live streaming data:


* **Access Push Stream Data:**  View detailed statistics (e.g., bitrates, frame rates, PTS) for quality analysis and historical records (e.g., streaming time, duration, termination reasons) for troubleshooting unexpected disconnections.

* **Monitor Pull Stream Data:**  Track key performance indicators such as bandwidth consumption, traffic volume, and the number of concurrent online viewers, vital for assessing content delivery performance.

* **Query Deleted Domain Data:**  Retrieve push\-stream and pull\-stream data associated with deleted domain names, providing valuable historical insights even after their deprecation.

* **Retrieve Callback Records:**  Access detailed information about various callback events (e.g., stream start, stream end, recording, screenshots), essential for troubleshooting callback issues and validating data integrity across your streaming workflows.


<span id="b54cf4d4"></span>
## Prerequisites


* You must have actual push\-stream and pull\-stream data.

* Prepare the domain name, App Name, and Stream Name for your query stream.


<span id="7d15b599"></span>
## Procedure

<span id="79df0818"></span>
### Querying push\-stream data

Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/streamstatistics/pushstream) and navigate to **Stream Data Query \> Push stream data**.

<span id="statistics-of-push-streams"></span>
#### Statistics of push streams


1. In the **Statistics** tab, select a domain name and enter the App Name and Stream Name.

2. Specify the time granularity and time range for your query.

3. Click **Search**.

4. Hover the mouse over the graph to view the bitrates, frame rates, PTS, and time intervals between two consecutive frames.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16034b3fe16d4972836ffcaa60b78fab~tplv-goo7wpa0wc-image.image) </span>


<span id="history-of-push-streams"></span>
#### History of push streams


1. In the **History** tab, select a domain name and enter the App Name and Stream Name. Specify the time granularity and time range.

2. Click **Search**.

3. You can investigate and troubleshoot the unexpected streaming interruption.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c1b36e8268d454c586727d91d983514e.png) </span>


Common causes of streaming interruption are listed as follows. If the cause is not listed in the following table, or you cannot determine the solution, [create a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) and contact technical support.


|**Cause of streaming interruption** |**Description** |
|---|---|
|FLV protocol parsing failed |FLV protocol parsing failed, which interrupted the push stream. |
|RTMP protocol is incompatible |RTMP protocol is incompatible, which interrupts the push stream. |
|TLS protocol failed |TLS protocol failed, which interrupted the push stream. |
|No data received for a long time |No data is transmitted on the push stream terminal for a long time, resulting in a timeout. |
|Actively disconnected by the push stream terminal |The push stream terminal causes the push stream to be disconnected by performing operations other than stopping the live stream normally, such as network interruption or directly closing the push stream software. |
|Data reading timeout |The push stream is disconnected due to data I/O errors in the MediaLive center |
|High\-priority stream replaces low\-priority stream |A low\-priority stream is disconnected when it is replaced by a high\-priority stream. |
|Authentication parameters are invalid |The URL authentication parameter field is invalid or authentication times out. As a result, the push stream is interrupted. |
|Live stream is disabled |The live stream is disabled and the push stream is disconnected. |
|The console disconnects the live stream |Call the KillStream interface and the live stream is interrupted |
|Internal error |The MediaLive center has an error. Please contact technical support. |
|Remote authentication failed |Remote authentication failed, which interrupted the push stream. |
|Push stream disconnected |The push stream is disconnected for complex reasons. Please contact technical support. |
|Push stream ends normally |The push stream terminal ends the live stream normally with the Stop Live function. |
|Network exception |The network is abnormal, which interrupts the push stream. |
|Repeated pushing of the same stream ID |Pushing a stream with the same stream name interrupts the push stream. |


<span id="621b7e63"></span>
### Querying pull\-stream data


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left navigation pane, click **Stream Data Query \> Pull stream data**.

3. Fill in the stream address in the **Search Address** box. You can enter either a push stream or a pull stream address.

4. Specify the time granularity and time range.

5. You can also customize your query by specifying the streaming protocol, operator, regions that correspond to the edge servers' IP addresses, and external IP addresses of client devices.

6. Click **Search**. Click each tab to view the corresponding statistics.


<span id="293b842a"></span>
#### Bandwidth data


1. Hover the mouse over the graph to view the bandwidth data for a specific time.

2. You can display data with a line graph, a bar graph, or a list.

3. You can view or download your search results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/631b274975d14cb48c60aaa278374763~tplv-goo7wpa0wc-image.image) </span>


<span id="ea6d28bd"></span>
#### Traffic data


1. Hover the mouse over the graph to view the traffic data for a specific time.

2. You can display data with a line graph, a bar graph, or a list.

3. You can view or download your search results.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0e770d23dc54ba4b6ec3f57974df9a0~tplv-goo7wpa0wc-image.image" width="860px" />   </div>
   


<span id="8d4da7f8"></span>
#### Online viewers


1. Hover the mouse over the graph to view the number of online viewers for a specific time.

2. You can display data with a line graph, a bar graph, or a list.

3. You can view or download your search results.


<span id="d7ea272c"></span>
### Querying Callback Records

The **Callback records** module allows you to query detailed information about various callback events configured for your streaming services, such as stream start, stream end, recording, and screenshot events.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left navigation pane, navigate to **Stream Data Query** and click **Callback records**.

3. On the **Callback records** page, specify your query criteria using the available filters in the search bar:

   
   |Parameter |Description |
   |---|---|
   |Domain |Select the domain name associated with the callback event. |
   |AppName |Enter the application name where the stream was published. |
   |StreamName |Enter the specific stream name. |
   |Callback type |Select the type of callback event to query. Options include stream pushing starts, stream pushing ends, recording events, and screenshot events. |
   |Callback status |Filter results by the status of the callback (e.g., Success, Failed). |
   |Time range |Choose a predefined time range (e.g., Last 30 mins, Last 4 hours, Last 24 hours) or select a custom date range using the calendar selectors. |
   

4. Click **Search** to retrieve the callback records.

5. The results table displays details for each matching callback event, including **Stream Name**, **App Name**, **Domain Name**, **Callback time**, **Callback status**, **Callback event type**, **Callback address**.

6. To view the detailed content of a specific callback event, click the **Details** button in the **Callback content** column for the desired record.

7. The **Callback content details** panel displays comprehensive information about the callback:

   
   |Parameter |Description |
   |---|---|
   |Callback status |The overall status of the callback (e.g., Success, Failed). |
   |Callback type |The specific type of callback event (e.g., Stream pushing starts, Recording events). |
   |Callback trigger time |The exact time when the callback was triggered by the system. |
   |Stream content |Data related to the stream's state or event that triggered the callback. |
   |Callback content |The actual JSON or text content of the callback payload sent by MediaLive to your configured callback URL. |
   |Response Time |The time when MediaLive received a response from your callback URL. |
   |Response content |The actual response body received from your callback URL. |
