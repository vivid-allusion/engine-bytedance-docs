---
title: "将直播间 H5 页面嵌入到您的移动端 React Native 应用"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-react-zh-CN"
---

您可以将 BytePlus Live 直播间的 H5 页面嵌入到您的移动端 React Native 应用中，以实现画中画和自动播放等常见功能。本主题以一个演示项目为例，指导您在自己的移动端 React Native 应用中实现这些功能。

<span id="ce48c0dd"></span>
## 前提条件

您可以通过以下任一方式获取直播间的 H5 页面：


* Web 观播 SDK：集成 2.0.16 及以上版本的 Web 观播 SDK 时，创建直播或点播播放器实例。生成的观看页（展示单个播放器）即为直播间 H5 页面。有关如何集成 Web 观播 SDK 的更多信息，请参见[集成 Web 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN)。

* SaaS：本节介绍如何从 BytePlus Live 控制台获取直播间 H5 页面。

   1. 在直播间列表中，点击某个直播间进入。

   2. 点击观看页地址，打开 SaaS 的直播间 H5 页面。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/740730a1c5a94d358f4a0977ba0fa4f5~tplv-goo7wpa0wc-image.image) </span>


<span id="37d985ae"></span>
## 运行演示项目的环境要求


* Node.js 22 或更高版本。

* 在 iOS 上运行演示项目时，请确保使用：

   * Xcode 16 或更高版本。

   * CocoaPods 16 或更高版本。

   * 运行 iOS 12.0 或更高版本的真机或模拟器。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">要在您的演示或项目中实现系统画中画功能，请确保您的iOS系统类型版本为14.0及以上。      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">模拟器仅用于UI调试，不保证音频、视频和画中画等功能能够正常运行。为避免出现屏幕花屏或黑边等问题，建议使用实体设备。      </div>
      

* 在 Android 上运行演示项目时，请确保使用：

   * Android Studio 3.0 或更高版本。

   * 运行 Android 6.0（API level 23）或更高版本的真机。

   * JDK 1.8.0 或更高版本。


<span id="91232540"></span>
## 项目介绍

BytePlus Live 提供了开源示例项目 ByteliveWebView，演示如何将直播间 H5 页面嵌入到您的移动端 React Native 应用中。该演示项目对 H5 页面进行了良好适配，提供了优化的观看体验以及画中画和自动播放等扩展功能。

您可以根据需要修改演示项目中的代码，以实现自定义的业务逻辑。

该演示项目在 iOS 和 Android 上实现了以下功能：


<Tabs>
<Tab zoneid="EpCiF9BXvx" title="在iOS上">
<TabTitle>在iOS上</TabTitle>

* 画中画（包括系统画中画和应用内画中画）

* 自动播放

* 配置全屏图标点击行为

* 自定义跳转逻辑


</Tab>
<Tab zoneid="vyCH2WoHqT" title="在Android上">
<TabTitle>在Android上</TabTitle>

* 画中画（包括系统画中画和应用内画中画）

* 自动播放

* 配置全屏图标点击行为

* 在系统画中画未开启时后台回放

* 自定义回放占位图

* 自定义跳转逻辑


</Tab>
</Tabs>


<span id="6c674daa"></span>
## 运行演示项目

请完成以下步骤以运行 ByteliveWebView 演示项目：


1. 联系 BytePlus Live 技术支持获取`ByteliveWebView` 包并解压。

2. 打开终端窗口，运行命令 `cd` 进入 `ByteliveWebView/example` 目录，并运行命令 `yarn install` 安装第三方库。

   ```Shell
   cd ./ByteliveWebView/example 
   yarn install
   ```
   

