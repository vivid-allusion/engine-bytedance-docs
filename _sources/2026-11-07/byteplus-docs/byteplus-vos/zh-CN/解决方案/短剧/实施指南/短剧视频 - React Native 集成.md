---
title: "短剧视频 - React Native 集成"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-integration-by-reactnative-zh-cn"
---

本文面向希望基于 VideoOne React Native Demo 集成短剧能力的开发者，介绍从获取源码、准备环境、配置项目和运行 Demo，到替换业务 API、理解代码结构的完整流程。

## 解决方案概述

React Native 短剧方案基于 BytePlus React Native VOD SDK 和 Expo 技术栈构建，提供移动端短剧场景的核心能力，包括短剧列表浏览、频道页导航、竖屏连续播放、剧集解锁、用户互动和推荐展示。对于已完成基础环境搭建的团队，建议复用 Demo 中的页面、组件和服务层，再逐步替换面向业务的实现。

|维度 |说明 |建议 |
|---|---|---|
|目标场景 |移动端短剧播放与分集消费 |适合希望快速验证短剧产品的团队 |
|核心能力 |选集、续播、倍速、清晰度切换、解锁、点赞、评论和推荐 |尽量复用 Demo 中现有的页面和服务边界 |
|集成工作量 |主要集中在 API 替换、数据映射和 UI 定制 |先跑通 Demo，再逐步替换业务模块 |

## 集成思路

与 Web 端的集成路径类似，React Native 短剧集成建议分两个阶段进行。第一阶段，完整运行官方 Demo，确认播放能力、许可证配置、原生项目和设备调试均正常。第二阶段，逐步将 Demo 数据源、解锁逻辑和视觉样式替换为自己的业务实现。分阶段推进有助于区分环境问题、SDK 配置问题和业务集成问题，更容易定位故障。

第一阶段，准备环境，配置服务地址和许可证，并在 iOS 和 Android 设备上运行 Demo。

第二阶段，替换短剧和频道 API、用户和解锁逻辑，映射业务数据结构，并定制样式与交互。

## 前置条件

开始集成 React Native 短剧前，请确保已满足运行 Demo 所需的基础条件。如果尚未完成基础项目搭建，建议先阅读同系列文档**在 React Native 上构建您的第一个应用**，再回到本文进行业务集成。

|项目 |用途 |获得的信息或资源 |
|---|---|---|
|BytePlus 账号和 AK/SK |访问云服务并进行业务服务鉴权 |Access Key 和 Secret Key |
|VOD 服务和应用 |提供视频播放能力 |App ID 和许可证文件 |
|React Native 开发环境 |运行 iOS 和 Android 项目 |Node、Expo CLI、Xcode、CocoaPods 和 Android Studio |
|实体测试设备 |验证移动端短剧交互 |Android 6.0+ 或 iOS 13.0+ 设备 |

## 运行 Demo

### 操作步骤

1. **获取源码**

   React Native Demo 位于 `VideoOneSolutions` 仓库的 `Client/ReactNative` 目录。建议直接基于该项目集成，以复用现有的短剧页面、服务层和组件结构。

   ```Shell
   git clone https://github.com/byteplus-sdk/VideoOneSolutions
   cd VideoOneSolutions/Client/ReactNative
   ```

> 如果目标是快速集成短剧场景，建议从 Demo 开始，替换其中面向业务的部分，避免从空项目搭建。

2. **安装依赖项**

   下载源码后，安装 JavaScript 依赖和 iOS 原生依赖。项目基于 Expo 和 React Native，JavaScript 依赖用于页面、路由和业务逻辑，`ios` 目录中的 Pods 用于原生集成。

   1. 安装 Expo CLI。

   2. 在项目根目录安装 npm 依赖。

   3. 进入 `ios` 目录，运行 `pod install`，安装 iOS 原生依赖。

   ```Shell
   npm install -g @expo/cli
   npm install
   cd ios && pod install
   ```

