---
title: "Viewer SDK for iOS: Type definitions"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions"
---

<span id="BDLPopupWebViewConfiguration(Config)"></span>
# BDLPopupWebViewConfiguration(Config)

```objectivec
@interface BDLPopupWebViewConfiguration (Config)
```


The configuration of WebView dialog box.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CGFloat |[viewHeight](https://docs.byteplus.com/en/docs/11/17341#BDLPopupWebViewConfiguration(Config)-viewheight) |
|NSString\* |[colorTheme](https://docs.byteplus.com/en/docs/11/17341#BDLPopupWebViewConfiguration(Config)-colortheme) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupWebViewConfiguration(Config)-viewheight"></span>
### viewHeight

```objectivec
@property (nonatomic, assign) CGFloat viewHeight;
```


The height of the content area. Default value: 460. Unit: points.

<span id="BDLPopupWebViewConfiguration(Config)-colortheme"></span>
### colorTheme

```objectivec
@property (nonatomic, copy, nullable) NSString *colorTheme;
```


The color theme. If the parameter value is `custom` or `light`, the color of the content area is white. Otherwise, the color is black (#20202A).

<span id="BDLCommentUserModel"></span>
# BDLCommentUserModel

```objectivec
@interface BDLCommentUserModel : BDLBaseModel
```


The model of user information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[nickname](https://docs.byteplus.com/en/docs/11/17341#BDLCommentUserModel-nickname) |
|NSString\* |[email](https://docs.byteplus.com/en/docs/11/17341#BDLCommentUserModel-email) |
|NSString\* |[externalId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentUserModel-externalid) |
|NSString\* |[avatarUrl](https://docs.byteplus.com/en/docs/11/17341#BDLCommentUserModel-avatarurl) |
|NSNumber\* |[userId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentUserModel-userid) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentUserModel-nickname"></span>
### nickname

```objectivec
@property (nonatomic, copy) NSString *nickname;
```


The nickname.

<span id="BDLCommentUserModel-email"></span>
### email

```objectivec
@property (nonatomic, copy) NSString *email;
```


The email.

<span id="BDLCommentUserModel-externalid"></span>
### externalId

```objectivec
@property (nonatomic, copy) NSString *externalId;
```


The unique identifier of the viewer on a third\-party platform.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property has a value only when the authentication mode is custom and the viewer has logged in to the live room.</div>


<span id="BDLCommentUserModel-avatarurl"></span>
### avatarUrl

```objectivec
@property (nonatomic, copy) NSString *avatarUrl;
```


The avatar URL.

<span id="BDLCommentUserModel-userid"></span>
### userId

```objectivec
@property (nonatomic, strong) NSNumber *userId;
```


The user ID, which is the unique identifier of the viewer in BytePlus Live.

<span id="BDLCardConfiguration"></span>
# BDLCardConfiguration

```objectivec
@interface BDLCardConfiguration : BDLRTBaseConfiguration
```


The product card configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIColor\* |[cardTitleColor](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration-cardtitlecolor) |
|UIColor\* |[strikeThroughTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration-strikethroughtextcolor) |
|UIColor\* |[cardHighLightColor](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration-cardhighlightcolor) |
|UIColor\* |[cardCellColor](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration-cardcellcolor) |
|BOOL |[productOriginalPriceShowStrikethrough](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration-productoriginalpriceshowstrikethrough) |


<span id="instructions"></span>
## Instructions

<span id="BDLCardConfiguration-cardtitlecolor"></span>
### cardTitleColor

```objectivec
@property (nonatomic, strong) UIColor *cardTitleColor;
```


The color of the product name.

<span id="BDLCardConfiguration-strikethroughtextcolor"></span>
### strikeThroughTextColor

```objectivec
@property (nonatomic, strong) UIColor *strikeThroughTextColor;
```


The color of the list price.

<span id="BDLCardConfiguration-cardhighlightcolor"></span>
### cardHighLightColor

```objectivec
@property (nonatomic, strong) UIColor *cardHighLightColor;
```


The color of the retail price.

<span id="BDLCardConfiguration-cardcellcolor"></span>
### cardCellColor

```objectivec
@property (nonatomic, strong) UIColor *cardCellColor;
```


The color of the cell.

<span id="BDLCardConfiguration-productoriginalpriceshowstrikethrough"></span>
### productOriginalPriceShowStrikethrough

```objectivec
@property (nonatomic, assign) BOOL productOriginalPriceShowStrikethrough;
```


Whether to display the strikethrough on the list price. Default value: `NO`. Valid values:


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="bdlactivitystatus"></span>
# BDLActivityStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLActivityStatus
)
```


The live room status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLActivityStatusUnknown |0 |Unknown. |
|BDLActivityStatusLive |1 |Live. |
|BDLActivityStatusPreview |2 |Preview. |
|BDLActivityStatusReplay |3 |Playback. |
|BDLActivityStatusEnd |4 |Over. |


<span id="BDLPopupRightShowViewProtocol"></span>
# BDLPopupRightShowViewProtocol

```objectivec
@protocol BDLPopupRightShowViewProtocol <BDLPopupBaseViewProtocol>
```


The protocol for displaying the dialog box on the right.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[rightShowInView:completion:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupRightShowViewProtocol-rightshowinview-completion) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupRightShowViewProtocol-rightshowinview-completion"></span>
### rightShowInView:completion:

```objectivec
- (void)rightShowInView:(UIView *)superview completion:(nullable void (^)(BDLPopupBaseView *view))completion;
```


Displays the dialog box on the right.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|superview |UIView\* |The dialog box will be displayed as a subview of the superview. |
|completion |nullable void(^)(BDLPopupBaseView\*view) |The callback triggered after the dialog box is displayed. |


<span id="BDLCommentBaseConfiguration"></span>
# BDLCommentBaseConfiguration

```objectivec
@interface BDLCommentBaseConfiguration : BDLRTBaseConfiguration
```


The base class configuration for comments and top comments.

<span id="BDLLivePullViewControllerConfig"></span>
# BDLLivePullViewControllerConfig

```objectivec
@interface BDLLivePullViewControllerConfig : NSObject
```


The configuration of the full\-featured live room.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[commentUrlFloatingEnable](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-commenturlfloatingenable) |
|BOOL |[disableClearScreen](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-disableclearscreen) |
|BOOL |[autoCloseFloatingPlayerWhenAppear](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-autoclosefloatingplayerwhenappear) |
|BOOL |[showCloseButtonWhenClearingScreen](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-showclosebuttonwhenclearingscreen) |
|BOOL |[showPortraitRoomTopShadow](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-showportraitroomtopshadow) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[shouldShowInAppPipIfAvailable](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-shouldshowinapppipifavailable) |
|BOOL |[isCloseWhileDisappear](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-isclosewhiledisappear) |
|BDLBaseView |[customizeAccountView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeaccountview) |
|BDLPageAdViewProtocol |[customizePageAdView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizepageadview) |
|void |[customizePlayerView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeplayerview) |
|UIView\* |[customizePlayerContainerView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeplayercontainerview) |
|void |[customizeLiveDescriptionView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizelivedescriptionview) |
|void |[customizeCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizecommentandnoticeview) |
|UIColor\* |[customizeBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizebackgroundcolor) |
|void |[customizeMenuBarView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizemenubarview) |
|void |[customizeMultiLanguageView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizemultilanguageview) |
|BDLBaseView |[customizeMoreOptionsView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizemoreoptionsview) |
|BDLPopupBottomShowViewProtocol |[customizePopupTopCommentView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizepopuptopcommentview) |
|BDLPopupBottomShowViewProtocol |[customizePopupWebView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizepopupwebview) |
|BDLPopupCenterShowViewProtocol |[customizeRiskWarningView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeriskwarningview) |
|UIView\* |[customizeCountdownView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizecountdownview) |
|void |[customizeCountdownViewConstrains](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizecountdownviewconstrains) |
|void |[customizeViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeviewconstraints) |
|void |[customizePlayerContainerViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeplayercontainerviewconstraints) |
|void |[customizePageAdViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizepageadviewconstraints) |
|BDLBaseView |[customizedNickNameInputView](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizednicknameinputview) |
|void |[customInteractiveToolController](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-custominteractivetoolcontroller) |
|void |[customShoppingCardController](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customshoppingcardcontroller) |
|void |[customFloatingController](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customfloatingcontroller) |


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewControllerConfig-commenturlfloatingenable"></span>
### commentUrlFloatingEnable

```objectivec
@property (nonatomic, assign) BOOL commentUrlFloatingEnable;
```


Whether the redirected content is displayed on a floating page in the live room after a URL in the comment is tapped. Default value: `NO`.


* `YES`: The redirected content is displayed on a floating page in the live room. Viewers can watch the video and view the redirected content at the same time.

* `NO`: The redirected content is displayed on a new browser tab. Viewers cannot watch the video and view the redirected content at the same time.

    &nbsp;


<span id="disableclearscreen"></span>
### disableClearScreen

```objectivec
@property (nonatomic, assign) BOOL disableClearScreen;
```


Whether to disable the clear screen feature in the live room in portrait mode. Default value: `NO`.


* `YES`: Disable.

* `NO`: Do not disable. Viewers can swipe right to clear the screen or tap the more (...) icon \> **Clear screen** to achieve the clear screen effect.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the portrait mode supports the clear screen feature.</div>


<span id="BDLLivePullViewControllerConfig-autoclosefloatingplayerwhenappear"></span>
### autoCloseFloatingPlayerWhenAppear

```objectivec
@property (nonatomic, assign) BOOL autoCloseFloatingPlayerWhenAppear;
```


Whether to close the currently displayed floating window when `viewDidAppear` is triggered, which happens when the full\-featured live room view is displayed. Default value: `NO`.


* `YES`: Close.

* `NO`: Do not close.

    &nbsp;


<span id="showclosebuttonwhenclearingscreen"></span>
### showCloseButtonWhenClearingScreen

```objectivec
@property (nonatomic, assign) BOOL showCloseButtonWhenClearingScreen;
```


Whether to display the button for closing the live room during screen clearing. Default value: `NO`.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="showportraitroomtopshadow"></span>
### showPortraitRoomTopShadow

```objectivec
@property (nonatomic, assign) BOOL showPortraitRoomTopShadow;
```


Whether to display a gradient overlay at the top of the live room in portrait mode. Default value: `YES`.


* `YES`: Display. If the background of your video is white, displaying the gradient overlay can make the white text at the top of the live room more visible.

* `NO`: Do not display.


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewControllerConfig-shouldshowinapppipifavailable"></span>
### shouldShowInAppPipIfAvailable

```objectivec
@property (nonatomic, copy, nullable) BOOL (^shouldShowInAppPipIfAvailable)(BDLLivePullViewController *viewController, BDLActivityStatus status, BOOL isClose);
```


Whether to display the in\-app picture\-in\-picture (PiP), namely the floating player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|status |BDLActivityStatus |The current live room status. For more information, see [BDLActivityStatus](https://docs.byteplus.com/en/docs/11/17341#BDLActivityStatus).<br><br>Call this method only when the live room is in any of the following statuses:<br><br><br>* Preview (with a preview added).<br><br>* Playback.<br><br>* Live. |
|isClose |BOOL |Whether to close the current page.<br><br><br>* `YES`: Close the current page, with in\-app PiP displayed by default.<br><br>* `NO`: Open a new page, with in\-app PiP not displayed by default. |


**Return Value**


* `YES`: Display in\-app PiP.

* `NO`: Do not display in\-app PiP.

    &nbsp;


<span id="isclosewhiledisappear"></span>
### isCloseWhileDisappear

```objectivec
@property (nonatomic, copy, nullable) BOOL (^isCloseWhileDisappear)(BDLLivePullViewController *viewController);
```


When viewDidDisappear is triggered and the `isClose` parameter value passed through [shouldShowInAppPipIfAvailable](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-shouldshowinapppipifavailable) does not meet expectations, use this property to adjust the parameter value.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


**Return Value**


* `YES`: Close the current page.

* `NO`: Open a new page.

    &nbsp;


<span id="customizeaccountview"></span>
### customizeAccountView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeAccountView)(BDLLivePullViewController *viewController, BDLBusinessAccountView *view);
```


Customizes the host account view. All properties except `hidden` can be customized. If you need to customize the `frame`, you can set it in [customizeViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeviewconstraints) using `mas_remakeConstraints`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLBusinessAccountView\* |The host account view. For more information, see [BDLBusinessAccountView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBusinessAccountView). |


**Return Value**

The host account view. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizepageadview"></span>
### customizePageAdView

```objectivec
@property (nonatomic, copy, nullable) UIView<BDLPageAdViewProtocol> * _Nullable (^customizePageAdView)(BDLLivePullViewController *viewController, BDLPageAdView *view);
```


Customizes the in\-page ad view. All properties except `hidden` can be customized.

If you need to customize the `frame`,


* For live rooms in landscape mode, you can set it in [customizeViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeviewconstraints) using `mas_remakeConstraints`.

* For live rooms in portrait mode, you can directly modify the `frame`, but `frame.origin` will be ignored, meaning only `frame.size` can be modified.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For live rooms in portrait mode, the header ad and in\-page ads share this view.</div>


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLPageAdView\* |The in\-page ad view. For more information, see [BDLPageAdView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPageAdView). |


**Return Value**

The in\-page ad view, which needs to conform to the [BDLPageAdViewProtocol](https://docs.byteplus.com/en/docs/11/17341#BDLPageAdViewProtocol) protocol. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizeplayerview"></span>
### customizePlayerView

```objectivec
@property (nonatomic, copy, nullable) void (^customizePlayerView)(BDLLivePullViewController *viewController, BDLPlayerView *view);
```


Customizes the player. All properties except `frame` can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |


<span id="BDLLivePullViewControllerConfig-customizeplayercontainerview"></span>
### customizePlayerContainerView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView * _Nullable (^customizePlayerContainerView)(BDLLivePullViewController *viewController, UIView *view);
```


Customizes the player container view. All properties except `frame` can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |UIView\* |The player container view. |


**Return Value**

The player container view. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizelivedescriptionview"></span>
### customizeLiveDescriptionView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeLiveDescriptionView)(BDLLivePullViewController *viewController, BDLLiveDescriptionView *describeView);
```


Customizes the live room description. All properties except `text`, `textColor`, and `hidden` can be customized. You can modify the overall layout using [customizeViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeviewconstraints), but customizing the layout of individual properties is not supported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|describeView |BDLLiveDescriptionView\* |The live room description view. For more information, see [BDLLiveDescriptionView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLiveDescriptionView). |


<span id="BDLLivePullViewControllerConfig-customizecommentandnoticeview"></span>
### customizeCommentAndNoticeView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeCommentAndNoticeView)(BDLLivePullViewController *viewController, BDLCommentAndNoticeView *view);
```


Customizes the comment and notification view for live rooms in portrait mode. All properties except `hidden` can be customized. You can modify the overall layout using [customizeViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeviewconstraints), but customizing the layout of individual properties is not supported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLCommentAndNoticeView\* |The comment and notification view. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/17341#BDLCommentAndNoticeView). |


<span id="BDLLivePullViewControllerConfig-customizebackgroundcolor"></span>
### customizeBackgroundColor

```objectivec
@property (nonatomic, copy, nullable) UIColor * _Nullable (^customizeBackgroundColor)(BDLLivePullViewController *viewController);
```


Customizes the background color of the live room. If the BytePlus Live server returns the background image for mobile devices, the background image will override the background color set by this method. The background color cannot be set to `clearColor`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


**Return Value**

The background color of the live room. If `nil`, the configured color returned by the BytePlus Live server will be displayed.

<span id="BDLLivePullViewControllerConfig-customizemenubarview"></span>
### customizeMenuBarView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeMenuBarView)(BDLLivePullViewController *viewController, BDLMenuBarView *view);
```


Customizes the menu bar. All properties except `hidden` can be customized. You can modify the overall layout using [customizeViewConstraints](https://docs.byteplus.com/en/docs/11/17341#BDLLivePullViewControllerConfig-customizeviewconstraints), but customizing the layout of individual properties is not supported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLMenuBarView\* |The menu bar view. For more information, see [BDLMenuBarView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLMenuBarView). |


<span id="BDLLivePullViewControllerConfig-customizemultilanguageview"></span>
### customizeMultiLanguageView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeMultiLanguageView)(BDLLivePullViewController *viewController, BDLMultiLanguageView *view);
```


Customizes the language selection dialog box view. All properties except `frame` can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLMultiLanguageView\* |The language selection dialog box view. For more information, see [BDLMultiLanguageView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLMultiLanguageView). |


<span id="BDLLivePullViewControllerConfig-customizemoreoptionsview"></span>
### customizeMoreOptionsView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeMoreOptionsView)(BDLLivePullViewController *viewController, BDLMoreOptionsView *view);
```


Customizes the more options dialog box view for the live room in portrait mode. All properties except `frame` can be customized. The more options dialog box is displayed after viewers tap the more (...) icon in the lower\-right corner of the live room in portrait mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLMoreOptionsView\* |The more options dialog box view. For more information, see [BDLMoreOptionsView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLMoreOptionsView). |


**Return Value**

The more options dialog box view. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizepopuptopcommentview"></span>
### customizePopupTopCommentView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView<BDLPopupBottomShowViewProtocol> * (^customizePopupTopCommentView)(BDLLivePullViewController *viewController, BDLPopupTopCommentView *popupTopCommentView);
```


Customizes the pinned comment details dialog box view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|popupTopCommentView |BDLPopupTopCommentView\* |The pinned comment details dialog box view. For more information, see [BDLPopupTopCommentView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPopupTopCommentView). |


**Return Value**

The pinned comment details dialog box view. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizepopupwebview"></span>
### customizePopupWebView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView<BDLPopupBottomShowViewProtocol> * (^customizePopupWebView)(BDLLivePullViewController *viewController, BDLPopupWebView *popupWebView);
```


Customizes the WebView dialog box. All properties can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|popupWebView |BDLPopupWebView\* |The WebView dialog box. For more information, see [BDLPopupWebView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPopupWebView). |


**Return Value**

The WebView dialog box. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizeriskwarningview"></span>
### customizeRiskWarningView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView<BDLPopupCenterShowViewProtocol> * _Nullable (^customizeRiskWarningView)(BDLLivePullViewController *viewController, BDLRiskWarningView *view);
```


Customizes the reminder view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLRiskWarningView\* |The reminder view. For more information, see [BDLRiskWarningView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLRiskWarningView). |


**Return Value**

The reminder view, which needs to conform to the [BDLPopupCenterShowViewProtocol](https://docs.byteplus.com/en/docs/11/17341#BDLPopupCenterShowViewProtocol) protocol. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizecountdownview"></span>
### customizeCountdownView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView * _Nullable (^customizeCountdownView)(BDLLivePullViewController *viewController, BDLCountdownView *view);
```


Customizes the countdown view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLCountdownView\* |The countdown view of the live room. For more information, see [BDLCountdownView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLCountdownView). |


**Return Value**

The countdown view of the live room. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-customizecountdownviewconstrains"></span>
### customizeCountdownViewConstrains

```objectivec
@property (nonatomic, copy, nullable) void (^customizeCountdownViewConstrains)(BDLLivePullViewController *viewController, UIView *view);
```


Customizes the layout of the countdown view.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Whether the booking feature is enabled affects the position of the countdown on the page.</div>


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |UIView\* |The countdown view. |


<span id="BDLLivePullViewControllerConfig-customizeviewconstraints"></span>
### customizeViewConstraints

```objectivec
@property (nonatomic, copy, nullable) void (^customizeViewConstraints)(BDLLivePullViewController *viewController);
```


Customizes the layout. The default implementation uses Masonry for layout. Here, `mas_remakeConstraints` can be used to modify the overall layout.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerConfig-customizeplayercontainerviewconstraints"></span>
### customizePlayerContainerViewConstraints

```objectivec
@property (nonatomic, copy, nullable) void (^customizePlayerContainerViewConstraints)(BDLLivePullViewController *viewController, UIView *view);
```


Customizes the layout of the player container.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |UIView\* |The player container view. |


<span id="BDLLivePullViewControllerConfig-customizepageadviewconstraints"></span>
### customizePageAdViewConstraints

```objectivec
@property (nonatomic, copy, nullable) void (^customizePageAdViewConstraints)(BDLLivePullViewController *viewController, UIView *view);
```


Customizes the position of in\-page ads.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |UIView\* |The in\-page ad view. |


<span id="BDLLivePullViewControllerConfig-customizednicknameinputview"></span>
### customizedNickNameInputView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * (^customizedNickNameInputView)(BDLLivePullViewController *viewController, BDLPopupInputView *view);
```


Customizes the nickname input interface.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|view |BDLPopupInputView\* |The nickname text box view. For more information, see [BDLPopupInputView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPopupInputView). |


**Return Value**

The nickname text box view. Not displayed if `nil`.

<span id="BDLLivePullViewControllerConfig-custominteractivetoolcontroller"></span>
### customInteractiveToolController

```objectivec
@property (nonatomic, copy, nullable) void (^customInteractiveToolController)(BDLLivePullViewController *viewController, BDLInteractiveToolController *interactiveToolController);
```


Customizes the interaction tool\-related controller.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|interactiveToolController |BDLInteractiveToolController\* |The interaction tools controller. For more information, see [BDLInteractiveToolController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLInteractiveToolController). |


<span id="BDLLivePullViewControllerConfig-customshoppingcardcontroller"></span>
### customShoppingCardController

```objectivec
@property (nonatomic, copy, nullable) void (^customShoppingCardController)(BDLLivePullViewController *viewController, BDLShoppingCardController *shoppingCardController);
```


Customizes the product card\-related controller.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|shoppingCardController |BDLShoppingCardController\* |The product card controller. For more information, see [BDLShoppingCardController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLShoppingCardController). |


<span id="BDLLivePullViewControllerConfig-customfloatingcontroller"></span>
### customFloatingController

```objectivec
@property (nonatomic, copy, nullable) void (^customFloatingController)(BDLLivePullViewController *viewController, BDLFloatingController *floatingController);
```


Customizes the floating window\-related controller.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|floatingController |BDLFloatingController\* |The floating window controller. For more information, see [BDLFloatingController](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController). |


<span id="Public-API"></span>
# Public API

<span id="function"></span>
## Function


|Return |Name |
|---|---|
|void |[BDLiveManagerCompleteBlock](https://docs.byteplus.com/en/docs/11/17341#bdlivemanagercompleteblock) |
|void |[BDLHttpFailureBlock](https://docs.byteplus.com/en/docs/11/17341#bdlhttpfailureblock) |
|void |[BDLMoreOptionsViewBlock](https://docs.byteplus.com/en/docs/11/17341#bdlmoreoptionsviewblock) |
|void |[BDLBasePlayerViewSeekCompletionBlock](https://docs.byteplus.com/en/docs/11/17341#bdlbaseplayerviewseekcompletionblock) |
|void |[BDLLanguageConfirmBlock](https://docs.byteplus.com/en/docs/11/17341#bdllanguageconfirmblock) |


<span id="instructions"></span>
## Instructions

<span id="bdlivemanagercompleteblock"></span>
### BDLiveManagerCompleteBlock

```objectivec
typedef void(^BDLiveManagerCompleteBlock)(BOOL allSuccess, NSString * _Nullable warningInfo, NSArray<NSError *>  * _Nullable errors);
```


The callback is triggered when the SDK initialization is complete.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|allSuccess |BOOL |Whether the licenses passed in are all successfully authorized. Valid values:<br><br><br>* `YES`: All licenses are successfully authorized.<br><br>* `NO`: Not all licenses are successfully authorized. |
|warningInfo |NSString\* |Warning message used to indicate issues such as license information mismatched with business type ([bizType](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-biztype)), or missing necessary licenses. |
|errors |NSArray<NSError\*\>\* |Error message. `error.domain` is `BDLSDKAuthErrorDomain`, and `error.code` is [BDLSDKAuthErrorCode](https://docs.byteplus.com/en/docs/11/17341#BDLSDKAuthErrorCode). |


<span id="bdlhttpfailureblock"></span>
### BDLHttpFailureBlock

```objectivec
typedef void (^BDLHttpFailureBlock)(NSHTTPURLResponse * _Nullable response, NSError *error);
```


The callback is triggered when a network failure occurs.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|response |NSHTTPURLResponse\* |An object that provides response metadata, such as HTTP headers and status codes. If you are sending an HTTP or HTTPS request, the returned object is actually an `NSHTTPURLResponse` object. |
|error |NSError\* |An error object, which is used to indicate the reason for the request failure. |


<span id="bdlmoreoptionsviewblock"></span>
### BDLMoreOptionsViewBlock

```objectivec
typedef void (^BDLMoreOptionsViewBlock)(BDLMoreOptionsView *moreOptionsView, BOOL isSelected);
```


The callback is triggered when a button in the more options dialog box is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|moreOptionsView |BDLMoreOptionsView\* |The view of the more options dialog box. For more information, see [BDLMoreOptionsView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLMoreOptionsView). |
|isSelected |BOOL |Whether a button is tapped.<br><br><br>* `YES`: Tapped.<br><br>* `NO`: Not tapped. |


<span id="bdlbaseplayerviewseekcompletionblock"></span>
### BDLBasePlayerViewSeekCompletionBlock

```objectivec
typedef void(^BDLBasePlayerViewSeekCompletionBlock)(BOOL success);
```


The callback is triggered after the seek operation is completed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|success |BOOL |Whether the seek operation is successful. The seek operation refers to jumping to a specific time point in the video.<br><br><br>&nbsp;<br><br>* `YES`: Successful.<br><br>* `NO`: Failed. |


<span id="bdllanguageconfirmblock"></span>
### BDLLanguageConfirmBlock

```objectivec
typedef void (^BDLLanguageConfirmBlock)(BDLLanguageType selectedLanguageType);
```


The callback is triggered when a language is selected.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|selectedLanguageType |BDLLanguageType |The selected language. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/17341#BDLLanguageType). |


<span id="BDLFloatingCardConfiguration"></span>
# BDLFloatingCardConfiguration

```objectivec
@interface BDLFloatingCardConfiguration : BDLRTBaseConfiguration
```


The configuration of the floating product card.

<span id="BDLiveEffectAuthInfo"></span>
# BDLiveEffectAuthInfo

```objectivec
@interface BDLiveEffectAuthInfo : BDLBaseModel
```


The authorization information of the CV license.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLiveEffectAuthType |[authType](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-authtype) |
|NSString\* |[licenseFilePath](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-licensefilepath) |
|NSString\* |[key](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-key) |
|NSString\* |[secret](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-secret) |


<span id="instructions"></span>
## Instructions

<span id="BDLiveEffectAuthInfo-authtype"></span>
### authType

```objectivec
@property (nonatomic, assign) BDLiveEffectAuthType authType;
```


Authorization method. For more information, see [BDLiveEffectAuthType](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthType).

<span id="BDLiveEffectAuthInfo-licensefilepath"></span>
### licenseFilePath

```objectivec
@property (nonatomic, copy) NSString *licenseFilePath;
```


The path of the license file for offline authorization. Contact BytePlus Live technical support to get the CV license.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property takes effect only when the value of <a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-authtype">authType</a> is <code>BDLiveEffectAuthTypeOffLine</code>.</div>


<span id="BDLiveEffectAuthInfo-key"></span>
### key

```objectivec
@property (nonatomic, copy) NSString *key;
```


The business identifier for online authorization. Contact BytePlus Live technical support to get the business identifier.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property takes effect only when the value of <a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-authtype">authType</a> is <code>BDLiveEffectAuthTypeOnLine</code>.</div>


<span id="BDLiveEffectAuthInfo-secret"></span>
### secret

```objectivec
@property (nonatomic, copy) NSString *secret;
```


The business secret key for online authorization, which can be obtained together with the business identifier when you create the business. Contact BytePlus Live technical support to get the business secret key.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property takes effect only when the value of <a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-authtype">authType</a> is <code>BDLiveEffectAuthTypeOnLine</code>.</div>


<span id="BDLQuestionnaireModel"></span>
# BDLQuestionnaireModel

```objectivec
@interface BDLQuestionnaireModel : BDLBaseModel
```


The model of questionnaire information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[questionnaireId](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-questionnaireid) |
|NSString\* |[title](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-title) |
|NSString\* |[questionDescription](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-questiondescription) |
|BDLQuestionnaireTrigger |[triggerTime](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-triggertime) |
|BDLQuestionnairePublishStatus |[publishStatus](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-publishstatus) |
|BOOL |[isRealNameEnable](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-isrealnameenable) |
|BOOL |[isUserFilled](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-isuserfilled) |
|NSArray<BDLQuestionnaireQuestionModel\*\>\* |[questions](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-questions) |
|NSDate\* |[createTime](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-createtime) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[isValid](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireModel-isvalid) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireModel-questionnaireid"></span>
### questionnaireId

```objectivec
@property (nonatomic, strong) NSNumber *questionnaireId;
```


The questionnaire ID.

<span id="BDLQuestionnaireModel-title"></span>
### title

```objectivec
@property (nonatomic, copy) NSString *title;
```


The questionnaire title.

<span id="BDLQuestionnaireModel-questiondescription"></span>
### questionDescription

```objectivec
@property (nonatomic, copy) NSString *questionDescription;
```


The questionnaire description.

<span id="BDLQuestionnaireModel-triggertime"></span>
### triggerTime

```objectivec
@property (nonatomic, assign) BDLQuestionnaireTrigger triggerTime;
```


The send time. For more information, see [BDLQuestionnaireTrigger](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireTrigger).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The string type returned by the server is converted to an enumeration value.</div>


<span id="BDLQuestionnaireModel-publishstatus"></span>
### publishStatus

```objectivec
@property (nonatomic, assign) BDLQuestionnairePublishStatus publishStatus;
```


The published status. For more information, see [BDLQuestionnairePublishStatus](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnairePublishStatus).

<span id="BDLQuestionnaireModel-isrealnameenable"></span>
### isRealNameEnable

```objectivec
@property (nonatomic, assign) BOOL isRealNameEnable;
```


Whether the questionnaire is non\-anonymous.


* `YES`: Non\-anonymous.

* `NO`: Anonymous.

    &nbsp;


<span id="isuserfilled"></span>
### isUserFilled

```objectivec
@property (nonatomic, assign) BOOL isUserFilled;
```


Whether the questionnaire is submitted by the viewer.


* `YES`: Submitted.

* `NO`: Not submitted.

    &nbsp;


<span id="questions"></span>
### questions

```objectivec
@property (nonatomic, copy) NSArray<BDLQuestionnaireQuestionModel *> *questions;
```


The question list of the questionnaire. For more information, see [BDLQuestionnaireQuestionModel](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel).

<span id="BDLQuestionnaireModel-createtime"></span>
### createTime

```objectivec
@property (nonatomic, strong) NSDate *createTime;
```


The creation time.

<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireModel-isvalid"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


Whether valid.

**Return Value**


* `YES`: Valid.

* `NO`: Invalid.

    &nbsp;


<span id="bdlinteractivecountdownbasemodel"></span>
# BDLInteractiveCountdownBaseModel

```objectivec
@interface BDLInteractiveCountdownBaseModel : BDLBaseModel
```


The parent class of the model for interaction tools with countdown.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[deadline](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveCountdownBaseModel-deadline) |
|NSInteger |[sendTime](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveCountdownBaseModel-sendtime) |
|NSInteger |[countdown](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveCountdownBaseModel-countdown) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveCountdownBaseModel-deadline"></span>
### deadline

```objectivec
@property (nonatomic, assign) NSInteger deadline;
```


The deadline. Unit: seconds.

<span id="BDLInteractiveCountdownBaseModel-sendtime"></span>
### sendTime

```objectivec
@property (nonatomic, assign) NSInteger sendTime;
```


The send time in Unix timestamp format. Unit: seconds.

<span id="BDLInteractiveCountdownBaseModel-countdown"></span>
### countdown

```objectivec
@property (nonatomic, assign) NSInteger countdown;
```


The remaining countdown time. Unit: seconds. Not returned by the BytePlus Live server.

<span id="BDLPopupWebViewConfiguration"></span>
# BDLPopupWebViewConfiguration

```objectivec
@interface BDLPopupWebViewConfiguration : BDLRTBaseConfiguration
```


The configuration of the WebView dialog box.

<span id="BDLDraggingMode"></span>
# BDLDraggingMode

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLDraggingMode
)
```


The dragging mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLDraggingModeDisabled |0 |Cannot drag. |
|BDLDraggingModeNormal |1 |Free drag. |
|BDLDraggingModeRevert |2 |Restore position after release. |
|BDLDraggingModePullOver |3 |Automatically aligns to the edges, but only to the left or right edges. |
|BDLDraggingModeAdsorb |4 |Automatically snap to the edges when aligned, and can snap to all four edges. |


<span id="BDLMoreOptionsViewConfiguration(Config)"></span>
# BDLMoreOptionsViewConfiguration(Config)

```objectivec
@interface BDLMoreOptionsViewConfiguration (Config)
```


The configuration of the more options dialog box.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The more options dialog box is displayed after viewers tap the more (...) icon in the lower\-right corner of the live room in portrait mode.</div>


<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImage\* |[multiLanguageImage](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsViewConfiguration(Config)-multilanguageimage) |
|UIImage\* |[clearScreenImage](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsViewConfiguration(Config)-clearscreenimage) |
|UIImage\* |[resolutionImage](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsViewConfiguration(Config)-resolutionimage) |


<span id="instructions"></span>
## Instructions

<span id="BDLMoreOptionsViewConfiguration(Config)-multilanguageimage"></span>
### multiLanguageImage

```objectivec
@property (nonatomic, strong) UIImage *multiLanguageImage;
```


The language selection button image.

<span id="BDLMoreOptionsViewConfiguration(Config)-clearscreenimage"></span>
### clearScreenImage

```objectivec
@property (nonatomic, strong) UIImage *clearScreenImage;
```


The clear screen button image.

<span id="BDLMoreOptionsViewConfiguration(Config)-resolutionimage"></span>
### resolutionImage

```objectivec
@property (nonatomic, strong) UIImage *resolutionImage;
```


The resolution selection button image.

<span id="BDLPlayerControlViewMode"></span>
# BDLPlayerControlViewMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLPlayerControlViewMode
)
```


The player control style.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPlayerControlViewModeDefault |0 |Default. |
|BDLPlayerControlViewModeCompact |1 |Compact. |


<span id="BDLPopupInputViewConfiguration(Config)"></span>
# BDLPopupInputViewConfiguration(Config)

```objectivec
@interface BDLPopupInputViewConfiguration (Config)
```


The configuration of the nickname text box.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[inputPlaceholder](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-inputplaceholder) |
|NSString\* |[titleText](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-titletext) |
|NSString\* |[confirmTitle](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-confirmtitle) |
|UIFont\* |[titleFont](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-titlefont) |
|UIFont\* |[textFieldFont](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-textfieldfont) |
|UIFont\* |[confirmFont](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-confirmfont) |
|UIColor\* |[confirmBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-confirmbackgroundcolor) |
|UIFont\* |[placeholderFont](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration(Config)-placeholderfont) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupInputViewConfiguration(Config)-inputplaceholder"></span>
### inputPlaceholder

```objectivec
@property (nonatomic, copy) NSString *inputPlaceholder;
```


The placeholder text of the text box.

<span id="BDLPopupInputViewConfiguration(Config)-titletext"></span>
### titleText

```objectivec
@property (nonatomic, copy) NSString *titleText;
```


The title text.

<span id="BDLPopupInputViewConfiguration(Config)-confirmtitle"></span>
### confirmTitle

```objectivec
@property (nonatomic, copy) NSString *confirmTitle;
```


The text of the confirm button.

<span id="BDLPopupInputViewConfiguration(Config)-titlefont"></span>
### titleFont

```objectivec
@property (nonatomic, strong) UIFont *titleFont;
```


The font and font size of the title.

<span id="BDLPopupInputViewConfiguration(Config)-textfieldfont"></span>
### textFieldFont

```objectivec
@property (nonatomic, strong) UIFont *textFieldFont;
```


The font and font size of the text box.

<span id="BDLPopupInputViewConfiguration(Config)-confirmfont"></span>
### confirmFont

```objectivec
@property (nonatomic, strong) UIFont *confirmFont;
```


The font and font size of the confirm button.

<span id="BDLPopupInputViewConfiguration(Config)-confirmbackgroundcolor"></span>
### confirmBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *confirmBackgroundColor;
```


The background color of the confirm button.

<span id="BDLPopupInputViewConfiguration(Config)-placeholderfont"></span>
### placeholderFont

```objectivec
@property (nonatomic, strong) UIFont *placeholderFont;
```


The font and font size for the placeholder text of the text box.

<span id="BDLCommentExtraModel"></span>
# BDLCommentExtraModel

```objectivec
@interface BDLCommentExtraModel: BDLBaseModel
```


The additional information model of comments.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLCommentUserModel\* |[user](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-user) |
|NSString\* |[textContent](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-textcontent) |
|NSString\* |[textContentCn](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-textcontentcn) |
|NSString\* |[textContentEn](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-textcontenten) |
|NSString\* |[textContentJp](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-textcontentjp) |
|BOOL |[isPresenter](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-ispresenter) |
|BDLMessageContentType |[contentType](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-contenttype) |
|NSString\* |[localId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-localid) |
|BOOL |[isDeleted](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-isdeleted) |
|BOOL |[isSelfLiked](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-isselfliked) |
|NSInteger |[likeCount](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-likecount) |
|BDLCommentSendState |[localSendState](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-localsendstate) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|NSString\* |[textContentForType:](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel-textcontentfortype) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentExtraModel-user"></span>
### user

```objectivec
@property (nonatomic, strong) BDLCommentUserModel *user;
```


The user who sent the comment. For more information, see [BDLCommentUserModel](https://docs.byteplus.com/en/docs/11/17341#BDLCommentUserModel).

<span id="BDLCommentExtraModel-textcontent"></span>
### textContent

```objectivec
@property (nonatomic, copy) NSString *textContent;
```


The comment content.

<span id="BDLCommentExtraModel-textcontentcn"></span>
### textContentCn

```objectivec
@property (nonatomic, copy) NSString *textContentCn;
```


The comment content in Chinese.

<span id="BDLCommentExtraModel-textcontenten"></span>
### textContentEn

```objectivec
@property (nonatomic, copy) NSString *textContentEn;
```


The comment content in English.

<span id="BDLCommentExtraModel-textcontentjp"></span>
### textContentJp

```objectivec
@property (nonatomic, copy) NSString *textContentJp;
```


The comment content in Japanese.

<span id="BDLCommentExtraModel-ispresenter"></span>
### isPresenter

```objectivec
@property (nonatomic, assign) BOOL isPresenter;
```


Whether the comment is sent by the host.


* `YES`: The host.

* `NO`: Not the host.

    &nbsp;


<span id="contenttype"></span>
### contentType

```objectivec
@property (nonatomic, assign) BDLMessageContentType contentType;
```


The type of comment content. For more information, see [BDLMessageContentType](https://docs.byteplus.com/en/docs/11/17341#BDLMessageContentType).

<span id="BDLCommentExtraModel-localid"></span>
### localId

```objectivec
@property (nonatomic, copy) NSString *localId;
```


The comment ID. Not returned by the BytePlus Live server.

<span id="BDLCommentExtraModel-isdeleted"></span>
### isDeleted

```objectivec
@property (nonatomic, assign) BOOL isDeleted;
```


Whether the comment is deleted.


* `YES`: Deleted.

* `NO`: Not deleted.

    &nbsp;


<span id="isselfliked"></span>
### isSelfLiked

```objectivec
@property (nonatomic, assign) BOOL isSelfLiked;
```


Whether the comment is liked by the user themselves.


* `YES`: Liked.

* `NO`: Not liked.

    &nbsp;


<span id="likecount"></span>
### likeCount

```objectivec
@property (nonatomic, assign) NSInteger likeCount;
```


The number of likes for the comment.

<span id="BDLCommentExtraModel-localsendstate"></span>
### localSendState

```objectivec
@property (nonatomic, assign) BDLCommentSendState localSendState;
```


The comment sending status. Not returned by the BytePlus Live server. For more information, see [BDLCommentSendState](https://docs.byteplus.com/en/docs/11/17341#BDLCommentSendState).

<span id="instructions"></span>
## Instructions

<span id="BDLCommentExtraModel-textcontentfortype"></span>
### textContentForType:

```objectivec
- (NSString *)textContentForType:(BDLLanguageType)type;
```


Gets the corresponding comment content according to the language type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |BDLLanguageType |The language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/17341#BDLLanguageType). |


**Return Value**

The comment content in the corresponding language.

<span id="BDLCommentTipOffType"></span>
# BDLCommentTipOffType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLCommentTipOffType
)
```


The comment report type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLCommentTipOffTypeVulgar |1 |Sexual. |
|BDLCommentTipOffTypeLaws |2 |Law and rule violations. |
|BDLCommentTipOffTypeAdvertising |3 |Advertising campaign. |
|BDLCommentTipOffTypeFraud |4 |Scams. |
|BDLCommentTipOffTypeCruse |5 |Abusive. |
|BDLCommentTipOffTypeAbetSuicide |6 |Suicide and self\-harm. |
|BDLCommentTipOffTypeOther |10 |Others. |


<span id="BDLMultiLanguageConfiguration"></span>
# BDLMultiLanguageConfiguration

```objectivec
@interface BDLMultiLanguageConfiguration : BDLRTBaseConfiguration
```


The custom configuration for multiple languages.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLLanguageType |[preferLanguage](https://docs.byteplus.com/en/docs/11/17341#BDLMultiLanguageConfiguration-preferlanguage) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|NSString\* |[customLanguageString](https://docs.byteplus.com/en/docs/11/17341#BDLMultiLanguageConfiguration-customlanguagestring) |


<span id="instructions"></span>
## Instructions

<span id="BDLMultiLanguageConfiguration-preferlanguage"></span>
### preferLanguage

```objectivec
@property (nonatomic, assign) BDLLanguageType preferLanguage;
```


The preferred language for the watch page. Supported languages are listed in [BDLLanguageType](https://docs.byteplus.com/en/docs/11/17341#BDLLanguageType). The default setting follows the system language. After setting, you need to restart the relevant interface to take effect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the languages enabled for the live room in the <a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live console</a> can be set as preferred languages.</div>


<span id="instructions"></span>
## Instructions

<span id="BDLMultiLanguageConfiguration-customlanguagestring"></span>
### customLanguageString

```objectivec
@property (nonatomic, copy) NSString *(^customLanguageString)(BDLLanguageType language, NSString *key, NSString *originString);
```


The callback is triggered when the system text is displayed, and is used to customize the system text.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|language |BDLLanguageType |The currently selected language. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/17341#BDLLanguageType). |
|key |NSString\* |The key of the system text. |
|originString |NSString\* |The default system text. |


**Return Value**

The custom system text.

<span id="BDLInteractiveToolConfiguration(Config)"></span>
# BDLInteractiveToolConfiguration(Config)

```objectivec
@interface BDLInteractiveToolConfiguration (Config)
```


The configuration of the menu for interaction tools.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[showPeopleCount](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolConfiguration(Config)-showpeoplecount) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolConfiguration(Config)-showpeoplecount"></span>
### showPeopleCount

```objectivec
@property (nonatomic, assign) BOOL showPeopleCount;
```


Whether to display the number of viewers who participate in the vote. Default value: `YES`.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="bdltaskawardruleitemtype"></span>
# BDLTaskAwardRuleItemType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLTaskAwardRuleItemType
)
```


The prize type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLTaskAwardRuleItemTypePhysical |0 |Physical prizes. |
|BDLTaskAwardRuleItemTypeVirtual |1 |Virtual prizes. |
|BDLTaskAwardRuleItemTypeCustomize |2 |Custom prizes. |
|BDLTaskAwardRuleItemTypeTicket |3 |Voucher prizes. |


<span id="BDLThemeIconModel(Config)"></span>
# BDLThemeIconModel(Config)

```objectivec
@interface BDLThemeIconModel (Config)
```


The icon model for various live room themes.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImage\* |[darkModeIcon](https://docs.byteplus.com/en/docs/11/17341#BDLThemeIconModel(Config)-darkmodeicon) |
|UIImage\* |[lightModeIcon](https://docs.byteplus.com/en/docs/11/17341#BDLThemeIconModel(Config)-lightmodeicon) |


<span id="instructions"></span>
## Instructions

<span id="BDLThemeIconModel(Config)-darkmodeicon"></span>
### darkModeIcon

```objectivec
@property (nonatomic, strong) UIImage *darkModeIcon;
```


The icon in dark mode.

<span id="BDLThemeIconModel(Config)-lightmodeicon"></span>
### lightModeIcon

```objectivec
@property (nonatomic, strong) UIImage *lightModeIcon;
```


The icon in non\-dark mode.

<span id="BDLiveAuthInfo"></span>
# BDLiveAuthInfo

```objectivec
@interface BDLiveAuthInfo : BDLBaseModel
```


The authorization information model for BytePlus Live SDK.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLiveBizType |[bizType](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-biztype) |
|NSString\* |[appId](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-appid) |
|NSString\* |[appName](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-appname) |
|NSString\* |[channel](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-channel) |
|NSString\* |[vodLicensePath](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-vodlicensepath) |
|NSString\* |[liveLicensePath](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-livelicensepath) |
|BDLiveEffectAuthInfo\* |[effectAuthInfo](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-effectauthinfo) |


<span id="instructions"></span>
## Instructions

<span id="BDLiveAuthInfo-biztype"></span>
### bizType

```objectivec
@property (nonatomic, assign) BDLiveBizType bizType;
```


The business type. For more information, see [BDLiveBizType](https://docs.byteplus.com/en/docs/11/17341#BDLiveBizType).

<span id="BDLiveAuthInfo-appid"></span>
### appId

```objectivec
@property (nonatomic, copy) NSString *appId;
```


The app ID returned after the successful license application. Contact BytePlus Live technical support to get the app ID.

<span id="BDLiveAuthInfo-appname"></span>
### appName

```objectivec
@property (nonatomic, copy, nullable) NSString *appName;
```


The app name used to apply for the license. By default, the bundle display name is used. Contact BytePlus Live technical support to get the app name.

<span id="BDLiveAuthInfo-channel"></span>
### channel

```objectivec
@property (nonatomic, copy, nullable) NSString *channel;
```


The name of the channel through which to download the app. Default value: `App Store`.

<span id="BDLiveAuthInfo-vodlicensepath"></span>
### vodLicensePath

```objectivec
@property (nonatomic, copy, nullable) NSString *vodLicensePath;
```


The path of the VOD license file. Contact BytePlus Live technical support to get the VOD license.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This property takes effect only when the business type (<a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-biztype">bizType</a>) includes Viewer SDK (<code>BDLiveBizTypeViewer</code>).</div>


* <div data-tips="true" data-tips-type="tip">If the VOD license file and the live streaming license file are the same file, set the value of <code>vodLicensePath</code> to be the same as <a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-livelicensepath">liveLicensePath</a>.</div>



<span id="BDLiveAuthInfo-livelicensepath"></span>
### liveLicensePath

```objectivec
@property (nonatomic, copy, nullable) NSString *liveLicensePath;
```


The path of the live streaming license file. Contact BytePlus Live technical support to get the live streaming license.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the live streaming license file and the VOD license file are the same file, set the value of <code>liveLicensePath</code> to be the same as <a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-vodlicensepath">vodLicensePath</a>.</div>


<span id="BDLiveAuthInfo-effectauthinfo"></span>
### effectAuthInfo

```objectivec
@property (nonatomic, strong) BDLiveEffectAuthInfo *effectAuthInfo;
```


The CV license authorization information. Applicable to scenarios requiring beauty AR, filters, and stickers features. For more information, see [BDLiveEffectAuthInfo](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property takes effect only when the business type (<a href="https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-biztype">bizType</a>) includes Live Streaming SDK (<code>BDLiveBizTypeLiveStreaming</code>).</div>


<span id="BDLNoticeType"></span>
# BDLNoticeType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLNoticeType
)
```


The notification type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLNoticeTypeJoinRoom |1 |Entrance message. |
|BDLNoticeTypeGiftReward |2 |Gift message. |
|BDLNoticeTypeAward |3 |Lucky draw notification. |


<span id="BDLMenuViewConfiguration(Config)"></span>
# BDLMenuViewConfiguration(Config)

```objectivec
@interface BDLMenuViewConfiguration (Config)
```


The configuration of the menu bar container view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIFont\* |[titleFont](https://docs.byteplus.com/en/docs/11/17341#BDLMenuViewConfiguration(Config)-titlefont) |
|CGFloat |[titleLineWidth](https://docs.byteplus.com/en/docs/11/17341#BDLMenuViewConfiguration(Config)-titlelinewidth) |


<span id="instructions"></span>
## Instructions

<span id="BDLMenuViewConfiguration(Config)-titlefont"></span>
### titleFont

```objectivec
@property (nonatomic, strong) UIFont *titleFont;
```


The font and font size of the title.

<span id="BDLMenuViewConfiguration(Config)-titlelinewidth"></span>
### titleLineWidth

```objectivec
@property (nonatomic, assign) CGFloat titleLineWidth;
```


The width of the indicator line at the bottom after the title is selected.

<span id="BDLCardConfiguration(Config)"></span>
# BDLCardConfiguration(Config)

```objectivec
@interface BDLCardConfiguration (Config)
```


The product card configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIFont\* |[cardTitleFont](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration(Config)-cardtitlefont) |
|UIFont\* |[strikeThroughFont](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration(Config)-strikethroughfont) |
|UIFont\* |[cardHighLightFont](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration(Config)-cardhighlightfont) |
|BOOL |[itemIndexEnable](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration(Config)-itemindexenable) |
|BOOL |[enableDirectUrl](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration(Config)-enabledirecturl) |


<span id="instructions"></span>
## Instructions

<span id="BDLCardConfiguration(Config)-cardtitlefont"></span>
### cardTitleFont

```objectivec
@property (nonatomic, strong) UIFont *cardTitleFont;
```


The font and font size of the product name.

<span id="BDLCardConfiguration(Config)-strikethroughfont"></span>
### strikeThroughFont

```objectivec
@property (nonatomic, strong) UIFont *strikeThroughFont;
```


The font and font size of the list price.

<span id="BDLCardConfiguration(Config)-cardhighlightfont"></span>
### cardHighLightFont

```objectivec
@property (nonatomic, strong) UIFont *cardHighLightFont;
```


The font and font size of the retail price.

<span id="BDLCardConfiguration(Config)-itemindexenable"></span>
### itemIndexEnable

```objectivec
@property (nonatomic, assign) BOOL itemIndexEnable;
```


Whether to display the serial number of product cards. Default value: `YES`.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="enabledirecturl"></span>
### enableDirectUrl

```objectivec
@property (nonatomic, assign) BOOL enableDirectUrl;
```


Whether the direct URL feature is enabled. Default value: `NO`.


* `YES`: If the BytePlus Live server returns a direct URL, read the direct URL first. If no direct URL is returned, read the product URL.

* `NO`: Regardless of whether the BytePlus Live server returns a direct URL, read the product URL.

    &nbsp;


<span id="bdladvertisementmodel"></span>
# BDLAdvertisementModel

```objectivec
@interface BDLAdvertisementModel : BDLBaseModel
```


The ad model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[Id](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-id) |
|NSInteger |[index](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-index) |
|NSString\* |[advertisementContent](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-advertisementcontent) |
|NSString\* |[advertisementRedirectUrl](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-advertisementredirecturl) |
|BDLPageAdvertisementType |[pageAdvertisementType](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-pageadvertisementtype) |
|CGSize |[scaledSize](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-scaledsize) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[isPageHeaderAd](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-ispageheaderad) |
|BOOL |[isPageAd](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-ispagead) |
|BOOL |[isPageUpperAd](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-ispageupperad) |
|BOOL |[isCardAd](https://docs.byteplus.com/en/docs/11/17341#BDLAdvertisementModel-iscardad) |


<span id="instructions"></span>
## Instructions

<span id="BDLAdvertisementModel-id"></span>
### Id

```objectivec
@property (nonatomic, strong) NSNumber *Id;
```


The ad ID.

<span id="BDLAdvertisementModel-index"></span>
### index

```objectivec
@property (nonatomic, assign) NSInteger index;
```


The ad index.

<span id="BDLAdvertisementModel-advertisementcontent"></span>
### advertisementContent

```objectivec
@property (nonatomic, copy) NSString* advertisementContent;
```


The ad content, which is currently the image URL configured for the ad.

<span id="BDLAdvertisementModel-advertisementredirecturl"></span>
### advertisementRedirectUrl

```objectivec
@property (nonatomic, copy) NSString* advertisementRedirectUrl;
```


The embedded link.

<span id="BDLAdvertisementModel-pageadvertisementtype"></span>
### pageAdvertisementType

```objectivec
@property (nonatomic, assign) BDLPageAdvertisementType pageAdvertisementType;
```


The ad type. For more information, see [BDLPageAdvertisementType](https://docs.byteplus.com/en/docs/11/17341#BDLPageAdvertisementType).

<span id="BDLAdvertisementModel-scaledsize"></span>
### scaledSize

```objectivec
@property (nonatomic, assign) CGSize scaledSize;
```


The size suitable for display after scaling in. Not returned by the BytePlus Live server.

<span id="instructions"></span>
## Instructions

<span id="BDLAdvertisementModel-ispageheaderad"></span>
### isPageHeaderAd

```objectivec
- (BOOL)isPageHeaderAd;
```


Whether it is a header ad.

**Return Value**


* `YES`: A header ad.

* `NO`: Not a header ad.

    &nbsp;


<span id="ispagead"></span>
### isPageAd

```objectivec
- (BOOL)isPageAd;
```


Whether it is an in\-page ad.

**Return Value**


* `YES`: An in\-page ad.

* `NO`: Not an in\-page ad.

    &nbsp;


<span id="ispageupperad"></span>
### isPageUpperAd

```objectivec
- (BOOL)isPageUpperAd;
```


Whether it is a floating ad.

**Return Value**


* `YES`: A floating ad.

* `NO`: Not a floating ad.

    &nbsp;


<span id="iscardad"></span>
### isCardAd

```objectivec
- (BOOL)isCardAd;
```


Whether it is a product card.

**Return Value**


* `YES`: A product card.

* `NO`: Not a product card.

    &nbsp;


<span id="bdlfloatingcontrollerviewtag"></span>
# BDLFloatingControllerViewTag

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLFloatingControllerViewTag
)
```


Type of the floating window view.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLFloatingControllerViewTagInteractiveToolContainer |0 |The container view of the interaction tool. |
|BDLFloatingControllerViewTagUpperAd |100 |The floating ad view. |
|BDLFloatingControllerViewTagCardFirst |300 |The view of the first product card. |
|BDLFloatingControllerViewTagCardSecond |310 |The view of the second product card. |
|BDLFloatingControllerViewTagCardThird |320 |The view of the third product card. |


<span id="BDLForceOfflineReason"></span>
# BDLForceOfflineReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLForceOfflineReason
)
```


Reasons for viewers being forcibly removed from the live room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLForceOfflineReasonMultiLogin |0 |After the repeated login prevention feature is enabled, the same viewer logs in to the same live room on multiple devices simultaneously. |
|BDLForceOfflineReasonCheckInTimeout |1 |Timeout due to not checking in. |
|BDLForceOfflineReasonIPBanned |2 |IP address banned. |
|BDLForceOfflineReasonKickOut |3 |Kicked out. |


<span id="BDLMenuModel"></span>
# BDLMenuModel

```objectivec
@interface BDLMenuModel : BDLBaseModel
```


The model of menu bar information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[name](https://docs.byteplus.com/en/docs/11/17341#BDLMenuModel-name) |
|BDLMenuType |[type](https://docs.byteplus.com/en/docs/11/17341#BDLMenuModel-type) |
|NSInteger |[index](https://docs.byteplus.com/en/docs/11/17341#BDLMenuModel-index) |
|BDLEmbeddedWebModel\* |[localEmbeddedWebModel](https://docs.byteplus.com/en/docs/11/17341#BDLMenuModel-localembeddedwebmodel) |


<span id="instructions"></span>
## Instructions

<span id="BDLMenuModel-name"></span>
### name

```objectivec
@property (nonatomic, copy) NSString *name;
```


The menu name.

<span id="BDLMenuModel-type"></span>
### type

```objectivec
@property (nonatomic, assign) BDLMenuType type;
```


The menu type. For more information, see [BDLMenuType](https://docs.byteplus.com/en/docs/11/17341#BDLMenuType).

<span id="BDLMenuModel-index"></span>
### index

```objectivec
@property (nonatomic, assign) NSInteger index;
```


The display index of the menu.

<span id="BDLMenuModel-localembeddedwebmodel"></span>
### localEmbeddedWebModel

```objectivec
@property (nonatomic, weak) BDLEmbeddedWebModel *localEmbeddedWebModel;
```


The model of embedded link information. Not returned by the BytePlus Live server. For more information, see [BDLEmbeddedWebModel](https://docs.byteplus.com/en/docs/11/17341#BDLEmbeddedWebModel).

<span id="BDLAwardUserModel"></span>
# BDLAwardUserModel

```objectivec
@interface BDLAwardUserModel : BDLBaseModel
```


The model of lucky draw\-related viewer information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLAwardUserStatus |[status](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserModel-status) |
|NSString\* |[address](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserModel-address) |
|NSString\* |[telephone](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserModel-telephone) |
|NSString\* |[receiverName](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserModel-receivername) |
|NSString\* |[awardLotteryTicketAddr](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserModel-awardlotteryticketaddr) |
|NSNumber\* |[awardItemId](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserModel-awarditemid) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardUserModel-status"></span>
### status

```objectivec
@property (nonatomic, assign) BDLAwardUserStatus status;
```


The lucky draw participation status of the viewer. For more information, see [BDLAwardUserStatus](https://docs.byteplus.com/en/docs/11/17341#BDLAwardUserStatus).

<span id="BDLAwardUserModel-address"></span>
### address

```objectivec
@property (nonatomic, copy) NSString *address;
```


The shipping address of the winner.

<span id="BDLAwardUserModel-telephone"></span>
### telephone

```objectivec
@property (nonatomic, copy) NSString *telephone;
```


The phone number of the winner.

<span id="BDLAwardUserModel-receivername"></span>
### receiverName

```objectivec
@property (nonatomic, copy) NSString *receiverName;
```


The recipient name of the winner.

<span id="BDLAwardUserModel-awardlotteryticketaddr"></span>
### awardLotteryTicketAddr

```objectivec
@property (nonatomic, copy) NSString *awardLotteryTicketAddr;
```


The claim link of the voucher prize.

<span id="BDLAwardUserModel-awarditemid"></span>
### awardItemId

```objectivec
@property (nonatomic, strong) NSNumber *awardItemId;
```


The prize ID.

<span id="BDLMenuFilterOption"></span>
# BDLMenuFilterOption

```objectivec
typedef NS_OPTIONS(
    NSUInteger,
    BDLMenuFilterOption
)
```


The menu filter options.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLMenuFilterOptionComment |1 << 0 |The menu for chat interaction. |
|BDLMenuFilterOptionHotComment |1 << 1 |The menu for top comments. |
|BDLMenuFilterOptionImageText |1 << 2 |The menu for graphics. |
|BDLMenuFilterOptionCard |1 << 3 |The menu for product cards. |
|BDLMenuFilterOptionInteractiveTool |1 << 4 |The menu for interaction tools. |
|BDLMenuFilterOptionEmbeddedUrl |BDLMenuFilterOptionPrivateChat << 1 |The menu for embedded link. |
|BDLMenuFilterOptionAll |NSUIntegerMax |All menu options. |


<span id="BDLCommentType"></span>
# BDLCommentType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLCommentType
)
```


The comment type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLCommentTypeMessage |0 |The message from the server, which is the default value. |
|BDLCommentTypeWelcome |1 |The welcome message. |
|BDLCommentTypeLiveDescription |2 |The live room description. |


<span id="BDLBusinessAccountConfiguration(Config)"></span>
# BDLBusinessAccountConfiguration(Config)

```objectivec
@interface BDLBusinessAccountConfiguration (Config)
```


The host account configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[followText](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)-followtext) |
|NSString\* |[followedText](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)-followedtext) |
|UIImage\* |[followBackgroundImage](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)-followbackgroundimage) |
|UIImage\* |[followedBackgroundImage](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)-followedbackgroundimage) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[getUserFollowStatusBlock](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)-getuserfollowstatusblock) |
|void |[onFollowClickBlock](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)-onfollowclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLBusinessAccountConfiguration(Config)-followtext"></span>
### followText

```objectivec
@property (nonatomic, copy) NSString *followText;
```


The button text when the host is not followed.

<span id="BDLBusinessAccountConfiguration(Config)-followedtext"></span>
### followedText

```objectivec
@property (nonatomic, copy) NSString *followedText;
```


The button text when the host is followed.

<span id="BDLBusinessAccountConfiguration(Config)-followbackgroundimage"></span>
### followBackgroundImage

```objectivec
@property (nonatomic, strong) UIImage *followBackgroundImage;
```


The background image of the button when the host is not followed.

<span id="BDLBusinessAccountConfiguration(Config)-followedbackgroundimage"></span>
### followedBackgroundImage

```objectivec
@property (nonatomic, strong) UIImage *followedBackgroundImage;
```


The background image of the button when the host is followed.

<span id="instructions"></span>
## Instructions

<span id="BDLBusinessAccountConfiguration(Config)-getuserfollowstatusblock"></span>
### getUserFollowStatusBlock

```objectivec
@property (nonatomic, copy) void(^getUserFollowStatusBlock)(BDLHostFollowInfoModel *model, void(^complete)(BOOL followed));
```


The SDK calls this method to get the viewer's follow status when the button to follow the host is displayed. You can implement the specific logic for getting the follow status within this method and return the result through the `complete` callback upon completion.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|model |BDLHostFollowInfoModel\* |The information required to follow the host. For more information, see [BDLHostFollowInfoModel](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel). |
|complete |void(^)(BOOL followed) |The callback triggered when the viewer's follow status is obtained.<br><br>&nbsp;<br><br>Input parameters:<br><br>&nbsp;<br><br>`followed`: Whether the viewer has followed the host.<br><br><br>* `YES`: Followed.<br><br>* `NO`: Not followed. |


<span id="BDLBusinessAccountConfiguration(Config)-onfollowclickblock"></span>
### onFollowClickBlock

```objectivec
@property (nonatomic, copy) void(^onFollowClickBlock)(BDLHostFollowInfoModel *model, BOOL followed, void(^complete)(BOOL followed));
```


The SDK calls this method when the viewer taps the button to follow or unfollow the host. You can implement the specific logic for following or unfollowing the host within this method and return the result through the `complete` callback upon completion.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|model |BDLHostFollowInfoModel\* |The information required to follow the host. For more information, see [BDLHostFollowInfoModel](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel). |
|followed |BOOL |The follow status when the viewer taps the button.<br><br><br>* `YES`: Followed.<br><br>* `NO`: Not followed. |
|complete |void(^)(BOOL followed) |The callback triggered when the viewer's follow or unfollow action is completed.<br><br>&nbsp;<br><br>Input parameters:<br><br>&nbsp;<br><br>`followed`: The viewer's latest follow status.<br><br><br>* `YES`: Followed.<br><br>* `NO`: Not followed. |


<span id="BDLPopupBaseViewShowDirection"></span>
# BDLPopupBaseViewShowDirection

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLPopupBaseViewShowDirection
)
```


The display direction of the dialog box.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPopupBaseViewShowDirectionBottom |0 |At the bottom. |
|BDLPopupBaseViewShowDirectionCenter |1 |In the center. |
|BDLPopupBaseViewShowDirectionRight |2 |On the right. |
|BDLPopupBaseViewShowDirectionTop |3 |At the top. |


<span id="BDLMenuType"></span>
# BDLMenuType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLMenuType
)
```


The menu type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLMenuTypeImageText |1 |Graphics. |
|BDLMenuTypeCard |2 |Product cards. |
|BDLMenuTypeComment |3 |Chat interaction. |
|BDLMenuTypeInteractiveTool |4 |Interaction tools. |
|BDLMenuTypeEmbeddedWebUrl |7 |Embedded link. |


<span id="BDLPlayerSpeed"></span>
# BDLPlayerSpeed

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLPlayerSpeed
)
```


The playback speed.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPlayerSpeed200X |0 |2x speed. |
|BDLPlayerSpeed150X |1 |1.5x speed. |
|BDLPlayerSpeed125X |2 |1.25x speed. |
|BDLPlayerSpeed100X |3 |Normal speed. |
|BDLPlayerSpeed075X |4 |0.75x speed. |
|BDLPlayerSpeed050X |5 |0.5x speed. |


<span id="BDLPlayerLoadState"></span>
# BDLPlayerLoadState

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLPlayerLoadState
)
```


The loading status of the player.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPlayerLoadStateUnknown |0 |Unknown. |
|BDLPlayerLoadStateStalled |1 |Stuttering. |
|BDLPlayerLoadStatePlayable |2 |Playable, without stuttering. |
|BDLPlayerLoadStateError |3 |An error occurred while loading. |


<span id="BDLMenuBarConfiguration"></span>
# BDLMenuBarConfiguration

```objectivec
@interface BDLMenuBarConfiguration : BDLRTBaseConfiguration
```


The menu bar configuration.

<span id="BDLGetInviteTokenResult"></span>
# BDLGetInviteTokenResult

```objectivec
@interface BDLGetInviteTokenResult : BDLBaseModel
```


The result after getting the invitation information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[inviterName](https://docs.byteplus.com/en/docs/11/17341#BDLGetInviteTokenResult-invitername) |
|NSString\* |[inviterToken](https://docs.byteplus.com/en/docs/11/17341#BDLGetInviteTokenResult-invitertoken) |


<span id="instructions"></span>
## Instructions

<span id="BDLGetInviteTokenResult-invitername"></span>
### inviterName

```objectivec
@property (nonatomic, copy) NSString *inviterName;
```


The sharer's nickname.

<span id="BDLGetInviteTokenResult-invitertoken"></span>
### inviterToken

```objectivec
@property (nonatomic, copy) NSString *inviterToken;
```


The sharer's invitation token.

<span id="BDLPopupTopCommentViewConfiguration(Config)"></span>
# BDLPopupTopCommentViewConfiguration(Config)

```objectivec
@interface BDLPopupTopCommentViewConfiguration (Config)
```


The configuration of the pinned comment details dialog box.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CGFloat |[viewHeight](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-viewheight) |
|NSString\* |[colorTheme](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-colortheme) |
|UIColor\* |[portraitContentBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-portraitcontentbackgroundcolor) |
|UIColor\* |[portraitTopFontColor](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-portraittopfontcolor) |
|UIFont\* |[contentFont](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-contentfont) |
|BOOL |[topTitleAlignmentLeft](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-toptitlealignmentleft) |
|BOOL |[commentUrlFloatingEnable](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)-commenturlfloatingenable) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupTopCommentViewConfiguration(Config)-viewheight"></span>
### viewHeight

```objectivec
@property (nonatomic, assign) CGFloat viewHeight;
```


The height of the content area. Default value: 400. Unit: points.

<span id="BDLPopupTopCommentViewConfiguration(Config)-colortheme"></span>
### colorTheme

```objectivec
@property (nonatomic, copy, nullable) NSString *colorTheme;
```


The color theme. If the parameter value is `custom` or `light`, the content area color is white. Otherwise, the color is black (#20202A).

<span id="BDLPopupTopCommentViewConfiguration(Config)-portraitcontentbackgroundcolor"></span>
### portraitContentBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *portraitContentBackgroundColor;
```


The background color for the live room in portrait mode.

<span id="BDLPopupTopCommentViewConfiguration(Config)-portraittopfontcolor"></span>
### portraitTopFontColor

```objectivec
@property (nonatomic, strong) UIColor *portraitTopFontColor;
```


The text color for the live room in portrait mode.

<span id="BDLPopupTopCommentViewConfiguration(Config)-contentfont"></span>
### contentFont

```objectivec
@property (nonatomic, strong) UIFont *contentFont;
```


The font and font size of the dialog box content.

<span id="BDLPopupTopCommentViewConfiguration(Config)-toptitlealignmentleft"></span>
### topTitleAlignmentLeft

```objectivec
@property (nonatomic, assign) BOOL topTitleAlignmentLeft;
```


Whether the dialog box title is left\-aligned. Default value: `NO`.


* `YES`: Left\-aligned.

* `NO`: Center\-aligned.

    &nbsp;


<span id="commenturlfloatingenable"></span>
### commentUrlFloatingEnable

```objectivec
@property (nonatomic, assign) BOOL commentUrlFloatingEnable;
```


Whether the redirected content is displayed on a floating page in the live room after a URL in the comment is tapped. Default value: `NO`.


* `YES`: The redirected content is displayed on a floating page in the live room. Viewers can watch the video and view the redirected content at the same time.

* `NO`: The redirected content is displayed on a new browser tab. Viewers cannot watch the video and view the redirected content at the same time.

    &nbsp;


<span id="bdlfloatingcontroller"></span>
# BDLFloatingController

```objectivec
@interface BDLFloatingController : NSObject <
BDLPageUpperAdService
, BDLMenuService
, BDLDraggingDelegate
>
```


The floating window controller.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[superview](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-superview) |
|BOOL |[hideAllFloatingView](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-hideallfloatingview) |
|UIView\* |[upperAdView](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-upperadview) |
|UIStackView\* |[floatingInteractiveToolContainerView](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-floatinginteractivetoolcontainerview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[openUrlBlock](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-openurlblock) |
|void |[insertFloatingView:position:dragMode:](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-insertfloatingview-position-dragmode) |
|void |[removeInsertedFloatingView:](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-removeinsertedfloatingview) |
|void |[setFloatShoppingCardMovable:](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-setfloatshoppingcardmovable) |
|void |[setFloatAdMovable:](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-setfloatadmovable) |
|BDLBaseView |[customizeUpperAdView](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-customizeupperadview) |
|BOOL |[customizeFloatingCardView](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-customizefloatingcardview) |
|UIStackView\* |[customizeInteractiveToolContainerView](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingController-customizeinteractivetoolcontainerview) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingController-superview"></span>
### superview

```objectivec
@property (nonatomic, strong, readonly) UIView *superview;
```


The view that displays the floating window.

<span id="BDLFloatingController-hideallfloatingview"></span>
### hideAllFloatingView

```objectivec
@property (nonatomic, assign, readonly) BOOL hideAllFloatingView;
```


Whether to hide all the floating windows.


* `YES`: Hide all the floating windows.

* `NO`: Display all the floating windows that should be displayed.

    &nbsp;


<span id="upperadview"></span>
### upperAdView

```objectivec
@property (nonatomic, strong, readonly) UIView *upperAdView;
```


The floating ad view.

<span id="BDLFloatingController-floatinginteractivetoolcontainerview"></span>
### floatingInteractiveToolContainerView

```objectivec
@property (nonatomic, strong, readonly) UIStackView *floatingInteractiveToolContainerView;
```


The container view of the interaction tool floating window view.

<span id="instructions"></span>
## Instructions

<span id="BDLFloatingController-openurlblock"></span>
### openUrlBlock

```objectivec
@property (nonatomic, copy, nullable) void(^openUrlBlock)(BDLFloatingController *floatingController, NSURL *url, BOOL isFloatingEnable);
```


The block is called when the floating window needs to open a URL.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingController |BDLFloatingController\* |The floating window controller. |
|url |NSURL\* |The URL that needs to be opened. |
|isFloatingEnable |BOOL |Whether the redirected content is displayed on a floating page in the live room.<br><br><br>* `YES`: The redirected content is displayed on a floating page in the live room. Viewers can watch the video and view the redirected content at the same time.<br><br>* `NO`: The redirected content is displayed on a new browser tab. Viewers cannot watch the video and view the redirected content at the same time. |


<span id="BDLFloatingController-insertfloatingview-position-dragmode"></span>
### insertFloatingView:position:dragMode:

```objectivec
- (void)insertFloatingView:(UIView *)view
                  position:(BDLFloatingControllerInsertPosition)position
                  dragMode:(BDLDraggingMode)dragMode;
```


Inserts a custom floating view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |UIView\* |The custom floating view, which can be inserted into a specific position in the live room. The views are arranged from top to bottom according to their `view.tag` values (the smaller the tag value, the higher the position), without affecting the views' hierarchy structure. For tags of the existing view, see [BDLFloatingControllerViewTag](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingControllerViewTag). |
|position |BDLFloatingControllerInsertPosition |The position to insert in the live room. For more information, see [BDLFloatingControllerInsertPosition](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingControllerInsertPosition). |
|dragMode |BDLDraggingMode |The dragging mode. For more information, see [BDLDraggingMode](https://docs.byteplus.com/en/docs/11/17341#BDLDraggingMode). |


<span id="BDLFloatingController-removeinsertedfloatingview"></span>
### removeInsertedFloatingView:

```objectivec
- (void)removeInsertedFloatingView:(UIView *)view;
```


Removes the inserted custom floating view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |UIView\* |The view that needs to be removed. |


<span id="BDLFloatingController-setfloatshoppingcardmovable"></span>
### setFloatShoppingCardMovable:

```objectivec
- (void)setFloatShoppingCardMovable:(BOOL)floatShoppingCardMovable;
```


Whether the floating product card can be dragged.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatShoppingCardMovable |BOOL |Whether the floating product card can be dragged. Default value: `NO`. Valid values:<br><br><br>* `YES`: Can be dragged.<br><br>* `NO`: Cannot be dragged. |


<span id="BDLFloatingController-setfloatadmovable"></span>
### setFloatAdMovable:

```objectivec
- (void)setFloatAdMovable:(BOOL)floatAdMovable;
```


Whether the floating ad can be dragged.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatAdMovable |BOOL |Whether the floating ad can be dragged. Default value: `NO`. Valid values:<br><br><br>* `YES`: Can be dragged.<br><br>* `NO`: Cannot be dragged. |


<span id="BDLFloatingController-customizeupperadview"></span>
### customizeUpperAdView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeUpperAdView)(BDLFloatingController *floatingController, BDLUpperAdView *view);
```


Customizes the floating ad view. The `BDLUpperAdView` involves dragging, so set the `view.frame` to adjust its position instead of using auto layout. However, the interior and subviews of `BDLUpperAdView` use the auto layout.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingController |BDLFloatingController\* |The floating window controller. |
|view |BDLUpperAdView\* |The floating ad view. For more information, see [BDLUpperAdView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLUpperAdView). |


**Return Value**

Instances of `BDLBaseView` and its subclasses.

<span id="BDLFloatingController-customizefloatingcardview"></span>
### customizeFloatingCardView

```objectivec
@property (nonatomic, copy, nullable) BOOL (^customizeFloatingCardView)(BDLFloatingController *floatingController, BDLFloatingCardView *view);
```


Customizes the floating product card view. Size setting is not supported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingController |BDLFloatingController\* |The floating window controller. |
|view |BDLFloatingCardView\* |The floating product card view. For more information, see [BDLFloatingCardView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingCardView). |


**Return Value**

Whether to display the floating window product card view.


* `YES`: Displays the floating window product card view.

* `NO`: Hides the floating window product card view.

    &nbsp;


<span id="customizeinteractivetoolcontainerview"></span>
### customizeInteractiveToolContainerView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIStackView * _Nullable (^customizeInteractiveToolContainerView)(BDLFloatingController *floatingController, UIStackView *view);
```


Customizes the container view of the interaction tool floating window view. `interactiveToolContainerView` involves dragging, so set the `view.frame` to adjust its position instead of using auto layout. However, the interior and subviews of `interactiveToolContainerView` use the auto layout.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingController |BDLFloatingController\* |The floating window controller. |
|view |UIStackView\* |The container view of the interaction tool floating window view. |


**Return Value**

Instances of `UIStackView` and its subclasses.

<span id="BDLInteractiveAwardType"></span>
# BDLInteractiveAwardType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveAwardType
)
```


The draw type for the lucky draw.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveAwardTypeAuto |1 |Automatic draw. |
|BDLInteractiveAwardTypeManual |2 |Manual draw. |


<span id="BDLPopupInputViewConfiguration"></span>
# BDLPopupInputViewConfiguration

```objectivec
@interface BDLPopupInputViewConfiguration : BDLRTBaseConfiguration
```


The configuration of nickname text box.

<span id="BDLQuestionnaireTrigger"></span>
# BDLQuestionnaireTrigger

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLQuestionnaireTrigger
)
```


The send time of the questionnaire.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLQuestionnaireTriggerUnknown |0 |Unknown. |
|BDLQuestionnaireTriggerManual |1 |Send manually. |
|BDLQuestionnaireTriggerLivePageIn |2 |When viewers join the live room. |
|BDLQuestionnaireTriggerLiveEnd |3 |When the live stream ends. |


<span id="BDLPlayerLandscapeConfiguration"></span>
# BDLPlayerLandscapeConfiguration

```objectivec
@interface BDLPlayerLandscapeConfiguration : BDLPlayerBaseConfiguration
```


The player configuration for the live room in landscape mode.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLPlayerControlViewMode |[controlViewMode](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerLandscapeConfiguration-controlviewmode) |
|UIColor\* |[replayViewBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerLandscapeConfiguration-replayviewbackgroundcolor) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerLandscapeConfiguration-controlviewmode"></span>
### controlViewMode

```objectivec
@property (nonatomic, assign) BDLPlayerControlViewMode controlViewMode;
```


The player control style. For more information, see [BDLPlayerControlViewMode](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerControlViewMode).

<span id="BDLPlayerLandscapeConfiguration-replayviewbackgroundcolor"></span>
### replayViewBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *replayViewBackgroundColor;
```


The background color of the replay interface.

<span id="BDLNetworkQuality"></span>
# BDLNetworkQuality

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLNetworkQuality
)
```


Network quality.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLNetworkQualityUnknown |0 |Unknown. |
|BDLNetworkQualityExcellent |1 |Excellent. |
|BDLNetworkQualityPoor |2 |Moderate. |
|BDLNetworkQualityBad |3 |Poor. |
|BDLNetworkQualityOffLine |NSIntegerMax |Offline. |


<span id="BDLSendMessageResultStatus"></span>
# BDLSendMessageResultStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLSendMessageResultStatus
)
```


The status after sending a comment.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLSendMessageResultStatusSuccess |1 |Sent successfully. |
|BDLSendMessageResultStatusImgUriError |2 |The image resource URL validation error occurred, meaning the image does not exist or does not belong to the current account. |
|BDLSendMessageResultStatusSecurityAuditError |3 |Security review API error. Retry. |
|BDLSendMessageResultStatusSecurityAuditNotSafe |4 |Failed to pass the security review. |


<span id="BDLAwardConfiguration(Config)"></span>
# BDLAwardConfiguration(Config)

```objectivec
@interface BDLAwardConfiguration (Config)
```


The lucky draw configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[needAwardContact](https://docs.byteplus.com/en/docs/11/17341#BDLAwardConfiguration(Config)-needawardcontact) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardConfiguration(Config)-needawardcontact"></span>
### needAwardContact

```objectivec
@property (nonatomic, assign) BOOL needAwardContact;
```


Whether personal information is required after winning a prize. Default value: `YES`.


* `YES`: Required.

* `NO`: Not required.

    &nbsp;


<span id="bdlbaseplayerconfiguration"></span>
# BDLBasePlayerConfiguration

```objectivec
@interface BDLBasePlayerConfiguration : NSObject
```


The custom player configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[liveAutoPlay](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-liveautoplay) |
|BOOL |[previewAutoPlay](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-previewautoplay) |
|BOOL |[playbackAutoPlay](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-playbackautoplay) |
|BOOL |[previewAutoReplay](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-previewautoreplay) |
|BOOL |[playbackAutoReplay](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-playbackautoreplay) |
|BOOL |[vodAutoContinuePlayback](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-vodautocontinueplayback) |
|BOOL |[isNeedAutoDemote](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-isneedautodemote) |
|BOOL |[backupDowngradeWhenStall](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-backupdowngradewhenstall) |
|BOOL |[shouldHandleRemoteCommand](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-shouldhandleremotecommand) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|NSDictionary<NSString\*, id\>\* |[customizeNowPlayingInfoBlock](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-customizenowplayinginfoblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLBasePlayerConfiguration-liveautoplay"></span>
### liveAutoPlay

```objectivec
@property (nonatomic, assign) BOOL liveAutoPlay;
```


Whether to autoplay the live stream. Default value: `YES`.


* `YES`: Autoplay.

* `NO`: Do not autoplay.

    &nbsp;


<span id="previewautoplay"></span>
### previewAutoPlay

```objectivec
@property (nonatomic, assign) BOOL previewAutoPlay;
```


Whether to autoplay the preview. Default value: `YES`.


* `YES`: Autoplay.

* `NO`: Do not autoplay.

    &nbsp;


<span id="playbackautoplay"></span>
### playbackAutoPlay

```objectivec
@property (nonatomic, assign) BOOL playbackAutoPlay;
```


Whether to autoplay the playback. Default value: `YES`.


* `YES`: Autoplay.

* `NO`: Do not autoplay.

    &nbsp;


<span id="previewautoreplay"></span>
### previewAutoReplay

```objectivec
@property (nonatomic, assign) BOOL previewAutoReplay;
```


Whether to automatically replay after the preview ends. Default value: `YES`.


* `YES`: Automatically replay.

* `NO`: Do not automatically replay.

    &nbsp;


<span id="playbackautoreplay"></span>
### playbackAutoReplay

```objectivec
@property (nonatomic, assign) BOOL playbackAutoReplay;
```


Whether to automatically replay after the playback ends. Default value: `YES`.


* `YES`: Automatically replay.

* `NO`: Do not automatically replay.

    &nbsp;


<span id="vodautocontinueplayback"></span>
### vodAutoContinuePlayback

```objectivec
@property (nonatomic, assign) BOOL vodAutoContinuePlayback;
```


Whether to enable automatic breakpoint resumption for VOD videos. Default value: `YES`.


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="isneedautodemote"></span>
### isNeedAutoDemote

```objectivec
@property (nonatomic, assign) BOOL isNeedAutoDemote;
```


Whether to support automatic downgrade or provide a prompt in case of stuttering during the live stream. Default value: `YES`.


* `YES`:

   * If the value of [backupDowngradeWhenStall](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-backupdowngradewhenstall) is `YES`, directly switch between the primary and backup streams.

   * If the value of [backupDowngradeWhenStall](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-backupdowngradewhenstall) is `NO`, in smart mode, automatically downgrade to a lower resolution. If stuttering still occurs at the lowest resolution, switch between the primary and backup streams. In non\-smart mode, provide a prompt to viewers asking whether to switch to a lower resolution, allowing them to choose as needed. If stuttering still occurs after viewers switch to the lowest resolution, switch between the primary and backup streams.

* `NO`: In smart mode, do not automatically downgrade. In non\-smart mode, do not notify viewers to switch to a lower resolution.

    &nbsp;


<span id="backupdowngradewhenstall"></span>
### backupDowngradeWhenStall

```objectivec
@property (nonatomic, assign) BOOL backupDowngradeWhenStall;
```


Whether to switch between the primary and backup streams directly in case of stuttering during the live stream. Default value: `NO`. This property takes effect only when the value of [isNeedAutoDemote](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration-isneedautodemote) is `YES`.


* `YES`: Directly switch between the primary and backup streams.

* `NO`: In smart mode, automatically downgrade to a lower resolution. If stuttering still occurs at the lowest resolution, switch between the primary and backup streams. In non\-smart mode, provide a prompt to viewers asking whether to switch to a lower resolution, allowing them to choose as needed. If stuttering still occurs after viewers switch to the lowest resolution, switch between the primary and backup streams.

    &nbsp;


<span id="shouldhandleremotecommand"></span>
### shouldHandleRemoteCommand

```objectivec
@property (nonatomic, assign) BOOL shouldHandleRemoteCommand;
```


Whether to respond to user actions in the Now Playing information section.

Default value: `YES`. For more information, see [MPRemoteCommandCenter](https://developer.apple.com/documentation/mediaplayer/mpremotecommandcenter?language=objc).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71c238a4a84348d3833ad3942d38ede2~tplv-goo7wpa0wc-image.image) </span>


* `YES`: Respond.

* `NO`: Do not respond.


<span id="instructions"></span>
## Instructions

<span id="BDLBasePlayerConfiguration-customizenowplayinginfoblock"></span>
### customizeNowPlayingInfoBlock

```objectivec
@property (nonatomic, copy, nullable) NSDictionary<NSString *, id> * _Nullable (^customizeNowPlayingInfoBlock)(NSDictionary<NSString *, id> *nowPlayingInfo);
```


The SDK calls this method when you need to customize the Now Playing information. By calling this method, you can modify the Now Playing information automatically generated by the player to display custom information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71c238a4a84348d3833ad3942d38ede2~tplv-goo7wpa0wc-image.image) </span>

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|nowPlayingInfo |NSDictionary<NSString\*, id\>\* |The Now Playing information automatically generated by the player. |


**Return Value**

The custom information modified based on the passed `nowPlayingInfo`, which is the final Now Playing information. If you do not want to display any information in the Now Playing information section, return `nil`. For more information, see [MPNowPlayingInfoCenter](https://developer.apple.com/documentation/mediaplayer/mpnowplayinginfocenter?language=objc).

<span id="BDLBaseView"></span>
# BDLBaseView

```objectivec
@interface BDLBaseView : UIView
```


The base view. The service will be automatically registered within the SDK.

<span id="BDLAwardConfiguration"></span>
# BDLAwardConfiguration

```objectivec
@interface BDLAwardConfiguration : BDLRTBaseConfiguration
```


The lucky draw configuration.

<span id="BDLVoteQuizOptionModel"></span>
# BDLVoteQuizOptionModel

```objectivec
@interface BDLVoteQuizOptionModel : BDLBaseModel
```


The model of quiz and vote options.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[optionSite](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel-optionsite) |
|NSString\* |[optionName](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel-optionname) |
|NSString\* |[optionPercent](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel-optionpercent) |
|NSInteger |[optionCount](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel-optioncount) |
|BOOL |[selected](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel-selected) |


<span id="instructions"></span>
## Instructions

<span id="BDLVoteQuizOptionModel-optionsite"></span>
### optionSite

```objectivec
@property (nonatomic, copy) NSString *optionSite;
```


The option index.

<span id="BDLVoteQuizOptionModel-optionname"></span>
### optionName

```objectivec
@property (nonatomic, copy) NSString *optionName;
```


The option content.

<span id="BDLVoteQuizOptionModel-optionpercent"></span>
### optionPercent

```objectivec
@property (nonatomic, copy) NSString *optionPercent;
```


The percentage of people who chose this option.

<span id="BDLVoteQuizOptionModel-optioncount"></span>
### optionCount

```objectivec
@property (nonatomic, assign) NSInteger optionCount;
```


The number of people who chose this option.

<span id="BDLVoteQuizOptionModel-selected"></span>
### selected

```objectivec
@property (nonatomic, assign) BOOL selected;
```


Whether the current viewer chose this option.


* `YES`: Chose.

* `NO`: Did not choose.

    &nbsp;


<span id="bdlinteractivequiztitletype"></span>
# BDLInteractiveQuizTitleType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveQuizTitleType
)
```


The quiz type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveQuizTitleTypeSingle |0 |Choose one. |
|BDLInteractiveQuizTitleTypeMultiple |1 |Choose all that apply. |


<span id="BDLUserInfoConfiguration"></span>
# BDLUserInfoConfiguration

```objectivec
@interface BDLUserInfoConfiguration : NSObject
```


The user information configuration.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setNickname:complete:](https://docs.byteplus.com/en/docs/11/17341#BDLUserInfoConfiguration-setnickname-complete) |


<span id="instructions"></span>
## Instructions

<span id="BDLUserInfoConfiguration-setnickname-complete"></span>
### setNickname:complete:

```objectivec
- (void)setNickname:(NSString *)nickname complete:(void (^)(BOOL success,  NSError * _Nullable error))complete;
```


Sets the user nickname when the authentication mode ([authMode](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLActivity-authmode)) of the live room is set to public (`BDLActivityAuthModePublic`).

You must call this method before viewers join the live room. When viewers join the live room successfully, SDK uses the value of `nickname` to complete the nickname registration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|nickname |NSString\* |The nickname. No action is taken if `nil`. |
|complete |void(^)(BOOL success, NSError\* error) |The callback triggered when the nickname registration is completed.<br><br>Input parameters:<br><br><br>* `success`: Whether the nickname registration is successful.<br><br>   * `YES`: Successful.<br><br>   * `NO`: Failed. Upon the next nickname registration attempt, for example, when viewers tap the comment text box, SDK uses the value of `nickname` to complete the nickname registration, and this callback is triggered. If the nickname registration still fails, the process continues on the next nickname registration attempt until it succeeds.<br><br>* `error`: The error information. |


<span id="BDLShoppingCardClickPosition"></span>
# BDLShoppingCardClickPosition

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLShoppingCardClickPosition
)
```


The product card tap source.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLShoppingCardClickPositionFloatingCardView |1 |The floating product card view. |
|BDLShoppingCardClickPositionCardView |2 |The card list view. |
|BDLShoppingCardClickPositionCardSearchView |3 |The product card search result view. |
|BDLShoppingCardClickPositionBuyAndOrderedNoticeView |4 |The "Buy Now" view in the chat area for viewing product messages and order messages. |


<span id="BDLAwardContactOptions"></span>
# BDLAwardContactOptions

```objectivec
typedef NS_OPTIONS(
    NSInteger,
    BDLAwardContactOptions
)
```


The type of information that prize winners must enter.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLAwardContactOptionsNone |0 |No information required. |
|BDLAwardContactOptionsPhone |1 |Phone number. |
|BDLAwardContactOptionsAddress |1 << 1 |Shipping address. |
|BDLAwardContactOptionsReceiver |1 << 2 |Recipient. |


<span id="BDLPlayerScalingMode"></span>
# BDLPlayerScalingMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLPlayerScalingMode
)
```


The video scaling mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPlayerScalingModeAspectFit |0 |Fill the player and keep the video's aspect ratio. The width or height of the video fills the width or height of the player. If the aspect ratio of the video is different from that of the player, the video is scaled to fit, with no content cropping. |
|BDLPlayerScalingModeAspectFill |1 |Fill the player and keep the video's aspect ratio. The width of the video fills the width of the player, and the height of the video fills the height of the player. If the aspect ratio of the video is different from that of the player, the video is cropped to fit. |
|BDLPlayerScalingModeFill |2 |Fill the player with the video. The aspect ratio of the video may be changed. |


<span id="BDLMoreOptionsController"></span>
# BDLMoreOptionsController

```objectivec
@interface BDLMoreOptionsController : NSObject <BDLLanguageService, BDLBasicService, BDLMoreOptionsProvider>
```


The more options dialog box controller, which implements the show and hide logic for the buttons of language switching, screen clearing, sharing, and resolution selection in the more options dialog box.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The more options dialog box is displayed after viewers tap the more (...) icon in the lower\-right corner of the live room in portrait mode.</div>


<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLMoreOptionsViewBlock |[multiLanguageClickBlock](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsController-multilanguageclickblock) |
|BDLMoreOptionsViewBlock |[clearScreenClickBlock](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsController-clearscreenclickblock) |
|BDLMoreOptionsViewBlock |[resolutionClickBlock](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsController-resolutionclickblock) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[multiLanguageChangeBlock](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsController-multilanguagechangeblock) |
|void |[modelsChangeBlock](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsController-modelschangeblock) |
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsController-initwithportrait) |


<span id="instructions"></span>
## Instructions

<span id="BDLMoreOptionsController-multilanguageclickblock"></span>
### multiLanguageClickBlock

```objectivec
@property (nonatomic, copy, nullable) BDLMoreOptionsViewBlock multiLanguageClickBlock;
```


The callback is triggered when the switch language button is tapped. For more information, see [BDLMoreOptionsViewBlock](https://docs.byteplus.com/en/docs/11/17341#bdlmoreoptionsviewblock).

<span id="BDLMoreOptionsController-clearscreenclickblock"></span>
### clearScreenClickBlock

```objectivec
@property (nonatomic, copy, nullable) BDLMoreOptionsViewBlock clearScreenClickBlock;
```


The callback is triggered when the clear screen button is tapped. For more information, see [BDLMoreOptionsViewBlock](https://docs.byteplus.com/en/docs/11/17341#bdlmoreoptionsviewblock).

<span id="BDLMoreOptionsController-resolutionclickblock"></span>
### resolutionClickBlock

```objectivec
@property (nonatomic, copy, nullable) BDLMoreOptionsViewBlock resolutionClickBlock;
```


The callback is triggered when the select resolution button is tapped. For more information, see [BDLMoreOptionsViewBlock](https://docs.byteplus.com/en/docs/11/17341#bdlmoreoptionsviewblock).

<span id="instructions"></span>
## Instructions

<span id="BDLMoreOptionsController-multilanguagechangeblock"></span>
### multiLanguageChangeBlock

```objectivec
@property (nonatomic, copy, nullable) void(^ multiLanguageChangeBlock)(BDLMoreOptionsController *controller);
```


The callback is triggered when the language of the viewing page is changed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMoreOptionsController\* |The more options dialog box controller. |


<span id="BDLMoreOptionsController-modelschangeblock"></span>
### modelsChangeBlock

```objectivec
@property (nonatomic, copy, nullable) void(^ modelsChangeBlock)(BDLMoreOptionsController *controller);
```


The callback is triggered when the display status of the buttons for language switching, screen clearing, sharing, or resolution selection is changed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMoreOptionsController\* |The controller of the more options dialog box. |


<span id="BDLMoreOptionsController-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the more options dialog box controller.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the more options dialog box controller.

<span id="BDLHostFollowInfoModel"></span>
# BDLHostFollowInfoModel

```objectivec
@interface BDLHostFollowInfoModel : BDLBaseModel
```


The information required to follow the host.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[externalId](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel-externalid) |
|NSString\* |[externalName](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel-externalname) |
|NSNumber\* |[activityId](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel-activityid) |
|NSNumber\* |[hostAccountId](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel-hostaccountid) |
|NSString\* |[hostAccountName](https://docs.byteplus.com/en/docs/11/17341#BDLHostFollowInfoModel-hostaccountname) |


<span id="instructions"></span>
## Instructions

<span id="BDLHostFollowInfoModel-externalid"></span>
### externalId

```objectivec
@property (nonatomic, copy) NSString *externalId;
```


The external user ID, which is the unique identifier for viewers on third\-party platforms. This ID is the `UserIdStr` parameter passed when calling [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi).

<span id="BDLHostFollowInfoModel-externalname"></span>
### externalName

```objectivec
@property (nonatomic, copy) NSString *externalName;
```


The viewer's nickname, which is the `Nickname` parameter passed when calling [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi).

<span id="BDLHostFollowInfoModel-activityid"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


The activity ID of the live room.

<span id="BDLHostFollowInfoModel-hostaccountid"></span>
### hostAccountId

```objectivec
@property (nonatomic, strong) NSNumber *hostAccountId;
```


The host account ID.

<span id="BDLHostFollowInfoModel-hostaccountname"></span>
### hostAccountName

```objectivec
@property (nonatomic, copy) NSString *hostAccountName;
```


The host account name.

<span id="BDLPlayerCommonConfiguration"></span>
# BDLPlayerCommonConfiguration

```objectivec
@interface BDLPlayerCommonConfiguration : NSObject
```


The common configuration of the player.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImage\* |[playButtonNormalImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-playbuttonnormalimage) |
|UIImage\* |[playButtonSelectedImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-playbuttonselectedimage) |
|UIImage\* |[centerPlayButtonNormalImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-centerplaybuttonnormalimage) |
|UIImage\* |[refreshButtonNormalImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-refreshbuttonnormalimage) |
|BOOL |[refreshButtonLocation](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-refreshbuttonlocation) |
|UIImage\* |[fullScreenButtonNormalImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-fullscreenbuttonnormalimage) |
|UIImage\* |[fullScreenButtonSelectedImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-fullscreenbuttonselectedimage) |
|BOOL |[enterFullScreenEnable](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-enterfullscreenenable) |
|UIImage\* |[exitFullScreenButtonNormalImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-exitfullscreenbuttonnormalimage) |
|UIColor\* |[themeColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-themecolor) |
|UIColor\* |[currentTimeColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-currenttimecolor) |
|UIColor\* |[totalTimeColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-totaltimecolor) |
|UIFont\* |[toastFont](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-toastfont) |
|CGFloat |[toastCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-toastcornerradius) |
|CGFloat |[toastHorizontalEdge](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-toasthorizontaledge) |
|CGFloat |[toastVerticalEdge](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-toastverticaledge) |
|CGFloat |[toastCenterYOffset](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-toastcenteryoffset) |
|NSInteger |[wwanPromptCount](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-wwanpromptcount) |
|NSString\* |[viaWWANText](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-viawwantext) |
|NSString\* |[networkNotReachableText](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-networknotreachabletext) |
|UIColor\* |[promptTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-prompttextcolor) |
|BOOL |[enableAudioPreemption](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-enableaudiopreemption) |
|BOOL |[enableBackgroundAudio](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-enablebackgroundaudio) |
|BOOL |[enableLivePiP](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-enablelivepip) |
|BOOL |[enableVodPiP](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-enablevodpip) |
|UIImage\* |[floatingCloseImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-floatingcloseimage) |
|CGSize |[floatingCloseImageSize](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-floatingcloseimagesize) |
|CGFloat |[floatingViewBorderWidth](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-floatingviewborderwidth) |
|UIColor\* |[floatingViewBorderColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-floatingviewbordercolor) |
|CGFloat |[floatingViewCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-floatingviewcornerradius) |
|BOOL |[closeResolutionViewAtOnce](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-closeresolutionviewatonce) |
|BOOL |[closeSpeedViewAtOnce](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration-closespeedviewatonce) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerCommonConfiguration-playbuttonnormalimage"></span>
### playButtonNormalImage

```objectivec
@property (nonatomic, strong) UIImage *playButtonNormalImage;
```


The image of the play button.

<span id="BDLPlayerCommonConfiguration-playbuttonselectedimage"></span>
### playButtonSelectedImage

```objectivec
@property (nonatomic, strong) UIImage *playButtonSelectedImage;
```


The image of the selected play button, namely the image of the pause button.

<span id="BDLPlayerCommonConfiguration-centerplaybuttonnormalimage"></span>
### centerPlayButtonNormalImage

```objectivec
@property (nonatomic, strong) UIImage *centerPlayButtonNormalImage;
```


The image of the play button displayed in the center of the player.

<span id="BDLPlayerCommonConfiguration-refreshbuttonnormalimage"></span>
### refreshButtonNormalImage

```objectivec
@property (nonatomic, strong) UIImage *refreshButtonNormalImage;
```


The image of the refresh button.

<span id="BDLPlayerCommonConfiguration-refreshbuttonlocation"></span>
### refreshButtonLocation

```objectivec
@property (nonatomic, assign) BOOL refreshButtonLocation;
```


Whether the refresh button is left\-aligned. Default value: `NO`.


* `YES`: Left\-aligned.

* `NO`: Not left\-aligned.

    &nbsp;


<span id="fullscreenbuttonnormalimage"></span>
### fullScreenButtonNormalImage

```objectivec
@property (nonatomic, strong) UIImage *fullScreenButtonNormalImage;
```


The image of the full\-screen button.

<span id="BDLPlayerCommonConfiguration-fullscreenbuttonselectedimage"></span>
### fullScreenButtonSelectedImage

```objectivec
@property (nonatomic, strong) UIImage *fullScreenButtonSelectedImage;
```


The image of the selected full\-screen button.

<span id="BDLPlayerCommonConfiguration-enterfullscreenenable"></span>
### enterFullScreenEnable

```objectivec
@property (nonatomic, assign) BOOL enterFullScreenEnable;
```


Whether to enable full\-screen mode. Default value: `YES`.


* `YES`: Enable. The full\-screen button is displayed in the player. The full\-screen button appears in:

   * live rooms in landscape mode.

   * live rooms in portrait mode when the width of the source video stream is greater than the height.

* `NO`: Disable. The full\-screen button is not displayed in the player.

    &nbsp;


<span id="exitfullscreenbuttonnormalimage"></span>
### exitFullScreenButtonNormalImage

```objectivec
@property (nonatomic, strong) UIImage *exitFullScreenButtonNormalImage;
```


The image of the exit full\-screen button.

<span id="BDLPlayerCommonConfiguration-themecolor"></span>
### themeColor

```objectivec
@property (nonatomic, strong) UIColor *themeColor;
```


The theme color, which is the background color of the played progress bar.

<span id="BDLPlayerCommonConfiguration-currenttimecolor"></span>
### currentTimeColor

```objectivec
@property (nonatomic, strong) UIColor *currentTimeColor;
```


The color of the current time label.

<span id="BDLPlayerCommonConfiguration-totaltimecolor"></span>
### totalTimeColor

```objectivec
@property (nonatomic, strong) UIColor *totalTimeColor;
```


The color of the total time label.

<span id="BDLPlayerCommonConfiguration-toastfont"></span>
### toastFont

```objectivec
@property (nonatomic, assign) UIFont *toastFont;
```


The font and font size of the toast indicating the preview or live stream has ended.

<span id="BDLPlayerCommonConfiguration-toastcornerradius"></span>
### toastCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat toastCornerRadius;
```


The corner radius of the toast indicating the preview or live stream has ended.

<span id="BDLPlayerCommonConfiguration-toasthorizontaledge"></span>
### toastHorizontalEdge

```objectivec
@property (nonatomic, assign) CGFloat toastHorizontalEdge;
```


The left and right margins for the toast indicating the preview or live stream has ended.

<span id="BDLPlayerCommonConfiguration-toastverticaledge"></span>
### toastVerticalEdge

```objectivec
@property (nonatomic, assign) CGFloat toastVerticalEdge;
```


The top and bottom margins for the toast indicating the preview or live stream has ended.

<span id="BDLPlayerCommonConfiguration-toastcenteryoffset"></span>
### toastCenterYOffset

```objectivec
@property (nonatomic, assign) CGFloat toastCenterYOffset;
```


The position of the toast indicating the preview or live stream has ended.

<span id="BDLPlayerCommonConfiguration-wwanpromptcount"></span>
### wwanPromptCount

```objectivec
@property (nonatomic, assign) NSInteger wwanPromptCount;
```


The prompt frequency.


* `-1`: Always prompt.

* `0`: Never prompt.

* Greater than `0`: Number of prompts. Default value: `1`.

    &nbsp;


<span id="viawwantext"></span>
### viaWWANText

```objectivec
@property (nonatomic, copy) NSString *viaWWANText;
```


The text of the mobile data access prompt.

<span id="BDLPlayerCommonConfiguration-networknotreachabletext"></span>
### networkNotReachableText

```objectivec
@property (nonatomic, copy) NSString *networkNotReachableText;
```


The text of the offline prompt.

<span id="BDLPlayerCommonConfiguration-prompttextcolor"></span>
### promptTextColor

```objectivec
@property (nonatomic, strong) UIColor *promptTextColor;
```


The text color of the prompt.

<span id="BDLPlayerCommonConfiguration-enableaudiopreemption"></span>
### enableAudioPreemption

```objectivec
@property (nonatomic, assign) BOOL enableAudioPreemption;
```


Whether to enable audio preemption management. Default value: `YES`.


* `YES`: After switching to the background, pause the video that has background audio playback and system PiP disabled. When switching back to the foreground, automatically play the video that has autoplay enabled.

* `NO`: If the video is playing and background audio playback is enabled, the audio will continue playing when switching to the background. If the video is paused when switching to the background, it will remain paused. When switching back to the foreground, the playback status will remain consistent with that in the background. If audio is playing in the background, the video will resume playing when switching to the foreground. If the video is paused in the background, it will remain paused when switching to the foreground.

    &nbsp;


<span id="enablebackgroundaudio"></span>
### enableBackgroundAudio

```objectivec
@property (nonatomic, assign) BOOL enableBackgroundAudio;
```


Whether to enable the background audio playback. Default value: `YES`.


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="enablelivepip"></span>
### enableLivePiP

```objectivec
@property (nonatomic, assign) BOOL enableLivePiP API_AVAILABLE(ios(14.0));
```


Whether to enable the system PiP for live videos. Default value: `YES`.


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="enablevodpip"></span>
### enableVodPiP

```objectivec
@property (nonatomic, assign) BOOL enableVodPiP API_AVAILABLE(ios(14.0));
```


Whether to enable the system PiP for Video\-on\-Demand (VOD) videos. Default value: `YES`.


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="floatingcloseimage"></span>
### floatingCloseImage

```objectivec
@property (nonatomic, strong) UIImage *floatingCloseImage;
```


The icon for closing the floating window.

<span id="BDLPlayerCommonConfiguration-floatingcloseimagesize"></span>
### floatingCloseImageSize

```objectivec
@property (nonatomic, assign) CGSize floatingCloseImageSize;
```


The size of the icon for closing the floating window.

<span id="BDLPlayerCommonConfiguration-floatingviewborderwidth"></span>
### floatingViewBorderWidth

```objectivec
@property (nonatomic, assign) CGFloat floatingViewBorderWidth;
```


The border width of the floating window.

<span id="BDLPlayerCommonConfiguration-floatingviewbordercolor"></span>
### floatingViewBorderColor

```objectivec
@property (nonatomic, strong) UIColor *floatingViewBorderColor;
```


The border color of the floating window.

<span id="BDLPlayerCommonConfiguration-floatingviewcornerradius"></span>
### floatingViewCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat floatingViewCornerRadius;
```


The corner radius of the floating window.

<span id="BDLPlayerCommonConfiguration-closeresolutionviewatonce"></span>
### closeResolutionViewAtOnce

```objectivec
@property (nonatomic, assign) BOOL closeResolutionViewAtOnce;
```


Whether to immediately close the resolution selection dialog box after switching the resolution. Default value: `YES`.


* `YES`: Close immediately.

* `NO`: Do not close immediately.

    &nbsp;


<span id="closespeedviewatonce"></span>
### closeSpeedViewAtOnce

```objectivec
@property (nonatomic, assign) BOOL closeSpeedViewAtOnce;
```


Whether to immediately close the playback speed selection dialog box after switching the speed. Default value: `YES`.


* `YES`: Close immediately.

* `NO`: Do not close immediately.

    &nbsp;


<span id="bdlpopuptopshowviewprotocol"></span>
# BDLPopupTopShowViewProtocol

```objectivec
@protocol BDLPopupTopShowViewProtocol <BDLPopupBaseViewProtocol>
```


The protocol for displaying the dialog box on the top.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setVerticalOffset:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopShowViewProtocol-setverticaloffset) |
|void |[topShowInView:completion:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopShowViewProtocol-topshowinview-completion) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupTopShowViewProtocol-setverticaloffset"></span>
### setVerticalOffset:

```objectivec
- (void)setVerticalOffset:(CGFloat)offset;
```


Sets the offset between the content view of the dialog box and the top of the dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|offset |CGFloat |The offset. Unit: points. Default value: `0`. |


<span id="BDLPopupTopShowViewProtocol-topshowinview-completion"></span>
### topShowInView:completion:

```objectivec
- (void)topShowInView:(UIView *)superview completion:(nullable void (^)(BDLPopupBaseView *view))completion;
```


Displays the dialog box on the top.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|superview |UIView\* |The view to display the self instance. |
|completion |nullable void(^)(BDLPopupBaseView\*view) |The callback triggered when the dialog box is displayed. The callback parameter `view` refers to the self instance, which is the instance of [BDLPopupBaseView](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseView) or its subclass. |


<span id="BDLCommentViewConfiguration(Config)"></span>
# BDLCommentViewConfiguration(Config)

```objectivec
@interface BDLCommentViewConfiguration (Config)
```


The configuration of the comment area and top comments.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImage\* |[shoppingCardButtonImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-shoppingcardbuttonimage) |
|UIImage\* |[giftIcon](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-gifticon) |
|UIImage\* |[interactiveButtonImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-interactivebuttonimage) |
|UIImage\* |[imageTextButtonImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-imagetextbuttonimage) |
|UIImage\* |[embeddedUrlButtonImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-embeddedurlbuttonimage) |
|UIImage\* |[moreOptionsButtonImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-moreoptionsbuttonimage) |
|UIImage\* |[shareImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-shareimage) |
|UIColor\* |[welcomeTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-welcometextcolor) |
|UIColor\* |[topCommentTagColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommenttagcolor) |
|BOOL |[topCommentNeedMargin](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentneedmargin) |
|NSUInteger |[rowsOfTopComment](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-rowsoftopcomment) |
|BOOL |[topCommentBackgroundWidthFitContent](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentbackgroundwidthfitcontent) |
|UIColor\* |[topCommentBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentbackgroundcolor) |
|CGFloat |[topCommentViewCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentviewcornerradius) |
|UIFont\* |[topCommentNicknameFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentnicknamefont) |
|UIColor\* |[topCommentNicknameColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentnicknamecolor) |
|CGFloat |[topCommentContentLineSpacingExtra](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentcontentlinespacingextra) |
|UIFont\* |[topCommentFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentfont) |
|UIColor\* |[topCommentFontColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-topcommentfontcolor) |
|BOOL |[isSendCommentEnable](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-issendcommentenable) |
|UIImage\* |[thumbUpButtonImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-thumbupbuttonimage) |
|NSArray<UIImage\*\>\* |[thumbUpImages](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-thumbupimages) |
|BOOL |[showCommentBottomBar](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-showcommentbottombar) |
|UIColor\* |[joinRoomMsgNicknameColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-joinroommsgnicknamecolor) |
|UIColor\* |[joinRoomMsgContentColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-joinroommsgcontentcolor) |
|UIColor\* |[inputBoxBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxbackgroundcolor) |
|CGFloat |[inputBoxCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxcornerradius) |
|CGFloat |[inputBoxBorderWidth](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxborderwidth) |
|UIColor\* |[inputBoxBorderColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxbordercolor) |
|UIColor\* |[inputBoxPromptColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxpromptcolor) |
|UIColor\* |[inputBoxPromptTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxprompttextcolor) |
|UIColor\* |[popupInputBoxPromptTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-popupinputboxprompttextcolor) |
|UIFont\* |[systemTagFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-systemtagfont) |
|UIColor\* |[systemTagColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-systemtagcolor) |
|UIFont\* |[systemCommentFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-systemcommentfont) |
|UIColor\* |[systemCommentColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-systemcommentcolor) |
|CGFloat |[distanceBetweenCell](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-distancebetweencell) |
|CGFloat |[commentCellCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-commentcellcornerradius) |
|CGFloat |[commentListViewBottomMargin](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-commentlistviewbottommargin) |
|UIColor\* |[commentListPullToRefreshColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-commentlistpulltorefreshcolor) |
|CGFloat |[functionEntranceButtonCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-functionentrancebuttoncornerradius) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[textViewShouldBeginEditing](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-textviewshouldbeginediting) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewConfiguration(Config)-shoppingcardbuttonimage"></span>
### shoppingCardButtonImage

```objectivec
@property (nonatomic, strong) UIImage *shoppingCardButtonImage;
```


The image of the shopping cart button.

<span id="BDLCommentViewConfiguration(Config)-gifticon"></span>
### giftIcon

```objectivec
@property (nonatomic, strong) UIImage *giftIcon;
```


The image of the gift button.

<span id="BDLCommentViewConfiguration(Config)-interactivebuttonimage"></span>
### interactiveButtonImage

```objectivec
@property (nonatomic, strong) UIImage *interactiveButtonImage;
```


The image of the interaction tools menu button for the live room in portrait mode.

<span id="BDLCommentViewConfiguration(Config)-imagetextbuttonimage"></span>
### imageTextButtonImage

```objectivec
@property (nonatomic, strong) UIImage *imageTextButtonImage;
```


The image of the graphics menu button for the live room in portrait mode.

<span id="BDLCommentViewConfiguration(Config)-embeddedurlbuttonimage"></span>
### embeddedUrlButtonImage

```objectivec
@property (nonatomic, strong) UIImage *embeddedUrlButtonImage;
```


The image of the embedded link menu button for the live room in portrait mode.

<span id="BDLCommentViewConfiguration(Config)-moreoptionsbuttonimage"></span>
### moreOptionsButtonImage

```objectivec
@property (nonatomic, strong) UIImage *moreOptionsButtonImage;
```


The image of the more options button for the live room in portrait mode.

<span id="BDLCommentViewConfiguration(Config)-shareimage"></span>
### shareImage

```objectivec
@property (nonatomic, strong) UIImage *shareImage;
```


The image of the share button for the live room in portrait mode.

<span id="BDLCommentViewConfiguration(Config)-welcometextcolor"></span>
### welcomeTextColor

```objectivec
@property (nonatomic, strong) UIColor *welcomeTextColor DEPRECATED_MSG_ATTRIBUTE("This property is deprecated since SDK version 1.53.0, use systemCommentColor instead.");
```


The text color of the welcome message.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This property is deprecated since version 1.53.0. Use <a href="https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-systemcommentcolor">systemCommentColor</a> instead.</div>


<span id="BDLCommentViewConfiguration(Config)-topcommenttagcolor"></span>
### topCommentTagColor

```objectivec
@property (nonatomic, strong) UIColor *topCommentTagColor;
```


The color of the vertical line to the left of the nickname in the pinned comment.

<span id="BDLCommentViewConfiguration(Config)-topcommentneedmargin"></span>
### topCommentNeedMargin

```objectivec
@property (nonatomic, assign) BOOL topCommentNeedMargin;
```


Whether a margin is needed on the left side of the pinned comment. Default value: `YES`.


* `YES`: Needed.

* `NO`: Not needed.

    &nbsp;


<span id="rowsoftopcomment"></span>
### rowsOfTopComment

```objectivec
@property (nonatomic, assign) NSUInteger rowsOfTopComment;
```


The number of lines displayed for the pinned comment. If the comment exceeds the configured number of display lines, viewers must tap to view the full content. Default value: `1`. The

value `0` means that the full content of the comment is displayed regardless of the number of lines.

<span id="BDLCommentViewConfiguration(Config)-topcommentbackgroundwidthfitcontent"></span>
### topCommentBackgroundWidthFitContent

```objectivec
@property (nonatomic, assign) BOOL topCommentBackgroundWidthFitContent;
```


Whether the width of the pinned comment background adjusts with the content width. Default value: `NO`.


* `YES`: The width of the pinned comment background adjusts with the content width.

* `NO`: The width of the pinned comment background is fixed.

    &nbsp;


<span id="topcommentbackgroundcolor"></span>
### topCommentBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *topCommentBackgroundColor;
```


The background color of the pinned comment.

<span id="BDLCommentViewConfiguration(Config)-topcommentviewcornerradius"></span>
### topCommentViewCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat topCommentViewCornerRadius;
```


The corner radius of the pinned comment‘s background. Default value: `8`. Unit: point.

<span id="BDLCommentViewConfiguration(Config)-topcommentnicknamefont"></span>
### topCommentNicknameFont

```objectivec
@property (nonatomic, strong) UIFont *topCommentNicknameFont;
```


The font and font size of the pinned comment's nickname. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentViewConfiguration(Config)-topcommentnicknamecolor"></span>
### topCommentNicknameColor

```objectivec
@property (nonatomic, strong) UIColor *topCommentNicknameColor;
```


The color of the pinned comment's nickname.

<span id="BDLCommentViewConfiguration(Config)-topcommentcontentlinespacingextra"></span>
### topCommentContentLineSpacingExtra

```objectivec
@property (nonatomic, assign) CGFloat topCommentContentLineSpacingExtra;
```


Line spacing for the content of the pinned comment. Unit: point.


* If the value is less than or equal to `0`, the default [[NSParagraphStyle defaultParagraphStyle].lineSpacing](https://developer.apple.com/documentation/uikit/nsparagraphstyle/linespacing?language=objc) is used.

* For values greater than `0`, assign it to [[NSParagraphStyle defaultParagraphStyle].lineSpacing](https://developer.apple.com/documentation/uikit/nsparagraphstyle/linespacing?language=objc).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property is valid only when the value of <a href="https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-rowsoftopcomment">rowsOfTopComment</a> is <code>0</code> or greater than<code>1</code>.</div>


<span id="BDLCommentViewConfiguration(Config)-topcommentfont"></span>
### topCommentFont

```objectivec
@property (nonatomic, strong) UIFont *topCommentFont;
```


The font and font size of the pinned comment.

<span id="BDLCommentViewConfiguration(Config)-topcommentfontcolor"></span>
### topCommentFontColor

```objectivec
@property (nonatomic, strong) UIColor *topCommentFontColor;
```


The text color for the content of the pinned comment.

<span id="BDLCommentViewConfiguration(Config)-issendcommentenable"></span>
### isSendCommentEnable

```objectivec
@property (nonatomic, assign) BOOL isSendCommentEnable;
```


Whether to allow viewers to send comments.


* `YES`: Allow.

* `NO`: Do not allow.

    &nbsp;


<span id="thumbupbuttonimage"></span>
### thumbUpButtonImage

```objectivec
@property (nonatomic, strong) UIImage *thumbUpButtonImage;
```


The image of the button for liking the live room.

<span id="BDLCommentViewConfiguration(Config)-thumbupimages"></span>
### thumbUpImages

```objectivec
@property (nonatomic, strong) NSArray<UIImage *> *thumbUpImages;
```


The floating animation images appeared when the button for liking the live room is tapped.

<span id="BDLCommentViewConfiguration(Config)-showcommentbottombar"></span>
### showCommentBottomBar

```objectivec
@property (nonatomic, assign) BOOL showCommentBottomBar;
```


Whether to display the comment text box and the interaction buttons on its right. Default value: `YES`.


* `YES`: Display.

* `NO`: Hide.

    &nbsp;


<span id="joinroommsgnicknamecolor"></span>
### joinRoomMsgNicknameColor

```objectivec
@property (nonatomic, strong) UIColor *joinRoomMsgNicknameColor;
```


The text color of the nickname in the entrance message.

<span id="BDLCommentViewConfiguration(Config)-joinroommsgcontentcolor"></span>
### joinRoomMsgContentColor

```objectivec
@property (nonatomic, strong) UIColor *joinRoomMsgContentColor;
```


The text color of the content in the entrance message.

<span id="BDLCommentViewConfiguration(Config)-inputboxbackgroundcolor"></span>
### inputBoxBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *inputBoxBackgroundColor;
```


The background color of the comment text box in non\-editing status, namely when the keyboard is not popped up. You can modify this property before or after viewers join the live room.

<span id="BDLCommentViewConfiguration(Config)-inputboxcornerradius"></span>
### inputBoxCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat inputBoxCornerRadius;
```


The corner radius of the comment text box in non\-editing status, namely when the keyboard is not popped up. Default value: `18`. Unit: point. You can modify this property before or after viewers join the live room.

<span id="BDLCommentViewConfiguration(Config)-inputboxborderwidth"></span>
### inputBoxBorderWidth

```objectivec
@property (nonatomic, assign) CGFloat inputBoxBorderWidth;
```


The border width of the comment text box in non\-editing status, namely when the keyboard is not popped up. Default value: `0`. Unit: point. You can modify this property before or after viewers join the live room.

<span id="BDLCommentViewConfiguration(Config)-inputboxbordercolor"></span>
### inputBoxBorderColor

```objectivec
@property (nonatomic, strong) UIColor *inputBoxBorderColor;
```


The border color of the comment text box in non\-editing status, namely when the keyboard is not popped up. You can modify this property before or after viewers join the live room.

<span id="BDLCommentViewConfiguration(Config)-inputboxpromptcolor"></span>
### inputBoxPromptColor

```objectivec
@property (nonatomic, strong) UIColor *inputBoxPromptColor DEPRECATED_MSG_ATTRIBUTE("use inputBoxPromptTextColor instead");
```


The placeholder text color of the comment text box in non\-editing status, namely when the keyboard is not popped up. You can modify this property before or after viewers join the live room.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property is deprecated since version 1.61.0. Use <a href="https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-inputboxprompttextcolor">inputBoxPromptTextColor</a> instead.</div>


<span id="BDLCommentViewConfiguration(Config)-inputboxprompttextcolor"></span>
### inputBoxPromptTextColor

```objectivec
@property (nonatomic, strong) UIColor *inputBoxPromptTextColor;
```


The placeholder text color of the comment text box in non\-editing status, namely when the keyboard is not popped up. You can modify this property before or after viewers join the live room.

<span id="BDLCommentViewConfiguration(Config)-popupinputboxprompttextcolor"></span>
### popupInputBoxPromptTextColor

```objectivec
@property (nonatomic, strong) UIColor *popupInputBoxPromptTextColor;
```


The placeholder text color of the comment text box in editing status, namely when the keyboard is popped up. You can modify this property before or after viewers join the live room.

<span id="BDLCommentViewConfiguration(Config)-systemtagfont"></span>
### systemTagFont

```objectivec
@property (nonatomic, strong) UIFont *systemTagFont;
```


The font, font size, and other properties of the tag for the live room description in portrait mode and welcome message. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentViewConfiguration(Config)-systemtagcolor"></span>
### systemTagColor

```objectivec
@property (nonatomic, strong) UIColor *systemTagColor;
```


The tag color for the live room description in portrait mode and welcome message.

<span id="BDLCommentViewConfiguration(Config)-systemcommentfont"></span>
### systemCommentFont

```objectivec
@property (nonatomic, strong) UIFont *systemCommentFont;
```


The font, font size, and other properties of the body for the live room description in portrait mode and welcome message. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentViewConfiguration(Config)-systemcommentcolor"></span>
### systemCommentColor

```objectivec
@property (nonatomic, strong) UIColor *systemCommentColor;
```


The body text color for the live room description in portrait mode and welcome message.

<span id="BDLCommentViewConfiguration(Config)-distancebetweencell"></span>
### distanceBetweenCell

```objectivec
@property (nonatomic, assign) CGFloat distanceBetweenCell;
```


The spacing between adjacent comment cells. Default value: `8`. Unit: points.

<span id="BDLCommentViewConfiguration(Config)-commentcellcornerradius"></span>
### commentCellCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat commentCellCornerRadius;
```


The corner radius of the comment cell. Default value: `12`. Unit: point.

<span id="BDLCommentViewConfiguration(Config)-commentlistviewbottommargin"></span>
### commentListViewBottomMargin

```objectivec
@property (nonatomic, assign) CGFloat commentListViewBottomMargin;
```


The spacing between the bottom of the comment list and the top of the comment text box. Default value: `8`. Unit: points.

<span id="BDLCommentViewConfiguration(Config)-commentlistpulltorefreshcolor"></span>
### commentListPullToRefreshColor

```objectivec
@property (nonatomic, strong) UIColor *commentListPullToRefreshColor;
```


The content color of the pull\-down refresh component, such as `↓ Pull to load more comments`.

<span id="BDLCommentViewConfiguration(Config)-functionentrancebuttoncornerradius"></span>
### functionEntranceButtonCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat functionEntranceButtonCornerRadius;
```


The corner radius of the functional entry buttons located in the lower\-right corner of the live room, such as the shopping cart and interaction tool buttons. Default value: `18`. Unit: point.

<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewConfiguration(Config)-textviewshouldbeginediting"></span>
### textViewShouldBeginEditing

```objectivec
@property (nonatomic, copy, nullable) BOOL (^textViewShouldBeginEditing)(BDLCommentTextViewBeginEditingModel *model);
```


Whether to allow viewers to enter content in the comment text box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|model |BDLCommentTextViewBeginEditingModel\* |Information required to determine whether to allow viewers to enter content in the comment text box. For more information, see [BDLCommentTextViewBeginEditingModel](https://docs.byteplus.com/en/docs/11/17341#BDLCommentTextViewBeginEditingModel). |


**Return Value**


* `YES`: Allow.

* `NO`: Do not allow.

    &nbsp;


<span id="bdltaskawardconfigmodel"></span>
# BDLTaskAwardConfigModel

```objectivec
@interface BDLTaskAwardConfigModel : BDLBaseModel
```


The model of watch time\-based lucky draw configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[taskAwardId](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardid) |
|NSArray<BDLTaskAwardRule\*\>\* |[taskAwardRule](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardrule) |
|NSString\* |[taskAwardIcon](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardicon) |
|NSString\* |[taskAwardInstructions](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardinstructions) |
|NSInteger |[taskAwardStartTime](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardstarttime) |
|NSInteger |[taskAwardEndTime](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardendtime) |
|BDLTaskAwardStatus |[taskAwardStatus](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-taskawardstatus) |
|BOOL |[isInitIcon](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-isiniticon) |
|BDLTaskAwardRule\* |[localCurrentRule](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-localcurrentrule) |
|NSUInteger |[localAvailableRuleCount](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-localavailablerulecount) |
|NSDate\* |[localTaskAwardStartTime](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-localtaskawardstarttime) |
|NSDate\* |[localTaskAwardEndTime](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-localtaskawardendtime) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[isValid](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardConfigModel-isvalid) |


<span id="instructions"></span>
## Instructions

<span id="BDLTaskAwardConfigModel-taskawardid"></span>
### taskAwardId

```objectivec
@property (nonatomic, strong) NSNumber *taskAwardId;
```


The lucky draw ID.

<span id="BDLTaskAwardConfigModel-taskawardrule"></span>
### taskAwardRule

```objectivec
@property (nonatomic, copy) NSArray<BDLTaskAwardRule *> *taskAwardRule;
```


The lucky draw rules. For more information, see [BDLTaskAwardRule](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule).

<span id="BDLTaskAwardConfigModel-taskawardicon"></span>
### taskAwardIcon

```objectivec
@property (nonatomic, copy) NSString *taskAwardIcon;
```


The URL of the custom lucky draw icon.

<span id="BDLTaskAwardConfigModel-taskawardinstructions"></span>
### taskAwardInstructions

```objectivec
@property (nonatomic, copy) NSString *taskAwardInstructions;
```


The event descripion.

<span id="BDLTaskAwardConfigModel-taskawardstarttime"></span>
### taskAwardStartTime

```objectivec
@property (nonatomic, assign) NSInteger taskAwardStartTime;
```


The start time of the lucky draw in Unix timestamp format. Unit: seconds.

<span id="BDLTaskAwardConfigModel-taskawardendtime"></span>
### taskAwardEndTime

```objectivec
@property (nonatomic, assign) NSInteger taskAwardEndTime;
```


The end time of the lucky draw in Unix timestamp format. Unit: seconds.

<span id="BDLTaskAwardConfigModel-taskawardstatus"></span>
### taskAwardStatus

```objectivec
@property (nonatomic, assign) BDLTaskAwardStatus taskAwardStatus;
```


The lucky draw status. For more information, see [BDLTaskAwardStatus](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardStatus).

<span id="BDLTaskAwardConfigModel-isiniticon"></span>
### isInitIcon

```objectivec
@property (nonatomic, assign) BOOL isInitIcon;
```


Whether to use the default lucky draw icon.


* `YES`: Use the default lucky draw icon. The value of `taskAwardIcon` does not take effect.

* `NO`: Use a custom lucky draw icon. The value of `taskAwardIcon` takes effect.

    &nbsp;


<span id="localcurrentrule"></span>
### localCurrentRule

```objectivec
@property (nonatomic, strong, nullable) BDLTaskAwardRule *localCurrentRule;
```


The ongoing rule. Not returned by the BytePlus Live server. For more information, see [BDLTaskAwardRule](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule).

<span id="BDLTaskAwardConfigModel-localavailablerulecount"></span>
### localAvailableRuleCount

```objectivec
@property (nonatomic, assign) NSUInteger localAvailableRuleCount;
```


The number of available rules.

<span id="BDLTaskAwardConfigModel-localtaskawardstarttime"></span>
### localTaskAwardStartTime

```objectivec
@property (nonatomic, strong) NSDate *localTaskAwardStartTime;
```


The start time of the lucky draw. Not returned by the BytePlus Live server.

<span id="BDLTaskAwardConfigModel-localtaskawardendtime"></span>
### localTaskAwardEndTime

```objectivec
@property (nonatomic, strong) NSDate *localTaskAwardEndTime;
```


The end time of the lucky draw. Not returned by the BytePlus Live server.

<span id="instructions"></span>
## Instructions

<span id="BDLTaskAwardConfigModel-isvalid"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


Whether valid.

**Return Value**


* `YES`: Valid.

* `NO`: Invalid.

    &nbsp;


<span id="bdlbusinessaccountconfiguration"></span>
# BDLBusinessAccountConfiguration

```objectivec
@interface BDLBusinessAccountConfiguration : BDLRTBaseConfiguration
```


The host account configuration.

<span id="BDLRichTextWebView"></span>
# BDLRichTextWebView

```objectivec
@interface BDLRichTextWebView : WKWebView
```


The WebView to display the rich text.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[finishedNavigation](https://docs.byteplus.com/en/docs/11/17341#BDLRichTextWebView-finishednavigation) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateWithRichText:color:](https://docs.byteplus.com/en/docs/11/17341#BDLRichTextWebView-updatewithrichtext-color) |
|void |[updateWithRichText:colorStr:](https://docs.byteplus.com/en/docs/11/17341#BDLRichTextWebView-updatewithrichtext-colorstr) |
|void |[updateWithTitle:richText:colorStr:](https://docs.byteplus.com/en/docs/11/17341#BDLRichTextWebView-updatewithtitle-richtext-colorstr) |


<span id="instructions"></span>
## Instructions

<span id="BDLRichTextWebView-finishednavigation"></span>
### finishedNavigation

```objectivec
@property (nonatomic, assign) BOOL finishedNavigation;
```


Whether [webView:didFinishNavigation:](https://developer.apple.com/documentation/webkit/wknavigationdelegate/1455629-webview?language=objc) is called.


* `YES`: Called.

* `NO`: Not called.


<span id="instructions"></span>
## Instructions

<span id="BDLRichTextWebView-updatewithrichtext-color"></span>
### updateWithRichText:color:

```objectivec
- (void)updateWithRichText:(NSString *)richText color:(nullable UIColor *)color;
```


Updates the content.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|richText |NSString\* |The rich text that needs to be displayed. |
|color |nullable UIColor\* |The content color.<br><br>&nbsp;<br><br>If `nil`, the color of `richText` is used. |


<span id="BDLRichTextWebView-updatewithrichtext-colorstr"></span>
### updateWithRichText:colorStr:

```objectivec
- (void)updateWithRichText:(NSString *)richText colorStr:(nullable NSString *)colorStr;
```


Updates the content.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|richText |NSString\* |The rich text that needs to be displayed. |
|colorStr |nullable NSString\* |The RGB value of the content color.<br><br>&nbsp;<br><br>If `nil`, the color of `richText` is used. |


<span id="BDLRichTextWebView-updatewithtitle-richtext-colorstr"></span>
### updateWithTitle:richText:colorStr:

```objectivec
- (void)updateWithTitle:(NSString *)title richText:(NSString *)content colorStr:(nullable NSString *)colorStr;
```


Updates the content.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|title |NSString\* |The title, which is concatenated with `content` and displayed within the SDK. |
|content |NSString\* |The content that needs to be displayed. |
|colorStr |nullable NSString\* |The RGB value of the content color.<br><br>&nbsp;<br><br>If `nil`, the color of `content` is used. |


<span id="BDLQuestionnaireQuestionModel"></span>
# BDLQuestionnaireQuestionModel

```objectivec
@interface BDLQuestionnaireQuestionModel : BDLBaseModel
```


The model of questionnaire questions.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[questionId](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-questionid) |
|NSString\* |[question](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-question) |
|BOOL |[isRequire](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-isrequire) |
|NSString\* |[questionTag](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-questiontag) |
|NSString\* |[questionSubTag](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-questionsubtag) |
|BDLQuestionnaireQuestionType |[questionType](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-questiontype) |
|NSArray<BDLQuestionOptionModel\*\>\* |[options](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-options) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[isValid](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionModel-isvalid) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireQuestionModel-questionid"></span>
### questionId

```objectivec
@property (nonatomic, strong) NSNumber *questionId;
```


The question ID.

<span id="BDLQuestionnaireQuestionModel-question"></span>
### question

```objectivec
@property (nonatomic, copy) NSString *question;
```


The question content.

<span id="BDLQuestionnaireQuestionModel-isrequire"></span>
### isRequire

```objectivec
@property (nonatomic, assign) BOOL isRequire;
```


Whether the question is required.


* `YES`: Required.

* `NO`: Not required.

    &nbsp;


<span id="questiontag"></span>
### questionTag

```objectivec
@property (nonatomic, copy) NSString *questionTag;
```


The question type.

<span id="BDLQuestionnaireQuestionModel-questionsubtag"></span>
### questionSubTag

```objectivec
@property (nonatomic, copy) NSString *questionSubTag;
```


The question subtype.

<span id="BDLQuestionnaireQuestionModel-questiontype"></span>
### questionType

```objectivec
@property (nonatomic, assign) BDLQuestionnaireQuestionType questionType;
```


The `questionType` enum, which is converted from the values of `questionTag` and `questionSubTag`. Not returned by the BytePlus Live server. For more information, see [BDLQuestionnaireQuestionType](https://docs.byteplus.com/en/docs/11/17341#BDLQuestionnaireQuestionType).

<span id="BDLQuestionnaireQuestionModel-options"></span>
### options

```objectivec
@property (nonatomic, copy, nullable) NSArray<BDLQuestionOptionModel *> *options;
```


The option content. For more information, see [BDLQuestionOptionModel](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLQuestionOptionModel).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property has a value only when the question type is multiple choice.</div>


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireQuestionModel-isvalid"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


Whether valid.

**Return Value**


* `YES`: Valid.

* `NO`: Invalid.

    &nbsp;


<span id="bdlnetworkstatus"></span>
# BDLNetworkStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLNetworkStatus
)
```


The network status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLNetworkStatusUnknown |0 |Unknown. |
|BDLNetworkStatusNotReachable |1 |Network unreachable, namely no network. |
|BDLNetworkStatusReachableViaWWAN |2 |Wireless Wide Area Network (WWAN). |
|BDLNetworkStatusReachableViaWiFi |3 |WiFi. |


<span id="BDLInteractiveAwardStatus"></span>
# BDLInteractiveAwardStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveAwardStatus
)
```


The lucky draw status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveAwardStatusIng |2 |Pending draw. |
|BDLInteractiveAwardStatusOpened |4 |Prize drawn. |
|BDLInteractiveAwardStatusWithdraw |7 |Withdrawn. |
|BDLInteractiveAwardStatusLottery |8 |Drawing in progress. |
|BDLInteractiveAwardStatusWaitingOpen |NSIntegerMax |Waiting for the prize to be drawn, for local delayed drawing. The BytePlus Live server has already drawn the prize. |


<span id="BDLPopupCenterShowViewProtocol"></span>
# BDLPopupCenterShowViewProtocol

```objectivec
@protocol BDLPopupCenterShowViewProtocol <BDLPopupBaseViewProtocol>
```


The protocol for displaying the dialog box in the middle.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setVerticalOffset:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupCenterShowViewProtocol-setverticaloffset) |
|void |[centerShowInView:completion:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupCenterShowViewProtocol-centershowinview-completion) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupCenterShowViewProtocol-setverticaloffset"></span>
### setVerticalOffset:

```objectivec
- (void)setVerticalOffset:(CGFloat)offset;
```


Sets the offset between the content view of the dialog box and `self.center.y`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|offset |CGFloat |The offset. Unit: points. Default value: `0`. |


<span id="BDLPopupCenterShowViewProtocol-centershowinview-completion"></span>
### centerShowInView:completion:

```objectivec
- (void)centerShowInView:(UIView *)superview completion:(nullable void (^)(BDLPopupBaseView *view))completion;
```


Displays the dialog box in the middle.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|superview |UIView\* |The dialog box will be displayed as a subview of the superview. |
|completion |nullable void(^)(BDLPopupBaseView\*view) |The callback triggered after the dialog box is displayed. |


<span id="BDLFloatingControllerConfiguration"></span>
# BDLFloatingControllerConfiguration

```objectivec
@interface BDLFloatingControllerConfiguration : BDLRTBaseConfiguration
```


The configuration of the floating window controller.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[hideFloatingViewsWhenKeyboardShow](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingControllerConfiguration-hidefloatingviewswhenkeyboardshow) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingControllerConfiguration-hidefloatingviewswhenkeyboardshow"></span>
### hideFloatingViewsWhenKeyboardShow

```objectivec
@property (nonatomic, assign) BOOL hideFloatingViewsWhenKeyboardShow;
```


Whether to automatically hide all the floating window controls, such as the floating product card, the floating ad, and interaction tool floating windows, when the keyboard pops up. Default value: `NO`. Valid values:


* `YES`: Automatically hide.

* `NO`: Do not automatically hide.

    &nbsp;


<span id="bdlpageadviewconfiguration-config"></span>
# BDLPageAdViewConfiguration(Config)

```objectivec
@interface BDLPageAdViewConfiguration (Config)
```


The in\-page ad configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSTimeInterval |[scrollTimeInterval](https://docs.byteplus.com/en/docs/11/17341#BDLPageAdViewConfiguration(Config)-scrolltimeinterval) |
|CGFloat |[cornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLPageAdViewConfiguration(Config)-cornerradius) |


<span id="instructions"></span>
## Instructions

<span id="BDLPageAdViewConfiguration(Config)-scrolltimeinterval"></span>
### scrollTimeInterval

```objectivec
@property (nonatomic, assign) NSTimeInterval scrollTimeInterval;
```


The carousel interval for in\-page ads, namely how frequently the ad scrolls to the right. Unit: seconds. Default value: 3. The value must be greater than 0.

<span id="BDLPageAdViewConfiguration(Config)-cornerradius"></span>
### cornerRadius

```objectivec
@property (nonatomic, assign) CGFloat cornerRadius;
```


The corner radius. Default value: 4.0.

<span id="BDLGetShareInfoResult"></span>
# BDLGetShareInfoResult

```objectivec
@interface BDLGetShareInfoResult : BDLBaseModel
```


The result after getting the sharing information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[canShare](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-canshare) |
|NSInteger |[canInvite](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-caninvite) |
|NSString\* |[coverImage](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-coverimage) |
|NSString\* |[title](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-title) |
|NSString\* |[sponsor](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-sponsor) |
|longlong |[liveStartTime](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-livestarttime) |
|NSString\* |[activityAddress](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-activityaddress) |
|NSString\* |[activityDesc](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-activitydesc) |
|NSInteger |[liveType](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-livetype) |
|NSString\* |[customAddress](https://docs.byteplus.com/en/docs/11/17341#BDLGetShareInfoResult-customaddress) |


<span id="instructions"></span>
## Instructions

<span id="BDLGetShareInfoResult-canshare"></span>
### canShare

```objectivec
@property (nonatomic, assign) NSInteger canShare;
```


Whether to enable sharing.


* `2`: Enable.

* Other values: Disable.

    &nbsp;


<span id="caninvite"></span>
### canInvite

```objectivec
@property (nonatomic, assign) NSInteger canInvite;
```


Whether to enable the invitation poster.


* `2`: Enable.

* Other values: Disable.

    &nbsp;


<span id="coverimage"></span>
### coverImage

```objectivec
@property (nonatomic, copy) NSString *coverImage;
```


The URL of the browser icon.

<span id="BDLGetShareInfoResult-title"></span>
### title

```objectivec
@property (nonatomic, copy) NSString *title;
```


The poster title.

<span id="BDLGetShareInfoResult-sponsor"></span>
### sponsor

```objectivec
@property (nonatomic, copy) NSString *sponsor;
```


The organizer.

<span id="BDLGetShareInfoResult-livestarttime"></span>
### liveStartTime

```objectivec
@property (nonatomic, assign) long long liveStartTime;
```


The start time of the live stream in Unix timestamp format. Unit: seconds.

<span id="BDLGetShareInfoResult-activityaddress"></span>
### activityAddress

```objectivec
@property (nonatomic, copy) NSString *activityAddress;
```


The event location.

<span id="BDLGetShareInfoResult-activitydesc"></span>
### activityDesc

```objectivec
@property (nonatomic, copy) NSString *activityDesc;
```


The event introduction.

<span id="BDLGetShareInfoResult-livetype"></span>
### liveType

```objectivec
@property (nonatomic, assign) NSInteger liveType;
```


The live mode.


* `1`: Portrait mode.

* `2`: Landscape mode.

    &nbsp;


<span id="customaddress"></span>
### customAddress

```objectivec
@property (nonatomic, copy) NSString *customAddress;
```


The shared address.

<span id="BDLPopupBottomShowViewProtocol"></span>
# BDLPopupBottomShowViewProtocol

```objectivec
@protocol BDLPopupBottomShowViewProtocol <BDLPopupBaseViewProtocol>
```


The protocol for displaying the dialog box at the bottom.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setVerticalOffset:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBottomShowViewProtocol-setverticaloffset) |
|void |[bottomShowInView:completion:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBottomShowViewProtocol-bottomshowinview-completion) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupBottomShowViewProtocol-setverticaloffset"></span>
### setVerticalOffset:

```objectivec
- (void)setVerticalOffset:(CGFloat)offset;
```


Sets the offset between the content view of the dialog box and the bottom of the dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|offset |CGFloat |The offset. Unit: points. Default value: `0`. |


<span id="BDLPopupBottomShowViewProtocol-bottomshowinview-completion"></span>
### bottomShowInView:completion:

```objectivec
- (void)bottomShowInView:(UIView *)superview completion:(nullable void (^)(BDLPopupBaseView *view))completion;
```


Displays the dialog box at the bottom.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|superview |UIView\* |The dialog box will be displayed as a subview of the superview. |
|completion |nullable void(^)(BDLPopupBaseView\*view) |The callback triggered after the dialog box is displayed. |


<span id="BDLPlayerCompactControlView"></span>
# BDLPlayerCompactControlView

```objectivec
@interface BDLPlayerCompactControlView : BDLPlayerControlView <BDLBasicService, BDLLanguageService>
```


A compact version of the player control view.

<span id="BDLFloatingControllerInsertPosition"></span>
# BDLFloatingControllerInsertPosition

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLFloatingControllerInsertPosition
)
```


The position to insert the custom floating view into the live room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLFloatingControllerInsertPositionNone |0 |Do not participate in rearranging the display order of the view. The display position is determined by the view's configuration. |
|BDLFloatingControllerInsertPositionLeftTop |1 |Displayed in the upper\-left corner of the live room, in conjunction with the interaction tool floating window in portrait mode. The display order of the views is rearranged based on their `view.tag` values. The smaller the `tag` value, the higher the display position.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the live room in portrait mode, the content displayed in the upper\-right corner (custom floating view, in\-page ads, and header ad) aligns in height at the top with the content displayed in the upper\-left corner (custom floating view and interaction tool floating window).</div><br> |
|BDLFloatingControllerInsertPositionRightBottom |2 |Displayed in the lower\-right corner of the live room, in conjunction with the interaction tool floating window in landscape mode, floating product cards, and floating ads. The display order of the views is rearranged based on their `view.tag` values. The smaller the `tag` value, the higher the display position. |
|BDLFloatingControllerInsertPositionRightTop |3 |Displayed in the upper\-right corner of the live room, in conjunction with the in\-page ads and header ad in portrait mode. The display order of the views is rearranged based on their `view.tag` values. The smaller the `tag` value, the higher the display position.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the live room in portrait mode, the content displayed in the upper\-right corner (custom floating view, in\-page ads, and header ad) aligns in height at the top with the content displayed in the upper\-left corner (custom floating view and interaction tool floating window).</div><br> |


<span id="BDLTaskAwardRule"></span>
# BDLTaskAwardRule

```objectivec
@interface BDLTaskAwardRule : BDLBaseModel
```


The model of watch time\-based lucky draw rules.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[taskAwardItemId](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-taskawarditemid) |
|NSInteger |[watchTime](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-watchtime) |
|NSUInteger |[awardParticipantLimit](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-awardparticipantlimit) |
|NSString\* |[awardItemName](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-awarditemname) |
|NSString\* |[awardItemIcon](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-awarditemicon) |
|NSString\* |[awardItemType](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-awarditemtype) |
|NSUInteger |[awardCount](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-awardcount) |
|NSString\* |[awardLotteryTicketAddress](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-awardlotteryticketaddress) |
|BDLTaskAwardRuleState |[localState](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-localstate) |
|NSInteger |[localEachPrizeWatchTime](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-localeachprizewatchtime) |
|BDLAwardContactOptions |[localContactOptions](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-localcontactoptions) |
|BDLTaskAwardRuleItemType |[localAwardItemType](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-localawarditemtype) |
|NSUInteger |[localCountdown](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRule-localcountdown) |


<span id="instructions"></span>
## Instructions

<span id="BDLTaskAwardRule-taskawarditemid"></span>
### taskAwardItemId

```objectivec
@property (nonatomic, strong) NSNumber *taskAwardItemId;
```


The lucky draw rule ID.

<span id="BDLTaskAwardRule-watchtime"></span>
### watchTime

```objectivec
@property (nonatomic, assign) NSInteger watchTime;
```


The total watch time. Unit: minutes.

<span id="BDLTaskAwardRule-awardparticipantlimit"></span>
### awardParticipantLimit

```objectivec
@property (nonatomic, assign) NSUInteger awardParticipantLimit;
```


The maximum number of participants.

<span id="BDLTaskAwardRule-awarditemname"></span>
### awardItemName

```objectivec
@property (nonatomic, copy) NSString *awardItemName;
```


The prize name.

<span id="BDLTaskAwardRule-awarditemicon"></span>
### awardItemIcon

```objectivec
@property (nonatomic, copy) NSString *awardItemIcon;
```


The URL of the prize image.

<span id="BDLTaskAwardRule-awarditemtype"></span>
### awardItemType

```objectivec
@property (nonatomic, copy) NSString *awardItemType;
```


The prize type.

<span id="BDLTaskAwardRule-awardcount"></span>
### awardCount

```objectivec
@property (nonatomic, assign) NSUInteger awardCount;
```


The number of prizes.

<span id="BDLTaskAwardRule-awardlotteryticketaddress"></span>
### awardLotteryTicketAddress

```objectivec
@property (nonatomic, copy) NSString *awardLotteryTicketAddress;
```


The claim link for voucher prizes.

<span id="BDLTaskAwardRule-localstate"></span>
### localState

```objectivec
@property (nonatomic, assign) BDLTaskAwardRuleState localState;
```


The lucky draw status. Not returned by the BytePlus Live server. For more information, see [BDLTaskAwardRuleState](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRuleState).

<span id="BDLTaskAwardRule-localeachprizewatchtime"></span>
### localEachPrizeWatchTime

```objectivec
@property (nonatomic, assign) NSInteger localEachPrizeWatchTime;
```


The time to unlock the treasure box. Unit: seconds. Not returned by the BytePlus Live server.

<span id="BDLTaskAwardRule-localcontactoptions"></span>
### localContactOptions

```objectivec
@property (nonatomic, assign) BDLAwardContactOptions localContactOptions;
```


The contact information of winners. Not returned by the BytePlus Live server. For more information, see [BDLAwardContactOptions](https://docs.byteplus.com/en/docs/11/17341#BDLAwardContactOptions).

<span id="BDLTaskAwardRule-localawarditemtype"></span>
### localAwardItemType

```objectivec
@property (nonatomic, assign) BDLTaskAwardRuleItemType localAwardItemType;
```


The prize type. Not returned by the BytePlus Live server. For more information, see [BDLTaskAwardRuleItemType](https://docs.byteplus.com/en/docs/11/17341#BDLTaskAwardRuleItemType).

<span id="BDLTaskAwardRule-localcountdown"></span>
### localCountdown

```objectivec
@property (nonatomic, assign) NSUInteger localCountdown;
```


The current countdown time. Unit: seconds. Not returned by the BytePlus Live server.

<span id="BDLTaskAwardRuleState"></span>
# BDLTaskAwardRuleState

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLTaskAwardRuleState
)
```


The status of watch time\-based lucky draws.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLTaskAwardRuleStateLock |0 |Locked. |
|BDLTaskAwardRuleStateIng |1 |In progress. |
|BDLTaskAwardRuleStateCanOpen |2 |Ready to draw the prize. |
|BDLTaskAwardRuleStateWin |3 |The current viewer has won the prize. |
|BDLTaskAwardRuleStateLost |4 |The current viewer does not win the prize. |


<span id="BDLImageTextViewConfiguration"></span>
# BDLImageTextViewConfiguration

```objectivec
@interface BDLImageTextViewConfiguration : BDLRTBaseConfiguration
```


The configuration of the menu for graphics.

<span id="BDLInteractiveToolModel"></span>
# BDLInteractiveToolModel

```objectivec
@interface BDLInteractiveToolModel : BDLBaseModel
```


The model of interaction tools.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[interactiveToolId](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-interactivetoolid) |
|NSDate\* |[createTime](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-createtime) |
|BOOL |[isDeleted](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-isdeleted) |
|NSArray<BDLInteractiveContextModel\*\>\* |[context](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-context) |
|CGFloat |[textHeight](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-textheight) |
|CGFloat |[imageHeight](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-imageheight) |
|CGFloat |[totalHeight](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-totalheight) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[contextContain:](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-contextcontain) |
|BDLInteractiveContextModel |[contextWithType:](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-contextwithtype) |
|BDLInteractiveContextModel |[getImageContext](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-getimagecontext) |
|void |[keepSupportedContexts:](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-keepsupportedcontexts) |
|BOOL |[isValid](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolModel-isvalid) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolModel-interactivetoolid"></span>
### interactiveToolId

```objectivec
@property (nonatomic, strong) NSNumber *interactiveToolId;
```


The interaction tool ID.

<span id="BDLInteractiveToolModel-createtime"></span>
### createTime

```objectivec
@property (nonatomic, strong) NSDate *createTime;
```


The creation time.

<span id="BDLInteractiveToolModel-isdeleted"></span>
### isDeleted

```objectivec
@property (nonatomic, assign) BOOL isDeleted;
```


Whether deleted.


* `YES`: Deleted.

* `NO`: Not deleted.

    &nbsp;


<span id="context"></span>
### context

```objectivec
@property (nonatomic, strong) NSArray<BDLInteractiveContextModel *> *context;
```


The content of interaction tools. For more information, see [BDLInteractiveContextModel](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLInteractiveContextModel).

<span id="BDLInteractiveToolModel-textheight"></span>
### textHeight

```objectivec
@property (nonatomic, assign) CGFloat textHeight;
```


The height of the text content. Unit: points.

<span id="BDLInteractiveToolModel-imageheight"></span>
### imageHeight

```objectivec
@property (nonatomic, assign) CGFloat imageHeight;
```


The height of the image content. Unit: points.

<span id="BDLInteractiveToolModel-totalheight"></span>
### totalHeight

```objectivec
@property (nonatomic, assign) CGFloat totalHeight;
```


The total height. Unit: points.

<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolModel-contextcontain"></span>
### contextContain:

```objectivec
- (BOOL)contextContain:(BDLInteractiveContextType)type;
```


Whether to contain the content of specific interaction tool type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |BDLInteractiveContextType |The interaction tool type. For more information, see [BDLInteractiveContextType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveContextType). |


**Return Value**


* `YES`: Contain.

* `NO`: Do not contain.

    &nbsp;


<span id="contextwithtype"></span>
### contextWithType:

```objectivec
- (BDLInteractiveContextModel *)contextWithType:(BDLInteractiveContextType)type;
```


Gets the corresponding content based on the interaction tool type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |BDLInteractiveContextType |The interaction tool type. For more information, see [BDLInteractiveContextType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveContextType). |


**Return Value**

The content of interaction tools. For more information, see [BDLInteractiveContextModel](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLInteractiveContextModel).

<span id="BDLInteractiveToolModel-getimagecontext"></span>
### getImageContext

```objectivec
- (NSArray<BDLInteractiveContextModel *> *)getImageContext;
```


Gets the image content.

**Return Value**

The content of interaction tools. For more information, see [BDLInteractiveContextModel](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLInteractiveContextModel).

<span id="BDLInteractiveToolModel-keepsupportedcontexts"></span>
### keepSupportedContexts:

```objectivec
- (void)keepSupportedContexts:(NSArray<NSNumber *> *)supportedContextTypes;
```


Only keeps the content of supported interaction tool types.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|supportedContextTypes |NSArray<NSNumber\*\>\* |The array of interaction tool types that need to be kept. For more information, see [BDLInteractiveContextType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveContextType). |


<span id="BDLInteractiveToolModel-isvalid"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


Whether the interaction tool is valid.

**Return Value**


* `YES`: Valid.

* `NO`: Invalid.

    &nbsp;


<span id="bdlinteractiveawardmodel"></span>
# BDLInteractiveAwardModel

```objectivec
@interface BDLInteractiveAwardModel : BDLInteractiveCountdownBaseModel
```


The model of real\-time lucky draws.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[name](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-name) |
|BDLInteractiveAwardType |[awardType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awardtype) |
|NSString\* |[barragePwd](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-barragepwd) |
|NSNumber\* |[awardId](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awardid) |
|NSInteger |[totalCount](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-totalcount) |
|BDLInteractiveAwardStatus |[status](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-status) |
|BOOL |[showPeopleNumber](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-showpeoplenumber) |
|NSInteger |[awardNum](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awardnum) |
|BDLAwardContactOptions |[contactOptions](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-contactoptions) |
|NSString\* |[awardIcon](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awardicon) |
|BDLInteractiveAwardItemType |[awardItemType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awarditemtype) |
|BDLAwardCondition\* |[awardCondition](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awardcondition) |
|BOOL |[isHideAwardNum](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-ishideawardnum) |
|NSArray<BDLAwardItemConfig\*\>\* |[awardItemConfigs](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awarditemconfigs) |
|NSString\* |[awardLotteryTicketAddr](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-awardlotteryticketaddr) |
|BOOL |[participated](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-participated) |
|NSInteger |[deadlineSecond](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardModel-deadlinesecond) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveAwardModel-name"></span>
### name

```objectivec
@property (nonatomic, copy) NSString *name;
```


The prize name.

<span id="BDLInteractiveAwardModel-awardtype"></span>
### awardType

```objectivec
@property (nonatomic, assign) BDLInteractiveAwardType awardType;
```


The draw method. For more information, see [BDLInteractiveAwardType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardType).

<span id="BDLInteractiveAwardModel-barragepwd"></span>
### barragePwd

```objectivec
@property (nonatomic, copy) NSString *barragePwd;
```


The bullet comment, which is automatically sent by viewers when they participate in some lucky draws.

<span id="BDLInteractiveAwardModel-awardid"></span>
### awardId

```objectivec
@property (nonatomic, strong) NSNumber *awardId;
```


The lucky draw ID.

<span id="BDLInteractiveAwardModel-totalcount"></span>
### totalCount

```objectivec
@property (nonatomic, assign) NSInteger totalCount;
```


The number of participants.

<span id="BDLInteractiveAwardModel-status"></span>
### status

```objectivec
@property (nonatomic, assign) BDLInteractiveAwardStatus status;
```


The lucky draw status. For more information, see [BDLInteractiveAwardStatus](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAwardStatus).

<span id="BDLInteractiveAwardModel-showpeoplenumber"></span>
### showPeopleNumber

```objectivec
@property (nonatomic, assign) BOOL showPeopleNumber;
```


Whether to display the number of participants.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="awardnum"></span>
### awardNum

```objectivec
@property (nonatomic, assign) NSInteger awardNum;
```


The number of prizes.

<span id="BDLInteractiveAwardModel-contactoptions"></span>
### contactOptions

```objectivec
@property (nonatomic, assign) BDLAwardContactOptions contactOptions;
```


The type of information that winners must enter. For more information, see [BDLAwardContactOptions](https://docs.byteplus.com/en/docs/11/17341#BDLAwardContactOptions).

<span id="BDLInteractiveAwardModel-awardicon"></span>
### awardIcon

```objectivec
@property (nonatomic, copy) NSString *awardIcon;
```


The lucky draw icon.

<span id="BDLInteractiveAwardModel-awarditemtype"></span>
### awardItemType

```objectivec
@property (nonatomic, assign) BDLInteractiveAwardItemType awardItemType;
```


The prize type. For more information, see [BDLInteractiveAwardItemType](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLInteractiveAwardItemType).

<span id="BDLInteractiveAwardModel-awardcondition"></span>
### awardCondition

```objectivec
@property (nonatomic, strong) BDLAwardCondition *awardCondition;
```


The conditions for participating in the lucyky draw. For more information, see [BDLAwardCondition](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLAwardCondition).

<span id="BDLInteractiveAwardModel-ishideawardnum"></span>
### isHideAwardNum

```objectivec
@property (nonatomic, assign) BOOL isHideAwardNum;
```


Whether to hide the number of each prize.


* `YES`: Hide.

* `NO`: Do not hide.

    &nbsp;


<span id="awarditemconfigs"></span>
### awardItemConfigs

```objectivec
@property (nonatomic, strong) NSArray<BDLAwardItemConfig *> *awardItemConfigs;
```


The lucky draw configuration. For more information, see [BDLAwardItemConfig](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLAwardItemConfig).

<span id="BDLInteractiveAwardModel-awardlotteryticketaddr"></span>
### awardLotteryTicketAddr

```objectivec
@property (nonatomic, strong) NSString *awardLotteryTicketAddr;
```


The claim link for voucher prizes.

<span id="BDLInteractiveAwardModel-participated"></span>
### participated

```objectivec
@property (nonatomic, assign) BOOL participated;
```


Whether the viewer participated in the lucky draw.


* `YES`: Participated.

* `NO`: Not participated.

    &nbsp;


<span id="deadlinesecond"></span>
### deadlineSecond

```objectivec
@property (nonatomic, assign) NSInteger deadlineSecond;
```


The countdown time of the lucky draw. Unit: seconds.

<span id="BDLCommentSendState"></span>
# BDLCommentSendState

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLCommentSendState
)
```


The sending status of comments.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLCommentSendStateDefault |0 |The default value, considered as data returned by the BytePlus Live server. No need to display loading or failure icon. |
|BDLCommentSendStateIng |1 |The comment is being sent, with loading displayed. |
|BDLCommentSendStateSuccess |2 |The comment is sent successfully, without the need to display loading. |
|BDLCommentSendStateFail |3 |Failed to send the comment, with the failure icon displayed. |


<span id="BDLScrollDirection"></span>
# BDLScrollDirection

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLScrollDirection
)
```


The scrolling direction.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLScrollDirectionRight |0 |To the right. |
|BDLScrollDirectionLeft |1 |To the left. |


<span id="BDLPageAdViewProtocol"></span>
# BDLPageAdViewProtocol

```objectivec
@protocol BDLPageAdViewProtocol
```


The protocol for in\-page ads, which must be followed by views returned by custom in\-page ads, such as [BDLPageAdView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPageAdView).

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setShowOrHideBlock:](https://docs.byteplus.com/en/docs/11/17341#BDLPageAdViewProtocol-setshoworhideblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLPageAdViewProtocol-setshoworhideblock"></span>
### setShowOrHideBlock:

```objectivec
- (void)setShowOrHideBlock:(void (^)(UIView *view))block;
```


For the custom in\-page ad view, this method needs to be implemented. Additionally, the block needs to be called when hiding the in\-page ad.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|block |void(^)(UIView\*view) |The block that needs to be called when hiding the in\-page ad. |


<span id="BDLNoticeModel"></span>
# BDLNoticeModel

```objectivec
@interface BDLNoticeModel : BDLBaseModel
```


The notification model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[msg](https://docs.byteplus.com/en/docs/11/17341#BDLNoticeModel-msg) |
|NSDate\* |[sendTime](https://docs.byteplus.com/en/docs/11/17341#BDLNoticeModel-sendtime) |
|BDLNoticeType |[type](https://docs.byteplus.com/en/docs/11/17341#BDLNoticeModel-type) |


<span id="instructions"></span>
## Instructions

<span id="BDLNoticeModel-msg"></span>
### msg

```objectivec
@property (nonatomic, copy) NSString *msg;
```


The notification content.

<span id="BDLNoticeModel-sendtime"></span>
### sendTime

```objectivec
@property (nonatomic, strong) NSDate *sendTime;
```


The send time.

<span id="BDLNoticeModel-type"></span>
### type

```objectivec
@property (nonatomic, assign) BDLNoticeType type;
```


The notification type. For more information, see [BDLNoticeType](https://docs.byteplus.com/en/docs/11/17341#BDLNoticeType).

<span id="BDLPlayerConfiguration"></span>
# BDLPlayerConfiguration

```objectivec
@interface BDLPlayerConfiguration : NSObject
```


The player configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLPlayerCommonConfiguration\* |[common](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerConfiguration-common) |
|BDLBasePlayerConfiguration\* |[basePlayerConfig](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerConfiguration-baseplayerconfig) |
|BDLPlayerPortraitConfiguration\* |[portrait](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerConfiguration-portrait) |
|BDLPlayerLandscapeConfiguration\* |[landscape](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerConfiguration-landscape) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerConfiguration-common"></span>
### common

```objectivec
@property (nonatomic, strong) BDLPlayerCommonConfiguration *common;
```


The common configuration of the player. For more information, see [BDLPlayerCommonConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerCommonConfiguration).

<span id="BDLPlayerConfiguration-baseplayerconfig"></span>
### basePlayerConfig

```objectivec
@property (nonatomic, strong) BDLBasePlayerConfiguration *basePlayerConfig;
```


The configuration of the custom player. For more information, see [BDLBasePlayerConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration).

<span id="BDLPlayerConfiguration-portrait"></span>
### portrait

```objectivec
@property (nonatomic, strong) BDLPlayerPortraitConfiguration *portrait;
```


The configuration of the player in portrait mode. For more information, see [BDLPlayerPortraitConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerPortraitConfiguration).

<span id="BDLPlayerConfiguration-landscape"></span>
### landscape

```objectivec
@property (nonatomic, strong) BDLPlayerLandscapeConfiguration *landscape;
```


The configuration of the player in landscape mode. For more information, see [BDLPlayerLandscapeConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerLandscapeConfiguration).

<span id="BDLQuestionnairePublishStatus"></span>
# BDLQuestionnairePublishStatus

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLQuestionnairePublishStatus
)
```


The publish status of questionnaires.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLQuestionnairePublishStatusUnknown |0 |Unknown. |
|BDLQuestionnairePublishStatusPublish |1 |Published. |


<span id="BDLLanguageType"></span>
# BDLLanguageType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLLanguageType
)
```


The language type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLLanguageTypeUnknown |\-1 |Unknown. |
|BDLLanguageTypeChinese |0 |Simplified Chinese. |
|BDLLanguageTypeEnglish |1 |English. |
|BDLLanguageTypeJapanese |2 |Japanese. |
|BDLLanguageTypeTraditional |3 |Traditional Chinese. |
|BDLLanguageTypeKorean |4 |Korean. |
|BDLLanguageTypeThai |5 |Thai. |
|BDLLanguageTypeVietnamese |6 |Vietnamese. |
|BDLLanguageTypeArabic |7 |Arabic. |
|BDLLanguageTypeTurkish |8 |Turkish. |
|BDLLanguageTypeSpanish |9 |Spanish. |
|BDLLanguageTypeIndonesian |10 |Indonesian. |
|BDLLanguageTypePortuguese |11 |Portuguese. |
|BDLLanguageTypeRussian |12 |Russian. |
|BDLLanguageTypeTagalog |13 |Tagalog. |
|BDLLanguageTypeKhmer |14 |Khmer. |
|BDLLanguageTypeLao |15 |Lao. |
|BDLLanguageTypeBurmese |16 |Burmese. |
|BDLLanguageTypeMalay |17 |Malay. |
|BDLLanguageTypeHindi |18 |Hindi. |
|BDLLanguageTypeFrench |19 |French. |
|BDLLanguageTypeGerman |20 |German. |
|BDLLanguageTypeItalian |21 |Italian. |


<span id="BDLPopupBaseViewProtocol"></span>
# BDLPopupBaseViewProtocol

```objectivec
@protocol BDLPopupBaseViewProtocol <NSObject>
```


The protocol for the base view of the dialog box.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setShowAnimationDuration:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseViewProtocol-setshowanimationduration) |
|void |[setHideAnimationDuration:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseViewProtocol-sethideanimationduration) |
|void |[setContentViewCorners:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseViewProtocol-setcontentviewcorners) |
|void |[setContentViewCornerRadii:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseViewProtocol-setcontentviewcornerradii) |
|void |[hideWithCompletion:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseViewProtocol-hidewithcompletion) |
|void |[hideWithAnimation:completion:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseViewProtocol-hidewithanimation-completion) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupBaseViewProtocol-setshowanimationduration"></span>
### setShowAnimationDuration:

```objectivec
- (void)setShowAnimationDuration:(NSTimeInterval)duration;
```


Sets the animation duration for displaying the dialog box. The duration implemented by `BDLPopupBaseView` is 0.3 seconds.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|duration |NSTimeInterval |The animation duration. Unit: seconds. |


<span id="BDLPopupBaseViewProtocol-sethideanimationduration"></span>
### setHideAnimationDuration:

```objectivec
- (void)setHideAnimationDuration:(NSTimeInterval)hideDuration;
```


Sets the animation duration for hiding the dialog box. The duration implemented by `BDLPopupBaseView` is 0.3 seconds.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|hideDuration |NSTimeInterval |The animation duration. Unit: seconds. |


<span id="BDLPopupBaseViewProtocol-setcontentviewcorners"></span>
### setContentViewCorners:

```objectivec
- (void)setContentViewCorners:(UIRectCorner)corner;
```


Sets rounded corners. By default, the upper\-left and upper\-right corners of the dialog box displayed at the bottom of the live room in portrait mode are rounded.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|corner |UIRectCorner |The rounded corner. |


<span id="BDLPopupBaseViewProtocol-setcontentviewcornerradii"></span>
### setContentViewCornerRadii:

```objectivec
- (void)setContentViewCornerRadii:(CGFloat)cornerRadii;
```


Sets the corner radius of the dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cornerRadii |CGFloat |The corner radius. Default value: `12`. |


<span id="BDLPopupBaseViewProtocol-hidewithcompletion"></span>
### hideWithCompletion:

```objectivec
- (void)hideWithCompletion:(nullable void (^)(BDLPopupBaseView *view))completion;
```


Hides the dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|completion |nullable void(^)(BDLPopupBaseView\*view) |The callback triggered after the dialog box is hidden. |


<span id="BDLPopupBaseViewProtocol-hidewithanimation-completion"></span>
### hideWithAnimation:completion:

```objectivec
- (void)hideWithAnimation:(nullable void (^)(void))animation completion:(nullable void (^)(BDLPopupBaseView *view))completion;
```


Hides the dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|animation |nullable void(^)(void) |The additional custom animations to execute when hiding the dialog box. |
|completion |nullable void(^)(BDLPopupBaseView\*view) |The callback triggered after the dialog box is hidden. |


<span id="BDLCardModel"></span>
# BDLCardModel

```objectivec
@interface BDLCardModel : BDLBaseModel
```


The product card model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[Id](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-id) |
|NSInteger |[index](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-index) |
|NSString\* |[title](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-title) |
|NSString\* |[highlight](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-highlight) |
|NSString\* |[strikeThrough](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-strikethrough) |
|NSString\* |[introduceImage](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-introduceimage) |
|NSString\* |[redirectImage](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-redirectimage) |
|NSString\* |[redirectUrl](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-redirecturl) |
|NSString\* |[directUrl](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-directurl) |
|NSInteger |[enableStatus](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-enablestatus) |
|NSInteger |[floatingStatus](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-floatingstatus) |
|NSString\* |[remark](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-remark) |
|NSDate\* |[explainTime](https://docs.byteplus.com/en/docs/11/17341#BDLCardModel-explaintime) |


<span id="instructions"></span>
## Instructions

<span id="BDLCardModel-id"></span>
### Id

```objectivec
@property (nonatomic, strong) NSNumber *Id;
```


The product ID.

<span id="BDLCardModel-index"></span>
### index

```objectivec
@property (nonatomic, assign) NSInteger index;
```


The product index.

<span id="BDLCardModel-title"></span>
### title

```objectivec
@property (nonatomic, copy) NSString *title;
```


The product name.

<span id="BDLCardModel-highlight"></span>
### highlight

```objectivec
@property (nonatomic, copy) NSString *highlight;
```


The product's retail price.

<span id="BDLCardModel-strikethrough"></span>
### strikeThrough

```objectivec
@property (nonatomic, copy) NSString *strikeThrough;
```


The product's list price.

<span id="BDLCardModel-introduceimage"></span>
### introduceImage

```objectivec
@property (nonatomic, copy) NSString *introduceImage;
```


The product image.

<span id="BDLCardModel-redirectimage"></span>
### redirectImage

```objectivec
@property (nonatomic, copy) NSString *redirectImage;
```


The product's button image.

<span id="BDLCardModel-redirecturl"></span>
### redirectUrl

```objectivec
@property (nonatomic, copy) NSString *redirectUrl;
```


The product URL.

<span id="BDLCardModel-directurl"></span>
### directUrl

```objectivec
@property (nonatomic, copy) NSString *directUrl;
```


The product's direct URL.

<span id="BDLCardModel-enablestatus"></span>
### enableStatus

```objectivec
@property (nonatomic, assign) NSInteger enableStatus;
```


Whether the product is listed on the viewing page. Valid values:


* `0`: Not listed.

* `1`: Listed.

    &nbsp;


<span id="floatingstatus"></span>
### floatingStatus

```objectivec
@property (nonatomic, assign) NSInteger floatingStatus;
```


Whether the product is featured, namely pinned to the top of the menu and displayed in a floating window on the viewing page. Valid values:


* `0`: Unfeatured.

* `1`: Featured.

    &nbsp;


<span id="remark"></span>
### remark

```objectivec
@property (nonatomic, copy) NSString *remark;
```


The product description.

<span id="BDLCardModel-explaintime"></span>
### explainTime

```objectivec
@property (nonatomic, strong, nullable) NSDate *explainTime;
```


The start time when the product is pinned to the top of the menu and displayed in a floating window on the viewing page.

<span id="BDLImageTextViewConfiguration(Config)"></span>
# BDLImageTextViewConfiguration(Config)

```objectivec
@interface BDLImageTextViewConfiguration (Config)
```


The configuration of the menu for graphics.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CGFloat |[viewMargin](https://docs.byteplus.com/en/docs/11/17341#BDLImageTextViewConfiguration(Config)-viewmargin) |
|UIColor\* |[imageTextTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLImageTextViewConfiguration(Config)-imagetexttextcolor) |


<span id="instructions"></span>
## Instructions

<span id="BDLImageTextViewConfiguration(Config)-viewmargin"></span>
### viewMargin

```objectivec
@property (nonatomic, assign) CGFloat viewMargin;
```


The margin of the WebView displaying the text and images relative to its parent control [BDLImageTextView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLImageTextView).

<span id="BDLImageTextViewConfiguration(Config)-imagetexttextcolor"></span>
### imageTextTextColor

```objectivec
@property (nonatomic, strong) UIColor *imageTextTextColor;
```


The text color under the menu for graphics. If `nil`, the text color returned by the BytePlus Live server is used.

<span id="BDLInteractiveQuizResultType"></span>
# BDLInteractiveQuizResultType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveQuizResultType
)
```


The timing for announcing the quiz answer.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveQuizResultTypeSubmit |0 |The answer is announced automatically after submission. |
|BDLInteractiveQuizResultTypeDeadline |1 |The answer is announced automatically when the time limit ends. |
|BDLInteractiveQuizResultTypeManual |2 |The answer is announced manually. |


<span id="BDLInteractiveVoteModel"></span>
# BDLInteractiveVoteModel

```objectivec
@interface BDLInteractiveVoteModel : BDLBaseModel
```


The vote model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[deadline](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveVoteModel-deadline) |
|NSString\* |[title](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveVoteModel-title) |
|NSString\* |[voteId](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveVoteModel-voteid) |
|BOOL |[userVotedStatus](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveVoteModel-uservotedstatus) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveVoteModel-deadline"></span>
### deadline

```objectivec
@property (nonatomic, assign) NSInteger deadline;
```


The voting deadline in Unix timestamp format. Unit: seconds.

<span id="BDLInteractiveVoteModel-title"></span>
### title

```objectivec
@property (nonatomic, copy) NSString *title;
```


The vote title.

<span id="BDLInteractiveVoteModel-voteid"></span>
### voteId

```objectivec
@property (nonatomic, copy) NSString *voteId;
```


The vote ID.

<span id="BDLInteractiveVoteModel-uservotedstatus"></span>
### userVotedStatus

```objectivec
@property (nonatomic, assign) BOOL userVotedStatus;
```


Whether the current viewer has submitted the vote.


* `YES`: Submitted.

* `NO`: Not submitted.

    &nbsp;


<span id="bdlvideoresolution"></span>
# BDLVideoResolution

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLVideoResolution
)
```


The video resolution.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLVideoResolutionUnknown |0 |\- |
|BDLVideoResolutionLD |1 |Smooth. |
|BDLVideoResolutionSD |2 |Standard Definition. |
|BDLVideoResolutionHD |3 |High Definition. |
|BDLVideoResolutionUHD |4 |Ultra\-High Definition. |
|BDLVideoResolutionBD |5 |Blu\-ray. |
|BDLVideoResolutionOrigin |6 |Original resolution. |
|BDLVideoResolutionAuto |7 |Smart. |


<span id="BDLInteractiveContextType"></span>
# BDLInteractiveContextType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveContextType
)
```


The content type of interaction tools.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveContextTypeText |1 |Text. |
|BDLInteractiveContextTypeImage |2 |Image. |
|BDLInteractiveContextTypeQuestionnaire |3 |Questionnaire. |
|BDLInteractiveContextTypeVote |5 |Vote. |
|BDLInteractiveContextTypeAward |6 |Real\-time lucky draw. |
|BDLInteractiveContextTypeCheckIn |8 |Check\-in. |
|BDLInteractiveContextTypeTaskAward |9 |Watch time\-based lucky draw. |
|BDLInteractiveContextTypeQuiz |10 |Quiz. |
|BDLInteractiveContextTypeAnnouncement |11 |Announcement. |


<span id="BDLFloatingCardConfiguration(Config)"></span>
# BDLFloatingCardConfiguration(Config)

```objectivec
@interface BDLFloatingCardConfiguration (Config)
```


The floating product card configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableDirectUrl](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingCardConfiguration(Config)-enabledirecturl) |
|NSString\* |[highLightString](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingCardConfiguration(Config)-highlightstring) |
|CGFloat |[cornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingCardConfiguration(Config)-cornerradius) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingCardConfiguration(Config)-enabledirecturl"></span>
### enableDirectUrl

```objectivec
@property (nonatomic, assign) BOOL enableDirectUrl;
```


Whether the direct URL feature is enabled. Default value: `NO`.


* `YES`: If the BytePlus Live server returns a direct URL, read the direct URL first. If no direct URL is returned, read the product URL.

* `NO`: Regardless of whether the BytePlus Live server returns a direct URL, read the product URL.

    &nbsp;


<span id="highlightstring"></span>
### highLightString

```objectivec
@property (nonatomic, copy, nullable) NSString *highLightString;
```


The retail price.

<span id="BDLFloatingCardConfiguration(Config)-cornerradius"></span>
### cornerRadius

```objectivec
@property (nonatomic, assign) CGFloat cornerRadius;
```


The background rounded corners of the floating product card. Unit: points. Default value: `5`.

<span id="BDLPopupBaseView"></span>
# BDLPopupBaseView

```objectivec
@interface BDLPopupBaseView : BDLBaseView <BDLPopupBaseViewProtocol, UIGestureRecognizerDelegate>
```


The base view of the dialog box.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[contentView](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseView-contentview) |
|UIEdgeInsets |[edgeInsets](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseView-edgeinsets) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onBackgroundTapCallback](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseView-onbackgroundtapcallback) |
|BDLPopupBaseView |[topPopupViewInView:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseView-toppopupviewinview) |
|BDLPopupBaseView |[neighborPopupViewInView:](https://docs.byteplus.com/en/docs/11/17341#BDLPopupBaseView-neighborpopupviewinview) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupBaseView-contentview"></span>
### contentView

```objectivec
@property (nonatomic, strong, readonly) UIView *contentView;
```


The content view of the dialog box. The `frame` is determined by the subclass.

<span id="BDLPopupBaseView-edgeinsets"></span>
### edgeInsets

```objectivec
@property (nonatomic) UIEdgeInsets edgeInsets;
```


The offset of the self instance (an instance of `BDLPopupBaseView` or its subclasses) relative to the superView (the view that displays the self instance).

<span id="instructions"></span>
## Instructions

<span id="BDLPopupBaseView-onbackgroundtapcallback"></span>
### onBackgroundTapCallback

```objectivec
@property (nonatomic, copy, nullable) void (^onBackgroundTapCallback)(BDLPopupBaseView *view);
```


The callback is triggered when the background is tapped. If `nil`, tapping the background has no effect.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLPopupBaseView\* |The base view of the dialog box. |


<span id="BDLPopupBaseView-toppopupviewinview"></span>
### topPopupViewInView:

```objectivec
- (BDLPopupBaseView *)topPopupViewInView:(UIView *)superview;
```


The `BDLPopupBaseView` instance that appears at the top in the superview, which is the most recently displayed dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|superview |UIView\* |The view to be searched for. |


**Return Value**

Instances of `BDLPopupBaseView` and its subclasses.

<span id="BDLPopupBaseView-neighborpopupviewinview"></span>
### neighborPopupViewInView:

```objectivec
- (BDLPopupBaseView *)neighborPopupViewInView:(UIView *)superview;
```


The `BDLPopupBaseView` instance adjacent to self in the superView, which is the previous dialog box of the current dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|superview |UIView\* |The view to be searched for. |


**Return Value**

Instances of `BDLPopupBaseView` and its subclasses.

<span id="BDLiveEffectAuthType"></span>
# BDLiveEffectAuthType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLiveEffectAuthType
)
```


The authorization method of the CV license.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLiveEffectAuthTypeNone |0 |No authorization, meaning the beauty AR, filters, and stickers features are not used. This is the default value. |
|BDLiveEffectAuthTypeOnLine |1 |Online authorization. You must set both [key](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-key) and [secret](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-secret). |
|BDLiveEffectAuthTypeOffLine |2 |Offline authorization. You must set the [licenseFilePath](https://docs.byteplus.com/en/docs/11/17341#BDLiveEffectAuthInfo-licensefilepath). |


<span id="BDLPageAdvertisementType"></span>
# BDLPageAdvertisementType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLPageAdvertisementType
)
```


