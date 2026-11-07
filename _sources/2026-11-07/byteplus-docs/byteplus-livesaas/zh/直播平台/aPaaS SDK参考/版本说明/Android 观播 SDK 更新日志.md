---
title: "Android 观播 SDK 更新日志"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN"
---

Android 观播 SDK 更新日志提供了所有更新的详细记录。本文件记录了每个版本的新功能、改进、兼容性变更及已修复的问题，帮助您及时了解最新动态并规划升级。

<span id="411ec2d4"></span>
## 2026年4月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2026\-04\-28 |1.66.3 |**已修复的问题**<br><br>修复了若干已知的偶发性崩溃问题。 |


<span id="5b5274a3"></span>
## 2025年11月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-11\-12 |1.65.0 |**改进**<br><br>支持更多 SDK 语言类型：<br><br><br>* 塔加拉语<br><br>* 高棉语<br><br>* 老挝语<br><br>* 缅甸语<br><br>* 马来语<br><br>* 印地语<br><br>* 法语<br><br>* 德语<br><br>* 意大利语 |


<span id="5d9e0fee"></span>
## 2025年10月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-10\-28 |1.64.1 |**已修复的问题**<br><br>修复了部分问题。 |


<span id="8f3765ba"></span>
## 2025年9月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-09\-25 |1.64.0 |**改进**<br><br><br>* 适配了 Android 16 KB 功能。<br><br>* 支持回放日志上报，增强故障排查能力。 |
|2025\-09\-09 |1.63.0 |**已修复的问题**<br><br>修复了部分问题。 |


<span id="5537e8e4"></span>
## 2025年8月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-08\-12 |1.62.0 |同步了 Android 开播 SDK 的版本号。 |


