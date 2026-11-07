---
title: "Player SDK for Flutter：高级功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features-zh-CN"
---

为提升应用中的观看体验，本文介绍如何实现 Player SDK for Flutter 的高级功能。你可以根据实际业务需求，按需实现复杂功能。

## 前提条件

* 你已集成基础功能。更多信息，请参见 [Player SDK for Flutter：基础功能](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features)。

* 如需使用 H.265 硬解码和软解码功能，请确保使用高级版或试用版许可证。

   > **注意**

   > 试用版许可证仅用于项目测试，且无法续期。试用版许可证过期会导致鉴权失败，从而中断服务。请在项目上线前升级到正式版许可证。更多信息，请参见[将试用版许可证升级为基础版或高级版许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

## 配置多路流

如需使用主备流和自适应码率（ABR）功能，必须调用此方法为播放器配置多路流。

```Dart
Future<void> setPlayStreamData(VeLivePlayerStreamData streamData);
```

> **说明**

> 类型定义请参见 [VeLivePlayerStreamData](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#dfb9d282)。

## 使用主备流

主备流功能为直播提供灾备能力。通过同时配置主流和备流，播放器可在其中一路流失败时自动切换。例如，主流失败时，播放器会切换到备流。你可以使用来自相同或不同服务提供商的流地址。

### 集成准备

获取主备流地址。如果你使用 BytePlus MediaLive 服务，可以通过 BytePlus MediaLive 控制台中的[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)生成主备流地址。

### 集成步骤

1. 为播放配置主备流地址。示例代码如下。

   ```Java
   // 设置主流地址。
   VeLivePlayerStream mainStream = VeLivePlayerStream(url: 'https://pull.example.com/live/主.flv');
   mainStream.format = VeLivePlayerFormat.flv;
   mainStream.resolution = VeLivePlayerResolution.origin;
   mainStream.type = VeLivePlayerStreamType.main;
   
   // 设置备流地址。
   VeLivePlayerStream backupStream = VeLivePlayerStream(url: 'https://pull.example.com/live/备.flv');
   backupStream.format = VeLivePlayerFormat.flv;
   backupStream.resolution = VeLivePlayerResolution.origin;
   backupStream.type = VeLivePlayerStreamType.backup;
   
   // 创建播放源。
   VeLivePlayerStreamData streamData = VeLivePlayerStreamData();
   
   // 开启主备流切换。
   streamData.enableMainBackupSwitch = true;
   
   // 添加主流。
   streamData.mainStream = [mainStream];
   // 添加备流。
   streamData.backupStream = [backupStream];
   
   // 配置播放源。
   manager.setPlayStreamData(streamData);
   
   // 开始播放。
   manager.play();
   ```

   > **说明**

   > 类型定义请参见 [VeLivePlayerStreamData](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#dfb9d282) 和 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd)。

2. `VeLivePlayerObserver` 中的 `onMainBackupSwitch` 回调会在播放器切换主备流时通知你。示例代码如下。

   ```Dart
   // 此回调会在主备流切换时触发。
   VeLivePlayerObserver observer = VeLivePlayerObserver(onMainBackupSwitch: (VeLivePlayerStreamType streamType, VeLivePlayerError? error) {
         _addItem('onMainBackupSwitch: $streamType, error:$error');
       });
   manager.setObserver(observer);
   ```

## ABR 拉流

ABR 是一种流媒体技术，可根据网络状况使用算法在不同分辨率的流之间自动切换。此过程可最大限度减少播放卡顿，并提升观看体验。

> **说明**

> ABR 功能仅适用于 FLV 流。

### 集成准备

获取每个分辨率的源流和转码流地址。如果你使用 BytePlus MediaLive 服务，请先登录控制台并完成[转码配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding)。然后可以按如下方式获取拉流地址：

* **用于调试**：你可以使用[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)获取拉流地址。

* **用于生产**：通过调用 API [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk)获取拉流地址。

本文中的集成步骤使用以下拉流地址作为示例。

|分辨率 |拉流地址 |码率（kbps） |
|---|---|---|
|源流（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高清（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|标清（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|低清（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

> **注意**

> 请确保每个分辨率的码率设置与[转码配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding)中配置的码率一致。

### 集成步骤

1. 为播放配置不同分辨率的流地址。示例代码如下。

   ```Dart
   // 配置不同分辨率的流地址。
   VeLivePlayerStream playStreamOrigin = VeLivePlayerStream(url: 'https://pull.example.com/live/123456.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.origin; // 原始流分辨率。
   playStreamOrigin.type = VeLivePlayerStreamType.main; 
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream playStreamUHD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_uhd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.uhd; // UHD 分辨率。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream playStreamHD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_hd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.hd; // HD 分辨率。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 1000;
   
   VeLivePlayerStream playStreamSD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_sd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.sd; // SD 分辨率。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 800;
   
   VeLivePlayerStream playStreamLD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_ld.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.ld; // LD 分辨率。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 500;
   
   // 创建播放源。
   VeLivePlayerStreamData streamData = VeLivePlayerStreamData();
   
   // 添加不同分辨率的流。
   List<VeLivePlayerStream> streamList = [];
   streamList.add(playStreamOrigin);
   streamList.add(playStreamUHD);
   streamList.add(playStreamHD);
   streamList.add(playStreamSD);
   streamList.add(playStreamLD);
   streamData.mainStream = streamList;
   
   // 配置播放开始时使用的默认分辨率。在以下示例中，将默认分辨率配置为原始流分辨率。
   streamData.defaultResolution = VeLivePlayerResolution.origin;
   
   // 开启 ABR 功能。
   streamData.enableABR = true;
   
   // 配置播放源。
   manager.setPlayStreamData(streamData);
   
   // 开始播放。
   manager.play();
   ```

   > **说明**

   > 类型定义请参见 [VeLivePlayerStreamData](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#dfb9d282) 和 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd)。

2. `VeLivePlayerObserver` 中的 `onResolutionSwitch` 回调会在分辨率自动切换时通知你。示例代码如下。

   ```Dart
   VeLivePlayerObserver observer = VeLivePlayerObserver(onResolutionSwitch:
           (VeLivePlayerResolution resolution, VeLivePlayerError? error,
               VeLivePlayerResolutionSwitchReason reason) {
         print('onResolutionSwitch: $resolution');
       });
   manager.setObserver(observer);
   ```
