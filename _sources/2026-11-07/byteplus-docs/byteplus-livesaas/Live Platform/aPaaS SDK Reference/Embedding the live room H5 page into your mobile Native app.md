---
title: "Embedding the live room H5 page into your mobile Native app"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/native-app-demo"
---

You can embed the H5 page of a BytePlus Live live room into your mobile Native app to enable common features such as picture\-in\-picture (PiP) and autoplay. This topic uses iOS and Android app demos as examples to introduce how to implement these features.

<span id="259416b3"></span>
## Prerequisites

Get the H5 page of a live room through any of the following methods:


* Web Viewer SDK: When integrating version 2.0.16 or above of the Web Viewer SDK, create a live or Video on Demand (VOD) player instance. The viewing page integrated with the Web Viewer SDK is the live room H5 page, displaying only one player. For more information on how to integrate the Web Viewer SDK, see [Integrating the Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk).

* SaaS: Here, use the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) as an example to introduce how to get the SaaS live room H5 page.

   1. In the live room list, click to enter a live room.

   2. Click the viewing page address to open the SaaS live room H5 page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cb3dbd6a900415191cc07edc9f8a9e3~tplv-goo7wpa0wc-image.image) </span>


<span id="04b7fe45"></span>
## Environmental requirements for running the demo


<Tabs>
<Tab zoneid="EbnK284v0w" title="iOS">
<TabTitle>iOS</TabTitle>

* Real devices or simulators running iOS 12.0 or above.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To implement the system PiP feature in your demo or project, make sure that your iOS operating system version is 14.0 or above.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Simulators are only intended for interface debugging and do not guarantee the normal functioning of features such as audio, video, and picture\-in\-picture (PiP). To avoid issues like screen artifacts or black borders, we recommend that you use a physical device.   </div>
   

* Xcode 16 or above.

* CocoaPods 16 or above.


</Tab>
<Tab zoneid="bqkOjqsUsb" title="Android">
<TabTitle>Android</TabTitle>

* Android Studio 3.0 or above.

* Real devices running Android 5.0 (API level 21) or above.

* JDK 1.7.0 or above.


</Tab>
</Tabs>


<span id="f34e455d"></span>
## Project introduction

BytePlus Live provides an open\-source example project, `BDLWebDemo`, which demonstrates how to embed the live room H5 page into your mobile Native app. The demo project has well\-adapted the H5 page, optimized the viewing experience, and provides extended features such as PiP and autoplay.

You can modify the code in the demo as needed to achieve customized business logic.

The demo project implements the following features:


<Tabs>
<Tab zoneid="l6L8VOMI7e" title="iOS">
<TabTitle>iOS</TabTitle>

* PiP, including system PiP and in\-app PiP

* Autoplay

* Configure fullscreen icon tap behavior

* Customize the redirection logic


</Tab>
<Tab zoneid="Up78M8sVQp" title="Android">
<TabTitle>Android</TabTitle>

* PiP, including system PiP and in\-app PiP

* Autoplay

* Configure fullscreen icon tap behavior

* Background playback while system PiP is disabled

* Customize the fallback image for playback

* Customize the redirection logic


</Tab>
</Tabs>


<span id="596b1370"></span>
## Running the demo


<Tabs>
<Tab zoneid="dQhSNfFhwo" title="iOS">
<TabTitle>iOS</TabTitle>

Complete the following steps to run the demo of the iOS app:


1. Contact BytePlus Live technical support to get the `BDLWebDemo` package and unzip it.

2. Open a terminal window, run the command `cd` to navigate to the `BDLWebDemo/iOS/Example` directory, and run the command `pod install` to install third\-party libraries.

   ```Shell
   cd ./BDLWebDemo/iOS/Example
   pod install
   ```
   

3. Find the **BDLWebDemo.xcworkspace** file in Finder and double\-click to open the Xcode project.

4. In the **BDLWebDemo** \> **Signing & Capabilities** \> **All** \> **Signing (Debug)**  section, select the **Automatically manage signing** checkbox and then modify the **Team** and **Bundle Identifier** to match your app information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79f580df703c425fb677b1253acd837b~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are running the demo on a simulator, you can skip this step.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Selecting the <strong>Automatically manage signing</strong> checkbox in Xcode simplifies the code signing process, saves time, and reduces potential errors. Therefore, we recommend that you select the checkbox. If you do not select the checkbox, you must modify the <strong>Provisioning Profile</strong> and <strong>Bundle Identifier</strong> to match your app information.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the demo, the <strong>Audio, AirPlay, and Picture in Picture</strong> checkbox in the <strong>Background Modes</strong> section is selected by default, so you do not need to select the checkbox manually when running the demo. However, when implementing the system PiP feature of the demo in your project, you need to select the checkbox manually. For detailed steps, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#850b1dac">Quickly implementing demo features</a>.   </div>
   

5. Press `⌘+R` on your keyboard to launch the demo app.

6. Open the app to view the following interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea8d077e522439fac34699d331e1aff~tplv-goo7wpa0wc-image.image) </span>

   You can perform the following operations:

   * Tap **Enter live room** to join the official demo live room of BytePlus Live. You can also replace the pre\-filled address with the address of the live room H5 page to join the specific live room. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#259416b3).

   * Tap the scan icon in the upper\-right corner and scan the QR code to join the specific live room.

      * To enter the SaaS live room H5 page by scanning the QR code, follow these steps:

         1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

         2. In the live room list, click to enter a live room.

         3. Move your pointer over **View on mobile** and scan the corresponding QR code.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0507eea490454bf9989785bd6586d652~tplv-goo7wpa0wc-image.image) </span>

      * To enter the live room H5 page integrated with the Web Viewer SDK by scanning the QR code, make sure the page has the corresponding QR code. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#259416b3).

   * Tap **Demo Config** to enter the configuration page. You can complete the following configurations as needed to achieve different demo effects.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4d0bf188c44ebaa5c6fc1d90e190a6~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The items selected above are the default configurations.      </div>
      


</Tab>
<Tab zoneid="KEPqg5ohg8" title="Android">
<TabTitle>Android</TabTitle>

Complete the following steps to run the demo of the Android app:


1. Contact BytePlus Live technical support to get the `BDLWebDemo` package and unzip it.

2. Open the `BDLWebDemo` project file using Android Studio.

3. After connecting to an Android device, click the **Run** icon in Android Studio to run the project.

4. Once the project runs successfully, follow the prompts to install the app named `BDLWebDemo` on your Android device.

