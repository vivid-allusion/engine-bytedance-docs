---
title: "短剧视频 - Flutter 集成"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-flutter-integration-zh-CN"
---

本文提供 BytePlus VideoOne Flutter 端集成短剧场景的方案概览，并为您详细介绍如何快速集成短剧 Demo。

<span id="集成方案概览"></span>
## 集成方案概览

BytePlus VideoOne 针对短剧场景提供集成方案。下表列出该解决方案的详细信息。


|**集成方案** |集成短剧 Demo |
|---|---|
|**方案说明** |基于短视频场景控件，支持剧集切换、切换页面无缝续播、付费内容解锁播放等短剧场景特色功能。 |
|**适用客户** |适用于开发新 App、可切换业务接口层逻辑的客户。 |
|**开发工作** |仅需切换业务接口层逻辑和转换数据结构。 |
|**上线时间** |最快一周上线 |
|**相关链接** |[VideoOneSolutions/Client/Flutter](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Flutter) |


<span id="集成短剧-demo"></span>
## 集成短剧 Demo

<span id="步骤-1：下载源码"></span>
### 步骤 1：下载源码

运行以下命令将源码下载至本地：

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions.git
```


<span id="步骤-2：拷贝代码"></span>
### 步骤 2：拷贝代码

将以下文件夹拷贝至您的项目根目录下：

```Bash
# 短剧核心代码
lib/src/solutions/minidrama
# 静态资源
assets/minidrama
```


<span id="步骤-3：配置证书"></span>
### 步骤 3：配置证书


1. 下载证书，放在 `assets/minidrama/licenses` 目录下：


```Bash
- assets/minidrama
    - licenses
        - ttsdk.lic
```



2. 在 `pubspec.yaml` 下配置对应的静态资源路径：


```YAML
 assets:
     # licenses
    - assets/minidrama/licenses/ttsdk.lic

    # other icon png
    - assets/minidrama
```



3. 打开 `lib/src/solutions/minidrama/constants/common.dart` 文件，修改 `APP_ID` 与 `LICENSE_PATH` 字段：


```Dart
const APP_ID = "your app id"; // BytePlus 对应 app id
const LICENSE_PATH = 'assets/minidrama/licenses/ttsdk.lic'; // 对应证书路径
```


<span id="步骤-4：配置依赖"></span>
### 步骤 4：配置依赖


1. 在 `pubspec.yaml` 下配置对应的依赖模块：


```YAML
dependencies:
  android_id: ^0.4.0
  byteplus_vod: ^1.44.2-1
  collection: ^1.18.0
  connectivity_plus: ^6.1.0
  crypto: ^3.0.6
  device_info_plus: ^11.1.1
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  flutter_screenutil: ^5.9.3
  fluttertoast: ^8.2.8
  http: ^1.2.2
  logger: ^2.5.0
  shared_preferences: ^2.3.3
  wakelock_plus: ^1.2.8
  carousel_slider: ^5.0.0
  lottie: ^3.2.0
  intl: ^0.20.2
  loader_overlay: ^4.0.4+1
  visibility_detector: ^0.4.0+2
  path_provider: ^2.1.5

byteplus_vod:
  sub_spec: premium
