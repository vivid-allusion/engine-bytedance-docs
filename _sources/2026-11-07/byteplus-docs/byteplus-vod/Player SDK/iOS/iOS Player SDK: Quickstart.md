---
title: "iOS Player SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk"
---

This article introduces how to integrate the iOS Player SDK into your iOS project and use the SDK to play videos.

<span id="a5138a4e"></span>
## Prerequisites


* Xcode 14.0 or higher. We recommend using the latest version.

* A device running iOS 11.0 or higher.

* Complete the following on the [SDK Management](https://console.byteplus.com/vodpaas/sdk/app/) page in the BytePlus VOD console:

   * Create an app and get the app ID and the English name of the app.

   * Purchase a license and associate it with your application.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management-overview">SDK management overview</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The testing license is valid for one month and cannot be extended. After it expires, SDK authentication will fail, and you must then apply for a new one.   </div>
   


<span id="361a8c64"></span>
## Procedure

<span id="d4aa2d92"></span>
### Step 1: Integrate the SDK

You can integrate the SDK through CocoaPods or Swift Package Manager (SPM).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The Player SDK is available in two editions: <strong>Standard</strong> and <strong>Premium</strong>. These editions offer different feature sets. Please integrate the Player SDK edition that matches your license.</div>



<Tabs>
<Tab zoneid="aCbk0TdMVL" title="Using CocoaPods">
<TabTitle>Using CocoaPods</TabTitle>

Integrate the SDK into your project using [CocoaPods](https://guides.cocoapods.org/using/getting-started.html#getting-started) as either a static or dynamic library. You need to add the required library to your project's `Podfile` and run `pod install`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-ios-player-sdk-release-notes">iOS Player SDK: Release notes</a>.</div>


<span id="6714ef08"></span>
#### (Recommend) Add the dynamic library

The following code adds the dynamic library for each edition:


* Standard:


```Ruby
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'

platform :ios, '11.0'

target 'VOLCDemo' do
  # Add the TTSDKFramework dynamic library and specify 'Player' in subspecs
  # Replace x.x.x.x with the version number
  pod 'TTSDKFramework', 'x.x.x.x-standard', :subspecs => ['Player']
 
end
```



* Premium:


```Ruby
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'

platform :ios, '11.0'

target 'VOLCDemo' do
  # Add the TTSDKFramework dynamic library and specify 'Player-SR' in subspecs.
  # If you do not need the Super Resolution feature and want to reduce your app's size, you can specify 'Player' instead.
  # Replace x.x.x.x with the version number
  pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['Player-SR']

end
```


<span id="22df4970"></span>
#### Add the static library

The code to add the static library for the different editions is as follows:


* Standard:


```Ruby
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'

platform :ios, '11.0'

target 'VOLCDemo' do
  # Add the TTSDK static library and specify 'Player' in subspecs
  # Replace x.x.x.x with the version number
  pod 'TTSDK', 'x.x.x.x-standard', :subspecs => ['Player']
 
end
```



* Premium:


```Ruby
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'

platform :ios, '11.0'

target 'VOLCDemo' do
  # Add the TTSDK static library and specify 'Player-SR' in subspecs.
  # If you do not need the Super Resolution feature and want to reduce your app's size, you can specify 'Player' instead.
  # Replace x.x.x.x with the version number
  pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['Player-SR']
 
end
```



</Tab>
<Tab zoneid="Yktq4lM1Zb" title="Using SPM">
<TabTitle>Using SPM</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">SPM packages are released on demand, and are not available for every SDK version. To integrate other versions, use CocoaPods instead.</div>


<div data-tips="true" data-tips-type="warning">Currently, the following versions of the Player SDK support integration via Swift Package Manager (SPM):</div>



* <div data-tips="true" data-tips-type="warning">Premium edition: 1.51300.3\-premium</div>


* <div data-tips="true" data-tips-type="warning">Standard edition: 1.51300.3\-standard</div>


* <div data-tips="true" data-tips-type="warning">Premium edition: 1.50.300\-premium</div>


* <div data-tips="true" data-tips-type="warning">Standard edition: 1.50.300\-standard</div>


* <div data-tips="true" data-tips-type="warning">Premium edition: 1.47.300\-premium</div>


* <div data-tips="true" data-tips-type="warning">Standard edition: 1.47.300\-standard</div>



The integration steps are as follows:


1. In your Xcode project, click the  **+**  button under the **Package Dependencies** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43f6a8ac547d47119ade6cd43aeb20c2~tplv-goo7wpa0wc-image.image) </span>

2. In the dialog box that appears, enter `git@github.com:byteplus-sdk/TTSDK_BytePlus_SPM.git` in the upper\-right corner, enter the version of the SDK you want to integrate, and click **Add Package** to add the TTSDK dependency.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Identify the edition by the suffix in the version number:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>-standard</code>: Standard   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>-premium</code>: Premium   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0453db409304d19b5970f1fe1a50ee6~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you select <strong>Exact Version</strong> as the <strong>Dependency Rule</strong>.   </div>
   

3. Select the components you need and click **Add Package** to add them to your targets.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48c06b478e4e44c09a726090ade1318a~tplv-goo7wpa0wc-image.image) </span>

   * `TTSDK_Player`: VOD player.

   * `TTSDK_Player_SR`: VOD player with Super Resolution feature.

   * `TTSDK_Player_H266`: VOD player with H.266 (VVC) decoding sup


