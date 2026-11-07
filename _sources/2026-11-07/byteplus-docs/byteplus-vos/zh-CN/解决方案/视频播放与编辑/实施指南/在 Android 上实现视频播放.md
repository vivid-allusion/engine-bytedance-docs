---
title: "在 Android 上实现视频播放"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-video-playback-edit-for-android-zh-CN"
---

本文介绍如何在您的 Android 应用中实现视频播放功能。

<span id="04b63222"></span>
# 开发环境


* Android Studio Arctic Fox 或更高版本。我们强烈建议使用最新版本的 Android Studio，以确保最佳性能。

* 一台运行 Android 5.0 或以上版本的实体移动设备。目前不支持在模拟器上构建。

* 请确保您使用的 CPU 架构为 armv7 或 arm64。


<span id="22cc987e"></span>
# 前提条件


* 拥有有效的 [BytePlus 账号](http://console.byteplus.com/)，并已激活 [BytePlus VOD](https://console.byteplus.com/vodpaas)。

* 请在 BytePlus VOD 控制台的 [SDK 管理](https://console.byteplus.com/vodpaas/sdk/)页面完成以下步骤：

   * 创建应用并获取应用 ID 及应用英文名称。

   * 注册应用后，购买并下载用于 Player SDK 和 Upload SDK 的许可证。对于 Player SDK，我们建议使用高级版。


<span id="889000d5"></span>
# 版本要求


* 要访问 **视频播放** 和 **媒体上传**功能，必须使用 BytePlus VOD SDK。请参阅[集成](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-video-playback-edit-for-android-zh-CN#29daa035)部分，获取每个 SDK 可用的正确版本号。

> 关于各方案所用 SDK 的对应版本，请参阅[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)。


<span id="29daa035"></span>
# 集成

<span id="419c0c9d"></span>
## 步骤 1：添加 Maven 仓库

打开项目根目录下的 `build.gradle` 文件，在 `repositories` 块中添加仓库地址，如下所示：

```Groovy
allprojects { 
    repositories { 
        google() 
        mavenCentral() 
        // BytePlus VOD SDK maven repository
        maven { url 'https://artifact.byteplus.com/repository/public/' }
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
    } 
} 

// BytePlus VOD SDK maven repository
apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
```


<span id="3cc1c219"></span>
## 步骤 2：集成 SDK

要将 SDK 集成到您的项目中，请在模块级 `build.gradle` 文件的 `dependencies` 块中添加所需 SDK 的依赖，如下所示：

```Groovy
dependencies { 
    // BytePlus VOD SDK dependencies
    ttsdkVersion = '1.43.300.3'
    implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdkVersion"
    implementation "com.bytedanceapi:ttsdk-ttuploader:$ttsdkVersion"
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3' 
    implementation 'com.squareup.okhttp3:okhttp:4.12.0'
}
```


<span id="edf52c62"></span>
## 步骤 3：声明应用权限

在项目“app”模块下的 `AndroidManifest.xml` 文件中声明 SDK 所需权限，如下所示：

```XML
<!-- BytePlus VOD SDK -->
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.WAKE_LOCK" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


此外，必须在运行时请求写入存储权限。详情请参见 Android 开发者指南中的 [请求运行时权限](https://developer.android.com/training/permissions/requesting)。

如果您的应用目标为 Android 10（API 等级 29），且未使用 Scoped Storage，则必须在应用的 `AndroidManifest.xml` 文件中包含属性 `android:requestLegacyExternalStorage="true"`：

```XML
<manifest> 
  <application android:requestLegacyExternalStorage="true">         
  </application> 
</manifest>
```


如果您的应用目标为 Android 11（API 等级 30）或更高版本，则必须支持 Scoped Storage。更多详情请参见 [临时退出 Scoped Storage](https://developer.android.com/training/data-storage/use-cases#opt-out-scoped-storage)。

<span id="a0d1e7bd"></span>
## 步骤 4：添加混淆规则

为防止 SDK 相关类被混淆，请将以下规则添加到 `proguard-rules.pro` 文件中。

```Plain
# For BytePlus VOD Player
-keep class com.ss.ttm.** {*;}  
-keep class com.ss.ttvideoengine.** {*;}  
-keep class com.ss.mediakit.** {*;}  
-keep class com.ss.texturerender.** {*;} 
-keep class com.bytedance.**{*;} 
-keep class com.pandora.ttlicense2.**{*;} 
-keep class com.pandora.common.applog.**{*;} 
-keep class com.pandora.vod.VodSDK {*;} 

# For BytePlus VOD Upload
-keep class com.pandora.common.applog.**{*;} 
-keep class com.pandora.ttuploader2.** {*;} 
-keep class com.ss.bduploader.** {*;}
```


<span id="de04d210"></span>
# 实现

<span id="bda47037"></span>
## 视频播放

<span id="6692310a"></span>
### 时序图

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSIzMjVweCIgdmlld0JveD0iLTAuNSAtMC41IDU2NSAzMjUiPjxkZWZzLz48Zz48cmVjdCB4PSIxNjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2NjZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMDIgNDIgTCAyMDIgMzIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTk3IiB5PSI4MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjkwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzMjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzk5ZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzNjIgNDIgTCAzNjIgMzIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5WT0QgUGxheWVyIFNESzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDgyIiB5PSIyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM5OWZmOTkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTIyIDQyIEwgNTIyIDMyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TWVkaWEgU2VydmVyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MTciIHk9IjE5MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjgwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQyIDkyIEwgMTg5LjM4IDkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTk2LjM4IDkyIEwgMTg5LjM4IDk1LjUgTCAxODkuMzggODguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LWVuZDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDg5cHg7IG1hcmdpbi1sZWZ0OiAxMjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5SZXF1ZXN0IGEgUGxheUF1dGggVG9rZW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzY2ZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MiA0MiBMIDQyIDMyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzNyIgeT0iODIiIHdpZHRoPSIxMCIgaGVpZ2h0PSIxNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDcgMjAyLjAyIEwgMzUzLjg4IDIwMS4wMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM2MC44OCAyMDEgTCAzNTMuODkgMjA0LjUzIEwgMzUzLjg3IDE5Ny41MyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LWVuZDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5OXB4OyBtYXJnaW4tbGVmdDogMjA1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PGRpdiBzdHlsZT0idGV4dC1hbGlnbjpsZWZ0Ij48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjpyZ2IoMjQ4LCAyNDksIDI1MCkiPlBhc3MgdGhlIFBsYXlBdXRoIFRva2VuPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0OC40OCAxNjEuNDYgTCAxOTcuNSAxNjIuNTYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU0LjM4IDE1OCBMIDQ3LjM2IDE2MS40NSBMIDU0LjMzIDE2NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTlweDsgbWFyZ2luLWxlZnQ6IDEyMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTJweCI+UmV0dXJuIHRoZSBQbGF5QXV0aCBUb2tlbjxiciBzdHlsZT0iZm9udC1zaXplOjEycHgiIC8+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjEyIiB5PSI5OCIgd2lkdGg9IjExMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMjhweDsgbWFyZ2luLWxlZnQ6IDIxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Mb2NhbGx5IGNoZWNrIG91dCB0aGUgUGxheUF1dGggVG9rZW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzY0LjE4IDIwMSBMIDUwNy42MyAyMDEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1MTIuODggMjAxIEwgNTA1Ljg4IDIwNC41IEwgNTA3LjYzIDIwMSBMIDUwNS44OCAxOTcuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM1OSIgeT0iMTgyIiB3aWR0aD0iMTYwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTJweDsgbWFyZ2luLWxlZnQ6IDM2MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5PYnRhaW4gcGxheWJhY2sgaW5mb3JtYXRpb248L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTE0IDI2MiBMIDM3MC4zNyAyNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM2NS4xMiAyNjIgTCAzNzIuMTIgMjU4LjUgTCAzNzAuMzcgMjYyIEwgMzcyLjEyIDI2NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzU5IiB5PSIyNDIiIHdpZHRoPSIxNjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI1MnB4OyBtYXJnaW4tbGVmdDogMzYwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJldHVybiBwbGF5YmFjayBpbmZvcm1hdGlvbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" width="565px" />

<span id="7f4900c6"></span>
### 步骤 1：初始化 SDK

建议在 `Application` 类的 `onCreate` 方法中初始化 SDK。请参考以下示例代码：

```Java
File videoCacheDir = new File(context.getCacheDir(), "video_cache"); 
if (!videoCacheDir.exists()) videoCacheDir.mkdirs(); 
VodConfig.Builder vodBuilder = new VodConfig.Builder(context) 
        .setCacheDirPath(videoCacheDir.getAbsolutePath()) 
        .setMaxCacheSize(300 * 1024 * 1024); 
         
Env.init(new Config.Builder() 
        .setApplicationContext(context) 
        .setAppID("Your app ID") 
        .setAppName("Your app English name") 
        .setAppVersion(BuildConfig.VERSION_NAME) 
        .setAppChannel("channel name") 
        .setLicenseUri("assets:///license/vod.lic") 
        .setVodConfig(vodBuilder.build()) 
        .build());
```


初始化 SDK 时，请设置以下参数：


|**名称** |**类型** |**是否必填** |**默认值** |**描述** |
|---|---|---|---|---|
|AppID |String |是 |无 |应用 ID。您可以在 **SDK 管理** \> **Application** **s** 页面，在 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/) 获取应用 ID。 |
|AppName |String |是 |无 |应用名称。您可以在 **SDK 管理** \> **Application** **s** 页面，在 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/) 获取应用名称。 |
|AppVersion |String |是 |无 |应用版本号。有效的版本号应包含两个或以上分隔符，例如“1.3.2”。 |
|AppChannel |String |是 |无 |应用分发渠道名称，例如 Google Play。 |
|LicenseUri |String |是 |无 |您的许可证路径。您需要将许可证放置在 app/assets 文件夹中，然后将 LicenseUri 参数设置为许可证路径，例如 assets/license/vod.lic。<br><br>关于许可证的更多信息，请参见 [Android Player SDK: License guide](https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-guide-android)。 |
|CacheDirPath |String |否 |/data/user/0/<package_name\>/cache/video_cache |视频缓存路径。 |
|MaxCacheSize |Int |否 |300 \* 1024 \* 1024 (300 MB) |视频缓存文件夹的最大字节数。 |


<span id="265a5194"></span>
### 步骤 2：创建播放器实例

使用 `TTVideoEngine` 类创建播放器实例，如下所示：

```Java
// When creating the instance, pass in the app context
TTVideoEngine ttVideoEngine = new TTVideoEngine(context, TTVideoEngine.PLAYER_TYPE_OWN);
```


<span id="9f79cb87"></span>
### 步骤 3：设置用于显示视频的视图

要显示视频，请将播放器绑定到 TextureView 或 SurfaceView。

<span id="eae89f96"></span>
#### 绑定播放器到 TextureView


1. 在 XML 中声明 TextureView，如下所示：

   ```XML
   <TextureView
       android:id="@+id/textureView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:background="@null" />
   ```
   

   如果您的应用目标为 Android API 等级 24 或更高，在声明 TextureView 时，不应设置 `background`，或必须将 `background` 设置为 `null`。否则，应用将会崩溃。

2. 获取您声明的纹理视图的 `SurfaceTexture` 实例，并将其传递给 `TTVideoEngine`。随后可以使用 `SurfaceTexture` 来渲染来自 `TTVideoEngine` 的视频。请参见以下示例代码：

   ```Java
   TextureView textureView = findViewById(R.id.textureView);
   // Set the listener for the TextureView's SurfaceTexture
   textureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
       @Override
       // Called when the TextureView's SurfaceTexture is ready for use
       public void onSurfaceTextureAvailable(SurfaceTexture surfaceTexture, int width, int height) {
           // Pass the TextureView's SurfaceTexture to the player
           ttVideoEngine.setSurface(new Surface(surfaceTexture));
       }
       @Override
       public void onSurfaceTextureSizeChanged(SurfaceTexture surfaceTexture, int width, int height) { 
       }
       @Override
       public boolean onSurfaceTextureDestroyed(SurfaceTexture surfaceTexture) {
           return true;
       }
       @Override
       public void onSurfaceTextureUpdated(SurfaceTexture surfaceTexture) {
       }
   });
   ```
   


<span id="696cc74b"></span>
#### 将播放器绑定到 SurfaceView


1. 在 XML 中声明一个 SurfaceView，如下所示：

   ```XML
   <SurfaceView
       android:id="@+id/surfaceView"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```
   

2. `SurfaceView` 提供专用的绘图表面。您可以通过 `SurfaceHolder` 接口获取底层表面，该接口可通过调用 `getHolder()` 获得。将 `SurfaceHolder` 接口传递给 `TTVideoEngine`，然后 `SurfaceView` 即可显示来自 `TTVideoEngine` 的视频。请参见以下示例代码：

   ```Java
   SurfaceView surfaceView = findViewById(R.id.surfaceView); 
   // Pass the SurfaceHolder to TTVideoEngine
   ttVideoEngine.setSurfaceHolder(surfaceView.getHolder());
   ```
   

> 注意事项：

> * 必须在调用 `ttVideoEngine.play` 之前调用 `ttVideoEngine.setSurface` 和 `ttVideoEngine.setSurfaceHolder` 方法。

> * 从 Android API 级别 24 开始，SurfaceView 支持与视图树中的其他视图同步窗口中的渲染位置。如果您的应用目标为 Android API 级别 24 或更低，可能会出现视图层级问题和动画不同步。详情请参见 Android API 参考中的[SurfaceView](https://developer.android.com/reference/android/view/SurfaceView.html)。


<span id="a0a98231"></span>
### 步骤 4：设置视频源

SDK 支持播放本地视频和在线视频。本节介绍如何播放不同来源的视频。

<span id="7f0f2764"></span>
#### 通过视频 ID 播放视频

如果您将视频上传至 BytePlus VOD 服务，可以使用关联的视频 ID 播放视频。您需要设置 `vid` 和 `playAuthToken` 参数，这些参数可从您的应用服务器获取。

请参见以下示例代码：

```Java
// Enable caching the video model
ttVideoEngine.setIntOption(PLAYER_OPTION_USE_VIDEOMODEL_CACHE, 1);

// Get the video ID from your app server
final String vid = "your video ID";
// Get the playback token from your app server
final String playAuthToken = "your playback token";

final int encodeType = TTVideoEngine.CODEC_TYPE_H264;
// final int encodeType = TTVideoEngine.CODEC_TYPE_H265;

// 1. Assemble the video source
StrategySource vidSource = new VidPlayAuthTokenSource.Builder()
        .setVid(vid)
        .setPlayAuthToken(playAuthToken)
        // Set the codec type. The default value is TTVideoEngine.CODEC_TYPE_H264
        .setEncodeType(encodeType)
        // Set the resolution when the video playback initiates. The default resolution is 360P
        // Here we set the resolution to 480p
        .setResolution(Resolution.High)
        .build();
// 2. Set the video source
ttVideoEngine.setStrategySource(vidSource);
// 3. Play the video
ttVideoEngine.play()
```


组装视频源时，请设置以下参数：


|**参数** |**类型** |**必填** |**默认值** |**描述** |
|---|---|---|---|---|
|Vid |String |是 |无 |视频 ID。 |
|PlayAuthToken |String |是 |无 |播放令牌。 |
|EncodeType |Int |否 |CODEC_TYPE_H264 |编解码类型：<br><br><br>* H.264（默认）<br><br>* ByteVC1（仅 SDK 高级版可用） |
|Resolution |Resolution |否 |Standard |视频分辨率。请参见下表。 |


分辨率


|档位 |视频质量 |音频质量 |
|---|---|---|
|Standard |360p，SD（标清） |普通 |
|High |480p，HD（高清） |高 |
|SuperHigh |720p，FHD（全高清） |非常高 |
|ExtremelyHigh |1080p |原始 |
|TwoK |2K |此参数不影响音频质量。 |
|FourK |4K |此参数不影响音频质量。 |
|Auto |对于 DASH 视频，播放器会根据观众的网络连接自动决定最佳分辨率，并在播放过程中调整视频质量以最大限度减少缓冲风险。 |此参数不影响音频质量。 |


<span id="d3e181c3"></span>
#### 通过 HTTP URL 播放视频

如果您将视频上传至 BytePlus VOD 服务或第三方存储服务，可以通过 HTTP URL 播放视频。您需要设置 `url` 参数。

请参见以下示例代码：

```Java
// The unique identifier of the video.
final String vid = "video id";
// The HTTP URL of the video.
final String url = "http://www.example.com/h264.mp4";
final String cacheKey = TTVideoEngine.computeMD5(url);

// 1. Assemble the video source
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(new DirectUrlSource.UrlItem.Builder()
                .setUrl(url)
                .setCacheKey(cacheKey)
                .build())
        .build();
       
// 2. Set the video source
ttVideoEngine.setStrategySource(directUrlSource);
// 3. Play the video
ttVideoEngine.play()
```


组装视频源时，请设置以下参数：


|**参数** |**类型** |**必填** |**默认值** |**描述** |
|---|---|---|---|---|
|Vid |String |是 |无 |视频 ID。 |
|Url |String |是 |无 |视频的 HTTP URL。 |
|CacheKey |String |是 |无 |缓存键，必须满足以下要求：<br><br><br>* 不应包含任何特殊字符，并且可作为文件名使用。<br><br>* 每个视频都有唯一的缓存键。<br><br><br>建议使用 URL 的 MD5 作为缓存键。 |


<span id="5d4504af"></span>
#### 播放本地视频

如果播放本地视频，请将本地地址赋值给 `videoFile` 参数。请参见以下示例代码：

```Java
// Replace "/sdcard/Download/video.MP4" with the local video file path
File videoFile = new File("/sdcard/Download/video.MP4"); 
ttVideoEngine.setLocalURL(videoFile.getAbsolutePath()); 
ttVideoEngine.play() 
```


<span id="ff0aee11"></span>
### 步骤 5：控制视频播放

`TTVideoEngine` 类提供以下方法用于控制视频播放：


* 调用 `play` 以开始或恢复播放。

   ```Java
   ttVideoEngine.play();
   ```
   

* 调用 `pause` 以暂停播放。调用 `play` 以恢复播放。

   ```Java
   ttVideoEngine.pause();
   ttVideoEngine.play();
   ```
   

* 调用 `seekTo` 以跳转到指定时间位置。此功能允许用户通过拖动进度条手动调整视频播放，实现快进或快退。

   ```Java
   // The offset from the start to seek to is 1000 milliseconds
   ttVideoEngine.seekTo(1000, new SeekCompletionListener() {
       @Override
       // Occurs when a seek operation completes
       // The success parameter indicates whether the seek operation succeeds
       public void onCompletion(boolean success) {
       }
   });
   
   ttVideoEngine.setVideoEngineInfoListener(new VideoEngineInfoListener() {
       @Override
       // The SDK starts rendering after the seek operation
       // When the rendering completes, the SDK triggers this callback
       public void onVideoEngineInfos(VideoEngineInfos videoEngineInfos) {
           if (TextUtils.equals(videoEngineInfos.getKey(), VideoEngineInfos.USING_RENDER_SEEK_COMPLETE)) {
           }
       }
   });
   ```
   

* 在调用 `play` 之前，调用 `setStartTime` 以指定播放开始的时间位置。此方法可用于“跳过片头”功能。

   ```Java
   int startPlayPositionMS = 1000;
   // Set the start time as one second
   ttVideoEngine.setStartTime(startPlayPositionMS);
   ttVideoEngine.play();
   ```
   

* 调用 `stop` 以停止播放。

   ```Java
   ttVideoEngine.stop();
   ```
   


<span id="8798b2ce"></span>
### 步骤 6：释放播放器实例

当视频播放结束或用户离开正在播放视频的页面时，可以通过调用 `releaseAsync` 停止播放并释放播放器实例。此操作会释放 `ttVideoEngine` 所使用的硬件解码器、内存和网络资源，以节省电量。

释放播放器实例后，不能再调用 `ttVideoEngine` 类中的方法。建议将 `ttVideoEngine` 设置为 `null`，以确保不再引用已释放的播放器实例。这有助于防止访问已释放的播放器实例或消耗不必要的内存资源等潜在问题。

```Java
ttVideoEngine.releaseAsync(); 
ttVideoEngine = null;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VOD Player SDK 还提供丰富的高级功能。如需详细信息，请参阅以下主题：</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-android">Android Player SDK：基础功能</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-advanced-features-android">Android Player SDK：高级功能</a></div>



<span id="dfb8fe29"></span>
## 媒体上传

本节介绍如何使用 VOD 上传 SDK。

<span id="7b23a02a"></span>
### 时序图

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSI0MDVweCIgdmlld0JveD0iLTAuNSAtMC41IDU2NSA0MDUiPjxkZWZzLz48Zz48cmVjdCB4PSIxNjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2NjZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMDIgNDIgTCAyMDIgNDAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTk3IiB5PSI4MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjkwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzMjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzk5ZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzNjIgNDIgTCAzNjIgNDAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5WT0QgVXBsb2FkIFNESzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDgyIiB5PSIyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM5OWZmOTkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTIyIDQyIEwgNTIyIDQwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TWVkaWEgU2VydmVyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MTciIHk9IjE5MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjE5MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MiA5MiBMIDE4OS4zOCA5MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE5Ni4zOCA5MiBMIDE4OS4zOCA5NS41IEwgMTg5LjM4IDg4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4OXB4OyBtYXJnaW4tbGVmdDogMTIwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+UmVxdWVzdCBhbiA8YnIgLz5VcGxvYWRBdXRoIFRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM2NmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDIgNDIgTCA0MiA0MDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIENsaWVudDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzciIHk9IjgyIiB3aWR0aD0iMTAiIGhlaWdodD0iMTUwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3IDIwMi4wMiBMIDM1My44OCAyMDEuMDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzNjAuODggMjAxIEwgMzUzLjg5IDIwNC41MyBMIDM1My44NyAxOTcuNTMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTlweDsgbWFyZ2luLWxlZnQ6IDIwNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXYgc3R5bGU9InRleHQtYWxpZ246bGVmdCI+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5QYXNzIHRoZSBVcGxvYWRBdXRoIFRva2VuPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0OC40OCAxNjEuNDYgTCAxOTcuNSAxNjIuNTYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU0LjM4IDE1OCBMIDQ3LjM2IDE2MS40NSBMIDU0LjMzIDE2NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTlweDsgbWFyZ2luLWxlZnQ6IDEyMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTJweCI+UmV0dXJuIHRoZSA8YnIgLz5VcGxvYWRBdXRoIFRva2VuPGJyIHN0eWxlPSJmb250LXNpemU6MTJweCIgLz48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyMTIiIHk9Ijk4IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyOHB4OyBtYXJnaW4tbGVmdDogMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkxvY2FsbHkgY2hlY2sgb3V0IHRoZSBVcGxvYWRBdXRoIFRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM2NC4xOCAyMDEgTCA1MDcuNjMgMjAxIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTEyLjg4IDIwMSBMIDUwNS44OCAyMDQuNSBMIDUwNy42MyAyMDEgTCA1MDUuODggMTk3LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTkiIHk9IjE3NSIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTg1cHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+T2J0YWluIHRoZSBzdG9yYWdlIHVybCBhbmQgY3JlZGVudGlhbHM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTE0IDI2MiBMIDM3MC4zNyAyNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM2NS4xMiAyNjIgTCAzNzIuMTIgMjU4LjUgTCAzNzAuMzcgMjYyIEwgMzcyLjEyIDI2NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzU5IiB5PSIyMzYiIHdpZHRoPSIxNjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI0NnB4OyBtYXJnaW4tbGVmdDogMzYwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJldHVybiB0aGUgc3RvcmFnZSB1cmwgYW5kIGNyZWRlbnRpYWxzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM2NC4xOCAzMDggTCA1MDcuNjMgMzA4IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTEyLjg4IDMwOCBMIDUwNS44OCAzMTEuNSBMIDUwNy42MyAzMDggTCA1MDUuODggMzA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTkiIHk9IjI5MCIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzAwcHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VXBsb2FkIHRoZSBtZWRpYTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1MTQgMzY4IEwgMzcwLjM3IDM2OCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzY1LjEyIDM2OCBMIDM3Mi4xMiAzNjQuNSBMIDM3MC4zNyAzNjggTCAzNzIuMTIgMzcxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTkiIHk9IjM0OCIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzU4cHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmV0dXJuIHRoZSB1cGxvYWQgcmVzdWx0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" width="565px" />

<span id="9e157fb4"></span>
### 步骤 1：初始化 SDK

建议您在 `onCreate` 方法的 `Application` 类中初始化 SDK。请参见以下示例代码：

```Java
Env.init(new Config.Builder() 
        .setApplicationContext(context) 
        .setAppID("your app id") 
        .setAppName("your app English name") 
        .setAppVersion(BuildConfig.VERSION_NAME) 
        .setAppChannel("channel name") 
        .build());
```


初始化 SDK 时，请设置以下参数：


|**参数** |**类型** |**描述** |
|---|---|---|
|AppID |String |应用 ID。您可以在 **SDK 管理** \> **应用** **s** 页面上的 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/) 获取应用 ID。 |
|AppName |String |应用名称。您可以在 **SDK 管理** \> **应用** **s** 页面上的 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/) 获取应用名称。 |
|AppVersion |String |应用版本号。有效的版本号应包含两个或以上的分隔符，例如“`1.3.2`”。 |
||||
|AppChannel |String |应用分发渠道的名称，例如 Google Play。 |
||||