The ad type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPageAdvertisementTypePageHeaderAd |1 |Header ads. |
|BDLPageAdvertisementTypePageAd |2 |In\-page ads. |
|BDLPageAdvertisementTypeFloatingAd |3 |Floating ads. |
|BDLPageAdvertisementTypeCardAd |4 |Product cards. |


<span id="BDLExternalReportConfiguration"></span>
# BDLExternalReportConfiguration

```objectivec
@interface BDLExternalReportConfiguration : BDLRTBaseConfiguration
```


Data reporting configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enable](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration-enable) |
|NSString\* |[url](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration-url) |
|CGFloat |[repeatInterval](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration-repeatinterval) |


<span id="instructions"></span>
## Instructions

<span id="BDLExternalReportConfiguration-enable"></span>
### enable

```objectivec
@property (nonatomic, assign) BOOL enable;
```


Whether to enable the data reporting feature. Default value: `NO`. Valid values:


* `YES`: Enable. The SDK will report data to the [url](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration-url) at the following timing:

   * When a viewer joins the live room successfully.

   * While a viewer is in the live room, data is reported at intervals specified by [repeatInterval](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration-repeatinterval).

   * When a viewer leaves the live room.

* `NO`: Disable.

    &nbsp;


<span id="url"></span>
### url

