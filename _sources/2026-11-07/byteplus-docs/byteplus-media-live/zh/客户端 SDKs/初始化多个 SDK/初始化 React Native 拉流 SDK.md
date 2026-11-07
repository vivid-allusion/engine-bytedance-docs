---
title: "初始化 React Native 拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-rn-zh-CN"
---

本主题介绍如何初始化 React Native 拉流 SDK。你只需初始化 SDK 一次。

<span id="de94af35"></span>
## 前提条件


* 你已按照 [集成 React Native 的拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-CN) 提供的说明将 SDK 集成到你的项目中。

* 你已获取应用 ID 及其他基本信息。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。


<span id="270ca9ed"></span>
## 初始化 SDK

打开 `src/store/pull/player.ts` 文件，并进行如下修改。

```JavaScript
import {initEnv} from '@byteplus/react-native-live-pull';

initEnv({
  AppID: 'appId', // 应用 ID，可在 MediaLive 控制台的 SDK 管理页面获取。
  // 应用名称。
  AppName: Platform.select({
      android: 'xxx', 
      ios: 'xxx'
  })

  // The channel through which to download the app.你也可以使用此参数区分不同环境的应用构建，例如生产、测试和调试。
  AppChannel: Platform.select({
      android: 'GoogleStore',
      ios: 'AppStore',
      default: ''
  }),

  // The version number of your Android app.有效的版本号应包含两个或以上分隔符，例如 "1.3.2"。
  AppVersion: '1.0.0',
  
  // 许可证文件名。如果更换许可证文件，需要在此处修改文件名。为快速验证 SDK，你可以替换原始许可证文件（ttsdk.lic）的内容。
  LicenseUri: {
    android: 'assets:///ttsdk.lic', 
    ios: 'ttsdk.lic'
  },
  UserUniqueID: 'VeLiveQuickStartDemo',
});
```


下表描述了初始化参数：


|**参数** |**必填** |**数据类型** |**参数说明** |**示例** |
|---|---|---|---|---|
|AppID |是 |String |应用 ID，即你的 SDK 应用的唯一标识。详情请参见 [创建 SDK 应用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)。 |`123456` |
|AppName |是 |String |应用名称，即你的 SDK 应用的名称。详情请参见 [创建 SDK 应用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)。 |`video_demo` |
|AppVersion |是 |String |你的应用版本号。有效的版本号应包含两个或以上分隔符，例如 "1.3.2"。 |`1.3.2` |
|AppChannel |是 |String |下载应用的渠道。你也可以使用此参数区分不同环境的应用构建，例如生产、测试和调试。 |`google_play` |
|LicenseUri.android |是 |String |Android 许可证文件的本地路径。 |`assets:///license1/license1_test.lic` |
|LicenseUri.ios |是 |String |iOS 许可证文件的本地路径。 |`assets:///license2/license2_test.lic` |


<span id="f3d9c23d"></span>
## 日志上传

默认情况下，已开启自动 SDK 日志上传，用于排查生产环境问题并在质量平台展示数据。为保护敏感数据，你可以在 [初始化 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn-zh-CN#270ca9ed) 前调用 `openLog: false` 禁用日志上传。