3. **配置应用服务**

   Demo 通过服务层封装业务数据。将 Demo 集成到自己的短剧业务时，通常先替换应用服务地址。可以先使用 Demo 服务验证完整页面流程，再切换到自己的生产服务。

   打开 `services/api.ts` 文件，更新 `SERVER_HOST` 等服务地址配置。如果仅验证 Demo，可以暂时保留 Demo 服务器地址；正式集成时，将其替换为自己的业务服务域名。

   > **说明**

   > Demo 服务地址仅适用于测试和验证，不能直接用于生产环境。

4. **配置许可证和原生项目**

   核心播放能力依赖 VOD SDK 许可证。将获取的许可证文件重命名为 `ttssdk.lic`，放入 `assets` 目录。当前 Demo 已通过 Expo Config Plugins 将许可证复制到原生资源目录。

   除许可证外，还需确保 Android 包名、iOS Bundle Identifier 和签名配置与证书一致，否则应用可能无法正常安装或运行。

   * Android：更新 `android/app/build.gradle` 中的 `applicationId`。

   * iOS：在 Xcode 的 `Signing & Capabilities` 中更新 `Bundle Identifier`，并完成签名相关配置。

5. **运行短剧 Demo**

   完成基础配置后，在实体设备上运行项目。短剧场景依赖滑动切换、沉浸式全屏播放、横竖屏适配和触觉反馈，模拟器无法充分验证这些体验，因此强烈建议使用实体设备测试。

   ```Shell
   npm run start
   npm run android
   npm run ios
   ```

   |命令 |用途 |说明 |
   |---|---|---|
   |`npm run start` |启动 Metro Server |提供资源打包和调试入口 |
   |`npm run android` |安装并启动 Android 调试应用 |建议在实体设备上验证滑动和解锁体验 |
   |`npm run ios` |安装并启动 iOS 调试应用 |建议在 iPhone 上验证播放、选集和交互 |

## 将 Demo 适配到自己的业务

Demo 稳定运行后，逐层替换业务逻辑。建议顺序为**数据层 → 页面入口 → 播放体验 → 变现逻辑 → 互动功能**，以兼顾实现效率和调试稳定性。

### 操作步骤

1. **替换 API**

   `services/` 目录是业务适配的主要入口，通常可按以下职责进行映射：

   * `dramaService.ts`：短剧列表、频道数据、推荐内容流和短剧详情获取。

   * `unlockService.ts`：解锁状态、广告解锁、批量解锁和 VIP 解锁逻辑。

   * `userService.ts`：用户信息、登录状态和用户相关行为。

   * `api.ts`：共享请求客户端、主机配置和通用请求处理。

   集成时，建议保留现有服务函数边界，仅替换内部请求实现和字段映射，尽量减少页面层的改造。

2. **适配数据结构**

   Web 短剧集成指南强调替换 API 和转换数据结构，React Native 版本同样适用。UI 组件通常需要稳定的前端数据模型，因此建议在服务层将后端响应字段统一转换为前端模型，避免在多个页面组件中分别适配不同的后端数据结构。

   > **说明**

   > 建议先将后端字段转换为统一的短剧、剧集、用户和解锁状态前端模型，再将这些模型传递给页面和组件。

3. **替换页面入口和路由**

   项目使用 Expo Router 组织页面，短剧相关入口主要位于以下文件：

   |**页面文件** |**职责** |**建议定制内容** |
   |---|---|---|
   |`app/index.tsx` |首页入口 |可替换为自己的首页或流量入口页 |
   |`app/drama_channel.tsx` |短剧频道页 |适配频道推荐、专题或分类逻辑 |
   |`app/drama_player.tsx` |短剧播放页 |重点替换短剧加载、续播、解锁和导航逻辑 |

4. **调整播放体验**

   播放器逻辑主要位于 `components/player/` 和播放器配置工具中。短剧业务通常需要关注以下方面：

   * 预加载和预渲染策略，减少切换剧集时的等待。

   * 竖屏播放体验和横屏控制布局。

   * 进度持久化和续播行为。

   * 倍速、清晰度和选集控件的显示策略。

   * 自动播放下一集，以及播放结束后的推荐衔接。

   如果业务目标是提升连续观看的流畅度，优先调整预加载策略、下一集衔接和解锁成功后的无缝续播。

