---
title: "Managing adaptive bitrate configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task"
---

Adaptive bitrate (ABR) is a viewer\-focused video delivery technology designed to deliver seamless, high\-quality playback experiences regardless of fluctuating network conditions. You preconfigure multiple substreams with different encoding formats, resolutions, and bitrates, and the player automatically selects the optimal stream based on a viewer's real\-time network conditions to balance smooth playback and video quality. This topic will walk you through how to manage the ABR configuration in the MediaLive console.

## Why use ABR?

ABR helps resolve key streaming challenges and significantly boosts viewer satisfaction by delivering smart, personalized live streaming experiences.

* **Automatically switch between quality levels to balance smooth playback and video quality**

   By creating several quality levels (such as UHD, HD, and SD), you enable the player to monitor each viewer's real\-time network conditions and seamlessly switch between these levels:

   * **When a viewer's network is poor**: The player automatically switches to a lower\-bitrate stream. This sacrifices some video quality but ensures smooth, buffer\-free playback.

   * **When a viewer's network recovers**: The player automatically switches back to a higher\-bitrate stream to deliver the best possible video quality.

      This dynamic adjustment provides an optimal and uninterrupted viewing experience, making your streams resilient to fluctuating network speeds.

* **Reduce bandwidth costs and improve compatibility**

   * **Lower bandwidth costs:**  You can convert your source stream from the standard H.264 codec to the more efficient H.265 codec before delivery. H.265 offers higher compression, significantly reducing your bandwidth consumption and costs.

   * **Boost player compatibility:**  If you are streaming in H.265, which some older browsers and devices do not support, you can provide an H.264 version simultaneously. This guarantees that all viewers can watch your stream without compatibility issues.

## How does ABR work?

ABR works differently depending on the protocol, but the playback goal is the same: balance smooth playback and video quality based on the viewer's network conditions.

* **HLS\-ABR and DASH\-ABR**: A player requests the ABR address to get the playback information for all available quality levels. The player then monitors the viewer's network conditions and automatically switches between quality levels during playback.

* **RTM\-ABR**: You use one RTM\-ABR pull stream address, and the suffix in the address determines the startup quality level. During playback, MediaLive automatically switches between quality levels based on the viewer's network conditions.

When the network is poor, MediaLive uses a lower\-bitrate stream to reduce buffering. When the network improves, MediaLive restores a higher\-bitrate stream to maintain video quality, ensuring an optimal and uninterrupted viewing experience.

## Prerequisites

* You have added the domain names for stream pushing and pulling under the same domain name space. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

* If you need to configure the display order of substreams in the master playlist or the URL mode of substreams, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable these features.

## Notes

* **Fees**: Substreams are created by transcoding the source stream to different resolutions and bitrates, and this process incurs transcoding fees. For more information, see [Transcoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding).

* **Activation time**: After adding, updating, or deleting an ABR configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.

* **Protocols**: ABR applies to HLS, DASH, and RTM protocols.

