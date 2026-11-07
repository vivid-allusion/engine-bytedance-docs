---
title: "Pushing a stream through the console"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-web-push"
---

This topic describes how to push streams through the BytePlus MediaLive console by using the **Web push** tool. You can quickly generate a push stream address and test BytePlus MediaLive features by pushing streams from the camera, screen share, or a local or online video file.

If you want to see the streamed content, you can use the [Web pull](https://docs.byteplus.com/byteplus-media-live/docs/web-pull) tool. Refer to [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost) for a detailed explanation of how push and pull stream addresses are related.

Web Push integrates the BytePlus MediaLive Broadcast SDK for Web. To integrate the SDK into your own application, refer to [Broadcast SDK for Web: SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web).

<span id="Prerequisites"></span>
## Prerequisites


* A domain name for stream pushing, with an SSL certificate configured. Refer to [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain) and [Adding an SSL certificate ](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)for more information.

* A camera and a microphone. Your browser should have permission to use the camera and microphone.


<span id="Procedure"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, go to **Toolkits** \> **Web push**.

3. Select the video source in the **Screen selection** section. You can choose your camera, screen share, a local video file, or an online MP4 file as the video source.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/194e73ab45e0489ab68e4402274f1b98~tplv-goo7wpa0wc-image.image) </span>

4. Select the audio source in the **Audio selection** section. In particular, you can upload a local audio file or add the address of an online MP3 file as the background audio.

5. Configure capture and push settings. You can use recommended settings or custom ones. For recommended settings, you may refer to the table below for more information.

   Video settings:

   
   |**Configuration** |**Resolution, frame rate, and bitrate** |
   |---|---|
   |120p |160x120, 15 fps, 200 Kbps |
   |180p |320x180, 15 fps, 350 Kbps |
   |240p |320x240, 15 fps, 400 Kbps |
   |360p |640x360, 15 fps, 800 Kbps |
   |480p |640x480, 15 fps, 900 Kbps |
   |720p\-1 |1280x720, 15 fps, 1500 Kbps |
   |720p\-2 |1280x720, 25 fps, 1500 Kbps |
   |720p\-3 |1280x720, 30 fps, 1500 Kbps |
   |1080p\-1 |1920x1080, 15 fps, 2000 Kbps |
   |1080p\-2 |1920x1080, 25 fps, 2000 Kbps |
   |1080p\-3 |1920x1080, 30 fps, 2000 Kbps |
   

   Audio settings:

   
   |**Configuration** |**Sample rate and bitrate** |
   |---|---|
   |STANDARD |48000 Hz, 40 Kbps |
   |HIGH |48000 Hz, 128 Kbps |
   

6. Enter an RTM push stream address. If you do not have the address already, click **Generate** under the preview window to generate one.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4dc17c1aaea4a068065bd6a78e52c49~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Web Push supports HTTPS addresses only. Additionally, please ensure that you include port number 9922 in the push stream address. The correct format should be: <code>https://{DOMAIN_NAME}:9922/{APP_NAME}/{STREAM_NAME}.sdp</code>.   </div>
   

7. Click **Start** to start pushing the stream.


<span id="Result"></span>
## Result


* Once you successfully start streaming, you will receive callback notifications in the **Callback notification** section notifying you that the connection is established. The notifications will also include detailed streaming statistics, such as codecs and bitrates. You can read, clear, or pause/restore callback notifications.

* During the streaming process, you can turn off the audio or video, change the audio and video sources, or change the capture settings.

* To stop streaming, click **Stop pushing**.


<span id="1857c856"></span>
## FAQ

If you receive the error message "[2001] Failed to fetch" in the **Callback notification** section after clicking **Start**, it means that an error has occurred during the SDK's attempt to push the stream. This error is commonly caused by network issues. We recommend waiting for a brief period of time before attempting to start the stream again.