<span id="1496aac1"></span>
## 2025年7月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-07\-30 |1.61.4 |**已修复的问题**<br><br>修复了部分问题。 |
|2025\-07\-28 |1.61.3 |* **兼容性变更**<br><br>   在`CustomSettings`中，删除了以下方法：<br><br>   * 删除了`setCommentEditViewHintTextColor`方法。请使用[setPopupInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#5fc5536f)和[setInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#e349d9b3)替代。<br><br>   * 删除了`setCommentEditViewTextColor`方法。请使用[setPopupInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#a128a852)和[setInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#bb581984)替代。<br><br>* **新功能**<br><br>   * 新增[setTopCommentBackgroundWidthFitContent](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#115fbc19)方法，用于设置置顶评论背景宽度是否随内容宽度自适应。<br><br>   * 新增[setTopCommentViewCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#8b6e0523)方法，用于设置置顶评论背景的圆角。<br><br>   * 新增[setTopCommentNicknameColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#36d938dc)方法，用于设置置顶评论昵称的颜色。<br><br>   * 新增[setTopCommentNicknameFontSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#e85f2897)方法，用于设置置顶评论昵称的字体大小。<br><br>   * 新增[setTopCommentNicknameFontStyle](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#9891737b)方法，用于设置置顶评论昵称的字体。<br><br>   * 新增[setTopCommentContentLineSpacingExtra](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#826adc59)方法，用于设置置顶评论内容的行间距。<br><br>   * 新增[setTopCommentTagColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#452857ff)方法，用于设置置顶评论昵称左侧竖线的颜色。<br><br>   * 新增[setTopCommentBackgroundColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#b5661b0f)方法，用于设置置顶评论的背景色。<br><br>   * 新增[setCommentContentLineSpacingExtra](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#016961d8)方法，用于设置评论内容的行间距。<br><br>   * 新增[setCommentCellCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#992d58e3)方法，用于设置评论单元格的圆角。<br><br>   * 新增[setFunctionEntranceButtonCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#2a63cdb6)方法，用于设置直播间右下角功能按钮（如购物车、互动工具按钮）的圆角。<br><br>   * 新增[setPopupInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#5fc5536f)方法，用于设置编辑评论输入框时（键盘弹出时）占位文字颜色。<br><br>   * 新增[setPopupInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#a128a852)方法，用于设置编辑评论输入框时（键盘弹出时）已输入文字颜色。<br><br>   * 新增[setInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#e349d9b3)方法，用于设置未编辑评论输入框时（键盘收起时）占位文字颜色。<br><br>   * 新增[setInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#bb581984)方法，用于设置未编辑评论输入框时（键盘收起时）已输入文字颜色。<br><br>   * 新增 [setInputBoxCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#40f70e3f) 方法，用于设置评论输入框在未编辑状态（键盘隐藏时）的圆角。<br><br>* **已修复的问题**<br><br>   修复了部分问题。 |
|2025\-07\-15 |1.60.0 |**功能优化**<br><br>优化观众端实时抽奖功能的 UI 样式，提升用户体验，支持在抽奖弹窗中展示奖品图片。 |
|2025\-07\-01 |1.59.0 |**已修复的问题**<br><br>修复了部分问题。 |


<span id="f7d1c2fd"></span>
## 2025年6月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-06\-04 |1.58.0 |**新功能**<br><br>支持设置 PiP 窗口在锁屏时是否暂停视频回放。更多信息，请参见 [setPauseOnLockScreenInMiniWindow](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#f8150cf4)。 |


<span id="0c667da8"></span>
## 2025年5月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-05\-20 |1.57.1 |**功能优化**<br><br>优化 SDK 日志上报信息，提升故障排查能力。 |


<span id="bd4b90e3"></span>
## 2025年4月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-04\-29 |1.56.0 |**已修复的问题**<br><br>修复了部分问题。 |
|2025\-04\-15 |1.55.2 |* **兼容性变更**<br><br>   参数变更<br><br>   以下方法中的参数 `reason` 修改为 `info`：<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline) 在 `ITVULiveRoomServerListener`<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline-2) 在 `LiveRoomStatusListener`<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline-3) 在 `SinglePlayerListener`<br><br>* **新功能**<br><br>   * 在 [BDLForceOfflineReason](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#7321845b) 中新增观众被强制移出直播间的原因：<br><br>      * `BDLiveForceOfflineReasonIPBanned`（IP 地址被封禁）<br><br>      * `BDLiveForceOfflineReasonKickOut`（被踢出）<br><br>   * 支持将观众踢出直播间及封禁观众 IP 地址。<br><br>* **功能优化**<br><br>   优化观众端签到功能的 UI 样式，提升用户体验。 |
|2025\-04\-07 |1.54.2 |**已修复的问题**<br><br>Android 观播 SDK 1.49.0 \- 1.54.1 版本存在日志事件上报问题。为避免影响线上问题排查，请将这些版本升级至 1.54.2。 |
|2025\-04\-03 |1.54.1 |**已修复的问题**<br><br>修复了部分问题。 |
|2025\-04\-01 |1.54.0 |* **兼容性变更**<br><br>   修改 SDK 版本后缀。更多信息，请参见 [集成 Android 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN)。<br><br>   * 导入全量功能的 Android 观播 SDK 时，SDK 版本后缀由 `pull-global:VersionNumber.external` 变更为 `pull:VersionNumber.globalFull`。例如，使用 `com.bytedance.bdlive:bdlive-pull-global:1.53.0.external` 导入全量功能的 Android 观播 SDK 1.53.0，使用 `com.bytedance.bdlive:bdlive-pull:1.54.0.globalFull` 导入全量功能的 Android 观播 SDK 1.54.0。<br><br>   * 导入不包含超低延时直播功能的 Android 观播 SDK 时，SDK 版本后缀由 `pull-global-remove-rtc:VersionNumber.external` 变更为 `pull:VersionNumber.globalLite`。例如，使用 `com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external` 导入不包含超低延时直播功能的 Android 观播 SDK 1.53.0，使用 `com.bytedance.bdlive:bdlive-pull:1.54.0.globalLite` 导入不包含超低延时直播功能的 Android 观播 SDK 1.54.0。<br><br>* **新功能**<br><br>   * 数据上报。<br><br>      支持数据上报。更多信息，请参见 [setBdlExternalReportConfiguration](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#543e5973)。<br><br>   * 评论输入框自定义<br><br>      支持设置评论输入框允许输入的最大字符数。更多信息，请参见 [setCommentInputCountLimit](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#542ef80d)。 |


<span id="da2a39bb"></span>
## 2025年3月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-03\-18 |1.53.0 |* **兼容性变更**<br><br>   * 部分方法弃用<br><br>      设置直播间欢迎语字体颜色的 `setWelcomeMsgFontColor` 方法已弃用。请使用 [setSystemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor) 方法。<br><br>   * 适用范围变更<br><br>      * [setHostCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentcolor) 现仅支持设置主播评论的字体颜色。如需设置主播标签颜色，请使用 [setHostTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontcolor)。<br><br>      * [setCommentContentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentcontentfontstyle) 现仅支持设置观众评论的字体。如需设置主播评论字体，请使用 [setHostCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontstyle)。<br><br>* **新功能**<br><br>   * 评论输入框自定义<br><br>      * 支持设置观众点击评论输入框时是否弹出键盘。更多信息，请参见 [commentShouldInterceptEditing](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#6cc8bcc5)。<br><br>      * 支持设置评论输入框的事件拦截监听器。更多信息，请参见[setCommentEditingListener](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#71fed577)。<br><br>      * 支持设置评论输入框在非编辑状态（即键盘未弹出时）下的以下内容：<br><br>         * 占位文本。更多信息，请参见[setInputBoxPrompt](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#8682c301)。<br><br>         * 占位文本颜色。更多信息，请参见[setInputBoxPromptColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#04aa818c)。<br><br>         * 背景颜色。更多信息，请参见[setInputBoxBackgroundColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#4a693500)。<br><br>         * 圆角半径。更多信息，请参见[setInputBoxCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#740ee52f)。<br><br>         * 边框宽度。更多信息，请参见[setInputBoxBorderWidth](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#0e05259a)。<br><br>         * 边框颜色。更多信息，请参见[setInputBoxBorderColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN#f81a58ab)。<br><br>   * 自定义评论区样式<br><br>      * 支持设置直播间描述在竖屏模式和欢迎语中的以下内容：<br><br>         * 标签的字体、字号和颜色。更多信息，请参见[setSystemCommentTagFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontstyle)、[setSystemCommentTagFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontsize)和[setSystemCommentTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontcolor)。<br><br>         * 正文的字体、字号和颜色。更多信息，请参见[setSystemCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentfontstyle)、[setSystemCommentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentfontsize)和[setSystemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor)。<br><br>      * 支持设置相邻评论之间的间距。更多信息，请参见[setCommentItemSpacing](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentitemspacing)。<br><br>      * 支持设置评论列表底部与评论输入框顶部之间的间距。更多信息，请参见[setRoomCommentListViewBottomMargin](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setroomcommentlistviewbottommargin)。<br><br>      * 支持设置下拉刷新组件内容颜色，例如`↓ 下拉加载更多评论`。更多信息，请参见[setCommentListPullToRefreshColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentlistpulltorefreshcolor)。<br><br>      * 支持设置非主播昵称和观众评论内容的字号。更多信息，请参见[setCommentNicknameFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentnicknamefontsize)和[setCommentContentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentcontentfontsize)。<br><br>      * 支持设置主播标签的字号和颜色。更多信息，请参见[setHostTagFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontsize)和[setHostTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontcolor)。<br><br>      * 支持设置主播评论内容的字体和字号。更多信息，请参见[setHostCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontstyle)和[setHostCommentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontsize)。 |
|2025\-03\-04 |1.52.1 |* **兼容性变更**<br><br>   * 逻辑更新<br><br>      更新了直播流卡顿时的处理逻辑。当[setNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setneedautodemote)的参数值为`true`时，新增根据[setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall)的参数值判断是否直接切换主流和备流的逻辑。<br><br>   * 用于设置部分自定义文本所需语言类型的`setLanguageType`方法已废弃。<br><br>* **新功能**<br><br>   * 新增`TVULiveRoomServer`实例创建成功时触发的回调。更多信息，请参见[onRoomServerCreated](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#38dde242)。<br><br>   * 新增[getDynamicSettings](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#2323d292)方法。可在观众进入直播间前或后调用该方法，自定义直播间相关设置。<br><br>   * 支持在观众进入直播间后动态更新直播间 UI 和交互行为。更多信息，请参见[动态更新直播间 UI 和交互行为](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#7b1d80cb)。<br><br>   * 主播账号<br><br>      * 支持关注主播。<br><br>      * 新增自定义鉴权模式下观众关注事件的回调类。更多信息，请参见[BDLUserFollowListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#35d14b67)。<br><br>      * 支持设置：<br><br>         * 主播被关注或未被关注时按钮的文本和背景图片。<br><br>         * 自定义鉴权模式下观众关注主播事件的监听器。<br><br>            更多信息，请参见[动态自定义设置](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN)。<br><br>   * 多语言<br><br>      支持以下语言：<br><br>      * 韩语<br><br>      * 泰语<br><br>      * 越南语<br><br>      * 阿拉伯语<br><br>      * 土耳其语<br><br>      * 西班牙语<br><br>      * 印尼语<br><br>      * 葡萄牙语<br><br>      * 俄语 |


<span id="1cfaefb3"></span>
## 2025年2月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-02\-24 |1.51.1 |**修复的问题**<br><br>修复了部分问题。 |
|2025\-02\-18 |1.51.0 |* **兼容性变更**<br><br>   * 删除的方法<br><br>      由于置顶评论的 UI 样式变更，删除以下方法：<br><br>      * `setTopCommentTagFontStyle` 用于设置置顶标签的字体。<br><br>      * `setTopCommentTagFontSize` 用于设置置顶标签的字体大小。<br><br>      * `setTopCommentTagFontColor` 用于设置置顶标签的文字颜色。<br><br>   * 默认值变更<br><br>      * 置顶评论显示的最大行数默认值由 `2` 改为 `1`。更多信息，请参见 [setTopCommentRowCount](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#261f08a4)。<br><br>      * 竖屏模式下直播间评论区高度的默认值由屏幕高度的 1/3 改为 194 dp。更多信息，请参见 [setPortraitCommentAreaHeight](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#4338c1b2)。<br><br>   * 适用范围变更<br><br>      [setCommentItemBgColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#2b82be95) 方法现在也适用于进场消息。<br><br>* **新功能**<br><br>   商品卡片菜单<br><br>   支持设置是否在刊例价上显示删除线。更多信息，请参见 [setProductOriginalPriceShowStrikethrough](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#4a00b94d)。<br><br>* **优化**<br><br>   优化了商品卡片、置顶评论和进场消息的 UI 样式，提升用户体验。 |


<span id="21f31c7d"></span>
## 2025年1月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-01\-21 |1.50.0 |**新功能**<br><br>支持设置热度标签文字的字体大小和颜色。更多信息，请参见 [setPeopleCountFontSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#d55a37d1) 和 [setPeopleCountTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#08753ee9)。 |
|2025\-01\-08 |1.49.0 |* **新功能**<br><br>   日志查询新增单点追踪能力，提升 SDK 问题定位能力。<br><br>* **问题修复**<br><br>   修复了部分问题。 |


<span id="a40194d6"></span>
## 2024年12月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-12\-24 |1.48.0 |**问题修复**<br><br>修复了部分问题。 |
|2024\-12\-10 |1.47.3 |* **兼容性变更**<br><br>   参数变更<br><br>   在 `addChildViewInLinearLayout` 方法中，用于指定直播间自定义浮标视图组件显示位置的参数由 `isLeftTop` 改为 `location`。<br><br>* **新功能**<br><br>   支持在直播间右上角显示自定义浮标视图组件。 |


<span id="73bc45d7"></span>
## 2024年11月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-11\-26 |1.47.2 |* **新功能**<br><br>   浮标广告<br><br>   支持设置浮标广告是否显示白色边框和背景。<br><br>* **问题修复**<br><br>   修复了部分问题。 |
|2024\-11\-07 |1.46.3 |* **新功能**<br><br>   渐变遮罩<br><br>   支持设置竖屏模式下直播间顶部是否显示渐变遮罩。若视频背景为白色，显示渐变遮罩可提升直播间顶部白色文字的可见性。<br><br>* **问题修复**<br><br>   修复了部分问题。 |


<span id="0384dd75"></span>
## 2024年10月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-10\-31 |1.46.2 |* **优化**<br><br>   兼容 Android 15。<br><br>* **问题修复**<br><br>   修复了部分问题。 |
|2024\-10\-28 |1.46.1 |**问题修复**<br><br>修复了部分问题。 |
|2024\-10\-24 |1.46.0 |**问题修复**<br><br>修复了部分问题 |
|2024\-10\-15 |1.45.0 |* **优化**<br><br>   优化了竖屏模式下直播间的 UI 样式。<br><br>* **问题修复**<br><br>   修复了部分问题。 |


<span id="6ac25cae"></span>
## 2024年9月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-09\-12 |1.44.0 |新增签到功能。 |
|2024\-09\-04 |1.43.4 |修复了部分问题。 |


<span id="9b00f991"></span>
## 2024年8月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-08\-28 |1.43.3 |修复了部分问题。 |
|2024\-08\-22 |1.43.2 |新增 [setShowCloseButtonWhenClearingScreen](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setshowclosebuttonwhenclearingscreen) 方法，用于配置清屏时是否显示关闭直播间按钮。 |
|2024\-08\-20 |1.43.1 |优化了竖屏模式下直播间底部购物车和礼物图标的可点击区域。 |
|2024\-08\-15 |1.43.0 |* 支持横屏模式下显示购物车图标。<br><br>* SDK 已从 JCenter 迁移至 Maven Central。 |
|2024\-08\-06 |1.42.1 |修复了部分问题。 |
|2024\-08\-01 |1.42.0 |新增 `setNeedAutoDemote` 方法，用于设置在直播流过程中网络延迟时，是否支持自动降级或提供提示。 |


<span id="4c21b251"></span>
## 2024年7月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-07\-23 |1.41.0 |优化了预约直播流逻辑。 |


<span id="38c9288e"></span>
## 2024年6月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-06\-27 |1.40.0 |* 在 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#joinLiveRoom) 方法中，新增参数 `joinRoomConfig`，并弃用参数 `activityId`、`token`、`roomAuthMode` 和 `isPortrait`。<br><br>* 在 `setPublicCommentNickName` 方法中，新增参数 `nameRegisterListener`。<br><br>* 新增 [JoinRoomConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#f39b2118)，用于加入完整直播间的配置。<br><br>* 新增 [JoinResultListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#610d4532)，用于完整直播间加入结果的回调类，包含 [onJoinSuccess](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#fc43f86c)（加入成功）和 [onJoinFailed](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#7ff8f393)（加入失败）。<br><br>* 新增 `PublicNickNameRegisterListener`，用于直播间认证模式为公开时昵称注册结果的回调类，包含 `onRegisterSuccess` 注册成功和 `onRegisterFail` 注册失败。<br><br>* 优化了 UI 样式。<br><br>* 修复了部分问题。 |
|2024\-06\-18 |1.39.3 |* 在 `TVUSinglePlayerView` 中新增 `setCoverImageContainerVisibility` 方法，用于配置直播间封面图容器的可见状态。<br><br>* 修复了部分问题。 |
|2024\-06\-12 |1.39.2 |修复了部分问题。 |
|2024\-06\-11 |1.39.1 |* 新增 [showFloatPermissionDialogInLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#98fe08db) 方法，用于在完整直播间显示悬浮窗权限请求弹窗。<br><br>* 新增 [FloatUtil](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil-zh-CN)，直播间悬浮窗工具类，包含 [checkPermission](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil-zh-CN#4b3dc68a) 和 [requestPermission](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil-zh-CN#f53394dc) 方法，用于检测应用是否拥有系统悬浮窗权限，以及在应用未拥有悬浮窗权限时跳转至系统页面请求该权限。<br><br>* 支持配置是否开启信息采集安全模式。更多信息请参见 [Step 5: 初始化 BDLive SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN#660b1619)。 |


<span id="abf86e2a"></span>
## 2024年4月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-04\-29 |1.32.0 |新增礼物奖励功能。 |
|2024\-04\-15 |1.31.1 |支持优化 SDK 包体积。更多信息请参见 [优化 SDK 包体积](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN#a90cb94f)。 |


<span id="098b07b9"></span>
## 2024年3月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-03\-28 |1.30.6 |修复了部分问题。 |
|2024\-03\-27 |1.30.5 |修复了部分问题。 |
|2024\-03\-11 |1.30.4 |修复了部分问题。 |


<span id="b3c8eedb"></span>
## 2024年2月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-02\-29 |1.30.3 |支持在竖屏模式下显示直播间描述。 |


<span id="cdd02e19"></span>
## 2024年1月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-01\-23 |1.30.0 |* 新增以下功能：<br><br>   * 自定义分享地址<br><br>   * 倒计时<br><br>   * 预约直播流<br><br>   * 场馆切换<br><br>   * 邀请海报<br><br>   * 系统通知<br><br>   * 欢迎语<br><br>   * 风险提示<br><br>   * 全屏水印<br><br>   * 问卷<br><br>   * 投票<br><br>   * 实时抽奖<br><br>      更多信息请参见 [SaaS 与 aPaaS 功能对比](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas)。<br><br>* 优化点赞功能：支持显示点赞数及自定义相关配置。<br><br>* 支持上报直播流质量数据。<br><br>* 新增混淆规则 `log.**{*;}`。更多信息请参见 [集成 Android 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android)。 |


<span id="2c6f1131"></span>
## 2023年11月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-11\-13 |1.10.9 |兼容 Android 14。 |


<span id="73379bac"></span>
## 2023年8月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-08\-04 |1.10.7 |修复了评论删除相关问题。 |


<span id="04d27ad2"></span>
## 2023年7月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-07\-20 |1.10.6 |* 图片库组件迁移至 Glide。更多信息请参见 [Glide 版本兼容性](https://docs.byteplus.com/en/byteplus-livesaas/docs/integrating-the-viewer-sdk-for-android#aca3bab7)。<br><br>* 修复了部分问题。 |
