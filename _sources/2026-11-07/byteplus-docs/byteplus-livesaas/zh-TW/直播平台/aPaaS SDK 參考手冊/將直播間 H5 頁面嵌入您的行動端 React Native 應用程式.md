---
title: "將直播間 H5 頁面嵌入您的行動端 React Native 應用程式"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-1-zh-TW"
---

您可以將 BytePlus Live 直播間的 H5 頁面嵌入您的行動端 React Native 應用程式，以啟用常見功能，例如子母畫面（PiP）和自動播放。本主題以範例程式為例，指導您在自己的行動端 React Native 應用程式中實現這些功能。

<span id="ce48c0dd"></span>
## 先決條件

您可以透過以下任一方式取得直播間的 H5 頁面：


* Web Viewer SDK：整合 Web Viewer SDK 2.0.16 或以上版本時，建立直播或隨選視訊（VOD）播放器實例。產生的觀看頁面（顯示單一播放器）即為直播間 H5 頁面。如需有關如何整合 Web Viewer SDK 的更多資訊，請參閱 [Integrating the Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk)。

* SaaS：本節說明如何從 BytePlus Live 控制台取得直播間 H5 頁面。

   1. 在直播間列表中，點擊某個直播間以進入。

   2. 點擊觀看頁面地址，即可開啟 SaaS 的直播間 H5 頁面。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/740730a1c5a94d358f4a0977ba0fa4f5~tplv-goo7wpa0wc-image.image) </span>


<span id="37d985ae"></span>
## 執行範例程式的環境要求


* Node.js 22 或以上版本。

* 若要在 iOS 上執行範例程式，請確保使用：

   * Xcode 16 或以上版本。

   * CocoaPods 16 或以上版本。

   * 運行 iOS 11.0 或以上版本的實體裝置或模擬器。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">要在你的 demo 或專案中實現系統 PiP 功能，請確保 iOS 作業系統版本為 14.0 或以上。      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">模擬器僅用於 UI 除錯，不保證音訊、視訊及子母畫面（PiP）等功能可正常運作。為避免出現螢幕殘影或黑邊等問題，建議使用實體裝置。      </div>
      

* 若要在 Android 上執行範例程式，請確保使用：

   * Android Studio 3.0 或以上版本。

   * 運行 Android 6.0（API 等級 23）或以上版本的實體裝置。

   * JDK 1.8.0 或以上版本。


<span id="91232540"></span>
## 專案介紹

BytePlus Live 提供開源範例專案 ByteliveWebView，展示如何將直播間 H5 頁面嵌入您的行動端 React Native 應用程式。範例專案針對 H5 頁面進行了良好適配，提供最佳化的觀看體驗及擴展功能，例如 PiP 和自動播放。

您可根據需求修改範例程式碼，以實現自訂業務邏輯。

範例專案在 iOS 和 Android 上實現以下功能：


<Tabs>
<Tab zoneid="J51jveqaN5" title="在 iOS 上">
<TabTitle>在 iOS 上</TabTitle>

* PiP（包含系統 PiP 與應用內 PiP）

* 自動播放

* 設定全螢幕圖示點擊行為

* 自訂跳轉邏輯


</Tab>
<Tab zoneid="INfoeohguY" title="在 Android 上">
<TabTitle>在 Android 上</TabTitle>

* PiP（包含系統 PiP 與應用內 PiP）

* 自動播放

* 設定全螢幕圖示點擊行為

* 當系統 PiP停用時的背景播放

* 自訂播放備用圖片

* 自訂跳轉邏輯


</Tab>
</Tabs>


<span id="6c674daa"></span>
## 執行範例程式

請完成以下步驟以執行 ByteliveWebView 範例程式：


1. 聯繫 BytePlus Live 技術支援取得 `ByteliveWebView` 套件並解壓縮。

