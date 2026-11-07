---
title: "iOS 观播 SDK：基础功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN"
---

本主题介绍如何集成 iOS 观播 SDK 的基础功能，包括如何集成完整直播间、完整播放器、独立播放器和悬浮播放器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">当前观众一次只能加入一个直播间。</div>


<span id="59273a71"></span>
## 前提条件

完成 [集成 iOS 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN) 的前 5 步。

<span id="98b7076d"></span>
## 功能

本主题介绍如何集成以下功能。


* [完整直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN#f2a7c3c8)

* [完整播放器](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN#886e9207)

* [独立播放器](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN#8f276f8b)

* [浮窗播放器](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN#765f75ba)


<span id="f2a7c3c8"></span>
## 完整直播间

完整直播间包含 BytePlus Live 直播间的所有功能模块，相较于单独集成各模块，集成更加简单便捷。除非有特殊需求，建议集成完整直播间。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0572b0440b4404dbdb4ef127dc6e574~tplv-goo7wpa0wc-image.image) </span>

关于完整直播间支持的功能详情，请参见 [SaaS 与 aPaaS 功能对比](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas-zh-CN)。

<span id="bb63491d"></span>
### 进入直播间

以下示例代码允许观众进入完整直播间，并在应用中展示完整直播间页面。

```objectivec
...
[[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                 success:^{
    // 1. Get the full-featured live room instance.
    BDLLivePullViewController *livePullVC = [[BDLLiveEngine sharedInstance] getLivePullViewController];
    // 2. (Optional) Set the modalPresentationStyle, which is the mode of displaying the live room.本例以全屏模式展示直播间。
    // If you choose to display the live room using the UINavigationController push mode, or to display the live room using the system's default mode, no additional configuration is needed.
    livePullVC.modalPresentationStyle = UIModalPresentationFullScreen;
    // 3. Set the actionProvider.此处以 "self" 为例，用于响应直播间的展示、隐藏等事件。
    livePullVC.actionProvider = self;
    // 4.（可选）配置直播间。
    [self configLivePullViewController:livePullVC];
    // 5. Display the live room.此处以 present 方式展示直播间为例。
    // 如需通过 UINavigationController push 方式展示直播间，参见通过 push 方式展示直播间。
    [self showLivePullViewController:livePullVC];
} failure:^(NSError * _Nonnull error) {
    // Process error messages.本例将错误信息打印到控制台以便调试和排查。
    NSLog(@"%@", error.localizedDescription);
}];

/// Configure the live room, including customizing the UI.你可以将功能代码复制到此方法中运行。
- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}

/// 6. Methods required for implementing actionProvider.
/// 6.1 展示直播间的方法。
/// Display the live room.当需要展示完整直播间时，SDK 会调用此方法。此处以 present 方式展示直播间为例。
/// To display the live room using the UINavigationController push mode, see Displaying the live room using push mode.
- (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self presentViewController:livePullVC animated:NO completion:nil];
}

/// 6.2 The method to hide the live room.
/// 隐藏直播间。当需要隐藏完整直播间时，SDK 会调用此方法。
- (void)hideLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self dismissViewControllerAnimated:YES completion:nil];
}
```


<span id="d649b214"></span>
### 使用 push 模式展示直播间

如需通过 `UINavigationController` `push` 模式展示完整直播间，可参考以下流程。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">仅 SDK 1.29.1 及以上版本支持<code>push</code>方式。</div>



1. 获取完整直播间实例后，配置悬浮播放器的展示逻辑，即应用内画中画（PiP）。

   1. 设置是否展示悬浮播放器。

      ```objectivec
      /// 当直播间状态发生变化时，会触发此回调，并将以下信息传递给应用：完整直播间实例、直播间状态以及直播间页面是否关闭。
      livePullVC.config.shouldShowInAppPipIfAvailable = ^BOOL(BDLLivePullViewController * _Nonnull viewController, BDLActivityStatus status, BOOL isClose) {
          /// 根据直播间状态和直播间页面是否关闭，判断是否展示浮窗播放器。
          switch (status) {
              case BDLActivityStatusLive: // 如果直播间状态为 Live，则执行以下逻辑。
                  return isClose ? YES : NO; // 本例中，isClose 为 YES 时返回 YES，isClose 为 NO 时返回 NO。换言之，当通过pop 或 dismiss 操作关闭直播间页面时，将展示浮窗播放器。当通过push 或 present 方式展示商品详情页等新页面时，不展示浮窗播放器。
              case BDLActivityStatusReplay: // 如果直播间状态为P回放，则执行以下逻辑。
                  return isClose ? YES : NO; // 在本示例中，当 isClose 的值为 YES 时返回 YES，当 isClose 的值为 NO 时返回 NO。换句话说，当通过pop 或 dismiss 操作关闭直播间页面时，会显示浮窗播放器。当通过 push 或 present 模式显示新页面（如商品详情页面）时，不显示浮窗播放器。
              case BDLActivityStatusPreview: // 如果直播间状态为P预告且预告正在播放，则执行以下逻辑。
                  return isClose ? YES : NO; // 在本示例中，当 isClose 的值为 YES 时返回 YES，当 isClose 的值为 NO 时返回 NO。换句话说，当通过pop 或 dismiss 操作关闭直播间页面时，会显示浮窗播放器。当通过 push 或 present 模式显示新页面（如商品详情页面）时，不显示浮窗播放器。
              default:
                  return NO; // The floating player is not displayed.通常此逻辑不会触发，但为避免错误，必须设置此默认返回值。
          }
      };
      ```
      

   2. 配置在 `viewDidAppear` 时，即完整直播间对应视图展示时，是否自动关闭正在显示的悬浮播放器。

      使用以下示例代码自动关闭正在显示的悬浮播放器。

      ```objectivec
      livePullVC.config.autoCloseFloatingPlayerWhenAppear = YES;
      ```
      

   若值为 `NO`，则需在合适时机调用关闭悬浮播放器的方法。

   使用以下示例代码关闭悬浮播放器并同时展示完整直播间。

   ```objectivec
   [livePullVC hideFloatingPlayerIfAvailable:YES]
   ```
   

2. 展示完整直播间。

   示例代码如下。

   ```objectivec
   - (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
       if (self.livePullVC.navigationController) { // 当通过 push 或 present 模式显示新页面（如商品详情页面）时，SDK 会关闭浮窗播放器，不显示完整直播间，且观众点击浮窗播放器的关闭按钮后不会离开直播间。
           [self.navigationController popToViewController:livePullVC animated:YES]; // 使用 pop 操作移除显示在完整直播间之上的其他页面（ViewController）。
           return;
       }
       [self.navigationController pushViewController:livePullVC animated:YES]; // 使用 push 模式显示完整直播间。
   }
   ```
   

3. （可选）若配置悬浮播放器在新页面 push 或 present 时展示（即在步骤 1.a 中 isClose 为 NO 时返回 YES），还需自定义悬浮播放器关闭按钮的点击行为。

   示例代码如下。

   ```objectivec
       __weak typeof(self) weakSelf = self;
       livePullVC.onFloatingPlayerCloseTapped = ^BOOL(BDLLivePullViewController * _Nonnull viewController, BDLFloatingPlayer * _Nonnull floatingPlayer) {
           if (viewController.navigationController) {
               // 当通过 push 或 present 模式显示新页面（如商品详情页面）时，SDK 会关闭浮窗播放器，不显示完整直播间，且观众点击浮窗播放器的关闭按钮后不会离开直播间。
               [viewController hideFloatingPlayerIfAvailable:NO];
               return NO;
           }
           else {
               // 当通过 pop 或 dismiss 操作关闭直播间页面时，SDK 会在观众点击浮窗播放器的关闭按钮后执行默认点击行为：关闭浮窗播放器并离开直播间。
               return YES;
           }
       };
   ```
   

4. （可选）除全屏模式外，完整直播间仅支持竖屏模式展示。如应用页面支持横屏展示，请完成以下配置。

   * 展示完整直播间时，需确保前一页面仅支持竖屏模式。

      示例代码如下。

      ```objectivec
      // 在 ViewController 中添加以下代码。
      @interface ViewController : UIViewController
      @property (nonatomic, assign) BOOL visible;
      @end
      
      // 当 viewDidAppear，即前一页面对应的视图显示时，将 visible 设置为 YES，表示当前视图可见。
      - (void)viewDidAppear:(BOOL)animated {
          [super viewDidAppear:animated];
          self.visible = YES;
      }
      // 当 viewDidDisappear，即前一页面对应的视图消失时，将 visible 设置为 NO，表示当前视图不可见。
      - (void)viewDidDisappear:(BOOL)animated {
          [super viewDidDisappear:animated];
          self.visible = NO;
      }
      
      // 指定当前视图支持的页面方向。
      - (UIInterfaceOrientationMask)supportedInterfaceOrientations {
          if (!self.visible) { // 当前视图不可见时，直播间仅支持竖屏方向，以避免因侧滑返回上一页面导致显示异常。
              return UIInterfaceOrientationMaskPortrait;
          }
          // 当前视图可见时，上一页面支持的页面方向。在本示例中，上一页面支持除 UpsideDown 外的所有方向。
          return UIInterfaceOrientationMaskAllButUpsideDown;
      }
      ```
      

   * 直播间页面以横屏展示（即全屏模式）时，需禁用侧滑返回，避免页面显示异常。

      ```objectivec
      // 在 ViewController 中添加以下代码。
      // 当设备方向即将发生变化时，系统会调用此方法。
      - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
          if (size.width > size.height) { // 宽度大于高度，表示页面方向为横屏。
              self.navigationController.interactivePopGestureRecognizer.enabled = NO; // 禁用侧滑返回。
          }
          else {
              self.navigationController.interactivePopGestureRecognizer.enabled = YES; // 启用侧滑返回。
          }
      }
      ```
      

   * 当设备在竖屏与横屏间切换时，确保悬浮播放器的方向与应用当前页面方向一致。

      ```objectivec
      // 请在 NavigationController 或 UIViewController 中添加以下代码。
      
      #import <BPLive/BPLive.h>
      @interface ViewController : UIViewController
      //NOTE:获取完整直播间实例时，为 livePullViewController 设置值。
      @property (nonatomic, weak) BDLLivePullViewController *livePullViewController;
      @end
      
      // 当设备方向即将发生变化时，系统会调用此方法。
      - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
          [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
      // 获取应用当前页面方向。
          UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
          if (@available(iOS 13, *)) {
              // 如果使用 self.view.window，当 ViewController 不可见时会返回 nil。因此，请使用 self.navigationController.view.window。
              orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
          } else {
              orientation = UIApplication.sharedApplication.statusBarOrientation;
          }
          // 先展示完整直播间，再展示浮窗播放器时，需调整 livePullViewController.floatingPlayerOrientation，使浮窗播放器方向与应用当前页面方向一致。
          if (self.livePullViewController.isFloating) {
              self.livePullViewController.floatingPlayerOrientation = orientation;
          }
          // 直接展示浮窗播放器时，需调整 floatingPlayer，使浮窗播放器方向与应用当前页面方向一致。
          if (self.floatingPlayer) {
              [self.floatingPlayer setUIOrientation:orientation];
          }
      }
      ```
      


<span id="b9af31ad"></span>
### 离开直播间

当需要观众离开直播间，例如观众无权限观看视频时，可通过以下示例代码实现。

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}
```


<span id="de46cbc8"></span>
### 完整示例代码

以下示例代码以使用 `present` 模式展示的竖屏模式直播间为例，活动 ID（`activityId`）为 `167808997736****`，`token` 为 `JQ****`，认证模式（`authMode`）为 public。你可以根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a> 获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>，并将 <code>Mode</code> 的值设置为 <code>1</code>，以获取公共模式下的授权 token。如需将认证模式更改为自定义，请参见 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#0f3118f8">自定义登录</a>。</div>



```objectivec
- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        BDLLivePullViewController *livePullVC = [[BDLLiveEngine sharedInstance] getLivePullViewController];
        livePullVC.modalPresentationStyle = UIModalPresentationFullScreen;
        livePullVC.actionProvider = self;
        [self configLivePullViewController:livePullVC];
        [self showLivePullViewController:livePullVC];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}

- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}

