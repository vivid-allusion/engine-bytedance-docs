---
title: "mSettings"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings"
---

This topic describes various customization methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">SDK customization settings take precedence over custom configurations set in the BytePlus Live console or by calling server\-side OpenAPIs. For example, if you customize the live room's like icon using both the <code>setThumbIcon</code> method of the SDK and in the BytePlus Live console, the icon customized by the <code>setThumbIcon</code> method is displayed on the viewing page.</div>


* <div data-tips="true" data-tips-type="tip">All methods in this topic must be called before viewers join the live room.</div>



<span id="c84ea727"></span>
## Player

<span id="14c1fc92"></span>
### setPlayerLayoutMode

Sets the video scaling mode for a live room in landscape mode.

```java
public void setPlayerLayoutMode(int playerLayoutMode)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerLayoutMode |Integer |The video scaling mode for a live room in landscape mode. Default value: `0`.<br><br><br>* `0`: `ImageAspectFit`. Fill the player and keep the video's aspect ratio. The width or height of the video fills the width or height of the player. If the aspect ratio of the video is different from that of the player, the video is scaled to fit, with no content cropping.<br><br>* `1`: `ImageToFill`. Fill the player with the video. The aspect ratio of the video may be changed.<br><br>* `2`: `ImageAspectFill`. Fill the player and keep the video's aspect ratio. The width of the video fills the width of the player, and the height of the video fills the height of the player. If the aspect ratio of the video is different from that of the player, the video is cropped to fit. |


<span id="bcd1844b"></span>
### setPortraitPlayerLayoutMode

Sets the video scaling mode for a live room in portrait mode.

```java
public void setPortraitPlayerLayoutMode(int playerLayoutMode)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerLayoutMode |Integer |The video scaling mode for a live room in portrait mode. Default value: `2`.<br><br><br>* `0`: `ImageAspectFit`. Fill the player and keep the video's aspect ratio. The width or height of the video fills the width or height of the player. If the aspect ratio of the video is different from that of the player, the video is scaled to fit, with no content cropping.<br><br>* `1`: `ImageToFill`. Fill the player with the video. The aspect ratio of the video may be changed.<br><br>* `2`: `ImageAspectFill`. Fill the player and keep the video's aspect ratio. The width of the video fills the width of the player, and the height of the video fills the height of the player. If the aspect ratio of the video is different from that of the player, the video is cropped to fit. |


<span id="9b743f4d"></span>
### setPeopleCountFontStyle

Sets the font of the popularity tag text.

