---
title: "Short drama videos - Android integration"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-android-integration"
---

To quickly add a complete short drama video feature to your Android app, you can integrate the BytePlus VideoOne short drama demo. This guide details the entire process, from downloading the source code and configuring dependencies to customizing business logic, data models, and specific features like paid content unlocking.

<span id="ea713aea"></span>
# Overview of integration solutions

BytePlus VideoOne offers four integration solutions tailored for short drama videos. The table below highlights the distinctions among these four solutions.


|**Solution / Introduction** |**Integrating the short drama demo** |**Integrating the short drama video controls** |**Integrating the PlayerKit controls** |**Integrating the player SDK** |
|---|---|---|---|---|
|Description |Built for short drama videos. This solution supports screen capture protection, episode switching, resuming playback seamlessly when switching pages, unlocking paid content and other short drama\-specific features. |This solution provides a framework for short drama playback, but doesn't include other business needs. |Built on the player SDK. This solution provides the ability to play videos on the View level and hides the details on how the player is used. |This solution directly integrates the player SDK. |
|Target client |Clients who are developing new apps and are able to replace the business APIs. |Clients who are developing new apps or have existing apps and are able to replace the player architecture. |Clients who are developing new apps or have existing apps and are able to replace the player architecture. |Clients who have existing apps and want to release the short drama features quickly by reusing the existing playback code and replacing the player kernel. Clients with strong development capabilities, extensive experience with players, and ample time to develop new apps. |
|Required development |Clients only need to replace the business APIs and convert the data structures. |Clients need to implement network connectivity, the short drama player UI, playback page switching, and payment functionality themselves. |Clients need to implement network connectivity, the short drama player UI, playback page switching, and payment functionality themselves. |Clients need to implement the player features and short drama\-specific features themselves. |
|Time to market |As short as one week |As short as two weeks |Two weeks to one month |Approximately one month |
|Related links |This document |[vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama) |[vod-playerkit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod/vod-playerkit) |[Android Player SDK: Integrating the SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android) |


<span id="cea5302c"></span>
# Running the demo

Before integrating the short drama demo, we recommend that you refer to the document [Running the demo (Android)](https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-android-) and try the short drama video features.

<span id="f751fbf7"></span>
# Integrating the short drama demo

The source code of the short drama demo is located in the [vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama) folder under the [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main) repository. Its directory structure is as follows:

```Bash
.
├── app                    # Entry point of the app 
├── build.gradle 
├── component              # Public components 
│   ├── avatars            # Avatar resources 
│   ├── loginkit           # Login 
│   └── solution-base      # Base library 
│   └── ...
└── solutions              # Solutions 
    ├── vod                # The video playback scene 
    │   ├── vod-playerkit  # VOD player kit
    │   ├── vod-scenekit   # VOD scene kit
    │   └── ...
    ├── vod-mini-drama     # The mini drama scene 
    └── ...
```


<span id="19027710"></span>
## Step 1: Download the source code

