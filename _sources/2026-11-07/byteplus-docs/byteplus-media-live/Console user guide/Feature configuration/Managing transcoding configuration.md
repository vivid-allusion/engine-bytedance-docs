---
title: "Managing transcoding configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding"
---

By transcoding your source stream, you can generate multiple transcoded streams with different encoding formats, resolutions, and bitrates. Offering a choice of quality levels allows viewers to select the stream that best fits their network conditions, ensuring a better playback experience for everyone. This topic will walk you through how to manage transcoding configurations in the MediaLive console.

<span id="4b90f58b"></span>
## Why use transcoding?

Transcoding allows you to solve common streaming challenges and enhance viewer satisfaction.


* **Ensure smooth playback on any network**

   Streaming at a single high bitrate can cause buffering for viewers on slower networks, while a single low\-bitrate stream compromises video quality for those with faster connections. By providing multiple transcoded streams at different bitrates, you can cater to all viewers. Viewers on high\-speed internet can select a high\-bitrate stream for maximum clarity, while those with limited bandwidth can opt for a lower\-bitrate stream to ensure smooth, buffer\-free playback. This ensures every viewer receives the best possible experience for their specific network conditions.

* **Reduce costs and improve compatibility**

   * **Lower bandwidth costs:**  You can convert your source stream from the standard H.264 codec to the more efficient H.265 codec before delivery. H.265 offers higher compression, significantly reducing your bandwidth consumption and costs.

   * **Boost player compatibility:**  If you are streaming in H.265, which some older browsers and devices do not support, you can provide an H.264 version simultaneously. This guarantees that all viewers can watch your stream without compatibility issues.


<span id="d43281de"></span>
## Prerequisites

You have added the domain names for stream pushing and pulling under the same domain name space. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

<span id="bf9bf2c2"></span>
## Notes


* **Fees:**  Using the transcoding feature will incur transcoding fees. For more information, see [Transcoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding).

* **Activation time**: After adding, updating, or deleting a transcoding configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.


