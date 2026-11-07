---
title: "Viewer SDK for iOS: APIs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine"
---

<span id="BDLAwardNoticeView"></span>
# BDLAwardNoticeView

```objectivec
@interface BDLAwardNoticeView : UIView <BDLLanguageService>
```


The lucky draw notification view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSArray\* |[langTypes](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-langtypes) |
|BDLLanguageType |[langType](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-langtype) |
|UIImageView\* |[bgImageView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-bgimageview) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-titlelabel) |
|UIButton\* |[participateButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-participatebutton) |
|BDLInteractiveAwardModel\* |[award](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-award) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onParticipateClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView-onparticipateclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardNoticeView-langtypes"></span>
### langTypes

```objectivec
@property (nonatomic, copy, readonly) NSArray *langTypes;
```


All the currently supported language types.

<span id="BDLAwardNoticeView-langtype"></span>
### langType

```objectivec
@property (nonatomic, assign, readonly) BDLLanguageType langType;
```


The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType).

<span id="BDLAwardNoticeView-bgimageview"></span>
### bgImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *bgImageView;
```


The background image. All properties can be customized.

<span id="BDLAwardNoticeView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The text label of "Lucky draw in progress". The `text` cannot be customized.

<span id="BDLAwardNoticeView-participatebutton"></span>
### participateButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *participateButton;
```


The participate button. The `text` in the `Normal` status cannot be customized.

<span id="BDLAwardNoticeView-award"></span>
### award

```objectivec
@property (nonatomic, strong) BDLInteractiveAwardModel *award;
```


The lucky draw information corresponding to the current notification. For more information, see [BDLInteractiveAwardModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveAwardModel).

<span id="instructions"></span>
## Instructions

<span id="BDLAwardNoticeView-onparticipateclickblock"></span>
### onParticipateClickBlock

```objectivec
@property (nonatomic, copy) void(^onParticipateClickBlock)(BDLAwardNoticeView *view);
```


The callback is triggered when the participate button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardNoticeView\* |The lucky draw notification view. |


<span id="BDLPlayerReplayView"></span>
# BDLPlayerReplayView

```objectivec
@interface BDLPlayerReplayView : BDLBaseView <BDLLanguageService>
```


The replay view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLPlayerReplayViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerReplayView-delegate) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:config:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerReplayView-initwithportrait-config) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerReplayView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerReplayView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLPlayerReplayViewDelegate> delegate;
```


The delegate method. For more information, see [BDLPlayerReplayViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLPlayerReplayViewDelegate).

<span id="instructions"></span>
## Instructions

<span id="BDLPlayerReplayView-initwithportrait-config"></span>
### initWithPortrait:config:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait config:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the replay view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the replay view.

<span id="BDLPlayerReplayView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLMultiLanguageView"></span>
# BDLMultiLanguageView

```objectivec
@interface BDLMultiLanguageView : BDLPopupBottomShowBaseView <BDLLanguageService>
```


The language selection dialog box view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLMultiLanguageViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLMultiLanguageView-delegate) |
|UITableView\* |[tableView](https://docs.byteplus.com/en/docs/11/5590#BDLMultiLanguageView-tableview) |
|UIButton\* |[cancelButton](https://docs.byteplus.com/en/docs/11/5590#BDLMultiLanguageView-cancelbutton) |


<span id="instructions"></span>
## Instructions

<span id="BDLMultiLanguageView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLMultiLanguageViewDelegate> delegate;
```


The delegate method. For more information, see [BDLMultiLanguageViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLMultiLanguageViewDelegate).

<span id="BDLMultiLanguageView-tableview"></span>
### tableView

```objectivec
@property (nonatomic, strong) UITableView *tableView;
```


The container view of the language list. All properties except `hidden` can be customized. If `hidden` is set to `YES`, a blank dialog box will appear.

<span id="BDLMultiLanguageView-cancelbutton"></span>
### cancelButton

```objectivec
@property (nonatomic, strong) UIButton *cancelButton;
```


The cancel button. All properties except `normalText` and `frame` can be customized.

<span id="BDLNoticeContainerView"></span>
# BDLNoticeContainerView

```objectivec
@interface BDLNoticeContainerView : BDLBaseView <BDLNoticeService, BDLInteractiveToolService>
```