</Tab>
</Tabs>


<span id="8713cc3e"></span>
### Step 2: Add the license

Copy the license file to your project directory and note the path to the license file, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec6ed14eb9904ed28938ea3c96fb6685~tplv-goo7wpa0wc-image.image) </span>

The license file has been associated with a Bundle ID and an App ID. If the `BundleID` and `AppID` of the license file differ from those of your project, the authentication will fail.

<span id="d217ee3b"></span>
### Step 3: Disable bitcode

To disable bitcode, go to **Project** \> **Build Settings**, search for bitcode in the search field, and set **Enable Bitcode** to **NO**, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea949a43de344e74ba24cf7cc57e064e~tplv-goo7wpa0wc-image.image) </span>

<span id="494eae9d"></span>
### Step 4: Import the header file

Import the header file based on how you have integrated the SDK:


* If you have added the dynamic library, use the following code:

   ```objectivec
   #import <TTSDKFramework/TTSDKFramework.h>
   ```
   

* If you have added the static library, use the following code:

   ```objectivec
   #import <TTSDK/TTSDKManager.h>
   #import <TTSDK/TTVideoEngineHeader.h>
   ```
   


<span id="9707a7fa"></span>
### Step 5: Initialize the SDK

Initialize the SDK in `appDelegate didFinishLaunchingWithOptions`. To configure log recording and retrieval in SDK `1.52.100.4` and later, see [Getting SDK logs](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-sdk-logs-ios). See the following sample code:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    // Initialize the SDK
    [self initTTSDK];
    
    return YES;
}


