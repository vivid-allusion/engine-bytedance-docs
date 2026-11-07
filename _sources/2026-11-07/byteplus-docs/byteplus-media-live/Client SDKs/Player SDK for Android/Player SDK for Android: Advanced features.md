---
title: "Player SDK for Android: Advanced features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2"
---

To enhance the viewing experience in your Android app, this topic details how to implement advanced features of the Player SDK for Android. You can implement complex features as needed, according to actual business requirements.

 &nbsp;

<span id="prerequisites"></span>
## Prerequisites


* You have implemented the basic features of the Player SDK by following the instructions provided in [Player SDK for Android: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2).

* To use the following features, ensure you use a premium or trial license.

   * [Playing RTM streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#af29cf39)

   * [QUIC stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#4d503d05)

   * [Playing CMAF streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#915c6bb1)

   * [Playing low-latency FLV streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#1d5784e5)

   * [Primary-backup stream switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#77618e0b)

   * [ABR stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#34e237fb)

   * [Super-resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#84bd3b42)

   * [H.265 hardware decoding and software decoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#3ca5b85e)

   * [H.266 software decoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#71012b84)

   * [Video sharpening](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#15a71a29)

   * Commercial DRM (Digital Rights Management)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7">Upgrading a trial license to a basic or premium license</a>.   </div>
   

 &nbsp;

<span id="notes"></span>
## Notes

Because the Player SDK uses various Android audio and video APIs that may not work properly on emulators, we recommend that you use a physical device for testing.

 &nbsp;

<span id="stream-fallback-strategy-and-primary-backup-stream-switching"></span>
## Stream fallback strategy and primary\-backup stream switching

If you configure only one pull stream address, playback might stutter or even fail when that address cannot be used due to network issues or other exceptions. To reduce the risk of playback failure caused by an exception on a single address, you can configure multiple pull stream addresses for one playback session and choose one of the following configuration methods as needed:


* **Stream fallback strategy**: Use this when you want the player to automatically try multiple pull stream addresses by priority. You can configure the priority and maximum retry count for each address. The player tries high\-priority addresses first. If an address is still unavailable after all retry attempts are exhausted, the player switches to the address with the next priority.

* **Primary\-backup stream switching**: Use this when your application maintains separate primary and backup stream lists. The player first tries the streams in the primary stream list according to the stream fallback strategy. Only after all addresses in the primary stream list fail does the player automatically switch to the backup stream list and continue trying.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support primary\-backup stream switching. The stream fallback strategy is available with all license types.</div>



* Stream fallback strategy

   The playback order in the primary or backup stream list is as follows:

   1. **Play the stream with the highest priority**: Based on the `priority` you set, the player tries to play streams in the current list from the highest priority to the lowest.

   2. **Retry on failure**: If the current stream fails to play, the player retries based on the stream's `retryMaxCount`.

   3. **Switch to a fallback stream**: If playback still fails after all retry attempts are exhausted, the player abandons the current stream and tries the next\-highest priority stream in the current list.

* Primary\-backup stream switching

   After primary\-backup stream switching is enabled, the player tries streams in the following order:

   1. **Play primary streams**: The player first tries to play streams in the primary stream list.

   2. **Switch to backup streams**: If all streams in the primary stream list fail to play, the player tries to play streams in the backup stream list.

   3. **Playback failure**: If all streams in the backup stream list also fail to play, playback fails.


During this process, the SDK notifies you of the current status using the following callbacks:


* [onInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-oninfo): Triggered when a stream fails to play but another available stream exists. You can use this callback to get detailed error information for debugging.

* [onStreamFormatSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch): Triggered when the player switches the stream format (for example, from RTM to FLV).

* [onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch): Triggered when all streams in the primary stream list fail to play and the player successfully switches to the backup stream list.

* [onError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onerror): Triggered when all streams in the primary and backup stream lists fail to play, and playback finally ends.


 &nbsp;

<span id="prerequisites-1"></span>
### Prerequisites

Get pull stream addresses for protocols such as RTM and FLV in one of the following ways. The fallback order within the same list is determined by the priority of each pull stream address.


* **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

* **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.


 &nbsp;

<span id="procedure"></span>
### Procedure

 &nbsp;

<span id="step-1:-configure-the-fallback-strategy"></span>
#### Step 1: Configure the fallback strategy

You can customize the fallback strategy by configuring the [priority](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-priority) and [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount) of `VeLivePlayerStream`.


* `priority`: The priority of the stream. The value must be `0` (default value) or a positive integer. **A larger value indicates a higher priority**. The player attempts to play higher\-priority streams first.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The priorities of the primary and backup stream lists are calculated independently and do not affect each other.   </div>
   

* `retryMaxCount`: The maximum number of playback attempts for the stream, including the initial attempt. For example, if the value is `3`, the player will retry a maximum of 2 more times after the first playback fails. Valid values:

   * `-1` (default value): Use the value of [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) in `VeLivePlayerConfiguration`.

   * `0`: Do not attempt to play this stream.

   * `>0`: The maximum number of playback attempts.



<Tabs>
<Tab zoneid="ZgjnIl56kX" title="Stream fallback strategy">
<TabTitle>Stream fallback strategy</TabTitle>

The following code sample demonstrates a basic stream fallback scenario, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4), with a maximum of 2 attempts.

3. If that also fails, playback ends.


```Java
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// Add an RTM primary stream (highest priority).
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// Configure the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```



</Tab>
<Tab zoneid="I1WQ4ZWaQi" title="Stream fallback strategy + primary-backup stream switching">
<TabTitle>Stream fallback strategy + primary-backup stream switching</TabTitle>

The following code sample demonstrates a scenario that combines the stream fallback strategy with primary\-backup stream switching, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5) from the primary stream list, with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4) from the primary stream list, with a maximum of 2 attempts.

3. If that still fails, the player switches to the backup stream list and tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

4. If that fails, the player falls back to the FLV stream (priority 4) from the backup stream list, with a maximum of 3 attempts.

5. If all of these attempts fail, playback ends.


```Java
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// Add an RTM primary stream (highest priority).
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// Configure the backup stream list.
List<VeLivePlayerStreamData.VeLivePlayerStream> backupStreams = new ArrayList<>();
// Add an RTM backup stream.
VeLivePlayerStreamData.VeLivePlayerStream rtmBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmBackupStream.url = "https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // Highest priority in the backup stream list.
backupStreams.add(rtmBackupStream);

// Add an FLV backup stream as a fallback stream.
VeLivePlayerStreamData.VeLivePlayerStream flvBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvBackupStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
backupStreams.add(flvBackupStream);
streamData.backupStreamList = backupStreams;

// Enable primary-backup stream switching.
streamData.enableMainBackupSwitch = true;

// Configure the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```



</Tab>
<Tab zoneid="jQIfz9ebuc" title="Multi-quality stream fallback strategy">
<TabTitle>Multi-quality stream fallback strategy</TabTitle>

The stream fallback strategy supports configuring fallback streams for multi\-quality stream configurations used by [resolution switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#23c93996), [ABR stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2) (FLV streams only), and [smooth quality level switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#d7282079). During configuration, set the same `priority` value for streams in the same multi\-quality stream group. The player first selects stream groups from the highest `priority` to the lowest. If playback of the high\-priority multi\-quality streams fails, the player falls back to lower\-priority streams.

In the following example, the player first plays the ABR multi\-quality streams whose `priority` is `5`. If playback of the ABR multi\-quality streams fails, the player falls back to a regular FLV stream whose `priority` is `4`.

```Java
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// Add the original quality level of the ABR multi-quality streams. The priority is 5.
VeLivePlayerStreamData.VeLivePlayerStream flvOriginStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvOriginStream.url = "https://xxx_origin.flv"; // Replace with the actual FLV pull stream address for the original quality level.
flvOriginStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvOriginStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvOriginStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvOriginStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // Original quality level.
flvOriginStream.bitrate = 2000;
flvOriginStream.retryMaxCount = 3;
flvOriginStream.priority = 5;
mainStreams.add(flvOriginStream);

// Add the UHD quality level of the ABR multi-quality streams. The priority is 5.
VeLivePlayerStreamData.VeLivePlayerStream flvUHDStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvUHDStream.url = "https://xxx_uhd.flv"; // Replace with the actual FLV pull stream address for the UHD quality level.
flvUHDStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvUHDStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvUHDStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvUHDStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // UHD quality level.
flvUHDStream.bitrate = 1800;
flvUHDStream.retryMaxCount = 3;
flvUHDStream.priority = 5;
mainStreams.add(flvUHDStream);

// Add the HD quality level of the ABR multi-quality streams. The priority is 5.
VeLivePlayerStreamData.VeLivePlayerStream flvHDStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvHDStream.url = "https://xxx_hd.flv"; // Replace with the actual FLV pull stream address for the HD quality level.
flvHDStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvHDStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvHDStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvHDStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // HD quality level.
flvHDStream.bitrate = 1500;
flvHDStream.retryMaxCount = 3;
flvHDStream.priority = 5;
mainStreams.add(flvHDStream);

// Add a regular FLV stream as a fallback stream. The priority is 4.
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// Configure the default startup quality level.
streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);

// Enable ABR.
streamData.enableABR = true;

// Configure the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```



</Tab>
</Tabs>


 &nbsp;

<span id="step-2:-add-callbacks"></span>
#### Step 2: Add callbacks

Add the following callbacks as needed to listen for events during the fallback process.


* Listen for stream format switching, for example, from RTM to FLV.

   ```Java
   @Override
   public void onStreamFormatSwitch(
       VeLivePlayer player,
       VeLivePlayerFormat fromStreamFormat,
       VeLivePlayerFormat toStreamFormat,
       VeLivePlayerError error,
       Bundle extraInfo
   ) {
   }
   ```
   

* Listen for recoverable issues encountered during playback. This callback is triggered when a stream fails to play but the SDK is about to perform a recovery action, such as switching to a fallback stream. This indicates that playback is still continuing, and you do not need to interrupt the playback process. You can use the returned error information to understand the specific reason for the stream playback failure during debugging.

   ```Java
   @Override
   public void onInfo(
       VeLivePlayer player,
       VeLivePlayerError error
   ) {
   }
   ```
   

* Listen for switching from the primary stream to the backup stream.

   ```Java
   @Override
   public void onMainBackupSwitch(
       VeLivePlayer player,
       VeLivePlayerStreamType streamType,
       VeLivePlayerError error
   ) {
   }
   ```
   

* Listen for when playback finally ends, meaning all streams have failed to play.

   ```Java
   @Override
   public void onError(
       VeLivePlayer player,
       VeLivePlayerError error
   ) {
   }
   ```
   


 &nbsp;

<span id="playing-rtm-streams"></span>
## Playing RTM streams

Playing RTM streams can reduce live streaming latency to 1\-2 seconds, providing viewers with a high\-quality live streaming experience.

However, the ultra\-low latency feature of RTM also places higher demands on the network environment. Under unstable network conditions, playback delays, stuttering, or failures may occur. If you want to automatically try pull stream addresses of other protocols, such as FLV, when an RTM pull stream address is unavailable, use this feature together with the stream fallback strategy or primary\-backup stream switching. For more information, see [Stream fallback strategy and primary-backup stream switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#77618e0b).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support playing RTM streams.</div>


 &nbsp;

<span id="prerequisites-2"></span>
### Prerequisites


* Ensure that you have integrated the Player SDK version 1.50.100 or later.

* Get pull stream addresses for protocols such as RTM and FLV in one of the following ways.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.


 &nbsp;

<span id="procedure-1"></span>
### Procedure

This topic provides the following two code samples, which correspond to scenarios from simple to complex:


* **Basic scenario**: Demonstrates how to automatically fall back to streams of other protocols, such as FLV, when a high\-priority RTM stream in the primary stream list fails to play.

* **Advanced scenario**: Adds the primary\-backup stream switching mechanism on top of the basic scenario. When all streams in the primary stream list, including the RTM stream and fallback streams, are unavailable, the player automatically switches to the backup stream list to retry.


We recommend that you start with the basic scenario.


<Tabs>
<Tab zoneid="kimfZYTmSS" title="Basic scenario">
<TabTitle>Basic scenario</TabTitle>

The following code sample demonstrates a basic stream fallback scenario, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4), with a maximum of 2 attempts.

3. If that also fails, playback ends.


```Java
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// Add an RTM primary stream (highest priority).
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// Configure the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```



</Tab>
<Tab zoneid="JdEJaz5byQ" title="Advanced scenario">
<TabTitle>Advanced scenario</TabTitle>

The following code sample demonstrates a scenario that combines the stream fallback strategy with primary\-backup stream switching, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5) from the primary stream list, with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4) from the primary stream list, with a maximum of 2 attempts.

3. If that still fails, the player switches to the backup stream list and tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

4. If that fails, the player falls back to the FLV stream (priority 4) from the backup stream list, with a maximum of 3 attempts.

5. If all of these attempts fail, playback ends.


```Java
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// Add an RTM primary stream (highest priority).
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// Configure the backup stream list.
List<VeLivePlayerStreamData.VeLivePlayerStream> backupStreams = new ArrayList<>();
// Add an RTM backup stream.
VeLivePlayerStreamData.VeLivePlayerStream rtmBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmBackupStream.url = "https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // Highest priority in the backup stream list.
backupStreams.add(rtmBackupStream);

// Add an FLV backup stream as a fallback stream.
VeLivePlayerStreamData.VeLivePlayerStream flvBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvBackupStream.url = "https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
backupStreams.add(flvBackupStream);
streamData.backupStreamList = backupStreams;

// Enable primary-backup stream switching.
streamData.enableMainBackupSwitch = true;

// Configure the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```



</Tab>
</Tabs>


 &nbsp;

<span id="playing-cmaf-streams"></span>
## Playing CMAF streams

CMAF (Common Media Application Format) is a packaging format designed for delivering media in segments. When playing CMAF streams, the player retrieves the playback manifest from a `.mpd` pull stream address and then pulls the corresponding audio and video segments for live playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support playing CMAF streams.</div>


 &nbsp;

<span id="prerequisites-3"></span>
### Prerequisites

Get `.mpd` pull stream addresses for source streams in one of the following ways.


* **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate `.mpd` pull stream addresses.

* **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate `.mpd` pull stream addresses.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Only <code>.mpd</code> pull stream addresses for source streams support CMAF playback. <code>.mpd</code> pull stream addresses for ABR streams do not support CMAF playback.</div>


 &nbsp;

<span id="procedure-2"></span>
### Procedure


* Call the [setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) method with a `.mpd` pull stream address for playback. The player automatically recognizes the stream as a CMAF stream, and no additional format configuration is required.

   ```Java
   mLivePlayer.setPlayUrl("https://pull.example.com/live/stream/index.mpd"); // Replace with your actual .mpd pull stream address.
   
   // Start playback.
   mLivePlayer.play();
   ```
   

* Call the [setPlayStreamData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) method to configure one or more pull stream addresses, and explicitly set the stream format to `VeLivePlayerFormatCMAF`. The following sample code uses a CMAF stream as the primary stream.

   ```Java
   VeLivePlayerStreamData.VeLivePlayerStream stream = new VeLivePlayerStreamData.VeLivePlayerStream();
   stream.url = "https://pull.example.com/live/stream/index.mpd"; // Replace with your actual .mpd pull stream address.
   stream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatCMAF; // Explicitly set the stream format to VeLivePlayerFormatCMAF.
   stream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   streamData.mainStreamList = new ArrayList<>();
   // Add the CMAF stream.
   streamData.mainStreamList.add(stream);
   // Set the default stream format of the playback source to CMAF.
   streamData.defaultFormat = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatCMAF;
   // Configure the playback source.
   mLivePlayer.setPlayStreamData(streamData);
   // Start playback.
   mLivePlayer.play();
   ```
   


 &nbsp;

<span id="playing-low-latency-flv-streams"></span>
## Playing low\-latency FLV streams

After low\-latency FLV streaming is enabled, FLV stream pulling can reduce live streaming latency to 2\-3 seconds.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To play low\-latency FLV streams, make sure that you have integrated SDK version 1.50.200.3 or later and are using a premium or trial license.</div>


 &nbsp;

<span id="procedure-3"></span>
### Procedure

Before starting playback, you can enable low\-latency FLV streaming through the player's advanced API [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty). When calling `setProperty`, you need to pass a `key-value` configuration.

**Key**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|VeLivePlayerKeySetParamsLowLatencyFLV |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |The property key for the low\-latency FLV streaming feature. |


**Value**

The value is a `JSONObject` object containing `key-value` pairs to configure the low\-latency FLV streaming feature.


* `Key`: `String` type. The value is fixed to `EnableLowLatencyFLV`, which indicates whether to enable the low\-latency FLV streaming feature.

* `Value`: `Integer` type. A value of `1` enables the low\-latency FLV streaming feature, and a value of `0` disables the feature. The default value is `0`.


The sample code is as follows.

```Java
JSONObject flv2s = new JSONObject();
flv2s.put("EnableLowLatencyFLV", 1);
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsLowLatencyFLV, flv2s);
```


 &nbsp;

<span id="quic-stream-pulling"></span>
## QUIC stream pulling

The Player SDK supports QUIC stream pulling. This feature should be used together with BytePlus MediaLive.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support QUIC stream pulling.</div>


 &nbsp;

<span id="prerequisites-4"></span>
### Prerequisites

Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) in the BytePlus Live console to generate an FLV pull stream address.

 &nbsp;

<span id="procedure-4"></span>
### Procedure

Configure a QUIC pull stream address and start playback. The sample code is as follows.

```Java
VeLivePlayerStreamData.VeLivePlayerStream playStreamFLV = new VeLivePlayerStreamData.VeLivePlayerStream();
playStreamFLV.url = "https://pull.example.com/live/stream.flv"; // Replace with your actual FLV pull stream address.
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;
playStreamFLV.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
playStreamFLV.streamType = VeLivePlayerStreamTypeMain;

// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
streamData.mainStreamList = new ArrayList<>();

// Add the FLV stream.
streamData.mainStreamList.add(playStreamFLV);

// Configure the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The Player SDK enables the QUIC failure fallback strategy by default. If QUIC stream pulling fails, the SDK automatically falls back to TCP stream pulling.</div>


 &nbsp;

<span id="using-an-ip-address-as-the-pull-stream-address"></span>
## Using an IP address for stream pulling

The player supports using the IP address of the domain for stream pulling to reduce time\-to\-first\-frame.

 &nbsp;

<span id="prerequisites-5"></span>
### Prerequisites

Obtain the pull stream address and resolve its IP address.

 &nbsp;

<span id="notes-1"></span>
### Notes


* When using [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) to map domain names and IP addresses, disable the DNS pre\-resolution feature in the initial configuration by setting [enableLiveDNS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#enablelivedns) to `false`.

* Call [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) to set the domain\-to\-IP mapping before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) to start playback.


 &nbsp;

<span id="procedure-5"></span>
### Procedure

Use the player's [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) API to associate the IP address with the domain name. The player then directly uses the IP address for stream pulling. The sample code is as follows.

```Java
mLivePlayer.setPlayUrl("https://pull.example.com/live/stream.flv"); // Replace with your actual pull stream address.
// Map the domain in the pull stream address to its resolved IP addresses.
List<String> valueList = new ArrayList<>();
valueList.add("xxx.xxx.xxx.xxx"); // Replace with an actual IP address resolved from the domain.
Map<String, List<String>> map = new HashMap<>();
map.put("pull.example.com", valueList); // Replace pull.example.com with the domain in your actual pull stream address.

// Set the domain-to-IP mapping.
mLivePlayer.setUrlHostIP(map);

// Start playback.
mLivePlayer.play();
```


 &nbsp;

<span id="resolution-switching"></span>
## Resolution switching

You can set multiple pull stream addresses with different resolutions and switch between these addresses during playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Resolution switching supports the stream fallback strategy. You can assign the same priority to one group of multi\-resolution streams and configure lower\-priority fallback streams. If playback of the higher\-priority stream group fails, the SDK automatically tries the fallback group. For more information, see <a href="https://docs.byteplus.com/en/docs/24/7567#stream-fallback-strategy-and-primary-backup-stream-switching">Stream fallback strategy and primary\-backup stream switching</a>.</div>


<span id="hRIMcpN0E"></span>
### Prerequisites

Obtain the pull stream addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:


1. [Configure a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

2. Get the pull stream addresses for the original and the transcoded streams in one of the following ways.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.


This procedure uses the following pull stream addresses as examples.

&nbsp;


|**Resolution** |**Pull stream address** |
|---|---|
|Original (Origin) |`https://pull.example.com/live/123456.flv` |
|Ultra high definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |
|High definition (HD) |`https://pull.example.com/live/123456_hd.flv` |
|Standard definition (SD) |`https://pull.example.com/live/123456_sd.flv` |
|Low definition (LD) |`https://pull.example.com/live/123456_ld.flv` |


<span id="hAFDjC5wI"></span>
### Procedure


1. Configure multi\-resolution pull stream addresses and start playback. The sample code is as follows.

   ```Java
   // Configure pull stream addresses for multiple quality levels.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // Replace with the actual pull stream address for the original quality level.
   playStreamOrigin.format = VeLivePlayerFormatFLV;
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // Original quality level.
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // Replace with the actual pull stream address for the UHD quality level.
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // UHD quality level.
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // Replace with the actual pull stream address for the HD quality level.
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // HD quality level.
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv"; // Replace with the actual pull stream address for the SD quality level.
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // SD quality level.
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv"; // Replace with the actual pull stream address for the LD quality level.
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // LD quality level.
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add the pull stream addresses.
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
   
   // Pass in the pull streaming configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

2. Call [switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) to change the resolution.

   ```Java
   mLivePlayer.switchResolution(new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD)); // Switch to the UHD quality level.
   ```
   

3. When the switch is successful, the [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) callback function will be triggered.

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
     // Triggered when the resolution switch is complete.
   }
   ```
   


 &nbsp;

<span id="abr-stream-pulling"></span>
## ABR stream pulling

Adaptive bitrate (ABR) stream pulling helps maintain smooth playback by switching to a more suitable quality level when network conditions change.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">ABR stream pulling supports <strong>RTM\-ABR streams</strong> and <strong>FLV streams</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Only premium and trial licenses support ABR stream pulling.</div>


* <div data-tips="true" data-tips-type="tip">ABR stream pulling supports the stream fallback strategy. For RTM\-ABR streams, you can use the RTM\-ABR pull stream address as an RTM stream in the fallback strategy. For FLV streams, assign the same priority to all quality levels in one ABR stream group and configure lower\-priority fallback streams. If playback of the higher\-priority ABR stream group fails, the SDK automatically tries the fallback group. For more information, see <a href="https://docs.byteplus.com/en/docs/24/7567#stream-fallback-strategy-and-primary-backup-stream-switching">Stream fallback strategy and primary\-backup stream switching</a>.</div>



Currently, the Player SDK for Android supports the following ABR modes:


* **RTM\-ABR streams**: A server\-side ABR capability for RTM playback. The player uses **only one** RTM\-ABR pull stream address, and the server automatically selects and switches quality levels based on the viewer's network conditions, which helps reduce stuttering in weak network environments while preserving RTM's low\-latency playback experience.

* **FLV streams**: A client\-side ABR capability. You provide multiple FLV pull stream addresses and bitrate information, and the SDK switches between them based on network conditions.


 &nbsp;

<span id="rtm-abr-streams"></span>
### RTM\-ABR streams

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Only versions 1.51.100.8 and later support RTM\-ABR streams.</div>


 &nbsp;

<span id="prerequisites-6"></span>
#### Prerequisites


* Configure multiple ABR substreams and select **RTM\-ABR** as the **Protocol Type** when you add an ABR configuration. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

* Get the RTM\-ABR pull stream addresses in one of the following ways.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) and select the startup quality level (suffix) to get the **RTM address** on the **Adaptive bitrate** tab. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate RTM\-ABR pull stream addresses. Different suffixes correspond to different startup quality levels. Use one of these addresses to start playback. Make sure the value of `Protocol` is `udp`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not manually append <code>rtmabr=true</code> to a regular RTM pull stream address. RTM\-ABR takes effect only after the RTM\-ABR configuration is completed and the generated RTM\-ABR address is used.   </div>
   

 &nbsp;

<span id="procedure-6"></span>
#### Procedure

Set the **RTM\-ABR** pull stream address and start playback.

```Java
mLivePlayer.setPlayUrl("https://pull.example.com/live/test_uhd.sdp?rtmabr=true"); // Replace with your actual RTM-ABR pull stream address.

// Start playback.
mLivePlayer.play();
```


 &nbsp;

<span id="flv-streams"></span>
### FLV streams

 &nbsp;

<span id="prerequisites-7"></span>
#### Prerequisites

Get the pull stream addresses for the source stream and the transcoded streams at each quality level. If you use BytePlus MediaLive, log in to the console and complete [transcoding configuration](https://console.byteplus.com/live/main/application/transcode) before obtaining the pull stream addresses. You can obtain addresses in either of the following ways:


* **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

* **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.


This procedure uses the following pull stream addresses as examples.

&nbsp;


|Quality level |Pull stream address |Bitrate (kbps) |
|---|---|---|
|Original (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
|Ultra high definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|High definition (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
|Standard definition (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
|Low definition (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">When configuring multiple quality\-level pull stream addresses for ABR, the encoding bitrate of each quality level in the SDK must be the same as the encoding bitrate configured in <a href="https://console.byteplus.com/live/main/application/transcode">transcoding configuration</a>. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding">Managing transcoding configuration</a>.</div>


 &nbsp;

<span id="hE0Lm2FGy"></span>
#### Procedure


1. Configure multi\-quality pull stream addresses and start playback. The sample code is as follows.

   ```Java
   // Configure pull stream addresses for multiple quality levels.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // Replace with the actual pull stream address for the original quality level.
   playStreamOrigin.format = VeLivePlayerFormatFLV;
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // Original quality level.
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain;
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // Replace with the actual pull stream address for the UHD quality level.
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // UHD quality level.
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // Replace with the actual pull stream address for the HD quality level.
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // HD quality level.
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";  // Replace with the actual pull stream address for the SD quality level.
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // SD quality level.
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";  // Replace with the actual pull stream address for the LD quality level.
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // LD quality level.
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   playStreamLD.bitrate = 500;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add multi-quality streams.
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // Configure the default startup quality level.
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
   
   // Enable ABR.
   streamData.enableABR = true;
   
   // Configure the playback source.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

2. When the ABR quality level switches automatically, the [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) callback of [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) is triggered. The sample code is as follows.

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
      // Quality level switch callback.
   }
   ```
   


 &nbsp;

<span id="smooth-quality-level-switching"></span>
## Smooth quality level switching

The smooth quality level switching feature ensures a seamless audio and video transition when viewers manually switch between different quality levels, such as ultra high definition, high definition, and standard definition. This **prevents black screens or stuttering** and improves the viewing experience.

To use this feature, configure the player with a list of streams from the same source at multiple quality levels and enable smooth quality level switching. After configuration, when viewers manually switch quality levels, the player smoothly transitions between streams of different bitrates to ensure continuous and stable live audio and video playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Smooth quality level switching supports the stream fallback strategy. You can assign the same priority to one group of smooth quality level switching streams and configure lower\-priority fallback streams. If playback of the higher\-priority stream group fails, the SDK automatically tries the fallback group. For more information, see <a href="https://docs.byteplus.com/en/docs/24/7567#stream-fallback-strategy-and-primary-backup-stream-switching">Stream fallback strategy and primary\-backup stream switching</a>.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">The smooth quality level switching feature is currently available only for FLV streams.</div>


* <div data-tips="true" data-tips-type="warning">Ensure that you have integrated the Player SDK version 1.50.100 or later.</div>



 &nbsp;

<span id="prerequisites-8"></span>
### Prerequisites

Prepare pull stream addresses for different quality levels of the same source stream.

If you use a push stream address from BytePlus MediaLive for streaming, make sure that you have completed the following:


* **Add domain names**: Add domain names for stream pushing and pulling under the same domain name space. For more information, see [Adding domain names](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

* **Configure transcoding**: Add transcoding configurations for different quality levels under the domain name space. For more information, see [Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).

* **Get pull stream addresses**: Get the pull stream addresses for the source stream and each transcoded stream.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

      * **Address type**: Select **Pull stream address**.

      * **Domain name**: Select the domain name for stream pulling under the domain name space used for the transcoding configuration.

      * **AppName** and **StreamName**: Enter the `AppName` and `StreamName` that match the push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, the `AppName` is `live` and the `StreamName` is `test`.

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.


**Example**

The following table lists sample FLV pull stream addresses and bitrates for different quality levels.

&nbsp;


|Quality level |FLV pull stream address |Bitrate (kbps) |
|---|---|---|
|Original (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
|Ultra high definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|High definition (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
|Standard definition (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
|Low definition (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |


 &nbsp;

<span id="procedure-8"></span>
### Procedure


1. Configure the streams for each quality level and set [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) to `true` to enable smooth quality level switching.

   ```Java
   // Configure streams for each quality level.
   // Original quality level.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // Replace with the actual pull stream address for the original quality level.
   playStreamOrigin.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // Quality level identifier.
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamOrigin.bitrate = 2500; // Bitrate in kbps.
   
   // UHD quality level.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // Replace with the actual pull stream address for the UHD quality level.
   playStreamUHD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // Quality level identifier.
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamUHD.bitrate = 2500; // Bitrate in kbps.
   
   // HD quality level.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // Replace with the actual pull stream address for the HD quality level.
   playStreamHD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // Quality level identifier.
   playStreamHD.streamType = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamHD.bitrate = 1000; // Bitrate in kbps.
   
   // SD quality level.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv"; // Replace with the actual pull stream address for the SD quality level.
   playStreamSD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // Quality level identifier.
   playStreamSD.streamType = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamSD.bitrate = 800; // Bitrate in kbps.
   
   // LD quality level.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv"; // Replace with the actual pull stream address for the LD quality level.
   playStreamLD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // Quality level identifier.
   playStreamLD.streamType = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamLD.bitrate = 500; // Bitrate in kbps.
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add streams for each quality level.
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // Configure the default startup quality level.
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD);
   
   // Enable smooth quality level switching.
   streamData.enableSmoothSwitchResolution = true;
   
   // Configure the playback source.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

2. During live streaming, when viewers manually switch quality levels, you can call [switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) to switch the quality level smoothly. The sample code is as follows.

   ```Java
   mLivePlayer.switchResolution(new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD)); // Switch to the UHD quality level.
   ```
   

3. Add the [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) callback to listen for quality level switch results. When the quality level changes, the SDK can trigger this callback and return information such as the switched quality level and the reason for the switch.

   ```Java
   @Override
   public void onResolutionSwitch(
       VeLivePlayer player,
       VeLivePlayerResolution resolution,
       VeLivePlayerError error,
       VeLivePlayerResolutionSwitchReason reason
   ) {
   }
   ```
   


 &nbsp;

<span id="snapshot-capturing"></span>
## Snapshot capturing

This feature enables you to capture the current video frame and generate an image.


1. Call [snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-snapshot) to take a snapshot. This feature takes effect during playback only.

   ```Java
   int result = mLivePlayer.snapshot();
   ```
   

2. After a snapshot is taken, the [onSnapshotComplete](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) callback function will be triggered with the image data.

   ```Java
   public void onSnapshotComplete(VeLivePlayer player, Bitmap bitmap) {
     // The callback function returns the image data through Bitmap.
   }
   ```
   


 &nbsp;

<span id="sei"></span>
## SEI

Supplemental Enhancement Information (SEI) is additional data embedded within a live stream. You can use SEI to transmit custom data or metadata.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support SEI.</div>



* String SEI messages

   1. Before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play), enable the [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablesei) property of the player. After this property is enabled, the player receives string SEI messages. The sample code is as follows.

      ```Java
      // Create a VeLivePlayerConfiguration instance.
      VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
      
      // Enable receiving string SEI messages.
      config.enableSei = true;
      
      // Configure the initial settings of the player.
      mLivePlayer.setConfig(config);
      ```
      

   2. When the player receives a string SEI message, the [onReceiveSeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) callback is triggered. The sample code is as follows.

      ```Java
      public void onReceiveSeiMessage(VeLivePlayer player, String message) {
         // String SEI message callback.
      }
      ```
      

* Binary SEI messages

   1. Before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play), enable the [enableBinarySei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablebinarysei) property of the player. After this property is enabled, the player receives binary SEI messages and no longer triggers the string SEI message callback. The sample code is as follows.

      ```Java
      // Create a VeLivePlayerConfiguration instance.
      VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
      
      // Enable receiving binary SEI messages.
      config.enableBinarySei = true;
      
      // Configure the initial settings of the player.
      mLivePlayer.setConfig(config);
      ```
      

   2. When the player receives a binary SEI message, the [onReceiveBinarySeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) callback is triggered. The sample code is as follows.

      ```Java
      public void onReceiveBinarySeiMessage(VeLivePlayer player, byte[] message) {
         // Binary SEI message callback.
      }
      ```
      


 &nbsp;

<span id="subscribing-to-video-data"></span>
## Subscribing to video data

By subscribing to decoded video data, you can obtain video frame data for custom processing and rendering. The player supports multiple video frame callback formats and provides the corresponding parameters and format options.

 &nbsp;

<span id="prerequisites-9"></span>
### Prerequisites

The following table describes the enumerations and meanings of video frame pixel formats and video data encapsulation formats.

&nbsp;


|Format Type |Enumeration |Description |
|---|---|---|
|Video frame pixel format |VeLivePlayerPixelFormatRGBA32 |RGBA32 |
|Video frame pixel format |VeLivePlayerPixelFormatTexture |2D texture |
|Video data encapsulation format |VeLivePlayerVideoBufferTypeByteBuffer |ByteBuffer |
|Video data encapsulation format |VeLivePlayerVideoBufferTypeByteArray |ByteArray |
|Video data encapsulation format |VeLivePlayerVideoBufferTypeTexture |Texture |


Before subscribing to video data, select a format combination based on your needs. The combination must follow the mapping between [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerpixelformat) and [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayervideobuffertype) shown in the following table.

&nbsp;


|Pixel Format/Encapsulation Format |VeLivePlayerPixelFormatRGBA32 |VeLivePlayerPixelFormatTexture |
|---|---|---|
|**VeLivePlayerVideoBufferTypeByteBuffer** |Supported |Not supported |
|**VeLivePlayerVideoBufferTypeByteArray** |Supported |Not supported |
|**VeLivePlayerVideoBufferTypeTexture** |Not supported |Supported (optimal performance) |


 &nbsp;

<span id="procedure-9"></span>
### Procedure


1. Call the player's [enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) API to enable or disable video frame data subscription. The API parameters are described in the following table.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable video frame callbacks. |
   |pixelFormat |VeLivePlayerPixelFormat |The video frame pixel format. |
   |bufferType |VeLivePlayerVideoBufferType |The video data encapsulation format. |
   

   The sample code is as follows.

   ```Java
   //
   mLivePlayer.enableVideoFrameObserver(true, VeLivePlayerPixelFormatRGBA32, VeLivePlayerVideoBufferTypeByteBuffer);
   ```
   

2. The SDK returns the decoded video frame data through the [onRenderVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) callback of [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver). The sample code is as follows.

   ```Java
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
      // Video frame data callback.
   }
   ```
   

   The [VeLivePlayerVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame) parameter is described in the following table.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |bufferType |VeLivePlayerVideoBufferType |The video frame data encapsulation format. |
   |pixelFormat |VeLivePlayerPixelFormat |The video frame pixel format. |
   |width |int |The video frame width, in px. |
   |height |int |The video frame height, in px. |
   |pts |long |The video frame rendering timestamp, in ms. |
   |texture |VeLivePlayerVideoTexture |The video data when `bufferType` is `VeLivePlayerVideoBufferTypeTexture`. This carries texture data used for OpenGL rendering. |
   |buffer |ByteBuffer |The video data when `bufferType` is `VeLivePlayerVideoBufferTypeByteBuffer`. This carries the direct buffer used at the JNI layer. |
   |data |byte[] |The video data when `bufferType` is `VeLivePlayerVideoBufferTypeByteArray`. This carries byte array data used at the Java layer. |
   


 &nbsp;

<span id="subscribing-to-audio-data"></span>
## Subscribing to audio data

By subscribing to decoded audio data, you can perform custom audio processing and rendering. The Player SDK supports subscribing to audio data in PCM Float32 sample format and ByteArray encapsulation format.

&nbsp;


|VeLivePlayerAudioBufferType |Audio Data Encapsulation Format |
|---|---|
|[VeLivePlayerAudioBufferTypeByteArray](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioBufferType) |ByteArray |


 &nbsp;

<span id="procedure-10"></span>
### Procedure


1. Call the player's [enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) API to enable or disable audio frame data subscription. The API parameters are described in the following table.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable audio frame callbacks. |
   |enableRendering |boolean |Whether to enable player rendering. Set this parameter to `false` if the player does not need to render audio internally. |
   

   The sample code is as follows.

   ```Java
   // Subscribe to audio frame data and enable internal audio rendering of the player.
   mLivePlayer.enableAudioFrameObserver(true, true);
   ```
   

2. The SDK returns the decoded audio frame data through the [onRenderAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) callback of [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver). The sample code is as follows.

   ```Java
   void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
      // Audio frame data callback.
   }
   ```
   

   The [VeLivePlayerAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame) parameter is described in the following table.

&nbsp;

   
   |Parameter |Data type |Description |
   |---|---|---|
   |bufferType |VeLivePlayerAudioBufferType |The audio frame data encapsulation format. |
   |sampleRate |int |The audio sample rate, in Hz. |
   |channels |int |The number of channels. |
   |bitDepth |int |The audio bit depth. |
   |pts |long |The audio rendering timestamp, in ms. |
   |buffer |byte[] |PCM audio data. |
   |samples |int |The number of audio samples. |
   


 &nbsp;

<span id="super-resolution"></span>
## Super\-resolution

Super\-resolution (SR) is a technology that reconstructs high\-resolution images from low\-resolution ones. Real\-time SR uses algorithms to reconstruct low\-resolution frames into high\-resolution ones in real time. This generates high\-resolution frames, which are then displayed on the screen. SR enhances video details and contrast, improving video clarity and the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support SR.</div>



1. Call the player's [setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) method to enable or disable SR.

   ```Java
   mLivePlayer.setEnableSuperResolution(true);
   ```
   

   
   |Name |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable SR. The default value is `false`.<br><br><br>* `true`: Enables SR.<br><br>* `false`: Disables SR. |
   

2. If enabling SR fails, the player notifies you through the [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) callback of [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver). The method signature is as follows.

   ```Java
   void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error);
   ```
   

   Common reasons for failure to enable SR are as follows.

   * The actual stream resolution is not within the supported range for SR.

   * The actual stream frame rate is not within the supported range for SR.

   * The current device model does not support SR.


 &nbsp;

<span id="customizing-http-request-headers"></span>
## Customizing HTTP request headers

Set custom request headers for the player's HTTP requests. This is commonly used to transmit additional information such as authentication tokens, cookies, and business tracking identifiers.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only versions 1.50.200.3 and later support customizing HTTP request headers.</div>


 &nbsp;

<span id="procedure-12"></span>
### Procedure

Before starting playback, you can set custom HTTP request headers through the player's advanced API [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty). When calling `setProperty`, you need to pass a `key-value` configuration.

**Key**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|VeLivePlayerKeySetParamsHttpHeaders |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |The property key used to configure custom HTTP request headers. |


**Value**

The value is a `Map<String, String>` object containing `key-value` pairs to set custom HTTP request headers.


* `Key`: `String` type. The request header name.

* `Value`: `String` type. The request header value.


The sample code is as follows.


* To set an HTTP request header

   ```Java
   Map<String, String> headerMap = new HashMap<>();
   headerMap.put("key", "value"); // Replace with the actual header name and value.
   mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders, headerMap);
   ```
   

* To set multiple HTTP request headers

   ```Java
   Map<String, String> headerMap = new HashMap<>();
   headerMap.put("key1", "value1"); // Replace with the actual header name and value.
   headerMap.put("key2", "value2"); // Replace with the actual header name and value.
   headerMap.put("key3", "value3"); // Replace with the actual header name and value.
   mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders, headerMap);
   ```
   


 &nbsp;

<span id="h.265-hardware-decoding-and-software-decoding"></span>
## H.265 hardware decoding and software decoding

The SDK with a premium or trial license enables H.265 hardware decoding and software decoding by default. When playing an H.265\-encoded video stream, the SDK first attempts to use H.265 hardware decoding. If H.265 hardware decoding fails, the SDK automatically switches to H.265 software decoding.

Before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play), enable or disable hardware decoding through the player's initial configuration. The sample code is as follows.

```Java
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
config.enableHardwareDecode = true;
mLivePlayer.setConfig(config);
```



* `true`: Enables hardware decoding.

* `false`: Disables hardware decoding and uses software decoding only.


You can listen for the [onStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) callback and use the [isHardwareDecode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-ishardwaredecode) property of [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics) to determine whether hardware decoding is used for the current stream.

 &nbsp;

<span id="h.266-software-decoding"></span>
## H.266 software decoding

The SDK with a premium or trial license enables H.266 software decoding by default, with no additional configuration required.

 &nbsp;

<span id="video-sharpening"></span>
## Video sharpening

Video sharpening enhances the video locally on the device to improve the clarity of edges and texture details. During playback, the SDK can enhance edges and texture details in real time, making the video appear clearer and improving the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support video sharpening.</div>


 &nbsp;

<span id="procedure-13"></span>
### Procedure


1. Call the player's [setEnableSharpen](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) method to enable or disable video sharpening.

   ```Java
   mLivePlayer.setEnableSharpen(true);
   ```
   

   
   |Name |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable video sharpening. The default value is `false`.<br><br><br>* `true`: Enables video sharpening.<br><br>* `false`: Disables video sharpening. |
   

2. If enabling video sharpening fails, the player notifies you through the [onStreamFailedOpenSharpen](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) callback of [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver). The method signature is as follows.

   ```Java
   default void onStreamFailedOpenSharpen(VeLivePlayer player, VeLivePlayerError error)
   ```
   

   Common reasons for failure to enable video sharpening are as follows.

   * The actual stream resolution is not within the supported range for video sharpening.

   * The actual stream frame rate is not within the supported range for video sharpening.

   * The current device model does not support video sharpening.

   * The current license does not support video sharpening.


 &nbsp;

<span id="picture-in-picture"></span>
## Picture in Picture

Picture in Picture (PiP) shrinks the player window into a small floating window in one corner of the screen, allowing viewers to continue watching the live stream while browsing other content or using other apps. The feature helps improve the viewing experience.

 &nbsp;

<span id="prerequisites-10"></span>
### Prerequisites

Android 6.0 or later.

 &nbsp;

<span id="procedure-14"></span>
### Procedure


1. Copy the [vepicutureinpicture](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/tree/main/Android/VeLiveQuickStartDemo/vepicutureinpicture) module code to the root directory of your main project.

2. Modify the SDK version in `vepicutureinpicture/live/build.gradle`. Replace `x.x.x.x` with the SDK version that you have integrated. For the version number, see [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes).

   ```Plain
   implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'
   ```
   

3. Import the `vepicutureinpicture` module into your project. You can refer to [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo) for configuration.

   ```Java
   include ':vepicutureinpicture:live'
   include ':vepicutureinpicture:base'
   
   api project(path: ':vepicutureinpicture:live')
   ```
   

4. Initialize the PiP feature.

   ```Java
   // mLivePlayer is the player instance.
   VeLivePictureInPicturePlayerManager mPipManager = new VeLivePictureInPicturePlayerManager(mLivePlayer, context);
   ```
   

5. Set the PiP observer to handle the logic for resuming normal playback from PiP mode. In the following sample code, replace `XXXActivity` with the Activity in your project that hosts the live playback page.

   ```Java
   mPipManager.setObserver(new VeLivePictureInPicturePlayerManager.VeLivePictureInPicturePlayerManagerObserver() {
       @Override
       public void onClickResumeAction() {
           // Resume normal playback from PiP mode.
           try {
               Class<?> cls = Class.forName(XXXActivity.class.getName());
               Intent intent = new Intent(getBaseContext(), cls);
               intent.setFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP | Intent.FLAG_ACTIVITY_NEW_TASK);
               startActivity(intent);
           } catch (ClassNotFoundException e) {
   
           }
       }
   });
   ```
   

6. Check whether the current app has the system overlay permission.

   ```Java
   boolean isPermission = mPipManager.isPermissionGranted();
   ```
   

   If the system overlay permission has not been granted, refer to the following sample code to request the permission and guide users to the system settings page to enable the permission.

   ```Java
   if (!isPermission) {
       mPipManager.requestPermission(new VePictureInPictureManager.VePictureInPicturePermissionCallback() {
           @Override
           public void onGranted(boolean granted) {
               // Callback for the permission request result. true indicates that the system overlay permission has been granted. false indicates that the system overlay permission has not been granted.
           }
   
           @Override
           public void onRequestPermission(Context context, VePictureInPictureManager.VePictureInPicturePermissionResult result) {
               // Guide users to the system settings page to enable the system overlay permission.
               new AlertDialog.Builder(context)
                       .setMessage("The system overlay permission is not enabled. Go to Settings and enable the [Display over other apps] permission.")
                       .setPositiveButton("Enable", (dialog, which) -> {
                           // The user agrees to enable the system overlay permission.
                           result.accept();
                       })
                       .setNegativeButton("Cancel", (dialog, which) -> {
                           // The user does not agree to enable the system overlay permission.
                           result.cancel();
                       })
                       .setCancelable(false)
                       .show();
           }
       });
   }
   ```
   

7. During live playback on the page, video is rendered on a `Surface` or `SurfaceHolder`. After integrating the PiP feature, pass the same `Surface` or `SurfaceHolder` to `mPipManager`, so that the current live video can continue to be displayed after entering PiP mode.

   
   <Tabs>
   <Tab zoneid="RX8p8c7Gu5" title="Set Surface">
   <TabTitle>Set Surface</TabTitle>
   
   ```Java
   // Set Surface.
   mLivePlayer.setSurface(surface);
   mPipManager.setSurface(surface);
   ```
   
   
   
   </Tab>
   <Tab zoneid="T0644mCkGN" title="Set SurfaceHolder">
   <TabTitle>Set SurfaceHolder</TabTitle>
   
   ```Java
   // Set SurfaceHolder.
   mLivePlayer.setSurfaceHolder(surfaceHolder);
   mPipManager.setSurfaceHolder(surfaceHolder);
   ```
   
   
   
   </Tab>
   </Tabs>
   

8. Pass the current video width and height returned by the player callback to `mPipManager`. This allows the PiP window to display the video using the video's actual aspect ratio.

   ```Java
   mLivePlayer.setVeLivePlayerObserver(new VeLivePlayerObserver() {
       @Override
       public void onVideoSizeChanged(VeLivePlayer player, int width, int height) {
           mPipManager.setVideoSize(width, height);
       }
   });
   ```
   

9. If you need to customize the PiP window size, refer to the following sample code for configuration.

   
   <Tabs>
   <Tab zoneid="yp9nNWEulD" title="Customize by width">
   <TabTitle>Customize by width</TabTitle>
   
   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // Set the maximum width of the PiP window to 720 px. The minimum width defaults to 50% of the maximum width. The height is automatically calculated based on the video's aspect ratio.
   configuration.maxWidth = 720;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```
   
   
   You can also set the PiP window size based on a proportion of the device screen width.
   
   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // Set the maximum width of the PiP window to 50% of the device screen width. The minimum width defaults to 50% of the maximum width. The height is automatically calculated based on the video's aspect ratio.
   configuration.maxWidthRatio = 0.5;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```
   
   
   
   </Tab>
   <Tab zoneid="EVulylGCIe" title="Customize by height">
   <TabTitle>Customize by height</TabTitle>
   
   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // Set the maximum height of the PiP window to 720 px. The minimum height defaults to 50% of the maximum height. The width is automatically calculated based on the video's aspect ratio.
   configuration.maxHeight = 720;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```
   
   
   You can also set the PiP window size based on a proportion of the device screen height.
   
   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // Set the maximum height of the PiP window to 50% of the device screen height. The minimum height defaults to 50% of the maximum height. The width is automatically calculated based on the video's aspect ratio.
   configuration.maxHeightRatio = 0.5;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```
   
   
   
   </Tab>
   </Tabs>
   

10. After live playback starts and the system overlay permission has been granted, you can start PiP mode.


```Java
mPipManager.startPictureInPicture();
```


If PiP mode is currently active, you can stop PiP mode.

```Java
mPipManager.stopPictureInPicture();
```



11. To determine whether the PiP window is currently displayed, call the following method.


```Java
boolean showing = mPipManager.isPictureInPictureShowing();
```



12. When the PiP feature is no longer needed, destroy `mPipManager`.


```Java
mPipManager.destroy();
```


 &nbsp;

<span id="advanced-api-configuration"></span>
## Advanced API configuration

 &nbsp;

<span id="removing-query-parameters-automatically-appended-by-the-sdk"></span>
### Removing query parameters automatically appended by the SDK

The Player SDK might append query parameters, such as `session_id`, to a pull stream address. These parameters identify a pull stream session and help locate the same session in both client and CDN logs when troubleshooting playback issues. To prevent the SDK from including automatically appended query parameters in the actual request URL, enable this feature. After this feature is enabled, SDK\-appended query parameters are removed from the actual request URL, while query parameters already present in the original pull stream address are retained.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only versions 1.52.100.5 and later support removing query parameters automatically appended by the SDK.</div>


<span id="procedure-15"></span>
#### Procedure

Before starting playback, you can use the player's advanced [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) API to configure whether to remove query parameters automatically appended by the SDK. When calling `setProperty`, you need to pass a `key-value` configuration.

**Key**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|VeLivePlayerKeySetParamsRemoveQueryParams |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |The property key for removing query parameters automatically appended by the SDK. |


**Value**

`Value` is a Boolean value that indicates whether to remove query parameters automatically appended by the SDK. The default value is `false`.


* `true`: Removes query parameters automatically appended by the SDK.

* `false`: Retains query parameters automatically appended by the SDK.


The sample code is as follows.

```Java
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsRemoveQueryParams, true);
```


**Effect example**

For example, the pull stream address is:

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```


When the SDK initiates the playback request, it automatically appends `session_id`:

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901&session_id=xxx
```


After this feature is enabled, the request URL no longer contains `session_id` but retains the `auth_key` authentication parameter from the original pull stream address:

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```
