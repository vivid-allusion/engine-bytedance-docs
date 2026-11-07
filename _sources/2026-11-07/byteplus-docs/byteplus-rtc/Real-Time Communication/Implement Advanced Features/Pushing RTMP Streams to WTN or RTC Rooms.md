---
title: "Pushing RTMP Streams to WTN or RTC Rooms"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1627491"
---

You can use standard RTMP tools (like OBS or FFmpeg) to push streams to WTN for large\-scale, low\-latency distribution, or directly into an RTC room for interactive live streaming—without needing to integrate an RTC SDK on the publisher's side. Pushing to an RTC room allows you to leverage full RTC features, like room\-based user management and real\-time call monitoring.

<span id="scenarios"></span>
## Scenarios


* **Interactive Live Streaming & Co\-hosting**: Push professional broadcast feeds, drone footage, or professional camera streams directly into an RTC room to participate in interactive sessions.

* **IP Camera/Hardware Integration**: Directly integrate IP cameras, industrial monitoring equipment, or hardware encoders into your RTC ecosystem without custom SDK integration.

* **Large\-scale Distribution**: Push RTMP streams into the WTN for millisecond\-level, global low\-latency distribution.


<span id="billing"></span>
## Billing

For billing\-related information, refer to [Billing of Push Media Stream to WTN](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392587).

<span id="restrictions"></span>
## Restrictions


* **Stream Format**: Must be an audio\-video stream. Pure audio or pure video is not supported.

* **Codec Format**: The video codec must be H.264, and the audio codec must be AAC.

* **Video Frames**: The video stream must not contain B\-frames. You can disable B\-frames by setting the `Profile` to `baseline` in your streaming software.

* **Stream Limit**: The number of concurrent RTMP streams under a single AppID should not exceed 5,000.


<span id="implementation"></span>
## Implementation

<span id="step-1-enable-the-feature"></span>
### Step 1: Enable the Feature


1. Log in to the [RTC console](https://console.byteplus.com/rtc), navigate to **Settings**.

2. Select your target application from the dropdown menu, then click the **Push Stream to WTN** tab.

3. Click the toggle switch to enable the function.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07c8d16ce128418d96670b4eabc47248~tplv-goo7wpa0wc-image.image) </span>


<span id="step-2-construct-the-push-url"></span>
### Step 2: Construct the Push URL

<span id="push-to-wtn"></span>
#### Push to WTN


<Tabs>
<Tab zoneid="I8Wcw8AQxe" title="Push via Domain">
<TabTitle>Push via Domain</TabTitle>

**URL Format**

```Plain
rtmp://wtn.rtcoversea.com/app/{streamID}?app_id={AppId}&vhost=rtmp_streaming&token=Bearer+{Token}
```



* `{streamID}`: A unique, user\-defined string that identifies the stream to push.