## Adding an ABR configuration

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and click the **Adaptive bitrate** tab on the right.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. On the **Basic information** tab, configure the following settings. These settings apply to all substreams.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb888f8cef8e4a80b6a9b3f1010a8146~tplv-goo7wpa0wc-topic.webp)

   |Parameter |Description |
   |---|---|
   |AppName |Specify the `AppName` this configuration will apply to. This name must exactly match the `AppName` in your push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then the `AppName` is `live`.<br><br>The `AppName` can contain letters (a\-z, A\-Z), numbers (0\-9), underscores (`_`), and hyphens (`-`), and must be 1\-30 characters long.<br><br>> **说明**<br><br><br>> Each `AppName` can only have one ABR configuration.<br> |
   |Type |Select the transcoding mode. This choice lets you balance transcoding costs against video quality and bandwidth usage.<br><br><br>* **Standard mode:**  A more economical option with standard compression. This option provides good quality and is ideal for scenarios where minimizing transcoding costs is your main priority.<br><br>* **Low\-bitrate HD:**  Uses more efficient compression than **Standard mode** to save bandwidth or enhance video quality.<br><br>   * **Save bandwidth:**  Maintain the same video quality at a lower bitrate, significantly reducing bandwidth consumption and delivery costs.<br><br>   * **Enhance video quality:**  Deliver a sharper, more detailed image at the same bitrate for a better viewing experience.<br><br>      This mode is suitable for live streaming scenarios where you want to achieve the same video quality at a lower bitrate, or better video quality at the same bitrate. Note that this mode incurs higher transcoding fees than **Standard mode**. |
   |Video codec |Choose the video codec for the substream. **H.265** offers better compression (saving bandwidth), while **H.264** provides wider compatibility across devices. |
   |Trigger transcoding |Choose when to start transcoding based on your priorities for cost and viewing experience.<br><br><br>* **Stream pushing (Default)** : Transcoding starts the moment you start pushing your source stream. This ensures zero startup delay for every viewer, as substreams are ready instantly. However, this option incurs higher costs because transcoding runs continuously as long as the source stream is live. Recommended for high\-priority events where instant availability is critical.<br><br>* **Stream pulling**: Transcoding starts only when the first viewer begins playing a substream. This is the most cost\-effective option, but the first viewer might experience a brief startup delay. Recommended for most use cases where cost optimization is a priority. |
   |Protocol Type |Choose one or more ABR protocol types. The protocol type determines how a viewer's player will receive and switch between the different quality levels.<br><br><br>* **HLS\-ABR** (`.m3u8`): Choose this to reach the **widest possible audience**. This protocol is required for native playback on Apple devices like iPhones and iPads, as well as in the Safari browser. Furthermore, HLS\-ABR offers excellent compatibility across Android, desktop browsers, and smart TVs, making this option a highly reliable choice. If you need to support the Apple ecosystem, HLS\-ABR is the recommended choice.<br><br>   > **Note**<br>   <br><br>   > For HLS\-ABR, the address is used to pull the main M3U8 playlist. The format is `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/abr.m3u8?{AuthInfo}`. After the player gets the main M3U8 playlist, it continues to request the substream URLs in the playlist to pull substreams at different quality levels.<br>   <br><br>   > If [URL authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication) is enabled for the domain name for stream pulling, MediaLive generates authentication parameters for each HLS substream URL based on the URL authentication configuration of the domain name for stream pulling and reuses the timestamp from the HLS\-ABR request. This ensures that when the player switches quality levels and requests the corresponding substream URL, the request can pass authentication and playback is not interrupted. For example, if the HLS\-ABR request URL is `https://pull.example.com/live/test/abr.m3u8?auth_key=1758296819-0-0-9fb836225****c9138541b36d7e1c4a3`, the substream URLs in the main M3U8 playlist can be `/live/test_hd/index.m3u8?auth_key=1758296819-0-0-4d96cffa****392aed81afc1e19e9e03` and `/live/test_sd/index.m3u8?auth_key=1758296819-0-0-537e80a2****164e449f1b5ae6978819`. The timestamp `1758296819` is the same, but each substream URL has a different authentication value.<br>   <br><br>* **DASH\-ABR** (`.mpd`): Choose this when most of your viewers are on **Android devices and non\-Safari desktop browsers** (like Chrome and Firefox), or if your workflow involves specific **Digital Rights Management (DRM)**  solutions. Please note that DASH is not natively supported on iOS Safari and requires a specific player library to function on that browser.<br><br>* **RTM\-ABR** (`.sdp`): Choose this for latency\-sensitive scenarios such as sports broadcasting. RTM\-ABR delivers **a low latency of about 2\-3 seconds** while maintaining a smooth viewing experience by automatically adjusting quality levels to match **unstable network conditions**. This prevents buffering and stuttering in weak network environments by switching to a lower quality level without increasing delay. If your goal is to achieve the lowest possible latency while ensuring playback stability, RTM\-ABR is the recommended choice. |
   |Copy user request parameters to substream URL |After you turn on the switch, MediaLive copies all original custom URL parameters carried in the ABR request URL to each substream URL in the main playlist or manifest.<br><br>For example, if the HLS\-ABR request URL is `https://pull.example.com/live/test/abr.m3u8?uid=10001&scene=live_home`, with this switch turned on, the substream URLs in the main M3U8 playlist carry the same parameters, such as `/live/test_hd/index.m3u8?uid=10001&scene=live_home` and `/live/test_sd/index.m3u8?uid=10001&scene=live_home`.<br><br>> **注意**<br><br><br><br>* > This feature applies only to HLS\-ABR and DASH\-ABR.<br><br><br>* > You cannot enable this setting if you are using the time shifting feature.<br> |
   |Substream order |Select whether higher\-bitrate or lower\-bitrate substreams appear first in the HLS master playlist. This setting changes only the order of substreams in the master playlist.<br><br><br>* **Descending by bitrate (Default)** : List higher\-bitrate substreams first.<br><br>* **Ascending by bitrate**: List lower\-bitrate substreams first.<br><br><br>> **注意**<br><br><br>> This feature applies only to HLS\-ABR. If you cannot find this field, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable the feature.<br> |
   |Substream URL mode |Select whether substream URLs in the HLS master playlist use absolute paths or relative paths. This setting changes how substream URLs are written in the master playlist.<br><br><br>* **Absolute path (Default)** : MediaLive keeps the default HLS\-ABR address format, which is `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/abr.m3u8`. Substream URLs in the master playlist use absolute paths.<br><br>* **Relative path**: MediaLive changes the HLS\-ABR address from `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}/abr.m3u8` to `http(s)://{DomainNameForStreamPulling}/{AppName}/{StreamName}_abr.m3u8`. Substream URLs in the master playlist use relative paths.<br><br><br>> **注意**<br><br><br>> This feature applies only to HLS\-ABR. If you cannot find this field, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable the feature.<br> |

