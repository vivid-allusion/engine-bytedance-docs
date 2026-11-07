---
title: "Implementing live sport streaming for Android"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-android"
---

This guide describes how to implement a sports live\-viewing experience on Android using the BytePlus MediaLive SDK. You will learn how to initialize the live player, pull a stream over a low\-latency protocol, switch camera angles and quality, and layer interactive features on top of playback.

<span id="lsa-env"></span>
## Environmental requirements


* Android Studio Arctic Fox or higher. We recommend using the latest version of Android Studio for optimal performance.

* A physical mobile device that runs Android 6.0 or higher.

* Ensure the CPU architecture that you use is armv7 or arm64.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Emulators are not yet supported.</div>


<span id="lsa-prereq"></span>
## Prerequisites


* A valid [BytePlus account](http://console.byteplus.com/) with [BytePlus MediaLive](https://console.byteplus.com/live) activated.

* Complete the [basic setup for Live stream](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started):

   * Obtain a BytePlus MediaLive SDK license.

      * For detailed instructions on how to acquire the license, see [Accessing your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license).

      * To learn more about choosing the right license type for your needs, refer to [SDK introduction](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction).


<span id="lsa-version"></span>
## Version requirements


* To access the **live stream pulling** feature, you must use the BytePlus MediaLive SDK. Remember to choose the correct SDK on the [Client SDK components](https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination) page.


<span id="lsa-integrate"></span>
## Integrate SDKs

<span id="lsa-maven"></span>
### Step 1: Add the maven repositories

Open your project's `build.gradle` file located in the project's root directory, and add the repository locations inside the `repositories` block, as shown below:

```Groovy
allprojects { 
    repositories { 
        google() 
        mavenCentral() 
        // BytePlus SDK maven repository
        maven { url 'https://artifact.byteplus.com/repository/public/' }
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
    } 
} 
```


<span id="lsa-dep"></span>
### Step 2: Integrate the SDK

To integrate the SDK, add the following dependencies to your module's `build.gradle` file:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To get the latest version number, see <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">Client SDK components</a>.</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.50.300.1"
    // BytePlus MediaLive SDK dependencies
    implementation "com.bytedanceapi:ttsdk-ttlivepull_premium:$ttsdkVersion"
    implementation 'commons-net:commons-net:3.9.0'
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="lsa-perm"></span>
### Step 3: Declare app permissions

Declare the permissions required by SDKs in `AndroidManifest.xml`.

```XML
<uses-permission android:name="android.permission.INTERNET" /> 
```


<span id="lsa-impl"></span>
## Implementation

This section describes how the Android demo implements the Sports Live experience. The demo code is organized in the following module:

```text
solutions/media-live/live-sport
```


The module includes three user\-facing experiences:


* **Live Watch**: Plays a sports live stream with camera switching, playback settings, comments, gifts, likes, and fullscreen controls.

* **Live Comparison**: Compares latency, image enhancement, and H.265/H.264 cost\-reduction streams side by side.

* **Custom Stream URL**: Allows viewers to enter a FLV, RTM, HLS, or RTMP pull URL and preview playback.


<span id="lsa-enter"></span>
### Step 1: Enter the Sports Live scenario

The Sports Live entry is registered in the VideoOne home scene list. When viewers open the Sports Live card, the app initializes the live SDK environment and launches the Sports Live home page.

Key code:


* `app/src/main/kotlin/com/videoone/app/protocol/SceneEntry.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/videoone/app/protocol/LiveSportEntry.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/entry/LiveSportHomeActivity.kt`


<span id="lsa-init"></span>
### Step 2: Initialize TTSDK and license

Before playback starts, initialize TTSDK and load a valid license. The demo centralizes this logic in `SportLiveEnv.ensureInitialized()`, which is safe to call multiple times.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLiveEnv.kt`

* `solutions/media-live/live-sport/gradle.properties`


```Kotlin
Env.init(
    Config.Builder()
        .setApplicationContext(appContext)
        .setAppID(BuildConfig.LIVE_TTSDK_APP_ID)
        .setAppName(BuildConfig.LIVE_TTSDK_APP_NAME)
        .setAppChannel(BuildConfig.LIVE_TTSDK_APP_CHANNEL)
        .setLicenseUri(BuildConfig.LIVE_TTSDK_LICENSE_URI)
        .setLicenseCallback(SportLicenseCallback())
        .build()
)
```


<span id="lsa-channel"></span>
### Step 3: Prepare channel data

The preset sports channels are data\-driven. Each channel can declare a camera ID, pull protocol strategy, FLV stream tiers, bitrate information, low\-latency FLV preference, and ABR preference.

Key code:


* `solutions/media-live/live-sport/src/main/assets/live_sport_channels.json`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/data/SportChannelRepo.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/data/SportChannel.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportPlayerModels.kt`


`SportChannelRepo` loads the JSON channel list, and `SportChannel.toPlayerConfig()` converts the selected channel into a `SportPlayerConfig` used by the player layer.

```Kotlin
val config = channel.toPlayerConfig(
    protocol = protocolOption,
    abrAuto = abrOn,
    pinnedResolution = pinnedResolution,
    enableSR = srEnabled,
    enableSharpen = sharpenEnabled,
)
```


<span id="lsa-player"></span>
### Step 4: Create the live player

The watch page uses `SportLivePlayer` as a wrapper around `VeLivePlayer`. This wrapper handles player lifecycle, `TextureView` binding, stream data setup, low\-latency FLV, ABR, super resolution, sharpen, playback events, and playback statistics.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLivePlayer.kt`


```Kotlin
player = SportLivePlayer(this).apply {
    setListener(playerListener)
    bindTextureView(playerTexture)
}
```


When playback starts, the wrapper creates a `VideoLiveManager`, applies `VeLivePlayerConfiguration`, sets the stream data, attaches the rendering surface, and calls `play()`.

For preset sports channels, the demo uses `setPlayStreamData()` so one channel can carry multiple FLV tiers for quality selection and ABR.

For a user\-entered custom stream URL, the demo uses `setPlayUrl()` and lets the SDK detect the protocol from the URL.

<span id="lsa-start"></span>
### Step 5: Start playback

`LiveWatchActivity` prepares the initial channel during page setup and starts playback when the page enters the foreground.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`


<span id="lsa-switch"></span>
### Step 6: Switch camera, protocol, and quality

Camera switching is handled by the watch page. When the viewer selects another camera, the page prepares a new channel config and restarts playback with the selected channel.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/camera/CameraListAdapter.kt`


Playback settings are staged in the settings panel. Protocol or ABR changes rebuild playback with a new `SportPlayerConfig`. Super resolution and sharpen are runtime toggles and do not require a player rebuild.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/panel/PlayerSettingsPanel.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLivePlayer.kt`


Quality selection is based on the FLV tiers declared by the selected channel. When ABR is enabled, the player can adapt among available tiers. When ABR is disabled, the selected resolution is pinned in `SportPlayerConfig` before playback is rebuilt.

<span id="lsa-interact"></span>
### Step 7: Add fullscreen and interactive features

Interactive features are implemented as UI layers on top of live playback.

Key code:


* Comments: `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/comment`

* Gifts: `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/gift`

* Likes: `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/like`

* Fullscreen controls: `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/fullscreen`

* Watch page orchestration: `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`


In fullscreen mode, `LandscapeController` moves the existing `TextureView` into a landscape overlay. This keeps the same player instance and avoids restarting playback when entering or leaving fullscreen.

<span id="lsa-compare"></span>
### Step 8: Add comparison and custom stream experiences

The comparison page uses independent player slots to compare multiple playback experiences side by side. Only the active comparison tab keeps its players running.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/LiveCompareActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/CompareSlot.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/CompareConfig.kt`

* `solutions/media-live/live-sport/src/main/assets/live_sport_compare.json`


The custom stream page validates a viewer\-entered URL and opens the watch page in custom stream mode.

Key code:


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/LiveStreamAddressActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/CustomStreamUrlParser.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/CustomStreamSettingsBinder.kt`


<span id="lsa-code"></span>
## Sample code

Refer to the demo source code to integrate this feature into your app.


* Android: [live-sport](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/media-live/live-sport)
