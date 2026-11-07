---
title: "Player SDK for iOS: Advanced features for versions earlier than 1.50.100"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player_sdk_for_ios_advanced_features_for_versions_earlier_than_150100"
---

To enhance viewing experience in your app, this topic details how to implement advanced features of the Player SDK for iOS. You can implement complex features as needed, according to actual business requirements.

<span id="f1bc2276"></span>
## Prerequisites


* You have implemented the basic features of the Player SDK by following the instructions provided in [Player SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3).

* To use the following features, ensure you use a premium or trial license.

   * [RTM stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d2fff36e)

   * [QUIC stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#78c4f3ae)

   * Low\-latency FLV stream pulling (with a latency of about 2 seconds)

   * [Primary and backup streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d32df4f2)

   * [ABR stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#aceb1766)

   * [Super-resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#4ea2c546)

   * H.265 hardware and software decoding

   * Video sharpening

   * [Playing a DRM-encrypted stream](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e1834266)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/managing_sdk_licenses#upgrading-a-trial-license-to-a-basic-or-premium-license">Upgrading a trial license to a basic or premium license</a>.   </div>
   

<span id="96fdbb93"></span>
## Notes

Because the Player SDK uses various iOS audio and video APIs that may not work properly on simulators, we recommend that you use a physical device for testing.

<span id="d2fff36e"></span>
## RTM stream pulling

This feature should be used in conjunction with the live\-streaming service provided by BytePlus MediaLive. For details, refer to [Introduction to Real Time Media](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-real-time-media).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">RTM protocol does not support pure audio or pure video streaming.</div>


<span id="16fcb8b3"></span>
### Preparation


* Make sure that you have integrated the **Premium** edition of the Player SDK.

* Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate RTM and FLV pull stream addresses. The FLV stream address can serve as an automatic fallback address if RTM stream pulling fails.


<span id="cec95e84"></span>
### Retry strategy

When RTM stream pulling fails, a retry mechanism is triggered.

You can customize the maximum number of retries and the retry interval by calling the [setConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-3#configuring-the-player) method to configure the following properties of `VeLivePlayerConfiguration`.


* `retryMaxCount`: Maximum number of retries. The default value is `5`.

* `retryIntervalTimeMs`: The retry interval. The default value is `5000` ms.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a backup stream exists, the retry interval does not take effect, and each retry is performed immediately. Additionally, each switch between the primary and backup streams consumes one retry count.</div>


<span id="a940286d"></span>
### Downgrade strategy

If you set both the RTM and FLV pull stream addresses, the player automatically downgrades to FLV stream pulling when the number of retries for RTM stream pulling exceeds `retryMaxCount`. When the number of retries for FLV stream pulling exceeds `retryMaxCount`, the player stops pulling the stream.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once downgraded to FLV stream pulling, the player cannot automatically recover to RTM stream pulling. To use the RTM stream, you must pull the stream again.</div>


<span id="ab5c5a97"></span>
### Integration

Set the RTM and FLV pull stream addresses for playing. The sample code is as follows.

```objectivec
// Set the RTM stream address.
VeLivePlayerStream *playStreamRTM = [[VeLivePlayerStream alloc]init];
playStreamRTM.url = "https://pull.example.com/live/stream.sdp";
playStreamRTM.format = VeLivePlayerFormatRTM;

// Set the FLV stream address.
VeLivePlayerStream *playStreamFLV = [[VeLivePlayerStream alloc]init];
playStreamFLV.url = "https://pull.example.com/live/stream.flv";
playStreamFLV.format = VeLivePlayerFormatFLV;


// Create a VeLivePlayerStreamData instance.
 VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];

// Add the RTM stream address to the list of primary stream addresses.
[mainStreams addObject:playStreamRTM];

// Add the FLV stream address to the list of primary stream addresses.
[mainStreams addObject:playStreamFLV];

// Set the list of primary stream addresses.
streamData.mainStream = mainStreams;

// Set the default live streaming format to RTM and the default transmission protocol to TLS.
streamData.defaultFormat = VeLivePlayerFormatRTM;
streamData.defaultProtocol = VeLivePlayerProtocolTLS;
    

// Set the playback source.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```


<span id="78c4f3ae"></span>
## QUIC stream pulling

This feature should be used in conjunction with the live\-streaming service provided by BytePlus MediaLive.

Use the following steps to pull a stream using the QUIC protocol:


1. Add `Quic/Pull` in `subspecs` to enable QUIC stream pulling when you integrate the Player SDK.


```objectivec
pod 'TTSDK', '1.37.1.8-premium', :subspecs => ['LivePull', 'Quic/Pull']
```



2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate an FLV pull stream address.

3. Provide the FLV pull stream address and set the streaming protocol to QUIC using the following code:


```objectivec
// Set the FLV address.
VeLivePlayerStream *playStreamFLV = [[VeLivePlayerStream alloc]init];
playStreamFLV.url = "https://pull.example.com/live/stream.flv";
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;


// Create a VeLivePlayerStreamData instance.
 VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
// Add the FLV stream address.
[mainStreams addObject:playStreamFLV];

streamData.mainStream = mainStreams;

// Set the default format and protocol.
streamData.defaultFormat = VeLivePlayerFormatFLV;
streamData.defaultProtocol = VeLivePlayerProtocolQUIC; // Set the default protocol to QUIC.
    

// Pass in the pull-stream configurations.
[self.livePlayer setPlayStreamData:streamData];

// Start playback.
[self.livePlayer play];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The player automatically switches to the TCP protocol if it fails to pull the stream using the QUIC protocol.</div>


<span id="e1834266"></span>
## Playing a DRM\-encrypted stream

To play streams encrypted by Digital Rights Management (DRM) licenses, do the following:


1. Follow the instructions detailed in [Encrypting your live streams using DRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm) and get the following information:

   * Get a DRM\-encrypted playback address in M3U8 format.

   * Get the URL to retrieve the DRM license using [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm). The URL contains authentication information and expiration time and must be generated by your app servers.

   * Get the FairPlay streaming certificate using [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm).

2. In your iOS project, initialize the player by calling `initWithType:`.

   ```objectivec
   self.livePlayer = [[TVLManager alloc] initWithType:VeLivePlayerTypeSystem];
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A player initialized with the <code>initWithType:</code> method does not support the following features:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Playing streams other than the M3U8 format   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Primary and backup streams   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ABR stream pulling   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Snapshot capturing   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Mirroring   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Custom rendering of audio and video   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Super\-resolution   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SEI   </div>
   

3. Set the pull stream address.

   ```objectivec
   NSString *playUrl = "http://pull.example.com/live/stream.m3u8";
   [self.livePlayer setPlayUrl:playUrl];
   ```
   

4. Register for the player observer and return the license and certificate addresses in the callback functions.

   ```objectivec
   - (NSData *)getDrmResourceLoaderCertificateData:(TVLManager *)player {
       // Enter the local path to the FairPlay streaming certificate
       NSString *filePath = [[NSBundle mainBundle] pathForResource:@"testfairplay" ofType:@"cer"];
       NSData *certificate = [NSData dataWithContentsOfFile:filePath];
       return certificate;
   }
   
   - (NSString *)getDrmResourceLoaderLicenseUrl:(TVLManager *)player {
       // Return the URL to retrieve the DRM license
       return @"https://drmtest/license";
   }
   ```
   

5. Play the DRM\-encrypted stream.

   ```objectivec
   [self.livePlayer play];
   ```
   


<span id="4b722f58"></span>
## Using an IP address as the pull stream address

You can use an IP address as the pull stream address to reduce the time\-to\-first\-frame.

Use the following steps to set an IP address as the pull stream address:


1. Obtain the pull stream address.

2. Resolve the IP address from the pull stream address.

3. Associate the IP address with the domain name for stream pulling by calling [setUrlHostIP:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#seturlhostip):


```objectivec
// Set the pull stream address.
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/stream.flv"];

// Associate the IP address with the domain name for stream pulling.
NSMutableArray<NSString *> *ipList = [[NSMutableArray alloc] initWithCapacity:1];
[ipList addObject:@"xxx.xxx.xxx.xxx"];  // Add the IP address.

NSMutableDictionary* ipHost = [[NSMutableDictionary alloc] initWithCapacity:1];
[ipHost setObject:ipList forKey:@"pull.example.com"]; // Replace "pull.example.com" with your domain name for stream pulling.

// Set the mapping of domain names to server IP addresses.
[self.livePlayer setUrlHostIP:ipHost];

// Start playback.
[self.livePlayer play];
```


<span id="d32df4f2"></span>
## Primary and backup streams

The primary and backup stream feature provides disaster recovery for live streaming. By configuring both a primary and a backup stream, the player can automatically switch between them if one fails. For example, if the primary stream fails, the player switches to the backup stream. You can use stream addresses from the same or different service providers.

Use the following steps to set a primary and a backup stream address:


1. Obtain a primary and a backup stream address. If you are using the live\-streaming service provided by BytePlus MediaLive, you can use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate the addresses.

2. Set the primary and the backup stream addresses by using the following code:


```objectivec
// Set the primary stream address.
VeLivePlayerStream *playStreamMain = [[VeLivePlayerStream alloc]init];
playStreamMain.url = @"https://pull.example.com/live/main.flv";
playStreamMain.type = VeLivePlayerStreamTypeMain; // Set the stream type to primary.
    
// Set the backup stream address.
VeLivePlayerStream *playStreamBackup = [[VeLivePlayerStream alloc]init];
playStreamBackup.url = @"https://pull.example.com/live/backup.flv";
playStreamBackup.type = VeLivePlayerStreamTypeBackup; // Set the stream type to backup.
    
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
    
// Enable the player to switch between the primary and the backup stream addresses.
streamData.enableMainBackupSwitch = YES;
    
// Add the primary stream.
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
[mainStreams addObject:playStreamMain];
streamData.mainStream = mainStreams;
    
// Add the backup stream.
NSMutableArray <VeLivePlayerStream *> *backupStreams = [NSMutableArray arrayWithCapacity:1];
[backupStreams addObject:playStreamBackup];
streamData.backupStream = backupStreams;
    
// Pass in the pull-stream configurations.
[self.livePlayer setPlayStreamData:streamData];
    
// Start playback.
[self.livePlayer play];
```



3. When the player switches between the primary and the backup stream addresses, the [onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) callback function will be triggered.


```objectivec
- (void)onMainBackupSwitch:(TVLManager *)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error {
 // Triggered when a switch is complete.
}
```


<span id="660adfe3"></span>
## Resolution switching

You can set multiple pull stream addresses with different resolutions and switch between these addresses during playback.

Use the following steps to enable resolution switching:


1. Obtain the pull stream addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:

   1. [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

   2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) or call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) to generate the corresponding pull stream addresses for the original and the transcoded streams.

2. Set the pull stream addresses. The following addresses are used as examples in the sample code.



|**Resolution** |**Pull stream address** |
|---|---|
|Original (Origin) |https://pull.example.com/live/123456.flv |
|Ultra high definition (UHD) |https://pull.example.com/live/123456_uhd.flv |
|High definition (HD) |https://pull.example.com/live/123456_hd.flv |
|Standard definition (SD) |https://pull.example.com/live/123456_sd.flv |
|Low definition (LD) |https://pull.example.com/live/123456_ld.flv |


```objectivec
// Set multiple pull stream addresses with different resolutions.
VeLivePlayerStream *playStreamOrgin = [[VeLivePlayerStream alloc]init];
playStreamOrgin.url = @"https://pull.example.com/live/123456.flv";
playStreamOrgin.resolution = VeLivePlayerResolutionOrigin; // Original.
    
VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv";
playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD.
    
VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv";
playStreamHD.resolution = VeLivePlayerResolutionHD; // HD.
    
VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv";
playStreamSD.resolution = VeLivePlayerResolutionSD; // SD.
    
VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv";
playStreamLD.resolution = VeLivePlayerResolutionLD; // LD.
    
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
    
// Add the pull stream addresses.
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
[mainStreams addObject:playStreamOrgin];
[mainStreams addObject:playStreamUHD];
[mainStreams addObject:playStreamHD];
[mainStreams addObject:playStreamSD];
[mainStreams addObject:playStreamLD];
streamData.mainStream = mainStreams;
    
// Set the default resolution to original.
streamData.defaultResolution = VeLivePlayerResolutionOrigin;
    
// Pass in the pull-stream configurations.
[self.livePlayer setPlayStreamData:streamData];
    
// Start playback.
[self.livePlayer play];
```



3. Call [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#switchresolution) to change the resolution.


```objectivec
[self.livePlayer switchResolution:VeLivePlayerResolutionUHD]; // Switch to UHD.
```



4. When the switch is successful, the [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onresolutionswitch-resolution-error-reason) callback function will be triggered.


```objectivec
- (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
  // Triggered when the resolution switch is complete.
}
```


<span id="f4206aae"></span>
## ABR stream pulling

Adaptive bitrate (ABR) is a streaming technology that uses algorithms to automatically switch between streams of different resolutions based on network conditions. This process minimizes playback stuttering and improves the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ABR stream pulling only applies to FLV streams.</div>


Use the following steps to enable ABR stream pulling:


1. Obtain the pull stream addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:

   1. [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

   2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) or call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) to generate the corresponding pull stream addresses for the original and the transcoded streams.

2. Set the pull stream addresses. The following addresses are used as examples in the sample code.



|**Resolution** |**Pull stream address** |**Bitrate (Kbps)**  |
|---|---|---|
|Original (Origin) |https://pull.example.com/live/123456.flv |2500 |
|Ultra high definition (UHD) |https://pull.example.com/live/123456_uhd.flv |2500 |
|High definition (HD) |https://pull.example.com/live/123456_hd.flv |1000 |
|Standard definition (SD) |https://pull.example.com/live/123456_sd.flv |800 |
|Low definition (LD) |https://pull.example.com/live/123456_ld.flv |500 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The encoding bitrate for each address must be identical to the one specified in the transcoding configurations. For example, if you set the bitrate of the UHD stream to 2500 Kbps in the transcoding configurations, you must set the <code>playStreamUHD.bitrate</code> to <code>2500</code> in the code.</div>


```objectivec
// Set multiple pull stream addresses with different resolutions.
VeLivePlayerStream *playStreamOrgin = [[VeLivePlayerStream alloc]init];
playStreamOrgin.url = @"https://pull.example.com/live/123456.flv";
playStreamOrgin.resolution = VeLivePlayerResolutionOrigin; // Original.
playStreamOrgin.bitrate = 2500; // The bitrate must be consistent with the transcoding configurations.

VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv";
playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD.
playStreamUHD.bitrate = 2500;
    
VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv";
playStreamHD.resolution = VeLivePlayerResolutionHD; // HD.
playStreamHD.bitrate = 1000;
    
VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv";
playStreamSD.resolution = VeLivePlayerResolutionSD; // SD.
playStreamSD.bitrate = 800;
    
VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv";
playStreamLD.resolution = VeLivePlayerResolutionLD; // LD.
playStreamLD.bitrate = 500;
    
// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
    
// Add the pull stream addresses.
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
[mainStreams addObject:playStreamOrgin];
[mainStreams addObject:playStreamUHD];
[mainStreams addObject:playStreamHD];
[mainStreams addObject:playStreamSD];
[mainStreams addObject:playStreamLD];
streamData.mainStream = mainStreams;
    
// Set the default resolution to original.
streamData.defaultResolution = VeLivePlayerResolutionOrigin;

// Enable ABR.
streamData.enableABR = YES;
    
// Pass in the pull-stream configurations.
[self.livePlayer setPlayStreamData:streamData];
    
// Start playback.
[self.livePlayer play];
```



3. When a resolution switch is complete, the [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onresolutionswitch-resolution-error-reason) callback function will be triggered.


```objectivec
- (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
  // Triggered when a resolution switch is complete.
}
```


<span id="90469fd2"></span>
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


<span id="aceb1766"></span>
## SEI

Supplemental enhancement information (SEI) is additional data embedded within a live stream. You can use SEI to transmit custom data or metadata.


1. Call [enableSei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#enablesei) before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) to enable the player to receive SEI messages.


```objectivec
// Create a VeLivePlayerConfiguration instance.
VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];

// Enable the player to receive SEI messages.
config.enableSei = YES;
        
// Configure the initial settings of the player.
[self.livePlayer setConfig:config];
```



2. When the live stream contains an SEI message, the [onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onreceiveseimessage-message) callback is triggered, providing the message.


```objectivec
- (void)onReceiveSeiMessage:(TVLManager *)player message:(NSString*)message  {
  // Triggered when an SEI message is received.
}
```


<span id="8921508a"></span>
## Subscribing to video data

By subscribing to decoded video data, you can perform custom video processing and rendering. The Player SDK supports subscribing to video data in the following pixel formats and encapsulation formats:


|**Format** |**Enumeration** |**Description** |
|---|---|---|
|Pixel format<br><br>[VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerpixelformat) |`VeLivePlayerPixelFormatNV12` |NV12 |
||`VeLivePlayerPixelFormatI420` |I420 |
|Encapsulation format<br><br>[VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideobuffertype) |`VeLivePlayerVideoBufferTypePixelBuffer` |CVPixelBufferRef |
||`VeLivePlayerVideoBufferTypeSampleBuffer` |CVSampleBufferRef |
||`VeLivePlayerVideoBufferTypeNSData` |NSData |


The supported combinations of pixel formats and encapsulation formats are shown in the table below:


|**Encapsulation format/Pixel format** |**VeLivePlayerPixelFormatNV12** |**VeLivePlayerPixelFormatI420** |
|---|---|---|
|VeLivePlayerVideoBufferTypePixelBuffer |√ (Optimal performance) |× |
|VeLivePlayerVideoBufferTypeSampleBuffer |√ |× |
|VeLivePlayerVideoBufferTypeNSData |√ |√ |



1. Subscribe to video data by calling [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enablevideoframeobserver-pixelformat-buffertype).


```objectivec
[self.livePlayer enableVideoFrameObserver:YES pixelFormat:VeLivePlayerPixelFormatNV12 bufferType:VeLivePlayerVideoBufferTypePixelBuffer];
```



2. The [onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onrendervideoframe-videoframe) callback function returns the decoded video data.


```objectivec
- (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
  // Returns decoded video data.
}
```


<span id="7afd4852"></span>
## Subscribing to audio data

By subscribing to decoded audio data, you can perform custom audio processing and rendering. The Player SDK supports subscribing to audio data in PCM Float32 sample format and NSData encapsulation format.


1. Subscribe to audio data by calling [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enableaudioframeobserver-enablerendering).


```objectivec
[self.livePlayer enableAudioFrameObserver:YES enableRendering:YES];
```



2. The [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onrenderaudioframe-audioframe) callback function returns the decoded audio data.


```objectivec
- (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
  // Returns decoded audio data.
}
```


<span id="4ea2c546"></span>
## Super\-resolution

Super\-resolution (SR) is a technology that reconstructs high\-resolution images from low\-resolution ones. Real\-time SR uses algorithms to reconstruct low\-resolution frames into high\-resolution ones in real time. This generates high\-resolution frames, which are then displayed on the screen. SR enhances video details and contrast, improving video clarity and the viewing experience.


1. Enable SR by calling [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setenablesuperresolution).

2. If the SDK fails to enable SR, the [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onstreamfailedopensuperresolution-error) callback will be triggered.


```objectivec
- (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
```


Possible reasons for failure to enable SR include:


* The resolution of the original stream is higher than the maximum resolution supported by SR, which is 1300\*750.

* The frame rate of the original stream is higher than the maximum frame rate supported by SR, which is 30 fps.

* The client device does not support SR.


Please contact BytePlus technical support if the maximum resolution and frame rate do not meet your business requirements.