5. **替换变现和解锁逻辑**

   Demo 已提供广告解锁、VIP 解锁和批量解锁等短剧变现示例。相关 UI 和弹窗逻辑主要位于：

   * `components/modals/VipUnlockModal.tsx`

   * `components/modals/UnlockMultipleModal.tsx`

   * `services/unlockService.ts`

   * `components/ui/AdComponent.tsx`

   可以将其替换为自己的变现模式，例如金币解锁、订阅会员、激励广告或混合解锁策略。建议在服务层和状态层集中处理解锁策略，避免将判断逻辑分散到多个页面。

6. **替换互动和推荐逻辑**

   短剧产品通常还包含社交互动和内容分发能力。Demo 已包含点赞、评论和推荐等基础功能，集成时重点处理以下内容：

   * 替换点赞和取消点赞 API。

   * 替换评论列表和评论提交 API。

   * 替换推荐召回和推荐展示逻辑。

   * 调整频道页、播放页和短剧结束页的推荐衔接策略。

## 开发投屏功能

VideoOne React Native Demo 在应用层实现投屏。iOS 通过系统 AirPlay 路由选择器和原生 AVPlayer 中转播放器处理播放；Android 通过 react\-native\-google\-cast 在 Google Cast 接收端加载媒体。TTVideoEngine 负责本地播放，Demo 协调投屏 UI、会话和页面交互。集成时需要同时接入 React Native 组件及对应的原生配置。

以下说明当前 `video-one-rn` 的实现。两个平台都通过 `useCast()` 暴露控制器，但启动、本地暂停和停止流程有所不同。

### 投屏方式和媒体要求

|项目 |iOS |Android |
|---|---|---|
|协议 |AirPlay |Google Cast |
|设备选择 |`AVRoutePickerView` |`showCastDialog()` |
|远端播放 |原生 `AirPlayRelay` 管理 AVPlayer |接收端通过 `RemoteMediaClient.loadMedia()` 加载 URL |
|本地播放暂停时机 |选择设备和启动期间静音；确认 `casting` 后暂停 |`isConnecting`、`isConnected` 或 `isCasting` 为 true 时暂停 |
|停止操作 |在系统选择器中选择 iPhone 或其他本地输出 |调用 `endCurrentSession(true)` |

媒体 URL 来自 `VideoPlayer.tsx` 当前播放信息中的 `MainPlayUrl`，通过 `onPlayUrlChange` 传递给 `EpisodePlayer`，播放回调持续更新进度。投屏需要接收端能够访问和解码的实际 URL。所有投屏接口的时间值均以秒为单位。是否支持投屏取决于解析后的 URL 和接收端能力，而非应用播放模式的名称。

当前中转请求不会转发本地播放器的自定义请求头、cookies 或 DRM 许可证配置。对于签名 URL、加密媒体或受限网络，请先验证接收端的访问和解密能力。手机播放成功并不代表接收端兼容。

### 原生项目配置

* **iOS**

   将 `ios/videoonern/AirPlayRelay.m` 和 `AirPlayRoutePickerViewManager.m` 加入应用 target，以导出桥接模块和原生视图。原生模块使用 `Playback`、`Default` 和 `LongFormVideo` 配置并激活 Audio Session。请检查本地网络使用说明，以及应用实际使用的 Bonjour 服务。Demo 还在 `UIBackgroundModes` 中包含 `audio`。

   本文介绍的 iOS 播放路径使用 AirPlay，无需在应用代码中初始化 `GCKCastContext`。当前 Pod 锁定文件仍包含 react\-native\-google\-cast 自动链接引入的 Google Cast 依赖；存在依赖并不意味着当前投屏路径使用该依赖。

* **Android**

   当前 `package.json` 声明 `react-native-google-cast: ^4.9.1`，应用 Gradle 文件显式依赖 `com.google.android.gms:play-services-cast-framework:21.5.0`。`CastOptionsProvider.kt` 配置接收端和媒体通知。Manifest 注册 `OPTIONS_PROVIDER_CLASS_NAME`，并声明互联网、网络状态和 Wi\-Fi 状态权限。`MainActivity.onCreate` 初始化 `RNGCCastContext.getSharedInstance(this)`。

   Demo 使用 Google 默认媒体接收端 ID `CC1AD845`。如果应用需要自定义接收端，请替换为已注册的 ID，并更新相关配置。Expo 项目应在 `app.json` 中保留 `./plugins/withGoogleCast`；该插件生成 Android 配置，并补充 iOS 本地网络设置。如果手动维护原生项目，请检查生成的文件。

