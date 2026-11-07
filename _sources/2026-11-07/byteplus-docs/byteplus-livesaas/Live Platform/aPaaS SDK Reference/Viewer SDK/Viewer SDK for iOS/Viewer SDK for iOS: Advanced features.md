---
title: "Viewer SDK for iOS: Advanced features"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features"
---

This topic describes how to integrate the advanced features of the Viewer SDK for iOS. You can implement complex features as needed based on your actual business requirements.

<span id="ca684b73"></span>
## Prerequisites


* Complete the first 5 steps in [Integrating the Viewer SDK for iOS](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios).

* The following integrations are required as needed.

   * Integrate basic features to customize the video scaling mode. For more information, see [Viewer SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features).

   * Integrate the full\-featured live room to implement other advanced features as described in this topic. For more information, see [Full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-basic-features#f2a7c3c8).


<span id="7b020e01"></span>
## Features

This topic describes how to integrate the following features.


* [Custom login](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#0f3118f8)

* [Custom redirection logic](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#971bbcde)

   * [Product card displayed under the menu](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#cbaa61a3)

   * [Header ad](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#19643834)

   * [In-page ad](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#dd1a11eb)

   * [Floating ad or floating product card](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#d100ba3a)

   * [Host account](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#27ae5bd9)

   * [URL in the comment area under the menu for chat interaction](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#80b34b11)

   * [URL in the pinned comment](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#b68c3584)

* [Customizing the UI](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#0269f8d1)

   * [Video scaling mode](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#a625195e)

   * [Icon to close the full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#eb320cbc)

   * [Floating interaction tools](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#ee6cf81c)

   * [Height of the menu for product cards](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-advanced-features#8ea12ced)


<span id="0f3118f8"></span>
## Custom login

If you need viewers to log in to your app first and then watch the live stream, participate in comments and interactions, and more, you can choose the custom login method. Viewers can use their identity information in your app to join the live room.

You can select the login timing of viewers in your app as needed.


* Viewers log in to your app first, and then join the live room.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46a7b800924a41d7a4f88933f07df41f~tplv-goo7wpa0wc-image.image) </span>

   1. After viewers log in to the app and join the live room, you need to call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `2` to get the authorization token.

   2. After getting the token, call the SDK's `joinLiveRoomWithActivity:success:failure:` method to join the live room.

   The sample code is as follows.

   ```objectivec
   - (void)joinLiveRoom {    
       BDLActivity *activity = [[BDLActivity alloc] init];
       activity.activityId = @(167808997736****); // The activity ID of the live room.
       activity.token = @"ak3T%2FdaGJDL5zSFD7%2F1GPGP****"; // The authorization token when the value of Mode is 2.
       activity.isPortrait = YES; // Live room in portrait mode. 
       activity.authMode = BDLActivityAuthModeCustom; // Custom mode.
       [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity success:^{
           // Join the live room successfully.
       } failure:^(NSError * _Nonnull error) {
           // Failed to join the live room.
       }];
   }
   ```
   

* Viewers first join the live room to watch the live stream, view comments, and more. The login process is triggered when they perform operations such as participating in comments and interactions, and then the authentication mode changes from public to custom.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the parameter value of <code>nickname</code> in the method <code>setNickname:complete:</code> is not empty, no methods of <code>BDLLoginProvider</code> can be triggered.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edc06578a28c4ab89f8d9c120fd31a38~tplv-goo7wpa0wc-image.image) </span>

   1. Viewers first join the live room in public mode.

   2. You need to implement the method of getting the authorization token in public mode. Then, call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `1` to get the token.

   3. Set the `loginProvider` of `BDLLiveEngine`, that is, the proxy for logging in to the live room in custom mode.

      The sample code is as follows.

      ```objectivec
      ...
      [[BDLLiveEngine sharedInstance] setLoginProvider:self];
      ...
      ```
      

   4. Call the SDK's `joinLiveRoomWithActivity:success:failure:` method to join the live room.

   5. When viewers perform the following operations that require user information, the custom login process of the app is triggered:

      * Tap the comment text box under the menu for chat interaction

      * Like a comment

      * Reward hosts with gifts

      * Tap the book button to book the live stream

      * Quizzes

      * Votes

      * Lucky draws

      * Non\-Anonymous questionnaires

   6. The SDK calls the `loginWithActivity:completion:` method to allow viewers to log in to the live room through your app. You need to implement the method of getting the authorization token in custom mode. Then, call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `2` to get the token when viewers complete the custom login. After getting the token, you need to call the `completion` method to pass the token to the SDK.

      The sample code is as follows.

      ```objectivec
      - (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion {
          // Replace the getToken: method with the method you use to get the authorization token.
          [self getToken:^(NSString *token) {
              completion(token);
          }];
      }
      ```
      

   7. The SDK requests viewer information from BytePlus Live by using the token.

   8. After verifying that the token is valid, BytePlus Live passes the viewer information to the SDK. If the token verification fails or the token is empty, BytePlus Live passes the error message to the SDK.

   9. The SDK calls the `loginComplete:error:` method to notify the app whether the custom login process is successful.

      The sample code is as follows.

      ```objectivec
      - (void)loginComplete:(BDLActivity *)activity error:(NSError *)error {
          if (!error) {
              NSLog(@"Custom login is successful");
          }
          else {
              NSLog(@"Custom login failed %@", error.localizedDescription);
          }
      }
      ```
      

   10. (Optional) If the live room page is closed during the viewer login process, the SDK triggers the `cancelLoginWithActivity:` callback, and you can cancel the custom login process as needed.

      The sample code is as follows.

      ```objectivec
      - (void)cancelLoginWithActivity:(BDLActivity *)activity {
      // After the cancelLoginWithActivity: callback is triggered, cancel the custom login process as needed.
          NSLog(@"If the live room page is closed during the login process, you can cancel the login process as needed in the app");
      }
      ```
      


<span id="971bbcde"></span>
## Custom redirection logic

The SDK executes the default redirection behavior when viewers tap the following items in the live room:


* Product card displayed under the menu

* Floating product card

* Header ad

* In\-page ad

* Floating ad

* Host account

* URL in the comment area under the menu for chat interaction

* URL in the pinned comment


You can intercept the SDK's default redirection behavior to implement custom redirection logic after viewers tap these items. This allows you to tailor the page redirection behavior based on specific scenarios or requirements, enhancing the user experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to configure the product card, header ad, in\-page ad, floating ad, host account, menu for chat interaction, and pinned comment on the BytePlus Live console, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream">Managing product cards</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-logo-and-ads">Adding ads</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account">Associating a host account to a live room</a>, and <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area">Managing the chat area</a>.</div>


You can add the relevant code in `configLivePullViewController:` to get information such as the tapped URL and customize the redirection logic.

```objectivec
- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}
```


<span id="cbaa61a3"></span>
### Product card displayed under the menu

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d5f66445f134fdcbfcce779cb957bea~tplv-goo7wpa0wc-image.image) </span>

The `cardViewTappedBlock` callback is triggered when viewers tap the product card under the menu, passing the following information to the app: the product card URL and whether the product detail page is displayed on the floating layer.

The sample code is as follows.

```objectivec
livePullVC.config.customShoppingCardController = ^(BDLLivePullViewController * _Nonnull viewController, BDLShoppingCardController * _Nonnull shoppingCardController) {
    shoppingCardController.customizeShoppingCardView = ^__kindof BDLBaseView * _Nullable(BDLShoppingCardController * _Nonnull controller, BDLShoppingCardView * _Nonnull shoppingCardView) {
        shoppingCardView.cardViewTappedBlock = ^(NSString * _Nullable urlStr, BOOL enableFloating) {
        // After triggering the cardViewTappedBlock callback, execute the custom redirection logic for the product card under the menu.
            NSLog(@"%@ %d", urlStr, enableFloating);
        };
        return shoppingCardView;
    };
};
```


<span id="19643834"></span>
### Header ad

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496a3e71f2244d44910d5c2f125fb275~tplv-goo7wpa0wc-image.image) </span>

The `livePullViewController:didClickHeaderAd:floatingEnable:` callback is triggered after viewers tap the header ad, passing the following information to the app: the embedded link for the header ad and whether the ad page is displayed on the floating layer.

The sample code is as follows.

```objectivec
- (void)livePullViewController:(BDLLivePullViewController *)livePullVC didClickHeaderAd:(NSString *)url floatingEnable:(BOOL)floatingEnable {
// After triggering the livePullViewController:didClickHeaderAd:floatingEnable: callback, execute the custom redirection logic for the header ad.
    NSLog(@"%@ %d", url, floatingEnable);
}
```


<span id="dd1a11eb"></span>
### In\-page ad

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b62ff8e729444d4989849130571a2e89~tplv-goo7wpa0wc-image.image) </span>

The `viewTappedBlock` callback is triggered after viewers tap the in\-page ad, passing the following information to the app: the current `BDLPageAdView` instance, ad\-related information, and whether the ad page is displayed on the floating layer.

The sample code is as follows.

```objectivec
livePullVC.config.customizePageAdView = ^__kindof BDLBaseView * _Nullable(BDLLivePullViewController *viewController, BDLPageAdView * _Nonnull view) {
    view.viewTappedBlock = ^(BDLPageAdView * _Nonnull view, BDLAdvertisementModel * _Nonnull ad, BOOL isFloatingEnable) {
    // After triggering the viewTappedBlock callback, execute the custom redirection logic for the in-page ad.
        NSLog(@"%@ %d", ad.advertisementRedirectUrl, isFloatingEnable);
    };
    return view;
};
```


<span id="d100ba3a"></span>
### Floating ad or floating product card


<Tabs>
<Tab zoneid="fuzmDhayFh" title="Floating ad">
<TabTitle>Floating ad</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f1e0d8440cc41b1b5bc362e5f99c6c4~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="uYOVsfd0RD" title="Floating product card">
<TabTitle>Floating product card</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87da2c3522a945b284b1c7ed4f89491f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


The `openUrlBlock` callback is triggered after viewers tap the floating ad or floating product card, passing the following information to the app: the floating window controller, the URL for the floating ad or floating product card, and whether the ad page or product detail page is displayed on the floating layer.

The sample code is as follows.

```objectivec
livePullVC.config.customFloatingController = ^(BDLLivePullViewController * _Nonnull viewController, BDLFloatingController * _Nonnull floatingController) {
    
    floatingController.openUrlBlock = ^(BDLFloatingController * _Nonnull floatingController, NSURL * _Nonnull url, BOOL isFloatingEnable) {
    // After triggering the openUrlBlock callback, execute the custom redirection logic for the floating ad or floating product card.
        NSLog(@"url: %@ isFloatingEnable:%d", url, isFloatingEnable);
    };
};
```


<span id="27ae5bd9"></span>
### Host account

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893f6480223a44eb98e1600506a1fdbd~tplv-goo7wpa0wc-image.image) </span>

The `viewTappedBlock` callback is triggered after viewers tap the avatar or name of the host account, passing the embedded link for the host account to the app.

The sample code is as follows.

```objectivec
livePullVC.config.customizeAccountView = ^__kindof BDLBaseView * _Nullable(BDLLivePullViewController *viewController, BDLBusinessAccountView * _Nonnull view) {
    view.viewTappedBlock = ^(NSString * _Nullable urlStr) {
     // After triggering the viewTappedBlock callback, execute the custom redirection logic for the host account.
        NSLog(@"%@", urlStr);
    };
    return view;
};
```


<span id="80b34b11"></span>
### URL in the comment area under the menu for chat interaction

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f36cd2c7f759428ca62815b51ee9a6b5~tplv-goo7wpa0wc-image.image) </span>

By default, only URLs in the host's comments are tappable. You can use the following method to set URLs in viewers' comments as tappable.

```objectivec
[[[BDLLiveEngine sharedInstance] liveRoomConfiguration] commentViewConfig].enableAudienceURLTap = YES;
```


The `urlClickBlock` callback is triggered after viewers tap the URL in the comment area under the menu for chat interaction (not the URL in the pinned comment), passing the following information to the app: the current `BDLCommentBaseView` instance, comment\-related information, and the URL in the comment.

The sample code is as follows.

```objectivec
void (^customizeCommentView)(BDLCommentView *view) = ^(BDLCommentView *view) {
    view.urlClickBlock = ^(__kindof BDLCommentBaseView * _Nonnull commentView, BDLCommentModel * _Nonnull comment, NSURL * _Nonnull url) {
       // After triggering the urlClickBlock callback, execute the custom redirection logic for the URL in the comment area. 
            NSLog(@"%@ %@", url, comment);
    };
};

// Call urlClickBlock in the comment area under the menu for chat interaction of a live room in portrait mode.
livePullVC.config.customizeCommentView = ^(BDLLivePullViewController * _Nonnull viewController, BDLCommentView * _Nonnull view) {
    customizeCommentView(view);
};

// Call urlClickBlock in the comment area under the menu for chat interaction of a live room in landscape mode.
// Use this method together with other customizeMenuBarView methods to avoid overwriting configurations.
livePullVC.config.customizeMenuBarView = ^(BDLLivePullViewController * _Nonnull viewController, BDLMenuBarView * _Nonnull view) {
    view.customizeCommentView = ^(BDLMenuBarView * _Nonnull view, BDLCommentView * _Nonnull commentView) {
        customizeCommentView(commentView);
    };
};
```


<span id="b68c3584"></span>
### URL in the pinned comment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b09965eb9a2c4f188485ab86c28b4bc6~tplv-goo7wpa0wc-image.image) </span>

After viewers tap the pinned comment, a pop\-up window displaying the pinned comment appears. The `urlClickBlock` callback is triggered after viewers tap the URL in the pop\-up window, passing the URL to the app.

The sample code is as follows.

```objectivec
livePullVC.config.customizeAlertController = ^__kindof UIViewController * _Nonnull(BDLLivePullViewController * _Nonnull viewController, BDLAlertController * _Nonnull controller) {
    __weak typeof(self) weakSelf = self;
    __weak BDLAlertController * weakController = controller;
    controller.urlClickBlock = ^(NSURL * _Nonnull url) {
        [weakController dismissAlertControllerAnimated:YES completion:^{
        // After triggering the urlClickBlock callback, execute the custom redirection logic for the URL in the pinned comment.       
            NSLog(@"%@", url);
        }];
    };
    return controller;
};
```


<span id="0269f8d1"></span>
## UI customization

You can customize the UI on the viewing page using the following methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The priority of the SDK's UI customization is higher than that of the customization on the BytePlus Live console or by calling server\-side APIs. For example, if you customize the icon image for liking a live room both through the SDK's <code>thumbUpButtonImage</code> method and the console, the icon image displayed on the viewing page is customized by the <code>thumbUpButtonImage</code> method.</div>


<span id="cc47b661"></span>
### Customization methods

<span id="41a574d3"></span>
#### By using properties with the prefix `customize`

You can get the `BDLLivePullViewController` instance by calling the `getLivePullViewController` method in the `joinLiveRoomWithActivity:success:failure:` success callback. Then, use the `config` property of `BDLLivePullViewController` to customize `BDLLivePullViewController`. `BDLLivePullViewControllerConfig` provides blocks with the prefix `customize`. You can get the corresponding view and customize the view properties based on the block parameters.


* For blocks with return values, after customizing the view properties, you can return the view to the SDK, or replace the view with your own implementation and return the instance of your own implementation to the SDK.

* For blocks without return values, you can only customize the view properties.


Take the `customizeAccountView` property as an example.

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeAccountView)(BDLLivePullViewController *viewController, BDLBusinessAccountView *view);
```


You can use the `customizeAccountView` property to customize the UI of the host account feature. For example, to customize all the properties of the host account avatar except for rounded corners, image, and `frame`, you can use the `customizeAccountView` property to get `BDLBusinessAccountView` and then configure `avatarImageView`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you use this method, we recommend that you configure the UI after viewers join the live room successfully, but before the live room page is displayed.</div>


* <div data-tips="true" data-tips-type="tip">To hide a view, return <code>nil</code> to the SDK, or disable the corresponding feature on the BytePlus Live console. We do not recommend hiding a view using the <code>hidden</code> property, as this may be overwritten by the configuration on the console.</div>


* <div data-tips="true" data-tips-type="tip">Due to the use of auto layout inside a view, we do not recommend customizing the position properties of the view unless specifically stated. To customize the position of the view, we recommend that you implement your own view and then replace the default implementation with your implementation.</div>


* <div data-tips="true" data-tips-type="tip">A UI control cannot be configured to be displayed all the time. In other words, you cannot disable a feature of certain UI controls on the BytePlus Live console and then configure these UI controls to be visible by using the SDK.</div>


* <div data-tips="true" data-tips-type="tip">Customizing multilingual texts is supported unless specifically stated. Separate texts in different languages with <code>|</code> and SDK can get the text in the corresponding language. The format is as follows:</div>


   <div data-tips="true" data-tips-type="tip"><code>简体中文|English|日本語|繁體中文|한국어|ภาษาไทย|Tiếng Việt|اللغة العربية|Türkçe|Español|Bahasa Indonesia|Português|Русский язык</code>   </div>
   


<span id="beaa7af4"></span>
#### By using properties with the suffix `Config`

The SDK provides properties with the suffix `Config` in `liveRoomConfiguration`. You can use the following sample code to get the corresponding `Config` API for customization.

```objectivec
[[BDLLiveEngine sharedInstance] liveRoomConfiguration].xxxxConfig
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use this method, we recommend that you configure the UI before viewers join the live room.</div>


<span id="2ccd7abe"></span>
### Implementation

In this topic, take the frequently used UI customization features in e\-commerce scenarios as an example.

<span id="a625195e"></span>
#### Video scaling mode

By default, the video for a live room in portrait mode keeps the original aspect ratio to fill the player. The width of the video fills the width of the player, and the height of the video fills the height of the player. If the aspect ratio of the video is different from that of the player, the video is cropped to fit. You can customize the video scaling mode.

The following sample code makes the video completely fill the player, but the aspect ratio of the video may change.


<Tabs>
<Tab zoneid="xnqNuTCK3L" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/123a2189d7a840fa8e6b2b6302abc4c7~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="ws41rSgxJ0" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a81142d11fa34c199aff2c0506d707df~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
BDLLiveRoomConfiguration *config = [[BDLLiveEngine sharedInstance] liveRoomConfiguration];
config.playerConfig.portrait.scalingMode = BDLPlayerScalingModeFill;
```


<span id="eb320cbc"></span>
#### Icon to close the full\-featured live room

By default, the icon to close the full\-featured live room in portrait mode is displayed as x. You can customize the icon display style.

The following sample code customizes the icon as the image named `back`.


<Tabs>
<Tab zoneid="VJbPEbtlUE" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0637d35400574edb81334f2f402fa154~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="iZIOrWjRnT" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2fd49d18ce0476bbd40b3f670f019cb~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
livePullVC.config.customizeCloseButton = ^__kindof UIButton * _Nullable(BDLLivePullViewController * _Nonnull viewController, UIButton * _Nonnull button) {
    // Customize the corner radius and border.
    button.clipsToBounds = YES;
    button.layer.cornerRadius = 3;
    button.layer.borderWidth = 2;
    button.layer.borderColor = UIColor.grayColor.CGColor;
    // Customize the icon as the image named back.
    [button setImage:[UIImage imageNamed:@"back"] forState:UIControlStateNormal];
    return button;
};
```


<span id="ee6cf81c"></span>
#### Floating interaction tools

Floating interaction tools contain the icons for lucky draws, quizzes, votes, questionnaires, and announcements. For a live room in portrait mode, floating interaction tools are displayed in the upper\-left corner of the live room by default. You can customize the default position of floating interaction tools.

The following sample code moves the default position of floating interaction tools down by 50 pt.


<Tabs>
<Tab zoneid="SNAukz9GBa" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2c389a4b49d437d97ef29c2eaa39b29~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="urWEnQzD9h" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bcad45935ec4e7e9da9c74dc16a1170~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
// Customize the floating window in the full-featured live room. 
livePullVC.config.customFloatingController = ^(BDLLivePullViewController * _Nonnull viewController, BDLFloatingController * _Nonnull floatingController) {
    // Customize the default position of floating interaction tools. The view supports dragging, so you must adjust the position by setting view.frame, instead of using the auto layout.
    floatingController.customizeInteractiveToolContainerView = ^__kindof UIStackView * _Nullable(BDLFloatingController * _Nonnull floatingController, UIStackView * _Nonnull view) {
        CGRect frame = view.frame;
        // Move the default position of floating interaction tools down by 50 pt.   
        frame.origin.y += 50;
        view.frame = frame;
        return view;
    };
};
```


<span id="8ea12ced"></span>
#### Height of the menu for product cards

By default, the height of the menu for product cards is 0.73 times the screen height. You can customize the height of the menu.

The following sample code sets the height of the menu to half of the screen height.


<Tabs>
<Tab zoneid="hiCwllk2Lh" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4789ad68e6c248f7876e4cfce8059b49~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="Z8u16C7LPZ" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8ff0f6b33c645d385457b7d7f53747c~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
livePullVC.config.customShoppingCardController = ^(BDLLivePullViewController * _Nonnull viewController, BDLShoppingCardController * _Nonnull shoppingCardController) {
    shoppingCardController.customizeShoppingCardView = ^__kindof BDLBaseView * _Nullable(BDLShoppingCardController * _Nonnull controller, BDLShoppingCardView * _Nonnull shoppingCardView) {
        [shoppingCardView mas_updateConstraints:^(MASConstraintMaker *make) {
            make.height.mas_equalTo(CGRectGetHeight(UIScreen.mainScreen.bounds) * 1 / 2);
        }];
        return shoppingCardView;
    };
};
```
