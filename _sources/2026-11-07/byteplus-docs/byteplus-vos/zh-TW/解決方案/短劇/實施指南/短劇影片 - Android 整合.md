---
title: "短劇影片 - Android 整合"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-android-integration-zh-TW"
---

要快速為您的 Android 應用新增完整的短劇影片功能，您可以整合 BytePlus VideoOne 短劇 Demo。本指南詳細介紹了整個流程，包括下載原始碼、配置依賴項，以及自定義業務邏輯、資料模型和諸如付費內容解鎖等特定功能。

<span id="ea713aea"></span>
# 整合方案概覽

BytePlus VideoOne 提供了四種專為短劇影片定製的整合方案。下表突出顯示了這四種方案之間的區別。


|**方案 / 簡介** |**整合短劇 Demo** |**整合短劇影片控制元件** |**整合 PlayerKit 控制元件** |**整合播放器 SDK** |
|---|---|---|---|---|
|說明 |專為短劇影片打造。該方案支援防錄屏、劇集切換、頁面切換時無縫續播、付費內容解鎖及其他短劇專屬功能。 |該方案提供短劇播放框架，不包含其他業務需求。 |基於播放器 SDK 構建。該方案可在 View 層實現影片播放，並隱藏播放器使用細節。 |該方案直接整合播放器 SDK。 |
|目標客戶 |正在開發新應用且能夠替換業務 API 的客戶。 |正在開發新應用或已有應用且能夠替換播放器架構的客戶。 |正在開發新應用或已有應用且能夠替換播放器架構的客戶。 |已有應用且希望透過複用現有播放程式碼並替換播放器核心快速上線短劇功能的客戶。具備強開發能力、豐富播放器經驗且有充足時間開發新應用的客戶。 |
|開發要求 |客戶僅需替換業務 API 並轉換資料結構。 |客戶需自行實現網路連線、短劇播放器 UI、播放頁面切換及支付功能。 |客戶端需自行實現網路連線、短劇播放器介面、播放頁面切換及支付功能。 |客戶端需自行實現播放器功能及短劇相關功能。 |
|上市時間 |最短一週 |最短兩週 |兩週至一個月 |約一個月 |
|相關連結 |本文件 |[vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama) |[vod-playerkit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod/vod-playerkit) |[Android 播放器 SDK：整合 SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android) |


<span id="cea5302c"></span>
# 執行 Demo

在整合短劇 Demo 之前，建議您參考文件[執行 Demo (Android)](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-android--zh-TW)並體驗短劇影片功能。

<span id="f751fbf7"></span>
# 整合短劇 Demo

短劇 Demo 的原始碼位於[vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama)資料夾下的[VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main)倉庫中。其目錄結構如下：

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
## 步驟 1：下載原始碼

執行以下命令，將原始碼下載到本地裝置：

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions
cd Client/Android
```


<span id="7597ea21"></span>
## 步驟 2：複製程式碼

將以下資料夾複製到您專案的根目錄，並保持目錄結構為[VideoOneSolutions/Client/Android](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android)：

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
## 步驟 3：配置 Maven 倉庫

在專案根目錄下的 `build.gradle` 檔案中新增以下配置。

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
## 步驟 4：SDK 整合

要將 SDK 整合到您的專案中，請在模組的 build.gradle 檔案中新增所需的庫。按如下方式新增庫：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">獲取最新版本號，請參見<a href="https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW">客戶端 SDK 元件</a>。</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.43.300.3"
    // BytePlus VOD SDK dependencies
    implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdkVersion"
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="d1098f9a"></span>
## 步驟 5：匯入短劇模組


1. 在 `settings.gradle` 檔案中新增 Demo 模組：


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



2. 在您的應用 `app/build.gradle` 檔案中新增對 `:solutions:vod-mini-drama` 模組的依賴：


```Groovy
dependencies {
    implementation project(':solutions:vod-mini-drama')
}
```



3. 同步 Gradle 檔案。如果 Android Studio 未報錯，則說明 Demo 模組已成功匯入。


<span id="f0bf822e"></span>
## 步驟 6：配置許可權與混淆規則


1. 將 BytePlus VOD Player 所需的混淆規則新增到專案的 `proguard-rules.pro` 檔案中。


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



2. 在 `AndroidManifest.xml` 檔案中宣告 SDK 所需的許可權。


```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">更多資訊請參見<a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android">整合 SDK</a>。</div>


