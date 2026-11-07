---
title: "Viewer SDK for Android release notes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes"
---

The Viewer SDK for Android release notes provide a detailed log of all updates. This document tracks new features, improvements, compatibility changes, and issues fixed for each version, helping you stay informed on the latest developments and plan your upgrades.

<span id="411ec2d4"></span>
## April 2026


|Release Date |Version |Description |
|---|---|---|
|2026\-04\-28 |1.66.3 |**Issues fixed**<br><br>Fixed several known occasional crash issues. |


<span id="5b5274a3"></span>
## November 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-11\-12 |1.65.0 |**Improvements**<br><br>Supported more SDK language types:<br><br><br>* Tagalog<br><br>* Khmer<br><br>* Lao<br><br>* Burmese<br><br>* Malay<br><br>* Hindi<br><br>* French<br><br>* German<br><br>* Italian |


<span id="5d9e0fee"></span>
## October 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-10\-28 |1.64.1 |**Issues fixed**<br><br>Fixed some issues. |


<span id="8f3765ba"></span>
## September 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-09\-25 |1.64.0 |**Improvements**<br><br><br>* Adapted to the Android 16 KB feature.<br><br>* Supported log reporting for playback to enhance troubleshooting capabilities. |
|2025\-09\-09 |1.63.0 |**Issues fixed**<br><br>Fixed some issues. |


<span id="5537e8e4"></span>
## August 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-08\-12 |1.62.0 |Synchronized the version number of the Live Streaming SDK for Android. |


