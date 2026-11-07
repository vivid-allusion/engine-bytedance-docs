---
title: "OBS"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/1125988"
---

To publish real\-time media streams to WTN, you can use the native WHIP (WebRTC\-HTTP Ingestion Protocol) support in OBS. This guide provides step\-by\-step instructions on how to configure OBS to push streams to WTN, allowing you to leverage its ultra\-low latency, stable, and reliable transmission service.

<span id="prerequisites"></span>
## Prerequisites


* A macOS, Ubuntu, or Windows device with a camera and microphone.

* OBS 30.1+ is installed. To install or upgrade OBS, see [Download OBS Studio](https://obsproject.com/download).


<span id="obtain-the-url-for-pushing-streams-to-wtn-using-whip"></span>
## Obtain the WHIP Push URL


1. Call the API to create the publishing resource, and get the publishing address `location` from the response. See [Create Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132482).


<span id="start-obs-and-set-the-push-stream-parameters"></span>
## Start OBS and Configure Streaming Settings


1. Open OBS and go to the settings page.

2. On the streaming settings page, fill in the relevant information:

   * Select `WHIP` as the service.

   * Enter the WTN push address you obtained previously.

   * For `Bearer Token`, enter the token you used to create the publishing resource.

3. Save the settings.


Your settings should look like this:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6947a0bc054d19963f94e3a88d861888.png) </span>

<span id="start-live-streaming"></span>
## Start Live Streaming


1. Add audio and video sources.

2. Start live streaming.


<span id="check-the-subscribed-stream"></span>
## Verify the Stream

Build the web app using the demo project, and then use the demo to subscribe to the upstream media stream from OBS. See [Web](https://docs.byteplus.com/docs/byteplus-rtc/132447).