```



2. 配置 Android 相关依赖。详情请参考[短剧视频 - Android 集成](https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-android-integration-zh-CN)。

   a. 增加以下仓库配置。

   * 在 `android/settings.gradle` 文件的 `pluginManagement.repositories` 中增加 Volcengine Maven 仓库：

   ```Groovy
   maven { url "https://artifact.bytedance.com/repository/Volcengine/" }
   ```
   

   * 在 `android/build.gradle` 文件的 `allprojects.repositories` 中增加 BytePlus 公共 Maven 仓库：

   ```Groovy
   maven { url "https://artifact.byteplus.com/repository/public/" }
   ```
   

   b. 在 `android/app/build.gradle` 文件中添加以下依赖：

   ```Groovy
   dependencies {
       implementation "com.squareup.okhttp3:okhttp:4.2.1"
   }
   ```
   

   c. 在项目的 `proguard-rules.pro` 文件中添加 BytePlus VOD Player 所需的混淆规则：

   ```Bash
   -keep class com.ss.ttm.** {*;}
   -keep class com.ss.ttvideoengine.** {*;}
   -keep class com.ss.mediakit.** {*;}
   -keep class com.ss.texturerender.** {*;}
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.pandora.common.applog.**{*;}
   -keep class com.pandora.vod.VodSDK {*;}
   -keep class com.bytertc.volcbaselog.VolcBaseLogConfig{*;}
   -keep class com.bytertc.volcbaselog.VolcBaseLogNative{*;}
   ```
   

3. 配置 iOS 相关依赖。详情请参考[短剧视频 - iOS 集成](https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-ios-integration-zh-CN)。在 `Podfile` 文件中配置对应的源：

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   


<span id="步骤-5：初始化播放器模块"></span>
### 步骤 5：初始化播放器模块

在 `lib/src/settings/settings_controller.dart` 中初始化 player：

```Dart
Future<void> loadSettings() async {
  _themeMode = await _settingsService.themeMode();

  // init byteplus_vod sdk
  await PlayerController.initTTSDK();

  // Important! Inform listeners a change has occurred.
  notifyListeners();
}
```


<span id="适配业务逻辑"></span>
## 适配业务逻辑

参考以下步骤快速将短剧 Demo 与您的业务逻辑进行适配：


1. 数据层适配，以快速接入短剧场景的核心功能。您需要：

   1. 替换业务接口：App 需要实现 `lib/src/solutions/minidrama/service` 中定义的 API。

   2. 转换数据结构：App 将业务 AppServer 返回的数据结构转换成短剧 Demo 中定义的数据结构，以便快速复用 Demo 中的现有业务逻辑。

2. 适配付费内容解锁播放等短剧场景特色功能。


<span id="短剧-demo-源码结构说明"></span>
### 短剧 Demo 源码结构说明

```Bash
├── android/                 # Android 平台特定代码
│   └── app/                 # Gradle 模块配置
│       └── build.gradle     # Android 构建配置
├── ios/                     # iOS 平台特定代码
│   ├── Runner.xcodeproj/    # Xcode 项目配置
│   └── Runner/              # iOS 应用主体
│       └── Runner.entitlements # 权限配置文件
├── lib/
│   ├── src/
│   │   ├── settings/        # 设置模块（当前核心组件）
│   │   │   ├── settings_controller.dart # 业务逻辑控制
│   │   │   └── settings_service.dart    # 数据持久层
│   │   ├── solutions/minidrama/ # 短剧项目入口
│   │   │   ├── constants/   # 常量配置项
│   │   │   ├── meta/        # 数据层
│   │   │   ├── pages/       # 短剧主页面
│   │   │   ├── service/     # 短剧接口层
│   │   │   ├── utils/       # 短剧工具类
│   │   │   ├── video_sdk/   # 播放器 SDK
│   │   │   └── widgets/     # 短剧组件
│   └── main.dart            # 应用入口
├── assets/
│   ├── minidrama/
│   │   └── licenses/        # 证书文件
│   ├── images/              # 图片资源
│   └── lotties/             # Lottie 动画资源
└── pubspec.yaml             # 依赖管理核心文件
```


<span id="数据层适配"></span>
### 数据层适配

<span id="数据结构介绍"></span>
#### 数据结构介绍

为构建短剧业务逻辑，短剧 Demo 层定义了 `drama_meta`（短剧信息）、`video_meta`（视频信息）、`comment_meta`（评论）数据结构。您需要将自己的应用服务端返回的数据结构转换为上述数据结构。数据结构具体说明如下表所示。


|类 |字段 |类型 |是否必须 |描述 |
|---|---|---|---|---|
|`drama_meta`<br><br>（短剧信息） |`dramaId` |String |必需 |短剧 ID。 |
||`dramaTitle` |String |必需 |短剧名称。 |
||`dramaCoverUrl` |String |必需 |短剧封面 URL。 |
||`dramaPlayTimes` |int |必需 |播放次数。 |
||`dramaVideoOrientation` |int |必需 |视频方向。<br><br>\- `0`：竖屏。<br><br>\- `1`：横屏。 |
||`dramaLength` |int |必需 |短剧总集数。 |
||`newRelease` |bool |可选 |是否展示 New 图标，默认 `false`。<br><br>\- `true`：展示。<br><br>\- `false`：隐藏。 |
|`video_meta`<br><br>（单集视频信息） |`vid` |String |必需 |视频 ID。 |
||`name` |String |可选 |视频标题。 |
||`duration` |double |必需 |视频时长（单位：秒）。 |
||`coverUrl` |String |必需 |封面地址。 |
||`playAuthToken` |String |可选 |视频数据源的 `PlayAuthToken`。AppServer 可使用 BytePlus VOD Server SDK 签发。 |
||`subtitleAuthToken` |String |可选 |视频数据源获取字幕的 Token。AppServer 可使用 BytePlus VOD Server SDK 签发。 |
||`videoModel` |String |可选 |视频数据源的 `VideoModel`。 |
||`playTimes` |int |可选 |播放次数。 |
||`caption` |String |可选 |视频标题文案。 |
||`subtitle` |String |可选 |视频副标题。 |
||`like` |int |可选 |视频喜欢次数。 |
||`comment` |int |可选 |视频评论次数。 |
||`height` |int |必需 |视频高度。 |
||`width` |int |必需 |视频宽度。 |
||`order` |int |必需 |视频在剧集中的次序。 |
||`uid` |int |可选 |上传者用户 ID。 |
||`vip` |bool |必需 |是否需要付费解锁。 |
||`displayType` |int |必需 |在 For you 页的短剧卡片展示类型。<br><br>\- `0`：TEXT，不带封面图。<br><br>\- `1`：COVER，带封面图。 |
|`comment_meta`<br><br>（评论） |`content` |String |可选 |评论内容。 |
||`name` |String |可选 |用户名称。 |
||`uid` |int |可选 |用户 ID。 |
||`like` |int |可选 |点赞数量。 |
||`createTime` |String |可选 |创建时间。 |
||`liked` |bool |可选 |是否点赞。 |


<span id="接口替换"></span>
#### 接口替换


1. 在 `lib/src/solutions/minidrama/constants/api.dart` 文件下，替换对应接口的路径：


```Dart
// get feed if drama
const GET_DRAMA_FEED = "/videoone/drama/v1/getDramaFeed";

const GET_DRAMA_CHANNEL = '/videoone/drama/v1/getDramaChannel';
const GET_VIDEO_COMMENT = '/videoone/drama/v1/getVideoComments';

// get Recommend
const GET_DRAMA_LIST = "/videoone/drama/v1/getDramaList";
const UNLOCK_DRAMA  = "/videoone/drama/v1/getDramaDetail";
```



2. `lib/src/solutions/minidrama/service` 目录下记录了当前接口的调用，您可根据自己的业务进行取值替换。