The container view of notifications.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|UIView\* |[customizeAwardNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLNoticeContainerView-customizeawardnoticeview) |
|void |[hideShowingNoticeViewWithFinish:](https://docs.byteplus.com/en/docs/11/5590#BDLNoticeContainerView-hideshowingnoticeviewwithfinish) |


<span id="instructions"></span>
## Instructions

<span id="BDLNoticeContainerView-customizeawardnoticeview"></span>
### customizeAwardNoticeView

```objectivec
@property (nonatomic, copy) __kindof UIView * (^customizeAwardNoticeView)(BDLNoticeContainerView *view, BDLAwardNoticeView *noticeView, BDLInteractiveAwardModel *award);
```


Customizes the lucky draw notification view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLNoticeContainerView\* |The container view of notifications. |
|noticeView |BDLAwardNoticeView\* |The lucky draw notification view. For more information, see [BDLAwardNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNoticeView). |
|award |BDLInteractiveAwardModel\* |The lucky draw information. For more information, see [BDLInteractiveAwardModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveAwardModel). |


**Return Value**

Instances of `UIView` and its subclasses.

<span id="BDLNoticeContainerView-hideshowingnoticeviewwithfinish"></span>
### hideShowingNoticeViewWithFinish:

```objectivec
- (void)hideShowingNoticeViewWithFinish:(void (^ _Nullable )(void))finish;
```


Hides the currently displayed notification view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|finish |void(^)(void) |The callback triggered when the notification view is hidden. |


<span id="BDLAwardWinnersView"></span>
# BDLAwardWinnersView

```objectivec
@interface BDLAwardWinnersView : BDLPopupCenterShowBaseView <BDLLanguageService>
```


The prize winner list view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLLanguageType |[languageType](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-languagetype) |
|UIImageView\* |[topBackgroundImageView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-topbackgroundimageview) |
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-closebutton) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-titlelabel) |
|UILabel\* |[countLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-countlabel) |
|UITableView\* |[tableView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-tableview) |
|BDLLoadingView\* |[loadingView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-loadingview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[backButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView-backbuttonclickedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardWinnersView-languagetype"></span>
### languageType

```objectivec
@property (nonatomic, assign, readonly) BDLLanguageType languageType;
```


The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType).

<span id="BDLAwardWinnersView-topbackgroundimageview"></span>
### topBackgroundImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *topBackgroundImageView;
```


The imageView for the top background. Customization is supported.

<span id="BDLAwardWinnersView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *closeButton;
```


The close button. Customization is supported.

<span id="BDLAwardWinnersView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The title label of the prize winner list. All properties except `text` can be customized.

<span id="BDLAwardWinnersView-countlabel"></span>
### countLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *countLabel;
```


The text label of "X winners in total". All properties except `text` can be customized.

<span id="BDLAwardWinnersView-tableview"></span>
### tableView

```objectivec
@property (nonatomic, strong, readonly) UITableView *tableView;
```


The container tableView of the prize winner list. Customization is supported.

<span id="BDLAwardWinnersView-loadingview"></span>
### loadingView

```objectivec
@property (nonatomic, strong, readonly) BDLLoadingView *loadingView;
```


The loading view. For more information, see [BDLLoadingView](https://docs.byteplus.com/en/docs/11/5590#BDLLoadingView).

<span id="instructions"></span>
## Instructions

<span id="BDLAwardWinnersView-backbuttonclickedblock"></span>
### backButtonClickedBlock

```objectivec
@property (nonatomic, copy) void (^backButtonClickedBlock)(BDLAwardWinnersView *view);
```


The callback is triggered when the back button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardWinnersView\* |The prize winner list view. |


<span id="BDLGetInviteTokenResponse"></span>
# BDLGetInviteTokenResponse

```objectivec
@interface BDLGetInviteTokenResponse : BDLBaseResponse
```


The result after getting the invitation information, which is returned by the BytePlus Live server.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLGetInviteTokenResult\* |[result](https://docs.byteplus.com/en/docs/11/5590#BDLGetInviteTokenResponse-result) |


<span id="instructions"></span>
## Instructions

<span id="BDLGetInviteTokenResponse-result"></span>
### result

```objectivec
@property (nonatomic, strong) BDLGetInviteTokenResult *result;
```


The result after getting the invitation information. For more information, see [BDLGetInviteTokenResult](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLGetInviteTokenResult).

<span id="BDLCardView"></span>
# BDLCardView

```objectivec
@interface BDLCardView : BDLBaseView <BDLLanguageService, BDLPullStreamUrlService, BDLBasicService>
```


The content view of the product card.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLCardView-isportrait) |
|BDLCardConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLCardView-config) |
|UITableView\* |[tableView](https://docs.byteplus.com/en/docs/11/5590#BDLCardView-tableview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLCardView-initwithportrait) |


<span id="instructions"></span>
## Instructions

<span id="BDLCardView-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.

    &nbsp;


<span id="config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLCardConfiguration *config;
```


The configuration of the product card. For more information, see [BDLCardConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCardConfiguration(Config)).

<span id="BDLCardView-tableview"></span>
### tableView

```objectivec
@property (nonatomic, strong, readonly) UITableView *tableView;
```


The container tableView to display products. All properties except `frame` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLCardView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the product card view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the product card view.

<span id="BDLCommentInputBaseView"></span>
# BDLCommentInputBaseView

```objectivec
@interface BDLCommentInputBaseView : BDLCommentBaseView <
UINavigationControllerDelegate,
UIImagePickerControllerDelegate
>
```


The parent control of the comment area under the menu for chat interaction.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[popupSuperView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentInputBaseView-popupsuperview) |
|UIView\* |[commentPromptView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentInputBaseView-commentpromptview) |
|UILabel\* |[commentPromptLabel](https://docs.byteplus.com/en/docs/11/5590#BDLCommentInputBaseView-commentpromptlabel) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[resetTextView:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentInputBaseView-resettextview) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentInputBaseView-popupsuperview"></span>
### popupSuperView

```objectivec
@property (nonatomic, weak) UIView *popupSuperView;
```


The parent view for displaying the dialog box. The SDK has a default implementation for dialog boxes such as the nickname text box. The dialog box will be added on top of `popupSuperView`.

<span id="BDLCommentInputBaseView-commentpromptview"></span>
### commentPromptView

```objectivec
@property (nonatomic, strong, readonly) UIView *commentPromptView;
```


The new comment prompt view. All properties except `hidden` and `frame` can be customized.

<span id="BDLCommentInputBaseView-commentpromptlabel"></span>
### commentPromptLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *commentPromptLabel;
```


The new comment notification label. All properties except `hidden` and `frame` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLCommentInputBaseView-resettextview"></span>
### resetTextView:

```objectivec
- (void)resetTextView:(BOOL)willEdit;
```


Resets the comment text box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|willEdit |BOOL |Whether in edit mode.<br><br><br>&nbsp;<br><br>* `YES`: In edit mode.<br><br>* `NO`: Not in edit mode. |


<span id="BDLCommentViewCellDelegate"></span>
# BDLCommentViewCellDelegate

```objectivec
@protocol BDLCommentViewCellDelegate <NSObject>
```


The delegate methods for the comment cell.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[commentViewCell:didClickLikeWithComment:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCellDelegate-commentviewcell-didclicklikewithcomment) |
|BOOL |[commentViewCell:shouldInteractWithURL:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCellDelegate-commentviewcell-shouldinteractwithurl) |
|void |[commentViewCell:didClickNicknameWithModel:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCellDelegate-commentviewcell-didclicknicknamewithmodel) |
|void |[commentViewCell:didClickTextContentWithModel:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCellDelegate-commentviewcell-didclicktextcontentwithmodel) |
|void |[commentViewCell:didClickBackgroundViewWithModel:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCellDelegate-commentviewcell-didclickbackgroundviewwithmodel) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewCellDelegate-commentviewcell-didclicklikewithcomment"></span>
### commentViewCell:didClickLikeWithComment:

```objectivec
- (void)commentViewCell:(BDLCommentViewCell *)cell didClickLikeWithComment:(BDLCommentModel *)comment;
```


The SDK calls this method when viewers tap the button for liking comments.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cell |BDLCommentViewCell\* |The comment cell. For more information, see [BDLCommentViewCell](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLCommentViewCellDelegate-commentviewcell-shouldinteractwithurl"></span>
### commentViewCell:shouldInteractWithURL:

```objectivec
- (BOOL)commentViewCell:(BDLCommentViewCell *)cell shouldInteractWithURL:(NSURL *)URL;
```


The SDK calls this method when viewers tap the URL in a comment.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cell |BDLCommentViewCell\* |The comment cell. For more information, see [BDLCommentViewCell](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell). |
|URL |NSURL\* |The tapped URL. |


**Return Value**

Whether the SDK responds to the URL.


* `YES`: Respond.

* `NO`: Do not respond.

    &nbsp;


<span id="commentviewcell-didclicknicknamewithmodel"></span>
### commentViewCell:didClickNicknameWithModel:

```objectivec
- (void)commentViewCell:(BDLCommentViewCell *)cell didClickNicknameWithModel:(id)model;
```


The SDK calls this method when viewers tap the nickname or avatar of a user who sent the comment.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cell |BDLCommentViewCell\* |The comment cell. For more information, see [BDLCommentViewCell](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell). |
|model |id |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLCommentViewCellDelegate-commentviewcell-didclicktextcontentwithmodel"></span>
### commentViewCell:didClickTextContentWithModel:

```objectivec
- (void)commentViewCell:(BDLCommentViewCell *)cell didClickTextContentWithModel:(id)model;
```


The SDK calls this method when viewers tap the text comment.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cell |BDLCommentViewCell\* |The comment cell. For more information, see [BDLCommentViewCell](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell). |
|model |id |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLCommentViewCellDelegate-commentviewcell-didclickbackgroundviewwithmodel"></span>
### commentViewCell:didClickBackgroundViewWithModel:

```objectivec
- (void)commentViewCell:(BDLCommentViewCell *)cell didClickBackgroundViewWithModel:(id)model;
```


The SDK calls this method when viewers tap the comment bubble.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cell |BDLCommentViewCell\* |The comment cell. For more information, see [BDLCommentViewCell](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell). |
|model |id |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLAwardItemConfig"></span>
# BDLAwardItemConfig

```objectivec
@interface BDLAwardItemConfig : BDLBaseModel
```


The lucky draw configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[awardId](https://docs.byteplus.com/en/docs/11/5590#BDLAwardItemConfig-awardid) |
|NSString\* |[awardItemName](https://docs.byteplus.com/en/docs/11/5590#BDLAwardItemConfig-awarditemname) |
|int |[awardItemCount](https://docs.byteplus.com/en/docs/11/5590#BDLAwardItemConfig-awarditemcount) |
|BDLInteractiveAwardItemType |[awardItemType](https://docs.byteplus.com/en/docs/11/5590#BDLAwardItemConfig-awarditemtype) |
|NSString\* |[awardItemIcon](https://docs.byteplus.com/en/docs/11/5590#BDLAwardItemConfig-awarditemicon) |
|BDLAwardContactOptions |[contactOptions](https://docs.byteplus.com/en/docs/11/5590#BDLAwardItemConfig-contactoptions) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardItemConfig-awardid"></span>
### awardId

```objectivec
@property (nonatomic, strong) NSNumber *awardId;
```


The lucky draw ID.

<span id="BDLAwardItemConfig-awarditemname"></span>
### awardItemName

```objectivec
@property (nonatomic, copy) NSString *awardItemName;
```


The lucky draw name.

<span id="BDLAwardItemConfig-awarditemcount"></span>
### awardItemCount

```objectivec
@property (nonatomic, assign) int awardItemCount;
```


The number of prizes.

<span id="BDLAwardItemConfig-awarditemtype"></span>
### awardItemType

```objectivec
@property (nonatomic, assign) BDLInteractiveAwardItemType awardItemType;
```


The prize type. For more information, see [BDLInteractiveAwardItemType](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveAwardItemType).

<span id="BDLAwardItemConfig-awarditemicon"></span>
### awardItemIcon

```objectivec
@property (nonatomic, copy) NSString *awardItemIcon;
```


The lucky draw icon.

<span id="BDLAwardItemConfig-contactoptions"></span>
### contactOptions

```objectivec
@property (nonatomic, assign) BDLAwardContactOptions contactOptions;
```


The information type that winners must enter. For more information, see [BDLAwardContactOptions](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLAwardContactOptions).

<span id="BDLLivePullViewController"></span>
# BDLLivePullViewController

```objectivec
@interface BDLLivePullViewController : UIViewController
```


The full\-featured live room controller.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLLivePullViewControllerDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-delegate) |
|id<BDLLivePullViewControllerActionProvider\> |[actionProvider](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-actionprovider) |
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-isportrait) |
|BOOL |[isFloating](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-isfloating) |
|BDLLivePullViewControllerConfig\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-config) |
|UIInterfaceOrientation |[floatingPlayerOrientation](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-floatingplayerorientation) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithActivityId:isPortrait:liveEngine:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-initwithactivityid-isportrait-liveengine) |
|instancetype |[initWithActivityId:isPortrait:liveEngine:basePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-initwithactivityid-isportrait-liveengine-baseplayerview) |
|void |[addBasePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-addbaseplayerview) |
|void |[close:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-close) |
|BOOL |[showFloatingPlayerIfAvailable:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-showfloatingplayerifavailable) |
|void |[hideFloatingPlayerIfAvailable:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-hidefloatingplayerifavailable) |


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewController-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLLivePullViewControllerDelegate> delegate;
```


The delegate method. For more information, see [BDLLivePullViewControllerDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLLivePullViewControllerDelegate).

<span id="BDLLivePullViewController-actionprovider"></span>
### actionProvider

```objectivec
@property (nonatomic, weak) id<BDLLivePullViewControllerActionProvider> actionProvider;
```


The event provider, which is used to respond to certain events outside of the SDK. For more information, see [BDLLivePullViewControllerActionProvider](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLLivePullViewControllerActionProvider).

<span id="BDLLivePullViewController-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode, which is passed in through the initialization method [initWithActivityId:isPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-initwithactivityid-isportrait-liveengine) or [initWithActivityId:isPortrait:basePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController-initwithactivityid-isportrait-liveengine-baseplayerview).


* `YES`: Portrait mode.

* `NO`: Landscape mode.

    &nbsp;


<span id="isfloating"></span>
### isFloating

```objectivec
@property (nonatomic, assign, readonly) BOOL isFloating;
```


Whether playing the video in the floating player.


* `YES`: In the floating player.

* `NO`: Not in the floating player.

    &nbsp;


<span id="config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLLivePullViewControllerConfig *config;
```


The configuration of the full\-featured live room. For more information, see [BDLLivePullViewControllerConfig](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLivePullViewControllerConfig).

<span id="BDLLivePullViewController-floatingplayerorientation"></span>
### floatingPlayerOrientation

```objectivec
@property (nonatomic, assign) UIInterfaceOrientation floatingPlayerOrientation;
```


The orientation of the floating player.

<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewController-initwithactivityid-isportrait-liveengine"></span>
### initWithActivityId:isPortrait:liveEngine:

```objectivec
- (instancetype)initWithActivityId:(NSNumber *)activityId isPortrait:(BOOL)isPortrait liveEngine:(BDLLiveEngine *)liveEngine;
```


Initializes the instance of the full\-featured live room controller.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activityId |NSNumber\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi). |
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|liveEngine |BDLLiveEngine\* |The entry class for the Viewer SDK. For more information, see [BDLLiveEngine](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine). |


**Return Value**

The instance of the full\-featured live room controller.

<span id="BDLLivePullViewController-initwithactivityid-isportrait-liveengine-baseplayerview"></span>
### initWithActivityId:isPortrait:liveEngine:basePlayerView:

```objectivec
- (instancetype)initWithActivityId:(NSNumber *)activityId
                        isPortrait:(BOOL)isPortrait
                        liveEngine:(BDLLiveEngine *)liveEngine
                    basePlayerView:(nullable BDLBasePlayerView *)basePlayerView;
```


Initializes the instance of the full\-featured live room controller.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activityId |NSNumber\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi). |
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|liveEngine |BDLLiveEngine\* |The entry class for the Viewer SDK. For more information, see [BDLLiveEngine](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine). |
|basePlayerView |nullable BDLBasePlayerView\* |The custom player that has already started playing. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView). |


**Return Value**

The instance of the full\-featured live room controller.

<span id="BDLLivePullViewController-addbaseplayerview"></span>
### addBasePlayerView:

```objectivec
- (void)addBasePlayerView:(BDLBasePlayerView *)basePlayerView;
```


Passes `basePlayerView` to `BDLLivePullViewController`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player that has already started playing. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView). |


<span id="BDLLivePullViewController-close"></span>
### close:

```objectivec
- (void)close:(BOOL)showFloatingPlayerIfAvailable;
```


Closes the full\-featured live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|showFloatingPlayerIfAvailable |BOOL |Whether to display the floating player when it can be displayed.<br><br><br>* `YES`: Display.<br><br>* `NO`: Do not display. |


<span id="BDLLivePullViewController-showfloatingplayerifavailable"></span>
### showFloatingPlayerIfAvailable:

```objectivec
- (BOOL)showFloatingPlayerIfAvailable:(BOOL)close;
```


Displays the floating player when it can be displayed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|close |BOOL |Whether to close the full\-featured live room.<br><br><br>* `YES`: Close. However, do not close the full\-featured live room if the floating player fails to display.<br><br>* `NO`: Do not close. |


**Return Value**

Whether the floating player is displayed successfully.


* `YES`: Successful.

* `NO`: Failed.

    &nbsp;


<span id="hidefloatingplayerifavailable"></span>
### hideFloatingPlayerIfAvailable:

```objectivec
- (void)hideFloatingPlayerIfAvailable:(BOOL)show;
```


Hides the floating player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|show |BOOL |Whether to display the full\-featured live room.<br><br><br>* `YES`: Close the floating player and display the full\-featured live room.<br><br>* `NO`: Close the floating player and do not display the full\-featured live room. |


<span id="BDLLivePullViewController(BDLDefaultAction)"></span>
# BDLLivePullViewController(BDLDefaultAction)

```objectivec
@interface BDLLivePullViewController (BDLDefaultAction)
```


The default implementation of full\-featured live room events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[defaultCloseAction](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultcloseaction) |
|void |[defaultFloatingPlayerTapAction](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayertapaction) |
|void |[defaultFloatingPlayerCloseAction](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayercloseaction) |
|CGRect |[defaultFloatingPlayerFrame](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayerframe) |
|void |[defaultOpenURLAction:enableFloating:](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultopenurlaction-enablefloating) |


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewController(BDLDefaultAction)-defaultcloseaction"></span>
### defaultCloseAction

```objectivec
- (void)defaultCloseAction;
```


The default implementation of the full\-featured live room close event, which is exiting the full\-featured live room. If a live or Video\-on\-Demand (VOD) video is playing and the floating player (in\-app picture\-in\-picture (PiP)) is enabled, the floating player is displayed while exiting the full\-featured live room.

<span id="BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayertapaction"></span>
### defaultFloatingPlayerTapAction

```objectivec
- (void)defaultFloatingPlayerTapAction;
```


The default implementation of the floating player tap event, which is closing the floating player and returning to the full\-featured live room.

<span id="BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayercloseaction"></span>
### defaultFloatingPlayerCloseAction

```objectivec
- (void)defaultFloatingPlayerCloseAction;
```


The default implementation of the floating player close event, which is closing the floating player.

<span id="BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayerframe"></span>
### defaultFloatingPlayerFrame

```objectivec
- (CGRect)defaultFloatingPlayerFrame;
```


Gets the default position of the floating player.

**Return Value**

The default position of the floating player.

<span id="BDLLivePullViewController(BDLDefaultAction)-defaultopenurlaction-enablefloating"></span>
### defaultOpenURLAction:enableFloating:

```objectivec
- (void)defaultOpenURLAction:(NSString *)urlStr enableFloating:(BOOL)enableFloating;
```


The default implementation of the tap event for product cards and ads (header ads, in\-page ads, and floating ads) with configured URLs, which is loading the configured URL.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|urlStr |NSString\* |The URL to load. |
|enableFloating |BOOL |Whether to display content on a floating page in the live room.<br><br><br>* `YES`: Display content on a floating page, which means opening a WebView window on the full\-featured live room page to display the content from the URL.<br><br>* `NO`: Display content on a new page, which means using the app's DeepLink mechanism to find an appropriate page to display the content from the URL. |


<span id="BDLPopupBottomShowBaseView"></span>
# BDLPopupBottomShowBaseView

```objectivec
@interface BDLPopupBottomShowBaseView : BDLPopupBaseView <BDLPopupBottomShowViewProtocol>
```


The base view of the bottom dialog box view.

<span id="BDLShareView"></span>
# BDLShareView

```objectivec
@interface BDLShareView : BDLPopupBottomShowBaseView <BDLBasicService>
```


The sharing dialog box view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[url](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-url) |
|BDLGetShareInfoResult\* |[shareInfo](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-shareinfo) |
|BDLGetInviteTokenResult\* |[inviteTokenModel](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-invitetokenmodel) |
|UIButton\* |[saveButton](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-savebutton) |
|UIButton\* |[inviteButton](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-invitebutton) |
|UIButton\* |[linkButton](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-linkbutton) |
|UIButton\* |[qrCodeButton](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-qrcodebutton) |
|UIButton\* |[cancelButton](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-cancelbutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithShareInfo:url:inviteTokenModel:](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-initwithshareinfo-url-invitetokenmodel) |
|void |[onInviteButtonClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-oninvitebuttonclickblock) |
|void |[onCopyLinkButtonClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-oncopylinkbuttonclickblock) |
|void |[onQRCodeButtonClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-onqrcodebuttonclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLShareView-url"></span>
### url

```objectivec
@property (nonatomic, strong, readonly, nullable) NSString *url;
```


The shared URL, which is passed in through the initialization method [initWithShareInfo:url:inviteTokenModel:](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-initwithshareinfo-url-invitetokenmodel).

<span id="BDLShareView-shareinfo"></span>
### shareInfo

```objectivec
@property (nonatomic, strong, readonly) BDLGetShareInfoResult *shareInfo;
```


The sharing information, which is passed in through the initialization method [initWithShareInfo:url:inviteTokenModel:](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-initwithshareinfo-url-invitetokenmodel).

<span id="BDLShareView-invitetokenmodel"></span>
### inviteTokenModel

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLGetInviteTokenResult *inviteTokenModel;
```


The sharer information, which is passed in through the initialization method [initWithShareInfo:url:inviteTokenModel:](https://docs.byteplus.com/en/docs/11/5590#BDLShareView-initwithshareinfo-url-invitetokenmodel).

<span id="BDLShareView-savebutton"></span>
### saveButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *saveButton;
```


The save button. The `text` in the `Normal` status cannot be customized.

<span id="BDLShareView-invitebutton"></span>
### inviteButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *inviteButton;
```


The poster button. The `text` in the `Normal` status cannot be customized.

<span id="BDLShareView-linkbutton"></span>
### linkButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *linkButton;
```


The copy link button. The `text` in the `Normal` status cannot be customized.

<span id="BDLShareView-qrcodebutton"></span>
### qrCodeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *qrCodeButton;
```


The QR code button. The `text` in the `Normal` status cannot be customized.

<span id="BDLShareView-cancelbutton"></span>
### cancelButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *cancelButton;
```


The cancel button. The `text` in the `Normal` status cannot be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLShareView-initwithshareinfo-url-invitetokenmodel"></span>
### initWithShareInfo:url:inviteTokenModel:

```objectivec
- (instancetype)initWithShareInfo:(BDLGetShareInfoResult *)shareInfo url:(NSString *)url inviteTokenModel:(BDLGetInviteTokenResult *)inviteTokenModel;
```


Initializes the instance of the sharing dialog box view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|shareInfo |BDLGetShareInfoResult\* |The sharing information. For more information, see [BDLGetShareInfoResult](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLGetShareInfoResult). |
|url |NSString\* |The shared URL. If `shareInfo.customAddress` is `nil`, share this URL. |
|inviteTokenModel |BDLGetInviteTokenResult\* |The sharer information. For more information, see [BDLGetInviteTokenResult](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLGetInviteTokenResult).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value is <code>nil</code> if the viewer does not log in to the live room.</div><br> |


**Return Value**

The instance of the sharing dialog box view.

<span id="BDLShareView-oninvitebuttonclickblock"></span>
### onInviteButtonClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onInviteButtonClickBlock)(BDLShareView *view);
```


The callback is triggered when the poster button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLShareView\* |The sharing dialog box view. |


<span id="BDLShareView-oncopylinkbuttonclickblock"></span>
### onCopyLinkButtonClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onCopyLinkButtonClickBlock)(BDLShareView *view);
```


The callback is triggered when the copy link button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLShareView\* |The sharing dialog box view. |


<span id="BDLShareView-onqrcodebuttonclickblock"></span>
### onQRCodeButtonClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onQRCodeButtonClickBlock)(BDLShareView *view);
```


The callback is triggered when the QR code button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLShareView\* |The sharing dialog box view. |


<span id="BDLActivity"></span>
# BDLActivity

```objectivec
@interface BDLActivity : BDLBaseModel
```


The information required to join the live room.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[activityId](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-activityid) |
|NSString\* |[token](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-token) |
|BDLActivityAuthMode |[authMode](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-authmode) |
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-isportrait) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[isValid](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-isvalid) |


<span id="instructions"></span>
## Instructions

<span id="BDLActivity-activityid"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


The activity ID of the live room.

<span id="BDLActivity-token"></span>
### token

```objectivec
@property (nonatomic, copy) NSString *token;
```


The authorization token required to join the live room.

<span id="BDLActivity-authmode"></span>
### authMode

```objectivec
@property (nonatomic, assign) BDLActivityAuthMode authMode;
```


The authentication mode of the live room. For more information, see [BDLActivityAuthMode](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLActivityAuthMode).

<span id="BDLActivity-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.


<span id="instructions"></span>
## Instructions

<span id="BDLActivity-isvalid"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


Verifies whether the live room information is valid.

**Return Value**


* `YES`: Valid. Neither [activityId](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-activityid) nor [token](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-token) is 'nil'.

* `NO`: Invalid. Either [activityId](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-activityid) or [token](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-token) is 'nil', or both are 'nil'.

    &nbsp;


<span id="bdlawarddetailsview"></span>
# BDLAwardDetailsView

```objectivec
@interface BDLAwardDetailsView : BDLPopupBottomShowBaseView <BDLLanguageService, BDLInteractiveToolService>
```


The lucky draw details view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLInteractiveAwardModel\* |[model](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-model) |
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-closebutton) |
|UIImageView\* |[headerImageView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-headerimageview) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-titlelabel) |
|BDLAwardCountdownView\* |[countdownView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-countdownview) |
|UILabel\* |[awardLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-awardlabel) |
|UILabel\* |[awardCountLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-awardcountlabel) |
|BDLAwardConditionView\* |[conditionView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-conditionview) |
|UIButton\* |[participateButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-participatebutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithModel:](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-initwithmodel) |
|void |[closeButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-closebuttonclickedblock) |
|void |[participateButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-participatebuttonclickedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardDetailsView-model"></span>
### model

```objectivec
@property (nonatomic, strong, readonly) BDLInteractiveAwardModel *model;
```


The lucky draw information, which is passed in through the initialization method [initWithModel:](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView-initwithmodel).

<span id="BDLAwardDetailsView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *closeButton;
```


The close button. All properties can be customized.

<span id="BDLAwardDetailsView-headerimageview"></span>
### headerImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *headerImageView;
```


The top imageView. All properties can be customized.

<span id="BDLAwardDetailsView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The about to draw label. All properties except `text` can be customized.

<span id="BDLAwardDetailsView-countdownview"></span>
### countdownView

```objectivec
@property (nonatomic, strong, readonly) BDLAwardCountdownView *countdownView;
```


The countdown view. For more information, see [BDLAwardCountdownView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCountdownView).

<span id="BDLAwardDetailsView-awardlabel"></span>
### awardLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *awardLabel;
```


The prize information label. All properties except `text` can be customized.

<span id="BDLAwardDetailsView-awardcountlabel"></span>
### awardCountLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *awardCountLabel;
```


The label for the number of prizes. All properties except `text` can be customized.

<span id="BDLAwardDetailsView-conditionview"></span>
### conditionView

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLAwardConditionView *conditionView;
```


The participation condition view. For more information, see [BDLAwardConditionView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardConditionView).

<span id="BDLAwardDetailsView-participatebutton"></span>
### participateButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *participateButton;
```


The participate button.

<span id="instructions"></span>
## Instructions

<span id="BDLAwardDetailsView-initwithmodel"></span>
### initWithModel:

```objectivec
- (instancetype)initWithModel:(BDLInteractiveAwardModel *)model;
```


Initializes the instance of the lucky draw details view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|model |BDLInteractiveAwardModel\* |The lucky draw information. For more information, see [BDLInteractiveAwardModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveAwardModel). |


**Return Value**

The instance of the lucky draw details view.

<span id="BDLAwardDetailsView-closebuttonclickedblock"></span>
### closeButtonClickedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^closeButtonClickedBlock)(BDLAwardDetailsView *view);
```


The callback is triggered when the close button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardDetailsView\* |The lucky draw details view. |


<span id="BDLAwardDetailsView-participatebuttonclickedblock"></span>
### participateButtonClickedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^participateButtonClickedBlock)(BDLAwardDetailsView *view);
```


The callback is triggered when the participate button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardDetailsView\* |The lucky draw details view. |


<span id="BDLLoadingView"></span>
# BDLLoadingView

```objectivec
@interface BDLLoadingView : UIView
```


The loading view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImageView\* |[imageView](https://docs.byteplus.com/en/docs/11/5590#BDLLoadingView-imageview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[showAnimation](https://docs.byteplus.com/en/docs/11/5590#BDLLoadingView-showanimation) |
|void |[hideAnimation](https://docs.byteplus.com/en/docs/11/5590#BDLLoadingView-hideanimation) |


<span id="instructions"></span>
## Instructions

<span id="BDLLoadingView-imageview"></span>
### imageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *imageView;
```


The imageView of the loading image.

<span id="instructions"></span>
## Instructions

<span id="BDLLoadingView-showanimation"></span>
### showAnimation

```objectivec
- (void)showAnimation;
```


Starts the animation.

<span id="BDLLoadingView-hideanimation"></span>
### hideAnimation

```objectivec
- (void)hideAnimation;
```


Ends the animation.

<span id="BDLLiveDescriptionView"></span>
# BDLLiveDescriptionView

```objectivec
@interface BDLLiveDescriptionView : BDLBaseView <
BDLBasicService
, BDLLanguageService
>
```


The live room description view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLScrollTextView\* |[scrollTextView](https://docs.byteplus.com/en/docs/11/5590#BDLLiveDescriptionView-scrolltextview) |
|UIButton\* |[arrowButton](https://docs.byteplus.com/en/docs/11/5590#BDLLiveDescriptionView-arrowbutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[arrowButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLLiveDescriptionView-arrowbuttonclickedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLLiveDescriptionView-scrolltextview"></span>
### scrollTextView

```objectivec
@property (nonatomic, strong, readonly) BDLScrollTextView *scrollTextView;
```


The view of the live room description text. For more information, see [BDLScrollTextView](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView).

<span id="BDLLiveDescriptionView-arrowbutton"></span>
### arrowButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *arrowButton;
```


The arrow icon.

<span id="instructions"></span>
## Instructions

<span id="BDLLiveDescriptionView-arrowbuttonclickedblock"></span>
### arrowButtonClickedBlock

```objectivec
@property (nonatomic, copy) void (^arrowButtonClickedBlock)(BDLLiveDescriptionView *view);
```


The callback is triggered when the arrow icon is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLLiveDescriptionView\* |The live room description view. |


<span id="BDLCommentBaseView"></span>
# BDLCommentBaseView

```objectivec
@interface BDLCommentBaseView : BDLBaseView
<
UITableViewDelegate,
UITableViewDataSource,
BDLLanguageService,
BDLBasicService,
BDLCommentConfigService
>
```


The common base class for comments and top comments.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-isportrait) |
|BDLCommentBaseConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-config) |
|BOOL |[isCommentTranslateEnable](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-iscommenttranslateenable) |
|NSArray\* |[langTypes](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-langtypes) |
|BDLLanguageType |[langType](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-langtype) |
|BDLNoCommentView\* |[noCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-nocommentview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-initwithportrait) |
|void |[refreshNoCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView-refreshnocommentview) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentBaseView-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.

    &nbsp;


<span id="config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLCommentBaseConfiguration *config;
```


The base class configuration. For more information, see [BDLCommentBaseConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration).

<span id="BDLCommentBaseView-iscommenttranslateenable"></span>
### isCommentTranslateEnable

```objectivec
@property (nonatomic, assign, readonly) BOOL isCommentTranslateEnable;
```


Whether to enable the comment translation.


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="langtypes"></span>
### langTypes

```objectivec
@property (nonatomic, copy, readonly) NSArray *langTypes;
```


All the currently supported language types.

<span id="BDLCommentBaseView-langtype"></span>
### langType

```objectivec
@property (nonatomic, assign, readonly) BDLLanguageType langType;
```


The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType).

<span id="BDLCommentBaseView-nocommentview"></span>
### noCommentView

```objectivec
@property (nonatomic, strong) BDLNoCommentView *noCommentView;
```


The view when there are no comments in the comment area. For more information, see [BDLNoCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLNoCommentView). All properties except `frame` and `hidden` can be customized .

<span id="instructions"></span>
## Instructions

<span id="BDLCommentBaseView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the base class for comments and top comments.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the base class for comments and top comments.

<span id="BDLCommentBaseView-refreshnocommentview"></span>
### refreshNoCommentView

```objectivec
- (void)refreshNoCommentView;
```


Updates the placeholder image for the comment area without comments.

<span id="BDLAwardResultView"></span>
# BDLAwardResultView

```objectivec
@interface BDLAwardResultView : BDLPopupCenterShowBaseView <BDLLanguageService>
```


The lucky draw result view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLInteractiveAwardModel\* |[awardModel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-awardmodel) |
|BDLAwardUserModel\* |[userModel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-usermodel) |
|UIImageView\* |[imageView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-imageview) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-titlelabel) |
|UIButton\* |[completeInfoButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-completeinfobutton) |
|UIButton\* |[awardWinnersButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-awardwinnersbutton) |
|UILabel\* |[termsLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-termslabel) |
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-closebutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithAwardModel:userModel:](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-initwithawardmodel-usermodel) |
|void |[closeButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-closebuttonclickedblock) |
|void |[completeInfoButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-completeinfobuttonclickedblock) |
|void |[awardWinnersButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-awardwinnersbuttonclickedblock) |
|BOOL |[shouldShowAwardContactEntrance](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-shouldshowawardcontactentrance) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardResultView-awardmodel"></span>
### awardModel

```objectivec
@property (nonatomic, strong, readonly) BDLInteractiveAwardModel *awardModel;
```


The lucky draw information, which is passed in through the initialization method [initWithAwardModel:userModel:](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-initwithawardmodel-usermodel).

<span id="BDLAwardResultView-usermodel"></span>
### userModel

```objectivec
@property (nonatomic, strong, readonly) BDLAwardUserModel *userModel;
```


The model of lucky draw\-related viewer information, which is passed in through the initialization method [initWithAwardModel:userModel:](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-initwithawardmodel-usermodel).

<span id="BDLAwardResultView-imageview"></span>
### imageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *imageView;
```


imageView. All properties except `image` can be customized.

<span id="BDLAwardResultView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The text label of "Congratulations, you won the prize" or "Sorry, you did not win". All properties except `text` can be customized.

<span id="BDLAwardResultView-completeinfobutton"></span>
### completeInfoButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *completeInfoButton;
```


The update personal information button or got it button. The `text` in the `Normal` status cannot be customized.

<span id="BDLAwardResultView-awardwinnersbutton"></span>
### awardWinnersButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *awardWinnersButton;
```


The view results button. The `text` in the `Normal` status cannot be customized.

<span id="BDLAwardResultView-termslabel"></span>
### termsLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *termsLabel;
```


The prize terms label. All properties except `text` can be customized.

<span id="BDLAwardResultView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *closeButton;
```


The close button. Customization is supported.

<span id="instructions"></span>
## Instructions

<span id="BDLAwardResultView-initwithawardmodel-usermodel"></span>
### initWithAwardModel:userModel:

```objectivec
- (instancetype)initWithAwardModel:(BDLInteractiveAwardModel *)awardModel userModel:(BDLAwardUserModel *)userModel;
```


Initializes the instance of the lucky draw result view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|awardModel |BDLInteractiveAwardModel\* |The lucky draw information. For more information, see [BDLInteractiveAwardModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveAwardModel). |
|userModel |BDLAwardUserModel\* |The model of lucky draw\-related viewer information. For more information, see [BDLAwardUserModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLAwardUserModel). |


**Return Value**

The instance of the lucky draw result view.

<span id="BDLAwardResultView-closebuttonclickedblock"></span>
### closeButtonClickedBlock

```objectivec
@property (nonatomic, copy) void (^closeButtonClickedBlock)(BDLAwardResultView *view);
```


The callback is triggered when the close button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardResultView\* |The lucky draw result view. |


<span id="BDLAwardResultView-completeinfobuttonclickedblock"></span>
### completeInfoButtonClickedBlock

```objectivec
@property (nonatomic, copy) void (^completeInfoButtonClickedBlock)(BDLAwardResultView *view);
```


The callback is triggered when the update personal information button is tapped by winners or the got it button is tapped by viewers without winning prizes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView-shouldshowawardcontactentrance">shouldShowAwardContactEntrance</a> to determine if the button is for updating personal information.</div>


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardResultView\* |The lucky draw result view. |


<span id="BDLAwardResultView-awardwinnersbuttonclickedblock"></span>
### awardWinnersButtonClickedBlock

```objectivec
@property (nonatomic, copy) void (^awardWinnersButtonClickedBlock)(BDLAwardResultView *view);
```


The callback is triggered when the view results button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLAwardResultView\* |The lucky draw result view. |


<span id="BDLAwardResultView-shouldshowawardcontactentrance"></span>
### shouldShowAwardContactEntrance

```objectivec
- (BOOL)shouldShowAwardContactEntrance;
```


Whether to display the entry for updating personal information.

**Return Value**


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="bdlquestionnaireupdatebodymodel"></span>
# BDLQuestionnaireUpdateBodyModel

```objectivec
@interface BDLQuestionnaireUpdateBodyModel : BDLBaseModel
```


The questionnaire model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[activityId](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUpdateBodyModel-activityid) |
|BDLQuestionnaireUserInfoModel\* |[userInfo](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUpdateBodyModel-userinfo) |
|BDLQuestionnaireAnswersModel\* |[questionnaireAnswer](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUpdateBodyModel-questionnaireanswer) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireUpdateBodyModel-activityid"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


The activity ID of the live room.

<span id="BDLQuestionnaireUpdateBodyModel-userinfo"></span>
### userInfo

```objectivec
@property (nonatomic, strong) BDLQuestionnaireUserInfoModel *userInfo;
```


The viewer information. For more information, see [BDLQuestionnaireUserInfoModel](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUserInfoModel).

<span id="BDLQuestionnaireUpdateBodyModel-questionnaireanswer"></span>
### questionnaireAnswer

```objectivec
@property (nonatomic, strong) BDLQuestionnaireAnswersModel *questionnaireAnswer;
```


The questionnaire content filled out by the viewer. For more information, see [BDLQuestionnaireAnswersModel](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireAnswersModel).

<span id="BDLTopCommentView"></span>
# BDLTopCommentView

```objectivec
@interface BDLTopCommentView : UIView
```


The pinned comment view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLTopCommentViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLTopCommentView-delegate) |
|BDLCommentModel\* |[comment](https://docs.byteplus.com/en/docs/11/5590#BDLTopCommentView-comment) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateViewWithComment:config:isPortrait:isCommentTranslateEnable:langType:langTypes:](https://docs.byteplus.com/en/docs/11/5590#BDLTopCommentView-updateviewwithcomment-config-isportrait-iscommenttranslateenable-langtype-langtypes) |


<span id="instructions"></span>
## Instructions

<span id="BDLTopCommentView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLTopCommentViewDelegate> delegate;
```


The delegate method. For more information, see [BDLTopCommentViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLTopCommentViewDelegate).

<span id="BDLTopCommentView-comment"></span>
### comment

```objectivec
@property (nonatomic, weak, readonly) BDLCommentModel *comment;
```


The comment corresponding to the current view. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel).

<span id="instructions"></span>
## Instructions

<span id="BDLTopCommentView-updateviewwithcomment-config-isportrait-iscommenttranslateenable-langtype-langtypes"></span>
### updateViewWithComment:config:isPortrait:isCommentTranslateEnable:langType:langTypes:

```objectivec
- (void)updateViewWithComment:(BDLCommentModel *)comment
                       config:(BDLCommentViewConfiguration *)config
                   isPortrait:(BOOL)isPortrait
     isCommentTranslateEnable:(BOOL)isCommentTranslateEnable
                     langType:(BDLLanguageType)langType
                    langTypes:(NSArray *)langTypes;
```


Updates the view based on the comment.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|comment |BDLCommentModel\* |The comment to display. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |
|config |BDLCommentViewConfiguration\* |The comment configuration. For more information, see [BDLCommentViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration). |
|isPortrait |BOOL |Whether the live room is in portrait mode.<br><br><br>&nbsp;<br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|isCommentTranslateEnable |BOOL |Whether to enable the comment translation.<br><br><br>* `YES`: Enable.<br><br>* `NO`: Disable. |
|langType |BDLLanguageType |The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType). |
|langTypes |NSArray\* |All the currently supported language types. |


<span id="BDLInteractiveToolContentView"></span>
# BDLInteractiveToolContentView

```objectivec
@interface BDLInteractiveToolContentView : BDLBaseView <BDLMenuService>
```


The interaction tool content view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-isportrait) |
|UILabel\* |[totalLabel](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-totallabel) |
|UITableView\* |[tableView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-tableview) |
|BDLLanguageType |[langType](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-langtype) |
|NSArray<NSNumber\*\>\* |[langTypes](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-langtypes) |
|BOOL |[isDarkTheme](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-isdarktheme) |
|NSArray<BDLInteractiveToolModel\*\>\* |[interactiveTools](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-interactivetools) |
|id<BDLInteractiveToolContentViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-delegate) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-updatewithconfig) |
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolContentView-initwithportrait) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolContentView-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.

    &nbsp;


<span id="totallabel"></span>
### totalLabel

```objectivec
@property (nonatomic, strong) UILabel *totalLabel;
```


The label for the total number of interaction tools sent in the live room.

<span id="BDLInteractiveToolContentView-tableview"></span>
### tableView

```objectivec
@property (nonatomic, strong) UITableView *tableView;
```


The container tableView of the content.

<span id="BDLInteractiveToolContentView-langtype"></span>
### langType

```objectivec
@property (nonatomic, assign) BDLLanguageType langType;
```


The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType).

<span id="BDLInteractiveToolContentView-langtypes"></span>
### langTypes

```objectivec
@property (nonatomic, copy) NSArray<NSNumber *> *langTypes;
```


All the currently supported language types.

<span id="BDLInteractiveToolContentView-isdarktheme"></span>
### isDarkTheme

```objectivec
@property (nonatomic, assign) BOOL isDarkTheme;
```


Whether the theme is dark mode.


* `YES`: Dark mode.

* `NO`: Not dark mode.

    &nbsp;


<span id="interactivetools"></span>
### interactiveTools

```objectivec
@property (nonatomic, copy) NSArray<BDLInteractiveToolModel *> *interactiveTools;
```


The data corresponding to the current interaction tool content view. For more information, see [BDLInteractiveToolModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveToolModel).

<span id="BDLInteractiveToolContentView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLInteractiveToolContentViewDelegate> delegate;
```


The delegate method. For more information, see [BDLInteractiveToolContentViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLInteractiveToolContentViewDelegate).

<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolContentView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLInteractiveToolConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLInteractiveToolConfiguration\* |The configuration. For more information, see [BDLInteractiveToolConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveToolConfiguration). |


<span id="BDLInteractiveToolContentView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the interaction tool content view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the interaction tool content view.

<span id="BDLPlayerControlView"></span>
# BDLPlayerControlView

```objectivec
@interface BDLPlayerControlView : BDLBaseView <BDLBasicService, BDLLanguageService, BDLPullStreamUrlService>
```


The player control view, including the play button, pause button, progress bar, refresh button, full\-screen button, and time text.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLPlayerControlViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-delegate) |
|UIView\* |[controlBarView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-controlbarview) |
|UIButton\* |[playButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-playbutton) |
|UIButton\* |[centerPlayButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-centerplaybutton) |
|UIButton\* |[refreshButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-refreshbutton) |
|UIButton\* |[fullScreenButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-fullscreenbutton) |
|UIButton\* |[backButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-backbutton) |
|BOOL |[needFullScreenButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-needfullscreenbutton) |
|UILabel\* |[currentTimeLabel](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-currenttimelabel) |
|UILabel\* |[durationLabel](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-durationlabel) |
|NSTimeInterval |[duration](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-duration) |
|NSTimeInterval |[currentTime](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-currenttime) |
|BDLPlayerSliderView\* |[sliderView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-sliderview) |
|BOOL |[sliding](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-sliding) |
|UIButton\* |[speedButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-speedbutton) |
|BDLPlayerSpeed |[speed](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-speed) |
|UIButton\* |[resolutionButton](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-resolutionbutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:config:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-initwithportrait-config) |
|void |[play](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-play) |
|void |[pause](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-pause) |
|void |[updatePlayButton:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-updateplaybutton) |
|void |[setProgress:animated:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-setprogress-animated) |
|void |[setCacheProgress:animated:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-setcacheprogress-animated) |
|BOOL |[showIfNeeded](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-showifneeded) |
|void |[hide](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-hide) |
|BOOL |[isPlaying](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-isplaying) |
|BOOL |[startFloating](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-startfloating) |
|void |[stopFloating](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-stopfloating) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-updatewithconfig) |
|void |[updateResolutionButtonWithResolutions:currentResolution:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-updateresolutionbuttonwithresolutions-currentresolution) |
|void |[changeResolutionSuccess:completeResolution:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-changeresolutionsuccess-completeresolution) |
|void |[onFullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView-onfullscreen) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerControlView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLPlayerControlViewDelegate> delegate;
```


The delegate method. For more information, see [BDLPlayerControlViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLPlayerControlViewDelegate).

<span id="BDLPlayerControlView-controlbarview"></span>
### controlBarView

```objectivec
@property (nonatomic, strong) UIView *controlBarView;
```


The parent control of feature elements such as play button, pause button, progress bar, refresh button, full\-screen button, and time text.

<span id="BDLPlayerControlView-playbutton"></span>
### playButton

```objectivec
@property (nonatomic, strong) UIButton *playButton;
```


The play or pause button.


* `selected` being `YES` indicates the video is playing, with the pause button displayed.

* `selected` being `NO` indicates the video is not playing, with the play button displayed.

    &nbsp;


<span id="centerplaybutton"></span>
### centerPlayButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *centerPlayButton;
```


The play button in the middle of the player, which is displayed only when the video is paused.

<span id="BDLPlayerControlView-refreshbutton"></span>
### refreshButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *refreshButton;
```


The refresh button, which is displayed only during a live stream.

<span id="BDLPlayerControlView-fullscreenbutton"></span>
### fullScreenButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *fullScreenButton;
```


The full\-screen button, which is displayed only in the live room in landscape mode and when the width of the video is greater than the height in the live room in portrait mode. You can customize the image by using [fullScreenButtonNormalImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-fullscreenbuttonnormalimage) and [fullScreenButtonSelectedImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-fullscreenbuttonselectedimage).