- (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self presentViewController:livePullVC animated:NO completion:nil];
}

- (void)hideLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self dismissViewControllerAnimated:YES completion:nil];
}
```


<span id="886e9207"></span>
## 完整播放器

如果你有自己的观看页且无需自定义播放器控制界面，可以选择仅集成完整播放器。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/336044b1c120414bb089a238261d94ff~tplv-goo7wpa0wc-image.image) </span>

<span id="76e1141c"></span>
### 加入直播间

使用以下示例代码加入直播间并创建完整播放器。

```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLPlayerView *playerView;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        // Create a player with the control interface, which means it has interactive buttons such as the play button.此处以竖屏模式初始化播放器为例。
        self.playerView =[[BDLPlayerView alloc] initWithPortrait:YES];
        // Set popupSuperView to the current view.SDK 使用此视图显示弹出菜单，例如回放速度和分辨率选择。
        self.playerView.popupSuperView = self.view;
        //  Add the playerView as a subview to the current view.
        [self.view addSubview:self.playerView];
        //  Set the playerView to fill its parent view, namely the current view.
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
     // Process error messages.本例中，错误信息会打印到控制台，用于调试和排查。
        NSLog(@"%@", error.localizedDescription);
    }];
```


<span id="a14bdc9d"></span>
### 离开直播间

当观众退出你的观看页时，使用以下示例代码离开直播间并释放完整播放器的引用。

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="380f8e9b"></span>
### 完整示例代码

以下示例代码以竖屏模式的直播间为例，活动 ID（`activityId`）为`167808997736****`，`token`为`JQ****`，认证模式（`authMode`）为 public。你可以根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a> 获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>，并将 <code>Mode</code> 的值设置为 <code>1</code>，以获取公共模式下的授权 token。</div>



```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLPlayerView *playerView;
@end

- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        self.playerView =[[BDLPlayerView alloc] initWithPortrait:YES];
        self.playerView.popupSuperView = self.view;
        [self.view addSubview:self.playerView];
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="8f276f8b"></span>
## 独立播放器

独立播放器不包含控制界面，即没有播放按钮等交互按钮。如果你有自己的观看页，并且对播放器控制界面有自定义需求，可以选择仅集成独立播放器。集成独立播放器后，你可以添加自定义控制界面。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12a767eab5b045c79c9cd7137b2adebb~tplv-goo7wpa0wc-image.image) </span>

<span id="a8ad5281"></span>
### 加入直播间

使用以下示例代码加入直播间并创建独立播放器。

```objectivec
@interface ViewController () <BDLBasePlayerViewDelegate>
@property (nonatomic, strong) BDLBasePlayerView *playerView;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        //  Create a custom player.
        self.playerView =[[BDLBasePlayerView alloc] init];
        // Set the current ViewController as the delegate of playerView to receive and process playerView events.
        self.playerView.delegate = self;
        // Add the playerView as a subview to the ViewController view.
        [self.view addSubview:self.playerView];
        // Set the playerView to fill its parent view, namely the ViewController view.
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
    // Process error messages.本例中，错误信息会打印到控制台，用于调试和排查。
        NSLog(@"%@", error.localizedDescription);
    }];
    ...
```


