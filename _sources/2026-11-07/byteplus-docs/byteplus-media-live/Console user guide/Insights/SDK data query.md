---
title: "SDK data query"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-clientdata"
---

This article introduces how to view the push\-based and pull\-based streaming metric data of MediaLive to help you monitor the quality performance of live streaming content on different platforms.

<span id="cbfcf895"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Insights** ＞ **SDK data query,**  and by default, you will enter the **All push streams** tab on the **SDK data query** page.

3. Switch between tabs to view data for **All push streams**, **Single push stream**, **All pull streams**, and **Single pull stream** within the specified time range.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">On the SDK data query page, you can use the following query functions to filter query results more finely.</div>



* <div data-tips="true" data-tips-type="tip">Specify application type: View data by application type. You can choose between App or Web, both of which have accessed the MediaLive client SDK. Currently, only the App is supported.</div>


* <div data-tips="true" data-tips-type="tip">Specify applications: View the SDK metric data of specified applications or all applications. By default, all applications are shown.</div>


* <div data-tips="true" data-tips-type="tip">Specify time: Quickly select a query time or manually specify time interval;</div>


* <div data-tips="true" data-tips-type="tip">Data splitting: Split the displayed data by up to three dimensions. By default, no data splitting is applied.</div>


* <div data-tips="true" data-tips-type="tip">Data aggregation: Select the time granularity of data aggregation.</div>


* <div data-tips="true" data-tips-type="tip">Specify metric: View data for specified metrics or all metrics.</div>


* <div data-tips="true" data-tips-type="tip">Condition filtering: Filter data according to specific value (e.g., equal to or not equal to values).</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When the SDK version is not the latest，there may be a problem of data loss in a certain item, resulting in abnormal values in the data dashboard. If this situation occurs, you can try to update the SDK version.</div>


<span id="d37e31f2"></span>
## Metric description

<span id="de270f9e"></span>
### SDK log reporting timing

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57854bdc6ecc499b8969dc6cf8f31983~tplv-goo7wpa0wc-image.image) </span>


* Setting the URL and calling the play method for the first time is considered a single play event. During this process, only one event tracking log is recorded and reported for each play.

* The playback success log is reported in the start stage when the user stops playing (calling stop method) and the playback stage when the user stops playing (calling stop method).


<span id="bedcc3ec"></span>
### Key quality metrics


|Stream type |Metric |Description |
|---|---|---|
|Push streaming |Average bitrate |Display the trend graph of the average bitrate of all push streams (or single push stream) at the time granularity of data aggregation, as well as the average bitrate during query time. |
||Average frame rate |Display the trend graph of the average frame rate of all push streams (or single push stream) at the time granularity of data aggregation, as well as the average frame rate during query time. |
|Pull streaming |Playback success rate |Refers to the proportion of successful reception and playback of live streams on the audience's device during the streaming process. It can measure the probability that the live stream can be normally pulled by the audience.<br><br>**Calculation method**: Playback success rate ＝ Playback success times / Playback times x 100%. |
||Average first frame latency |Refers to the time elapsed from when the user clicks to watch the live stream or play button to when the first frame of video content is displayed on the screen during the video live streaming process. This measures the audience's wait time for the video to start.<br><br>**Calculation method**: First frame latency ＝ First frame playback timestamp \- User clicks play button timestamp. |
||Video stuttering time per 100 seconds |Refers to the duration of video rendering stuttering every 100s of playback time during the live streaming. It can measure the severity of the stuttering during playback.<br><br>**Calculation method**: Video stuttering time per 100 seconds ＝Video sluttering time during playback / Playback time x 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The video rendering stuttering judgment criterion: When the interval between the rendered video frame and the previous rendered video frame is greater than 200ms, it is counted into the video rendering stuttering duration. By continuously monitoring and optimizing this index, the smoothness of video playback and user experience can be improved.</div><br> |
||Average bitrate |Display the trend graph of the average bitrate of all pull streams (or single pull stream) at the time granularity of data aggregation, as well as the average bit rate within the query time range.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To reduce the impact of bitrate fluctuations during startup, the statistical range of pull stream bitrate excludes the first 5 seconds after playback starts.</div><br> |
||End\-to\-end delay |Refers to the time elapsed from when server push stream after encoding is complete to when the first frame of video is rendered on the screen during the streaming. It measures the audience's waiting time required to start watching the stream.<br><br>**Calculation method**: End\-to\-end delay ＝ AVG (first frame completion rendering timestamp \- the timestamp of the actual stream push after encoding is complete) |
||Average playback time |Display the trend graph of the average playback duration of all pull streams (or single pull stream) in the time granularity of data aggregation and the average playback duration within the query time range. |
