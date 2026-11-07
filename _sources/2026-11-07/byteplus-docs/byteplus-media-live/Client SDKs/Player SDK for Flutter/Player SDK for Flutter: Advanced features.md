---
title: "Player SDK for Flutter: Advanced features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features"
---

To enhance viewing experience in your app, this topic details how to implement advanced features of the Player SDK for Flutter. You can implement complex features as needed, according to actual business requirements.

<span id="dd785362"></span>
## Prerequisites


* You have integrated the basic features. For more information, see [Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features).

* To use the H.265 hardware and software decoding features, ensure you use a premium or trial license.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7">Upgrading a trial license to a basic or premium license</a>.   </div>
   

<span id="c955251c"></span>
## Configuring multiple streams

To use the primary and backup streams and adaptive bitrate (ABR) features, you must call this method to configure multiple streams for the player.

```Dart
Future<void> setPlayStreamData(VeLivePlayerStreamData streamData);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For type definitions, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#dfb9d282">VeLivePlayerStreamData</a>.</div>


<span id="97511097"></span>
## Using primary and backup streams

The primary and backup stream feature provides disaster recovery for live streaming. By configuring both a primary and a backup stream, the player can automatically switch between them if one fails. For example, if the primary stream fails, the player switches to the backup stream. You can use stream addresses from the same or different service providers.

<span id="fc2a7ac7"></span>
### Integration preparation

Get the primary and backup stream addresses. If you use the BytePlus MediaLive service, you can generate primary and backup stream addresses through the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) in the BytePlus MediaLive console.

<span id="83e07645"></span>
### Integration steps


1. Configure the primary and backup stream addresses for playback. The sample code is as follows.

   ```Java
   // Set the primary stream address.
   VeLivePlayerStream mainStream = VeLivePlayerStream(url: 'https://pull.example.com/live/主.flv');
   mainStream.format = VeLivePlayerFormat.flv;
   mainStream.resolution = VeLivePlayerResolution.origin;
   mainStream.type = VeLivePlayerStreamType.main;
   
   // Set the backup stream address.
   VeLivePlayerStream backupStream = VeLivePlayerStream(url: 'https://pull.example.com/live/备.flv');
   backupStream.format = VeLivePlayerFormat.flv;
   backupStream.resolution = VeLivePlayerResolution.origin;
   backupStream.type = VeLivePlayerStreamType.backup;
   
   // Create the playback source.
   VeLivePlayerStreamData streamData = VeLivePlayerStreamData();
   
   // Enable primary and backup stream switching.
   streamData.enableMainBackupSwitch = true;
   
   // Add the primary stream.
   streamData.mainStream = [mainStream];
   // Add the backup stream.
   streamData.backupStream = [backupStream];
   
   // Configure the playback source.
   manager.setPlayStreamData(streamData);
   
   // Start playback.
   manager.play();
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For type definitions, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#dfb9d282">VeLivePlayerStreamData</a> and <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd">VeLivePlayerStream</a>.   </div>
   

2. The `onMainBackupSwitch` callback from `VeLivePlayerObserver` notifies you when the player switches between primary and backup streams. The sample code is as follows.

   ```Dart
   // This callback is triggered when the primary and backup streams switch.
   VeLivePlayerObserver observer = VeLivePlayerObserver(onMainBackupSwitch: (VeLivePlayerStreamType streamType, VeLivePlayerError? error) {
         _addItem('onMainBackupSwitch: $streamType, error:$error');
       });
   manager.setObserver(observer);
   ```
   


<span id="ae69d1e9"></span>
## ABR stream pulling

ABR is a streaming technology that uses algorithms to automatically switch between streams of different resolutions based on network conditions. This process minimizes playback stuttering and improves the viewing experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The ABR feature only applies to FLV streams.</div>


<span id="c07520a7"></span>
### Integration preparation

Get the source stream and transcoded stream addresses for each resolution. If you use the BytePlus MediaLive service, first log in to the console and complete the [transcoding configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding). You can then get the pull stream address as follows:


* **For debugging**: You can use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to get the pull stream address.

* **For production**: Get the pull stream address by calling the API [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or using the [server SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk).


The integration steps in this topic use the following pull stream addresses as an example.


|Resolution |Pull stream address |Bitrate (kbps) |
|---|---|---|
|Source stream (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
|Ultra High Definition (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|High Definition (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
|Standard Definition (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
|Low Definition (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Ensure that the bitrate settings for each resolution are consistent with the bitrate configured in the <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding">transcoding configuration</a>.</div>


<span id="097e0679"></span>
### Integration steps


1. Configure stream addresses of different resolutions for playback. The sample code is as follows.

   ```Dart
   // Configure stream addresses of different resolutions.
   VeLivePlayerStream playStreamOrigin = VeLivePlayerStream(url: 'https://pull.example.com/live/123456.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.origin; // Original stream resolution.
   playStreamOrigin.type = VeLivePlayerStreamType.main; 
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream playStreamUHD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_uhd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.uhd; // UHD resolution.
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream playStreamHD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_hd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.hd; // HD resolution.
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 1000;
   
   VeLivePlayerStream playStreamSD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_sd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.sd; // SD resolution.
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 800;
   
   VeLivePlayerStream playStreamLD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_ld.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.ld; // LD resolution.
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 500;
   
   // Create the playback source.
   VeLivePlayerStreamData streamData = VeLivePlayerStreamData();
   
   // Add streams of different resolutions.
   List<VeLivePlayerStream> streamList = [];
   streamList.add(playStreamOrigin);
   streamList.add(playStreamUHD);
   streamList.add(playStreamHD);
   streamList.add(playStreamSD);
   streamList.add(playStreamLD);
   streamData.mainStream = streamList;
   
   // Configure the default resolution used when playback starts. In the following example, configure the default resolution to the original stream resolution.
   streamData.defaultResolution = VeLivePlayerResolution.origin;
   
   // Enable the ABR feature.
   streamData.enableABR = true;
   
   // Configure the playback source.
   manager.setPlayStreamData(streamData);
   
   // Start playback.
   manager.play();
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For type definitions, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#dfb9d282">VeLivePlayerStreamData</a> and <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd">VeLivePlayerStream</a>.   </div>
   

2. The `onResolutionSwitch` callback from `VeLivePlayerObserver` notifies you when the resolution switches automatically. The sample code is as follows.

   ```Dart
   VeLivePlayerObserver observer = VeLivePlayerObserver(onResolutionSwitch:
           (VeLivePlayerResolution resolution, VeLivePlayerError? error,
               VeLivePlayerResolutionSwitchReason reason) {
         print('onResolutionSwitch: $resolution');
       });
   manager.setObserver(observer);
   ```