Run the following commands to download the source code to your local device:

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions
cd Client/Android
```


<span id="7597ea21"></span>
## Step 2: Copy the code

Copy the following folders to the root directory of your project and keep the directory structure as [VideoOneSolutions/Client/Android](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android):

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
## Step 3: Configure the Maven repository

Add the following configurations to the `build.gradle` file in the root directory of the project.

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
## Step 4: SDK integration

To integrate the SDK into your project, add the required libraries to your module's build.gradle file. Add the libraries as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To get the latest version number, see <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">Client SDK components</a></div>


```Groovy
dependencies {
    def ttsdkVersion = "1.43.300.3"
    // BytePlus VOD SDK dependencies
    implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdkVersion"
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="d1098f9a"></span>
## Step 5: Import the short drama module


1. Add the demo module to the `settings.gradle` file:


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



2. Add a dependency on the `:solutions:vod-mini-drama` module in your app's `app/build.gradle` file:


```Groovy
dependencies {
    implementation project(':solutions:vod-mini-drama')
}
```



3. Sync the Gradle files. If Android Studio doesn't report any errors, it means the demo module has been imported successfully.


<span id="f0bf822e"></span>
## Step 6: Configure permissions and obfuscation rules


1. Add the obfuscation rules required by the BytePlus VOD Player to the `proguard-rules.pro` file of the project.


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



2. Declare the permissions required by the SDK in the `AndroidManifest.xml` file.


```XML
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android">Integrating the SDK</a>.</div>


<span id="fa2fcde4"></span>
## Step 7: Initialize the short drama demo

Call the `init` method of the VodSDK to initialize the demo.

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
## Step 8: Integrate the short drama pages

You can refer to the code below to directly use the [DramaMainActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/main/DramaMainActivity.java) that has been configured in the[vod-mini-drama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-mini-drama) module:

```Java
context.startActivity(new Intent(context, DramaMainActivity.class));
```


<span id="e11d376d"></span>
# Tailoring to your business requirements

To quickly align the short drama demo with your business requirements, follow the steps below:


1. Customize the data layer to efficiently incorporate essential short drama video features. This involves:

   1. Replacing the business APIs: Implement the APIs outlined in the [vod/minidrama/remote/api/DramaApi](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/api/DramaApi.java) package.

   2. Converting the data structure: Adapt the data structure received from your app server to match the structure defined in the short drama demo, enabling utilization of existing business workflows in the demo.

2. Customize short drama\-specific functionalities like unlocking paid content.


<span id="aa0af5e1"></span>
## Source code structure of the short drama demo

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
## Adapting the data layer

<span id="b5aa1afc"></span>
### Replace the business APIs


1. Update the "Home" page API: Refer to the sample code below to call the API that gets short drama recommendations for the "Home" page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed implementation, refer to <a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/theater/DramaTheaterFragment.java">DramaTheaterFragment.java</a>.</div>


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



2. Update the "Info" page API: Refer to the sample code below to call the API that gets short drama information for the "Info" page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed implementation, refer to <a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/DramaDetailVideoFragment.java">DramaDetailVideoFragment.java</a>.</div>


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



3. Update the "For you" page API: Refer to the sample code below to call the API that gets short drama lists for the "For you" page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed implementation, refer to <a href="https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/recommend/DramaRecommendVideoFragment.java">DramaRecommendVideoFragment.java</a>.</div>


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
### Converting the data structure

The short drama demo layer has defined data structures including [DramaInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaInfo.java) (short drama information), [DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java) (short drama episode information), [DramaUnlockMeta](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaUnlockMeta.java) (episode unlocking information), and [CommentDetail](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-common/src/main/java/com/byteplus/vodcommon/data/remote/api2/model/CommentDetail.java) (comments).

You must convert the data structures received from your app server into these data structures. The table below provides a breakdown of the details of these data structures.


|**Class** |**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|[DramaInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaInfo.java)<br><br>（Short drama info） |dramaId |String |Required |Drama ID |
||dramaTitle |String |Required |Short drama name |
||dramaCoverUrl |String |Required |Short drama cover URL |
||dramaPlayTimes |int |Required |Playback count |
||orientation |int |Required |Video orientation<br><br>0 : PORTRAIT<br><br>1 : LANDSCAPE |
||totalEpisodeNumber |int |Required |Total number of episodes |
||newRelease |boolean |Optional |Whether to display a "New" label (false by default).<br><br>true : Display<br><br>false : Hide |
|[DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java)<br><br>（Episode info） |vid |String |Required |Video ID |
||title |String |Optional |Video title |
||duration |double |Required |Video duration (in seconds) |
||coverUrl |String |Required |Video cover URL |
||playAuthToken |String |Optional |This is the PlayAuthToken for the video's data source, which can be issued by the AppServer through the BytePlus VOD Server SDK. |
||subtitleAuthToken |String |Optional |The subtitle token for the video's data source which can be issued by the AppServer through the BytePlus VOD Server SDK. |
||playTimes |int |Optional |Playback count |
||subtitle |String |Optional |Subheading of the video |
||createTime |Date |Optional |Time of uploading in *RFC3339* format |
||userName |String |Optional |Uploader name |
||userId |String |Optional |Uploader's userId |
||likeCount |int |Optional |Number of likes |
||commentCount |int |Optional |Number of comments |
||height |int |Required |Video height |
||width |int |Required |Video width |
||dramaIndex |int |Required |Video position in the episode list |
||dramaId |String |Required |Short drama ID |
||needVip |boolean |Required |Whether payment is required to unlock (false by default). |
||displayType |DisplayType |Required |Display type of the short drama card on the "For you" page<br><br>0: TEXT, without cover image<br><br>1: COVER, with cover image |
|[DramaUnlockMeta](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaUnlockMeta.java)<br><br>（Episode unlocking info） |dramaId |String |Required |Short drama ID |
||vid |String |Required |Video ID |
||dramaIndex |int |Optional |Video position in the episode list |
||playAuthToken |String |Required |The PlayAuthToken of the video's data source which can be issued by the AppServer through the BytePlus VOD Server SDK. |


The short drama demo's video controls use the [VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java) data structure. Therefore, you must convert [DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java) objects to [VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java) objects for compatibility.

```Java
// Convert DramaFeed to VideoItem
VideoItem videoItem = DramaFeed.toVideoItem();
```


Components built on the video controls use [VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java) objects. To implement your business logic, you must retrieve the original [DramaFeed](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/remote/model/drama/DramaFeed.java) data from a [VideoItem](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-scenekit/src/main/java/com/byteplus/vod/scenekit/data/model/VideoItem.java) object. This allows you to access the necessary short drama information.

```Java
// Get DramaFeed from VideoItem
DramaFeed dramaFeed = DramaFeed.of(videoItem);
```


<span id="3c0ce5a8"></span>
## Customizing short drama\-specific features

<span id="5b4b03ce"></span>
### Anti\-screen recording

You can refer to the sample code below to call the system API through the Activity `onCreate` method to enable anti\-screen recording. In the short drama demo, anti\-screen recording has been enabled for [DramaDetailVideoActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/DramaDetailVideoActivity.java) and [DramaMainActivity](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/main/DramaMainActivity.java). For more information, refer to [Preventing screen recording](https://docs.byteplus.com/en/docs/byteplus-vos/docs-anti-screen-recording#window-anti-screen-recording-anti-screenshot).

```Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Window window = getWindow();
    window.addFlags(WindowManager.LayoutParams.FLAG_SECURE);
}
```


<span id="07a883d6"></span>
### Unlocking paid content

The process for unlocking and playing paid content in the short drama demo is shown in the image below.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5MjZweCIgaGVpZ2h0PSI4MDdweCIgdmlld0JveD0iLTAuNSAtMC41IDkyNiA4MDciPjxkZWZzLz48Zz48cmVjdCB4PSI0MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNDA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRyYW1hIFNjZW5lIEtpdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjAzIiB5PSIzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjNweDsgbWFyZ2luLWxlZnQ6IDIwNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzcHg7IG1hcmdpbi1sZWZ0OiA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNjA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBheW1lbnQgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI4MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogODA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXltZW50IFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MyA1MyBMIDYzIDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHJlY3QgeD0iNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iNzQwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNjMgODAzIEwgNjMgNzkzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNjIuNTggNTMgTCAyNjIuNSA0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDYzIDgwMyBMIDQ2Mi41IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NjMuMzEgMzEzIEwgNjY0IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4NjIuOTIgMzQzIEwgODYyLjUgNDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cmVjdCB4PSIyNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iMTEwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDQzMyBMIDI2MyAxNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc2IDczIEwgMjQ0Ljc2IDczLjk1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTAuNzYgNzMuOTkgTCAyNDIuNzQgNzcuOTQgTCAyNDQuNzYgNzMuOTUgTCAyNDIuNzkgNjkuOTQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NHB4OyBtYXJnaW4tbGVmdDogMTY1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bMV1nZXREcmFtYUxpc3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA4MC41IEwgMzQzIDgwLjUgUSAzNTMgODAuNSAzNTMgOTAuNSBMIDM1MyAxMjUuNSBRIDM1MyAxMzUuNSAzNDMgMTM1LjUgTCAyODEuMjQgMTM1LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3NS4yNCAxMzUuNSBMIDI4My4yNCAxMzEuNSBMIDI4MS4yNCAxMzUuNSBMIDI4My4yNCAxMzkuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwOXB4OyBtYXJnaW4tbGVmdDogMzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzEuMV1VbmxvY2tlZCBlcGlzb2RlczxiciAvPsKgbm8gcGxheWJhY2sgYXV0aCB0b2tlbi91cmw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjU0IDE0OS40NyBMIDg1LjI0IDE0Ny44IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc5LjI0IDE0Ny43NCBMIDg3LjI4IDE0My44MiBMIDg1LjI0IDE0Ny44IEwgODcuMiAxNTEuODIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDlweDsgbWFyZ2luLWxlZnQ6IDE2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlsyXVJldHVybiBkcmFtYUxpc3Q8YnIgLz57RHJhbWFGZWVkW119PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NTMiIHk9IjE4MyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjgwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzYgMTkzIEwgNDQxLjc2IDE5Ni40NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDQ3Ljc2IDE5Ni41IEwgNDM5LjczIDIwMC40MiBMIDQ0MS43NiAxOTYuNDQgTCA0MzkuOCAxOTIuNDIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTVweDsgbWFyZ2luLWxlZnQ6IDI2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzNdc2V0SXRlbXModmlkZW9JdGVtc1tdKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDczIDIwMyBMIDUzMyAyMDMgUSA1NDMgMjAzIDU0MyAyMTMgTCA1NDMgMjMzIFEgNTQzIDI0MyA1MzMgMjQzIEwgNDgxLjI0IDI0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjI0IDI0MyBMIDQ4My4yNCAyMzkgTCA0ODEuMjQgMjQzIEwgNDgzLjI0IDI0NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyM3B4OyBtYXJnaW4tbGVmdDogNTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzMuMV1QcmV2aWV3L1BsYXliYWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTMiIHk9IjMxMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjI0MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2NCA4MDMgTCA2NjMuMzIgNTUzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MyAzMjMgTCA2MzkuNzYgMzI0LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY0NS43NiAzMjQuNTEgTCA2MzcuNzUgMzI4LjQ5IEwgNjM5Ljc2IDMyNC41IEwgNjM3Ljc3IDMyMC40OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyNHB4OyBtYXJnaW4tbGVmdDogMzYxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNF1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iODUzIiB5PSIzNDMiIHdpZHRoPSIyMCIgaGVpZ2h0PSIxMjAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA4NjMgODAzIEwgODYzIDQ2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjczIDM1MyBMIDg0NC43NyAzNTYuODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MC43NiAzNTYuOTUgTCA4NDIuNjggMzYwLjc3IEwgODQ0Ljc3IDM1Ni44MiBMIDg0Mi44NiAzNTIuNzcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTVweDsgbWFyZ2luLWxlZnQ6IDc2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzQuMV1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA4NTMgMzkzIEwgNjgxLjI0IDM5NS4xMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzUuMjQgMzk1LjIgTCA2ODMuMTkgMzkxLjEgTCA2ODEuMjQgMzk1LjEzIEwgNjgzLjI4IDM5OS4xIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzk0cHg7IG1hcmdpbi1sZWZ0OiA3NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bNC4yXVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNTMiIHk9IjQzMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjkwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDU3MyBMIDI2MyA1MjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MyA0NDMgTCAyODIuMjQgNDQ1LjQ3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3Ni4yNCA0NDUuNSBMIDI4NC4yMiA0NDEuNDcgTCAyODIuMjQgNDQ1LjQ3IEwgMjg0LjI1IDQ0OS40NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0NHB4OyBtYXJnaW4tbGVmdDogNTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzQuM11Ob3RpZnkgcGF5IHN1Y2Nlc3Mob3JkZXJJZCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjUzIDU0Mi45MiBMIDg2LjI0IDU0NC4zNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4MC4yNCA1NDQuMzUgTCA4OC4yMyA1NDAuMzMgTCA4Ni4yNCA1NDQuMzQgTCA4OC4yNSA1NDguMzMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NDRweDsgbWFyZ2luLWxlZnQ6IDM2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls1XVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA0NTUuNSBMIDMzMyA0NTUuNSBRIDM0MyA0NTUuNSAzNDMgNDY1LjUgTCAzNDMgNDkwLjUgUSAzNDMgNTAwLjUgMzMzIDUwMC41IEwgMjgxLjI0IDUwMC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNzUuMjQgNTAwLjUgTCAyODMuMjQgNDk2LjUgTCAyODEuMjQgNTAwLjUgTCAyODMuMjQgNTA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0NzlweDsgbWFyZ2luLWxlZnQ6IDM0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+WzQuNF08Zm9udCBzdHlsZT0iZm9udC1zaXplOjEzcHgiPlJlY29yZCA8YnIgLz5wYXltZW50IHN0YXR1czwvZm9udD48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDczIDI2MyBMIDEzMyAyNjMgUSAxNDMgMjYzIDE0MyAyNzMgTCAxNDMgMjkzIFEgMTQzIDMwMyAxMzMgMzAzIEwgODEuMjQgMzAzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3NS4yNCAzMDMgTCA4My4yNCAyOTkgTCA4MS4yNCAzMDMgTCA4My4yNCAzMDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODNweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXY+U3dpcGUgdG88L2Rpdj48ZGl2PnVubG9ja2VkIGVwaXNvZGU8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI1MyIgeT0iNTczIiB3aWR0aD0iMjAiIGhlaWdodD0iOTAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNjMgODAzIEwgMjYzIDY2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzMgNTgzIEwgMjQ0Ljc2IDU4MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjUwLjc2IDU4MyBMIDI0Mi43NiA1ODcgTCAyNDQuNzYgNTgzIEwgMjQyLjc2IDU3OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU3M3B4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNl1nZXREcmFtYURldGFpbChvcmRlcklkKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjUzIDY0NC43NSBMIDE3MyA2NDMuMTkgUSAxNjMgNjQzIDE1MyA2NDMgTCA4NC4yNCA2NDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzguMjQgNjQzIEwgODYuMjQgNjM5IEwgODQuMjQgNjQzIEwgODYuMjQgNjQ3IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjIzcHg7IG1hcmdpbi1sZWZ0OiAxNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bN11SZXR1cm4gRHJhbWFVbmxvY2sgbWV0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDUzIiB5PSI2NzAiIHdpZHRoPSIyMCIgaGVpZ2h0PSI4MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MyA2OTAgTCA1MzMgNjkwIFEgNTQzIDY5MCA1NDMgNzAwIEwgNTQzIDcyMCBRIDU0MyA3MzAgNTMzIDczMCBMIDQ4MS4yNCA3MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ3NS4yNCA3MzAgTCA0ODMuMjQgNzI2IEwgNDgxLjI0IDczMCBMIDQ4My4yNCA3MzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3MTBweDsgbWFyZ2luLWxlZnQ6IDU0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls4LjFdUHJldmlldy9QbGF5YmFjazwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3OSA2NzMgTCA0NDQuNzYgNjc2LjQ0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0NTAuNzYgNjc2LjUgTCA0NDIuNzMgNjgwLjQyIEwgNDQ0Ljc2IDY3Ni40NCBMIDQ0Mi44IDY3Mi40MiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3NXB4OyBtYXJnaW4tbGVmdDogMjY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bOF1hcHBlbmRJdGVtcyh2aWRlb0l0ZW1zW10pPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

The short drama demo does not include a third\-party SDK; it provides a mock implementation to illustrate the process.

Insert the third\-party SDK and replace the imitation payment process on the [DramaEpisodeUnlockByPaymentFragment](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod-mini-drama/src/main/java/com/byteplus/vod/minidrama/scene/detail/pay/DramaEpisodeUnlockByPaymentFragment.java) page.

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