5. Open the app to view the following interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911f35c1e7bc484ab9af6314b94a6330~tplv-goo7wpa0wc-image.image) </span>

   You can perform the following operations:

   * Tap **GO TO LIVEROOM** to join the official demo live room of BytePlus Live. You can also replace the pre\-filled address with the address of the live room H5 page to join the specific live room. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#259416b3).

   * Tap the scan icon in the upper\-right corner and scan the QR code to join the specific live room.

      * To enter the SaaS live room H5 page by scanning the QR code, follow these steps:

         1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement).

         2. In the live room list, click to enter a live room.

         3. Move your pointer over **View on mobile** and scan the corresponding QR code.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f556d9da28514d8b8896d8d3dde73196~tplv-goo7wpa0wc-image.image) </span>

      * To enter the live room H5 page integrated with the Web Viewer SDK by scanning the QR code, make sure the page has the corresponding QR code. For more information on how to get the live room H5 page, see [Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#259416b3).

   * Tap **DEMO CONFIGURATION** to enter the configuration page. You can complete the following configurations as needed to achieve different demo effects.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda0c24b7dd0476b92b908e9ab67fe4b~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The items selected above are the default configurations.      </div>
      


</Tab>
</Tabs>


<span id="dc6ebb18"></span>
## Feature implementation

<span id="850b1dac"></span>
### Quickly implementing demo features

If there are no custom requirements, you can quickly implement the demo features in your project by copying the demo code.


<Tabs>
<Tab zoneid="S2n10g3qqL" title="iOS">
<TabTitle>iOS</TabTitle>

Complete the following steps:


1. Copy all the code from the `BDLWebDemo/iOS/BDLWeb` directory into your project.

   ```objectivec
   BDLWebDemo
   └── iOS
       ├── BDLWeb // Web feature encapsulation code. You can copy all the code from this directory into your project to quickly implement the demo features.
       │   ├── BDLWeb
       │   │   ├── Category // System class capability extensions.
       │   │   │   ├── UIDevice+BDL.h
       │   │   │   ├── UIDevice+BDL.m
       │   │   │   ├── UIImage+BDLAdditions.h
       │   │   │   ├── UIImage+BDLAdditions.m
       │   │   │   ├── UIWindow+BDLAdditions.h
       │   │   │   └── UIWindow+BDLAdditions.m
       │   │   ├── Config // Custom configurations.
       │   │   │   ├── BDLSettings.h
       │   │   │   └── BDLSettings.m
       │   │   ├── FloatingPlayer // In-app PiP logic.
       │   │   │   ├── BDLFloatingPlayer.h
       │   │   │   ├── BDLFloatingPlayer.m
       │   │   │   ├── BDLFloatingWindow.h
       │   │   │   └── BDLFloatingWindow.m
       │   │   ├── PiP // System PiP logic.
       │   │   │   ├── BDLPiPHelper.h
       │   │   │   ├── BDLPiPHelper.m
       │   │   │   ├── BDLPiPVideoWriter.h
       │   │   │   └── BDLPiPVideoWriter.m
       │   │   ├── Utils // Utility tools.
       │   │   │   ├── BDLDefines.h
       │   │   │   ├── BDLResponder.h
       │   │   │   ├── BDLResponder.m
       │   │   │   ├── BDLUtils.h
       │   │   │   └── BDLUtils.m
       │   │   └── WebView // Live room container.
       │   │       ├── BDLWebMessageModel.h
       │   │       ├── BDLWebMessageModel.m
       │   │       ├── BDLWebView.h
       │   │       ├── BDLWebView.m
       │   │       ├── BDLWebViewController.h
       │   │       └── BDLWebViewController.m
       │   └── BDLWeb.podspec
       └── Example // Demo UI code, including configuration page, QR code scanning page, and guide page for entering the viewing page address.
           └── BDLWebDemo
               ├── AppDelegate.h
               ├── AppDelegate.m
               ├── BDLCommonWebViewController.h // A general WebView for opening URLs such as product details page, which can be replaced with the WebView or product page in your app.
               ├── BDLCommonWebViewController.m
               ├── BDLCustomConfig.h
               ├── BDLCustomConfig.m
               ├── BDLScanViewController.h // QR code scanning page in the demo.
               ├── BDLScanViewController.m
               ├── BDLSelectionCell.h
               ├── BDLSelectionCell.m
               ├── BDLSelectionView.h
               ├── BDLSelectionView.m
               ├── BDLSelectionViewController.h  // Configuration page in the demo.
               ├── BDLSelectionViewController.m
               ├── NavigationController.h // Navigation bar in the demo.
               ├── NavigationController.m
               ├── ViewController.h // Guide page for entering the viewing page address in the demo.
               └── ViewController.m
           └── Podfile
   ```
   

2. Refer to the configuration in the `BDLWebDemo/iOS/Example/Podfile` file, and add dependencies on `BDLWeb` in your project's `Podfile` file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If CocoaPods is not used in your project before, run the command <code>pod init && pod install</code> in the project's root directory to obtain the <code>Podfile</code> file.   </div>
   

   ```Ruby
   # The name of your app target
   target 'BDLWebDemo' do
   ...
     # Replace ../BDLWeb with the path to the BDLWeb folder in your project.
     pod 'BDLWeb', :path => '../BDLWeb'
   
   end
   ```
   

3. Open a terminal window and run the command `cd` to navigate to the root directory of your project. Run the command `pod install` to install the dependencies.

4. Refer to the code in `ViewController.m` located in the `BDLWebDemo/iOS/Example` directory to import the header files `BDLSettings.h` from the `BDLWebDemo/iOS/BDLWeb/BDLWeb/Config` directory and `BDLWebViewController.h` from the `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` directory for integrating BDLWeb.

5. Refer to the following code in the `ViewController.m` file located in the `BDLWebDemo/iOS/Example` directory to create and manage a live room.

   ```objectivec
   
   // MARK: - These are the key codes for integration.
   
   - (void)onJoinButtonClicked:(UIButton *)sender {
       // Since the Enter live room button may be tapped again while in-app PiP is displayed, it is necessary to check if the webViewController already exists.
       if (!self.webViewController) {
           self.webViewController = [[BDLWebViewController alloc] init];
           self.webViewController.modalPresentationStyle = UIModalPresentationFullScreen;
           self.webViewController.delegate = self;
       }
       // Check if the entered viewing page address is the same as the current live room's viewing page address. If not, reload the newly entered viewing page address.
       if (![self.textField.text isEqualToString:self.currentURL]) {
           [self.webViewController loadURLStr:self.textField.text];
           self.currentURL = self.textField.text;
       }
       [self.navigationController pushViewController:self.webViewController animated:YES];
   }
   
   - (void)viewWillAppear:(BOOL)animated {
       [super viewWillAppear:animated];
       // If in-app PiP is not enabled, set webViewController to nil to destroy webViewController, avoiding memory leaks and continuous live room audio playback.
       if (!BDLSettings.sharedInstance.enableInAppPiP) {
           self.webViewController = nil;
           self.currentURL = nil;
       }
   }
   
   - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
       [coordinator animateAlongsideTransition:nil completion:^(id<UIViewControllerTransitionCoordinatorContext>  _Nonnull context) {
       }];
       UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
       if (@available(iOS 13, *)) {
           orientation = self.view.window.windowScene.interfaceOrientation;
       } else {
           orientation = UIApplication.sharedApplication.statusBarOrientation;
       }
       // Set the floatingPlayerOrientation of webViewController to the current orientation to ensure that the orientation of the in-app PiP window is consistent with the current screen orientation.
       self.webViewController.floatingPlayerOrientation = orientation;
   }
   
   // MARK: - BDLWebViewControllerDelegate
   // Callback triggered when the in-app PiP window is tapped.
   - (void)webViewController:(BDLWebViewController *)controller floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
       // Tapping the PiP window on the demo home page displays the live room page in push mode.
       if (![self.navigationController.viewControllers containsObject:controller]) {
           [self.navigationController pushViewController:controller animated:YES];
           return;
       }
       // Tapping the PiP window on the product details page pops the ViewController above the live room page until the live room page is displayed.
       [self.navigationController popToViewController:controller animated:YES];
   }
   
   - (void)webViewController:(BDLWebViewController *)controller floatingPlayerDidClickClose:(BDLFloatingPlayer *)floatingPlayer {
   }
   // Callback triggered when the URL is tapped. This callback is triggered only when the URL content is displayed on a new page.
   - (void)webViewController:(BDLWebViewController *)controller onURLRequestClicked:(NSURLRequest *)urlRequest {
       NSLog(@"debug %s request %@ url %@", __func__, urlRequest, urlRequest.URL);
       // Here, a general WebView is used as an example. Replace it with the WebView or product page in your app to display the URL content.
       BDLCommonWebViewController *vc = [[BDLCommonWebViewController alloc] init];
       [vc.webView loadRequest:urlRequest];
       [self.navigationController pushViewController:vc animated:YES];
   }
   
   - (void)webViewControllerWillLeaveLiveRoom:(BDLWebViewController *)controller {
       // When viewers leave the live room, set webViewController to nil to avoid memory leaks.
       self.webViewController = nil;
       self.currentURL = nil;
   }
   ```
   

6. To ensure the proper functioning of the system PiP feature, complete the following steps:

   1. In Xcode, under your project's app target, click  **+ Capability** under the **Signing & Capabilities** tab, and double\-click to add **Background Modes**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2c3f9d97d084533ae3828c115bfe907~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Background Modes** section, select the **Audio, AirPlay, and Picture in Picture** checkbox.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c7c65846b8b4bb998593395246a197d~tplv-goo7wpa0wc-image.image) </span>

7. To modify the default configuration in the demo code, you can call the following methods in `BDLSettings`.

   * System PiP

      Set a value for `BDLSettings.sharedInstance.enableSystemPiP` to enable or disable system PiP. The default value is `YES`.

      * `YES`: Enable. When viewers send the app to the background and the **Start PiP** **Automatically** switch is enabled under **Settings \> General \> Picture in Picture** on their devices, they can continue watching live or VOD videos in PiP mode.

      * `NO`: Disable.

   * In\-app PiP

      Set a value for `BDLSettings.sharedInstance.enableInAppPiP` to enable or disable in\-app PiP. The default value is `YES`.

      * `YES`: Enable. When viewers navigate to other pages within the app, they can continue watching live or VOD videos in PiP mode.

      * `NO`: Disable.

   * Autoplay

      Set a value for `BDLSettings.sharedInstance.enableAutoPlay` to set whether live or VOD videos play automatically when viewers join the live room. The default value is `YES`.

      * `YES`: Automatically play.

      * `NO`: Do not automatically play.

   * Configure fullscreen icon tap behavior

      Set a value for `BDLSettings.sharedInstance.fullscreenBtnType` to set the fullscreen icon tap behavior, specifically, whether the screen will rotate when viewers enter fullscreen mode. The default value is `BDLSettingsFullscreenBtnTypeRotate`, which determines whether the screen rotates based on the video's aspect ratio.

      Valid values are as follows.

      ```objectivec
      typedef NS_ENUM(NSUInteger, BDLSettingsFullscreenBtnType) {
          /**
           * The screen does not rotate and the screen orientation remains portrait. 
           */
          BDLSettingsFullscreenBtnTypeDoNotRotate,
          /**
           * The screen rotates based on the video's aspect ratio. For landscape videos (width greater than height), the screen rotates to landscape mode when viewers enter fullscreen mode. For portrait videos (width less than height), the screen orientation remains portrait when viewers enter fullscreen mode.
           */
          BDLSettingsFullscreenBtnTypeRotate,
          /**
           * The screen is forced to rotate to landscape mode.
           */
          BDLSettingsFullscreenBtnTypeForceRotate,
      };
      ```
      


</Tab>
<Tab zoneid="MPiq6XoAzR" title="Android">
<TabTitle>Android</TabTitle>

Complete the following steps:


1. In the directory `app/src/main/java/com/bdlive/bdlwebdemo`, copy all the code from the `sdk` directory into your project.

   ```Python
   com.bdlive.bdlwebdemo
   ├── demo        # Demo UI code, including configuration page, QR code scanning page, and guide page for entering the viewing page address.
   ├── sdk         # Web feature encapsulation code. You can copy all the code from this directory into your project to quickly implement the demo features.
       ├── api         # Public API.
           ├── BDLWebViewActivity.java  # WebView container page.
           ├── WebConfig.java  # WebView configuration class.
       ├── data        # Used to store web interaction data.
       ├── pip         # PiP logic.
       ├── util        # Utility class.
       ├── webview     # WebView encapsulation logic.
           ├── BDLNativeBridge.java     # Communication bridge for handling communication between the app and Web.
           ├── BDLWebView.java          # Custom WebView.
           ├── BDLWebViewController.java # WebView manager.
   ```
   

2. Complete the following configurations in the `AndroidManifest.xml` file under the `app/src/main` directory:

   * Add permissions.

      ```XML
      <!-- Network status permissions -->
      <uses-permission android:name="android.permission.INTERNET" />
      <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
      
      <!-- System window permissions -->
      <uses-permission android:name="android.permission.REORDER_TASKS" />
      <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
      <uses-permission android:name="android.permission.SYSTEM_OVERLAY_WINDOW" />
      ```
      

   * Declare `Activity` to ensure that the behavior of `BDLWebViewActivity` aligns with expectations and provides a consistent user experience.

      ```XML
      <activity
          android:name="com.bdlive.bdlwebdemo.sdk.api.BDLWebViewActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:exported="false"
          android:launchMode="singleTask"
          android:screenOrientation="portrait"
          android:theme="@style/TVUAppThemeFullscreen"
          android:windowSoftInputMode="adjustResize|adjustNothing|stateAlwaysHidden"
          tools:ignore="LockedOrientationActivity" />
      ```
      

3. In the `app/src/main/res` directory, copy the layout files from the `layout` directory, `values/strings.xml`, `style.xml`, and other resource files referenced in the Java code into the corresponding directories in your project to avoid resource not found errors during compilation and runtime. If there are any omissions, IDEs like Android Studio will highlight missing resource files with red indicators. Locate and copy the resource files into the corresponding directories in your project as indicated.

4. Call the `start` method in `BDLWebViewActivity` to enter the live room page.

   ```Java
   BDLWebViewActivity.start(activity, webUrl);
   ```
   

5. To modify the default configuration in the demo code, you can call the following methods in `WebConfig`.

   * PiP

      Use the `setPIPConfig` method to enable system PiP, enable in\-app PiP, or disable PiP. The default value is `VALUE_PIP_SYSTEM`, which enables system PiP.

      * Enable system PiP: Viewers can continue watching live or VOD videos in PiP mode when they move the app to the background or navigate to other pages within the app. Android users need to enable the floating window permission on their devices to use system PiP. For a better user experience, we recommend that you enable system PiP.

      * Enable in\-app PiP: Viewers can continue watching live or VOD videos in PiP mode when opening other pages in the current app.

      * Disable PiP: Viewers cannot watch live or VOD videos in PiP mode.

      Valid values are as follows.

      ```Java
      // Disable PiP.
      public static final int VALUE_PIP_DISABLE = 0;
      // Enable in-app PiP.
      public static final int VALUE_PIP_APPLICATION = 1;
      // Enable system PiP.
      public static final int VALUE_PIP_SYSTEM = 2;
      ```
      

   * Autoplay

      Use the `setAutoPlayConfig` method to set whether live or VOD videos play automatically when viewers join the live room. The default value is `true`.

      * `true`: Automatically play.

      * `false`: Do not automatically play.

   * Background playback

      Use the `setBackPlayConfig` method to set whether the live or VOD videos will continue playing in the background when viewers switch the current app to the background while system PiP is disabled. The default value is `true`.

      * `true`: Continue playing in the background.

      * `false`: Stop playing in the background.

   * Replace the fallback image for playback

      The fallback image for playback refers to the image displayed in the player when the first frame of the video is loaded. The default fallback image is shown as follows.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf95747ba41c46459d670681a0180238~tplv-goo7wpa0wc-image.image) </span>

      Use the `setDefaultBitmapConfig` method to set whether to replace the default fallback image with a custom image. The default value is `true`. In the demo, the fallback image is replaced with a transparent image. To customize the fallback image, see [Basic custom configurations](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#7f8f09c3).

      * `true`: Replace.

      * `false`: Do not replace.

   * Configure fullscreen icon tap behavior

      Use the `setFullscreenActionConfig` method to set the fullscreen icon tap behavior, specifically, whether the screen will rotate when viewers enter fullscreen mode. The default value is `VALUE_FULLSCREEN_ACTION_AUTO`, which determines whether the screen rotates based on the video's aspect ratio.

      Valid values are as follows.

      ```Java
      // The screen rotates based on the video's aspect ratio. For landscape videos (width greater than height), the screen rotates to landscape mode when viewers enter fullscreen mode. For portrait videos (width less than height), the screen orientation remains portrait when viewers enter fullscreen mode. 
      public static final int VALUE_FULLSCREEN_ACTION_AUTO = 0;
      // The screen is forced to rotate to landscape mode.
      public static final int VALUE_FULLSCREEN_ACTION_ROTATE_SCREEN = 1;
      // The screen does not rotate and the screen orientation remains portrait.
      public static final int VALUE_FULLSCREEN_ACTION_KEEP_SCREEN_ORIENTATION = 2;
      ```
      


</Tab>
</Tabs>


<span id="7f8f09c3"></span>
### Basic custom configurations

After [Quickly implementing demo features](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#850b1dac), to make some basic custom configurations to the features in the demo, you can refer to the following content.


<Tabs>
<Tab zoneid="Tmjvjjc1tN" title="iOS">
<TabTitle>iOS</TabTitle>

* Modify the width and height of the in\-app PiP window

   In the `getFloatingFrame` method located in the `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView/BDLWebViewController.m` file, modify the values of `size.height` (height) and `size.width` (width). Unit: points.

   ```objectivec
   - (CGRect)getFloatingFrame {
       CGSize size = self.webView.videoSize;
       // Portrait video, width is less than height.
       if (self.webView.isPortraitVideo) {
           CGFloat height = size.height;
           size.height = 180;
           size.width = size.width / height * 180;
       }
       else {
       // Landscape video, width is greater than height.
           CGFloat width = size.width;
           size.width = 180;
           size.height = size.height / width * 180;
       }
       CGSize screenSize = [BDLUtils landscapeScreenSize];
       if (self.isPortrait) {
           screenSize = [BDLUtils portraitScreenSize];
       }
       return CGRectMake(screenSize.width - size.width - 20,
                         screenSize.height - size.height - 20,
                         size.width,
                         size.height);
   }
   ```
   

* Add control UI or customize the display style of the control UI in the in\-app PiP window

   In the `showWithFrame:closeButton:` method located in the `BDLWebDemo/iOS/BDLWeb/BDLWeb/FloatingPlayer/BDLFloatingPlayer.m` file, add the control UI or customize the display style of the control UI for the in\-app PiP window.

   The following sample code modifies the display style of the close icon for the in\-app PiP window.

   ```objectivec
   - (BOOL)showWithFrame:(CGRect)frame closeButton:(BOOL)haveCloseButton {
       if ([self.floatingWindow isFloating]) {
           return NO;
       }
       
       self.haveCloseButton = haveCloseButton;
       self.floatingFrame = frame;
           
       @bdl_weakify(self);
       self.floatingWindow.allowClose = self.haveCloseButton;
       // Replace with a custom close icon image.
       UIImage *closeImage = [BDLUtils imageNamed:@"close"]; 
       [self.floatingWindow showWithView:self.containerView
                              closeImage:closeImage
                          closeImageSize:CGSizeMake(30, 30)
                               initFrame:[self getInitFrame]
                              finalFrame:self.floatingFrame
                                duration:0.3
                              willAppear:^(UIView * _Nonnull floatingView) {
           @bdl_strongify(self);
           if ([self.delegate respondsToSelector:@selector(floatingPlayerWillAppear:)]) {
               [self.delegate floatingPlayerWillAppear:self];
           }
       } didDisappear:^(UIView * _Nonnull floatingView) {
           @bdl_strongify(self);
           if ([self.delegate respondsToSelector:@selector(floatingPlayerDidDisappear:)]) {
               [self.delegate floatingPlayerDidDisappear:self];
           }
       } willClose:^(UIView * _Nonnull floatingView) {
           @bdl_strongify(self);
           if ([self.delegate respondsToSelector:@selector(floatingPlayerWillClose:)]) {
               [self.delegate floatingPlayerWillClose:self];
           }
       }];
       return YES;
   }
   ```
   

* Customize the redirection logic

   In the demo, when viewers tap a product card under the menu, a floating product card, a header ad, an in\-page ad, a floating ad, a host account, a URL in the comment area under the chat interaction menu, or a URL in a pinned comment, the basic WKWebView will be used to open addresses with `http` or `https` protocol headers. To customize the redirection logic and tailor the page redirection behavior to specific scenarios or requirements, you can replace the logic in the `webViewController:onURLRequestClicked:` method located in the `BDLWebDemo/iOS/Example/ViewController.m` file with your own custom redirection logic.

   ```objectivec
   - (void)webViewController:(BDLWebViewController *)controller onURLRequestClicked:(NSURLRequest *)urlRequest {
       NSLog(@"debug %s request %@ url %@", __func__, urlRequest, urlRequest.URL);
       BDLCommonWebViewController *vc = [[BDLCommonWebViewController alloc] init];
       [vc.webView loadRequest:urlRequest];
       [self.navigationController pushViewController:vc animated:YES];
   }
   ```
   


</Tab>
<Tab zoneid="xvKd4saKb9" title="Android">
<TabTitle>Android</TabTitle>

* Modify the width and height of the PiP window

   In the `updateTargetParams` method of the `FloatView` class located in the `sdk/pip` directory, modify the values of `mTargetWidth` (width) and `mTargetHeight` (height). Unit: px.

   ```Java
   public void updateTargetParams() {
   
       // requestWidthHeightRatio is the aspect ratio of the video.
       if (requestWidthHeightRatio > 0) {
           if (requestWidthHeightRatio > 1) {
               // Landscape video, width is greater than height.
               mTargetWidth = SizeUtils.dp2px(180);
               mTargetHeight = mTargetWidth / requestWidthHeightRatio;
           } else {
               // Portrait video, width is less than height.
               mTargetWidth = SizeUtils.dp2px(102);
               mTargetHeight = mTargetWidth / requestWidthHeightRatio;
           }
       } else {
           mTargetWidth = SizeUtils.dp2px(180);
           mTargetHeight = SizeUtils.dp2px(102);
       }
       
       //...
   }
   ```
   

* Add control UI or customize the display style of the control UI in the PiP window

   In the `addChildView` method of the `FloatView` class located in the `sdk/pip` directory, add the control UI or customize the display style of the control UI for the PiP window, such as customizing the display style of the close icon.

   The following sample code adds a custom TextView to the PiP window.

   ```TypeScript
   // Add a custom TextView.
   TextView textView = new TextView(mContext);
   textView.setText("Custom Text");
   mChildCard.addView(textView,new LayoutParams(SizeUtils.dp2px(30),SizeUtils.dp2px(20)));
   ```
   

* Customize the permission request dialog box for floating windows

   After enabling system PiP using the `setPIPConfig` method, viewers need to additionally enable the device's floating window permission to use system PiP. To customize the permission request dialog box for floating windows displayed in the live room, you can replace the `ConfirmDialog` dialog box with a custom dialog box in the `showSystemPIPPermissionDialog` method of the `BDLWebViewActivity` class located in the `sdk/api` directory.

   ```Java
   public void showSystemPIPPermissionDialog(boolean isExit) {
       ConfirmDialog.Builder builder = new ConfirmDialog.Builder(this);
       builder.setTitle(getString(R.string.open_float_window_play_tips))
               .setConfirmText(getString(R.string.go_open))
               .setCancelText(getString(R.string.cancel))
               .setConfirmListener(v -> {
                   FloatUtil.requestPermission(this);
               })
               .setCancelListener(v -> {
                   hasShowRequestPIPPermissionDialog = true;
                   if (isExit) {
                       doManualFinish();
                   }
               }).build().show();
   }
   ```
   

* Customize the fallback image for playback

   The fallback image for playback refers to the image displayed in the player when the first frame of the video is loaded.

   After replacing the fallback image using the `setDefaultBitmapConfig` method, the default fallback image is a transparent image. To replace the transparent image with a custom fallback image, you can replace the returned Bitmap with a custom fallback image in the `getDefaultVideoPoster` method of the `BDLWebViewController` class located in the `sdk/webview` directory.

   ```Java
   public Bitmap getDefaultVideoPoster() {
       if (WebConfig.getDefaultBitmapConfig(appContext)) {
           // Create a transparent image.
           return Bitmap.createBitmap(1, 1, Bitmap.Config.ARGB_8888);
       }
       return super.getDefaultVideoPoster();
   }
   ```
   

* Customize the redirection logic

   In the demo, when viewers tap a product card under the menu, a floating product card, a header ad, an in\-page ad, a floating ad, a host account, or a URL in a comment, the system browser will be used to open addresses with `http` or `https` protocol headers. To customize the redirection logic and tailor the page redirection behavior to specific scenarios or requirements, you can replace the logic in the `shouldOverrideUrlLoading` method of the `BDLWebViewController` class located in the `sdk/webview` directory with your own custom redirection logic.

   ```Java
   @Override
   public boolean shouldOverrideUrlLoading(WebView view, WebResourceRequest request) {
       Uri requestUri = request.getUrl();
       Log.d(TAG, "shouldOverrideUrlLoading: " + requestUri);
       String scheme = requestUri.getScheme();
       if ("http".equals(scheme) || "https".equals(scheme)) {
           attemptViewUri(appContext, requestUri);
           return true;
       }
       return super.shouldOverrideUrlLoading(view, request);
   }
   ```
   


</Tab>
</Tabs>


<span id="413edda7"></span>
### In\-depth custom development

If [Basic custom configurations](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo#7f8f09c3) cannot meet your requirements, you need to understand the specific logic of the demo features and perform in\-depth custom development.

This section introduces the specific implementation of core capabilities in the demo to help you understand the logic behind them.


<Tabs>
<Tab zoneid="LBZT84bhFs" title="iOS">
<TabTitle>iOS</TabTitle>

<span id="ead8512e"></span>
#### System PiP

Find the key code in the `BDLWebDemo/iOS/BDLWeb/BDLWeb/PiP` directory. `BDLPiPVideoWriter` implements the logic for creating black frame videos, and `BDLPiPHelper` is responsible for managing `AVPlayerController` and adding the AVPlayerController to the current live room container (`BDLWebViewController`).

The key methods are as follows:


* In `BDLPiPHelper`,

   * `setEnablePiPMode` sets whether to enable system PiP.

   * `updateVideoSize:` updates the video size. When switching playback videos, the actual video size may change. At this time, `BDLWebViewController` will call this method to update the size of the black frame video.

   * `preparePlayer` creates an `AVPlayerController` and `adds the AVPlayerController` to the current live room container.

   * `updatePlayerVCParentViewController` updates the parent view of `AVPlayerController`, allowing the switch animation to display properly when viewers switch back to the app from system PiP.

   * `playLocalVideoIfNeeded` creates and plays local black frame videos.

   * `playerViewControllerWillStartPictureInPicture:` notifies `BDLWebViewController` that PiP is about to start and adds the WebView to the `WindowScene` for system PiP.

* In `BDLPiPVideoWriter`,

   * `videoWithSize:color:completion:` attempts to get a black frame video of the corresponding size. If a black frame video of the corresponding size does not exist, call the `writeVideoWithSize:color:atPath:completion:` method to create a black frame video and return the black frame video path.

   * `writeVideoWithSize:color:atPath:completion:` creates a black frame video based on the video size, color, and path, and returns the black frame video path.


The implementation process for displaying and closing the system PiP window is as follows.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0MDVweCIgaGVpZ2h0PSIxMDQ1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSA0MDUgMTA0NSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gNzIgNjIgTCA3MiAxMzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiAxNDAuODggTCA2OC41IDEzMy44OCBMIDcyIDEzNS42MyBMIDc1LjUgMTMzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+Q3JlYXRlIGFuZCBpbml0aWFsaXplwqBCRExQaVBIZWxwZXI8L3NwYW4+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3MiAyMDIgTCA3MiAyNzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiAyODAuODggTCA2OC41IDI3My44OCBMIDcyIDI3NS42MyBMIDc1LjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTQyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q3JlYXRlIGEgYmxhY2sgZnJhbWUgdmlkZW88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIgMzQyIEwgNzIgNDE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIgNDIwLjg4IEwgNjguNSA0MTMuODggTCA3MiA0MTUuNjMgTCA3NS41IDQxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjI4MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzEycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXkgdGhlIGJsYWNrIGZyYW1lIHZpZGVvPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcyIDQ4MiBMIDcyIDU1NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDU2MC44OCBMIDY4LjUgNTUzLjg4IEwgNzIgNTU1LjYzIEwgNzUuNSA1NTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDcyIDYyMiBMIDcyIDY5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDcwMC44OCBMIDY4LjUgNjkzLjg4IEwgNzIgNjk1LjYzIEwgNzUuNSA2OTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI1NjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5MnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FbWJlZCB0aGUgV2ViVmlldyBpbnRvIHRoZSBQaVAgd2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcyIDc2MiBMIDcyIDgzNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDg0MC44OCBMIDY4LjUgODMzLjg4IEwgNzIgODM1LjYzIEwgNzUuNSA4MzMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI3MDIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDczMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAgc3dpdGNoZXMgdG8gdGhlIGZvcmVncm91bmQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIgOTAyIEwgNzIgOTc1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIgOTgwLjg4IEwgNjguNSA5NzMuODggTCA3MiA5NzUuNjMgTCA3NS41IDk3My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9Ijg0MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODcycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vdGlmeSBCRExXZWJWaWV3Q29udHJvbGxlciB0byBleGl0IFBpUCBtb2RlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI5ODIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwMTJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRoZSBXZWJWaWV3IGJhY2sgdG8gQkRMRmxvYXRpbmdQbGF5ZXIgb3IgQkRMV2ViVmlld0NvbnRyb2xsZXLCoDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNTIgNDUyIEwgMjUyIDEwMTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTIgNDUyIEwgMTQ4LjM3IDQ1MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0My4xMiA0NTIgTCAxNTAuMTIgNDQ4LjUgTCAxNDguMzcgNDUyIEwgMTUwLjEyIDQ1NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjYyIiB5PSI3NTIiIHdpZHRoPSIxNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc2MnB4OyBtYXJnaW4tbGVmdDogMjYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPklmIHRoZSBhcHAgc3dpdGNoZXMgdG8gdGhlIGJhY2tncm91bmQgYWdhaW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjQyMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDUycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcCBzd2l0Y2hlcyB0byB0aGUgYmFja2dyb3VuZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDIgMTAxMiBMIDI1MiAxMDEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjwvZz48L3N2Zz4=" />

Display the system PiP window:


1. When the WebView starts playing a video, `BDLWebViewController` creates and initializes `BDLPiPHelper`.

2. `BDLPiPHelper` creates a black frame video and uses `AVPlayerController` to play the black frame video on the screen at an extremely slow speed, while setting `AVPlayer`'s view transparency to fully transparent. This ensures that viewers do not see the black frame video while watching the video.

3. When the app switches to the background, `AVPlayerController` automatically creates a `WindowScene` for system PiP.

4. `BDLPiPHelper` embeds the WebView into the PiP window by adding the WebView to the `WindowScene` for system PiP, thereby displaying the system PiP window.


Close the system PiP window:


1. When the app switches to the foreground, `BDLPiPHelper` replays the black frame video to ensure that the PiP window can be displayed normally the next time the app switches to the background.

2. `BDLPiPHelper` notifies `BDLWebViewController` to exit PiP mode and adds the WebView back to `BDLFloatingPlayer`, thereby converting the system PiP window into an in\-app PiP window, or adds the WebView back to `BDLWebViewController` to return to the live room page.


<span id="4115a661"></span>
#### In\-app PiP

The live room (`BDLWebViewController`) contains `BDLFloatingPlayer`, and `BDLFloatingPlayer` contains `BDLFloatingWindow`.

The key methods are as follows:


* In `BDLFloatingPlayer`,

   * `updateWebView`: Add `BDLWebView` to `BDLFloatingWindow` when viewers exit system PiP mode.

   * `getNewFloatingWindow`: Creates a `BDLFloatingWindow` instance based on the passed rotation orientation.

   * `setUIOrientation:` Sets the UI orientation of `BDLFloatingPlayer`. This method calls `getNewFloatingWindow:` to recreate a `BDLFloatingWindow` instance in a new orientation.

   * `showWithFrame:closeButton:` displays the in\-app PiP window.

   * `close` closes the in\-app PiP window.

* In `BDLFloatingWindow`,

   * `floatingWnd` creates a lazy loading method for `UIWindow`.

   * `showWithView:closeImage:closeImageSize:initFrame:finalFrame:duration:willAppear:didDisappear:willClose:` displays the in\-app PiP window.

   * `close` notifies `BDLWebViewController` that in\-app PiP mode is about to exit and closes the in\-app PiP window.

   * `onPanGesture:` implements the dragging feature for the in\-app PiP window.


The implementation process for displaying and closing the in\-app PiP window is as follows.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxOTZweCIgaGVpZ2h0PSIxMjM1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxOTYgMTIzNSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gOTggNjIgTCA5OCAxMzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5OCAxNDAuODggTCA5NC41IDEzMy44OCBMIDk4IDEzNS42MyBMIDEwMS41IDEzMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+T3BlbiBhbm90aGVyIHBhZ2UgaW4gdGhlIGN1cnJlbnQgYXBwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk4IDIwMiBMIDk4IDI3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDI4MC44OCBMIDk0LjUgMjczLjg4IEwgOTggMjc1LjYzIEwgMTAxLjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzgiIHk9IjE0MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTcycHg7IG1hcmdpbi1sZWZ0OiAzOXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DcmVhdGUgQkRMRmxvYXRpbmdQbGF5ZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggMzQyIEwgOTggNDE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gOTggNDIwLjg4IEwgOTQuNSA0MTMuODggTCA5OCA0MTUuNjMgTCAxMDEuNSA0MTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOCIgeT0iMjgyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMTJweDsgbWFyZ2luLWxlZnQ6IDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNyZWF0ZTxiciAvPkJETEZsb2F0aW5nV2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk4IDQ4MiBMIDk4IDU1NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDU2MC44OCBMIDk0LjUgNTUzLjg4IEwgOTggNTU1LjYzIEwgMTAxLjUgNTUzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzgiIHk9IjQyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDUycHg7IG1hcmdpbi1sZWZ0OiAzOXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj7CoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPkNyZWF0ZTwvc3Bhbj48ZGl2PjxkaXY+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPsKgVUlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggNjIyIEwgOTggNjYyIEwgOTcuNyA2NjIgTCA5Ny43IDY5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk3LjcgNzAwLjg4IEwgOTQuMiA2OTMuODggTCA5Ny43IDY5NS42MyBMIDEwMS4yIDY5My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSI1NjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5MnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRoZSBVSVdpbmRvdyB0byB0aGUgY3VycmVudCBhcHAncyBrZXlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTcuNyA4MTIgTCA5Ny43IDg0NyBMIDk4IDg0NyBMIDk4IDg3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDg4MC44OCBMIDk0LjUgODczLjg4IEwgOTggODc1LjYzIEwgMTAxLjUgODczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMi4zOCIgeT0iNzAyIiB3aWR0aD0iMTkwLjYyIiBoZWlnaHQ9IjExMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTg5cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzU3cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPldoZW4gdmlld2VycyB0YXAgdGhlIFBpUCB3aW5kb3cncyB2aWRlbyBjb250ZW50IG9yIGNsb3NlIGljb24sIG9yIHdoZW4gYSB3ZWJwYWdlIG5vdGlmaWVzIHRoYXQgdGhlIFBpUCB3aW5kb3cgbmVlZHMgdG8gYmUgY2xvc2VkLCB0aGV5IHJldHVybiB0byB0aGUgbGl2ZSByb29tIHBhZ2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggOTQyIEwgOTggMTAxNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDEwMjAuODggTCA5NC41IDEwMTMuODggTCA5OCAxMDE1LjYzIEwgMTAxLjUgMTAxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSI4ODIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkxMnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmVtb3ZlIHRoZSBVSVdpbmRvdyBmcm9tIHRoZSBrZXlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggMTA4MiBMIDk4IDExNjUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5OCAxMTcwLjg4IEwgOTQuNSAxMTYzLjg4IEwgOTggMTE2NS42MyBMIDEwMS41IDExNjMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOCIgeT0iMTAyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1MnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGVzdHJveSBCRExGbG9hdGluZ1dpbmRvdzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzgiIHk9IjExNzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMDJweDsgbWFyZ2luLWxlZnQ6IDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRlc3Ryb3kgQkRMRmxvYXRpbmdQbGF5ZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />

Display the in\-app PiP window:


1. When viewers open another page in the current app (including returning to the demo homepage), `BDLWebViewController` creates `BDLFloatingPlayer`, ``which subsequently creates `BDLFloatingWindow`.

2. `BDLFloatingWindow` creates a `UIWindow` and adds the `UIWindow` to the current app's `keyWindow`, thereby displaying the in\-app PiP window.


Close the in\-app PiP window:


1. When viewers tap the PiP window's video content or close icon, or when a webpage notifies that the PiP window needs to be closed, they return to the live room page.

2. `BDLFloatingWindow` removes the `UIWindow` from the `keyWindow`.

3. Destroy `BDLFloatingWindow`.

4. Destroy `BDLFloatingPlayer` to close the in\-app PiP window.


Find the key code in the `BDLWebDemo/iOS/BDLWeb/BDLWeb/FloatingPlayer` directory.

<span id="b855b04a"></span>
#### Autoplay

Refer to the `BDLWebView.m` file under the `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` directory. The key code is as follows.

```objectivec
if (BDLSettings.sharedInstance.enableAutoPlay) {
    // If autoplay is enabled, live and VOD videos will play without user action.
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeNone;
}
else {
    // If autoplay is disabled, live and VOD videos require user action to play.
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeAll;
}
```


<span id="c0adba21"></span>
#### Fullscreen icon tap behavior

When viewers tap the fullscreen icon to enter fullscreen mode, call the `webView:didEnterFullScreen:` method.

```objectivec
- (void)webView:(nonnull BDLWebView *)webView didEnterFullScreen:(nonnull BDLWebMessageModel *)model {
    BDLSettings *settings = BDLSettings.sharedInstance;
    // If the current screen orientation is portrait and the fullscreen icon tap behavior is set to force rotation to landscape mode, or if the screen rotates based on the video's aspect ratio and the video width is greater than its height.
    if (self.isPortrait
        && (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeForceRotate
            || (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeRotate
                && !self.webView.isPortraitVideo))) {
        // Rotate to landscape mode.
        [UIDevice BDL_switchNewOrientation:UIInterfaceOrientationLandscapeRight];
    }
    [self updateViewFullscreen:YES];
}
```


When viewers tap the fullscreen icon to exit fullscreen mode, call the `webView:didExitFullScreen:` method.

```objectivec
- (void)webView:(nonnull BDLWebView *)webView didExitFullScreen:(nonnull BDLWebMessageModel *)model {
     // If the current screen orientation is landscape, rotate to portrait mode.
    if (!self.isPortrait) {
        [UIDevice BDL_switchNewOrientation:UIInterfaceOrientationPortrait];
    }
    [self updateViewFullscreen:NO];
}
```


You can also use the `supportedInterfaceOrientations` method to define supported screen orientations.

```objectivec
- (UIInterfaceOrientationMask)supportedInterfaceOrientations {
    // If the player is not created, the screen orientation only supports portrait.
    if (!self.webView.isPlayerCreated) {
        return UIInterfaceOrientationMaskPortrait;
    }
    BDLSettings *settings = BDLSettings.sharedInstance;
    // If the fullscreen icon tap behavior is set to force rotation to landscape mode, or if the screen rotates based on the video's aspect ratio and the video width is greater than its height, all screen orientations except upside-down are supported.
    if (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeForceRotate
        || (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeRotate
            && !self.webView.isPortraitVideo)) {
        return UIInterfaceOrientationMaskAllButUpsideDown;
    }
    //  Otherwise, the screen orientation only supports portrait.
    return UIInterfaceOrientationMaskPortrait;
}
```


For more information, see the `BDLWebViewController.m` file under the `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` directory.


</Tab>
<Tab zoneid="zQ0bySDx0U" title="Android">
<TabTitle>Android</TabTitle>

<span id="bd77eeb4"></span>
#### PiP

The key methods are as follows:


* In the `sdk/pip` directory, the `PiPManager` class (which manages the display logic of the PiP window) includes the `showPiPWebView` and `hidePiPWebView` methods, which are used to display and hide the PiP window. Additionally, the PiPManager class includes the `handleContentClick` and `handleExitClick` methods, which handle the tap behavior for the PiP video content and the close icon.

* In the `sdk/pip` directory, the `FloatView` class (which handles the interaction between the PiP window and the `WindowManager`, as well as the position and style of the PiP window) includes the `initWindow` and `addToWindow` methods. These methods are used to initialize the `window` parameters of `WindowManager` and to add the small window to the `window` hierarchy of `WindowManager`, thereby achieving the PiP effect.

* In the `sdk/api` directory, the `BDLWebViewActivity` class includes the `onPause`, `onResume`, and `initWebView` methods. These methods are respectively used to handle the operations when the live room page (`BDLWebViewActivity`) goes to the background, resumes from the background to the foreground, and initializes the WebView.


**Display the PiP window**

The implementation process for displaying the PiP window is as follows.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxNDM1cHgiIGhlaWdodD0iMTAyNXB4IiB2aWV3Qm94PSItMC41IC0wLjUgMTQzNSAxMDI1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAyODIgMTI3IEwgNDM1LjYzIDEyNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ0MC44OCAxMjcgTCA0MzMuODggMTMwLjUgTCA0MzUuNjMgMTI3IEwgNDMzLjg4IDEyMy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIyIiB5PSI5MiIgd2lkdGg9IjE2MCIgaGVpZ2h0PSI3MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTI3cHg7IG1hcmdpbi1sZWZ0OiAxMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGlubGluZWNvZGU+QkRMV2ViVmlld0FjdGl2aXR5wqA8L2lubGluZWNvZGU+aXMgYWJvdXQgdG8gZ28gdG8gdGhlIGJhY2tncm91bmQ8ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NTcgMjUyIEwgNTU3IDMyNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU1NyAzMzAuODggTCA1NTMuNSAzMjMuODggTCA1NTcgMzI1LjYzIEwgNTYwLjUgMzIzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2NjIgMTI3IEwgNzM1LjYzIDEyNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc0MC44OCAxMjcgTCA3MzMuODggMTMwLjUgTCA3MzUuNjMgMTI3IEwgNzMzLjg4IDEyMy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1NTcgMiBMIDY2MiAxMjcgTCA1NTcgMjUyIEwgNDUyIDEyNyBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiciAvPkRldGVybWluZSB3aGV0aGVyIHRoZSBQaVAgd2luZG93IGNhbiBiZSBkaXNwbGF5ZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijc1MiIgeT0iOTciIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRvIG5vdCBkaXNwbGF5IFBpUCB3aW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjY3NyIgeT0iNzciIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDg3cHg7IG1hcmdpbi1sZWZ0OiA2OTdweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5DYW5ub3QgYmUgZGlzcGxheWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NzIiIHk9IjI4MiIgd2lkdGg9IjExMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjkycHg7IG1hcmdpbi1sZWZ0OiA1NzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2FuIGJlIGRpc3BsYXllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NjQuNSAzOTIgTCA1NjQuNSA0MjcgTCA1NjQuNiA0MjcgTCA1NjQuNiA0NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NjQuNiA0NjAuODggTCA1NjEuMSA0NTMuODggTCA1NjQuNiA0NTUuNjMgTCA1NjguMSA0NTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0NTkuNSIgeT0iMzMyIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjJweDsgbWFyZ2luLWxlZnQ6IDQ2MXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DYWxsIHRoZcKgPHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+UElQTWFuYWdlci5zaG93UGlQV2ViVmlldygpIG1ldGhvZDwvc3Bhbj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NjQuNiA2MjIgTCA1NjQuNiA2NDIgTCA1NjQuNSA2NDIgTCA1NjQuNSA2NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NjQuNSA2NjAuODggTCA1NjEgNjUzLjg4IEwgNTY0LjUgNjU1LjYzIEwgNTY4IDY1My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQzNC42NSIgeT0iNDYyIiB3aWR0aD0iMjU5LjY5IiBoZWlnaHQ9IjE2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTQycHg7IG1hcmdpbi1sZWZ0OiA0MzZweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PjEuQ3JlYXRlIEZsb2F0Vmlld8KgwqA8L2Rpdj48ZGl2PkZsb2F0VmlldyBmbG9hdFZpZXcgPSBmbG9hdFZpZXdXZWFrUmVmZXJlbmNlLmdldCgpOzwvZGl2PjxkaXY+PGJyIC8+PC9kaXY+PGRpdj4yLiBBZGQgV2ViVmlldyB0byBGbG9hdFZpZXc8L2Rpdj48ZGl2PmZsb2F0Vmlldy5hZGRDaGlsZFZpZXcoYmRsV2ViVmlldyk7PC9kaXY+PGRpdj48YnIgLz48L2Rpdj48ZGl2PjMuIENhbGwgdGhlIGFkZFRvV2luZG93IG1ldGhvZCB0byBhZGQgRmxvYXRWaWV3IHRvIHRoZSB3aW5kb3cgaGllcmFyY2h5PC9kaXY+PGRpdj48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5mbG9hdFZpZXcuYWRkVG9XaW5kb3c8L3NwYW4+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+KCk7PC9zcGFuPjwvZGl2PjxkaXY+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDQ2NyA3NzcgTCAzOTMuMzcgNzc3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzg4LjEyIDc3NyBMIDM5NS4xMiA3NzMuNSBMIDM5My4zNyA3NzcgTCAzOTUuMTIgNzgwLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2MiA3NzcgTCA3MzUuNjMgNzc3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzQwLjg4IDc3NyBMIDczMy44OCA3ODAuNSBMIDczNS42MyA3NzcgTCA3MzMuODggNzczLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDU2NC41IDY2MiBMIDY2MiA3NzcgTCA1NjQuNSA4OTIgTCA0NjcgNzc3IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTkzcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzc3cHg7IG1hcmdpbi1sZWZ0OiA0NjhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGV0ZXJtaW5lIHdoZXRoZXIgc3lzdGVtIFBpUCBpcyBlbmFibGVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDExMTIgNzg0LjUgTCAxMjA1LjYzIDc4NC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTIxMC44OCA3ODQuNSBMIDEyMDMuODggNzg4IEwgMTIwNS42MyA3ODQuNSBMIDEyMDMuODggNzgxIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNzQyIiB5PSI3NDciIHdpZHRoPSIzNzAiIGhlaWdodD0iNzUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc4NXB4OyBtYXJnaW4tbGVmdDogNzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlNldCB0aGUgdmFsdWUgb2bCoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPm1QYXJhbXMudHlwZSB0byBXaW5kb3dNYW5hZ2VyLkxheW91dFBhcmFtcy5UWVBFX0FQUExJQ0FUSU9OX1BBTkVMPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTIxMiIgeT0iNzU3IiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjU1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3ODVweDsgbWFyZ2luLWxlZnQ6IDEyMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5SZWdpc3RlcsKgPGlubGluZWNvZGU+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+QWN0aXZpdHlMaWZlY3ljbGVDYWxsYmFjazwvc3Bhbj48L2lubGluZWNvZGU+PC9kaXY+PGRpdj48aW5saW5lY29kZT50byBoaWRlIG9yIHJlc3RvcmUgdGhlIFBpUCB3aW5kb3c8L2lubGluZWNvZGU+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NjIiIHk9IjczNyIgd2lkdGg9IjcwIiBoZWlnaHQ9IjI1IiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc1MHB4OyBtYXJnaW4tbGVmdDogNjYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkluLUFwcCBQaVAgZW5hYmxlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDAyIiB5PSI3NDIiIHdpZHRoPSI1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NTJweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TeXN0ZW0gUGlQIGVuYWJsZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iNzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwN3B4OyBtYXJnaW4tbGVmdDogMjkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbGwgdGhlwqA8c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5vblBhdXNlwqA8L3NwYW4+bWV0aG9kPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI3NDciIHdpZHRoPSIzODAiIGhlaWdodD0iNjUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc4MHB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TZXQgdGhlIHZhbHVlIG9mwqA8c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5tUGFyYW1zLnR5cGUgdG88L3NwYW4+PGRpdj7CoFdpbmRvd01hbmFnZXIuTGF5b3V0UGFyYW1zLlRZUEVfQVBQTElDQVRJT05fT1ZFUkxBWTwvZGl2PjxkaXY+KFRoZSB2YWx1ZXMgb2YgbVBhcmFtcy50eXBlIHZhcnkgYmFzZWQgb24gZGlmZmVyZW50IEFuZHJvaWQgdmVyc2lvbnMuIEhlcmUsIHRha2UgQW5kcm9pZCA4LjAgYW5kIGFib3ZlIGFzIGFuIGV4YW1wbGUpPC9kaXY+PGRpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQzOC4yNSIgeT0iOTUyIiB3aWR0aD0iMjUyLjUiIGhlaWdodD0iNzAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI1MXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDk4N3B4OyBtYXJnaW4tbGVmdDogNDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbGwgdGhlIHN5c3RlbSBBUEkgdG8gYWRkIEZsb2F0VmlldyB0byB0aGUgc3lzdGVtIHdpbmRvdyBoaWVyYXJjaHk8YnIgLz48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5XaW5kb3dNYW5hZ2VyLmFkZFZpZXcoZmxvYXR2aWV3LCBtUGFyYW1zKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTkyIDk5MiBMIDE5MS42MiA4MTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxOTIgOTg4IEwgNDMxLjg4IDk4OC4yNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQzNy4xMyA5ODguMjUgTCA0MzAuMTMgOTkxLjc0IEwgNDMxLjg4IDk4OC4yNCBMIDQzMC4xNCA5ODQuNzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDEzMjIgOTgyIEwgMTMyMiA4MTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMzIyIDk4MiBMIDY5Ny4xMiA5ODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2OTEuODcgOTgyIEwgNjk4Ljg3IDk3OC41IEwgNjk3LjEyIDk4MiBMIDY5OC44NyA5ODUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />


1. When the live room page (`BDLWebViewActivity`) is about to go to the background, the system calls the `onPause` method.

2. Use the `webViewController.canShowPIP()` and `WebConfig.getPIPConfig()` methods to determine whether the PiP window can be displayed.

   ```Java
   @Override
   protected void onPause() {
       super.onPause();
       if (webViewController == null) {
           return;
       }
       // Exit fullscreen mode.
       webViewController.hideCustomView();
       // Get the current PiP configuration of the app.
       int pipConfig = WebConfig.getPIPConfig(this);
       Intent intent = getIntent();
       intent.putExtra(INTENT_URL, url);
       // Determine if the PiP window can be displayed.
       if (!disablePIP && webViewController.canShowPIP()) {
           switch (pipConfig) {
               case WebConfig.VALUE_PIP_DISABLE:
                   //  PiP is disabled, so do nothing.
                   break;
               case WebConfig.VALUE_PIP_APPLICATION: // Enable in-app PiP.
               case WebConfig.VALUE_PIP_SYSTEM: // Enable system PiP.
                   // Display the PiP window.
                   PiPManager.showPiPWebView(this, intent, webViewController);
                   break;
           }
       }
   }
   ```
   

3. After determining that the PiP window can be displayed, call the `PIPManager.showPiPWebView()` method and implement the following logic in the `PIPManager.showPiPWebView()` method:

   1. Create `FloatView`.

   2. Add WebView to `FloatView`.

   3. Call the `addToWindow` method to add `FloatView` to the window hierarchy.

   ```Java
   public static boolean showPiPWebView(Activity activity, Intent intent, BDLWebViewController controller) {
       if (WebConfig.getPIPConfig(activity) == WebConfig.VALUE_PIP_SYSTEM && !FloatUtil.checkPermission(activity)) {
           return false;
       }
       webViewController = controller;
       appContext = activity.getApplicationContext();
       bindActivity = new WeakReference<>(activity);
       backIntentReference = new WeakReference<>(intent);
       BDLWebView bdlWebView = webViewController.getBdlWebView();
       ViewUtil.removeViewParent(bdlWebView);
       floatViewWeakReference = new WeakReference<>(new FloatView(activity.getApplicationContext()));
       // Create FloatView. 
       FloatView floatView = floatViewWeakReference.get();
       // Add WebView to FloatView. 
       floatView.addChildView(bdlWebView);
       // Call the addToWindow method to add FloatView to the window hierarchy.
       floatView.addToWindow(webViewController.getVideoAspectRatio(), activity);
       floatView.setContentClickListener(v -> {
           handleContentClick();
       });
       floatView.setExitClickListener(v -> {
           handleExitClick();
       });
       webViewController.notifyJoinPIP();
       return true;
   }
   ```
   

4. Call the `initWindow` and `addToWindow` methods to set the `mParams.type` for system PiP and in\-app PiP and add `FloatView` to the system `window` hierarchy.

   If in\-app PiP is enabled, register `ActivityLifecycleCallback` to hide or restore the PiP window when the live room page goes to the background or foreground.

   ```Java
   private void initWindow() {
       mWindowManager = getWindowManager(mContext);
       mParams = new WindowManager.LayoutParams();
        // Determine whether in-app PiP is enabled.
       if (WebConfig.getPIPConfig(mContext) == WebConfig.VALUE_PIP_APPLICATION) {
           mParams.type = WindowManager.LayoutParams.TYPE_APPLICATION_PANEL; 
       } else {
           // Set different mParams.type values for system PiP based on different Android versions.
           if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            // Android 8.0 and above.
               mParams.type = WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY; 
           } else if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
            // Android 7.0 and above.
               mParams.type = WindowManager.LayoutParams.TYPE_PHONE;
           } else {
           // Other versions.
               mParams.type = WindowManager.LayoutParams.TYPE_TOAST;
           }
       }
   
       mParams.flags = WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE;
   
       // Set the initial position of the PiP window.
       mParams.gravity = Gravity.TOP | Gravity.START;
   }
   
   
   public boolean addToWindow(float requestWidthHeightRatio, Activity activity) {
       this.requestWidthHeightRatio = requestWidthHeightRatio;
       adjustSize();
       if (mWindowManager != null) {
           if (!isAttachedToWindow()) {
               if (WebConfig.getPIPConfig(mContext) == WebConfig.VALUE_PIP_APPLICATION && activity != null) {
                   application = activity.getApplication();
                   mParams.token = activity.getWindow().getDecorView().getWindowToken();
                   // If in-app PiP is enabled, register ActivityLifecycleCallback to hide or restore the PiP window when the live room page goes to the background or foreground.
                   application.registerActivityLifecycleCallbacks(callback);
               } else {
               // Call the system API to add FloatView to the system window hierarchy.
                   mWindowManager.addView(this, mParams);
               }
               mHasAddWindow = true;
               return true;
           } else {
               return false;
           }
       } else {
           return false;
       }
   }
   ```
   


**Tap the PiP window**

The implementation process for tapping the video content or close icon of the PiP window is as follows.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0NzBweCIgaGVpZ2h0PSI2MDVweCIgdmlld0JveD0iLTAuNSAtMC41IDQ3MCA2MDUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE3NyAzMiBMIDM0MC42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM0NS44OCAzMiBMIDMzOC44OCAzNS41IEwgMzQwLjYzIDMyIEwgMzM4Ljg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDExNi43MSAxMiBMIDExNi43MSAyMDUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMTYuNzEgMjEwLjg4IEwgMTEzLjIxIDIwMy44OCBMIDExNi43MSAyMDUuNjMgTCAxMjAuMjEgMjAzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNTciIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA1OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjwvZGl2PjxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPkRpc3BsYXlpbmcgRmxvYXRWaWV3PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzQ3IiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+UmVkaXJlY3Qgdmlld2VycyB0b8KgPC9kaXY+PGRpdj48aW5saW5lY29kZT5CRExXZWJWaWV3QWN0aXZpdHk8L2lubGluZWNvZGU+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNjciIHk9IjIiIHdpZHRoPSIyMDAiIGhlaWdodD0iMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDdweDsgbWFyZ2luLWxlZnQ6IDE2OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PlRhcCB0aGUgdmlkZW8gY29udGVudMKgPC9kaXY+PGRpdj5vZiB0aGUgUGlQIHdpbmRvdzwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMTcgNDUyIEwgMTE3IDUyNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExNyA1MzAuODggTCAxMTMuNSA1MjMuODggTCAxMTcgNTI1LjYzIEwgMTIwLjUgNTIzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMzIgMzMyIEwgMzA1LjYzIDMzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMxMC44OCAzMzIgTCAzMDMuODggMzM1LjUgTCAzMDUuNjMgMzMyIEwgMzAzLjg4IDMyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxMTcgMjEyIEwgMjMyIDMzMiBMIDExNyA0NTIgTCAyIDMzMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DaGVjayB3aGV0aGVyIHRoZSBib3VuZCBBY3Rpdml0eSAoQkRMV2ViVmlld0FjdGl2aXR5KSBpcyBzdGlsbCBhbGl2ZTxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMDciIHk9IjEyMiIgd2lkdGg9IjE4MCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTM3cHg7IG1hcmdpbi1sZWZ0OiAxMDhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGFwIHRoZSBjbG9zZSBpY29uIG9mIHRoZSBQaVAgd2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NyIgeT0iNTMyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjcwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NjdweDsgbWFyZ2luLWxlZnQ6IDQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+SGlkZSBGbG9hdFZpZXcgYW5kIHBhdXNlIFdlYlZpZXcgcGxheWJhY2s8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMxNyIgeT0iMzAyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzJweDsgbWFyZ2luLWxlZnQ6IDMxOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PkhpZGUgRmxvYXRWaWV3IGFuZCBkZXN0cm95IHRoZSBXZWJWaWV3PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNDciIHk9IjMwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMxMnB4OyBtYXJnaW4tbGVmdDogMjQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRlc3Ryb3llZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTI3IiB5PSI0ODIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0OTJweDsgbWFyZ2luLWxlZnQ6IDEyOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BbGl2ZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

When `FloatView` is displayed and viewers tap the video content of the PiP window, they will be redirected to the live room page (`BDLWebViewActivity`). When viewers tap the close icon of the PiP window, the system will check whether the bound Activity (`BDLWebViewActivity`) is still alive.


* `BDLWebViewActivity` is still alive: Hide `FloatView` and pause WebView playback.

* `BDLWebViewActivity` has been destroyed: Hide `FloatView` and destroy the WebView.


The sample code is as follows.

```Java
// Handle the tap behavior of the PiP window's video content.
private static void handleContentClick() {
    // If the PiP window is not currently displayed, do nothing.
    if (!isInPIP()) {
        return;
    }
    if (backIntentReference == null || backIntentReference.get() == null) {
        return;
    }
    FloatUtil.setTopApp(appContext);
    Intent intent = backIntentReference.get();
    intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
    appContext.startActivity(intent);
}
// Handle the tap behavior of the PiP window's close icon.
private static void handleExitClick() {
    if (isBindActivityAlive()) {
        // If the bound Activity (BDLWebViewActivity) is still alive, hide FloatView and pause WebView playback.
        hidePiPWebView();
        if (webViewController != null) {
            webViewController.pauseWebView();
        }
    } else {
        // If the bound Activity (BDLWebViewActivity) has been destroyed, hide FloatView and destroy the WebView.
        hideAndDestroyPiPWebView();
    }
}
```


**Continue playing the video after the live room page is redisplayed**

By reusing the PiP WebView, you can continue playing live or VOD videos in the PiP window when the live room page is displayed again.

The implementation process is as follows.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3NzVweCIgaGVpZ2h0PSI1ODhweCIgdmlld0JveD0iLTAuNSAtMC41IDc3NSA1ODgiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEzMiAxMDUgTCAyOTUuNjMgMTA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzAwLjg4IDEwNSBMIDI5My44OCAxMDguNSBMIDI5NS42MyAxMDUgTCAyOTMuODggMTAxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxMiIgeT0iNzUiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5XaGVuIHRoZSBsaXZlIHJvb20gcGFnZSBuZWVkcyB0byBiZSByZWRpc3BsYXllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTUyIiB5PSI3NSIgd2lkdGg9IjEzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODVweDsgbWFyZ2luLWxlZnQ6IDE1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PkNhbGwgdGhlwqA8aW5saW5lY29kZT5vblJlc3VtZTwvaW5saW5lY29kZT7CoG1ldGhvZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzODcgMjA3LjUgTCAzODcgMjYzLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzg3IDI2OC44OCBMIDM4My41IDI2MS44OCBMIDM4NyAyNjMuNjMgTCAzOTAuNSAyNjEuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MiAxMDUgTCA1NDUuNjMgMTA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTUwLjg4IDEwNSBMIDU0My44OCAxMDguNSBMIDU0NS42MyAxMDUgTCA1NDMuODggMTAxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDM4NyAyLjUgTCA0NzIgMTA1IEwgMzg3IDIwNy41IEwgMzAyIDEwNSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMzAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldGVybWluZSB3aGV0aGVyIHRoZSA8YnIgLz5saXZlIHJvb20gcGFnZSBuZWVkcyB0byBwb3B1bGF0ZSB0aGUgV2ViVmlldzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTUyIiB5PSI3NSIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1cHg7IG1hcmdpbi1sZWZ0OiA1NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RG8gbm90IHBvcHVsYXRlIHRoZSBXZWJWaWV3PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0ODIiIHk9Ijc1IiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODVweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5ObyBuZWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MDIiIHk9IjIxNSIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyNXB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5lZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDc3IDM3NSBMIDU1MC42MyAzNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NTUuODggMzc1IEwgNTQ4Ljg4IDM3OC41IEwgNTUwLjYzIDM3NSBMIDU0OC44OCAzNzEuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjk3IDM3NSBMIDIyMy4zNyAzNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMTguMTIgMzc1IEwgMjI1LjEyIDM3MS41IEwgMjIzLjM3IDM3NSBMIDIyNS4xMiAzNzguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzg3IDI3NSBMIDQ3NyAzNzUgTCAzODcgNDc1IEwgMjk3IDM3NSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM3NXB4OyBtYXJnaW4tbGVmdDogMjk4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldGVybWluZSB3aGV0aGVyIHRoZSBQSVBNYW5hZ2VyJ3Mgd2ViVmlld0NvbnRyb2xsZXIgY2FuIGJlIHJldXNlZDxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0OTIiIHk9IjMzNSIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM0NXB4OyBtYXJnaW4tbGVmdDogNDkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbm5vdCBiZSByZXVzZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIzMiIgeT0iMzQ1IiB3aWR0aD0iNTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzU1cHg7IG1hcmdpbi1sZWZ0OiAyMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2FuIGJlIHJldXNlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTYyIiB5PSIzMTUiIHdpZHRoPSIyMTAiIGhlaWdodD0iMTAwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjVweDsgbWFyZ2luLWxlZnQ6IDU2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjEuIE5vdGlmeSBQSVBNYW5hZ2VyIHRvIGhpZGUgdGhlIEZsb2F0VmlldyBhbmQgZGVzdHJveSB0aGUgYm91bmQgV2ViVmlldzwvZGl2PjxkaXY+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+Mi7CoDwvc3Bhbj48L2Rpdj5DcmVhdGUgYSBuZXcgV2Vidmlld0NvbnRyb2xsZXI8YnIgLz48ZGl2PjxpbmxpbmVjb2RlPjMuIExvYWQgdGhlIHZpZXdpbmcgcGFnZSBhZGRyZXNzPC9pbmxpbmVjb2RlPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMzIwIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjExMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzc1cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+MS7CoDwvZGl2PlJldXNlIHRoZSB3ZWJWaWV3Q29udHJvbGxlciBvZiBQSVBNYW5hZ2VywqA8ZGl2PjIuwqA8L2Rpdj5Ob3RpZnkgUElQTWFuYWdlciB0byBoaWRlIHRoZSBGbG9hdFZpZXc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iNTI1IiB3aWR0aD0iMTkwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NTVweDsgbWFyZ2luLWxlZnQ6IDI5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BZGQgdGhlIFdlYlZpZXcgaW4gd2ViVmlld0NvbnRyb2xsZXIgdG8gdGhlIHdlYlZpZXdDb250YWluZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTEyIDU1NSBMIDEwNyA0MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzIgNTU1IEwgNjcyIDQxNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExMiA1NTUgTCAyODUuNjMgNTU1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjkwLjg4IDU1NSBMIDI4My44OCA1NTguNSBMIDI4NS42MyA1NTUgTCAyODMuODggNTUxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY3MiA1NTUgTCA0ODguMzcgNTU1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDgzLjEyIDU1NSBMIDQ5MC4xMiA1NTEuNSBMIDQ4OC4zNyA1NTUgTCA0OTAuMTIgNTU4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9zdmc+" />


1. When the live room page (`BDLWebViewActivity`) needs to be redisplayed, for example, when viewers tap the video content in the PiP window, the system will call the `onResume` method.

2. Determine whether the live room page needs to populate the WebView.

   * Need to populate: `webViewController` is null, or the parent container of `webViewController` is not `webViewContainer`. In this case, call the `initWebView` method to initialize the WebView.

   * No need to populate: `webViewController` is not null, and the parent container of `webViewController` is `webViewContainer`.

3. When calling the `initWebView` method to initialize WebView, determine whether the `PIPManager`'s `webViewController` can be reused.

   * Can be reused: When a usable video exists in `PIPManager`, and the viewing page address of the PiP window is the same as that of the live room page (`BDLWebViewActivity`), reuse the `webViewController` of `PIPManager` and notify `PIPManager` to hide the `FloatView`, thereby continuing playing the live or VOD video in the PiP window on the live room page.

   * Cannot be reused: When no usable video exists in `PIPManager`, or the viewing page address of the PiP window is different from that of the live room page (`BDLWebViewActivity`), perform the following logic:

      1. Notify `PIPManager` to hide the `FloatView` and destroy the bound WebView.

      2. Create a new `WebviewController`.

      3. Load the viewing page address.

4. Add the WebView in `webViewController` to the `webViewContainer`, ensuring the WebView is displayed on the live room page.


The sample code is as follows.

```Java
protected void onResume() {
    super.onResume();
    // When webViewController is null or the parent container of webViewController is not webViewContainer, call the initWebView method to initialize the WebView.
    if (webViewController == null || webViewController.getBdlWebView().getParent() != webViewContainer) {
        initWebView();
    }
}

private void initWebView() {
    BDLWebViewController pipWebController = PiPManager.getWebViewController();
    String pipUrl = null;
    if (pipWebController != null) {
        pipUrl = pipWebController.getUrl();
    }

    if (pipWebController != null
            && Objects.equals(url, pipUrl)) {
        // If a usable video exists in PIPManager, and the viewing page address of the PiP window is the same as that of the live room page, directly reuse the webViewController of PIPManager and notify PIPManager to hide the FloatView.
        webViewController = pipWebController;
        PiPManager.hidePiPWebView();
        webViewController.notifyLeavePIP();
    } else {
        // Notify PIPManager to hide the FloatView and destroy the bound WebView.
        PiPManager.hideAndDestroyPiPWebView();
        // Create a new WebviewController.
        webViewController = new BDLWebViewController(this, url);
        // Load the viewing page address.
        webViewController.getBdlWebView().loadUrl(url);
    }

    webViewController.setJsEventConsumer(jsEventConsumer);
    // Add the WebView in webViewController to the webViewContainer.
    webViewContainer.addView(webViewController.getBdlWebView(), new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
}
```


<span id="92df55d2"></span>
#### Autoplay

Refer to the `BDLWebViewController` class under the `sdk/webview` directory. The key code is as follows.

```Java
if (WebConfig.getAutoPlayConfig(appContext)) {
    // By disabling the restriction that video playback requires user gestures, live or VOD videos can automatically play without viewer gestures.
    webSetting.setMediaPlaybackRequiresUserGesture(false);
}
```


<span id="ce7c3d49"></span>
#### Background playback

To continue playing live or VOD videos in the background without enabling system PiP when viewers switch the current app to the background, refer to the `dispatchWindowVisibilityChanged` method in the `BDLWebView` class under the `sdk/webview` directory. The key code is as follows.

```Java
public void dispatchWindowVisibilityChanged(int visibility) {
  // To continue playing live or VOD videos when the app is switched to the background, force the visibility status to View.VISIBLE (window visible).
  if (keepMediaPlayWhenPause) {
    visibility = View.VISIBLE;
  }
  // Call the parent class's dispatchWindowVisibilityChanged method, passing the processed visibility status.
  super.dispatchWindowVisibilityChanged(visibility);
}
```


<span id="079d5ab7"></span>
#### Fullscreen icon tap behavior

After viewers tap the fullscreen icon, the webpage can enter and exit fullscreen mode using the `onShowCustomView` and `onHideCustomView` methods provided by Android WebView. Refer to the `onShowCustomView` and `onHideCustomView` methods in the `BDLWebViewController` class under the `sdk/webview` directory to enter and exit fullscreen mode.

```Java
@Override
public void onShowCustomView(View view, CustomViewCallback callback) {
    super.onShowCustomView(view, callback);
    // Enter fullscreen mode.
    showCustomView(view, callback);
}

@Override
public void onHideCustomView() {
    super.onHideCustomView();
    // Exit fullscreen mode.
    hideCustomView();
}
```


Configure the fullscreen icon tap behavior, namely setting whether the screen will rotate after viewers tap the fullscreen icon to enter fullscreen mode. The key code is as follows.

```Java
boolean needRotateScreen = false;
// Based on the configuration of the fullscreen icon tap behavior, determine whether the screen needs to rotate after viewers enter fullscreen mode.
int fullscreenActionConfig = WebConfig.getFullscreenActionConfig(appContext);
switch (fullscreenActionConfig) {
    case WebConfig.VALUE_FULLSCREEN_ACTION_AUTO:
        // Determine whether the screen needs to rotate based on the aspect ratio of the video.
        float videoAspectRatio = getVideoAspectRatio();
        if (videoAspectRatio > 1) {
            // Landscape video (width greater than height) rotates to landscape mode after viewers enter fullscreen mode.
            needRotateScreen = true;
        }
        break;
    case WebConfig.VALUE_FULLSCREEN_ACTION_KEEP_SCREEN_ORIENTATION:
        // Do not rotate the screen.
        break;
    case WebConfig.VALUE_FULLSCREEN_ACTION_ROTATE_SCREEN:
    default:
        // Rotate to landscape mode.
        needRotateScreen = true;
}

FrameLayout decorView = (FrameLayout) viewAttachActivity.getWindow().getDecorView();
FrameLayout contentLayout = viewAttachActivity.findViewById(R.id.main);
if (contentLayout == null) {
    return;
}
ViewUtil.removeViewParent(view);
if (needRotateScreen) {
    // If the screen needs to rotate to landscape mode, add the view to decorView.
    decorView.addView(view, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
} else {
    // If the screen does not need to rotate to landscape mode, add the view to contentLayout.
    contentLayout.addView(view, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
}
// If the screen needs to rotate to landscape mode, set the screen orientation to landscape.
if (needRotateScreen) {
    viewAttachActivity.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
}
```



</Tab>
</Tabs>


<span id="773a72d8"></span>
## FAQ

<span id="226c57e2"></span>
### How do the Web and your mobile Native app communicate with each other?

BytePlus Live Web and your mobile Native app (hereafter referred to as Native) have a set of communication mechanisms. The Web and Native send messages to each other to implement the features introduced in this topic. To communicate between your own web page (including your own web page with WebView embedded using iframe) and Native to achieve related features, you need to understand the communication mechanism between Web and Native and implement the reception and transmission of Web events on your own web page yourself.

<span id="4149446a"></span>
#### `JsBridge` interaction process

`JSBridge` is a bridge between the Native and Web, serving as a medium for two\-way communication.

BytePlus Live injects the global variable `window.ByteLiveJsBridge` into the `window`, including the following APIs:


* `nativeCallBack`: The Native calls `window.ByteLiveJsBridge.nativeCallBack` to send messages to the Web.

* `invokeNative`: The Web calls this API to send messages to the Native.


**Web events listened to by the Native**

```TypeScript
const data = {
  eventKey:11000, // The event triggered when the player is created.
  info: {
     isPortrait: true, // Portrait mode.
     isLive: true, // In Live status. 
};

// Send a message to the Native.
function sendMessage(){
    if(isIos){
    // Use window.webkit.messageHandlers.invokeNative.postMessage to send messages on iOS platform.
        window.webkit.messageHandlers.invokeNative.postMessage(data);
    }else{
    // Use window.ByteLiveJsBridge.invokeNative to send messages on other platforms.
        window.ByteLiveJsBridge.invokeNative(data);
    }
}
```



|Event |Key |Description |
|---|---|---|
|INIT_FINISH |10001 |The event triggered when the `JsBridge` loading is complete. |
|CREATE_PLAYER |11000 |The event triggered when the player is created.<br><br>After this event is triggered, the Native can use the `isLive` parameter to get whether the live room is in Live status and the `isPortrait` parameter to get whether the live room is in portrait mode.<br><br><br>* Valid values of the `isLive` parameter:<br><br>   * `true`: In Live status.<br><br>   * `false`: Not in Live status.<br><br>* Valid values of the `isPortrait` parameter:<br><br>   * `true`: Portrait mode.<br><br>   * `false`: Landscape mode. |
|DESTROY_PLAYER |11001 |The event triggered when the player is destroyed. |
|OPEN_FULLSCREEN |11002 |The event triggered when viewers enter fullscreen mode. |
|EXIT_FULLSCREEN |11003 |The event triggered when viewers exit fullscreen mode. |
|LIVE_ROOM_STATE_CHANGE |11004 |The event triggered when the live room status changes.<br><br>After this event is triggered, the Native can use the `status` parameter to get the live room status.<br><br>Valid values of the `status` parameter:<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |
|PLAYER_STATE_CHANGE |11005 |The event triggered when the player status changes.<br><br>After this event is triggered, the Native can use the `created` and `paused` parameters to get the player status.<br><br><br>* Valid values of the `created` parameter:<br><br>   * `true`: Created.<br><br>   * `false`: Destroyed.<br><br>* Valid values of the `paused` parameter:<br><br>   * `true`: Paused or ended.<br><br>   * `false`: Playing. |
|MEDIA_LOAD_FINISH |11006 |The event triggered when the video resource loading is complete.<br><br>After this event is triggered, the Native can use the `videoWidth` and `videoHeight` parameters to get the actual dimensions of the video and configure the width and height of the PiP window based on the video's aspect ratio. |
|CLOSE_MINI_WINDOW |11008 |The event triggered when viewers exit PiP mode. This event is triggered when the player reports an error. At the same time, the Web closes the PiP window and returns to the live room page. |
|OPEN_WAKE_LOCK |11009 |Screen always\-on enabled event. This event is triggered when a viewer joins the live room. |
|EXIT_WAKE_LOCK |110010 |Screen always\-on disabled event. This event is triggered when a viewer leaves the live room. |


**Events sent by Native to the Web**

```TypeScript
// The event to enter PiP mode. 
window.ByteLiveJsBridge.nativeCallBack({
  eventKey: 21000   
})
```



|Event |Key |Description |
|---|---|---|
|ENTER_MINI_WINDOW |21000 |The event to enter PiP mode. |
|EXIT_MINI_WINDOW |21001 |The event to exit PiP mode. |
|STOP_PLAY |21002 |The event to pause playing. |
|START_PLAY |21003 |The event to resume playing and exit PiP mode. |
|PLAY |21004 |The event to play live or VOD videos. |


<span id="0f3adec3"></span>
#### Communication process for implementing PiP and fullscreen features

Taking PiP and fullscreen features as examples, this section introduces the communication process between the Web and Native.


* PiP

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4274838fc5a4f21bc87c923587184e6~tplv-goo7wpa0wc-image.image) </span>

   1. A viewer visits the viewing page, and then the Native detects the Web’s `INIT_FINISH` event, indicating that the `JSBridge` has completed loading.

   2. Upon detecting the Web’s `CREATE_PLAYER` event, the Native confirms that the player has been created, and knows whether the live room is in Live status and in portrait mode.

   3. When the viewer leaves the viewing page, the Native needs to implement entering PiP mode and send the `ENTER_MINI_WINDOW` event to the Web.

   4. Upon detecting the Native’s `ENTER_MINI_WINDOW` event, the Web displays the player in fullscreen mode within the PiP window.

   5. The Native needs to implement exiting PiP mode and send the `EXIT_MINI_WINDOW` event to the Web in the following situations. Upon detecting the Native’s `EXIT_MINI_WINDOW` event, the Web exits the fullscreen mode of the player and returns to the viewing page.

      * The viewer returns to the viewing page by tapping the PiP window or in other ways.

      * When the live room status changes or the viewer switches the live source, the Native detects the Web's `DESTROY_PLAYER` event, indicating the player has been destroyed.

   6. (Optional) Native can send events to the Web as needed to play or pause playing live or VOD videos:

      * Send the `PLAY` event to the Web when the playing is paused in the WebView. Upon detecting this event, the Web can resume playing live or VOD videos.

      * Send the `STOP_PLAY` event to the Web during playing in the WebView. Upon detecting this event, the Web can pause the live or VOD videos.

* Fullscreen

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/698764704c154ab6a2b1609e2c4207d1~tplv-goo7wpa0wc-image.image) </span>

   1. When a viewer enters fullscreen mode, the Native detects the Web's `OPEN_FULLSCREEN` event, indicating the viewer has entered fullscreen mode, and determines whether to rotate to landscape mode.

   2. When a viewer exits fullscreen mode, the Native detects the Web's `EXIT_FULLSCREEN` event, indicating the viewer has exited fullscreen mode, and determines whether to revert to portrait mode.