<span id="1496aac1"></span>
## July 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-07\-30 |1.61.4 |**Issues fixed**<br><br>Fixed some issues. |
|2025\-07\-28 |1.61.3 |* **Compatibility changes**<br><br>   In `CustomSettings`, deleted the following methods:<br><br>   * Deleted the `setCommentEditViewHintTextColor` method. Use [setPopupInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#5fc5536f) and [setInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#e349d9b3) instead.<br><br>   * Deleted the `setCommentEditViewTextColor` method. Use [setPopupInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#a128a852) and [setInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#bb581984) instead.<br><br>* **New features**<br><br>   * Added the [setTopCommentBackgroundWidthFitContent](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#115fbc19) method to set whether the width of the pinned comment background adjusts with the content width.<br><br>   * Added the [setTopCommentViewCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#8b6e0523) method to set the corner radius of the pinned comment's background.<br><br>   * Added the [setTopCommentNicknameColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#36d938dc) method to set the color of the pinned comment's nickname.<br><br>   * Added the [setTopCommentNicknameFontSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#e85f2897) method to set the font size of the pinned comment's nickname.<br><br>   * Added the [setTopCommentNicknameFontStyle](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#9891737b) method to set the font of the pinned comment's nickname.<br><br>   * Added the [setTopCommentContentLineSpacingExtra](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#826adc59) method to set the line spacing for the content of the pinned comment.<br><br>   * Added the [setTopCommentTagColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#452857ff) method to set the color of the vertical line to the left of the nickname in the pinned comment.<br><br>   * Added the [setTopCommentBackgroundColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#b5661b0f) method to set the background color of the pinned comment.<br><br>   * Added the [setCommentContentLineSpacingExtra](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#016961d8) method to set the line spacing for the comment content.<br><br>   * Added the [setCommentCellCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#992d58e3) method to set the corner radius of the comment cell.<br><br>   * Added the [setFunctionEntranceButtonCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#2a63cdb6) method to set the corner radius of the function buttons located in the lower\-right corner of the live room, such as the shopping cart and interaction tool buttons.<br><br>   * Added the [setPopupInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#5fc5536f) method to set the placeholder text color of the comment text box while editing (when the keyboard is displayed).<br><br>   * Added the [setPopupInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#a128a852) method to set the entered text color for the comment text box while editing (when the keyboard is displayed).<br><br>   * Added the [setInputBoxPromptTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#e349d9b3) method to set the placeholder text color of the comment text box when not editing (when the keyboard is hidden).<br><br>   * Added the [setInputBoxTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#bb581984) method to set the entered text color for the comment text box when not editing (when the keyboard is hidden).<br><br>   * Added the [setInputBoxCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#40f70e3f) method to set the corner radius of the comment text box when not editing (when the keyboard is hidden).<br><br>* **Issues fixed**<br><br>   Fixed some issues. |
|2025\-07\-15 |1.60.0 |**Improvements**<br><br>Optimized the UI style of the real\-time lucky draw feature in the viewer to enhance the user experience, including support for displaying prize images in the lucky draw dialog box. |
|2025\-07\-01 |1.59.0 |**Issues fixed**<br><br>Fixed some issues. |


<span id="f7d1c2fd"></span>
## June 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-06\-04 |1.58.0 |**New features**<br><br>Support for setting whether the PiP window pauses video playback when the screen is locked. For more information, see [setPauseOnLockScreenInMiniWindow](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#f8150cf4). |


<span id="0c667da8"></span>
## May 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-05\-20 |1.57.1 |**Improvements**<br><br>Improved SDK log reporting information to enhance troubleshooting capabilities. |


<span id="bd4b90e3"></span>
## April 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-04\-29 |1.56.0 |**Issues fixed**<br><br>Fixed some issues. |
|2025\-04\-15 |1.55.2 |* **Compatibility changes**<br><br>   Parameter changes<br><br>   The parameter `reason` in the following methods is changed to `info`:<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline) in `ITVULiveRoomServerListener`<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline-2) in `LiveRoomStatusListener`<br><br>   * [onUserForceOffline](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#onuserforceoffline-3) in `SinglePlayerListener`<br><br>* **New features**<br><br>   * In [BDLForceOfflineReason](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#7321845b), the following reasons for viewers being forcibly removed from the live room are added:<br><br>      * `BDLiveForceOfflineReasonIPBanned` (IP address banned)<br><br>      * `BDLiveForceOfflineReasonKickOut` (kicked out)<br><br>   * Support kicking viewers out of the live room and banning viewers' IP addresses.<br><br>* **Improvements**<br><br>   Optimized the UI style of the check\-in feature in the viewer to enhance user experience. |
|2025\-04\-07 |1.54.2 |**Issues fixed**<br><br>The Viewer SDK for Android versions 1.49.0 \- 1.54.1 have issues with log event reporting. To avoid affecting the troubleshooting of online issues, please upgrade these versions to 1.54.2. |
|2025\-04\-03 |1.54.1 |**Issues fixed**<br><br>Fixed some issues. |
|2025\-04\-01 |1.54.0 |* **Compatibility changes**<br><br>   Modified the SDK version suffix. For more information, see [Integrating the Viewer SDK for Android](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android).<br><br>   * When importing the Viewer SDK with all features, the SDK version suffix has changed from `pull-global:VersionNumber.external` to `pull:VersionNumber.globalFull`. For example, use `com.bytedance.bdlive:bdlive-pull-global:1.53.0.external` to import the Viewer SDK 1.53.0 with all features, and use `com.bytedance.bdlive:bdlive-pull:1.54.0.globalFull` to import the Viewer SDK 1.54.0 with all features.<br><br>   * When importing the Viewer SDK excluding the feature of ultra\-low latency live streaming, the SDK version suffix has changed from `pull-global-remove-rtc:VersionNumber.external` to `pull:VersionNumber.globalLite`. For example, use `com.bytedance.bdlive:bdlive-pull-global-remove-rtc:1.53.0.external` to import the Viewer SDK 1.53.0 excluding the feature of ultra\-low latency live streaming, and use `com.bytedance.bdlive:bdlive-pull:1.54.0.globalLite` to import the Viewer SDK 1.54.0 excluding the feature of ultra\-low latency live streaming.<br><br>* **New features**<br><br>   * Data reporting.<br><br>      Support for data reporting. For more information, see [setBdlExternalReportConfiguration](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#543e5973).<br><br>   * Customizing the comment text box<br><br>      Support for setting the maximum number of characters allowed in the comment text box. For more information, see [setCommentInputCountLimit](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#542ef80d). |


<span id="da2a39bb"></span>
## March 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-03\-18 |1.53.0 |* **Compatibility changes**<br><br>   * Deprecated some methods<br><br>      The method `setWelcomeMsgFontColor` for setting the text color of the welcome message in the live room is deprecated. Use [setSystemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor) instead.<br><br>   * Scope changes<br><br>      * [setHostCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentcolor) now only supports setting the text color of host's comments. To set the color of the host tag, use [setHostTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontcolor) instead.<br><br>      * [setCommentContentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentcontentfontstyle) now only supports setting the font of viewer comments. To set the font of host's comments, use [setHostCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontstyle) instead.<br><br>* **New features**<br><br>   * Customizing the comment text box<br><br>      * Support for setting whether to pop up the keyboard when viewers tap the comment text box. For more information, see [commentShouldInterceptEditing](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#6cc8bcc5).<br><br>      * Support for setting the event interception listener for the comment text box. For more information, see [setCommentEditingListener](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#71fed577).<br><br>      * Support for setting the following content of the comment text box in non\-editing status, namely when the keyboard is not popped up:<br><br>         * Placeholder text. For more information, see [setInputBoxPrompt](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#8682c301).<br><br>         * Placeholder text color. For more information, see [setInputBoxPromptColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#04aa818c).<br><br>         * Background color. For more information, see [setInputBoxBackgroundColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#4a693500).<br><br>         * Corner radius. For more information, see [setInputBoxCornerRadius](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#740ee52f).<br><br>         * Border width. For more information, see [setInputBoxBorderWidth](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#0e05259a).<br><br>         * Border color. For more information, see [setInputBoxBorderColor](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings#f81a58ab).<br><br>   * Customizing the style of the comment area<br><br>      * Support for setting the following content of the live room description in portrait mode and welcome message:<br><br>         * The font, font size, and color of the tag. For more information, see [setSystemCommentTagFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontstyle), [setSystemCommentTagFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontsize), and [setSystemCommentTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommenttagfontcolor).<br><br>         * The font, font size, and color of the body. For more information, see [setSystemCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentfontstyle), [setSystemCommentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentfontsize), and [setSystemCommentColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor).<br><br>      * Support for setting the spacing between adjacent comments. For more information, see [setCommentItemSpacing](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentitemspacing).<br><br>      * Support for setting the spacing between the bottom of the comment list and the top of the comment text box. For more information, see [setRoomCommentListViewBottomMargin](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setroomcommentlistviewbottommargin).<br><br>      * Support for setting the content color of the pull\-down refresh component, such as `↓ Pull to load more comments`. For more information, see [setCommentListPullToRefreshColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentlistpulltorefreshcolor).<br><br>      * Support for setting the font size of non\-hosts' nicknames and that of viewer comments. For more information, see [setCommentNicknameFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentnicknamefontsize) and [setCommentContentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setcommentcontentfontsize).<br><br>      * Support for setting the font size and color of the host tag. For more information, see [setHostTagFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontsize) and [setHostTagFontColor](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethosttagfontcolor).<br><br>      * Support for setting the font and font size of host's comments. For more information, see [setHostCommentFontStyle](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontstyle) and [setHostCommentFontSize](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#sethostcommentfontsize). |
|2025\-03\-04 |1.52.1 |* **Compatibility changes**<br><br>   * Logic update<br><br>      Updated the handling logic for stuttering during the live stream. When the parameter value of [setNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setneedautodemote) is `true`, added a check to determine whether to switch between the primary and backup streams directly based on the parameter value of [setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall).<br><br>   * The `setLanguageType` method for setting the required language type of some custom text is deprecated.<br><br>* **New features**<br><br>   * Added the callback triggered when the `TVULiveRoomServer` instance is successfully created. For more information, see [onRoomServerCreated](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#38dde242).<br><br>   * Added the [getDynamicSettings](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#2323d292) method. You can call this method either before or after viewers join the live room to customize the relevant settings of the live room.<br><br>   * Support for updating live room UI and interaction behaviors dynamically after viewers join the live room. For more information, see [Updating live room UI and interaction behaviors dynamically](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#7b1d80cb).<br><br>   * Host account<br><br>      * Support for following the host.<br><br>      * Added the callback class for the viewer follow event in custom authentication mode. For more information, see [BDLUserFollowListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#35d14b67).<br><br>      * Support for setting:<br><br>         * the text and background image of the button when the host is followed or not followed.<br><br>         * the listener for the event of a viewer following the host in custom authentication mode.<br><br>            For more information, see [DynamicCustomSettings](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings).<br><br>   * Multiple languages<br><br>      Support for the following languages:<br><br>      * Korean<br><br>      * Thai<br><br>      * Vietnamese<br><br>      * Arabic<br><br>      * Turkish<br><br>      * Spanish<br><br>      * Indonesian<br><br>      * Portuguese<br><br>      * Russian |


<span id="1cfaefb3"></span>
## February 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-02\-24 |1.51.1 |**Issues fixed**<br><br>Fixed some issues. |
|2025\-02\-18 |1.51.0 |* **Compatibility changes**<br><br>   * Deleted methods<br><br>      Due to changes in the UI style of the pinned comment, the following methods are deleted:<br><br>      * `setTopCommentTagFontStyle` for setting the font of the pinned tag.<br><br>      * `setTopCommentTagFontSize` for setting the font size of the pinned tag.<br><br>      * `setTopCommentTagFontColor` for setting the text color of the pinned tag.<br><br>   * Default value changes<br><br>      * The default value for the maximum number of lines displayed for the pinned comment is changed from `2` to `1`. For more information, see [setTopCommentRowCount](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#261f08a4).<br><br>      * The default value for the height of the comment area in the live room in portrait mode is changed from 1/3 of the screen height to 194 dp. For more information, see [setPortraitCommentAreaHeight](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#4338c1b2).<br><br>   * Scope changes<br><br>      The [setCommentItemBgColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#2b82be95) method now also applies to entrance messages.<br><br>* **New features**<br><br>   Menu for product cards<br><br>   Support for setting whether to display the strikethrough on the list price. For more information, see [setProductOriginalPriceShowStrikethrough](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#4a00b94d).<br><br>* **Improvements**<br><br>   Optimized the UI styles of product cards, the pinned comment, and entrance messages to enhance the user experience. |


<span id="21f31c7d"></span>
## January 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-01\-21 |1.50.0 |**New features**<br><br>Support for setting the font size and color of the popularity tag text. For more information, see [setPeopleCountFontSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#d55a37d1) and [setPeopleCountTextColor](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#08753ee9). |
|2025\-01\-08 |1.49.0 |* **New features**<br><br>   Added support for single\-point tracking in log queries to improve the ability to identify SDK issues.<br><br>* **Issues fixed**<br><br>   Fixed some issues. |


<span id="a40194d6"></span>
## December 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-12\-24 |1.48.0 |**Issues fixed**<br><br>Fixed some issues. |
|2024\-12\-10 |1.47.3 |* **Compatibility changes**<br><br>   Parameter change<br><br>   In the `addChildViewInLinearLayout` method, the parameter used to specify the display position of the custom floating view component in the live room is changed from `isLeftTop` to `location`.<br><br>* **New features**<br><br>   Support for displaying the custom floating view component in the upper\-right corner of the live room. |


<span id="73bc45d7"></span>
## November 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-11\-26 |1.47.2 |* **New features**<br><br>   Floating ad<br><br>   Support for setting whether the floating ad displays a white border and background.<br><br>* **Issues fixed**<br><br>   Fixed some issues. |
|2024\-11\-07 |1.46.3 |* **New features**<br><br>   Gradient overlay<br><br>   Support for setting whether to display a gradient overlay at the top of the live room in portrait mode. If your video background is white, displaying the gradient overlay can make the white text at the top of the live room more visible.<br><br>* **Issues fixed**<br><br>   Fixed some issues. |


<span id="0384dd75"></span>
## October 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-10\-31 |1.46.2 |* **Improvements**<br><br>   Compatible with Android 15.<br><br>* **Issues fixed**<br><br>   Fixed some issues. |
|2024\-10\-28 |1.46.1 |**Issues fixed**<br><br>Fixed some issues. |
|2024\-10\-24 |1.46.0 |**Issues fixed**<br><br>Fixed some issues |
|2024\-10\-15 |1.45.0 |* **Improvements**<br><br>   Improved the UI style of a live room in portrait mode.<br><br>* **Issues fixed**<br><br>   Fixed some issues. |


<span id="6ac25cae"></span>
## September 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-09\-12 |1.44.0 |Added the check\-in feature. |
|2024\-09\-04 |1.43.4 |Fixed some issues. |


<span id="9b00f991"></span>
## August 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-08\-28 |1.43.3 |Fixed some issues. |
|2024\-08\-22 |1.43.2 |Added the [setShowCloseButtonWhenClearingScreen](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setshowclosebuttonwhenclearingscreen) method to configure whether to display the button for closing the live room during screen clearing. |
|2024\-08\-20 |1.43.1 |Optimized the clickable areas of the shopping cart and gift icons at the bottom of the live room in portrait mode. |
|2024\-08\-15 |1.43.0 |* Support for displaying the shopping cart icon in landscape mode.<br><br>* The SDK has migrated from JCenter to Maven Central. |
|2024\-08\-06 |1.42.1 |Fixed some issues. |
|2024\-08\-01 |1.42.0 |Added the `setNeedAutoDemote` method for setting whether to support automatic downgrade or provide a prompt in case of network lag during the live stream. |


<span id="4c21b251"></span>
## July 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-07\-23 |1.41.0 |Optimized the logic for booking a live stream. |


<span id="38c9288e"></span>
## June 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-06\-27 |1.40.0 |* For method [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#joinLiveRoom), added the parameter `joinRoomConfig`, and deprecated parameters `activityId`, `token`, `roomAuthMode`, and `isPortrait`.<br><br>* For the `setPublicCommentNickName` method, the `nameRegisterListener` parameter was added.<br><br>* Added [JoinRoomConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#f39b2118), the configurations required to join the full\-featured live room.<br><br>* Added [JoinResultListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#610d4532), the callback class for the result of joining the full\-featured live room, which includes [onJoinSuccess](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#fc43f86c) for successful entry and [onJoinFailed](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#7ff8f393) for failed entry.<br><br>* Added `PublicNickNameRegisterListener`, the callback class for the result of nickname registration when the authentication mode of the live room is public, which includes `onRegisterSuccess` for successful nickname registration and `onRegisterFail` for failed registration.<br><br>* Optimized the UI style.<br><br>* Fixed some issues. |
|2024\-06\-18 |1.39.3 |* Added the `setCoverImageContainerVisibility` method in `TVUSinglePlayerView` to configure the visibility status of the container for the live room's cover image.<br><br>* Fixed some issues. |
|2024\-06\-12 |1.39.2 |Fixed some issues. |
|2024\-06\-11 |1.39.1 |* Added the [showFloatPermissionDialogInLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#98fe08db) method to display a permission request dialog box for the floating window in the full\-featured live room.<br><br>* Added [FloatUtil](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil), the utility class for the floating window in the live room, which includes the [checkPermission](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil#4b3dc68a) and [requestPermission](https://docs.byteplus.com/docs/byteplus-livesaas/floatutil#f53394dc) methods to check whether the app has the system's floating window permission and redirect the app to the system's page to request this permission when the app does not have the floating window permission.<br><br>* Support for configuring whether to enable the information collection safety mode. For more information, see [Step 5: Initialize the BDLive SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android#660b1619). |


<span id="abf86e2a"></span>
## April 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-04\-29 |1.32.0 |Added the gift rewards feature. |
|2024\-04\-15 |1.31.1 |Support for optimizing the SDK package size. For more information, see [Optimizing the SDK package size ](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android#a90cb94f). |


<span id="098b07b9"></span>
## March 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-03\-28 |1.30.6 |Fixed some issues. |
|2024\-03\-27 |1.30.5 |Fixed some issues. |
|2024\-03\-11 |1.30.4 |Fixed some issues. |


<span id="b3c8eedb"></span>
## February 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-02\-29 |1.30.3 |Support for displaying the live room description in portrait mode. |


<span id="cdd02e19"></span>
## January 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-01\-23 |1.30.0 |* Added the following features:<br><br>   * Customizing shared address<br><br>   * Countdown<br><br>   * Booking a live stream<br><br>   * Switching between different venues<br><br>   * Invitation poster<br><br>   * System notifications<br><br>   * Welcome message<br><br>   * Risk warning<br><br>   * Fullscreen watermark<br><br>   * Questionnaires<br><br>   * Voting<br><br>   * Real\-time lucky draws<br><br>      For more information, see [Feature comparison between SaaS and aPaaS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas).<br><br>* Optimized the likes feature: supports displaying the number of likes and customizing related configurations.<br><br>* Support for reporting live streaming quality data.<br><br>* Added the obfuscation rule `log.**{*;}`. For more information, see [Integrating the Viewer SDK for Android](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android). |


<span id="2c6f1131"></span>
## November 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-11\-13 |1.10.9 |Compatible with Android 14. |


<span id="73379bac"></span>
## August 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-08\-04 |1.10.7 |Fixed a bug related to comment deletion. |


<span id="04d27ad2"></span>
## July 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-07\-20 |1.10.6 |* Migrated the image library component to Glide. For more information, see [Glide version compatibility](https://docs.byteplus.com/en/byteplus-livesaas/docs/integrating-the-viewer-sdk-for-android#aca3bab7).<br><br>* Fixed some issues. |
