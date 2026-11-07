---
title: "Generating stream addresses"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator"
---

Use the address generator tool in the MediaLive console to generate push and pull stream addresses for your live stream.

> **说明**

> For more information about address composition rules and generation methods, see [Generating live\-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses).

## Prerequisites

* You have added domain names for stream pushing and pulling and completed the CNAME configuration. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain) and [Adding a CNAME record](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record).

* Enable HTTPS if you need to:

   * Use the online push streaming tool provided by the BytePlus MediaLive console.

   * Use the online playback tool provided by the BytePlus MediaLive console.

   * Use HTTPS push or pull stream addresses.

   * Push or play RTM streams in a browser environment.

      For more information, see [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).

* To perform URL authentication for push or pull stream addresses, you must enable URL authentication. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

* To generate pull stream addresses for transcoded streams, you must complete the transcoding configuration. For more information, see [Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).

* To generate pull stream addresses for ABR streams of specific protocols, you must complete the ABR configuration and select the corresponding protocol type. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

* To generate pull stream addresses for encrypted streams, you must complete the encryption configuration. For more information, see [Managing encryption configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task).

## Procedure

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Toolkits** \> **Address generator**.

3. Select the **Address type** and **Domain name**, and enter a custom `AppName`, `StreamName`, and expiration time.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/305f90015f364f2e8ce96f4f455612de~tplv-goo7wpa0wc-topic.webp)

   |Parameter |Description |
   |---|---|
   |Address type |Select the type of address to generate.<br><br><br>* **Push stream address**: Use this address to push a stream from the host to MediaLive.<br><br>* **Pull stream address**: Use this address to pull a stream from MediaLive to viewers. |
   |Domain name |Select a domain name for stream pushing or pulling based on the address type. |
   |AppName |The `AppName` for the generated address, which can include letters (A\-Z, a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. The default value is `live`.<br><br>> **说明**<br><br><br>> When pulling the specified stream, the `AppName` for the push and pull stream addresses must be the same.<br> |
   |StreamName |The `StreamName` for the generated address, which can include letters (A\-Z, a\-z), numbers (0\-9), underscores (_) and hyphens (\-), with a length ranging from 1 to 100 characters.<br><br>> **说明**<br><br><br>> When pulling the specified stream, the `StreamName` for the push and pull stream addresses must be the same.<br> |
   |Expiring on |Select when the address expires.<br><br>After expiration, the address can no longer be used to initiate new requests to push or pull streams. Existing requests initiated before expiration are not affected.<br><br>> **警告**<br><br><br>> You can configure the expiration time only when URL authentication is enabled for the selected domain. To enable URL authentication, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).<br> |

4. Click **Generates Push stream address** or **Generates Pull stream address** to get push or pull stream addresses in the **Result** section.

   * **Push stream address**: Supports generating push stream addresses with authentication information. The address generator supports the following push protocols: RTMP, TS over SRT, RTMP over SRT, and RTM.

      > **说明**

      * > If you use OBS (Open Broadcaster Software) to push streams over RTMP, you can get the **OBS push stream address** and **OBS Streaming Key** from the generated results, and enter them in the **Server** and **Stream Key** fields in OBS respectively.

      * > To include authentication information, you must first enable URL authentication for the domain name for stream pushing. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c168f4ac83b440cd85c8caffef3d8286~tplv-goo7wpa0wc-topic.webp)