3. 请按如下操作在 iOS 或 Android 上运行演示项目：

   
   <Tabs>
   <Tab zoneid="OKLVPMIbvw" title="在iOS上">
   <TabTitle>在iOS上</TabTitle>
   
      1. 打开终端窗口，运行命令`cd`，进入`ByteliveWebView/example/ios`目录，然后运行命令`pod install`以安装第三方库。
   
         ```Shell
         cd ./ByteliveWebView/example/ios 
         pod install
         ```
         
   
      2. 在 Finder 中找到`ByteliveWebViewExample.xcworkspace`文件，双击以打开 Xcode 项目。
   
      3. 在**ByteliveWebViewExample** \> **Signing & Capabilities** \> **All** \> **Signing (Debug)** 部分，勾选**Automatically manage signing**复选框，然后修改**Team**和**Bundle Identifier**，使其与您的应用信息一致。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43171777593a408b93ccc3ea96de2ec7~tplv-goo7wpa0wc-image.image) </span>
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">如果你使用模拟器运行演示，可以跳过此步骤。      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">在 Xcode 中勾选 <strong>Automatically manage signing</strong> 复选框可以简化代码签名流程，节省时间，并减少潜在错误。因此，我们建议你勾选该复选框。如果你未勾选该复选框，则必须修改 <strong>Provisioning Profile</strong> 和 <strong>Bundle Identifier</strong> 以匹配你的应用信息。      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">在本演示中，<strong>Audio, AirPlay, and Picture in Picture</strong> 复选框在 <strong>Background Modes</strong> 部分默认已选中。因此，你无需手动勾选该复选框即可在运行演示时实现系统 PiP 功能。      </div>
         
   
      4. 打开终端窗口，运行命令`cd`，进入`ByteliveWebView/example`目录，然后运行命令`yarn ios`以运行 demo。
   
         ```Shell
         cd ./ByteliveWebView/example 
         yarn ios
         ```
         
   
      5. 运行 demo 后，您可以看到如下界面。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c957b32b105d4882901598660bcd26f4~tplv-goo7wpa0wc-image.image) </span>
   
         您可以执行以下操作：
   
         * 点击**Go to WebView**，加入 BytePlus Live 官方 demo 直播间。您也可以将预填地址替换为直播间 H5 页面的地址，以加入指定直播间。关于如何获取直播间 H5 页面，详见[前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-react-zh-CN#ce48c0dd)。
   
         * 点击右上角的扫码图标并扫描二维码，加入指定直播间。
   
            * 要通过扫码加入 SaaS 直播间 H5 页面，您可以完成以下步骤：
   
               1. 登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。
   
               2. 在直播间列表中，点击某个直播间进入。
   
               3. 将鼠标悬停在**View on mobile**上，扫描对应二维码。
   
                  <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8c5364afe25423a99fb1aacda1eb9e5~tplv-goo7wpa0wc-image.image) </span>
   
            * 要通过扫码加入集成了 Web 观播 SDK 的直播间 H5 页面，请确保页面有对应二维码。关于如何获取直播间 H5 页面，详见[前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-react-zh-CN#ce48c0dd)。
   
         * 点击**DEMO Config**进入配置页面。您可以调整设置以查看不同的 demo 效果。
   
            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf7249d3606d41feb0f7cf0b70bceb16~tplv-goo7wpa0wc-image.image) </span>
   
         * 点击**Open in\-app Mini Window, Close Mini Window**、**Update Source URL**、**Mute**和**Unmute** 以体验画中画（PiP）功能。
   
            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">截图中选中的选项为默认设置。         </div>
            
   
   
   </Tab>
   <Tab zoneid="Izi8328y4v" title="在Android上">
   <TabTitle>在Android上</TabTitle>
   
      1. 使用 Android Studio 打开`ByteliveWebView/example/android`目录下的 Android 项目文件。
   
      2. 进入**Settings**\> **Build, Execution, Deployment**\> **Build Tools**\> **Gradle**页面，在**Gradle Projects**部分为**Gradle SDK**选择版本 11。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27d20cd1f77546d785ae215486b1ca03~tplv-goo7wpa0wc-image.image) </span>
   
      3. 将 Android 设备连接到您的电脑。
   
      4. 打开终端窗口，运行命令`cd`，进入`ByteliveWebView/example`目录，然后运行命令`yarn android`以运行 demo。
   
         ```Shell
         cd ./ByteliveWebView/example 
         yarn android
         ```
         
   
      5. 运行 demo 后，您可以看到如下界面。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bd0182447e34641a778b57a153e8c6d~tplv-goo7wpa0wc-image.image) </span>
   
         您可以执行以下操作：
   
         * 点击**GO TO WEBVIEW** ，加入 BytePlus Live 官方 demo 直播间。您也可以将预填地址替换为直播间 H5 页面的地址，以加入指定直播间。关于如何获取直播间 H5 页面，详见[前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-react-zh-CN#ce48c0dd)。
   
         * 点击**DEMO CONFIG**进入配置页面。您可以调整设置以查看不同的 demo 效果。
   
            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142d41f4b7144dfb8884707381ecf876~tplv-goo7wpa0wc-image.image) </span>
   
         * 点击**OPEN MINI WINDOW**、 **CLOSE MINI WINDOW**、**UPDATE SOURCE URL**、**MUTE**和**UNMUTE** 以体验画中画（PiP）功能。
   
            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">截图中选中的选项为默认设置。         </div>
            
   
   
   </Tab>
   </Tabs>
   