<span id="d9932e09"></span>
### 步骤 2：创建上传器实例

使用 `BDVideoUploader` 类创建上传器实例，操作如下：

```Java
BDVideoUploader mUploader = new BDVideoUploader();
```


<span id="0897b289"></span>
### 步骤 3：指定待上传文件的路径

调用 `setPathName` 指定待上传文件的绝对路径：

```Java
mUploader.setPathName("/data/user/0/xxx/files/test.mp4");
```


<span id="6af71b71"></span>
### 步骤 4：设置鉴权参数

从您的应用服务器获取鉴权参数，并传递给 SDK：

```Java
mUploader.setTopAccessKey("xxx"); 
mUploader.setTopSecretKey("xxx"); 
mUploader.setTopSessionToken("xxx");
```


<span id="1bdae923"></span>
### 步骤 5：指定文件上传的空间

调用 `setSpaceName` 设置文件上传的空间。关于空间的详细信息，请参见 [空间管理](https://docs.byteplus.com/en/byteplus-vod/docs/space-management)。

```Java
mUploader.setSpaceName("xxx");
```


<span id="38ed2fde"></span>
### 步骤 6：指定云存储中的文件路径

上传完成后，云存储中的文件路径如下：

`StoreUri={{BucketName}}/{{FilePrefix}}{{FileTitle}}{{FileExtension}}`


|**Parameter** |**Description** |
|---|---|
|BucketName |桶名称由系统自动生成。 |
|FilePrefix |文件前缀必须以 `/` 结尾，例如 `“path/to/foo/bar/”`。 |
|FileTitle |文件名称。如未设置，SDK 将自动生成一个 32 位字符串作为文件名。 |
|FileExtension |文件后缀必须以 `.` 开头，例如 `“.mp4”`。 |


设置存储路径时，您可以指定完整路径，也可以只指定文件前缀和后缀。


* 调用 `setFileName` 设置完整路径。请确保完整路径必须包含后缀，例如 `.mp4` 或 `.mp3`，否则会发生错误。

   ```Java
   // The file path is tos-pathxxx/volc/test.mp4
   mUploader.setFileName("volc/test.mp4"); 
   // The file path is tos-pathxxx/test.mp4
   mUploader.setFileName("test.mp4");
   ```
   

* 调用 `setFilePrefix` 设置前缀，调用 `setFileExtension` 设置后缀：

   ```Java
   // The file path is tos-pathxxx/volc/b8bb180086f945709dfda76bc9c6133d.mp4
   mUploader.setFileExtension(".mp4");  
   mUploader.setFilePrefix("volc/");  
   // The file path is tos-pathxxx/b8bb180086f945709dfda76bc9c6133d.mp4
   mUploader.setFileExtension(".mp4");
   ```
   


<span id="e95f3071"></span>
### 步骤 7：控制上传流程

上传 SDK 提供以下方法用于控制上传流程：


* 调用 `start` 开始上传：

   ```Java
   mUploader.start();
   ```
   

* 调用 `stop` 暂停上传：

   ```Java
   mUploader.stop();
   ```
   

* 上传完成后，调用 `close` 终止上传。否则会导致内存泄漏。

   ```Java
   mUploader.close()
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VOD 上传 SDK 还提供丰富的高级功能。如需了解更多详情，请参阅以下主题：</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/byteplus-vod/docs/uploading-audios-and-videos">BytePlus VOD 上传 SDK：音频与视频上传</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/byteplus-vod/docs/uploading-materials?version=v1.0">BytePlus VOD 上传 SDK：素材上传</a></div>