2. 開啟終端機視窗，執行 `cd` 指令切換至 `ByteliveWebView/example` 目錄，並執行 `yarn install` 指令安裝第三方函式庫。

   ```Shell
   cd ./ByteliveWebView/example 
   yarn install
   ```
   

3. 請依下列方式在 iOS 或 Android 上執行範例程式：

   
   <Tabs>
   <Tab zoneid="A8tNj7OZKL" title="在 iOS 上">
   <TabTitle>在 iOS 上</TabTitle>
   
      1. 開啟終端視窗，執行指令 `cd` 以切換至 `ByteliveWebView/example/ios` 目錄，並執行指令 `pod install` 以安裝第三方函式庫。
   
         ```Shell
         cd ./ByteliveWebView/example/ios 
         pod install
         ```
         
   
      2. 在 Finder 中找到 `ByteliveWebViewExample.xcworkspace` 檔案，並雙擊以開啟 Xcode 專案。
   
      3. 於 **ByteliveWebViewExample** \> **Signing & Capabilities** \> **All** \> **Signing (Debug)**  區段，勾選 **Automatically manage signing** 核取方塊，然後修改 **Team** 與 **Bundle Identifier** 以符合您的應用資訊。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43171777593a408b93ccc3ea96de2ec7~tplv-goo7wpa0wc-image.image) </span>
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">若使用模擬器執行範例，請略過此步驟。      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">在 Xcode 勾選 <strong>自動管理簽名</strong>核取方塊可簡化程式碼簽名流程，節省時間並減少潛在錯誤。因此，我們建議您勾選此核取方塊。若未勾選此核取方塊，您必須修改 <strong>Provisioning Profile</strong> 和 <strong>Bundle Identifier</strong>，以符合您的應用程式資訊。      </div>
         
   
         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">在此範例中，<strong>音訊、AirPlay 與畫中畫</strong>核取方塊預設已於 <strong>Background Modes</strong>區段中勾選。因此，您無需手動勾選核取方塊即可在執行範例時啟用系統 PiP 功能。      </div>
         
   
      4. 開啟終端視窗，執行指令 `cd` 以切換至 `ByteliveWebView/example` 目錄，並執行指令 `yarn ios` 以執行範例程式。
   
         ```Shell
         cd ./ByteliveWebView/example 
         yarn ios
         ```
         
   
      5. 執行範例程式後，您可以看到以下介面。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c957b32b105d4882901598660bcd26f4~tplv-goo7wpa0wc-image.image) </span>
   
         您可以執行以下操作：
   
         * 點擊 **Go to WebView** 以加入 BytePlus Live 官方範例直播間。您也可以將預填地址替換為直播間 H5 頁面的地址，以加入特定直播間。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-1-zh-TW#ce48c0dd)。
   
         * 點擊右上角的掃描圖示並掃描 QR code，即可加入特定直播間。
   
            * 若要透過掃描 QR code 加入 SaaS 的直播間 H5 頁面，您可完成以下步驟：
   
               1. 登入 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)。
   
               2. 在直播間列表中，點擊某個直播間以進入。
   
               3. 將滑鼠移至 **View on mobile** 並掃描對應的 QR code。
   
                  <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8c5364afe25423a99fb1aacda1eb9e5~tplv-goo7wpa0wc-image.image) </span>
   
            * 若要透過掃描 QR code 加入已整合 Web Viewer SDK 的直播間 H5 頁面，請確保該頁面具有對應的 QR code。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-1-zh-TW#ce48c0dd)。
   
         * 點擊 **DEMO Config** 以進入設定頁面。您可以調整設定以查看不同的範例效果。
   
            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf7249d3606d41feb0f7cf0b70bceb16~tplv-goo7wpa0wc-image.image) </span>
   
         * 點擊 **Open in\-app Mini Window, Close Mini Window**、**Update Source URL**、**Mute** 和 **Unmute** ，以檢查 PiP 功能。
   
            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">螢幕截圖中所選的選項為預設設定。         </div>
            
   
   
   </Tab>
   <Tab zoneid="odvVwaQFIY" title="在 Android 上">
   <TabTitle>在 Android 上</TabTitle>
   
      1. 使用 Android Studio 開啟 `ByteliveWebView/example/android` 目錄下的 Android 專案檔案。
   
      2. 前往 **Settings**\> **Build, Execution, Deployment**\> **Build Tools**\> **Gradle** 頁面，在 **Gradle Projects** 區段的 **Gradle SDK** 選擇版本 11。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27d20cd1f77546d785ae215486b1ca03~tplv-goo7wpa0wc-image.image) </span>
   
      3. 將 Android 裝置連接至您的電腦。
   
      4. 開啟終端視窗，執行指令 `cd` 以切換至 `ByteliveWebView/example` 目錄，並執行指令 `yarn android` 以執行範例程式。
   
         ```Shell
         cd ./ByteliveWebView/example 
         yarn android
         ```
         
   
      5. 執行範例程式後，您可以看到以下介面。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bd0182447e34641a778b57a153e8c6d~tplv-goo7wpa0wc-image.image) </span>
   
         您可以執行以下操作：
   
         * 點擊 **GO TO WEBVIEW** 以加入 BytePlus Live 官方範例直播間。您也可以將預填地址替換為直播間 H5 頁面的地址，以加入特定直播間。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-1-zh-TW#ce48c0dd)。
   
         * 點擊 **DEMO CONFIG** 以進入設定頁面。您可以調整設定以查看不同的範例效果。
   
            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142d41f4b7144dfb8884707381ecf876~tplv-goo7wpa0wc-image.image) </span>
   
         * 點擊 **OPEN MINI WINDOW**、 **CLOSE MINI WINDOW**、**UPDATE SOURCE URL**、**MUTE** 和 **UNMUTE** ，以檢查 PiP 功能。
   
            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
            
   
            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">螢幕截圖中所選的選項為預設設定。         </div>
            
   
   
   </Tab>
   </Tabs>
   