<span id="98960cf6"></span>
### 处理代理

你可以处理代理，在以下场景下将相关回调信息传递给你的应用以自定义控制界面：


* 封面图、播放内容、播放状态、视频尺寸或卡顿状态发生变化。

* 进入或退出画中画模式。

* 首帧加载成功。


在以下示例代码中，当视频卡顿状态发生变化时会打印日志信息。

```objectivec
// The video starts to stutter.
- (void)basePlayerViewStallStart:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}

// The video stops stuttering.
- (void)basePlayerViewStallEnd:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}
```


<span id="5193c9b6"></span>
### 离开直播间

当观众退出你的观看页时，使用以下示例代码离开直播间并释放独立播放器的引用。

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="b59c0c4b"></span>
### 完整示例代码

以下示例代码以竖屏模式的直播间为例，活动 ID（`activityId`）为`167808997736****`，`token`为`JQ****`，认证模式（`authMode`）为 public。你可以根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a> 获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>，并将 <code>Mode</code> 的值设置为 <code>1</code>，以获取公共模式下的授权 token。</div>



```objectivec
@interface ViewController () <BDLBasePlayerViewDelegate>
@property (nonatomic, strong) BDLBasePlayerView *playerView;
@end

- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        self.playerView =[[BDLBasePlayerView alloc] init];
        self.playerView.delegate = self;
        [self.view addSubview:self.playerView];
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}

- (void)basePlayerViewStallStart:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}

- (void)basePlayerViewStallEnd:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}
```


<span id="765f75ba"></span>
## 浮窗播放器

浮窗播放器，也称为画中画（PiP），可在直播间页面关闭后通过`pop`或`dismiss`操作显示。

集成完整直播间后，即可使用浮窗播放器。但如果需要先显示浮窗播放器，再显示完整直播间，则必须集成浮窗播放器。例如，观众先进入你的商品详情页查看商品，然后点击浮窗播放器加入完整直播间。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eecf0f7799614561aa635a2eb28ebf66~tplv-goo7wpa0wc-image.image) </span>

<span id="c430d76f"></span>
### 加入直播间

使用以下示例代码加入直播间并显示浮窗播放器。