<span id="BDLPlayerControlView-backbutton"></span>
### backButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *backButton;
```


The exit ful\- screen button, which is displayed only in the live room in landscape mode and when the width of the video is greater than the height in the live room in portrait mode. You can customize the image by using [exitFullScreenButtonNormalImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-exitfullscreenbuttonnormalimage).

<span id="BDLPlayerControlView-needfullscreenbutton"></span>
### needFullScreenButton

```objectivec
@property (nonatomic, assign) BOOL needFullScreenButton;
```


Whether the full\-screen button is needed. Default value: `YES`.


* `YES`: Needed.

* `NO`: Not needed.

    &nbsp;


<span id="currenttimelabel"></span>
### currentTimeLabel

```objectivec
@property (nonatomic, strong) UILabel *currentTimeLabel;
```


The current playback time label, which is displayed only when the VOD video is playing. You can customize the color by using [currentTimeColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-currenttimecolor).

<span id="BDLPlayerControlView-durationlabel"></span>
### durationLabel

```objectivec
@property (nonatomic, strong) UILabel *durationLabel;
```


The total duration label, which is displayed only when the VOD video is playing. You can customize the color by using [totalTimeColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-totaltimecolor).

<span id="BDLPlayerControlView-duration"></span>
### duration

```objectivec
@property (nonatomic, assign) NSTimeInterval duration;
```


The total duration. Unit: seconds. The value is `0` during a live stream.

<span id="BDLPlayerControlView-currenttime"></span>
### currentTime

```objectivec
@property (nonatomic, assign) NSTimeInterval currentTime;
```


The current duration. Unit: seconds. The value is `0` during a live stream.

<span id="BDLPlayerControlView-sliderview"></span>
### sliderView

```objectivec
@property (nonatomic, strong) BDLPlayerSliderView *sliderView;
```


The progress bar view, which is displayed only when the VOD video is playing. For more information, see [BDLPlayerSliderView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView).

<span id="BDLPlayerControlView-sliding"></span>
### sliding

```objectivec
@property (nonatomic, readonly, getter=isSliding) BOOL sliding;
```


Whether the progress bar is being dragged.


* `YES`: Being dragged.

* `NO`: Not being dragged.

    &nbsp;


<span id="speedbutton"></span>
### speedButton

```objectivec
@property (nonatomic, strong) UIButton *speedButton;
```


The playback speed button. All properties except `text` can be customized.

<span id="BDLPlayerControlView-speed"></span>
### speed

```objectivec
@property (nonatomic, assign) BDLPlayerSpeed speed;
```


The current playback speed. For more information, see [BDLPlayerSpeed](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerSpeed).

<span id="BDLPlayerControlView-resolutionbutton"></span>
### resolutionButton

```objectivec
@property (nonatomic, strong, nullable) UIButton *resolutionButton;
```


The resolution button.

<span id="instructions"></span>
## Instructions

<span id="BDLPlayerControlView-initwithportrait-config"></span>
### initWithPortrait:config:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait config:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the player control view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the player control view.

<span id="BDLPlayerControlView-play"></span>
### play

```objectivec
- (void)play;
```


Plays the video.

<span id="BDLPlayerControlView-pause"></span>
### pause

```objectivec
- (void)pause;
```


Pauses the video.

<span id="BDLPlayerControlView-updateplaybutton"></span>
### updatePlayButton:

```objectivec
- (void)updatePlayButton:(BOOL)isPlaying;
```


Synchronizes the play button's status according to the playback status.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPlaying |BOOL |Whether the video is playing.<br><br><br>&nbsp;<br><br>* `YES`: Playing. The pause button is displayed.<br><br>* `NO`: Not playing. The play button is displayed. |


<span id="BDLPlayerControlView-setprogress-animated"></span>
### setProgress:animated:

```objectivec
- (void)setProgress:(CGFloat)progress animated:(BOOL)animated;
```


Sets the current playback progress.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|progress |CGFloat |The current playback progress. Value range: [0,1]. |
|animated |BOOL |Whether animation is needed.<br><br><br>&nbsp;<br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLPlayerControlView-setcacheprogress-animated"></span>
### setCacheProgress:animated:

```objectivec
- (void)setCacheProgress:(CGFloat)progress animated:(BOOL)animated;
```


Sets the cache progress.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|progress |CGFloat |The cache progress. Value range: [0,1]. |
|animated |BOOL |Whether animation is needed.<br><br><br>&nbsp;<br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLPlayerControlView-showifneeded"></span>
### showIfNeeded

```objectivec
- (BOOL)showIfNeeded;
```


Displays the control view. The SDK internally determines whether the view can be displayed.

**Return Value**


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="hide"></span>
### hide

```objectivec
- (void)hide;
```


Hides the control view.

<span id="BDLPlayerControlView-isplaying"></span>
### isPlaying

```objectivec
- (BOOL)isPlaying;
```


Whether the video is playing.

**Return Value**


* `YES`: Playing.

* `NO`: Not playing.

    &nbsp;


<span id="startfloating"></span>
### startFloating

```objectivec
- (BOOL)startFloating;
```


Starts playing in the floating player (in\-app PiP). The SDK contains internal logic to control the visibility of certain controls while playing in the floating player.

**Return Value**

Whether the video has started playing in the floating player successfully.


* `YES`: Successful.

* `NO`: Failed.

    &nbsp;


<span id="stopfloating"></span>
### stopFloating

```objectivec
- (void)stopFloating;
```


Stops playing in the floating player (in\-app PiP).

<span id="BDLPlayerControlView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLPlayerControlView-updateresolutionbuttonwithresolutions-currentresolution"></span>
### updateResolutionButtonWithResolutions:currentResolution:

```objectivec
- (void)updateResolutionButtonWithResolutions:(NSArray<NSNumber *> *)resolutions currentResolution:(BDLVideoResolution)resolution;
```


Updates the resolution.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|resolutions |NSArray<NSNumber\*\>\* |All the supported resolutions. |
|resolution |BDLVideoResolution |The currently selected resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLPlayerControlView-changeresolutionsuccess-completeresolution"></span>
### changeResolutionSuccess:completeResolution:

```objectivec
- (void)changeResolutionSuccess:(BOOL)success completeResolution:(BDLVideoResolution)completeResolution;
```


Changes the resolution to synchronize the display of the resolution button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|success |BOOL |Whether the resolution is changed successfully.<br><br><br>&nbsp;<br><br>* `YES`: Successful.<br><br>* `NO`: Failed. |
|completeResolution |BDLVideoResolution |The final resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLPlayerControlView-onfullscreen"></span>
### onFullScreen

```objectivec
- (void)onFullScreen;
```


Enters or exits full\-screen mode.

<span id="BDLRiskWarningView"></span>
# BDLRiskWarningView

```objectivec
@interface BDLRiskWarningView : BDLPopupCenterShowBaseView
```


The reminder view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLLanguageType |[languageType](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-languagetype) |
|NSArray\* |[languageTypeArray](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-languagetypearray) |
|UIImageView\* |[topBackgroundImageView](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-topbackgroundimageview) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-titlelabel) |
|UILabel\* |[contentLabel](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-contentlabel) |
|UIView\* |[bottomMaskView](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-bottommaskview) |
|UIButton\* |[confirmButton](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-confirmbutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onConfirmButtonClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLRiskWarningView-onconfirmbuttonclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLRiskWarningView-languagetype"></span>
### languageType

```objectivec
@property (nonatomic, assign, readonly) BDLLanguageType languageType;
```


The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType).

<span id="BDLRiskWarningView-languagetypearray"></span>
### languageTypeArray

```objectivec
@property (nonatomic, copy, readonly) NSArray *languageTypeArray;
```


All the currently supported language types.

<span id="BDLRiskWarningView-topbackgroundimageview"></span>
### topBackgroundImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *topBackgroundImageView;
```


The top background image view. Customization is supported.

<span id="BDLRiskWarningView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The title label. All properties except `text` can be customized. You can customize the title on the BytePlus Live server.

<span id="BDLRiskWarningView-contentlabel"></span>
### contentLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *contentLabel;
```


The content label. All properties except `text` can be customized. You can customize the content on the BytePlus Live server.

<span id="BDLRiskWarningView-bottommaskview"></span>
### bottomMaskView

```objectivec
@property (nonatomic, strong, readonly) UIView *bottomMaskView;
```


The semi\-transparent view at the bottom of the content that appears when scrolling to the bottom. All properties except `hidden` can be customized.

<span id="BDLRiskWarningView-confirmbutton"></span>
### confirmButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *confirmButton;
```


The confirm button. All properties except `title` (button text) can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLRiskWarningView-onconfirmbuttonclickblock"></span>
### onConfirmButtonClickBlock

```objectivec
@property (nonatomic, copy) void(^onConfirmButtonClickBlock)(BDLRiskWarningView *view);
```


The callback is triggered when the confirm button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLRiskWarningView\* |The reminder view. |


<span id="BDLPlayerMaskView"></span>
# BDLPlayerMaskView

```objectivec
@interface BDLPlayerMaskView : BDLBaseView <BDLBasicService, BDLLanguageService>
```


The mask view, including the live room status (Preview or Over), watermark, and popularity view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UILabel\* |[promptLabel](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-promptlabel) |
|UIView\* |[promptContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-promptcontainerview) |
|UIImageView\* |[watermarkImageView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-watermarkimageview) |
|UILabel\* |[tagLabel](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-taglabel) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:config:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-initwithportrait-config) |
|BOOL |[startFloating](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-startfloating) |
|void |[stopFloating](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-stopfloating) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerMaskView-promptlabel"></span>
### promptLabel

```objectivec
@property (nonatomic, strong) UILabel *promptLabel;
```


The label of the toast indicating the preview or live stream has ended. All properties except `text` and `hidden` can be customized. You can customize the font and font size by using [toastFont](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-toastfont).

<span id="BDLPlayerMaskView-promptcontainerview"></span>
### promptContainerView

```objectivec
@property (nonatomic, strong) UIView *promptContainerView;
```


The container view of the toast indicating the preview or live stream has ended. All properties except `hidden` can be customized. You can customize the rounded corner by using [toastCornerRadius](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-toastcornerradius).

<span id="BDLPlayerMaskView-watermarkimageview"></span>
### watermarkImageView

```objectivec
@property (nonatomic, strong, nullable) UIImageView *watermarkImageView;
```


The watermark's imageView, which is displayed only in the live room in landscape mode. All properties except `image` can be customized.

<span id="BDLPlayerMaskView-taglabel"></span>
### tagLabel

```objectivec
@property (nonatomic, strong, nullable) UILabel *tagLabel;
```


The label of the Preview or Over status. All properties except `text` and `hidden` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLPlayerMaskView-initwithportrait-config"></span>
### initWithPortrait:config:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait config:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the mask view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the mask view.

<span id="BDLPlayerMaskView-startfloating"></span>
### startFloating

```objectivec
- (BOOL)startFloating;
```


Starts playing in the floating player (in\-app PiP). The SDK contains internal logic to control the visibility of certain controls while playing in the floating player.

**Return Value**

Whether the video has started playing in the floating player successfully.


* `YES`: Successful.

* `NO`: Failed.

    &nbsp;


<span id="stopfloating"></span>
### stopFloating

```objectivec
- (void)stopFloating;
```


Stops playing in the floating player (in\-app PiP).

<span id="BDLPlayerMaskView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLShoppingCardView"></span>
# BDLShoppingCardView

```objectivec
@interface BDLShoppingCardView : BDLBaseView
```


The product card view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView-isportrait) |
|UILabel\* |[totalCountLabel](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView-totalcountlabel) |
|UIScrollView\* |[titleScrollView](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView-titlescrollview) |
|UIScrollView\* |[contentScrollView](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView-contentscrollview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onCardSearchClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView-oncardsearchclickblock) |
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView-initwithportrait) |


<span id="instructions"></span>
## Instructions

<span id="BDLShoppingCardView-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.

    &nbsp;


<span id="totalcountlabel"></span>
### totalCountLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *totalCountLabel;
```


The text label of "x products in total". All properties except `text` and `frame` can be customized.

<span id="BDLShoppingCardView-titlescrollview"></span>
### titleScrollView

```objectivec
@property (nonatomic, strong, readonly) UIScrollView *titleScrollView;
```


The scrollable `scrollView` in the menu bar title area. All properties except `contentSize` can be customized.

<span id="BDLShoppingCardView-contentscrollview"></span>
### contentScrollView

```objectivec
@property (nonatomic, strong, readonly) UIScrollView *contentScrollView;
```


The scrollable `scrollView` in the content area under the menu bar title. All properties except `contentSize` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLShoppingCardView-oncardsearchclickblock"></span>
### onCardSearchClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onCardSearchClickBlock)(BDLShoppingCardView *shoppingCardView, NSArray <BDLMenuModel *> *menus);
```


The callback is triggered when the product card is searched.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|shoppingCardView |BDLShoppingCardView\* |The product card view. |
|menus |NSArray<BDLMenuModel\*\>\* |The model of menu bar information. For more information, see [BDLMenuModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLMenuModel). |


<span id="BDLShoppingCardView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the product card view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the product card view.

<span id="UIView(BDLDraggable)"></span>
# UIView(BDLDraggable)

```objectivec
@interface UIView (BDLDraggable) <UIGestureRecognizerDelegate>
```


The related classification of BytePlus Live for UIView dragging.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLDraggingDelegate\> |[bdl_delegate](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_delegate) |
|BDLDraggingMode |[bdl_draggingMode](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_draggingmode) |
|BOOL |[bdl_draggingInBounds](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_dragginginbounds) |
|UIEdgeInsets |[bdl_edgeInsets](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_edgeinsets) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[bdl_adsorbingAnimated:](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_adsorbinganimated) |
|void |[bdl_pullOverAnimated:](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_pulloveranimated) |
|void |[bdl_revertAnimated:](https://docs.byteplus.com/en/docs/11/5590#UIView(BDLDraggable)-bdl_revertanimated) |


<span id="instructions"></span>
## Instructions

<span id="UIView(BDLDraggable)-bdl_delegate"></span>
### bdl_delegate

```objectivec
@property (nonatomic, weak) id<BDLDraggingDelegate> bdl_delegate;
```


The drag event delegate, which can listen to the start, change, and end of drag events. For more information, see [BDLDraggingDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLDraggingDelegate).

<span id="UIView(BDLDraggable)-bdl_draggingmode"></span>
### bdl_draggingMode

```objectivec
@property (nonatomic, assign) BDLDraggingMode bdl_draggingMode;
```


The dragging mode. Default value: `BDLDraggingModeDisabled`. For more information, see [BDLDraggingMode](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLDraggingMode).

<span id="UIView(BDLDraggable)-bdl_dragginginbounds"></span>
### bdl_draggingInBounds

```objectivec
@property (nonatomic, assign) BOOL bdl_draggingInBounds;
```


Whether dragging is limited to the `superview` bounds. Default value: `YES`.


* `YES`: Dragging is limited to the `superview` bounds.

* `NO`: Dragging is allowed outside the `superview` bounds. The part outside the `superview` bounds cannot respond to drag actions again.

    &nbsp;


<span id="bdl-edgeinsets"></span>
### bdl_edgeInsets

```objectivec
@property (nonatomic, assign) UIEdgeInsets bdl_edgeInsets;
```


The non\-draggable border area. Default value: `0`. Not supported for `BDLDraggingModeAdsorb`.

<span id="instructions"></span>
## Instructions

<span id="UIView(BDLDraggable)-bdl_adsorbinganimated"></span>
### bdl_adsorbingAnimated:

```objectivec
- (void)bdl_adsorbingAnimated:(BOOL)animated;
```


Automatically snaps to and adheres to the edge.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|animated |BOOL |Whether animation is needed.<br><br><br>&nbsp;<br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="UIView(BDLDraggable)-bdl_pulloveranimated"></span>
### bdl_pullOverAnimated:

```objectivec
- (void)bdl_pullOverAnimated:(BOOL)animated;
```


Automatically snaps to the edge.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|animated |BOOL |Whether animation is needed.<br><br><br>&nbsp;<br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="UIView(BDLDraggable)-bdl_revertanimated"></span>
### bdl_revertAnimated:

```objectivec
- (void)bdl_revertAnimated:(BOOL)animated;
```


Automatically reverts to the original position.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|animated |BOOL |Whether animation is needed.<br><br><br>&nbsp;<br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLCountdownView"></span>
# BDLCountdownView

```objectivec
@interface BDLCountdownView : BDLBaseView <BDLBasicService, BDLLanguageService>
```


The live room countdown view, including the live booking.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLCountdownViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-delegate) |
|UILabel\* |[hintLabel](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-hintlabel) |
|UILabel\* |[countdownLabel](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-countdownlabel) |
|UIButton\* |[bookingButton](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-bookingbutton) |
|NSString\* |[addEventSuccessToast](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-addeventsuccesstoast) |
|NSString\* |[addEventFailToast](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-addeventfailtoast) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-initwithportrait) |
|void |[cancel](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-cancel) |
|void |[setActivityBooked](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-setactivitybooked) |
|BOOL |[onBookingButtonClicked](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-onbookingbuttonclicked) |
|void |[onCalendarResult](https://docs.byteplus.com/en/docs/11/5590#BDLCountdownView-oncalendarresult) |


<span id="instructions"></span>
## Instructions

<span id="BDLCountdownView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLCountdownViewDelegate> delegate;
```


The delegate method. For more information, see [BDLCountdownViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLCountdownViewDelegate).

<span id="BDLCountdownView-hintlabel"></span>
### hintLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *hintLabel;
```


The text label of "The live stream will start in". All properties except `frame` and `text` can be customized.

<span id="BDLCountdownView-countdownlabel"></span>
### countdownLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *countdownLabel;
```


The label of the current remaining time. All properties except `text` can be customized.

<span id="BDLCountdownView-bookingbutton"></span>
### bookingButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *bookingButton;
```


The book button, which is displayed only when the live booking feature is enabled. The `text` in the `Normal` and `Disabled` status cannot be customized.

<span id="BDLCountdownView-addeventsuccesstoast"></span>
### addEventSuccessToast

```objectivec
@property (nonatomic, copy) NSString *addEventSuccessToast;
```


The text of the toast indicating that booking the live stream is successful.

<span id="BDLCountdownView-addeventfailtoast"></span>
### addEventFailToast

```objectivec
@property (nonatomic, copy) NSString *addEventFailToast;
```


The text of the toast indicating that booking the live stream failed.

<span id="instructions"></span>
## Instructions

<span id="BDLCountdownView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the live room countdown view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the live room countdown view.

<span id="BDLCountdownView-cancel"></span>
### cancel

```objectivec
- (void)cancel;
```


Stops the countdown.

<span id="BDLCountdownView-setactivitybooked"></span>
### setActivityBooked

```objectivec
- (void)setActivityBooked;
```


The callback is triggered when the system calendar event is successfully created.

After successfully creating a system calendar event on your own, you need to call this callback to notify the SDK that the viewer has booked the live stream. Once the SDK receives the notification, you can change the button for booking the live stream to the booked status.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the authentication mode is set to public, you can call the <a href="https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-clearcache">clearCache</a> method to clear all local cache of the SDK on the viewer's current device, thereby changing the button from the booked status to unbooked status in all live rooms of the viewer.</div>


<span id="BDLCountdownView-onbookingbuttonclicked"></span>
### onBookingButtonClicked

```objectivec
@property (nonatomic, copy) BOOL (^onBookingButtonClicked)(BDLActivityBookingModel *activityBookingModel);
```


The callback is triggered when the live booking button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activityBookingModel |BDLActivityBookingModel\* |The model of live booking information. For more information, see [BDLActivityBookingModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLActivityBookingModel). |


**Return Value**

Whether you need to create a system calendar event on your own. If this callback is not implemented, the SDK automatically creates a system calendar event.


* `YES`: You need to create a system calendar event on your own. You can use the SDK's [addCalendarEvent:alarms:startDate:endDate:completion:](https://docs.byteplus.com/en/docs/11/5590#BDLCalendarUtils-addcalendarevent-alarms-startdate-enddate-completion) method to create a system calendar event, or you can create the event in other ways.

* `NO`: The SDK automatically creates a system calendar event.

    &nbsp;


<span id="oncalendarresult"></span>
### onCalendarResult

```objectivec
@property (nonatomic, copy) void (^onCalendarResult)(BDLActivityBookingModel *activityBookingModel, BOOL isSuccess);
```


The callback for system calendar event creation results.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activityBookingModel |BDLActivityBookingModel\* |The model of live booking information. For more information, see [BDLActivityBookingModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLActivityBookingModel). |
|isSuccess |BOOL |Whether the system calendar event creation is successful.<br><br><br>* `YES`: Successful.<br><br>* `NO`: Failed. |


<span id="BDLNetworkViaWWANView"></span>
# BDLNetworkViaWWANView

```objectivec
@interface BDLNetworkViaWWANView : BDLBaseView <BDLLanguageService>
```


The mobile data access prompt view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLNetworkViaWWANViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkViaWWANView-delegate) |
|UILabel\* |[promptLabel](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkViaWWANView-promptlabel) |
|UIView\* |[contentView](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkViaWWANView-contentview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:config:](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkViaWWANView-initwithportrait-config) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkViaWWANView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLNetworkViaWWANView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLNetworkViaWWANViewDelegate> delegate;
```


The delegate method. For more information, see [BDLNetworkViaWWANViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLNetworkViaWWANViewDelegate).

<span id="BDLNetworkViaWWANView-promptlabel"></span>
### promptLabel

```objectivec
@property (nonatomic, strong) UILabel *promptLabel;
```


The prompt label. You can customize the prompt text and text color by using [viaWWANText](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-viawwantext) and [promptTextColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-prompttextcolor).

<span id="BDLNetworkViaWWANView-contentview"></span>
### contentView

```objectivec
@property (nonatomic, strong) UIView *contentView;
```


The background view. Customization is supported.

<span id="instructions"></span>
## Instructions

<span id="BDLNetworkViaWWANView-initwithportrait-config"></span>
### initWithPortrait:config:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait config:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the mobile data access prompt view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the mobile data access prompt view.

<span id="BDLNetworkViaWWANView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLCalendarUtils"></span>
# BDLCalendarUtils

```objectivec
@interface BDLCalendarUtils : NSObject
```


The calendar utility class.

<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|void |[addCalendarEvent:alarms:startDate:endDate:completion:](https://docs.byteplus.com/en/docs/11/5590#BDLCalendarUtils-addcalendarevent-alarms-startdate-enddate-completion) |


<span id="instructions"></span>
## Instructions

<span id="BDLCalendarUtils-addcalendarevent-alarms-startdate-enddate-completion"></span>
### addCalendarEvent:alarms:startDate:endDate:completion:

```objectivec
+ (void)addCalendarEvent:(NSString *)eventTitle 
                  alarms:(NSArray<EKAlarm *> *)alarms
               startDate:(NSDate *)startDate
                 endDate:(NSDate *)endDate
              completion:(void(^)(BOOL success, NSError *error))completion;
```


Creates a system calendar event.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|eventTitle |NSString\* |The event title, namely the live room name. |
|alarms |NSArray<EKAlarm\*\>\* |How long a notification is sent in advance of the start time of the live stream. For more information, see [EKAlarm](https://developer.apple.com/documentation/eventkit/ekalarm?language=objc).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Multiple reminder times can be set.</div><br> |
|startDate |NSDate\* |The start time of the live stream. |
|endDate |NSDate\* |The end time of the live stream. |
|completion |void(^)(BOOL success, NSError\*error) |The callback triggered when the system calendar event is created.<br><br>&nbsp;<br><br>Input parameters:<br><br><br>* `success`: Whether the system calendar event creation is successful.<br><br>   * `YES`: Successful.<br><br>   * `NO`: Failed.<br><br>* `error`: The error information. For more information, see [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=l_1&language=objc). |


<span id="BDLUpperAdView"></span>
# BDLUpperAdView

```objectivec
@interface BDLUpperAdView : BDLBaseView <BDLPageUpperAdService>
```


The floating ad view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLUpperAdView-closebutton) |
|UIImageView\* |[imageView](https://docs.byteplus.com/en/docs/11/5590#BDLUpperAdView-imageview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[viewTappedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLUpperAdView-viewtappedblock) |
|void |[closeButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLUpperAdView-closebuttonclickedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLUpperAdView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong) UIButton* closeButton;
```


The close button. All properties except `frame` and `hidden` can be customized.

<span id="BDLUpperAdView-imageview"></span>
### imageView

```objectivec
@property (nonatomic, strong) UIImageView* imageView;
```


The ad image. All properties except `frame` and `hidden` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLUpperAdView-viewtappedblock"></span>
### viewTappedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^viewTappedBlock)(NSString * _Nullable urlStr, BOOL enableFloating);
```


The callback is triggered when the floating ad is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|urlStr |NSString\* |The embedded link returned by the BytePlus Live server. |
|enableFloating |BOOL |Whether the ad details page is displayed on a floating page in the live room.<br><br><br>* `YES`: The ad details page is displayed on a floating page in the live room after viewers tap the floating ad. Viewers can watch the video and view the ad details page at the same time.<br><br>* `NO`: The ad details page is displayed on a new browser tab after viewers tap the floating ad. Viewers cannot watch the video and view the ad details page at the same time. |


<span id="BDLUpperAdView-closebuttonclickedblock"></span>
### closeButtonClickedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^closeButtonClickedBlock)(void);
```


The callback is triggered when the close button is tapped.

<span id="BDLLivePullViewController()"></span>
# BDLLivePullViewController()

```objectivec
@interface BDLLivePullViewController ()
```


The full\-featured live room controller.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIScrollView\* |[contentScrollView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-contentscrollview) |
|UIImageView\* |[backgroundImageView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-backgroundimageview) |
|UIImageView\* |[headerImageView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-headerimageview) |
|UIButton\* |[exitClearModeButton](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-exitclearmodebutton) |
|BDLFloatingController\* |[floatingController](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-floatingcontroller) |
|UIView\* |[accountView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-accountview) |
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-closebutton) |
|UIButton\* |[shareButton](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-sharebutton) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-titlelabel) |
|UIView\* |[pageAdView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-pageadview) |
|BDLPlayerView\* |[playerView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-playerview) |
|UIView\* |[playerContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-playercontainerview) |
|UIView\* |[countdownView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-countdownview) |
|UIView\* |[countdownContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-countdowncontainerview) |
|BDLLiveDescriptionView\* |[liveDescriptionView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-livedescriptionview) |
|BDLCommentAndNoticeView\* |[commentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-commentandnoticeview) |
|BDLMenuBarView\* |[menuBarView](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-menubarview) |
|UIButton\* |[multiLangButton](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-multilangbutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[floatingPlayerViewWillAppear](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-floatingplayerviewwillappear) |
|void |[floatingPlayerViewDidDisappear](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-floatingplayerviewdiddisappear) |
|void |[floatingPlayerViewWillClose](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-floatingplayerviewwillclose) |
|CGRect |[frameForFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-frameforfloatingplayer) |
|BOOL |[onFloatingPlayerTapped](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-onfloatingplayertapped) |
|BOOL |[onFloatingPlayerCloseTapped](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-onfloatingplayerclosetapped) |
|void |[onUserForceOfflineBlock](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController()-onuserforceofflineblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewController()-contentscrollview"></span>
### contentScrollView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIScrollView *contentScrollView;
```


The `ScrollView` that displays content.

<span id="BDLLivePullViewController()-backgroundimageview"></span>
### backgroundImageView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIImageView *backgroundImageView;
```


The background image view.

<span id="BDLLivePullViewController()-headerimageview"></span>
### headerImageView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIImageView *headerImageView;
```


The header image view.

<span id="BDLLivePullViewController()-exitclearmodebutton"></span>
### exitClearModeButton

```objectivec
@property (nonatomic, strong, readonly, nullable) UIButton *exitClearModeButton;
```


The button for exiting the screen clearing.

<span id="BDLLivePullViewController()-floatingcontroller"></span>
### floatingController

```objectivec
@property (nonatomic, strong, readonly) BDLFloatingController *floatingController;
```


The floating player. For more information, see [BDLFloatingController](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLFloatingController).

<span id="BDLLivePullViewController()-accountview"></span>
### accountView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIView *accountView;
```


The host account view.

<span id="BDLLivePullViewController()-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly, nullable) UIButton *closeButton;
```


The button for closing the live room.

<span id="BDLLivePullViewController()-sharebutton"></span>
### shareButton

```objectivec
@property (nonatomic, strong, readonly, nullable) UIButton *shareButton;
```


The share button.

<span id="BDLLivePullViewController()-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly, nullable) UILabel *titleLabel;
```


The title label.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For live rooms in portrait mode, the title is displayed only when no host account is added to the live room.</div>


<span id="BDLLivePullViewController()-pageadview"></span>
### pageAdView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIView *pageAdView;
```


The in\-page ad view.

<span id="BDLLivePullViewController()-playerview"></span>
### playerView

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLPlayerView *playerView;
```


The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView).

<span id="BDLLivePullViewController()-playercontainerview"></span>
### playerContainerView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIView *playerContainerView;
```


The container view of the player.

<span id="BDLLivePullViewController()-countdownview"></span>
### countdownView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIView *countdownView;
```


The live room countdown view.

<span id="BDLLivePullViewController()-countdowncontainerview"></span>
### countdownContainerView

```objectivec
@property (nonatomic, strong, readonly, nonnull) UIView *countdownContainerView;
```


The container view of the live room countdown.

<span id="BDLLivePullViewController()-livedescriptionview"></span>
### liveDescriptionView

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLLiveDescriptionView *liveDescriptionView;
```


The live room description view. For more information, see [BDLLiveDescriptionView](https://docs.byteplus.com/en/docs/11/5590#BDLLiveDescriptionView).

<span id="BDLLivePullViewController()-commentandnoticeview"></span>
### commentAndNoticeView

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLCommentAndNoticeView *commentAndNoticeView;
```


The comment and notification view. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView).

