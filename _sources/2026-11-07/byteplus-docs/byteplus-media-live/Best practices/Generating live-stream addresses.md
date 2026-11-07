---
title: "Generating live-stream addresses"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generating-live-stream-addresses"
---

To begin your live stream, you need valid push and pull stream addresses. This topic provides instructions for generating these addresses through three different methods: manual construction for batch operations, the console's address generator tool for quick, single\-address generation, and API calls for seamless integration into your applications.

## Usage scenarios

* **Manual construction**: Suitable for generating push/pull stream addresses in batches for your business applications. By following the provided address construction rules, you can use the MediaLive service without making API calls.

* **Using the address generator tool**: Ideal for generating a single stream address. No coding is required, as this can be done directly on the page.

* **Using the API**: Suitable for integrating the live streaming function into your application to automatically generate live streaming addresses.

## Context

### Address information description

A live address typically consists of `Domain`, `AppName`, and `StreamName`, and if you have URL authentication enabled, it also includes authentication information.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/760f0061f25f4875ba068a1910305167~tplv-goo7wpa0wc-topic.webp)

The following table describes the live address parameters.

|Parameter |Description |
|---|---|
|Domain |The domain name you have added.<br><br><br>* Use your domain name for stream pushing to generate the push stream address.<br><br>* Use your domain name for stream pulling to generate the pull stream address.<br><br><br>> **Note**<br><br><br>> To use a pull stream address to play a live stream pushed through a specific push stream address, the domain names for stream pushing and pulling must belong to the same domain name space.<br> |
|AppName |The `AppName` of the live stream. When pulling the specified stream, the `AppName` for the push and pull stream addresses must be the same. |
|StreamName |The `StreamName` of the live stream. When pulling the specified stream, the `StreamName` for the push and pull stream addresses must be the same.<br><br>> **Note**<br><br><br><br>* > After [URL authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication) is enabled, the `StreamName` used for authentication calculation is as follows:<br><br><br>   * > Source stream addresses:<br><br><br>      * > For the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, use `{StreamName}_autortm`, such as `test_autortm`.<br><br><br>      * > For other source stream addresses, use `{StreamName}`, such as `test`.<br><br><br>   * > Transcoded stream addresses:<br><br><br>      * > For the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, use `{StreamName}{Suffix}_autortm`, such as `test_hd_autortm`. `Suffix` is the transcoding suffix in your transcoding configuration.<br><br><br>      * > For other transcoded stream addresses, use `{StreamName}{Suffix}`, such as `test_hd`.<br><br><br>   * > ABR addresses:<br><br><br>      * > For HLS\-ABR absolute\-path addresses, use `{StreamName}`, such as `test`.<br><br><br>      * > For HLS\-ABR relative\-path addresses and DASH\-ABR addresses, use `{StreamName}_abr`, such as `test_abr`.<br><br><br>      * > For RTM\-ABR pull stream addresses for the BytePlus MediaLive Player SDKs for iOS and Android, and other players, use `{StreamName}{Suffix}`, such as `test_uhd`. `Suffix` is the substream suffix in your ABR configuration.<br><br><br>      * > For the RTM\-ABR pull stream address for the BytePlus MediaLive Player SDK for Web, use `{StreamName}{Suffix}_autortm`, such as `test_uhd_autortm`.<br> |
|AuthInfo |Refer to [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication) to understand the URL authentication structure and construct the authentication string. |

### Address composition rules

Address formats and composition rules vary by transport protocol, as shown below:

**Push stream address**

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/643156abf4e14e9b914050c72af157ba~tplv-goo7wpa0wc-topic.webp)

* RTMP push stream address: `rtmp://{DomainNameForStreamPushing}/{AppName}/{StreamName}?{AuthInfo}`. For example, `rtmp://push.example.com/live/test?expire=1782309627&sign=a6937f4926****7b05f3987b088d473c`. If you use OBS to push streams, use `rtmp://{DomainNameForStreamPushing}/{AppName}/` as the **Server**, and `{StreamName}?{AuthInfo}` as the **Stream Key**.

   > **Note**

   > To generate an RTMPS push stream address, replace `rtmp://` in the generated RTMP address with `rtmps://`.

* TS over SRT push stream address: `srt://{DomainNameForStreamPushing}:9000?streamid=#!::h={DomainNameForStreamPushing},r={AppName}/{StreamName},m=publish,{AuthInfo}`. For example, `srt://push.example.com:9000?streamid=#!::h=push.example.com,r=live/test,m=publish,expire=1782309627,sign=a6937f4926****7b05f3987b088d473c`.

