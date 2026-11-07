---
title: "Player SDK for Android: Advanced features for versions earlier than 1.50.100"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player_sdk_for_android_advanced_features_for_versions_earlier_than_15010"
---

To enhance viewing experience in your app, this topic details how to implement advanced features of the Player SDK for Android. You can implement complex features as needed, according to actual business requirements.

<span id="75fa227a"></span>
## Prerequisites


* You have implemented the basic features of the Player SDK by following the instructions provided in [Player SDK for Android: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2).

* To use the following features, ensure you use a premium or trial license.

   * [RTM stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#af29cf39)

   * [QUIC stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#4d503d05)

   * Playing CMAF streams

   * Low\-latency FLV stream pulling (with a latency of about 2 seconds)

   * [Primary and backup streams](/docs/byteplus\-media\-live/docs\-implementing\-advanced\-features\-2#Setting multiple addresses for stream pulling)

   * [ABR stream pulling](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#34e237fb)

   * [Super-resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#84bd3b42)

   * H.265 hardware and software decoding

   * H.266 software decoding

   * Video sharpening

   * Commercial DRM (Digital Rights Management)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/managing_sdk_licenses#upgrading-a-trial-license-to-a-basic-or-premium-license">Upgrading a trial license to a basic or premium license</a>.   </div>
   

<span id="00f4cec7"></span>
## Notes

Because the Player SDK uses various Android audio and video APIs that may not work properly on simulators, we recommend that you use a physical device for testing.

<span id="af29cf39"></span>
## RTM stream pulling

This feature should be used in conjunction with the live\-streaming service provided by BytePlus MediaLive. For details, refer to [Introduction to Real Time Media](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-real-time-media).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The RTM protocol does not support audio\-only or video\-only streams.</div>


<span id="6bce4b53"></span>
### Preparation

Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate RTM and FLV pull stream addresses. The FLV stream address can serve as an automatic fallback if RTM stream pulling fails.

<span id="7e61a39f"></span>
### Retry strategy

When RTM stream pulling fails, a retry mechanism is triggered.

You can customize the maximum number of retries and the retry interval by calling the [setConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-2#configuring-the-player) method to configure the following properties of `VeLivePlayerConfiguration`.


* `retryMaxCount`: Maximum number of retries. The default value is `5`.

* `retryIntervalTimeMs`: The retry interval. The default value is `5000` ms.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The retry strategy depends on whether a backup stream exists.</div>



* <div data-tips="true" data-tips-type="tip">If a backup stream exists: The retry interval does not take effect. Each retry is performed immediately, and each switch between the primary and backup streams consumes one retry count.</div>


* <div data-tips="true" data-tips-type="tip">If no backup stream exists: The first 3 retries are performed immediately. Starting from the 4th retry, subsequent retries are performed at intervals set by <code>retryIntervalTimeMs</code>.</div>



Because some player errors are difficult to recover from even after retries, the player will directly downgrade to FLV stream pulling. Therefore, to make sure that retries for RTM stream pulling adhere to `retryMaxCount`, call the following method before starting to pull the stream.

```Java
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetForceRTMRetry, true);
```


<span id="19922329"></span>
### Downgrade strategy

If you set both the RTM and FLV pull stream addresses, the player automatically downgrades to FLV stream pulling when the number of retries for RTM stream pulling exceeds `retryMaxCount`. When the number of retries for FLV stream pulling exceeds `retryMaxCount`, the player stops pulling the stream.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once downgraded to FLV stream pulling, the player cannot automatically recover to RTM stream pulling. To use the RTM stream, you must pull the stream again.</div>


<span id="88effa8b"></span>
### Integration

Set the RTM and FLV pull stream addresses for playing. The sample code is as follows.

```Java
// Set the RTM stream address.
VeLivePlayerStream playStreamRTM = new VeLivePlayerStream();
playStreamRTM.url = "https://pull.example.com/live/stream.sdp";
playStreamRTM.format = VeLivePlayerFormatRTM;
playStreamRTM.resolution = VeLivePlayerResolutionOrigin;
playStreamRTM.streamType = VeLivePlayerStreamTypeMain;

// Set the FLV stream address.
VeLivePlayerStream playStreamFLV = new VeLivePlayerStream();
playStreamFLV.url = "https://pull.example.com/live/stream.flv";
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.resolution = VeLivePlayerResolutionOrigin;
playStreamFLV.streamType = VeLivePlayerStreamTypeMain;

// Create a VeLivePlayerStreamData instance.
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
// Set the list of primary stream addresses.
streamData.mainStreamList = new ArrayList<>();

// Add the RTM stream address to the list of primary stream addresses.
streamData.mainStreamList.add(playStreamRTM);

// Add the FLV stream address to the list of primary stream addresses.
streamData.mainStreamList.add(playStreamFLV);

// Set the default live streaming format to RTM and the default transmission protocol to TLS.
streamData.defaultFormat = VeLivePlayerFormatRTM;
streamData.defaultProtocol = VeLivePlayerProtocolTLS;

// Set the playback source.
mLivePlayer.setPlayStreamData(streamData);

// Start playback.
mLivePlayer.play();
```


<span id="4d503d05"></span>
## QUIC stream pulling

This feature should be used in conjunction with the live\-streaming service provided by BytePlus MediaLive.

Use the following steps to pull a stream using the QUIC protocol:


1. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate an FLV stream pulling address.

2. Provide the FLV pull stream address and set the streaming protocol to QUIC using the following code:

   ```Java
   // Set the FLV address.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamFLV = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamFLV.url = "https://pull.example.com/live/stream.flv";
   playStreamFLV.format = VeLivePlayerFormatFLV;
   playStreamFLV.resolution = VeLivePlayerResolutionOrigin;
   playStreamFLV.streamType = VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   streamData.mainStreamList = new ArrayList<>();
   
   // Add the FLV stream.
   streamData.mainStreamList.add(playStreamFLV);
   
   // Set the default format and protocol.
   streamData.defaultFormat = VeLivePlayerFormatFLV;
   streamData.defaultProtocol = VeLivePlayerProtocolQUIC; // QUIC.
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The player automatically switches to the TCP protocol if it fails to pull the stream using the QUIC protocol.</div>


<span id="Using an IP address in the playing URL"></span>
## Using an IP address as the pull stream address

You can use an IP address as the pull streaming address to reduce the time\-to\-first\-frame.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When using setUrlHostIP to map domain names and IP addresses, disable the DNS pre\-resolution feature in the initial configuration by setting <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#enablelivedns">enableLiveDNS</a> to false.</div>


* <div data-tips="true" data-tips-type="tip">Call this method to set the mapping of domain names and IP addresses before calling <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#play">play</a> to start playback.</div>



Use the following steps to set an IP address as the stream pulling address:


1. Obtain the pull streaming address.

2. Resolve the IP address from the pull streaming address.

3. Associate the IP address with the domain name for stream pulling by calling [setUrlHostIP](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip):

   ```Java
   // Set the stream pulling address.
   mLivePlayer.setPlayUrl("https://pull.example.com/live/stream.flv");
   // Associate the IP address with the domain name for stream pulling.
   List<String> valueList = new ArrayList<>();
   valueList.add("xxx.xxx.xxx.xxx"); // Add the IP address.
   Map<String, List<String>> map = new HashMap<>();
   map.put("pull.example.com", valueList); // Replace "pull.example.com" with your domain name for stream pulling.
   
   // Set the mapping of domain names to server IP addresses.
   mLivePlayer.setUrlHostIP(map);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<span id="Setting multiple addresses for stream pulling"></span>
## Primary and backup streams

This feature is primarily utilized for ensuring disaster tolerance during live\-streaming events. If you set a primary and a backup stream address for the player, when the player fails to pull streaming from one address or if an error occurs during playback, the player automatically switches to the other address. The primary and the backup stream addresses can come from the same live\-streaming service provider or different providers.

Use the following steps to set a primary and a backup stream address:


1. Obtain a primary and a backup stream address. If you are using the live\-streaming service provided by BytePlus MediaLive, you can use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate the addresses.

2. Set the primary and the backup stream addresses by using the following code:

   ```Java
   // Set the primary stream address.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamMain = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamMain.url = "https://pull.example.com/live/primary.flv";
   playStreamMain.format = VeLivePlayerFormatFLV;
   playStreamMain.resolution = VeLivePlayerResolutionOrigin;
   playStreamMain.streamType = VeLivePlayerStreamTypeMain; // Set the stream type to primary.
   
   // Set the backup stream address.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamBackup = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamBackup.url = "https://pull.example.com/live/backup.flv";
   playStreamBackup.format = VeLivePlayerFormatFLV;
   playStreamBackup.resolution = VeLivePlayerResolutionOrigin;
   playStreamBackup.streamType = VeLivePlayerStreamTypeBackup; // Set the stream type to backup.
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Enable the player to switch between the primary and the backup stream addresses.
   streamData.enableMainBackupSwitch = true;
   
   // Add the primary stream address.
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamMain);
   
   // Add the backup stream address.
   streamData.backupStreamList = new ArrayList<>();
   streamData.backupStreamList.add(playStreamBackup);
   
   // Pass in the pull streaming configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. When the player switches between the primary and the backup stream addresses, the [onMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch) callback function will be triggered.

   ```Java
   public void onMainBackupSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStreamType streamType, VeLivePlayerError error) {
     // Triggered when a switch is complete.
   }
   ```
   


<span id="23c93996"></span>
## Resolution switching

You can set multiple pull streaming addresses with different resolutions and switch between these addresses during playback.

Use the following steps to enable resolution switching:


1. Obtain the pull streaming addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:

   1. [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

   2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) or call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) to generate the corresponding pull streaming addresses for the original and the transcoded streams.

2. Set the pull streaming addresses. The following addresses are used as examples in the sample code.

   
   |**Resolution** |**Pull streaming address** |
   |---|---|
   |Original (Origin) |https://pull.example.com/live/123456.flv |
   |Ultra high definition (UHD) |https://pull.example.com/live/123456_uhd.flv |
   |High definition (HD) |https://pull.example.com/live/123456_hd.flv |
   |Standard definition (SD) |https://pull.example.com/live/123456_sd.flv |
   |Low definition (LD) |https://pull.example.com/live/123456_ld.flv |
   

   ```Java
   // Set multiple pull streaming addresses with different resolutions.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrgin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrgin.url = "https://pull.example.com/live/123456.flv";
   playStreamOrgin.format = VeLivePlayerFormatFLV;
   playStreamOrgin.resolution = VeLivePlayerResolutionOrigin; // Original.
   playStreamOrgin.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv";
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD.
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv";
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD.
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD.
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD.
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add the pull streaming addresses.
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrgin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // Pass in the pull streaming configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. Call [switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) to change the resolution.

   ```Java
   mLivePlayer.switchResolution(VeLivePlayerResolutionUHD); // Switch to UHD.
   ```
   

4. When the switch is successful, the [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) callback function will be triggered.

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
     // Triggered when the resolution switch is complete.
   }
   ```
   


<span id="5b3ef3d2"></span>
## ABR stream pulling

Adaptive bitrate (ABR) is a streaming technology that uses algorithms to automatically switch between streams of different resolutions based on network conditions. This process minimizes playback stuttering and improves the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ABR stream pulling only applies to FLV streams.</div>


Use the following steps to enable ABR stream pulling:


1. Obtain the pull streaming addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:

   1. [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

   2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) or call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) to generate the corresponding pull streaming addresses for the original and the transcoded streams.

2. Set the pull streaming addresses. The following addresses are used as examples in the sample code.

   
   |**Resolution** |**Pull streaming address** |**Bitrate (Kbps)**  |
   |---|---|---|
   |Original (Origin) |https://pull.example.com/live/123456.flv |2500 |
   |Ultra high definition (UHD) |https://pull.example.com/live/123456_uhd.flv |2500 |
   |High definition (HD) |https://pull.example.com/live/123456_hd.flv |1000 |
   |Standard definition (SD) |https://pull.example.com/live/123456_sd.flv |800 |
   |Low definition (LD) |https://pull.example.com/live/123456_ld.flv |500 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The encoding bitrate for each address must be identical to the one specified in the transcoding configurations. For example, if you set the bitrate of the UHD stream to 2500 Kbps in the transcoding configurations, you must set the <code>playStreamUHD.bitrate</code> to <code>2500</code> in the code.   </div>
   

   ```Java
   // Set multiple pull streaming addresses with different resolutions.
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrgin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrgin.url = "https://pull.example.com/live/123456.flv";
   playStreamOrgin.format = VeLivePlayerFormatFLV;
   playStreamOrgin.resolution = VeLivePlayerResolutionOrigin; // Original.
   playStreamOrgin.streamType = VeLivePlayerStreamTypeMain;
   playStreamOrgin.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv";
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD.
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
    playStreamHD.url = "https://pull.example.com/live/123456_hd.flv";
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD.
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD.
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD.
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   playStreamLD.bitrate = 500;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add the pull streaming addresses.
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrgin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // Enable ABR.
   streamData.enableABR = true;
   
   // Pass in the pull streaming configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. When a resolution switch is complete, the [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) callback function will be triggered.

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
     // Triggered when a resolution switch is complete.
   }
   ```
   


<span id="756b5d71"></span>
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
   


<span id="34e237fb"></span>
## SEI

Supplemental enhancement information (SEI) is additional data embedded within a live stream. You can use SEI to transmit custom data or metadata.


1. Call [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablesei) before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) to enable the player to receive SEI messages.

   ```Java
   // Create a VeLivePlayerConfiguration instance.
   VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
   
   // Enable the player to receive SEI messages.
    config.enableSei = true;
           
   // Configure the initial settings of the player.
   mLivePlayer.setConfig(config);
   ```
   

2. When the live stream contains an SEI message, the [onReceiveSeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) callback is triggered, which contains the message.

   ```Java
   public void onReceiveSeiMessage(VeLivePlayer player, String message) 
     // Triggered when an SEI message is received.
   }
   ```
   


<span id="8b4f2be3"></span>
## Subscribing to video data

By subscribing to decoded video data, you can perform custom video processing and rendering. The Player SDK supports subscribing to video data in the following pixel formats and encapsulation formats:


|**Format** |**Enumeration** |**Description** |
|---|---|---|
|Pixel format<br><br>[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerpixelformat) |`VeLivePlayerPixelFormatRGBA32` |RGBA32 |
||`VeLivePlayerPixelFormatTexture` |2D Texture |
|Encapsulation format[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayervideobuffertype) |`VeLivePlayerVideoBufferTypeByteBuffer` |ByteBuffer |
||`VeLivePlayerVideoBufferTypeByteArray` |ByteArray |
||`VeLivePlayerVideoBufferTypeTexture` |Texture |


The supported combinations of pixel formats and encapsulation formats are shown in the table below:


|**Encapsulation format/Pixel format** |**VeLivePlayerPixelFormatRGBA32** |**VeLivePlayerPixelFormatTexture** |
|---|---|---|
|VeLivePlayerVideoBufferTypeByteBuffer |√ |× |
|VeLivePlayerVideoBufferTypeByteArray |√ |× |
|VeLivePlayerVideoBufferTypeTexture |× |√ (Optimal performance) |



1. Subscribe to video data by calling [enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver).

   ```Java
   mLivePlayer.enableVideoFrameObserver(true, VeLivePlayerPixelFormatRGBA32, VeLivePlayerVideoBufferTypeByteBuffer);
   ```
   

2. The [onRenderVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) callback function returns the decoded video data.

   ```Java
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
     // Returns decoded video data.
   }
   ```
   


<span id="2397b8f8"></span>
## Subscribing to audio data

By subscribing to decoded audio data, you can perform custom audio processing and rendering. The Player SDK supports subscribing to audio data in PCM Float32 sample format and ByteArray encapsulation format.


1. Subscribe to audio data by calling [enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver).

   ```Java
   mLivePlayer.enableAudioFrameObserver(true, true);
   ```
   

2. The [onRenderAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) callback function returns the decoded audio data.

   ```Java
   void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
     // Returns decoded audio data.
   }
   ```
   


<span id="84bd3b42"></span>
## Super\-resolution

Super\-resolution (SR) is a technology that reconstructs high\-resolution images from low\-resolution ones. Real\-time SR uses algorithms to reconstruct low\-resolution frames into high\-resolution ones in real time. This generates high\-resolution frames, which are then displayed on the screen. SR enhances video details and contrast, improving video clarity and the viewing experience.


1. Enable SR by calling [setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution).

2. If the SDK fails to enable SR, the [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) callback will be triggered.

   ```Java
   void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error);
   ```
   


Possible reasons for failure to enable SR include:


* The resolution of the original stream is higher than the maximum resolution supported by SR, which is 1300\*750.

* The frame rate of the original stream is higher than the maximum frame rate supported by SR, which is 30 fps.

* The client device does not support SR.


If you require support for higher resolutions or frame rates, contact [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).