<span id="ee84dc05"></span>
## 功能實現

請完成以下步驟，快速在您的專案中實現範例功能。

<span id="f3f2e413"></span>
### 嵌入直播間 H5 頁面的 WebView


1. 聯繫 BytePlus Live 技術支援取得 `ByteliveWebView` 套件並解壓縮至您的專案。本節將套件解壓縮至根目錄。若您有舊版本套件，請先刪除後再解壓縮目前版本。

2. 開啟專案中的 `package.json` 檔案（通常位於根目錄），並新增以下程式碼。

   ```JSON
     "dependencies": {
       ...
       "react-native-bytelive-webview": "file:./ByteliveWebView",
       ...
     }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad2f775ac3b844bbbd479b1ca45a0b95~tplv-goo7wpa0wc-image.image) </span>

3. 在專案根目錄開啟終端機視窗，執行 `yarn install` 指令，將 `ByteliveWebView` 加入 `node_modules` 依賴項。

   ```Shell
   yarn install
   ```
   

4. 檢查 `ByteliveWebView` 是否已加入 `node_modules`。如果版本號與你的`ByteliveWebView`套件一致，則依賴已成功新增。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/700080d0557548f488d86b35f9677770~tplv-goo7wpa0wc-image.image) </span>

5. 請參考`WebView.tsx`檔案（位於`ByteliveWebView/example/src/pages`目錄下）的以下程式碼，並使用`ByteliveWebViewWrapper`，將你的直播間 H5 頁面的 WebView 嵌入到行動端 React Native 應用中。

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
### 實現 PiP 功能

要實現 PiP 功能，請完成以下步驟：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在開始之前，請先熟悉以下概念：</div>



* <div data-tips="true" data-tips-type="tip"><code>react-native-webview</code>：您的 React Native 應用的 WebView</div>


* <div data-tips="true" data-tips-type="tip"><code>react-native-bytelive-webview</code>：您的直播間 H5 頁面的 WebView</div>


* <div data-tips="true" data-tips-type="tip">網頁：SaaS 的直播間 H5 頁面或與 Web Viewer SDK 整合</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49ace200e8984b63af0e1fbcac2f0773~tplv-goo7wpa0wc-image.image" width="1443px" /></div>



1. 觀眾開啟 React Native 應用，進入你的直播間 H5 頁面。

2. 當 H5 頁面加載完成後，Web 客戶端會建立播放器並將其資料傳送到原生 iOS 層，然後再轉發到`react-native-bytelive-webview`。`react-native-bytelive-webview`可以使用`onMessage`方法獲取資料。


範例程式碼如下。

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



3. 當觀眾離開直播間 H5 頁面（例如點擊直播間中的商品卡片），`react-native-bytelive-webview`會向 Web 發送`ENTER_MINI_WINDOW`事件，然後觀眾會自動進入 PiP 模式。

4. 當觀眾點擊 PiP 視窗時，`react-native-bytelive-webview`會向 Web 發送`EXIT_MINI_WINDOW`事件，然後觀眾會自動退出 PiP 模式。

   你也可以使用`react-native-bytelive-webview`實例的`closeMiniWindow`方法手動關閉 PiP 視窗。

   範例程式碼如下。

   ```TypeScript
   ByteliveWebViewLiveRoom.closeMiniWindow()
   ```
   

5. `react-native-bytelive-webview`可以使用`onMiniWindowClicked`方法，讓觀眾返回直播間 H5 頁面。

   範例程式碼如下。

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
   

6. 如需主動開啟或關閉 PiP、更新 PiP 中的 URL，以及靜音直播影片，請參考以下步驟。

   
   |**操作** |**步驟** |
   |---|---|
   |在您的頁面上顯示直播 PiP |呼叫 `openInAppMiniWindow` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.openInAppMiniWindow(url);```<br> |
   |更新 PiP 視訊中的 URL |呼叫 `updateSourceURL` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.updateSourceURL(url);```<br> |
   |關閉 PiP 視窗 |呼叫 `closeMiniWindow` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.closeMiniWindow();```<br> |
   |將視訊靜音 |呼叫 `mute` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.mute();```<br> |
   |同時顯示直播 PiP 並將 PiP 視訊靜音 |先呼叫 `openInAppMiniWindow` 方法，透過呼叫 `isMiniWindowOpening()` 檢查 PiP 模式是否啟用，然後呼叫 `mute` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.openInAppMiniWindow(url).then(async () => {```<br>```  const isOpening = await ByteliveWebViewLiveRoom.isMiniWindowOpening();```<br>```  if (isOpening) {```<br>```    ByteliveWebViewLiveRoom.mute();```<br>```  }```<br>```});```<br> |
   |取消視訊靜音 |呼叫 `unmute` 方法：<br><br>```TypeScript```<br>```ByteliveWebViewLiveRoom.unmute();```<br> |
   


