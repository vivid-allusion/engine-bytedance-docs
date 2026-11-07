---
title: "Embedding the live room H5 page into your mobile React Native app"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/react-native-demo"
---

You can embed the H5 page of a BytePlus Live live room into your mobile React Native app to enable common features such as picture\-in\-picture (PiP) and autoplay. This topic uses a demo as an example to guide you through implementing these features in your own mobile React Native app.

<span id="ce48c0dd"></span>
## Prerequisites

Get the H5 page of a live room through any of the following methods:


* Web Viewer SDK: When integrating version 2.0.16 or above of the Web Viewer SDK, create a live or Video on Demand (VOD) player instance. The resulting viewing page, which displays a single player, is the live room H5 page. For more information on how to integrate the Web Viewer SDK, see [Integrating the Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk).

* SaaS: This section explains how to get the live room H5 page from the BytePlus Live console.

   1. In the live room list, click a live room to enter it.

   2. Click the viewing page address to open the live room H5 page of SaaS.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/740730a1c5a94d358f4a0977ba0fa4f5~tplv-goo7wpa0wc-image.image) </span>


<span id="37d985ae"></span>
## Environmental requirements for running the demo


* Node.js 22 or above.

* To run the demo on iOS, make sure that you use:

   * Xcode 16 or above.

   * CocoaPods 16 or above.

   * Real devices or simulators running iOS 12.0 or above.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To implement the system PiP feature in your demo or project, make sure that your iOS operating system version is 14.0 or above.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The simulator is for UI debugging only and does not guarantee that features such as audio, video, and picture\-in\-picture (PiP) will function correctly. To avoid issues like screen artifacts or black borders, we recommend that you use a physical device.      </div>
      

* To run the demo on Android, make sure that you use:

   * Android Studio 3.0 or above.

   * Real devices running Android 6.0 (API level 23) or above.

   * JDK 1.8.0 or above.


<span id="91232540"></span>
## Project introduction

BytePlus Live provides an open\-source example project ByteliveWebView, demonstrating how to embed the live room H5 page into your mobile React Native app. The demo project is well\-adapted for the H5 page, offering an optimized viewing experience and extended features like PiP and autoplay.

You can modify the code in the demo as needed to implement your custom business logic.

The demo project implements the following features on iOS and Android:


<Tabs>
<Tab zoneid="zdUYMrp8Ut" title="On iOS">
<TabTitle>On iOS</TabTitle>

* PiP (including system PiP and in\-app PiP)

* Autoplay

* Configuring fullscreen icon tap behavior

* Customizing redirection logic


</Tab>
<Tab zoneid="j3DVfvLg4Y" title="On Android">
<TabTitle>On Android</TabTitle>

* PiP (including system PiP and in\-app PiP)

* Autoplay

* Configuring fullscreen icon tap behavior

* Background playback while system PiP is disabled

* Customizing fallback image for playback

* Customizing redirection logic


</Tab>
</Tabs>


<span id="6c674daa"></span>
## Running the demo

Complete the following steps to run the ByteliveWebView demo:


1. Contact BytePlus Live technical support to get the `ByteliveWebView` package and unzip it.

2. Open a terminal window, run the command `cd` to navigate to the `ByteliveWebView/example` directory, and run the command `yarn install` to install third\-party libraries.

   ```Shell
   cd ./ByteliveWebView/example 
   yarn install
   ```
   