<span id="fa2fcde4"></span>
## 步驟 7：初始化短劇 Demo

呼叫 VodSDK 的 `init` 方法以初始化 Demo。

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
## 步驟 8：整合短劇頁面

您可以參考以下程式碼，直接使用[DramaMainActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/main/DramaMainActivity.java)，該頁面已在 [vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama)模組中配置：

```Java
context.startActivity(new Intent(context, DramaMainActivity.class));
```


<span id="e11d376d"></span>
# 根據您的業務需求定製

要快速使短劇 Demo 適配您的業務需求，請按照以下步驟操作：


1. 自定義資料層，以高效整合關鍵短劇影片功能。包括：

   1. 替換業務 API：實現[vod/minidrama/remote/api/DramaApi](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/api/DramaApi.java)包中定義的 API。

   2. 轉換資料結構：將您的應用伺服器返回的資料結構適配為短劇 Demo 中定義的結構，從而能夠複用 Demo 中的現有業務流程。

2. 自定義短劇專屬功能，如付費內容解鎖。


<span id="aa0af5e1"></span>
## 短劇 Demo 原始碼結構

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
## 適配資料層

<span id="b5aa1afc"></span>
### 替換業務 API


1. 更新“首頁”API：可參考以下示例程式碼，呼叫獲取“首頁”短劇推薦的 API。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">詳細實現請參見<a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/theater/DramaTheaterFragment.java">DramaTheaterFragment.java</a>。</div>


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



2. 更新“Info”頁面的 API：請參考下方示例程式碼，呼叫 API 以獲取“Info”頁面的短劇資訊。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">詳細實現請參見<a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/DramaDetailVideoFragment.java">DramaDetailVideoFragment.java</a>。</div>


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



3. 更新“For you”頁面的 API：請參考下方示例程式碼，呼叫 API 以獲取“For you”頁面的短劇列表。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">詳細實現請參見<a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/recommend/DramaRecommendVideoFragment.java">DramaRecommendVideoFragment.java</a>。</div>


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
### 資料結構轉換

短劇 Demo 層已定義資料結構，包括[DramaInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaInfo.java)（短劇資訊）、[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)（短劇集資訊）、[DramaUnlockMeta](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaUnlockMeta.java)（劇集解鎖資訊）以及[CommentDetail](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-common/src/main/java/com/byteplus/vodcommon/data/remote/api2/model/CommentDetail.java)（評論）。

您必須將從應用伺服器接收到的資料結構轉換為上述資料結構。下表詳細說明了這些資料結構的具體內容。