<span id="ee84dc05"></span>
## 功能实现

请完成以下步骤，将演示项目的功能快速集成到您的项目中。

<span id="f3f2e413"></span>
### 嵌入您的直播间 H5 页面的 WebView


1. 联系 BytePlus Live 技术支持获取`ByteliveWebView` 包，并解压到您的项目中。本节以将包解压到项目根目录为例。如已存在旧版本包，请先删除后再解压当前版本。

2. 打开项目中的 `package.json` 文件（通常位于根目录），并添加如下代码。

   ```JSON
     "dependencies": {
       ...
       "react-native-bytelive-webview": "file:./ByteliveWebView",
       ...
     }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad2f775ac3b844bbbd479b1ca45a0b95~tplv-goo7wpa0wc-image.image) </span>

3. 在项目根目录下打开终端窗口，运行命令 `yarn install`，将 `ByteliveWebView` 作为依赖添加到 `node_modules`。

   ```Shell
   yarn install
   ```
   

4. 检查 `ByteliveWebView` 是否已添加到 `node_modules`。如果版本号与您的`ByteliveWebView`包一致，则依赖已成功添加。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/700080d0557548f488d86b35f9677770~tplv-goo7wpa0wc-image.image) </span>

5. 请参考`WebView.tsx`文件（位于`ByteliveWebView/example/src/pages`目录）中的以下代码，并使用`ByteliveWebViewWrapper`将您的直播间H5页面的WebView嵌入到移动端React Native应用中。

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
### 实现画中画功能

要实现画中画功能，请完成以下步骤：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在开始之前，请先了解以下概念：</div>



* <div data-tips="true" data-tips-type="tip"><code>react-native-webview</code>：您的 React Native 应用中的 WebView</div>


* <div data-tips="true" data-tips-type="tip"><code>react-native-bytelive-webview</code>：您的直播间 H5 页面中的 WebView</div>


* <div data-tips="true" data-tips-type="tip">Web：SaaS 直播间 H5 页面或集成 Web 观播 SDK 的页面</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49ace200e8984b63af0e1fbcac2f0773~tplv-goo7wpa0wc-image.image" width="1443px" /></div>



1. 观众打开React Native应用，进入您的直播间H5页面。

2. 当H5页面加载完成后，Web客户端会创建播放器并将其数据发送到原生iOS层，随后数据会转发至`react-native-bytelive-webview`。`react-native-bytelive-webview`可通过`onMessage`方法获取数据。


示例代码如下。

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



3. 当观众离开直播间H5页面（例如点击直播间中的商品卡片），`react-native-bytelive-webview`会向Web端发送`ENTER_MINI_WINDOW`事件，观众会自动进入画中画模式。

4. 当观众点击画中画窗口时，`react-native-bytelive-webview`会向Web端发送`EXIT_MINI_WINDOW`事件，观众会自动退出画中画模式。

   您也可以通过`react-native-bytelive-webview`实例的`closeMiniWindow`方法手动关闭画中画窗口。

   示例代码如下。

   ```TypeScript
   ByteliveWebViewLiveRoom.closeMiniWindow()
   ```
   

5. `react-native-bytelive-webview`可通过`onMiniWindowClicked`方法使观众返回直播间H5页面。

   示例代码如下。

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
   

6. 要主动开启或关闭画中画、更新画中画中的URL并静音直播视频，请参考以下步骤。

   
   |**操作** |**步骤** |
   |---|---|
   |在你的页面上显示直播画中画 |调用 `openInAppMiniWindow` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.openInAppMiniWindow(url);```<br> |
   |更新画中画视频中的 URL |调用 `updateSourceURL` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.updateSourceURL(url);```<br> |
   |关闭画中画窗口 |调用 `closeMiniWindow` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.closeMiniWindow();```<br> |
   |静音视频 |调用 `mute` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.mute();```<br> |
   |同时显示直播画中画并将画中画视频静音 |先调用 `openInAppMiniWindow` 方法，通过调用 `isMiniWindowOpening()` 检查画中画模式是否已开启，然后调用 `mute` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.openInAppMiniWindow(url).then(async () => {```<br>```  const isOpening = await ByteliveWebViewLiveRoom.isMiniWindowOpening();```<br>```  if (isOpening) {```<br>```    ByteliveWebViewLiveRoom.mute();```<br>```  }```<br>```});```<br> |
   |取消视频静音 |调用 `unmute` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.unmute();```<br> |
   


<span id="5a92f0c3"></span>
### 实现全屏功能

要实现全屏功能，请完成以下步骤：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在开始之前，请了解以下概念：</div>



* <div data-tips="true" data-tips-type="tip"><code>react-native-webview</code>：你的 React Native 应用的 WebView</div>


* <div data-tips="true" data-tips-type="tip"><code>react-native-bytelive-webview</code>：你的直播间 H5 页面的 WebView</div>


* <div data-tips="true" data-tips-type="tip">Web：SaaS 直播间 H5 页面或集成 Web 观播 SDK 的页面</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70c385efdea34b01bcbb196b1310a685~tplv-goo7wpa0wc-image.image) </span>


1. 当观众进入全屏模式时，Web端会向iOS发送`OPEN_FULLSCREEN`事件，随后iOS会向`react-native-bytelive-webview`发送事件。`react-native-bytelive-webview`可通过`onWebViewControllerDidEnterFullScreen`方法获取iOS发送的事件。

2. 当观众退出全屏模式时，Web端会向iOS发送`EXIT_FULLSCREEN`事件，随后iOS会向`react-native-bytelive-webview`发送事件。`react-native-bytelive-webview`可通过`onWebViewControllerDidExitFullScreen`方法获取iOS发送的事件。

   以下示例代码在观众进入全屏模式时隐藏页面头部，在观众退出全屏模式时显示页面头部。

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
### 修改默认演示配置

要修改演示代码中的默认配置，可调用`BDLRNWebViewLiveRoom.setConfig(config);`方法。示例代码如下：

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


详细信息如下：


|**配置** |**参数** |**默认值** |**参数接口行为** |
|---|---|---|---|
|开启系统画中画和应用内画中画、仅开启应用内画中画或关闭画中画。 |miniWindowType |`ByteliveWebViewMiniWindowType.inAppAndSystem` |画中画窗口显示模式。<br><br><br>* `ByteliveWebViewMiniWindowType.none`（未开启画中画）：观众无法在画中画模式下观看直播或回放视频。<br><br>* `ByteliveWebViewMiniWindowType.inApp`（已开启应用内画中画）：观众在当前应用打开其他页面时，仍可在画中画模式下继续观看直播或回放视频。<br><br>* `ByteliveWebViewMiniWindowType.inAppAndSystem`（已开启系统画中画和应用内画中画）：观众将应用切换到后台或在应用内跳转其他页面时，仍可在画中画模式下继续观看直播或回放视频。Android 用户需在设备上开启悬浮窗权限以使用画中画功能，iOS 用户需在设备的 **设置** \> **通用** \> **画中画** 下打开 **自动启动画中画** 开关以使用系统画中画功能。为获得更好的用户体验，建议选择该值。 |
|自动播放 |autoPlay |`true` |设置观众进入直播间时，直播或回放视频是否自动播放。<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |
|配置全屏图标点击行为 |fullScreenButtonType |`ByteliveWebViewFullScreenButtonType` |设置点击全屏图标时的行为，决定进入全屏模式时屏幕是否旋转。<br><br><br>* `ByteliveWebViewFullScreenButtonType.doNotRotate`：屏幕不旋转，屏幕方向保持竖屏。<br><br>* `ByteliveWebViewFullScreenButtonType.rotate`：屏幕根据视频长宽比旋转。对于横屏视频（宽 \> 高），屏幕旋转为横屏模式。对于竖屏视频（宽 < 高），屏幕保持竖屏方向。<br><br>* `ByteliveWebViewFullScreenButtonType.forceRotate`：屏幕强制旋转为横屏模式。 |
|画中画未开启时后台回放（仅限 Android） |backgroundPlayWhenNoMiniWindow |`true` |设置观众在画中画未开启时，将当前应用切换到后台后，直播或回放视频是否继续后台播放。<br><br><br>* `true`：后台继续播放。<br><br>* `false`：后台停止播放。 |
|替换回放占位图（仅限 Android） |customWebViewPlaceHolderBitmap |`true` |设置是否用自定义图片替换默认回放占位图。<br><br><br>* `true`：替换。<br><br>* `false`：不替换。<br><br>   回放占位图是在视频第一帧渲染前播放器显示的图片。默认回放占位图如下。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf95747ba41c46459d670681a0180238~tplv-goo7wpa0wc-image.image) </span> |
|修改应用内画中画窗口大小 |miniWindowLongSideSize |`180` |配置此参数以修改应用内 PiP 窗口的大小。iOS 系统的 PiP 窗口不受影响。单位：点。 |