<span id="6be97ef4"></span>
## Adding a transcoding configuration


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration**. By default, you will be on the **Transcoding** tab.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. Complete the configuration to define your transcoded stream. See the following table for a detailed explanation of each setting.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03d8bbc5359c40e5afcb2e5d01f9ff17~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Description |
   |---|---|
   |AppName |Specify the `AppName` this configuration will apply to. This name must exactly match the `AppName` in your push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then the `AppName` is `live`.<br><br>Enter the `AppName`, which can contain letters (a\-z, A\-Z), numbers (0\-9), underscores (`_`), hyphens (`-`), and periods (`.`), and must be 1\-30 characters long. You can also enter a single asterisk (`*`).<br><br><br>* If you enter an asterisk (`*`), the transcoding configuration applies to all `AppName`s in the domain name space. This means the configuration becomes a global configuration for the current domain name space.<br><br>* If both a global configuration and an `AppName`\-specific configuration exist for the same `AppName`, the `AppName`\-specific configuration takes precedence. For example, if you have added transcoding configuration **A** for `AppName` `*` and transcoding configuration **B** for `AppName` `live`, streams with `AppName` `live` are transcoded using transcoding configuration **B** by default. |
   |Suffix |A unique suffix, such as `uhd`, for this transcoded stream. This suffix is appended to the stream name with an underscore (_) as the separator to generate the new pull stream address for the transcoded stream. The suffix can contain letters (A\-Z, a\-z), numbers (0\-9), and hyphens (\-), and must be 1\-10 characters long.<br><br>For example, if the pull stream address of the source stream is `https://pull.example.com/appname/streamname.flv`, the pull stream address of the transcoded stream can be `https://pull.example.com/appname/streamname_uhd.flv`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the same <code>AppName</code>, ensure this suffix does not conflict with any suffix used in an adaptive bitrate (ABR) configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Do not use <code>abr</code> as a suffix if you are also using a <strong>DASH\-ABR</strong> configuration for the same <code>AppName</code>. The system reserves the <code>abr</code> suffix for the DASH main playlist URL, and using <code>abr</code> here will cause a naming conflict.</div><br> |
   |Video codec |Choose the video codec for the transcoded stream. **H.265** offers better compression (saving bandwidth), while **H.264** provides wider compatibility across devices. |
   |Type |Select the transcoding mode. This choice lets you balance transcoding costs against video quality and bandwidth usage.<br><br><br>* **Standard mode:**  A more economical option with standard compression. This option provides good quality and is ideal for scenarios where minimizing transcoding costs is your main priority.<br><br>* **Low\-bitrate HD:**  Uses advanced compression to deliver higher video quality at the same bitrate or the same quality at a lower bitrate compared to **Standard mode**. This allows you to prioritize either bandwidth savings or viewing experience:<br><br>   * **Save bandwidth:**  Achieve the same video quality at a lower bitrate, significantly reducing data consumption and delivery costs.<br><br>   * **Enhance video quality:**  Deliver a visibly sharper, more detailed image at the same bitrate for a premium viewing experience.<br><br>   This mode is recommended for your high\-value streams, offering an optimal balance between video quality and bandwidth savings. Note that this advanced compression comes at a higher transcoding fee compared to **Standard mode**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can create separate configurations for the same <code>AppName</code> to offer both modes.</div><br> |
   |Recommended |Save time by using pre\-defined configuration templates tailored to common streaming scenarios. These templates automatically configure the resolution, bitrate, and frame rate. Other settings, such as GOP and audio option, are set to standard defaults (2 seconds for GOP, AAC for audio). You can use these templates as\-is or customize them after selection.<br><br><br>* **4K (2160p):**  15,000 kbps, 60 fps<br><br>* **2K (1440p):**  10,000 kbps, 30 fps<br><br>* **UHD (1080p):**  3200 kbps (standard mode)/2000 kbps (low\-bitrate HD), 30 fps<br><br>* **HD (720p):**  2048 kbps (standard mode)/1638 kbps (low\-bitrate HD), 25 fps<br><br>* **SD (540p):**  1638 kbps (standard mode)/1024 kbps (low\-bitrate HD), 25 fps<br><br>* **LD (360p):**  1024 kbps (standard mode)/500 kbps (low\-bitrate HD), 20 fps<br><br>* **Original:**  Keeps the video and audio configuration identical to the source stream.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To enable the 4K or 2K options, contact the BytePlus support team by <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">creating a ticket</a>.</div><br> |
   |Resolution |Define the output video's resolution in pixels. All scaling modes preserve the original aspect ratio to prevent distortion. Setting any value to `0` keeps the original resolution.<br><br>Choose a scaling mode that best fits your workflow:<br><br><br>* **Fixed width**: Sets a fixed width, and the height adjusts automatically.<br><br>   * **When to use**: Ideal for fitting videos into a specific horizontal space, such as a website column where you primarily expect landscape streams.<br><br>   * **Example**: Set to `1280` to convert a `1920x1080` source into a `1280x720` video.<br><br>* **Fixed height**: Sets a fixed height, and the width adjusts automatically.<br><br>   * **When to use**: Best for fitting videos into a specific vertical space, like a vertical feed in a mobile app.<br><br>   * **Example**: Set to `720` to convert a `1920x1080` source into a `1280x720` video.<br><br>* **Fixed long side**: Sets the length of the video's longer side, and the shorter side adjusts automatically.<br><br>   * **When to use**: The most flexible option for handling both landscape and portrait videos with a single, future\-proof rule, which intelligently adapts to any orientation.<br><br>   * **Example**: A value of `1280` correctly transforms a `1920x1080` (landscape) source into `1280x720` and a `1080x1920` (portrait) source into `720x1280`.<br><br>* **Fixed short side**: Sets the length of the video's shorter side, and the longer side adjusts automatically.<br><br>   * **When to use**: Guarantees a minimum level of detail regardless of orientation. Useful for setting a baseline quality standard for all incoming streams.<br><br>   * **Example**: A value of `480` ensures the video's smallest dimension will always be at least 480 px.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting a resolution higher than the source stream does not improve video quality and can result in unnecessary processing costs.</div><br> |
   |Bitrate |Set the bitrate of the transcoded stream in kbps. A higher bitrate results in a sharper image but requires more bandwidth. The value can range from 0 to 30,000 kbps. Set the value to `0` to keep the bitrate identical to the source stream. This is useful when the source bitrate already meets your quality requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Similar to resolution, setting a bitrate higher than the source is not recommended, as doing so only increases bandwidth costs without adding visual detail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Pushing a stream with an excessively high bitrate can overload the transcoding server, leading to transcoding errors and playback stuttering for your viewers.</div><br> |
   |Frame rate |Set the frame rate of the transcoded stream in fps. A higher frame rate creates smoother motion but requires more processing and bandwidth. The value can range from 0 to 60 fps. Set the value to `0` to keep the frame rate identical to the source stream. This is useful when the source frame rate already meets your quality requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Similar to resolution, setting a frame rate higher than the source is not recommended, as doing so results in duplicate frames without creating smoother motion.</div><br> |
   |GOP |The Group of Pictures (GOP) size, set in seconds, determines how often a full video frame (keyframe) is sent. The value can range from 1 to 20 seconds. This setting lets you balance the viewing experience against your bandwidth costs.<br><br><br>* **Lower GOP (1\-2 seconds):**  Sends keyframes more frequently. This improves the viewing experience for stream startup and seeking. However, a lower GOP increases bandwidth consumption (uses more data) and requires a higher bitrate to maintain the same video quality, which increases your costs.<br><br>* **Higher GOP (3 or more seconds):**  Sends keyframes less frequently. This reduces bandwidth consumption (uses less data), allowing you to deliver better video quality at the same bitrate or the same quality at a lower bitrate, thus saving bandwidth costs. The trade\-off is a potentially slower startup and seeking experience for your viewers.<br><br><br>A value of 2 seconds is a common industry standard that offers a good balance between playback performance and cost efficiency. |
   |Audio option |Choose how to handle the audio for your transcoded stream. Your choice depends on whether you prioritize maximum compatibility, bandwidth usage, or cost savings.<br><br><br>* **AAC**: Select this for maximum compatibility. AAC is the industry standard and will play on virtually any device or browser, including older ones. This is the safest choice to reach the widest audience.<br><br>* **Opus**: Select this to use advanced compression, which provides excellent audio quality while saving on bandwidth costs. While ideal for modern platforms, note that Opus may not be supported on some legacy devices.<br><br>* **Copy source stream**: Select this to use the original audio directly without making any changes. This skips the audio transcoding process, which saves on transcoding fees and is the most cost\-effective option. Because there is no re\-encoding, your original audio quality is perfectly preserved. This option is recommended when your source audio format and quality already meet your requirements and you want to maximize cost savings. |
   |Trigger transcoding |Choose when to start transcoding based on your priorities for cost and viewing experience.<br><br><br>* **Stream pulling (Default)** : Transcoding starts only when the first viewer begins playing a transcoded stream. This is the most cost\-effective option, but the first viewer might experience a brief startup delay. Recommended for most use cases where cost optimization is a priority.<br><br>* **Stream pushing**: Transcoding starts the moment you start pushing your source stream. This ensures zero startup delay for every viewer, as transcoded streams are ready instantly. However, this option incurs higher costs because transcoding runs continuously as long as the source stream is live. Recommended for high\-priority events where instant availability is critical.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This option is only available when <code>AppName</code> is set to a specific value, instead of <code>*</code>.   </div><br>    |
   |Transcoding stop waiting time |Set a waiting period (in seconds) for the transcoding task to remain active after the last viewer **stops pulling the stream**. This setting helps you balance the viewing experience and transcoding costs.<br><br>Parameter values:<br><br><br>* **0 to 300:**  Defines a specific waiting period. The task stops if no new viewer joins before this period expires.<br><br>*  **\-1:**  Sets the waiting period to **infinite**. The task will never stop automatically as long as the source stream is live.<br><br><br>Configure the waiting time based on your streaming scenario:<br><br><br>* **For the best experience:**  If you expect high viewer turnover (for example, during live sports or popular events), set a **longer waiting time (such as 60\-180 seconds)** . This ensures most new viewers experience instant playback but will increase costs during idle periods.<br><br>* **To control costs:**  If your viewers are relatively stable or cost\-saving is a priority, set a **shorter waiting time (such as 10\-30 seconds)** . This stops transcoding tasks sooner when no one is watching, reducing your expenses.<br><br>* **For critical 24/7 streams:**  Use a value of  **\-1** only for essential streams where instant startup is mandatory at all times, and you accept continuous transcoding costs.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This setting is only available when <strong>Trigger transcoding</strong> is set to <strong>Stream pulling</strong>.</div><br> |
   |Bitrate control method |Specifies how the encoder allocates the bitrate for your transcoded stream. You can choose **abr** or **cbr**.<br><br><br>* **abr (average bitrate):**  This method flexibly adjusts the bitrate, allocating more data to complex, high\-motion scenes and less to simple, static ones. While the bitrate fluctuates to match the content's demands, the average bitrate remains very close to your target setting over the stream's duration. This results in more consistent video quality, delivering sharper images in high\-motion scenes without wasting bandwidth on less detailed scenes. The **abr** option is recommended for most streaming scenarios as this option offers the best balance between video quality and bandwidth usage.<br><br>* **cbr**  **(constant bitrate)** : This method maintains a fixed, steady bitrate throughout the entire stream, regardless of the complexity of the video content. This provides a highly predictable and stable stream size, which can simplify bandwidth management. However, because the bitrate cannot increase to handle complexity, video quality may drop during high\-motion scenes. Choose **cbr** only if your player or downstream services have strict requirements for a constant bitrate.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For 4K or 2K quality, the bitrate control method is fixed to <strong>abr</strong>.</div><br> |
   |Resolution does not exceed the source stream |* **Enabled (Default):**  Prevents upscaling the video resolution to a higher resolution than the source stream. If the source stream's resolution is lower than your configured setting, for example, your transcoding configuration is set to `1080p`, but the source stream is `720p`, the output resolution will also be `720p`. This avoids potential quality degradation and unnecessary costs.<br><br>* **Disabled:**  Forces the output to match the configured resolution, even if this means upscaling a lower\-resolution source. Only disable this if your player or downstream services strictly require a fixed resolution. |
   |Bitrate does not exceed the source stream |* **Enabled (Default):**  Prevents the output bitrate from exceeding the source stream. If the source stream's bitrate is lower than your configured setting, for example, your transcoding configuration is set to 3200 kbps, but the source stream is 2048 kbps, the output bitrate will also be 2048 kbps. This optimizes bandwidth usage and reduces costs because increasing the bitrate beyond the source stream brings no benefit.<br><br>* **Disabled:**  Forces the output to match the configured bitrate. Only disable this if a specific, constant bitrate is strictly required for your player or downstream services. |
   |Frame rate does not exceed the source stream |* **Enabled (Default):**  Prevents the output frame rate from exceeding the source stream. If the source stream's frame rate is lower than your configured setting, for example, your transcoding configuration is set to 30 fps, but the source stream is 25 fps, the output frame rate will also be 25 fps. This ensures smooth playback by avoiding frame duplication and reduces unnecessary processing costs.<br><br>* **Disabled**: Forces the output to match the configured frame rate. Only disable this if your player or downstream services have a strict requirement for a constant frame rate. Forcing a higher frame rate can cause stuttering or jerky motion, as this process involves duplicating existing frames to meet the target. |
   

