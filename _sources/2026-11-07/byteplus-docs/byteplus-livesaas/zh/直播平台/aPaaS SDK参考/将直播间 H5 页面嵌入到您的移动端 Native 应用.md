---
title: "将直播间 H5 页面嵌入到您的移动端 Native 应用"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN"
---

您可以将 BytePlus Live 直播间的 H5 页面嵌入到您的移动端 Native 应用，以实现画中画（PiP）、自动播放等常用功能。本主题以 iOS 和 Android 应用演示为例，介绍如何实现这些功能。

<span id="259416b3"></span>
## 前提条件

通过以下任一方式获取直播间的 H5 页面：


* Web 观播 SDK：集成 Web 观播 SDK 2.0.16 及以上版本时，创建直播或点播播放器实例。集成 Web 观播 SDK 的观看页即为直播间 H5 页面，仅展示一个播放器。关于如何集成 Web 观播 SDK 的更多信息，请参见 [集成 Web 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN)。

* SaaS：此处以 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)为例，介绍如何获取 SaaS 直播间 H5 页面。

   1. 在直播间列表中，点击进入某个直播间。

   2. 点击观看页地址，打开 SaaS 直播间 H5 页面。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cb3dbd6a900415191cc07edc9f8a9e3~tplv-goo7wpa0wc-image.image) </span>


<span id="04b7fe45"></span>
## 运行演示的环境要求


<Tabs>
<Tab zoneid="CsDckud5Nw" title="iOS">
<TabTitle>iOS</TabTitle>

* 运行iOS 12.0及以上系统的真机或模拟器。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">要在你的演示或项目中实现系统画中画功能，请确保你的 iOS 系统类型版本为 14.0 或以上。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">模拟器仅用于界面调试，无法保证音频、视频、画中画等功能的正常运行。为避免出现屏幕花屏或黑边等问题，建议使用实体设备。   </div>
   

* Xcode 16及以上版本。

* CocoaPods 16及以上版本。


</Tab>
<Tab zoneid="RmARPVy6jH" title="Android">
<TabTitle>Android</TabTitle>

* Android Studio 3.0及以上版本。

* 运行Android 5.0（API level 21）及以上系统的真机。

* JDK 1.7.0及以上版本。


</Tab>
</Tabs>


<span id="f34e455d"></span>
## 项目介绍

BytePlus Live 提供了一个开源示例项目 `BDLWebDemo`，演示如何将直播间 H5 页面嵌入到您的移动端 Native 应用。该演示项目对 H5 页面进行了良好适配，优化了观看体验，并提供了画中画、自动播放等扩展功能。

您可以根据需要修改演示中的代码，以实现自定义业务逻辑。

演示项目实现了以下功能：


<Tabs>
<Tab zoneid="bauSqByI4Q" title="iOS">
<TabTitle>iOS</TabTitle>

* PiP，包括系统PiP和应用内PiP

* 自动播放

* 配置全屏图标点击行为

* 自定义跳转逻辑


</Tab>
<Tab zoneid="iS9IyytyVt" title="Android">
<TabTitle>Android</TabTitle>

* PiP，包括系统PiP和应用内PiP

* 自动播放

* 配置全屏图标点击行为

* 系统PiP未开启时的后台回放

* 自定义回放的备用图片

* 自定义跳转逻辑


</Tab>
</Tabs>


<span id="596b1370"></span>
## 运行演示


<Tabs>
<Tab zoneid="vFtX7ifEJN" title="iOS">
<TabTitle>iOS</TabTitle>

完成以下步骤以运行iOS应用的演示：


1. 联系BytePlus Live技术支持获取`BDLWebDemo`包并解压。

2. 打开终端窗口，运行命令`cd`进入`BDLWebDemo/iOS/Example`目录，并运行命令`pod install`安装第三方库。

   ```Shell
   cd ./BDLWebDemo/iOS/Example
   pod install
   ```
   

3. 在Finder中找到**BDLWebDemo.xcworkspace**文件，双击打开Xcode项目。

4. 在 **BDLWebDemo** \> **Signing & Capabilities** \> **All** \> **Signing (Debug)**  部分，勾选 **Automatically manage signing** 复选框，然后修改 **Team** 和 **Bundle Identifier**，使其与您的应用信息一致。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79f580df703c425fb677b1253acd837b~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果你在模拟器上运行演示，可以跳过此步骤。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">在 Xcode 中勾选 <strong>自动管理签名</strong> 复选框可以简化代码签名流程，节省时间，并减少潜在错误。因此，我们建议你勾选该复选框。如果你未勾选该复选框，则必须修改 <strong>Provisioning Profile</strong> 和 <strong>Bundle Identifier</strong>，以匹配你的应用信息。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">在演示中，<strong>音频、AirPlay 和画中画</strong> 复选框在 <strong>后台模式</strong>部分默认已选中，因此运行演示时无需手动勾选该复选框。但在你的项目中实现演示的系统画中画功能时，需要手动勾选该复选框。详细步骤请参见 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#850b1dac">快速实现演示功能</a>。   </div>
   

5. 在键盘上按下 `⌘+R`，启动演示应用。

