---
title: "Player SDK for iOS: Advanced features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3"
---

To enhance the viewing experience in your iOS app, this topic details how to implement advanced features of the Player SDK for iOS. You can implement complex features as needed, according to actual business requirements.

 &nbsp;

<span id="prerequisites"></span>
## Prerequisites


* You have implemented the basic features of the Player SDK by following the instructions provided in [Player SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3).

* To use the following features, ensure you use a premium or trial license.

   * [Playing RTM streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d2fff36e)

   * [QUIC stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#78c4f3ae)

   * [Playing low-latency FLV streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#3d66c491)

   * [Primary-backup stream switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368)

   * [ABR stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#aceb1766)

   * [Super-resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#4ea2c546)

   * [H.265 hardware decoding and software decoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#953988b6)

   * [Video sharpening](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e3976737)

   * [Playing a DRM-encrypted stream](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e1834266)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7">Upgrading a trial license to a basic or premium license</a>.   </div>
   

 &nbsp;

<span id="notes"></span>
## Notes

Because the Player SDK uses various iOS audio and video APIs that may not work properly on simulators, we recommend that you use a physical device for testing.

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


* [onInfo:info:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info): Triggered when a stream fails to play but another available stream exists. You can use this callback to get detailed error information for debugging.

* [onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo): Triggered when the player switches the stream format (for example, from RTM to FLV).

* [onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error): Triggered when all streams in the primary stream list fail to play and the player successfully switches to the backup stream list.

* [onError:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error): Triggered when all streams in the primary and backup stream lists fail to play, and playback finally ends.


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

You can customize the fallback strategy by configuring the [priority](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-priority) and [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount) of `VeLivePlayerStream`.


* `priority`: The priority of the stream. The value must be `0` (default value) or a positive integer. **A larger value indicates a higher priority**. The player attempts to play higher\-priority streams first.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The priorities of the primary and backup stream lists are calculated independently and do not affect each other.   </div>
   

* `retryMaxCount`: The maximum number of playback attempts for the stream, including the initial attempt. For example, if the value is `3`, the player will retry a maximum of 2 more times after the first playback fails. Valid values:

   * `-1` (default value): Use the value of [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) in `VeLivePlayerConfiguration`.

   * `0`: Do not attempt to play this stream.

   * `>0`: The maximum number of playback attempts.



<Tabs>
<Tab zoneid="JlmMM6SV5l" title="Stream fallback strategy">
<TabTitle>Stream fallback strategy</TabTitle>

The following code sample demonstrates a basic stream fallback scenario, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4), with a maximum of 2 attempts.

3. If that also fails, playback ends.


```objectivec
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// Add an RTM primary stream (highest priority).
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// Configure the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```



</Tab>
<Tab zoneid="rNKmSQ5OVx" title="Stream fallback strategy + primary-backup stream switching">
<TabTitle>Stream fallback strategy + primary-backup stream switching</TabTitle>

The following code sample demonstrates a scenario that combines the stream fallback strategy with primary\-backup stream switching, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5) from the primary stream list, with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4) from the primary stream list, with a maximum of 2 attempts.

3. If that still fails, the player switches to the backup stream list and tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

4. If that fails, the player falls back to the FLV stream (priority 4) from the backup stream list, with a maximum of 3 attempts.

5. If all of these attempts fail, playback ends.


```objectivec
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
// Configure the primary stream list.
NSMutableArray *mainStreams = [NSMutableArray new];

// Add an RTM primary stream (highest priority).
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// Configure the backup stream list.
NSMutableArray *backupStreams = [NSMutableArray new];
// Add an RTM backup stream.
VeLivePlayerStream *rtmBackupStream = [[VeLivePlayerStream alloc] init];
rtmBackupStream.url = @"https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmBackupStream.format = VeLivePlayerFormatRTM;
rtmBackupStream.type = VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // Highest priority in the backup stream list.
[backupStreams addObject:rtmBackupStream];

// Add an FLV backup stream as a fallback stream.
VeLivePlayerStream *flvBackupStream = [[VeLivePlayerStream alloc] init];
flvBackupStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvBackupStream.format = VeLivePlayerFormatFLV;
flvBackupStream.type = VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
[backupStreams addObject:flvBackupStream];
streamData.backupStream = backupStreams;

// Enable primary-backup stream switching.
streamData.enableMainBackupSwitch = YES;

// Configure the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```



</Tab>
<Tab zoneid="il2TVXWUD7" title="Multi-quality stream fallback strategy">
<TabTitle>Multi-quality stream fallback strategy</TabTitle>

The stream fallback strategy supports configuring fallback streams for multi\-quality stream configurations used by [resolution switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#660adfe3), [ABR stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae) (FLV streams only), and [smooth quality level switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#37bcd52d). During configuration, set the same `priority` value for streams in the same multi\-quality stream group. The player first selects stream groups from the highest `priority` to the lowest. If playback of the high\-priority multi\-quality streams fails, the player falls back to lower\-priority streams.

In the following example, the player first plays the ABR multi\-quality streams whose `priority` is `5`. If playback of the ABR multi\-quality streams fails, the player falls back to a regular FLV stream whose `priority` is `4`.

```objectivec
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// Add the original quality level of the ABR multi-quality streams. The priority is 5.
VeLivePlayerStream *flvOriginStream = [[VeLivePlayerStream alloc] init];
flvOriginStream.url = @"https://xxx_origin.flv"; // Replace with the actual FLV pull stream address for the original quality level.
flvOriginStream.format = VeLivePlayerFormatFLV;
flvOriginStream.type = VeLivePlayerStreamTypeMain;
flvOriginStream.protocol = VeLivePlayerProtocolTLS;
flvOriginStream.resolution = VeLivePlayerResolutionOrigin; // Quality level identifier.
flvOriginStream.bitrate = 2000;
flvOriginStream.retryMaxCount = 3;
flvOriginStream.priority = 5;
[mainStreams addObject:flvOriginStream];

// Add the UHD quality level of the ABR multi-quality streams. The priority is 5.
VeLivePlayerStream *flvUHDStream = [[VeLivePlayerStream alloc] init];
flvUHDStream.url = @"https://xxx_uhd.flv"; // Replace with the actual FLV pull stream address for the UHD quality level.
flvUHDStream.format = VeLivePlayerFormatFLV;
flvUHDStream.type = VeLivePlayerStreamTypeMain;
flvUHDStream.protocol = VeLivePlayerProtocolTLS;
flvUHDStream.resolution = VeLivePlayerResolutionUHD; // Quality level identifier.
flvUHDStream.bitrate = 1800;
flvUHDStream.retryMaxCount = 3;
flvUHDStream.priority = 5;
[mainStreams addObject:flvUHDStream];

// Add the HD quality level of the ABR multi-quality streams. The priority is 5.
VeLivePlayerStream *flvHDStream = [[VeLivePlayerStream alloc] init];
flvHDStream.url = @"https://xxx_hd.flv"; // Replace with the actual FLV pull stream address for the HD quality level.
flvHDStream.format = VeLivePlayerFormatFLV;
flvHDStream.type = VeLivePlayerStreamTypeMain;
flvHDStream.protocol = VeLivePlayerProtocolTLS;
flvHDStream.resolution = VeLivePlayerResolutionHD; // Quality level identifier.
flvHDStream.bitrate = 1500;
flvHDStream.retryMaxCount = 3;
flvHDStream.priority = 5;
[mainStreams addObject:flvHDStream];

// Add a regular FLV stream as a fallback stream. The priority is 4.
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// Configure the default startup quality level.
streamData.defaultResolution = VeLivePlayerResolutionOrigin;

// Enable ABR.
streamData.enableABR = YES;

// Configure the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```



</Tab>
</Tabs>


 &nbsp;

<span id="step-2:-add-callbacks"></span>
#### Step 2: Add callbacks

Add the following callbacks as needed to listen for events during the fallback process.


* Listen for stream format switching, for example, from RTM to FLV.

   ```objectivec
   - (void)onStreamFormatSwitch:(TVLManager *_Nonnull)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(NSDictionary *)extraInfo;
   ```
   

* Listen for recoverable issues encountered during playback. This callback is triggered when a stream fails to play but the SDK is about to perform a recovery action, such as switching to a fallback stream. This indicates that playback is still continuing, and you do not need to interrupt the playback process. You can use the returned error information to understand the specific reason for the stream playback failure during debugging.

   ```objectivec
   - (void)onInfo:(TVLManager *_Nonnull)player info:(VeLivePlayerError *_Nonnull)info;
   ```
   

* Listen for switching from the primary stream to the backup stream.

   ```objectivec
   - (void)onMainBackupSwitch:(TVLManager *_Nonnull)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error;
   ```
   

* Listen for when playback finally ends, meaning all streams have failed to play.

   ```objectivec
   - (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
   ```
   


 &nbsp;

<span id="playing-rtm-streams"></span>
## Playing RTM streams

Playing RTM streams can reduce live streaming latency to 1\-2 seconds, providing viewers with a high\-quality live streaming experience.

However, the ultra\-low latency feature of RTM also places higher demands on the network environment. Under unstable network conditions, playback delays, stuttering, or failures may occur. If you want to automatically try pull stream addresses of other protocols, such as FLV, when an RTM pull stream address is unavailable, use this feature together with the stream fallback strategy or primary\-backup stream switching. For more information, see [Stream fallback strategy and primary-backup stream switching](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support playing RTM streams.</div>


 &nbsp;

<span id="prerequisites-2"></span>
### Prerequisites


* Ensure that you have integrated the Player SDK version 1.50.100 or later, and added the `LivePull-RTS` dependency. For more information, see [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios).

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
<Tab zoneid="n2uNE44V3A" title="Basic scenario">
<TabTitle>Basic scenario</TabTitle>

The following code sample demonstrates a basic stream fallback scenario, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4), with a maximum of 2 attempts.

3. If that also fails, playback ends.


```objectivec
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// Add an RTM primary stream (highest priority).
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// Configure the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```



</Tab>
<Tab zoneid="k0BSNPCEfZ" title="Advanced scenario">
<TabTitle>Advanced scenario</TabTitle>

The following code sample demonstrates a scenario that combines the stream fallback strategy with primary\-backup stream switching, with the playback order as follows:


1. First, the player tries to play the RTM stream (priority 5) from the primary stream list, with a maximum of 3 attempts.

2. If that fails, the player falls back to the FLV stream (priority 4) from the primary stream list, with a maximum of 2 attempts.

3. If that still fails, the player switches to the backup stream list and tries to play the RTM stream (priority 5), with a maximum of 3 attempts.

4. If that fails, the player falls back to the FLV stream (priority 4) from the backup stream list, with a maximum of 3 attempts.

5. If all of these attempts fail, playback ends.


```objectivec
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
// Configure the primary stream list.
NSMutableArray *mainStreams = [NSMutableArray new];

// Add an RTM primary stream (highest priority).
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// Add an FLV primary stream as a fallback stream.
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// Configure the backup stream list.
NSMutableArray *backupStreams = [NSMutableArray new];
// Add an RTM backup stream.
VeLivePlayerStream *rtmBackupStream = [[VeLivePlayerStream alloc] init];
rtmBackupStream.url = @"https://xxx.sdp"; // Replace with your actual RTM pull stream address.
rtmBackupStream.format = VeLivePlayerFormatRTM;
rtmBackupStream.type = VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // Highest priority in the backup stream list.
[backupStreams addObject:rtmBackupStream];

// Add an FLV backup stream as a fallback stream.
VeLivePlayerStream *flvBackupStream = [[VeLivePlayerStream alloc] init];
flvBackupStream.url = @"https://xxx.flv"; // Replace with your actual FLV pull stream address.
flvBackupStream.format = VeLivePlayerFormatFLV;
flvBackupStream.type = VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
[backupStreams addObject:flvBackupStream];
streamData.backupStream = backupStreams;

// Enable primary-backup stream switching.
streamData.enableMainBackupSwitch = YES;

// Configure the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```



</Tab>
</Tabs>


 &nbsp;

<span id="playing-low-latency-flv-streams"></span>
## Playing low\-latency FLV streams

After low\-latency FLV streaming is enabled, FLV stream pulling can reduce live streaming latency to 2\-3 seconds.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To play low\-latency FLV streams, make sure that you have integrated SDK version 1.50.200.3\-premium or later and are using a premium or trial license.</div>


 &nbsp;

<span id="procedure-2"></span>
### Procedure

Before starting playback, you can enable low\-latency FLV streaming through the player's advanced API [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value). When calling `setProperty:value:`, you need to pass a `key-value` configuration.

**Key**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|VeLivePlayerKeySetParamsLowLatencyFlv |NSString |The property key for the low\-latency FLV streaming feature. |


**Value**

The value is an `NSDictionary` object containing `key-value` pairs to configure the low\-latency FLV streaming feature.


* `Key`: `NSString` type. The value is fixed to `EnableLowLatencyFLV`, which indicates whether to enable the low\-latency FLV streaming feature.

* `Value`: `NSNumber` type. A value of `1` enables the low\-latency FLV streaming feature, and a value of `0` disables the feature. The default value is `0`.


The sample code is as follows.

```objectivec
[self.livePlayer setProperty:VeLivePlayerKeySetParamsLowLatencyFlv value:@{@"EnableLowLatencyFLV": @1}];
```


 &nbsp;

<span id="quic-stream-pulling"></span>
## QUIC stream pulling

The Player SDK supports QUIC stream pulling. This feature should be used together with BytePlus MediaLive.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support QUIC stream pulling.</div>


 &nbsp;

<span id="prerequisites-3"></span>
### Prerequisites

Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) in the BytePlus Live console to generate an FLV pull stream address.

 &nbsp;

<span id="procedure-3"></span>
### Procedure

Configure a QUIC pull stream address and start playback. The sample code is as follows.

```objectivec
VeLivePlayerStream *playStreamFLV = [[VeLivePlayerStream alloc]init]; 
playStreamFLV.url = @"https://pull.example.com/live/stream.flv"; // Replace with your actual FLV pull stream address.
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;

// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];

// Add the FLV stream address.
[mainStreams addObject:playStreamFLV];

streamData.mainStream = mainStreams;

// Configure the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The Player SDK enables the QUIC failure fallback strategy by default. If QUIC stream pulling fails, the SDK automatically falls back to TCP stream pulling.</div>


 &nbsp;

<span id="playing-a-drm-encrypted-stream"></span>
## Playing a DRM\-encrypted stream

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support playing a DRM\-encrypted stream.</div>


To play streams protected by Digital Rights Management (DRM), do the following:


1. Follow the instructions detailed in [Encrypting your live streams using DRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm) and get the following information:

   * Get a DRM\-encrypted pull stream address in M3U8 format.

   * Get the URL to retrieve the DRM license using [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm). The URL contains authentication information and expiration time.

   * Get the FairPlay streaming certificate using [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm).

2. In your iOS project, initialize the player by calling [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype).

   ```objectivec
   self.livePlayer = [[TVLManager alloc] initWithType:VeLivePlayerTypeSystem];
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A system player initialized with <code>initWithType:</code> does not support the following features:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Playing streams other than the M3U8 format   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Primary\-backup stream switching   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ABR stream pulling   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Snapshot capturing   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Mirroring   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Custom rendering of audio and video   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Super\-resolution   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SEI   </div>
   

3. Set the DRM\-encrypted pull stream address.

   ```objectivec
   NSString *playUrl = @"http://pull.example.com/live/stream.m3u8"; // Replace with your actual DRM-encrypted pull stream address.
   [self.livePlayer setPlayUrl:playUrl];
   ```
   

4. Implement the [getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#getdrmresourceloadercertificatedata) and [getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#getdrmresourceloaderlicenseurl) callbacks of the player observer to provide the FairPlay certificate data and DRM license URL to the SDK.

   ```objectivec
   - (NSData *)getDrmResourceLoaderCertificateData:(TVLManager *)player {
       NSString *filePath = [[NSBundle mainBundle] pathForResource:@"testfairplay" ofType:@"cer"]; // Replace testfairplay with the actual FairPlay certificate file name.
       NSData *certificate = [NSData dataWithContentsOfFile:filePath];
       return certificate;
   }
   
   - (NSString *)getDrmResourceLoaderLicenseUrl:(TVLManager *)player {
       return @"https://drmtest/license"; // Replace with the actual DRM license URL.
   }
   ```
   

5. Play the DRM\-encrypted stream.

   ```objectivec
   [self.livePlayer play];
   ```
   


 &nbsp;

<span id="using-an-ip-address-as-the-pull-stream-address"></span>
## Using an IP address for stream pulling

The player supports using the IP address of the domain for stream pulling to reduce time\-to\-first\-frame.

 &nbsp;

<span id="using-ip-address-prerequisites"></span>
### Prerequisites

Obtain the pull stream address and resolve its IP address.

 &nbsp;

<span id="using-ip-address-procedure"></span>
### Procedure

Use the player's [setUrlHostIP:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#seturlhostip) API to associate the IP address with the domain name. The player then directly uses the IP address for stream pulling. The sample code is as follows.

```objectivec
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/stream.flv"]; // Replace with your actual pull stream address.

// Map the domain in the pull stream address to its resolved IP addresses.
NSMutableArray<NSString *> *ipList = [[NSMutableArray alloc] initWithCapacity:1];
[ipList addObject:@"xxx.xxx.xxx.xxx"];  // Replace with an actual IP address resolved from the domain.

NSMutableDictionary* ipHost = [[NSMutableDictionary alloc] initWithCapacity:1];
[ipHost setObject:ipList forKey:@"pull.example.com"]; // Replace pull.example.com with the domain in your actual pull stream address.

// Set the domain-to-IP mapping.
[self.livePlayer setUrlHostIP:ipHost];

// Start playback.
[self.livePlayer play];
```


 &nbsp;

<span id="resolution-switching"></span>
## Resolution switching

You can set multiple pull stream addresses with different resolutions and switch between these addresses during playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Resolution switching supports the stream fallback strategy. You can assign the same priority to one group of multi\-resolution streams and configure lower\-priority fallback streams. If playback of the higher\-priority stream group fails, the SDK automatically tries the fallback group. For more information, see <a href="https://docs.byteplus.com/en/docs/24/7585#stream-fallback-strategy-and-primary-backup-stream-switching">Stream fallback strategy and primary\-backup stream switching</a>.</div>


<span id="hX7l4MYRR"></span>
### Prerequisites

Obtain the pull stream addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:


1. [Configure a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

2. Get the pull stream addresses for the original and the transcoded streams in one of the following ways.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.

      This section uses the following pull stream addresses as examples.

   
   |**Resolution** |**Pull stream address** |
   |---|---|
   |Original (Origin) |`https://pull.example.com/live/123456.flv` |
   |Ultra High Definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |
   |High Definition (HD) |`https://pull.example.com/live/123456_hd.flv` |
   |Standard Definition (SD) |`https://pull.example.com/live/123456_sd.flv` |
   |Low Definition (LD) |`https://pull.example.com/live/123456_ld.flv` |
   


<span id="hgrWjxvY1"></span>
### Procedure


1. Configure multi\-resolution pull stream addresses and start playback. The sample code is as follows.

   ```objectivec
   // Configure pull stream addresses for multiple quality levels.
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // Replace with the actual pull stream address for the original quality level.
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // Original quality level.
   
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // Replace with the actual pull stream address for the UHD quality level.
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD quality level.
   
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // Replace with the actual pull stream address for the HD quality level.
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD quality level.
   
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // Replace with the actual pull stream address for the SD quality level.
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD quality level.
   
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv"; // Replace with the actual pull stream address for the LD quality level.
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD quality level.
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // Add the pull stream addresses.
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // Set the default resolution to original.
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // Configure the playback source.
   [self.livePlayer setPlayStreamData:streamData];
   
   // Start playback.
   [self.livePlayer play];
   ```
   

2. Call [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#switchresolution) to change the resolution.

   ```objectivec
   [self.livePlayer switchResolution:VeLivePlayerResolutionUHD]; // Switch to the UHD quality level.
   ```
   

3. When the switch is successful, the [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) callback will be triggered.

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
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


* <div data-tips="true" data-tips-type="tip">ABR stream pulling supports the stream fallback strategy. For RTM\-ABR streams, you can use the RTM\-ABR pull stream address as an RTM stream in the fallback strategy. For FLV streams, assign the same priority to all quality levels in one ABR stream group and configure lower\-priority fallback streams. If playback of the higher\-priority ABR stream group fails, the SDK automatically tries the fallback group. For more information, see <a href="https://docs.byteplus.com/en/docs/24/7585#stream-fallback-strategy-and-primary-backup-stream-switching">Stream fallback strategy and primary\-backup stream switching</a>.</div>



Currently, the Player SDK for iOS supports the following ABR modes:


* **RTM\-ABR streams**: A server\-side ABR capability for RTM playback. The player uses **only one** RTM\-ABR pull stream address, and the server automatically selects and switches quality levels based on the viewer's network conditions, which helps reduce stuttering in weak network environments while preserving RTM's low\-latency playback experience.

* **FLV streams**: A client\-side ABR capability. You provide multiple FLV pull stream addresses and bitrate information, and the SDK switches between them based on network conditions.


 &nbsp;

<span id="rtm-abr-streams"></span>
### RTM\-ABR streams

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Only versions 1.51.100.3\-premium and later support RTM\-ABR streams.</div>


 &nbsp;

<span id="rtm-abr-prerequisites"></span>
#### Prerequisites


* Configure multiple ABR substreams and select **RTM\-ABR** as the **Protocol Type** when you add an ABR configuration. For more information, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

* Get the RTM\-ABR pull stream addresses in one of the following ways.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) and select the startup quality level (suffix) to get the **RTM address** on the **Adaptive bitrate** tab. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate RTM\-ABR pull stream addresses. Different suffixes correspond to different startup quality levels. Use one of these addresses to start playback. Make sure the value of `Protocol` is `udp`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not manually append <code>rtmabr=true</code> to a regular RTM pull stream address. RTM\-ABR takes effect only after the RTM\-ABR configuration is completed and the generated RTM\-ABR address is used.   </div>
   

 &nbsp;

<span id="rtm-abr-procedure"></span>
#### Procedure

Set the **RTM\-ABR** pull stream address and start playback.

```objectivec
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/test_uhd.sdp?rtmabr=true"]; // Replace with your actual RTM-ABR pull stream address.

// Start playback.
[self.livePlayer play];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">You can also use the RTM\-ABR pull stream address in the stream fallback strategy for RTM streams. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368">Stream fallback strategy and primary\-backup stream switching</a>.</div>


 &nbsp;

<span id="flv-streams"></span>
### FLV streams

 &nbsp;

<span id="prerequisites-4"></span>
#### Prerequisites

Get the pull stream addresses for the source stream and the transcoded streams at each quality level. If you use BytePlus MediaLive, log in to the console and complete [transcoding configuration](https://console.byteplus.com/live/main/application/transcode) before obtaining the pull stream addresses. You can obtain addresses in either of the following ways:


* **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

* **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.


This section uses the following pull stream addresses as examples.

&nbsp;


|Quality level |Pull stream address |Bitrate (kbps) |
|---|---|---|
|Original (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
|Ultra High Definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|High Definition (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
|Standard Definition (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
|Low Definition (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">When configuring multiple quality\-level pull stream addresses for ABR, the encoding bitrate of each quality level in the SDK must be the same as the encoding bitrate configured in <a href="https://console.byteplus.com/live/main/application/transcode">transcoding configuration</a>. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding">Managing transcoding configuration</a>.</div>


 &nbsp;

<span id="procedure-4"></span>
#### Procedure


1. Configure multi\-quality pull stream addresses and start playback. The sample code is as follows.

   ```objectivec
   // Configure pull stream addresses for multiple quality levels.
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // Replace with the actual pull stream address for the original quality level.
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // Original quality level.
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // Replace with the actual pull stream address for the UHD quality level.
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD quality level.
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // Replace with the actual pull stream address for the HD quality level.
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD quality level.
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // Replace with the actual pull stream address for the SD quality level.
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD quality level.
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv";  // Replace with the actual pull stream address for the LD quality level.
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD quality level.
   playStreamLD.bitrate = 500;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // Add multi-quality streams.
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // Configure the default startup quality level.
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // Enable ABR.
   streamData.enableABR = YES;
   
   // Configure the playback source.
   [self.livePlayer setPlayStreamData:streamData];
   
   // Start playback.
   [self.livePlayer play];
   ```
   

2. When the ABR quality level switches automatically, the [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) callback defined in the [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) protocol is triggered. The sample code is as follows.

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
      // Quality level switch callback.
   }
   ```
   


 &nbsp;

<span id="smooth-quality-level-switching"></span>
## Smooth quality level switching

The smooth quality level switching feature ensures a seamless audio and video transition when viewers manually switch between different quality levels, such as ultra high definition, high definition, and standard definition. This **prevents black screens or stuttering** and improves the viewing experience.

To use this feature, configure the player with a list of streams from the same source at multiple quality levels and enable smooth quality level switching. After configuration, when viewers manually switch quality levels, the player smoothly transitions between streams of different bitrates to ensure continuous and stable live audio and video playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Smooth quality level switching supports the stream fallback strategy. You can assign the same priority to one group of smooth quality level switching streams and configure lower\-priority fallback streams. If playback of the higher\-priority stream group fails, the SDK automatically tries the fallback group. For more information, see <a href="https://docs.byteplus.com/en/docs/24/7585#stream-fallback-strategy-and-primary-backup-stream-switching">Stream fallback strategy and primary\-backup stream switching</a>.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">The smooth quality level switching feature is currently available only for FLV streams.</div>


* <div data-tips="true" data-tips-type="warning">Ensure that you have integrated the Player SDK version 1.50.100 or later.</div>



 &nbsp;

<span id="smooth-switch-prerequisites"></span>
### Prerequisites

Prepare pull stream addresses for different quality levels of the same source stream.

If you use a push stream address from BytePlus MediaLive for streaming, make sure that you have completed the following:


* **Add domain names**: Add a push domain and a pull domain under the same domain namespace. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

* **Configure transcoding**: Add transcoding configurations for different quality levels under the domain namespace. For more information, see [Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).

* **Get pull stream addresses**: Get the pull stream addresses for the source stream and each transcoded stream.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate pull stream addresses.

      * **Address type**: Select **Pull stream address**.

      * **Domain name**: Select the pull domain under the domain namespace used for the transcoding configuration.

      * **AppName** and **StreamName**: Enter the `AppName` and `StreamName` that match the push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, the `AppName` is `live` and the `StreamName` is `test`.

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate pull stream addresses.

      **Example**

      The following table lists sample FLV pull stream addresses and bitrates for different quality levels.

   
   |Quality level |FLV pull stream address |Bitrate (kbps) |
   |---|---|---|
   |Original (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
   |Ultra High Definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
   |High Definition (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
   |Standard Definition (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
   |Low Definition (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |
   


 &nbsp;

<span id="smooth-switch-procedure"></span>
### Procedure


1. Configure the streams for each quality level and set [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) to `YES` to enable smooth quality level switching.

   ```objectivec
   // Configure streams for each quality level.
   // Original quality level.
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // Replace with the actual pull stream address for the original quality level.
   playStreamOrigin.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // Quality level identifier.
   playStreamOrigin.type = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamOrigin.bitrate = 2500; // Bitrate in kbps.
   
   // UHD quality level.
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // Replace with the actual pull stream address for the UHD quality level.
   playStreamUHD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // Quality level identifier.
   playStreamUHD.type = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamUHD.bitrate = 2500; // Bitrate in kbps.
   
   // HD quality level.
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // Replace with the actual pull stream address for the HD quality level.
   playStreamHD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamHD.resolution = VeLivePlayerResolutionHD; // Quality level identifier.
   playStreamHD.type = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamHD.bitrate = 1000; // Bitrate in kbps.
   
   // SD quality level.
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // Replace with the actual pull stream address for the SD quality level.
   playStreamSD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamSD.resolution = VeLivePlayerResolutionSD; // Quality level identifier.
   playStreamSD.type = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamSD.bitrate = 800; // Bitrate in kbps.
   
   // LD quality level.
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv"; // Replace with the actual pull stream address for the LD quality level.
   playStreamLD.format = VeLivePlayerFormatFLV; // Stream format.
   playStreamLD.resolution = VeLivePlayerResolutionLD; // Quality level identifier.
   playStreamLD.type = VeLivePlayerStreamTypeMain; // Stream type used to distinguish primary and backup streams.
   playStreamLD.bitrate = 500; // Bitrate in kbps.
   
   // Create the playback source.
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // Add streams for each quality level.
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:5];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // Configure the default startup quality level.
   streamData.defaultResolution = VeLivePlayerResolutionSD;
   
   // Enable smooth quality level switching.
   streamData.enableSmoothSwitchResolution = YES;
   
   // Configure the playback source.
   [self.livePlayer setPlayStreamData:streamData];
   
   // Start playback.
   [self.livePlayer play];
   ```
   

2. During live streaming, when viewers manually switch quality levels, you can call [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) to switch the quality level smoothly. The sample code is as follows.

   ```objectivec
   // Switch to the UHD quality level.
   [self.livePlayer switchResolution:VeLivePlayerResolutionUHD];
   ```
   

3. Add the [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) callback to listen for quality level switch results. When the quality level changes, the SDK can trigger this callback and return information such as the switched quality level and the reason for the switch.

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *_Nonnull)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason;
   ```
   


 &nbsp;

<span id="snapshot-capturing"></span>
## Snapshot capturing

This feature enables you to capture the current video frame and generate an image.


1. Call [snapshot](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#snapshot) to take a snapshot. This feature only works during playback.


```objectivec
int result = [self.livePlayer snapshot];
```



2. After a snapshot is taken, the [onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onsnapshotcomplete-image) callback function will be triggered with the image data.


```objectivec
- (void)onSnapshotComplete:(TVLManager *)player image:(UIImage *)image  {
  // The callback function returns the image data through image.
}
```


 &nbsp;

<span id="sei"></span>
## SEI

Supplemental Enhancement Information (SEI) is additional data embedded within a live stream. You can use SEI to transmit custom data or metadata.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support SEI.</div>


 &nbsp;

<span id="sei-procedure"></span>
### Procedure


* String SEI messages

   1. Before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play), enable the [enableSei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablesei) property of the player. After this property is enabled, the player receives string SEI messages. The sample code is as follows.

      ```objectivec
      // Create a VeLivePlayerConfiguration instance.
      VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
      
      // Enable receiving string SEI messages.
      config.enableSei = YES;
      
      // Configure the initial settings of the player.
      [self.livePlayer setConfig:config];
      ```
      

   2. When the player receives a string SEI message, the [onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) callback is triggered. The sample code is as follows.

      ```objectivec
      - (void)onReceiveSeiMessage:(TVLManager *_Nonnull)player message:(NSString *_Nonnull)message  {
         // String SEI message callback.
      }
      ```
      

* Binary SEI messages

   1. Before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play), enable the [enableBinarySei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablebinarysei) property of the player. After this property is enabled, the player receives binary SEI messages and no longer triggers the string SEI message callback. The sample code is as follows.

      ```objectivec
      // Create a VeLivePlayerConfiguration instance.
      VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
      
      // Enable receiving binary SEI messages.
      config.enableBinarySei = YES;
      
      // Configure the initial settings of the player.
      [self.livePlayer setConfig:config];
      ```
      

   2. When the player receives a binary SEI message, the [onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) callback is triggered. The sample code is as follows.

      ```objectivec
      - (void)onReceiveBinarySeiMessage:(TVLManager *_Nonnull)player message:(NSData *_Nonnull)message  {
         // Binary SEI message callback.
      }
      ```
      


 &nbsp;

<span id="subscribing-to-video-data"></span>
## Subscribing to video data

By subscribing to decoded video data, you can obtain video frame data for custom processing and rendering. The player supports multiple video frame callback formats and provides the corresponding parameters and format options.

 &nbsp;

<span id="prerequisites-6"></span>
### Prerequisites

The following table describes the enumerations and meanings of video frame pixel formats and video data encapsulation formats.

&nbsp;


|Format type |Enumeration |Description |
|---|---|---|
|Video frame pixel format |VeLivePlayerPixelFormatNV12 |NV12 |
|Video frame pixel format |VeLivePlayerPixelFormatI420 |I420 |
|Video data encapsulation format |VeLivePlayerVideoBufferTypePixelBuffer |CVPixelBufferRef |
|Video data encapsulation format |VeLivePlayerVideoBufferTypeSampleBuffer |CVSampleBufferRef |
|Video data encapsulation format |VeLivePlayerVideoBufferTypeNSData |NSData |


Before subscribing to video data, select a format combination based on your needs. The combination must follow the mapping between [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerpixelformat) and [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideobuffertype) shown in the following table.

&nbsp;


|Pixel format/encapsulation format |VeLivePlayerPixelFormatNV12 |VeLivePlayerPixelFormatI420 |
|---|---|---|
|**VeLivePlayerVideoBufferTypePixelBuffer** |Supported (optimal performance) |Not supported |
|**VeLivePlayerVideoBufferTypeSampleBuffer** |Supported |Not supported |
|**VeLivePlayerVideoBufferTypeNSData** |Supported |Supported |


 &nbsp;

<span id="procedure-10"></span>
### Procedure


1. Call the player's [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enablevideoframeobserver-pixelformat-buffertype) API to enable or disable video frame data subscription. The API parameters are described in the following table.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |enable |BOOL |Whether to enable video frame callbacks. |
   |pixelFormat |VeLivePlayerPixelFormat |The video frame pixel format. |
   |bufferType |VeLivePlayerVideoBufferType |The video data encapsulation format. |
   

   The sample code is as follows.

   ```objectivec
   [self.livePlayer enableVideoFrameObserver:YES pixelFormat:VeLivePlayerPixelFormatNV12 bufferType:VeLivePlayerVideoBufferTypePixelBuffer];
   ```
   

2. The SDK returns the decoded video frame data through the [onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) callback of [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver). The sample code is as follows.

   ```objectivec
   - (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
      // Video frame data callback.
   }
   ```
   

   The [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideoframe) parameter is described in the following table.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |bufferType |VeLivePlayerVideoBufferType |The video frame data encapsulation format. |
   |pixelFormat |VeLivePlayerPixelFormat |The video frame pixel format. |
   |width |NSInteger |The video frame width, in px. |
   |height |NSInteger |The video frame height, in px. |
   |pts |int64_t |The video frame rendering timestamp, in ms. |
   |pixelBuffer |CVPixelBufferRef |The video data when `bufferType` is `VeLivePlayerVideoBufferTypePixelBuffer`. |
   |sampleBuffer |CMSampleBufferRef |The video data when `bufferType` is `VeLivePlayerVideoBufferTypeSampleBuffer`. |
   |data |NSData\* |The video data when `bufferType` is `VeLivePlayerVideoBufferTypeNSData`. |
   


 &nbsp;

<span id="subscribing-to-audio-data"></span>
## Subscribing to audio data

By subscribing to decoded audio data, you can perform custom audio processing and rendering. The Player SDK supports subscribing to audio data in PCM Float32 sample format and NSData encapsulation format.

&nbsp;


|VeLivePlayerAudioBufferType |Audio data encapsulation format |
|---|---|
|[VeLivePlayerAudioBufferTypeNSData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayeraudiobuffertype) |NSData |


 &nbsp;

<span id="procedure-11"></span>
### Procedure


1. Call the player's [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enableaudioframeobserver-enablerendering) API to enable or disable audio frame data subscription. The API parameters are described in the following table.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |enable |BOOL |Whether to enable audio frame callbacks. |
   |enableRendering |BOOL |Whether to enable player rendering. Set this parameter to `NO` if the player does not need to render audio internally. |
   

   The sample code is as follows.

   ```objectivec
   // Subscribe to audio frame data and enable internal audio rendering of the player.
   [self.livePlayer enableAudioFrameObserver:YES enableRendering:YES];
   ```
   

2. The SDK returns the decoded audio frame data through the [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) callback defined in the [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) protocol. The sample code is as follows.

   ```objectivec
   - (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
      // Audio frame data callback.
   }
   ```
   

   The [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayeraudioframe) parameter is described in the following table.

&nbsp;

   
   |Parameter |Data type |Description |
   |---|---|---|
   |bufferType |VeLivePlayerAudioBufferType |The audio frame data encapsulation format. |
   |sampleRate |int |The audio sample rate, in Hz. |
   |channels |int |The number of channels. |
   |bitDepth |int |The audio bit depth. |
   |pts |CMTime |The audio rendering timestamp, in ms. |
   |data |NSData\* |PCM audio data. |
   |samples |int |The number of audio samples. |
   

    &nbsp;


<span id="super-resolution"></span>
## Super\-resolution

Super\-resolution (SR) is a technology that reconstructs high\-resolution images from low\-resolution ones. Real\-time SR uses algorithms to reconstruct low\-resolution frames into high\-resolution ones in real time. This generates high\-resolution frames, which are then displayed on the screen. SR enhances video details and contrast, improving video clarity and the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support SR.</div>


 &nbsp;

<span id="super-resolution-prerequisites"></span>
### Prerequisites

Starting from version 1.51.300.2\-premium, to use the SR feature, you need to add the `LivePull-BMF` dependency in addition to the stream pulling component when integrating the Player SDK. For more information, see [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios).

 &nbsp;

<span id="super-resolution-procedure"></span>
### Procedure


1. Starting from version 1.51.300.2\-premium, import the `VeLivePlayer+SuperResolution.h` header file.

   
   <Tabs>
   <Tab zoneid="z1b53KKerA" title="Dynamic library">
   <TabTitle>Dynamic library</TabTitle>
   
   ```objectivec
   #import <TTSDKFramework/VeLivePlayer+SuperResolution.h>
   ```
   
   
   
   </Tab>
   <Tab zoneid="m59NgipAYn" title="Static library">
   <TabTitle>Static library</TabTitle>
   
   ```objectivec
   #import <TTSDK/VeLivePlayer+SuperResolution.h>
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Call the player's [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setenablesuperresolution) method to enable or disable SR.

   ```objectivec
   [self.livePlayer setEnableSuperResolution:YES];
   ```
   

   
   |Name |Type |Description |
   |---|---|---|
   |enable |BOOL |Whether to enable SR. The default value is `NO`.<br><br><br>* `YES`: Enables SR.<br><br>* `NO`: Disables SR. |
   

3. If enabling SR fails, the player notifies you through the [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) callback of [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver). The method signature is as follows.

   ```objectivec
   - (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
   ```
   

   Common reasons for failure to enable SR are as follows.

   * The actual stream resolution is not within the supported range for SR.

   * The actual stream frame rate is not within the supported range for SR.

   * The current device model does not support SR.


 &nbsp;

<span id="customizing-http-request-headers"></span>
## Customizing HTTP request headers

Set custom request headers for the player's HTTP requests. This is commonly used to transmit additional information such as authentication tokens, cookies, and service\-specific tracing identifiers.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only versions 1.50.200.3\-premium and later support customizing HTTP request headers.</div>


 &nbsp;

<span id="procedure-7"></span>
### Procedure

Before starting playback, you can set custom HTTP request headers through the player's advanced API [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value). When calling `setProperty:value:`, you need to pass a `key-value` configuration.

**Key**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|VeLivePlayerKeySetParamsHttpHeaders |NSString |The property key used to configure custom HTTP request headers. |


**Value**

The value is an `NSDictionary` object containing `key-value` pairs to set custom HTTP request headers.


* `Key`: `NSString` type. The request header name.

* `Value`: `NSString` type. The request header value.


The sample code is as follows.


* To set an HTTP request header

   ```objectivec
   [self.livePlayer setProperty:VeLivePlayerKeySetParamsHttpHeaders value:@{@"key": @"value"}]; // Replace with the actual header name and value.
   ```
   

* To set multiple HTTP request headers

   ```objectivec
   [self.livePlayer setProperty:VeLivePlayerKeySetParamsHttpHeaders
                             value:@{
                               @"key1": @"value1", // Replace with the actual header name and value.
                               @"key2": @"value2", // Replace with the actual header name and value.
                               @"key3": @"value3" // Replace with the actual header name and value.
                             }];
   ```
   


 &nbsp;

<span id="h.265-hardware-decoding-and-software-decoding"></span>
## H.265 hardware decoding and software decoding

The SDK with a premium or trial license enables H.265 hardware decoding and software decoding by default. When playing an H.265\-encoded video stream, the SDK first attempts to use H.265 hardware decoding. If H.265 hardware decoding fails, the SDK automatically switches to H.265 software decoding.

Before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play), enable or disable hardware decoding through the player's initial configuration. The sample code is as follows.

```objectivec
VeLivePlayerConfiguration *config = [VeLivePlayerConfiguration new];
config.enableHardwareDecode = YES;
[self.livePlayer setConfig:config];
```



* `YES`: Enables hardware decoding.

* `NO`: Disables hardware decoding and uses software decoding only.


You can listen for the [onStatistics:statistics:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) callback and use the [isHardWareDecode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-ishardwaredecode) property of [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerstatistics) to determine whether hardware decoding is used for the current stream.

 &nbsp;

<span id="video-sharpening"></span>
## Video sharpening

Video sharpening enhances the video locally on the device to improve the clarity of edges and texture details. During playback, the SDK can enhance edges and texture details in real time, making the video appear clearer and improving the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only premium and trial licenses support video sharpening.</div>


 &nbsp;

<span id="video-sharpening-prerequisites"></span>
### Prerequisites

Starting from version 1.51.300.2\-premium, to use the video sharpening feature, you need to add the `LivePull-BMF` dependency in addition to the stream pulling component when integrating the Player SDK. For more information, see [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios).

 &nbsp;

<span id="video-sharpening-procedure"></span>
### Procedure


1. Starting from version 1.51.300.2\-premium, import the `VeLivePlayer+SuperResolution.h` header file.

   
   <Tabs>
   <Tab zoneid="I7C7CfgEbn" title="Dynamic library">
   <TabTitle>Dynamic library</TabTitle>
   
   ```objectivec
   #import <TTSDKFramework/VeLivePlayer+SuperResolution.h>
   ```
   
   
   
   </Tab>
   <Tab zoneid="uC1gLPyLf8" title="Static library">
   <TabTitle>Static library</TabTitle>
   
   ```objectivec
   #import <TTSDK/VeLivePlayer+SuperResolution.h>
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Call the player's [setEnableSharpen:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) method to enable or disable video sharpening.

   ```objectivec
   [self.livePlayer setEnableSharpen:YES];
   ```
   

   
   |Name |Type |Description |
   |---|---|---|
   |enable |BOOL |Whether to enable video sharpening. The default value is `NO`.<br><br><br>* `YES`: Enables video sharpening.<br><br>* `NO`: Disables video sharpening. |
   

3. If enabling video sharpening fails, the player notifies you through the [onError:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) callback of [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver). The method signature is as follows.

   ```objectivec
   - (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
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

<span id="prerequisites-8"></span>
### Prerequisites


* You have integrated SDK version 1.51.200.4\-premium or later.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are using an SDK version earlier than 1.51.200.4\-premium, you can integrate the PiP solution to enable the PiP feature. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d46ae38e">PiP solution</a>.   </div>
   

* iOS 15.0 or later.

* In Xcode, enable the background mode required for PiP on your app target.

   1. On the **Signing & Capabilities** tab, click  **+**  **Capability**, and then double\-click **Background Modes**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8ccac9b131740cab54e2d294a73885f~tplv-goo7wpa0wc-topic.webp) </span>

   2. In the **Background Modes** section, select **Audio, AirPlay, and Picture in Picture**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0782c08333eb411b8f27c201d6968bb3~tplv-goo7wpa0wc-topic.webp) </span>

* Guide viewers to enable the system\-level PiP setting on their devices: go to **Settings** \> **General** \> **Picture in Picture** and turn on **Start PiP Automatically**. After this setting is enabled, PiP playback can start automatically when the app enters the background.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08beec9cc01b4adb9ca988dc02c4b569~tplv-goo7wpa0wc-topic.webp) </span>


 &nbsp;

<span id="procedure-9"></span>
### Procedure


1. Import the PiP header file.

   
   <Tabs>
   <Tab zoneid="F9xsucVhGM" title="Static library integration">
   <TabTitle>Static library integration</TabTitle>
   
   If you use static library integration for the SDK, import the PiP header file by using `#import <TTSDK/VeLivePlayer+PictureInPicture.h>`.
   
   
   </Tab>
   <Tab zoneid="PmWk15yHSO" title="Dynamic library integration">
   <TabTitle>Dynamic library integration</TabTitle>
   
   If you use dynamic library integration for the SDK, import the PiP header file by using `#import <TTSDKFramework/VeLivePlayer+PictureInPicture.h>`.
   
   
   </Tab>
   </Tabs>
   

2. Check whether the current device supports PiP.

   ```objectivec
   if ([TVLManager isPictureInPictureSupported]) {
       // Implement your business logic based on whether the current device supports PiP.
   }
   ```
   

3. Initialize the SDK's built\-in player and enable PiP. PiP is disabled by default.

   ```objectivec
   TVLManager *player = [[TVLManager alloc]initWithType:VeLivePlayerTypeOwn];
   player.enablePictureInPicture = YES;
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">PiP is supported only by the SDK's built\-in player and is not supported by the system player.   </div>
   

4. Configure whether PiP starts automatically when the app enters the background. This setting applies only to the current player and does not change the system\-level PiP setting on the viewer's device.

   By default, PiP starts automatically when the app enters the background. If you do not want PiP to start automatically, set [canStartPictureInPictureAutomaticallyFromInline](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline) to `NO`. The following sample code enables PiP to start automatically when the app enters the background.

   ```objectivec
   player.canStartPictureInPictureAutomaticallyFromInline = YES;
   ```
   

5. If you want to listen for PiP lifecycle events such as start and stop, you can set the following PiP delegate properties. The SDK already handles the key delegate methods required for PiP internally, so in most cases you do not need to implement them yourself.

   ```objectivec
   @property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate;
   @property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate;
   ```
   

6. After playback starts, you can manually start PiP.

   ```objectivec
   [player startPictureInPicture];
   ```
   

   If PiP is currently active, you can manually stop PiP.

   ```objectivec
   [player stopPictureInPicture];
   ```
   

7. To check whether PiP has started successfully, call the following method.

   ```objectivec
   BOOL isStarted = [TVLManager isPictureInPictureStarted];
   ```
   

8. To manually update the PiP playback button state and progress display, call [invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate). The SDK automatically updates the playback button state and progress display internally, so you do not need to call this method in most cases.

   ```objectivec
   [player invalidatePictureInPicturePlaybackState];
   ```
   


 &nbsp;

<span id="pip-solution"></span>
### PiP solution

If you are using an SDK version earlier than 1.51.200.4\-premium, you can integrate the [PiP solution](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/blob/main/VeLivePictureInPicture.podspec) to enable the PiP feature.

Choose one of the following integration methods as needed:


<Tabs>
<Tab zoneid="P2vZkm44FB" title="Online integration">
<TabTitle>Online integration</TabTitle>

```objectivec
pod 'VeLivePictureInPicture', :git => 'https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git', :branch => 'main'
```



</Tab>
<Tab zoneid="juNdLcX9UE" title="Local integration">
<TabTitle>Local integration</TabTitle>

Copy the following files from the [PiP solution](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/blob/main/VeLivePictureInPicture.podspec) to your local project:


* Source files in the `VeLivePictureInPicture` directory

* `VeLivePictureInPicture.podspec`


`path` indicates the path of these files relative to the `Podfile` in your local project. For example, if these files are located in the same directory as the `Podfile` in your local project, set `path` to `./`.

```objectivec
pod 'VeLivePictureInPicture', :path => './'
```



</Tab>
</Tabs>


After integrating the PiP solution, you can use the same APIs as in SDK version 1.51.200.4\-premium or later. For more information, see [Procedure](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#97a32559).

 &nbsp;

<span id="advanced-api-configuration"></span>
## Advanced API configuration

 &nbsp;

<span id="removing-query-parameters-automatically-appended-by-the-sdk"></span>
### Removing query parameters automatically appended by the SDK

The Player SDK might append query parameters, such as `session_id`, to a pull stream address. These parameters identify a pull stream session and help locate the same session in both client and CDN logs when troubleshooting playback issues. To prevent the SDK from including automatically appended query parameters in the actual request URL, enable this feature. After this feature is enabled, SDK\-appended query parameters are removed from the actual request URL, while query parameters already present in the original pull stream address are retained.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only versions 1.52.1 and later support removing query parameters automatically appended by the SDK.</div>


<span id="remove-query-params-procedure"></span>
#### Procedure

Before starting playback, you can use the player's advanced [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) API to configure whether to remove query parameters automatically appended by the SDK. When calling `setProperty:value:`, you need to pass a `key-value` configuration.

**Key**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|VeLivePlayerKeySetParamsRemoveQueryParams |NSString |The property key for removing query parameters automatically appended by the SDK. |


**Value**

`Value` is an `NSNumber` value that indicates whether to remove query parameters automatically appended by the SDK. The default value is `0`.


* `1`: Removes query parameters automatically appended by the SDK.

* `0`: Retains query parameters automatically appended by the SDK.


The sample code is as follows.

```objectivec
[self.livePlayer setProperty:@"VeLivePlayerKeySetParamsRemoveQueryParams" value:@1];
```


**Effect example**

For example, the pull stream address is:

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```


When the SDK initiates the playback request, it automatically appends `session_id`.

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901&session_id=xxx
```


After this feature is enabled, the request URL no longer contains `session_id` but retains the `auth_key` authentication parameter from the original pull stream address:

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```
