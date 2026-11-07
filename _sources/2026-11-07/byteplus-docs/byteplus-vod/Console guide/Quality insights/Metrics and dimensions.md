---
title: "Metrics and dimensions "
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-dimensions-and-metrics"
---

<span id="dbce7eb2"></span>
## Metrics

A metric is a quantitative measurement, such as an average, ratio, percentage, and so on. It's always a number as opposed to text. This section introduces the metrics that appear on the BytePlus VOD quality platform.

<span id="38074cb4"></span>
### QoS metrics


|**Metric** |**What it is** |**How it is calculated** |
|---|---|---|
|Video views (vv) |Video views are the total number of video playback requests made by users. Note that if a user pauses and plays the video multiple times within a single viewing session, it will still only count as one video view. |N/A |
|Unsuccessful playback rate |A playback is considered unsuccessful if an error occurs during playback and the video cannot be resumed automatically. |Unsuccessful playback rate = (Number of failed playback / Total number of playbacks) × 100%. |
|Actual video views |The term "actual video views" refers to the number of times the first frame is successfully rendered during playback. |N/A |
|Time to first frame (TTFF) |Time to first frame (TTFF) refers to the time difference between when a user clicks the play button and when the first frame of the video is displayed. |TTFF = AVG (The time when the first frame of the video is played \- The time when the user clicks the play button). |
|Video buffering rate |Video buffering occurs when the player buffers video data due to a poor connection. Note that if a user drags a progress bar causing the video to buffer, this is not considered a video buffering event. |Video buffering rate = (Number of video playbacks during which buffering occurs / Total number of playbacks) × 100%. |
|Interruption rate |An interruption occurs when the player encounters an internal error during playback and triggers a retry. The retry may either succeed or fail. |Interruption rate = (Number of video playbacks during which an interruption occurs / Total number of playbacks) × 100%. |
|No play rate |If a user exits before playback is started or the player fails to start playback, it is considered "No play." |No play rate = (Number of video playbacks during which "no play" occurs / Total number of playbacks) × 100%. |
|Video freezes duration within 100 seconds |The duration of video freezes within 100 seconds is a measure of video playback quality. The higher the duration, the worse the viewing experience. |Duration of video freezes within 100 seconds = (Total duration of video freezes / Total video duration) × 100 seconds. |
|Average playback bitrate |The average playback bitrate is the average bitrate of all video files that have been played. |Average playback bitrate = AVG (bit_rate) |
|Average seek time |The average seek time is the average buffering time caused by a user dragging the progress bar to a specific time position. |Average seek time = Total buffering time caused by a user dragging the progress bar / Total number of times a user drags the progress bar.<br><br>This can also be represented by the formula: Average seek time = Sum(seek_dur) / Sum(seek_cnt). |


<span id="b996694e"></span>
### QoE metrics


|**Metric** |**What it is** |**How it is calculated** |
|---|---|---|
|Number of finished playbacks |The "finished playback" refers to playbacks where the last audio or video frame is successfully displayed. Loop playback is counted as one finished playback, and the following cases are also considered finished playbacks:<br><br><br>* When a user drags the progress bar directly to the last frame.<br><br>* When a user drags the progress bar to a specific time position and the player continues playing the video until the last frame is displayed.<br><br>* When a user exits playback during looping playback after the last frame is displayed. |Number of finished playbacks = Sum(finish_cnt). |
|Finished playback rate |The finished playback rate is calculated by dividing the number of finished playbacks by the total number of playbacks. |Finished playback rate = (Number of finished playbacks / Total number of playbacks) × 100%. |
|Number of daily active users |The number of Daily Active Users (DAU) is calculated based on the device ID \- a unique identifier for each device \- by BytePlus VOD. |Number of users = Count(Distinct(device_id)). |
|Video watching time per user |The "video watching time" is the time difference (in milliseconds) between when a user starts playing the video and when they exit playback, excluding the following times:<br><br><br>* When the video is paused.<br><br>* When the progress bar is being dragged.<br><br>* When the video freezes due to poor network connection.<br><br>* The time of retries. |Video watching time per user = Total playback duration / Number of users = Sum(watch_dur) / Count(distinct case when watch_cnt \> 0 THEN device_id end). |
|Number of playbacks per user |The average number of playbacks per user. |Number of playbacks per user = Number of playbacks / Number of users. |
|Number of finished playbacks per user |The "finished playback" refers to playbacks where the last audio or video frame is successfully displayed. Loop playback is counted as one finished playback, and the following cases are also considered finished playbacks:<br><br><br>* When a user drags the progress bar directly to the last frame.<br><br>* When a user drags the progress bar to a specific time position and the player continues playing the video until the last frame is displayed.<br><br>* When a user exits playback during looping playback after the last frame is displayed. |Number of finished playbacks per user = Number of finished playbacks / Number of users = Sum(finish_cnt) / Count (Distinct(device_id)). |
|Average playback duration |The "video watching time" is the time difference (in milliseconds) between when a user starts playing the video and when they exit playback, excluding the following times:<br><br><br>* When the video is paused.<br><br>* When the progress bar is being dragged.<br><br>* When the video freezes due to poor network connection.<br><br>* The time of retries. |Average playback time = Total video watching time / Number of playbacks = Sum (watch_dur) / Sum(watch_cnt). |
|Average video duration |The "video duration" refers to the length of the video obtained from the video header. |Average video duration = AVG(vplay_video_dur). |