<span id="BDLLivePullViewController()-menubarview"></span>
### menuBarView

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLMenuBarView *menuBarView;
```


The menu bar view. For more information, see [BDLMenuBarView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView).

<span id="BDLLivePullViewController()-multilangbutton"></span>
### multiLangButton

```objectivec
@property (nonatomic, strong, readonly, nullable) UIButton *multiLangButton;
```


The button for changing the viewing page language.

<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewController()-floatingplayerviewwillappear"></span>
### floatingPlayerViewWillAppear

```objectivec
@property (nonatomic, copy, nullable) void (^floatingPlayerViewWillAppear)(BDLLivePullViewController *viewController, BDLFloatingPlayer *floatingPlayer);
```


The SDK calls this method when the floating player is about to appear.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer). |


<span id="BDLLivePullViewController()-floatingplayerviewdiddisappear"></span>
### floatingPlayerViewDidDisappear

```objectivec
@property (nonatomic, copy, nullable) void (^floatingPlayerViewDidDisappear)(BDLLivePullViewController *viewController, BDLFloatingPlayer *floatingPlayer);
```


The SDK calls this method when the floating player disappears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer). |


<span id="BDLLivePullViewController()-floatingplayerviewwillclose"></span>
### floatingPlayerViewWillClose

```objectivec
@property (nonatomic, copy, nullable) void (^floatingPlayerViewWillClose)(BDLLivePullViewController *viewController, BDLFloatingPlayer *floatingPlayer);
```


The SDK calls this method when the floating player is about to close.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer). |


<span id="BDLLivePullViewController()-frameforfloatingplayer"></span>
### frameForFloatingPlayer

```objectivec
@property (nonatomic, copy, nullable) CGRect (^frameForFloatingPlayer)(BDLLivePullViewController *viewController, BDLFloatingPlayer *floatingPlayer);
```


Customizes the initial position of the floating player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer). |


**Return Value**

The initial position of the floating player.

<span id="BDLLivePullViewController()-onfloatingplayertapped"></span>
### onFloatingPlayerTapped

```objectivec
@property (nonatomic, copy, nullable) BOOL (^onFloatingPlayerTapped)(BDLLivePullViewController *viewController, BDLFloatingPlayer *floatingPlayer);
```


The SDK calls this method when viewers tap the floating player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer). |


**Return Value**

Whether to execute [defaultFloatingPlayerTapAction](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayertapaction).


* `YES`: Execute.

* `NO`: Do not execute.

    &nbsp;


<span id="onfloatingplayerclosetapped"></span>
### onFloatingPlayerCloseTapped

```objectivec
@property (nonatomic, copy, nullable) BOOL (^onFloatingPlayerCloseTapped)(BDLLivePullViewController *viewController, BDLFloatingPlayer *floatingPlayer);
```


The SDK calls this method when viewers tap the close button of the floating player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer). |


**Return Value**

Whether to execute [defaultFloatingPlayerCloseAction](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController(BDLDefaultAction)-defaultfloatingplayercloseaction).


* `YES`: Execute.

* `NO`: Do not execute.

    &nbsp;


<span id="onuserforceofflineblock"></span>
### onUserForceOfflineBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onUserForceOfflineBlock)(BDLLivePullViewController *viewController, BDLForceOfflineInfo *info);
```


The SDK calls this method when viewers are forcibly removed from the live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|viewController |BDLLivePullViewController\* |The full\-featured live room. |
|info |BDLForceOfflineInfo\* |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLForceOfflineInfo). |


<span id="BDLCommentAndNoticeView"></span>
# BDLCommentAndNoticeView

```objectivec
@interface BDLCommentAndNoticeView : BDLBaseView
```


The comment and notification view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLNoticeContainerView\* |[noticeContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView-noticecontainerview) |
|BDLCommentView\* |[commentView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView-commentview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[topCommentClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView-topcommentclickblock) |
|void |[topCommentNicknameClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView-topcommentnicknameclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentAndNoticeView-noticecontainerview"></span>
### noticeContainerView

```objectivec
@property (nonatomic, strong, readonly) BDLNoticeContainerView *noticeContainerView;
```


The container view of notifications. For more information, see [BDLNoticeContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLNoticeContainerView).

<span id="BDLCommentAndNoticeView-commentview"></span>
### commentView

```objectivec
@property (nonatomic, strong, readonly) BDLCommentView *commentView;
```


The comment area view. For more information, see [BDLCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView).

<span id="instructions"></span>
## Instructions

<span id="BDLCommentAndNoticeView-topcommentclickblock"></span>
### topCommentClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^topCommentClickBlock)(BDLCommentAndNoticeView *view, BDLCommentModel *comment);
```


The callback is triggered when the pinned text comment is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLCommentAndNoticeView\* |The comment and notification view. |
|comment |BDLCommentModel\* |The tapped comment. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLCommentAndNoticeView-topcommentnicknameclickblock"></span>
### topCommentNicknameClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^topCommentNicknameClickBlock)(BDLCommentAndNoticeView *view, BDLCommentModel *comment);
```


The callback is triggered when the nickname of the pinned comment is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLCommentAndNoticeView\* |The comment and notification view. |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLPopupBottomOrRightShowBaseView"></span>
# BDLPopupBottomOrRightShowBaseView

```objectivec
@interface BDLPopupBottomOrRightShowBaseView : BDLPopupBaseView <BDLPopupBottomOrRightShowViewProtocol>
```


The base view for bottom or right\-side dialog box view.

<span id="BDLFloatingPlayer"></span>
# BDLFloatingPlayer

```objectivec
@interface BDLFloatingPlayer : NSObject
```


The floating player.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLFloatingPlayerDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-delegate) |
|BDLBasePlayerView\* |[basePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-baseplayerview) |
|UIView\* |[containerView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-containerview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-initwithportrait) |
|instancetype |[initWithPortrait:basePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-initwithportrait-baseplayerview) |
|BDLBasePlayerView |[removeBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-removebaseplayerview) |
|void |[setUIOrientation:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-setuiorientation) |
|BOOL |[showWithCloseButton:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-showwithclosebutton) |
|BOOL |[showWithFrame:closeButton:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-showwithframe-closebutton) |
|void |[hide](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-hide) |
|void |[close](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-close) |
|BOOL |[isFloating](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-isfloating) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingPlayer-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLFloatingPlayerDelegate> delegate;
```


The delegate method. For more information, see [BDLFloatingPlayerDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLFloatingPlayerDelegate).

<span id="BDLFloatingPlayer-baseplayerview"></span>
### basePlayerView

```objectivec
@property (nonatomic, strong, readonly) BDLBasePlayerView *basePlayerView;
```


The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView).

<span id="BDLFloatingPlayer-containerview"></span>
### containerView

```objectivec
@property (nonatomic, strong, readonly) UIView *containerView;
```


The container view.

<span id="instructions"></span>
## Instructions

<span id="BDLFloatingPlayer-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the floating player instance.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode. Get the loading image of the floating player by using [loadingImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimage) and the loading image size by using [loadingImageSize](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimagesize).<br><br>* `NO`: Landscape mode. Get the loading image of the floating player by using [loadingImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimage) and the loading image size by using [loadingImageSize](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimagesize). |


**Return Value**

The floating player instance.

<span id="BDLFloatingPlayer-initwithportrait-baseplayerview"></span>
### initWithPortrait:basePlayerView:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait basePlayerView:(BDLBasePlayerView *)basePlayerView;
```


Initializes the floating player instance.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode. Get the loading image of the floating player by using [loadingImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimage) and the loading image size by using [loadingImageSize](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimagesize).<br><br>* `NO`: Landscape mode. Get the loading image of the floating player by using [loadingImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimage) and the loading image size by using [loadingImageSize](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-loadingimagesize). |
|basePlayerView |BDLBasePlayerView\* |The custom player that has already started playing. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView). |


**Return Value**

The floating player instance.

<span id="BDLFloatingPlayer-removebaseplayerview"></span>
### removeBasePlayerView

```objectivec
- (BDLBasePlayerView *)removeBasePlayerView;
```


Removes the custom player that has already started playing.

**Return Value**

The removed custom player.

<span id="BDLFloatingPlayer-setuiorientation"></span>
### setUIOrientation:

```objectivec
- (void)setUIOrientation:(UIInterfaceOrientation)orientation;
```


Sets the player orientation.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|orientation |UIInterfaceOrientation |The player orientation. |


<span id="BDLFloatingPlayer-showwithclosebutton"></span>
### showWithCloseButton:

```objectivec
- (BOOL)showWithCloseButton:(BOOL)haveCloseButton;
```


Displays the player. The player is displayed in the lower\-right corner with a 16:9 aspect ratio. If a video size is already specified, the aspect ratio is either 16:9 or 9:16 based on the video size.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|haveCloseButton |BOOL |Whether to display the close button in the upper\-right corner of the floating player.<br><br><br>* `YES`: Display.<br><br>* `NO`: Do not display. |


**Return Value**


* `YES`: Displayed successfully.

* `NO`: The floating player is being displayed.

    &nbsp;


<span id="showwithframe-closebutton"></span>
### showWithFrame:closeButton:

```objectivec
- (BOOL)showWithFrame:(CGRect)frame closeButton:(BOOL)haveCloseButton;
```


Displays the player at the specified position.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |CGRect |The display position. |
|haveCloseButton |BOOL |Whether the close button is needed.<br><br><br>&nbsp;<br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


**Return Value**


* `YES`: Displayed successfully.

* `NO`: The floating player is being displayed.

    &nbsp;


<span id="hide"></span>
### hide

```objectivec
- (void)hide;
```


Hides the player.

<span id="BDLFloatingPlayer-close"></span>
### close

```objectivec
- (void)close;
```


Closes the player. This has the same effect as [hide](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingPlayer-hide), but additionally triggers the [floatingPlayerWillClose](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLFloatingPlayerDelegate-floatingplayerwillclose) callback.

<span id="BDLFloatingPlayer-isfloating"></span>
### isFloating

```objectivec
- (BOOL)isFloating;
```


Whether the player is in the floating mode.

**Return Value**


* `YES`: In the floating mode.

* `NO`: Not in the floating mode.

    &nbsp;


<span id="bdlpopuprightshowbaseview"></span>
# BDLPopupRightShowBaseView

```objectivec
@interface BDLPopupRightShowBaseView : BDLPopupBaseView <BDLPopupRightShowViewProtocol>
```


The base view for the right\-side dialog box view.

<span id="BDLBasePlayerView"></span>
# BDLBasePlayerView

```objectivec
@interface BDLBasePlayerView : BDLBaseView <BDLBasicService, BDLPullStreamUrlService>
```


The custom player view. The player internally listens to the live room status and supports playing the corresponding VOD or live video based on the live room status.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLBasePlayerViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-delegate) |
|UIImageView\* |[coverImageView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-coverimageview) |
|UIView\* |[watermarkView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-watermarkview) |
|UIView\* |[videoView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-videoview) |
|BDLPlayerScalingMode |[scalingMode](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-scalingmode) |
|BOOL |[muted](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-muted) |
|BOOL |[forbidPlay](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-forbidplay) |
|BOOL |[enablePictureInPicture](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-enablepictureinpicture) |
|BOOL |[isLive](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-islive) |
|BOOL |[isVod](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-isvod) |
|BOOL |[isPlaying](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-isplaying) |
|BDLPlayerState |[playerState](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-playerstate) |
|BOOL |[isStalling](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-isstalling) |
|BOOL |[isFirstVideoFrameRendered](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-isfirstvideoframerendered) |
|CGSize |[videoSize](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-videosize) |
|NSArray<NSNumber\*\>\* |[supportedVideoResolutions](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-supportedvideoresolutions) |
|BDLVideoResolution |[currentVideoResolution](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-currentvideoresolution) |
|BDLBasePlayerConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-config) |
|NSError\* |[liveError](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-liveerror) |
|NSTimeInterval |[duration](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-duration) |
|NSTimeInterval |[playableDuration](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-playableduration) |
|NSTimeInterval |[currentPlaybackTime](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-currentplaybacktime) |
|BOOL |[isSeeking](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-isseeking) |
|BOOL |[looping](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-looping) |
|CGFloat |[playbackSpeed](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-playbackspeed) |
|BOOL |[visible](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-visible) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setVodStartTime:](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-setvodstarttime) |
|void |[play](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-play) |
|void |[stop](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-stop) |
|void |[pause](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-pause) |
|void |[seek:completion:](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-seek-completion) |
|void |[addPeriodicObserverWithInterval:queue:usingBlock:](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-addperiodicobserverwithinterval-queue-usingblock) |
|void |[removePeriodicObserver](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-removeperiodicobserver) |
|BOOL |[resetCurrentContinuePlaybackTime](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView-resetcurrentcontinueplaybacktime) |


<span id="instructions"></span>
## Instructions

<span id="BDLBasePlayerView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLBasePlayerViewDelegate> delegate;
```


The delegate method. For more information, see [BDLBasePlayerViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLBasePlayerViewDelegate).

<span id="BDLBasePlayerView-coverimageview"></span>
### coverImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *coverImageView;
```


The live cover imageView.

<span id="BDLBasePlayerView-watermarkview"></span>
### watermarkView

```objectivec
@property (nonatomic, strong, readonly) UIView *watermarkView;
```


The watermark view.

<span id="BDLBasePlayerView-videoview"></span>
### videoView

```objectivec
@property (nonatomic, strong, readonly, nullable) UIView *videoView;
```


The player view.

<span id="BDLBasePlayerView-scalingmode"></span>
### scalingMode

```objectivec
@property (nonatomic, assign) BDLPlayerScalingMode scalingMode;
```


The video scaling mode. For more information, see [BDLPlayerScalingMode](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerScalingMode).

<span id="BDLBasePlayerView-muted"></span>
### muted

```objectivec
@property (nonatomic, assign) BOOL muted;
```


Whether to mute the video.


* `YES`: Mute.

* `NO`: Do not mute.

    &nbsp;


<span id="forbidplay"></span>
### forbidPlay

```objectivec
@property (nonatomic, assign) BOOL forbidPlay;
```


Whether to prohibit playing the video.


* `YES`: Prohibit.

* `NO`: Do not prohibit.

    &nbsp;


<span id="enablepictureinpicture"></span>
### enablePictureInPicture

```objectivec
@property (nonatomic, assign) BOOL enablePictureInPicture API_AVAILABLE(ios(14.0));
```


Whether to enable system PiP.


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="islive"></span>
### isLive

```objectivec
@property (nonatomic, assign, readonly) BOOL isLive;
```


Whether it is a live stream.


* `YES`: A live stream.

* `NO`: Not a live stream.

    &nbsp;


<span id="isvod"></span>
### isVod

```objectivec
@property (nonatomic, assign, readonly) BOOL isVod;
```


Whether it is a VOD video.


* `YES`: A VOD video.

* `NO`: Not a VOD video.

    &nbsp;


<span id="isplaying"></span>
### isPlaying

```objectivec
@property (nonatomic, assign, readonly) BOOL isPlaying;
```


Whether a video is playing.


* `YES`: Playing.

* `NO`: Not playing.

    &nbsp;


<span id="playerstate"></span>
### playerState

```objectivec
@property (nonatomic, assign, readonly) BDLPlayerState playerState;
```


The player status. For more information, see [BDLPlayerState](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerState).

<span id="BDLBasePlayerView-isstalling"></span>
### isStalling

```objectivec
@property (nonatomic, assign, readonly) BOOL isStalling;
```


Whether the video is stuttering.


* `YES`: Stuttering.

* `NO`: Not stuttering.

    &nbsp;


<span id="isfirstvideoframerendered"></span>
### isFirstVideoFrameRendered

```objectivec
@property (nonatomic, assign, readonly) BOOL isFirstVideoFrameRendered;
```


Whether the first frame of the video is rendered.


* `YES`: Rendered.

* `NO`: Not rendered.

    &nbsp;


<span id="videosize"></span>
### videoSize

```objectivec
@property (nonatomic, assign, readonly) CGSize videoSize;
```


The video size.

<span id="BDLBasePlayerView-supportedvideoresolutions"></span>
### supportedVideoResolutions

```objectivec
@property (nonatomic, copy, readonly, nullable) NSArray<NSNumber *> *supportedVideoResolutions;
```


The currently supported resolutions.

<span id="BDLBasePlayerView-currentvideoresolution"></span>
### currentVideoResolution

```objectivec
@property (nonatomic, assign) BDLVideoResolution currentVideoResolution;
```


The currently used resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution).

<span id="BDLBasePlayerView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLBasePlayerConfiguration *config;
```


The player configuration. For more information, see [BDLBasePlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLBasePlayerConfiguration).

<span id="BDLBasePlayerView-liveerror"></span>
### liveError

```objectivec
@property (nonatomic, strong, readonly) NSError *liveError;
```


The live error information.

<span id="BDLBasePlayerView-duration"></span>
### duration

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval duration;
```


The total duration of the VOD video. Unit: seconds.

<span id="BDLBasePlayerView-playableduration"></span>
### playableDuration

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval playableDuration;
```


The current playable duration, namely the cached duration. Unit: seconds.

<span id="BDLBasePlayerView-currentplaybacktime"></span>
### currentPlaybackTime

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval currentPlaybackTime;
```


The current playback time. Unit: seconds.

<span id="BDLBasePlayerView-isseeking"></span>
### isSeeking

```objectivec
@property (nonatomic, assign, readonly) BOOL isSeeking;
```


Whether the player is seeking to a specific time point of the video.


* `YES`: Seeking.

* `NO`: Not seeking.

    &nbsp;


<span id="looping"></span>
### looping

```objectivec
@property (nonatomic, assign) BOOL looping;
```


Whether to play in a loop.


* `YES`: In a loop.

* `NO`: Not in a loop.

    &nbsp;


<span id="playbackspeed"></span>
### playbackSpeed

```objectivec
@property (nonatomic, assign) CGFloat playbackSpeed;
```


The playback speed.

<span id="BDLBasePlayerView-visible"></span>
### visible

```objectivec
@property (nonatomic, assign) BOOL visible;
```


Whether the player is visible. Default value: `YES`.


* `YES`: Visible. When the player is invisible, the paused live or VOD video automatically resumes playing. If system PiP is enabled, the system PiP is displayed when the app switches to the background.

* `NO`: Invisible. When the app switches to the background, the system PiP is not displayed even if it is enabled, and the playing live or VOD video is paused. Additionally, the video does not automatically play when the live room status changes, even if autoplay is enabled.


<span id="instructions"></span>
## Instructions

<span id="BDLBasePlayerView-setvodstarttime"></span>
### setVodStartTime:

```objectivec
- (void)setVodStartTime:(NSTimeInterval)startTime;
```


Sets the time from which to start playing the VOD video.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|startTime |NSTimeInterval |The time from which to start playing the VOD video. Unit: seconds. |


<span id="BDLBasePlayerView-play"></span>
### play

```objectivec
- (void)play;
```


Plays the video.

<span id="BDLBasePlayerView-stop"></span>
### stop

```objectivec
- (void)stop;
```


Stops playing the video.

<span id="BDLBasePlayerView-pause"></span>
### pause

```objectivec
- (void)pause;
```


Pauses the video.

<span id="BDLBasePlayerView-seek-completion"></span>
### seek:completion:

```objectivec
- (void)seek:(NSTimeInterval)playbackTime completion:(BDLBasePlayerViewSeekCompletionBlock _Nullable)completion;
```


Seeks to the specific time point of the preview or playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playbackTime |NSTimeInterval |The time point to seek to. Unit: seconds. |
|completion |BDLBasePlayerViewSeekCompletionBlock |The callback triggered after the seek operation is complete. For more information, see [BDLBasePlayerViewSeekCompletionBlock](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#bdlbaseplayerviewseekcompletionblock). |


<span id="BDLBasePlayerView-addperiodicobserverwithinterval-queue-usingblock"></span>
### addPeriodicObserverWithInterval:queue:usingBlock:

```objectivec
- (void)addPeriodicObserverWithInterval:(NSTimeInterval)interval queue:(dispatch_queue_t)queue usingBlock:(void (^)(void))block;
```


Adds a periodic event to regularly get data from the player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interval |NSTimeInterval |The time interval. Unit: seconds. |
|queue |dispatch_queue_t |The target queue for executing operations. |
|block |void(^)(void) |The periodic task to perform. |


<span id="BDLBasePlayerView-removeperiodicobserver"></span>
### removePeriodicObserver

```objectivec
- (void)removePeriodicObserver;
```


Removes the periodic event.

<span id="BDLBasePlayerView-resetcurrentcontinueplaybacktime"></span>
### resetCurrentContinuePlaybackTime

```objectivec
- (BOOL)resetCurrentContinuePlaybackTime;
```


Resets the resume playback record for the current video.

**Return Value**


* `YES`: Reset successfully.

* `NO`: Failed to reset.

    &nbsp;


<span id="bdlawardconditionview"></span>
# BDLAwardConditionView

```objectivec
@interface BDLAwardConditionView : BDLBaseView <BDLLanguageService>
```


The view of the participation condtions in the lucky draw details.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardConditionView-titlelabel) |
|UILabel\* |[subTitleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardConditionView-subtitlelabel) |
|UILabel\* |[conditionLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardConditionView-conditionlabel) |
|UIImageView\* |[checkMarkImageView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardConditionView-checkmarkimageview) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardConditionView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The text label of "Condition". All properties except `text` can be customized.

<span id="BDLAwardConditionView-subtitlelabel"></span>
### subTitleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *subTitleLabel;
```


The text label of "Click Participate to automatically send the bullet comment password and take part in the lucky draw". All properties except `text` can be customized.

<span id="BDLAwardConditionView-conditionlabel"></span>
### conditionLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *conditionLabel;
```


The label for specific participation conditions. All properties except `text` can be customized.

<span id="BDLAwardConditionView-checkmarkimageview"></span>
### checkMarkImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *checkMarkImageView;
```


The imageView for the participation condition selection status. Custom images are supported.

<span id="BDLPlayerResolutionView"></span>
# BDLPlayerResolutionView

```objectivec
@interface BDLPlayerResolutionView : BDLPopupBottomOrRightShowBaseView <BDLLanguageService>
```


The resolution selection view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLPlayerResolutionViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerResolutionView-delegate) |
|BOOL |[fullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerResolutionView-fullscreen) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateWithResolutions:currentResolution:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerResolutionView-updatewithresolutions-currentresolution) |
|void |[changeResolutionSuccess:completeResolution:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerResolutionView-changeresolutionsuccess-completeresolution) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerResolutionView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerResolutionView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLPlayerResolutionViewDelegate> delegate;
```


The delegate method. For more information, see [BDLPlayerResolutionViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLPlayerResolutionViewDelegate).

<span id="BDLPlayerResolutionView-fullscreen"></span>
### fullScreen

```objectivec
@property (nonatomic, assign) BOOL fullScreen;
```


Whether in full\-screen mode.


* `YES`: In full\-screen mode.

* `NO`: Not in full\-screen mode.


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerResolutionView-updatewithresolutions-currentresolution"></span>
### updateWithResolutions:currentResolution:

```objectivec
- (void)updateWithResolutions:(NSArray<NSNumber *> *)resolutions currentResolution:(BDLVideoResolution)currentResolution;
```


Updates the resolution.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|resolutions |NSArray<NSNumber\*\>\* |All the supported resolutions. |
|currentResolution |BDLVideoResolution |The currently selected resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLPlayerResolutionView-changeresolutionsuccess-completeresolution"></span>
### changeResolutionSuccess:completeResolution:

```objectivec
- (void)changeResolutionSuccess:(BOOL)success completeResolution:(BDLVideoResolution)completeResolution;
```


Changes the resolution to synchronize the display of the resolution button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|success |BOOL |Whether the resolution change is successful.<br><br><br>* `YES`: Successful.<br><br>* `NO`: Failed. |
|completeResolution |BDLVideoResolution |The final resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLPlayerResolutionView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLPlayerView"></span>
# BDLPlayerView

```objectivec
@interface BDLPlayerView : BDLBaseView <BDLBasicService, BDLLanguageService, BDLCardExplainService>
```


The player view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[popupSuperView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-popupsuperview) |
|id<BDLPlayerViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-delegate) |
|BDLBasePlayerView\* |[basePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-baseplayerview) |
|BDLPlayerMaskView\* |[playerMaskView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-playermaskview) |
|BDLPlayerControlView\* |[controlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-controlview) |
|BDLPlayerResolutionView\* |[resolutionView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-resolutionview) |
|BDLPlayerSpeedView\* |[speedView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-speedview) |
|BDLLoadingView\* |[loadingView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-loadingview) |
|BDLNetworkNotReachableView\* |[networkNotReachableView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-networknotreachableview) |
|BDLNetworkViaWWANView\* |[networkViaWWANView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-networkviawwanview) |
|BDLPlayerReplayView\* |[replayView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-replayview) |
|BDLContinuePlaybackToastView\* |[continuePlaybackToastView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-continueplaybacktoastview) |
|BDLPlayerConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-config) |
|BOOL |[isPiPStarted](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-ispipstarted) |
|BOOL |[isFullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-isfullscreen) |
|BOOL |[isPlayerFullSuper](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-isplayerfullsuper) |
|BOOL |[isPortraitVideo](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-isportraitvideo) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-initwithportrait) |
|instancetype |[initWithPortrait:basePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-initwithportrait-baseplayerview) |
|UIView\* |[customizeVodContinuePlaybackToastView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-customizevodcontinueplaybacktoastview) |
|void |[customizeSpeedView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-customizespeedview) |
|void |[showControlViewIfNeededWithAutoHide:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-showcontrolviewifneededwithautohide) |
|void |[hideControlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-hidecontrolview) |
|void |[autoHideControlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-autohidecontrolview) |
|BOOL |[canFloating](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-canfloating) |
|void |[enterFullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-enterfullscreen) |
|void |[leaveFullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-leavefullscreen) |
|UIImage\* |[getFloatingCloseImage](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-getfloatingcloseimage) |
|CGSize |[getFloatingCloseImageSize](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-getfloatingcloseimagesize) |
|CGSize |[getCurrentShowingMediaSize](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-getcurrentshowingmediasize) |
|void |[updatePlayerWhenLeaveFullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-updateplayerwhenleavefullscreen) |
|void |[addBasePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-addbaseplayerview) |
|BDLBasePlayerView |[removeBasePlayerViewFromSuperview](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-removebaseplayerviewfromsuperview) |
|void |[play](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-play) |
|void |[pause](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-pause) |
|void |[stop](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-stop) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerView-popupsuperview"></span>
### popupSuperView