5. Click **Add substream** to configure a substream. You can add a maximum of 15 substreams.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6424428b4474cce9a98fbf7c09c121a~tplv-goo7wpa0wc-topic.webp)

   |Parameter |Description |
   |---|---|
   |Quality level |Select a quality level. You can save time by using default configurations for each level, which define the resolution, bitrate, and frame rate. Audio settings are set to AAC by default. You can use these default settings as\-is or customize them after selection.<br><br><br>* **4K (2160p):**  15,000 kbps, 60 fps<br><br>* **2K (1440p):**  10,000 kbps, 30 fps<br><br>* **UHD (1080p):**  3200 kbps, 30 fps<br><br>* **HD (720p):**  2048 kbps, 30 fps<br><br>* **SD (540p):**  1638 kbps, 30 fps<br><br>* **LD (360p):**  1024 kbps, 30 fps<br><br><br>> **说明**<br><br><br>> To enable the 4K or 2K options, contact the BytePlus support team by [creating a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).<br> |
   |Substream suffix |A unique suffix, such as `uhd`, for this substream. The suffix can contain letters (A\-Z, a\-z), numbers (0\-9), and hyphens (\-), and must be 1\-10 characters long.<br><br>> **说明**<br><br><br><br>* > For the same `AppName`, ensure this suffix does not conflict with any suffix used in a separate transcoding configuration.<br><br><br>* > If you select **DASH\-ABR** as the **Protocol Type**, the system automatically uses the `abr` suffix for the MPD manifest URL (such as `https://pull.example.com/live/test_abr/index.mpd`). To prevent a naming conflict, you **cannot** use `abr` as a suffix for a separate transcoding configuration under the same `AppName`.<br> |
   |Resolution |The resolution of the substream, in pixels. The value range is 150\-4096.<br><br>> **说明**<br><br><br>> Setting a resolution higher than the source stream does not improve video quality and can result in unnecessary processing costs.<br> |
   |Bitrate |Set the bitrate of the substream in kbps. A higher bitrate results in a sharper image but requires more bandwidth. The value range is 0\-30,000 kbps. Set the value to 0 to keep the bitrate identical to the source stream. This is useful when the source bitrate already meets your quality requirements.<br><br>> **说明**<br><br><br>> Setting a bitrate higher than the source stream does not add visual detail and only increases bandwidth costs.<br> |
   |Frame rate |Set the frame rate of the substream in fps. A higher frame rate creates smoother motion but requires more processing and bandwidth. The value range is 0\-60 fps. Set the value to 0 to keep the frame rate identical to the source stream. This is useful when the source frame rate already meets your quality requirements.<br><br>> **说明**<br><br><br>> Setting a frame rate higher than the source stream only results in duplicate frames. Such duplicate frames do not make motion appear smoother and may instead make the video look unnatural.<br> |
   |Audio settings |Choose how to handle the audio for your substream. Your choice depends on whether you prioritize maximum compatibility, bandwidth usage, or cost savings.<br><br><br>* **AAC**: Select this for maximum compatibility. AAC is the industry standard and will play on virtually any device or browser, including older ones. This is the most reliable choice to reach the widest audience.<br><br>* **Opus**: Select this to use advanced compression, which provides excellent audio quality while saving on bandwidth costs. While ideal for modern platforms, note that Opus may not be supported on some legacy devices.<br><br>* **Copy source stream**: Select this to use the original audio directly without making any changes. This skips the audio transcoding process, which saves on transcoding fees and is the most cost\-effective option. Because there is no re\-encoding, your original audio quality is perfectly preserved. This option is recommended when your source audio format and quality already meet your requirements and you want to maximize cost savings. |
   |Transcoding stop waiting time |Set a waiting period (in seconds) for the transcoding task to remain active after the last viewer **stops pulling the stream**. This setting helps you balance the viewing experience and transcoding costs.<br><br>Parameter values:<br><br><br>* **0\-300:**  Defines a specific waiting period. The task stops if no new viewer joins before this period expires.<br><br>*  **\-1:**  Sets the waiting period to **infinite**. The task will never stop automatically as long as the source stream is live.<br><br><br>Configure the waiting time based on your streaming scenario:<br><br><br>* **For the best experience:**  If you expect high viewer turnover (for example, during live sports or popular events), set a **longer waiting time (such as 60\-180 seconds)** . This ensures most new viewers experience instant playback but will increase costs during idle periods.<br><br>* **To control costs:**  If your viewers are relatively stable or cost\-saving is a priority, set a **shorter waiting time (such as 10\-30 seconds)** . This stops transcoding tasks sooner when no one is watching, reducing your expenses.<br><br>* **For critical 24/7 streams:**  Use a value of  **\-1** only for essential streams where instant startup is mandatory at all times, and you accept continuous transcoding costs.<br><br><br>> **说明**<br><br><br>> This setting is only active when **Trigger transcoding** is set to **Stream pulling**.<br> |
   |Resolution not exceeding the original |* **Enabled (Default):**  Prevents upscaling the video resolution to a higher resolution than the source stream. If the source stream's resolution is lower than your configured setting, for example, your ABR configuration is set to `1080p`, but the source stream is `720p`, the output resolution will also be `720p`. This avoids potential quality degradation and unnecessary costs.<br><br>* **Disabled:**  Forces the output to match the configured resolution, even if this means upscaling a lower\-resolution source. Only disable this if your player or downstream services strictly require a fixed resolution. |
   |Bitrate not exceeding the original |* **Enabled (Default):**  Prevents the output bitrate from exceeding the source stream. If the source stream's bitrate is lower than your configured setting, for example, your ABR configuration is set to 3200 kbps, but the source stream is 2048 kbps, the output bitrate will also be 2048 kbps. This optimizes bandwidth usage and reduces costs because increasing the bitrate beyond the source stream brings no benefit.<br><br>* **Disabled:**  Forces the output to match the configured bitrate. Only disable this if your player or downstream services have a strict requirement for a constant bitrate. |
   |Frame rate not exceeding the original |* **Enabled (Default):**  Prevents the output frame rate from exceeding the source stream. If the source stream's frame rate is lower than your configured setting, for example, your ABR configuration is set to 30 fps, but the source stream is 25 fps, the output frame rate will also be 25 fps. This ensures smooth playback by avoiding frame duplication and reduces unnecessary processing costs.<br><br>* **Disabled**: Forces the output to match the configured frame rate. Only disable this if your player or downstream services have a strict requirement for a constant frame rate. |