### 控制器和页面集成

`app/drama_player.tsx` 创建一个 `castController`，通过 `EpisodePlayer` 传递给按钮和播放器。页面也使用该控制器渲染投屏覆盖层。集成已有页面时，请保留这一数据流，确保按钮和页面共享会话状态。

```tsx
const castController = useCast();

<CastButton
  castController={castController}
  videoUrl={currentPlayUrl}
  currentTime={currentPlayTime}
  title={dramaTitle}
  coverUrl={dramaCoverUrl}
/>
```

示例中的媒体和进度变量由页面维护。iOS 上，`CastButton` 渲染原生选择器，`VideoPlayer` 通过 `AirPlayRelay.configureMedia()` 提供媒体。Android 上，建立会话后，按钮使用传入的 URL、进度和元数据调用 `startCasting()`。

|接口或状态 |当前行为 |
|---|---|
|`isConnecting` |iOS 上映射为 `routeSelecting / routeSelected / starting`；Android 上跟随会话连接事件。 |
|`isConnected / isCasting` |iOS 上均使用原生快照中的 `isCasting`。Android 上分别表示已建立会话，以及由媒体加载或状态回调设置的投屏标志。 |
|`remotePosition` |两个平台均以秒为单位更新。iOS 设备标签为 AirPlay；Android 读取接收端的友好名称。 |
|`showCastPicker / startCasting / updateCastMedia / seekRemote` |Android 上执行对应操作。iOS hook 中这些接口不执行操作，投屏由原生选择器和中转模块驱动。 |
|`stopCasting` |主动结束 Android 会话。iOS 上仅在路由已回到本地时恢复 Audio Session，不能替代系统选择器中的路由选择。 |
|`isAvailable` |iOS 上检查原生桥接模块是否存在。Android 上当前始终为 false，因此不表示设备发现结果，也不能作为隐藏按钮的可靠条件。 |

### iOS：AirPlay 中转流程

仅当剧集可播放、播放器处于活动状态且页面拥有导航焦点时，才配置 AirPlay 媒体。`configureMedia()` 提供 URL、`startTime`、标题、封面和 `localWasPlaying`。选择器显示前调用 `beginRouteSelection()`，关闭后调用 `endRouteSelection()`。原生层还监听路由通知，以确定实际输出。

```text
idle → routeSelecting → routeSelected → starting → casting
casting → stopping → idle
starting → failed
```

在 `routeSelecting`、`routeSelected` 和 `starting` 期间，React Native 播放器静音，并记录此前是否正在播放。原生 AVPlayer 同样以静音状态启动，跳转到传入进度后开始播放。只有跳转完成、`readyToPlay` 和 `externalPlaybackActive` 均满足时，中转播放器才取消静音并报告 `casting`，随后 React Native 暂停本地播放器。

原生模块通过 `AirPlayRelayStateChanged` 发送快照，通过 `AirPlayRelayProgress` 大约每秒发送一次进度更新。快照包含 `generation`、状态、路由和外部播放标志、进度以及本地恢复标志。原生异步操作和 React Native 进度监听器会检查 generation，丢弃过期回调。启动超时为 12 秒；失败时报告错误，并清理中转播放器、观察者和定时器。

覆盖层的停止投屏操作使用另一个 `AVRoutePickerView`。显示前调用 `beginStopRouteSelection()`，用户在系统面板中选择本地输出。保留外部路由而仅关闭面板，不算停止投屏。路由回到本地后，原生层释放中转播放器、恢复 Audio Session，并报告 `idle`；播放器随后恢复本地播放。

### Android：Google Cast 中转流程