- (void)initTTSDK {
#ifdef DEBUG
    // We recommend enabling logging to get more detailed playback information
    [TTVideoEngine setLogFlag:TTVideoEngineLogFlagDefault];
#endif

    // Replace "YOUR_APP_ID" with your app ID
    NSString *appId = @"YOUR_APP_ID"; 
    // Replace "ttlicense.lic" with the name of your license file
    NSString *licenseName = @"ttlicense.lic";
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:appId licenseName:licenseName];
    
    TTSDKVodConfiguration *vodConfig = [[TTSDKVodConfiguration alloc] init];
    vodConfig.cacheMaxSize = 300 * 1024 *1024;
    configuration.vodConfiguration = vodConfig;

    [TTSDKManager startWithConfiguration:configuration]; 
}
```


When initializing the SDK, set the following parameters:


|**Name** |**Type** |**Required** |**Default value** |**Description** |
|---|---|---|---|---|
|AppID |String |Yes |None |The app ID. You can get the app ID on the [app management](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. |
|LicenseName |String |Yes |None |The name of your license file.<br><br>For more information on the license, see [License Guide](https://docs.byteplus.com/docs/byteplus-vod/docs-license-guide-ios). |
|cacheMaxSize |Int |No |100 \* 1024 \* 1024 (100 MB) |The maximum size (bytes) of the folder for caching videos. We recommend setting `cacheMaxSize` to 300 \* 1024 \* 1024 (300 MB). If the cache size exceeds this limit, a Least Recently Used (LRU) eviction policy is applied. |


<span id="23b9f2ed"></span>
### Step 6: Create a player instance

Create a player instance with the `TTVideoEngine` class, as follows:

```objectivec
self.engine = [[TTVideoEngine alloc] initWithOwnPlayer:YES];
```


<span id="eac8f415"></span>
### Step 7: Set up a view for displaying the video

The `TTVideoEngine` class provides a view for displaying the video. The following sample code shows how to add the view as a subview:

```objectivec
// Add the player view provided by TTVideoEngine as a subview
[self.view addSubview:self.engine.playerView];
```


<span id="a09b013b"></span>
### Step 8: Set the playback source

This section explains how to play videos from different sources.

<span id="4d7699f2"></span>
#### Play a video via VideoID

If you upload your videos to the BytePlus VOD service, you can play the videos with the video IDs. You need to set the `videoId` and `playAuthToken` parameters, which can be retrieved from your app server. See the following sample code:

```objectivec
// Replace "video ID" with your actual video ID
NSString *videoId = @"video ID";
// Replace "play auth token" with your actual token
NSString *playAuthToken = @"play auth token";
[self.engine setVideoID:videoId];
[self.engine setPlayAuthToken:playAuthToken];
[self.engine play];
```


<span id="f32d4d33"></span>
#### Play a video via HTTP URL

If you upload your videos to the BytePlus VOD service or third\-party storage service, you can play the videos with the HTTP URL. You need to set the `videoUrl` parameter. See the following sample code:

```objectivec
// Replace "your video URL" with an actual URL
NSString *videoUrl = @"your video URL";
NSString *cacheKey = [videoUrl md5]; 
[self.engine ls_setDirectURL:videoUrl key:cacheKey];
[self.engine play];
```


When setting the video source URL, use the following parameters:


|**Parameter** |**Type** |**Required** |**Default value** |**Description** |
|---|---|---|---|---|
|videoUrl |String |Required |None |The HTTP URL of the video |
|cacheKey |String |Required |None |The cache key. Every video has a unique cache key. It is recommended to use the MD5 of the URL as the cache key. |


<span id="b936efdf"></span>
#### Play a local video

If you play a local video, set the `localVideoPath` parameter to specify the local path. See the following sample code:

```objectivec
// Replace "file://xxx.xx" with the local path of the video
NSString *localVideoPath = @"file://xxx.xx";
[self.engine setLocalURL:localVideoPath];
[self.engine play];
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">Issue: On iOS 18, using <code>(AVURLAsset *)asset.URL.absoluteString</code> to retrieve the local video path may lead to an incorrect path, resulting in playback failure. An example of such an incorrect path is <code>file:///var/mobile/Media/DCIM/100APPLE/IMG_01.MP4#YnBsaXN0MDDRAQJfEBtSZWNvbW1lbmRlZEZvckltbWVyc2l2ZU1vZGUQAAgLKQAAAAAAAAEBAAAAAAAAAAMAAAAAAAAAAAAAAAAAAAAr</code>, which contains a fragment identifier (the part after #) that can cause playback failure.</div>


* <div data-tips="true" data-tips-type="warning">Solution: To prevent playback failure, it is recommended to use <code>(AVURLAsset *)asset.URL.relativePath</code> to obtain the accurate local path. Additionally, explore other solutions appropriate for your app to retrieve the correct path.</div>



<span id="c79d0284"></span>
### Step 9: Release the player instance

When the video ends, or the user leaves the page where the video is played, you need to stop playback and release the player instance by calling `closeAysnc`. This is to release the hardware decoder, memory, and network occupied by `TTVideoEngine` and save the device's power.

After the player instance is released, do not call any methods in the `TTVideoEngine` class. We also recommend setting `engine` to `nil`. See the following sample code:

```objectivec
// Remove the view
[self.engine.playerView removeFromSuperview];
// Release the instance
[self.engine closeAysnc];
self.engine = nil;
```