6. Click **Confirm** to save your configuration. You can always click **Edit** or **Delete** in the **Action** column to edit or delete the configuration.

   After adding, updating, or deleting an ABR configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.

## What to do next

1. Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate the ABR pull stream address.

   1. Complete the following configurations, and click **Generates Pull stream address**.

      * **Address type**: Select **Pull stream address**.

      * **Domain name**: Select the domain name for stream pulling within the domain name space used when adding the ABR configuration.

      * **AppName** and **StreamName**: Enter the `AppName` and `StreamName` from your push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then the `AppName` is `live`, and the `StreamName` is `test`.

   2. Get the ABR pull stream address on the **Adaptive bitrate** tab. You can copy the address or generate a QR code by clicking the icon on the right. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d1af8b216d44940a91b4a576a318520~tplv-goo7wpa0wc-topic.webp)

   * **HLS\-ABR address**: The `.m3u8` address.

   * **DASH\-ABR address**: The `.mpd` address.

   * **RTM\-ABR address**: Select the startup quality level (suffix) to get the corresponding RTM\-ABR address.

      * **RTM address**: Use this address for playback with the BytePlus MediaLive Player SDKs for iOS and Android, and other players.

      * **RTM Web SDK playback address**: Use this address for playback with the BytePlus MediaLive Player SDK for Web. This RTM\-ABR pull stream address preserves the original ABR configuration and adds the following processing:

         * The system automatically detects whether the substream contains B\-frames.

            * If B\-frames are present: The substream is transcoded to remove the B\-frames, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

            * If B\-frames are not present: The substream is transcoded according to the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

         * The system automatically detects whether the audio codec is AAC or Opus.

            * If the audio codec is AAC: The audio is converted to Opus, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

            * If the audio codec is Opus: The audio is copied without audio transcoding, while the other settings follow the original ABR configuration, and transcoding fees are charged according to the original ABR configuration.

      > **注意**

      > If you cannot get the **RTM Web SDK playback address**, contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).

2. Use your push stream address to push the source stream. Make sure the domain names for stream pushing and pulling belong to the same domain name space, and use the same `AppName` and `StreamName` for the push and pull stream addresses. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

