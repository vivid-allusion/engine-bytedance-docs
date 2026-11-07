---
title: "Managing time shifting configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-time-shifting"
---

The time shifting feature allows viewers to control the progress of a live stream, just like watching a video on demand. Whether the live stream is ongoing or has ended, viewers can pause and seamlessly resume, replay any previously streamed content, or start from the beginning at any time within the configured time range, ensuring they do not miss any important content. This topic will guide you through the complete steps from configuration to playback.

## Core values

* **Enhanced viewing experience**: Viewers are no longer limited to "real time". They can pause and replay key moments at any time, for example, goals in sports events or key explanations in online classes, which greatly enhances viewing flexibility and satisfaction.

* **Increased content consumption**: Viewers who join midway can watch from the beginning to experience the full content, which effectively increases their online time and engagement.

* **Instant content reuse**: After the live stream ends, time\-shifted content is available for on\-demand playback, achieving a "live\-to\-replay" experience.

## How it works

Time shifting can be simply understood as streaming while recording simultaneously. When you enable the time shifting feature, the server performs the following operations:

1. Real\-time recording and indexing: The server segments the live stream into video clips (TS files) in real time according to the HLS protocol. At the same time, the system maintains an M3U8 playlist file that contains the complete playback sequence of all these TS files.

2. Responding to playback requests: When a viewer pauses, rewinds, or starts from the beginning, the player requests video content at a specific point in time from the server using the `timeshift` or `start`/`end` parameters.

3. Generating a custom playlist: After receiving the request, the server dynamically generates a temporary, custom playlist for the viewer based on the M3U8 file. This playlist contains only the TS files for the time range the viewer wants to watch.

4. On\-demand playback: After getting the custom playlist, the player loads and plays the TS files in sequence, creating the time\-shifting effect.

## Notes