5. Click **Confirm** to save your configuration. You can always click **Edit** or **Delete** in the **Action** column to edit or delete the configuration.

   After adding, updating, or deleting a transcoding configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.


<span id="0a7effed"></span>
## What to do next


1. Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate the pull stream address of the transcoded stream for playback.

   1. Complete the following configurations, and click **Generates Pull stream address**.

      * **Address type**: Select **Pull stream address**.

      * **Domain name**: Select the domain name for stream pulling within the domain name space used when adding the transcoding configuration.

      * **AppName** and **StreamName**: Enter the `AppName` and `StreamName` from your push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then the `AppName` is `live`, and the `StreamName` is `test`.

   2. Get the pull stream address of the transcoded stream.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe6ba99a0eb497b8ee1f4d55bea8e35~tplv-goo7wpa0wc-image.image) </span>

2. Use your push stream address to push the source stream.

3. Pull the transcoded stream for playback using one of the following methods:

   
   |Method |Scenario |Description |
   |---|---|---|
   |Player SDK for Web |Play transcoded streams in a web browser. |Integrate the Player SDK for Web and pull the transcoded stream on your website or web app. For more information, see [Feature integration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-feature-integration). |
   |Client SDK |Play transcoded streams in a native mobile app. |Integrate the client SDK and pull the transcoded stream in a mobile app. For more information, see:<br><br><br>* iOS: [Player SDK for iOS: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)<br><br>* Android: [Player SDK for Android: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)<br><br>* Flutter: [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* React Native: [Player SDK for React Native: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features) |
   |BytePlus MediaLive console |For quick preview and debugging during development or testing. |On the [Web pull page](https://console.byteplus.com/live/main/webPullStream/play) in the console, enter the pull stream address of the transcoded stream to quickly verify playback. For more information, see [Pulling a stream through the console](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports playing FLV, HLS, and RTM streams.</div><br> |
   


<span id="de0efcc1"></span>
## FAQ

<span id="030af93e"></span>
### Why isn't my new transcoding configuration working?

After adding, updating, or deleting a transcoding configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.

<span id="8b43b1de"></span>
### How do I offer multiple quality levels, like 1080p, 720p, and 540p, for a single stream?

You can achieve this by adding a separate transcoding configuration for each quality level you want to offer. Ensure all configurations are added within the same domain name space and apply to the same `AppName`.

For example, for a single `AppName`, add multiple configurations, each with a unique suffix:


* One configuration with the suffix `uhd` for a 1080p stream.

* A second configuration with the suffix `hd` for a 720p stream.

* A third configuration with the suffix `sd` for a 540p stream.


Unique pull stream addresses are generated for each quality level by appending the corresponding suffix to the `StreamName`. For example, if your `StreamName` is `myStream`, you will get separate addresses like `myStream_uhd`, `myStream_hd`, and `myStream_sd`.

<span id="a97812a7"></span>
### The first viewer to watch my stream experiences a delay. How can I fix this?

This delay occurs because the **Trigger transcoding** setting is set to **Stream pulling**, which starts transcoding only when the first viewer starts watching. To eliminate this startup delay, change the trigger to **Stream pushing**. This will start the transcoding process the moment your source stream goes live, ensuring instant playback for all viewers. Be aware that this option incurs costs as long as the source stream is live, even if no one is watching.

<span id="9fc233b8"></span>
### What are the best ways to control transcoding costs?

To optimize your expenses, consider these strategies:


* **Use the stream pulling trigger:**  Keep **Trigger transcoding** set to **Stream pulling**, so you only pay for transcoding when someone is actively watching.

* **Copy the source audio:**  Set the **Audio option** to **Copy source stream**. This avoids audio transcoding fees entirely and preserves the original audio quality.

* **Choose the standard transcoding mode:**  Select **Standard mode** as the **Type**. This is the more economical option and is ideal for scenarios where minimizing transcoding costs is your main priority.

* **Avoid unnecessary upscaling:**  Keep the **does not exceed the source stream** options enabled. This prevents wasting resources, as transcoding to a resolution, bitrate, or frame rate higher than the source does not improve video quality.


<span id="fab0d0e5"></span>
### What's the best resolution setting for streams viewed on both mobile and desktop?

For maximum flexibility, use the **Fixed long side** scaling mode for your resolution. This setting intelligently adapts to both landscape and portrait streams with a single rule. For instance, if you set the long side to 1280 px, this setting will correctly resize a 1920x1080 desktop stream to 1280x720 and a 1080x1920 mobile stream to 720x1280, ensuring an optimal viewing experience on any device.

<span id="05b08348"></span>
### Transcoding vs. adaptive bitrate: Which one should I use?

Choose the configuration that best fits your streaming protocol and desired viewing experience. The key difference lies in whether the player can automatically switch between quality levels.


* **Transcoding**: Use the transcoding configuration in the following scenarios:

   * **Broader protocol support**: When you need to stream using protocols that the ABR feature does not support, such as RTMP.

   * **Manual quality selection**: When you want to provide separate pull stream addresses for each quality level and implement a manual quality selector in your player, allowing viewers to choose their preferred resolution.

* **ABR**: Use the ABR configuration to provide a seamless, auto\-adjusting viewing experience. This feature provides multiple quality levels, and the player automatically switches between them based on the viewer's network conditions, ensuring smooth playback at the best possible video quality.


<span id="17aff9cd"></span>
### What is the difference between ABR (adaptive bitrate) and abr (average bitrate)?


* **ABR** (adaptive bitrate): This is a delivery technology that bundles multiple transcoded streams into a single playlist, enabling the player to switch quality levels automatically.

* **abr** (average bitrate): This is an encoding setting within a transcoding configuration that optimizes video quality by allowing the bitrate to fluctuate based on scene complexity.


<span id="6bcc8379"></span>
### Can transcoding improve the quality of a blurry source stream?

No, transcoding cannot create detail that is not in the source stream. If your source stream is blurry or low\-quality, the transcoded streams will also appear blurry, even if you set them to a higher resolution, bitrate, or frame rate.

<span id="56b955de"></span>
### When does transcoding start to be billed?

Transcoding is billed based on the duration of the transcoding task.


* If you select **Stream pushing** as the **Trigger transcoding**: Billing starts when you start pushing your source stream. You are billed for the entire duration of your live stream, whether or not anyone is watching.

* If you select **Stream pulling** as the **Trigger transcoding**: Billing starts only when the first viewer begins playing a transcoded stream. You only pay for the time that your transcoded streams are actively being watched.