3. Do the following to run the demo on iOS or Android:

   
   <Tabs>
   <Tab zoneid="kDQuh6DwWn" title="On iOS">
   <TabTitle>On iOS</TabTitle>
   
      1. Open a terminal window, run the command `cd` to navigate to the `ByteliveWebView/example/ios` directory, and run the command `pod install` to install third\-party libraries.
   
         ```Shell
         cd ./ByteliveWebView/example/ios 
         pod install
         ```
         
   
      2. Find the `ByteliveWebViewExample.xcworkspace` file in Finder and double\-click to open the Xcode project.
   
      3. In the **ByteliveWebViewExample** \> **Signing & Capabilities** \> **All** \> **Signing (Debug)**  section, select the **Automatically** **manage signing** checkbox and then modify the **Team** and **Bundle Identifier** to match your app information.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43171777593a408b93ccc3ea96de2ec7~tplv-goo7wpa0wc-image.image) </span>
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Skip this step if you use a simulator to run the demo.      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Selecting the <strong>Automatically manage signing</strong> checkbox in Xcode simplifies the code signing process, saves time, and reduces potential errors. Therefore, we recommend that you select the checkbox. If you do not select the checkbox, you must modify the <strong>Provisioning Profile</strong> and <strong>Bundle Identifier</strong> to match your app information.      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In this demo, the <strong>Audio, AirPlay, and Picture in Picture</strong> checkbox is selected in the <strong>Background Modes</strong> section by default. Therefore, you do not need to select the checkbox manually to implement the system PiP feature when running the demo.      </div>
         
   
      4. Open a terminal window, run the command `cd` to navigate to the `ByteliveWebView/example` directory, and run the command `yarn ios` to run the demo.
   
         ```Shell
         cd ./ByteliveWebView/example 
         yarn ios
         ```
         
   
      5. After running the demo, you can view the following interface.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c957b32b105d4882901598660bcd26f4~tplv-goo7wpa0wc-image.image) </span>
   
         You can do the following:
   
         * Tap **Go to WebView** to join the official demo live room of BytePlus Live. You can also replace the pre\-filled address with the address of the live room H5 page to join the specific live room. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/react-native-demo#ce48c0dd).
   
         * Tap the scan icon in the upper\-right corner and scan the QR code to join the specific live room.
   
            * To join the live room H5 page of SaaS by scanning the QR code, you can complete the following steps:
   
               1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).
   
               2. In the live room list, click a live room to enter it.
   
               3. Move your pointer over **View on mobile** and scan the corresponding QR code.
   
                  <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8c5364afe25423a99fb1aacda1eb9e5~tplv-goo7wpa0wc-image.image) </span>
   
            * To join the live room H5 page integrated with the Web Viewer SDK by scanning the QR code, make sure the page has the corresponding QR code. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/react-native-demo#ce48c0dd).
   
         * Tap **DEMO Config** to enter the configuration page. You can adjust the settings to see different demo effects.
   
            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf7249d3606d41feb0f7cf0b70bceb16~tplv-goo7wpa0wc-image.image) </span>
   
         * Tap **Open in\-app Mini Window, Close Mini Window**, **Update Source URL**, **Mute**, and **Unmute** to check the PiP feature.
   
            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The options selected in the screenshot are the default settings.         </div>
            
   
   
   </Tab>
   <Tab zoneid="Pf4r9DjqzU" title="On Android">
   <TabTitle>On Android</TabTitle>
   
      1. Use Android Studio to open the Android project file under the `ByteliveWebView/example/android` directory.
   
      2. Navigate to the **Settings**\> **Build, Execution, Deployment**\> **Build Tools**\> **Gradle** page, select version 11 for the **Gradle SDK** in the **Gradle Projects** section.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27d20cd1f77546d785ae215486b1ca03~tplv-goo7wpa0wc-image.image) </span>
   
      3. Connect an Android device to your PC.
   
      4. Open a terminal window, run the command `cd` to navigate to the `ByteliveWebView/example` directory, and run the command `yarn android` to run the demo.
   
         ```Shell
         cd ./ByteliveWebView/example 
         yarn android
         ```
         
   
      5. After running the demo, you can view the following interface.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bd0182447e34641a778b57a153e8c6d~tplv-goo7wpa0wc-image.image) </span>
   
         You can do the following:
   
         * Tap **GO TO WEBVIEW** to join the official demo live room of BytePlus Live. You can also replace the pre\-filled address with the address of the live room H5 page to join the specific live room. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/react-native-demo#ce48c0dd).
   
         * Tap **DEMO CONFIG** to enter the configuration page. You can adjust the settings to see different demo effects.
   
            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142d41f4b7144dfb8884707381ecf876~tplv-goo7wpa0wc-image.image) </span>
   
         * Tap **OPEN MINI WINDOW**, **CLOSE MINI WINDOW**, **UPDATE SOURCE URL**, **MUTE** and **UNMUTE** to check the PiP feature.
   
            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The options selected in the screenshot are the default settings.         </div>
            
   
   
   </Tab>
   </Tabs>
   