```objectivec
@property (nonatomic, copy) NSString *url;
```


After enabling the data reporting feature through [enable](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration-enable), the SDK will send a `POST` request to this URL at specific timing for data reporting.

<span id="BDLExternalReportConfiguration-repeatinterval"></span>
### repeatInterval

```objectivec
@property (nonatomic, assign) CGFloat repeatInterval;
```


The time interval for reporting data. Unit: seconds. Default value: `30`.

<span id="BDLFloatingInteractiveToolViewType"></span>
# BDLFloatingInteractiveToolViewType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLFloatingInteractiveToolViewType
)
```


The type of interaction tool floating window view.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLFloatingInteractiveToolViewTypeAnnouncement |1 |Announcement. |
|BDLFloatingInteractiveToolViewTypeVote |2 |Vote. |
|BDLFloatingInteractiveToolViewTypeQuiz |3 |Quiz. |
|BDLFloatingInteractiveToolViewTypeOngoingAward |4 |The lucky draw in progress. |
|BDLFloatingInteractiveToolViewTypeOpenedAward |5 |The lucky draw already drawn. |
|BDLFloatingInteractiveToolViewTypeQuestionnaire |6 |Questionnaire. |
|BDLFloatingInteractiveToolViewTypeTaskAward |7 |Watch time\-based lucky draw. |
|BDLFloatingInteractiveToolViewTypeCheckIn |8 |Check\-in. |


<span id="BDLCommentModel"></span>
# BDLCommentModel

```objectivec
@interface BDLCommentModel: BDLBaseModel
```


The comment model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLCommentType |[localCommentType](https://docs.byteplus.com/en/docs/11/17341#BDLCommentModel-localcommenttype) |
|BDLCommentCommonModel\* |[common](https://docs.byteplus.com/en/docs/11/17341#BDLCommentModel-common) |
|BDLCommentExtraModel\* |[extra](https://docs.byteplus.com/en/docs/11/17341#BDLCommentModel-extra) |
|NSAttributedString\* |[localShowAttributedString](https://docs.byteplus.com/en/docs/11/17341#BDLCommentModel-localshowattributedstring) |
|NSArray\* |[localClickableRanges](https://docs.byteplus.com/en/docs/11/17341#BDLCommentModel-localclickableranges) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentModel-localcommenttype"></span>
### localCommentType

```objectivec
@property (nonatomic, assign) BDLCommentType localCommentType;
```


The comment type. Not returned by the BytePlus Live server.

<span id="BDLCommentModel-common"></span>
### common

```objectivec
@property (nonatomic, strong) BDLCommentCommonModel *common;
```


The model of public comment information. For more information, see [BDLCommentCommonModel](https://docs.byteplus.com/en/docs/11/17341#BDLCommentCommonModel).

<span id="BDLCommentModel-extra"></span>
### extra

```objectivec
@property (nonatomic, strong) BDLCommentExtraModel *extra;
```


The model of additional comment information. For more information, see [BDLCommentExtraModel](https://docs.byteplus.com/en/docs/11/17341#BDLCommentExtraModel).

<span id="BDLCommentModel-localshowattributedstring"></span>
### localShowAttributedString

```objectivec
@property (nonatomic, copy) NSAttributedString *localShowAttributedString;
```


The cached rich text to be displayed. Not returned by the BytePlus Live server.

<span id="BDLCommentModel-localclickableranges"></span>
### localClickableRanges

```objectivec
@property (nonatomic, copy) NSArray *localClickableRanges;
```


The cached clickable area. Not returned by the BytePlus Live server.

<span id="BDLLiveRoomConfiguration"></span>
# BDLLiveRoomConfiguration

```objectivec
@interface BDLLiveRoomConfiguration : NSObject
```


The live room configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLPopupTopCommentViewConfiguration\* |[popupTopCommentViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-popuptopcommentviewconfig) |
|BDLPopupWebViewConfiguration\* |[popupWebViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-popupwebviewconfig) |
|BDLPopupInputViewConfiguration\* |[popupInputViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-popupinputviewconfig) |
|BDLCommentViewConfiguration\* |[commentViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-commentviewconfig) |
|BDLCardConfiguration\* |[cardConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-cardconfig) |
|BDLPlayerConfiguration\* |[playerConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-playerconfig) |
|BDLBasePlayerConfiguration\* |[basePlayerConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-baseplayerconfig) |
|BDLImageTextViewConfiguration\* |[imageTextViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-imagetextviewconfig) |
|BDLInteractiveToolConfiguration\* |[interactiveToolConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-interactivetoolconfig) |
|BDLMenuBarConfiguration\* |[menuBarConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-menubarconfig) |
|BDLMenuViewConfiguration\* |[menuViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-menuviewconfig) |
|BDLFloatingCardConfiguration\* |[floatingCardConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-floatingcardconfig) |
|BDLPageAdViewConfiguration\* |[pageAdViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-pageadviewconfig) |
|BDLMoreOptionsViewConfiguration\* |[moreOptionsViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-moreoptionsviewconfig) |
|BDLAwardConfiguration\* |[awardConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-awardconfig) |
|BDLMultiLanguageConfiguration\* |[multiLanguageConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-multilanguageconfig) |
|BDLUserInfoConfiguration\* |[userInfoConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-userinfoconfig) |
|BDLPeopleCountConfiguration\* |[peopleCountConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-peoplecountconfig) |
|BDLBusinessAccountConfiguration\* |[businessAccountConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-businessaccountconfig) |
|BDLCommentAndNoticeViewConfiguration\* |[commentAndNoticeViewConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-commentandnoticeviewconfig) |
|BDLFloatingControllerConfiguration\* |[floatingControllerConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-floatingcontrollerconfig) |
|BDLExternalReportConfiguration\* |[externalReportConfig](https://docs.byteplus.com/en/docs/11/17341#BDLLiveRoomConfiguration-externalreportconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLLiveRoomConfiguration-popuptopcommentviewconfig"></span>
### popupTopCommentViewConfig

```objectivec
@property (nonatomic, strong) BDLPopupTopCommentViewConfiguration *popupTopCommentViewConfig;
```


The configuration of the pinned comment details dialog box. For more information, see [BDLPopupTopCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/11/17341#BDLPopupTopCommentViewConfiguration(Config)).

<span id="BDLLiveRoomConfiguration-popupwebviewconfig"></span>
### popupWebViewConfig

```objectivec
@property (nonatomic, strong) BDLPopupWebViewConfiguration *popupWebViewConfig;
```


The WebView dialog box configuration. For more information, see [BDLPopupWebViewConfiguration(Config)](https://docs.byteplus.com/en/docs/11/17341#BDLPopupWebViewConfiguration(Config)).

<span id="BDLLiveRoomConfiguration-popupinputviewconfig"></span>
### popupInputViewConfig

```objectivec
@property (nonatomic, strong) BDLPopupInputViewConfiguration *popupInputViewConfig;
```


The configuration of the nickname text box. For more information, see [BDLPopupInputViewConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLPopupInputViewConfiguration).

<span id="BDLLiveRoomConfiguration-commentviewconfig"></span>
### commentViewConfig

```objectivec
@property (nonatomic, strong) BDLCommentViewConfiguration *commentViewConfig;
```


The configuration of the comment area and top comments. For more information, see [BDLCommentViewConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration).

<span id="BDLLiveRoomConfiguration-cardconfig"></span>
### cardConfig

```objectivec
@property (nonatomic, strong) BDLCardConfiguration *cardConfig;
```


The product card configuration. For more information, see [BDLCardConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLCardConfiguration(Config)).

<span id="BDLLiveRoomConfiguration-playerconfig"></span>
### playerConfig

```objectivec
@property (nonatomic, strong) BDLPlayerConfiguration *playerConfig;
```


The player configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerConfiguration).

<span id="BDLLiveRoomConfiguration-baseplayerconfig"></span>
### basePlayerConfig

```objectivec
@property (nonatomic, strong) BDLBasePlayerConfiguration *basePlayerConfig;
```


The custom player configuration. For more information, see [BDLBasePlayerConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLBasePlayerConfiguration).

<span id="BDLLiveRoomConfiguration-imagetextviewconfig"></span>
### imageTextViewConfig

```objectivec
@property (nonatomic, strong) BDLImageTextViewConfiguration *imageTextViewConfig;
```


The configuration of the menu for graphics. For more information, see [BDLImageTextViewConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLImageTextViewConfiguration).

<span id="BDLLiveRoomConfiguration-interactivetoolconfig"></span>
### interactiveToolConfig

```objectivec
@property (nonatomic, strong) BDLInteractiveToolConfiguration *interactiveToolConfig;
```


The configuration of the menu for interaction tools. For more information, see [BDLInteractiveToolConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolConfiguration).

<span id="BDLLiveRoomConfiguration-menubarconfig"></span>
### menuBarConfig

```objectivec
@property (nonatomic, strong) BDLMenuBarConfiguration *menuBarConfig;
```


The menu bar configuration. For more information, see [BDLMenuBarConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLMenuBarConfiguration).

<span id="BDLLiveRoomConfiguration-menuviewconfig"></span>
### menuViewConfig

```objectivec
@property (nonatomic, strong) BDLMenuViewConfiguration *menuViewConfig;
```


The configuration of the menu bar container view. For more information, see [BDLMenuViewConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLMenuViewConfiguration).

<span id="BDLLiveRoomConfiguration-floatingcardconfig"></span>
### floatingCardConfig

```objectivec
@property (nonatomic, strong) BDLFloatingCardConfiguration *floatingCardConfig;
```


The floating product card configuration. For more information, see [BDLFloatingCardConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingCardConfiguration(Config)).

<span id="BDLLiveRoomConfiguration-pageadviewconfig"></span>
### pageAdViewConfig

```objectivec
@property (nonatomic, strong) BDLPageAdViewConfiguration *pageAdViewConfig;
```


The in\-page ad configuration. For more information, see [BDLPageAdViewConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLPageAdViewConfiguration).

<span id="BDLLiveRoomConfiguration-moreoptionsviewconfig"></span>
### moreOptionsViewConfig

```objectivec
@property (nonatomic, strong) BDLMoreOptionsViewConfiguration *moreOptionsViewConfig;
```


The configuration of the more options dialog box. For more information, see [BDLMoreOptionsViewConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLMoreOptionsViewConfiguration).

<span id="BDLLiveRoomConfiguration-awardconfig"></span>
### awardConfig

```objectivec
@property (nonatomic, strong) BDLAwardConfiguration *awardConfig;
```


The lucky draw configuration. For more information, see [BDLAwardConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLAwardConfiguration).

<span id="BDLLiveRoomConfiguration-multilanguageconfig"></span>
### multiLanguageConfig

```objectivec
@property (nonatomic, strong) BDLMultiLanguageConfiguration *multiLanguageConfig;
```


The configuration of multi\-language customization. For more information, see [BDLMultiLanguageConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLMultiLanguageConfiguration).

<span id="BDLLiveRoomConfiguration-userinfoconfig"></span>
### userInfoConfig

```objectivec
@property (nonatomic, strong) BDLUserInfoConfiguration *userInfoConfig;
```


The user information configuration. For more information, see [BDLUserInfoConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLUserInfoConfiguration).

<span id="BDLLiveRoomConfiguration-peoplecountconfig"></span>
### peopleCountConfig

```objectivec
@property (nonatomic, strong) BDLPeopleCountConfiguration *peopleCountConfig;
```


The popularity configuration. For more information, see [BDLPeopleCountConfiguration](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPeopleCountConfiguration(Config)).

<span id="BDLLiveRoomConfiguration-businessaccountconfig"></span>
### businessAccountConfig

```objectivec
@property (nonatomic, strong) BDLBusinessAccountConfiguration *businessAccountConfig;
```


The host account configuration. For more information, see [BDLBusinessAccountConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLBusinessAccountConfiguration(Config)).

<span id="BDLLiveRoomConfiguration-commentandnoticeviewconfig"></span>
### commentAndNoticeViewConfig

```objectivec
@property (nonatomic, strong) BDLCommentAndNoticeViewConfiguration *commentAndNoticeViewConfig;
```


The configuration of the comment and notification view. For more information, see [BDLCommentAndNoticeViewConfiguration](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLCommentAndNoticeViewConfiguration).

<span id="BDLLiveRoomConfiguration-floatingcontrollerconfig"></span>
### floatingControllerConfig

```objectivec
@property (nonatomic, strong) BDLFloatingControllerConfiguration *floatingControllerConfig;
```


The configuration of the floating window controller. For more information, see [BDLFloatingControllerConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLFloatingControllerConfiguration).

<span id="BDLLiveRoomConfiguration-externalreportconfig"></span>
### externalReportConfig

```objectivec
@property (nonatomic, strong) BDLExternalReportConfiguration *externalReportConfig;
```


Data reporting configuration. For more information, see [BDLExternalReportConfiguration](https://docs.byteplus.com/en/docs/11/17341#BDLExternalReportConfiguration).

<span id="BDLiveBizType"></span>
# BDLiveBizType

```objectivec
typedef NS_OPTIONS(
    NSUInteger,
    BDLiveBizType
)
```


The business type for BytePlus Live SDK.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLiveBizTypeNone |0 |None, which is the default value. |
|BDLiveBizTypeViewer |1 << 1 |Viewer SDK. |
|BDLiveBizTypeLiveStreaming |1 << 2 |Live Streaming SDK. |
|BDLiveBizTypeAll |NSUIntegerMax |All business types except for `BDLiveBizTypeNone`. |


<span id="BDLPopupBottomOrRightShowViewProtocol"></span>
# BDLPopupBottomOrRightShowViewProtocol

```objectivec
@protocol BDLPopupBottomOrRightShowViewProtocol <BDLPopupBottomShowViewProtocol, BDLPopupRightShowViewProtocol>
```


The protocol for displaying the dialog box at the bottom or on the right.

<span id="BDLRegisterStatus"></span>
# BDLRegisterStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLRegisterStatus
)
```