3. Use one of the following methods for playback.

   |Method |Scenario |Description |
   |---|---|---|
   |Third\-party stream pulling tool |No SDK development resources. |Configure the ABR address in the third\-party stream pulling tool to play the live stream. For more information, refer to the corresponding official documentation or consult official customer support. |
   |Player SDK for Web |Play the stream in a web browser. |Integrate the Player SDK for Web and play the stream on your website or web app. For more information, see [Adaptive bitrate streaming](https://docs.byteplus.com/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr). |
   |Client SDK |Play the stream in a native mobile app. |Integrate the client SDK and play the stream in a mobile app. For more information, see:<br><br><br>* iOS: [RTM-ABR streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#affd8a26)<br><br>* Android: [RTM-ABR streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#ff47ac00) |
   |BytePlus MediaLive console |For quick preview and debugging during development or testing. |On the [Web pull page](https://console.byteplus.com/live/main/webPullStream/play) in the console, enter the HLS\-ABR or RTM\-ABR address to quickly verify playback. For more information, see [Pulling a stream through the console](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull). |

## FAQ

### Why isn't my new ABR configuration working?

After adding, updating, or deleting an ABR configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.

### The first viewer to watch my stream experiences a delay. How can I fix this?

This delay occurs because the **Trigger transcoding** setting is set to **Stream pulling**, which starts transcoding only when the first viewer starts watching. To eliminate this startup delay, change the trigger to **Stream pushing**. This will start the transcoding process the moment your source stream goes live, ensuring instant playback for all viewers. Be aware that this option incurs costs as long as the source stream is live, even if no one is watching.

### What are the best ways to control transcoding costs?

To optimize your expenses, consider these strategies:

* **Use the stream pulling trigger:**  Keep **Trigger transcoding** set to **Stream pulling**, so you only pay for transcoding when someone is actively watching.

* **Copy the source audio:**  Set the **Audio settings** to **Copy source stream**. This avoids audio transcoding fees entirely and preserves the original audio quality.

* **Choose the standard transcoding mode:**  Select **Standard mode** as the **Type**. This is the more economical option and is ideal for scenarios where minimizing transcoding costs is your main priority.

* **Avoid unnecessary upscaling:**  Keep the **not exceeding the original** options enabled. This prevents wasting resources, as transcoding to a resolution, bitrate, or frame rate higher than the source does not improve video quality.

### Adaptive bitrate vs. transcoding: Which one should I use?

Choose the configuration that best fits your streaming protocol and desired viewing experience. The key difference lies in whether the player can automatically switch between quality levels.

* **ABR**: Use the ABR configuration to provide a seamless, auto\-adjusting viewing experience. This feature provides multiple quality levels, and the player automatically switches between them based on the viewer's network conditions, ensuring smooth playback at the best possible video quality.

* **Transcoding**: Use the transcoding configuration in the following scenarios:

   * **Broader protocol support**: When you need to stream using protocols that the ABR feature does not support, such as RTMP.

   * **Manual quality selection**: When you want to provide separate pull stream addresses for each quality level and implement a manual quality selector in your player, allowing viewers to choose their preferred resolution.

### Can transcoding improve the quality of a blurry source stream?

No, transcoding cannot create detail that is not in the source stream. If your source stream is blurry or low\-quality, the substreams will also appear blurry, even if you set them to a higher resolution, bitrate, or frame rate.

### Why does an HLS\-ABR or DASH\-ABR address stop playing after a while?

If your business depends on custom URL parameters in an HLS\-ABR or DASH\-ABR address, such as `uid` or `scene`, playback may stop because these parameters are not passed to substream requests. To fix this, turn on the **Copy user request parameters to substream URL** switch. After you turn on the switch, MediaLive copies all original custom URL parameters carried in the ABR request URL to each substream URL, helping prevent playback interruptions caused by missing parameters. You cannot enable this switch if you use the time shifting feature.

### Which protocol should I choose: HLS\-ABR, DASH\-ABR, or RTM\-ABR?

The best choice depends on your target audience, playback devices, and latency requirements:

* Choose **HLS\-ABR** for the widest compatibility. If you need to support the Apple ecosystem or are unsure which to pick, HLS\-ABR is the recommended choice.

* Choose **DASH\-ABR** if your viewers are primarily on Android and non\-Safari browsers (like Chrome and Firefox) or if you have specific DRM requirements.

* Choose **RTM\-ABR** for **latency\-sensitive scenarios** like sports broadcasting. If your goal is to achieve the lowest possible latency while ensuring playback stability, RTM\-ABR is the recommended choice.