* RTMP over SRT push stream address: `rtmp://{DomainNameForStreamPushing}:1999/{AppName}/{StreamName}?{AuthInfo}`. For example, `rtmp://push.example.com:1999/live/test?expire=1782309627&sign=a6937f4926****7b05f3987b088d473c`.

* RTM push stream address: `http(s)://{DomainNameForStreamPushing}:9922/{AppName}/{StreamName}.sdp?{AuthInfo}`. For example, `https://push.example.com:9922/live/test.sdp?expire=1782309627&sign=a6937f4926****7b05f3987b088d473c`.

> **Warning**

* > To use an HTTPS push stream address or push RTM streams in a browser environment, you must first enable HTTPS for the domain name for stream pushing. For more information, see [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).

* > To include authentication information, you must first enable URL authentication for the domain name for stream pushing. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

**Pull stream address**

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/609da30481ca476f8076d58aebd5c545~tplv-goo7wpa0wc-topic.webp)

* RTMP pull stream address: `rtmp://{DomainNameForStreamPulling}/{AppName}/{StreamName}?{AuthInfo}`. For example, `rtmp://pull.example.com/live/test?auth_key=1779891783-0-0-a808d5b3****d47e28fdafb87a65ce9a`.

   > **Note**

   > To generate an RTMPS pull stream address, replace `rtmp://` in the generated RTMP address with `rtmps://`.

* FLV pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}.flv?{AuthInfo}`. For example, `https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901`.

* HLS pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}.m3u8?{AuthInfo}`. For example, `https://pull.example.com/live/test.m3u8?auth_key=1779891783-0-0-cd9bdb2b6****5e9f6f27c180a13a652`.

* RTM pull stream address for client SDKs (BytePlus MediaLive Player SDKs for iOS, Android, React Native, and Flutter) and other players: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}.sdp?{AuthInfo}`. For example, `https://pull.example.com/live/test.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70`.

* RTM pull stream address for the BytePlus MediaLive Player SDK for Web: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}_autortm.sdp?{AuthInfo}`. For example, `https://pull.example.com/live/test_autortm.sdp?auth_key=1779891783-0-0-cd9bdb2b6****5e9f6f27c180a13a652`. After URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}_autortm`. For example, if the address is `https://pull.example.com/live/test_autortm.sdp`, the `StreamName` used for authentication calculation is `test_autortm`. This address triggers automatic transcoding as follows:

   * The system automatically detects whether the stream contains B\-frames.

      * If B\-frames are present: The stream is transcoded to remove the B\-frames, and standard transcoding fees apply.

      * If B\-frames are not present: The video in the source stream is copied, and no video transcoding fees apply.

   * The system automatically detects whether the audio codec is AAC or Opus.

      * If the audio codec is AAC: The audio is converted to Opus. If no video transcoding is involved, audio\-only transcoding fees apply. For more information, see [Audio-only transcoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding#audio-only-transcoding).

      * If the audio codec is Opus: The audio in the source stream is copied, and no audio\-only transcoding fees apply.

* DASH pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/index.mpd?{AuthInfo}`. For example, `https://pull.example.com/live/test/index.mpd?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70`.

> **Warning**

* > To use an HTTPS pull stream address or play RTM streams in a browser, you must first enable HTTPS for the domain name for stream pulling. For more information, see [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).

* > To include authentication information, you must first enable URL authentication for the domain name for stream pulling. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

* > If you cannot use the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

**Transcoding stream address**

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c50fe77f76f4316b462e86b0134f20d~tplv-goo7wpa0wc-topic.webp)

* RTMP pull stream address: `rtmp://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}?{AuthInfo}`. For example, `rtmp://pull.example.com/live/test_hd?auth_key=1779891783-0-0-a808d5b3****d47e28fdafb87a65ce9a`.

   > **Note**

   > To generate an RTMPS pull stream address, replace `rtmp://` in the generated RTMP address with `rtmps://`.

* FLV pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}.flv?{AuthInfo}`. For example, `https://pull.example.com/live/test_hd.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901`.

* HLS pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}.m3u8?{AuthInfo}`. For example, `https://pull.example.com/live/test_hd.m3u8?auth_key=1779891783-0-0-cd9bdb2b6****5e9f6f27c180a13a652`.

* RTM pull stream address for client SDKs (BytePlus MediaLive Player SDKs for iOS, Android, React Native, and Flutter) and other players: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}.sdp?{AuthInfo}`. For example, `https://pull.example.com/live/test_hd.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70`.

