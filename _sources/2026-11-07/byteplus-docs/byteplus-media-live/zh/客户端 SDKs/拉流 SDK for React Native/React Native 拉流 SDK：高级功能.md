---
title: "React Native 拉流 SDK：高级功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rnplayer-advanced-features-zh-CN"
---

为提升应用中的观看体验，本文介绍如何实现 React Native 拉流 SDK 的高级功能。你可以根据实际业务需求实现复杂功能。

<span id="0410f60d"></span>
## 前提条件


* 你已按照 [iOS 拉流 SDK：基础功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3-zh-CN) 提供的说明实现了拉流 SDK 的基础功能。

* 如需使用以下功能，请确保使用高级或试用许可证。

   * H.265 硬件和软解

   * [超分辨率](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features-zh-CN#b0f80f88)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">试用许可证仅用于项目测试，无法续期。试用许可证过期后将导致鉴权失败，服务会中断。在项目上线前，请升级为正式许可证。更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management-zh-CN#777c7de7">将试用许可证升级为基础或高级许可证</a>。   </div>
   

<span id="f5462033"></span>
## 说明

由于拉流 SDK 使用了多种音视频 API，这些 API 在模拟器上可能无法正常工作，建议使用真实设备进行测试。

<span id="5c83d510"></span>
## RTM 拉流

此功能需配合 BytePlus MediaLive 提供的直播流服务使用。详情请参见 [实时媒体简介](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-real-time-media)。


1. 使用 [地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) 生成 RTM 拉流地址和 FLV 拉流地址。若 RTM 拉流失败，播放器会自动切换至 FLV 拉流。

2. 通过以下代码设置 RTM 地址和 FLV 地址：

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
## QUIC 拉流

此功能需配合 BytePlus MediaLive 提供的直播流服务使用。

按以下步骤使用 QUIC 协议进行拉流：


1. 使用 [地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) 生成 FLV 拉流地址。

2. 传入 FLV 拉流地址，并通过以下代码将拉流协议设置为 QUIC：

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
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若播放器使用 QUIC 协议拉流失败，会自动切换为 TCP 协议。   </div>
   

<span id="8a517a0b"></span>
## 使用 IP 地址进行拉流

播放器支持通过设置回放域名的 IP 地址进行拉流，可减少首帧时间。

按以下步骤使用 IP 地址进行拉流：


1. 获取直播流 URL 并解析 IP 地址。

2. 播放器使用指定的 IP 地址进行拉流。示例代码如下。

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
## 主流与备流

主流与备流功能为直播流提供容灾能力。通过配置主流和备流，播放器可在其中一个流故障时自动切换。例如，当主流故障时，播放器会切换至备流。你可以使用来自同一或不同服务商的流地址。

按以下步骤设置主流和备流地址：


1. 获取主流和备流地址。若使用 BytePlus MediaLive 提供的直播流服务，可通过 [地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) 生成地址。

2. 通过以下代码设置主流和备流地址：

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
   

3. 当播放器在主流和备流地址间切换时，会触发 [onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onmainbackupswitch) 回调函数。

   ```JavaScript
   mLivePlayer.setObserver('onMainBackupSwitch', event => {});
   ```
   


<span id="3276b5ea"></span>
## 分辨率切换

你可以设置多个不同分辨率的拉流地址，并在回放过程中切换这些地址。

按以下步骤启用分辨率切换：


1. 获取不同分辨率的拉流地址。若使用 BytePlus MediaLive 提供的直播流服务，请执行以下操作：

   1. [配置转码任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)以生成多路不同分辨率的转码流。

   2. 使用[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)或调用[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，为原始流和转码流生成对应的拉流地址。

2. 设置拉流地址。以下地址用于示例代码。

   
   |分辨率 |拉流地址 |
   |---|---|
   |原始（Origin） |https://pull.example.com/live/123456.flv |
   |超高清（UHD） |https://pull.example.com/live/123456_uhd.flv |
   |高清（HD） |https://pull.example.com/live/123456_hd.flv |
   |标清（SD） |https://pull.example.com/live/123456_sd.flv |
   |低清（LD） |https://pull.example.com/live/123456_ld.flv |
   

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
   

3. 调用[switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#switchresolution)以切换分辨率。

   ```Python
   mLivePlayer.switchResolution(VeLivePlayerResolution.VeLivePlayerResolutionUHD); // Switch to UHD.
   ```
   

4. 切换成功后，将触发[onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onresolutionswitch)回调函数。

   ```JavaScript
   mLivePlayer.setObserver('onResolutionSwitch', () => {});
   ```
   


<span id="1ada31f7"></span>
## 自适应码率拉流

自适应码率（ABR）是一种流媒体技术，通过算法根据网络状况自动切换不同分辨率的流。此过程可最大程度减少回放卡顿并提升观看体验。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ABR 拉流仅适用于 FLV 流。</div>


使用以下步骤启用自适应码率拉流：


1. 获取不同分辨率的拉流地址。如果你使用的是 BytePlus MediaLive 提供的直播流服务，请执行以下操作：

   1. [配置转码任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)以生成多路不同分辨率的转码流。

   2. 使用[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)或调用[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，为原始流和转码流生成对应的拉流地址。

2. 设置拉流地址。以下地址用于示例代码。

   
   |**分辨率** |**拉流地址** |**码率（Kbps）**  |
   |---|---|---|
   |原始（Origin） |https://pull.example.com/live/123456.flv |2500 |
   |超高清（UHD） |https://pull.example.com/live/123456_uhd.flv |2500 |
   |高清（HD） |https://pull.example.com/live/123456_hd.flv |1000 |
   |标清（SD） |https://pull.example.com/live/123456_sd.flv |800 |
   |低清（LD） |https://pull.example.com/live/123456_ld.flv |500 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">每个地址的编码码率必须与转码配置中指定的码率一致。例如，如果在转码配置中将 UHD 流的码率设置为 2500 Kbps，则必须在 <code>playStreamUHD.bitrate</code> 中设置为 <code>2500</code>。   </div>
   

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
   

3. 分辨率切换完成后，将触发[onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onresolutionswitch)回调函数。

   ```JavaScript
   mLivePlayer.setObserver('onResolutionSwitch', () => {});
   ```
   


<span id="dd3af7d9"></span>
## SEI

补充增强信息（SEI）是嵌入在直播流中的附加数据。你可以使用 SEI 传输自定义数据或元数据。


1. 在播放器初始化期间，可以通过配置播放器的 enableSei 属性来启用 SEI 信息接收。

   ```JavaScript
   // Create a player initialization configuration
   initPlayer({
     enableSei: true, // Enable receiving SEI messages.
     ...
   })
   ```
   

2. 当直播流包含 SEI 消息时，将触发[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onreceiveseimessage)回调并提供该消息。

   ```JavaScript
   mLivePlayer.setObserver('onReceiveSeiMessage', seiMessage => {
     // processing received SEI messages
   });
   ```
   


<span id="b0f80f88"></span>
## 超分辨率

超分辨率（SR）是一项将低分辨率图像重建为高分辨率图像的技术。客户端实时 SR 利用算法在客户端设备上对低分辨率帧进行实时重建。这样会生成高分辨率帧，并显示在屏幕上。SR 可增强视频细节和对比度，提升视频清晰度和观看体验。


1. 使用前请联系 BytePlus[技术支持](https://www.byteplus.com/en/support)开通该功能。

2. 通过调用[setEnableSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setenablesuperresolution)启用 SR。默认值为`false`。

   
   |参数 |类型 |接口行为 |
   |---|---|---|
   |enable |boolean |是否启用超分辨率功能。 |
   

3. 若 SDK 启用 SR 失败，将触发[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onstreamfailedopensuperresolution)回调。

   ```JavaScript
   mLivePlayer.setObserver('onStreamFailedOpenSuperResolution', () => {});
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SR 可能无法启用，原因如下：</div>



* <div data-tips="true" data-tips-type="tip">原始流的分辨率高于 SR 支持的最大分辨率（1300\*750）。</div>


* <div data-tips="true" data-tips-type="tip">原始流的帧率高于 SR 支持的最大帧率（30 fps）。</div>


* <div data-tips="true" data-tips-type="tip">客户端设备不支持 SR。</div>



<div data-tips="true" data-tips-type="tip">若最大分辨率和帧率无法满足您的业务需求，请联系 BytePlus 技术支持。</div>


<span id="7074e732"></span>
## 画中画

画中画（PiP）允许用户在悬浮窗中继续观看视频，同时与其他应用交互，实现多任务处理。该功能支持具备原生 PiP 能力的 Android 和 iOS 系统。

<span id="f8c90919"></span>
### Step 1: Configure iOS permissions

要在 iOS 上启用 PiP，必须在 Xcode 中配置必要权限：


1. 在 Xcode 中打开你的项目并选择目标。

2. 前往**Signing & Capabilities**标签页。

3. 点击\*\*+ Capability\*\*，然后添加**Background Modes**。

4. 启用**Audio, AirPlay, and Picture in Picture**选项。


<span id="b7f3f8d3"></span>
### Step 2: Start Picture\-in\-Picture mode

视频播放时，调用`startPictureInPicture`方法进入 PiP 模式：

```TypeScript
startPictureInPicture(aspectRatio?: number, x?: number, y?: number): Promise<void>
```



* 在**Android**上，你可以传递可选参数以控制视频长宽比和 PiP 窗口的初始位置。

* 在**iOS**上，无需参数。系统会自动确定 PiP 窗口的大小和位置。


<span id="171026db"></span>
### Step 3: Manage background behavior on iOS

若要在应用进入后台时（仅限 iOS），让播放器进入 PiP 模式，请在播放器处于播放状态**时按以下步骤操作**：


1. 调用 `enablePictureInPicture` 以启用 PiP 功能。

2. 然后调用 `startPictureInPicture` 以进入 PiP 模式。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若需阻止应用在切换到后台时自动启动 PiP，请调用 disablePictureInPicture。</div>


<span id="6482915f"></span>
### Step 4: 监听 PiP 事件

使用 `setPictureInPictureListener` 方法监听与 PiP 相关的事件，例如进入、退出、点击悬浮窗或发生错误。

示例：

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