```java
public void setPeopleCountFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the popularity tag text. |


<span id="d55a37d1"></span>
### setPeopleCountFontSize

Sets the font size of the popularity tag text.

```Java
public void setPeopleCountFontSize(int peopleCountFontSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|peopleCountFontSiz |Integer |The font size of the popularity tag text. Unit: sp. |


<span id="08753ee9"></span>
### setPeopleCountTextColor

Sets the color of the popularity tag text.

```Java
public void setPeopleCountTextColor(int peopleCountTextColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|peopleCountTextColor |Integer |The color of the popularity tag text. |


<span id="351984cc"></span>
### setPeopleCountIconDrawable

Sets the popularity icon.

```java
public void setPeopleCountIconDrawable(Drawable drawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|drawable |Drawable |The popularity icon. |


<span id="3fecc7b5"></span>
### setPlayerThemeColor

Sets the theme color of the player, namely the color of the speed button, progress bar, and resolution button.

```java
public void setPlayerThemeColor(int playerThemeColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerThemeColor |Integer |The theme color of the player, namely the color of the speed button, progress bar, and resolution button. |


<span id="45fcf8aa"></span>
### setRoomStatusTextTipFontSize

Sets the font size of the live room status.

```java
public void setRoomStatusTextTipFontSize(int roomStatusTextTipFontSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|roomStatusTextTipFontSize |Integer |The font size of the live room status. Unit: sp. |


<span id="a38c2a91"></span>
### setRoomStatusTextTipCenterOffset

Sets the vertical offset of the live room status text relative to the center of the player.

```java
public void setRoomStatusTextTipCenterOffset(int roomStatusTextTipCenterOffset)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|roomStatusTextTipCenterOffset |Integer |The vertical offset of the live room status text relative to the center of the player. Unit: dp. |


<span id="0e07387a"></span>
### setRoomStatusTextTipRadius

Sets the rounded corner of the background of the live room status text.

```java
public void setRoomStatusTextTipRadius(int roomStatusTextTipRadius)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|roomStatusTextTipRadius |Integer |The rounded corner of the background of the live room status text. Unit: dp. |


<span id="3aaaec13"></span>
### setRoomStatusTextTipHorizontalPadding

Sets the horizontal padding of the live room status text.

```java
public void setRoomStatusTextTipHorizontalPadding(int roomStatusTextTipHorizontalPadding)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|roomStatusTextTipHorizontalPadding |Integer |The horizontal padding of the live room status text. This value cannot be negative. Unit: dp. |


<span id="eb9159a4"></span>
### setRoomStatusTextTipVerticalPadding

Sets the vertical padding of the live room status text.

```java
public void setRoomStatusTextTipVerticalPadding(int roomStatusTextTipVerticalPadding)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|roomStatusTextTipVerticalPadding |Integer |The vertical padding of the live room status text. This value cannot be negative. Unit: dp. |


<span id="3da839f7"></span>
### setPlayerTimeColor

Sets the time color of Video on Demand (VOD) videos.

```java
public void setPlayerTimeColor(int playerTimeColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerTimeColor |Integer |The time color of VOD videos. |


<span id="de7e091f"></span>
### setFullScreenIcon

Sets the full screen icon.

```java
public void setFullScreenIcon(Drawable fullScreenIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|fullScreenIcon |Drawable |The full screen icon. |


<span id="c53da99c"></span>
### setSmallScreenIcon

Sets the exit full screen icon.

```java
public void setSmallScreenIcon(Drawable smallScreenIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|smallScreenIcon |Drawable |The exit full screen icon. |


<span id="10d1e9a9"></span>
### setLiveRefreshIcon

Sets the refresh icon shown in the lower\-left corner of the player in **Live** status.

```java
public void setLiveRefreshIcon(Drawable liveRefreshIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|liveRefreshIcon |Drawable |The refresh icon shown in the lower\-left corner of the player in **Live** status. |


<span id="fea0b7ee"></span>
### setPlayerStartIcon

Sets the play icon shown in the lower\-left corner of the player.

```java
public void setPlayerStartIcon(Drawable playerStartIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerStartIcon |Drawable |The play icon shown in the lower\-left corner of the player. |


<span id="741fd598"></span>
### setPlayerPauseIcon

Sets the pause icon shown in the lower\-left corner of the player.

```java
public void setPlayerPauseIcon(Drawable playerPauseIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerPauseIcon |Drawable |The pause icon shown in the lower\-left corner of the player. |


<span id="b9f9855e"></span>
### setPlayerPausedCenterIcon

Sets the pause status icon shown in the center of the player.

```java
public void setPlayerPausedCenterIcon(Drawable playerPausedCenterIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerPausedCenterIcon |Drawable |The pause status icon shown in the center of the player. |


<span id="4c0db46f"></span>
### setCustomLiveName

Sets the live room name.

```java
public void setCustomLiveName(String customLiveName)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|customLiveName |String |The live room name. After setting, the passed name will take precedence. If an empty string is passed, the name will be hidden. |


<span id="f1b19520"></span>
### setSpeedSettingDialogAutoClose

Sets whether the speed selection dialog box automatically closes when the viewer selects a speed.

```java
public void setSpeedSettingDialogAutoClose(boolean speedSettingDialogAutoClose)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|speedSettingDialogAutoClose |Boolean |Whether the speed selection dialog box automatically closes when the viewer selects a speed. Default value: `false`.<br><br><br>* `true`: Automatically close.<br><br>* `false`: Do not automatically close. |


<span id="d34e9355"></span>
### setResolutionSettingDialogAutoClose

Sets whether the resolution selection dialog box automatically closes when the viewer selects a resolution.

```java
public void setResolutionSettingDialogAutoClose(boolean resolutionSettingDialogAutoClose)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolutionSettingDialogAutoClose |Boolean |Whether the resolution selection dialog box automatically closes when the viewer selects a resolution. Default value: `false`.<br><br><br>* `true`: Automatically close.<br><br>* `false`: Do not automatically close. |


<span id="1df9583d"></span>
### setSimpleControlBar

Sets whether to enable the simple control bar for the live room in landscape mode. The simple control bar does not have the speed and resolution selection buttons.

```java
public void setSimpleControlBar(boolean mSimpleControlBar)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mSimpleControlBar |Boolean |Whether to enable the simple control bar for the live room in landscape mode.<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |


<span id="958af3e1"></span>
### setReplayTipText

Sets the text of the replay button for playbacks.

```java
public void setReplayTipText(String mReplayTipText)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mReplayTipText |String |The text of the replay button for playbacks. |


<span id="f77abe2b"></span>
### setLiveAutoPlay

Sets whether to automatically play the live video.

```java
public void setLiveAutoPlay(boolean mLiveAutoPlay)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mLiveAutoPlay |Boolean |Whether to automatically play the live video.<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |


<span id="102e91a5"></span>
### setPlayBackAutoPlay

Sets whether to play the playback automatically when the live room is in landscape mode.

```java
public void setPlayBackAutoPlay(boolean mPlayBackAutoPlay)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPlayBackAutoPlay |Boolean |Whether to play the playback automatically when the live room is in landscape mode.<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |


<span id="a7710614"></span>
### setPortraitPlayBackAutoPlay

Sets whether to play the playback automatically when the live room is in portrait mode.

```java
public void setPortraitPlayBackAutoPlay(boolean mPortraitPlayBackAutoPlay)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPortraitPlayBackAutoPlay |Boolean |Whether to play the playback automatically when the live room is in portrait mode.<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |


<span id="f630c72c"></span>
### setForceShowAutoPlay

Sets whether to play the preview automatically when the live room is in landscape mode.

```java
public void setForceShowAutoPlay(boolean mForceShowAutoPlay)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mForceShowAutoPlay |Boolean |Whether to play the preview automatically when the live room is in landscape mode.<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |


<span id="28a79c72"></span>
### setPortraitForceShowAutoPlay

Sets whether to play the preview automatically when the live room is in portrait mode.

```java
public void setPortraitForceShowAutoPlay(boolean mPortraitForceShowAutoPlay)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPortraitForceShowAutoPlay |Boolean |Whether to play the preview automatically when the live room is in portrait mode.<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |


<span id="c0b34f9b"></span>
### setPlayBackLoop

Sets whether to loop the playback automatically when the live room is in landscape mode.

```java
public void setPlayBackLoop(boolean mIsPlayBackLoop)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mIsPlayBackLoop |Boolean |Whether to loop the playback automatically when the live room is in landscape mode.<br><br><br>* `true`: Loop automatically.<br><br>* `false`: Do not loop automatically. |


<span id="311325a4"></span>
### setPortraitPlayBackLoop

Sets whether to loop the playback automatically when the live room is in portrait mode.

```java
public void setPortraitPlayBackLoop(boolean mIsPortraitPlayBackLoop)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mIsPortraitPlayBackLoop |Boolean |Whether to loop the playback automatically when the live room is in portrait mode.<br><br><br>* `true`: Loop automatically.<br><br>* `false`: Do not loop automatically. |


<span id="2a2cd31c"></span>
### setForceShowLoop

Sets whether to loop the preview automatically when the live room is in landscape mode.

```java
public void setForceShowLoop(boolean mIsForceShowLoop)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mIsForceShowLoop |Boolean |Whether to loop the preview automatically when the live room is in landscape mode.<br><br><br>* `true`: Loop automatically.<br><br>* `false`: Do not loop automatically. |


<span id="f32e4191"></span>
### setPortraitForceShowLoop

Sets whether to loop the preview automatically when the live room is in portrait mode.

```java
public void setPortraitForceShowLoop(boolean mIsPortraitForceShowLoop)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mIsPortraitForceShowLoop |Boolean |Whether to loop the preview automatically when the live room is in portrait mode.<br><br><br>* `true`: Loop automatically.<br><br>* `false`: Do not loop automatically. |


<span id="937879b8"></span>
### setVodAutoContinuePlayback

Sets whether to enable automatic breakpoint resumption for VOD videos.

```java
public void setVodAutoContinuePlayback(boolean isVodAutoContinuePlayback)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isVodAutoContinuePlayback |Boolean |Whether to enable automatic breakpoint resumption for VOD videos. Default value: `true`.<br><br><br>* `true`: Enable automatic breakpoint resumption. VOD videos automatically resume from the breakpoint when viewers exit and then rejoin the live room.<br><br>* `false`: Disable automatic breakpoint resumption. |


<span id="3884d8f7"></span>
### setVodAutoSeekTipTextVisible

Sets whether to display a prompt upon automatic breakpoint resumption for VOD videos.

```java
public void setVodAutoSeekTipTextVisible(boolean mVodAutoSeekTipTextVisible)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mVodAutoSeekTipTextVisible |Boolean |Whether to display a prompt upon automatic breakpoint resumption for VOD videos. Default value: `true`.<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="355c7e9b"></span>
### setVodAutoSeekTipTextSize

Sets the font size of the automatic breakpoint resumption prompt for VOD videos.

```java
public void setVodAutoSeekTipTextSize(float mVodAutoSeekTipTextSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mVodAutoSeekTipTextSize |float |The font size of the automatic breakpoint resumption prompt for VOD videos. Default value: `11`. Unit: sp. |


<span id="05c5b49f"></span>
### setEnterFullScreenEnable

Sets whether viewers can enter full screen mode.

```Java
public void setEnterFullScreenEnable(boolean enterFullScreenEnable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|enterFullScreenEnable |Boolean |Whether viewers can enter full screen mode. Default value: `true`.<br><br><br>* `true`: Viewers can enter full screen mode. The full screen button is displayed in the player. The full screen button is displayed in a live room in portrait mode when the width of the source video stream is greater than its height for live videos or VOD videos, and in a live room in landscape mode.<br><br>* `false`: Viewers cannot enter full screen mode. The full screen button is not displayed in the player. |


<span id="1909af7e"></span>
### setNeedAutoDemote

Sets whether to support automatic downgrade or provide a prompt in case of network lag during the live stream.

```Java
public void setNeedAutoDemote(boolean needAutoDemote)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|needAutoDemote |Boolean |Whether to support automatic downgrade or provide a prompt in case of network lag during the live stream. Default value: `true`.<br><br><br>* `true`:<br><br>   * If the parameter value of [setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall) is `true`, directly switch between the primary and backup streams.<br><br>   * If the parameter value of [setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall) is `false`, in smart mode, automatically downgrade to a lower resolution. If stuttering still occurs at the lowest resolution, switch between the primary and backup streams. In non\-smart mode, provide a prompt to viewers asking whether to switch to a lower resolution, allowing them to choose as needed. If stuttering still occurs after viewers switch to the lowest resolution, switch between the primary and backup streams.<br><br>* `false`: In smart mode, do not automatically downgrade. In non\-smart mode, do not notify viewers to switch to a lower resolution. |


<span id="8c5dc53a"></span>
### setBackupDowngradeWhenStall

Sets whether to switch between the primary and backup streams directly in case of stuttering during the live stream.

```Java
public void setBackupDowngradeWhenStall(boolean backupDowngradeWhenStall)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|backupDowngradeWhenStall |boolean |Whether to switch between the primary and backup streams directly in case of stuttering during the live stream. Default value: `false`. This method takes effect only when the parameter value of [setNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setneedautodemote) is `true`.<br><br><br>* `true`: Directly switch between the primary and backup streams.<br><br>* `false`: In smart mode, automatically downgrade to a lower resolution. If stuttering still occurs at the lowest resolution, switch between the primary and backup streams. In non\-smart mode, provide a prompt to viewers asking whether to switch to a lower resolution, allowing them to choose as needed. If stuttering still occurs after viewers switch to the lowest resolution, switch between the primary and backup streams. |


<span id="2d369486"></span>
## Menus

<span id="d0e012ac"></span>
### setMenuTabBackgroundDrawable

Sets the background of the menu bar for the live room in landscape mode.

```java
public void setMenuTabBackgroundDrawable(Drawable drawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|drawable |Drawable |The background of the menu bar for the live room in landscape mode. |


<span id="53ea42b5"></span>
### setMenuFontColor

Sets the text color of menu items in the menu bar when selected or unselected.

```java
public void setMenuFontColor(new Pair<>(unSelectedColor,selectedColor))
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|unSelectedColor |Integer |The text color of menu items in the menu bar when unselected for the live room in landscape mode. |
|selectedColor |Integer |The text color of menu items in the menu bar when selected for the live room in landscape mode. |


<span id="b7289d01"></span>
### setMenuFontStyle

Sets the font of the menu bar.

```java
public void setMenuFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the menu bar. |


<span id="04b74c84"></span>
### setLandMenuFlowingTagColor

Sets the indicator color for selected menu items in the menu bar of the live room in landscape mode.

```java
public void setLandMenuFlowingTagColor(int landMenuFlowingTagColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|landMenuFlowingTagColor |Integer |The indicator color for selected menu items in the menu bar of the live room in landscape mode. Default value: `0xFF3370FF`. |


<span id="15c8126e"></span>
### setMenuDialogFlowingTagColor

Sets the indicator color for selected embedded link and graphics menu items in the menu bar of the live room in portrait mode.

```Java
public void  setMenuDialogFlowingTagColor(int menuDialogFlowingTagColor) 
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|menuDialogFlowingTagColor |Integer |The indicator color for selected embedded link and graphics menu items in the menu bar of the live room in portrait mode. Default value: `0xFF161823`. |


<span id="34aaada2"></span>
### setImageEmbeddedWebUrlsIcon

Sets the icon for the embedded link menu of the live room in portrait mode.

```Java
public void setImageEmbeddedWebUrlsIcon(Drawable imageEmbeddedWebUrlsIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|imageEmbeddedWebUrlsIcon |Drawable |The icon for the embedded link menu of the live room in portrait mode. |


<span id="ea75f056"></span>
### setMenuDialogTabFontSize

Sets the font size for the titles of the embedded link and graphics menus.

```Java
public void setMenuDialogTabFontSize(int menuDialogTabFontSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|menuDialogTabFontSize |Integer |The font size for the titles of the embedded link and graphics menus. Unit: sp. |


<span id="26a3e658"></span>
### setMenuDialogTabSelectedFontColor

Sets the title text color of the embedded link and graphics menus when selected.

```java
public void setMenuDialogTabSelectedFontColor(int menuDialogTabSelectedFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|menuDialogTabSelectedFontColor |Integer |The title text color of the embedded link and graphics menus when selected. Default value: `0xFF161823`. |


<span id="6c07f026"></span>
### setMenuDialogTabUnSelectedFontColor

Sets the title text color of the embedded link and graphics menus when unselected.

```java
public void setMenuDialogTabUnSelectedFontColor(int menuDialogTabUnSelectedFontColor) 
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|menuDialogTabUnSelectedFontColor |Integer |The title text color of the embedded link and graphics menus when unselected. Default value: `0xFF161823`. |


<span id="6bc0db40"></span>
## Comments

<span id="fe61f617"></span>
### setNoCommentIconDrawable

Sets the placeholder icon shown in the comment area when it has no comments.

```java
public void setNoCommentIconDrawable(Drawable drawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|drawable |Drawable |The placeholder icon shown in the comment area when it has no comments. |


<span id="7a4995ea"></span>
### setCommentNicknameFontStyle

Sets the font of non\-hosts' nicknames.

```java
public void setCommentNicknameFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of non\-hosts' nicknames. |


<span id="44c1830f"></span>
### setCommentNicknameFontColor

Sets the color of non\-hosts' nicknames.

```java
public void setCommentNicknameFontColor(int commentNicknameFontColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentNicknameFontColor |Integer |The color of non\-hosts' nicknames. |


<span id="2885642f"></span>
### setCommentNicknameFontSize

Sets the font size of non\-hosts' nicknames.

```Java
public void setCommentNicknameFontSize(int commentNicknameFontSize)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentNicknameFontSize |Integer |The font size of non\-hosts' nicknames. Unit: sp. |


<span id="910f28cf"></span>
### setCommentContentFontColor

Sets the text color of non\-hosts' comments.

```java
public void setCommentContentFontColor(int commentContentFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentContentFontColor |Integer |The text color of non\-hosts' comments. |


<span id="d73603d2"></span>
### setCommentLinkColor

Sets the color of comment links.

```java
public void setCommentLinkColor(int mCommentLinkColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mCommentLinkColor |Integer |The color of comment links. |


<span id="4d6e871a"></span>
### setAudienceCommentLinkClickable

Sets whether links in non\-hosts' comments are clickable.

```java
public void setAudienceCommentLinkClickable(boolean mAudienceCommentLinkClickable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mAudienceCommentLinkClickable |Boolean |Whether links in non\-hosts' comments are clickable. For custom actions taken when viewers click links in comments, see [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#be1306ce).<br><br><br>* `true`: Clickable.<br><br>* `false`: Not clickable. |


<span id="7975da1e"></span>
### setCommentContentFontStyle

Sets the font of non\-hosts' comments.

```java
public void setCommentContentFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of non\-hosts' comments. |


<span id="a6dabe5a"></span>
### setCommentContentFontSize

Sets the font size of non\-hosts' comments.

```Kotlin
public void setCommentContentFontSize(int commentContentFontSize)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentContentFontSize |Integer |The font size of non\-hosts' comments. Unit: sp. |


<span id="032f1ab3"></span>
### setHostTagFontStyle

Sets the font of the host tag.

```java
public void setHostTagFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the host tag. |


<span id="3e4dfbf9"></span>
### setHostTagFontSize

Sets the font size of the host tag.

```Java
public void setHostTagFontSize(int hostTagFontSize)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|hostTagFontSize |Integer |The font size of the host tag. Unit: sp. |


<span id="158d5023"></span>
### setTopCommentTagFontStyle

Sets the font of the pinned tag.

```java
public void setTopCommentTagFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the pinned tag. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This method is no longer supported starting from version 1.51.0.</div>


<span id="52954629"></span>
### setTopCommentFontStyle

Sets the font of pinned content.

```java
public void setTopCommentFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of pinned content. |


<span id="262969ee"></span>
### setTopCommentFontColor

Sets the text color of pinned content.

```java
public void setTopCommentFontColor(int topCommentFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|topCommentFontColor |Integer |The text color of pinned content. |


<span id="261f08a4"></span>
### setTopCommentRowCount

Sets the maximum number of lines displayed for the pinned comment.

```java
public void setTopCommentRowCount(int count)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|count |Integer |The maximum number of lines displayed for the pinned comment. Default value: `1`. |


<span id="70a0fcb1"></span>
### setTopCommentDialogTitleAtStart

Sets whether the title of the pinned content details dialog box is displayed on the far left side.

```java
public void setTopCommentDialogTitleAtStart(boolean mTopCommentDialogAtStart)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mTopCommentDialogAtStart |Boolean |Whether the title of the pinned content details dialog box is displayed on the far left side.<br><br><br>* `true`: On the far left side.<br><br>* `false`: Not on the far left side. |


<span id="4338c1b2"></span>
### setPortraitCommentAreaHeight

Sets the height of the comment area in the live room in portrait mode.

```java
public void setPortraitCommentAreaHeight(int mPortraitCommentAreaHeight)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPortraitCommentAreaHeight |Integer |The height of the comment area in the live room in portrait mode. This value cannot be negative. Default value: `194`. Unit: dp. |


<span id="748d2665"></span>
### setPortraitCommentLineCount

Sets the maximum number of lines displayed per comment in the live room in portrait mode.

```java
public void setPortraitCommentLineCount(int mPortraitCommentLineCount)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPortraitCommentLineCount |Integer |The maximum number of lines displayed per comment in the live room in portrait mode. |


<span id="a2aac31c"></span>
### setCommentEditViewHintTextColor

Sets the color of the placeholder text in the comment text box.

```java
public void setCommentEditViewHintTextColor(int color)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|color |Integer |The color of the placeholder text in the comment text box. Default value: `0xB3FFFFFF` |


<span id="bab9d110"></span>
### setCommentEditViewTextColor

Sets the color of the text entered in the comment text box.

```java
public void setCommentEditViewTextColor(int mCommentEditViewTextColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mCommentEditViewTextColor |Integer |The color of the text entered in the comment text box. Default value: `0xFF000000`. |


<span id="425e8f28"></span>
### setCommentIntervalTip

Sets the content of the comment interval prompt.

```java
public void setCommentIntervalTip(String tip)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|tip |String |The content of the comment interval prompt. |


<span id="175601a7"></span>
### setCommentIntervalFontStyle

Sets the font of the comment interval prompt content.

```java
public void setCommentIntervalFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the comment interval prompt content. |


<span id="2b82be95"></span>
### setCommentItemBgColor

Sets the background color of the welcome message, entrance messages, and non\-hosts' comments.

```java
public void setCommentItemBgColor(int commentItemBgColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentItemBgColor |Integer |The background color of the welcome message, entrance message, and non\-hosts' comments. Default value: `#33000000`. |


<span id="ff6e1afe"></span>
### setPullCommentCount

Sets the number of comments pulled each time.

```java
public void setPullCommentCount(int count)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|count |Integer |The number of comments pulled each time. |


<span id="ad021546"></span>
### setPullHistoryCommentTotalCount

Sets the total number of previous comments that can be pulled.

```java
public void setPullHistoryCommentTotalCount(int count)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|count |Integer |The total number of previous comments that can be pulled. |


<span id="075b7249"></span>
### setThumbIcon

Sets the icon for liking the live room.

```java
public void setThumbIcon(Drawable drawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|drawable |Drawable |The icon for liking the live room. |


<span id="40624408"></span>
### setJoinRoomMsgNicknameColor

Sets the text color of the nickname in the live room entry message.

```java
public void setJoinRoomMsgNicknameColor(int mJoinRoomMsgNicknameColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mJoinRoomMsgNicknameColor |Integer |The text color of the nickname in the live room entry message. |


<span id="5488ff75"></span>
### setJoinRoomMsgContentColor

Sets the text color of the content of the live room entry message.

```java
public void setJoinRoomMsgContentColor(int mJoinRoomMsgContentColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mJoinRoomMsgContentColor |Integer |The text color of the content of the live room entry message. |


<span id="b006f58b"></span>
### setWelcomeMsgFontColor

Sets the text color of the welcome message in the live room.

```java
public void setWelcomeMsgFontColor(int mWelcomeMsgFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mWelcomeMsgFontColor |Integer |The text color of the welcome message in the live room |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This method is no longer supported starting from version 1.53.0. Use the <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor">setSystemCommentColor</a> method instead.</div>


<span id="c5541059"></span>
### setLandscapeCommentShouldShowAvatar

Sets whether user avatars are displayed in the comment area of the live room in landscape mode.

Call [setHostDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#3dc09158) to set the default avatar of the host and call [setCommentDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#a8949de3) to set the default avatar of non\-hosts. In custom mode (when `roomAuthMode` is `CUSTOM`), you can call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) to pass the avatar URLs of specified users.

```java
public void setLandscapeCommentShouldShowAvatar(boolean landscapeCommentShouldShowAvatar)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|landscapeCommentShouldShowAvatar |Boolean |Whether user avatars are displayed in the comment area of the live room in landscape mode. Default value: `true`.<br><br><br>* `true`: Displayed.<br><br>* `false`: Not displayed. |


<span id="f68ed0e2"></span>
### setPortraitCommentShouldShowAvatar

Sets whether user avatars are displayed in the comment area of the live room in portrait mode.

Call [setHostDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#3dc09158) to set the default avatar of the host and call [setCommentDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#a8949de3) to set the default avatar of non\-host. In custom mode (when `roomAuthMode` is `CUSTOM`), you can call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) to pass the avatar URLs of specified users.

```java
public void setPortraitCommentShouldShowAvatar(boolean portraitCommentShouldShowAvatar)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|portraitCommentShouldShowAvatar |Boolean |Whether user avatars are displayed in the comment area of the live room in portrait mode. Default value: `false`.<br><br><br>* `true`: Displayed.<br><br>* `false`: Not displayed. |


<span id="3dc09158"></span>
### setHostDefaultAvatar

Sets the default avatar of the host in the comment area.

```java
public void setHostDefaultAvatar(Drawable hostDefaultAvatar)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|hostDefaultAvatar |Drawable |The default avatar of the host in the comment area. |


<span id="a8949de3"></span>
### setCommentDefaultAvatar

Sets the default avatar of non\-hosts in the comment area. Once set, this avatar will be displayed in front of every non\-host's comment.

```java
public void setCommentDefaultAvatar(Drawable commentDefaultAvatar)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentDefaultAvatar |Drawable |The default avatar of non\-hosts in the comment area. |


<span id="3c5e004d"></span>
### setThumbFloatingDrawableListener

Sets the listener for the floating animated icons displayed after viewers like a live room. For callback information, see [ITVUMultipleDrawableListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#7929f65e).

```java
public void setThumbFloatingDrawableListener(ITVUMultipleDrawableListener listener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |ITVUMultipleDrawableListener |The listener for the floating animated icons displayed after viewers like a live room. |


<span id="3822d4b1"></span>
### setHostCommentColor

Sets the text color of host's comments.

```Java
public void setHostCommentColor(int hostCommentColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|hostCommentColor |Integer |The text color of host's comments. |


<span id="ac731a87"></span>
### setHostCommentBackgroundColor

Sets the background color of host's comments.

```Java
public void setHostCommentBackgroundColor(int hostCommentBackgroundColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|hostCommentBackgroundColor |Integer |The background color of host's comments. |


<span id="9169ea51"></span>
### setHostTagFontColor

Sets the color of the host tag.

```Java
public void setHostTagFontColor(int hostTagFontColor) 
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|hostTagFontColor |Integer |The color of the host tag. |


<span id="f7ccfd88"></span>
### setHostCommentFontSize

Sets the font size of host's comments.

```Java
public void setHostCommentFontSize(int mHostCommentFontSize)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|mHostCommentFontSize |Integer |The font size of host's comments. Unit: sp. |


<span id="68c26a6c"></span>
### setHostCommentFontStyle

Sets the font of host's comments.

```Java
public void setHostCommentFontStyle(Typeface hostCommentFontStyle)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|hostCommentFontStyle |Typeface |The font of host's comments. |


<span id="c30d44f3"></span>
### setSystemCommentTagFontStyle

Sets the font of the tag for the live room description in portrait mode and welcome message.

```Java
public void setSystemCommentTagFontStyle(Typeface systemCommentTagFontStyle)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|systemCommentTagFontStyle |Typeface |The font of the tag for the live room description in portrait mode and welcome message. |


<span id="1de92ebe"></span>
### setSystemCommentTagFontSize

Sets the font size of the tag for the live room description in portrait mode and welcome message.

```Java
public void setSystemCommentTagFontSize(int systemCommentTagFontSize
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|systemCommentTagFontSize |Integer |The font size of the tag for the live room description in portrait mode and welcome message. Unit: sp. |


<span id="d5b319a2"></span>
### setSystemCommentTagFontColor

Sets the tag color for the live room description in portrait mode and welcome message.

```Java
public void setSystemCommentTagFontColor(int systemCommentTagFontColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|systemCommentTagFontColor |Integer |The tag color for the live room description in portrait mode and welcome message. |


<span id="06ae9e64"></span>
### setSystemCommentFontStyle

Sets the font of the body for the live room description in portrait mode and welcome message.

```Java
public void setSystemCommentFontStyle(Typeface systemCommentFontStyle)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|systemCommentFontStyle |Typeface |The font of the body for the live room description in portrait mode and welcome message. |


<span id="599c655a"></span>
### setSystemCommentFontSize

Sets the font size of the body for the live room description in portrait mode and welcome message.

```Java
public void setSystemCommentFontSize(int systemCommentFontSize)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|systemCommentFontSize |Integer |The font size of the body for the live room description in portrait mode and welcome message. Unit: sp. |


<span id="c7606a4c"></span>
### setSystemCommentColor

Sets the body text color for the live room description in portrait mode and welcome message.

```Java
public void setSystemCommentColor(int systemCommentColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|systemCommentColor |Integer |The body text color for the live room description in portrait mode and welcome message. |


<span id="931a0bba"></span>
### setCommentItemSpacing

Sets the spacing between adjacent comments.

```Java
public void setCommentItemSpacing(int mDistanceBetweenCommentItem
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|mDistanceBetweenCommentItem |Integer |The spacing between adjacent comments. Default value: `6`. Unit: dp. |


<span id="5f9f91d5"></span>
### setRoomCommentListViewBottomMargin

Sets the spacing between the bottom of the comment list and the top of the comment text box.

```Java
public void setRoomCommentListViewBottomMargin(int roomCommentListViewBottomMargin)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|roomCommentListViewBottomMargin |Integer |The spacing between the bottom of the comment list and the top of the comment text box. Default value: `0`. Unit: dp. |


<span id="08f729f4"></span>
### setCommentListPullToRefreshColor

Sets the content color of the pull\-down refresh component, such as `↓ Pull to load more comments`.

```Java
public void setCommentListPullToRefreshColor(int mCommentListPullToRefreshColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|mCommentListPullToRefreshColor |Integer |The content color of the pull\-down refresh component, such as `↓ Pull to load more comments`. |


<span id="a60099d7"></span>
### setCommentLikedIcon

Sets the Like icon when a comment has already been liked.

```Java
public void setCommentLikedIcon(BDThemeIconModel commentLikedIcon) {
    mCommentLikedIcon = commentLikedIcon;
}
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentLikedIcon |BDThemeIconModel |The button information. For more information, see [BDThemeIconModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#56a27a1b). |


<span id="166c853b"></span>
### setCommentLikeIcon

Sets the Like icon when a comment has not yet been liked.

```Java
public void setCommentLikeIcon(BDThemeIconModel commentLikeIcon) {
    mCommentLikeIcon = commentLikeIcon;
}
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentLikeIcon |BDThemeIconModel |The button information. For more information, see [BDThemeIconModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#56a27a1b). |


<span id="542ef80d"></span>
### setCommentInputCountLimit

Sets the maximum number of characters allowed in the comment text box.

```Java
public void setCommentInputCountLimit(int commentInputCountLimit)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentInputCountLimit |Integer |The maximum number of characters allowed in the comment text box. Default value: `200`. |


<span id="ea9bfd75"></span>
### setCommentCustomListener

Sets the custom listener for live room comments.

```Java
public void setCommentCustomizeListener(CommentCustomizeListener commentCustomizeListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentCustomizeListener |CommentCustomizeListener |The custom listener for live room comments. For more information, see [CommentCustomizeListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#2c977992). |


**Sample code**

The following sample code changes the color of `123` in a text comment to yellow and replaces the smiley face emoji with another image.

```Java
settings.setCommentCustomizeListener((commentModel, commentConfigModel, uiConfigModel, languageManager, spannableStringBuilder, textView) -> {
    boolean presenter = commentModel.isPresenter(); // Judge whether the comment is sent by the host.
    boolean lightTheme = uiConfigModel.isLightTheme(); // Judge whether the theme is not dark mode.
    LanguageManager.LANGUAGE currentLanguage = languageManager.getCurrentLanguage();// Get the language currently selected in the live room.
    
    String s = spannableStringBuilder.toString();
    
    // Change the color of "123" in the text comment to yellow.
    if (s.contains("123")) {
        spannableStringBuilder.setSpan(new ForegroundColorSpan(Color.YELLOW),
                s.indexOf("123"), s.indexOf("123") + 3, Spannable.SPAN_INCLUSIVE_EXCLUSIVE);
    }
    
    // Replace the smile emoji with another image.
    if (s.contains("[Smile]")) {
        spannableStringBuilder.setSpan(new GlideImageSpan(textView, "https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/055f8e4f26c04fd39aa3a3935a43866e~tplv-goo7wpa0wc-image.image"),
                s.indexOf("[Smile]"), s.indexOf("[Smile]") + "[Smile]".length(), Spannable.SPAN_INCLUSIVE_EXCLUSIVE);
    }
    // Reset the textView to apply the changes.
    textView.setText(spannableStringBuilder);
});
```


<span id="8b6e0523"></span>
### setTopCommentViewCornerRadius

Sets the corner radius of the pinned comment‘s background.

```Java
public void setTopCommentViewCornerRadius(int topCommentViewCornerRadius)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentViewCornerRadius |int |The corner radius of the pinned comment‘s background. Default value: `8`. Unit: dp. |


<span id="115fbc19"></span>
### setTopCommentBackgroundWidthFitContent

Sets whether the width of the pinned comment background adjusts with the content width.

```Java
public void setTopCommentBackgroundWidthFitContent(boolean topCommentBackgroundWidthFitContent)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentBackgroundWidthFitContent |boolean |Whether the width of the pinned comment background adjusts with the content width. Default value: `false`. Valid values:<br><br><br>* `true`: The width of the pinned comment background adjusts with the content width.<br><br>* `false`: The width of the pinned comment background is fixed. |


<span id="36d938dc"></span>
### setTopCommentNicknameColor

Sets the color of the pinned comment's nickname.

```Java
public void setTopCommentNicknameColor(int topCommentNicknameColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentNicknameColor |int |The color of the pinned comment's nickname. |


<span id="e85f2897"></span>
### setTopCommentNicknameFontSize

Sets the font size of the pinned comment's nickname.

```Java
public void setTopCommentNicknameFontSize(int topCommentNicknameFontSize)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentNicknameFontSize |int |The font size of the pinned comment's nickname. Unit: sp. |


<span id="9891737b"></span>
### setTopCommentNicknameFontStyle

Sets the font of the pinned comment's nickname.

```Java
public void setTopCommentNicknameFontStyle(Typeface topCommentNicknameFontStyle)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentNicknameFontStyle |Typeface |The font of the pinned comment's nickname. |


<span id="826adc59"></span>
### setTopCommentContentLineSpacingExtra

Sets the line spacing for the content of the pinned comment.

```Java
public void setTopCommentContentLineSpacingExtra(int topCommentContentLineSpacingExtra)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentContentLineSpacingExtra |int |Line spacing for the content of the pinned comment. Unit: dp. |


<span id="452857ff"></span>
### setTopCommentTagColor

Sets the color of the vertical line to the left of the nickname in the pinned comment.

```Java
public void setTopCommentTagColor(int topCommentTagColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentTagColor |int |The color of the vertical line to the left of the nickname in the pinned comment. |


<span id="b5661b0f"></span>
### setTopCommentBackgroundColor

Sets the background color of the pinned comment.

```Java
public void setTopCommentBackgroundColor(int topCommentBackgroundColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|topCommentBackgroundColor |int |The background color of the pinned comment. |


<span id="5fc5536f"></span>
### setPopupInputBoxPromptTextColor

Sets the placeholder text color of the comment text box in editing status, namely when the keyboard is popped up.

```Java
public void setPopupInputBoxPromptTextColor(int popupInputBoxPromptTextColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|popupInputBoxPromptTextColor |int |The placeholder text color of the comment text box in editing status, namely when the keyboard is popped up. |


<span id="a128a852"></span>
### setPopupInputBoxTextColor

Sets the entered text color for the comment text box in editing status, namely when the keyboard is popped up.

```Java
public void setPopupInputBoxTextColor(int popupInputBoxTextColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|popupInputBoxTextColor |int |The entered text color for the comment text box in editing status, namely when the keyboard is popped up. |


<span id="e349d9b3"></span>
### setInputBoxPromptTextColor

Sets the placeholder text color of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxPromptTextColor(int inputBoxPromptTextColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxPromptTextColor |int |The placeholder text color of the comment text box in non\-editing status, namely when the keyboard is not popped up. |


<span id="bb581984"></span>
### setInputBoxTextColor

Sets the entered text color for the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxTextColor(int inputBoxTextColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxTextColor |int |The entered text color for the comment text box in non\-editing status, namely when the keyboard is not popped up. |


<span id="40f70e3f"></span>
### setInputBoxCornerRadius

Sets the corner radius of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxCornerRadius(int inputBoxCornerRadius)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxCornerRadius |int |The corner radius of the comment text box in non\-editing status, namely when the keyboard is not popped up. Default value: `19`. Unit: dp. |


<span id="992d58e3"></span>
### setCommentCellCornerRadius

Sets the corner radius of the comment cell.

```Java
public void setCommentCellCornerRadius(int commentCellCornerRadius)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentCellCornerRadius |int |The corner radius of the comment cell. Default value: `12`. Unit: dp. |


<span id="016961d8"></span>
### setCommentContentLineSpacingExtra

Sets the line spacing for the comment content.

```Java
public void setCommentContentLineSpacingExtra(int commentContentLineSpacingExtra)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentContentLineSpacingExtra |int |Line spacing for the comment content. Unit: dp. |


<span id="2a63cdb6"></span>
### setFunctionEntranceButtonCornerRadius

Sets the corner radius of the functional entry buttons located in the lower\-right corner of the live room, such as the shopping cart and interaction tool buttons.

```Java
public void setFunctionEntranceButtonCornerRadius(int functionEntranceButtonCornerRadius)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|functionEntranceButtonCornerRadius |int |The corner radius of the functional entry buttons located in the lower\-right corner of the live room, such as the shopping cart and interaction tool buttons. Default value: `18`. Unit: dp. |


<span id="a75bf5dd"></span>
## Registration dialog box

<span id="de14983a"></span>
### setNicknameDialogHeadFontStyle

Sets the font of the title.

```java
public void setNicknameDialogHeadFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the title. |


<span id="8dee7093"></span>
### setNicknameDialogEditTextFontStyle

Sets the font of the text in the text box.

```java
public void setNicknameDialogEditTextFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the text in the text box. |


<span id="31291001"></span>
### setNicknameDialogHintText

Sets the placeholder in the text box.

```java
public void setNicknameDialogHintText(String tip)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|tip |String |The placeholder in the text box. |


<span id="902a970a"></span>
### setNicknameDialogButtonColor

Sets the background color of the confirm button.

```java
public void setNicknameDialogButtonColor(int color)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|color |Integer |The background color of the confirm button. |


<span id="719a810a"></span>
### setNicknameDialogButtonTextFontStyle

Sets the font of the confirm button.

```java
public void setNicknameDialogButtonTextFontStyle(Typeface typeface)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|typeface |Typeface |The font of the confirm button. |


<span id="f2244eec"></span>
### setNicknameDialogCloseButtonIconDrawable

Sets the close icon.

```java
public void setNicknameDialogCloseButtonIconDrawable(Drawable drawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|drawable |Drawable |The close icon. |


<span id="83ccfbdf"></span>
## Graphics

<span id="7aea6698"></span>
### setRichTextPadding

Sets the top, bottom, left, and right margins of the graphics area.

```java
public void setRichTextPadding(int padding)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|padding |Integer |The top, bottom, left, and right margins of the graphics area. This value cannot be negative. Unit: dp. |


<span id="bfdcd525"></span>
### setImageTextContentColor

Sets the text color of the graphics content.

```java
public void setImageTextContentColor(int mImageTextContentColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mImageTextContentColor |Integer |The text color of the graphics content.<br><br>If the value is `0` or empty, the text color returned by the server is used. |


<span id="5bf1f53a"></span>
## Ads

<span id="f6305e09"></span>
### setPageCenterAdRatio

Sets the aspect ratio of in\-page ads.

```java
public void setPageCenterAdRatio(float pageCenterAdRatio)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|pageCenterAdRatio |float |The aspect ratio of in\-page ads. |


<span id="50a8bd40"></span>
### setCenterAdStrokeColor

Sets the border color of in\-page ads.

```java
public void setCenterAdStrokeColor(int centerAdStrokeColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|centerAdStrokeColor |Integer |The border color of in\-page ads. |


<span id="1be75c00"></span>
### setCenterAdRadius

Sets the rounded corner of in\-page ads.

```java
public void setCenterAdRadius(int centerAdRadius)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|centerAdRadius |Integer |The rounded corner of in\-page ads. |


<span id="314388e8"></span>
### setCenterAdRotationInterval

Sets the carousel speed of in\-page ads.

```java
public void setCenterAdRotationInterval(int centerAdRotationInterval)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|centerAdRotationInterval |Integer |The carousel speed of in\-page ads, specifically how often the carousel slides to the right. Unit: ms. |


<span id="1448f45f"></span>
### setFloatAdLayoutParams

Sets the default position of the floating ad.

```Java
public void setFloatAdLayoutParams(SimpleLayoutParams floatAdLayoutParams)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatAdLayoutParams |SimpleLayoutParams |The default position of the floating ad. For configuration details, see [SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e4a2c940). |


<span id="039e38e4"></span>
### setFloatAdSize

Sets the size of the floating ad.

```Java
public void setFloatAdSize(CustomSize floatAdSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatAdSize |CustomSize |The size of the floating ad. For configuration details, see [CustomSize](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#38b050a5). |


<span id="a252408c"></span>
### setFloatAdMovable

Sets whether to allow viewers to drag the floating ad.

```Java
public void setFloatAdMovable(boolean FloatAdMovable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|FloatAdMovable |Boolean |Whether to allow viewers to drag the floating ad. Default value: `false`. Valid values:<br><br><br>* `true`: Allow.<br><br>* `false`: Do not allow. |


<span id="845b7139"></span>
### setFloatAdShowBounds

Sets whether the floating ad displays the white border and background.

```Java
public void setFloatAdShowBounds(boolean floatAdShowBounds)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatAdShowBounds |Boolean |Whether the floating ad displays the white border and background. Default value: `true`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="de9bce95"></span>
### **setShowPageHeaderImage**

Sets whether to display the header image.

```Java
  public void setShowPageHeaderImage(boolean show)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|show |Boolean |Whether to display the header image. Default value: `true`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="c2532e01"></span>
### **setShowPageCenterAd**

Sets whether to display in\-page ads.

```Java
  public void setShowPageCenterAd(boolean show)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|show |Boolean |Whether to display in\-page ads. Default value: `true`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="3a79a1ea"></span>
## Player network status changes

<span id="83c1947d"></span>
### setShowNonWiFiToast

Sets whether to show a prompt for using mobile data.

```java
public void setShowNonWiFiToast(boolean mShowNonWiFiToast)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mShowNonWiFiToast |Boolean |Whether to show a prompt for using mobile data. Default value: `true`. Valid values:<br><br><br>* `true`: Show.<br><br>* `false`: Do not show. |


<span id="6a5da8bd"></span>
### setLandNonWifiToastCount

Sets the number of times the prompt text for using mobile data appears in the live room in landscape mode.

```java
public void setLandNonWifiToastCount(int mNonWifiToastCount)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNonWifiToastCount |Integer |The number of times the prompt text for using mobile data appears in the live room in landscape mode. Default value: `1`.<br><br><br>* `-1`: Show the prompt each time.<br><br>* `0`: Do not show the prompt.<br><br>* `≥ 1`: Show the prompt 1 or more times. |


<span id="fe25a490"></span>
### setRetryBtnBackgroundColor

Sets the background color of the **Retry** button in the live room in landscape mode.

```java
public void setRetryBtnBackgroundColor(int btnBackGround)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|btnBackGround |Integer |The background color of the **Retry** button in the live room in landscape mode. |


<span id="80e7d2c4"></span>
### setPorRetryBtnBackgroundColor

Sets the background color of the **Retry** button in the live room in portrait mode.

```java
public void setPorRetryBtnBackgroundColor(int btnBackGround)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|btnBackGround |Integer |The background color of the **Retry** button in the live room in portrait mode. |


<span id="61f1657e"></span>
### setLandscapeRetryBtnCornerRadius

Sets the rounded corner of the **Retry** button in the live room in landscape mode.

```java
public void setLandscapeRetryBtnCornerRadius(float btnCorner)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|btnCorner |Float |The rounded corner of the **Retry** button in the live room in landscape mode. |


<span id="031c6eb4"></span>
### setPortraitRetryBtnCornerRadius

Sets the rounded corner of the **Retry** button in the live room in portrait mode.

```java
public void setPortraitRetryBtnCornerRadius(float btnCorner)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|btnCorner |Float |The rounded corner of the **Retry** button in the live room in portrait mode. |


<span id="e1e44fa2"></span>
### setNetErrorBtn

Sets the button text of the network error prompt.

```java
public void setNetErrorBtn(String mNetErrorBut)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNetErrorBut |String |The button text of the network error prompt. |


<span id="0e34b2ee"></span>
### setNonWIFIBtn

Sets the button text for non\-WiFi status.

```java
public void setNonWIFIBtn(String mNonWIFIBut)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNonWIFIBut |String |The button text for non\-WiFi status. |


<span id="4161f237"></span>
### setNetErrorText

Sets the text of the network error prompt.

```java
public void setNetErrorText(String mNetErrorText)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNetErrorText |String |The text of the network error prompt. |


<span id="bdd6dcee"></span>
### setNonWIFIText

Sets the prompt text for non\-WiFi status.

```java
public void setNonWIFIText(String mNonWIFIText)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNonWIFIText |String |The prompt text for non\-WiFi status. |


<span id="9dc535c9"></span>
### setNetWorkChangeTextColor

Sets the color of the prompt text for using mobile data.

```java
public void setNetWorkChangeTextColor(int mNetWorkChangeTextColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNetWorkChangeTextColor |Integer |The color of the prompt text for using mobile data. The default color is white. |


<span id="f1bb9981"></span>
### setLoadingDrawable

Sets the loading icon for the live room in landscape mode.

```java
public void setLoadingDrawable(Drawable mLoadingDrawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mLoadingDrawable |Drawable |The loading icon for the live room in landscape mode. |


<span id="c55cac87"></span>
### setPorLoadingDrawable

Sets the loading icon for the live room in portrait mode.

```java
public void setPorLoadingDrawable(Drawable mLoadingDrawable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mLoadingDrawable |Drawable |The loading icon for the live room in portrait mode. |


<span id="14848730"></span>
### setLoadingDrawableSize

Sets the size of the loading icon for the live room in landscape mode.

```java
public void setLoadingDrawableSize(int size)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|size |Integer |The size of the loading icon for the live room in landscape mode. |


<span id="e0017ed2"></span>
### setPorLoadingDrawableSize

Sets the size of the loading icon for the live room in portrait mode.

```java
public void setPorLoadingDrawableSize(int size)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|size |Integer |The size of the loading icon for the live room in portrait mode. |


<span id="dfb9b61c"></span>
## Host accounts

<span id="b7619504"></span>
### setAccountImageSize

Sets the avatar size of the host account.

```java
public void setAccountImageSize(int mAccountImageSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mAccountImageSize |Integer |The avatar size of the host account. |


<span id="fb45e202"></span>
### setAccountViewColor

Sets the background color of the host account.

```java
public void setAccountViewColor(int mAccountViewColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mAccountViewColor |Integer |The background color of the host account. |


<span id="f44e96b4"></span>
### setAccountFontSize

Sets the font size of the host account.

```java
public void setAccountFontSize(int mAccountFontSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mAccountFontSize |Integer |The font size of the host account. Unit: sp. |


<span id="59f6d2ac"></span>
### setAccountFontColor

Sets the text color of the host account.

```java
public void setAccountFontColor(int accountFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|accountFontColor |Integer |The text color of the host account.。 |


<span id="d5a89797"></span>
## Floating window

The floating window is the picture\-in\-picture (PiP) window.

<span id="17b259a9"></span>
### setOpenLiveFloatWindow

Sets whether to enable the floating window for the live stream, namely whether to support displaying the live video in PiP mode.

```java
public void setOpenLiveFloatWindow(boolean mOpenFloatWindow)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mOpenFloatWindow |Boolean |Whether to enable the floating window for the live stream. Default value: `true`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |


<span id="afd1a6ca"></span>
### setOpenVodFloatWindow

Sets whether to enable the floating window for the VOD video, namely whether to support displaying the preview or playback in PiP mode.

```java
public void setOpenVodFloatWindow(boolean mOpenFloatWindow)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mOpenFloatWindow |Boolean |Whether to enable the floating window for the VOD video. Default value: `true`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |


<span id="ef659165"></span>
### setFloatWindowBorderWidth

Sets the border width of the floating window.

```java
public void setFloatWindowBorderWidth(int mFloatWindowBorderWidth)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatWindowBorderWidth |Integer |The border width of the floating window. This value cannot be negative. Unit: dp. |


<span id="1aef7bd9"></span>
### setFloatWindowBorderColor

Sets the border color of the floating window.

```java
public void setFloatWindowBorderColor(int mFloatWindowBorderColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatWindowBorderColor |Integer |The border color of the floating window. |


<span id="1ef9f97b"></span>
### setFloatWindowExitBtn

Sets the close icon of the floating window.

```java
public void setFloatWindowExitBtn(Drawable mFloatWindowExitBtn)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatWindowExitBtn |Drawable |The close icon of the floating window. |


<span id="9a3a861e"></span>
### setFloatWindowCorner

Sets the rounded corner of the floating window.

```java
public void setFloatWindowCorner(float mFloatWindowCorner)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatWindowCorner |Float |The rounded corner of the floating window. |


<span id="644b100e"></span>
### setFloatViewActionListener

Sets the tap event listener for the floating window or its close icon. After the setting, the SDK notifies the `FloatViewActionListener` of the tap event when viewers tap the floating window or its close icon, but does not execute the default tap behavior. For callback information, see [FloatViewActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#379862a5).

```java
public void setFloatViewActionListener(FloatViewActionListener floatViewActionListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatViewActionListener |FloatViewActionListener |The tap event listener for the floating window or its close icon. |


<span id="f8150cf4"></span>
### setPauseOnLockScreenInMiniWindow

Sets whether the PiP window pauses playing the video when the screen is locked.

```Java
public void setPauseOnLockScreenInMiniWindow(boolean pauseOnLockScreenInMiniWindow)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|pauseOnLockScreenInMiniWindow |boolean |Whether the PiP window pauses playing the video when the screen is locked. The default value is `false`. Valid values:<br><br><br>* `true`: Pause playing the video.<br><br>* `false`: Continue playing the video. |


<span id="dab5088d"></span>
## Multi\-languages

<span id="e3daaa52"></span>
### setLanguageType

Sets the required language type. All languages (Simplified Chinese, Traditional Chinese, English, and Japanese) are supported by default. This only applies to the following custom text. To set the language of the viewing page, call the [setPreferLanguage](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#0fee5955) method.


* Comment interval reminder text

* Replay button text

* Prompt text for using mobile data in the live room

* Button text for network disconnection

* Prompt text for network disconnection


```java
public void setLanguageType(LanguageManager.LANGUAGE[] mLanguageType)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mLanguageType |LanguageManager.LANGUAGE[] |The required language type. |


To implement multi\-language custom texts in the live room, you need to first pass an array of the required language types, and then separate the custom texts by the array index order using "|". The following sample code customizes the text of the replay button.

```java
LanguageManager.LANGUAGE[] mLanguageType = {LanguageManager.LANGUAGE.ZH_HANS, LanguageManager.LANGUAGE.EN
        , LanguageManager.LANGUAGE.JA, LanguageManager.LANGUAGE.ZH_HANT};
        
settings.setLanguageType(mLanguageType);

settings.setReplayTipText("重新观看|Watch again|もう一度見る|重新觀看");
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This method is no longer supported starting from version 1.52.1.</div>


<span id="9b8a2dce"></span>
### setMultiLanguageIcon

Sets the icon for switching languages.

```java
public void setMultiLanguageIcon(Drawable mMultiLanguageIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mMultiLanguageIcon |Drawable |The icon for switching languages. |


<span id="f7139b44"></span>
### setLanguageListener

Sets the listener for switching languages. For callback information, see [LanguageListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#76956141).

```java
public void setLanguageListener(LanguageListener mLanguageListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mLanguageListener |LanguageListener |The listener for switching languages. |


<span id="0fee5955"></span>
### setPreferLanguage

Sets the preferred language of the viewing page.

```java
public void setPreferLanguage(LanguageManager.LANGUAGE mPreferLanguage)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPreferLanguage |LanguageManager.LANGUAGE |The preferred language of the viewing page.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only for languages enabled on the BytePlus Live console.</div><br> |


<span id="c37c04d4"></span>
## Product cards

<span id="b4177ecc"></span>
### setShowGoodsCount

Sets whether to display the total number of product cards.

```java
public void setShowGoodsCount(boolean mShowGoodsCount)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mShowGoodsCount |Boolean |Whether to display the total number of product cards. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="f13496d0"></span>
### setShoppingCardIcon

Sets the shopping cart icon displayed in the live room.

```java
public void setShoppingCardIcon(Drawable shoppingCardIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardIcon |Drawable |The shopping cart icon displayed in the live room. |


<span id="65eb7338"></span>
### setShopCardItemImageCorner

Sets the rounded corner of the product card item's background.

```java
public void setShopCardItemImageCorner(int mShopCardItemImageCorner)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mShopCardItemImageCorner |Integer |The rounded corner of the product card item's background. |


<span id="8a715680"></span>
### setShoppingCardDialogHeight

Sets the height of the product card dialog box.

```java
public void setShoppingCardDialogHeight(int shoppingCardDialogHeight)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardDialogHeight |Integer |The height of the product card dialog box. This value cannot be negative. By default, the height is 0.73 times the screen height. Unit: dp. |


<span id="d2c8b7e7"></span>
### setShoppingCardDialogBackgroundColor

Sets the background color of the product card dialog box.

```java
public void setShoppingCardDialogBackgroundColor(int shoppingCardDialogBackgroundColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardDialogBackgroundColor |Integer |The background color of the product card dialog box. |


<span id="4112416e"></span>
### setShoppingCardTabFontStyle

Sets the font of the product card menu bar.

```java
public void setShoppingCardTabFontStyle(Typeface shoppingCardTabFontStyle)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardTabFontStyle |Typeface |The font of the product card menu bar. |


<span id="6c2bb529"></span>
### setShoppingCardTitleFontStyle

Sets the font of the product name.

```java
public void setShoppingCardTitleFontStyle(Typeface shoppingCardTitleFontStyle)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardTitleFontStyle |Typeface |The font of the product name. |


<span id="ee5486a7"></span>
### setShoppingCardTitleFontSize

Sets the font size of the product name.

```java
public void setShoppingCardTitleFontSize(int shoppingCardTitleFontSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardTitleFontSize |Integer |The font size of the product name. Unit: sp. |


<span id="44b490a3"></span>
### setShoppingCardTitleFontColor

Sets the color of the product name.

```java
public void setShoppingCardTitleFontColor(int shoppingCardTitleFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardTitleFontColor |Integer |The color of the product name. |


<span id="9f848956"></span>
### setShoppingCardHighLightFontStyle

Sets the font of the retail price.

```java
public void setShoppingCardHighLightFontStyle(Typeface shoppingCardHighLightFontStyle)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardHighLightFontStyle |Typeface |The font of the retail price. |


<span id="ab1031d9"></span>
### setShoppingCardHighLightFontSize

Sets the font size of the retail price.

```java
public void setShoppingCardHighLightFontSize(int shoppingCardHighLightFontSize)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardHighLightFontSize |Integer |The font size of the retail price. Unit: sp. |


<span id="18b68aa4"></span>
### setShoppingCardHighLightFontColor

Sets the color of the retail price.

```java
public void setShoppingCardHighLightFontColor(int shoppingCardHighLightFontColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardHighLightFontColor |Integer |The color of the retail price. |


<span id="4a00b94d"></span>
### setProductOriginalPriceShowStrikethrough

Sets whether to display the strikethrough on the list price.

```Java
public void setProductOriginalPriceShowStrikethrough(boolean productOriginalPriceShowStrikethrough)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|productOriginalPriceShowStrikethrough |Boolean |Whether to display the strikethrough on the list price. Default value: `false`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="78f83141"></span>
### setShoppingCardBackgroundColor

Sets the background color of the product card.

```java
public void setShoppingCardBackgroundColor(int shoppingCardBackgroundColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shoppingCardBackgroundColor |Integer |The background color of the product card. |


<span id="e7f49df1"></span>
### setEnableDirectUrl

Sets whether to enable the direct URL of products.

```java
public void setEnableDirectUrl(boolean mEnableDirectUrl) {
    this.mEnableDirectUrl = mEnableDirectUrl;
}
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mEnableDirectUrl |Boolean |Whether to enable the direct URL of products. Valid values:<br><br><br>* `true`: If the direct URL is configured on the BytePlus Live console, the direct URL is used first.<br><br>* `false`: The product URL is used. |


<span id="c962222d"></span>
## Floating product card

The floating product card is a product card displayed in the form of a floating icon.

<span id="b6d0c80f"></span>
### setFloatingShoppingCardBuyBtn

Sets the button of the floating product card.

```java
public void setFloatingShoppingCardBuyBtn(Drawable floatingShoppingCardBuyBtn)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatingShoppingCardBuyBtn |Drawable |The button of the floating product card. |


<span id="191d8368"></span>
### setFloatingShopCardBtnText

Sets the button text of the floating product card.

```typescript
public void setFloatingShopCardBtnText(String mFloatingShopCardBtnText)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatingShopCardBtnText |String |The button text of the floating product card. By default, the retail price of the product configured on the BytePlus Live console is used. Once set, the parameter value is used. |


<span id="9f41e9e3"></span>
### setFloatingShoppingCardLayoutParams

Sets the default position of the floating product card.

```Java
public void setFloatingShoppingCardLayoutParams(SimpleLayoutParams floatingShoppingCardLayoutParams)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatingShoppingCardLayoutParams |SimpleLayoutParams |The default position of the floating product card. For configuration details, see [SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e4a2c940). |


<span id="f9c4dc83"></span>
### setFloatShoppingCardMovable

Sets whether to allow viewers to drag the floating product card.

```Java
public void setFloatShoppingCardMovable(boolean FloatShoppingCardMovable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|FloatShoppingCardMovable |Boolean |Whether to allow viewers to drag the floating product card. Default value: `false`. Valid values:<br><br><br>* `true`: Allow.<br><br>* `false`: Do not allow. |


<span id="3c19c5d6"></span>
### setFloatShopCardCorner

Sets the outer rounded corner of the floating product card.

```java
public void setFloatShopCardCorner(int mFloatShopCardCorner)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatShopCardCorner |Integer |The outer rounded corner of the floating product card. The inner image's rounded corner automatically adapts to the outer rounded corner. |


<span id="fe186922"></span>
## URL redirection in the live room


* By default, the SDK redirects viewers to the WebView or external browser after they tap the product card under the menu, floating product card, avatar or name of the host account, header ad, in\-page ad, floating ad, or comment URL. To implement custom redirection, you can call [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#be1306ce) to listen to tap events and then implement the custom redirection based on detected tap events.

* The SDK does not have default redirection behavior if viewers who log in to the live room in custom mode tap the user nickname in the comment area. You must call [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#be1306ce) to listen to tap events and then implement the custom redirection based on detected tap events.


<span id="be1306ce"></span>
### setRedirectPageListener

Sets the tap event listener for links in the live room. Once set, the SDK triggers the corresponding tap events when viewers tap the above\-mentioned links. You need to implement custom redirection based on the tap events.

```java
public void setRedirectPageListener(RedirectPageListener mRedirectPageListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mRedirectPageListener |[RedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#f163f66b) |The tap event listener for links in the live room. |


**Sample code**

```Java
CustomSettings.Holder.mSettings.setRedirectPageListener(new RedirectPageListener() {
    /**
     *
     *
     * @param liveActivity The Activity of the live room.
     * @param redirectInfo The information required for redirection.
     * @return Whether to intercept the SDK's default redirection behavior. true: Intercept. The SDK no longer executes the default redirection behavior. false: Do not intercept. The SDK continues to execute the default redirection behavior.
     */
    @Override
    public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo) {
        // Check the entry of tap events based on the entrance field.
        String entrance = redirectInfo.getEntrance();
        switch (redirectInfo.getContentType()){
            case RedirectInfo.CONTENT_TYPE_URL:
                // Get the urlRedirectInfo field when the content type is URL.
                UrlRedirectInfo urlRedirectInfo = redirectInfo.getUrlRedirectInfo();
                
                if (entrance.equals(Entrance.FLOATING_ADVERTISEMENT.value)){
                    // To only intercept the default redirection behavior of the floating ad, return true when the entrance is floating ad and return false in all other cases. 
                    
                    // Display the SDK's internal WebViewDialog. You can also use a custom Dialog.
                    new CommonWebViewDialog(liveActivity,urlRedirectInfo.getUrl(),
                            R.style.TvuLiveBottomDialog).show();
                    return true;
                }
            case RedirectInfo.CONTENT_TYPE_COMMENT:
                // Get the commentModel field when the content type is comment.
                SingleCommentModel commentModel = redirectInfo.getCommentModel();
                // Implement the custom redirection after getting the commentModel field.    
                return true;
        }
        
        return false;
    }
});
```


<span id="4cd11aeb"></span>
## Live room status

<span id="8d1bd70f"></span>
### setLiveRoomStatusListener

Sets the listener for live room status. For callback information, see [LiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#1c2e9aff).

```java
public void setLiveRoomStatusListener(LiveRoomStatusListener mLiveRoomStatusListener)
```



|**Name** |**Type** |**Description** |
|---|---|---|
|mLiveRoomStatusListener |LiveRoomStatusListener |The listener for live room status. |


<span id="59235a7d"></span>
### setLiveRoomActionListener

Sets the exit event listener for the full\-featured live room. Once set, the SDK notifies the `LiveRoomActionListener` of the tap event when viewers tap the exit button or the physical back button to exit the full\-featured live room, without executing the default tap behavior. For callback information, see [LiveRoomActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#1d31736d).

```java
public void setLiveRoomActionListener(LiveRoomActionListener liveRoomActionListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|liveRoomActionListener |LiveRoomActionListener |The exit event listener for the full\-featured live room. |


<span id="6ae57c28"></span>
## Lucky draws

<span id="329545cb"></span>
### setFloatAwardListener

Sets the listener for the lucky draw icon. For callback information, see [FloatingAwardView.Listener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#f36aa242).

```java
public void setFloatAwardListener(FloatingAwardView.Listener mFloatAwardListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mFloatAwardListener |FloatingAwardView.Listener |The listener for the lucky draw icon. |


<span id="b0aec866"></span>
### setNeedFillAwardInfo

Sets whether viewers need to update their personal information after winning a prize.

```java
public void setNeedFillAwardInfo(boolean mNeedFillAwardInfo)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNeedFillAwardInfo |Boolean |Whether viewers need to update their personal information after winning a prize. Default value: `true`. Valid values:<br><br><br>* `true`: Viewers need to update their personal information.<br><br>* `false`: Viewers do not need to update their personal information. |


<span id="a247b2a2"></span>
## Interaction tools

<span id="d680233d"></span>
### setFloatInteractToolLayoutParams

Sets the default position for the complete set of interaction tool icons. The complete set of interaction tool icons includes all the interaction tool icons displayed on the viewing page.

```Java
public void setFloatInteractToolLayoutParams(SimpleLayoutParams floatInteractToolLayoutParams)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|floatInteractToolLayoutParams |SimpleLayoutParams |The default position for the complete set of interaction tool icons. For configuration details, see [SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e4a2c940). |


<span id="3d641a87"></span>
### setFloatInteractToolMovable

Sets whether to allow viewers to drag the complete set of interaction tool icons. The complete set of interaction tool icons includes all the interaction tool icons displayed on the viewing page.

```Java
public void setFloatInteractToolMovable(boolean FloatInteractToolMovable)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|FloatInteractToolMovable |Boolean |Whether to allow viewers to drag the complete set of interaction tool icons. Default value: `true`. Valid values:<br><br><br>* `true`: Allow.<br><br>* `false`: Do not allow. |


<span id="d49d3e3f"></span>
### setVotePeopleCountVisible

Sets whether to display the number of viewers who participate in the votes.

```Java
public void setVotePeopleCountVisible(boolean visible)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|visible |Boolean |Whether to display the number of viewers who participate in the votes. Default value: `true`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="dcf1c092"></span>
## Other

<span id="360e675a"></span>
### setPortraitExitIconPosition

Sets the position of the exit icon in the live room in portrait mode.

```java
public void setPortraitExitIconPosition(boolean mPortraitExitIconPosition)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPortraitExitIconPosition |Boolean |The position of the exit icon in the live room in portrait mode.<br><br><br>* `true`: On the right side of the live room.<br><br>* `false`: On the left side of the live room. |


<span id="6c8a8268"></span>
### setLandScapeExitIconPosition

Sets the position of the exit icon in the live room in landscape mode.

```java
public void setLandScapeExitIconPosition(boolean mLandScapeExitIconPosition)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mLandScapeExitIconPosition |Boolean |The position of the exit icon in the live room in landscape mode.<br><br><br>* `true`: On the right side of the live room.<br><br>* `false`: On the left side of the live room. |


<span id="313cdccf"></span>
### setCommentLinkToWebView

Sets whether the content is displayed on the current live room page after viewers tap the link.

```java
public void setCommentLinkToWebView(boolean mCommentLinkToWebView)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mCommentLinkToWebView |Boolean |Whether the content is displayed on the current live room page after viewers tap the link. Valid values:<br><br><br>* `true`: Displayed on the current live room page.<br><br>* `false`: Displayed on the new page. |


<span id="7ba2e7be"></span>
### setExitRoomIcon

Sets the icon to exit the live room.

```java
public void setExitRoomIcon(Drawable exitRoomIcon)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|exitRoomIcon |Drawable |The icon to exit the live room. |


<span id="6f30af5f"></span>
### setPageBackGroundColor

Sets the background color of the live room.

```java
public void setPageBackGroundColor(int mPageBackGroundColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mPageBackGroundColor |Integer |The background color of the live room. |


<span id="9565823b"></span>
### setTransitionPage

Sets the loading page for the live room in portrait mode. We recommend that you use an image with a black background.

```java
public void setTransitionPage(Drawable transitionPage)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|transitionPage |Drawable |The loading page for the live room in portrait mode. |


<span id="ad65c19c"></span>
### setCustomLoginListener

Sets the listener for logging in to your own account system when the authentication mode is public. For callback information, see [CustomLoginListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#75007939).

```java
public void setCustomLoginListener(CustomLoginListener mCustomLoginListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mCustomLoginListener |CustomLoginListener |The listener for logging in to your own account system when the authentication mode is public. |


<span id="4bec9c3c"></span>
### setBookSuccessText

Sets the prompt text for successful live stream booking.

```java
public void setBookSuccessText(String bookSuccessText)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|bookSuccessText |String |The prompt text for successful live stream booking. |


<span id="70e35b57"></span>
### setBookFailText

Sets the prompt text for failed live stream booking.

```java
public void setBookFailText(String bookFailText)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|bookFailText |String |The prompt text for failed live stream booking. |


<span id="af612d85"></span>
### setActivityBottomNavBarColor

Sets the background color of the system bottom navigation bar when it is displayed in the live room.

```Java
public void setActivityBottomNavBarColor(int activityBottomNavBarColor)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityBottomNavBarColor |Integer |The background color of the system bottom navigation bar when it is displayed in the live room. The default color is pure black (`#000000`). |


<span id="7b592acf"></span>
### setShareListener

Sets the listener for tapping the share icon in the full\-featured live room. Once set, the SDK notifies the `ShareListener` of the tap event when viewers tap the share icon in the full\-featured live room, without executing the default tap behavior. For callback information, see [ShareListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#2a6e0df9).

```Java
public void setShareListener(ShareListener shareListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|shareListener |[ShareListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#2a6e0df9) |The listener for tapping the share icon in the full\-featured live room. |


<span id="278b0202"></span>
### setPortraitRoomClearScreenEnable

Sets whether to enable the clear screen feature for the live room in portrait mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The clear screen feature is only supported in live rooms in portrait mode.</div>


```Java
public void setPortraitRoomClearScreenEnable(boolean portraitRoomClearScreenEnable)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|portraitRoomClearScreenEnable |Boolean |Whether to enable the clear screen feature for the live room in portrait mode. Default value: `true`. Valid values:<br><br><br>* `true`: Enable. Viewers can clear the screen by swiping right or tapping the more icon (...) \> **Clear**.<br><br>* `false`: Disable. |


<span id="28b8fb22"></span>
### setShowCloseButtonWhenClearingScreen

Sets whether to display the icon for closing the live room during screen clearing.

```Java
public void setShowCloseButtonWhenClearingScreen(boolean showCloseButtonWhenClearingScreen)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|showCloseButtonWhenClearingScreen |Boolean |Whether to display the icon for closing the live room during screen clearing. Default value: `false`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="ba44eae4"></span>
### setShowRetryPageWhenJoinRoomFail

Sets whether to display a retry page when the initialization of the full\-feature live room page fails.

```Java
public void setShowRetryPageWhenJoinRoomFail(boolean showRetryPageWhenJoinRoomFail)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|showRetryPageWhenJoinRoomFail |Boolean |Whether to display a retry page when the initialization of the full\-feature live room page fails. Default value: `true`. Valid values:<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |


<span id="b29215e9"></span>
### setActivityBookListener

Sets the listener for live stream booking. For callback information, see [ActivityBookListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#2d2129c0).

```Java
public void setActivityBookListener(ActivityBookListener listener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |ActivityBookListener |The listener for live stream booking. |


<span id="d240e1b4"></span>
### setCustomLanguageStringListener

Sets the listener for custom system texts. For callback information, see [CustomLanguageStringListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#c5d14099).

```Java
public void setCustomLanguageStringListener(CustomLanguageStringListener mCustomLanguageStringListener) 
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|mCustomLanguageStringListener |CustomLanguageStringListener |The listener for custom system texts. |


**Sample code**

The following sample code changes the text with the `key` `more` to `123` when the viewing page language is English.

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setCustomLanguageStringListener(new CustomLanguageStringListener() {
    @Override
    public String onCustomLanguageString(LanguageManager.LANGUAGE language, String key, String originString) {
        if (language == EN && "more".equals(key)) {
            return "123";  
        }
        return originString;
    }
});
```


<span id="773ba2f1"></span>
### setPublicCommentNickName

Sets the default nickname for viewers who join the live room when the authentication mode is public.

```Java
public void setPublicCommentNickName(String publicRegisterNickName, PublicNickNameRegisterListener nameRegisterListener)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|publicRegisterNickName |String |The nickname. If empty, no action is taken. |
|nameRegisterListener |PublicNickNameRegisterListener |The callback class for nickname registration results when the authentication mode of the live room is public. This parameter can be null. For more information, see [PublicNickNameRegisterListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#192a9ac2). |


<span id="9fa8eed2"></span>
### setShowPortraitRoomTopShadow

Sets whether to display a gradient overlay at the top of the live room in portrait mode.

```Java
public void setShowPortraitRoomTopShadow(boolean showPortraitRoomTopShadow)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|showPortraitRoomTopShadow |Boolean |Whether to display a gradient overlay at the top of the live room in portrait mode. Default value: `true`. Valid values:<br><br><br>* `true`: Display. If your video background is white, displaying the gradient overlay can make the white text at the top of the live room more visible.<br><br>* `false`: Do not display. |


<span id="543e5973"></span>
### setBdlExternalReportConfiguration

Sets data reporting configuration

```Java
public void setBdlExternalReportConfiguration(BDLExternalReportConfiguration bdlExternalReportConfiguration)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|bdlExternalReportConfiguration |BDLExternalReportConfiguration |Data reporting configuration. For more information, see [BDLExternalReportConfiguration](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#446d9b7a). |