* RTM pull stream address for the BytePlus MediaLive Player SDK for Web: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}_autortm.sdp?{AuthInfo}`. For example, `https://pull.example.com/live/test_hd_autortm.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70`. After URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}{Suffix}_autortm`. For example, if the address is `https://pull.example.com/live/test_hd_autortm.sdp`, the `StreamName` used for authentication calculation is `test_hd_autortm`. This RTM pull stream address preserves the original transcoding configuration and adds the following processing:

   * The system automatically detects whether the stream contains B\-frames.

      * If B\-frames are present: The stream is transcoded to remove the B\-frames, while the other settings follow the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

      * If B\-frames are not present: The stream is transcoded according to the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

   * The system automatically detects whether the audio codec is AAC or Opus.

      * If the audio codec is AAC: The audio is converted to Opus, while the other settings follow the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

      * If the audio codec is Opus: The audio is copied without audio transcoding, while the other settings follow the original transcoding configuration, and transcoding fees are charged according to the original transcoding configuration.

* DASH pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}/index.mpd?{AuthInfo}`. For example, `https://pull.example.com/live/test_hd/index.mpd?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70`.

> **Warning**

* > `{Suffix}` is the transcoding suffix in your transcoding configuration, such as `_uhd` and `_hd`.

* > To include authentication information, you must first enable URL authentication for the domain name for stream pulling. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication). After URL authentication is enabled, except for the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, the `StreamName` used for authentication calculation is `{StreamName}{Suffix}`. For example, if the address is `https://pull.example.com/live/test_hd.m3u8`, the `StreamName` used for authentication calculation is `test_hd`. For the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, the `StreamName` used for authentication calculation is `{StreamName}{Suffix}_autortm`.

* > To use an HTTPS pull stream address or play RTM streams in a browser environment, you must first enable HTTPS for the domain name for stream pulling. For more information, see [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).

* > If you cannot use the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

**ABR stream address**

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4864c19731864cd8b1737f86ded82023~tplv-goo7wpa0wc-topic.webp)

* HLS\-ABR pull stream address:

   * Absolute path: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/abr.m3u8?{AuthInfo}`. For example, `https://pull.example.com/live/test/abr.m3u8?auth_key=1779891783-0-0-cd9bdb2b6****5e9f6f27c180a13a652`. This is the default path format. If URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}`. For example, if the address is `https://pull.example.com/live/test/abr.m3u8`, the `StreamName` used for authentication calculation is `test`.

   * Relative path: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}_abr.m3u8?{AuthInfo}`. For example, `https://pull.example.com/live/test_abr.m3u8?auth_key=1779891783-0-0-cd9bdb2b6****5e9f6f27c180a13a652`. This path format is available only after you contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable the substream URL mode feature and set **Substream URL mode** to **Relative path** in the ABR configuration. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task). If URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}_abr`. For example, if the address is `https://pull.example.com/live/test_abr.m3u8`, the `StreamName` used for authentication calculation is `test_abr`.

* DASH\-ABR pull stream address: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}_abr/index.mpd?{AuthInfo}`. For example, `https://pull.example.com/live/test_abr/index.mpd?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70`. If URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}_abr`. For example, if the address is `https://pull.example.com/live/test_abr/index.mpd`, the `StreamName` used for authentication calculation is `test_abr`.

* RTM\-ABR pull stream address for the BytePlus MediaLive Player SDKs for iOS and Android, and other players: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}.sdp?rtmabr=true&{AuthInfo}`. For example, `https://pull.example.com/live/test_uhd.sdp?rtmabr=true&auth_key=1782838680-0-0-1da010c****8e2207e0dbb974cc3e17a`. `{Suffix}` is the substream suffix in your ABR configuration, such as `_uhd` and `_hd`. The suffix determines the startup quality level for RTM\-ABR playback. If URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}{Suffix}`. For example, if the address is `https://pull.example.com/live/test_uhd.sdp?rtmabr=true`, the `StreamName` used for authentication calculation is `test_uhd`.