```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLFloatingPlayer *floatingPlayer;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
       
        // Create the floating player.此处以竖屏模式初始化浮窗播放器为例。
        // 参数值仅影响获取浮窗播放器加载图片及图片尺寸的方法，不影响浮窗播放器的显示。浮窗播放器的视频长宽比与视频一致。
        self.floatingPlayer = [[BDLFloatingPlayer alloc] initWithPortrait:YES];
        // 显示浮窗播放器。此处以在浮窗播放器右上角显示关闭图标为例。
        self.floatingPlayer.delegate = self;
        [self.floatingPlayer showWithCloseButton:YES];
    } failure:^(NSError * _Nonnull error) {
     // 处理错误信息。在此示例中，错误信息会打印到控制台，用于调试和故障排查。
        NSLog(@"%@", error.localizedDescription);
    }];
```


<span id="69016853"></span>
### 离开直播间

使用以下示例代码关闭浮窗播放器并离开直播间。

```objectivec
// 当观众点击浮窗播放器的关闭图标时，关闭浮窗播放器并离开直播间。
- (void)floatingPlayerWillClose:(BDLFloatingPlayer *)floatingPlayer {
    [self leaveLiveRoom]
}

// 关闭浮窗播放器，离开直播间，并释放浮窗播放器的引用，当需要关闭浮窗播放器时。
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.floatingPlayer hide];
    self.floatingPlayer = nil;
}
```


<span id="1252ec6b"></span>
### 自动旋转浮窗播放器方向

使用以下示例代码，在设备方向于竖屏和横屏间切换时，使浮窗播放器方向与应用当前页面方向保持一致。

```objectivec
// 系统在设备方向即将发生变化时调用此方法。
- (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
    [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
// 获取应用当前页面方向。
    UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
    if (@available(iOS 13, *)) {
        // 如果使用 self.view.window，当 ViewController 不可见时会返回 nil。因此，使用 self.navigationController.view.window替代。
        orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
    } else {
        orientation = UIApplication.sharedApplication.statusBarOrientation;
    }
    // 保持浮窗播放器的方向与应用当前页面方向一致。
    [self.floatingPlayer setUIOrientation:orientation];
}
```


<span id="a5a967d5"></span>
### 返回完整直播间后继续播放视频

为确保观众点击浮窗播放器返回完整直播间时能够持续回放，请使用以下示例代码。

```objectivec
// MARK: - BDLFloatingPlayerDelegate
// This callback is triggered when viewers tap the floating player.
- (void)floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
    // Hide the floating player.
    [self.floatingPlayer hide];
    // 获取浮窗播放器中的 basePlayerView。
    BDLBasePlayerView *basePlayerView = [floatingPlayer removeBasePlayerView];
    // Create the full-featured live room and pass the obtained basePlayerView.
    BDLLivePullViewController *vc = [[BDLLiveEngine sharedInstance] getLivePullViewControllerWithBasePlayerView:basePlayerView];
    vc.delegate = self;
    vc.actionProvider = self;
    self.livePullViewController = vc;
    self.floatingPlayer = nil;
    // 根据需要选择使用 push 或 present 模式展示完整直播间。
    [self.navigationController pushViewController:self.livePullViewController animated:YES];
}
```


<span id="ef5b1cff"></span>
### 完整示例代码

以下示例代码以竖屏模式下的直播间为例，活动 ID（`activityId`）为`167808997736****`，`token`为`JQ****`，认证模式（`authMode`）为 public。你可以根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a>或<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a>以获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>并将<code>Mode</code>的值设置为<code>1</code>，以获取公共模式下的授权令牌。</div>



```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLFloatingPlayer *floatingPlayer;
@end


- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        self.floatingPlayer = [[BDLFloatingPlayer alloc] initWithPortrait:YES];
        self.floatingPlayer.delegate = self;
        [self.floatingPlayer showWithCloseButton:YES];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}

- (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
    [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
    
    UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
    if (@available(iOS 13, *)) {
        orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
    } else {
        orientation = UIApplication.sharedApplication.statusBarOrientation;
    }
    [self.floatingPlayer setUIOrientation:orientation];
}

- (void)floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
    [self.floatingPlayer hide];
    BDLBasePlayerView *basePlayerView = [floatingPlayer removeBasePlayerView];
    BDLLivePullViewController *vc = [[BDLLiveEngine sharedInstance] getLivePullViewControllerWithBasePlayerView:basePlayerView];
    vc.delegate = self;
    vc.actionProvider = self;
    self.livePullViewController = vc;
    self.floatingPlayer = nil;
    [self.navigationController pushViewController:self.livePullViewController animated:YES];
}
```