<span id="ee84dc05"></span>
## Feature implementation

Complete the following steps to quickly implement the demo features in your project.

<span id="f3f2e413"></span>
### Embed the WebView of your live room H5 page


1. Contact BytePlus Live technical support to get the `ByteliveWebView` package and unzip it to your project. In this section, unzip the package to the root directory. If you have an older version of the package, delete it before unzipping the current version.

2. Open the `package.json` file in your project, typically located in your root directory, and add the following code.

   ```JSON
     "dependencies": {
       ...
       "react-native-bytelive-webview": "file:./ByteliveWebView",
       ...
     }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad2f775ac3b844bbbd479b1ca45a0b95~tplv-goo7wpa0wc-image.image) </span>

3. Open a terminal window in the root directory of your project and run the command `yarn install` to add `ByteliveWebView` as a dependency to `node_modules`.

   ```Shell
   yarn install
   ```
   

4. Check if `ByteliveWebView` is added to `node_modules`. If the version number matches that of your `ByteliveWebView` package, the dependency is successfully added.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/700080d0557548f488d86b35f9677770~tplv-goo7wpa0wc-image.image) </span>

5. Refer to the following code in the `WebView.tsx` file under the `ByteliveWebView/example/src/pages` directory, and use `ByteliveWebViewWrapper` to embed the WebView of your live room H5 page into your mobile React Native app.

   ```TypeScript
   import { useRef } from 'react';
   import { View, StyleSheet } from 'react-native';
   import {
     ByteliveWebViewWrapper,
     ByteliveWebViewWrapperRef,
   } from 'react-native-bytelive-webview';
   import type { WebViewScreenProps } from '../types';
   
   const DEFAULT_URL = 'https://live.byteplus.com/demo/sdk/index.mobile.all-portrait.html';
   
   export function WebViewScreen({ navigation, route }: WebViewScreenProps) {
     const { url = DEFAULT_URL } = route?.params || {};
     const liveWebView = useRef<ByteliveWebViewWrapperRef>(null);
   
     return (
         <View style={styles.container}>
           {/* @ts-ignore */}
           <ByteliveWebViewWrapper
             style={styles.webview}
             sourceURL={url}
             ref={liveWebView}
             onWebViewControllerDidEnterFullScreen={() => {
               navigation.setOptions({
                 headerShown: false,
               });
             }}
             onWebViewControllerDidExitFullScreen={() => {
               navigation.setOptions({
                 headerShown: true,
               });
             }}
             onMiniWindowClicked={() => {
               navigation.navigate('WebView', { url });
               liveWebView.current?.injectJavaScript?.('console.log(onMiniWindowClicked)');
             }}
             onMessage={(event) => {
               console.log(event);
             }}
             onURLRequestClicked={(event) => {
               navigation.navigate('CardDetail', { url: event.result });
             }}
           />
         </View>
     );
   }
   
   const styles = StyleSheet.create({
     safeArea: {
       flex: 1,
       backgroundColor: '#fff',
     },
     container: {
       flex: 1,
       alignItems: 'center',
       alignContent: 'center',
     },
     webview: {
       width: '100%',
       height: '100%',
     },
   });
   ```
   


<span id="faf99d0f"></span>
### Implement the PiP feature

To implement the PiP feature, complete the following steps:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you begin, familiarize yourself with the following concepts:</div>



* <div data-tips="true" data-tips-type="tip"><code>react-native-webview</code>: WebView of your React Native app</div>


* <div data-tips="true" data-tips-type="tip"><code>react-native-bytelive-webview</code>: WebView of your live room H5 page</div>


* <div data-tips="true" data-tips-type="tip">Web: Live room H5 page of SaaS or integrated with the Web Viewer SDK</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49ace200e8984b63af0e1fbcac2f0773~tplv-goo7wpa0wc-image.image" width="1443px" /></div>



1. A viewer opens the React Native app to go to your live room H5 page.

2. Once the H5 page finishes loading, the web client creates a player and sends its data to the native iOS layer, which then forwards the data to `react-native-bytelive-webview`. `react-native-bytelive-webview` can use the `onMessage` method to get the data.

   The sample code is as follows.

   ```JavaScript
   const liveWebView = useRef<ByteliveWebViewWrapperRef>(null);
   
   <ByteliveWebViewWrapper
     style={styles.webview}
     sourceURL={url}
     ref={liveWebView}
     onMessage={(event) => {
       console.log(event);
     }}
   />
   ```
   

3. When a viewer leaves the live room H5 page, such as by tapping the product card in your live room, `react-native-bytelive-webview` sends the `ENTER_MINI_WINDOW` event to the Web, and then the viewer enters PiP mode automatically.

4. When a viewer taps the PiP window, `react-native-bytelive-webview` sends the `EXIT_MINI_WINDOW` event to the Web, and then the viewer exits PiP mode automatically.

   You can also use the `closeMiniWindow` method of the `react-native-bytelive-webview` instance to close the PiP window manually.

   The sample code is as follows.

   ```TypeScript
   ByteliveWebViewLiveRoom.closeMiniWindow()
   ```
   

5. `react-native-bytelive-webview` can use the `onMiniWindowClicked` method to allow the viewer to return to the live room H5 page.

   The sample code is as follows.

   ```JavaScript
   ByteliveWebViewLiveRoom.setCallbackProps({
     onMiniWindowClicked: () => {
       console.log('onMiniWindowClicked');
       navigation.navigate(
         'WebView',
         { url },
         {
           pop: true,
         }
       );
     },
   ...
   });
   ```
   

6. To actively enable or disable PiP, update the URLs in PiP, and mute the live video, refer to the following steps.

   
   |**Action** |**Steps** |
   |---|---|
   |Display a live PiP on your page |Call the `openInAppMiniWindow` method:<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.openInAppMiniWindow(url);```<br> |
   |Update the URLs in the PiP video |Call the `updateSourceURL` method:<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.updateSourceURL(url);```<br> |
   |Close the PiP window |Call the `closeMiniWindow` method:<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.closeMiniWindow();```<br> |
   |Mute the video |Call the `mute` method:<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.mute();```<br> |
   |Display a live PiP and mute the PiP video at the same time |Call the `openInAppMiniWindow` method first, check if the PiP mode is enabled by calling `isMiniWindowOpening()` and then call the `mute` method:<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.openInAppMiniWindow(url).then(async () => {```<br>```  const isOpening = await ByteliveWebViewLiveRoom.isMiniWindowOpening();```<br>```  if (isOpening) {```<br>```    ByteliveWebViewLiveRoom.mute();```<br>```  }```<br>```});```<br> |
   |Unmute the video |Call the `unmute` method:<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.unmute();```<br> |
   


<span id="5a92f0c3"></span>
### Implement the fullscreen feature

To implement the fullscreen feature, complete the following steps:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Know the following concepts before you begin:</div>



* <div data-tips="true" data-tips-type="tip"><code>react-native-webview</code>: WebView of your React Native app</div>


* <div data-tips="true" data-tips-type="tip"><code>react-native-bytelive-webview</code>: WebView of your live room H5 page</div>


* <div data-tips="true" data-tips-type="tip">Web: Live room H5 page of SaaS or integrated with the Web Viewer SDK</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70c385efdea34b01bcbb196b1310a685~tplv-goo7wpa0wc-image.image) </span>


1. When a viewer enters fullscreen mode, the Web sends the `OPEN_FULLSCREEN` event to iOS, which then sends an event to `react-native-bytelive-webview`. `react-native-bytelive-webview` can use the `onWebViewControllerDidEnterFullScreen` method to get the event sent by iOS.

2. When a viewer exits fullscreen mode, the Web sends the `EXIT_FULLSCREEN` event to iOS, which then sends an event to `react-native-bytelive-webview`. `react-native-bytelive-webview` can use the `onWebViewControllerDidExitFullScreen` method to get the event sent by iOS.

   The following sample code hides the page header when viewers enter fullscreen mode and displays the page header when viewers exit fullscreen mode.

   ```JavaScript
   <ByteliveWebViewWrapper
     style={styles.webview}
     sourceURL={url}
     ref={liveWebView}
     onWebViewControllerDidEnterFullScreen={() => {
       navigation.setOptions({
         headerShown: false,
       });
       liveWebView.current?.injectJavaScript?.('console.log(123123)');
     }}
     onWebViewControllerDidExitFullScreen={() => {
       navigation.setOptions({
         headerShown: true,
       });
     }}
   />
   ```
   


<span id="359d81fc"></span>
### Modify the default demo configuration

To modify the default configuration in the demo code, you can call the `BDLRNWebViewLiveRoom.setConfig(config);` method. The sample code is as follows:

```TypeScript
const config = {
  miniWindowType: ByteliveWebViewMiniWindowType.inAppAndSystem,
  autoPlay: true,
  fullScreenButtonType: ByteliveWebViewFullScreenButtonType.rotate,
  backgroundPlayWhenNoMiniWindow: false,
  customWebViewPlaceHolderBitmap: false,
  miniWindowLongSideSize: 180,
};
BDLRNWebViewLiveRoom.setConfig(config);
```


The details are as follows:


|**Configuration** |**Parameter** |**Default value** |**Parameter description** |
|---|---|---|---|
|Enable system PiP and in\-app PiP, enable in\-app PiP, or disable PiP. |miniWindowType |`ByteliveWebViewMiniWindowType.inAppAndSystem` |PiP window display mode.<br><br><br>* `ByteliveWebViewMiniWindowType.none` (Disable PiP): Viewers cannot watch live or VOD videos in PiP mode.<br><br>* `ByteliveWebViewMiniWindowType.inApp` (Enable in\-app PiP): Viewers can continue watching live or VOD videos in PiP mode when opening other pages in the current app.<br><br>* `ByteliveWebViewMiniWindowType.inAppAndSystem` (Enable system PiP and in\-app PiP): Viewers can continue watching live or VOD videos in PiP mode when they move the app to the background or navigate to other pages within the app. Android users need to enable the floating window permission on their devices to use the PiP feature, while iOS users need to turn on the **Start PiP Automatically** switch under **Settings** \> **General** \> **Picture in Picture** on their devices to use the system PiP feature. For a better user experience, we recommend that you select this value. |
|Autoplay |autoPlay |`true` |Set whether live or VOD videos play automatically when viewers join the live room.<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |
|Configuring fullscreen icon tap behavior |fullScreenButtonType |`ByteliveWebViewFullScreenButtonType` |Sets the behavior when the fullscreen icon is tapped, determining if the screen rotates upon entering fullscreen mode.<br><br><br>* `ByteliveWebViewFullScreenButtonType.doNotRotate`: The screen does not rotate and the screen orientation remains portrait.<br><br>* `ByteliveWebViewFullScreenButtonType.rotate`: The screen rotates based on the video's aspect ratio. For landscape videos (width \> height), the screen rotates to landscape. For portrait videos (width < height), the screen remains in portrait orientation.<br><br>* `ByteliveWebViewFullScreenButtonType.forceRotate`: The screen is forced to rotate to landscape mode. |
|Background playback while PiP is disabled (for Android only) |backgroundPlayWhenNoMiniWindow |`true` |Set whether the live or VOD videos will continue playing in the background when viewers switch the current app to the background while PiP is disabled.<br><br><br>* `true`: Continue playing in the background.<br><br>* `false`: Stop playing in the background. |
|Replacing fallback image for playback (for Android only) |customWebViewPlaceHolderBitmap |`true` |Set whether to replace the default fallback image with a custom image.<br><br><br>* `true`: Replace.<br><br>* `false`: Do not replace.<br><br>   The fallback image for playback is the image displayed in the player before the first frame of the video is rendered. The default fallback image is as follows.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf95747ba41c46459d670681a0180238~tplv-goo7wpa0wc-image.image) </span> |
|Modify the size of the in\-app PiP window |miniWindowLongSideSize |`180` |Configure this parameter to modify the size of the in\-app PiP window. System PiP windows on iOS are not affected. Unit: points. |
