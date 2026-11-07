---
title: "短剧视频 - Android 集成"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-android-integration-zh-CN"
---

要快速为您的 Android 应用添加完整的短剧视频功能，您可以集成 BytePlus VideoOne 短剧 Demo。本指南详细介绍了整个流程，包括下载源代码、配置依赖项，以及自定义业务逻辑、数据模型和诸如付费内容解锁等特定功能。

<span id="ea713aea"></span>
# 集成方案概览

BytePlus VideoOne 提供了四种专为短剧视频定制的集成方案。下表突出显示了这四种方案之间的区别。


|**方案 / 简介** |**集成短剧 Demo** |**集成短剧视频控件** |**集成 PlayerKit 控件** |**集成播放器 SDK** |
|---|---|---|---|---|
|说明 |专为短剧视频打造。该方案支持防录屏、剧集切换、页面切换时无缝续播、付费内容解锁及其他短剧专属功能。 |该方案提供短剧播放框架，不包含其他业务需求。 |基于播放器 SDK 构建。该方案可在 View 层实现视频播放，并隐藏播放器使用细节。 |该方案直接集成播放器 SDK。 |
|目标客户 |正在开发新应用且能够替换业务 API 的客户。 |正在开发新应用或已有应用且能够替换播放器架构的客户。 |正在开发新应用或已有应用且能够替换播放器架构的客户。 |已有应用且希望通过复用现有播放代码并替换播放器内核快速上线短剧功能的客户。具备强开发能力、丰富播放器经验且有充足时间开发新应用的客户。 |
|开发要求 |客户仅需替换业务 API 并转换数据结构。 |客户需自行实现网络连接、短剧播放器 UI、播放页面切换及支付功能。 |客户端需自行实现网络连接、短剧播放器界面、播放页面切换及支付功能。 |客户端需自行实现播放器功能及短剧相关功能。 |
|上市时间 |最短一周 |最短两周 |两周至一个月 |约一个月 |
|相关链接 |本文档 |[vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama) |[vod-playerkit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod/vod-playerkit) |[Android 播放器 SDK：集成 SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android) |


<span id="cea5302c"></span>
# 运行 Demo

在集成短剧 Demo 之前，建议您参考文档[运行 Demo (Android)](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-CN)并体验短剧视频功能。

<span id="f751fbf7"></span>
# 集成短剧 Demo

短剧 Demo 的源代码位于[vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama)文件夹下的[VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main)仓库中。其目录结构如下：

```Bash
.
├── app                    # 应用入口
├── build.gradle 
├── component              # 公共组件
│   ├── avatars            # 头像资源
│   ├── loginkit           # 登录
│   └── solution-base      # 基础库
│   └── ...
└── solutions              # 解决方案
    ├── vod                # 视频播放场景
    │   ├── vod-playerkit  # VOD播放器套件
    │   ├── vod-scenekit   # VOD场景套件
    │   └── ...
    ├── vod-mini-drama     # 短剧场景
    └── ...
```


<span id="19027710"></span>
## 步骤 1：下载源代码

运行以下命令，将源代码下载到本地设备：

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions
cd Client/Android
```


<span id="7597ea21"></span>
## 步骤 2：复制代码

将以下文件夹复制到您项目的根目录，并保持目录结构为[VideoOneSolutions/Client/Android](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android)：

```Bash
component/solution-base
component/avatars
component/loginkit
component/rtc-toolkit

solutions/vod/vod-common
solutions/vod/vod-demo
solutions/vod/vod-playerkit
solutions/vod/vod-scenekit
solutions/vod/vod-settingskit
solutions/vod/vod-input-media
solutions/vod-mini-drama
```


<span id="d0a0f691"></span>
## 步骤 3：配置 Maven 仓库

在项目根目录下的 `build.gradle` 文件中添加以下配置。

```Groovy
allprojects {
    repositories {
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
        maven { url 'https://artifact.byteplus.com/repository/public/' }

        google()
        mavenCentral()
    }
}

apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
```


<span id="4ffbbc75"></span>
## 步骤 4：SDK 集成

要将 SDK 集成到您的项目中，请在模块的 build.gradle 文件中添加所需的库。按如下方式添加库：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">获取最新版本号，请参见<a href="https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN">客户端 SDK 组件</a>。</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.43.300.3"
    // BytePlus VOD SDK dependencies
    implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdkVersion"
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="d1098f9a"></span>
## 步骤 5：导入短剧模块


1. 在 `settings.gradle` 文件中添加 Demo 模块：


```Groovy
include ':app'
include ':component:avatars'
include ':component:solution-base'
include ':component:loginkit'
include ':component:rtc-toolkit'
// vod
include ':solutions:vod:vod-common'
include ':solutions:vod:vod-demo'
include ':solutions:vod:vod-input-media'
// vod-playerkit
include ':solutions:vod:vod-playerkit'
include ':solutions:vod:vod-playerkit:vod-player-utils'
include ':solutions:vod:vod-playerkit:vod-player'
include ':solutions:vod:vod-playerkit:vod-player-ve'
// vod-scenekit
include ':solutions:vod:vod-scenekit'
include ':solutions:vod:vod-settingskit'

include ':solutions:vod-mini-drama'
```



2. 在您的应用 `app/build.gradle` 文件中添加对 `:solutions:vod-mini-drama` 模块的依赖：


```Groovy
dependencies {
    implementation project(':solutions:vod-mini-drama')
}
```



3. 同步 Gradle 文件。如果 Android Studio 未报错，则说明 Demo 模块已成功导入。


<span id="f0bf822e"></span>
## 步骤 6：配置权限与混淆规则


1. 将 BytePlus VOD Player 所需的混淆规则添加到项目的 `proguard-rules.pro` 文件中。


```Python
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



2. 在 `AndroidManifest.xml` 文件中声明 SDK 所需的权限。


```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">更多信息请参见<a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android">集成 SDK</a>。</div>


<span id="fa2fcde4"></span>
## 步骤 7：初始化短剧 Demo

调用 VodSDK 的 `init` 方法以初始化 Demo。

```Java
public class App extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        VodSDK.init(this,
            "your app id",
            "your app name",
            "your app channel",
            "your app version",
            "singapore",
            "assets:///your_license_name.lic",
        );
    }
}
```


<span id="10eb1e02"></span>
## 步骤 8：集成短剧页面

您可以参考以下代码，直接使用[DramaMainActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/main/DramaMainActivity.java)，该页面已在 [vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama)模块中配置：

```Java
context.startActivity(new Intent(context, DramaMainActivity.class));
```


<span id="e11d376d"></span>
# 根据您的业务需求定制

要快速使短剧 Demo 适配您的业务需求，请按照以下步骤操作：


1. 自定义数据层，以高效集成关键短剧视频功能。包括：

   1. 替换业务 API：实现[vod/minidrama/remote/api/DramaApi](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/api/DramaApi.java)包中定义的 API。

   2. 转换数据结构：将您的应用服务器返回的数据结构适配为短剧 Demo 中定义的结构，从而能够复用 Demo 中的现有业务流程。

2. 自定义短剧专属功能，如付费内容解锁。


<span id="aa0af5e1"></span>
## 短剧 Demo 源代码结构

```Bash
├ VodSDK.java                            // BytePlus VOD Player initialization class
├ minidrama
    ├ remote
    │   ├ api
    │   │   └ DramaApi.java              // Drama HTTP API
    │   └ model                          // Drama data models
    ├ event                              // EventBus-related drama events
    └ scene
        ├ comment                        // Comment dialogs
        ├ data                           // Drama data items
        ├ detail                         // Drama detail pages
        │   ├ pay                        // Drama ad & payment pages
        │   └ selector                   // Drama selector dialogs
        ├ main                           // Drama main page 
        ├ recommend                      // "For You" page
        ├ theater                        // Theater page
        └ widgets                        // Common widgets