The registration status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLRegisterStatusUnregistered |0 |Unregistered. |
|BDLRegisterStatusRegistering |1 |Registering. |
|BDLRegisterStatusRegistered |2 |Registered. |


<span id="BDLPopupTopShowBaseView"></span>
# BDLPopupTopShowBaseView

```objectivec
@interface BDLPopupTopShowBaseView : BDLPopupBaseView <BDLPopupTopShowViewProtocol>
```


The base view for the top dialog box view.

<span id="BDLTaskAwardStatus"></span>
# BDLTaskAwardStatus

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLTaskAwardStatus
)
```


The status of the watch time\-based lucky draws.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLTaskAwardStatusInit |0 |Initializing. |
|BDLTaskAwardStatusStart |1 |Started. |
|BDLTaskAwardStatusEnd |2 |Ended. |
|BDLTaskAwardStatusClose |3 |Closed. |


<span id="BDLInteractiveToolConfiguration"></span>
# BDLInteractiveToolConfiguration

```objectivec
@interface BDLInteractiveToolConfiguration : BDLRTBaseConfiguration
```


The configuration of the menu for interation tools.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[customizeFloatingViewImageViewImage](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveToolConfiguration-customizefloatingviewimageviewimage) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolConfiguration-customizefloatingviewimageviewimage"></span>
### customizeFloatingViewImageViewImage

```objectivec
@property (nonatomic, copy, nullable) void(^customizeFloatingViewImageViewImage)(UIImageView *imageView, BDLFloatingInteractiveToolViewType type);
```


Customizes the floating window image view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|imageView |UIImageView\* |The floating window image view. |
|type |BDLFloatingInteractiveToolViewType |The type of interaction tool floating window view. For details, see [BDLFloatingInteractiveToolViewType](https://docs.byteplus.com/en/docs/11/17341#bdlfloatinginteractivetoolviewtype). |


<span id="BDLActivityAuthMode"></span>
# BDLActivityAuthMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLActivityAuthMode
)
```