<span id="5a92f0c3"></span>
### 實現全螢幕功能

要實現全螢幕功能，請完成以下步驟：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">開始前請先了解以下概念：</div>



* <div data-tips="true" data-tips-type="tip"><code>react-native-webview</code>：您的 React Native 應用程式的 WebView</div>


* <div data-tips="true" data-tips-type="tip"><code>react-native-bytelive-webview</code>：您的直播間 H5 頁面的 WebView</div>


* <div data-tips="true" data-tips-type="tip">網頁：SaaS 的直播間 H5 頁面或與 Web Viewer SDK 整合</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70c385efdea34b01bcbb196b1310a685~tplv-goo7wpa0wc-image.image) </span>


1. 當觀眾進入全螢幕模式時，Web 會向 iOS 發送`OPEN_FULLSCREEN`事件，然後再將事件傳送給`react-native-bytelive-webview`。`react-native-bytelive-webview`可以使用`onWebViewControllerDidEnterFullScreen`方法獲取 iOS 傳送的事件。

2. 當觀眾退出全螢幕模式時，Web 會向 iOS 發送`EXIT_FULLSCREEN`事件，然後再將事件傳送給`react-native-bytelive-webview`。`react-native-bytelive-webview`可以使用`onWebViewControllerDidExitFullScreen`方法獲取 iOS 傳送的事件。

   以下範例程式碼會在觀眾進入全螢幕模式時隱藏頁首，並在觀眾退出全螢幕模式時顯示頁首。

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
### 修改預設 demo 配置