* `{Token}`: Generate and URL\-encode this by following the [Authentication Rules](https://docs.byteplus.com/en/docs/byteplus-rtc/132442).


</Tab>
<Tab zoneid="N22izXnVix" title="Push via IP Address">
<TabTitle>Push via IP Address</TabTitle>

**URL Format**

```Plain
rtmp://{ip}:{port}/app/{streamID}?app_id={AppId}&vhost=rtmp_streaming&token=Bearer+{Token}
```



* `{ip}`, `{port}`, `{streamID}`, `{AppId}`: Call [RtmpAccessInfo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392589) to obtain them.

* `{Token}`: Follow the [Authentication Rules](https://docs.byteplus.com/en/docs/byteplus-rtc/132442) to generate and URL\-encode a `Token`.


</Tab>
</Tabs>


<span id="005bd920"></span>
#### Push to an RTC Room

URL Format:

```Plain
rtmp://wtn.rtcoversea.com/app/{streamID}?app_id={AppId}&room_id={RoomID}&user_id={UserID}&vhost=rtmp_streaming_rtc&token=Bearer+{Token} 
```



|Parameter |Description |
|---|---|
|`{streamID}` |A unique, user\-defined string that identifies the stream. |
|`{RoomID}` |The ID of the RTC room you want the stream to join. |
|`{UserID}` |The user ID to assign to the RTMP stream publisher within the room. Other users will use this ID to subscribe. |
|`{Token}` |Generate it using the `AppId`, `RoomID`, and `UserID`. For instructions, refer to [Authentication with Token](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70121). |


<span id="step-3-push-the-stream"></span>
### Step 3: Push the Stream

Use OBS, FFmpeg, or another RTMP library to push the stream.


1. Go to the [OBS official website](https://obsproject.com/) to download OBS.

2. Add an input source: In the Sources tab, click + to add your video/audio source.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_64d2674d577a8ab176d13a9ce801bce2.png) </span>

3. Configure the stream.

   1. In the bottom\-right corner of the main window, click **Settings** to open the settings window.

   2. Click the **Stream** tab and set **Service** to **Custom**.

      * **Server**: Paste the complete URL (domain or IP\-based) from [Step 2: Construct the Push URL](https://docs.byteplus.com/docs/byteplus-rtc/docs-1627491#step-2-construct-the-push-url).

      * **Stream Key**: Leave this blank.

         <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2d4e247d6445a9fe6ecfa40577ca6a2b.png) </span>

4. Set Output Parameters.

   Go to the **Output** tab and select **Advanced** mode. For ultra\-low latency and compatibility, apply these settings:

   * **Keyframe Interval**: `2`

   * **CPU Usage Preset**: `ultrafast`

   * **Profile**: `baseline` (to remove B\-frames)

   * **Tune**: `zerolatency`

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_85bcf9ed16aef2aa6bb2c3ce8c67fa25.png) </span>

5. Go to the  **"Video"**  tab to set your stream's quality.

   Set your desired **Resolution** and **FPS (Framerate)** . These settings control the clarity and smoothness of your stream. For recommendations on matching Bitrate, Resolution, and FPS, refer to the [Encoding parameter reference](https://docs.byteplus.com/docs/byteplus-rtc/docs-70122#encoding-parameter-reference).

6. In the bottom\-right corner, click **Start Streaming**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7c53f136f166c6aa3e4d61c587150fec.png) </span>


Use the command\-line interface to push your stream. The video encoding should be H.264, audio encoding should be AAC, and the container format should be FLV. It is recommended to set the GOP to 2 seconds.


* FFmpeg command line

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For a detailed explanation of common parameters, see <a href="https://docs.byteplus.com/docs/byteplus-rtc/docs-1627491#appendix-common-ffmpeg-parameters">Appendix: Common FFmpeg Parameters</a>. For a full list, refer to the <a href="https://ffmpeg.org/ffmpeg.html">FFmpeg official website</a>.   </div>
   

   ```Bash
   ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} 
   ```
   

* The following example shows reading a file and pushing it to WTN:

   `<Your_Final_Complete_URL>` : Replace with your complete URL from [Step 2: Construct the Push URL](https://docs.byteplus.com/docs/byteplus-rtc/docs-1627491#step-2-construct-the-push-url).

   ```Bash
   # Replace the input file and the URL with your own
   ffmpeg -re -i sample.flv -c:v libx264 -profile:v baseline -f flv <Your_Final_Complete_URL>
   ```
   


<span id="3fccbc7f"></span>
### Step 4: Subscription & Play

<span id="9a6b697c"></span>
#### Subscribing to a Stream in an RTC Room

Once the stream is successfully pushed to an RTC room, it is recognized as a regular participant. You can manage and subscribe to this stream using standard RTC SDK methods.


|Function |Description |
|---|---|
|Perception & Callbacks |Other users in the same room will receive the following SDK callbacks:<br><br><br>* **User Joined/Left**: onUserJoined and onUserLeave (triggered when the RTMP stream starts or stops).<br><br>* **Stream Published/Removed**: onUserPublishStreamAudio/onUserPublishStreamVideo (triggered when the media track is added or removed). |
|Subscribe |* **Automatic Subscription**: If your RTC SDK is configured for automatic subscription, the stream will be subscribed to automatically upon detection.<br><br>* **Manual Subscription**: If manual subscription is enabled, you must call APIs to receive the video and audio stream.<br><br>   * Native SDK: call the subscribeStreamVideo/subscribeStreamAudio method. See details in [Client API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-client-api).<br><br>   * Web SDK: call [subscribeStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#rtcengine-subscribestream) method. |
|Termination |Simply disconnect the stream from your RTMP tool (OBS/FFmpeg). The RTC system will detect the loss of connection, automatically trigger the onUserLeave and onUserUnpublishStream callbacks to all participants, and release all room resources. |


<span id="c8789d52"></span>
#### Playing a WTN Stream

After pushing the RTMP stream to WTN, you can play the stream using the StreamID you defined in your push URL via the following two methods:


* Using the RTC SDK:

   You can call the [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#subscribewtnvideostream) (Native)/ [startPlayWTN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#wtnstream-startplaywtn) (Web) interface and pass the StreamID to play the ultra\-low\-latency stream.

* Using the WebRTC protocol:

   * Call the [Create Subscription Resource](https://docs.byteplus.com/en/docs/byteplus-rtc/132484) interface and pass the StreamID to create a subscription resource.

   * Refer to [Subscriber: Subscribe to and Play Audio and Video Streams](https://docs.byteplus.com/en/docs/byteplus-rtc/132450#step-5-publishing-side-and-subscription-side-exchange-sdp-offer-via-wtn) to play the ultra\-low\-latency stream.


<span id="appendix-common-ffmpeg-parameters"></span>
## **Appendix: Common FFmpeg Parameters**


* Common FFmpeg Options

   
   |Option |Description |
   |---|---|
   |\-re |Read input at the native frame rate, usually only used for reading local files |
   

* The configurable options for **output_file_options** include:

   
   |Option |Description |
   |---|---|
   |\-c:v |Video encoding, it is recommended to use libx264 |
   |\-b:v |Video bitrate, for example, 1500k means 1500kbps |
   |\-r |Video frame rate |
   |\-profile:v |Video profile. Specifying `baseline` will not encode B\-frames as the RTC backend does not support B\-frames |
   |\-g |GOP frame interval |
   |\-c:a |Audio encoding, it is recommended to use libfdk_aac |
   |\-ac |Number of audio channels, set to 2 or 1 |
   |\-b:a |Audio bitrate |
   |\-f |Specify the format, and always use `flv`. Use the FLV container for packaging when sending to RTC |