The authentication mode of the live room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLActivityAuthModeUnknown |0 |Unknown mode, which is the default value. |
|BDLActivityAuthModePublic |1 |Public mode. The nickname is entered by the viewer or passed through the `nickname` parameter of the [setNickname:complete:](https://docs.byteplus.com/en/docs/11/17341#BDLUserInfoConfiguration-setnickname-complete) method. |
|BDLActivityAuthModeCustom |2 |Custom mode. Viewers join the live room by logging in to your own account system. Nicknames are synchronized from your own account system to the live room, without requiring viewers to enter. |


<span id="BDLForceOfflineInfo"></span>
# BDLForceOfflineInfo

```objectivec
@interface BDLForceOfflineInfo : BDLBaseModel
```


The information model for viewers being forcibly removed from the live room.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLForceOfflineReason |[reason](https://docs.byteplus.com/en/docs/11/17341#BDLForceOfflineInfo-reason) |
|NSString\* |[prompt](https://docs.byteplus.com/en/docs/11/17341#BDLForceOfflineInfo-prompt) |


<span id="instructions"></span>
## Instructions

<span id="BDLForceOfflineInfo-reason"></span>
### reason

```objectivec
@property (nonatomic, assign) BDLForceOfflineReason reason;
```


The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineReason](https://docs.byteplus.com/en/docs/11/17341#BDLForceOfflineReason).

<span id="BDLForceOfflineInfo-prompt"></span>
### prompt

```objectivec
@property (nonatomic, copy, nullable) NSString *prompt;
```


The prompt text for viewers being forcibly removed from the live room.

<span id="BDLAwardUserStatus"></span>
# BDLAwardUserStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLAwardUserStatus
)
```


The status of viewer participation in the lucky draw.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLAwardUserStatusNotParticipate |1 |Not participated. |
|BDLAwardUserStatusParticipated |2 |Already participated. |
|BDLAwardUserStatusWin |4 |Won. |
|BDLAwardUserStatusUnWin |5 |Not won. |


<span id="BDLSendActivityMessageResult"></span>
# BDLSendActivityMessageResult

```objectivec
@interface BDLSendActivityMessageResult : BDLBaseModel
```


The result after comments are successfully sent.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[H5MsgId](https://docs.byteplus.com/en/docs/11/17341#BDLSendActivityMessageResult-h5msgid) |
|NSString\* |[nickname](https://docs.byteplus.com/en/docs/11/17341#BDLSendActivityMessageResult-nickname) |
|BDLSendMessageResultStatus |[status](https://docs.byteplus.com/en/docs/11/17341#BDLSendActivityMessageResult-status) |


<span id="instructions"></span>
## Instructions

<span id="BDLSendActivityMessageResult-h5msgid"></span>
### H5MsgId

```objectivec
@property (nonatomic, copy) NSString *H5MsgId;
```


The comment ID.

<span id="BDLSendActivityMessageResult-nickname"></span>
### nickname

```objectivec
@property (nonatomic, copy) NSString *nickname;
```


The nickname of the user who sent the comment.

<span id="BDLSendActivityMessageResult-status"></span>
### status

```objectivec
@property (nonatomic, assign) BDLSendMessageResultStatus status;
```


The status after comments are sent, which is returned by the BytePlus Live server. For more information, see [BDLSendMessageResultStatus](https://docs.byteplus.com/en/docs/11/17341#BDLSendMessageResultStatus).

<span id="BDLQuestionnaireQuestionType"></span>
# BDLQuestionnaireQuestionType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLQuestionnaireQuestionType
)
```


The question types of questionnaires.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLQuestionnaireQuestionTypeUnknown |0 |Unknown. |
|BDLQuestionnaireQuestionTypeRadio |1 |Multiple choice \> Choose one. |
|BDLQuestionnaireQuestionTypeCheckbox |2 |Multiple choice \> Choose all that apply. |
|BDLQuestionnaireQuestionTypeText |3 |Fill\-in\-the\-blank. |
|BDLQuestionnaireQuestionTypePhoneNumber |4 |Phone number. |
|BDLQuestionnaireQuestionTypeEmail |5 |Email. |
|BDLQuestionnaireQuestionTypeNickname |6 |Nickname. |


<span id="BDLActivityBookingModel"></span>
# BDLActivityBookingModel

```objectivec
@interface BDLActivityBookingModel : BDLBaseModel
```


The model of live booking information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[activityName](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-activityname) |
|NSNumber\* |[activityId](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-activityid) |
|NSDate\* |[startDate](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-startdate) |
|NSDate\* |[endDate](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-enddate) |
|NSString\* |[nickname](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-nickname) |
|NSString\* |[externalUserId](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-externaluserid) |
|NSNumber\* |[userId](https://docs.byteplus.com/en/docs/11/17341#BDLActivityBookingModel-userid) |


<span id="instructions"></span>
## Instructions

<span id="BDLActivityBookingModel-activityname"></span>
### activityName

```objectivec
@property (nonatomic, copy) NSString *activityName;
```


The live room name.

<span id="BDLActivityBookingModel-activityid"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


The activity ID of the live room.

<span id="BDLActivityBookingModel-startdate"></span>
### startDate

```objectivec
@property (nonatomic, strong) NSDate *startDate;
```


The start time of the live stream.

<span id="BDLActivityBookingModel-enddate"></span>
### endDate

```objectivec
@property (nonatomic, strong) NSDate *endDate;
```


The end time of the live stream.

<span id="BDLActivityBookingModel-nickname"></span>
### nickname

```objectivec
@property (nonatomic, copy, nullable) NSString *nickname;
```


The viewer's nickname.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>nil</code>.</div>


<span id="BDLActivityBookingModel-externaluserid"></span>
### externalUserId

```objectivec
@property (nonatomic, copy, nullable) NSString *externalUserId;
```


The unique identifier of the viewer on third\-party platforms.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property has a value only when the authentication mode is custom and the viewer has logged in to the live room.</div>


<span id="BDLActivityBookingModel-userid"></span>
### userId

```objectivec
@property (nonatomic, strong, nullable) NSNumber *userId;
```


The user ID, which is the unique identifier of the viewer in BytePlus Live.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>0</code>.</div>


<span id="BDLCommentViewConfiguration"></span>
# BDLCommentViewConfiguration

```objectivec
@interface BDLCommentViewConfiguration : BDLCommentBaseConfiguration
```


The configuration of the comment area and top comments.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLThemeIconModel\* |[commentLikeIcon](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration-commentlikeicon) |
|BDLThemeIconModel\* |[commentLikedIcon](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration-commentlikedicon) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[customizeCommentCell](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration-customizecommentcell) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewConfiguration-commentlikeicon"></span>
### commentLikeIcon

```objectivec
@property (nonatomic, strong, readonly) BDLThemeIconModel *commentLikeIcon;
```


The like icon when the comment is not liked.

<span id="BDLCommentViewConfiguration-commentlikedicon"></span>
### commentLikedIcon

```objectivec
@property (nonatomic, strong, readonly) BDLThemeIconModel *commentLikedIcon;
```


The like icon when the comment is liked.

<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewConfiguration-customizecommentcell"></span>
### customizeCommentCell

```objectivec
void customizeCommentCell(
    BDLCommentView *view,
    BDLCommentViewCell *commentViewCell,
    BDLCommentModel *comment,
    BOOL isPortrait,
    BOOL isCommentTranslateEnable,
    BOOL isLikeEnable,
    BOOL isDarkTheme,
    BDLLanguageType langType,
    NSArray *langTypes
);
```


Customizes the comment cell.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLCommentView\* |The comment area view. For more information, see [BDLCommentView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLCommentView). |
|commentViewCell |BDLCommentViewCell\* |The comment cell. For more information, see [BDLCommentViewCell](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLCommentViewCell). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/17341#BDLCommentModel). |
|isPortrait |BOOL |Whether the live room is in portrait mode. The value is passed in by the initialization method [initWithActivityId:isPortrait:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController-initwithactivityid-isportrait-liveengine) or [initWithActivityId:isPortrait:basePlayerView:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController-initwithactivityid-isportrait-liveengine-baseplayerview).<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|isCommentTranslateEnable |BOOL |Whether to enable comment translation.<br><br><br>* `YES`: Enable.<br><br>* `NO`: Disable. |
|isLikeEnable |BOOL |Whether to enable comment liking.<br><br><br>* `YES`: Enable.<br><br>* `NO`: Disable. |
|isDarkTheme |BOOL |Whether the theme is the dark mode.<br><br><br>&nbsp;<br><br>* `YES`: The dark mode.<br><br>* `NO`: Not the dark mode. |
|langType |BDLLanguageType |The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/17341#BDLLanguageType). |
|langTypes |NSArray\* |All the currently supported language types. |


<span id="BDLInteractiveQuizModel"></span>
# BDLInteractiveQuizModel

```objectivec
@interface BDLInteractiveQuizModel : BDLInteractiveCountdownBaseModel
```


The quiz model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[quizTitle](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quiztitle) |
|NSNumber\* |[quizID](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quizid) |
|NSNumber\* |[activityID](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-activityid) |
|BDLInteractiveQuizResultType |[quizResultType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quizresulttype) |
|BDLInteractiveQuizTitleType |[quizTitleType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quiztitletype) |
|BDLInteractiveQuizStatus |[quizStatus](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quizstatus) |
|NSArray<BDLVoteQuizOptionModel\*\>\* |[quizOptions](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quizoptions) |
|NSArray<NSString\*\>\* |[rightOptions](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-rightoptions) |
|BOOL |[isRight](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-isright) |
|NSArray<NSString\*\>\* |[submitOptions](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-submitoptions) |
|NSString\* |[quizAnalysis](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizModel-quizanalysis) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveQuizModel-quiztitle"></span>
### quizTitle

```objectivec
@property (nonatomic, copy) NSString *quizTitle;
```


The quiz title.

<span id="BDLInteractiveQuizModel-quizid"></span>
### quizID

```objectivec
@property (nonatomic, strong) NSNumber *quizID;
```


The quiz ID.

<span id="BDLInteractiveQuizModel-activityid"></span>
### activityID

```objectivec
@property (nonatomic, strong) NSNumber *activityID;
```


The activity ID of the live room corresponding to the quiz.

<span id="BDLInteractiveQuizModel-quizresulttype"></span>
### quizResultType

```objectivec
@property (nonatomic, assign) BDLInteractiveQuizResultType quizResultType;
```


The timing for announcing the answer. For more information, see [BDLInteractiveQuizResultType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizResultType).

<span id="BDLInteractiveQuizModel-quiztitletype"></span>
### quizTitleType

```objectivec
@property (nonatomic, assign) BDLInteractiveQuizTitleType quizTitleType;
```


The quiz type. For more information, see [BDLInteractiveQuizTitleType](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizTitleType).

<span id="BDLInteractiveQuizModel-quizstatus"></span>
### quizStatus

```objectivec
@property (nonatomic, assign) BDLInteractiveQuizStatus quizStatus;
```


The quiz status. For more information, see [BDLInteractiveQuizStatus](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveQuizStatus).

<span id="BDLInteractiveQuizModel-quizoptions"></span>
### quizOptions

```objectivec
@property (nonatomic, copy) NSArray<BDLVoteQuizOptionModel *> *quizOptions;
```


The options. For more information, see [BDLVoteQuizOptionModel](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel).

<span id="BDLInteractiveQuizModel-rightoptions"></span>
### rightOptions

```objectivec
@property (nonatomic, copy) NSArray<NSString *> *rightOptions;
```


The correct answer, which corresponds to the [optionsite](https://docs.byteplus.com/en/docs/11/17341#BDLVoteQuizOptionModel-optionsite).

<span id="BDLInteractiveQuizModel-isright"></span>
### isRight

```objectivec
@property (nonatomic, assign) BOOL isRight;
```


Whether the answer is correct.


* `YES`: Correct.

* `NO`: Incorrect.

    &nbsp;


<span id="submitoptions"></span>
### submitOptions

```objectivec
@property (nonatomic, copy) NSArray<NSString *> *submitOptions;
```


The option selected by the viewer.

<span id="BDLInteractiveQuizModel-quizanalysis"></span>
### quizAnalysis

```objectivec
@property (nonatomic, copy) NSString *quizAnalysis;
```


The answer explanation.

<span id="BDLMoreOptionsViewConfiguration"></span>
# BDLMoreOptionsViewConfiguration

```objectivec
@interface BDLMoreOptionsViewConfiguration : BDLRTBaseConfiguration
```


The configuration of the more options dialog box.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The more options dialog box is displayed after viewers tap the more (...) icon in the lower\-right corner of the live room in portrait mode.</div>


<span id="BDLPageAdViewConfiguration"></span>
# BDLPageAdViewConfiguration

```objectivec
@interface BDLPageAdViewConfiguration : BDLRTBaseConfiguration
```


The in\-page ad configuration.

<span id="BDLCommentBaseConfiguration(Config)"></span>
# BDLCommentBaseConfiguration(Config)

```objectivec
@interface BDLCommentBaseConfiguration (Config)
```


The base configuration for comments and top comments.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[landscapeShouldShowAvatar](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-landscapeshouldshowavatar) |
|BOOL |[portraitShouldShowAvatar](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-portraitshouldshowavatar) |
|UIImage\* |[defaultAvatar](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-defaultavatar) |
|UIImage\* |[defaultHostAvatar](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-defaulthostavatar) |
|NSTimeInterval |[voiceInterval](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-voiceinterval) |
|UIFont\* |[commentFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-commentfont) |
|UIFont\* |[nickNameFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-nicknamefont) |
|UIFont\* |[hostCommentFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-hostcommentfont) |
|UIColor\* |[hostCommentColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-hostcommentcolor) |
|UIFont\* |[hostTagFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-hosttagfont) |
|UIColor\* |[hostTagColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-hosttagcolor) |
|UIColor\* |[nickNameColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-nicknamecolor) |
|UIColor\* |[commentColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-commentcolor) |
|UIColor\* |[linkColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-linkcolor) |
|UIColor\* |[hostCommentBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-hostcommentbackgroundcolor) |
|UIColor\* |[backgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-backgroundcolor) |
|NSString\* |[inputBoxPrompt](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-inputboxprompt) |
|UIColor\* |[inputBoxTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-inputboxtextcolor) |
|UIColor\* |[popupInputBoxTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-popupinputboxtextcolor) |
|NSString\* |[justSendPrompt](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-justsendprompt) |
|UIFont\* |[justSendFont](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-justsendfont) |
|UIImage\* |[noCommentImage](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-nocommentimage) |
|BOOL |[enableAudienceURLTap](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-enableaudienceurltap) |
|NSUInteger |[rowsOfComment](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-rowsofcomment) |
|CGFloat |[commentContentLineSpacingExtra](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-commentcontentlinespacingextra) |
|NSUInteger |[singlePullCount](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-singlepullcount) |
|NSUInteger |[pullMaxNumber](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-pullmaxnumber) |
|NSUInteger |[commentInputCountLimit](https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-commentinputcountlimit) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentBaseConfiguration(Config)-landscapeshouldshowavatar"></span>
### landscapeShouldShowAvatar

```objectivec
@property (nonatomic, assign) BOOL landscapeShouldShowAvatar;
```


Whether to display the avatar for the live room in landscape mode. Default value: `YES`.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="portraitshouldshowavatar"></span>
### portraitShouldShowAvatar

```objectivec
@property (nonatomic, assign) BOOL portraitShouldShowAvatar;
```


Whether to display the avatar for the live room in portrait mode. Default value: `NO`.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="defaultavatar"></span>
### defaultAvatar

```objectivec
@property (nonatomic, strong) UIImage *defaultAvatar;
```


The default avatar for non\-hosts.

<span id="BDLCommentBaseConfiguration(Config)-defaulthostavatar"></span>
### defaultHostAvatar

```objectivec
@property (nonatomic, strong) UIImage *defaultHostAvatar;
```


The default avatar for the host.

<span id="BDLCommentBaseConfiguration(Config)-voiceinterval"></span>
### voiceInterval

```objectivec
@property (nonatomic, assign) NSTimeInterval voiceInterval;
```


The minimum interval between comments. Unit: seconds. Default value: `3`.

<span id="BDLCommentBaseConfiguration(Config)-commentfont"></span>
### commentFont

```objectivec
@property (nonatomic, strong) UIFont *commentFont;
```


The font, font size, and other properties of non\-hosts' comments. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentBaseConfiguration(Config)-nicknamefont"></span>
### nickNameFont

```objectivec
@property (nonatomic, strong) UIFont *nickNameFont;
```


The font, font size, and other properties of non\-hosts' nicknames. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentBaseConfiguration(Config)-hostcommentfont"></span>
### hostCommentFont

```objectivec
 @property (nonatomic, strong) UIFont *hostCommentFont;
```


The font, font size, and other properties of the host's comments. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentBaseConfiguration(Config)-hostcommentcolor"></span>
### hostCommentColor

```objectivec
@property (nonatomic, strong) UIColor *hostCommentColor;
```


The text color of the host's comments.

<span id="BDLCommentBaseConfiguration(Config)-hosttagfont"></span>
### hostTagFont

```objectivec
@property (nonatomic, strong) UIFont *hostTagFont;
```


The font, font size, and other properties of the host tag. For more information, see [UIFont](https://developer.apple.com/documentation/uikit/uifont?language=objc).

<span id="BDLCommentBaseConfiguration(Config)-hosttagcolor"></span>
### hostTagColor

```objectivec
 @property (nonatomic, strong) UIColor *hostTagColor;
```


The color of the host tag.

<span id="BDLCommentBaseConfiguration(Config)-nicknamecolor"></span>
### nickNameColor

```objectivec
@property (nonatomic, strong) UIColor *nickNameColor;
```


The text color of non\-hosts' nicknames.

<span id="BDLCommentBaseConfiguration(Config)-commentcolor"></span>
### commentColor

```objectivec
@property (nonatomic, strong) UIColor *commentColor;
```


The text color of non\-hosts' comments.

<span id="BDLCommentBaseConfiguration(Config)-linkcolor"></span>
### linkColor

```objectivec
@property (nonatomic, strong) UIColor *linkColor;
```


The color of clickable URLs in comments.

<span id="BDLCommentBaseConfiguration(Config)-hostcommentbackgroundcolor"></span>
### hostCommentBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *hostCommentBackgroundColor;
```


The background color of the host's comments.

<span id="BDLCommentBaseConfiguration(Config)-backgroundcolor"></span>
### backgroundColor

```objectivec
@property (nonatomic, strong) UIColor *backgroundColor;
```


The background color for the welcome message, entrance message, and non\-hosts' comments.

<span id="BDLCommentBaseConfiguration(Config)-inputboxprompt"></span>
### inputBoxPrompt

```objectivec
@property (nonatomic, copy, nullable) NSString *inputBoxPrompt;
```


The placeholder text of the comment text box in non\-editing status, namely when the keyboard is not popped up. You can modify this property before or after viewers join the live room.

<span id="BDLCommentBaseConfiguration(Config)-inputboxtextcolor"></span>
### inputBoxTextColor

```objectivec
@property (nonatomic, strong) UIColor *inputBoxTextColor;
```


The color of the text entered in the comment text box.

<span id="BDLCommentBaseConfiguration(Config)-popupinputboxtextcolor"></span>
### popupInputBoxTextColor

```objectivec
@property (nonatomic, strong) UIColor *popupInputBoxTextColor;
```


The entered text color for the comment text box in editing status, namely when the keyboard is popped up. You can modify this property before or after viewers join the live room.

<span id="BDLCommentBaseConfiguration(Config)-justsendprompt"></span>
### justSendPrompt

```objectivec
@property (nonatomic, copy) NSString *justSendPrompt;
```


The prompt text for sending too frequently.

<span id="BDLCommentBaseConfiguration(Config)-justsendfont"></span>
### justSendFont

```objectivec
@property (nonatomic, strong) UIFont *justSendFont;
```


The font and font size of the prompt text for sending too frequently.

<span id="BDLCommentBaseConfiguration(Config)-nocommentimage"></span>
### noCommentImage

```objectivec
@property (nonatomic, strong) UIImage *noCommentImage;
```


The image displayed when no comments are under the menu.

<span id="BDLCommentBaseConfiguration(Config)-enableaudienceurltap"></span>
### enableAudienceURLTap

```objectivec
@property (nonatomic, assign) BOOL enableAudienceURLTap;
```


Whether URLs in non\-hosts' comments are clickable. Default value: `NO`.


* `YES`: Clickable.

* `NO`: Not clickable.

    &nbsp;


<span id="rowsofcomment"></span>
### rowsOfComment

```objectivec
@property (nonatomic, assign) NSUInteger rowsOfComment;
```


The number of lines displayed for comments. If a comment exceeds the configured number of display lines, the full content of the comment cannot be displayed. The default value `0` means that the full content of the comment is displayed regardless of the number of lines.

<span id="BDLCommentBaseConfiguration(Config)-commentcontentlinespacingextra"></span>
### commentContentLineSpacingExtra

```objectivec
@property (nonatomic, assign) CGFloat commentContentLineSpacingExtra;
```


Line spacing for the comment content. Unit: point.


* If the value is less than or equal to `0`, the default [[NSParagraphStyle defaultParagraphStyle].lineSpacing](https://developer.apple.com/documentation/uikit/nsparagraphstyle/linespacing?language=objc) is used.

* For values greater than `0`, assign it to [[NSParagraphStyle defaultParagraphStyle].lineSpacing](https://developer.apple.com/documentation/uikit/nsparagraphstyle/linespacing?language=objc).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property is valid only when the value of <a href="https://docs.byteplus.com/en/docs/11/17341#BDLCommentBaseConfiguration(Config)-rowsofcomment">rowsOfComment</a> is <code>0</code> or greater than<code>1</code>.</div>


<span id="BDLCommentBaseConfiguration(Config)-singlepullcount"></span>
### singlePullCount

```objectivec
@property (nonatomic, assign) NSUInteger singlePullCount;
```


The number of comments to pull each time. Default value: `20`.

<span id="BDLCommentBaseConfiguration(Config)-pullmaxnumber"></span>
### pullMaxNumber

```objectivec
@property (nonatomic, assign) NSUInteger pullMaxNumber;
```


The maximum number of comments to pull. Default value: `10,000`.

<span id="BDLCommentBaseConfiguration(Config)-commentinputcountlimit"></span>
### commentInputCountLimit

```objectivec
@property (nonatomic, assign) NSUInteger commentInputCountLimit;
```


The maximum number of characters allowed in the comment text box. Default value: `200`.

<span id="BDLMessageContentType"></span>
# BDLMessageContentType

```objectivec
typedef NS_OPTIONS(
    NSUInteger,
    BDLMessageContentType
)
```


The message content type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLMessageContentTypeText |0 |Text. |
|BDLMessageContentTypeImage |1 |Image. |


<span id="BDLMenuViewConfiguration"></span>
# BDLMenuViewConfiguration

```objectivec
@interface BDLMenuViewConfiguration : BDLRTBaseConfiguration
```


The configuration of the menu bar container view.

<span id="BDLSDKAuthErrorCode"></span>
# BDLSDKAuthErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLSDKAuthErrorCode
)
```


Error codes for SDK initialization failure.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLSDKAuthErrorCodeProcessing |1 |The previously called [startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete) method has not yet been completed. The `startWithAuthInfo:complete:` method can only be called again after the SDK initialization completion callback (`complete`) is triggered. |
|BDLSDKAuthErrorCodeInvalidBizType |2 |[bizType](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-biztype) is not available. Make sure the value is not `BDLiveBizTypeNone`. |
|BDLSDKAuthErrorCodeInvalidAppId |3 |[appId](https://docs.byteplus.com/en/docs/11/17341#BDLiveAuthInfo-appid) is not available. Make sure the value is not `nil`. |
|BDLSDKAuthErrorCodeVodAuthFail |4 |VOD authorization failed. Check the VOD license, such as whether the license file has expired, or whether the bundle ID used when applying for the VOD license matches the bundle ID configured in the project. |
|BDLSDKAuthErrorCodeLivePullAuthFail |5 |Pull streaming authorization failed. Check the live streaming license, such as whether the license file has expired, or whether the bundle ID used when applying for the live streaming license matches the bundle ID configured in the project. |
|BDLSDKAuthErrorCodeLivePushAuthFail |6 |Push streaming authorization failed. Check the live streaming license, such as whether the license file has expired, or whether the bundle ID used when applying for the live streaming license matches the bundle ID configured in the project. |
|BDLSDKAuthErrorCodeEffectAuthFail |7 |CV license authorization failed. Check whether the CV license authorization information is correct, such as whether the bundle ID used when applying for the CV license matches the bundle ID configured in the project. |


<span id="BDLCommentTextViewBeginEditingModel"></span>
# BDLCommentTextViewBeginEditingModel

```objectivec
@interface BDLCommentTextViewBeginEditingModel : BDLBaseModel
```


Information required to determine whether to allow viewers to enter content in the comment text box. This can be used in the [textViewShouldBeginEditing](https://docs.byteplus.com/en/docs/11/17341#BDLCommentViewConfiguration(Config)-textviewshouldbeginediting) method.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[activityId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentTextViewBeginEditingModel-activityid) |
|NSString\* |[nickname](https://docs.byteplus.com/en/docs/11/17341#BDLCommentTextViewBeginEditingModel-nickname) |
|NSString\* |[externalUserId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentTextViewBeginEditingModel-externaluserid) |
|NSNumber\* |[userId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentTextViewBeginEditingModel-userid) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentTextViewBeginEditingModel-activityid"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


The activity ID of the live room.

<span id="BDLCommentTextViewBeginEditingModel-nickname"></span>
### nickname

```objectivec
@property (nonatomic, copy, nullable) NSString *nickname;
```


The viewer's nickname.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>nil</code>.</div>


<span id="BDLCommentTextViewBeginEditingModel-externaluserid"></span>
### externalUserId

```objectivec
@property (nonatomic, copy, nullable) NSString *externalUserId;
```


The unique identifier of the viewer on third\-party platforms.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property has a value only when the authentication mode is custom and the viewer has logged in to the live room.</div>


<span id="BDLCommentTextViewBeginEditingModel-userid"></span>
### userId

```objectivec
@property (nonatomic, strong, nullable) NSNumber *userId;
```


The user ID, which is the unique identifier of the viewer in BytePlus Live.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>0</code>.</div>


<span id="BDLEmbeddedWebModel"></span>
# BDLEmbeddedWebModel

```objectivec
@interface BDLEmbeddedWebModel : BDLBaseModel
```


The model of embedded link menu.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[embeddedWebId](https://docs.byteplus.com/en/docs/11/17341#BDLEmbeddedWebModel-embeddedwebid) |
|NSString\* |[mobileUrl](https://docs.byteplus.com/en/docs/11/17341#BDLEmbeddedWebModel-mobileurl) |


<span id="instructions"></span>
## Instructions

<span id="BDLEmbeddedWebModel-embeddedwebid"></span>
### embeddedWebId

```objectivec
@property (nonatomic, assign) NSInteger embeddedWebId;
```


The ID of this model.

<span id="BDLEmbeddedWebModel-mobileurl"></span>
### mobileUrl

```objectivec
@property (nonatomic, copy) NSString *mobileUrl;
```


The URL.

<span id="BDLPlayerPortraitConfiguration"></span>
# BDLPlayerPortraitConfiguration

```objectivec
@interface BDLPlayerPortraitConfiguration : BDLPlayerBaseConfiguration
```


The configuration of the player in portrait mode.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIColor\* |[replayButtonBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerPortraitConfiguration-replaybuttonbackgroundcolor) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerPortraitConfiguration-replaybuttonbackgroundcolor"></span>
### replayButtonBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *replayButtonBackgroundColor;
```


The background color of the replay button.

<span id="BDLCommentCommonModel"></span>
# BDLCommentCommonModel

```objectivec
@interface BDLCommentCommonModel : BDLBaseModel
```


The model of public comment information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[msgId](https://docs.byteplus.com/en/docs/11/17341#BDLCommentCommonModel-msgid) |
|long |[createTime](https://docs.byteplus.com/en/docs/11/17341#BDLCommentCommonModel-createtime) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentCommonModel-msgid"></span>
### msgId

```objectivec
@property (nonatomic, strong) NSNumber *msgId;
```


The comment ID.

<span id="BDLCommentCommonModel-createtime"></span>
### createTime

```objectivec
@property (nonatomic, assign) long createTime;
```


The creation time in Unix timestamp format. Unit: seconds.

<span id="BDLInteractiveQuizStatus"></span>
# BDLInteractiveQuizStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveQuizStatus
)
```


The quiz status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveQuizStatusInit |0 |Initializing. |
|BDLInteractiveQuizStatusSend |1 |Sent. |
|BDLInteractiveQuizStatusManual |2 |Answer manually announced. |
|BDLInteractiveQuizStatusEnd |3 |Ended. |
|BDLInteractiveQuizStatusDelete |4 |Deleted. |
|BDLInteractiveQuizStatusRevoke |5 |Withdrawn. |


<span id="BDLMenuBarConfiguration(Config)"></span>
# BDLMenuBarConfiguration(Config)

```objectivec
@interface BDLMenuBarConfiguration (Config)
```


The menu bar configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIColor\* |[tabColor](https://docs.byteplus.com/en/docs/11/17341#BDLMenuBarConfiguration(Config)-tabcolor) |
|UIColor\* |[selectedTabColor](https://docs.byteplus.com/en/docs/11/17341#BDLMenuBarConfiguration(Config)-selectedtabcolor) |


<span id="instructions"></span>
## Instructions

<span id="BDLMenuBarConfiguration(Config)-tabcolor"></span>
### tabColor

```objectivec
@property (nonatomic, strong) UIColor *tabColor;
```


The default color of the title.

<span id="BDLMenuBarConfiguration(Config)-selectedtabcolor"></span>
### selectedTabColor

```objectivec
@property (nonatomic, strong) UIColor *selectedTabColor;
```


The color of the selected title.

<span id="BDLPlayerBaseConfiguration"></span>
# BDLPlayerBaseConfiguration

```objectivec
@interface BDLPlayerBaseConfiguration : NSObject
```


The base class configuration of the player.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLPlayerScalingMode |[scalingMode](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-scalingmode) |
|BOOL |[liveEnterForegroundAutoPlay](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-liveenterforegroundautoplay) |
|BOOL |[previewEnterForegroundAutoPlay](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-previewenterforegroundautoplay) |
|BOOL |[playbackEnterForegroundAutoPlay](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-playbackenterforegroundautoplay) |
|NSString\* |[retryButtonTitle](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-retrybuttontitle) |
|CGFloat |[retryButtonCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-retrybuttoncornerradius) |
|UIColor\* |[retryButtonBackgroundColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-retrybuttonbackgroundcolor) |
|NSString\* |[replayText](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-replaytext) |
|UIColor\* |[replayTextColor](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-replaytextcolor) |
|UIImage\* |[replayButtonNormalImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-replaybuttonnormalimage) |
|CGSize |[replayButtonNormalImageSize](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-replaybuttonnormalimagesize) |
|CGFloat |[replayButtonCornerRadius](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-replaybuttoncornerradius) |
|UIImage\* |[loadingImage](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-loadingimage) |
|CGSize |[loadingImageSize](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerBaseConfiguration-loadingimagesize) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerBaseConfiguration-scalingmode"></span>
### scalingMode

```objectivec
@property (nonatomic, assign) BDLPlayerScalingMode scalingMode;
```


The video scaling mode.

The default value for the live room in portrait mode is `BDLPlayerScalingModeAspectFill` and that for the live room in landscape mode is `BDLPlayerScalingModeAspectFit`. For more information, see [BDLPlayerScalingMode](https://docs.byteplus.com/en/docs/11/17341#BDLPlayerScalingMode).

<span id="BDLPlayerBaseConfiguration-liveenterforegroundautoplay"></span>
### liveEnterForegroundAutoPlay

```objectivec
@property (nonatomic, assign) BOOL liveEnterForegroundAutoPlay;
```


Whether to automatically play the live stream when switching from the background to the foreground. Default value: `YES`.


* `YES`: Automatically play.

* `NO`: Do not automatically play.

    &nbsp;


<span id="previewenterforegroundautoplay"></span>
### previewEnterForegroundAutoPlay

```objectivec
@property (nonatomic, assign) BOOL previewEnterForegroundAutoPlay;
```


Whether to automatically play the preview when switching from the background to the foreground. Default value: `NO`.


* `YES`: Automatically play.

* `NO`: Do not automatically play.

    &nbsp;


<span id="playbackenterforegroundautoplay"></span>
### playbackEnterForegroundAutoPlay

```objectivec
@property (nonatomic, assign) BOOL playbackEnterForegroundAutoPlay;
```


Whether to automatically play the playback when switching from the background to the foreground. Default value: `NO`.


* `YES`: Automatically play.

* `NO`: Do not automatically play.

    &nbsp;


<span id="retrybuttontitle"></span>
### retryButtonTitle

```objectivec
@property (nonatomic, copy) NSString *retryButtonTitle;
```


The text of the retry button.

<span id="BDLPlayerBaseConfiguration-retrybuttoncornerradius"></span>
### retryButtonCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat retryButtonCornerRadius;
```


The corner radius of the retry button.

<span id="BDLPlayerBaseConfiguration-retrybuttonbackgroundcolor"></span>
### retryButtonBackgroundColor

```objectivec
@property (nonatomic, strong) UIColor *retryButtonBackgroundColor;
```


The background color of the retry button.

<span id="BDLPlayerBaseConfiguration-replaytext"></span>
### replayText

```objectivec
@property (nonatomic, copy) NSString *replayText;
```


The replay prompt text.

<span id="BDLPlayerBaseConfiguration-replaytextcolor"></span>
### replayTextColor

```objectivec
@property (nonatomic, strong) UIColor *replayTextColor;
```


The text color of the replay prompt.

<span id="BDLPlayerBaseConfiguration-replaybuttonnormalimage"></span>
### replayButtonNormalImage

```objectivec
@property (nonatomic, strong) UIImage *replayButtonNormalImage;
```


The image of the replay button.

<span id="BDLPlayerBaseConfiguration-replaybuttonnormalimagesize"></span>
### replayButtonNormalImageSize

```objectivec
@property (nonatomic, assign) CGSize replayButtonNormalImageSize;
```


The image size of the replay button.

<span id="BDLPlayerBaseConfiguration-replaybuttoncornerradius"></span>
### replayButtonCornerRadius

```objectivec
@property (nonatomic, assign) CGFloat replayButtonCornerRadius;
```


The corner radius of the replay button.

<span id="BDLPlayerBaseConfiguration-loadingimage"></span>
### loadingImage

```objectivec
@property (nonatomic, strong) UIImage *loadingImage;
```


The loading image.

<span id="BDLPlayerBaseConfiguration-loadingimagesize"></span>
### loadingImageSize

```objectivec
@property (nonatomic, assign) CGSize loadingImageSize;
```


The size of the loading image.

<span id="BDLPlayerState"></span>
# BDLPlayerState

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLPlayerState
)
```


The player status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLPlayerStateUnknown |0 |Unknown. |
|BDLPlayerStatePrepared |1 |The player is ready, waiting for rendering. |
|BDLPlayerStateStopped |2 |Stop playing. |
|BDLPlayerStatePlaying |3 |Playing. |
|BDLPlayerStatePaused |4 |Paused. |
|BDLPlayerStateError |5 |Error. |


<span id="BDLSendActivityMessageResponse"></span>
# BDLSendActivityMessageResponse

```objectivec
@interface BDLSendActivityMessageResponse : BDLBaseResponse
```


The result after comments are sent, which is returned by the BytePlus Live server.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLSendActivityMessageResult\* |[result](https://docs.byteplus.com/en/docs/11/17341#BDLSendActivityMessageResponse-result) |


<span id="instructions"></span>
## Instructions

<span id="BDLSendActivityMessageResponse-result"></span>
### result

```objectivec
@property (nonatomic, strong) BDLSendActivityMessageResult *result;
```


The result of sending comments. For more information, see [BDLSendActivityMessageResult](https://docs.byteplus.com/en/docs/11/17341#BDLSendActivityMessageResult).

<span id="BDLNetworkService"></span>
# BDLNetworkService

```objectivec
@protocol BDLNetworkService <NSObject>
```


The network\-related service.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BDLNetworkStatus |[networkStatus](https://docs.byteplus.com/en/docs/11/17341#BDLNetworkService-networkstatus) |


<span id="instructions"></span>
## Instructions

<span id="BDLNetworkService-networkstatus"></span>
### networkStatus

```objectivec
- (BDLNetworkStatus)networkStatus;
```


Gets the current network status.

**Return Value**

The current network status. For more information, see [BDLNetworkStatus](https://docs.byteplus.com/en/docs/11/17341#BDLNetworkStatus).

<span id="BDLPopupTopCommentViewConfiguration"></span>
# BDLPopupTopCommentViewConfiguration

```objectivec
@interface BDLPopupTopCommentViewConfiguration : BDLRTBaseConfiguration
```


The configuration of the pinned comment details dialog box.

<span id="BDLInteractiveAnnouncementModel"></span>
# BDLInteractiveAnnouncementModel

```objectivec
@interface BDLInteractiveAnnouncementModel : BDLBaseModel
```


The announcement model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[announcementId](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAnnouncementModel-announcementid) |
|NSString\* |[title](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAnnouncementModel-title) |
|NSString\* |[content](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAnnouncementModel-content) |
|NSInteger |[sendTime](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAnnouncementModel-sendtime) |
|NSString\* |[contentString](https://docs.byteplus.com/en/docs/11/17341#BDLInteractiveAnnouncementModel-contentstring) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveAnnouncementModel-announcementid"></span>
### announcementId

```objectivec
@property (nonatomic, assign) NSInteger announcementId;
```


The announcement ID.

<span id="BDLInteractiveAnnouncementModel-title"></span>
### title

```objectivec
@property (nonatomic, copy) NSString *title;
```


The announcement title.

<span id="BDLInteractiveAnnouncementModel-content"></span>
### content

```objectivec
@property (nonatomic, copy) NSString *content;
```


The announcement content.

<span id="BDLInteractiveAnnouncementModel-sendtime"></span>
### sendTime

```objectivec
@property (nonatomic, assign) NSInteger sendTime;
```


The send time in Unix timestamp format. Unit: seconds.

<span id="BDLInteractiveAnnouncementModel-contentstring"></span>
### contentString

```objectivec
@property (nonatomic, copy) NSString *contentString;
```


The text of the `content` displayed under the menu for interaction tools. Not returned by the BytePlus Live server.
