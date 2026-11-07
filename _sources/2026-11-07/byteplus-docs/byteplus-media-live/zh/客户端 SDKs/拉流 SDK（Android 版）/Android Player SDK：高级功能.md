---
title: "Android Player SDK：高级功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2-zh-CN"
---

为提升 Android 应用中的观看体验，本文介绍如何实现 Android Player SDK 的高级功能。你可以根据实际业务需求按需实现复杂功能。

## 前提条件

* 你已按照 [Android Player SDK：基础功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2) 中的说明实现 Player SDK 的基础功能。

* 如需使用以下功能，请确保使用高级版或试用版 License。

   * [播放 RTM 流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#af29cf39)

   * [QUIC 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#4d503d05)

   * [播放 CMAF 流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#915c6bb1)

   * [播放低延迟 FLV 流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#1d5784e5)

   * [主备流切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#77618e0b)

   * [ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#34e237fb)

   * [超分](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#84bd3b42)

   * [H.265 硬件解码和软件解码](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#3ca5b85e)

   * [H.266 软件解码](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#71012b84)

   * [视频锐化](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#15a71a29)

   * 商业 DRM（数字版权管理）

   > **警告**

   > 试用版 License 仅用于项目测试，且不可续期。试用版 License 过期会导致鉴权失败，从而中断服务。请在项目上线前升级为正式 License。更多信息，请参见[将试用版 License 升级为基础版或高级版 License](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

## 注意事项

由于 Player SDK 使用了多种 Android 音视频 API，而这些 API 在模拟器上可能无法正常工作，因此建议使用真机进行测试。

## 流降级策略和主备流切换

如果仅配置一个拉流地址，当该地址因网络问题或其他异常不可用时，播放可能会卡顿甚至失败。为降低单个地址异常导致播放失败的风险，你可以为一次播放会话配置多个拉流地址，并根据需要选择以下配置方式之一：

* **流降级策略**：当你希望播放器按优先级自动尝试多个拉流地址时使用。你可以为每个地址配置优先级和最大重试次数。播放器会优先尝试高优先级地址。如果某个地址在所有重试次数耗尽后仍不可用，播放器会切换到下一个优先级的地址。

* **主备流切换**：当你的应用维护独立的主流列表和备流列表时使用。播放器会先按流降级策略尝试主流列表中的流。仅当主流列表中的所有地址均失败后，播放器才会自动切换到备流列表并继续尝试。

> **说明**

> 仅高级版和试用版 License 支持主备流切换。所有 License 类型均支持流降级策略。

* 流降级策略

   主流或备流列表中的播放顺序如下：

   1. **播放最高优先级的流**：播放器会根据你设置的 `priority`，从当前列表中的最高优先级到最低优先级依次尝试播放流。

   2. **失败后重试**：如果当前流播放失败，播放器会根据该流的 `retryMaxCount` 重试。

   3. **切换到降级流**：如果所有重试次数耗尽后播放仍失败，播放器会放弃当前流，并尝试当前列表中下一个较高优先级的流。

* 主备流切换

   启用主备流切换后，播放器会按以下顺序尝试流：

   1. **播放主流**：播放器首先尝试播放主流列表中的流。

   2. **切换到备流**：如果主流列表中的所有流均播放失败，播放器会尝试播放备流列表中的流。

   3. **播放失败**：如果备流列表中的所有流也播放失败，则播放失败。

在此过程中，SDK 会通过以下回调通知当前状态：

* [onInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-oninfo)：当某个流播放失败但仍存在其他可用流时触发。你可以使用此回调获取详细错误信息，以便调试。

* [onStreamFormatSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch)：当播放器切换流格式时触发，例如从 RTM 切换到 FLV。

* [onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch)：当主流列表中的所有流均播放失败，且播放器成功切换到备流列表时触发。

* [onError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onerror)：当主流和备流列表中的所有流均播放失败，且播放最终结束时触发。

### 前提条件

通过以下任一方式获取 RTM、FLV 等协议的拉流地址。同一列表内的降级顺序由每个拉流地址的优先级决定。

* **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

* **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

### 操作步骤

#### 步骤 1：配置降级策略

你可以通过配置 `VeLivePlayerStream` 的 [priority](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-priority) 和 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount) 自定义降级策略。

* `priority`：流的优先级。取值必须为 `0`（默认值）或正整数。**值越大，优先级越高**。播放器会优先尝试播放高优先级流。

   > **说明**

   > 主流列表和备流列表的优先级独立计算，互不影响。

* `retryMaxCount`：该流的最大播放尝试次数，包括首次尝试。例如，取值为 `3` 时，首次播放失败后，播放器最多再重试 2 次。有效取值：

   * `-1`（默认值）：使用 `VeLivePlayerConfiguration` 中 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) 的值。

   * `0`：不尝试播放该流。

   * `>0`：最大播放尝试次数。

**流降级策略**

以下代码示例演示基本流降级场景，播放顺序如下：

1. 首先，播放器尝试播放 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器降级到 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，播放结束。

```Java
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 添加 FLV 主流作为降级流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 配置播放源。
mLivePlayer.setPlayStreamData(streamData);

// 开始播放。
mLivePlayer.play();
```

**流降级策略 + 主备流切换**

以下代码示例演示将流降级策略与主备流切换结合的场景，播放顺序如下：

1. 首先，播放器尝试播放主流列表中的 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器降级到主流列表中的 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，播放器切换到备流列表，并尝试播放 RTM 流（优先级 5），最多尝试 3 次。

4. 如果失败，播放器降级到备流列表中的 FLV 流（优先级 4），最多尝试 3 次。

5. 如果这些尝试全部失败，播放结束。

```Java
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 添加 FLV 主流作为降级流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 配置备流列表。
List<VeLivePlayerStreamData.VeLivePlayerStream> backupStreams = new ArrayList<>();
// 添加 RTM 备流。
VeLivePlayerStreamData.VeLivePlayerStream rtmBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmBackupStream.url = "https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 备流列表中的最高优先级。
backupStreams.add(rtmBackupStream);

// 添加 FLV 备流作为降级流。
VeLivePlayerStreamData.VeLivePlayerStream flvBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvBackupStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
backupStreams.add(flvBackupStream);
streamData.backupStreamList = backupStreams;

// 启用主备流切换。
streamData.enableMainBackupSwitch = true;

// 配置播放源。
mLivePlayer.setPlayStreamData(streamData);

// 开始播放。
mLivePlayer.play();
```

**多画质流降级策略**

流降级策略支持为[清晰度切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#23c93996)、[ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2)（仅 FLV 流）和[平滑画质切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#d7282079)使用的多画质流配置降级流。配置时，将同一多画质流组中的流设置为相同的 `priority` 值。播放器会先从最高 `priority` 到最低 `priority` 选择流组。如果高优先级多画质流播放失败，播放器会降级到低优先级流。

在以下示例中，播放器先播放 `priority` 为 `5` 的 ABR 多画质流。如果 ABR 多画质流播放失败，播放器会降级到 `priority` 为 `4` 的普通 FLV 流。

```Java
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 添加 ABR 多画质流的原画画质。优先级为 5。
VeLivePlayerStreamData.VeLivePlayerStream flvOriginStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvOriginStream.url = "https://xxx_origin.flv"; // 替换为原画画质的实际 FLV 拉流地址。
flvOriginStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvOriginStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvOriginStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvOriginStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 原画画质。
flvOriginStream.bitrate = 2000;
flvOriginStream.retryMaxCount = 3;
flvOriginStream.priority = 5;
mainStreams.add(flvOriginStream);

// 添加 ABR 多画质流的超高清画质。优先级为 5。
VeLivePlayerStreamData.VeLivePlayerStream flvUHDStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvUHDStream.url = "https://xxx_uhd.flv"; // 替换为超高清画质的实际 FLV 拉流地址。
flvUHDStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvUHDStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvUHDStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvUHDStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // 超高清画质。
flvUHDStream.bitrate = 1800;
flvUHDStream.retryMaxCount = 3;
flvUHDStream.priority = 5;
mainStreams.add(flvUHDStream);

// 添加 ABR 多画质流的高清画质。优先级为 5。
VeLivePlayerStreamData.VeLivePlayerStream flvHDStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvHDStream.url = "https://xxx_hd.flv"; // 替换为高清画质的实际 FLV 拉流地址。
flvHDStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvHDStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvHDStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvHDStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // 高清画质。
flvHDStream.bitrate = 1500;
flvHDStream.retryMaxCount = 3;
flvHDStream.priority = 5;
mainStreams.add(flvHDStream);

// 添加普通 FLV 流作为降级流。优先级为 4。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 配置默认启动画质。
streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);

// 启用 ABR。
streamData.enableABR = true;

// 配置播放源。
mLivePlayer.setPlayStreamData(streamData);

// 开始播放。
mLivePlayer.play();
```

#### 步骤 2：添加回调

根据需要添加以下回调，以监听降级过程中的事件。

* 监听流格式切换，例如从 RTM 切换到 FLV。

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

* 监听播放过程中遇到的可恢复问题。当某个流播放失败，但 SDK 即将执行恢复操作（例如切换到降级流）时，会触发此回调。这表示播放仍在继续，你无需中断播放流程。调试时，你可以使用返回的错误信息了解流播放失败的具体原因。

   ```Java
   @Override
   public void onInfo(
       VeLivePlayer player,
       VeLivePlayerError error
   ) {
   }
   ```

* 监听从主流切换到备流。

   ```Java
   @Override
   public void onMainBackupSwitch(
       VeLivePlayer player,
       VeLivePlayerStreamType streamType,
       VeLivePlayerError error
   ) {
   }
   ```

* 监听播放最终结束，即所有流均播放失败。

   ```Java
   @Override
   public void onError(
       VeLivePlayer player,
       VeLivePlayerError error
   ) {
   }
   ```

## 播放 RTM 流

播放 RTM 流可将直播延迟降低到 1\-2 秒，为观众提供高质量直播观看体验。

但是，RTM 的超低延迟能力也对网络环境提出了更高要求。在网络不稳定时，可能出现播放延迟、卡顿或失败。如果你希望在 RTM 拉流地址不可用时自动尝试 FLV 等其他协议的拉流地址，请将此功能与流降级策略或主备流切换一起使用。更多信息，请参见[流降级策略和主备流切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#77618e0b)。

> **说明**

> 仅高级版和试用版 License 支持播放 RTM 流。

### 前提条件

* 确保已集成 1.50.100 或更高版本的 Player SDK。

* 通过以下任一方式获取 RTM、FLV 等协议的拉流地址。

   * **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

   * **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

### 操作步骤

本文提供以下两个代码示例，对应从简单到复杂的场景：

* **基础场景**：演示当主流列表中的高优先级 RTM 流播放失败时，如何自动降级到 FLV 等其他协议的流。

* **高级场景**：在基础场景上增加主备流切换机制。当主流列表中的所有流（包括 RTM 流和降级流）均不可用时，播放器会自动切换到备流列表重试。

建议你从基础场景开始。

**基础场景**

以下代码示例演示基本流降级场景，播放顺序如下：

1. 首先，播放器尝试播放 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器降级到 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，播放结束。

```Java
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 添加 FLV 主流作为降级流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 配置播放源。
mLivePlayer.setPlayStreamData(streamData);

// 开始播放。
mLivePlayer.play();
```

**高级场景**

以下代码示例演示将流降级策略与主备流切换结合的场景，播放顺序如下：

1. 首先，播放器尝试播放主流列表中的 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器降级到主流列表中的 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，播放器切换到备流列表，并尝试播放 RTM 流（优先级 5），最多尝试 3 次。

4. 如果失败，播放器降级到备流列表中的 FLV 流（优先级 4），最多尝试 3 次。

5. 如果这些尝试全部失败，播放结束。

```Java
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 添加 FLV 主流作为降级流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 配置备流列表。
List<VeLivePlayerStreamData.VeLivePlayerStream> backupStreams = new ArrayList<>();
// 添加 RTM 备流。
VeLivePlayerStreamData.VeLivePlayerStream rtmBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmBackupStream.url = "https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 备流列表中的最高优先级。
backupStreams.add(rtmBackupStream);

// 添加 FLV 备流作为降级流。
VeLivePlayerStreamData.VeLivePlayerStream flvBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvBackupStream.url = "https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
backupStreams.add(flvBackupStream);
streamData.backupStreamList = backupStreams;

// 启用主备流切换。
streamData.enableMainBackupSwitch = true;

// 配置播放源。
mLivePlayer.setPlayStreamData(streamData);

// 开始播放。
mLivePlayer.play();
```

## 播放 CMAF 流

CMAF（Common Media Application Format）是一种用于分段传输媒体的封装格式。播放 CMAF 流时，播放器会从 `.mpd` 拉流地址获取播放清单，然后拉取对应的音视频分片进行直播播放。

> **说明**

> 仅高级版和试用版 License 支持播放 CMAF 流。

### 前提条件

通过以下任一方式获取源流的 `.mpd` 拉流地址。

* **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成 `.mpd` 拉流地址。

* **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成 `.mpd` 拉流地址。

> **警告**

> 仅源流的 `.mpd` 拉流地址支持 CMAF 播放。ABR 流的 `.mpd` 拉流地址不支持 CMAF 播放。

### 操作步骤

* 调用 [setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) 方法并传入 `.mpd` 拉流地址进行播放。播放器会自动识别该流为 CMAF 流，无需额外配置格式。

   ```Java
   mLivePlayer.setPlayUrl("https://pull.example.com/live/stream/index.mpd"); // 替换为你的实际 .mpd 拉流地址。
   
   // 开始播放。
   mLivePlayer.play();
   ```

* 调用 [setPlayStreamData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) 方法配置一个或多个拉流地址，并将流格式显式设置为 `VeLivePlayerFormatCMAF`。以下示例代码使用 CMAF 流作为主流。

   ```Java
   VeLivePlayerStreamData.VeLivePlayerStream stream = new VeLivePlayerStreamData.VeLivePlayerStream();
   stream.url = "https://pull.example.com/live/stream/index.mpd"; // 替换为你的实际 .mpd 拉流地址。
   stream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatCMAF; // 将流格式显式设置为 VeLivePlayerFormatCMAF。
   stream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   // 创建 VeLivePlayerStreamData 实例。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   streamData.mainStreamList = new ArrayList<>();
   // 添加 CMAF 流。
   streamData.mainStreamList.add(stream);
   // 将播放源的默认流格式设置为 CMAF。
   streamData.defaultFormat = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatCMAF;
   // 配置播放源。
   mLivePlayer.setPlayStreamData(streamData);
   // 开始播放。
   mLivePlayer.play();
   ```

## 播放低延迟 FLV 流

启用低延迟 FLV 拉流后，FLV 拉流可将直播延迟降低到 2\-3 秒。

> **说明**

> 如需播放低延迟 FLV 流，请确保已集成 1.50.200.3 或更高版本的 SDK，并使用高级版或试用版 License。

### 操作步骤

开始播放前，你可以通过播放器高级 API [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) 启用低延迟 FLV 拉流。调用 `setProperty` 时，需要传入 `key-value` 配置。

**Key**

|参数名称 |类型 |描述 |
|---|---|---|
|VeLivePlayerKeySetParamsLowLatencyFLV |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |低延迟 FLV 拉流功能的属性键。 |

**Value**

该值是一个包含 `key-value` 对的 `JSONObject` 对象，用于配置低延迟 FLV 拉流功能。

* `Key`：`String` 类型。取值固定为 `EnableLowLatencyFLV`，表示是否启用低延迟 FLV 拉流功能。

* `Value`：`Integer` 类型。取值为 `1` 时启用低延迟 FLV 拉流功能，取值为 `0` 时禁用该功能。默认值为 `0`。

示例代码如下。

```Java
JSONObject flv2s = new JSONObject();
flv2s.put("EnableLowLatencyFLV", 1);
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsLowLatencyFLV, flv2s);
```

## QUIC 拉流

Player SDK 支持 QUIC 拉流。此功能应与 BytePlus MediaLive 一起使用。

> **说明**

> 仅高级版和试用版 License 支持 QUIC 拉流。

### 前提条件

在 BytePlus Live 控制台中使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成 FLV 拉流地址。

### 操作步骤

配置 QUIC 拉流地址并开始播放。示例代码如下。

```Java
VeLivePlayerStreamData.VeLivePlayerStream playStreamFLV = new VeLivePlayerStreamData.VeLivePlayerStream();
playStreamFLV.url = "https://pull.example.com/live/stream.flv"; // 替换为你的实际 FLV 拉流地址。
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;
playStreamFLV.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
playStreamFLV.streamType = VeLivePlayerStreamTypeMain;

// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
streamData.mainStreamList = new ArrayList<>();

// 添加 FLV 流。
streamData.mainStreamList.add(playStreamFLV);

// 配置播放源。
mLivePlayer.setPlayStreamData(streamData);

// 开始播放。
mLivePlayer.play();
```

> **说明**

> Player SDK 默认启用 QUIC 失败降级策略。如果 QUIC 拉流失败，SDK 会自动降级到 TCP 拉流。

## 使用 IP 地址拉流

播放器支持使用域名的 IP 地址进行拉流，以缩短首帧时间。

### 前提条件

获取拉流地址并解析其 IP 地址。

### 注意事项

* 使用 [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) 映射域名和 IP 地址时，请在初始配置中将 [enableLiveDNS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#enablelivedns) 设置为 `false`，以禁用 DNS 预解析功能。

* 在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 开始播放前，调用 [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) 设置域名到 IP 的映射。

### 操作步骤

使用播放器的 [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) API 将 IP 地址与域名关联。随后播放器会直接使用 IP 地址拉流。示例代码如下。

```Java
mLivePlayer.setPlayUrl("https://pull.example.com/live/stream.flv"); // 替换为你的实际拉流地址。
// 将拉流地址中的域名映射到其解析出的 IP 地址。
List<String> valueList = new ArrayList<>();
valueList.add("xxx.xxx.xxx.xxx"); // 替换为从域名解析出的实际 IP 地址。
Map<String, List<String>> map = new HashMap<>();
map.put("pull.example.com", valueList); // 将 pull.example.com 替换为你的实际拉流地址中的域名。

// 设置域名到 IP 的映射。
mLivePlayer.setUrlHostIP(map);

// 开始播放。
mLivePlayer.play();
```

## 清晰度切换

你可以设置多个不同清晰度的拉流地址，并在播放过程中在这些地址之间切换。

> **说明**

> 清晰度切换支持流降级策略。你可以为一组多清晰度流分配相同优先级，并配置较低优先级的降级流。如果较高优先级流组播放失败，SDK 会自动尝试降级组。更多信息，请参见[流降级策略和主备流切换](https://docs.byteplus.com/en/docs/24/106190#stream-fallback-strategy-and-primary-backup-stream-switching)。

### 前提条件

获取不同清晰度的拉流地址。如果你使用 BytePlus MediaLive 提供的直播服务，请执行以下操作：

1. [配置转码任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)，以生成多个不同清晰度的转码流。

2. 通过以下任一方式获取原始流和转码流的拉流地址。

   * **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

   * **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

此流程使用以下拉流地址作为示例。

|**清晰度** |**拉流地址** |
|---|---|
|原画（Origin） |`https://pull.example.com/live/123456.flv` |
|超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |
|高清（HD） |`https://pull.example.com/live/123456_hd.flv` |
|标清（SD） |`https://pull.example.com/live/123456_sd.flv` |
|低清（LD） |`https://pull.example.com/live/123456_ld.flv` |

### 操作步骤

1. 配置多清晰度拉流地址并开始播放。示例代码如下。

   ```Java
   // 配置多个画质档位的拉流地址。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // 替换为原画画质的实际拉流地址。
   playStreamOrigin.format = VeLivePlayerFormatFLV;
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 原画画质。
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // 替换为超高清画质的实际拉流地址。
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // 超高清画质。
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // 替换为高清画质的实际拉流地址。
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // 高清画质。
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv"; // 替换为标清画质的实际拉流地址。
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // 标清画质。
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv"; // 替换为低清画质的实际拉流地址。
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // 低清画质。
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   
   // 创建 VeLivePlayerStreamData 实例。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // 添加拉流地址。
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // 将默认清晰度设置为原画。
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
   
   // 传入拉流配置。
   mLivePlayer.setPlayStreamData(streamData);
   
   // 开始播放。
   mLivePlayer.play();
   ```

2. 调用 [switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) 切换清晰度。

   ```Java
   mLivePlayer.switchResolution(new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD)); // 切换到超高清画质。
   ```

3. 切换成功后，会触发 [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回调函数。

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
     // 清晰度切换完成时触发。
   }
   ```

## ABR 拉流

自适应码率（ABR）拉流可在网络状况变化时切换到更合适的画质，帮助保持流畅播放。

> **说明**

* > ABR 拉流支持 **RTM\-ABR 流**和 **FLV 流**。

* > 仅高级版和试用版 License 支持 ABR 拉流。

* > ABR 拉流支持流降级策略。对于 RTM\-ABR 流，你可以将 RTM\-ABR 拉流地址作为降级策略中的 RTM 流使用。对于 FLV 流，请为同一 ABR 流组中的所有画质档位分配相同优先级，并配置较低优先级的降级流。如果较高优先级 ABR 流组播放失败，SDK 会自动尝试降级组。更多信息，请参见[流降级策略和主备流切换](https://docs.byteplus.com/en/docs/24/106190#stream-fallback-strategy-and-primary-backup-stream-switching)。

目前，Android Player SDK 支持以下 ABR 模式：

* **RTM\-ABR 流**：RTM 播放的服务端 ABR 能力。播放器仅使用**一个** RTM\-ABR 拉流地址，服务端会根据观众的网络状况自动选择和切换画质。在保留 RTM 低延迟播放体验的同时，这有助于降低弱网环境下的卡顿。

* **FLV 流**：客户端 ABR 能力。你需要提供多个 FLV 拉流地址和码率信息，SDK 会根据网络状况在这些地址之间切换。

### RTM\-ABR 流

> **警告**

> 仅 1.51.100.8 及更高版本支持 RTM\-ABR 流。

#### 前提条件

* 配置多个 ABR 子流，并在添加 ABR 配置时选择 **RTM\-ABR** 作为 **Protocol Type**。更多信息，请参见[管理自适应码率配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)。

* 通过以下任一方式获取 RTM\-ABR 拉流地址。

   * **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)，并选择启动画质（后缀），在 **Adaptive bitrate** 页签获取 **RTM address**。更多信息，请参见[生成直播地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   * **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成 RTM\-ABR 拉流地址。不同后缀对应不同启动画质。使用其中一个地址开始播放。确保 `Protocol` 的值为 `udp`。

   > **警告**

   > 不要手动向普通 RTM 拉流地址追加 `rtmabr=true`。仅完成 RTM\-ABR 配置并使用生成的 RTM\-ABR 地址后，RTM\-ABR 才会生效。

#### 操作步骤

设置 **RTM\-ABR** 拉流地址并开始播放。

```Java
mLivePlayer.setPlayUrl("https://pull.example.com/live/test_uhd.sdp?rtmabr=true"); // 替换为你的实际 RTM-ABR 拉流地址。

// 开始播放。
mLivePlayer.play();
```

### FLV 流

#### 前提条件

获取源流以及每个画质档位转码流的拉流地址。如果使用 BytePlus MediaLive，请登录控制台并在获取拉流地址前完成[转码配置](https://console.byteplus.com/live/main/application/transcode)。你可以通过以下任一方式获取地址：

* **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

* **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

此流程使用以下拉流地址作为示例。

|画质档位 |拉流地址 |码率（kbps） |
|---|---|---|
|原画（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高清（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|标清（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|低清（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

> **警告**

> 为 ABR 配置多个画质档位拉流地址时，SDK 中每个画质档位的编码码率必须与[转码配置](https://console.byteplus.com/live/main/application/transcode)中配置的编码码率一致。更多信息，请参见[管理转码配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

#### 操作步骤

1. 配置多画质拉流地址并开始播放。示例代码如下。

   ```Java
   // 配置多个画质档位的拉流地址。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // 替换为原画画质的实际拉流地址。
   playStreamOrigin.format = VeLivePlayerFormatFLV;
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 原画画质。
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain;
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // 替换为超高清画质的实际拉流地址。
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // 超高清画质。
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // 替换为高清画质的实际拉流地址。
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // 高清画质。
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";  // 替换为标清画质的实际拉流地址。
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // 标清画质。
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";  // 替换为低清画质的实际拉流地址。
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // 低清画质。
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   playStreamLD.bitrate = 500;
   
   // 创建 VeLivePlayerStreamData 实例。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // 添加多画质流。
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // 配置默认启动画质。
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
   
   // 启用 ABR。
   streamData.enableABR = true;
   
   // 配置播放源。
   mLivePlayer.setPlayStreamData(streamData);
   
   // 开始播放。
   mLivePlayer.play();
   ```

2. 当 ABR 画质档位自动切换时，会触发 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回调。示例代码如下。

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
      // 画质档位切换回调。
   }
   ```

## 平滑画质切换

平滑画质切换功能可确保观众在手动切换不同画质档位（如超高清、高清和标清）时，音视频无缝过渡。此功能可**避免黑屏或卡顿**，提升观看体验。

如需使用此功能，请为播放器配置同一源的多画质流列表，并启用平滑画质切换。配置后，当观众手动切换画质档位时，播放器会在不同码率的流之间平滑过渡，确保直播音视频连续稳定播放。

> **说明**

> 平滑画质切换支持流降级策略。你可以为一组平滑画质切换流分配相同优先级，并配置较低优先级的降级流。如果较高优先级流组播放失败，SDK 会自动尝试降级组。更多信息，请参见[流降级策略和主备流切换](https://docs.byteplus.com/en/docs/24/106190#stream-fallback-strategy-and-primary-backup-stream-switching)。

> **警告**

* > 平滑画质切换功能目前仅适用于 FLV 流。

* > 确保已集成 1.50.100 或更高版本的 Player SDK。

### 前提条件

准备同一源流不同画质档位的拉流地址。

如果你使用 BytePlus MediaLive 的推流地址进行推流，请确保已完成以下操作：

* **添加域名**：在同一域名空间下添加推流和拉流域名。更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

* **配置转码**：在域名空间下为不同画质档位添加转码配置。更多信息，请参见[管理转码配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

* **获取拉流地址**：获取源流和每路转码流的拉流地址。

   * **调试场景**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

      * **地址类型**：选择 **Pull stream address**。

      * **域名**：选择转码配置所用域名空间下的拉流域名。

      * **AppName** 和 **StreamName**：输入与推流地址匹配的 `AppName` 和 `StreamName`。例如，如果推流地址为 `rtmp://push.example.com/live/test?authinfo`，则 `AppName` 为 `live`，`StreamName` 为 `test`。

   * **生产场景**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

**示例**

下表列出了不同画质档位的 FLV 拉流地址和码率示例。

|画质档位 |FLV 拉流地址 |码率（kbps） |
|---|---|---|
|原画（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高清（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|标清（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|低清（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

### 操作步骤

1. 配置各画质档位的流，并将 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) 设置为 `true`，以启用平滑画质切换。

   ```Java
   // 配置各画质档位的流。
   // 原画画质。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // 替换为原画画质的实际拉流地址。
   playStreamOrigin.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 画质档位标识。
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamOrigin.bitrate = 2500; // 码率，单位为 kbps。
   
   // 超高清画质。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // 替换为超高清画质的实际拉流地址。
   playStreamUHD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // 画质档位标识。
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamUHD.bitrate = 2500; // 码率，单位为 kbps。
   
   // 高清画质。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // 替换为高清画质的实际拉流地址。
   playStreamHD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // 画质档位标识。
   playStreamHD.streamType = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamHD.bitrate = 1000; // 码率，单位为 kbps。
   
   // 标清画质。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv"; // 替换为标清画质的实际拉流地址。
   playStreamSD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // 画质档位标识。
   playStreamSD.streamType = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamSD.bitrate = 800; // 码率，单位为 kbps。
   
   // 低清画质。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv"; // 替换为低清画质的实际拉流地址。
   playStreamLD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // 画质档位标识。
   playStreamLD.streamType = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamLD.bitrate = 500; // 码率，单位为 kbps。
   
   // 创建 VeLivePlayerStreamData 实例。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // 添加各画质档位的流。
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // 配置默认启动画质。
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD);
   
   // 启用平滑画质切换。
   streamData.enableSmoothSwitchResolution = true;
   
   // 配置播放源。
   mLivePlayer.setPlayStreamData(streamData);
   
   // 开始播放。
   mLivePlayer.play();
   ```

2. 直播过程中，当观众手动切换画质档位时，你可以调用 [switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) 平滑切换画质档位。示例代码如下。

   ```Java
   mLivePlayer.switchResolution(new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD)); // 切换到超高清画质。
   ```

3. 添加 [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回调，以监听画质档位切换结果。当画质档位变化时，SDK 可触发此回调并返回切换后的画质档位、切换原因等信息。

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

## 截图

此功能可捕获当前视频帧并生成图像。

1. 调用 [snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-snapshot) 进行截图。此功能仅在播放过程中生效。

   ```Java
   int result = mLivePlayer.snapshot();
   ```

2. 截图完成后，会触发 [onSnapshotComplete](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) 回调函数并返回图像数据。

   ```Java
   public void onSnapshotComplete(VeLivePlayer player, Bitmap bitmap) {
     // 回调函数通过 Bitmap 返回图像数据。
   }
   ```

## SEI

补充增强信息（SEI）是嵌入直播流中的附加数据。你可以使用 SEI 传输自定义数据或元数据。

> **说明**

> 仅高级版和试用版 License 支持 SEI。

* 字符串 SEI 消息

   1. 调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，启用播放器的 [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablesei) 属性。启用此属性后，播放器会接收字符串 SEI 消息。示例代码如下。

      ```Java
      // 创建 VeLivePlayerConfiguration 实例。
      VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
      
      // 启用接收字符串 SEI 消息。
      config.enableSei = true;
      
      // 配置播放器的初始设置。
      mLivePlayer.setConfig(config);
      ```

   2. 当播放器收到字符串 SEI 消息时，会触发 [onReceiveSeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) 回调。示例代码如下。

      ```Java
      public void onReceiveSeiMessage(VeLivePlayer player, String message) {
         // 字符串 SEI 消息回调。
      }
      ```

* 二进制 SEI 消息

   1. 调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，启用播放器的 [enableBinarySei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablebinarysei) 属性。启用此属性后，播放器会接收二进制 SEI 消息，且不再触发字符串 SEI 消息回调。示例代码如下。

      ```Java
      // 创建 VeLivePlayerConfiguration 实例。
      VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
      
      // 启用接收二进制 SEI 消息。
      config.enableBinarySei = true;
      
      // 配置播放器的初始设置。
      mLivePlayer.setConfig(config);
      ```

   2. 当播放器收到二进制 SEI 消息时，会触发 [onReceiveBinarySeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) 回调。示例代码如下。

      ```Java
      public void onReceiveBinarySeiMessage(VeLivePlayer player, byte[] message) {
         // 二进制 SEI 消息回调。
      }
      ```

## 订阅视频数据

通过订阅解码后的视频数据，你可以获取视频帧数据进行自定义处理和渲染。播放器支持多种视频帧回调格式，并提供对应的参数和格式选项。

### 前提条件

下表描述了视频帧像素格式和视频数据封装格式的枚举及含义。

|格式类型 |枚举值 |描述 |
|---|---|---|
|视频帧像素格式 |VeLivePlayerPixelFormatRGBA32 |RGBA32 |
|视频帧像素格式 |VeLivePlayerPixelFormatTexture |2D 纹理 |
|视频数据封装格式 |VeLivePlayerVideoBufferTypeByteBuffer |ByteBuffer |
|视频数据封装格式 |VeLivePlayerVideoBufferTypeByteArray |ByteArray |
|视频数据封装格式 |VeLivePlayerVideoBufferTypeTexture |Texture |

订阅视频数据前，请根据需要选择格式组合。该组合必须遵循下表所示的 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerpixelformat) 与 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayervideobuffertype) 的映射关系。

|像素格式/封装格式 |VeLivePlayerPixelFormatRGBA32 |VeLivePlayerPixelFormatTexture |
|---|---|---|
|**VeLivePlayerVideoBufferTypeByteBuffer** |支持 |不支持 |
|**VeLivePlayerVideoBufferTypeByteArray** |支持 |不支持 |
|**VeLivePlayerVideoBufferTypeTexture** |不支持 |支持（性能最优） |

### 操作步骤

1. 调用播放器的 [enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) API 启用或禁用视频帧数据订阅。API 参数说明如下表所示。

   |参数 |类型 |描述 |
   |---|---|---|
   |enable |boolean |是否启用视频帧回调。 |
   |pixelFormat |VeLivePlayerPixelFormat |视频帧像素格式。 |
   |bufferType |VeLivePlayerVideoBufferType |视频数据封装格式。 |

   示例代码如下。

   ```Java
   //
   mLivePlayer.enableVideoFrameObserver(true, VeLivePlayerPixelFormatRGBA32, VeLivePlayerVideoBufferTypeByteBuffer);
   ```

2. SDK 会通过 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onRenderVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) 回调返回解码后的视频帧数据。示例代码如下。

   ```Java
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
      // 视频帧数据回调。
   }
   ```

   [VeLivePlayerVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame) 参数说明如下表所示。

   |参数 |类型 |描述 |
   |---|---|---|
   |bufferType |VeLivePlayerVideoBufferType |视频帧数据封装格式。 |
   |pixelFormat |VeLivePlayerPixelFormat |视频帧像素格式。 |
   |width |int |视频帧宽度，单位为 px。 |
   |height |int |视频帧高度，单位为 px。 |
   |pts |long |视频帧渲染时间戳，单位为 ms。 |
   |texture |VeLivePlayerVideoTexture |当 `bufferType` 为 `VeLivePlayerVideoBufferTypeTexture` 时的视频数据。该字段携带用于 OpenGL 渲染的纹理数据。 |
   |buffer |ByteBuffer |当 `bufferType` 为 `VeLivePlayerVideoBufferTypeByteBuffer` 时的视频数据。该字段携带 JNI 层使用的直接缓冲区。 |
   |data |byte[] |当 `bufferType` 为 `VeLivePlayerVideoBufferTypeByteArray` 时的视频数据。该字段携带 Java 层使用的字节数组数据。 |

## 订阅音频数据

通过订阅解码后的音频数据，你可以执行自定义音频处理和渲染。Player SDK 支持订阅 PCM Float32 采样格式和 ByteArray 封装格式的音频数据。

|VeLivePlayerAudioBufferType |音频数据封装格式 |
|---|---|
|[VeLivePlayerAudioBufferTypeByteArray](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioBufferType) |ByteArray |

### 操作步骤

1. 调用播放器的 [enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) API 启用或禁用音频帧数据订阅。API 参数说明如下表所示。

   |参数 |类型 |描述 |
   |---|---|---|
   |enable |boolean |是否启用音频帧回调。 |
   |enableRendering |boolean |是否启用播放器渲染。如果播放器无需内部渲染音频，请将此参数设置为 `false`。 |

   示例代码如下。

   ```Java
   // 订阅音频帧数据，并启用播放器内部音频渲染。
   mLivePlayer.enableAudioFrameObserver(true, true);
   ```

2. SDK 会通过 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onRenderAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) 回调返回解码后的音频帧数据。示例代码如下。

   ```Java
   void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
      // 音频帧数据回调。
   }
   ```

   [VeLivePlayerAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame) 参数说明如下表所示。

   |参数 |数据类型 |描述 |
   |---|---|---|
   |bufferType |VeLivePlayerAudioBufferType |音频帧数据封装格式。 |
   |sampleRate |int |音频采样率，单位为 Hz。 |
   |channels |int |声道数。 |
   |bitDepth |int |音频位深。 |
   |pts |long |音频渲染时间戳，单位为 ms。 |
   |buffer |byte[] |PCM 音频数据。 |
   |samples |int |音频采样数。 |

## 超分

超分辨率（SR）是一种从低分辨率图像重建高分辨率图像的技术。实时 SR 使用算法将低分辨率帧实时重建为高分辨率帧。生成的高分辨率帧随后显示在屏幕上。SR 可增强视频细节和对比度，提升视频清晰度和观看体验。

> **说明**

> 仅高级版和试用版 License 支持 SR。

1. 调用播放器的 [setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) 方法启用或禁用 SR。

   ```Java
   mLivePlayer.setEnableSuperResolution(true);
   ```

   |名称 |类型 |描述 |
   |---|---|---|
   |enable |boolean |是否启用 SR。默认值为 `false`。<br><br><br>* `true`：启用 SR。<br><br>* `false`：禁用 SR。 |

2. 如果启用 SR 失败，播放器会通过 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) 回调通知你。方法签名如下。

   ```Java
   void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error);
   ```

   启用 SR 失败的常见原因如下。

   * 实际流分辨率不在 SR 支持范围内。

   * 实际流帧率不在 SR 支持范围内。

   * 当前设备型号不支持 SR。

## 自定义 HTTP 请求头

为播放器的 HTTP 请求设置自定义请求头。这通常用于传输身份验证 Token、Cookie、业务跟踪标识等附加信息。

> **说明**

> 仅 1.50.200.3 及更高版本支持自定义 HTTP 请求头。

### 操作步骤

开始播放前，你可以通过播放器高级 API [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) 设置自定义 HTTP 请求头。调用 `setProperty` 时，需要传入 `key-value` 配置。

**Key**

|参数名称 |类型 |描述 |
|---|---|---|
|VeLivePlayerKeySetParamsHttpHeaders |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |用于配置自定义 HTTP 请求头的属性键。 |

**Value**

该值是一个包含 `key-value` 对的 `Map<String, String>` 对象，用于设置自定义 HTTP 请求头。

* `Key`：`String` 类型。请求头名称。

* `Value`：`String` 类型。请求头值。

示例代码如下。

* 设置一个 HTTP 请求头

   ```Java
   Map<String, String> headerMap = new HashMap<>();
   headerMap.put("key", "value"); // 替换为实际请求头名称和值。
   mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders, headerMap);
   ```

* 设置多个 HTTP 请求头

   ```Java
   Map<String, String> headerMap = new HashMap<>();
   headerMap.put("key1", "value1"); // 替换为实际请求头名称和值。
   headerMap.put("key2", "value2"); // 替换为实际请求头名称和值。
   headerMap.put("key3", "value3"); // 替换为实际请求头名称和值。
   mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders, headerMap);
   ```

## H.265 硬件解码和软件解码

使用高级版或试用版 License 的 SDK 默认启用 H.265 硬件解码和软件解码。播放 H.265 编码的视频流时，SDK 会先尝试使用 H.265 硬件解码。如果 H.265 硬件解码失败，SDK 会自动切换到 H.265 软件解码。

调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，通过播放器初始配置启用或禁用硬件解码。示例代码如下。

```Java
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
config.enableHardwareDecode = true;
mLivePlayer.setConfig(config);
```

* `true`：启用硬件解码。

* `false`：禁用硬件解码，仅使用软件解码。

你可以监听 [onStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) 回调，并使用 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics) 的 [isHardwareDecode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-ishardwaredecode) 属性判断当前流是否使用硬件解码。

## H.266 软件解码

使用高级版或试用版 License 的 SDK 默认启用 H.266 软件解码，无需额外配置。

## 视频锐化

视频锐化会在设备本地增强视频，以提升边缘和纹理细节的清晰度。播放过程中，SDK 可实时增强边缘和纹理细节，使视频看起来更清晰，并提升观看体验。

> **说明**

> 仅高级版和试用版 License 支持视频锐化。

### 操作步骤

1. 调用播放器的 [setEnableSharpen](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) 方法启用或禁用视频锐化。

   ```Java
   mLivePlayer.setEnableSharpen(true);
   ```

   |名称 |类型 |描述 |
   |---|---|---|
   |enable |boolean |是否启用视频锐化。默认值为 `false`。<br><br><br>* `true`：启用视频锐化。<br><br>* `false`：禁用视频锐化。 |

2. 如果启用视频锐化失败，播放器会通过 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onStreamFailedOpenSharpen](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) 回调通知你。方法签名如下。

   ```Java
   default void onStreamFailedOpenSharpen(VeLivePlayer player, VeLivePlayerError error)
   ```

   启用视频锐化失败的常见原因如下。

   * 实际流分辨率不在视频锐化支持范围内。

   * 实际流帧率不在视频锐化支持范围内。

   * 当前设备型号不支持视频锐化。

   * 当前 License 不支持视频锐化。

## 画中画

画中画（PiP）会将播放器窗口缩小为屏幕角落的一个小悬浮窗，使观众在浏览其他内容或使用其他应用时仍可继续观看直播。此功能有助于提升观看体验。

### 前提条件

Android 6.0 或更高版本。

### 操作步骤

1. 将 [vepicutureinpicture](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/tree/main/Android/VeLiveQuickStartDemo/vepicutureinpicture) 模块代码复制到主项目的根目录。

2. 修改 `vepicutureinpicture/live/build.gradle` 中的 SDK 版本。将 `x.x.x.x` 替换为你已集成的 SDK 版本。版本号请参见 [Android Player SDK 发布说明](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)。

   ```Plain
   implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'
   ```

3. 将 `vepicutureinpicture` 模块导入你的项目。你可以参考 [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo) 进行配置。

   ```Java
   include ':vepicutureinpicture:live'
   include ':vepicutureinpicture:base'
   
   api project(path: ':vepicutureinpicture:live')
   ```

4. 初始化 PiP 功能。

   ```Java
   // mLivePlayer 是播放器实例。
   VeLivePictureInPicturePlayerManager mPipManager = new VeLivePictureInPicturePlayerManager(mLivePlayer, context);
   ```

5. 设置 PiP 观察者，以处理从 PiP 模式恢复正常播放的逻辑。在以下示例代码中，将 `XXXActivity` 替换为你项目中承载直播播放页面的 Activity。

   ```Java
   mPipManager.setObserver(new VeLivePictureInPicturePlayerManager.VeLivePictureInPicturePlayerManagerObserver() {
       @Override
       public void onClickResumeAction() {
           // 从 PiP 模式恢复正常播放。
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

6. 检查当前应用是否具有系统悬浮窗权限。

   ```Java
   boolean isPermission = mPipManager.isPermissionGranted();
   ```

   如果尚未授予系统悬浮窗权限，请参考以下示例代码请求权限，并引导用户前往系统设置页面启用权限。

   ```Java
   if (!isPermission) {
       mPipManager.requestPermission(new VePictureInPictureManager.VePictureInPicturePermissionCallback() {
           @Override
           public void onGranted(boolean granted) {
               // 权限请求结果回调。true 表示已授予系统悬浮窗权限。false 表示未授予系统悬浮窗权限。
           }
   
           @Override
           public void onRequestPermission(Context context, VePictureInPictureManager.VePictureInPicturePermissionResult result) {
               // 引导用户前往系统设置页面启用系统悬浮窗权限。
               new AlertDialog.Builder(context)
                       .setMessage("The system overlay permission is not enabled. Go to Settings and enable the [Display over other apps] permission.")
                       .setPositiveButton("Enable", (dialog, which) -> {
                           // 用户同意启用系统悬浮窗权限。
                           result.accept();
                       })
                       .setNegativeButton("Cancel", (dialog, which) -> {
                           // 用户不同意启用系统悬浮窗权限。
                           result.cancel();
                       })
                       .setCancelable(false)
                       .show();
           }
       });
   }
   ```

7. 页面直播播放期间，视频会渲染到 `Surface` 或 `SurfaceHolder`。集成 PiP 功能后，将同一个 `Surface` 或 `SurfaceHolder` 传递给 `mPipManager`，以便进入 PiP 模式后当前直播视频可继续显示。

   **设置 Surface**

```Java
   // 设置 Surface。
   mLivePlayer.setSurface(surface);
   mPipManager.setSurface(surface);
   ```

   **设置 SurfaceHolder**

```Java
   // 设置 SurfaceHolder。
   mLivePlayer.setSurfaceHolder(surfaceHolder);
   mPipManager.setSurfaceHolder(surfaceHolder);
   ```

8. 将播放器回调返回的当前视频宽高传递给 `mPipManager`。这可使 PiP 窗口按视频实际宽高比显示视频。

   ```Java
   mLivePlayer.setVeLivePlayerObserver(new VeLivePlayerObserver() {
       @Override
       public void onVideoSizeChanged(VeLivePlayer player, int width, int height) {
           mPipManager.setVideoSize(width, height);
       }
   });
   ```

9. 如果需要自定义 PiP 窗口大小，请参考以下示例代码进行配置。

   **按宽度自定义**

```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 将 PiP 窗口最大宽度设置为 720 px。最小宽度默认为最大宽度的 50%。高度会根据视频宽高比自动计算。
   configuration.maxWidth = 720;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

   你也可以按设备屏幕宽度的比例设置 PiP 窗口大小。

   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 将 PiP 窗口最大宽度设置为设备屏幕宽度的 50%。最小宽度默认为最大宽度的 50%。高度会根据视频宽高比自动计算。
   configuration.maxWidthRatio = 0.5;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

   **按高度自定义**

```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 将 PiP 窗口最大高度设置为 720 px。最小高度默认为最大高度的 50%。宽度会根据视频宽高比自动计算。
   configuration.maxHeight = 720;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

   你也可以按设备屏幕高度的比例设置 PiP 窗口大小。

   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 将 PiP 窗口最大高度设置为设备屏幕高度的 50%。最小高度默认为最大高度的 50%。宽度会根据视频宽高比自动计算。
   configuration.maxHeightRatio = 0.5;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

10. 直播播放开始且已授予系统悬浮窗权限后，你可以启动 PiP 模式。

```Java
mPipManager.startPictureInPicture();
```

如果当前已处于 PiP 模式，你可以停止 PiP 模式。

```Java
mPipManager.stopPictureInPicture();
```

11. 如需判断 PiP 窗口当前是否显示，请调用以下方法。

```Java
boolean showing = mPipManager.isPictureInPictureShowing();
```

12. 当不再需要 PiP 功能时，销毁 `mPipManager`。

```Java
mPipManager.destroy();
```

## 高级 API 配置

### 移除 SDK 自动追加的查询参数

Player SDK 可能会向拉流地址追加查询参数，例如 `session_id`。这些参数用于标识拉流会话，并在排查播放问题时帮助在客户端和 CDN 日志中定位同一会话。如需阻止 SDK 在实际请求 URL 中包含自动追加的查询参数，请启用此功能。启用此功能后，SDK 追加的查询参数会从实际请求 URL 中移除，而原始拉流地址中已存在的查询参数会保留。

> **说明**

> 仅 1.52.100.5 及更高版本支持移除 SDK 自动追加的查询参数。

#### 操作步骤

开始播放前，你可以使用播放器高级 [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) API 配置是否移除 SDK 自动追加的查询参数。调用 `setProperty` 时，需要传入 `key-value` 配置。

**Key**

|参数名称 |类型 |描述 |
|---|---|---|
|VeLivePlayerKeySetParamsRemoveQueryParams |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |用于移除 SDK 自动追加查询参数的属性键。 |

**Value**

`Value` 是一个布尔值，表示是否移除 SDK 自动追加的查询参数。默认值为 `false`。

* `true`：移除 SDK 自动追加的查询参数。

* `false`：保留 SDK 自动追加的查询参数。

示例代码如下。

```Java
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsRemoveQueryParams, true);
```

**效果示例**

例如，拉流地址为：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```

当 SDK 发起播放请求时，会自动追加 `session_id`：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901&session_id=xxx
```

启用此功能后，请求 URL 不再包含 `session_id`，但会保留原始拉流地址中的 `auth_key` 鉴权参数：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```
