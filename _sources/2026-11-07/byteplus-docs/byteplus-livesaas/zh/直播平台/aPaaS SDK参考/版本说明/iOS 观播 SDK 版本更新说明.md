---
title: "iOS 观播 SDK 版本更新说明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN"
---

本版本更新说明全面记录了 iOS 观播 SDK 的所有更新日志。您可以通过本文档跟踪每个版本的新功能、兼容性变更、优化和 bug 修复。

## 2026 年 10 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2026\-10\-23 |1.66.4 |**新功能**<br><br>新增支持通过 Swift Package Manager (SPM) 集成 SDK。SDK 以预编译的 `.xcframework` 通过 SPM 二进制目标（binary target）分发。更多信息，请参见[集成 iOS 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。 |

## 2026 年 4 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2026\-04\-28 |1.66.1 |**问题修复**<br><br><br>* 修复了若干已知的偶发性崩溃问题。<br><br>* 修复了部分加载提示未能显示的问题。 |

## 2025 年 11 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-11\-25 |1.65.2 |**问题修复**<br><br>修复了部分问题。 |
|2025\-11\-17 |1.65.1 |**问题修复**<br><br>修复了部分问题。 |
|2025\-11\-12 |1.65.0 |* **新功能**<br><br>   * 新增 [customizeFloatingViewImageViewImage](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#customizefloatingviewimageviewimage) 属性，用于设置悬浮窗图片视图。<br><br>   * 多语言<br><br>      * 新增 [preferLanguage](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#preferlanguage) 属性，用于设置观看页的首选语言。<br><br>      * 支持更多 SDK 语言类型：<br><br>         * 塔加拉语<br><br>         * 高棉语<br><br>         * 老挝语<br><br>         * 缅甸语<br><br>         * 马来语<br><br>         * 印地语<br><br>         * 法语<br><br>         * 德语<br><br>         * 意大利语<br><br>* **问题修复**<br><br>   修复了部分问题。 |

## 2025 年 8 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-09\-25 |1.64.0 |**兼容性变更**<br><br>在 [BDLFloatingController](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlfloatingcontroller) 中：<br><br><br>* 移除了 `floatingCardView`（商品浮窗视图）属性。该视图现已被 [BDLFloatingControllerViewTag](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLFloatingControllerViewTag) 替代。<br><br>* 更新了 [customizeFloatingCardView](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLFloatingController-customizefloatingcardview) 的返回类型为 **BOOL**，用于指示是否显示商品浮窗视图。<br><br><br>**优化**<br><br>SDK 现已支持回放日志上报，提升故障排查能力。 |
|2025\-09\-09 |1.63.0 |**兼容性变更**<br><br>移除了 `BDLTaskAwardRuleContactOptions`（获奖者联系信息）和 `BDLInteractiveAwardContactOptions`（获奖者必填信息）。请改用 [BDLAwardContactOptions](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlawardcontactoptions)（获奖者必填信息）。 |
|2025\-08\-26 |1.62.1 |**兼容性变更**<br><br><br>* 删除了以下商品卡片点击回调。请在 `BDLShoppingCardController` 中使用商品卡片点击回调 [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock)：<br><br>   * `BDLCardView` 中的 viewTappedBlock<br><br>   * `BDLShoppingCardView` 中的 cardViewTappedBlock<br><br>   * `BDLFloatingCardView` 中的 viewTappedBlock<br><br>   * `BDLFloatingController` 中的 onCardClickBlock<br><br>* **BDLShoppingCardController** 中的 [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock) 回调新增了参数 `clickPosition`（商品卡片点击位置），用于区分商品卡片的不同点击位置。 |
|2025\-08\-12 |1.62.0 |同步 iOS 开播 SDK 的版本号。 |

## 2025 年 7 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-07\-28 |1.61.2 |* **兼容性变更**<br><br>   部分属性、方法或视图已废弃或删除：<br><br>   * 在 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 中，废弃了 `inputBoxPromptColor` 属性。请改用 [inputBoxPromptTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-inputboxprompttextcolor) 属性。<br><br>   * 在 [BDLInteractiveToolController](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlinteractivetoolcontroller) 中，删除了用于自定义获奖者个人信息弹窗视图的方法 `customizeAwardContactView`。<br><br>   * 在 [BDLAwardWinnersView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlawardwinnersview) 中，删除了用于初始化获奖者列表视图实例的方法 `initWithAwardId:`。<br><br>   * 删除了 `BDLAwardContactView`（获奖者个人信息弹窗视图）。<br><br>* **新功能**<br><br>   * 新增 [topCommentFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentfontcolor) 属性，用于设置置顶评论内容的文字颜色。<br><br>   * 新增 [topCommentBackgroundWidthFitContent](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentbackgroundwidthfitcontent) 属性，用于设置置顶评论背景宽度是否随内容宽度自适应。<br><br>   * 新增 [topCommentViewCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentviewcornerradius) 属性，用于设置置顶评论背景的圆角。<br><br>   * 新增 [topCommentNicknameColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentnicknamecolor) 属性，用于设置置顶评论昵称的颜色。<br><br>   * 新增 [topCommentNicknameFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentnicknamefont) 属性，用于设置置顶评论昵称的字体及字号。<br><br>   * 新增 [topCommentContentLineSpacingExtra](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentcontentlinespacingextra) 属性，用于设置置顶评论内容的行间距。<br><br>   * 新增 [topCommentBackgroundColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#topcommentbackgroundcolor) 属性，用于设置置顶评论的背景色。<br><br>   * 新增 [commentContentLineSpacingExtra](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentcontentlinespacingextra) 属性，用于设置评论内容的行间距。<br><br>   * 新增 [commentCellCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentcellcornerradius) 属性，用于设置评论单元格的圆角。<br><br>   * 新增 [popupInputBoxPromptTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#popupinputboxprompttextcolor) 属性，用于设置评论输入框激活状态（即键盘弹出时）的占位符文本颜色。<br><br>   * 新增 [popupInputBoxTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#popupinputboxtextcolor) 属性，用于设置评论输入框激活状态（即键盘弹出时）已输入文本的颜色。<br><br>   * 新增 [inputBoxPromptTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-inputboxprompttextcolor) 属性，用于设置评论输入框未激活状态（即键盘收起时）的占位符文本颜色。<br><br>   * 新增 [FunctionEntranceButtonCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#functionentrancebuttoncornerradius) 属性，用于设置直播间右下角功能按钮（如购物车、互动工具按钮）的圆角。<br><br>   * 新增错误码 `BDLErrorCodeForceOffline`，表示当前观众已被封禁，无法进入直播间。更多信息请参见 [iOS 观播 SDK：错误码](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-error-codes)。<br><br>* **问题修复**<br><br>   修复了部分问题。 |
|2025\-07\-15 |1.60.0 |* **兼容性变更**<br><br>   修改了 `Podfile` 文件中 BPLive 的引用方式。更多信息请参见 [Step 1: 添加依赖](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。<br><br>* **优化项**<br><br>   优化了观看页实时抽奖功能的 UI 样式，提升用户体验，并支持在抽奖弹窗中展示奖品图片。 |
|2025\-07\-01 |1.59.0 |**问题修复**<br><br>修复了部分问题。 |

## 2025 年 6 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-06\-04 |1.58.0 |同步了 iOS 开播 SDK 的版本号。 |

## 2025 年 5 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-05\-20 |1.57.0 |* **优化项**<br><br>   完善了 SDK 日志上报信息，提升排查能力。<br><br>* **问题修复**<br><br>   修复了 SDK 初始化相关问题。 |
|2025\-05\-06 |1.56.1 |**问题修复**<br><br>修复了部分问题。 |

## 2025 年 4 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-04\-29 |1.56.0 |* **兼容性变更**<br><br>   * 修改了初始化方式。更多信息请参见 [Step 4: 初始化 BPLive](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#f951ba1a)。<br><br>   * 添加依赖时，删除 `pod 'RangersAppLog', :podspec => ' https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/RangersAppLog/6.16.2/RangersAppLog.podspec.json'`。更多信息请参见 [Step 1: 添加依赖](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。<br><br>   * 删除的方法<br><br>      在 `BDLShoppingCardController` 中，删除了商品 URL 加载时触发的回调 `openUrlBlock`。请使用 [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock) 代替。<br><br>   * 参数变更<br><br>      以下方法新增参数 `cardModel`（商品卡片模型），用于获取商品信息。<br><br>      * [viewTappedBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCardView) 在 `BDLCardView`<br><br>      * [cardViewTappedBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardView) 在 `BDLShoppingCardView`<br><br>      * [viewTappedBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLFloatingCardView) 在 `BDLFloatingCardView`<br><br>* **新功能**<br><br>   * 商品卡片<br><br>      新增以下商品卡片点击时触发的回调。<br><br>      * [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLFloatingController) 在 `BDLFloatingController`<br><br>      * [onCardClickBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLShoppingCardController-oncardclickblock) 在 `BDLShoppingCardController`<br><br>   * 初始化<br><br>      * 新增 SDK 初始化方法。更多信息请参见 [startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete)。<br><br>      * 支持获取 `BDLiveManager` 实例。更多信息请参见 [sharedInstance](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-sharedinstance)。<br><br>* **问题修复**<br><br>   修复了部分问题。 |
|2025\-04\-16 |1.55.1 |**优化项**<br><br>优化了部分越南语 UI 文本。 |
|2025\-04\-15 |1.55.0 |* **兼容性变更**<br><br>   * 参数变更<br><br>      以下方法中的参数 `reason` 修改为 `info`：<br><br>      * [onUserForceOfflineBlock](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#onuserforceofflineblock)<br><br>      * [basePlayerView:onUserForceOffline:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#baseplayerview-onuserforceoffline)<br><br>      * [playerView:onUserForceOffline:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#playerview-onuserforceoffline)<br><br>      * [floatingPlayer:onUserForceOffline:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#floatingplayer-onuserforceoffline)<br><br>   * 枚举值类型变更<br><br>      在 [BDLForceOfflineReason](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlforceofflinereason) 中，`BDLiveForceOfflineReasonMultiLogin` 修改为 `BDLForceOfflineReasonMultiLogin`，`BDLiveForceOfflineReasonCheckInTimeout` 修改为 `BDLForceOfflineReasonCheckInTimeout`。<br><br>* **新功能**<br><br>   * 在 [BDLForceOfflineReason](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlforceofflinereason) 中，新增以下观众被强制移出直播间的原因：<br><br>      * `BDLForceOfflineReasonIPBanned`（IP 地址被封禁）<br><br>      * `BDLForceOfflineReasonKickOut`（被踢出）<br><br>   * 支持将观众踢出直播间及封禁观众 IP 地址。<br><br>* **优化项**<br><br>   优化了观看页签到功能的 UI 样式，提升用户体验。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |
|2025\-04\-01 |1.54.0 |* **兼容性变更**<br><br>   * 删除了部分方法<br><br>      * 删除了用于设置是否允许观众在评论输入框中输入内容的方法 `textFieldShouldBeginEditing`。请改用方法 [textViewShouldBeginEditing](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-textviewshouldbeginediting)。<br><br>      * 在 [BDLCommentInputBaseView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentinputbaseview) 中，删除了用于自定义评论输入框的方法 `customizeTextField`。请改用 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 或 [BDLCommentBaseConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration%28Config%29) 中的属性。<br><br>      * 在 [BDLCommentInputBaseView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentinputbaseview) 中，删除了属性 `textField`（评论输入框）。<br><br>      * 在 [BDLCommentBaseConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration%28Config%29) 中，删除了属性 `inputTextIconImage`（评论输入框左侧图标）。<br><br>   * 方法名变更<br><br>      将用于重置评论输入框的方法 `resetTextField:` 更名为 [resetTextView:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#resettextview)。<br><br>* **新增功能**<br><br>   * 数据上报。<br><br>      新增对数据上报的支持。详情请参见 [externalReportConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#externalreportconfig)。<br><br>   * 评论输入框自定义<br><br>      * 支持设置评论输入框允许输入的最大字符数。详情请参见 [commentInputCountLimit](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentinputcountlimit)。<br><br>      * 支持设置评论输入框内输入文本的颜色。详情请参见 [inputBoxTextColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxtextcolor)。 |

## 2025 年 3 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-03\-18 |1.53.0 |* **兼容性变更**<br><br>   * 删除了部分属性<br><br>      在 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 中，删除了 `likeIconImage`（未点赞评论图标）和 `likedIconImage`（已点赞评论图标）。请改用 [commentLikeIcon](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-commentlikeicon) 和 [commentLikedIcon](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-commentlikedicon)。<br><br>   * 弃用部分属性<br><br>      在 [BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29) 中，属性 `welcomeTextColor`（欢迎语文本颜色）已弃用。请改用 [systemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-systemcommentcolor)。<br><br>   * 作用范围变更<br><br>      * [commentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentfont) 现仅支持设置非主播评论的字体、字号及其他属性。如需设置主播评论的相关属性，请使用 [hostCommentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hostcommentfont)。<br><br>      * [hostCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hostcommentcolor) 现仅支持设置主播评论的文本颜色。如需设置主播标签颜色，请使用 [hostTagColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hosttagcolor)。<br><br>* **新增功能**<br><br>   * 评论输入框自定义<br><br>      * 支持设置是否允许观众在评论输入框中输入内容。详情请参见 [textFieldShouldBeginEditing](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-textviewshouldbeginediting)。<br><br>      * 支持设置评论输入框在非编辑状态（即键盘未弹出时，观众进直播间前后）的以下属性：<br><br>         * 背景色。详情请参见 [inputBoxBackgroundColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxbackgroundcolor)。<br><br>         * 圆角。详情请参见 [inputBoxCornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxcornerradius)。<br><br>         * 边框宽度。详情请参见 [inputBoxBorderWidth](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxborderwidth)。<br><br>         * 边框颜色。详情请参见 [inputBoxBorderColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxbordercolor)。<br><br>         * 占位文本颜色。详情请参见 [inputBoxPromptColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#inputboxpromptcolor)。<br><br>   * 评论区样式自定义<br><br>      * 支持设置竖屏模式下直播间描述和欢迎语的以下属性：<br><br>         * 标签的字体、字号及其他属性。详情请参见 [systemTagFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#systemtagfont)。<br><br>         * 标签颜色。详情请参见 [systemTagColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#systemtagcolor)。<br><br>         * 正文的字体、字号及其他属性。详情请参见 [systemCommentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#systemcommentfont)。<br><br>         * 正文文本颜色。详情请参见 [systemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-systemcommentcolor)。<br><br>      * 支持设置相邻评论单元格之间的间距。详情请参见 [distanceBetweenCell](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#distancebetweencell)。<br><br>      * 支持设置评论列表底部与评论输入框顶部之间的间距。详情请参见 [commentListViewBottomMargin](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentlistviewbottommargin)。<br><br>      * 支持设置下拉刷新组件内容颜色，例如 `↓ Pull to load more comments`。详情请参见 [commentListPullToRefreshColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#commentlistpulltorefreshcolor)。<br><br>      * 支持设置主播标签颜色以及主播评论的字体、字号等属性。更多信息请参见[hostTagColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hosttagcolor)和[hostCommentFont](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hostcommentfont)。<br><br>   * 新增属性[floatingControllerConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#floatingcontrollerconfig)（悬浮窗控制器配置），支持设置当键盘弹出时是否自动隐藏所有悬浮窗控件，如商品浮窗、浮标广告和互动工具悬浮窗。<br><br>* **问题修复**<br><br>   修复了部分问题。 |
|2025\-03\-04 |1.52.0 |* **兼容性变更**<br><br>   * 逻辑更新<br><br>      更新了直播流卡顿处理逻辑。当[isNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#isneedautodemote)的值为`YES`时，新增检测以[backupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLBasePlayerConfiguration-backupdowngradewhenstall)的值直接判断是否切换主流和备流。<br><br>   * 删除部分方法<br><br>      在[BDLMultiLanguageView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlmultilanguageview)中，<br><br>      * 删除了用于显示语言选择对话框视图的`show`方法。请改用[bottomShowInView:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bottomshowinview-completion)方法。<br><br>      * 删除了用于隐藏语言选择对话框视图的`hide`方法。请改用[hideWithCompletion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hidewithcompletion)方法或[hideWithAnimation:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#hidewithanimation-completion)方法。<br><br>* **新功能**<br><br>   * 主播账号<br><br>      * 支持关注主播。<br><br>      * 新增[businessAccountConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#businessaccountconfig)（主播账号配置）属性，支持设置“关注”和“已关注”状态按钮的文本及背景图片。<br><br>   * 多语言<br><br>      * 支持以下语言：<br><br>         * 韩语<br><br>         * 泰语<br><br>         * 越南语<br><br>         * 阿拉伯语<br><br>         * 土耳其语<br><br>         * 西班牙语<br><br>         * 印尼语<br><br>         * 葡萄牙语<br><br>         * 俄语<br><br>      * [highLightString](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#highlightstring)现已支持多语言。 |

## 2025 年 2 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-02\-24 |1.51.1 |同步了 iOS 开播 SDK 的版本号。 |
|2025\-02\-18 |1.51.0 |* **兼容性变更**<br><br>   * 删除部分方法、属性、回调和视图<br><br>      * 删除`BDLBottomNoticeView`（横屏模式直播间入口消息视图）和`BDLEnterLiveRoomNoticeView`（竖屏模式直播间入口消息视图）。请改用[BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCommentAndNoticeView)（评论与通知视图）。<br><br>      * 删除`BDLBottomNoticeViewProtocol`（底部消息通知视图协议）。<br><br>      * 在[BDLTopCommentView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdltopcommentview)中，删除了`shouldHandleGestureRecognizerWithTouch:`方法（是否处理手势）。<br><br>      * 在[BDLFloatingCardView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlfloatingcardview)中，删除了`containerView`（容器视图）、`titleLabel`（商品名称标签）、`highLightBgView`（刊例价背景视图）、`highLightLabel`（刊例价标签）、`imageView`（商品图片）、`closeButton`（关闭按钮）、`goImageView`（GO 图片视图）和`explainingButton`（讲解标签）属性。<br><br>      * 在[BDLCommentView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentview)中，<br><br>         * 删除了底部消息通知视图的`bottomNoticeView`属性。<br><br>         * 删除了自定义底部消息通知视图的`customizeBottomNoticeView`方法。请改用[customizeCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLMenuBarView-customizecommentandnoticeview)方法自定义横屏和竖屏模式直播间的评论与通知视图。<br><br>      * 在[BDLLivePullViewController()](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLivePullViewController%28%29)中，删除了评论视图的`commentView`属性。请改用评论与通知视图的[commentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLivePullViewController%28%29-commentandnoticeview)属性。<br><br>      * 在[BDLMenuBarView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlmenubarview)中，<br><br>         * 删除了横屏模式直播间菜单栏评论视图的`commentView`属性。请改用横屏模式直播间评论与通知视图的[commentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#commentandnoticeview-2)属性。<br><br>         * 删除了横屏模式直播间菜单栏评论视图自定义方法`customizeCommentView`。请改用横屏模式直播间评论与通知视图自定义方法[customizeCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#customizecommentandnoticeview)。<br><br>      * 由于置顶评论 UI 样式变更，删除了`topTagFont`属性（[BDLCommentViewConfiguration(Config)](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29)中置顶标签的字体及字号）。<br><br>   * 方法迁移<br><br>      * 以下方法已从[BDLCommentView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCommentView)迁移至[BDLCommentAndNoticeView](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentandnoticeview)。<br><br>         * `topCommentClickBlock`（当置顶文本评论被点击时触发的回调）<br><br>         * `topCommentNicknameClickBlock`（当置顶评论的昵称被点击时触发的回调）<br><br>      * 以下方法已从[BDLLivePullViewControllerConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdllivepullviewcontrollerconfig)迁移至[BDLCommentAndNoticeViewConfiguration](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlcommentandnoticeviewconfiguration)。<br><br>         * `customizePortraitCommentViewHeight`用于自定义竖屏模式下直播间评论区（包含输入框）的高度。<br><br>         * `customizeCommentView`用于自定义竖屏模式下直播间的评论视图。<br><br>         * `customizeNoticeContainerView`用于自定义通知容器视图。<br><br>   * 更新了[setNickname:complete: ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLUserInfoConfiguration-setnickname-complete)方法的实现逻辑。该方法现在仅支持在观众加入直播间前调用。注册失败时，SDK会使用`nickname`的值完成注册，并在下次尝试时触发完成回调。若再次注册失败，SDK将在后续尝试中持续重试，直到注册成功。<br><br>   * 默认值变更<br><br>      * 置顶评论显示的行数默认值由`2`变更为`1`。详情请参见[rowsOfTopComment](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-rowsoftopcomment)。<br><br>      * 竖屏模式下直播间评论区（包含评论输入框）高度的默认值由完整直播间高度的0.4倍变更为241点。详情请参见[customizePortraitCommentViewHeight](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLCommentAndNoticeViewConfiguration-customizeportraitcommentviewheight)。<br><br>   * 适用范围变更<br><br>      [backgroundColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentBaseConfiguration%28Config%29-backgroundcolor)属性现在也适用于进房消息。<br><br>* **新增功能**<br><br>   * 商品卡片菜单<br><br>      新增[productOriginalPriceShowStrikethrough](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#productoriginalpriceshowstrikethrough)方法，用于设置是否在刊例价上显示删除线。<br><br>   * 商品浮窗<br><br>      新增[cornerRadius](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#cornerradius-2)属性，用于设置商品浮窗背景的圆角。<br><br>   * 进房消息<br><br>      * 新增[joinRoomMsgNicknameColor ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-joinroommsgnicknamecolor)属性，用于设置进房消息中昵称文本的颜色。<br><br>      * 新增[joinRoomMsgContentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLCommentViewConfiguration%28Config%29-joinroommsgcontentcolor)属性，用于设置进房消息内容文本的颜色。<br><br>   * 置顶评论<br><br>      新增[topCommentView:didClickComment: ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#topcommentview-didclickcomment)方法。当观众点击置顶评论的文本或空白区域时，SDK会调用该方法。<br><br>   * 直播间配置<br><br>      新增评论与通知视图的配置项。详情请参见[commentAndNoticeViewConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLLiveRoomConfiguration-commentandnoticeviewconfig)。<br><br>   * 错误码<br><br>      新增错误码`BDLErrorCodeUserHasJoinLiveRoom`，表示调用[setNickname:complete: ](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#BDLUserInfoConfiguration-setnickname-complete)方法设置用户昵称失败。详情请参见[iOS 观播 SDK：错误码](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-error-codes)。<br><br>* **优化项**<br><br>   优化了商品卡片、置顶评论和进房消息的 UI 样式，提升用户体验。 |

## 2025 年 1 月

|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-01\-21 |1.50.0 |* **兼容性变更**<br><br>   删除的属性<br><br>   在`BDLPlayerLandscapeConfiguration`中，删除了`popularityFont`（人气标签文本的字体及字号）和`popularityImage`（人气图标）属性。<br><br>* **新增功能**<br><br>   直播间人气<br><br>   支持配置人气图标，以及人气标签文本的字体、字号和颜色。 |
|2025\-01\-08 |1.49.0 |* **兼容性变更**<br><br>   * 在`BDLPlayerViewDelegate`中，删除了观众双击播放器时调用的`playerViewDidDoubleTap:`方法。<br><br>   * 变更了 SDK 导入 URL 和集成 SDK 时需添加的 BPLive 依赖项。详情请参见[集成 iOS 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN)。<br><br>* **新增功能**<br><br>   * 加载直播流发生错误时，可通过`liveError`获取具体错误信息。<br><br>   * 日志查询新增单点追踪支持，提升定位 SDK 问题的能力。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |

## 2024 年 12 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-12\-24 |1.48.0 |**已修复的问题**<br><br>修复了部分问题。 |
|2024\-12\-10 |1.47.3 |* **兼容性变更**<br><br>   竖屏模式下自定义直播间 `customizePageAdView` 的 frame 方法发生变更：不再通过 `mas_remakeConstrain` 在 `customizeViewConstraints` 中设置，而需直接修改 `frame`。但 `frame.origin` 会被忽略，仅可修改 `frame.size`。<br><br>* **新增功能**<br><br>   支持在直播间右上角显示自定义悬浮视图。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |
|2024\-12\-03 |1.47.2 |**新增功能**<br><br>支持使用 TTSDK 的静态库版本。更多信息请参见 [使用 TTSDK 的静态库版本](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b4f49ac2)。 |

## 2024 年 11 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-11\-26 |1.47.1 |**已修复的问题**<br><br>修复了部分问题。 |

## 2024 年 10 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-10\-31 |1.46.1 |* **优化项**<br><br>   适配 iOS 18。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |
|2024\-10\-24 |1.46.0 |* **新增功能**<br><br>   * 应用播放媒体的 Now Playing 信息区块。<br><br>      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71c238a4a84348d3833ad3942d38ede2~tplv-goo7wpa0wc-image.image)<br><br>      * 新增自定义 Now Playing 信息的支持。<br><br>      * 新增设置是否响应 Now Playing 信息区块用户操作的支持。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |
|2024\-10\-15 |1.45.0 |* **优化项**<br><br>   优化竖屏模式下直播间的 UI 风格。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |

## 2024 年 9 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-09\-12 |1.44.0 |* 新增签到功能。<br><br>* 适配 Xcode 16。<br><br>* 在 `BDLRiskWarningView` 中，`maskView` 属性重命名为 `bottomMaskView`。<br><br>* 在 `BDLPlayerView` 中，`maskView` 属性重命名为 `playerMaskView`。 |
|2024\-09\-04 |1.43.3 |修复了部分问题。 |

## 2024 年 8 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-08\-22 |1.43.2 |新增 [showCloseButtonWhenClearingScreen](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#showclosebuttonwhenclearingscreen) 属性，用于配置清屏时是否显示关闭直播间按钮。 |
|2024\-08\-15 |1.43.0 |SDK 现已支持横屏模式下显示购物车图标。 |
|2024\-08\-06 |1.42.1 |修复了部分问题。 |
|2024\-08\-01 |1.42.0 |* 变更 `TTNetworkManager` 依赖的版本号。更多信息请参见 [Step 1: 添加依赖](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。<br><br>* 在 `BDLBasePlayerConfiguration` 中新增 `isNeedAutoDemote` 方法，用于设置直播流网络类型卡顿时是否支持自动降级或提示。 |

## 2024 年 7 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-07\-23 |1.41.0 |优化直播流预约逻辑。 |

## 2024 年 6 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-06\-28 |1.40.1 |* 在 `BDLUpperAdView` 的 `viewTappedBlock` 方法中新增 `enableFloating` 参数。<br><br>* 修复了部分问题。 |
|2024\-06\-26 |1.40.0 |* 删除 [BDLActivity](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-type-for-ios-zh-CN#0b6ae4e5) 中的 `nickName` 属性。<br><br>* 弃用 [BDLLiveEngine](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-type-for-ios-zh-CN#e53a9ad6) 中的 `joinLiveRoomWithActivity:` 方法。<br><br>* 在 `BDLLiveRoomConfiguration` 中新增属性 `userInfoConfig`（用户信息配置）。<br><br>* 新增用户信息配置 `BDLUserInfoConfiguration`，包含 `setNickname:complete:` 方法，用于在公开认证模式下设置用户昵称。<br><br>* 在 `BDLCommentView` 中新增属性 `imageTextButton`（竖屏模式下图文菜单按钮）和方法 `imageTextClickBlock`（竖屏模式下图文菜单按钮点击回调）。<br><br>* 在 `BDLCommentViewConfiguration` 中新增属性 `imageTextButtonImage`（竖屏模式下图文菜单按钮图片）。<br><br>* 支持竖屏模式下显示图文菜单。<br><br>* 优化 UI 风格。<br><br>* 修复了部分问题。 |
|2024\-06\-07 |1.39.0 |更新集成 SDK 时需添加的 BPLive 依赖。更多信息请参见 [Step 1: 添加依赖](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。 |

## 2024 年 5 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-05\-30 |1.35.0 |删除了用于置顶评论和 H5 页面（如观众点击商品卡片或广告后在浮层中展示的页面）的 `BDLAlertController`，新增了 `BDLPopupTopCommentView` 和 `BDLPopupWebView`，以提升兼容性。 |

## 2024 年 4 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-04\-29 |1.34.0 |* 新增礼物奖励功能。<br><br>* 修复了 PiP 相关问题。 |
|2024\-04\-15 |1.33.0 |* 支持优化 SDK 包体大小。更多信息，请参见 [优化 SDK 包体积](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#762f64ce)。<br><br>* 修复了部分问题。 |

## 2024 年 3 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-03\-27 |1.32.2 |修复了部分问题。 |
|2024\-03\-11 |1.32.1 |* 优化了依赖项。仅集成 iOS 观播 SDK 时，不再需要 `TTVideoEditor` 依赖。更多信息，请参见 [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-ios#6fbbbde0)。<br><br>* 修复了部分问题。 |

## 2024 年 2 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-02\-29 |1.32.0 |支持在竖屏模式下展示直播间描述。 |

## 2024 年 1 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2024\-01\-24 |1.26.0 |* 升级至此版本时，需修改 `Podfile` 文件，添加 BPLive 依赖。更多信息，请参见 [Integrating the Viewer SDK for iOS](https://docs.byteplus.com/en/byteplus-livesaas/docs/integrating-the-viewer-sdk-for-ios?version=v1.0#6fbbbde0)。<br><br>* 新增以下功能：<br><br>   * 自定义分享地址<br><br>   * 倒计时<br><br>   * 预约直播流<br><br>   * 场馆切换<br><br>   * 邀请海报<br><br>   * 系统通知<br><br>   * 欢迎语<br><br>   * 风险提示<br><br>   * 全屏水印<br><br>   * 问卷<br><br>   * 投票<br><br>   * 实时抽奖<br><br>      更多信息，请参见 [Feature comparison between SaaS and aPaaS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas)。<br><br>* 优化点赞功能：支持展示点赞数及自定义相关配置。<br><br>* 支持上报直播流质量数据。 |

## 2023 年 8 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2023\-08\-04 |1.25.2 |修复了评论删除相关 bug。 |

## 2023 年 7 月

|发布时间 |版本 |接口行为 |
|---|---|---|
|2023\-07\-20 |1.25.0 |修复了部分问题。 |