用户未连接时点击按钮，会打开设备对话框，并记录连接后加载媒体的意图。如果已连接，则直接请求加载媒体。`useCast` 监听会话启动、恢复、结束和连接失败事件，通过 Remote Media Client 订阅媒体状态和进度，并在组件卸载时移除监听器。

加载请求包含 `contentId / contentUrl`、根据 URL 扩展名推断的 MIME 类型、标题、封面、`startTime` 和 `autoplay: true`。最多尝试加载 3 次：先立即尝试，再分别等待 500 和 1200 毫秒后重试。扩展名推断覆盖 HLS、DASH 和 WebM，其他情况提交 MP4。MIME 类型推断并不能确认接收端支持该媒体。

Android 在连接期间暂停本地播放：`EpisodePlayer` 将 `isConnecting || isCasting || isConnected` 传递给本地播放器。加载成功或媒体状态回调会更新投屏标志，但仅凭该标志不能证明电视正在显示视频。当前加载失败主要输出控制台日志。如果应用需要向用户显示错误，或在失败后自动恢复本地播放，需要补充相应处理。

主动停止时，先抑制自动恢复并清除 UI 状态，再调用 `endCurrentSession(true)`，并在有限范围内检查会话是否终止。抑制逻辑会忽略延迟到达的会话恢复和媒体回调，直到用户再次主动选择设备或启动投屏。完成有限检查不等于已经确认接收端停止播放。

### 本地恢复和页面生命周期

两个平台都使用当前快照或远端进度、保存的远端进度以及本地进度中的最大值进行恢复。这种策略倾向于避免向后跳转，不能保证总是恢复到接收端的精确最终位置。远端向后拖动等场景需要单独验证。恢复时使用现有播放器实例。

* **iOS 恢复**

   对于需要恢复的 `idle` 或 `failed` 快照，播放器先请求恢复 Audio Session，再跳转本地进度并取消静音。此播放交接分支仅在 `shouldResumeLocal` 为 true、投屏前本地正在播放且播放器当前已暂停时调用播放。独立的页面焦点和前台处理逻辑也会恢复播放；如果应用需要严格保留用户的暂停状态，请一并检查这些入口。

* **Android 恢复**

   投屏标志清除后，活动的本地播放器跳转进度并直接调用播放，不会保留投屏前已暂停的意图。如果应用要求两个平台采用相同的暂停恢复策略，需要显式实现。

页面使用 `isCasting || isConnected` 显示全屏投屏覆盖层、关闭选集和解锁对话框、禁用列表翻页，并防止本地播放完成后自动切换下一集。这些 UI 限制基于已连接或投屏状态，不能据此确认每个连接过渡阶段都被锁定。

仅使用停止投屏操作会保留当前播放页。iOS 会保存待执行的导航操作，仅在 `idle` 且 `routeActive` 为 false 后执行。返回操作不会强制改变系统路由，用户仍需通过停止投屏入口选择本地输出。Android 页面返回按钮在停止尝试结束后再执行导航；其他页面移除事件也会请求停止，并通过退出保护避免对同一会话重复停止。

为防止隐藏页面恢复播放，iOS 媒体配置和状态订阅仅作用于拥有导航焦点的活动播放器。回到前台时的恢复也会检查导航焦点、活动状态和投屏暂停条件。页面失去焦点时，即使尚未收到正在播放的回调，也会暂停本地播放器。当前后台 AppState 处理逻辑会暂停本地播放器，但不会统一终止远端会话。

### 参考代码和验证

|文件 |检查内容 |
|---|---|
|`hooks/useCast.ts` |跨平台状态、Android 会话和媒体请求，以及 iOS 快照映射。 |
|`components/cast/CastButton.tsx`<br><br>`CastActiveOverlay.tsx` |启动入口、投屏覆盖层和各平台的停止入口。 |
|`components/player/VideoPlayer.tsx`<br><br>`EpisodePlayer.tsx` |解析后的 URL、进度、静音、暂停和本地恢复。 |
|`app/drama_player.tsx` |共享控制器、UI 限制和导航处理。 |
|`ios/videoonern/AirPlayRelay.m`<br><br>`AirPlayRoutePickerViewManager.m` |原生状态机、Audio Session、中转播放器和系统选择器。 |
|`android/app/src/main/java/com/byteplus/videoone/rn/CastOptionsProvider.kt`<br><br>`plugins/withGoogleCast.js` |接收端、通知和原生项目配置。 |