|**類** |**引數** |**型別** |**必填** |**說明** |
|---|---|---|---|---|
|[DramaInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaInfo.java)<br><br>（短劇資訊） |dramaId |String |必填 |短劇 ID |
||dramaTitle |String |必填 |短劇名稱 |
||dramaCoverUrl |String |必填 |短劇封面 URL |
||dramaPlayTimes |int |必填 |播放次數 |
||orientation |int |必填 |影片方向<br><br>0 : 豎屏<br><br>1 : 橫屏 |
||totalEpisodeNumber |int |必填 |總集數 |
||newRelease |boolean |選填 |是否顯示“新”標籤（預設 false）。<br><br>true : 顯示<br><br>false : 隱藏 |
|[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)<br><br>（劇集資訊） |vid |String |必填 |影片 ID |
||title |String |選填 |影片標題 |
||duration |double |必填 |影片時長（單位：秒） |
||coverUrl |String |必填 |影片封面 URL |
||playAuthToken |String |選填 |該欄位為影片資料來源的 PlayAuthToken，可由 AppServer 透過 BytePlus VOD Server SDK 下發。 |
||subtitleAuthToken |String |選填 |該欄位為影片資料來源的字幕 Token，可由 AppServer 透過 BytePlus VOD Server SDK 下發。 |
||playTimes |int |選填 |播放次數 |
||subtitle |String |選填 |影片副標題 |
||createTime |Date |選填 |上傳時間，格式為*RFC3339* |
||userName |String |選填 |上傳者名稱 |
||userId |String |選填 |上傳者 userId |
||likeCount |int |選填 |點贊數 |
||commentCount |int |選填 |評論數 |
||height |int |必填 |影片高度 |
||width |int |必填 |影片寬度 |
||dramaIndex |int |必填 |劇集列表中的影片位置 |
||dramaId |String |必填 |短劇 ID |
||needVip |boolean |必填 |是否需要付費解鎖（預設 false）。 |
||displayType |DisplayType |必填 |“為你推薦”頁面短劇卡片的展示型別<br><br>0: 文字，無封面圖<br><br>1: 封面，有封面圖 |
|[DramaUnlockMeta](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaUnlockMeta.java)<br><br>（劇集解鎖資訊） |dramaId |String |必填 |短劇 ID |
||vid |String |必填 |影片 ID |
||dramaIndex |int |選填 |劇集列表中的影片位置 |
||playAuthToken |String |必填 |該欄位為影片資料來源的 PlayAuthToken，可由 AppServer 透過 BytePlus VOD Server SDK 下發。 |


短劇 Demo 的影片控制元件使用[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)資料結構。因此，您需要將[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)物件轉換為[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)物件以實現相容。

```Java
// Convert DramaFeed to VideoItem
VideoItem videoItem = DramaFeed.toVideoItem();
```


基於影片控制元件構建的元件使用[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)物件。為實現您的業務邏輯，您必須從[VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java)物件中獲取原始[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)資料。這樣您即可訪問所需的短劇資訊。

```Java
// Get DramaFeed from VideoItem
DramaFeed dramaFeed = DramaFeed.of(videoItem);
```


<span id="3c0ce5a8"></span>
## 定製短劇專屬功能

<span id="5b4b03ce"></span>
### 防錄屏