6. 打开应用以查看如下界面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea8d077e522439fac34699d331e1aff~tplv-goo7wpa0wc-image.image) </span>

   您可以执行以下操作：

   * 点击 **Enter live room**，加入 BytePlus Live 官方演示直播间。您也可以将预填地址替换为直播间 H5 页面的地址，以加入指定直播间。关于如何获取直播间 H5 页面，详见 [前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#259416b3)。

   * 点击右上角的扫码图标，扫描二维码以加入指定直播间。

      * 通过扫描二维码进入 SaaS 直播间 H5 页面，请按以下步骤操作：

         1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

         2. 在直播间列表中，点击进入某个直播间。

         3. 将鼠标悬停于 **View on mobile**，并扫描对应二维码。

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0507eea490454bf9989785bd6586d652~tplv-goo7wpa0wc-image.image) </span>

      * 通过扫描二维码进入集成 Web 观播 SDK 的直播间 H5 页面，请确保页面上有对应二维码。关于如何获取直播间 H5 页面，详见 [前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#259416b3)。

   * 点击 **Demo Config**，进入 配置页面。您可根据需要完成以下配置，以实现不同的演示效果。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4d0bf188c44ebaa5c6fc1d90e190a6~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">上述已选项为默认配置。      </div>
      


</Tab>
<Tab zoneid="Kv4BOMxAVm" title="Android">
<TabTitle>Android</TabTitle>

完成以下步骤以运行 Android 应用的演示：


1. 联系 BytePlus Live 技术支持获取 `BDLWebDemo` 包并解压。

2. 使用 Android Studio 打开 `BDLWebDemo` 项目文件。

3. 连接 Android 设备后，在 Android Studio 中点击 **Run** 图标运行项目。

4. 项目成功运行后，按照提示在您的 Android 设备上安装名为 `BDLWebDemo` 的应用。

5. 打开应用以查看如下界面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911f35c1e7bc484ab9af6314b94a6330~tplv-goo7wpa0wc-image.image) </span>

   您可以执行以下操作：

   * 点击 **GO TO LIVEROOM**，加入 BytePlus Live 官方演示直播间。您也可以将预填地址替换为直播间 H5 页面的地址，以加入指定直播间。关于如何获取直播间 H5 页面，详见 [前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#259416b3)。

   * 点击右上角的扫码图标，扫描二维码以加入指定直播间。

      * 通过扫描二维码进入 SaaS 直播间 H5 页面，请按以下步骤操作：

         1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement)。

         2. 在直播间列表中，点击进入某个直播间。

         3. 将鼠标悬停于 **View on mobile**，并扫描对应二维码。

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f556d9da28514d8b8896d8d3dde73196~tplv-goo7wpa0wc-image.image) </span>

      * 通过扫描二维码进入集成 Web 观播 SDK 的直播间 H5 页面，请确保页面上有对应二维码。关于如何获取直播间 H5 页面，详见 [前提条件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#259416b3)。

   * 点击 **DEMO CONFIGURATION**，进入 配置页面。您可根据需要完成以下配置，以实现不同的演示效果。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda0c24b7dd0476b92b908e9ab67fe4b~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">上述已选项为默认配置。      </div>
      


</Tab>
</Tabs>


<span id="dc6ebb18"></span>
## 功能实现

<span id="850b1dac"></span>
### 快速实现演示功能

如无自定义需求，您可以通过复制演示代码，快速在项目中实现演示功能。


<Tabs>
<Tab zoneid="XwMNHSezDK" title="iOS">
<TabTitle>iOS</TabTitle>

完成以下步骤：


1. 将 `BDLWebDemo/iOS/BDLWeb` 目录下的所有代码复制到你的项目中。

   ```objectivec
   BDLWebDemo
   └── iOS
       ├── BDLWeb // Web 功能封装代码。你可以将该目录下的所有代码复制到你的项目中，快速实现演示功能。
       │   ├── BDLWeb
       │   │   ├── Category // 系统类能力扩展。
       │   │   │   ├── UIDevice+BDL.h
       │   │   │   ├── UIDevice+BDL.m
       │   │   │   ├── UIImage+BDLAdditions.h
       │   │   │   ├── UIImage+BDLAdditions.m
       │   │   │   ├── UIWindow+BDLAdditions.h
       │   │   │   └── UIWindow+BDLAdditions.m
       │   │   ├── Config // 自定义配置。
       │   │   │   ├── BDLSettings.h
       │   │   │   └── BDLSettings.m
       │   │   ├── FloatingPlayer // 应用内画中画逻辑。
       │   │   │   ├── BDLFloatingPlayer.h
       │   │   │   ├── BDLFloatingPlayer.m
       │   │   │   ├── BDLFloatingWindow.h
       │   │   │   └── BDLFloatingWindow.m
       │   │   ├── PiP // 系统画中画逻辑。
       │   │   │   ├── BDLPiPHelper.h
       │   │   │   ├── BDLPiPHelper.m
       │   │   │   ├── BDLPiPVideoWriter.h
       │   │   │   └── BDLPiPVideoWriter.m
       │   │   ├── Utils // 工具类。
       │   │   │   ├── BDLDefines.h
       │   │   │   ├── BDLResponder.h
       │   │   │   ├── BDLResponder.m
       │   │   │   ├── BDLUtils.h
       │   │   │   └── BDLUtils.m
       │   │   └── WebView // 直播间容器。
       │   │       ├── BDLWebMessageModel.h
       │   │       ├── BDLWebMessageModel.m
       │   │       ├── BDLWebView.h
       │   │       ├── BDLWebView.m
       │   │       ├── BDLWebViewController.h
       │   │       └── BDLWebViewController.m
       │   └── BDLWeb.podspec
       └── Example // 演示 UI 代码，包括配置页、二维码扫描页，以及输入观看页地址的引导页。
           └── BDLWebDemo
               ├── AppDelegate.h
               ├── AppDelegate.m
               ├── BDLCommonWebViewController.h // 通用 WebView，用于打开如商品详情页等 URL，可替换为你应用中的 WebView 或商品页。
               ├── BDLCommonWebViewController.m
               ├── BDLCustomConfig.h
               ├── BDLCustomConfig.m
               ├── BDLScanViewController.h // 演示中的二维码扫描页。
               ├── BDLScanViewController.m
               ├── BDLSelectionCell.h
               ├── BDLSelectionCell.m
               ├── BDLSelectionView.h
               ├── BDLSelectionView.m
               ├── BDLSelectionViewController.h  // 演示中的配置页。
               ├── BDLSelectionViewController.m
               ├── NavigationController.h // 演示中的导航栏。
               ├── NavigationController.m
               ├── ViewController.h // 演示中输入观看页地址的引导页。
               └── ViewController.m
           └── Podfile
   ```
   

2. 参考 `BDLWebDemo/iOS/Example/Podfile` 文件中的配置，并在你的项目的 `Podfile` 文件中添加对 `BDLWeb` 的依赖。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果你的项目之前未使用 CocoaPods，请在项目根目录下运行命令 <code>pod init && pod install</code>，以获取 <code>Podfile</code> 文件。   </div>
   

   ```Ruby
   # 你的应用 target 名称
   target 'BDLWebDemo' do
   ...
     # 将 ../BDLWeb 替换为你项目中 BDLWeb 文件夹的路径。
     pod 'BDLWeb', :path => '../BDLWeb'
   
   end
   ```
   

3. 打开终端窗口，运行 `cd` 命令，进入你的项目根目录。运行 `pod install` 命令安装依赖。

4. 参考 `ViewController.m` 文件（位于 `BDLWebDemo/iOS/Example` 目录），导入 `BDLWebDemo/iOS/BDLWeb/BDLWeb/ Config` 目录下的头文件 `BDLSettings.h` 和 `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` 目录下的 `BDLWebViewController.h`，以集成 BDLWeb。

5. 参考 `ViewController.m` 文件（位于 `BDLWebDemo/iOS/Example` 目录）中的以下代码，用于创建和管理直播间。

   ```objectivec
   
   // MARK: - These are the key codes for integration.
   
   - (void)onJoinButtonClicked:(UIButton *)sender {
       // Since the Enter live room button may be tapped again while in-app PiP is displayed, it is necessary to check if the webViewController already exists.
       if (!self.webViewController) {
           self.webViewController = [[BDLWebViewController alloc] init];
           self.webViewController.modalPresentationStyle = UIModalPresentationFullScreen;
           self.webViewController.delegate = self;
       }
       // Check if the entered viewing page address is the same as the current live room's viewing page address.如不一致，则重新加载新输入的观看页地址。
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
   // Callback triggered when the URL is tapped.仅当 URL 内容在新页面显示时才会触发此回调。
   - (void)webViewController:(BDLWebViewController *)controller onURLRequestClicked:(NSURLRequest *)urlRequest {
       NSLog(@"debug %s request %@ url %@", __func__, urlRequest, urlRequest.URL);
       // Here, a general WebView is used as an example.请将其替换为应用中的 WebView 或产品页，以显示 URL 内容。
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
   

6. 为确保系统画中画（PiP）功能正常运行，请完成以下步骤：

   1. 在 Xcode 中，项目的应用目标下，点击  **+ Capability**（位于 **Signing & Capabilities** 标签页），双击添加 **Background Modes**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2c3f9d97d084533ae3828c115bfe907~tplv-goo7wpa0wc-image.image) </span>

   2. 在 **Background Modes** 部分，勾选 **Audio, AirPlay, and Picture in Picture** 复选框。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c7c65846b8b4bb998593395246a197d~tplv-goo7wpa0wc-image.image) </span>

7. 如需修改示例代码中的默认配置，可在 `BDLSettings` 中调用以下方法。

   * 系统画中画（PiP）

      设置 `BDLSettings.sharedInstance.enableSystemPiP` 的值，以启用或禁用系统画中画。默认值为 `YES`。

      * `YES`：启用。当观众将应用切换到后台，并且设备的 **设置 \> 通用 \> 画中画** 下的 **自动启动画中画**开关已开启时，观众可以在画中画模式下继续观看直播或点播视频。

      * `NO`：禁用。

   * 应用内画中画（PiP）

      设置 `BDLSettings.sharedInstance.enableInAppPiP` 的值，以启用或禁用应用内画中画。默认值为 `YES`。

      * `YES`：启用。当观众在应用内跳转到其他页面时，仍可在画中画模式下继续观看直播或点播视频。

      * `NO`：禁用。

   * 自动播放

      设置 `BDLSettings.sharedInstance.enableAutoPlay` 的值，以设置观众进入直播间时直播或点播视频是否自动播放。默认值为 `YES`。

      * `YES`：自动播放。

      * `NO`：不自动播放。

   * 配置全屏图标点击行为

      设置 `BDLSettings.sharedInstance.fullscreenBtnType` 的值，以配置全屏图标点击行为，即观众进入全屏模式时屏幕是否旋转。默认值为 `BDLSettingsFullscreenBtnTypeRotate`，该值会根据视频长宽比决定屏幕是否旋转。

      有效值如下。

      ```objectivec
      typedef NS_ENUM(NSUInteger, BDLSettingsFullscreenBtnType) {
          /**
           * 屏幕不旋转，方向保持为竖屏模式。
           */
          BDLSettingsFullscreenBtnTypeDoNotRotate,
          /**
           * 屏幕根据视频长宽比进行旋转。对于横屏视频（宽度大于高度），观众进入全屏模式时屏幕会旋转为横屏模式。对于竖屏视频（宽度小于高度），观众进入全屏模式时屏幕方向保持为竖屏模式。
           */
          BDLSettingsFullscreenBtnTypeRotate,
          /**
           * 屏幕强制旋转为横屏模式。
           */
          BDLSettingsFullscreenBtnTypeForceRotate,
      };
      ```
      


</Tab>
<Tab zoneid="wXwynVC0Sm" title="Android">
<TabTitle>Android</TabTitle>

完成以下步骤：


1. 在 `app/src/main/java/com/bdlive/bdlwebdemo` 目录下，将 `sdk` 目录中的所有代码复制到你的项目中。

   ```Python
   com.bdlive.bdlwebdemo
   ├── demo        # Demo UI 代码，包括配置页、二维码扫描页，以及输入观看页地址的引导页。
   ├── sdk         # Web 功能封装代码。你可以将该目录下所有代码复制到你的项目中，快速实现 Demo 功能。
       ├── api         # 公共 API。
           ├── BDLWebViewActivity.java  # WebView 容器页。
           ├── WebConfig.java  # WebView 配置类。
       ├── data        # 用于存储 Web 交互数据。
       ├── pip         # PiP 逻辑。
       ├── util        # 工具类。
       ├── webview     # WebView 封装逻辑。
           ├── BDLNativeBridge.java     # 用于处理应用与 Web 通信的桥接。
           ├── BDLWebView.java          # 自定义 WebView。
           ├── BDLWebViewController.java # WebView 管理器。
   ```
   

2. 在 `app/src/main` 目录下的 `AndroidManifest.xml` 文件中完成以下配置：

   * 添加权限。

      ```XML
      <!-- 网络状态权限 -->
      <uses-permission android:name="android.permission.INTERNET" />
      <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
      
      <!-- 系统窗口权限 -->
      <uses-permission android:name="android.permission.REORDER_TASKS" />
      <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
      <uses-permission android:name="android.permission.SYSTEM_OVERLAY_WINDOW" />
      ```
      

   * 声明 `Activity`，以确保 `BDLWebViewActivity` 的行为符合预期并提供一致的用户体验。

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
      

3. 在 `app/src/main/res` 目录下，将 `layout` 目录中的布局文件、`values/strings.xml`、`style.xml` 以及 Java 代码中引用的其他资源文件复制到项目对应的目录，以避免编译和运行时出现资源未找到错误。如有遗漏，Android Studio 等 IDE 会以红色标记缺失的资源文件。根据提示，将资源文件复制到你的项目对应的目录。

4. 在 `BDLWebViewActivity` 中调用 `start` 方法，进入直播间页面。

   ```Java
   BDLWebViewActivity.start(activity, webUrl);
   ```
   

5. 要修改演示代码中的默认配置，可以在`WebConfig`中调用以下方法。

   * 画中画（PiP）

      使用`setPIPConfig`方法可启用系统画中画、启用应用内画中画或关闭画中画。默认值为`VALUE_PIP_SYSTEM`，即启用系统画中画。

      * 启用系统画中画：观众在将应用切换到后台或在应用内跳转到其他页面时，可以继续以画中画模式观看直播或点播视频。Android 用户需在设备上开启悬浮窗权限才能使用系统画中画。为提升用户体验，建议启用系统画中画。

      * 启用应用内画中画：观众在当前应用内打开其他页面时，可以继续以画中画模式观看直播或点播视频。

      * 关闭画中画：观众无法以画中画模式观看直播或点播视频。

      有效值如下。

      ```Java
      // Disable PiP.
      public static final int VALUE_PIP_DISABLE = 0;
      // Enable in-app PiP.
      public static final int VALUE_PIP_APPLICATION = 1;
      // Enable system PiP.
      public static final int VALUE_PIP_SYSTEM = 2;
      ```
      

   * 自动播放

      使用`setAutoPlayConfig`方法设置观众进入直播间时直播或点播视频是否自动播放。默认值为`true`。

      * `true`：自动播放。

      * `false`：不自动播放。

   * 后台播放

      使用`setBackPlayConfig`方法设置在系统画中画未开启时，观众将当前应用切换到后台后直播或点播视频是否继续后台播放。默认值为`true`。

      * `true`：后台继续播放。

      * `false`：后台停止播放。

   * 替换播放的备用图片

      播放的备用图片指播放器加载视频首帧时显示的图片。默认备用图片如下所示。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf95747ba41c46459d670681a0180238~tplv-goo7wpa0wc-image.image) </span>

      使用`setDefaultBitmapConfig`方法设置是否用自定义图片替换默认备用图片。默认值为`true`。在演示中，备用图片被替换为透明图片。如需自定义备用图片，请参见[基础自定义配置](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#7f8f09c3)。

      * `true`：替换。

      * `false`：不替换。

   * 配置全屏图标点击行为

      使用`setFullscreenActionConfig`方法配置全屏图标点击行为，即观众进入全屏模式时屏幕是否旋转。默认值为 `VALUE_FULLSCREEN_ACTION_AUTO`，即根据视频长宽比判断屏幕是否旋转。

      有效值如下。

      ```Java
      // 屏幕根据视频长宽比进行旋转。对于横屏视频（宽度大于高度），观众进入全屏模式时屏幕会旋转为横屏模式。对于竖屏视频（宽度小于高度），观众进入全屏模式时屏幕方向保持为竖屏模式。
      public static final int VALUE_FULLSCREEN_ACTION_AUTO = 0;
      // 屏幕强制旋转为横屏模式。
      public static final int VALUE_FULLSCREEN_ACTION_ROTATE_SCREEN = 1;
      // 屏幕不旋转，方向保持为竖屏模式。
      public static final int VALUE_FULLSCREEN_ACTION_KEEP_SCREEN_ORIENTATION = 2;
      ```
      


</Tab>
</Tabs>


<span id="7f8f09c3"></span>
### 基础自定义配置

完成[快速实现演示功能](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#850b1dac)后，如需对演示中的功能进行基础自定义配置，可参考以下内容。


<Tabs>
<Tab zoneid="bSJajYuCaG" title="iOS">
<TabTitle>iOS</TabTitle>

* 修改应用内画中画窗口的宽高

   在`getFloatingFrame`方法（位于`BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView/BDLWebViewController.m`文件）中，修改`size.height`（高度）和`size.width`（宽度）的值。单位：points。

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
   

* 在应用内画中画窗口中添加控制界面或自定义控制界面的显示样式

   在`showWithFrame:closeButton:`方法（位于`BDLWebDemo/iOS/BDLWeb/BDLWeb/FloatingPlayer/BDLFloatingPlayer.m`文件）中，为应用内画中画窗口添加控制界面或自定义控制界面的显示样式。

   以下示例代码修改了应用内画中画窗口关闭图标的显示样式。

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
   

* 自定义跳转逻辑

   在演示中，当观众点击菜单下的商品卡片、商品浮窗、页头广告、页中广告、浮标广告、主播账号、聊天互动菜单下评论区的 URL 或置顶评论中的 URL 时，将使用基础 WKWebView 打开带有 `http` 或 `https` 协议头的地址。要自定义跳转逻辑，并根据特定场景或需求定制页面跳转行为，可以将 `webViewController:onURLRequestClicked:` 方法（位于 `BDLWebDemo/iOS/Example/ViewController.m` 文件）中的逻辑替换为自定义跳转逻辑。

   ```objectivec
   - (void)webViewController:(BDLWebViewController *)controller onURLRequestClicked:(NSURLRequest *)urlRequest {
       NSLog(@"debug %s request %@ url %@", __func__, urlRequest, urlRequest.URL);
       BDLCommonWebViewController *vc = [[BDLCommonWebViewController alloc] init];
       [vc.webView loadRequest:urlRequest];
       [self.navigationController pushViewController:vc animated:YES];
   }
   ```
   


</Tab>
<Tab zoneid="OfvQSymmvj" title="Android">
<TabTitle>Android</TabTitle>

* 修改 PiP 窗口的宽度和高度

   在 `sdk/pip` 目录下 `FloatView` 类的 `updateTargetParams` 方法中，修改 `mTargetWidth`（宽度）和 `mTargetHeight`（高度）的值。单位：px。

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
   

* 在 PiP 窗口中添加控制 UI 或自定义控制 UI 的显示样式

   在 `sdk/pip` 目录下 `FloatView` 类的 `addChildView` 方法中，为 PiP 窗口添加控制 UI 或自定义控制 UI 的显示样式，例如自定义关闭图标的显示样式。

   以下示例代码为 PiP 窗口添加了自定义 TextView。

   ```TypeScript
   // Add a custom TextView.
   TextView textView = new TextView(mContext);
   textView.setText("Custom Text");
   mChildCard.addView(textView,new LayoutParams(SizeUtils.dp2px(30),SizeUtils.dp2px(20)));
   ```
   

* 自定义悬浮窗权限请求弹窗

   通过 `setPIPConfig` 方法启用系统 PiP 后，观众还需开启设备的悬浮窗权限才能使用系统 PiP。要自定义直播间中显示的 悬浮窗权限请求弹窗，可以在 `sdk/api` 目录下 `BDLWebViewActivity` 类的 `showSystemPIPPermissionDialog` 方法中，将 `ConfirmDialog` 弹窗替换为自定义弹窗。

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
   

* 自定义回放的兜底图片

   回放的兜底图片指的是播放器 加载视频首帧时显示的图片。

   通过 `setDefaultBitmapConfig` 方法替换兜底图片后，默认兜底图片为透明图片。要将透明图片 替换为自定义兜底图片，可以在 `sdk/webview` 目录下 `BDLWebViewController` 类的 `getDefaultVideoPoster` 方法中，将返回的 Bitmap 替换为自定义兜底图片。

   ```Java
   public Bitmap getDefaultVideoPoster() {
       if (WebConfig.getDefaultBitmapConfig(appContext)) {
           // Create a transparent image.
           return Bitmap.createBitmap(1, 1, Bitmap.Config.ARGB_8888);
       }
       return super.getDefaultVideoPoster();
   }
   ```
   

* 自定义跳转逻辑

   在演示中，当观众点击菜单下的商品卡片、商品浮窗、页头广告、页中广告、浮标广告、主播账号或评论中的 URL 时，将使用系统浏览器打开带有 `http` 或 `https` 协议头的地址。要自定义跳转逻辑，并根据特定场景或需求定制页面跳转行为，可以将 `sdk/webview` 目录下 `BDLWebViewController` 类的 `shouldOverrideUrlLoading` 方法中的逻辑替换为自定义跳转逻辑。

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
### 深度自定义开发

若[基础自定义配置](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN#7f8f09c3)无法满足您的需求，您需要了解演示功能的具体逻辑，并进行深度自定义开发。

本节介绍演示中核心能力的具体实现，帮助您理解其背后的逻辑。


<Tabs>
<Tab zoneid="nRTg5zJkik" title="iOS">
<TabTitle>iOS</TabTitle>

<span id="ead8512e"></span>
#### 系统 PiP

在 `BDLWebDemo/iOS/BDLWeb/BDLWeb/PiP` 目录下查找关键代码。`BDLPiPVideoWriter` 实现了黑帧视频的生成逻辑，`BDLPiPHelper` 负责管理 `AVPlayerController` 并将 AVPlayerController 添加到当前直播间容器（`BDLWebViewController`）。

关键方法如下：


* 在 `BDLPiPHelper` 中，

   * `setEnablePiPMode` 设置是否启用系统 PiP。

   * `updateVideoSize:` 更新视频尺寸。切换回放视频时，实际视频尺寸可能会发生变化。此时，`BDLWebViewController`会调用此方法以更新黑帧视频的尺寸。

   * `preparePlayer`会创建一个`AV Player Controller`，并`将 AVPlayerController`添加到当前直播间容器中。

   * `updatePlayerVCParentViewController`会更新 `AVPlayerController`的父视图，以便观众从系统 PiP 切回应用时切换动画能够正常显示。

   * `playLocalVideoIfNeeded`会创建并播放本地黑帧视频。

   * `playerViewControllerWillStartPictureInPicture:`通知`BDLWebViewController`即将启动 PiP，并将 WebView 添加到`WindowScene`以用于系统 PiP。

* 在`BDLPiPVideoWriter`中，

   * `videoWithSize:color:completion:`尝试获取对应尺寸的黑帧视频。如果不存在对应尺寸的黑帧视频，则调用`writeVideoWithSize:color:atPath:completion:`方法创建黑帧视频，并返回黑帧视频路径。

   * `writeVideoWithSize:color:atPath:completion:`会根据视频尺寸、颜色和路径创建黑帧视频，并返回黑帧视频路径。


系统 PiP 窗口的显示与关闭实现流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0MDVweCIgaGVpZ2h0PSIxMDQ1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSA0MDUgMTA0NSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gNzIgNjIgTCA3MiAxMzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiAxNDAuODggTCA2OC41IDEzMy44OCBMIDcyIDEzNS42MyBMIDc1LjUgMTMzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+Q3JlYXRlIGFuZCBpbml0aWFsaXplwqBCRExQaVBIZWxwZXI8L3NwYW4+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3MiAyMDIgTCA3MiAyNzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiAyODAuODggTCA2OC41IDI3My44OCBMIDcyIDI3NS42MyBMIDc1LjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTQyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q3JlYXRlIGEgYmxhY2sgZnJhbWUgdmlkZW88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIgMzQyIEwgNzIgNDE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIgNDIwLjg4IEwgNjguNSA0MTMuODggTCA3MiA0MTUuNjMgTCA3NS41IDQxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjI4MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzEycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXkgdGhlIGJsYWNrIGZyYW1lIHZpZGVvPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcyIDQ4MiBMIDcyIDU1NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDU2MC44OCBMIDY4LjUgNTUzLjg4IEwgNzIgNTU1LjYzIEwgNzUuNSA1NTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDcyIDYyMiBMIDcyIDY5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDcwMC44OCBMIDY4LjUgNjkzLjg4IEwgNzIgNjk1LjYzIEwgNzUuNSA2OTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI1NjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5MnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FbWJlZCB0aGUgV2ViVmlldyBpbnRvIHRoZSBQaVAgd2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcyIDc2MiBMIDcyIDgzNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDg0MC44OCBMIDY4LjUgODMzLjg4IEwgNzIgODM1LjYzIEwgNzUuNSA4MzMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI3MDIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDczMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAgc3dpdGNoZXMgdG8gdGhlIGZvcmVncm91bmQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIgOTAyIEwgNzIgOTc1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIgOTgwLjg4IEwgNjguNSA5NzMuODggTCA3MiA5NzUuNjMgTCA3NS41IDk3My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9Ijg0MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODcycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vdGlmeSBCRExXZWJWaWV3Q29udHJvbGxlciB0byBleGl0IFBpUCBtb2RlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI5ODIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwMTJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRoZSBXZWJWaWV3IGJhY2sgdG8gQkRMRmxvYXRpbmdQbGF5ZXIgb3IgQkRMV2ViVmlld0NvbnRyb2xsZXLCoDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNTIgNDUyIEwgMjUyIDEwMTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTIgNDUyIEwgMTQ4LjM3IDQ1MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0My4xMiA0NTIgTCAxNTAuMTIgNDQ4LjUgTCAxNDguMzcgNDUyIEwgMTUwLjEyIDQ1NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjYyIiB5PSI3NTIiIHdpZHRoPSIxNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc2MnB4OyBtYXJnaW4tbGVmdDogMjYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPklmIHRoZSBhcHAgc3dpdGNoZXMgdG8gdGhlIGJhY2tncm91bmQgYWdhaW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjQyMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDUycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcCBzd2l0Y2hlcyB0byB0aGUgYmFja2dyb3VuZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDIgMTAxMiBMIDI1MiAxMDEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjwvZz48L3N2Zz4=" />

显示系统 PiP 窗口：


1. 当 WebView 开始播放视频时，`BDLWebViewController`会创建并初始化`BDLPiPHelper`。

2. `BDLPiPHelper`会创建黑帧视频，并利用`AVPlayerController`以极慢速度在屏幕上播放黑帧视频，同时将 `AVPlayer`的视图透明度设置为完全透明。这样可以确保观众在观看视频时不会看到黑帧视频。

3. 当应用切换到后台时，`AVPlayerController`会自动创建一个用于系统 PiP 的`WindowScene`。

4. `BDLPiPHelper`通过将 WebView 添加到系统 PiP 的`WindowScene`中，将 WebView 嵌入 PiP 窗口，从而显示系统 PiP 窗口。


关闭系统 PiP 窗口：


1. 当应用切换到前台时，`BDLPiPHelper`会重新播放黑帧视频，以确保 PiP 窗口下次应用切换到后台时能够正常显示。

2. `BDLPiPHelper`通知`BDLWebViewController`退出 PiP 模式，并将 WebView 添加回`BDLFloatingPlayer`，从而将系统 PiP 窗口转换为应用内 PiP 窗口，或将 WebView 添加回`BDLWebViewController`以返回直播间页面。


<span id="4115a661"></span>
#### 应用内 PiP

直播间（`BDLWebViewController`）包含`BDLFloatingPlayer`，`BDLFloatingPlayer`包含`BDLFloatingWindow`。

主要方法如下：


* 在`BDLFloatingPlayer`中，

   * `updateWebView`：当观众退出系统 PiP 模式时，`将 BDLWebView`添加到 `BDLFloatingWindow`。

   * `getNewFloatingWindow`：根据传入的旋转方向`创建一个 BDLFloatingWindow`实例。

   * `setUIOrientation:`设置 `BDLFloating`Player 的 UI 方向。该方法会调用`getNewFloatingWindow:`，以新的方向重新创建`BDLFloatingWindow`实例。

   * `showWithFrame:closeButton:`会显示应用内 PiP窗口。

   * `close`会关闭应用内 PiP窗口。

* 在`BDLFloatingWindow`中，

   * `floatingWnd`会创建`UIWindow`的懒加载方法。

   * `showWithView:closeImage:closeImageSize:initFrame:finalFrame:duration:willAppear:didDisappear:willClose:`会显示应用内 PiP 窗口。

   * `close`会通知`BDLWebViewController`应用内PiP 模式即将退出，并关闭应用内 PiP 窗口。

   * `onPanGesture:`实现应用内 PiP 窗口的拖动功能。


应用内 PiP 窗口的显示与关闭实现流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxOTZweCIgaGVpZ2h0PSIxMjM1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxOTYgMTIzNSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gOTggNjIgTCA5OCAxMzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5OCAxNDAuODggTCA5NC41IDEzMy44OCBMIDk4IDEzNS42MyBMIDEwMS41IDEzMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+T3BlbiBhbm90aGVyIHBhZ2UgaW4gdGhlIGN1cnJlbnQgYXBwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk4IDIwMiBMIDk4IDI3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDI4MC44OCBMIDk0LjUgMjczLjg4IEwgOTggMjc1LjYzIEwgMTAxLjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzgiIHk9IjE0MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTcycHg7IG1hcmdpbi1sZWZ0OiAzOXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DcmVhdGUgQkRMRmxvYXRpbmdQbGF5ZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggMzQyIEwgOTggNDE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gOTggNDIwLjg4IEwgOTQuNSA0MTMuODggTCA5OCA0MTUuNjMgTCAxMDEuNSA0MTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOCIgeT0iMjgyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMTJweDsgbWFyZ2luLWxlZnQ6IDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNyZWF0ZTxiciAvPkJETEZsb2F0aW5nV2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk4IDQ4MiBMIDk4IDU1NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDU2MC44OCBMIDk0LjUgNTUzLjg4IEwgOTggNTU1LjYzIEwgMTAxLjUgNTUzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzgiIHk9IjQyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDUycHg7IG1hcmdpbi1sZWZ0OiAzOXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj7CoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPkNyZWF0ZTwvc3Bhbj48ZGl2PjxkaXY+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPsKgVUlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggNjIyIEwgOTggNjYyIEwgOTcuNyA2NjIgTCA5Ny43IDY5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk3LjcgNzAwLjg4IEwgOTQuMiA2OTMuODggTCA5Ny43IDY5NS42MyBMIDEwMS4yIDY5My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSI1NjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5MnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRoZSBVSVdpbmRvdyB0byB0aGUgY3VycmVudCBhcHAncyBrZXlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTcuNyA4MTIgTCA5Ny43IDg0NyBMIDk4IDg0NyBMIDk4IDg3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDg4MC44OCBMIDk0LjUgODczLjg4IEwgOTggODc1LjYzIEwgMTAxLjUgODczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMi4zOCIgeT0iNzAyIiB3aWR0aD0iMTkwLjYyIiBoZWlnaHQ9IjExMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTg5cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzU3cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPldoZW4gdmlld2VycyB0YXAgdGhlIFBpUCB3aW5kb3cncyB2aWRlbyBjb250ZW50IG9yIGNsb3NlIGljb24sIG9yIHdoZW4gYSB3ZWJwYWdlIG5vdGlmaWVzIHRoYXQgdGhlIFBpUCB3aW5kb3cgbmVlZHMgdG8gYmUgY2xvc2VkLCB0aGV5IHJldHVybiB0byB0aGUgbGl2ZSByb29tIHBhZ2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggOTQyIEwgOTggMTAxNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDEwMjAuODggTCA5NC41IDEwMTMuODggTCA5OCAxMDE1LjYzIEwgMTAxLjUgMTAxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSI4ODIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkxMnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmVtb3ZlIHRoZSBVSVdpbmRvdyBmcm9tIHRoZSBrZXlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggMTA4MiBMIDk4IDExNjUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5OCAxMTcwLjg4IEwgOTQuNSAxMTYzLjg4IEwgOTggMTE2NS42MyBMIDEwMS41IDExNjMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOCIgeT0iMTAyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1MnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGVzdHJveSBCRExGbG9hdGluZ1dpbmRvdzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzgiIHk9IjExNzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMDJweDsgbWFyZ2luLWxlZnQ6IDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRlc3Ryb3kgQkRMRmxvYXRpbmdQbGF5ZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />

显示应用内 PiP 窗口：


1. 当观众在当前应用中打开其他页面（包括返回到演示主页）时，`BDLWebViewController`会创建`BDLFloatingPlayer`，随后会创建`BDLFloatingWindow`。

2. `BDLFloatingWindow`会创建一个`UIWindow`，并将`UIWindow`添加到当前应用的`keyWindow`，从而显示应用内画中画窗口。


关闭应用内画中画窗口：


1. 当观众点击画中画窗口的视频内容或关闭图标，或网页通知需要关闭画中画窗口时，将返回到直播间页面。

2. `BDLFloatingWindow`会将`UIWindow`从`keyWindow`中移除。

3. 销毁`BDLFloatingWindow`。

4. 销毁`BDLFloatingPlayer`以关闭应用内画中画窗口。


在`BDLWebDemo/iOS/BDLWeb/BDLWeb/FloatingPlayer`目录下查找关键代码。

<span id="b855b04a"></span>
#### 自动播放

参考`BDLWebView.m`文件，位于`BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView`目录下。关键代码如下。

```objectivec
if (BDLSettings.sharedInstance.enableAutoPlay) {
    // 若已开启自动播放，直播和点播视频无需用户操作即可播放。
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeNone;
}
else {
    // 若未开启自动播放，直播和点播视频需用户操作后才可播放。
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeAll;
}
```


<span id="c0adba21"></span>
#### 全屏图标点击行为

当观众点击全屏图标进入全屏模式时，调用`webView:didEnterFullScreen:`方法。

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


当观众点击全屏图标退出全屏模式时，调用`webView:didExitFullScreen:`方法。

```objectivec
- (void)webView:(nonnull BDLWebView *)webView didExitFullScreen:(nonnull BDLWebMessageModel *)model {
     // If the current screen orientation is landscape, rotate to portrait mode.
    if (!self.isPortrait) {
        [UIDevice BDL_switchNewOrientation:UIInterfaceOrientationPortrait];
    }
    [self updateViewFullscreen:NO];
}
```


你也可以使用`supportedInterfaceOrientations`方法定义支持的屏幕方向。

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


更多信息请参见`BDLWebViewController.m`文件，位于`BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView`目录下。


</Tab>
<Tab zoneid="y5aG7sSvBG" title="Android">
<TabTitle>Android</TabTitle>

<span id="bd77eeb4"></span>
#### 画中画

关键方法如下：


* 在`sdk/pip`目录下，`PiPManager`类（负责管理画中画窗口的显示逻辑）包含`showPiPWebView`和`hidePiPWebView`方法，用于显示和隐藏画中画窗口。此外，PiPManager类还包含`handleContentClick`和`handleExitClick`方法，用于处理画中画视频内容和关闭图标的点击行为。

* 在`sdk/pip`目录下，`FloatView`类（负责处理画中画窗口与`WindowManager`的交互，以及画中画窗口的位置和样式）包含`initWindow`和`addToWindow`方法。这些方法用于初始化`WindowManager`的`window`参数，并将小窗口添加到`WindowManager`的`window`层级，实现画中画效果。

* 在`sdk/api`目录下，`BDLWebViewActivity`类包含`onPause`、`onResume`和`initWebView`方法。这些方法分别用于处理直播间页面（`BDLWebViewActivity`）进入后台、从后台恢复到前台以及初始化WebView的操作。


**显示画中画窗口**

显示画中画窗口的实现流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxNDM1cHgiIGhlaWdodD0iMTAyNXB4IiB2aWV3Qm94PSItMC41IC0wLjUgMTQzNSAxMDI1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAyODIgMTI3IEwgNDM1LjYzIDEyNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ0MC44OCAxMjcgTCA0MzMuODggMTMwLjUgTCA0MzUuNjMgMTI3IEwgNDMzLjg4IDEyMy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIyIiB5PSI5MiIgd2lkdGg9IjE2MCIgaGVpZ2h0PSI3MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTI3cHg7IG1hcmdpbi1sZWZ0OiAxMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGlubGluZWNvZGU+QkRMV2ViVmlld0FjdGl2aXR5wqA8L2lubGluZWNvZGU+aXMgYWJvdXQgdG8gZ28gdG8gdGhlIGJhY2tncm91bmQ8ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NTcgMjUyIEwgNTU3IDMyNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU1NyAzMzAuODggTCA1NTMuNSAzMjMuODggTCA1NTcgMzI1LjYzIEwgNTYwLjUgMzIzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2NjIgMTI3IEwgNzM1LjYzIDEyNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc0MC44OCAxMjcgTCA3MzMuODggMTMwLjUgTCA3MzUuNjMgMTI3IEwgNzMzLjg4IDEyMy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1NTcgMiBMIDY2MiAxMjcgTCA1NTcgMjUyIEwgNDUyIDEyNyBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiciAvPkRldGVybWluZSB3aGV0aGVyIHRoZSBQaVAgd2luZG93IGNhbiBiZSBkaXNwbGF5ZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijc1MiIgeT0iOTciIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRvIG5vdCBkaXNwbGF5IFBpUCB3aW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjY3NyIgeT0iNzciIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDg3cHg7IG1hcmdpbi1sZWZ0OiA2OTdweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5DYW5ub3QgYmUgZGlzcGxheWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NzIiIHk9IjI4MiIgd2lkdGg9IjExMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjkycHg7IG1hcmdpbi1sZWZ0OiA1NzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2FuIGJlIGRpc3BsYXllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NjQuNSAzOTIgTCA1NjQuNSA0MjcgTCA1NjQuNiA0MjcgTCA1NjQuNiA0NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NjQuNiA0NjAuODggTCA1NjEuMSA0NTMuODggTCA1NjQuNiA0NTUuNjMgTCA1NjguMSA0NTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0NTkuNSIgeT0iMzMyIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjJweDsgbWFyZ2luLWxlZnQ6IDQ2MXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DYWxsIHRoZcKgPHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+UElQTWFuYWdlci5zaG93UGlQV2ViVmlldygpIG1ldGhvZDwvc3Bhbj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NjQuNiA2MjIgTCA1NjQuNiA2NDIgTCA1NjQuNSA2NDIgTCA1NjQuNSA2NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NjQuNSA2NjAuODggTCA1NjEgNjUzLjg4IEwgNTY0LjUgNjU1LjYzIEwgNTY4IDY1My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQzNC42NSIgeT0iNDYyIiB3aWR0aD0iMjU5LjY5IiBoZWlnaHQ9IjE2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTQycHg7IG1hcmdpbi1sZWZ0OiA0MzZweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PjEuQ3JlYXRlIEZsb2F0Vmlld8KgwqA8L2Rpdj48ZGl2PkZsb2F0VmlldyBmbG9hdFZpZXcgPSBmbG9hdFZpZXdXZWFrUmVmZXJlbmNlLmdldCgpOzwvZGl2PjxkaXY+PGJyIC8+PC9kaXY+PGRpdj4yLiBBZGQgV2ViVmlldyB0byBGbG9hdFZpZXc8L2Rpdj48ZGl2PmZsb2F0Vmlldy5hZGRDaGlsZFZpZXcoYmRsV2ViVmlldyk7PC9kaXY+PGRpdj48YnIgLz48L2Rpdj48ZGl2PjMuIENhbGwgdGhlIGFkZFRvV2luZG93IG1ldGhvZCB0byBhZGQgRmxvYXRWaWV3IHRvIHRoZSB3aW5kb3cgaGllcmFyY2h5PC9kaXY+PGRpdj48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5mbG9hdFZpZXcuYWRkVG9XaW5kb3c8L3NwYW4+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+KCk7PC9zcGFuPjwvZGl2PjxkaXY+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDQ2NyA3NzcgTCAzOTMuMzcgNzc3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzg4LjEyIDc3NyBMIDM5NS4xMiA3NzMuNSBMIDM5My4zNyA3NzcgTCAzOTUuMTIgNzgwLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2MiA3NzcgTCA3MzUuNjMgNzc3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzQwLjg4IDc3NyBMIDczMy44OCA3ODAuNSBMIDczNS42MyA3NzcgTCA3MzMuODggNzczLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDU2NC41IDY2MiBMIDY2MiA3NzcgTCA1NjQuNSA4OTIgTCA0NjcgNzc3IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTkzcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzc3cHg7IG1hcmdpbi1sZWZ0OiA0NjhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGV0ZXJtaW5lIHdoZXRoZXIgc3lzdGVtIFBpUCBpcyBlbmFibGVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDExMTIgNzg0LjUgTCAxMjA1LjYzIDc4NC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTIxMC44OCA3ODQuNSBMIDEyMDMuODggNzg4IEwgMTIwNS42MyA3ODQuNSBMIDEyMDMuODggNzgxIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNzQyIiB5PSI3NDciIHdpZHRoPSIzNzAiIGhlaWdodD0iNzUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc4NXB4OyBtYXJnaW4tbGVmdDogNzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlNldCB0aGUgdmFsdWUgb2bCoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPm1QYXJhbXMudHlwZSB0byBXaW5kb3dNYW5hZ2VyLkxheW91dFBhcmFtcy5UWVBFX0FQUExJQ0FUSU9OX1BBTkVMPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTIxMiIgeT0iNzU3IiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjU1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3ODVweDsgbWFyZ2luLWxlZnQ6IDEyMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5SZWdpc3RlcsKgPGlubGluZWNvZGU+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+QWN0aXZpdHlMaWZlY3ljbGVDYWxsYmFjazwvc3Bhbj48L2lubGluZWNvZGU+PC9kaXY+PGRpdj48aW5saW5lY29kZT50byBoaWRlIG9yIHJlc3RvcmUgdGhlIFBpUCB3aW5kb3c8L2lubGluZWNvZGU+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NjIiIHk9IjczNyIgd2lkdGg9IjcwIiBoZWlnaHQ9IjI1IiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc1MHB4OyBtYXJnaW4tbGVmdDogNjYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkluLUFwcCBQaVAgZW5hYmxlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDAyIiB5PSI3NDIiIHdpZHRoPSI1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NTJweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TeXN0ZW0gUGlQIGVuYWJsZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iNzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwN3B4OyBtYXJnaW4tbGVmdDogMjkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbGwgdGhlwqA8c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5vblBhdXNlwqA8L3NwYW4+bWV0aG9kPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI3NDciIHdpZHRoPSIzODAiIGhlaWdodD0iNjUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc4MHB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TZXQgdGhlIHZhbHVlIG9mwqA8c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5tUGFyYW1zLnR5cGUgdG88L3NwYW4+PGRpdj7CoFdpbmRvd01hbmFnZXIuTGF5b3V0UGFyYW1zLlRZUEVfQVBQTElDQVRJT05fT1ZFUkxBWTwvZGl2PjxkaXY+KFRoZSB2YWx1ZXMgb2YgbVBhcmFtcy50eXBlIHZhcnkgYmFzZWQgb24gZGlmZmVyZW50IEFuZHJvaWQgdmVyc2lvbnMuIEhlcmUsIHRha2UgQW5kcm9pZCA4LjAgYW5kIGFib3ZlIGFzIGFuIGV4YW1wbGUpPC9kaXY+PGRpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQzOC4yNSIgeT0iOTUyIiB3aWR0aD0iMjUyLjUiIGhlaWdodD0iNzAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI1MXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDk4N3B4OyBtYXJnaW4tbGVmdDogNDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbGwgdGhlIHN5c3RlbSBBUEkgdG8gYWRkIEZsb2F0VmlldyB0byB0aGUgc3lzdGVtIHdpbmRvdyBoaWVyYXJjaHk8YnIgLz48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5XaW5kb3dNYW5hZ2VyLmFkZFZpZXcoZmxvYXR2aWV3LCBtUGFyYW1zKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTkyIDk5MiBMIDE5MS42MiA4MTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxOTIgOTg4IEwgNDMxLjg4IDk4OC4yNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQzNy4xMyA5ODguMjUgTCA0MzAuMTMgOTkxLjc0IEwgNDMxLjg4IDk4OC4yNCBMIDQzMC4xNCA5ODQuNzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDEzMjIgOTgyIEwgMTMyMiA4MTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMzIyIDk4MiBMIDY5Ny4xMiA5ODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2OTEuODcgOTgyIEwgNjk4Ljg3IDk3OC41IEwgNjk3LjEyIDk4MiBMIDY5OC44NyA5ODUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />


1. 当直播间页面（`BDLWebViewActivity`）即将进入后台时，系统会调用`onPause`方法。

2. 使用`webViewController.canShowPIP()`和`WebConfig.getPIPConfig()`方法判断是否可以显示画中画窗口。

   ```Java
   @Override
   protected void onPause() {
       super.onPause();
       if (webViewController == null) {
           return;
       }
       // 退出全屏模式。
       webViewController.hideCustomView();
       // 获取应用当前的 PiP 配置。
       int pipConfig = WebConfig.getPIPConfig(this);
       Intent intent = getIntent();
       intent.putExtra(INTENT_URL, url);
       // 判断 PiP 窗口是否可以显示。
       if (!disablePIP && webViewController.canShowPIP()) {
           switch (pipConfig) {
               case WebConfig.VALUE_PIP_DISABLE:
                   // PiP 未开启，因此无需操作。
                   break;
               case WebConfig.VALUE_PIP_APPLICATION: // 启用应用内 PiP。
               case WebConfig.VALUE_PIP_SYSTEM: // 启用系统 PiP。
                   // 显示 PiP 窗口。
                   PiPManager.showPiPWebView(this, intent, webViewController);
                   break;
           }
       }
   }
   ```
   

3. 确定画中画窗口可以显示后，调用`PIPManager.showPiPWebView()`方法，并在`PIPManager.showPiPWebView()`方法中实现如下逻辑：

   1. 创建`FloatView`。

   2. 将WebView添加到`FloatView`。

   3. 调用`addToWindow`方法，将`FloatView`添加到窗口层级。

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
   

4. 调用`initWindow`和`addToWindow`方法，设置系统画中画和应用内画中画的`mParams.type`，并将`FloatView`添加到系统`window`层级。

   如果已开启应用内画中画，注册`ActivityLifecycleCallback`，以便直播间页面进入后台或前台时隐藏或恢复画中画窗口。

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
   


**点击画中画窗口**

PiP 窗口的视频内容或关闭图标的点击实现流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0NzBweCIgaGVpZ2h0PSI2MDVweCIgdmlld0JveD0iLTAuNSAtMC41IDQ3MCA2MDUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE3NyAzMiBMIDM0MC42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM0NS44OCAzMiBMIDMzOC44OCAzNS41IEwgMzQwLjYzIDMyIEwgMzM4Ljg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDExNi43MSAxMiBMIDExNi43MSAyMDUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMTYuNzEgMjEwLjg4IEwgMTEzLjIxIDIwMy44OCBMIDExNi43MSAyMDUuNjMgTCAxMjAuMjEgMjAzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNTciIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA1OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjwvZGl2PjxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPkRpc3BsYXlpbmcgRmxvYXRWaWV3PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzQ3IiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+UmVkaXJlY3Qgdmlld2VycyB0b8KgPC9kaXY+PGRpdj48aW5saW5lY29kZT5CRExXZWJWaWV3QWN0aXZpdHk8L2lubGluZWNvZGU+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNjciIHk9IjIiIHdpZHRoPSIyMDAiIGhlaWdodD0iMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDdweDsgbWFyZ2luLWxlZnQ6IDE2OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PlRhcCB0aGUgdmlkZW8gY29udGVudMKgPC9kaXY+PGRpdj5vZiB0aGUgUGlQIHdpbmRvdzwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMTcgNDUyIEwgMTE3IDUyNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExNyA1MzAuODggTCAxMTMuNSA1MjMuODggTCAxMTcgNTI1LjYzIEwgMTIwLjUgNTIzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMzIgMzMyIEwgMzA1LjYzIDMzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMxMC44OCAzMzIgTCAzMDMuODggMzM1LjUgTCAzMDUuNjMgMzMyIEwgMzAzLjg4IDMyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxMTcgMjEyIEwgMjMyIDMzMiBMIDExNyA0NTIgTCAyIDMzMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DaGVjayB3aGV0aGVyIHRoZSBib3VuZCBBY3Rpdml0eSAoQkRMV2ViVmlld0FjdGl2aXR5KSBpcyBzdGlsbCBhbGl2ZTxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMDciIHk9IjEyMiIgd2lkdGg9IjE4MCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTM3cHg7IG1hcmdpbi1sZWZ0OiAxMDhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGFwIHRoZSBjbG9zZSBpY29uIG9mIHRoZSBQaVAgd2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NyIgeT0iNTMyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjcwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NjdweDsgbWFyZ2luLWxlZnQ6IDQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+SGlkZSBGbG9hdFZpZXcgYW5kIHBhdXNlIFdlYlZpZXcgcGxheWJhY2s8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMxNyIgeT0iMzAyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzJweDsgbWFyZ2luLWxlZnQ6IDMxOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PkhpZGUgRmxvYXRWaWV3IGFuZCBkZXN0cm95IHRoZSBXZWJWaWV3PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNDciIHk9IjMwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMxMnB4OyBtYXJnaW4tbGVmdDogMjQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRlc3Ryb3llZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTI3IiB5PSI0ODIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0OTJweDsgbWFyZ2luLWxlZnQ6IDEyOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BbGl2ZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

当显示 `FloatView` 且观众点击 PiP 窗口的视频内容时，将跳转至直播间页面（`BDLWebViewActivity`）。当观众点击 PiP 窗口的关闭图标时，系统会检查绑定的 Activity（`BDLWebViewActivity`）是否仍然存活。


* `BDLWebViewActivity` 仍然存活：隐藏 `FloatView` 并暂停 WebView 回放。

* `BDLWebViewActivity` 已被销毁：隐藏 `FloatView` 并销毁 WebView。


示例代码如下。

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


**直播间页面重新展示后继续播放视频**

通过复用 PiP WebView，当直播间页面再次展示时，可以在 PiP 窗口中继续播放直播或点播视频。

实现流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3NzVweCIgaGVpZ2h0PSI1ODhweCIgdmlld0JveD0iLTAuNSAtMC41IDc3NSA1ODgiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEzMiAxMDUgTCAyOTUuNjMgMTA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzAwLjg4IDEwNSBMIDI5My44OCAxMDguNSBMIDI5NS42MyAxMDUgTCAyOTMuODggMTAxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxMiIgeT0iNzUiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5XaGVuIHRoZSBsaXZlIHJvb20gcGFnZSBuZWVkcyB0byBiZSByZWRpc3BsYXllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTUyIiB5PSI3NSIgd2lkdGg9IjEzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODVweDsgbWFyZ2luLWxlZnQ6IDE1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PkNhbGwgdGhlwqA8aW5saW5lY29kZT5vblJlc3VtZTwvaW5saW5lY29kZT7CoG1ldGhvZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzODcgMjA3LjUgTCAzODcgMjYzLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzg3IDI2OC44OCBMIDM4My41IDI2MS44OCBMIDM4NyAyNjMuNjMgTCAzOTAuNSAyNjEuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MiAxMDUgTCA1NDUuNjMgMTA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTUwLjg4IDEwNSBMIDU0My44OCAxMDguNSBMIDU0NS42MyAxMDUgTCA1NDMuODggMTAxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDM4NyAyLjUgTCA0NzIgMTA1IEwgMzg3IDIwNy41IEwgMzAyIDEwNSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMzAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldGVybWluZSB3aGV0aGVyIHRoZSA8YnIgLz5saXZlIHJvb20gcGFnZSBuZWVkcyB0byBwb3B1bGF0ZSB0aGUgV2ViVmlldzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTUyIiB5PSI3NSIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1cHg7IG1hcmdpbi1sZWZ0OiA1NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RG8gbm90IHBvcHVsYXRlIHRoZSBXZWJWaWV3PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0ODIiIHk9Ijc1IiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODVweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5ObyBuZWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MDIiIHk9IjIxNSIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyNXB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5lZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDc3IDM3NSBMIDU1MC42MyAzNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NTUuODggMzc1IEwgNTQ4Ljg4IDM3OC41IEwgNTUwLjYzIDM3NSBMIDU0OC44OCAzNzEuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjk3IDM3NSBMIDIyMy4zNyAzNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMTguMTIgMzc1IEwgMjI1LjEyIDM3MS41IEwgMjIzLjM3IDM3NSBMIDIyNS4xMiAzNzguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzg3IDI3NSBMIDQ3NyAzNzUgTCAzODcgNDc1IEwgMjk3IDM3NSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM3NXB4OyBtYXJnaW4tbGVmdDogMjk4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldGVybWluZSB3aGV0aGVyIHRoZSBQSVBNYW5hZ2VyJ3Mgd2ViVmlld0NvbnRyb2xsZXIgY2FuIGJlIHJldXNlZDxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0OTIiIHk9IjMzNSIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM0NXB4OyBtYXJnaW4tbGVmdDogNDkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbm5vdCBiZSByZXVzZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIzMiIgeT0iMzQ1IiB3aWR0aD0iNTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzU1cHg7IG1hcmdpbi1sZWZ0OiAyMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2FuIGJlIHJldXNlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTYyIiB5PSIzMTUiIHdpZHRoPSIyMTAiIGhlaWdodD0iMTAwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjVweDsgbWFyZ2luLWxlZnQ6IDU2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjEuIE5vdGlmeSBQSVBNYW5hZ2VyIHRvIGhpZGUgdGhlIEZsb2F0VmlldyBhbmQgZGVzdHJveSB0aGUgYm91bmQgV2ViVmlldzwvZGl2PjxkaXY+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+Mi7CoDwvc3Bhbj48L2Rpdj5DcmVhdGUgYSBuZXcgV2Vidmlld0NvbnRyb2xsZXI8YnIgLz48ZGl2PjxpbmxpbmVjb2RlPjMuIExvYWQgdGhlIHZpZXdpbmcgcGFnZSBhZGRyZXNzPC9pbmxpbmVjb2RlPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMzIwIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjExMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzc1cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+MS7CoDwvZGl2PlJldXNlIHRoZSB3ZWJWaWV3Q29udHJvbGxlciBvZiBQSVBNYW5hZ2VywqA8ZGl2PjIuwqA8L2Rpdj5Ob3RpZnkgUElQTWFuYWdlciB0byBoaWRlIHRoZSBGbG9hdFZpZXc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iNTI1IiB3aWR0aD0iMTkwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NTVweDsgbWFyZ2luLWxlZnQ6IDI5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BZGQgdGhlIFdlYlZpZXcgaW4gd2ViVmlld0NvbnRyb2xsZXIgdG8gdGhlIHdlYlZpZXdDb250YWluZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTEyIDU1NSBMIDEwNyA0MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzIgNTU1IEwgNjcyIDQxNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExMiA1NTUgTCAyODUuNjMgNTU1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjkwLjg4IDU1NSBMIDI4My44OCA1NTguNSBMIDI4NS42MyA1NTUgTCAyODMuODggNTUxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY3MiA1NTUgTCA0ODguMzcgNTU1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDgzLjEyIDU1NSBMIDQ5MC4xMiA1NTEuNSBMIDQ4OC4zNyA1NTUgTCA0OTAuMTIgNTU4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9zdmc+" />


1. 当需要重新展示直播间页面（`BDLWebViewActivity`），例如观众点击 PiP 窗口中的视频内容时，系统会调用 `onResume` 方法。

2. 判断直播间页面是否需要填充 WebView。

   * 需要填充：`webViewController` 为空，或 `webViewController` 的父容器不是 `webViewContainer`。此时调用 `initWebView` 方法初始化 WebView。

   * 无需填充：`webViewController` 不为空，且 `webViewController` 的父容器为 `webViewContainer`。

3. 调用 `initWebView` 方法初始化 WebView 时，判断 `PIPManager` 的 `webViewController` 是否可复用。

   * 可复用：当 `PIPManager` 中存在可用视频，且 PiP 窗口的观看页地址与直播间页面（`BDLWebViewActivity`）一致时，复用 `PIPManager` 的 `webViewController`，并通知 `PIPManager` 隐藏 `FloatView`，从而在直播间页面in the PiP window继续播放直播或点播视频。

   * 不可复用：当 `PIPManager` 中不存在可用视频，或 PiP 窗口的观看页地址与直播间页面（`BDLWebViewActivity`）不一致时，执行如下逻辑：

      1. 通知 `PIPManager` 隐藏 `FloatView` 并销毁绑定的 WebView。

      2. 新建 `WebviewController`。

      3. 加载观看页地址。

4. 将 `webViewController` 中的 WebView 添加到 `webViewContainer`，确保 WebView 展示在直播间页面。


示例代码如下。

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
#### 自动播放

参考 `BDLWebViewController` 类，位于 `sdk/webview` 目录下。关键代码如下。

```Java
if (WebConfig.getAutoPlayConfig(appContext)) {
    // 通过关闭视频回放需用户手势的限制，直播或回放视频可自动播放，无需观众手势。
    webSetting.setMediaPlaybackRequiresUserGesture(false);
}
```


<span id="ce7c3d49"></span>
#### 后台播放

要在观众将当前应用切换到后台时，在未开启系统 PiP 的情况下继续播放直播或点播视频，请参考 `dispatchWindowVisibilityChanged` 方法，位于 `BDLWebView` 类的 `sdk/webview` 目录下。关键代码如下。

```Java
public void dispatchWindowVisibilityChanged(int visibility) {
  // 为保证应用切换到后台时直播或回放视频继续播放，强制将可见状态设置为 View.VISIBLE（窗口可见）。
  if (keepMediaPlayWhenPause) {
    visibility = View.VISIBLE;
  }
  // 调用父类的 dispatchWindowVisibilityChanged 方法，传递处理后的可见状态。
  super.dispatchWindowVisibilityChanged(visibility);
}
```


<span id="079d5ab7"></span>
#### 全屏图标点击行为

观众点击全屏图标后，网页可通过 Android WebView 提供的 `onShowCustomView` 和 `onHideCustomView` 方法进入和退出全屏模式。参考 `onShowCustomView` 和 `onHideCustomView` 方法，位于 `BDLWebViewController` 类的 `sdk/webview` 目录下，实现进入和退出全屏模式。

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


配置全屏图标点击行为，即设置观众点击全屏图标进入全屏模式后屏幕是否旋转。关键代码如下。

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
## 常见问题

<span id="226c57e2"></span>
### Web 与您的移动端 Native 应用如何互相通信？

BytePlus Live Web 与您的移动端 Native 应用（下文简称 Native）具备一套通信机制。Web 与 Native 互相发送消息，以实现本主题介绍的功能。要实现自有网页（包括通过 iframe 嵌入 WebView 的自有网页）与 Native 的通信及相关功能，需了解 Web 与 Native 的通信机制，并在自有网页上自行实现 Web 事件的接收与发送。

<span id="4149446a"></span>
#### `JsBridge` 交互流程

`JSBridge` 是 Native 与 Web 之间的桥梁，作为双向通信的媒介。

BytePlus Live 会向 `window` 注入全局变量 `window.ByteLiveJsBridge`，包含以下 API：


* `nativeCallBack`：Native 调用 `window.ByteLiveJsBridge.nativeCallBack`，向 Web 发送消息。

* `invokeNative`：Web 调用该 API，向 Native 发送消息。


**Native监听的Web事件**

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



|事件 |键值 |接口行为 |
|---|---|---|
|INIT_FINISH |10001 |当 `JsBridge` 加载完成时触发的事件。 |
|CREATE_PLAYER |11000 |当播放器创建时触发的事件。<br><br>该事件触发后，Native 可通过 `isLive` 参数获取直播间是否处于直播状态，以及通过 `isPortrait` 参数获取直播间是否为竖屏模式。<br><br><br>* `isLive` 参数的有效值：<br><br>   * `true`：处于直播状态。<br><br>   * `false`：未处于直播状态。<br><br>* `isPortrait` 参数的有效值：<br><br>   * `true`：竖屏模式。<br><br>   * `false`：横屏模式。 |
|DESTROY_PLAYER |11001 |当播放器销毁时触发的事件。 |
|OPEN_FULLSCREEN |11002 |当观众进入全屏模式时触发的事件。 |
|EXIT_FULLSCREEN |11003 |当观众退出全屏模式时触发的事件。 |
|LIVE_ROOM_STATE_CHANGE |11004 |当直播间状态发生变化时触发的事件。<br><br>该事件触发后，Native 可通过 `status` 参数获取直播间状态。<br><br>`status` 参数的有效值：<br><br><br>* `1`：直播。<br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：结束。 |
|PLAYER_STATE_CHANGE |11005 |当播放器状态发生变化时触发的事件。<br><br>该事件触发后，Native 可通过 `created` 和 `paused` 参数获取播放器状态。<br><br><br>* `created` 参数的有效值：<br><br>   * `true`：已创建。<br><br>   * `false`：已销毁。<br><br>* `paused` 参数的有效值：<br><br>   * `true`：已暂停或已结束。<br><br>   * `false`：正在播放。 |
|MEDIA_LOAD_FINISH |11006 |当视频资源加载完成时触发的事件。<br><br>该事件触发后，Native 可通过 `videoWidth` 和 `videoHeight` 参数获取视频实际维度，并根据视频长宽比配置画中画窗口的宽高。 |
|CLOSE_MINI_WINDOW |11008 |当观众退出画中画模式时触发的事件。当播放器上报错误时会触发该事件。同时，Web 会关闭画中画窗口并返回直播间页面。 |
|OPEN_WAKE_LOCK |11009 |屏幕常亮已开启事件。当观众进入直播间时会触发该事件。 |
|EXIT_WAKE_LOCK |110010 |屏幕常亮未开启事件。当观众离开直播间时会触发该事件。 |


**Native发送给Web的事件**

```TypeScript
// 进入画中画模式的事件。
window.ByteLiveJsBridge.nativeCallBack({
  eventKey: 21000   
})
```



|事件 |键值 |接口行为 |
|---|---|---|
|ENTER_MINI_WINDOW |21000 |进入画中画模式的事件。 |
|EXIT_MINI_WINDOW |21001 |退出画中画模式的事件。 |
|STOP_PLAY |21002 |暂停播放的事件。 |
|START_PLAY |21003 |恢复播放并退出画中画模式的事件。 |
|PLAY |21004 |播放直播或点播视频的事件。 |


<span id="0f3adec3"></span>
#### 实现PiP和全屏功能的通信流程

以PiP和全屏功能为例，本节介绍Web与Native之间的通信流程。


* PiP

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4274838fc5a4f21bc87c923587184e6~tplv-goo7wpa0wc-image.image) </span>

   1. 观众访问观看页后，Native检测到Web的`INIT_FINISH`事件，表示`JSBridge`已加载完成。

   2. 检测到Web的`CREATE_PLAYER`事件后，Native确认播放器已创建，并获知直播间是否处于Live状态及是否为竖屏模式。

   3. 当观众离开观看页时，Native需实现进入PiP模式，并向Web发送`ENTER_MINI_WINDOW`事件。

   4. 检测到Native的`ENTER_MINI_WINDOW`事件后，Web将在PiP窗口内以全屏模式展示播放器。

   5. Native需在以下场景实现退出PiP模式，并向Web发送`EXIT_MINI_WINDOW`事件。检测到Native的`EXIT_MINI_WINDOW`事件后，Web将退出播放器的全屏模式并返回观看页。

      * 观众通过点击PiP窗口或其他方式返回观看页。

      * 当直播间状态发生变化或观众切换直播源时，Native检测到Web的`DESTROY_PLAYER`事件，表示播放器已被销毁。

   6. （可选）Native可根据需要向Web发送事件，以播放或暂停直播或点播视频：

      * 在WebView中播放被暂停时，向Web发送`PLAY`事件。检测到该事件后，Web可恢复播放直播或点播视频。

      * 在WebView播放过程中，向Web发送`STOP_PLAY`事件。检测到该事件后，Web可暂停直播或点播视频。

* 全屏

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/698764704c154ab6a2b1609e2c4207d1~tplv-goo7wpa0wc-image.image) </span>

   1. 观众进入全屏模式时，Native检测到Web的`OPEN_FULLSCREEN`事件，表示观众已进入全屏模式，并判断是否旋转为横屏模式。

   2. 观众退出全屏模式时，Native检测到Web的`EXIT_FULLSCREEN`事件，表示观众已退出全屏模式，并判断是否恢复为竖屏模式。