```objectivec
@property (nonatomic, weak) UIView *popupSuperView;
```


The parent view for displaying the dialog box. The SDK has a default implementation for dialog boxes such as the playback speed and resolution. The dialog box will be added on top of `popupSuperView`.

<span id="BDLPlayerView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLPlayerViewDelegate> delegate;
```


The delegate method. For more information, see [BDLPlayerViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLPlayerViewDelegate).

<span id="BDLPlayerView-baseplayerview"></span>
### basePlayerView

```objectivec
@property (nonatomic, strong, readonly, nullable) BDLBasePlayerView *basePlayerView;
```


The custom player view. `playerView` holds a `basePlayerView` and adds the control logic. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView).

<span id="BDLPlayerView-playermaskview"></span>
### playerMaskView

```objectivec
@property (nonatomic, strong) BDLPlayerMaskView *playerMaskView;
```


The player mask view, including the live room status, watermark, and popularity view. For more information, see [BDLPlayerMaskView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerMaskView).

<span id="BDLPlayerView-controlview"></span>
### controlView

```objectivec
@property (nonatomic, strong) BDLPlayerControlView *controlView;
```


The player control view, including the play button, pause button, progress bar, refresh button, full\-screen button, and time text. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerControlView).

<span id="BDLPlayerView-resolutionview"></span>
### resolutionView

```objectivec
@property (nonatomic, strong, nullable) BDLPlayerResolutionView *resolutionView;
```


The resolution selection view. For more information, see [BDLPlayerResolutionView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerResolutionView).`

<span id="BDLPlayerView-speedview"></span>
### speedView

```objectivec
@property (nonatomic, strong, nullable) BDLPlayerSpeedView *speedView;
```


The playback speed selection view. For more information, see [BDLPlayerSpeedView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView).

<span id="BDLPlayerView-loadingview"></span>
### loadingView

```objectivec
@property (nonatomic, strong, nullable) BDLLoadingView *loadingView;
```