您可參考下方示例程式碼，透過 Activity 的 `onCreate` 方法呼叫系統 API 以啟用防錄屏功能。在短劇 Demo 中，[DramaDetailVideoActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/DramaDetailVideoActivity.java)和[DramaMainActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/main/DramaMainActivity.java)已啟用防錄屏。更多資訊請參見[防止螢幕錄製](https://docs.byteplus.com/docs/byteplus-vos/docs-anti-screen-recording-zh-TW)。

```Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Window window = getWindow();
    window.addFlags(WindowManager.LayoutParams.FLAG_SECURE);
}
```


<span id="07a883d6"></span>
### 付費內容解鎖

短劇 Demo 中付費內容的解鎖與播放流程如下圖所示。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5MjZweCIgaGVpZ2h0PSI4MDdweCIgdmlld0JveD0iLTAuNSAtMC41IDkyNiA4MDciPjxkZWZzLz48Zz48cmVjdCB4PSI0MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNDA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRyYW1hIFNjZW5lIEtpdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjAzIiB5PSIzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjNweDsgbWFyZ2luLWxlZnQ6IDIwNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzcHg7IG1hcmdpbi1sZWZ0OiA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNjA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBheW1lbnQgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI4MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogODA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXltZW50IFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MyA1MyBMIDYzIDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHJlY3QgeD0iNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iNzQwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNjMgODAzIEwgNjMgNzkzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNjIuNTggNTMgTCAyNjIuNSA0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDYzIDgwMyBMIDQ2Mi41IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NjMuMzEgMzEzIEwgNjY0IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4NjIuOTIgMzQzIEwgODYyLjUgNDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cmVjdCB4PSIyNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iMTEwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDQzMyBMIDI2MyAxNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc2IDczIEwgMjQ0Ljc2IDczLjk1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTAuNzYgNzMuOTkgTCAyNDIuNzQgNzcuOTQgTCAyNDQuNzYgNzMuOTUgTCAyNDIuNzkgNjkuOTQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NHB4OyBtYXJnaW4tbGVmdDogMTY1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bMV1nZXREcmFtYUxpc3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA4MC41IEwgMzQzIDgwLjUgUSAzNTMgODAuNSAzNTMgOTAuNSBMIDM1MyAxMjUuNSBRIDM1MyAxMzUuNSAzNDMgMTM1LjUgTCAyODEuMjQgMTM1LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3NS4yNCAxMzUuNSBMIDI4My4yNCAxMzEuNSBMIDI4MS4yNCAxMzUuNSBMIDI4My4yNCAxMzkuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwOXB4OyBtYXJnaW4tbGVmdDogMzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzEuMV1VbmxvY2tlZCBlcGlzb2RlczxiciAvPsKgbm8gcGxheWJhY2sgYXV0aCB0b2tlbi91cmw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjU0IDE0OS40NyBMIDg1LjI0IDE0Ny44IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc5LjI0IDE0Ny43NCBMIDg3LjI4IDE0My44MiBMIDg1LjI0IDE0Ny44IEwgODcuMiAxNTEuODIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDlweDsgbWFyZ2luLWxlZnQ6IDE2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlsyXVJldHVybiBkcmFtYUxpc3Q8YnIgLz57RHJhbWFGZWVkW119PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NTMiIHk9IjE4MyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjgwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzYgMTkzIEwgNDQxLjc2IDE5Ni40NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDQ3Ljc2IDE5Ni41IEwgNDM5LjczIDIwMC40MiBMIDQ0MS43NiAxOTYuNDQgTCA0MzkuOCAxOTIuNDIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTVweDsgbWFyZ2luLWxlZnQ6IDI2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzNdc2V0SXRlbXModmlkZW9JdGVtc1tdKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDczIDIwMyBMIDUzMyAyMDMgUSA1NDMgMjAzIDU0MyAyMTMgTCA1NDMgMjMzIFEgNTQzIDI0MyA1MzMgMjQzIEwgNDgxLjI0IDI0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjI0IDI0MyBMIDQ4My4yNCAyMzkgTCA0ODEuMjQgMjQzIEwgNDgzLjI0IDI0NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyM3B4OyBtYXJnaW4tbGVmdDogNTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzMuMV1QcmV2aWV3L1BsYXliYWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTMiIHk9IjMxMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjI0MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2NCA4MDMgTCA2NjMuMzIgNTUzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MyAzMjMgTCA2MzkuNzYgMzI0LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY0NS43NiAzMjQuNTEgTCA2MzcuNzUgMzI4LjQ5IEwgNjM5Ljc2IDMyNC41IEwgNjM3Ljc3IDMyMC40OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyNHB4OyBtYXJnaW4tbGVmdDogMzYxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNF1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iODUzIiB5PSIzNDMiIHdpZHRoPSIyMCIgaGVpZ2h0PSIxMjAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA4NjMgODAzIEwgODYzIDQ2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjczIDM1MyBMIDg0NC43NyAzNTYuODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MC43NiAzNTYuOTUgTCA4NDIuNjggMzYwLjc3IEwgODQ0Ljc3IDM1Ni44MiBMIDg0Mi44NiAzNTIuNzcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTVweDsgbWFyZ2luLWxlZnQ6IDc2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzQuMV1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA4NTMgMzkzIEwgNjgxLjI0IDM5NS4xMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzUuMjQgMzk1LjIgTCA2ODMuMTkgMzkxLjEgTCA2ODEuMjQgMzk1LjEzIEwgNjgzLjI4IDM5OS4xIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzk0cHg7IG1hcmdpbi1sZWZ0OiA3NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bNC4yXVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNTMiIHk9IjQzMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjkwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDU3MyBMIDI2MyA1MjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MyA0NDMgTCAyODIuMjQgNDQ1LjQ3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3Ni4yNCA0NDUuNSBMIDI4NC4yMiA0NDEuNDcgTCAyODIuMjQgNDQ1LjQ3IEwgMjg0LjI1IDQ0OS40NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0NHB4OyBtYXJnaW4tbGVmdDogNTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzQuM11Ob3RpZnkgcGF5IHN1Y2Nlc3Mob3JkZXJJZCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjUzIDU0Mi45MiBMIDg2LjI0IDU0NC4zNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4MC4yNCA1NDQuMzUgTCA4OC4yMyA1NDAuMzMgTCA4Ni4yNCA1NDQuMzQgTCA4OC4yNSA1NDguMzMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NDRweDsgbWFyZ2luLWxlZnQ6IDM2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls1XVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA0NTUuNSBMIDMzMyA0NTUuNSBRIDM0MyA0NTUuNSAzNDMgNDY1LjUgTCAzNDMgNDkwLjUgUSAzNDMgNTAwLjUgMzMzIDUwMC41IEwgMjgxLjI0IDUwMC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNzUuMjQgNTAwLjUgTCAyODMuMjQgNDk2LjUgTCAyODEuMjQgNTAwLjUgTCAyODMuMjQgNTA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0NzlweDsgbWFyZ2luLWxlZnQ6IDM0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+WzQuNF08Zm9udCBzdHlsZT0iZm9udC1zaXplOjEzcHgiPlJlY29yZCA8YnIgLz5wYXltZW50IHN0YXR1czwvZm9udD48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDczIDI2MyBMIDEzMyAyNjMgUSAxNDMgMjYzIDE0MyAyNzMgTCAxNDMgMjkzIFEgMTQzIDMwMyAxMzMgMzAzIEwgODEuMjQgMzAzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3NS4yNCAzMDMgTCA4My4yNCAyOTkgTCA4MS4yNCAzMDMgTCA4My4yNCAzMDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODNweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXY+U3dpcGUgdG88L2Rpdj48ZGl2PnVubG9ja2VkIGVwaXNvZGU8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI1MyIgeT0iNTczIiB3aWR0aD0iMjAiIGhlaWdodD0iOTAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNjMgODAzIEwgMjYzIDY2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzMgNTgzIEwgMjQ0Ljc2IDU4MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjUwLjc2IDU4MyBMIDI0Mi43NiA1ODcgTCAyNDQuNzYgNTgzIEwgMjQyLjc2IDU3OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU3M3B4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNl1nZXREcmFtYURldGFpbChvcmRlcklkKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjUzIDY0NC43NSBMIDE3MyA2NDMuMTkgUSAxNjMgNjQzIDE1MyA2NDMgTCA4NC4yNCA2NDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzguMjQgNjQzIEwgODYuMjQgNjM5IEwgODQuMjQgNjQzIEwgODYuMjQgNjQ3IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjIzcHg7IG1hcmdpbi1sZWZ0OiAxNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bN11SZXR1cm4gRHJhbWFVbmxvY2sgbWV0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDUzIiB5PSI2NzAiIHdpZHRoPSIyMCIgaGVpZ2h0PSI4MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MyA2OTAgTCA1MzMgNjkwIFEgNTQzIDY5MCA1NDMgNzAwIEwgNTQzIDcyMCBRIDU0MyA3MzAgNTMzIDczMCBMIDQ4MS4yNCA3MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ3NS4yNCA3MzAgTCA0ODMuMjQgNzI2IEwgNDgxLjI0IDczMCBMIDQ4My4yNCA3MzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3MTBweDsgbWFyZ2luLWxlZnQ6IDU0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls4LjFdUHJldmlldy9QbGF5YmFjazwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3OSA2NzMgTCA0NDQuNzYgNjc2LjQ0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0NTAuNzYgNjc2LjUgTCA0NDIuNzMgNjgwLjQyIEwgNDQ0Ljc2IDY3Ni40NCBMIDQ0Mi44IDY3Mi40MiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3NXB4OyBtYXJnaW4tbGVmdDogMjY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bOF1hcHBlbmRJdGVtcyh2aWRlb0l0ZW1zW10pPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

短劇 Demo 未整合第三方 SDK，僅提供模擬實現以展示流程。

請整合第三方 SDK，並在[DramaEpisodeUnlockByPaymentFragment](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/pay/DramaEpisodeUnlockByPaymentFragment.java)頁面替換模擬支付流程。

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