* **Fees:**

   * Using time shifting will incur storage fees and recording fees. See [Time shifting](https://docs.byteplus.com/docs/byteplus-media-live/docs-time-shifting) for storage fees and [Recording](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding_2) for recording fees.

   * Selecting **Transcoding stream** or **HLS\-ABR** as the **Recording stream type** will incur transcoding fees. For more information, see [Transcoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding).

* **Activation time**: After adding, updating, or deleting a time\-shifting configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.

## Prerequisites

* You have added a domain name for stream pushing and a domain name for stream pulling to your desired domain name space. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

* To add a configuration by using the settings from an existing recording configuration, make sure you have added a recording configuration using **HLS** as the recording format and storing recorded files in a TOS bucket. For more information, see [Storing recorded files in a TOS bucket](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-recordings#fbac8c5c).

* To generate time\-shifted content from transcoded streams, add a transcoding configuration with the **Trigger transcoding** set to **Stream pushing** under your desired domain name space. Make sure the transcoding configuration and the time\-shifting configuration to be added use the same `AppName` and domain name space. For more information, see [Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).

* To generate time\-shifted content from adaptive bitrate (ABR) substreams of the main playlist, add an ABR configuration with **HLS\-ABR** as the protocol type under your desired domain name space. Make sure the ABR configuration and the time\-shifting configuration to be added use the same `AppName` and domain name space. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

## Step 1: Add a time\-shifting configuration

You can add a time\-shifting configuration in two ways. Your choice depends on whether you are already using the recording feature and where you want to store the time\-shifted content.

* [Adding a configuration from scratch](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting#8cd67d7c): Uses MediaLive default storage for time\-shifted content. The time\-shifted content is stored in a public TOS bucket managed by BytePlus. You do not need to provide or manage your own storage bucket.

   Select this when:

   * You are **not** using the recording feature.

   * You want a **quick and simple setup** without having to manage your own TOS bucket for time\-shifting.

   * Your primary goal is to simply enable the time\-shifting feature, and you do not need direct access to the time\-shifted content files.

* [Add from an existing recording configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting#c0228dfa): Allows you to add a time\-shifting configuration by reusing the settings from an existing recording configuration that uses **HLS** as the recording format and stores files in your own TOS bucket.

   Select this when:

   * You are **already** using the recording feature with your own TOS bucket.

   * Your recording configuration uses **HLS** as the recording format.

   * You need **direct access** to the time\-shifted content files for further processing.

### Adding a configuration from scratch

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and click the **Time shifting** tab on the right.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. Complete the configurations and click **Confirm**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67a99a1d0c22452695cf9bc3b9a631bc~tplv-goo7wpa0wc-topic.webp)

   |Parameter |Description |
   |---|---|
   |Storage type |Select **MediaLive default storage**. |
   |AppName |Specify the `AppName` this configuration will apply to. This name must exactly match the `AppName` in your push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then the `AppName` is `live`.<br><br>The `AppName` can contain letters (a\-z, A\-Z), numbers (0\-9), underscores (`_`), and hyphens (`-`), and must be 1\-30 characters long. |
   |StreamName |Specify the `StreamName` this configuration will apply to. This name must exactly match the `StreamName` in your push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then the `StreamName` is `test`.<br><br><br>* **For a specific stream**: Enter the `StreamName`, which can contain letters (a\-z, A\-Z), numbers (0\-9), underscores (`_`), and hyphens (`-`), and must be 1\-100 characters long. The configuration applies only to that stream under the specified `AppName`.<br><br>* **For all streams under the specified AppName**: Enter a single asterisk (`*`) or leave the field empty. The configuration applies to all streams under the specified `AppName`.<br><br><br>> **Note**<br><br><br><br>* > When multiple time\-shifting configurations match the same stream, the most specific configuration takes precedence.<br><br><br>* > For the same domain name space and `AppName`, you can add time\-shifting configurations for up to 20 specific `StreamName` values. This limit applies only to configurations with a specific `StreamName`. Configurations that apply to all streams under an `AppName` do not count toward this limit.<br><br><br>* > If multiple streams under the same `AppName` use the same time\-shifting rule, set `StreamName` to `*` or leave it empty. If you create configurations for specific `StreamName` values one by one, only those configured streams can use time shifting.<br> |
   |Recording stream type |Select the stream type to generate the time\-shifted content.<br><br><br>* **Original stream**: Use the original stream to generate time\-shifted content without transcoding. Viewers will see video quality identical to the original stream when watching time\-shifted content.<br><br>* **Transcoding stream**: Use transcoded streams to generate time\-shifted content. Viewers can switch quality levels when watching time\-shifted content. Time\-shifted content is generated for all transcoded streams that match this configuration. You cannot select specific transcoded stream suffixes.<br><br>   Time\-shifted content is generated only from transcoded streams produced by transcoding configurations with **Trigger transcoding** set to **Stream pushing** for the same `AppName` in the selected domain name space.<br><br>* **HLS\-ABR**: Use all substreams in the main playlist to generate time\-shifted content, so viewers can continue watching time\-shifted content when the player automatically switches quality levels based on network conditions. You cannot select specific substreams.<br><br>   You can select **HLS\-ABR** only when an ABR configuration with **HLS\-ABR** as the protocol type already exists for the same `AppName` in the selected domain name space.<br><br><br>> **Note**<br><br><br><br>* > You can only select **HLS\-ABR** when adding a time\-shifting configuration. After the configuration is added, you cannot change the **Recording stream type** to or from **HLS\-ABR**.<br><br><br>* > Please manage the transcoding or ABR configuration that is being used by the time\-shifting configuration carefully to ensure that your time\-shifted content is generated properly.<br><br><br>   * > If you delete a transcoding or ABR configuration that is being used by the time\-shifting configuration, viewers will not be able to watch time\-shifted content.<br><br><br>   * > If you update a transcoding or ABR configuration that is being used by the time\-shifting configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect.<br> |
   |TS segment length |The duration of each video segment (TS file) in the HLS video stream, in seconds. Value range [3, 20].<br><br>This value primarily affects seeking precision and playback stability. You must find a balance between these two when adjusting this value.<br><br><br>* Shorter segment length (for example, 3\-5 seconds)<br><br>   * **Pros**: Provides higher seeking precision. Smaller segments enable viewers to locate and jump to a specific moment on the progress bar more accurately.<br><br>   * **Cons**: Increases the risk of stuttering. Smaller segments reduce the player's buffer time and the tolerance for network fluctuations, making stuttering more likely during network jitter.<br><br>   * **Scenarios**: Scenarios that require high seeking precision, for example, sports event analysis, game highlight replays, and reviewing key points in online courses.<br><br>* Longer segment length (for example, 10\-15 seconds)<br><br>   * **Pros**: Improves playback stability. With larger segments, the player can obtain a longer buffer from a single download, effectively resisting network jitter and reducing stuttering during playback.<br><br>   * **Cons**: Lowers seeking precision. Longer segments restrict viewers from precisely locating a position on the progress bar, making it difficult to jump to a specific second.<br><br>   * **Scenarios**: Scenarios where smooth playback is prioritized over precise seeking, for example, watching replays of general programs and watching recorded press conferences. |
   |Shift time |The duration that time\-shifted content is retained for viewers to watch after the live stream ends. The retention period starts from the actual end time of the live stream. Once the retention period expires, the system automatically deletes the stored time\-shift files, and viewers can no longer watch the time\-shifted content. Deleting the time\-shifting configuration does not change the expiration time of existing time\-shift files.<br><br>For example, if you set **Shift time** to **1 day** for a live stream from 19:00 to 20:00 on January 1, viewers can watch the time\-shifted content before 20:00 on January 2.<br><br>Valid values:<br><br><br>* **1 day**<br><br>* **3 days**<br><br>* **7 days**<br><br>* **15 days** |
   |Distribution domain name |Select a domain name for stream pulling under the current domain name space to generate the playback address for time\-shifted content. Viewers can watch the time\-shifted content using the selected domain name. |

5. You can always click **Edit** or **Delete** in the **Action** column to edit or delete the configuration.

   After adding, updating, or deleting a time\-shifting configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect. After the configuration takes effect, **Online** is displayed in the **Status** column.

### Add from an existing recording configuration

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and click the **Time shifting** tab on the right.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. Complete the configurations and click **Confirm**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9c0f183c131405981d5bea36b6cd435~tplv-goo7wpa0wc-topic.webp)

   > **Note**

   > Settings such as **Bucketname**, **StreamName**, and **Recording stream type** are reused directly from the selected recording configuration and displayed in the time\-shifting configuration. These settings cannot be modified in the time\-shifting configuration.

   * > If the selected recording configuration uses **Transcoding stream** as the **Recording stream type**, the time\-shifting configuration also uses **Transcoding stream**, and time\-shifted content is generated for the same transcoded stream suffixes selected in the recording configuration.

   * > If the selected recording configuration uses **HLS\-ABR** as the **Recording stream type**, the time\-shifting configuration also uses **HLS\-ABR**, and time\-shifted content is generated for the same ABR substreams selected in the recording configuration.

   * > A time\-shifting configuration added from an existing recording configuration requires HLS recording to be enabled for the selected recording configuration. When the live stream is recorded, time\-shifted playback uses the HLS files generated by the recording configuration.

   * > Do not delete the HLS playlist or TS files generated by the selected recording configuration. Deleting these files can prevent time\-shifted playback for the affected content.

   |Parameter |Description |
   |---|---|
   |Storage type |Select **Use the pre\-configured AppName (for Recording)** . |
   |AppName |Select the `AppName` of the recording configuration.<br><br>You can also click **Configure a recording task** to add a recording configuration. Make sure you use **HLS** as the recording format and TOS as the storage location for the recording configuration. |
   |Shift time |Sets how long viewers can access time\-shifted content after the live stream ends. When the duration ends, viewers can no longer use time\-shifted playback. **Shift time** does not change how long recorded files are stored.<br><br>For example, if you set **Shift time** to **1 day** for a live stream from 19:00 to 20:00 on January 1, viewers can watch the time\-shifted content before 20:00 on January 2.<br><br>Valid values:<br><br><br>* **1 day**<br><br>* **3 days**<br><br>* **7 days**<br><br>* **15 days** |
   |Distribution domain name |Select a domain name for stream pulling under the current domain name space to generate the time\-shifted playback address. Viewers can watch the time\-shifted content using the selected domain name. |

5. You can always click **Edit** or **Delete** in the **Action** column to edit or delete the configuration.

   After adding, updating, or deleting a time\-shifting configuration, you must wait for 3\-5 minutes and then restart pushing your stream for the new configuration to take effect. After the configuration takes effect, **Online** is displayed in the **Status** column.

## Step 2: Generate a playback address for time\-shifted content

After adding a time\-shifting configuration, generate a playback address for the time\-shifted content and use the address in your player.

To enable time\-shifted playback, configure your player to use the pull stream address for the live stream first. When viewers rewind, start from the beginning, or choose a past time point to watch, generate a time\-shifted playback address and pass the address to the player to pull and play the requested content, as follows.

> **Note**

> If you use the Player SDK for Web to pull and play the requested content, see [Live time shifting](https://docs.byteplus.com/docs/byteplus-media-live/docs-live-time-shifting).

* **Relative time shifting**: Use this mode during an ongoing live stream when viewers need to replay content from a certain amount of time before the current live position.

   When a viewer drags the progress bar to replay earlier content, the player calculates the time difference, in seconds, between the target position and the current live position. The player then uses this value for the `timeshift` parameter to generate a new playback address and play the requested content.

   Append `&{AuthInfo}` to the playback address only when URL authentication is enabled. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

   For original and transcoded streams, the time\-shifted playback address uses the following format:

   ```Plain
   http(s)://{DomainName}/{AppName}/{StreamName}{Suffix}.m3u8?timeshift={time}&{AuthInfo}
   ```

   For an original stream, leave `Suffix` empty. For a transcoded stream, `Suffix` is the transcoding suffix in your transcoding configuration, such as `_hd`.

   For HLS\-ABR time\-shifted content, use the HLS\-ABR address format:

   ```Plain
   http(s)://{DomainName}/{AppName}/{StreamName}/abr.m3u8?timeshift={time}&{AuthInfo}
   ```

   **Example**:

   A viewer drags the progress bar to replay content from 5 minutes earlier.

   * Original stream playback address: `http://pull.example.com/live/test.m3u8`

   * Original stream time\-shifted playback address generated by the player: `http://pull.example.com/live/test.m3u8?timeshift=300`

   * Transcoded stream time\-shifted playback address generated by the player: `http://pull.example.com/live/test_hd.m3u8?timeshift=300`

   * HLS\-ABR time\-shifted playback address generated by the player: `http://pull.example.com/live/test/abr.m3u8?timeshift=300`

   After the player uses the time\-shifted playback address to pull the content, the viewer immediately jumps to the content from 5 minutes earlier and continues watching from that point.

* **Absolute time shifting**: Use this mode when you want viewers to watch content from a specific time range, either during the live stream or after the live stream ends. To do this, add the `mode`, `start`, and `end` parameters to the playback address. The `start` and `end` values support RFC3339 UTC time with second precision, Unix timestamps in seconds, or the `YYYYMMDDHHMMSS` format. Values in the `YYYYMMDDHHMMSS` format are interpreted as UTC+0. For example, `20260325153000` means 15:30:00 UTC+0 on March 25, 2026.

   A common example is when a viewer joins an ongoing live stream late and wants to start from the beginning, or when a viewer wants to replay a specific period after the live stream ends, such as from 19:00 to 19:30.

   * `mode`: This parameter determines how the player plays the requested time range and what happens after playback reaches the `end` time. The default value is `1`.

      * When the value is `1`: The content is played like video on demand. This is suitable for complete replays or highlight playback after the live stream ends. The server returns a playlist (M3U8 file) that includes the `#EXT-X-ENDLIST` tag, and the player stops playing the video automatically when reaching the `end` time. Viewers can drag the progress bar freely, just like watching an on\-demand video.

      * When the value is `3`: The content is played like a live stream. This is suitable when viewers need to start from an earlier time point during an ongoing live stream and then continue watching the live stream. The server returns a playlist (M3U8 file) without the `#EXT-X-ENDLIST` tag, so the player treats the stream as still live. After playback reaches the `end` time, the player continues with the following live content if the live stream is still ongoing.

      > **Warning**

      > When `mode` is set to `3`, the `start` value cannot be earlier than 2 hours before the actual start time for the live stream. For example, if the live stream starts at 15:00 on March 25, 2026, the earliest valid `start` value is 13:00 on March 25, 2026. An earlier value returns a `404` error.

   * `start`: The playback start time.

   * `end`: The playback end time.

      Append `&{AuthInfo}` to the playback address only when URL authentication is enabled. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication).

      For original and transcoded streams, the time\-shifted playback address uses the following format:

   ```Plain
   http(s)://{DomainName}/{AppName}/{StreamName}{Suffix}.m3u8?mode={mode}&start={UTC/Unix/Human}&end={UTC/Unix/Human}&{AuthInfo}
   ```

   For an original stream, leave `Suffix` empty. For a transcoded stream, `Suffix` is the transcoding suffix in your transcoding configuration, such as `_hd`.

   For HLS\-ABR time\-shifted content, use the HLS\-ABR address format:

   ```Plain
   http(s)://{DomainName}/{AppName}/{StreamName}/abr.m3u8?mode={mode}&start={UTC/Unix/Human}&end={UTC/Unix/Human}&{AuthInfo}
   ```

   **Example**:

   Assume a live stream runs from 15:00 to 17:00 UTC+0 on March 25, 2026. To provide a complete replay after the live stream ends, use one of the following playback addresses:

   * Original stream: `http://pull.example.com/live/test.m3u8?mode=1&start=20260325150000&end=20260325170000`

   * Transcoded stream with the `_hd` suffix: `http://pull.example.com/live/test_hd.m3u8?mode=1&start=20260325150000&end=20260325170000`

   * HLS\-ABR: `http://pull.example.com/live/test/abr.m3u8?mode=1&start=20260325150000&end=20260325170000`

The parameters are described as follows:

|Parameter |Description |Sample value |
|---|---|---|
|DomainName |The domain name for stream pulling, which is the one selected in the time shifting configuration. |`pull.example.com` |
|AppName |The `AppName`, which is the same as that in your push stream address. |`live` |
|StreamName |The `StreamName`, which is the same as that in your push stream address. |`test` |
|AuthInfo |The authentication information, which is necessary only when you enable the URL authentication for the domain name for stream pulling. For example, if you use Type A URL authentication, the authentication information is `auth_key={timestamp}-{rand}-{uid}-{md5hash}`. For more information, see [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication). |`auth_key=1758296819-123e4567-0-fbe5e26c0b****1431c3c897f7bdc278` |
|timeshift |In relative time shifting mode, this is the time difference, in seconds, between the target position and the current live position when a viewer drags the progress bar to replay earlier content. The valid range is (0,604800]. For example, a value of `300` lets the viewer watch live content from 5 minutes earlier. |`300` |
|mode |In absolute time shifting mode, this parameter determines how the player plays the requested time range and what happens after playback reaches the `end` time. The default value is `1`. Valid values:<br><br><br>* `1`: The content is played like video on demand. The player stops playing the video automatically when reaching the `end` time. Viewers can drag the progress bar freely, just like watching an on\-demand video.<br><br>* `3`: The content is played like a live stream. After playback reaches the `end` time, the player continues with the following live content if the live stream is still ongoing. |`3` |
|start |The playback start time. `start` and `end` can use different supported formats, but we recommend using the same format for both values to avoid confusion. Supported formats are as follows:<br><br><br>* `UTC`: RFC3339 UTC time with second precision, for example, `2026-03-25T15:00:00Z`.<br><br>* `Unix`: Unix timestamp in seconds, for example, `1774422000`.<br><br>* `Human`: A human\-readable time in the `YYYYMMDDHHMMSS` format, interpreted as UTC+0. For example, `20260325153000` means 15:30:00 UTC+0 on March 25, 2026. |`1774422000` |
|end |The playback end time. Supported formats are as follows:<br><br><br>* `UTC`: RFC3339 UTC time with second precision, for example, `2026-03-25T17:00:00Z`.<br><br>* `Unix`: Unix timestamp in seconds, for example, `1774429200`.<br><br>* `Human`: A human\-readable time in the `YYYYMMDDHHMMSS` format, interpreted as UTC+0. For example, `20260325170000` means 17:00:00 UTC+0 on March 25, 2026. |`1774429200` |
