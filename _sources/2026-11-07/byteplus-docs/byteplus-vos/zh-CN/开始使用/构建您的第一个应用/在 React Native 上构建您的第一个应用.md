---
title: "在 React Native 上构建您的第一个应用"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-react-native-zh-CN"
---

要快速构建一个跨平台视频应用，您可以参考本指南运行 VideoOne Demo 项目。本文档为您提供在 React Native 框架内搭建项目并利用 React Native SDK 的分步操作说明。完成后，您将拥有一套代码库，可同时生成具备强大视频播放功能的 Android 和 iOS 应用。

## 前置条件

请在开始前完成以下任务。建议您集中记录每项任务获得的信息，便于项目搭建过程中随时查阅。

|**任务** |**任务依赖功能** |**任务说明** |**完成后获得的信息** |
|---|---|---|---|
|1. 注册 BytePlus 账号。<br><br>2. 为账号创建访问密钥。 |全部功能 |* [注册 BytePlus 账号](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [创建访问密钥](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* 访问密钥 ID（AK）<br><br>* 访问密钥（SK） |
|1. 激活 BytePlus VOD 服务。<br><br>2. 创建 VOD 应用并获取许可证。<br><br>> 如已创建 BytePlus MediaLive 应用，请绑定已有应用，无需新建。 |视频播放 |* [步骤 1：启用 BytePlus VOD 服务](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [应用管理](https://docs.byteplus.com/byteplus-vod/docs/sdk-management)<br><br>* [许可证管理](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* 应用 ID<br><br>* BytePlus VOD SDK 许可证文件 |

## 开发环境

* **Watchman、Xcode 和 CocoaPods：** Xcode 需为 14.1 或更高版本。

* **Android JDK 和 Android Studio**

* **Node.js：** 建议使用 18.0 或更高版本。

* **实体移动设备：**

   * Android 6.0 或更高版本。

   * iOS 13.0 或更高版本。

## 操作流程

### 克隆项目

请按照以下步骤克隆 Demo 项目：

1. 访问 GitHub 并克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 仓库。

2. 打开终端，将当前目录切换到 `Client/ReactNative`，即项目根目录，并使用集成开发环境（IDE）打开该目录。

### 安装依赖项

1. 全局安装 Expo CLI。

   ```Shell
   npm install -g @expo/cli
   ```

2. 安装项目依赖项。

   ```Shell
   npm install
   ```

3. 进入 ios 目录并安装 iOS 依赖项。

   ```Shell
   cd ios && pod install
   ```

### 配置应用服务

打开 `services/api.ts` 文件，将 `SERVER_HOST` 修改为您的应用服务器地址。

如需使用 BytePlus 提供的 Demo 应用服务器，请将 `SERVER_HOST` 字段设置为 `videocloud.byteplusapi.com`。

> **说明**

> 该地址仅供测试使用，不能用于生产环境。

### 配置 VOD 许可证

将您在前置准备环节获得的许可证文件重命名为 `ttsdk.lic`，并移动到 `assets` 目录下。

> **说明**

> 本项目通过 [Expo 插件](https://docs.expo.dev/config-plugins/plugins/) 将许可证文件复制到原生资源目录。您也可以参考 [React Native Player SDK: Integrating the SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart) 中的指引，将许可证文件分别放置在对应的 `ios` 和 `android` 目录下。

### 项目配置

请按照以下步骤确保 App ID 与证书一致。

1. 在 `android/app/build.gradle` 文件中，将 `applicationId` 修改为与证书对应的 Android 包名。

2. 使用 Xcode 打开 `ios` 目录。在 **Signing & Capabilities** 部分，将 **Bundle Identifier** 修改为与证书对应的 Bundle ID，并完成其他配置文件的设置。

### 编译并运行项目

请按照以下步骤编译并运行项目。

1. 执行下方命令以启动 Metro Server。启动完成后，终端会显示调试用二维码。

   ```Shell
   npm run start
   ```

2. 构建调试应用：

   * Android

      1. 将电脑与 Android 手机连接。

      2. 执行下方命令，并在弹出的设备列表中选择已连接的手机设备。

         ```Shell
         npm run android
         ```

      3. 在手机上允许应用安装请求以完成安装。

   * iOS

      4. 将电脑与 iPhone 连接。

      5. 执行下方命令，并在弹出的设备列表中选择已连接的 iPhone 设备。项目会自动在您的手机上安装应用。

      `Shell npm run ios`

### 体验应用

打开应用后，您可以探索并体验短剧解决方案。

|![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/159babc54d5d42c1af358e6f9105572a~tplv-goo7wpa0wc-image.image) |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03abd5dd80ce4af2b5234c251de3f8f7~tplv-goo7wpa0wc-image.image) |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2adc5303e4f14a47be08b7f7b923b36f~tplv-goo7wpa0wc-image.image) |
|---|---|---|

## 代码解析

### 项目结构

Demo 项目的目录树如下：

```Plain
Client/ReactNative/
├── app/                    # App screens (Expo Router)
│   ├── _layout.tsx         # Root layout
│   ├── index.tsx           # Home screen
│   ├── drama_channel.tsx   # Drama channel screen
│   ├── drama_player.tsx    # Video player screen
│   └── +not-found.tsx      # 404 screen
├── components/             # Reusable components
│   ├── player/             # Video player components
│   │   ├── VideoPlayer.tsx      # Main video player
│   │   ├── EpisodePlayer.tsx    # Episode player wrapper
│   │   ├── PlaybackControls.tsx # Playback control component
│   │   └── index.ts
│   ├── modals/             # Modal components
│   ├── feed/               # Content feed components
│   ├── ui/                 # UI components
│   ├── shared/             # Shared components
│   ├── drama/              # Drama-related components
│   │   ├── DramaCarousel.tsx  # Drama carousel
│   │   ├── DramaCover.tsx     # Drama cover
│   │   ├── DramaList.tsx      # Drama list
│   │   └── index.ts
│   └── index.ts            # Component exports
├── services/               # API services
│   ├── api.ts              # Base API client
│   ├── dramaService.ts     # Drama data service
│   ├── unlockService.ts    # Content unlock service
│   └── userService.ts      # User management service
├── hooks/                  # Custom React hooks
├── utils/                  # Utility functions
├── types/                  # TypeScript type definitions
├── constants/              # App constants
├── assets/                 # Static assets
│   ├── images/             # Images and icons
│   ├── minidrama/          # Drama-specific assets
│   └── ttsdk.lic           # SDK license file
├── android/                # Android-specific files
│   ├── app/                # Android app module
│   │   ├── build.gradle    # App build configuration
│   │   └── src/            # Android source code
│   ├── build.gradle        # Project build configuration
│.  ├── ...
├── ios/                    # iOS-specific files
│   ├── videoonern/         # iOS app target
│   │   ├── AppDelegate.swift
│   │   ├── ...
│   ├── videoonern.xcodeproj/     # Xcode project
│   ├── videoonern.xcworkspace/   # Xcode workspace
│   ├── Podfile             # CocoaPods dependencies
│   ├── Podfile.lock        # CocoaPods lock file
│   └── Pods/               # CocoaPods dependencies
├── plugins/                # Expo config plugins
│   ├── withATSConfig.js    # ATS configuration plugin
│   ├── withLicense.js      # License file plugin
│   ├── withPodfileSources.js # Podfile sources plugin
│   └── xcodeUtils.js       # Xcode utilities
├── app.json                # Expo app configuration
├── tsconfig.json           # TypeScript configuration
├── package.json            # npm package configuration
├── expo-env.d.ts           # Expo TypeScript definitions
├── eslint.config.js        # ESLint configuration
├── detection_tool.py       # Detection utility
├── LICENSE                 # License file
├── README.md               # English documentation
└── README-zh_CN.md         # Chinese documentation
```

### 技术架构

#### 核心技术

* **React Native**：跨平台移动开发框架

* **Expo**：拥有丰富 API 和组件的开发平台及工具链

* **TypeScript**：类型安全的 JavaScript 超集

* **Expo Router**：基于文件的路由系统，简化导航管理

#### 架构设计

以下主要介绍 VOD 短剧场景功能的设计：

1. **组件化架构**：按功能模块组织组件，提高代码复用性

   * `player/`：视频播放相关组件

   * `modals/`：弹窗组件

   * `feed/`：内容流组件

   * `ui/`：通用 UI 组件

   * `shared/`：共享组件

   * `drama/`：短剧相关组件

2. **服务层分离**：按业务领域分离 API 服务

   * `dramaService.ts`：短剧数据管理

   * `unlockService.ts`：内容解锁服务

   * `userService.ts`：用户管理服务

3. **自定义 hooks**：封装可复用的业务逻辑

   * `useDramaChannel.ts`：短剧频道数据管理

   * `useColorScheme.ts`：主题色管理

4. **类型安全**：全面的 TypeScript 类型定义

   * 完整的接口定义

   * 严格的类型检查

   * 优异的开发体验

### 功能介绍

以下介绍短剧解决方案的功能。有关播放器各功能的具体用法，请参考文档 [React Native Player SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart)。

#### 短剧功能

##### 播放功能

* **预加载视频**：支持自动策略的视频预加载

* **预渲染视频**：支持视频播放器的预渲染策略。

* **高质量视频流**：支持多种清晰度选项（720p、480p 等）

* **播放控制**：播放/暂停、进度条、音量控制

* **多倍速播放**：支持 0.5x 至 2.0x 的播放速度

* **横竖屏切换**：自动适配屏幕方向，提供不同控制界面

* **进度管理**：支持拖动快进与播放位置记忆

##### 用户交互功能

* **点赞系统**：支持点赞/取消点赞，实时计数更新

* **评论功能**：用户评论与互动

* **触觉反馈**：提供触觉反馈，提升用户体验

##### 变现功能

* **广告解锁**：观看广告解锁付费内容

* **VIP 订阅**：付费解锁全部内容

* **批量解锁**：一次解锁多集内容

##### 投屏功能

video\-one\-rn Demo 在应用层实现投屏。TTVideoEngine 负责本地播放，Demo 协调设备选择、原生投屏会话和播放交接。

* **AirPlay（iOS）** ：使用系统 AVRoutePickerView 和原生 AVPlayer 中转播放器。在路由选择和中转启动期间，本地播放器静音；确认跳转完成、媒体就绪和外部播放激活后，暂停本地播放。

* **Google Cast（Android）** ：使用 react\-native\-google\-cast 选择接收端，通过 RemoteMediaClient 加载解析后的媒体 URL、元数据和起始进度。连接期间即暂停本地播放，此时尚未确认远端正在显示视频。

* **停止投屏并返回本地播放**：iOS 上，停止投屏会打开系统选择器，用户需选择本地输出；未改变外部路由而仅关闭选择器，不会结束投屏。Android 会主动请求终止 Cast 会话，并抑制延迟到达的自动恢复回调。仅停止投屏会保留当前播放页；待执行的 iOS 返回操作会在路由回到本地且中转状态为 idle 后继续执行。

* **页面行为**：已连接或投屏状态会显示全屏覆盖层、禁用剧集翻页、关闭选集和解锁对话框，并防止本地播放完成后自动切换下一集。页面焦点和前台检查会防止隐藏的本地播放器与当前活动播放器同时恢复播放。

两个平台都使用报告的远端进度、保存的远端进度和本地进度中的最大值，恢复现有播放器。远端向后拖动后，该位置可能与接收端的精确最终位置不同。iOS 的播放交接分支在恢复前检查投屏前的播放状态；Android 会自动恢复本地播放。独立的页面焦点和前台处理逻辑也会影响恢复。

投屏需要接收端能够访问和解码的已解析 URL。当前请求不会转发本地播放器的自定义请求头、cookies 或 DRM 许可证配置。请在实体设备和目标接收端上验证签名 URL、加密媒体、播放交接和音频行为。

原生配置、控制器集成、各平台流程和验证场景，请参见[短剧视频 - React Native 集成：开发投屏功能](https://docs.byteplus.com/docs/byteplus-vos/short-drama-integration-by-reactnative-zh-cn#developing-the-casting-feature)。

##### 内容管理

* **短剧轮播**：首页短剧推荐轮播

* **内容列表**：分类展示短剧内容

* **推荐系统**：基于用户行为的智能推荐