```


<span id="72075161"></span>
## 适配数据层

<span id="b5aa1afc"></span>
### 替换业务 API


1. 更新“首页”API：可参考以下示例代码，调用获取“首页”短剧推荐的 API。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">详细实现请参见<a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/theater/DramaTheaterFragment.java">DramaTheaterFragment.java</a>。</div>


```Java
public class DramaTheaterFragment extends Fragment {
    private GetDramas mRemoteApi;

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mRemoteApi = new GetDramas();
        // ...
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        // ...
        refresh();
    }
    
    private void refresh() {
        // ...
        mRemoteApi.getDramaChannel(new HttpCallback<>() {
            @Override
            public void onSuccess(DramaTheaterEntity result) {
                L.d(this, "refresh", "success");
                // ...
            }
            @Override
            public void onError(Throwable e) {
                L.d(this, "refresh", e, "error");
                // ...
            }
        });
    }
}
```



2. 更新“Info”页面的 API：请参考下方示例代码，调用 API 以获取“Info”页面的短剧信息。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">详细实现请参见<a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/DramaDetailVideoFragment.java">DramaDetailVideoFragment.java</a>。</div>


```Java
public class DramaDetailVideoFragment extends BaseFragment {
    private GetDramas mRemoteApi;

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mRemoteApi = new GetDramas();
        // ...
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        // ...
        load(dramaItem);
    }

    private void load(@NonNull DramaItem dramaItem) {
        // ...
        mRemoteApi.getDramaList(dramaItem.getDramaId(), new HttpCallback<>() {
            @Override
            public void onSuccess(List<DramaFeed> items) {
                L.d(this, "load", "success", DramaItem.dump(dramaItem), items);
                // ...
            }
            @Override
            public void onError(Throwable e) {
                L.e(this, "load", e, "error", DramaItem.dump(dramaItem));
                // ...
            }
        });
    }
}
```



3. 更新“For you”页面的 API：请参考下方示例代码，调用 API 以获取“For you”页面的短剧列表。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">详细实现请参见<a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/recommend/DramaRecommendVideoFragment.java">DramaRecommendVideoFragment.java</a>。</div>


```Java
public class DramaRecommendVideoFragment extends Fragment {
    private GetDramas mRemoteApi;

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mRemoteApi = new GetDramas();
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        // ...
        refresh();
    }

    private void refresh() {
        // ...
        mRemoteApi.getDramaFeed(0, mBook.pageSize(), new HttpCallback<>() {
            @Override
            public void onSuccess(List<DramaRecommend> items) {
               // ...
            }
            @Override
            public void onError(Throwable e) {
               // ...
            }
        });
    }
}
```


<span id="c5d8dad0"></span>
### 数据结构转换

短剧 Demo 层已定义数据结构，包括[DramaInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaInfo.java)（短剧信息）、[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)（短剧集信息）、[DramaUnlockMeta](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaUnlockMeta.java)（剧集解锁信息）以及[CommentDetail](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-common/src/main/java/com/byteplus/vodcommon/data/remote/api2/model/CommentDetail.java)（评论）。

您必须将从应用服务器接收到的数据结构转换为上述数据结构。下表详细说明了这些数据结构的具体内容。


|**类** |**参数** |**类型** |**必填** |**说明** |
|---|---|---|---|---|
|[DramaInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaInfo.java)<br><br>（短剧信息） |dramaId |String |必填 |短剧 ID |
||dramaTitle |String |必填 |短剧名称 |
||dramaCoverUrl |String |必填 |短剧封面 URL |
||dramaPlayTimes |int |必填 |播放次数 |
||orientation |int |必填 |视频方向<br><br>0 : 竖屏<br><br>1 : 横屏 |
||totalEpisodeNumber |int |必填 |总集数 |
||newRelease |boolean |选填 |是否显示“新”标签（默认 false）。<br><br>true : 显示<br><br>false : 隐藏 |
|[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)<br><br>（剧集信息） |vid |String |必填 |视频 ID |
||title |String |选填 |视频标题 |
||duration |double |必填 |视频时长（单位：秒） |
||coverUrl |String |必填 |视频封面 URL |
||playAuthToken |String |选填 |该字段为视频数据源的 PlayAuthToken，可由 AppServer 通过 BytePlus VOD Server SDK 下发。 |
||subtitleAuthToken |String |选填 |该字段为视频数据源的字幕 Token，可由 AppServer 通过 BytePlus VOD Server SDK 下发。 |
||playTimes |int |选填 |播放次数 |
||subtitle |String |选填 |视频副标题 |
||createTime |Date |选填 |上传时间，格式为*RFC3339* |
||userName |String |选填 |上传者名称 |
||userId |String |选填 |上传者 userId |
||likeCount |int |选填 |点赞数 |
||commentCount |int |选填 |评论数 |
||height |int |必填 |视频高度 |
||width |int |必填 |视频宽度 |
||dramaIndex |int |必填 |剧集列表中的视频位置 |
||dramaId |String |必填 |短剧 ID |
||needVip |boolean |必填 |是否需要付费解锁（默认 false）。 |
||displayType |DisplayType |必填 |“为你推荐”页面短剧卡片的展示类型<br><br>0: 文本，无封面图<br><br>1: 封面，有封面图 |
|[DramaUnlockMeta](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaUnlockMeta.java)<br><br>（剧集解锁信息） |dramaId |String |必填 |短剧 ID |
||vid |String |必填 |视频 ID |
||dramaIndex |int |选填 |剧集列表中的视频位置 |
||playAuthToken |String |必填 |该字段为视频数据源的 PlayAuthToken，可由 AppServer 通过 BytePlus VOD Server SDK 下发。 |


短剧 Demo 的视频控件使用[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)数据结构。因此，您需要将[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)对象转换为[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)对象以实现兼容。

```Java
// Convert DramaFeed to VideoItem
VideoItem videoItem = DramaFeed.toVideoItem();
```


基于视频控件构建的组件使用[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)对象。为实现您的业务逻辑，您必须从[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)对象中获取原始[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)数据。这样您即可访问所需的短剧信息。

```Java
// Get DramaFeed from VideoItem
DramaFeed dramaFeed = DramaFeed.of(videoItem);
```


<span id="3c0ce5a8"></span>
## 定制短剧专属功能

<span id="5b4b03ce"></span>
### 防录屏

您可参考下方示例代码，通过 Activity 的 `onCreate` 方法调用系统 API 以启用防录屏功能。在短剧 Demo 中，[DramaDetailVideoActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/DramaDetailVideoActivity.java)和[DramaMainActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/main/DramaMainActivity.java)已启用防录屏。更多信息请参见[防止屏幕录制](https://docs.byteplus.com/docs/byteplus-vos/docs-anti-screen-recording-zh-CN)。

```Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Window window = getWindow();
    window.addFlags(WindowManager.LayoutParams.FLAG_SECURE);
}
```


<span id="07a883d6"></span>
### 付费内容解锁

短剧 Demo 中付费内容的解锁与播放流程如下图所示。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5MjZweCIgaGVpZ2h0PSI4MDdweCIgdmlld0JveD0iLTAuNSAtMC41IDkyNiA4MDciPjxkZWZzLz48Zz48cmVjdCB4PSI0MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNDA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRyYW1hIFNjZW5lIEtpdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjAzIiB5PSIzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjNweDsgbWFyZ2luLWxlZnQ6IDIwNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzcHg7IG1hcmdpbi1sZWZ0OiA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNjA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBheW1lbnQgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI4MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogODA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXltZW50IFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MyA1MyBMIDYzIDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHJlY3QgeD0iNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iNzQwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNjMgODAzIEwgNjMgNzkzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNjIuNTggNTMgTCAyNjIuNSA0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDYzIDgwMyBMIDQ2Mi41IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NjMuMzEgMzEzIEwgNjY0IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4NjIuOTIgMzQzIEwgODYyLjUgNDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cmVjdCB4PSIyNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iMTEwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDQzMyBMIDI2MyAxNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc2IDczIEwgMjQ0Ljc2IDczLjk1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTAuNzYgNzMuOTkgTCAyNDIuNzQgNzcuOTQgTCAyNDQuNzYgNzMuOTUgTCAyNDIuNzkgNjkuOTQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NHB4OyBtYXJnaW4tbGVmdDogMTY1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bMV1nZXREcmFtYUxpc3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA4MC41IEwgMzQzIDgwLjUgUSAzNTMgODAuNSAzNTMgOTAuNSBMIDM1MyAxMjUuNSBRIDM1MyAxMzUuNSAzNDMgMTM1LjUgTCAyODEuMjQgMTM1LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3NS4yNCAxMzUuNSBMIDI4My4yNCAxMzEuNSBMIDI4MS4yNCAxMzUuNSBMIDI4My4yNCAxMzkuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwOXB4OyBtYXJnaW4tbGVmdDogMzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzEuMV1VbmxvY2tlZCBlcGlzb2RlczxiciAvPsKgbm8gcGxheWJhY2sgYXV0aCB0b2tlbi91cmw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjU0IDE0OS40NyBMIDg1LjI0IDE0Ny44IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc5LjI0IDE0Ny43NCBMIDg3LjI4IDE0My44MiBMIDg1LjI0IDE0Ny44IEwgODcuMiAxNTEuODIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDlweDsgbWFyZ2luLWxlZnQ6IDE2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlsyXVJldHVybiBkcmFtYUxpc3Q8YnIgLz57RHJhbWFGZWVkW119PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NTMiIHk9IjE4MyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjgwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzYgMTkzIEwgNDQxLjc2IDE5Ni40NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDQ3Ljc2IDE5Ni41IEwgNDM5LjczIDIwMC40MiBMIDQ0MS43NiAxOTYuNDQgTCA0MzkuOCAxOTIuNDIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTVweDsgbWFyZ2luLWxlZnQ6IDI2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzNdc2V0SXRlbXModmlkZW9JdGVtc1tdKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDczIDIwMyBMIDUzMyAyMDMgUSA1NDMgMjAzIDU0MyAyMTMgTCA1NDMgMjMzIFEgNTQzIDI0MyA1MzMgMjQzIEwgNDgxLjI0IDI0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjI0IDI0MyBMIDQ4My4yNCAyMzkgTCA0ODEuMjQgMjQzIEwgNDgzLjI0IDI0NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyM3B4OyBtYXJnaW4tbGVmdDogNTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzMuMV1QcmV2aWV3L1BsYXliYWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTMiIHk9IjMxMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjI0MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2NCA4MDMgTCA2NjMuMzIgNTUzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MyAzMjMgTCA2MzkuNzYgMzI0LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY0NS43NiAzMjQuNTEgTCA2MzcuNzUgMzI4LjQ5IEwgNjM5Ljc2IDMyNC41IEwgNjM3Ljc3IDMyMC40OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyNHB4OyBtYXJnaW4tbGVmdDogMzYxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNF1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iODUzIiB5PSIzNDMiIHdpZHRoPSIyMCIgaGVpZ2h0PSIxMjAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA4NjMgODAzIEwgODYzIDQ2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjczIDM1MyBMIDg0NC43NyAzNTYuODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MC43NiAzNTYuOTUgTCA4NDIuNjggMzYwLjc3IEwgODQ0Ljc3IDM1Ni44MiBMIDg0Mi44NiAzNTIuNzcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTVweDsgbWFyZ2luLWxlZnQ6IDc2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzQuMV1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA4NTMgMzkzIEwgNjgxLjI0IDM5NS4xMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzUuMjQgMzk1LjIgTCA2ODMuMTkgMzkxLjEgTCA2ODEuMjQgMzk1LjEzIEwgNjgzLjI4IDM5OS4xIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzk0cHg7IG1hcmdpbi1sZWZ0OiA3NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bNC4yXVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNTMiIHk9IjQzMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjkwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDU3MyBMIDI2MyA1MjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MyA0NDMgTCAyODIuMjQgNDQ1LjQ3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3Ni4yNCA0NDUuNSBMIDI4NC4yMiA0NDEuNDcgTCAyODIuMjQgNDQ1LjQ3IEwgMjg0LjI1IDQ0OS40NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0NHB4OyBtYXJnaW4tbGVmdDogNTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzQuM11Ob3RpZnkgcGF5IHN1Y2Nlc3Mob3JkZXJJZCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjUzIDU0Mi45MiBMIDg2LjI0IDU0NC4zNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4MC4yNCA1NDQuMzUgTCA4OC4yMyA1NDAuMzMgTCA4Ni4yNCA1NDQuMzQgTCA4OC4yNSA1NDguMzMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NDRweDsgbWFyZ2luLWxlZnQ6IDM2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls1XVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA0NTUuNSBMIDMzMyA0NTUuNSBRIDM0MyA0NTUuNSAzNDMgNDY1LjUgTCAzNDMgNDkwLjUgUSAzNDMgNTAwLjUgMzMzIDUwMC41IEwgMjgxLjI0IDUwMC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNzUuMjQgNTAwLjUgTCAyODMuMjQgNDk2LjUgTCAyODEuMjQgNTAwLjUgTCAyODMuMjQgNTA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0NzlweDsgbWFyZ2luLWxlZnQ6IDM0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+WzQuNF08Zm9udCBzdHlsZT0iZm9udC1zaXplOjEzcHgiPlJlY29yZCA8YnIgLz5wYXltZW50IHN0YXR1czwvZm9udD48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDczIDI2MyBMIDEzMyAyNjMgUSAxNDMgMjYzIDE0MyAyNzMgTCAxNDMgMjkzIFEgMTQzIDMwMyAxMzMgMzAzIEwgODEuMjQgMzAzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3NS4yNCAzMDMgTCA4My4yNCAyOTkgTCA4MS4yNCAzMDMgTCA4My4yNCAzMDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODNweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXY+U3dpcGUgdG88L2Rpdj48ZGl2PnVubG9ja2VkIGVwaXNvZGU8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI1MyIgeT0iNTczIiB3aWR0aD0iMjAiIGhlaWdodD0iOTAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNjMgODAzIEwgMjYzIDY2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzMgNTgzIEwgMjQ0Ljc2IDU4MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjUwLjc2IDU4MyBMIDI0Mi43NiA1ODcgTCAyNDQuNzYgNTgzIEwgMjQyLjc2IDU3OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU3M3B4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNl1nZXREcmFtYURldGFpbChvcmRlcklkKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjUzIDY0NC43NSBMIDE3MyA2NDMuMTkgUSAxNjMgNjQzIDE1MyA2NDMgTCA4NC4yNCA2NDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzguMjQgNjQzIEwgODYuMjQgNjM5IEwgODQuMjQgNjQzIEwgODYuMjQgNjQ3IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjIzcHg7IG1hcmdpbi1sZWZ0OiAxNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bN11SZXR1cm4gRHJhbWFVbmxvY2sgbWV0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDUzIiB5PSI2NzAiIHdpZHRoPSIyMCIgaGVpZ2h0PSI4MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MyA2OTAgTCA1MzMgNjkwIFEgNTQzIDY5MCA1NDMgNzAwIEwgNTQzIDcyMCBRIDU0MyA3MzAgNTMzIDczMCBMIDQ4MS4yNCA3MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ3NS4yNCA3MzAgTCA0ODMuMjQgNzI2IEwgNDgxLjI0IDczMCBMIDQ4My4yNCA3MzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3MTBweDsgbWFyZ2luLWxlZnQ6IDU0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls4LjFdUHJldmlldy9QbGF5YmFjazwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3OSA2NzMgTCA0NDQuNzYgNjc2LjQ0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0NTAuNzYgNjc2LjUgTCA0NDIuNzMgNjgwLjQyIEwgNDQ0Ljc2IDY3Ni40NCBMIDQ0Mi44IDY3Mi40MiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3NXB4OyBtYXJnaW4tbGVmdDogMjY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bOF1hcHBlbmRJdGVtcyh2aWRlb0l0ZW1zW10pPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

短剧 Demo 未集成第三方 SDK，仅提供模拟实现以展示流程。

请集成第三方 SDK，并在[DramaEpisodeUnlockByPaymentFragment](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/pay/DramaEpisodeUnlockByPaymentFragment.java)页面替换模拟支付流程。

```Java
public class DramaEpisodeUnlockByPaymentFragment extends BottomSheetDialogFragment {

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        // ...
        binding.action.setOnClickListener(v -> {
            SKU value = Objects.requireNonNull(viewModel.sku.getValue());
           // After a successful payment, request unlockEpisodes to get playback auth tokens
            List<String> episodes = //...
            unlockStateModel.unlockEpisodes(dramaItem.getDramaId(), episodes);
        });
    }
}
```