<span id="eb0bf28f"></span>
### Cost metrics


|**Metric** |**What it is** |**How it is calculated** |
|---|---|---|
|Bandwidth usage of Player SDK |The bandwidth usage consumed by the Player SDK. |Bandwidth usage of the Player SDK = Sum(player_stream_data) x 8 / 300 |
|Traffic of the Player SDK |The amount of traffic consumed by the Player SDK. |Traffic usage of the Player SDK = Sum(player_stream_data) |


<span id="5774927d"></span>
### External subtitle metrics


|**Metric** |**What it is** |**How it is calculated** |
|---|---|---|
|Plays with subtitles enabled |The total number of plays where subtitles were both available and enabled by the user. |/ |
|Subtitle display failure rate |The percentage of attempts to load subtitles that failed. |This is calculated as the number of failed subtitle requests or loads divided by the total number of times subtitles were enabled. If 100 attempts were made to load subtitles and 20 failed, the failure rate is `20 / 100 = 20%`. |
|Subtitle load time |The average time elapsed from the initial request for subtitles until they are successfully loaded and displayed. This metric indicates how quickly subtitles appear to the user. For playback in Vid mode, this duration includes both the time to fetch subtitle metadata and the time to download the subtitle file itself. |/ |
|Subtitle cache hit rate |The percentage of times subtitles were successfully loaded from the local cache instead of being fetched from the network. This metric measures the effectiveness of the subtitle preloading strategy. |/ |


<span id="9a3c79a7"></span>
### Upload metrics


|**Metric** |**What it is** |**How it is calculated** |
|---|---|---|
|Total uploads |The total number of upload requests made by the user. |Sum(total) |
|Unsuccessful upload rate |The number of uploads that failed as a percentage of the total number of uploads. |Cast(sum(error_filter_not_userstop) as double) / Sum(error_not_userstop_total) \* 100 |
|Average upload speed |The average speed of each upload by a user. |Cast(sum(upload_speed) as DOUBLE) / Sum(valid_speed) |
|Average upload time |The average time taken for each upload by a user. |Cast(sum(upload_duration) as DOUBLE) / Sum(valid_duration) |
|Average uploaded file size |The average file size for each upload by a user. |Cast(sum(file_size) as DOUBLE) / Sum(valid_filesize) / 1024 |
|Error code rate |The number of times the error code appears as a percentage of the total number of uploads. |M = Sum(error_filter_not_userstop)<br><br>D = error_code |


<span id="61a5815c"></span>
## Dimensions

A dimension is an attribute of your data. It describes your data and it's usually text as opposed to numbers. The following table lists the dimensions that appear on the BytePlus VOD quality platform.


|**Dimension** |**What it is** |
|---|---|
|Operating system |The operating system used by users on your application. Typical operating systems include 'Android', 'iOS', and 'Windows'. |
|Business tag |The business tag is used to differentiate between various types of audio and video content under the same App ID. For example, you can categorize videos based on their length, such as short or long videos. To set the business tags, use the following code:<br><br><br>* For iOS Player SDK:<br><br>   ```objectivec```<br>```   [videoEngine setOptionForKey:VEKKeyLogTag_NSString value:@"tag"];```<br>```   ```<br>   <br><br>* For Player SDK:<br><br>   ```Java```<br>```   mVideoEngine.setTag("tag");```<br>```   ```<br>    |
|Business subtag |The business subtag is used to differentiate even further between various types of audio and video content under the same business tag. For example, you can categorize videos based on whether they are encrypted or not. To set the business subtag, use the following code:<br><br><br>* For iOS Player SDK:<br><br>   ```objectivec```<br>```   [videoEngine setOptionForKey:VEKKeyLogSubTag_NSString value:@"subtag"];```<br>```   ```<br>   <br><br>* For Player SDK:<br><br>   ```Java```<br>```   mVideoEngine.setSubTag("subtag");```<br>```   ```<br>    |
|App version |Your app's version. |
|Player SDK version |The version of the Player SDK that was integrated into your app. |
|Video codec |The code of the video that was played, such as "h264". |
|Audio codec |The code of the audio that was played, such as "mp3". |
|Operating system with version |The operating system and version on which the video was played, such as "Android 13" and "iOS 14". |
|Playback method |The method by which the video was played, such as "vid" and "dir_url". |
|Video container format |The container format of the video that was played, such as "mp4". |
|Hardware decoding |Whether hardware decoding was used to play the video. |
|Video resolution |The width and height (in pixels) of the video that was played. Examples include "640p", "720p", and "4k". |
|Network |The type of network in which the video was played, such as "wifi". |
|CDN vendor |Your custom CDN vendor. |
|Domain name |The domain name used for video playback, such as "https://www.xxxxx.byteplus.com/". |
|Distribution channel |The channel from which your mobile app can be downloaded and installed, such as the App Store on iOS. |
|Level of device model |Device models are categorized based on their performance scores, with some being labeled as "high\-end devices". |
|Error code of the Player SDK |The [error code](https://docs.byteplus.com/en/byteplus-vod/docs/error-code) reported by the Player SDK. |
