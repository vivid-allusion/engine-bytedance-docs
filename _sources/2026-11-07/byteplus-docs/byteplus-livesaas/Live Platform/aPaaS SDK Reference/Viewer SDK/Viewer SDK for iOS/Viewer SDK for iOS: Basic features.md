---
title: "Viewer SDK for iOS: Basic features"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features"
---

This topic describes how to integrate the basic features of the Viewer SDK for iOS, including how to integrate a full\-featured live room, a default player, a custom player, and a floating player.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, viewers can only join one live room at a time.</div>


<span id="59273a71"></span>
## Prerequisites

Complete the first 5 steps in [Integrating the Viewer SDK for iOS](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios).

<span id="98b7076d"></span>
## Features

This topic describes how to integrate the following features.


* [Full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features#f2a7c3c8)

* [Default player](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features#886e9207)

* [Custom player](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features#8f276f8b)

* [Floating player](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features#765f75ba)


<span id="f2a7c3c8"></span>
## Full\-featured live room

A full\-featured live room includes all the functional modules of a BytePlus Live live room, making it easier and more convenient to integrate than modules. Unless you have special requirements, we recommend that you integrate a full\-featured live room.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0572b0440b4404dbdb4ef127dc6e574~tplv-goo7wpa0wc-image.image) </span>

For more information on the features supported by a full\-featured live room, see [Feature comparison between SaaS and aPaaS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas).

<span id="bb63491d"></span>
### Joining the live room

The following sample code allows viewers to join the full\-featured live room and displays the full\-featured live room page in the app.

```objectivec
...
[[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                 success:^{
    // 1. Get the full-featured live room instance. 
    BDLLivePullViewController *livePullVC = [[BDLLiveEngine sharedInstance] getLivePullViewController];
    // 2. (Optional) Set the modalPresentationStyle, which is the mode of displaying the live room. Here, display the live room in full-screen mode as an example.
    // If you choose to display the live room using the UINavigationController push mode, or to display the live room using the system's default mode, no additional configuration is needed. 
    livePullVC.modalPresentationStyle = UIModalPresentationFullScreen;
    // 3. Set the actionProvider. Here, "self" is used as an example to respond to live room events such as display and hide.
    livePullVC.actionProvider = self;
    // 4. (Optional) Configure the live room.
    [self configLivePullViewController:livePullVC];
    // 5. Display the live room. Here, display the live room using present mode as an example. 
    // To display the live room using the UINavigationController push mode, see Displaying the live room using push mode.
    [self showLivePullViewController:livePullVC];
} failure:^(NSError * _Nonnull error) {
    // Process error messages. In this example, error messages are printed to the console for debugging and troubleshooting.
    NSLog(@"%@", error.localizedDescription);
}];

/// Configure the live room, including customizing the UI. You can copy the feature code into this method to run.
- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}

/// 6. Methods required for implementing actionProvider. 
/// 6.1 The method to display the live room.
/// Display the live room. SDK calls this method when you need to display the full-featured live room. Here, display the live room using present mode as an example. 
/// To display the live room using the UINavigationController push mode, see Displaying the live room using push mode. 
- (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self presentViewController:livePullVC animated:NO completion:nil];
}

/// 6.2 The method to hide the live room. 
/// Hide the live room. SDK calls this method when you need to hide the full-featured live room.
- (void)hideLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self dismissViewControllerAnimated:YES completion:nil];
}
```


<span id="d649b214"></span>
### Displaying the live room using push mode

To display a full\-featured live room using the `UINavigationController` `push` mode, you can refer to the following process.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only SDK 1.29.1 and above support <code>push</code> mode.</div>



1. After getting the full\-featured live room instance, configure the logic of displaying the floating player, namely the In\-App picture\-in\-picture (PiP).

   1. Set whether to display the floating player.

      ```objectivec
      /// When the live room status changes, this callback is triggered and passes the following information to the app: the full-featured live room instance, live room status, and whether the live room page is closed.
      livePullVC.config.shouldShowInAppPipIfAvailable = ^BOOL(BDLLivePullViewController * _Nonnull viewController, BDLActivityStatus status, BOOL isClose) {
          /// Determine whether to display the floating player based on the live room status and whether the live room page is closed. 
          switch (status) {
              case BDLActivityStatusLive: // If the live room status is Live, execute the following logic.
                  return isClose ? YES : NO; // In this example, return YES when the value of isClose is YES, and return NO when the value of isClose is NO. In other words, when the live room page is closed using the pop or dismiss action, the floating player is displayed. When new pages such as the product detail page are displayed using the push or present mode, the floating player is not displayed.
              case BDLActivityStatusReplay: // If the live room status is Playback, execute the following logic. 
                  return isClose ? YES : NO; // In this example, return YES when the value of isClose is YES, and return NO when the value of isClose is NO. In other words, when the live room page is closed using the pop or dismiss action, the floating player is displayed. When new pages such as the product detail page are displayed using the push or present mode, the floating player is not displayed.
              case BDLActivityStatusPreview: //  If the live room status is Preview and the preview is playing, execute the following logic. 
                  return isClose ? YES : NO; // In this example, return YES when the value of isClose is YES, and return NO when the value of isClose is NO. In other words, when the live room page is closed using the pop or dismiss action, the floating player is displayed. When new pages such as the product detail page are displayed using the push or present mode, the floating player is not displayed.
              default:
                  return NO; // The floating player is not displayed. Normally, this logic is not triggered, but to avoid errors, this default return value must be set.
          }
      };
      ```
      

   2. Configure whether to automatically close the floating player that is being displayed when `viewDidAppear`, that is, when the view corresponding to the full\-featured live room is displayed.

      Use the following sample code to automatically close the floating player that is being displayed.

      ```objectivec
      livePullVC.config.autoCloseFloatingPlayerWhenAppear = YES;
      ```
      

      If the value is `NO`, then the method to close the floating player must be called at an appropriate time.

      Use the following sample code to close the floating player and simultaneously display the full\-featured live room.

      ```objectivec
      [livePullVC hideFloatingPlayerIfAvailable:YES]
      ```
      

2. Display the full\-featured live room.

   The sample code is as follows.

   ```objectivec
   - (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
       if (self.livePullVC.navigationController) { // When new pages such as the product detail page are displayed using the push or present mode, the SDK closes the floating player, does not display the full-featured live room, and does not leave the live room after viewers tap the close button of the floating player.
           [self.navigationController popToViewController:livePullVC animated:YES]; // Use pop action to remove other pages (ViewController) displayed over the full-featured live room.
           return;
       }
       [self.navigationController pushViewController:livePullVC animated:YES]; // Use push mode to display the full-featured live room.
   }
   ```
   

3. (Optional) If you return `YES` when the value of `isClose` is `NO` in step 1.a, namely the floating player is displayed when new pages such as the product detail page are displayed using the `push` or `present` mode, you need to modify whether to execute the default tap behavior of the close button of the floating player.

   The sample code is as follows.

   ```objectivec
       __weak typeof(self) weakSelf = self;
       livePullVC.onFloatingPlayerCloseTapped = ^BOOL(BDLLivePullViewController * _Nonnull viewController, BDLFloatingPlayer * _Nonnull floatingPlayer) {
           if (viewController.navigationController) {
               // When you use the push or present mode to display new pages such as the product detail page, the SDK closes the floating player, does not display the full-featured live room, and does not leave the live room after viewers tap the close button of the floating player.
               [viewController hideFloatingPlayerIfAvailable:NO];
               return NO;
           }
           else {
               // When the live room page is closed using the pop or dismiss action, the SDK executes the default tap behavior after viewers tap the close button of the floating player: close the floating player and leave the live room.
               return YES;
           }
       };
   ```
   

4. (Optional) Except for full\-screen mode, the full\-featured live room can only be displayed in portrait orientation. Complete the following configuration if the app's pages support displaying in landscape orientation.

   * When displaying the full\-featured live room page, make sure the previous page (app‘s page displayed before entering the live room page) only supports portrait orientation.

      The sample code is as follows.

      ```objectivec
      // Add the following code in the ViewController.
      @interface ViewController : UIViewController
      @property (nonatomic, assign) BOOL visible;
      @end
      
      // When viewDidAppear, that is, when the view corresponding to the previous page is displayed, set visible to YES to indicate that the current view is visible. 
      - (void)viewDidAppear:(BOOL)animated {
          [super viewDidAppear:animated];
          self.visible = YES;
      }
      // When viewDidDisappear, that is, when the view corresponding to the previous page disappears, set visible to NO to indicate that the current view is not visible. 
      - (void)viewDidDisappear:(BOOL)animated {
          [super viewDidDisappear:animated];
          self.visible = NO;
      }
      
      // Specify the page orientations supported by the current view. 
      - (UIInterfaceOrientationMask)supportedInterfaceOrientations {
          if (!self.visible) { // When the current view is not visible, only the portrait orientation is supported in the live room to avoid display anomalies caused by side-swipe return to the previous page.
              return UIInterfaceOrientationMaskPortrait;
          }
          // Page orientations supported by the previous page when the current view is visible. In this example, the previous page supports all orientations except for UpsideDown.
          return UIInterfaceOrientationMaskAllButUpsideDown;
      }
      ```
      

   * When the live room page is displayed in landscape orientation, that is, in full\-screen mode, disable the side\-swipe return to prevent page display anomalies.

      ```objectivec
      // Add the following code in the ViewController.
      // This method is called by the system when the device orientation is about to change.
      - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
          if (size.width > size.height) { // Width is greater than height, indicating the page orientation is landscape.
              self.navigationController.interactivePopGestureRecognizer.enabled = NO; // Disable side-swipe return.
          }
          else {
              self.navigationController.interactivePopGestureRecognizer.enabled = YES; // Enable side-swipe return.
          }
      }
      ```
      

   * Make sure that the floating player's orientation matches the app's current page orientation when the device orientation changes between portrait and landscape.

      ```objectivec
      // Add the following code in the NavigationController or UIViewController.
      
      #import <BPLive/BPLive.h>
      @interface ViewController : UIViewController
      //NOTE: Set a value to livePullViewController when obtaining the full-featured live room instance.
      @property (nonatomic, weak) BDLLivePullViewController *livePullViewController;
      @end
      
      // This method is called by the system when the device orientation is about to change.
      - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
          [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
      // Get the current page orientation of the app.
          UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
          if (@available(iOS 13, *)) {
              // If you use self.view.window, nil is returned when the ViewController is not visible. Therefore, use self.navigationController.view.window instead.
              orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
          } else {
              orientation = UIApplication.sharedApplication.statusBarOrientation;
          }
          // When displaying the full-featured live room first and then the floating player, adjust livePullViewController.floatingPlayerOrientation to match the floating player's orientation with the app's current page orientation.
          if (self.livePullViewController.isFloating) {
              self.livePullViewController.floatingPlayerOrientation = orientation;
          }
          // When directly displaying the floating player, adjust the floatingPlayer to match the floating player's orientation with the app's current page orientation.
          if (self.floatingPlayer) {
              [self.floatingPlayer setUIOrientation:orientation];
          }
      }
      ```
      


<span id="b9af31ad"></span>
### Leaving the live room

When you need viewers to leave the live room, for example, when viewers do not have permission to watch the videos, you can implement this with the following sample code.

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}
```


<span id="de46cbc8"></span>
### Complete sample code

The following sample code takes a live room in portrait mode displayed using `present` mode as an example, with the activity ID (`activityId`) as `167808997736****`, the `token` as `JQ****`, and the authentication mode (`authMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode. To change the authentication mode to custom, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#0f3118f8">Custom login</a>.</div>



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
## Default player

If you have your own viewing page and do not need to customize the player control interface, you can choose to integrate only the default player.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/336044b1c120414bb089a238261d94ff~tplv-goo7wpa0wc-image.image) </span>

<span id="76e1141c"></span>
### Joining the live room

Use the following sample code to join the live room and create a default player.

```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLPlayerView *playerView;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        // Create a player with the control interface, which means it has interactive buttons such as the play button. Here, initialize the player in portrait mode as an example. 
        self.playerView =[[BDLPlayerView alloc] initWithPortrait:YES];
        // Set popupSuperView as the current view. By default, the SDK internally implements pop-up effects such as playback speed selection and resolution selection. These pop-up windows are added over the popupSuperView.  
        self.playerView.popupSuperView = self.view;
        //  Add the playerView as a subview to the current view. 
        [self.view addSubview:self.playerView];
        //  Set the playerView to fill its parent view, namely the current view. 
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
     // Process error messages. In this example, error messages are printed to the console for debugging and troubleshooting.
        NSLog(@"%@", error.localizedDescription);
    }];
```


<span id="a14bdc9d"></span>
### Leaving the live room

When viewers exit your viewing page, use the following sample code to leave the live room and release the reference to the default player.

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="380f8e9b"></span>
### Complete sample code

The following sample code takes a live room in portrait mode as an example, with the activity ID (`activityId`) as `167808997736****`, the `token` as `JQ****`, and the authentication mode (`authMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode.</div>



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
## Custom player

A custom player does not include the control interface, which means it does not have interactive buttons such as the play button. If you have your own viewing page and custom requirements for the player's control interface, you can choose to integrate only the custom player. After integrating the custom player, you can add your own custom control interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12a767eab5b045c79c9cd7137b2adebb~tplv-goo7wpa0wc-image.image) </span>

<span id="a8ad5281"></span>
### Joining the live room

Use the following sample code to join the live room and create a custom player.

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
    // Process error messages. In this example, error messages are printed to the console for debugging and troubleshooting.
        NSLog(@"%@", error.localizedDescription);
    }];
    ...
```


<span id="98960cf6"></span>
### Processing the delegate

You can process the delegate to pass relevant callback information to your app for customizing the control interface in the following scenarios:


* Changes in cover image, playing content, playing status, video size, or stuttering status.

* Entering or exiting PiP mode.

* The first frame successfully loads.


In the following sample code, a log message is printed when the video stuttering status changes.

```objectivec
// The video starts to stutter.
- (void)basePlayerViewStallStart:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}

// The video stops stuttering
- (void)basePlayerViewStallEnd:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}
```


<span id="5193c9b6"></span>
### Leaving the live room

When viewers exit your viewing page, use the following sample code to leave the live room and release the reference to the custom player.

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="b59c0c4b"></span>
### Complete sample code

The following sample code takes a live room in portrait mode as an example, with the activity ID (`activityId`) as `167808997736****`, the `token` as `JQ****`, and the authentication mode (`authMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode.</div>



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
## Floating player

The floating player, namely the In\-App PiP, can be displayed after the live room page is closed using the `pop` or `dismiss` action.

After integrating the full\-featured live room, the floating player is available. However, if you need to display the floating player first and then the full\-featured live room, you must integrate the floating player. For example, viewers enter your product detail page first to view the product, and then tap the floating player to join the full\-featured live room.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eecf0f7799614561aa635a2eb28ebf66~tplv-goo7wpa0wc-image.image) </span>

<span id="c430d76f"></span>
### Joining the live room

Use the following sample code to join the live room and display the floating player.

```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLFloatingPlayer *floatingPlayer;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
       
        // Create the floating player. Here, initialize the floating player in portrait mode as an example. 
        // The parameter value only affects the methods for getting the loading image and the image size of the floating player, without affecting the display of the floating player. The aspect ratio of the floating player is the same as that of the video. 
        self.floatingPlayer = [[BDLFloatingPlayer alloc] initWithPortrait:YES];
        // Display the floating player. Here, display the close icon in the upper-right corner of the floating player as an example. 
        self.floatingPlayer.delegate = self;
        [self.floatingPlayer showWithCloseButton:YES];
    } failure:^(NSError * _Nonnull error) {
     // Process error messages. In this example, error messages are printed to the console for debugging and troubleshooting.
        NSLog(@"%@", error.localizedDescription);
    }];
```


<span id="69016853"></span>
### Leaving the live room

Use the following sample code to close the floating player and leave the live room.

```objectivec
// Close the floating player and leave the live room when viewers tap the close icon of the floating player.
- (void)floatingPlayerWillClose:(BDLFloatingPlayer *)floatingPlayer {
    [self leaveLiveRoom]
}

// Close the floating player, leave the live room, and release the reference to the floating player when you need to close the floating player.
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.floatingPlayer hide];
    self.floatingPlayer = nil;
}
```


<span id="1252ec6b"></span>
### Automatically rotating the floating player's orientation

Use the following sample code to keep the floating player's orientation the same as the app's current page orientation when the device orientation changes between portrait and landscape.

```objectivec
// This method is called by the system when the device orientation is about to change.
- (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
    [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
// Get the current page orientation of the app.        
    UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
    if (@available(iOS 13, *)) {
        // If you use self.view.window, nil is returned when the ViewController is not visible. Therefore, use self.navigationController.view.window instead. 
        orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
    } else {
        orientation = UIApplication.sharedApplication.statusBarOrientation;
    }
    // Keep the floating player's orientation the same as the app's current page orientation.
    [self.floatingPlayer setUIOrientation:orientation];
}
```


<span id="a5a967d5"></span>
### Continuing to play the video after returning to the full\-featured live room

After viewers tap the floating player to return to the full\-featured live room, to avoid interrupting the playing of the video, use the following sample code to make sure that the video can continue to play.

```objectivec
// MARK: - BDLFloatingPlayerDelegate
// This callback is triggered when viewers tap the floating player.
- (void)floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
    // Hide the floating player. 
    [self.floatingPlayer hide];
    // Get the basePlayerView in the floating player. 
    BDLBasePlayerView *basePlayerView = [floatingPlayer removeBasePlayerView];
    // Create the full-featured live room and pass the obtained basePlayerView. 
    BDLLivePullViewController *vc = [[BDLLiveEngine sharedInstance] getLivePullViewControllerWithBasePlayerView:basePlayerView];
    vc.delegate = self;
    vc.actionProvider = self;
    self.livePullViewController = vc;
    self.floatingPlayer = nil;
    // Select to display the full-featured live room using push or present mode as needed. 
    [self.navigationController pushViewController:self.livePullViewController animated:YES];
}
```


<span id="ef5b1cff"></span>
### Complete sample code

The following sample code takes a live room in portrait mode as an example, with the activity ID (`activityId`) as `167808997736****`, the `token` as `JQ****`, and the authentication mode (`authMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode.</div>



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