如需修改 demo 程式碼中的預設配置，可呼叫`BDLRNWebViewLiveRoom.setConfig(config);`方法。範例程式碼如下：

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


詳細內容如下：


|**設定** |**參數** |**預設值** |**參數說明** |
|---|---|---|---|
|啟用系統 PiP 與應用內 PiP、僅啟用應用內 PiP，或停用 PiP。 |miniWindowType |`ByteliveWebViewMiniWindowType.inAppAndSystem` |PiP 視窗顯示模式。<br><br><br>* `ByteliveWebViewMiniWindowType.none`（停用 PiP）：觀眾無法以 PiP 模式觀看直播或點播視訊。<br><br>* `ByteliveWebViewMiniWindowType.inApp`（啟用應用內 PiP）：觀眾在開啟本應用程式其他頁面時，仍可以 PiP 模式繼續觀看直播或點播視訊。<br><br>* `ByteliveWebViewMiniWindowType.inAppAndSystem`（啟用系統 PiP 與應用內 PiP）：觀眾將應用程式移至背景或在應用程式內瀏覽其他頁面時，仍可以 PiP 模式繼續觀看直播或點播視訊。Android 用戶需在裝置上啟用浮動視窗權限才能使用 PiP 功能，iOS 用戶需在裝置的 **設定** \> **一般** \> **畫中畫** 下開啟 **自動啟動 PiP** 開關才能使用系統 PiP 功能。為提升使用者體驗，建議您選擇此值。 |
|自動播放 |autoPlay |`true` |設定觀眾進入直播間時，直播或點播視訊是否自動播放。<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |
|設定全螢幕圖示點擊行為 |fullScreenButtonType |`ByteliveWebViewFullScreenButtonType` |設定點擊全螢幕圖示時的行為，決定進入全螢幕模式時螢幕是否旋轉。<br><br><br>* `ByteliveWebViewFullScreenButtonType.doNotRotate`：螢幕不旋轉，螢幕方向維持直向。<br><br>* `ByteliveWebViewFullScreenButtonType.rotate`：螢幕依據視訊的長寬比旋轉。若為橫向視訊（寬度 \> 高度），螢幕會旋轉為橫向。若為直向視訊（寬度 < 高度），螢幕維持直向。<br><br>* `ByteliveWebViewFullScreenButtonType.forceRotate`：螢幕強制旋轉為橫向模式。 |
|停用 PiP 時的背景播放（僅限 Android） |backgroundPlayWhenNoMiniWindow |`true` |設定觀眾將本應用程式切換至背景時，停用 PiP 時直播或點播視訊是否繼續在背景播放。<br><br><br>* `true`：持續在背景播放。<br><br>* `false`：停止在背景播放。 |
|替換播放備用圖片（僅限 Android） |customWebViewPlaceHolderBitmap |`true` |設定是否以自訂圖片替換預設備用圖片。<br><br><br>* `true`：替換。<br><br>* `false`：不替換。<br><br>   播放備用圖片是指在視訊第一幀渲染前，播放器所顯示的圖片。預設備用圖片如下。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf95747ba41c46459d670681a0180238~tplv-goo7wpa0wc-image.image) </span> |
|修改應用內 PiP 視窗大小 |miniWindowLongSideSize |`180` |設定此參數以修改應用程式內 PiP 視窗的大小。iOS 系統的 PiP 視窗不受影響。單位：點。 |