* RTM\-ABR pull stream address for the BytePlus MediaLive Player SDK for Web: `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}{Suffix}_autortm.sdp?rtmabr=true&{AuthInfo}`. For example, `https://pull.example.com/live/test_uhd_autortm.sdp?rtmabr=true&auth_key=1782838680-0-0-1da010c****8e2207e0dbb974cc3e17a`. `{Suffix}` is the substream suffix in your ABR configuration, such as `_uhd` and `_hd`. The suffix determines the startup quality level for RTM\-ABR playback. If URL authentication is enabled for the domain name for stream pulling, the `StreamName` used for authentication calculation is `{StreamName}{Suffix}_autortm`. For example, if the address is `https://pull.example.com/live/test_uhd_autortm.sdp?rtmabr=true`, the `StreamName` used for authentication calculation is `test_uhd_autortm`. This RTM\-ABR pull stream address preserves the original ABR configuration and adds the following processing:

   * The system automatically detects whether the substream contains B\-frames.

      * If B\-frames are present: The substream is transcoded to remove the B\-frames, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

      * If B\-frames are not present: The substream is transcoded according to the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

   * The system automatically detects whether the audio codec is AAC or Opus.

      * If the audio codec is AAC: The audio is converted to Opus, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

      * If the audio codec is Opus: The audio is copied without audio transcoding, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

> **Warning**

* > To use an HTTPS pull stream address or play RTM streams in a browser, you must first enable HTTPS for the domain name for stream pulling. For more information, see [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).

* > To include authentication information, you must first enable URL authentication for the domain name for stream pulling. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

* > If you cannot use the RTM\-ABR pull stream address for the BytePlus MediaLive Player SDK for Web, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

## Prerequisites

* You have added domain names for stream pushing and pulling and completed the CNAME configuration. For more information, see [Adding domain names](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain) and [Adding a CNAME record](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record).

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

## Method 1: Manual **construction**

According to [Address composition rules](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses#f7580405), you can:

* Manually construct a single address;

* Use code for batch generation. For an example, see the [Address generation code example](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses#c8dfbaa6).

## Method 2: Using the address generator

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Toolkits** \> **Address generator**.

3. Select the **Address type** and **Domain name**, and enter a custom `AppName`, `StreamName`, and expiration time.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/305f90015f364f2e8ce96f4f455612de~tplv-goo7wpa0wc-topic.webp)

   |Parameter |Description |
   |---|---|
   |Address type |Select the type of address to generate.<br><br><br>* **Push stream address**: Use this address to push a stream from the host to MediaLive.<br><br>* **Pull stream address**: Use this address to pull a stream from MediaLive to viewers. |
   |Select domain name |Select a domain name for stream pushing or pulling based on the address type. |
   |AppName |The `AppName` for the generated address, which can include letters (A\-Z, a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. The default value is `live`. |
   |StreamName |The `StreamName` for the generated address, which can include letters (A\-Z, a\-z), numbers (0\-9), underscores (_) and hyphens (\-), with a length ranging from 1 to 100 characters. |
   |Expiring on |Select when the address expires.<br><br>After expiration, the address can no longer be used to initiate new requests to push or pull streams. Existing requests initiated before expiration are not affected.<br><br>> **警告**<br><br><br>> You can configure the expiration time only when URL authentication is enabled for the selected domain. To enable URL authentication, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).<br> |

4. Click **Generates Push stream address** or **Generates Pull stream address** to get push or pull stream addresses in the **Result** section.

   * **Push stream address**: Supports generating push stream addresses with authentication information. The address generator supports the following push protocols: RTMP, TS over SRT, RTMP over SRT, and RTM.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c168f4ac83b440cd85c8caffef3d8286~tplv-goo7wpa0wc-topic.webp)

      > **Note**

      * > If you use OBS (Open Broadcaster Software) to push streams over RTMP, you can get the **OBS push stream address** and **OBS Streaming Key** from the generated results, and enter them in the **Server** and **Stream Key** fields in OBS respectively.

      * > To include authentication information, you must first enable URL authentication for the domain name for stream pushing. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