* **Pull stream address**: Supports generating pull stream addresses with authentication information for source streams, transcoded streams, and ABR streams. The address generator supports the following pull protocols: RTMP, FLV, HLS (M3U8), RTM, and DASH.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ba7e572d98e4d6f83fb4492893052aa~tplv-goo7wpa0wc-topic.webp)

   * On the **Pull Stream URL** tab, you can find two kinds of RTM pull stream addresses.

      * **RTM Web SDK playback address**: Use this address for playback with the BytePlus MediaLive Player SDK for Web. This address triggers automatic transcoding as follows:

         * The system automatically detects whether the stream contains B\-frames.

            * If B\-frames are present: The stream is transcoded to remove the B\-frames, and standard transcoding fees apply.

            * If B\-frames are not present: The video in the source stream is copied, and no video transcoding fees apply.

         * The system automatically detects whether the audio codec is AAC or Opus.

            * If the audio codec is AAC: The audio is converted to Opus. If no video transcoding is involved, audio\-only transcoding fees apply. For more information, see [Audio\-only transcoding](/docs/byteplus\-media\-live/docs\-transcoding#Audio transcoding).

            * If the audio codec is Opus: The audio in the source stream is copied, and no audio\-only transcoding fees apply.

      * **RTM address**: Use this address for playback with client SDKs (BytePlus MediaLive Player SDKs for iOS, Android, React Native, and Flutter) and other players.

   * On the **Transcoding stream** tab, you can select a transcoding suffix to get different transcoded stream addresses. You can also find two kinds of RTM pull stream addresses.

      * **RTM Web SDK playback address**: Use this address for playback with the BytePlus MediaLive Player SDK for Web. This RTM pull stream address preserves the original transcoding configuration and adds the following processing:

         * The system automatically detects whether the stream contains B\-frames.

            * If B\-frames are present: The stream is transcoded to remove the B\-frames, while the other settings follow the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

            * If B\-frames are not present: The stream is transcoded according to the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

         * The system automatically detects whether the audio codec is AAC or Opus.

            * If the audio codec is AAC: The audio is converted to Opus, while the other settings follow the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

            * If the audio codec is Opus: The audio is copied without audio transcoding, while the other settings follow the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

      * **RTM address**: Use this address for playback with client SDKs (BytePlus MediaLive Player SDKs for iOS, Android, React Native, and Flutter) and other players.

   * On the **Adaptive bitrate** tab:

      * Depending on the ABR configuration, the HLS\-ABR address uses either the default `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/abr.m3u8?{AuthInfo}` format or the relative\-path `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}_abr.m3u8?{AuthInfo}` format. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

      * If RTM\-ABR is enabled in the ABR configuration, select the startup quality level (suffix) to get the corresponding RTM\-ABR address. You can also find two kinds of RTM\-ABR pull stream addresses.

         * **RTM Web SDK playback address**: Use this address for playback with the BytePlus MediaLive Player SDK for Web. This RTM\-ABR pull stream address preserves the original ABR configuration and adds the following processing:

            * The system automatically detects whether the substream contains B\-frames.

               * If B\-frames are present: The substream is transcoded to remove the B\-frames, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

               * If B\-frames are not present: The substream is transcoded according to the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

            * The system automatically detects whether the audio codec is AAC or Opus.

               * If the audio codec is AAC: The audio is converted to Opus, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

               * If the audio codec is Opus: The audio is copied without audio transcoding, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

         * **RTM address**: Use this address for playback with the BytePlus MediaLive Player SDKs for iOS and Android, and other players.

   > **说明**

   * > To include authentication information, you must first enable URL authentication for the domain name for stream pulling. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

   * > If you cannot get the **RTM Web SDK playback address**, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

5. You can also:

   * Click the online streaming icon to start streaming on the **Web push** page of the console.

   * Click the online playback icon to start playback on the **Web pull** page of the console.

   * Click the copy icon to copy the address.

   * Click the QR code icon to view the QR code.

   * Click **History** in the upper\-right corner of the page to view previously generated address records.

## What to do next

* Use the [Web push](https://console.byteplus.com/live/main/WebPushStream) and [Web pull](https://console.byteplus.com/live/main/webPullStream/play) tools provided by the MediaLive console to try push and pull streaming over HTTPS.

* Use the VePlayer [Web player V1](https://demo.byteplus.com/common/veplayer/basic/example?tab=function-display) based on Web Player SDK 1.x and developed in collaboration with BytePlus VOD to try various web playback features.

* Use the VePlayer [Web player V2](https://demo.byteplus.com/common/veplayer/v2/basic/example?tab=function-display) based on Web Player SDK 2.x and developed for MediaLive to try various web playback features.