The loading view. For more information, see [BDLLoadingView](https://docs.byteplus.com/en/docs/11/5590#BDLLoadingView).

<span id="BDLPlayerView-networknotreachableview"></span>
### networkNotReachableView

```objectivec
@property (nonatomic, strong, nullable) BDLNetworkNotReachableView *networkNotReachableView;
```


The network disconnection prompt view. For more information, see [BDLNetworkNotReachableView](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkNotReachableView).

<span id="BDLPlayerView-networkviawwanview"></span>
### networkViaWWANView

```objectivec
@property (nonatomic, strong, nullable) BDLNetworkViaWWANView *networkViaWWANView;
```


The mobile data access prompt view. For more information, see [BDLNetworkViaWWANView](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkViaWWANView).

<span id="BDLPlayerView-replayview"></span>
### replayView

```objectivec
@property (nonatomic, strong, nullable) BDLPlayerReplayView *replayView;
```


The replay view. For more information, see [BDLPlayerReplayView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerReplayView).

<span id="BDLPlayerView-continueplaybacktoastview"></span>
### continuePlaybackToastView

```objectivec
@property (nonatomic, strong, nullable) BDLContinuePlaybackToastView *continuePlaybackToastView;
```


The breakpoint resumption prompt view. For more information, see [BDLContinuePlaybackToastView](https://docs.byteplus.com/en/docs/11/5590#BDLContinuePlaybackToastView).

<span id="BDLPlayerView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLPlayerConfiguration *config;
```


The player configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration).

<span id="BDLPlayerView-ispipstarted"></span>
### isPiPStarted

```objectivec
@property (nonatomic, assign, readonly) BOOL isPiPStarted;
```


Whether the system PiP mode is started.


* `YES`: Started.

* `NO`: Not started.

    &nbsp;


<span id="isfullscreen"></span>
### isFullScreen

```objectivec
@property (nonatomic, assign, readonly) BOOL isFullScreen;
```


Whether in full\-screen mode.


* `YES`: In full\-screen mode.

* `NO`: Not in full\-screen mode.

    &nbsp;


<span id="isplayerfullsuper"></span>
### isPlayerFullSuper

```objectivec
@property (nonatomic, assign) BOOL isPlayerFullSuper;
```


Whether the player is in full\-screen mode.


* `YES`: In full\-screen mode.

* `NO`: Not in full\-screen mode.

    &nbsp;


<span id="isportraitvideo"></span>
### isPortraitVideo

```objectivec
@property (nonatomic, assign) BOOL isPortraitVideo;
```


Whether the video height is greater than the width.


* `YES`: Height is greater than the width.

* `NO`: Height is less than the width.


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the player view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode. The aspect ratios of source stream videos are different, resulting in different display styles for the video and the control interface (interaction buttons such as the play button).<br><br>&nbsp;<br><br>   * When the width of the source stream video is greater than or equal to its height: The video width is equal to the player width, and the video height is 9/16 of the player width, with the video positioned 120 px from the top of the player. The control interface is located at the bottom of the video, with a full\-screen button included by default.<br><br>   * When the width of the source stream video is less than its height: The video occupies the entire player. When playing VOD videos, the control interface is at the bottom of the player, but the player does not have the control interface during a live stream.<br><br>* `NO`: Landscape mode. Regardless of the aspect ratio of the source stream video, the video occupies the entire player, with the control interface located at the bottom of the player. |


**Return Value**

The instance of the player view.

<span id="BDLPlayerView-initwithportrait-baseplayerview"></span>
### initWithPortrait:basePlayerView:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait basePlayerView:(nullable BDLBasePlayerView *)basePlayerView;
```


Initializes the instance of the player view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode. The aspect ratios of source stream videos are different, resulting in different display styles for the video and the control interface (interaction buttons such as the play button).<br><br>&nbsp;<br><br>   * When the width of the source stream video is greater than or equal to its height: The video width is equal to the player width, and the video height is 9/16 of the player width, with the video positioned 120 px from the top of the player. The control interface is located at the bottom of the video, with a full\-screen button included by default.<br><br>   * When the width of the source stream video is less than its height: The video occupies the entire player. When playing VOD videos, the control interface is at the bottom of the player, but the player does not have the control interface during a live stream.<br><br>* `NO`: Landscape mode. Regardless of the aspect ratio of the source stream video, the video occupies the entire player, with the control interface located at the bottom of the player. |
|basePlayerView |nullable BDLBasePlayerView\* |The custom player that has already started playing. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView). |


**Return Value**

The instance of the player view.

<span id="BDLPlayerView-customizevodcontinueplaybacktoastview"></span>
### customizeVodContinuePlaybackToastView

```objectivec
@property (nonatomic, copy) __kindof UIView * (^customizeVodContinuePlaybackToastView)(BDLPlayerView *view, BDLContinuePlaybackToastView *toastView, NSTimeInterval currentPlaybackTime);
```


Customizes the breakpoint resumption prompt view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLPlayerView\* |The player view. |
|toastView |BDLContinuePlaybackToastView\* |The breakpoint resumption prompt view. For more information, see [BDLContinuePlaybackToastView](https://docs.byteplus.com/en/docs/11/5590#BDLContinuePlaybackToastView). |
|currentPlaybackTime |NSTimeInterval |The current playback time. Unit: seconds. |


**Return Value**

Instances of `UIView` and its subclasses.

<span id="BDLPlayerView-customizespeedview"></span>
### customizeSpeedView

```objectivec
@property (nonatomic, copy) void (^customizeSpeedView)(BDLPlayerView *playerView, BDLPlayerSpeedView *speedView);
```


Customizes the playback speed selection interface.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. |
|speedView |BDLPlayerSpeedView\* |The playback speed selection view. For more information, see [BDLPlayerSpeedView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView). |


<span id="BDLPlayerView-showcontrolviewifneededwithautohide"></span>
### showControlViewIfNeededWithAutoHide:

```objectivec
- (void)showControlViewIfNeededWithAutoHide:(BOOL)autoHide;
```


Displays the [controlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-controlview).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|autoHide |BOOL |Whether to hide automatically.<br><br><br>&nbsp;<br><br>* `YES`: Hide automatically.<br><br>* `NO`: Do not hide automatically. |


<span id="BDLPlayerView-hidecontrolview"></span>
### hideControlView

```objectivec
- (void)hideControlView;
```


Hides the [controlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-controlview).

<span id="BDLPlayerView-autohidecontrolview"></span>
### autoHideControlView

```objectivec
- (void)autoHideControlView;
```


Automatically hides the [controlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-controlview).

<span id="BDLPlayerView-canfloating"></span>
### canFloating

```objectivec
- (BOOL)canFloating;
```


Whether the video can play in the floating player.

**Return Value**


* `YES`: Can play in the floating player.

* `NO`: Cannot play in the floating player.

    &nbsp;


<span id="enterfullscreen"></span>
### enterFullScreen

```objectivec
- (void)enterFullScreen;
```


Enters full\-screen mode. Call this method after implementing the full\-screen logic externally to change the status of the [controlView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView-controlview)'s full\-screen button.

<span id="BDLPlayerView-leavefullscreen"></span>
### leaveFullScreen

```objectivec
- (void)leaveFullScreen;
```


Exits full\-screen mode.

<span id="BDLPlayerView-getfloatingcloseimage"></span>
### getFloatingCloseImage

```objectivec
- (UIImage *)getFloatingCloseImage;
```


Gets the image of the floating player's close button.

**Return Value**

The image of the floating player's close button.

<span id="BDLPlayerView-getfloatingcloseimagesize"></span>
### getFloatingCloseImageSize

```objectivec
- (CGSize)getFloatingCloseImageSize;
```


Gets the image size of the floating player's close button.

**Return Value**

The image size of the floating player's close button.

<span id="BDLPlayerView-getcurrentshowingmediasize"></span>
### getCurrentShowingMediaSize

```objectivec
- (CGSize)getCurrentShowingMediaSize;
```


Gets the size of the currently displayed media file (image or video).

**Return Value**

The size of the currently displayed media file (image or video).

<span id="BDLPlayerView-updateplayerwhenleavefullscreen"></span>
### updatePlayerWhenLeaveFullScreen

```objectivec
- (void)updatePlayerWhenLeaveFullScreen;
```


Updates the player when exiting full\-screen mode.

<span id="BDLPlayerView-addbaseplayerview"></span>
### addBasePlayerView:

```objectivec
- (void)addBasePlayerView:(BDLBasePlayerView *)basePlayerView;
```


Adds `basePlayerView`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView). |


<span id="BDLPlayerView-removebaseplayerviewfromsuperview"></span>
### removeBasePlayerViewFromSuperview

```objectivec
- (BDLBasePlayerView *)removeBasePlayerViewFromSuperview;
```


Removes `basePlayerView` from [BDLPlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerView) to not have `basePlayerView` displayed on the interface, while the property `self.basePlayerView` is not 'nil', and `BDLPlayerView` retains a reference to `basePlayerView`.

**Return Value**

The removed `basePlayerView`.

<span id="BDLPlayerView-play"></span>
### play

```objectivec
- (void)play;
```


Plays the video.

<span id="BDLPlayerView-pause"></span>
### pause

```objectivec
- (void)pause;
```


Pauses the video.

<span id="BDLPlayerView-stop"></span>
### stop

```objectivec
- (void)stop;
```


Stops playing the video.

<span id="BDLiveManager"></span>
# BDLiveManager

```objectivec
@interface BDLiveManager : NSObject
```


The entry class of BytePlus Live SDK.

<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|instancetype |[sharedInstance](https://docs.byteplus.com/en/docs/11/5590#BDLiveManager-sharedinstance) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/11/5590#BDLiveManager-startwithauthinfo-complete) |


<span id="instructions"></span>
## Instructions

<span id="BDLiveManager-sharedinstance"></span>
### sharedInstance

```objectivec
+ (instancetype)sharedInstance;
```


Gets the `BDLiveManager` instance.

**Return Value**

The `BDLiveManager` instance.

<span id="BDLiveManager-startwithauthinfo-complete"></span>
### startWithAuthInfo:complete:

```objectivec
- (void)startWithAuthInfo:(BDLiveAuthInfo *)authInfo
                 complete:(BDLiveManagerCompleteBlock)complete;
```


Initializes the SDK. You must call this method after connecting to the network.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|authInfo |BDLiveAuthInfo\* |Authorization information. For more information, see [BDLiveAuthInfo](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLiveAuthInfo). |
|complete |BDLiveManagerCompleteBlock |The callback triggered when the SDK initialization is complete. For more information, see [BDLiveManagerCompleteBlock](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#bdlivemanagercompleteblock). |


<span id="BDLScrollTextView"></span>
# BDLScrollTextView

```objectivec
@interface BDLScrollTextView : UIView
```


The live room description text view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLScrollDirection |[scrollDirection](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-scrolldirection) |
|float |[scrollSpeed](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-scrollspeed) |
|NSTimeInterval |[pauseInterval](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-pauseinterval) |
|NSInteger |[labelSpacing](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-labelspacing) |
|UIViewAnimationOptions |[animationOptions](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-animationoptions) |
|BOOL |[scrolling](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-scrolling) |
|CGFloat |[fadeLength](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-fadelength) |
|UIFont\* |[font](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-font) |
|NSString\* |[text](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-text) |
|NSAttributedString\* |[attributedText](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-attributedtext) |
|UIColor\* |[textColor](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-textcolor) |
|NSTextAlignment |[textAlignment](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-textalignment) |
|UIColor\* |[shadowColor](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-shadowcolor) |
|CGSize |[shadowOffset](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-shadowoffset) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[refreshLabels](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-refreshlabels) |
|void |[setText:refreshLabels:](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-settext-refreshlabels) |
|void |[setAttributedText:refreshLabels:](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-setattributedtext-refreshlabels) |
|void |[scrollLabelIfNeeded](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-scrolllabelifneeded) |
|void |[observeApplicationNotifications](https://docs.byteplus.com/en/docs/11/5590#BDLScrollTextView-observeapplicationnotifications) |


<span id="instructions"></span>
## Instructions

<span id="BDLScrollTextView-scrolldirection"></span>
### scrollDirection

```objectivec
@property (nonatomic, assign) BDLScrollDirection scrollDirection;
```


The scroll direction. For more information, see [BDLScrollDirection](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLScrollDirection).

<span id="BDLScrollTextView-scrollspeed"></span>
### scrollSpeed

```objectivec
@property (nonatomic, assign) float scrollSpeed;
```


The scroll speed, namely the number of points scrolled per second. Unit: points. Default value: `30`.

<span id="BDLScrollTextView-pauseinterval"></span>
### pauseInterval

```objectivec
@property (nonatomic, assign) NSTimeInterval pauseInterval;
```


The interval of pause between two scrolls. Unit: seconds. The default value is `0.0`, indicating continuous scrolling.

<span id="BDLScrollTextView-labelspacing"></span>
### labelSpacing

```objectivec
@property (nonatomic, assign) NSInteger labelSpacing;
```


The blank space on the left side of the label. Unit: points. Default value: `20`.

<span id="BDLScrollTextView-animationoptions"></span>
### animationOptions

```objectivec
@property (nonatomic, assign) UIViewAnimationOptions animationOptions;
```


The animation options during scrolling.

<span id="BDLScrollTextView-scrolling"></span>
### scrolling

```objectivec
@property (nonatomic, assign, readonly) BOOL scrolling;
```


Whether scrolling。


* `YES`: Scrolling.

* `NO`: Not scrolling.

    &nbsp;


<span id="fadelength"></span>
### fadeLength

```objectivec
@property (nonatomic, assign) CGFloat fadeLength;
```


The length of the gradient mask. Unit: points. Default value: `7.0`.

<span id="BDLScrollTextView-font"></span>
### font

```objectivec
@property (nonatomic, strong) UIFont *font;
```


The font and font size.

<span id="BDLScrollTextView-text"></span>
### text

```objectivec
@property (nonatomic, copy, nullable) NSString *text;
```


The text.

<span id="BDLScrollTextView-attributedtext"></span>
### attributedText

```objectivec
@property (nonatomic, copy, nullable) NSAttributedString *attributedText;
```


The rich text.

<span id="BDLScrollTextView-textcolor"></span>
### textColor

```objectivec
@property (nonatomic, strong) UIColor *textColor;
```


The text color.

<span id="BDLScrollTextView-textalignment"></span>
### textAlignment

```objectivec
@property (nonatomic, assign) NSTextAlignment textAlignment;
```


The text alignment. Effective when not scrolling automatically.

<span id="BDLScrollTextView-shadowcolor"></span>
### shadowColor

```objectivec
@property (nonatomic, strong, nullable) UIColor *shadowColor;
```


The shadow color.

<span id="BDLScrollTextView-shadowoffset"></span>
### shadowOffset

```objectivec
@property (nonatomic, assign) CGSize shadowOffset;
```


The shadow offset.

<span id="instructions"></span>
## Instructions

<span id="BDLScrollTextView-refreshlabels"></span>
### refreshLabels

```objectivec
- (void)refreshLabels;
```


Refreshes the label.

<span id="BDLScrollTextView-settext-refreshlabels"></span>
### setText:refreshLabels:

```objectivec
- (void)setText:(nullable NSString *)text refreshLabels:(BOOL)refresh;
```


Sets the text.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|text |nullable NSString\* |The text. |
|refresh |BOOL |Whether refresh is needed.<br><br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLScrollTextView-setattributedtext-refreshlabels"></span>
### setAttributedText:refreshLabels:

```objectivec
- (void)setAttributedText:(nullable NSAttributedString *)theText refreshLabels:(BOOL)refresh;
```


Sets the rich text.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|theText |nullable NSAttributedString\* |The rich text. |
|refresh |BOOL |Whether refresh is needed.<br><br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLScrollTextView-scrolllabelifneeded"></span>
### scrollLabelIfNeeded

```objectivec
- (void)scrollLabelIfNeeded;
```


Scrolls the label.

<span id="BDLScrollTextView-observeapplicationnotifications"></span>
### observeApplicationNotifications

```objectivec
- (void)observeApplicationNotifications;
```


Listens to notifications (`UIApplicationDidBecomeActiveNotification` and `UIApplicationWillEnterForegroundNotification`) when the app enters the foreground to refresh and start scrolling the label.

<span id="BDLPlayerSliderView"></span>
# BDLPlayerSliderView

```objectivec
@interface BDLPlayerSliderView : UIView
```


The player progress bar view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[thumbView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-thumbview) |
|UIView\* |[backgroundView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-backgroundview) |
|UIView\* |[trackProgressView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-trackprogressview) |
|UIView\* |[cacheProgressView](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-cacheprogressview) |
|id<BDLPlayerSliderViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-delegate) |
|CGFloat |[progress](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-progress) |
|CGFloat |[cacheProgress](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-cacheprogress) |
|BOOL |[sliding](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-sliding) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-initwithconfig) |
|void |[setProgress:animated:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-setprogress-animated) |
|void |[setCacheProgress:animated:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-setcacheprogress-animated) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSliderView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerSliderView-thumbview"></span>
### thumbView

```objectivec
@property (nonatomic, strong) UIView *thumbView;
```


The small dot of the current position. All properties except `frame` can be customized.

<span id="BDLPlayerSliderView-backgroundview"></span>
### backgroundView

```objectivec
@property (nonatomic, strong) UIView *backgroundView;
```


The background view. All properties except `frame` can be customized.

<span id="BDLPlayerSliderView-trackprogressview"></span>
### trackProgressView

```objectivec
@property (nonatomic, strong) UIView *trackProgressView;
```


The current progress view. You can customize the background color by using [themeColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-themecolor).

<span id="BDLPlayerSliderView-cacheprogressview"></span>
### cacheProgressView

```objectivec
@property (nonatomic, strong) UIView *cacheProgressView;
```


The cache progress view.

<span id="BDLPlayerSliderView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLPlayerSliderViewDelegate> delegate;
```


The delegate method. For more information, see [BDLPlayerSliderViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLPlayerSliderViewDelegate).

<span id="BDLPlayerSliderView-progress"></span>
### progress

```objectivec
@property (nonatomic, assign, readonly) CGFloat progress;
```


The current progress. Value range: [0,1].

<span id="BDLPlayerSliderView-cacheprogress"></span>
### cacheProgress

```objectivec
@property (nonatomic, assign, readonly) CGFloat cacheProgress;
```


The cache progress. Value range: [0,1].

<span id="BDLPlayerSliderView-sliding"></span>
### sliding

```objectivec
@property (nonatomic, assign, readonly, getter=isSliding) BOOL sliding;
```


Whether being dragged.


* `YES`: Being dragged.

* `NO`: Not being dragged.


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerSliderView-initwithconfig"></span>
### initWithConfig:

```objectivec
- (instancetype)initWithConfig:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the player progress bar view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the player progress bar view.

<span id="BDLPlayerSliderView-setprogress-animated"></span>
### setProgress:animated:

```objectivec
- (void)setProgress:(CGFloat)progress animated:(BOOL)animated;
```


Sets the current playback progress.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|progress |CGFloat |The current playback progress. Value range: [0,1]. |
|animated |BOOL |Whether animation is needed.<br><br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLPlayerSliderView-setcacheprogress-animated"></span>
### setCacheProgress:animated:

```objectivec
- (void)setCacheProgress:(CGFloat)progress animated:(BOOL)animated;
```


Sets the cache progress.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|progress |CGFloat |The cache progress. Value range: [0,1]. |
|animated |BOOL |Whether animation is needed.<br><br><br>* `YES`: Needed.<br><br>* `NO`: Not needed. |


<span id="BDLPlayerSliderView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLFloatingCardView"></span>
# BDLFloatingCardView

```objectivec
@interface BDLFloatingCardView : BDLBaseView
```


The floating product card view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLFloatingCardConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingCardView-config) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[closeButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingCardView-closebuttonclickedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingCardView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLFloatingCardConfiguration *config;
```


The configuration of the floating product card. For more information, see [BDLFloatingCardConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLFloatingCardConfiguration(Config)).

<span id="instructions"></span>
## Instructions

<span id="BDLFloatingCardView-closebuttonclickedblock"></span>
### closeButtonClickedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^closeButtonClickedBlock)(void);
```


The callback is triggered when the close button is tapped.

<span id="BDLImageTextView"></span>
# BDLImageTextView

```objectivec
@interface BDLImageTextView : BDLBaseView
```


The graphics menu view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLImageTextViewConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLImageTextView-config) |
|BDLRichTextWebView\* |[webView](https://docs.byteplus.com/en/docs/11/5590#BDLImageTextView-webview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateWithImageText:defaultColor:](https://docs.byteplus.com/en/docs/11/5590#BDLImageTextView-updatewithimagetext-defaultcolor) |


<span id="instructions"></span>
## Instructions

<span id="BDLImageTextView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLImageTextViewConfiguration *config;
```


The configuration of the graphics menu. For more information, see [BDLImageTextViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLImageTextViewConfiguration).

<span id="BDLImageTextView-webview"></span>
### webView

```objectivec
@property (nonatomic, strong) BDLRichTextWebView *webView;
```


The WebView that displays text and images. For more information, see [BDLRichTextWebView](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLRichTextWebView). All properties except `frame` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLImageTextView-updatewithimagetext-defaultcolor"></span>
### updateWithImageText:defaultColor:

```objectivec
- (void)updateWithImageText:(NSString *)richText defaultColor:(nullable UIColor *)defaultColor;
```


Updates based on rich text.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|richText |NSString\* |HTML5 code. |
|defaultColor |nullable UIColor\* |The default color.<br><br>&nbsp;<br><br>If [imageTextTextColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLImageTextViewConfiguration(Config)-imagetexttextcolor) is `nil`, this color is used. If this color is also `nil`, the color of `richText` is used. |


<span id="BDLContinuePlaybackToastView"></span>
# BDLContinuePlaybackToastView

```objectivec
@interface BDLContinuePlaybackToastView : UIView
```


The breakpoint resumption prompt view. The prompt is displayed only when the viewing page language is Simplified Chinese.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UILabel\* |[label](https://docs.byteplus.com/en/docs/11/5590#BDLContinuePlaybackToastView-label) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPlaybackTime:languageType:](https://docs.byteplus.com/en/docs/11/5590#BDLContinuePlaybackToastView-initwithplaybacktime-languagetype) |


<span id="instructions"></span>
## Instructions

<span id="BDLContinuePlaybackToastView-label"></span>
### label

```objectivec
@property (nonatomic, strong) UILabel *label;
```


The breakpoint resumption prompt label. All properties except `text` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLContinuePlaybackToastView-initwithplaybacktime-languagetype"></span>
### initWithPlaybackTime:languageType:

```objectivec
- (instancetype)initWithPlaybackTime:(NSTimeInterval)time languageType:(BDLLanguageType)languageType;
```


Initializes the instance of the breakpoint resumption prompt view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|time |NSTimeInterval |The position to which the video seeks after automatically resuming from where it stopped. Unit: seconds. |
|languageType |BDLLanguageType |The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType). |


**Return Value**

The instance of the breakpoint resumption prompt view.

<span id="BDLMenuBarView"></span>
# BDLMenuBarView

```objectivec
@interface BDLMenuBarView : BDLBaseView <
BDLProductService
, BDLLanguageService
, BDLMenuService
, BDLRichTextService
, BDLBasicService
, BDLCommentConfigService
>
```


The menu bar view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLMenuBarConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-config) |
|BDLMenuView\* |[menuView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-menuview) |
|BDLCommentAndNoticeView\* |[commentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-commentandnoticeview) |
|BDLHotCommentView\* |[hotCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-hotcommentview) |
|BDLMenuFilterOption |[filterOption](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-filteroption) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[customizeCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-customizecommentandnoticeview) |
|BDLBaseView |[customizeHotCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-customizehotcommentview) |
|BDLBaseView |[customizeImageTextView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-customizeimagetextview) |
|UIView\* |[customizeEmbeddedUrlWebView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-customizeembeddedurlwebview) |
|instancetype |[initWithPortrait:filterOption:](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-initwithportrait-filteroption) |
|void |[indexDidChangeBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-indexdidchangeblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLMenuBarView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLMenuBarConfiguration *config;
```


The configuration of the menu bar. For more information, see [BDLMenuBarConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLMenuBarConfiguration).

<span id="BDLMenuBarView-menuview"></span>
### menuView

```objectivec
@property (nonatomic, strong) BDLMenuView *menuView;
```


The container view of the menu bar, which is used to implement the left and right sliding and switching of the menu bar. For more information, see [BDLMenuView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView).

<span id="BDLMenuBarView-commentandnoticeview"></span>
### commentAndNoticeView

```objectivec
@property (nonatomic, strong, nullable) BDLCommentAndNoticeView *commentAndNoticeView;
```


The comment and notification view for live rooms in landscape mode. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView).

<span id="BDLMenuBarView-hotcommentview"></span>
### hotCommentView

```objectivec
@property (nonatomic, strong, nullable) BDLHotCommentView *hotCommentView;
```


The top comment view for live rooms in landscape mode. For more information, see [BDLHotCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLHotCommentView).

<span id="BDLMenuBarView-filteroption"></span>
### filterOption

```objectivec
@property (nonatomic, assign, readonly) BDLMenuFilterOption filterOption;
```


The menu filter options, which is passed in through the initialization method [initWithPortrait:filterOption:](https://docs.byteplus.com/en/docs/11/5590#BDLMenuBarView-initwithportrait-filteroption).

<span id="instructions"></span>
## Instructions

<span id="BDLMenuBarView-customizecommentandnoticeview"></span>
### customizeCommentAndNoticeView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeCommentAndNoticeView)(BDLMenuBarView *view, BDLCommentAndNoticeView *commentAndNoticeView);
```


Customizes the comment and notification view for live rooms in landscape mode. All properties except `hidden` and `frame` can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMenuBarView\* |The menu bar view. |
|commentAndNoticeView |BDLCommentAndNoticeView\* |The comment and notification view. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView). |


<span id="BDLMenuBarView-customizehotcommentview"></span>
### customizeHotCommentView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeHotCommentView)(BDLMenuBarView *view, BDLHotCommentView *hotCommentView);
```


Customizes the top comment view for live rooms in landscape mode. All properties except `hidden` and `frame` can be customized. If you hide the `commentView`, the top comment view is not displayed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMenuBarView\* |The menu bar view. |
|hotCommentView |BDLHotCommentView\* |The top comment view. For more information, see [BDLHotCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLHotCommentView). |


**Return Value**

Instances of `BDLBaseView` and its subclasses.

<span id="BDLMenuBarView-customizeimagetextview"></span>
### customizeImageTextView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeImageTextView)(BDLMenuBarView *view, BDLImageTextView *imageTextView);
```


Customizes the graphics menu view for live rooms in landscape mode. All properties except `hidden` and `frame` can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMenuBarView\* |The menu bar view. |
|imageTextView |BDLImageTextView\* |The graphics menu view. For more information, see [BDLImageTextView](https://docs.byteplus.com/en/docs/11/5590#BDLImageTextView). |


**Return Value**

Instances of `BDLBaseView` and its subclasses.

<span id="BDLMenuBarView-customizeembeddedurlwebview"></span>
### customizeEmbeddedUrlWebView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView * _Nullable (^customizeEmbeddedUrlWebView)(BDLMenuBarView *view, WKWebView *webView);
```


Customizes the embedded link view. All properties except `hidden` and `frame` can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMenuBarView\* |The menu bar view. |
|webView |WKWebView\* |The WebView that displays content. |


**Return Value**

Instances of `UIView` and its subclasses.

<span id="BDLMenuBarView-initwithportrait-filteroption"></span>
### initWithPortrait:filterOption:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait filterOption:(BDLMenuFilterOption)filterOption;
```


Initializes the instance of the menu bar view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|filterOption |BDLMenuFilterOption |The menu filter options, displaying only the included menu types. For more information, see [BDLMenuFilterOption](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLMenuFilterOption). |


**Return Value**

The instance of the menu bar view.

<span id="BDLMenuBarView-indexdidchangeblock"></span>
### indexDidChangeBlock

```objectivec
@property (nonatomic, copy, nullable) void(^indexDidChangeBlock)(BDLMenuBarView *view, NSUInteger index);
```


The SDK calls this method when the selected menu changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMenuBarView\* |The menu bar view. |
|index |NSUInteger |The array index of the currently selected menu, with the index starting from 0. |


<span id="BDLHotCommentView"></span>
# BDLHotCommentView

```objectivec
@interface BDLHotCommentView : BDLCommentBaseView
```


The top comment view, which is inherited from [BDLCommentBaseView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView).

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[urlClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLHotCommentView-urlclickblock) |
|void |[nicknameClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLHotCommentView-nicknameclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLHotCommentView-urlclickblock"></span>
### urlClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^urlClickBlock)(__kindof BDLCommentBaseView *commentView, BDLCommentModel *comment, NSURL *url);
```


The callback is triggered when the URL in a comment is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentView |__kindof BDLCommentBaseView\* |The common base class for comments and top comments. For more information, see [BDLCommentBaseView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |
|url |NSURL\* |The tapped URL. |


<span id="BDLHotCommentView-nicknameclickblock"></span>
### nicknameClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^nicknameClickBlock)(__kindof BDLCommentBaseView *commentView, BDLCommentModel *comment);
```


The callback is triggered when the nickname is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentView |__kindof BDLCommentBaseView\* |The common base class for comments and top comments. For more information, see [BDLCommentBaseView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLMoreOptionsView"></span>
# BDLMoreOptionsView

```objectivec
@interface BDLMoreOptionsView : BDLPopupBottomShowBaseView <BDLLanguageService, BDLMoreOptionsService, BDLMenuItemsService>
```


The more options dialog box view.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The more options dialog box appears after viewers tap the more (...) icon in the lower\-right corner of the live room in portrait mode.</div>


<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLMoreOptionsViewBlock |[closeClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMoreOptionsView-closeclickblock) |
|UICollectionView\* |[optionsView](https://docs.byteplus.com/en/docs/11/5590#BDLMoreOptionsView-optionsview) |
|UIView\* |[splitView](https://docs.byteplus.com/en/docs/11/5590#BDLMoreOptionsView-splitview) |
|UIButton\* |[cancelButton](https://docs.byteplus.com/en/docs/11/5590#BDLMoreOptionsView-cancelbutton) |


<span id="instructions"></span>
## Instructions

<span id="BDLMoreOptionsView-closeclickblock"></span>
### closeClickBlock

```objectivec
@property (nonatomic, copy, nullable) BDLMoreOptionsViewBlock closeClickBlock;
```


The callback is triggered when viewers tap to close the more options dialog box. For more information, see [BDLMoreOptionsViewBlock](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#bdlmoreoptionsviewblock).

<span id="BDLMoreOptionsView-optionsview"></span>
### optionsView

```objectivec
@property (nonatomic, strong, readonly) UICollectionView *optionsView;
```


The options view. All properties except `frame` can be customized.

<span id="BDLMoreOptionsView-splitview"></span>
### splitView

```objectivec
@property (nonatomic, strong, readonly) UIView *splitView;
```


The divider line between the options and the bottom cancel button. All properties can be customized. Masonry is used internally for layout. To modify the `frame`, it is recommended to use `mas_remake`.

<span id="BDLMoreOptionsView-cancelbutton"></span>
### cancelButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *cancelButton;
```


The bottom cancel button. All properties can be customized. Masonry is used internally for layout. To modify the `frame`, it is recommended to use `mas_remake`.

<span id="BDLPageAdView"></span>
# BDLPageAdView

```objectivec
@interface BDLPageAdView : BDLBaseView <BDLPageAdViewProtocol, BDLMarketService, BDLBasicService>
```


The in\-page ad view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSArray<BDLAdvertisementModel\*\>\* |[showingPageAdModels](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-showingpageadmodels) |
|BDLPageAdViewConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-config) |
|UICollectionView\* |[collectionView](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-collectionview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-initwithportrait) |
|void |[viewTappedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-viewtappedblock) |
|void |[closeButtonClickedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-closebuttonclickedblock) |
|BOOL |[shouldShowAdBlock](https://docs.byteplus.com/en/docs/11/5590#BDLPageAdView-shouldshowadblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLPageAdView-showingpageadmodels"></span>
### showingPageAdModels

```objectivec
@property (nonatomic, copy, readonly) NSArray<BDLAdvertisementModel *> *showingPageAdModels;
```


The model of currently displayed ad. For more information, see [BDLAdvertisementModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLAdvertisementModel).

<span id="BDLPageAdView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLPageAdViewConfiguration *config;
```


The configuration of the current in\-page ad. For more information, see [BDLPageAdViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPageAdViewConfiguration).

<span id="BDLPageAdView-collectionview"></span>
### collectionView

```objectivec
@property (nonatomic, strong) UICollectionView *collectionView;
```


The in\-page ad carousel is implemented based on the `collectionView`.

<span id="instructions"></span>
## Instructions

<span id="BDLPageAdView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the in\-page ad view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the in\-page ad view.

<span id="BDLPageAdView-viewtappedblock"></span>
### viewTappedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^viewTappedBlock)(BDLPageAdView *view, BDLAdvertisementModel *ad, BOOL isFloatingEnable);
```


The callback is triggered when the in\-page ad is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLPageAdView\* |The in\-page ad view. |
|ad |BDLAdvertisementModel\* |The ad information, which is returned by the BytePlus Live server. For more information, see [BDLAdvertisementModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLAdvertisementModel). |
|isFloatingEnable |BOOL |Whether the ad details page is displayed on a floating page in the live room.<br><br><br>* `YES`: The ad details page is displayed on a floating page in the live room after viewers tap the in\-page ad. Viewers can watch the video and view the ad details page at the same time.<br><br>* `NO`: The ad details page is displayed on a new browser tab after viewers tap the in\-page ad. Viewers cannot watch the video and view the ad details page at the same time. |


<span id="BDLPageAdView-closebuttonclickedblock"></span>
### closeButtonClickedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^closeButtonClickedBlock)(void);
```


The callback is triggered when the close button is tapped.

<span id="BDLPageAdView-shouldshowadblock"></span>
### shouldShowAdBlock

```objectivec
@property (nonatomic, copy, nullable) BOOL (^shouldShowAdBlock)(BDLPageAdView *adView, BDLPageAdvertisementType type);
```


The callback is triggered when the in\-page or header ad is configured for live rooms in portrait mode or when the in\-page ad is configured for live rooms in landscape mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|adView |BDLPageAdView\* |The in\-page ad view. |
|type |BDLPageAdvertisementType |The ad type. For more information, see [BDLPageAdvertisementType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPageAdvertisementType). |


**Return Value**

Whether to display the ad. Default value: `YES`.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="bdlinteractiveawarditemtype"></span>
# BDLInteractiveAwardItemType

```objectivec
typedef NS_ENUM(
    NSInteger,
    BDLInteractiveAwardItemType
)
```


The prize type of lucky draws.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLInteractiveAwardItemTypeInKind |1 |Physical prizes. |
|BDLInteractiveAwardItemTypeTheoretical |2 |Virtual prizes. |
|BDLInteractiveAwardItemTypeCustom |3 |Custom prizes. |
|BDLInteractiveAwardItemTypeMillions |4 |Voucher prizes. |


<span id="BDLNoCommentView"></span>
# BDLNoCommentView

```objectivec
@interface BDLNoCommentView : BDLBaseView
```


The view when there are no comments in the comment area.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImageView\* |[imageView](https://docs.byteplus.com/en/docs/11/5590#BDLNoCommentView-imageview) |
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLNoCommentView-titlelabel) |


<span id="instructions"></span>
## Instructions

<span id="BDLNoCommentView-imageview"></span>
### imageView

```objectivec
@property (nonatomic, strong) UIImageView *imageView;
```


The `imageView`. All properties except `frame` and `image` can be customized. You can customize `image` by using [noCommentImage](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration(Config)-nocommentimage).

<span id="BDLNoCommentView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong) UILabel *titleLabel;
```


The text. All properties except `text` and `frame` can be customized.

<span id="BDLPeopleCountConfiguration(Config)"></span>
# BDLPeopleCountConfiguration(Config)

```objectivec
@interface BDLPeopleCountConfiguration (Config)
```


The popularity configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIFont\* |[textFont](https://docs.byteplus.com/en/docs/11/5590#BDLPeopleCountConfiguration(Config)-textfont) |
|UIColor\* |[textColor](https://docs.byteplus.com/en/docs/11/5590#BDLPeopleCountConfiguration(Config)-textcolor) |
|UIImage\* |[iconImage](https://docs.byteplus.com/en/docs/11/5590#BDLPeopleCountConfiguration(Config)-iconimage) |


<span id="instructions"></span>
## Instructions

<span id="BDLPeopleCountConfiguration(Config)-textfont"></span>
### textFont

```objectivec
@property (nonatomic, strong) UIFont *textFont;
```


The font and font size of the popularity tag text (font size unit: points).

<span id="BDLPeopleCountConfiguration(Config)-textcolor"></span>
### textColor

```objectivec
@property (nonatomic, strong) UIColor *textColor;
```


The color of the popularity tag text.

<span id="BDLPeopleCountConfiguration(Config)-iconimage"></span>
### iconImage

```objectivec
@property (nonatomic, strong) UIImage *iconImage;
```


The popularity icon.

<span id="BDLCommentView"></span>
# BDLCommentView

```objectivec
@interface BDLCommentView : BDLCommentInputBaseView <BDLNoticeService, BDLMessageSwitchService>
```


The comment area view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLMenuItemsController\* |[menuItemsController](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView-menuitemscontroller) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[customizeMoreOptionsController](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView-customizemoreoptionscontroller) |
|void |[urlClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView-urlclickblock) |
|void |[nicknameClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView-nicknameclickblock) |
|void |[textContentClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView-textcontentclickblock) |
|void |[sendTextMessage:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView-sendtextmessage-success-failure) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentView-menuitemscontroller"></span>
### menuItemsController

```objectivec
@property (nonatomic, strong, readonly) BDLMenuItemsController *menuItemsController;
```


The controller of the buttons at the bottom of the comment area.

<span id="instructions"></span>
## Instructions

<span id="BDLCommentView-customizemoreoptionscontroller"></span>
### customizeMoreOptionsController

```objectivec
@property (nonatomic, copy) void (^customizeMoreOptionsController)(BDLCommentView *view, BDLMoreOptionsController *controller);
```


Customizes the controller of the more options dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLCommentView\* |The comment area view. |
|controller |BDLMoreOptionsController\* |The controller of the more options dialog box. For more information, see [BDLMoreOptionsController](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLMoreOptionsController). |


<span id="BDLCommentView-urlclickblock"></span>
### urlClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^urlClickBlock)(__kindof BDLCommentBaseView *commentView, BDLCommentModel *comment, NSURL *url);
```


The callback is triggered when the URL in a comment is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentView |__kindof BDLCommentBaseView\* |The common base class for comments and top comments. For more information, see [BDLCommentBaseView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |
|url |NSURL\* |The tapped URL. |


<span id="BDLCommentView-nicknameclickblock"></span>
### nicknameClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^nicknameClickBlock)(__kindof BDLCommentBaseView *commentView, BDLCommentModel *comment);
```


The callback is triggered when the nickname is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentView |__kindof BDLCommentBaseView\* |The common base class for comments and top comments. For more information, see [BDLCommentBaseView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLCommentView-textcontentclickblock"></span>
### textContentClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^textContentClickBlock)(__kindof BDLCommentBaseView *commentView, BDLCommentModel *comment);
```


The callback is triggered when the text comment is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentView |__kindof BDLCommentBaseView\* |The common base class for comments and top comments. For more information, see [BDLCommentBaseView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentBaseView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLCommentView-sendtextmessage-success-failure"></span>
### sendTextMessage:success:failure:

```objectivec
- (void)sendTextMessage:(NSString *)text
                success:(void (^)(BDLSendActivityMessageResponse *response))success
                failure:(void (^)(NSError *error))failure;
```


Sends a text comment. The SDK triggers the corresponding callback after the comment is successfully sent or failed to send.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|text |NSString\* |The comment content. |
|success |void(^)(BDLSendActivityMessageResponse\*response) |The callback triggered when the comment is successfully sent.<br><br>&nbsp;<br><br>Input parameters: The result after the comment is sent, which is returned by the BytePlus Live server. For more information, see [BDLSendActivityMessageResponse](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLSendActivityMessageResponse). |
|failure |void(^)(NSError\*error) |The callback triggered when the comment failed to send.<br><br>&nbsp;<br><br>Input parameters: The error information. For more information, see [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=l_1&language=objc). |


<span id="BDLCommentViewCell"></span>
# BDLCommentViewCell

```objectivec
@interface BDLCommentViewCell : UITableViewCell
```


The comment cell.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLCommentViewCellDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-delegate) |
|BDLCommentModel\* |[comment](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-comment) |
|UIView\* |[bgView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-bgview) |
|UITextView\* |[textView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-textview) |
|UIButton\* |[likeButton](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-likebutton) |
|UIButton\* |[avatarButton](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-avatarbutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateWithComment:config:isPortrait:isCommentTranslateEnable:isLikeEnable:isDarkTheme:langType:langTypes:](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCell-updatewithcomment-config-isportrait-iscommenttranslateenable-islikeenable-isdarktheme-langtype-langtypes) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewCell-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLCommentViewCellDelegate> delegate;
```


The delegate method. For more information, see [BDLCommentViewCellDelegate](https://docs.byteplus.com/en/docs/11/5590#BDLCommentViewCellDelegate).

<span id="BDLCommentViewCell-comment"></span>
### comment

```objectivec
@property (nonatomic, weak, readonly) BDLCommentModel *comment;
```


The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel).

<span id="BDLCommentViewCell-bgview"></span>
### bgView

```objectivec
@property (nonatomic, strong, readonly) UIView *bgView;
```


The background view.

<span id="BDLCommentViewCell-textview"></span>
### textView

```objectivec
@property (nonatomic, strong, readonly) UITextView *textView;
```


The text content view.

<span id="BDLCommentViewCell-likebutton"></span>
### likeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *likeButton;
```


The icon for liking comments.

<span id="BDLCommentViewCell-avatarbutton"></span>
### avatarButton

```objectivec
@property (nonatomic, strong) UIButton *avatarButton;
```


The user avatar button.

<span id="instructions"></span>
## Instructions

<span id="BDLCommentViewCell-updatewithcomment-config-isportrait-iscommenttranslateenable-islikeenable-isdarktheme-langtype-langtypes"></span>
### updateWithComment:config:isPortrait:isCommentTranslateEnable:isLikeEnable:isDarkTheme:langType:langTypes:

```objectivec
- (void)updateWithComment:(BDLCommentModel *)comment
                   config:(BDLCommentViewConfiguration *)config
               isPortrait:(BOOL)isPortrait
 isCommentTranslateEnable:(BOOL)isCommentTranslateEnable
             isLikeEnable:(BOOL)isLikeEnable
              isDarkTheme:(BOOL)isDarkTheme
                 langType:(BDLLanguageType)langType
                langTypes:(NSArray *)langTypes;
```


Updates the comment under the menu for chat interaction.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |
|config |BDLCommentViewConfiguration\* |The comment configuration. For more information, see [BDLCommentViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration(Config)). |
|isPortrait |BOOL |Whether the live room is in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|isCommentTranslateEnable |BOOL |Whether to enable the comment translation.<br><br><br>* `YES`: Enable.<br><br>* `NO`: Disable. |
|isLikeEnable |BOOL |Whether to enable the feature of liking comments.<br><br><br>* `YES`: Enable.<br><br>* `NO`: Disable. |
|isDarkTheme |BOOL |Whether the theme is dark mode.<br><br><br>* `YES`: Dark mode.<br><br>* `NO`: Not dark mode. |
|langType |BDLLanguageType |The current language type. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType). |
|langTypes |NSArray\* |All the currently supported language types. |


<span id="BDLInteractiveToolView"></span>
# BDLInteractiveToolView

```objectivec
@interface BDLInteractiveToolView : BDLBaseView <BDLInteractiveToolService, BDLLanguageService, BDLMenuService, BDLBasicService>
```


The interaction tools menu view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UILabel\* |[nameLabel](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-namelabel) |
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-closebutton) |
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-isportrait) |
|BOOL |[urlFloatingEnable](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-urlfloatingenable) |
|BDLInteractiveToolConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-config) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[urlClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-urlclickblock) |
|void |[onContextClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-oncontextclickblock) |
|void |[onCloseBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-oncloseblock) |
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView-initwithportrait) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolView-namelabel"></span>
### nameLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *nameLabel;
```


The name label for live rooms in portrait mode. All properties except `text`, `textColor`, and `frame` can be customized.

<span id="BDLInteractiveToolView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *closeButton;
```


The close button of the interaction tools dialog box.

<span id="BDLInteractiveToolView-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.

    &nbsp;


<span id="urlfloatingenable"></span>
### urlFloatingEnable

```objectivec
@property (nonatomic, assign, readonly) BOOL urlFloatingEnable;
```


Whether the redirected content is displayed on a floating page in the live room after viewers tap the URL.


* `YES`: The redirected content is displayed on a floating page in the live room. Viewers can watch the video and view the redirected content at the same time.

* `NO`: The redirected content is displayed on a new browser tab. Viewers cannot watch the video and view the redirected content at the same time.

    &nbsp;


<span id="config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLInteractiveToolConfiguration *config;
```


The configuration of interaction tools menu. For more information, see [BDLInteractiveToolConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveToolConfiguration).

<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolView-urlclickblock"></span>
### urlClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^urlClickBlock)(BDLInteractiveToolView *view, NSURL *url);
```


The callback is triggered when the URL under the menu for interaction tools is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLInteractiveToolView\* |The interaction tools menu view. |
|url |NSURL\* |The tapped URL. |


<span id="BDLInteractiveToolView-oncontextclickblock"></span>
### onContextClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onContextClickBlock)(BDLInteractiveToolView *view, BDLInteractiveToolModel *model, BDLInteractiveContextModel *context);
```


The callback is triggered when the context of interaction tools is tapped. The context of interaction tools refers to interaction tools such as lucky draws, quizzes, and questionnaires under the menu for interaction tools.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLInteractiveToolView\* |The interaction tools menu view. |
|model |BDLInteractiveToolModel\* |The model of interaction tools. For more information, see [BDLInteractiveToolModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveToolModel). |
|context |BDLInteractiveContextModel\* |The content model of interaction tools. For more information, see [BDLInteractiveContextModel](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel). |


<span id="BDLInteractiveToolView-oncloseblock"></span>
### onCloseBlock

```objectivec
@property (nonatomic, copy, nullable) void (^onCloseBlock)(BDLInteractiveToolView *view);
```


The callback is triggered when the close button of the interaction tools dialog box is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLInteractiveToolView\* |The interaction tools menu view. |


<span id="BDLInteractiveToolView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait;
```


Initializes the instance of the interaction tools menu view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the interaction tools menu view.

<span id="BDLAwardUserResponse"></span>
# BDLAwardUserResponse

```objectivec
@interface BDLAwardUserResponse : BDLBaseResponse
```


The lucky draw viewer information, which is returned by the BytePlus Live server.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLAwardUserModel\* |[result](https://docs.byteplus.com/en/docs/11/5590#BDLAwardUserResponse-result) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardUserResponse-result"></span>
### result

```objectivec
@property (nonatomic, strong) BDLAwardUserModel *result;
```


The model of lucky draw\-related viewer information. For more information, see [BDLAwardUserModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLAwardUserModel).

<span id="BDLQuestionAnswerModel"></span>
# BDLQuestionAnswerModel

```objectivec
@interface BDLQuestionAnswerModel : BDLBaseModel
```


The questionnaire model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[questionId](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-questionid) |
|NSString\* |[question](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-question) |
|NSMutableSet<NSNumber\*\>\* |[answers](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-answers) |
|NSString\* |[answer](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-answer) |
|BDLQuestionnaireQuestionModel\* |[questionModel](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-questionmodel) |
|BOOL |[needShowWarning](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-needshowwarning) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[isAnswerValid](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel-isanswervalid) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionAnswerModel-questionid"></span>
### questionId

```objectivec
@property (nonatomic, strong) NSNumber *questionId;
```


The question ID.

<span id="BDLQuestionAnswerModel-question"></span>
### question

```objectivec
@property (nonatomic, copy) NSString *question;
```


The question content.

<span id="BDLQuestionAnswerModel-answers"></span>
### answers

```objectivec
@property (nonatomic, strong) NSMutableSet<NSNumber *> *answers;
```


The number of submitted questionnaires.

<span id="BDLQuestionAnswerModel-answer"></span>
### answer

```objectivec
@property (nonatomic, copy) NSString *answer;
```


The questionnaire content filled out by the viewer.

<span id="BDLQuestionAnswerModel-questionmodel"></span>
### questionModel

```objectivec
@property (nonatomic, strong) BDLQuestionnaireQuestionModel *questionModel;
```


The question model of a questionnaire. For more information, see [BDLQuestionnaireQuestionModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLQuestionnaireQuestionModel).

<span id="BDLQuestionAnswerModel-needshowwarning"></span>
### needShowWarning

```objectivec
@property (nonatomic, assign) BOOL needShowWarning;
```


Whether displaying the error message is needed.


* `YES`: Needed.

* `NO`: Not needed.


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionAnswerModel-isanswervalid"></span>
### isAnswerValid

```objectivec
- (BOOL)isAnswerValid;
```


Whether the questionnaire content filled out by the viewer is valid.

**Return Value**


* `YES`: Valid.

* `NO`: Invalid.

    &nbsp;


<span id="bdlawardcondition"></span>
# BDLAwardCondition

```objectivec
@interface BDLAwardCondition : BDLBaseModel
```


The conditions for participating in lucky draws.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[checkIn](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCondition-checkin) |
|NSString\* |[questionnaire](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCondition-questionnaire) |
|NSString\* |[quiz](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCondition-quiz) |
|NSString\* |[rightQuiz](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCondition-rightquiz) |
|NSString\* |[vote](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCondition-vote) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardCondition-checkin"></span>
### checkIn

```objectivec
@property (nonatomic, copy) NSString *checkIn;
```


The check\-in condition, including submitting all check\-ins and submitting at least the specified number of check\-ins.

<span id="BDLAwardCondition-questionnaire"></span>
### questionnaire

```objectivec
@property (nonatomic, copy) NSString *questionnaire;
```


The questionnaire condition, including submitting all questionnaires and submitting at least the specified number of questionnaires.

<span id="BDLAwardCondition-quiz"></span>
### quiz

```objectivec
@property (nonatomic, copy) NSString *quiz;
```


The quiz condition, including submitting all quizzes and submitting at least the specified number of quizzes.

<span id="BDLAwardCondition-rightquiz"></span>
### rightQuiz

```objectivec
@property (nonatomic, copy) NSString *rightQuiz;
```


The quiz condition, including correctly answering all quizzes and correctly answering at least the specified number of quizzes.

<span id="BDLAwardCondition-vote"></span>
### vote

```objectivec
@property (nonatomic, copy) NSString *vote;
```


The vote condition, including submitting all votes and submitting at least the specified number of votes.

<span id="BDLMenuItemsController"></span>
# BDLMenuItemsController

```objectivec
@interface BDLMenuItemsController : NSObject
```


The controller for the buttons at the bottom of the comment area.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isPortrait](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-isportrait) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[shoppingCardClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-shoppingcardclickblock) |
|void |[giftClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-giftclickblock) |
|BOOL |[likeClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-likeclickblock) |
|void |[interactiveToolClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-interactivetoolclickblock) |
|void |[imageTextClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-imagetextclickblock) |
|void |[embeddedUrlClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-embeddedurlclickblock) |
|void |[shareClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-shareclickblock) |
|void |[moreOptionsClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-moreoptionsclickblock) |
|instancetype |[initWithConfig:portrait:](https://docs.byteplus.com/en/docs/11/5590#BDLMenuItemsController-initwithconfig-portrait) |


<span id="instructions"></span>
## Instructions

<span id="BDLMenuItemsController-isportrait"></span>
### isPortrait

```objectivec
@property (nonatomic, assign, readonly) BOOL isPortrait;
```


Whether the live room is in portrait mode.


* `YES`: Portrait mode.

* `NO`: Landscape mode.


<span id="instructions"></span>
## Instructions

<span id="BDLMenuItemsController-shoppingcardclickblock"></span>
### shoppingCardClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^shoppingCardClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the shopping cart button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-giftclickblock"></span>
### giftClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^giftClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the gift button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-likeclickblock"></span>
### likeClickBlock

```objectivec
@property (nonatomic, copy, nullable) BOOL (^likeClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the button for liking the live room is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


**Return Value**

Whether to display the tap animation.


* `YES`: Display.

* `NO`: Do not display.

    &nbsp;


<span id="interactivetoolclickblock"></span>
### interactiveToolClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^interactiveToolClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the interaction tools menu button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-imagetextclickblock"></span>
### imageTextClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^imageTextClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the graphics menu button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-embeddedurlclickblock"></span>
### embeddedUrlClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^embeddedUrlClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the embedded link menu button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-shareclickblock"></span>
### shareClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^shareClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the share button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-moreoptionsclickblock"></span>
### moreOptionsClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^moreOptionsClickBlock)(BDLMenuItemsController *controller);
```


The callback is triggered when the more options button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLMenuItemsController\* |The controller for the buttons at the bottom of the comment area. |


<span id="BDLMenuItemsController-initwithconfig-portrait"></span>
### initWithConfig:portrait:

```objectivec
- (instancetype)initWithConfig:(BDLCommentViewConfiguration *)config portrait:(BOOL)isPortrait;
```


Initializes the instance of the controller for the buttons at the bottom of the comment area.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLCommentViewConfiguration\* |The configuration. For more information, see [BDLCommentViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration(Config)). |
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the controller for the buttons at the bottom of the comment area.

<span id="BDLBusinessAccountView"></span>
# BDLBusinessAccountView

```objectivec
@interface BDLBusinessAccountView : BDLBaseView <BDLBusinessAccountService, BDLLanguageService, BDLPopularityService>
```


The host account view, which corresponds to the host account feature of BytePlus Live.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIImageView\* |[avatarImageView](https://docs.byteplus.com/en/docs/11/5590#BDLBusinessAccountView-avatarimageview) |
|UILabel\* |[nameLabel](https://docs.byteplus.com/en/docs/11/5590#BDLBusinessAccountView-namelabel) |
|UILabel\* |[popularityLabel](https://docs.byteplus.com/en/docs/11/5590#BDLBusinessAccountView-popularitylabel) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[viewTappedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLBusinessAccountView-viewtappedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLBusinessAccountView-avatarimageview"></span>
### avatarImageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *avatarImageView;
```


The avatar. All properties except rounded corners, image, and `frame` can be customized.

<span id="BDLBusinessAccountView-namelabel"></span>
### nameLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *nameLabel;
```


The account name label. All properties except `text` and `frame` can be customized.

<span id="BDLBusinessAccountView-popularitylabel"></span>
### popularityLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *popularityLabel;
```


The popularity label, including the popularity value and popularity icon. All properties except `text` and `frame` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLBusinessAccountView-viewtappedblock"></span>
### viewTappedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^viewTappedBlock)(NSString * _Nullable urlStr);
```


The callback is triggered when the host account view is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|urlStr |NSString\* |The embedded link, which is returned by the BytePlus Live server. |


<span id="BDLPeopleCountConfiguration"></span>
# BDLPeopleCountConfiguration

```objectivec
@interface BDLPeopleCountConfiguration : BDLRTBaseConfiguration
```


The popularity configuration.

<span id="BDLPopupInputView"></span>
# BDLPopupInputView

```objectivec
@interface BDLPopupInputView : BDLBaseView
```


The nickname text box view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLPopupInputView-closebutton) |
|UITextField\* |[inputTextField](https://docs.byteplus.com/en/docs/11/5590#BDLPopupInputView-inputtextfield) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[confirmBlock](https://docs.byteplus.com/en/docs/11/5590#BDLPopupInputView-confirmblock) |
|void |[closeBlock](https://docs.byteplus.com/en/docs/11/5590#BDLPopupInputView-closeblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupInputView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *closeButton;
```


The close button. Customization is supported.

<span id="BDLPopupInputView-inputtextfield"></span>
### inputTextField

```objectivec
@property (nonatomic, strong, readonly) UITextField *inputTextField;
```


The text box. All properties except `attributedPlaceholder`, `backgroundColor`, `textColor`, and `font` can be customized.

<span id="instructions"></span>
## Instructions

<span id="BDLPopupInputView-confirmblock"></span>
### confirmBlock

```objectivec
@property (nonatomic, copy, nullable) void (^confirmBlock)(NSString *__nullable text);
```


The callback is triggered when the confirm button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|text |NSString\*__nullable |The entered nickname. |


<span id="BDLPopupInputView-closeblock"></span>
### closeBlock

```objectivec
@property (nonatomic, copy, nullable) void (^closeBlock)(void);
```


The callback is triggered when the close button is tapped.

<span id="BDLQuestionOptionModel"></span>
# BDLQuestionOptionModel

```objectivec
@interface BDLQuestionOptionModel : BDLBaseModel
```


The option information model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[optionId](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionOptionModel-optionid) |
|NSString\* |[optionName](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionOptionModel-optionname) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionOptionModel-optionid"></span>
### optionId

```objectivec
@property (nonatomic, strong) NSNumber *optionId;
```


The option ID.

<span id="BDLQuestionOptionModel-optionname"></span>
### optionName

```objectivec
@property (nonatomic, copy) NSString *optionName;
```


The option content.

<span id="BDLCommentAndNoticeViewConfiguration"></span>
# BDLCommentAndNoticeViewConfiguration

```objectivec
@interface BDLCommentAndNoticeViewConfiguration : BDLRTBaseConfiguration
```


The configuration of the comment and notification view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|CGFloat |[customizePortraitCommentViewHeight](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeViewConfiguration-customizeportraitcommentviewheight) |
|void |[customizeCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeViewConfiguration-customizecommentview) |
|void |[customizeNoticeContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeViewConfiguration-customizenoticecontainerview) |


<span id="instructions"></span>
## Instructions

<span id="BDLCommentAndNoticeViewConfiguration-customizeportraitcommentviewheight"></span>
### customizePortraitCommentViewHeight

```objectivec
@property (nonatomic, copy, nullable) CGFloat (^customizePortraitCommentViewHeight)(BDLCommentAndNoticeView *commentAndNoticeView);
```


Customizes the height of the comment area (including the text box) for live rooms in portrait mode. Unit: points. Default value: `241`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentAndNoticeView |BDLCommentAndNoticeView\* |The comment and notification view. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView). |


**Return Value**

The height of the comment area. Unit: points. If the return value is less than `0`, the default configuration is used, which is 241 pt.

<span id="BDLCommentAndNoticeViewConfiguration-customizecommentview"></span>
### customizeCommentView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeCommentView)(BDLCommentAndNoticeView *commentAndNoticeView, BDLCommentView *view);
```


Customizes the comment view for live rooms in portrait mode. All properties except `hidden` can be customized. You can modify the overall layout using [customizeViewConstraints](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLivePullViewControllerConfig-customizeviewconstraints), but customizing the layout of individual properties is not supported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentAndNoticeView |BDLCommentAndNoticeView\* |The comment and notification view. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView). |
|view |BDLCommentView\* |The comment area view. For more information, see [BDLCommentView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentView). |


<span id="BDLCommentAndNoticeViewConfiguration-customizenoticecontainerview"></span>
### customizeNoticeContainerView

```objectivec
@property (nonatomic, copy, nullable) void (^customizeNoticeContainerView)(BDLCommentAndNoticeView *commentAndNoticeView, BDLNoticeContainerView *view);
```


Customizes the container view of notifications. You can use this view to customize system notifications, such as lucky draw notifications.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|commentAndNoticeView |BDLCommentAndNoticeView\* |The comment and notification view. For more information, see [BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/11/5590#BDLCommentAndNoticeView). |
|view |BDLNoticeContainerView\* |The container view of notifications. For more information, see [BDLNoticeContainerView](https://docs.byteplus.com/en/docs/11/5590#BDLNoticeContainerView). |


<span id="BDLPopupTopCommentView"></span>
# BDLPopupTopCommentView

```objectivec
@interface BDLPopupTopCommentView : BDLPopupBottomShowBaseView
```


The pinned comment details dialog box.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLPopupTopCommentViewConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLPopupTopCommentView-config) |
|UIButton\* |[backButton](https://docs.byteplus.com/en/docs/11/5590#BDLPopupTopCommentView-backbutton) |
|UITextView\* |[textView](https://docs.byteplus.com/en/docs/11/5590#BDLPopupTopCommentView-textview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithComment:isPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLPopupTopCommentView-initwithcomment-isportrait) |
|void |[urlClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLPopupTopCommentView-urlclickblock) |
|void |[commentNicknameClick](https://docs.byteplus.com/en/docs/11/5590#BDLPopupTopCommentView-commentnicknameclick) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupTopCommentView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLPopupTopCommentViewConfiguration *config;
```


The configuration of the pinned comment details dialog box. For more information, see [BDLPopupTopCommentViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPopupTopCommentViewConfiguration(Config)).

<span id="BDLPopupTopCommentView-backbutton"></span>
### backButton

```objectivec
@property (nonatomic, strong, readonly, nullable) UIButton *backButton;
```


The back button. All properties except `frame` can be customized.

<span id="BDLPopupTopCommentView-textview"></span>
### textView

```objectivec
@property (nonatomic, strong, readonly, nullable) UITextView *textView;
```


The text display. All properties except `attributedText` and `font` can be customized. You can customize the `font` by using [contentFont](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPopupTopCommentViewConfiguration(Config)-contentfont).

<span id="instructions"></span>
## Instructions

<span id="BDLPopupTopCommentView-initwithcomment-isportrait"></span>
### initWithComment:isPortrait:

```objectivec
- (instancetype)initWithComment:(BDLCommentModel *)comment isPortrait:(BOOL)isPortrait;
```


Initializes the instance of the pinned comment details dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|comment |BDLCommentModel\* |The comment to display. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the pinned comment details dialog box.

<span id="BDLPopupTopCommentView-urlclickblock"></span>
### urlClickBlock

```objectivec
@property (nonatomic, copy, nullable) void (^urlClickBlock)(NSURL *url);
```


The callback is triggered when the URL in a comment is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|url |NSURL\* |The tapped URL. |


<span id="BDLPopupTopCommentView-commentnicknameclick"></span>
### commentNicknameClick

```objectivec
@property (nonatomic, copy, nullable) void (^commentNicknameClick)(BDLPopupTopCommentView *popupView, BDLCommentModel *comment);
```


The callback is triggered when a comment nickname is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|popupView |BDLPopupTopCommentView\* |The current `BDLPopupTopCommentView` instance. |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLQuestionnaireAnswersModel"></span>
# BDLQuestionnaireAnswersModel

```objectivec
@interface BDLQuestionnaireAnswersModel : BDLBaseModel
```


The model of questionnaires filled out by viewers.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSNumber\* |[questionnaireId](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireAnswersModel-questionnaireid) |
|NSArray<BDLQuestionAnswerModel\*\>\* |[questionAnswers](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireAnswersModel-questionanswers) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireAnswersModel-questionnaireid"></span>
### questionnaireId

```objectivec
@property (nonatomic, strong) NSNumber *questionnaireId;
```


The questionnaire ID.

<span id="BDLQuestionnaireAnswersModel-questionanswers"></span>
### questionAnswers

```objectivec
@property (nonatomic, copy) NSArray<BDLQuestionAnswerModel *> *questionAnswers;
```


The questionnaire content filled out by viewers. For more information, see [BDLQuestionAnswerModel](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionAnswerModel).

<span id="BDLInteractiveToolController"></span>
# BDLInteractiveToolController

```objectivec
@interface BDLInteractiveToolController : NSObject
```


The interaction tools controller.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[popupSuperview](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-popupsuperview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[showFloatingViewBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-showfloatingviewblock) |
|void |[hideFloatingViewBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-hidefloatingviewblock) |
|void |[closeLiveRoomBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-closeliveroomblock) |
|BDLBaseView |[customizeInteractiveToolView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-customizeinteractivetoolview) |
|UIView\* |[customizeFloatingView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-customizefloatingview) |
|BDLPopupBottomShowViewProtocol |[customizeAwardDetailsView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-customizeawarddetailsview) |
|BDLPopupCenterShowViewProtocol |[customizeAwardWinnersView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-customizeawardwinnersview) |
|BDLPopupCenterShowViewProtocol |[customizeAwardResultView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-customizeawardresultview) |
|void |[interactiveToolViewURLTappedBlock](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolController-interactivetoolviewurltappedblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolController-popupsuperview"></span>
### popupSuperview

```objectivec
@property (nonatomic, strong, nullable) UIView *popupSuperview;
```


The view that displays the dialog box. The related dialog box is not displayed if `nil`.

<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolController-showfloatingviewblock"></span>
### showFloatingViewBlock

```objectivec
@property (nonatomic, copy, nullable) void(^showFloatingViewBlock)(BDLInteractiveToolController *interactiveToolController, UIView *floatingView, UIView *withoutCloseButtonView);
```


The SDK calls this method when the interaction tool floating window is displayed on the viewing page. If the type is the same, the `floatingView` will be the same. By default, use the type of [BDLFloatingInteractiveToolView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView), and you can determine the type of the floating window through [type](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-type).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interactiveToolController |BDLInteractiveToolController\* |The interaction tools controller. |
|floatingView |UIView\* |The displayed interaction tool floating window. |
|withoutCloseButtonView |UIView\* |The displayed interaction tool floating window without a close button. |


<span id="BDLInteractiveToolController-hidefloatingviewblock"></span>
### hideFloatingViewBlock

```objectivec
@property (nonatomic, copy, nullable) void(^hideFloatingViewBlock)(BDLInteractiveToolController *interactiveToolController, UIView *floatingView, UIView *withoutCloseButtonView);
```


The SDK calls this method when the interaction tool floating window is hidden on the viewing page. If the type is the same, the `floatingView` will be the same. By default, use the type of [BDLFloatingInteractiveToolView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView), and you can determine the type of the floating window through [type](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-type).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interactiveToolController |BDLInteractiveToolController\* |The interaction tools controller. |
|floatingView |UIView\* |The hidden interaction tool floating window. |
|withoutCloseButtonView |UIView\* |The hidden interaction tool floating window without a close button. |


<span id="BDLInteractiveToolController-closeliveroomblock"></span>
### closeLiveRoomBlock

```objectivec
@property (nonatomic, copy, nullable) void(^closeLiveRoomBlock)(BDLInteractiveToolController *interactiveToolController);
```


The SDK calls this method when the live room needs to be closed. Currently, this method is only applicable to scenarios where the questionnaire sent when viewers join the live room needs to be forcibly closed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interactiveToolController |BDLInteractiveToolController\* |The interaction tools controller. |


<span id="BDLInteractiveToolController-customizeinteractivetoolview"></span>
### customizeInteractiveToolView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeInteractiveToolView)(BDLInteractiveToolController *controller, BDLInteractiveToolView *interactiveToolView);
```


Customizes the interaction tools menu. All properties can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLInteractiveToolController\* |The interaction tools controller. |
|interactiveToolView |BDLInteractiveToolView\* |The interaction tools menu view. For more information, see [BDLInteractiveToolView](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolView). |


**Return Value**

Instances of `BDLBaseView` and its subclasses.

<span id="BDLInteractiveToolController-customizefloatingview"></span>
### customizeFloatingView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView * _Nullable (^customizeFloatingView)(BDLInteractiveToolController *controller, BDLFloatingInteractiveToolView *floatingView);
```


Customizes the floating window view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLInteractiveToolController\* |The interaction tools controller. |
|floatingView |BDLFloatingInteractiveToolView\* |The interaction tool floating window view. For more information, see [BDLFloatingInteractiveToolView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView). |


**Return Value**

The floating window view.

<span id="BDLInteractiveToolController-customizeawarddetailsview"></span>
### customizeAwardDetailsView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView<BDLPopupBottomShowViewProtocol> * _Nullable (^customizeAwardDetailsView)(BDLInteractiveToolController *controller, BDLAwardDetailsView *view);
```


Customizes the lucky draw details view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLInteractiveToolController\* |The interaction tools controller. |
|view |BDLAwardDetailsView\* |The lucky draw details view. For more information, see [BDLAwardDetailsView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardDetailsView). |


**Return Value**

The lucky draw details view, which needs to conform to the [BDLPopupBottomShowViewProtocol](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPopupBottomShowViewProtocol) protocol.

<span id="BDLInteractiveToolController-customizeawardwinnersview"></span>
### customizeAwardWinnersView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView<BDLPopupCenterShowViewProtocol> * _Nullable (^customizeAwardWinnersView)(BDLInteractiveToolController *controller, BDLAwardWinnersView *view);
```


Customizes the prize winner list view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLInteractiveToolController\* |The interaction tools controller. |
|view |BDLAwardWinnersView\* |The prize winner list view. For more information, see [BDLAwardWinnersView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardWinnersView). |


**Return Value**

The prize winner list view, which needs to conform to the [BDLPopupCenterShowViewProtocol](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPopupCenterShowViewProtocol) protocol.

<span id="BDLInteractiveToolController-customizeawardresultview"></span>
### customizeAwardResultView

```objectivec
@property (nonatomic, copy, nullable) __kindof UIView<BDLPopupCenterShowViewProtocol> * _Nullable (^customizeAwardResultView)(BDLInteractiveToolController *controller, BDLAwardResultView *view);
```


Customizes the lucky draw results view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLInteractiveToolController\* |The interaction tools controller. |
|view |BDLAwardResultView\* |The lucky draw results view. For more information, see [BDLAwardResultView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardResultView). |


**Return Value**

The lucky draw results view, which needs to conform to the [BDLPopupCenterShowViewProtocol](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPopupCenterShowViewProtocol) protocol.

<span id="BDLInteractiveToolController-interactivetoolviewurltappedblock"></span>
### interactiveToolViewURLTappedBlock

```objectivec
@property (nonatomic, copy, nullable) void (^interactiveToolViewURLTappedBlock)(NSURL * _Nullable url, BOOL enableFloating);
```


The SDK calls this method when viewers tap the URL in the interaction tool message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|url |NSURL\* |The tapped URL. |
|enableFloating |BOOL |Whether the redirected content is displayed on a floating page in the live room.<br><br><br>* `YES`: The redirected content is displayed on a floating page in the live room. Viewers can watch the video and view the redirected content at the same time.<br><br>* `NO`: The redirected content is displayed on a new browser tab. Viewers cannot watch the video and view the redirected content at the same time. |


<span id="BDLQuestionnaireUserInfoModel"></span>
# BDLQuestionnaireUserInfoModel

```objectivec
@interface BDLQuestionnaireUserInfoModel : BDLBaseModel
```


The information model of viewers who submit questionnaires.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[userId](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUserInfoModel-userid) |
|NSString\* |[externalId](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUserInfoModel-externalid) |
|BDLActivityAuthMode |[registerType](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUserInfoModel-registertype) |
|NSString\* |[nickname](https://docs.byteplus.com/en/docs/11/5590#BDLQuestionnaireUserInfoModel-nickname) |


<span id="instructions"></span>
## Instructions

<span id="BDLQuestionnaireUserInfoModel-userid"></span>
### userId

```objectivec
@property (nonatomic, copy) NSString *userId;
```


The user ID, which is the unique identifier of the viewer in BytePlus Live.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>0</code>.</div>


<span id="BDLQuestionnaireUserInfoModel-externalid"></span>
### externalId

```objectivec
@property (nonatomic, copy) NSString *externalId;
```


The unique identifier of the viewer on third\-party platforms.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This property has a value only when the authentication mode is custom and the viewer has logged in to the live room.</div>


<span id="BDLQuestionnaireUserInfoModel-registertype"></span>
### registerType

```objectivec
@property (nonatomic, assign) BDLActivityAuthMode registerType;
```


The authentication mode. For more information, see [BDLActivityAuthMode](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLActivityAuthMode).

<span id="BDLQuestionnaireUserInfoModel-nickname"></span>
### nickname

```objectivec
@property (nonatomic, copy) NSString *nickname;
```


The viewer's nickname.

<span id="BDLPlayerSpeedView"></span>
# BDLPlayerSpeedView

```objectivec
@interface BDLPlayerSpeedView : BDLPopupBottomOrRightShowBaseView <BDLLanguageService>
```


The playback speed selection view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLPlayerSpeedViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-delegate) |
|BOOL |[fullScreen](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-fullscreen) |
|BDLPlayerSpeed |[speed](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-speed) |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|CGFloat |[valueFromSpeed:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-valuefromspeed) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[customizeSpeedButtons](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-customizespeedbuttons) |
|instancetype |[initWithPortrait:config:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-initwithportrait-config) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLPlayerSpeedView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerSpeedView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLPlayerSpeedViewDelegate> delegate;
```


The delegate method. For more information, see [BDLPlayerSpeedViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLPlayerSpeedViewDelegate).

<span id="BDLPlayerSpeedView-fullscreen"></span>
### fullScreen

```objectivec
@property (nonatomic, assign) BOOL fullScreen;
```


Whether currently is in full\-screen mode.


* `YES`: In full\-screen mode.

* `NO`: Not in full\-screen mode.

    &nbsp;


<span id="speed"></span>
### speed

```objectivec
@property (nonatomic, assign) BDLPlayerSpeed speed;
```


The current playback speed. For more information, see [BDLPlayerSpeed](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerSpeed).

<span id="instructions"></span>
## Instructions

<span id="BDLPlayerSpeedView-valuefromspeed"></span>
### valueFromSpeed:

```objectivec
+ (CGFloat)valueFromSpeed:(BDLPlayerSpeed)speed;
```


Changes the playback speed based on the enumeration value.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|speed |BDLPlayerSpeed |The playback speed. For more information, see [BDLPlayerSpeed](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerSpeed). |


**Return Value**

The playback speed.

<span id="BDLPlayerSpeedView-customizespeedbuttons"></span>
### customizeSpeedButtons

```objectivec
@property (nonatomic, copy, nullable) void (^customizeSpeedButtons)(NSArray<UIButton *> * buttons, NSUInteger selectedIndex);
```


Customizes the playback speed button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|buttons |NSArray<UIButton\*\>\* |An array of playback speed buttons. |
|selectedIndex |NSUInteger |The currently selected array index. |


<span id="BDLPlayerSpeedView-initwithportrait-config"></span>
### initWithPortrait:config:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait config:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the playback speed selection view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the playback speed selection view.

<span id="BDLPlayerSpeedView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLPopupCenterShowBaseView"></span>
# BDLPopupCenterShowBaseView

```objectivec
@interface BDLPopupCenterShowBaseView : BDLPopupBaseView <BDLPopupCenterShowViewProtocol>
```


The base view of the center dialog box view.

<span id="BDLInteractiveContextModel"></span>
# BDLInteractiveContextModel

```objectivec
@interface BDLInteractiveContextModel : BDLBaseModel
```


The interaction tool content model.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLInteractiveContextType |[type](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-type) |
|NSString\* |[imageTextContext](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-imagetextcontext) |
|BDLInteractiveAwardModel\* |[awardContext](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-awardcontext) |
|BDLQuestionnaireModel\* |[questionnaireContext](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-questionnairecontext) |
|BDLInteractiveAnnouncementModel\* |[announcementContext](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-announcementcontext) |
|BDLInteractiveVoteModel\* |[voteContext](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-votecontext) |
|BDLInteractiveQuizModel\* |[quizContext](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-quizcontext) |
|BDLTaskAwardConfigModel\* |[taskAward](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveContextModel-taskaward) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveContextModel-type"></span>
### type

```objectivec
@property (nonatomic, assign) BDLInteractiveContextType type;
```


The type of interaction tool content. For more information, see [BDLInteractiveContextType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveContextType).

<span id="BDLInteractiveContextModel-imagetextcontext"></span>
### imageTextContext

```objectivec
@property (nonatomic, copy) NSString *imageTextContext;
```


The content of the text and image.

<span id="BDLInteractiveContextModel-awardcontext"></span>
### awardContext

```objectivec
@property (nonatomic, strong) BDLInteractiveAwardModel *awardContext;
```


The content of real\-time lucky draws. For more information, see [BDLInteractiveAwardModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveAwardModel).

<span id="BDLInteractiveContextModel-questionnairecontext"></span>
### questionnaireContext

```objectivec
@property (nonatomic, strong) BDLQuestionnaireModel *questionnaireContext;
```


The questionnaire content. For more information, see [BDLQuestionnaireModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLQuestionnaireModel).

<span id="BDLInteractiveContextModel-announcementcontext"></span>
### announcementContext

```objectivec
@property (nonatomic, strong) BDLInteractiveAnnouncementModel *announcementContext;
```


The announcement content. For more information, see [BDLInteractiveAnnouncementModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveAnnouncementModel).

<span id="BDLInteractiveContextModel-votecontext"></span>
### voteContext

```objectivec
@property (nonatomic, strong) BDLInteractiveVoteModel *voteContext;
```


The vote content. For more information, see [BDLInteractiveVoteModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveVoteModel).

<span id="BDLInteractiveContextModel-quizcontext"></span>
### quizContext

```objectivec
@property (nonatomic, strong) BDLInteractiveQuizModel *quizContext;
```


The quiz content. For more information, see [BDLInteractiveQuizModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveQuizModel).

<span id="BDLInteractiveContextModel-taskaward"></span>
### taskAward

```objectivec
@property (nonatomic, strong) BDLTaskAwardConfigModel *taskAward;
```


The content of watch time\-based lucky draws. For more information, see [BDLTaskAwardConfigModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLTaskAwardConfigModel).

<span id="BDLShoppingCardController"></span>
# BDLShoppingCardController

```objectivec
@interface BDLShoppingCardController : NSObject
```


The product card controller.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UIView\* |[popupSuperview](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardController-popupsuperview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BDLBaseView |[customizeShoppingCardView](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardController-customizeshoppingcardview) |
|void |[onCardClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardController-oncardclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLShoppingCardController-popupsuperview"></span>
### popupSuperview

```objectivec
@property (nonatomic, strong, nullable) UIView *popupSuperview;
```


The view that displays the dialog box. The related dialog box is not displayed if `nil`.

<span id="instructions"></span>
## Instructions

<span id="BDLShoppingCardController-customizeshoppingcardview"></span>
### customizeShoppingCardView

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeShoppingCardView)(BDLShoppingCardController *controller, BDLShoppingCardView *shoppingCardView);
```


Customizes the product card menu. All properties can be customized.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLShoppingCardController\* |The product card controller. |
|shoppingCardView |BDLShoppingCardView\* |The product card view. For more information, see [BDLShoppingCardView](https://docs.byteplus.com/en/docs/11/5590#BDLShoppingCardView). |


**Return Value**

Instances of `BDLBaseView` and its subclasses.

<span id="BDLShoppingCardController-oncardclickblock"></span>
### onCardClickBlock

```objectivec
@property (nonatomic, copy, nullable) void(^onCardClickBlock)(BDLShoppingCardController *controller, NSURL *url, BOOL isFloatingEnable, BDLCardModel *cardModel, BDLShoppingCardClickPosition clickPosition);
```


The callback is triggered when the product card is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controller |BDLShoppingCardController\* |The product card controller. |
|url |NSURL\* |The URL of the product card. |
|isFloatingEnable |BOOL |Whether the product details page is displayed on a floating page in the live room, which is returned from the BytePlus Live server. Valid values:<br><br><br>* `YES`: The product details page is displayed on a floating page in the live room after viewers tap the product card. Viewers can watch the video and view the product details page at the same time.<br><br>* `NO`: The product details page is displayed on a new browser tab after viewers tap the product card. Viewers cannot watch the video and view the product details page at the same time. |
|cardModel |BDLCardModel\* |The product card model. For more information, see [BDLCardModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCardModel). |
|clickPosition |BDLShoppingCardClickPosition |The product card tap source. For more information, see [BDLShoppingCardClickPosition](https://docs.byteplus.com/en/docs/11/1185544#BDLShoppingCardClickPosition). |


<span id="BDLMenuView"></span>
# BDLMenuView

```objectivec
@interface BDLMenuView : BDLBaseView
```


The menu bar container view, which is used to implement the left and right sliding and switching of the menu bar.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLMenuViewConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-config) |
|UIView\* |[titleBackgroundView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-titlebackgroundview) |
|UIScrollView\* |[titleScrollView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-titlescrollview) |
|UIView\* |[titleBottomLine](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-titlebottomline) |
|UIScrollView\* |[contentScrollView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-contentscrollview) |
|CGFloat |[titleRightMargin](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-titlerightmargin) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-initwithportrait) |
|void |[updateWithTitleArray:contentViewArray:normalColor:selectedColor:selectIndex:](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-updatewithtitlearray-contentviewarray-normalcolor-selectedcolor-selectindex) |
|void |[indexDidChangeBlock](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-indexdidchangeblock) |
|NSUInteger |[currentIndex](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-currentindex) |
|UIView\* |[currentContentView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-currentcontentview) |
|void |[willRotate](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-willrotate) |
|void |[didRotate](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-didrotate) |


<span id="instructions"></span>
## Instructions

<span id="BDLMenuView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLMenuViewConfiguration *config;
```


The configuration of the menu bar container view. For more information, see [BDLMenuViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLMenuViewConfiguration).

<span id="BDLMenuView-titlebackgroundview"></span>
### titleBackgroundView

```objectivec
@property (nonatomic, strong, readonly) UIView *titleBackgroundView;
```


The background view of the menu bar title area. All properties can be customized.

<span id="BDLMenuView-titlescrollview"></span>
### titleScrollView

```objectivec
@property (nonatomic, strong, readonly) UIScrollView *titleScrollView;
```


The scrollable `scrollView` in the menu bar title area. All properties except `contentSize` can be customized.

<span id="BDLMenuView-titlebottomline"></span>
### titleBottomLine

```objectivec
@property (nonatomic, strong, readonly) UIView *titleBottomLine;
```


The indicator line at the bottom of the currently selected title. All properties except `frame` can be customized.

<span id="BDLMenuView-contentscrollview"></span>
### contentScrollView

```objectivec
@property (nonatomic, strong, readonly) UIScrollView *contentScrollView;
```


The scrollable `scrollView` in the content area under the menu bar title. All properties except `contentSize` can be customized.

<span id="BDLMenuView-titlerightmargin"></span>
### titleRightMargin

```objectivec
@property (nonatomic, assign) CGFloat titleRightMargin;
```


The distance between the menu bar container view and the right side of the screen. Unit: points. If the live room has the live source selection entry or playback video list entry, the default value is 120. Otherwise, the default value is 0.

<span id="instructions"></span>
## Instructions

<span id="BDLMenuView-initwithportrait"></span>
### initWithPortrait:

```objectivec
- (instancetype)initWithPortrait:(BOOL)portrait;
```


Initializes the instance of the menu bar container view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|portrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the menu bar container view.

<span id="BDLMenuView-updatewithtitlearray-contentviewarray-normalcolor-selectedcolor-selectindex"></span>
### updateWithTitleArray:contentViewArray:normalColor:selectedColor:selectIndex:

```objectivec
- (void)updateWithTitleArray:(NSArray *)titleArray
            contentViewArray:(NSArray<__kindof UIView *> *)contentViewArray
                 normalColor:(UIColor *)normalColor
               selectedColor:(UIColor *)selectedColor
                 selectIndex:(NSInteger)selectIndex;
```


The update method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|titleArray |NSArray\* |An array of titles. |
|contentViewArray |NSArray<__kindof UIView\*\>\* |An array of content views under the title. |
|normalColor |UIColor\* |The default color of the title. |
|selectedColor |UIColor\* |The color of the selected title. |
|selectIndex |NSInteger |The default selected array index. |


<span id="BDLMenuView-indexdidchangeblock"></span>
### indexDidChangeBlock

```objectivec
@property (nonatomic, copy, nullable) void(^indexDidChangeBlock)(BDLMenuView *view, NSUInteger index);
```


The callback is triggered when the currently selected array index changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMenuView\* |The menu bar container view. |
|index |NSUInteger |The currently selected array index. |


<span id="BDLMenuView-currentindex"></span>
### currentIndex

```objectivec
- (NSUInteger)currentIndex;
```


Gets the index of the displayed content view.

**Return Value**

The index of the displayed content view.

<span id="BDLMenuView-currentcontentview"></span>
### currentContentView

```objectivec
- (UIView *)currentContentView;
```


Gets the currently displayed content view.

**Return Value**

The currently displayed content view.

<span id="BDLMenuView-willrotate"></span>
### willRotate

```objectivec
- (void)willRotate;
```


Call this method when the screen is rotating, which is used to adjust the `contentOffset` value of the [contentScrollView](https://docs.byteplus.com/en/docs/11/5590#BDLMenuView-contentscrollview).

<span id="BDLMenuView-didrotate"></span>
### didRotate

```objectivec
- (void)didRotate;
```


Call this method after the screen rotation is complete.

<span id="BDLLiveEngine"></span>
# BDLLiveEngine

```objectivec
@interface BDLLiveEngine : NSObject
```


The entry class of the Viewer SDK.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isJoining](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-isjoining) |
|BDLLiveRoomConfiguration\* |[liveRoomConfiguration](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-liveroomconfiguration) |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|instancetype |[sharedInstance](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-sharedinstance) |
|NSString\* |[sdkVersion](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-sdkversion) |
|void |[clearCache](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-clearcache) |
|NSString\* |[userUniqueId](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-useruniqueid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[setActivityListener:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-setactivitylistener) |
|BOOL |[setLoginProvider:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-setloginprovider) |
|BOOL |[joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) |
|BOOL |[updateActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-updateactivity-success-failure) |
|BDLLivePullViewController |[getLivePullViewController](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-getlivepullviewcontroller) |
|BDLLivePullViewController |[getLivePullViewControllerWithBasePlayerView:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-getlivepullviewcontrollerwithbaseplayerview) |
|BDLActivityService |[getActivityService](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-getactivityservice) |
|nullable id |[serviceWithProtocol:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-servicewithprotocol) |
|void |[leaveLiveRoom](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-leaveliveroom) |


<span id="instructions"></span>
## Instructions

<span id="BDLLiveEngine-isjoining"></span>
### isJoining

```objectivec
@property (nonatomic, assign, readonly) BOOL isJoining;
```


Whether the user is joining the live room.


* `YES`: Joining.

* `NO`: Not joining.

    &nbsp;


<span id="liveroomconfiguration"></span>
### liveRoomConfiguration

```objectivec
@property (nonatomic, strong, readonly) BDLLiveRoomConfiguration *liveRoomConfiguration;
```


The live room configuration. For more information, see [BDLLiveRoomConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLiveRoomConfiguration).

<span id="instructions"></span>
## Instructions

<span id="BDLLiveEngine-sharedinstance"></span>
### sharedInstance

```objectivec
+ (instancetype)sharedInstance;
```


Gets the `BDLLiveEngine` instance.

**Return Value**

The `BDLLiveEngine` instance.

<span id="BDLLiveEngine-sdkversion"></span>
### sdkVersion

```objectivec
+ (NSString *)sdkVersion;
```


Gets the SDK version number.

**Return Value**

The SDK version number.

<span id="BDLLiveEngine-clearcache"></span>
### clearCache

```objectivec
+ (void)clearCache;
```


Clears all local caches of the SDK on the viewer's current device. The local cache includes:


* Records of reminder dialog boxes. After the cache is cleared, viewers will see the dialog box again when they rejoin the live room.

* Records of live stream bookings in the system calendar when the authentication mode is public. After the cache is cleared, the **Book** button will revert to **Book now**, but the events in the system calendar will remain.

* Records of VOD video playback progress. After the cache is cleared, VOD videos will start from the beginning when viewers rejoin the live room.

    &nbsp;


<span id="useruniqueid"></span>
### userUniqueId

```objectivec
+ (NSString *)userUniqueId;
```


Gets the user's unique ID. Call this method after the user successfully joins the live room. This ID can be provided to BytePlus Live technical support when reporting issues to help diagnose and resolve problems.

**Return Value**

The unique ID of the user.

<span id="BDLLiveEngine-setactivitylistener"></span>
### setActivityListener:

```objectivec
- (void)setActivityListener:(nullable id<BDLActivityListener>)listener;
```


Sets the live room listener.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|listener |nullable id<BDLActivityListener\> |The live room listener. For more information, see [BDLActivityListener](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLActivityListener). |


<span id="BDLLiveEngine-setloginprovider"></span>
### setLoginProvider:

```objectivec
- (BOOL)setLoginProvider:(nullable id<BDLLoginProvider>)loginProvider;
```


Sets the delegate for custom login to the live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|loginProvider |nullable id<BDLLoginProvider\> |The delegate for custom login to the live room. For more information, see [BDLLoginProvider](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLLoginProvider). |


**Return Value**


* `YES`: Set successfully.

* `NO`: Return `NO` if the [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) method is not implemented, indicating that the setting failed.

    &nbsp;


<span id="joinliveroomwithactivity-success-failure"></span>
### joinLiveRoomWithActivity:success:failure:

```objectivec
- (BOOL)joinLiveRoomWithActivity:(BDLActivity *)activity
                         success:(void (^)(void))success
                         failure:(void (^)(NSError *error))failure;
```


Joins the live room. After successfully joining or failing to join the live room, the SDK triggers the corresponding callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information. For more information, see [BDLActivity](https://docs.byteplus.com/en/docs/11/5590#BDLActivity). |
|success |void(^)(void) |The callback triggered after successfully joining the live room, with no return value. |
|failure |void(^)(NSError\*error) |The callback triggered after failing to join the live room, with no return value.<br><br>&nbsp;<br><br>Input parameter:<br><br>&nbsp;<br><br>`error`: The error information. The value of `error.code` is an enumeration value of `BDLError`. For more information, see [BDLError](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-error-codes#BDLError).<br><br>&nbsp;<br><br>Example:<br><br>&nbsp;<br><br>`failure:^(NSError * _Nonnull error) { if ([error.domain isEqualToString:BDLErrorDomain]) { if (error.code == BDLErrorPullDisallowed) } else if ... { } } else { } }];` |


**Return Value**


* `YES`: The method is called successfully.

* `NO`: Invalid parameters, meaning the value of either [activityId](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-activityid) or [token](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-token) is `nil`.

    &nbsp;


<span id="updateactivity-success-failure"></span>
### updateActivity:success:failure:

```objectivec
- (BOOL)updateActivity:(BDLActivity *)activity
               success:(void (^)(void))success
               failure:(void (^)(NSError *error))failure;
```


Updates the live room information, namely updating the live room's [token](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-token) and [authMode](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-authmode). After successfully updating or failing to update the live room information, the SDK triggers the corresponding callback.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Use the <a href="https://docs.byteplus.com/en/docs/11/5590#BDLActivity-activityid">activityId</a> and <a href="https://docs.byteplus.com/en/docs/11/5590#BDLActivity-isportrait">isPortrait</a> when calling <a href="https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure">joinLiveRoomWithActivity:success:failure:</a> to update the corresponding live room information.</div>


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information. For more information, see [BDLActivity](https://docs.byteplus.com/en/docs/11/5590#BDLActivity). |
|success |void(^)(void) |The callback triggered after successfully updating the live room information, with no return value. |
|failure |void(^)(NSError\*error) |The callback triggered after failing to update the live room information, with no return value.<br><br>&nbsp;<br><br>Input parameter:<br><br>&nbsp;<br><br>`error`: The error information. The value of `error.code` is an enumeration value of `BDLError`. For more information, see [BDLError](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-error-codes#BDLError).<br><br>&nbsp;<br><br>Example:<br><br>&nbsp;<br><br>`failure:^(NSError * _Nonnull error) { if ([error.domain isEqualToString:BDLErrorDomain]) { if (error.code == BDLErrorPullDisallowed) } else if ... { } } else {} }];<br/>` |


**Return Value**


* `YES`: The method is called successfully.

* `NO`: Invalid parameters, meaning the value of `activityId` or `isPortrait` is different from that used when calling [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure), or the value of [activityId](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-activityid) or [token](https://docs.byteplus.com/en/docs/11/5590#BDLActivity-token) is `nil`.

    &nbsp;


<span id="getlivepullviewcontroller"></span>
### getLivePullViewController

```objectivec
- (nullable BDLLivePullViewController *)getLivePullViewController;
```


Gets the live room page.

Call `getLivePullViewController` in the `success` callback of [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure).

**Return Value**


* Instance of [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController).

* The return value is `nil` in the following scenarios:

   * [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) is not called.

   * [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) is called and the return value is `NO`.

   * [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) is called but failed to join the live room.

       &nbsp;


<span id="getlivepullviewcontrollerwithbaseplayerview"></span>
### getLivePullViewControllerWithBasePlayerView:

```objectivec
- (nullable BDLLivePullViewController *)getLivePullViewControllerWithBasePlayerView:(nullable BDLBasePlayerView *)basePlayerView;
```


Gets the live room page by passing an already playing `basePlayerView`. After passing the `basePlayerView` into this method, you can avoid getting and playing the video content again, allowing viewers to seamlessly continue watching the previous video content upon joining the live room.

Call `getLivePullViewControllerWithBasePlayerView:` in the `success` callback of [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |nullable BDLBasePlayerView\* |The custom player, which is used to display the live room video content in advance. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/5590#BDLBasePlayerView). |


**Return Value**


* Instance of [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/5590#BDLLivePullViewController).

* The return value is `nil` in the following scenarios:

   * [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) is not called.

   * [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) is called and the return value is `NO`.

   * [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) is called but failed to join the live room.

       &nbsp;


<span id="getactivityservice"></span>
### getActivityService

```objectivec
- (nullable id <BDLActivityService>)getActivityService;
```


Gets `ActivityService`. Call this method after [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/5590#BDLLiveEngine-joinliveroomwithactivity-success-failure) succeeds.

**Return Value**

Instances of classes that conform to the `BDLActivityService` protocol.

<span id="BDLLiveEngine-servicewithprotocol"></span>
### serviceWithProtocol:

```objectivec
- (nullable id)serviceWithProtocol:(Protocol *)protocol;
```


Find instances of classes that conform to the protocol based on the protocol.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|protocol |Protocol\* |The protocol to conform to. |


**Return Value**

Instances of classes that conform to the protocol.

<span id="BDLLiveEngine-leaveliveroom"></span>
### leaveLiveRoom

```objectivec
- (void)leaveLiveRoom;
```


Leaves the live room.

<span id="BDLNetworkNotReachableView"></span>
# BDLNetworkNotReachableView

```objectivec
@interface BDLNetworkNotReachableView : BDLBaseView <BDLLanguageService>
```


The network disconnection prompt view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<BDLNetworkNotReachableViewDelegate\> |[delegate](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkNotReachableView-delegate) |
|UILabel\* |[promptLabel](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkNotReachableView-promptlabel) |
|UIButton\* |[retryButton](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkNotReachableView-retrybutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithPortrait:config:](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkNotReachableView-initwithportrait-config) |
|void |[updateWithConfig:](https://docs.byteplus.com/en/docs/11/5590#BDLNetworkNotReachableView-updatewithconfig) |


<span id="instructions"></span>
## Instructions

<span id="BDLNetworkNotReachableView-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<BDLNetworkNotReachableViewDelegate> delegate;
```


The delegate method. For more information, see [BDLNetworkNotReachableViewDelegate](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLNetworkNotReachableViewDelegate).

<span id="BDLNetworkNotReachableView-promptlabel"></span>
### promptLabel

```objectivec
@property (nonatomic, strong) UILabel *promptLabel;
```


The prompt label. You can customize the text and text color of the prompt by using [networkNotReachableText](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-networknotreachabletext) and [promptTextColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerCommonConfiguration-prompttextcolor).

<span id="BDLNetworkNotReachableView-retrybutton"></span>
### retryButton

```objectivec
@property (nonatomic, strong) UIButton *retryButton;
```


The retry button. You can customize the background color, text, and rounded corners for live rooms in landscape or portrait mode by using [retryButtonBackgroundColor](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-retrybuttonbackgroundcolor), [retryButtonTitle](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-retrybuttontitle), and [retryButtonCornerRadius](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerBaseConfiguration-retrybuttoncornerradius) of `config.landscape` or `config.portrait`.

<span id="instructions"></span>
## Instructions

<span id="BDLNetworkNotReachableView-initwithportrait-config"></span>
### initWithPortrait:config:

```objectivec
- (instancetype)initWithPortrait:(BOOL)isPortrait config:(BDLPlayerConfiguration *)config;
```


Initializes the instance of the network disconnection prompt view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


**Return Value**

The instance of the network disconnection prompt view.

<span id="BDLNetworkNotReachableView-updatewithconfig"></span>
### updateWithConfig:

```objectivec
- (void)updateWithConfig:(BDLPlayerConfiguration *)config;
```


Updates the view based on the configuration.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |BDLPlayerConfiguration\* |The configuration. For more information, see [BDLPlayerConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerConfiguration). |


<span id="BDLFloatingInteractiveToolView"></span>
# BDLFloatingInteractiveToolView

```objectivec
@interface BDLFloatingInteractiveToolView : BDLBaseView
```


The interaction tool floating window view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id |[model](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-model) |
|BDLFloatingInteractiveToolViewType |[type](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-type) |
|UIImageView\* |[imageView](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-imageview) |
|UILabel\* |[label](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-label) |
|UIButton\* |[closeButton](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-closebutton) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithType:isPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-initwithtype-isportrait) |
|void |[clickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-clickblock) |
|void |[closeButtonClickBlock](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-closebuttonclickblock) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingInteractiveToolView-model"></span>
### model

```objectivec
@property (nonatomic, strong) id model;
```


The interaction tool model corresponding to the current view. The model type varies depending on the `type`.

<span id="BDLFloatingInteractiveToolView-type"></span>
### type

```objectivec
@property (nonatomic, assign, readonly) BDLFloatingInteractiveToolViewType type;
```


The type of the interaction tool floating window view, which is passed in through the initialization method [initWithType:isPortrait:](https://docs.byteplus.com/en/docs/11/5590#BDLFloatingInteractiveToolView-initwithtype-isportrait).

<span id="BDLFloatingInteractiveToolView-imageview"></span>
### imageView

```objectivec
@property (nonatomic, strong, readonly) UIImageView *imageView;
```


The imageView that displays the icon. To customize the image, use [customizeFloatingViewImageViewImage](https://docs.byteplus.com/en/docs/11/5590#BDLInteractiveToolConfiguration-customizeFloatingViewImageViewImage).

<span id="BDLFloatingInteractiveToolView-label"></span>
### label

```objectivec
@property (nonatomic, strong, readonly) UILabel *label;
```


The bottom text label. All properties except `text` can be customized.

<span id="BDLFloatingInteractiveToolView-closebutton"></span>
### closeButton

```objectivec
@property (nonatomic, strong, readonly) UIButton *closeButton;
```


The close button. Customization is supported.

<span id="instructions"></span>
## Instructions

<span id="BDLFloatingInteractiveToolView-initwithtype-isportrait"></span>
### initWithType:isPortrait:

```objectivec
- (instancetype)initWithType:(BDLFloatingInteractiveToolViewType)type isPortrait:(BOOL)isPortrait;
```


Initializes the instance of the interaction tool floating window view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |BDLFloatingInteractiveToolViewType |The type of the interaction tool floating window view. For more information, see [BDLFloatingInteractiveToolViewType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLFloatingInteractiveToolViewType). |
|isPortrait |BOOL |Whether to initialize in portrait mode.<br><br><br>* `YES`: Portrait mode.<br><br>* `NO`: Landscape mode. |


**Return Value**

The instance of the interaction tool floating window view.

<span id="BDLFloatingInteractiveToolView-clickblock"></span>
### clickBlock

```objectivec
@property (nonatomic, copy) void(^clickBlock)(BDLFloatingInteractiveToolView *view);
```


The callback is triggered when the current view is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLFloatingInteractiveToolView\* |The interaction tool floating window view. |


<span id="BDLFloatingInteractiveToolView-closebuttonclickblock"></span>
### closeButtonClickBlock

```objectivec
@property (nonatomic, copy) void(^closeButtonClickBlock)(BDLFloatingInteractiveToolView *view, UIButton *button);
```


The callback is triggered when the close button is tapped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLFloatingInteractiveToolView\* |The interaction tool floating window view. |
|button |UIButton\* |The close button. |


<span id="BDLAwardCountdownView"></span>
# BDLAwardCountdownView

```objectivec
@interface BDLAwardCountdownView : UIView
```


TThe lucky draw countdown view.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSArray<BDLAwardNumberView\*\>\* |[numberViews](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCountdownView-numberviews) |
|NSArray<UILabel\*\>\* |[colons](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCountdownView-colons) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[updateViewWithCountdown:](https://docs.byteplus.com/en/docs/11/5590#BDLAwardCountdownView-updateviewwithcountdown) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardCountdownView-numberviews"></span>
### numberViews

```objectivec
@property (nonatomic, copy) NSArray<BDLAwardNumberView *> *numberViews;
```


An array of number views. For more information, see [BDLAwardNumberView](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNumberView).

<span id="BDLAwardCountdownView-colons"></span>
### colons

```objectivec
@property (nonatomic, copy) NSArray<UILabel *> *colons;
```


An array of colon labels.

<span id="instructions"></span>
## Instructions

<span id="BDLAwardCountdownView-updateviewwithcountdown"></span>
### updateViewWithCountdown:

```objectivec
- (void)updateViewWithCountdown:(NSInteger)countdown;
```


Updates the interface.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|countdown |NSInteger |The remaining countdown time. Unit: seconds. |


<span id="BDLGetShareInfoResponse"></span>
# BDLGetShareInfoResponse

```objectivec
@interface BDLGetShareInfoResponse : BDLBaseResponse
```


The result after getting the sharing information, which is returned by the BytePlus Live server.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLGetShareInfoResult\* |[result](https://docs.byteplus.com/en/docs/11/5590#BDLGetShareInfoResponse-result) |


<span id="instructions"></span>
## Instructions

<span id="BDLGetShareInfoResponse-result"></span>
### result

```objectivec
@property (nonatomic, strong) BDLGetShareInfoResult *result;
```


The result after getting the sharing information. For more information, see [BDLGetShareInfoResult](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLGetShareInfoResult).

<span id="BDLAwardNumberView"></span>
# BDLAwardNumberView

```objectivec
@interface BDLAwardNumberView : UIView
```


The countdown timer view for lucky draws.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|UILabel\* |[titleLabel](https://docs.byteplus.com/en/docs/11/5590#BDLAwardNumberView-titlelabel) |


<span id="instructions"></span>
## Instructions

<span id="BDLAwardNumberView-titlelabel"></span>
### titleLabel

```objectivec
@property (nonatomic, strong, readonly) UILabel *titleLabel;
```


The number label. All properties except `text` can be customized.

<span id="BDLPopupWebView"></span>
# BDLPopupWebView

```objectivec
@interface BDLPopupWebView : BDLPopupBottomShowBaseView
```


The WebView dialog box.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BDLPopupWebViewConfiguration\* |[config](https://docs.byteplus.com/en/docs/11/5590#BDLPopupWebView-config) |
|WKWebView\* |[webView](https://docs.byteplus.com/en/docs/11/5590#BDLPopupWebView-webview) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[initWithRedirectUrl:](https://docs.byteplus.com/en/docs/11/5590#BDLPopupWebView-initwithredirecturl) |


<span id="instructions"></span>
## Instructions

<span id="BDLPopupWebView-config"></span>
### config

```objectivec
@property (nonatomic, strong, readonly) BDLPopupWebViewConfiguration *config;
```


The WebView dialog box configuration. For more information, see [BDLPopupWebViewConfiguration](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPopupWebViewConfiguration(Config)).

<span id="BDLPopupWebView-webview"></span>
### webView

```objectivec
@property (nonatomic, strong, readonly, nullable) WKWebView *webView;
```


The WebView that displays the content.

<span id="instructions"></span>
## Instructions

<span id="BDLPopupWebView-initwithredirecturl"></span>
### initWithRedirectUrl:

```objectivec
- (instancetype)initWithRedirectUrl:(NSString *)redirectUrl;
```


Initializes the instance of the WebView dialog box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|redirectUrl |NSString\* |The URL to load. |


**Return Value**

The instance of the WebView dialog box.
