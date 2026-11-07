---
title: "在 Android 上實現影片播放"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-video-playback-edit-for-android-zh-TW"
---

本文介紹如何在您的 Android 應用中實現影片播放功能。

<span id="04b63222"></span>
# 開發環境


* Android Studio Arctic Fox 或更高版本。我們強烈建議使用最新版本的 Android Studio，以確保最佳效能。

* 一臺執行 Android 5.0 或以上版本的實體移動裝置。目前不支援在模擬器上構建。

* 請確保您使用的 CPU 架構為 armv7 或 arm64。


<span id="22cc987e"></span>
# 前提條件


* 擁有有效的 [BytePlus 賬號](http://console.byteplus.com/)，並已啟用 [BytePlus VOD](https://console.byteplus.com/vodpaas)。

* 請在 BytePlus VOD 控制檯的 [SDK 管理](https://console.byteplus.com/vodpaas/sdk/)頁面完成以下步驟：

   * 建立應用並獲取應用 ID 及應用英文名稱。

   * 註冊應用後，購買並下載用於 Player SDK 和 Upload SDK 的許可證。對於 Player SDK，我們建議使用高階版。


<span id="889000d5"></span>
# 版本要求


* 要訪問 **影片播放** 和 **媒體上傳**功能，必須使用 BytePlus VOD SDK。請參閱[整合](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-video-playback-edit-for-android-zh-TW#29daa035)部分，獲取每個 SDK 可用的正確版本號。

> 關於各方案所用 SDK 的對應版本，請參閱[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)。


<span id="29daa035"></span>
# 整合

<span id="419c0c9d"></span>
## 步驟 1：新增 Maven 倉庫

開啟專案根目錄下的 `build.gradle` 檔案，在 `repositories` 塊中新增倉庫地址，如下所示：

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
## 步驟 2：整合 SDK

要將 SDK 整合到您的專案中，請在模組級 `build.gradle` 檔案的 `dependencies` 塊中新增所需 SDK 的依賴，如下所示：

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
## 步驟 3：宣告應用許可權

在專案“app”模組下的 `AndroidManifest.xml` 檔案中宣告 SDK 所需許可權，如下所示：

```XML
<!-- BytePlus VOD SDK -->
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.WAKE_LOCK" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


此外，必須在執行時請求寫入儲存許可權。詳情請參見 Android 開發者指南中的 [請求執行時許可權](https://developer.android.com/training/permissions/requesting)。

如果您的應用目標為 Android 10（API 等級 29），且未使用 Scoped Storage，則必須在應用的 `AndroidManifest.xml` 檔案中包含屬性 `android:requestLegacyExternalStorage="true"`：

```XML
<manifest> 
  <application android:requestLegacyExternalStorage="true">         
  </application> 
</manifest>
```


如果您的應用目標為 Android 11（API 等級 30）或更高版本，則必須支援 Scoped Storage。更多詳情請參見 [臨時退出 Scoped Storage](https://developer.android.com/training/data-storage/use-cases#opt-out-scoped-storage)。

<span id="a0d1e7bd"></span>
## 步驟 4：新增混淆規則

為防止 SDK 相關類被混淆，請將以下規則新增到 `proguard-rules.pro` 檔案中。

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
# 實現

<span id="bda47037"></span>
## 影片播放

<span id="6692310a"></span>
### 時序圖

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSIzMjVweCIgdmlld0JveD0iLTAuNSAtMC41IDU2NSAzMjUiPjxkZWZzLz48Zz48cmVjdCB4PSIxNjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2NjZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMDIgNDIgTCAyMDIgMzIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTk3IiB5PSI4MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjkwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzMjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzk5ZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzNjIgNDIgTCAzNjIgMzIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5WT0QgUGxheWVyIFNESzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDgyIiB5PSIyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM5OWZmOTkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTIyIDQyIEwgNTIyIDMyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TWVkaWEgU2VydmVyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MTciIHk9IjE5MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjgwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQyIDkyIEwgMTg5LjM4IDkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTk2LjM4IDkyIEwgMTg5LjM4IDk1LjUgTCAxODkuMzggODguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LWVuZDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDg5cHg7IG1hcmdpbi1sZWZ0OiAxMjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5SZXF1ZXN0IGEgUGxheUF1dGggVG9rZW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzY2ZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MiA0MiBMIDQyIDMyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzNyIgeT0iODIiIHdpZHRoPSIxMCIgaGVpZ2h0PSIxNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDcgMjAyLjAyIEwgMzUzLjg4IDIwMS4wMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM2MC44OCAyMDEgTCAzNTMuODkgMjA0LjUzIEwgMzUzLjg3IDE5Ny41MyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LWVuZDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5OXB4OyBtYXJnaW4tbGVmdDogMjA1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PGRpdiBzdHlsZT0idGV4dC1hbGlnbjpsZWZ0Ij48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjpyZ2IoMjQ4LCAyNDksIDI1MCkiPlBhc3MgdGhlIFBsYXlBdXRoIFRva2VuPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0OC40OCAxNjEuNDYgTCAxOTcuNSAxNjIuNTYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU0LjM4IDE1OCBMIDQ3LjM2IDE2MS40NSBMIDU0LjMzIDE2NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTlweDsgbWFyZ2luLWxlZnQ6IDEyMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTJweCI+UmV0dXJuIHRoZSBQbGF5QXV0aCBUb2tlbjxiciBzdHlsZT0iZm9udC1zaXplOjEycHgiIC8+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjEyIiB5PSI5OCIgd2lkdGg9IjExMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMjhweDsgbWFyZ2luLWxlZnQ6IDIxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Mb2NhbGx5IGNoZWNrIG91dCB0aGUgUGxheUF1dGggVG9rZW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzY0LjE4IDIwMSBMIDUwNy42MyAyMDEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1MTIuODggMjAxIEwgNTA1Ljg4IDIwNC41IEwgNTA3LjYzIDIwMSBMIDUwNS44OCAxOTcuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM1OSIgeT0iMTgyIiB3aWR0aD0iMTYwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTJweDsgbWFyZ2luLWxlZnQ6IDM2MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5PYnRhaW4gcGxheWJhY2sgaW5mb3JtYXRpb248L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTE0IDI2MiBMIDM3MC4zNyAyNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM2NS4xMiAyNjIgTCAzNzIuMTIgMjU4LjUgTCAzNzAuMzcgMjYyIEwgMzcyLjEyIDI2NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzU5IiB5PSIyNDIiIHdpZHRoPSIxNjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI1MnB4OyBtYXJnaW4tbGVmdDogMzYwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJldHVybiBwbGF5YmFjayBpbmZvcm1hdGlvbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" width="565px" />

<span id="7f4900c6"></span>
### 步驟 1：初始化 SDK

建議在 `Application` 類的 `onCreate` 方法中初始化 SDK。請參考以下示例程式碼：

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


初始化 SDK 時，請設定以下引數：


|**名稱** |**型別** |**是否必填** |**預設值** |**描述** |
|---|---|---|---|---|
|AppID |String |是 |無 |應用 ID。您可以在 **SDK 管理** \> **Application** **s** 頁面，在 [BytePlus VOD 控制檯](https://console.byteplus.com/vodpaas/) 獲取應用 ID。 |
|AppName |String |是 |無 |應用名稱。您可以在 **SDK 管理** \> **Application** **s** 頁面，在 [BytePlus VOD 控制檯](https://console.byteplus.com/vodpaas/) 獲取應用名稱。 |
|AppVersion |String |是 |無 |應用版本號。有效的版本號應包含兩個或以上分隔符，例如“1.3.2”。 |
|AppChannel |String |是 |無 |應用分發渠道名稱，例如 Google Play。 |
|LicenseUri |String |是 |無 |您的許可證路徑。您需要將許可證放置在 app/assets 資料夾中，然後將 LicenseUri 引數設定為許可證路徑，例如 assets/license/vod.lic。<br><br>關於許可證的更多資訊，請參見 [Android Player SDK: License guide](https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-guide-android)。 |
|CacheDirPath |String |否 |/data/user/0/<package_name\>/cache/video_cache |影片快取路徑。 |
|MaxCacheSize |Int |否 |300 \* 1024 \* 1024 (300 MB) |影片快取資料夾的最大位元組數。 |


<span id="265a5194"></span>
### 步驟 2：建立播放器例項

使用 `TTVideoEngine` 類建立播放器例項，如下所示：

```Java
// When creating the instance, pass in the app context
TTVideoEngine ttVideoEngine = new TTVideoEngine(context, TTVideoEngine.PLAYER_TYPE_OWN);
```


<span id="9f79cb87"></span>
### 步驟 3：設定用於顯示影片的檢視

要顯示影片，請將播放器繫結到 TextureView 或 SurfaceView。

<span id="eae89f96"></span>
#### 繫結播放器到 TextureView


1. 在 XML 中宣告 TextureView，如下所示：

   ```XML
   <TextureView
       android:id="@+id/textureView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:background="@null" />
   ```
   

   如果您的應用目標為 Android API 等級 24 或更高，在宣告 TextureView 時，不應設定 `background`，或必須將 `background` 設定為 `null`。否則，應用將會崩潰。

2. 獲取您宣告的紋理檢視的 `SurfaceTexture` 例項，並將其傳遞給 `TTVideoEngine`。隨後可以使用 `SurfaceTexture` 來渲染來自 `TTVideoEngine` 的影片。請參見以下示例程式碼：

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
#### 將播放器繫結到 SurfaceView


1. 在 XML 中宣告一個 SurfaceView，如下所示：

   ```XML
   <SurfaceView
       android:id="@+id/surfaceView"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```
   

2. `SurfaceView` 提供專用的繪圖表面。您可以透過 `SurfaceHolder` 介面獲取底層表面，該介面可透過呼叫 `getHolder()` 獲得。將 `SurfaceHolder` 介面傳遞給 `TTVideoEngine`，然後 `SurfaceView` 即可顯示來自 `TTVideoEngine` 的影片。請參見以下示例程式碼：

   ```Java
   SurfaceView surfaceView = findViewById(R.id.surfaceView); 
   // Pass the SurfaceHolder to TTVideoEngine
   ttVideoEngine.setSurfaceHolder(surfaceView.getHolder());
   ```
   

> 注意事項：

> * 必須在呼叫 `ttVideoEngine.play` 之前呼叫 `ttVideoEngine.setSurface` 和 `ttVideoEngine.setSurfaceHolder` 方法。

> * 從 Android API 級別 24 開始，SurfaceView 支援與檢視樹中的其他檢視同步視窗中的渲染位置。如果您的應用目標為 Android API 級別 24 或更低，可能會出現檢視層級問題和動畫不同步。詳情請參見 Android API 參考中的[SurfaceView](https://developer.android.com/reference/android/view/SurfaceView.html)。


<span id="a0a98231"></span>
### 步驟 4：設定影片源

SDK 支援播放本地影片和線上影片。本節介紹如何播放不同來源的影片。

<span id="7f0f2764"></span>
#### 透過影片 ID 播放影片

如果您將影片上傳至 BytePlus VOD 服務，可以使用關聯的影片 ID 播放影片。您需要設定 `vid` 和 `playAuthToken` 引數，這些引數可從您的應用伺服器獲取。

請參見以下示例程式碼：

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


組裝影片源時，請設定以下引數：


|**引數** |**型別** |**必填** |**預設值** |**描述** |
|---|---|---|---|---|
|Vid |String |是 |無 |影片 ID。 |
|PlayAuthToken |String |是 |無 |播放令牌。 |
|EncodeType |Int |否 |CODEC_TYPE_H264 |編解碼型別：<br><br><br>* H.264（預設）<br><br>* ByteVC1（僅 SDK 高階版可用） |
|Resolution |Resolution |否 |Standard |影片解析度。請參見下表。 |


解析度


|檔位 |影片質量 |音訊質量 |
|---|---|---|
|Standard |360p，SD（標清） |普通 |
|High |480p，HD（高畫質） |高 |
|SuperHigh |720p，FHD（全高畫質） |非常高 |
|ExtremelyHigh |1080p |原始 |
|TwoK |2K |此引數不影響音訊質量。 |
|FourK |4K |此引數不影響音訊質量。 |
|Auto |對於 DASH 影片，播放器會根據觀眾的網路連線自動決定最佳解析度，並在播放過程中調整影片質量以最大限度減少緩衝風險。 |此引數不影響音訊質量。 |


<span id="d3e181c3"></span>
#### 透過 HTTP URL 播放影片

如果您將影片上傳至 BytePlus VOD 服務或第三方儲存服務，可以透過 HTTP URL 播放影片。您需要設定 `url` 引數。

請參見以下示例程式碼：

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


組裝影片源時，請設定以下引數：


|**引數** |**型別** |**必填** |**預設值** |**描述** |
|---|---|---|---|---|
|Vid |String |是 |無 |影片 ID。 |
|Url |String |是 |無 |影片的 HTTP URL。 |
|CacheKey |String |是 |無 |快取鍵，必須滿足以下要求：<br><br><br>* 不應包含任何特殊字元，並且可作為檔名使用。<br><br>* 每個影片都有唯一的快取鍵。<br><br><br>建議使用 URL 的 MD5 作為快取鍵。 |


<span id="5d4504af"></span>
#### 播放本地影片

如果播放本地影片，請將本地地址賦值給 `videoFile` 引數。請參見以下示例程式碼：

```Java
// Replace "/sdcard/Download/video.MP4" with the local video file path
File videoFile = new File("/sdcard/Download/video.MP4"); 
ttVideoEngine.setLocalURL(videoFile.getAbsolutePath()); 
ttVideoEngine.play() 
```


<span id="ff0aee11"></span>
### 步驟 5：控制影片播放

`TTVideoEngine` 類提供以下方法用於控制影片播放：


* 呼叫 `play` 以開始或恢復播放。

   ```Java
   ttVideoEngine.play();
   ```
   

* 呼叫 `pause` 以暫停播放。呼叫 `play` 以恢復播放。

   ```Java
   ttVideoEngine.pause();
   ttVideoEngine.play();
   ```
   

* 呼叫 `seekTo` 以跳轉到指定時間位置。此功能允許使用者透過拖動進度條手動調整影片播放，實現快進或快退。

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
   

* 在呼叫 `play` 之前，呼叫 `setStartTime` 以指定播放開始的時間位置。此方法可用於“跳過片頭”功能。

   ```Java
   int startPlayPositionMS = 1000;
   // Set the start time as one second
   ttVideoEngine.setStartTime(startPlayPositionMS);
   ttVideoEngine.play();
   ```
   

* 呼叫 `stop` 以停止播放。

   ```Java
   ttVideoEngine.stop();
   ```
   


<span id="8798b2ce"></span>
### 步驟 6：釋放播放器例項

當影片播放結束或使用者離開正在播放影片的頁面時，可以透過呼叫 `releaseAsync` 停止播放並釋放播放器例項。此操作會釋放 `ttVideoEngine` 所使用的硬體解碼器、記憶體和網路資源，以節省電量。

釋放播放器例項後，不能再呼叫 `ttVideoEngine` 類中的方法。建議將 `ttVideoEngine` 設定為 `null`，以確保不再引用已釋放的播放器例項。這有助於防止訪問已釋放的播放器例項或消耗不必要的記憶體資源等潛在問題。

```Java
ttVideoEngine.releaseAsync(); 
ttVideoEngine = null;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VOD Player SDK 還提供豐富的高階功能。如需詳細資訊，請參閱以下主題：</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-android">Android Player SDK：基礎功能</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-advanced-features-android">Android Player SDK：高階功能</a></div>



<span id="dfb8fe29"></span>
## 媒體上傳

本節介紹如何使用 VOD 上傳 SDK。

<span id="7b23a02a"></span>
### 時序圖

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSI0MDVweCIgdmlld0JveD0iLTAuNSAtMC41IDU2NSA0MDUiPjxkZWZzLz48Zz48cmVjdCB4PSIxNjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2NjZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMDIgNDIgTCAyMDIgNDAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTk3IiB5PSI4MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjkwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzMjIiIHk9IjIiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzk5ZmY5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzNjIgNDIgTCAzNjIgNDAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMnB4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5WT0QgVXBsb2FkIFNESzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDgyIiB5PSIyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM5OWZmOTkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTIyIDQyIEwgNTIyIDQwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TWVkaWEgU2VydmVyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MTciIHk9IjE5MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjE5MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0MiA5MiBMIDE4OS4zOCA5MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE5Ni4zOCA5MiBMIDE4OS4zOCA5NS41IEwgMTg5LjM4IDg4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4OXB4OyBtYXJnaW4tbGVmdDogMTIwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+UmVxdWVzdCBhbiA8YnIgLz5VcGxvYWRBdXRoIFRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM2NmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDIgNDIgTCA0MiA0MDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIENsaWVudDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzciIHk9IjgyIiB3aWR0aD0iMTAiIGhlaWdodD0iMTUwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3IDIwMi4wMiBMIDM1My44OCAyMDEuMDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzNjAuODggMjAxIEwgMzUzLjg5IDIwNC41MyBMIDM1My44NyAxOTcuNTMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTlweDsgbWFyZ2luLWxlZnQ6IDIwNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXYgc3R5bGU9InRleHQtYWxpZ246bGVmdCI+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5QYXNzIHRoZSBVcGxvYWRBdXRoIFRva2VuPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0OC40OCAxNjEuNDYgTCAxOTcuNSAxNjIuNTYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU0LjM4IDE1OCBMIDQ3LjM2IDE2MS40NSBMIDU0LjMzIDE2NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1lbmQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTlweDsgbWFyZ2luLWxlZnQ6IDEyMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTJweCI+UmV0dXJuIHRoZSA8YnIgLz5VcGxvYWRBdXRoIFRva2VuPGJyIHN0eWxlPSJmb250LXNpemU6MTJweCIgLz48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyMTIiIHk9Ijk4IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyOHB4OyBtYXJnaW4tbGVmdDogMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkxvY2FsbHkgY2hlY2sgb3V0IHRoZSBVcGxvYWRBdXRoIFRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM2NC4xOCAyMDEgTCA1MDcuNjMgMjAxIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTEyLjg4IDIwMSBMIDUwNS44OCAyMDQuNSBMIDUwNy42MyAyMDEgTCA1MDUuODggMTk3LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTkiIHk9IjE3NSIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTg1cHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+T2J0YWluIHRoZSBzdG9yYWdlIHVybCBhbmQgY3JlZGVudGlhbHM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTE0IDI2MiBMIDM3MC4zNyAyNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM2NS4xMiAyNjIgTCAzNzIuMTIgMjU4LjUgTCAzNzAuMzcgMjYyIEwgMzcyLjEyIDI2NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzU5IiB5PSIyMzYiIHdpZHRoPSIxNjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI0NnB4OyBtYXJnaW4tbGVmdDogMzYwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJldHVybiB0aGUgc3RvcmFnZSB1cmwgYW5kIGNyZWRlbnRpYWxzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM2NC4xOCAzMDggTCA1MDcuNjMgMzA4IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTEyLjg4IDMwOCBMIDUwNS44OCAzMTEuNSBMIDUwNy42MyAzMDggTCA1MDUuODggMzA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTkiIHk9IjI5MCIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzAwcHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VXBsb2FkIHRoZSBtZWRpYTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1MTQgMzY4IEwgMzcwLjM3IDM2OCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzY1LjEyIDM2OCBMIDM3Mi4xMiAzNjQuNSBMIDM3MC4zNyAzNjggTCAzNzIuMTIgMzcxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTkiIHk9IjM0OCIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzU4cHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmV0dXJuIHRoZSB1cGxvYWQgcmVzdWx0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" width="565px" />

<span id="9e157fb4"></span>
### 步驟 1：初始化 SDK

建議您在 `onCreate` 方法的 `Application` 類中初始化 SDK。請參見以下示例程式碼：

```Java
Env.init(new Config.Builder() 
        .setApplicationContext(context) 
        .setAppID("your app id") 
        .setAppName("your app English name") 
        .setAppVersion(BuildConfig.VERSION_NAME) 
        .setAppChannel("channel name") 
        .build());
```


初始化 SDK 時，請設定以下引數：


|**引數** |**型別** |**描述** |
|---|---|---|
|AppID |String |應用 ID。您可以在 **SDK 管理** \> **應用** **s** 頁面上的 [BytePlus VOD 控制檯](https://console.byteplus.com/vodpaas/) 獲取應用 ID。 |
|AppName |String |應用名稱。您可以在 **SDK 管理** \> **應用** **s** 頁面上的 [BytePlus VOD 控制檯](https://console.byteplus.com/vodpaas/) 獲取應用名稱。 |
|AppVersion |String |應用版本號。有效的版本號應包含兩個或以上的分隔符，例如“`1.3.2`”。 |
||||
|AppChannel |String |應用分發渠道的名稱，例如 Google Play。 |
||||


<span id="d9932e09"></span>
### 步驟 2：建立上傳器例項

使用 `BDVideoUploader` 類建立上傳器例項，操作如下：

```Java
BDVideoUploader mUploader = new BDVideoUploader();
```


<span id="0897b289"></span>
### 步驟 3：指定待上傳檔案的路徑

呼叫 `setPathName` 指定待上傳檔案的絕對路徑：

```Java
mUploader.setPathName("/data/user/0/xxx/files/test.mp4");
```


<span id="6af71b71"></span>
### 步驟 4：設定鑑權引數

從您的應用伺服器獲取鑑權引數，並傳遞給 SDK：

```Java
mUploader.setTopAccessKey("xxx"); 
mUploader.setTopSecretKey("xxx"); 
mUploader.setTopSessionToken("xxx");
```


<span id="1bdae923"></span>
### 步驟 5：指定檔案上傳的空間

呼叫 `setSpaceName` 設定檔案上傳的空間。關於空間的詳細資訊，請參見 [空間管理](https://docs.byteplus.com/en/byteplus-vod/docs/space-management)。

```Java
mUploader.setSpaceName("xxx");
```


<span id="38ed2fde"></span>
### 步驟 6：指定雲端儲存中的檔案路徑

上傳完成後，雲端儲存中的檔案路徑如下：

`StoreUri={{BucketName}}/{{FilePrefix}}{{FileTitle}}{{FileExtension}}`


|**Parameter** |**Description** |
|---|---|
|BucketName |桶名稱由系統自動生成。 |
|FilePrefix |檔案字首必須以 `/` 結尾，例如 `“path/to/foo/bar/”`。 |
|FileTitle |檔名稱。如未設定，SDK 將自動生成一個 32 位字串作為檔名。 |
|FileExtension |檔案字尾必須以 `.` 開頭，例如 `“.mp4”`。 |


設定儲存路徑時，您可以指定完整路徑，也可以只指定檔案字首和字尾。


* 呼叫 `setFileName` 設定完整路徑。請確保完整路徑必須包含字尾，例如 `.mp4` 或 `.mp3`，否則會發生錯誤。

   ```Java
   // The file path is tos-pathxxx/volc/test.mp4
   mUploader.setFileName("volc/test.mp4"); 
   // The file path is tos-pathxxx/test.mp4
   mUploader.setFileName("test.mp4");
   ```
   

* 呼叫 `setFilePrefix` 設定字首，呼叫 `setFileExtension` 設定字尾：

   ```Java
   // The file path is tos-pathxxx/volc/b8bb180086f945709dfda76bc9c6133d.mp4
   mUploader.setFileExtension(".mp4");  
   mUploader.setFilePrefix("volc/");  
   // The file path is tos-pathxxx/b8bb180086f945709dfda76bc9c6133d.mp4
   mUploader.setFileExtension(".mp4");
   ```
   


<span id="e95f3071"></span>
### 步驟 7：控制上傳流程

上傳 SDK 提供以下方法用於控制上傳流程：


* 呼叫 `start` 開始上傳：

   ```Java
   mUploader.start();
   ```
   

* 呼叫 `stop` 暫停上傳：

   ```Java
   mUploader.stop();
   ```
   

* 上傳完成後，呼叫 `close` 終止上傳。否則會導致記憶體洩漏。

   ```Java
   mUploader.close()
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VOD 上傳 SDK 還提供豐富的高階功能。如需瞭解更多詳情，請參閱以下主題：</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/byteplus-vod/docs/uploading-audios-and-videos">BytePlus VOD 上傳 SDK：音訊與影片上傳</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/byteplus-vod/docs/uploading-materials?version=v1.0">BytePlus VOD 上傳 SDK：素材上傳</a></div>