源码回归检查覆盖 AirPlay 状态机、中转清理和过期回调、投屏覆盖层交互，以及页面焦点恢复。集成后，请在实体手机和目标接收端上验证以下场景，检查视频、音频和进度。状态标志和测试通过不能替代接收端测试。

|场景 |验证内容 |
|---|---|
|开始投屏 |剧集和起始进度正确，接收端显示视频，交接后本地无残留音频。 |
|取消、失败和网络断开 |选择器取消、启动超时、接收端加载失败和 URL 过期后的状态、音频和恢复操作。 |
|停止和路由变化 |iOS 选择本地输出与未改变路由而仅关闭面板的区别；Android 停止后延迟到达的会话恢复回调。 |
|进度和暂停意图 |接收端向前和向后拖动、投屏前暂停的行为，以及各平台恢复策略的影响。 |
|页面生命周期 |覆盖层、剧集限制、停止后留在当前页、待执行导航、前后台切换，以及隐藏页面不发出音频。 |

## 理解代码结构

为高效修改 React Native 短剧 Demo，建议按**页面 → 组件 → 服务 → 工具**的顺序理解项目，先建立页面级数据流的整体认识，再查看单个 API 文件。

### 关键目录

|**目录** |**用途** |**关注重点** |
|---|---|---|
|`app/` |页面和路由入口 |理解短剧入口、频道页和播放页之间的关系 |
|`components/player/` |播放器相关组件 |关注播放控制、续播、选集和屏幕方向逻辑 |
|`components/modals/` |解锁和选集对话框 |关注变现和短剧消费流程 |
|`components/feed/` |内容流和推荐展示组件 |关注推荐卡片和信息面板适配 |
|`components/drama/` |短剧业务组件 |关注短剧封面、短剧列表和轮播展示 |
|`services/` |服务抽象层 |API 替换的主要入口 |
|`hooks/` |可复用的状态逻辑 |关注频道数据获取和主题相关逻辑 |
|`utils/` |工具和播放器配置 |关注播放器设置、数据转换和图片处理 |

### 建议阅读顺序

1. 先阅读 `app/drama_channel.tsx` 和 `app/drama_player.tsx`，理解路由和交互链路。

2. 再阅读 `services/dramaService.ts`、`unlockService.ts` 和 `userService.ts`，理解页面数据来源。

3. 随后阅读 `components/player/` 和 `components/modals/`，理解播放、选集和解锁行为。

4. 最后查看 `hooks/`、`types/` 和 `utils/`，补全对状态管理、类型定义和工具实现的认识。

## 建议集成检查清单

* 完成投屏集成，确保 iOS AirPlay 和 Android Chromecast 中转播放均正常。

* 验证投屏断点续播，确保结束投屏后应用内播放器从正确位置恢复。

* 验证投屏与 PiP 的互斥逻辑，防止同时激活。

* 在没有可用投屏设备或发生网络错误时，提供合理的错误提示。

* 先跑通官方 Demo，确认播放、许可证和原生环境均正常。

* 定义自己的频道、短剧、剧集、解锁状态和用户信息业务 API 模型。

* 在 `services/` 层完成统一的数据映射。

* 在实体设备上验证续播、选集、屏幕方向变化和解锁流程。

* 替换推荐位、运营内容和视觉样式，以适配品牌。

* 发布前补充数据分析、监控和生产配置。

## 后续步骤

如果希望快速将 Demo 转为可投入生产的业务应用，接下来重点完成三件事：确定前后端数据契约并完成服务层映射，定义解锁流程和用户权益体系，在实体设备上反复验证滑动切换、续播、解锁弹窗和推荐衔接。这些部分稳定后，Demo 就具备了演进为实际短剧产品的基础。

> **说明**

> 建议结合[在 React Native 上构建您的第一个应用](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-react-native-zh-CN)阅读本文：该文档介绍如何运行项目，本文介绍如何将短剧能力集成到自己的业务中。
