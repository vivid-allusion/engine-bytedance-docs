---
title: "适用于 iOS 的 Player SDK：高级功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3-zh-CN"
---

为提升 iOS 应用中的观看体验，本文介绍如何实现适用于 iOS 的 Player SDK 的高级功能。你可以根据实际业务需求按需实现复杂功能。

## 前提条件

* 你已按照 [适用于 iOS 的 Player SDK：基础功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3)中的说明实现 Player SDK 的基础功能。

* 如需使用以下功能，请确保使用高级版或试用版 license。

   * [播放 RTM 流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d2fff36e)

   * [QUIC 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#78c4f3ae)

   * [播放低延迟 FLV 流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#3d66c491)

   * [主备流切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368)

   * [ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#aceb1766)

   * [超分辨率](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#4ea2c546)

   * [H.265 硬解码和软解码](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#953988b6)

   * [视频锐化](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e3976737)

   * [播放 DRM 加密流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e1834266)

   > **警告**

   > 试用版 license 仅用于项目测试，且不可续期。试用版 license 过期后会导致鉴权失败，从而中断服务。请在项目上线前升级为正式 license。更多信息，请参见[将试用版 license 升级为基础版或高级版 license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

## 注意事项

由于 Player SDK 使用多种 iOS 音视频 API，而这些 API 在模拟器上可能无法正常工作，建议使用真机进行测试。

## 流容灾策略和主备流切换

如果只配置一个拉流地址，当该地址因网络问题或其他异常不可用时，播放可能卡顿甚至失败。为降低单一地址异常导致的播放失败风险，你可以为一次播放会话配置多个拉流地址，并根据需要选择以下配置方式之一：

* **流容灾策略**：当你希望播放器按优先级自动尝试多个拉流地址时使用。你可以为每个地址配置优先级和最大重试次数。播放器优先尝试高优先级地址。如果某个地址在所有重试次数耗尽后仍不可用，播放器会切换到下一优先级的地址。

* **主备流切换**：当你的应用维护独立的主流列表和备流列表时使用。播放器会先按照流容灾策略尝试主流列表中的流。仅当主流列表中的所有地址均失败后，播放器才会自动切换到备流列表并继续尝试。

> **说明**

> 仅高级版和试用版 license 支持主备流切换。所有 license 类型均支持流容灾策略。

* 流容灾策略

   主流或备流列表中的播放顺序如下：

   1. **播放优先级最高的流**：播放器根据你设置的 `priority`，按从高到低的优先级尝试播放当前列表中的流。

   2. **失败后重试**：如果当前流播放失败，播放器会根据该流的 `retryMaxCount` 进行重试。

   3. **切换到容灾流**：如果所有重试次数耗尽后播放仍失败，播放器会放弃当前流，并尝试当前列表中下一优先级的流。

* 主备流切换

   启用主备流切换后，播放器按以下顺序尝试流：

   1. **播放主流**：播放器会先尝试播放主流列表中的流。

   2. **切换到备流**：如果主流列表中的所有流均播放失败，播放器会尝试播放备流列表中的流。

   3. **播放失败**：如果备流列表中的所有流也播放失败，则播放失败。

在此过程中，SDK 会通过以下回调通知你当前状态：

* [onInfo:info:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info)：当某个流播放失败但存在其他可用流时触发。你可以使用此回调获取详细错误信息，以便调试。

* [onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo)：当播放器切换流格式时触发，例如从 RTM 切换到 FLV。

* [onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error)：当主流列表中的所有流均播放失败，且播放器成功切换到备流列表时触发。

* [onError:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error)：当主流和备流列表中的所有流均播放失败，且播放最终结束时触发。

### 前提条件

通过以下任一方式获取 RTM、FLV 等协议的拉流地址。同一列表内的容灾顺序由每个拉流地址的优先级决定。

* **用于调试**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

* **用于生产**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

### 操作步骤

#### 步骤 1：配置容灾策略

你可以通过配置 `VeLivePlayerStream` 的 [priority](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-priority) 和 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount) 自定义容灾策略。

* `priority`：流的优先级。取值必须为 `0`（默认值）或正整数。**数值越大，优先级越高**。播放器会优先尝试播放高优先级的流。

   > **说明**

   > 主流列表和备流列表的优先级独立计算，互不影响。

* `retryMaxCount`：该流的最大播放尝试次数，包括首次尝试。例如，如果取值为 `3`，则首次播放失败后，播放器最多再重试 2 次。有效取值：

   * `-1`（默认值）：使用 `VeLivePlayerConfiguration` 中 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) 的值。

   * `0`：不尝试播放该流。

   * `>0`：最大播放尝试次数。

**流容灾策略**

以下代码示例演示了一个基础的流容灾场景，播放顺序如下：

1. 首先，播放器尝试播放 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器容灾到 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，则播放结束。

```objectivec
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 添加 FLV 主流作为容灾流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置播放源。
[self.livePlayer setPlayStreamData:streamData];

// 开始播放。
[self.livePlayer play];
```

**流容灾策略 + 主备流切换**

以下代码示例演示了将流容灾策略与主备流切换结合使用的场景，播放顺序如下：

1. 首先，播放器尝试播放主流列表中的 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器容灾到主流列表中的 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，播放器切换到备流列表，并尝试播放 RTM 流（优先级 5），最多尝试 3 次。

4. 如果失败，播放器容灾到备流列表中的 FLV 流（优先级 4），最多尝试 3 次。

5. 如果所有尝试均失败，则播放结束。

```objectivec
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
// 配置主流列表。
NSMutableArray *mainStreams = [NSMutableArray new];

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 添加 FLV 主流作为容灾流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置备流列表。
NSMutableArray *backupStreams = [NSMutableArray new];
// 添加 RTM 备流。
VeLivePlayerStream *rtmBackupStream = [[VeLivePlayerStream alloc] init];
rtmBackupStream.url = @"https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmBackupStream.format = VeLivePlayerFormatRTM;
rtmBackupStream.type = VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 备流列表中的最高优先级。
[backupStreams addObject:rtmBackupStream];

// 添加 FLV 备流作为容灾流。
VeLivePlayerStream *flvBackupStream = [[VeLivePlayerStream alloc] init];
flvBackupStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvBackupStream.format = VeLivePlayerFormatFLV;
flvBackupStream.type = VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
[backupStreams addObject:flvBackupStream];
streamData.backupStream = backupStreams;

// 启用主备流切换。
streamData.enableMainBackupSwitch = YES;

// 配置播放源。
[self.livePlayer setPlayStreamData:streamData];

// 开始播放。
[self.livePlayer play];
```

**多档位流容灾策略**

流容灾策略支持为[分辨率切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#660adfe3)、[ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae)（仅 FLV 流）和[无感清晰度切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#37bcd52d)使用的多档位流配置容灾流。配置时，请为同一多档位流组中的流设置相同的 `priority` 值。播放器会先按 `priority` 从高到低选择流组。如果高优先级多档位流播放失败，播放器会容灾到低优先级流。

在以下示例中，播放器会先播放 `priority` 为 `5` 的 ABR 多档位流。如果 ABR 多档位流播放失败，播放器会容灾到 `priority` 为 `4` 的普通 FLV 流。

```objectivec
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// 添加 ABR 多档位流的原画档位。优先级为 5。
VeLivePlayerStream *flvOriginStream = [[VeLivePlayerStream alloc] init];
flvOriginStream.url = @"https://xxx_origin.flv"; // 替换为原画档位的实际 FLV 拉流地址。
flvOriginStream.format = VeLivePlayerFormatFLV;
flvOriginStream.type = VeLivePlayerStreamTypeMain;
flvOriginStream.protocol = VeLivePlayerProtocolTLS;
flvOriginStream.resolution = VeLivePlayerResolutionOrigin; // 清晰度档位标识。
flvOriginStream.bitrate = 2000;
flvOriginStream.retryMaxCount = 3;
flvOriginStream.priority = 5;
[mainStreams addObject:flvOriginStream];

// 添加 ABR 多档位流的 UHD 档位。优先级为 5。
VeLivePlayerStream *flvUHDStream = [[VeLivePlayerStream alloc] init];
flvUHDStream.url = @"https://xxx_uhd.flv"; // 替换为 UHD 档位的实际 FLV 拉流地址。
flvUHDStream.format = VeLivePlayerFormatFLV;
flvUHDStream.type = VeLivePlayerStreamTypeMain;
flvUHDStream.protocol = VeLivePlayerProtocolTLS;
flvUHDStream.resolution = VeLivePlayerResolutionUHD; // 清晰度档位标识。
flvUHDStream.bitrate = 1800;
flvUHDStream.retryMaxCount = 3;
flvUHDStream.priority = 5;
[mainStreams addObject:flvUHDStream];

// 添加 ABR 多档位流的 HD 档位。优先级为 5。
VeLivePlayerStream *flvHDStream = [[VeLivePlayerStream alloc] init];
flvHDStream.url = @"https://xxx_hd.flv"; // 替换为 HD 档位的实际 FLV 拉流地址。
flvHDStream.format = VeLivePlayerFormatFLV;
flvHDStream.type = VeLivePlayerStreamTypeMain;
flvHDStream.protocol = VeLivePlayerProtocolTLS;
flvHDStream.resolution = VeLivePlayerResolutionHD; // 清晰度档位标识。
flvHDStream.bitrate = 1500;
flvHDStream.retryMaxCount = 3;
flvHDStream.priority = 5;
[mainStreams addObject:flvHDStream];

// 添加普通 FLV 流作为容灾流。优先级为 4。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置默认起播清晰度档位。
streamData.defaultResolution = VeLivePlayerResolutionOrigin;

// 启用 ABR。
streamData.enableABR = YES;

// 配置播放源。
[self.livePlayer setPlayStreamData:streamData];

// 开始播放。
[self.livePlayer play];
```

#### 步骤 2：添加回调

根据需要添加以下回调，用于监听容灾过程中的事件。

* 监听流格式切换，例如从 RTM 切换到 FLV。

   ```objectivec
   - (void)onStreamFormatSwitch:(TVLManager *_Nonnull)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(NSDictionary *)extraInfo;
   ```

* 监听播放过程中遇到的可恢复问题。当某个流播放失败但 SDK 即将执行恢复操作（例如切换到容灾流）时，会触发此回调。这表示播放仍在继续，你无需中断播放流程。调试时，你可以使用返回的错误信息了解流播放失败的具体原因。

   ```objectivec
   - (void)onInfo:(TVLManager *_Nonnull)player info:(VeLivePlayerError *_Nonnull)info;
   ```

* 监听从主流切换到备流。

   ```objectivec
   - (void)onMainBackupSwitch:(TVLManager *_Nonnull)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error;
   ```

* 监听播放最终结束，即所有流均播放失败。

   ```objectivec
   - (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
   ```

## 播放 RTM 流

播放 RTM 流可将直播延迟降低到 1\-2 秒，为观众提供高质量的直播观看体验。

但是，RTM 的超低延迟能力也对网络环境提出了更高要求。在网络不稳定时，可能出现播放延迟、卡顿或失败。如果你希望在 RTM 拉流地址不可用时，自动尝试 FLV 等其他协议的拉流地址，请将此功能与流容灾策略或主备流切换配合使用。更多信息，请参见[流容灾策略和主备流切换](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368)。

> **说明**

> 仅高级版和试用版 license 支持播放 RTM 流。

### 前提条件

* 确保已集成 1.50.100 或更高版本的 Player SDK，并添加 `LivePull-RTS` 依赖。更多信息，请参见[集成适用于 iOS 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)。

* 通过以下任一方式获取 RTM、FLV 等协议的拉流地址。

   * **用于调试**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

   * **用于生产**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

### 操作步骤

本文提供以下两个代码示例，对应从简单到复杂的场景：

* **基础场景**：演示主流列表中的高优先级 RTM 流播放失败时，如何自动容灾到 FLV 等其他协议的流。

* **高级场景**：在基础场景之上增加主备流切换机制。当主流列表中的所有流（包括 RTM 流和容灾流）均不可用时，播放器会自动切换到备流列表重试。

建议从基础场景开始。

**基础场景**

以下代码示例演示了一个基础的流容灾场景，播放顺序如下：

1. 首先，播放器尝试播放 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器容灾到 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，则播放结束。

```objectivec
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 添加 FLV 主流作为容灾流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置播放源。
[self.livePlayer setPlayStreamData:streamData];

// 开始播放。
[self.livePlayer play];
```

**高级场景**

以下代码示例演示了将流容灾策略与主备流切换结合使用的场景，播放顺序如下：

1. 首先，播放器尝试播放主流列表中的 RTM 流（优先级 5），最多尝试 3 次。

2. 如果失败，播放器容灾到主流列表中的 FLV 流（优先级 4），最多尝试 2 次。

3. 如果仍失败，播放器切换到备流列表，并尝试播放 RTM 流（优先级 5），最多尝试 3 次。

4. 如果失败，播放器容灾到备流列表中的 FLV 流（优先级 4），最多尝试 3 次。

5. 如果所有尝试均失败，则播放结束。

```objectivec
// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
// 配置主流列表。
NSMutableArray *mainStreams = [NSMutableArray new];

// 添加 RTM 主流（最高优先级）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 添加 FLV 主流作为容灾流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置备流列表。
NSMutableArray *backupStreams = [NSMutableArray new];
// 添加 RTM 备流。
VeLivePlayerStream *rtmBackupStream = [[VeLivePlayerStream alloc] init];
rtmBackupStream.url = @"https://xxx.sdp"; // 替换为你的实际 RTM 拉流地址。
rtmBackupStream.format = VeLivePlayerFormatRTM;
rtmBackupStream.type = VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 备流列表中的最高优先级。
[backupStreams addObject:rtmBackupStream];

// 添加 FLV 备流作为容灾流。
VeLivePlayerStream *flvBackupStream = [[VeLivePlayerStream alloc] init];
flvBackupStream.url = @"https://xxx.flv"; // 替换为你的实际 FLV 拉流地址。
flvBackupStream.format = VeLivePlayerFormatFLV;
flvBackupStream.type = VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
[backupStreams addObject:flvBackupStream];
streamData.backupStream = backupStreams;

// 启用主备流切换。
streamData.enableMainBackupSwitch = YES;

// 配置播放源。
[self.livePlayer setPlayStreamData:streamData];

// 开始播放。
[self.livePlayer play];
```

## 播放低延迟 FLV 流

启用低延迟 FLV 直播后，FLV 拉流可将直播延迟降低到 2\-3 秒。

> **说明**

> 如需播放低延迟 FLV 流，请确保已集成 1.50.200.3\-premium 或更高版本的 SDK，并使用高级版或试用版 license。

### 操作步骤

开始播放前，你可以通过播放器的高级 API [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) 启用低延迟 FLV 直播。调用 `setProperty:value:` 时，需要传入 `key-value` 配置。

**Key**

|参数名称 |类型 |描述 |
|---|---|---|
|VeLivePlayerKeySetParamsLowLatencyFlv |NSString |低延迟 FLV 直播功能的属性键。 |

**Value**

该值为 `NSDictionary` 对象，包含用于配置低延迟 FLV 直播功能的 `key-value` 对。

* `Key`：`NSString` 类型。取值固定为 `EnableLowLatencyFLV`，表示是否启用低延迟 FLV 直播功能。

* `Value`：`NSNumber` 类型。取值为 `1` 表示启用低延迟 FLV 直播功能，取值为 `0` 表示禁用该功能。默认值为 `0`。

示例代码如下。

```objectivec
[self.livePlayer setProperty:VeLivePlayerKeySetParamsLowLatencyFlv value:@{@"EnableLowLatencyFLV": @1}];
```

## QUIC 拉流

Player SDK 支持 QUIC 拉流。该功能需与 BytePlus MediaLive 配合使用。

> **说明**

> 仅高级版和试用版 license 支持 QUIC 拉流。

### 前提条件

使用 BytePlus Live 控制台中的[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成 FLV 拉流地址。

### 操作步骤

配置 QUIC 拉流地址并开始播放。示例代码如下。

```objectivec
VeLivePlayerStream *playStreamFLV = [[VeLivePlayerStream alloc]init]; 
playStreamFLV.url = @"https://pull.example.com/live/stream.flv"; // 替换为你的实际 FLV 拉流地址。
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;

// 创建 VeLivePlayerStreamData 实例。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];

// 添加 FLV 流地址。
[mainStreams addObject:playStreamFLV];

streamData.mainStream = mainStreams;

// 配置播放源。
[self.livePlayer setPlayStreamData:streamData];

// 开始播放。
[self.livePlayer play];
```

> **说明**

> Player SDK 默认启用 QUIC 失败容灾策略。如果 QUIC 拉流失败，SDK 会自动容灾到 TCP 拉流。

## 播放 DRM 加密流

> **说明**

> 仅高级版和试用版 license 支持播放 DRM 加密流。

如需播放受数字版权管理（DRM）保护的流，请执行以下操作：

1. 按照[使用 DRM 加密直播流](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm)中的说明获取以下信息：

   * 获取 M3U8 格式的 DRM 加密拉流地址。

   * 使用 [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm) 获取用于获取 DRM license 的 URL。该 URL 包含鉴权信息和过期时间。

   * 使用 [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm) 获取 FairPlay 直播证书。

2. 在 iOS 项目中，通过调用 [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype) 初始化播放器。

   ```objectivec
   self.livePlayer = [[TVLManager alloc] initWithType:VeLivePlayerTypeSystem];
   ```

   > **说明**

   > 使用 `initWithType:` 初始化的系统播放器不支持以下功能：

   * > 播放 M3U8 格式以外的流

   * > 主备流切换

   * > ABR 拉流

   * > 截图

   * > 镜像

   * > 音视频自定义渲染

   * > 超分辨率

   * > SEI

3. 设置 DRM 加密拉流地址。

   ```objectivec
   NSString *playUrl = @"http://pull.example.com/live/stream.m3u8"; // 替换为你的实际 DRM 加密拉流地址。
   [self.livePlayer setPlayUrl:playUrl];
   ```

4. 实现播放器 observer 的 [getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#getdrmresourceloadercertificatedata) 和 [getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#getdrmresourceloaderlicenseurl) 回调，向 SDK 提供 FairPlay 证书数据和 DRM license URL。

   ```objectivec
   - (NSData *)getDrmResourceLoaderCertificateData:(TVLManager *)player {
       NSString *filePath = [[NSBundle mainBundle] pathForResource:@"testfairplay" ofType:@"cer"]; // 将 testfairplay 替换为实际的 FairPlay 证书文件名。
       NSData *certificate = [NSData dataWithContentsOfFile:filePath];
       return certificate;
   }
   
   - (NSString *)getDrmResourceLoaderLicenseUrl:(TVLManager *)player {
       return @"https://drmtest/license"; // 替换为实际的 DRM license URL。
   }
   ```

5. 播放 DRM 加密流。

   ```objectivec
   [self.livePlayer play];
   ```

## 使用 IP 地址拉流

播放器支持使用域名对应的 IP 地址进行拉流，以降低首帧时间。

### 前提条件

获取拉流地址并解析其 IP 地址。

### 操作步骤

使用播放器的 [setUrlHostIP:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#seturlhostip) API 将 IP 地址与域名关联。随后播放器会直接使用 IP 地址拉流。示例代码如下。

```objectivec
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/stream.flv"]; // 替换为你的实际拉流地址。

// 将拉流地址中的域名映射到其解析后的 IP 地址。
NSMutableArray<NSString *> *ipList = [[NSMutableArray alloc] initWithCapacity:1];
[ipList addObject:@"xxx.xxx.xxx.xxx"];  // 替换为从域名解析得到的实际 IP 地址。

NSMutableDictionary* ipHost = [[NSMutableDictionary alloc] initWithCapacity:1];
[ipHost setObject:ipList forKey:@"pull.example.com"]; // 将 pull.example.com 替换为你的实际拉流地址中的域名。

// 设置域名到 IP 的映射。
[self.livePlayer setUrlHostIP:ipHost];

// 开始播放。
[self.livePlayer play];
```

## 分辨率切换

你可以设置多个不同分辨率的拉流地址，并在播放过程中在这些地址之间切换。

> **说明**

> 分辨率切换支持流容灾策略。你可以为一组多分辨率流分配相同优先级，并配置更低优先级的容灾流。如果高优先级流组播放失败，SDK 会自动尝试容灾组。更多信息，请参见[流容灾策略和主备流切换](https://docs.byteplus.com/en/docs/24/106184#stream-fallback-strategy-and-primary-backup-stream-switching)。

### 前提条件

获取不同分辨率的拉流地址。如果你使用 BytePlus MediaLive 提供的直播服务，请执行以下操作：

1. [配置转码任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)，生成多个不同分辨率的转码流。

2. 通过以下任一方式获取原始流和转码流的拉流地址。

   * **用于调试**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

   * **用于生产**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

      本节使用以下拉流地址作为示例。

   |**分辨率** |**拉流地址** |
   |---|---|
   |原画（Origin） |`https://pull.example.com/live/123456.flv` |
   |超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |
   |高清（HD） |`https://pull.example.com/live/123456_hd.flv` |
   |标清（SD） |`https://pull.example.com/live/123456_sd.flv` |
   |流畅（LD） |`https://pull.example.com/live/123456_ld.flv` |

### 操作步骤

1. 配置多分辨率拉流地址并开始播放。示例代码如下。

   ```objectivec
   // 配置多个清晰度档位的拉流地址。
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // 替换为原画档位的实际拉流地址。
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // 原画档位。
   
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // 替换为 UHD 档位的实际拉流地址。
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD 档位。
   
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // 替换为 HD 档位的实际拉流地址。
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD 档位。
   
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // 替换为 SD 档位的实际拉流地址。
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD 档位。
   
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv"; // 替换为 LD 档位的实际拉流地址。
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD 档位。
   
   // 创建 VeLivePlayerStreamData 实例。
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // 添加拉流地址。
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // 设置默认分辨率为原画。
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // 配置播放源。
   [self.livePlayer setPlayStreamData:streamData];
   
   // 开始播放。
   [self.livePlayer play];
   ```

2. 调用 [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#switchresolution) 更改分辨率。

   ```objectivec
   [self.livePlayer switchResolution:VeLivePlayerResolutionUHD]; // 切换到 UHD 档位。
   ```

3. 切换成功后，将触发 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回调。

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
     // 分辨率切换完成时触发。
   }
   ```

## ABR 拉流

自适应码率（ABR）拉流可在网络状况变化时切换到更合适的清晰度档位，从而保持播放流畅。

> **说明**

* > ABR 拉流支持 **RTM\-ABR 流**和 **FLV 流**。

* > 仅高级版和试用版 license 支持 ABR 拉流。

* > ABR 拉流支持流容灾策略。对于 RTM\-ABR 流，你可以在容灾策略中将 RTM\-ABR 拉流地址作为 RTM 流使用。对于 FLV 流，请为一个 ABR 流组中的所有清晰度档位分配相同优先级，并配置更低优先级的容灾流。如果高优先级 ABR 流组播放失败，SDK 会自动尝试容灾组。更多信息，请参见[流容灾策略和主备流切换](https://docs.byteplus.com/en/docs/24/106184#stream-fallback-strategy-and-primary-backup-stream-switching)。

目前，适用于 iOS 的 Player SDK 支持以下 ABR 模式：

* **RTM\-ABR 流**：一种用于 RTM 播放的服务端 ABR 能力。播放器只使用**一个** RTM\-ABR 拉流地址，服务端会根据观众的网络状况自动选择并切换清晰度档位。这有助于减少弱网环境下的卡顿，同时保留 RTM 的低延迟播放体验。

* **FLV 流**：一种客户端 ABR 能力。你需要提供多个 FLV 拉流地址和码率信息，SDK 会根据网络状况在这些地址之间切换。

### RTM\-ABR 流

> **警告**

> 仅 1.51.100.3\-premium 及更高版本支持 RTM\-ABR 流。

#### 前提条件

* 配置多个 ABR 子流，并在添加 ABR 配置时选择 **RTM\-ABR** 作为**协议类型**。更多信息，请参见[管理自适应码率配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)。

* 通过以下任一方式获取 RTM\-ABR 拉流地址。

   * **用于调试**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)，并选择起播清晰度档位（后缀），在**自适应码率**页签获取 **RTM 地址**。更多信息，请参见[生成流地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   * **用于生产**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成 RTM\-ABR 拉流地址。不同后缀对应不同的起播清晰度档位。使用其中一个地址开始播放。请确保 `Protocol` 的值为 `udp`。

   > **警告**

   > 请勿手动向普通 RTM 拉流地址追加 `rtmabr=true`。只有完成 RTM\-ABR 配置并使用生成的 RTM\-ABR 地址后，RTM\-ABR 才会生效。

#### 操作步骤

设置 **RTM\-ABR** 拉流地址并开始播放。

```objectivec
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/test_uhd.sdp?rtmabr=true"]; // 替换为你的实际 RTM-ABR 拉流地址。

// 开始播放。
[self.livePlayer play];
```

### FLV 流

#### 前提条件

获取源流和各清晰度档位转码流的拉流地址。如果你使用 BytePlus MediaLive，请登录控制台并完成[转码配置](https://console.byteplus.com/live/main/application/transcode)，然后获取拉流地址。你可以通过以下任一方式获取地址：

* **用于调试**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

* **用于生产**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

本节使用以下拉流地址作为示例。

|清晰度档位 |拉流地址 |码率（kbps） |
|---|---|---|
|原画（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高清（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|标清（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|流畅（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

> **警告**

> 为 ABR 配置多个清晰度档位的拉流地址时，SDK 中每个清晰度档位的编码码率必须与[转码配置](https://console.byteplus.com/live/main/application/transcode)中配置的编码码率一致。更多信息，请参见[管理转码配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

#### 操作步骤

1. 配置多档位拉流地址并开始播放。示例代码如下。

   ```objectivec
   // 配置多个清晰度档位的拉流地址。
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // 替换为原画档位的实际拉流地址。
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // 原画档位。
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // 替换为 UHD 档位的实际拉流地址。
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD 档位。
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // 替换为 HD 档位的实际拉流地址。
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD 档位。
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // 替换为 SD 档位的实际拉流地址。
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD 档位。
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv";  // 替换为 LD 档位的实际拉流地址。
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD 档位。
   playStreamLD.bitrate = 500;
   
   // 创建 VeLivePlayerStreamData 实例。
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // 添加多档位流。
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // 配置默认起播清晰度档位。
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // 启用 ABR。
   streamData.enableABR = YES;
   
   // 配置播放源。
   [self.livePlayer setPlayStreamData:streamData];
   
   // 开始播放。
   [self.livePlayer play];
   ```

2. 当 ABR 清晰度档位自动切换时，会触发 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 协议中定义的 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回调。示例代码如下。

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
      // 清晰度档位切换回调。
   }
   ```

## 无感清晰度切换

无感清晰度切换功能可确保观众在超高清、高清、标清等不同清晰度档位之间手动切换时，音视频能够无缝过渡。该功能可**避免黑屏或卡顿**，提升观看体验。

如需使用此功能，请为播放器配置来自同一源的多个清晰度档位流列表，并启用无感清晰度切换。配置完成后，当观众手动切换清晰度档位时，播放器会在不同码率的流之间平滑过渡，确保直播音视频连续稳定播放。

> **说明**

> 无感清晰度切换支持流容灾策略。你可以为一组无感清晰度切换流分配相同优先级，并配置更低优先级的容灾流。如果高优先级流组播放失败，SDK 会自动尝试容灾组。更多信息，请参见[流容灾策略和主备流切换](https://docs.byteplus.com/en/docs/24/106184#stream-fallback-strategy-and-primary-backup-stream-switching)。

> **警告**

* > 无感清晰度切换功能目前仅适用于 FLV 流。

* > 确保已集成 1.50.100 或更高版本的 Player SDK。

### 前提条件

准备同一源流不同清晰度档位的拉流地址。

如果你使用 BytePlus MediaLive 的推流地址进行直播，请确保已完成以下操作：

* **添加域名**：在同一域名空间下添加推流域名和拉流域名。更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

* **配置转码**：在域名空间下为不同清晰度档位添加转码配置。更多信息，请参见[管理转码配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

* **获取拉流地址**：获取源流和每个转码流的拉流地址。

   * **用于调试**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成拉流地址。

      * **地址类型**：选择**拉流地址**。

      * **域名**：选择用于转码配置的域名空间下的拉流域名。

      * **AppName** 和 **StreamName**：输入与推流地址匹配的 `AppName` 和 `StreamName`。例如，如果推流地址为 `rtmp://push.example.com/live/test?authinfo`，则 `AppName` 为 `live`，`StreamName` 为 `test`。

   * **用于生产**：调用 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 动态生成拉流地址。

      **示例**

      下表列出了不同清晰度档位的示例 FLV 拉流地址和码率。

   |清晰度档位 |FLV 拉流地址 |码率（kbps） |
   |---|---|---|
   |原画（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
   |超高清（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
   |高清（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
   |标清（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
   |流畅（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

### 操作步骤

1. 配置各清晰度档位的流，并将 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) 设置为 `YES`，以启用无感清晰度切换。

   ```objectivec
   // 配置各清晰度档位的流。
   // 原画档位。
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // 替换为原画档位的实际拉流地址。
   playStreamOrigin.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // 清晰度档位标识。
   playStreamOrigin.type = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamOrigin.bitrate = 2500; // 码率，单位 kbps。
   
   // UHD 档位。
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // 替换为 UHD 档位的实际拉流地址。
   playStreamUHD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // 清晰度档位标识。
   playStreamUHD.type = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamUHD.bitrate = 2500; // 码率，单位 kbps。
   
   // HD 档位。
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // 替换为 HD 档位的实际拉流地址。
   playStreamHD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamHD.resolution = VeLivePlayerResolutionHD; // 清晰度档位标识。
   playStreamHD.type = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamHD.bitrate = 1000; // 码率，单位 kbps。
   
   // SD 档位。
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // 替换为 SD 档位的实际拉流地址。
   playStreamSD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamSD.resolution = VeLivePlayerResolutionSD; // 清晰度档位标识。
   playStreamSD.type = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamSD.bitrate = 800; // 码率，单位 kbps。
   
   // LD 档位。
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv"; // 替换为 LD 档位的实际拉流地址。
   playStreamLD.format = VeLivePlayerFormatFLV; // 流格式。
   playStreamLD.resolution = VeLivePlayerResolutionLD; // 清晰度档位标识。
   playStreamLD.type = VeLivePlayerStreamTypeMain; // 用于区分主流和备流的流类型。
   playStreamLD.bitrate = 500; // 码率，单位 kbps。
   
   // 创建播放源。
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // 添加各清晰度档位的流。
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:5];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // 配置默认起播清晰度档位。
   streamData.defaultResolution = VeLivePlayerResolutionSD;
   
   // 启用无感清晰度切换。
   streamData.enableSmoothSwitchResolution = YES;
   
   // 配置播放源。
   [self.livePlayer setPlayStreamData:streamData];
   
   // 开始播放。
   [self.livePlayer play];
   ```

2. 直播过程中，当观众手动切换清晰度档位时，你可以调用 [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) 平滑切换清晰度档位。示例代码如下。

   ```objectivec
   // 切换到 UHD 档位。
   [self.livePlayer switchResolution:VeLivePlayerResolutionUHD];
   ```

3. 添加 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回调，以监听清晰度档位切换结果。当清晰度档位变化时，SDK 可以触发该回调，并返回切换后的清晰度档位、切换原因等信息。

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *_Nonnull)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason;
   ```

## 截图

该功能支持截取当前视频帧并生成图片。

1. 调用 [snapshot](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#snapshot) 进行截图。该功能仅在播放过程中生效。

```objectivec
int result = [self.livePlayer snapshot];
```

2. 截图完成后，将触发 [onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onsnapshotcomplete-image) 回调函数，并返回图片数据。

```objectivec
- (void)onSnapshotComplete:(TVLManager *)player image:(UIImage *)image  {
  // 回调函数通过 image 返回图片数据。
}
```

## SEI

补充增强信息（SEI）是嵌入直播流中的附加数据。你可以使用 SEI 传输自定义数据或元数据。

> **说明**

> 仅高级版和试用版 license 支持 SEI。

### 操作步骤

* 字符串 SEI 消息

   1. 在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前，启用播放器的 [enableSei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablesei) 属性。启用该属性后，播放器会接收字符串 SEI 消息。示例代码如下。

      ```objectivec
      // 创建 VeLivePlayerConfiguration 实例。
      VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
      
      // 启用接收字符串 SEI 消息。
      config.enableSei = YES;
      
      // 配置播放器的初始设置。
      [self.livePlayer setConfig:config];
      ```

   2. 当播放器收到字符串 SEI 消息时，会触发 [onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) 回调。示例代码如下。

      ```objectivec
      - (void)onReceiveSeiMessage:(TVLManager *_Nonnull)player message:(NSString *_Nonnull)message  {
         // 字符串 SEI 消息回调。
      }
      ```

* 二进制 SEI 消息

   1. 在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前，启用播放器的 [enableBinarySei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablebinarysei) 属性。启用该属性后，播放器会接收二进制 SEI 消息，并且不再触发字符串 SEI 消息回调。示例代码如下。

      ```objectivec
      // 创建 VeLivePlayerConfiguration 实例。
      VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
      
      // 启用接收二进制 SEI 消息。
      config.enableBinarySei = YES;
      
      // 配置播放器的初始设置。
      [self.livePlayer setConfig:config];
      ```

   2. 当播放器收到二进制 SEI 消息时，会触发 [onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) 回调。示例代码如下。

      ```objectivec
      - (void)onReceiveBinarySeiMessage:(TVLManager *_Nonnull)player message:(NSData *_Nonnull)message  {
         // 二进制 SEI 消息回调。
      }
      ```

## 订阅视频数据

通过订阅解码后的视频数据，你可以获取视频帧数据，用于自定义处理和渲染。播放器支持多种视频帧回调格式，并提供对应的参数和格式选项。

### 前提条件

下表说明视频帧像素格式和视频数据封装格式的枚举及含义。

|格式类型 |枚举 |描述 |
|---|---|---|
|视频帧像素格式 |VeLivePlayerPixelFormatNV12 |NV12 |
|视频帧像素格式 |VeLivePlayerPixelFormatI420 |I420 |
|视频数据封装格式 |VeLivePlayerVideoBufferTypePixelBuffer |CVPixelBufferRef |
|视频数据封装格式 |VeLivePlayerVideoBufferTypeSampleBuffer |CVSampleBufferRef |
|视频数据封装格式 |VeLivePlayerVideoBufferTypeNSData |NSData |

订阅视频数据前，请根据需求选择格式组合。该组合必须遵循下表所示的 [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerpixelformat) 和 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideobuffertype) 之间的映射关系。

|像素格式/封装格式 |VeLivePlayerPixelFormatNV12 |VeLivePlayerPixelFormatI420 |
|---|---|---|
|**VeLivePlayerVideoBufferTypePixelBuffer** |支持（性能最优） |不支持 |
|**VeLivePlayerVideoBufferTypeSampleBuffer** |支持 |不支持 |
|**VeLivePlayerVideoBufferTypeNSData** |支持 |支持 |

### 操作步骤

1. 调用播放器的 [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enablevideoframeobserver-pixelformat-buffertype) API 启用或禁用视频帧数据订阅。API 参数说明如下表所示。

   |参数 |类型 |描述 |
   |---|---|---|
   |enable |BOOL |是否启用视频帧回调。 |
   |pixelFormat |VeLivePlayerPixelFormat |视频帧像素格式。 |
   |bufferType |VeLivePlayerVideoBufferType |视频数据封装格式。 |

   示例代码如下。

   ```objectivec
   [self.livePlayer enableVideoFrameObserver:YES pixelFormat:VeLivePlayerPixelFormatNV12 bufferType:VeLivePlayerVideoBufferTypePixelBuffer];
   ```

2. SDK 通过 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 的 [onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) 回调返回解码后的视频帧数据。示例代码如下。

   ```objectivec
   - (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
      // 视频帧数据回调。
   }
   ```

   [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideoframe) 参数说明如下表所示。

   |参数 |类型 |描述 |
   |---|---|---|
   |bufferType |VeLivePlayerVideoBufferType |视频帧数据封装格式。 |
   |pixelFormat |VeLivePlayerPixelFormat |视频帧像素格式。 |
   |width |NSInteger |视频帧宽度，单位 px。 |
   |height |NSInteger |视频帧高度，单位 px。 |
   |pts |int64_t |视频帧渲染时间戳，单位 ms。 |
   |pixelBuffer |CVPixelBufferRef |当 `bufferType` 为 `VeLivePlayerVideoBufferTypePixelBuffer` 时的视频数据。 |
   |sampleBuffer |CMSampleBufferRef |当 `bufferType` 为 `VeLivePlayerVideoBufferTypeSampleBuffer` 时的视频数据。 |
   |data |NSData\* |当 `bufferType` 为 `VeLivePlayerVideoBufferTypeNSData` 时的视频数据。 |

## 订阅音频数据

通过订阅解码后的音频数据，你可以执行自定义音频处理和渲染。Player SDK 支持订阅 PCM Float32 采样格式和 NSData 封装格式的音频数据。

|VeLivePlayerAudioBufferType |音频数据封装格式 |
|---|---|
|[VeLivePlayerAudioBufferTypeNSData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayeraudiobuffertype) |NSData |

### 操作步骤

1. 调用播放器的 [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enableaudioframeobserver-enablerendering) API 启用或禁用音频帧数据订阅。API 参数说明如下表所示。

   |参数 |类型 |描述 |
   |---|---|---|
   |enable |BOOL |是否启用音频帧回调。 |
   |enableRendering |BOOL |是否启用播放器渲染。如果播放器不需要内部渲染音频，请将该参数设置为 `NO`。 |

   示例代码如下。

   ```objectivec
   // 订阅音频帧数据，并启用播放器内部音频渲染。
   [self.livePlayer enableAudioFrameObserver:YES enableRendering:YES];
   ```

2. SDK 通过 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 协议中定义的 [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) 回调返回解码后的音频帧数据。示例代码如下。

   ```objectivec
   - (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
      // 音频帧数据回调。
   }
   ```

   [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayeraudioframe) 参数说明如下表所示。

   |参数 |数据类型 |描述 |
   |---|---|---|
   |bufferType |VeLivePlayerAudioBufferType |音频帧数据封装格式。 |
   |sampleRate |int |音频采样率，单位 Hz。 |
   |channels |int |声道数。 |
   |bitDepth |int |音频位深。 |
   |pts |CMTime |音频渲染时间戳，单位 ms。 |
   |data |NSData\* |PCM 音频数据。 |
   |samples |int |音频采样数。 |

## 超分辨率

超分辨率（SR）是一种从低分辨率图像重建高分辨率图像的技术。实时 SR 使用算法实时将低分辨率帧重建为高分辨率帧。它会生成高分辨率帧，并显示在屏幕上。SR 可增强视频细节和对比度，提高视频清晰度和观看体验。

> **说明**

> 仅高级版和试用版 license 支持 SR。

### 前提条件

从 1.51.300.2\-premium 版本开始，如需使用 SR 功能，集成 Player SDK 时，除拉流组件外还需要添加 `LivePull-BMF` 依赖。更多信息，请参见[集成适用于 iOS 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)。

### 操作步骤

1. 从 1.51.300.2\-premium 版本开始，导入 `VeLivePlayer+SuperResolution.h` 头文件。

   **动态库**

```objectivec
   #import <TTSDKFramework/VeLivePlayer+SuperResolution.h>
   ```

   **静态库**

```objectivec
   #import <TTSDK/VeLivePlayer+SuperResolution.h>
   ```

2. 调用播放器的 [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setenablesuperresolution) 方法启用或禁用 SR。

   ```objectivec
   [self.livePlayer setEnableSuperResolution:YES];
   ```

   |名称 |类型 |描述 |
   |---|---|---|
   |enable |BOOL |是否启用 SR。默认值为 `NO`。<br><br><br>* `YES`：启用 SR。<br><br>* `NO`：禁用 SR。 |

3. 如果启用 SR 失败，播放器会通过 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 的 [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) 回调通知你。方法签名如下。

   ```objectivec
   - (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
   ```

   启用 SR 失败的常见原因如下。

   * 实际流分辨率不在 SR 支持范围内。

   * 实际流帧率不在 SR 支持范围内。

   * 当前设备型号不支持 SR。

## 自定义 HTTP 请求头

为播放器的 HTTP 请求设置自定义请求头。该功能常用于传递鉴权 token、cookie、业务特定链路追踪标识等附加信息。

> **说明**

> 仅 1.50.200.3\-premium 及更高版本支持自定义 HTTP 请求头。

### 操作步骤

开始播放前，你可以通过播放器的高级 API [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) 设置自定义 HTTP 请求头。调用 `setProperty:value:` 时，需要传入 `key-value` 配置。

**Key**

|参数名称 |类型 |描述 |
|---|---|---|
|VeLivePlayerKeySetParamsHttpHeaders |NSString |用于配置自定义 HTTP 请求头的属性键。 |

**Value**

该值为 `NSDictionary` 对象，包含用于设置自定义 HTTP 请求头的 `key-value` 对。

* `Key`：`NSString` 类型。请求头名称。

* `Value`：`NSString` 类型。请求头值。

示例代码如下。

* 设置一个 HTTP 请求头

   ```objectivec
   [self.livePlayer setProperty:VeLivePlayerKeySetParamsHttpHeaders value:@{@"key": @"value"}]; // 替换为实际请求头名称和值。
   ```

* 设置多个 HTTP 请求头

   ```objectivec
   [self.livePlayer setProperty:VeLivePlayerKeySetParamsHttpHeaders
                             value:@{
                               @"key1": @"value1", // 替换为实际请求头名称和值。
                               @"key2": @"value2", // 替换为实际请求头名称和值。
                               @"key3": @"value3" // 替换为实际请求头名称和值。
                             }];
   ```

## H.265 硬解码和软解码

使用高级版或试用版 license 的 SDK 默认启用 H.265 硬解码和软解码。播放 H.265 编码的视频流时，SDK 会先尝试使用 H.265 硬解码。如果 H.265 硬解码失败，SDK 会自动切换到 H.265 软解码。

调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前，通过播放器的初始配置启用或禁用硬解码。示例代码如下。

```objectivec
VeLivePlayerConfiguration *config = [VeLivePlayerConfiguration new];
config.enableHardwareDecode = YES;
[self.livePlayer setConfig:config];
```

* `YES`：启用硬解码。

* `NO`：禁用硬解码，仅使用软解码。

你可以监听 [onStatistics:statistics:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) 回调，并使用 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerstatistics) 的 [isHardWareDecode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-ishardwaredecode) 属性，判断当前流是否使用硬解码。

## 视频锐化

视频锐化会在设备本地增强视频，以提高清晰边缘和纹理细节。播放过程中，SDK 可以实时增强边缘和纹理细节，使视频看起来更清晰，并提升观看体验。

> **说明**

> 仅高级版和试用版 license 支持视频锐化。

### 前提条件

从 1.51.300.2\-premium 版本开始，如需使用视频锐化功能，集成 Player SDK 时，除拉流组件外还需要添加 `LivePull-BMF` 依赖。更多信息，请参见[集成适用于 iOS 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)。

### 操作步骤

1. 从 1.51.300.2\-premium 版本开始，导入 `VeLivePlayer+SuperResolution.h` 头文件。

   **动态库**

```objectivec
   #import <TTSDKFramework/VeLivePlayer+SuperResolution.h>
   ```

   **静态库**

```objectivec
   #import <TTSDK/VeLivePlayer+SuperResolution.h>
   ```

2. 调用播放器的 [setEnableSharpen:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) 方法启用或禁用视频锐化。

   ```objectivec
   [self.livePlayer setEnableSharpen:YES];
   ```

   |名称 |类型 |描述 |
   |---|---|---|
   |enable |BOOL |是否启用视频锐化。默认值为 `NO`。<br><br><br>* `YES`：启用视频锐化。<br><br>* `NO`：禁用视频锐化。 |

3. 如果启用视频锐化失败，播放器会通过 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 的 [onError:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) 回调通知你。方法签名如下。

   ```objectivec
   - (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
   ```

   启用视频锐化失败的常见原因如下。

   * 实际流分辨率不在视频锐化支持范围内。

   * 实际流帧率不在视频锐化支持范围内。

   * 当前设备型号不支持视频锐化。

   * 当前 license 不支持视频锐化。

## 画中画

画中画（PiP）会将播放器窗口缩小为屏幕一角的小悬浮窗，允许观众在浏览其他内容或使用其他应用时继续观看直播。该功能有助于提升观看体验。

### 前提条件

* 你已集成 1.51.200.4\-premium 或更高版本的 SDK。

   > **说明**

   > 如果你使用的 SDK 版本早于 1.51.200.4\-premium，可以集成 PiP 方案以启用 PiP 功能。更多信息，请参见 [PiP 方案](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d46ae38e)。

* iOS 15.0 或更高版本。

* 在 Xcode 中，为应用 target 启用 PiP 所需的后台模式。

   1. 在 **Signing & Capabilities** 页签上，单击  **+**  **Capability**，然后双击 **Background Modes**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8ccac9b131740cab54e2d294a73885f~tplv-goo7wpa0wc-topic.webp)

   2. 在 **Background Modes** 区域，选择 **Audio, AirPlay, and Picture in Picture**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0782c08333eb411b8f27c201d6968bb3~tplv-goo7wpa0wc-topic.webp)

* 引导观众在设备上启用系统级 PiP 设置：进入 **Settings** \> **General** \> **Picture in Picture**，并开启 **Start PiP Automatically**。启用该设置后，应用进入后台时即可自动开始 PiP 播放。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08beec9cc01b4adb9ca988dc02c4b569~tplv-goo7wpa0wc-topic.webp)

### 操作步骤

1. 导入 PiP 头文件。

   **静态库集成**

如果你使用 SDK 的静态库集成方式，请使用 `#import <TTSDK/VeLivePlayer+PictureInPicture.h>` 导入 PiP 头文件。

   **动态库集成**

如果你使用 SDK 的动态库集成方式，请使用 `#import <TTSDKFramework/VeLivePlayer+PictureInPicture.h>` 导入 PiP 头文件。

2. 检查当前设备是否支持 PiP。

   ```objectivec
   if ([TVLManager isPictureInPictureSupported]) {
       // 根据当前设备是否支持 PiP 实现你的业务逻辑。
   }
   ```

3. 初始化 SDK 内置播放器并启用 PiP。PiP 默认禁用。

   ```objectivec
   TVLManager *player = [[TVLManager alloc]initWithType:VeLivePlayerTypeOwn];
   player.enablePictureInPicture = YES;
   ```

   > **说明**

   > PiP 仅支持 SDK 内置播放器，不支持系统播放器。

4. 配置应用进入后台时是否自动启动 PiP。该设置仅对当前播放器生效，不会更改观众设备上的系统级 PiP 设置。

   默认情况下，应用进入后台时会自动启动 PiP。如果你不希望自动启动 PiP，请将 [canStartPictureInPictureAutomaticallyFromInline](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline) 设置为 `NO`。以下示例代码启用应用进入后台时自动启动 PiP。

   ```objectivec
   player.canStartPictureInPictureAutomaticallyFromInline = YES;
   ```

5. 如果你希望监听 PiP 开始、停止等生命周期事件，可以设置以下 PiP delegate 属性。SDK 内部已经处理 PiP 所需的关键 delegate 方法，因此大多数情况下你无需自行实现。

   ```objectivec
   @property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate;
   @property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate;
   ```

6. 播放开始后，你可以手动启动 PiP。

   ```objectivec
   [player startPictureInPicture];
   ```

   如果 PiP 当前处于活动状态，你可以手动停止 PiP。

   ```objectivec
   [player stopPictureInPicture];
   ```

7. 如需检查 PiP 是否已成功启动，请调用以下方法。

   ```objectivec
   BOOL isStarted = [TVLManager isPictureInPictureStarted];
   ```

8. 如需手动更新 PiP 播放按钮状态和进度显示，请调用 [invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate)。SDK 会在内部自动更新播放按钮状态和进度显示，因此大多数情况下你无需调用此方法。

   ```objectivec
   [player invalidatePictureInPicturePlaybackState];
   ```

### PiP 方案

如果你使用的 SDK 版本早于 1.51.200.4\-premium，可以集成 [PiP 方案](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/blob/main/VeLivePictureInPicture.podspec)以启用 PiP 功能。

根据需要选择以下任一集成方式：

**在线集成**

```objectivec
pod 'VeLivePictureInPicture', :git => 'https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git', :branch => 'main'
```

**本地集成**

将以下文件从 [PiP 方案](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/blob/main/VeLivePictureInPicture.podspec)复制到你的本地项目：

* `VeLivePictureInPicture` 目录中的源文件

* `VeLivePictureInPicture.podspec`

`path` 表示这些文件相对于本地项目中 `Podfile` 的路径。例如，如果这些文件与本地项目中的 `Podfile` 位于同一目录，请将 `path` 设置为 `./`。

```objectivec
pod 'VeLivePictureInPicture', :path => './'
```

集成 PiP 方案后，你可以使用与 SDK 1.51.200.4\-premium 或更高版本相同的 API。更多信息，请参见[操作步骤](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#97a32559)。

## 高级 API 配置

### 移除 SDK 自动追加的查询参数

Player SDK 可能会向拉流地址追加 `session_id` 等查询参数。这些参数用于标识拉流会话，并在排查播放问题时帮助在客户端日志和 CDN 日志中定位同一会话。如需阻止 SDK 在实际请求 URL 中包含自动追加的查询参数，请启用此功能。启用后，SDK 追加的查询参数会从实际请求 URL 中移除，而原始拉流地址中已存在的查询参数会保留。

> **说明**

> 仅 1.52.1 及更高版本支持移除 SDK 自动追加的查询参数。

#### 操作步骤

开始播放前，你可以使用播放器的高级 [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) API，配置是否移除 SDK 自动追加的查询参数。调用 `setProperty:value:` 时，需要传入 `key-value` 配置。

**Key**

|参数名称 |类型 |描述 |
|---|---|---|
|VeLivePlayerKeySetParamsRemoveQueryParams |NSString |用于移除 SDK 自动追加查询参数的属性键。 |

**Value**

`Value` 是一个 `NSNumber` 值，表示是否移除 SDK 自动追加的查询参数。默认值为 `0`。

* `1`：移除 SDK 自动追加的查询参数。

* `0`：保留 SDK 自动追加的查询参数。

示例代码如下。

```objectivec
[self.livePlayer setProperty:@"VeLivePlayerKeySetParamsRemoveQueryParams" value:@1];
```

**效果示例**

例如，拉流地址为：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```

当 SDK 发起播放请求时，会自动追加 `session_id`。

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901&session_id=xxx
```

启用此功能后，请求 URL 不再包含 `session_id`，但会保留原始拉流地址中的 `auth_key` 鉴权参数：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```