* **Pull stream address**: Supports generating pull stream addresses with authentication information for source streams, transcoded streams, and ABR streams. The address generator supports RTMP, FLV, HLS (M3U8), RTM, and DASH.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cad7cfdd654d4e7f9c8d9bb3feb16929~tplv-goo7wpa0wc-topic.webp)

   * On the **Pull Stream URL** tab, you can find two kinds of RTM pull stream addresses.

      * **RTM Web SDK playback address**: Use this address for playback with the BytePlus MediaLive Player SDK for Web. This address triggers automatic transcoding as follows:

         * The system automatically detects whether the stream contains B\-frames.

            * If B\-frames are present: The stream is transcoded to remove the B\-frames, and standard transcoding fees apply.

            * If B\-frames are not present: The video in the source stream is copied, and no video transcoding fees apply.

         * The system automatically detects whether the audio codec is AAC or Opus.

            * If the audio codec is AAC: The audio is converted to Opus. If no video transcoding is involved, audio\-only transcoding fees apply. For more information, see [Audio-only transcoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding#audio-only-transcoding).

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

      * Depending on the ABR configuration, the HLS\-ABR address may use either the default `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/abr.m3u8?{AuthInfo}` format or the relative\-path `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}_abr.m3u8?{AuthInfo}` format. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

      * If RTM\-ABR is enabled in the ABR configuration, select the startup quality level (suffix) to get the corresponding RTM\-ABR address. You can also find two kinds of RTM\-ABR pull stream addresses.

         * **RTM Web SDK playback address**: Use this address for playback with the BytePlus MediaLive Player SDK for Web. This RTM\-ABR pull stream address preserves the original ABR configuration and adds the following processing:

            * The system automatically detects whether the substream contains B\-frames.

               * If B\-frames are present: The substream is transcoded to remove the B\-frames, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

               * If B\-frames are not present: The substream is transcoded according to the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

            * The system automatically detects whether the audio codec is AAC or Opus.

               * If the audio codec is AAC: The audio is converted to Opus, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

               * If the audio codec is Opus: The audio is copied without audio transcoding, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

         * **RTM address**: Use this address for playback with the BytePlus MediaLive Player SDKs for iOS and Android, and other players.

   > **Note**

   * > To include authentication information, you must first enable URL authentication for the domain name for stream pulling. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

   * > If you cannot get the **RTM Web SDK playback address**, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

5. You can also:

   * Click the online streaming icon to start streaming on the **Web push** page of the console.

   * Click the online playback icon to start playback on the **Web pull** page of the console.

   * Click the copy icon to copy the address.

   * Click the QR code icon to view the QR code.

   * Click **History** in the upper\-right corner of the page to view previously generated address records.

## Method 3: **Using API**

1. (Optional) Call the [UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) API to enable and configure the authentication key for the domain name.

2. Call [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) API to generate the push address.

3. Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) API to generate the pull address.

## Address generation code example

This section provides sample code in Go, Python, Java, and PHP for generating authenticated RTMP stream addresses. You can generate addresses for other protocols according to the address composition rules.

**Go**

```Go
package main

import (
   "crypto/md5"
   "fmt"
)

func main() {
   fmt.Println(GenAuthUrl("testDomain", "testApp", "testStream", "testKey", 1636963457))
}

func GenAuthUrl(domain, app, stream, secretKey string, unixtime int64) string {
   src := fmt.Sprintf("/%s/%s%s%d", app, stream, secretKey, unixtime)
   sign := fmt.Sprintf("%x", md5.Sum([]byte(src)))
   return fmt.Sprintf("rtmp://%s/%s/%s?expire=%d&sign=%s", domain, app, stream, unixtime, sign)
}
```

**Python**

```Python
import hashlib

def GenAuthUrl(domain, app, stream, secretKey, unixtime):
    src = "/%s/%s%s%d" % (app, stream, secretKey, unixtime)
    sign = hashlib.md5(src.encode("utf8")).hexdigest()
    return "rtmp://%s/%s/%s?expire=%d&sign=%s" % (domain, app, stream, unixtime, sign)

if __name__ == '__main__':
    print(GenAuthUrl("testDomain", "testApp", "testStream", "testKey", 1636963457))
```

**Java**

```Java
package demo;

import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class Demo1 {
    public static void main(String[] args) throws NoSuchAlgorithmException {
        System.out.println((GenAuthUrl("testDomain", "testApp", "testStream", "testKey", 1636963457)));
    }

    public static String GenAuthUrl(String domain, String app, String stream, String secretKey, int unixtime) throws NoSuchAlgorithmException {

        String src = String.format("/%s/%s%s%d", app, stream, secretKey, unixtime);
        MessageDigest md5 = MessageDigest.getInstance("MD5");
        byte[] md5Bytes = md5.digest(src.getBytes(StandardCharsets.UTF_8));
        String sign = "";
        for (int i = 0; i < md5Bytes.length; i++) {
            sign += Integer.toHexString(md5Bytes[i] | 0xFFFFFF00).substring(6);
        }

        return String.format("rtmp://%s/%s/%s?expire=%d&sign=%s", domain, app, stream, unixtime, sign);
    }
}
```

**PHP**

```PHP
function GenAuthUrl($domain, $app, $stream, $secretKey, $unixtime){

    $src = sprintf("/%s/%s%s%d", $app, $stream, $secretKey, $unixtime);
    $sign = sprintf("%s",md5($src));
    return sprintf("rtmp://%s/%s/%s?expire=%d&sign=%s",$domain, $app, $stream, $unixtime, $sign);
}

echo GenAuthUrl("testDomain", "testApp", "testStream", "testKey", 1636963457);
```
