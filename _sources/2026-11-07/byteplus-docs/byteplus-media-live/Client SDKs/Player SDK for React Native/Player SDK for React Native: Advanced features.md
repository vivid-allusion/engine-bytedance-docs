---
title: "Player SDK for React Native: Advanced features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rnplayer-advanced-features"
---

To enhance viewing experience in your app, this topic details how to implement advanced features of the Player SDK for React Native. You can implement complex features as needed, according to actual business requirements.

<span id="0410f60d"></span>
## Prerequisites


* You have implemented the basic features of the Player SDK by following the instructions provided in [Player SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3).

* To use the following features, ensure you use a premium or trial license.

   * H.265 hardware and software decoding

   * [Super-resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features#b0f80f88)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7">Upgrading a trial license to a basic or premium license</a>.   </div>
   

<span id="f5462033"></span>
## Notes

Because the Player SDK uses various audio and video APIs that may not work properly on simulators, we recommend that you use a physical device for testing.

<span id="5c83d510"></span>
## RTM stream pulling

This feature should be used in conjunction with the live\-streaming service provided by BytePlus MediaLive. For details, refer to [Introduction to Real Time Media](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-real-time-media).


1. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate an RTM pull stream address and an FLV pull stream address. If RTM stream pulling fails, the player will automatically switch to FLV stream pulling.

2. Set the RTM address and the FLV address with the following code:

   ```JavaScript
   // Set the RTM address.
   const playStreamRTM = new VeLivePlayerStream();
   playStreamRTM.url = 'https://pull.example.com/live/stream.sdp';
   playStreamRTM.format = VeLivePlayerFormat.VeLivePlayerFormatRTM;
   playStreamRTM.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamRTM.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Set the FLV address.
   const playStreamFLV = new VeLivePlayerStream();
   playStreamFLV.url = 'https://pull.example.com/live/stream.flv';
   playStreamFLV.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamFLV.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamFLV.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   const mainStreamList = [];
   
   // Add the RTM stream address.
   mainStreamList.push(playStreamRTM);
   
   // Add the FLV stream address.
   mainStreamList.push(playStreamFLV);
   
   // Set the default format and protocol.
   streamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatRTM;
   streamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<span id="aa70c92b"></span>
## QUIC stream pulling

This feature should be used in conjunction with the live\-streaming service provided by BytePlus MediaLive.

Use the following steps to pull a stream using the QUIC protocol:


1. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate an FLV pull stream address.

2. Pass in the FLV pull stream address and set the streaming protocol to QUIC by using the following code:

   ```JavaScript
   // Set the FLV address.
   const playStreamFLV = new VeLivePlayerStream();
   playStreamFLV.url = 'https://pull.example.com/live/stream.flv';
   playStreamFLV.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamFLV.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamFLV.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   const mainStreamList = [];
   
   // Add the FLV stream address.
   mainStreamList.push(playStreamFLV);
   
   // Set the default format and protocol.
   streamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   streamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolQUIC; // Use QUIC protocol
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The player automatically switches to the TCP protocol if it fails to pull the stream using the QUIC protocol.   </div>
   

<span id="8a517a0b"></span>
## Using an IP address for stream pulling

The player supports pull streaming by setting the playback domain's IP address, reducing the time to first frame.

Use the following steps to pull a stream using the IP Address:


1. Obtain the live streaming URL and resolve the IP address.

2. The player uses the specific IP address to pull the stream. The sample code is as follows.

   ```JavaScript
   // Set Playback URL
   mLivePlayer.setPlayUrl('https://pull.example.com/live/stream.flv');
   // Add IP Address and Domain name association
   const valueList = [];
   valueList.push('xxx.xxx.xxx.xxx'); // IP Address
   const map = {};
   map['pull.example.com'] = valueList;
   
   // Set IP Address
   mLivePlayer.setUrlHostIP(map);
   
   // Start playback
   mLivePlayer.play();
   ```
   


<span id="a95a61a8"></span>
## Primary and backup streams

The primary and backup stream feature provides disaster recovery for live streaming. By configuring both a primary and a backup stream, the player can automatically switch between them if one fails. For example, if the primary stream fails, the player switches to the backup stream. You can use stream addresses from the same or different service providers.

Use the following steps to set a primary and a backup stream address:


1. Obtain a primary and a backup stream address. If you are using the live\-streaming service provided by BytePlus MediaLive, you can use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate the addresses.

2. Set the primary and the backup stream addresses by using the following code:

   ```JavaScript
   // Set the primary stream address.
   const playStreamMain = new VeLivePlayerStream();
   playStreamMain.url = 'https://pull.example.com/live/main.flv';
   playStreamMain.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamMain.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamMain.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain; // Set the stream type to primary.
   
   // Set the backup stream address.
   const playStreamBackup = new VeLivePlayerStream();
   playStreamBackup.url = 'https://pull.example.com/live/backup.flv';
   playStreamBackup.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamBackup.resolution =
     VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamBackup.streamType =
     VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup; // Set the stream type to backup.
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   
   // Enable automatic switching between primary and backup streams.
   streamData.enableMainBackupSwitch = true;
   
   // Add the primary stream.
   const mainStreamList = [];
   mainStreamList.push(playStreamMain);
   
   // Add the backup stream.
   const backupStreamList = [];
   backupStreamList.push(playStreamBackup);
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. When the player switches between the primary and the backup stream addresses, the [onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onmainbackupswitch) callback function will be triggered.

   ```JavaScript
   mLivePlayer.setObserver('onMainBackupSwitch', event => {});
   ```
   


<span id="3276b5ea"></span>
## Resolution switching

You can set multiple pull stream addresses with different resolutions and switch between these addresses during playback.

Use the following steps to enable resolution switching:


1. Obtain the pull stream addresses of different resolutions. If you are using the live\-streaming service provided by BytePlus MediaLive, do the following:

   1. [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) to generate multiple transcoded streams of different resolutions.

   2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) or call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) to generate the corresponding pull stream addresses for the original and the transcoded streams.

2. Set the pull stream addresses. The following addresses are used as examples in the sample code.

   
   |Resolution |Pull stream address |
   |---|---|
   |Original (Origin) |https://pull.example.com/live/123456.flv |
   |Ultra high definition (UHD) |https://pull.example.com/live/123456_uhd.flv |
   |High definition (HD) |https://pull.example.com/live/123456_hd.flv |
   |Standard definition (SD) |https://pull.example.com/live/123456_sd.flv |
   |Low definition (LD) |https://pull.example.com/live/123456_ld.flv |
   

   ```JavaScript
   // Set multiple pull stream addresses with different resolutions.
   const playStreamOrgin = new VeLivePlayerStream();
   playStreamOrgin.url = "https://pull.example.com/live/123456.flv";
   playStreamOrgin.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamOrgin.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin; // Original.
   playStreamOrgin.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   const playStreamUHD = new VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv";
   playStreamUHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamUHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionUHD; // UHD.
   playStreamUHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv";
   playStreamHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionHD; // HD.
   playStreamHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";
   playStreamSD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamSD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionSD; // SD.
   playStreamSD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";
   playStreamLD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamLD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionLD; // LD.
   playStreamLD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add the pull stream addresses.
   const mainStreamList = [];
   mainStreamList.push(playStreamOrgin);
   mainStreamList.push(playStreamUHD);
   mainStreamList.push(playStreamHD);
   mainStreamList.push(playStreamSD);
   mainStreamList.push(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. Call [switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#switchresolution) to change the resolution.

   ```Python
   mLivePlayer.switchResolution(VeLivePlayerResolution.VeLivePlayerResolutionUHD); // Switch to UHD.
   ```
   

4. When the switch is successful, the [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onresolutionswitch) callback function will be triggered.

   ```JavaScript
   mLivePlayer.setObserver('onResolutionSwitch', () => {});
   ```
   


<span id="1ada31f7"></span>
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
   |Original (Orgin) |https://pull.example.com/live/123456.flv |2500 |
   |Ultra high definition (UHD) |https://pull.example.com/live/123456_uhd.flv |2500 |
   |High definition (HD) |https://pull.example.com/live/123456_hd.flv |1000 |
   |Standard definition (SD) |https://pull.example.com/live/123456_sd.flv |800 |
   |Low definition (LD) |https://pull.example.com/live/123456_ld.flv |500 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The encoding bitrate for each address must be identical to the one specified in the transcoding configurations. For example, if you set the bitrate of the UHD stream to 2500 Kbps in the transcoding configurations, you must set the <code>playStreamUHD.bitrate</code> to <code>2500</code> in the code.   </div>
   

   ```JavaScript
   // Set multiple pull stream addresses with different resolutions.
   const playStreamOrgin = new VeLivePlayerStream();
   playStreamOrgin.url = 'https://pull.example.com/live/123456.flv';
   playStreamOrgin.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamOrgin.resolution =
     VeLivePlayerResolution.VeLivePlayerResolutionOrigin; // Original.
   playStreamOrgin.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamOrgin.bitrate = 2500; // The bitrate must be consistent with the transcoding configurations.
   
   const playStreamUHD = new VeLivePlayerStream();
   playStreamUHD.url = 'https://pull.example.com/live/123456_uhd.flv';
   playStreamUHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamUHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionUHD; // UHD.
   playStreamUHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamUHD.bitrate = 2500;
   
   const playStreamHD = new VeLivePlayerStream();
   playStreamHD.url = 'https://pull.example.com/live/123456_hd.flv';
   playStreamHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionHD; // HD.
   playStreamHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamHD.bitrate = 1000;
   
   const playStreamSD = new VeLivePlayerStream();
   playStreamSD.url = 'https://pull.example.com/live/123456_sd.flv';
   playStreamSD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamSD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionSD; // SD.
   playStreamSD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamSD.bitrate = 800;
   
   const playStreamLD = new VeLivePlayerStream();
   playStreamLD.url = 'https://pull.example.com/live/123456_ld.flv';
   playStreamLD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamLD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionLD; // LD.
   playStreamLD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamLD.bitrate = 500;
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   
   // Add the pull stream addresses.
   const mainStreamList = [];
   mainStreamList.push(playStreamOrgin);
   mainStreamList.push(playStreamUHD);
   mainStreamList.push(playStreamHD);
   mainStreamList.push(playStreamSD);
   mainStreamList.push(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution =
     VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   
   // Enable ABR.
   streamData.enableABR = true;
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. When a resolution switch is complete, the [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onresolutionswitch) callback function will be triggered.

   ```JavaScript
   mLivePlayer.setObserver('onResolutionSwitch', () => {});
   ```
   


<span id="dd3af7d9"></span>
## SEI

Supplemental enhancement information (SEI) is additional data embedded within a live stream. You can use SEI to transmit custom data or metadata.


1. During the initialization of the player, you can enable the receiving of SEI information by configuring the enableSei property of the player.

   ```JavaScript
   // Create a player initialization configuration
   initPlayer({
     enableSei: true, // Enable receiving SEI messages.
     ...
   })
   ```
   

2. When the live stream contains an SEI message, the [onReceiveSeiMessage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onreceiveseimessage) callback is triggered, providing the message.

   ```JavaScript
   mLivePlayer.setObserver('onReceiveSeiMessage', seiMessage => {
     // processing received SEI messages
   });
   ```
   


<span id="b0f80f88"></span>
## Super\-resolution

Super\-resolution (SR) is a technology that reconstructs low\-resolution images into high\-resolution ones. Real\-time SR on the client side uses algorithms to perform real\-time reconstruction of low\-resolution frames on client devices. This generates high\-resolution frames, which are then displayed on the screen. SR enhances video details and contrast, improving video clarity and the viewing experience.


1. Contact BytePlus [technical support](https://www.byteplus.com/en/support) to activate the feature before using it.

2. Enable SR by calling [setEnableSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setenablesuperresolution). The default value is `false`.

   
   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable the super\-resolution function. |
   

3. If the SDK fails to enable SR, the [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onstreamfailedopensuperresolution) callback will be triggered.

   ```JavaScript
   mLivePlayer.setObserver('onStreamFailedOpenSuperResolution', () => {});
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SR might fail to enable for the following reasons:</div>



* <div data-tips="true" data-tips-type="tip">The resolution of the original stream is higher than the maximum resolution supported by SR, which is 1300\*750.</div>


* <div data-tips="true" data-tips-type="tip">The frame rate of the original stream is higher than the maximum frame rate supported by SR, which is 30 fps.</div>


* <div data-tips="true" data-tips-type="tip">The client device does not support SR.</div>



<div data-tips="true" data-tips-type="tip">Please contact BytePlus technical support if the maximum resolution and frame rate do not meet your business requirements.</div>


<span id="7074e732"></span>
## Picture\-in\-Picture

Picture\-in\-Picture (PiP) allows users to continue watching a video in a floating window while interacting with other apps, enabling multitasking. This feature is supported on Android and iOS systems that provide native PiP capabilities.

<span id="f8c90919"></span>
### Step 1: Configure iOS permissions

To enable PiP on iOS, you must configure the necessary permissions in Xcode:


1. Open your project in Xcode and select the target.

2. Go to the **Signing & Capabilities** tab.

3. Click  **+ Capability**, then add **Background Modes**.

4. Enable the option **Audio, AirPlay, and Picture in Picture**.


<span id="b7f3f8d3"></span>
### Step 2: Start Picture\-in\-Picture mode

While the video is playing, call the `startPictureInPicture` method to enter PiP mode:

```TypeScript
startPictureInPicture(aspectRatio?: number, x?: number, y?: number): Promise<void>
```



* On **Android**, you can pass optional parameters to control the aspect ratio and the initial position of the PiP window.

* On **iOS**, parameters are not required. The system automatically determines the size and position of the PiP window.


<span id="171026db"></span>
### Step 3: Manage background behavior on iOS

If you want the player to enter PiP mode when the app goes into the background (iOS only), follow these steps **while the player is in a playing state**:


1. Call `enablePictureInPicture` to enable PiP capability.

2. Then call `startPictureInPicture` to enter PiP mode.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to prevent PiP from starting automatically when the app moves to the background, call disablePictureInPicture instead.</div>


<span id="6482915f"></span>
### Step 4: Listen for PiP events

Use the `setPictureInPictureListener` method to listen for PiP\-related events such as entering, exiting, clicking the floating window, or encountering an error.

Example:

```JavaScript
playerRef.current?.setPictureInPictureListener({
  onStartPictureInPicture: () => {
    addLog('onStartPictureInPicture');
  },
  onStopPictureInPicture: () => {
    addLog('onStopPictureInPicture');
    if (AppState.currentState !== 'active') {
      playerRef.current?.stop();
    }
    manualPip.current = false;
  },
  onClickPictureInPicture: () => {
    addLog('onClickPictureInPicture');
  },
  onError: errorCode => {
    addLog('onError' + errorCode);
  },
});
```
