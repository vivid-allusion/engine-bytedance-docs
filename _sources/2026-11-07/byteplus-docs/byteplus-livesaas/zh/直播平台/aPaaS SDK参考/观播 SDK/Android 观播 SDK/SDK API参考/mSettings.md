---
title: "mSettings"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings-zh-CN"
---

本主题介绍多种自定义方法。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">SDK 的自定义设置优先于在 BytePlus Live 控制台或通过调用服务端 OpenAPI 设置的自定义配置。例如，如果你同时通过 SDK 的<code>setThumbIcon</code>方法和 BytePlus Live 控制台自定义直播间的点赞图标，则观看页显示的是<code>setThumbIcon</code>方法自定义的图标。</div>


* <div data-tips="true" data-tips-type="tip">本主题中的所有方法必须在观众进入直播间前调用。</div>



<span id="c84ea727"></span>
## 播放器

<span id="14c1fc92"></span>
### setPlayerLayoutMode

设置直播间在横屏模式下的视频缩放模式。

```java
public void setPlayerLayoutMode(int playerLayoutMode)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerLayoutMode |Integer |横屏模式下直播间的视频缩放模式。默认值：`0`。<br><br><br>* `0`：`ImageAspectFit`。填充播放器并保持视频长宽比。视频的宽度或高度填满播放器的宽度或高度。如果视频长宽比与播放器不同，视频会缩放以适应，且不会裁剪内容。<br><br>* `1`：`ImageToFill`。用视频填充播放器。视频长宽比可能会被改变。<br><br>* `2`：`ImageAspectFill`。填充播放器并保持视频长宽比。视频的宽度填满播放器的宽度，视频的高度填满播放器的高度。如果视频长宽比与播放器不同，视频会裁剪以适应。 |


<span id="bcd1844b"></span>
### setPortraitPlayerLayoutMode

设置直播间在竖屏模式下的视频缩放模式。

```java
public void setPortraitPlayerLayoutMode(int playerLayoutMode)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerLayoutMode |Integer |竖屏模式下直播间的视频缩放模式。默认值：`2`。<br><br><br>* `0`：`ImageAspectFit`。填充播放器并保持视频长宽比。视频的宽度或高度填满播放器的宽度或高度。如果视频长宽比与播放器不同，视频会缩放以适应，且不会裁剪内容。<br><br>* `1`：`ImageToFill`。用视频填满播放器。视频长宽比可能会发生变化。<br><br>* `2`：`ImageAspectFill`。填充播放器并保持视频长宽比。视频的宽度填满播放器的宽度，视频的高度填满播放器的高度。如果视频长宽比与播放器不同，视频会裁剪以适应。 |


<span id="9b743f4d"></span>
### setPeopleCountFontStyle

设置人气标签文本的字体。

```java
public void setPeopleCountFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |人气标签文本的字体。 |


<span id="d55a37d1"></span>
### setPeopleCountFontSize

设置人气标签文本的字体大小。

```Java
public void setPeopleCountFontSize(int peopleCountFontSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|peopleCountFontSiz |Integer |人气标签文本的字体大小。单位：sp。 |


<span id="08753ee9"></span>
### setPeopleCountTextColor

设置人气标签文本的颜色。

```Java
public void setPeopleCountTextColor(int peopleCountTextColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|peopleCountTextColor |Integer |人气标签文本的颜色。 |


<span id="351984cc"></span>
### setPeopleCountIconDrawable

设置人气图标。

```java
public void setPeopleCountIconDrawable(Drawable drawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|drawable |Drawable |人气图标。 |


<span id="3fecc7b5"></span>
### setPlayerThemeColor

设置播放器的主题色，即倍速按钮、进度条和分辨率按钮的颜色。

```java
public void setPlayerThemeColor(int playerThemeColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerThemeColor |Integer |播放器的主题色，即倍速按钮、进度条和分辨率按钮的颜色。 |


<span id="45fcf8aa"></span>
### setRoomStatusTextTipFontSize

设置直播间状态文本的字体大小。

```java
public void setRoomStatusTextTipFontSize(int roomStatusTextTipFontSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|roomStatusTextTipFontSize |Integer |直播间状态文本的字体大小。单位：sp。 |


<span id="a38c2a91"></span>
### setRoomStatusTextTipCenterOffset

设置直播间状态文本相对于播放器中心的垂直偏移。

```java
public void setRoomStatusTextTipCenterOffset(int roomStatusTextTipCenterOffset)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|roomStatusTextTipCenterOffset |Integer |直播间状态文本相对于播放器中心的垂直偏移。单位：dp。 |


<span id="0e07387a"></span>
### setRoomStatusTextTipRadius

设置直播间状态文本背景的圆角。

```java
public void setRoomStatusTextTipRadius(int roomStatusTextTipRadius)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|roomStatusTextTipRadius |Integer |直播间状态文本背景的圆角。单位：dp。 |


<span id="3aaaec13"></span>
### setRoomStatusTextTipHorizontalPadding

设置直播间状态文本的水平内边距。

```java
public void setRoomStatusTextTipHorizontalPadding(int roomStatusTextTipHorizontalPadding)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|roomStatusTextTipHorizontalPadding |Integer |直播间状态文本的水平内边距。该值不能为负。单位：dp。 |


<span id="eb9159a4"></span>
### setRoomStatusTextTipVerticalPadding

设置直播间状态文本的垂直内边距。

```java
public void setRoomStatusTextTipVerticalPadding(int roomStatusTextTipVerticalPadding)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|roomStatusTextTipVerticalPadding |Integer |直播间状态文本的垂直内边距。该值不能为负。单位：dp。 |


<span id="3da839f7"></span>
### setPlayerTimeColor

设置点播视频的时间颜色。

```java
public void setPlayerTimeColor(int playerTimeColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerTimeColor |Integer |点播视频的时间颜色。 |


<span id="de7e091f"></span>
### setFullScreenIcon

设置全屏图标。

```java
public void setFullScreenIcon(Drawable fullScreenIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|fullScreenIcon |Drawable |全屏图标。 |


<span id="c53da99c"></span>
### setSmallScreenIcon

设置退出全屏图标。

```java
public void setSmallScreenIcon(Drawable smallScreenIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|smallScreenIcon |Drawable |退出全屏图标。 |


<span id="10d1e9a9"></span>
### setLiveRefreshIcon

设置播放器左下角在**Live**状态下显示的刷新图标。

```java
public void setLiveRefreshIcon(Drawable liveRefreshIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|liveRefreshIcon |Drawable |**Live**状态下播放器左下角显示的刷新图标。 |


<span id="fea0b7ee"></span>
### setPlayerStartIcon

设置播放器左下角显示的播放图标。

```java
public void setPlayerStartIcon(Drawable playerStartIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerStartIcon |Drawable |播放器左下角显示的播放图标。 |


<span id="741fd598"></span>
### setPlayerPauseIcon

设置播放器左下角显示的暂停图标。

```java
public void setPlayerPauseIcon(Drawable playerPauseIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerPauseIcon |Drawable |播放器左下角显示的暂停图标。 |


<span id="b9f9855e"></span>
### setPlayerPausedCenterIcon

设置播放器中心显示的暂停状态图标。

```java
public void setPlayerPausedCenterIcon(Drawable playerPausedCenterIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerPausedCenterIcon |Drawable |播放器中央显示的暂停状态图标。 |


<span id="4c0db46f"></span>
### setCustomLiveName

设置直播间名称。

```java
public void setCustomLiveName(String customLiveName)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|customLiveName |String |直播间名称。设置后，传入的名称优先显示。如果传入空字符串，则名称会隐藏。 |


<span id="f1b19520"></span>
### setSpeedSettingDialogAutoClose

设置观众选择倍速时，倍速选择弹窗是否自动关闭。

```java
public void setSpeedSettingDialogAutoClose(boolean speedSettingDialogAutoClose)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|speedSettingDialogAutoClose |Boolean |当观众选择倍速时，倍速选择弹窗是否自动关闭。默认值：`false`。<br><br><br>* `true`：自动关闭。<br><br>* `false`：不自动关闭。 |


<span id="d34e9355"></span>
### setResolutionSettingDialogAutoClose

设置观众选择分辨率时，分辨率选择弹窗是否自动关闭。

```java
public void setResolutionSettingDialogAutoClose(boolean resolutionSettingDialogAutoClose)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|resolutionSettingDialogAutoClose |Boolean |当观众选择分辨率时，分辨率选择弹窗是否自动关闭。默认值：`false`。<br><br><br>* `true`：自动关闭。<br><br>* `false`：不自动关闭。 |


<span id="1df9583d"></span>
### setSimpleControlBar

设置直播间在横屏模式下是否启用简易控制栏。简易控制栏不包含倍速和分辨率选择按钮。

```java
public void setSimpleControlBar(boolean mSimpleControlBar)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mSimpleControlBar |Boolean |是否在横屏模式下启用直播间的简易控制栏。<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |


<span id="958af3e1"></span>
### setReplayTipText

设置回放的重播按钮文本。

```java
public void setReplayTipText(String mReplayTipText)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mReplayTipText |String |回放按钮的文本内容。 |


<span id="f77abe2b"></span>
### setLiveAutoPlay

设置是否自动播放直播视频。

```java
public void setLiveAutoPlay(boolean mLiveAutoPlay)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLiveAutoPlay |Boolean |是否自动播放直播视频。<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |


<span id="102e91a5"></span>
### setPlayBackAutoPlay

设置直播间在横屏模式下是否自动播放回放。

```java
public void setPlayBackAutoPlay(boolean mPlayBackAutoPlay)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPlayBackAutoPlay |Boolean |直播间在横屏模式下是否自动播放回放。<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |


<span id="a7710614"></span>
### setPortraitPlayBackAutoPlay

设置直播间在竖屏模式下是否自动播放回放。

```java
public void setPortraitPlayBackAutoPlay(boolean mPortraitPlayBackAutoPlay)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPortraitPlayBackAutoPlay |Boolean |直播间在竖屏模式下是否自动播放回放。<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |


<span id="f630c72c"></span>
### setForceShowAutoPlay

设置直播间在横屏模式下是否自动播放预告。

```java
public void setForceShowAutoPlay(boolean mForceShowAutoPlay)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mForceShowAutoPlay |Boolean |直播间在横屏模式下是否自动播放预告。<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |


<span id="28a79c72"></span>
### setPortraitForceShowAutoPlay

设置直播间在竖屏模式下是否自动播放预告。

```java
public void setPortraitForceShowAutoPlay(boolean mPortraitForceShowAutoPlay)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPortraitForceShowAutoPlay |Boolean |直播间在竖屏模式下是否自动播放预告。<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |


<span id="c0b34f9b"></span>
### setPlayBackLoop

设置直播间在横屏模式下是否自动循环播放回放。

```java
public void setPlayBackLoop(boolean mIsPlayBackLoop)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mIsPlayBackLoop |Boolean |直播间在横屏模式下是否自动循环播放回放。<br><br><br>* `true`：自动循环播放。<br><br>* `false`：不自动循环播放。 |


<span id="311325a4"></span>
### setPortraitPlayBackLoop

设置直播间在竖屏模式下是否自动循环播放回放。

```java
public void setPortraitPlayBackLoop(boolean mIsPortraitPlayBackLoop)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mIsPortraitPlayBackLoop |Boolean |直播间在竖屏模式下是否自动循环播放回放。<br><br><br>* `true`：自动循环播放。<br><br>* `false`：不自动循环播放。 |


<span id="2a2cd31c"></span>
### setForceShowLoop

设置直播间在横屏模式下是否自动循环播放预告。

```java
public void setForceShowLoop(boolean mIsForceShowLoop)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mIsForceShowLoop |Boolean |直播间在横屏模式下是否自动循环播放预告。<br><br><br>* `true`：自动循环播放。<br><br>* `false`：不自动循环播放。 |


<span id="f32e4191"></span>
### setPortraitForceShowLoop

设置当直播间处于竖屏模式时是否自动循环播放预告。

```java
public void setPortraitForceShowLoop(boolean mIsPortraitForceShowLoop)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mIsPortraitForceShowLoop |Boolean |直播间在竖屏模式下是否自动循环播放预告。<br><br><br>* `true`：自动循环播放。<br><br>* `false`：不自动循环播放。 |


<span id="937879b8"></span>
### setVodAutoContinuePlayback

设置是否启用点播视频的自动断点续播功能。

```java
public void setVodAutoContinuePlayback(boolean isVodAutoContinuePlayback)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|isVodAutoContinuePlayback |Boolean |是否启用点播视频的自动断点续播功能。默认值：`true`。<br><br><br>* `true`：启用自动断点续播。当观众退出并重新进入直播间时，点播视频会自动从断点处继续播放。<br><br>* `false`：禁用自动断点续播。 |


<span id="3884d8f7"></span>
### setVodAutoSeekTipTextVisible

设置点播视频自动断点续播时是否显示提示。

```java
public void setVodAutoSeekTipTextVisible(boolean mVodAutoSeekTipTextVisible)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mVodAutoSeekTipTextVisible |Boolean |点播视频自动断点续播时是否显示提示。默认值：`true`。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="355c7e9b"></span>
### setVodAutoSeekTipTextSize

设置点播视频自动断点续播提示的字体大小。

```java
public void setVodAutoSeekTipTextSize(float mVodAutoSeekTipTextSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mVodAutoSeekTipTextSize |float |点播视频自动断点续播提示的字体大小。默认值：`11`。单位：sp。 |


<span id="05c5b49f"></span>
### setEnterFullScreenEnable

设置观众是否可以进入全屏模式。

```Java
public void setEnterFullScreenEnable(boolean enterFullScreenEnable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|enterFullScreenEnable |Boolean |观众是否可以进入全屏模式。默认值：`true`。<br><br><br>* `true`：观众可以进入全屏模式。播放器中会显示全屏按钮。当直播视频或点播视频的源视频流宽度大于高度时，在竖屏模式的直播间和横屏模式的直播间中会显示全屏按钮。<br><br>* `false`：观众无法进入全屏模式。播放器中不会显示全屏按钮。 |


<span id="1909af7e"></span>
### setNeedAutoDemote

设置直播流出现网络卡顿时是否支持自动降级或弹出提示。

```Java
public void setNeedAutoDemote(boolean needAutoDemote)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|needAutoDemote |Boolean |直播流过程中出现网络类型卡顿时，是否支持自动降级或提示。默认值：`true`。<br><br><br>* `true`：<br><br>   * 若[setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall)参数值为`true`，则直接在主流和备流之间切换。<br><br>   * 如果[setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall)参数值为`false`，在智能模式下，将自动降级到更低的分辨率。如果在最低分辨率下仍然出现卡顿，则在主流和备流之间切换。在非智能模式下，向观众弹出提示，询问是否切换到更低的分辨率，允许观众根据需要选择。如果观众切换到最低分辨率后仍然出现卡顿，则在主流和备流之间切换。<br><br>* `false`：在智能模式下，不自动降级。在非智能模式下，不通知观众切换到更低的分辨率。 |


<span id="8c5dc53a"></span>
### setBackupDowngradeWhenStall

设置直播流卡顿时是否直接切换主流和备流。

```Java
public void setBackupDowngradeWhenStall(boolean backupDowngradeWhenStall)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|backupDowngradeWhenStall |boolean |直播流出现卡顿时，是否直接在主流和备流之间切换。默认值：`false`。仅当[setNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setneedautodemote)参数值为`true`时，该方法生效。<br><br><br>* `true`：直接在主流和备流之间切换。<br><br>* `false`：在智能模式下，自动降级到更低的分辨率。如果在最低分辨率下仍然出现卡顿，则在主流和备流之间切换。在非智能模式下，向观众弹出提示，询问是否切换到更低的分辨率，允许观众根据需要选择。如果观众切换到最低分辨率后仍然出现卡顿，则在主流和备流之间切换。 |


<span id="6fafa479"></span>
### setEnableShowPortraitRoomTopArea

设置竖屏模式下是否显示直播间顶部区域，包括右上角关闭按钮、主播账号信息、热度数和多线路切换按钮。

```Java
public void setEnableShowPortraitRoomTopArea(boolean enableShowPortraitRoomTopArea)
```


**参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|enableShowPortraitRoomTopArea |Boolean |是否显示竖屏直播间的整个顶部区域。默认值：`true`。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="a208dfb2"></span>
### addChildViewInLinearLayout

在直播间指定位置插入自定义悬浮 View。

```Java
public void addChildViewInLinearLayout(View childView, int location, boolean isLastChild, CustomSize customSize)
```


**参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|childView |View |待插入的自定义View。 |
|location |int |指定插入位置。默认值：。<br><br><br>* `ADD_CHILD_VIEW_LEFT_TOP`：将视图插入到左上角。<br><br>* `ADD_CHILD_VIEW_RIGHT_TOP`：将视图插入到右上角。<br><br>* `ADD_CHILD_VIEW_RIGHT_BOTTOM`：将视图插入到右下角。 |
|isLastChild |Boolean |当前视图是否为最后一个子View。默认值：。<br><br><br>* `true`：该视图为最后一个View。<br><br>* `false`：该视图不是最后一个View。 |
|customSize |CustomSize |自定义View的尺寸。默认值：。 |


<span id="2d369486"></span>
## 菜单

<span id="d0e012ac"></span>
### setMenuTabBackgroundDrawable

设置横屏模式下直播间菜单栏的背景。

```java
public void setMenuTabBackgroundDrawable(Drawable drawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|drawable |Drawable |横屏模式下直播间菜单栏的背景。 |


<span id="53ea42b5"></span>
### setMenuFontColor

设置菜单栏菜单项在选中或未选中时的文本颜色。

```java
public void setMenuFontColor(new Pair<>(unSelectedColor,selectedColor))
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|unSelectedColor |Integer |横屏模式下直播间菜单栏未选中菜单项的文本颜色。 |
|selectedColor |Integer |横屏模式下直播间菜单栏选中菜单项的文本颜色。 |


<span id="b7289d01"></span>
### setMenuFontStyle

设置菜单栏的字体。

```java
public void setMenuFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |菜单栏的字体。 |


<span id="04b74c84"></span>
### setLandMenuFlowingTagColor

设置横屏模式下直播间菜单栏选中菜单项的指示器颜色。

```java
public void setLandMenuFlowingTagColor(int landMenuFlowingTagColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|landMenuFlowingTagColor |Integer |横屏模式下直播间菜单栏选中菜单项的指示器颜色。默认值：`0xFF3370FF`。 |


<span id="15c8126e"></span>
### setMenuDialogFlowingTagColor

设置竖屏模式下直播间菜单栏内嵌链接和图文菜单项选中时的指示器颜色。

```Java
public void  setMenuDialogFlowingTagColor(int menuDialogFlowingTagColor) 
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|menuDialogFlowingTagColor |Integer |竖屏模式下直播间菜单栏内嵌链接和图文菜单项选中时的指示器颜色。默认值：`0xFF161823`。 |


<span id="34aaada2"></span>
### setImageEmbeddedWebUrlsIcon

设置竖屏模式下直播间内嵌链接菜单的图标。

```Java
public void setImageEmbeddedWebUrlsIcon(Drawable imageEmbeddedWebUrlsIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|imageEmbeddedWebUrlsIcon |Drawable |竖屏模式下直播间内嵌链接菜单的图标。 |


<span id="ea75f056"></span>
### setMenuDialogTabFontSize

设置内嵌链接和图文菜单标题的字体大小。

```Java
public void setMenuDialogTabFontSize(int menuDialogTabFontSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|menuDialogTabFontSize |Integer |内嵌链接和图文菜单标题的字体大小。单位：sp。 |


<span id="26a3e658"></span>
### setMenuDialogTabSelectedFontColor

设置内嵌链接和图文菜单选中时标题文本颜色。

```java
public void setMenuDialogTabSelectedFontColor(int menuDialogTabSelectedFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|menuDialogTabSelectedFontColor |Integer |选中时，内嵌链接和图形菜单的标题文本颜色。默认值：`0xFF161823`。 |


<span id="6c07f026"></span>
### setMenuDialogTabUnSelectedFontColor

设置内嵌链接和图文菜单未选中时标题文本颜色。

```java
public void setMenuDialogTabUnSelectedFontColor(int menuDialogTabUnSelectedFontColor) 
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|menuDialogTabUnSelectedFontColor |整数 |未选中时，内嵌链接和图形菜单的标题文本颜色。默认值：`0xFF161823`。 |


<span id="6bc0db40"></span>
## 评论

<span id="fe61f617"></span>
### setNoCommentIconDrawable

设置评论区无评论时显示的占位图标。

```java
public void setNoCommentIconDrawable(Drawable drawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|drawable |Drawable |评论区无评论时显示的占位图标。 |


<span id="7a4995ea"></span>
### setCommentNicknameFontStyle

设置非主播昵称的字体。

```java
public void setCommentNicknameFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |非主播昵称的字体。 |


<span id="44c1830f"></span>
### setCommentNicknameFontColor

设置非主播昵称的颜色。

```java
public void setCommentNicknameFontColor(int commentNicknameFontColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentNicknameFontColor |整数 |非主播昵称的颜色。 |


<span id="2885642f"></span>
### setCommentNicknameFontSize

设置非主播昵称的字体大小。

```Java
public void setCommentNicknameFontSize(int commentNicknameFontSize)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentNicknameFontSize |整数 |非主播昵称的字体大小。单位：sp。 |


<span id="910f28cf"></span>
### setCommentContentFontColor

设置非主播评论内容的文本颜色。

```java
public void setCommentContentFontColor(int commentContentFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentContentFontColor |整数 |非主播评论的文本颜色。 |


<span id="d73603d2"></span>
### setCommentLinkColor

设置评论链接的颜色。

```java
public void setCommentLinkColor(int mCommentLinkColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mCommentLinkColor |整数 |评论链接的颜色。 |


<span id="4d6e871a"></span>
### setAudienceCommentLinkClickable

设置非主播评论中的链接是否可点击。

```java
public void setAudienceCommentLinkClickable(boolean mAudienceCommentLinkClickable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mAudienceCommentLinkClickable |布尔值 |非主播评论中的链接是否可点击。关于观众点击评论中的链接时的自定义操作，请参见[setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#be1306ce)。<br><br><br>* `true`：可点击。<br><br>* `false`：不可点击。 |


<span id="7975da1e"></span>
### setCommentContentFontStyle

设置非主播评论内容的字体。

```java
public void setCommentContentFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |非主播评论的字体。 |


<span id="a6dabe5a"></span>
### setCommentContentFontSize

设置非主播评论内容的字体大小。

```Kotlin
public void setCommentContentFontSize(int commentContentFontSize)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentContentFontSize |整数 |非主播评论的字体大小。单位：sp。 |


<span id="032f1ab3"></span>
### setHostTagFontStyle

设置主播标签的字体。

```java
public void setHostTagFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |主播标签的字体。 |


<span id="3e4dfbf9"></span>
### setHostTagFontSize

设置主播标签的字体大小。

```Java
public void setHostTagFontSize(int hostTagFontSize)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|hostTagFontSize |整数 |主播标签的字体大小。单位：sp。 |


<span id="158d5023"></span>
### setTopCommentTagFontStyle

设置置顶标签的字体。

```java
public void setTopCommentTagFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |置顶标签的字体。 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">此方法自 1.51.0 版本起不再支持。</div>


<span id="52954629"></span>
### setTopCommentFontStyle

设置置顶内容的字体。

```java
public void setTopCommentFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |置顶内容的字体。 |


<span id="262969ee"></span>
### setTopCommentFontColor

设置置顶内容的文本颜色。

```java
public void setTopCommentFontColor(int topCommentFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|topCommentFontColor |整数 |置顶内容的文本颜色。 |


<span id="261f08a4"></span>
### setTopCommentRowCount

设置置顶评论显示的最大行数。

```java
public void setTopCommentRowCount(int count)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|count |整数 |置顶评论显示的最大行数。默认值：`1`。 |


<span id="70a0fcb1"></span>
### setTopCommentDialogTitleAtStart

设置是否将置顶内容详情对话框的标题显示在最左侧。

```java
public void setTopCommentDialogTitleAtStart(boolean mTopCommentDialogAtStart)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mTopCommentDialogAtStart |布尔值 |置顶内容详情弹窗的标题是否显示在最左侧。<br><br><br>* `true`：在最左侧。<br><br>* `false`：不在最左侧。 |


<span id="4338c1b2"></span>
### setPortraitCommentAreaHeight

设置竖屏模式下直播间评论区的高度。

```java
public void setPortraitCommentAreaHeight(int mPortraitCommentAreaHeight)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPortraitCommentAreaHeight |整数 |竖屏模式下直播间评论区的高度。该值不能为负数。默认值：`194`。单位：dp。 |


<span id="748d2665"></span>
### setPortraitCommentLineCount

设置竖屏模式下直播间每条评论显示的最大行数。

```java
public void setPortraitCommentLineCount(int mPortraitCommentLineCount)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPortraitCommentLineCount |整数 |竖屏模式下直播间每条评论显示的最大行数。 |


<span id="a2aac31c"></span>
### setCommentEditViewHintTextColor

设置评论输入框占位文本的颜色。

```java
public void setCommentEditViewHintTextColor(int color)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|color |整数 |评论输入框占位文本的颜色。默认值：`0xB3FFFFFF` |


<span id="bab9d110"></span>
### setCommentEditViewTextColor

设置评论输入框中输入文本的颜色。

```java
public void setCommentEditViewTextColor(int mCommentEditViewTextColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mCommentEditViewTextColor |整数 |评论输入框中输入文本的颜色。默认值：`0xFF000000`。 |


<span id="425e8f28"></span>
### setCommentIntervalTip

设置评论间隔提示的内容。

```java
public void setCommentIntervalTip(String tip)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|tip |字符串 |评论间隔提示的内容。 |


<span id="175601a7"></span>
### setCommentIntervalFontStyle

设置评论间隔提示内容的字体样式。

```java
public void setCommentIntervalFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |评论间隔提示内容的字体。 |


<span id="2b82be95"></span>
### setCommentItemBgColor

设置欢迎消息、进房消息和非主播评论的背景色。

```java
public void setCommentItemBgColor(int commentItemBgColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentItemBgColor |整数 |欢迎消息、进房消息及非主播评论的背景色。默认值：`#33000000`。 |


<span id="ff6e1afe"></span>
### setPullCommentCount

设置每次拉取的评论条数。

```java
public void setPullCommentCount(int count)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|count |整数 |每次拉取的评论数量。 |


<span id="ad021546"></span>
### setPullHistoryCommentTotalCount

设置可拉取的历史评论总数。

```java
public void setPullHistoryCommentTotalCount(int count)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|count |整数 |可拉取的历史评论总数。 |


<span id="075b7249"></span>
### setThumbIcon

设置直播间点赞的图标。

```java
public void setThumbIcon(Drawable drawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|drawable |Drawable |直播间点赞图标。 |


<span id="40624408"></span>
### setJoinRoomMsgNicknameColor

设置直播间进房消息中昵称的文本颜色。

```java
public void setJoinRoomMsgNicknameColor(int mJoinRoomMsgNicknameColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mJoinRoomMsgNicknameColor |整数 |直播间进房消息昵称的文本颜色。 |


<span id="5488ff75"></span>
### setJoinRoomMsgContentColor

设置直播间进房消息内容的文本颜色。

```java
public void setJoinRoomMsgContentColor(int mJoinRoomMsgContentColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mJoinRoomMsgContentColor |整数 |直播间进房消息内容的文本颜色。 |


<span id="b006f58b"></span>
### setWelcomeMsgFontColor

设置直播间欢迎消息的文本颜色。

```java
public void setWelcomeMsgFontColor(int mWelcomeMsgFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mWelcomeMsgFontColor |整数 |直播间欢迎消息的文本颜色 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">从 1.53.0 版本开始不再支持此方法。请改用 <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor">setSystemCommentColor</a> 方法。</div>


<span id="c5541059"></span>
### setLandscapeCommentShouldShowAvatar

设置横屏模式下直播间评论区是否显示用户头像。

调用[setHostDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#3dc09158)设置主播默认头像，调用[setCommentDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#a8949de3)设置非主播默认头像。自定义模式下（当`roomAuthMode`为CUSTOM时），可调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)传入指定用户的头像URL。

```java
public void setLandscapeCommentShouldShowAvatar(boolean landscapeCommentShouldShowAvatar)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|landscapeCommentShouldShowAvatar |Boolean |横屏模式下，是否在直播间评论区显示用户头像。默认值：`true`。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="f68ed0e2"></span>
### setPortraitCommentShouldShowAvatar

设置竖屏模式下直播间评论区是否显示用户头像。

调用[setHostDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#3dc09158)设置主播默认头像，调用[setCommentDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#a8949de3)设置非主播默认头像。自定义模式下（当`roomAuthMode`为CUSTOM时），可调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)传入指定用户的头像URL。

```java
public void setPortraitCommentShouldShowAvatar(boolean portraitCommentShouldShowAvatar)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|portraitCommentShouldShowAvatar |Boolean |竖屏模式下，是否在直播间评论区显示用户头像。默认值：`false`。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="3dc09158"></span>
### setHostDefaultAvatar

设置评论区主播的默认头像。

```java
public void setHostDefaultAvatar(Drawable hostDefaultAvatar)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|hostDefaultAvatar |Drawable |评论区主播的默认头像。 |


<span id="a8949de3"></span>
### setCommentDefaultAvatar

设置评论区非主播的默认头像。设置后，该头像会显示在每条非主播评论前。

```java
public void setCommentDefaultAvatar(Drawable commentDefaultAvatar)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentDefaultAvatar |Drawable |评论区非主播的默认头像。 |


<span id="3c5e004d"></span>
### setThumbFloatingDrawableListener

设置观众点赞直播间后显示的浮动动画图标的监听器。回调信息详见[ITVUMultipleDrawableListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#7929f65e)。

```java
public void setThumbFloatingDrawableListener(ITVUMultipleDrawableListener listener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|listener |ITVUMultipleDrawableListener |观众点赞直播间后显示的浮动动画图标的监听器。 |


<span id="3822d4b1"></span>
### setHostCommentColor

设置主播评论的文本颜色。

```Java
public void setHostCommentColor(int hostCommentColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|hostCommentColor |Integer |主播评论的文本颜色。 |


<span id="ac731a87"></span>
### setHostCommentBackgroundColor

设置主播评论的背景色。

```Java
public void setHostCommentBackgroundColor(int hostCommentBackgroundColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|hostCommentBackgroundColor |Integer |主播评论的背景颜色。 |


<span id="9169ea51"></span>
### setHostTagFontColor

设置主播标签的颜色。

```Java
public void setHostTagFontColor(int hostTagFontColor) 
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|hostTagFontColor |Integer |主播标签的颜色。 |


<span id="f7ccfd88"></span>
### setHostCommentFontSize

设置主播评论的字体大小。

```Java
public void setHostCommentFontSize(int mHostCommentFontSize)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|mHostCommentFontSize |Integer |主播评论的字体大小。单位：sp。 |


<span id="68c26a6c"></span>
### setHostCommentFontStyle

设置主播评论的字体样式。

```Java
public void setHostCommentFontStyle(Typeface hostCommentFontStyle)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|hostCommentFontStyle |Typeface |主播评论的字体。 |


<span id="c30d44f3"></span>
### setSystemCommentTagFontStyle

设置竖屏模式下直播间接口行为标签和欢迎消息的字体样式。

```Java
public void setSystemCommentTagFontStyle(Typeface systemCommentTagFontStyle)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|systemCommentTagFontStyle |Typeface |竖屏模式下直播间描述和欢迎消息标签的字体。 |


<span id="1de92ebe"></span>
### setSystemCommentTagFontSize

设置竖屏模式下直播间接口行为标签和欢迎消息的字体大小。

```Java
public void setSystemCommentTagFontSize(int systemCommentTagFontSize
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|systemCommentTagFontSize |Integer |竖屏模式下直播间描述和欢迎消息标签的字体大小。单位：sp。 |


<span id="d5b319a2"></span>
### setSystemCommentTagFontColor

设置竖屏模式下直播间接口行为标签和欢迎消息的标签颜色。

```Java
public void setSystemCommentTagFontColor(int systemCommentTagFontColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|systemCommentTagFontColor |Integer |竖屏模式下直播间描述和欢迎消息标签的颜色。 |


<span id="06ae9e64"></span>
### setSystemCommentFontStyle

设置竖屏模式下直播间描述和欢迎消息正文的字体。

```Java
public void setSystemCommentFontStyle(Typeface systemCommentFontStyle)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|systemCommentFontStyle |Typeface |竖屏模式下直播间描述和欢迎消息正文的字体。 |


<span id="599c655a"></span>
### setSystemCommentFontSize

设置竖屏模式下直播间描述和欢迎消息正文的字体大小。

```Java
public void setSystemCommentFontSize(int systemCommentFontSize)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|systemCommentFontSize |Integer |竖屏模式下直播间描述和欢迎消息正文的字体大小。单位：sp。 |


<span id="c7606a4c"></span>
### setSystemCommentColor

设置竖屏模式下直播间描述和欢迎消息正文的文本颜色。

```Java
public void setSystemCommentColor(int systemCommentColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|systemCommentColor |Integer |竖屏模式下直播间描述和欢迎消息正文的文本颜色。 |


<span id="931a0bba"></span>
### setCommentItemSpacing

设置相邻评论之间的间距。

```Java
public void setCommentItemSpacing(int mDistanceBetweenCommentItem
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|mDistanceBetweenCommentItem |Integer |相邻评论之间的间距。默认值：`6`。单位：dp。 |


<span id="5f9f91d5"></span>
### setRoomCommentListViewBottomMargin

设置评论列表底部与评论输入框顶部之间的间距。

```Java
public void setRoomCommentListViewBottomMargin(int roomCommentListViewBottomMargin)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|roomCommentListViewBottomMargin |Integer |评论列表底部与评论输入框顶部之间的间距。默认值：`0`。单位：dp。 |


<span id="08f729f4"></span>
### setCommentListPullToRefreshColor

设置下拉刷新组件的内容颜色，例如`↓ 下拉加载更多评论`。

```Java
public void setCommentListPullToRefreshColor(int mCommentListPullToRefreshColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|mCommentListPullToRefreshColor |Integer |下拉刷新组件的内容颜色，例如 `↓ 下拉加载更多评论`。 |


<span id="a60099d7"></span>
### setCommentLikedIcon

设置评论已点赞时的点赞图标。

```Java
public void setCommentLikedIcon(BDThemeIconModel commentLikedIcon) {
    mCommentLikedIcon = commentLikedIcon;
}
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentLikedIcon |BDThemeIconModel |按钮信息。更多信息请参见 [BDThemeIconModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#56a27a1b)。 |


<span id="166c853b"></span>
### setCommentLikeIcon

设置评论未点赞时的点赞图标。

```Java
public void setCommentLikeIcon(BDThemeIconModel commentLikeIcon) {
    mCommentLikeIcon = commentLikeIcon;
}
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentLikeIcon |BDThemeIconModel |按钮信息。更多信息请参见 [BDThemeIconModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#56a27a1b)。 |


<span id="542ef80d"></span>
### setCommentInputCountLimit

设置评论输入框允许输入的最大字符数。

```Java
public void setCommentInputCountLimit(int commentInputCountLimit)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentInputCountLimit |Integer |评论输入框允许输入的最大字符数。默认值：`200`。 |


<span id="ea9bfd75"></span>
### setCommentCustomListener

设置直播间评论的自定义监听器。

```Java
public void setCommentCustomizeListener(CommentCustomizeListener commentCustomizeListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentCustomizeListener |CommentCustomizeListener |直播间评论的自定义监听器。更多信息请参见 [CommentCustomizeListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#2c977992)。 |


**示例代码**

以下示例代码将文本评论中的`123`颜色改为黄色，并将笑脸表情替换为其他图片。

```Java
settings.setCommentCustomizeListener((commentModel, commentConfigModel, uiConfigModel, languageManager, spannableStringBuilder, textView) -> {
    boolean presenter = commentModel.isPresenter(); // 判断评论是否由主播发送。
    boolean lightTheme = uiConfigModel.isLightTheme(); // 判断主题是否为非暗色模式。
    LanguageManager.LANGUAGE currentLanguage = languageManager.getCurrentLanguage();// 获取直播间当前选择的语言。
    
    String s = spannableStringBuilder.toString();
    
    // 将文本评论中的“123”颜色改为黄色。
    if (s.contains("123")) {
        spannableStringBuilder.setSpan(new ForegroundColorSpan(Color.YELLOW),
                s.indexOf("123"), s.indexOf("123") + 3, Spannable.SPAN_INCLUSIVE_EXCLUSIVE);
    }
    
    // 将笑脸表情替换为其他图片。
    if (s.contains("[Smile]")) {
        spannableStringBuilder.setSpan(new GlideImageSpan(textView, "https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/055f8e4f26c04fd39aa3a3935a43866e~tplv-goo7wpa0wc-image.image"),
                s.indexOf("[Smile]"), s.indexOf("[Smile]") + "[Smile]".length(), Spannable.SPAN_INCLUSIVE_EXCLUSIVE);
    }
    // 重置 textView 以应用更改。
    textView.setText(spannableStringBuilder);
});
```


<span id="8b6e0523"></span>
### setTopCommentViewCornerRadius

设置置顶评论背景的圆角。

```Java
public void setTopCommentViewCornerRadius(int topCommentViewCornerRadius)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentViewCornerRadius |int |置顶评论背景的圆角半径。默认值：`8`。单位：dp。 |


<span id="115fbc19"></span>
### setTopCommentBackgroundWidthFitContent

设置置顶评论背景宽度是否随内容宽度自适应。

```Java
public void setTopCommentBackgroundWidthFitContent(boolean topCommentBackgroundWidthFitContent)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentBackgroundWidthFitContent |boolean |置顶评论背景的宽度是否随内容宽度自适应。默认值：`false`。有效值：<br><br><br>* `true`：置顶评论背景宽度随内容宽度自适应。<br><br>* `false`：置顶评论背景宽度为固定值。 |


<span id="36d938dc"></span>
### setTopCommentNicknameColor

设置置顶评论昵称的颜色。

```Java
public void setTopCommentNicknameColor(int topCommentNicknameColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentNicknameColor |int |置顶评论昵称的颜色。 |


<span id="e85f2897"></span>
### setTopCommentNicknameFontSize

设置置顶评论昵称的字体大小。

```Java
public void setTopCommentNicknameFontSize(int topCommentNicknameFontSize)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentNicknameFontSize |int |置顶评论昵称的字体大小。单位：sp。 |


<span id="9891737b"></span>
### setTopCommentNicknameFontStyle

设置置顶评论昵称的字体。

```Java
public void setTopCommentNicknameFontStyle(Typeface topCommentNicknameFontStyle)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentNicknameFontStyle |Typeface |置顶评论昵称的字体。 |


<span id="826adc59"></span>
### setTopCommentContentLineSpacingExtra

设置置顶评论内容的行间距。

```Java
public void setTopCommentContentLineSpacingExtra(int topCommentContentLineSpacingExtra)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentContentLineSpacingExtra |int |置顶评论内容的行间距。单位：dp。 |


<span id="452857ff"></span>
### setTopCommentTagColor

设置置顶评论昵称左侧竖线的颜色。

```Java
public void setTopCommentTagColor(int topCommentTagColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentTagColor |int |置顶评论昵称左侧竖线的颜色。 |


<span id="b5661b0f"></span>
### setTopCommentBackgroundColor

设置置顶评论的背景颜色。

```Java
public void setTopCommentBackgroundColor(int topCommentBackgroundColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|topCommentBackgroundColor |int |置顶评论的背景色。 |


<span id="5fc5536f"></span>
### setPopupInputBoxPromptTextColor

设置评论输入框处于编辑状态（即弹出键盘时）的占位文本颜色。

```Java
public void setPopupInputBoxPromptTextColor(int popupInputBoxPromptTextColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|popupInputBoxPromptTextColor |int |编辑状态下评论输入框的占位文本颜色，即键盘弹出时。 |


<span id="a128a852"></span>
### setPopupInputBoxTextColor

设置评论输入框处于编辑状态（即弹出键盘时）已输入文本的颜色。

```Java
public void setPopupInputBoxTextColor(int popupInputBoxTextColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|popupInputBoxTextColor |int |编辑状态下评论输入框的已输入文本颜色，即键盘弹出时。 |


<span id="e349d9b3"></span>
### setInputBoxPromptTextColor

设置评论输入框处于非编辑状态（即未弹出键盘时）的占位文本颜色。

```Java
public void setInputBoxPromptTextColor(int inputBoxPromptTextColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|inputBoxPromptTextColor |int |非编辑状态下评论输入框的占位文本颜色，即键盘未弹出时。 |


<span id="bb581984"></span>
### setInputBoxTextColor

设置评论输入框处于非编辑状态（即未弹出键盘时）已输入文本的颜色。

```Java
public void setInputBoxTextColor(int inputBoxTextColor)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|inputBoxTextColor |int |非编辑状态下评论输入框的已输入文本颜色，即键盘未弹出时。 |


<span id="40f70e3f"></span>
### setInputBoxCornerRadius

设置评论输入框处于非编辑状态（即未弹出键盘时）的圆角。

```Java
public void setInputBoxCornerRadius(int inputBoxCornerRadius)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|inputBoxCornerRadius |int |非编辑状态下评论输入框的圆角半径，即键盘未弹出时。默认值：`19`。单位：dp。 |


<span id="992d58e3"></span>
### setCommentCellCornerRadius

设置评论单元格的圆角。

```Java
public void setCommentCellCornerRadius(int commentCellCornerRadius)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentCellCornerRadius |int |评论单元格的圆角半径。默认值：`12`。单位：dp。 |


<span id="016961d8"></span>
### setCommentContentLineSpacingExtra

设置评论内容的行间距。

```Java
public void setCommentContentLineSpacingExtra(int commentContentLineSpacingExtra)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentContentLineSpacingExtra |int |评论内容的行间距。单位：dp。 |


<span id="2a63cdb6"></span>
### setFunctionEntranceButtonCornerRadius

设置直播间右下角功能入口按钮（如购物车、互动工具按钮）的圆角。

```Java
public void setFunctionEntranceButtonCornerRadius(int functionEntranceButtonCornerRadius)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|functionEntranceButtonCornerRadius |int |位于直播间右下角的功能入口按钮（如购物车、互动工具按钮）的圆角半径。默认值：`18`。单位：dp。 |


<span id="a75bf5dd"></span>
## 注册对话框

<span id="de14983a"></span>
### setNicknameDialogHeadFontStyle

设置标题的字体。

```java
public void setNicknameDialogHeadFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |标题的字体。 |


<span id="8dee7093"></span>
### setNicknameDialogEditTextFontStyle

设置输入框内文本的字体。

```java
public void setNicknameDialogEditTextFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |输入框内文本的字体。 |


<span id="31291001"></span>
### setNicknameDialogHintText

设置输入框的占位文本。

```java
public void setNicknameDialogHintText(String tip)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|tip |String |输入框的占位符。 |


<span id="902a970a"></span>
### setNicknameDialogButtonColor

设置确认按钮的背景色。

```java
public void setNicknameDialogButtonColor(int color)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|color |Integer |确认按钮的背景色。 |


<span id="719a810a"></span>
### setNicknameDialogButtonTextFontStyle

设置确认按钮的字体。

```java
public void setNicknameDialogButtonTextFontStyle(Typeface typeface)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|typeface |Typeface |确认按钮的字体。 |


<span id="f2244eec"></span>
### setNicknameDialogCloseButtonIconDrawable

设置关闭图标。

```java
public void setNicknameDialogCloseButtonIconDrawable(Drawable drawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|drawable |Drawable |关闭图标。 |


<span id="83ccfbdf"></span>
## 图形

<span id="7aea6698"></span>
### setRichTextPadding

设置图形区域的上、下、左、右边距。

```java
public void setRichTextPadding(int padding)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|padding |Integer |图文区域的上、下、左、右边距。该值不能为负数。单位：dp。 |


<span id="bfdcd525"></span>
### setImageTextContentColor

设置图形内容的文字颜色。

```java
public void setImageTextContentColor(int mImageTextContentColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mImageTextContentColor |Integer |图文内容的文本颜色。<br><br>若值为`0`或为空，则使用服务器返回的文本颜色。 |


<span id="5bf1f53a"></span>
## 广告

<span id="f6305e09"></span>
### setPageCenterAdRatio

设置页中广告的视频长宽比。

```java
public void setPageCenterAdRatio(float pageCenterAdRatio)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|pageCenterAdRatio |float |页中广告的视频长宽比。 |


<span id="50a8bd40"></span>
### setCenterAdStrokeColor

设置页中广告的边框颜色。

```java
public void setCenterAdStrokeColor(int centerAdStrokeColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|centerAdStrokeColor |Integer |页中广告的边框颜色。 |


<span id="1be75c00"></span>
### setCenterAdRadius

设置页中广告的圆角。

```java
public void setCenterAdRadius(int centerAdRadius)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|centerAdRadius |Integer |页中广告的圆角。 |


<span id="314388e8"></span>
### setCenterAdRotationInterval

设置页中广告的轮播速度。

```java
public void setCenterAdRotationInterval(int centerAdRotationInterval)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|centerAdRotationInterval |Integer |页中广告的轮播速度，具体指轮播向右滑动的频率。单位：ms。 |


<span id="1448f45f"></span>
### setFloatAdLayoutParams

设置浮标广告的默认位置。

```Java
public void setFloatAdLayoutParams(SimpleLayoutParams floatAdLayoutParams)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatAdLayoutParams |SimpleLayoutParams |浮标广告的默认位置。有关配置详情，请参见[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e4a2c940)。 |


<span id="039e38e4"></span>
### setFloatAdSize

设置浮标广告的尺寸。

```Java
public void setFloatAdSize(CustomSize floatAdSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatAdSize |CustomSize |浮标广告的尺寸。有关配置详情，请参见[CustomSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#38b050a5)。 |


<span id="a252408c"></span>
### setFloatAdMovable

设置是否允许观众拖动浮标广告。

```Java
public void setFloatAdMovable(boolean FloatAdMovable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|FloatAdMovable |Boolean |是否允许观众拖动浮标广告。默认值：`false`。可选值：<br><br><br>* `true`：允许。<br><br>* `false`：不允许。 |


<span id="845b7139"></span>
### setFloatAdShowBounds

设置浮标广告是否显示白色边框和背景。

```Java
public void setFloatAdShowBounds(boolean floatAdShowBounds)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatAdShowBounds |Boolean |浮标广告是否显示白色边框和背景。默认值：`true`。可选值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="de9bce95"></span>
### **setShowPageHeaderImage**

设置是否显示页头图。

```Java
  public void setShowPageHeaderImage(boolean show)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|show |Boolean |是否显示页头图。默认值：`true`。可选值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="c2532e01"></span>
### **setShowPageCenterAd**

设置是否显示页中广告。

```Java
  public void setShowPageCenterAd(boolean show)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|show |Boolean |是否显示页中广告。默认值：`true`。可选值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="3a79a1ea"></span>
## 播放器网络类型状态变化

<span id="83c1947d"></span>
### setShowNonWiFiToast

设置是否显示使用移动数据的提示。

```java
public void setShowNonWiFiToast(boolean mShowNonWiFiToast)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mShowNonWiFiToast |Boolean |是否显示使用移动数据的提示。默认值：`true`。可选值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="6a5da8bd"></span>
### setLandNonWifiToastCount

设置横屏模式下直播间内使用移动数据提示文本出现的次数。

```java
public void setLandNonWifiToastCount(int mNonWifiToastCount)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNonWifiToastCount |Integer |在横屏模式下，直播间内使用移动数据提示文本出现的次数。默认值：`1`。<br><br><br>* `-1`：每次都显示提示。<br><br>* `0`：不显示提示。<br><br>* `≥ 1`：显示1次及以上提示。 |


<span id="fe25a490"></span>
### setRetryBtnBackgroundColor

设置横屏模式下直播间**重试**按钮的背景色。

```java
public void setRetryBtnBackgroundColor(int btnBackGround)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|btnBackGround |Integer |横屏模式下，直播间中**Retry**按钮的背景色。 |


<span id="80e7d2c4"></span>
### setPorRetryBtnBackgroundColor

设置竖屏模式下直播间**重试**按钮的背景色。

```java
public void setPorRetryBtnBackgroundColor(int btnBackGround)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|btnBackGround |Integer |竖屏模式下，直播间中**Retry**按钮的背景色。 |


<span id="61f1657e"></span>
### setLandscapeRetryBtnCornerRadius

设置横屏模式下直播间**重试**按钮的圆角。

```java
public void setLandscapeRetryBtnCornerRadius(float btnCorner)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|btnCorner |Float |横屏模式下，直播间中**Retry**按钮的圆角。 |


<span id="031c6eb4"></span>
### setPortraitRetryBtnCornerRadius

设置竖屏模式下直播间**重试**按钮的圆角。

```java
public void setPortraitRetryBtnCornerRadius(float btnCorner)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|btnCorner |Float |竖屏模式下，直播间中**Retry**按钮的圆角。 |


<span id="e1e44fa2"></span>
### setNetErrorBtn

设置网络类型错误提示的按钮文本。

```java
public void setNetErrorBtn(String mNetErrorBut)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNetErrorBut |String |网络类型错误提示的按钮文本。 |


<span id="0e34b2ee"></span>
### setNonWIFIBtn

设置非WiFi状态下的按钮文本。

```java
public void setNonWIFIBtn(String mNonWIFIBut)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNonWIFIBut |String |非WiFi状态下的按钮文本。 |


<span id="4161f237"></span>
### setNetErrorText

设置网络类型错误提示的文本。

```java
public void setNetErrorText(String mNetErrorText)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNetErrorText |String |网络类型错误提示的文本。 |


<span id="bdd6dcee"></span>
### setNonWIFIText

设置非WiFi状态下的提示文本。

```java
public void setNonWIFIText(String mNonWIFIText)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNonWIFIText |String |非WiFi状态下的提示文本。 |


<span id="9dc535c9"></span>
### setNetWorkChangeTextColor

设置使用移动数据提示文本的颜色。

```java
public void setNetWorkChangeTextColor(int mNetWorkChangeTextColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNetWorkChangeTextColor |Integer |使用移动数据提示文本的颜色。默认颜色为白色。 |


<span id="f1bb9981"></span>
### setLoadingDrawable

设置横屏模式下直播间的加载图标。

```java
public void setLoadingDrawable(Drawable mLoadingDrawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLoadingDrawable |Drawable |横屏模式下，直播间的加载图标。 |


<span id="c55cac87"></span>
### setPorLoadingDrawable

设置竖屏模式下直播间的加载图标。

```java
public void setPorLoadingDrawable(Drawable mLoadingDrawable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLoadingDrawable |Drawable |竖屏模式下，直播间的加载图标。 |


<span id="14848730"></span>
### setLoadingDrawableSize

设置横屏模式下直播间加载图标的尺寸。

```java
public void setLoadingDrawableSize(int size)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|size |Integer |横屏模式下，直播间加载图标的尺寸。 |


<span id="e0017ed2"></span>
### setPorLoadingDrawableSize

设置竖屏模式下直播间加载图标的尺寸。

```java
public void setPorLoadingDrawableSize(int size)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|size |Integer |竖屏模式下，直播间加载图标的尺寸。 |


<span id="dfb9b61c"></span>
## 主播账号

<span id="b7619504"></span>
### setAccountImageSize

设置主播账号头像的尺寸。

```java
public void setAccountImageSize(int mAccountImageSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mAccountImageSize |Integer |主播账号的头像尺寸。 |


<span id="fb45e202"></span>
### setAccountViewColor

设置主播账号的背景色。

```java
public void setAccountViewColor(int mAccountViewColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mAccountViewColor |Integer |主播账号的背景色。 |


<span id="f44e96b4"></span>
### setAccountFontSize

设置主播账号的字体大小。

```java
public void setAccountFontSize(int mAccountFontSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mAccountFontSize |Integer |主播账号的字体大小。单位：sp。 |


<span id="59f6d2ac"></span>
### setAccountFontColor

设置主播账号的文字颜色。

```java
public void setAccountFontColor(int accountFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|accountFontColor |Integer |主播账号的文本颜色。 |


<span id="d5a89797"></span>
## 悬浮窗

悬浮窗即画中画（PiP）窗口。

<span id="17b259a9"></span>
### setOpenLiveFloatWindow

设置是否开启直播流悬浮窗，即是否支持以画中画模式显示直播视频。

```java
public void setOpenLiveFloatWindow(boolean mOpenFloatWindow)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mOpenFloatWindow |Boolean |是否开启直播流悬浮窗。默认值：`true`。可选值：<br><br><br>* `true`：开启。<br><br>* `false`：关闭。 |


<span id="afd1a6ca"></span>
### setOpenVodFloatWindow

设置是否启用 VOD 视频的悬浮窗，即是否支持在画中画模式下显示预告或回放。

```java
public void setOpenVodFloatWindow(boolean mOpenFloatWindow)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mOpenFloatWindow |Boolean |是否启用点播视频的悬浮窗。默认值：`true`。可选值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |


<span id="ef659165"></span>
### setFloatWindowBorderWidth

设置悬浮窗的边框宽度。

```java
public void setFloatWindowBorderWidth(int mFloatWindowBorderWidth)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatWindowBorderWidth |Integer |悬浮窗的边框宽度。该值不能为负数。单位：dp。 |


<span id="1aef7bd9"></span>
### setFloatWindowBorderColor

设置悬浮窗的边框颜色。

```java
public void setFloatWindowBorderColor(int mFloatWindowBorderColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatWindowBorderColor |Integer |悬浮窗的边框颜色。 |


<span id="1ef9f97b"></span>
### setFloatWindowExitBtn

设置悬浮窗的关闭图标。

```java
public void setFloatWindowExitBtn(Drawable mFloatWindowExitBtn)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatWindowExitBtn |Drawable |悬浮窗的关闭图标。 |


<span id="9a3a861e"></span>
### setFloatWindowCorner

设置悬浮窗的圆角。

```java
public void setFloatWindowCorner(float mFloatWindowCorner)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatWindowCorner |Float |悬浮窗的圆角。 |


<span id="644b100e"></span>
### setFloatViewActionListener

设置悬浮窗或其关闭图标的点击事件监听器。设置后，SDK 会在观众点击悬浮窗或其关闭图标时通知 `FloatViewActionListener`，但不会执行默认的点击行为。回调信息请参见 [FloatViewActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#379862a5)。

```java
public void setFloatViewActionListener(FloatViewActionListener floatViewActionListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatViewActionListener |FloatViewActionListener |悬浮窗或其关闭图标的点击事件监听器。 |


<span id="f8150cf4"></span>
### setPauseOnLockScreenInMiniWindow

设置画中画窗口在屏幕锁定时是否暂停播放视频。

```Java
public void setPauseOnLockScreenInMiniWindow(boolean pauseOnLockScreenInMiniWindow)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|pauseOnLockScreenInMiniWindow |boolean |当锁屏时，画中画窗口是否暂停播放视频。默认值为`false`。可选值：<br><br><br>* `true`：暂停播放视频。<br><br>* `false`：继续播放视频。 |


<span id="dab5088d"></span>
## 多语言

<span id="e3daaa52"></span>
### setLanguageType

设置所需的语言类型。默认支持所有语言（简体中文、繁体中文、英文和日文）。仅适用于以下自定义文本。要设置观看页的语言，请调用 [setPreferLanguage](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#0fee5955) 方法。


* 评论间隔提醒文本

* 回放按钮文本

* 在直播间使用移动数据的提示文本

* 网络类型断开按钮文本

* 网络类型断开提示文本


```java
public void setLanguageType(LanguageManager.LANGUAGE[] mLanguageType)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLanguageType |LanguageManager.LANGUAGE[] |所需的语言类型。 |


要在直播间实现多语言自定义文本，需先传入所需语言类型的数组，然后按数组索引顺序用“|”分隔自定义文本。以下示例代码自定义了回放按钮的文本。

```java
LanguageManager.LANGUAGE[] mLanguageType = {LanguageManager.LANGUAGE.ZH_HANS, LanguageManager.LANGUAGE.EN
        , LanguageManager.LANGUAGE.JA, LanguageManager.LANGUAGE.ZH_HANT};
        
settings.setLanguageType(mLanguageType);

settings.setReplayTipText("重新观看|Watch again|もう一度見る|重新觀看");
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 1.52.1 版本起，该方法不再支持。</div>


<span id="9b8a2dce"></span>
### setMultiLanguageIcon

设置切换语言的图标。

```java
public void setMultiLanguageIcon(Drawable mMultiLanguageIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mMultiLanguageIcon |Drawable |切换语言的图标。 |


<span id="f7139b44"></span>
### setLanguageListener

设置切换语言的监听器。回调信息请参见 [LanguageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#76956141)。

```java
public void setLanguageListener(LanguageListener mLanguageListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLanguageListener |LanguageListener |切换语言的监听器。 |


<span id="0fee5955"></span>
### setPreferLanguage

设置观看页的首选语言。

```java
public void setPreferLanguage(LanguageManager.LANGUAGE mPreferLanguage)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPreferLanguage |LanguageManager.LANGUAGE |观看页的首选语言。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅对 BytePlus Live 控制台已开启的语言生效。</div><br> |


<span id="c37c04d4"></span>
## 商品卡片

<span id="b4177ecc"></span>
### setShowGoodsCount

设置是否显示商品卡片的总数。

```java
public void setShowGoodsCount(boolean mShowGoodsCount)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mShowGoodsCount |Boolean |是否展示商品卡片的总数。可选值：<br><br><br>* `true`：展示。<br><br>* `false`：不展示。 |


<span id="f13496d0"></span>
### setShoppingCardIcon

设置直播间展示的购物车图标。

```java
public void setShoppingCardIcon(Drawable shoppingCardIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardIcon |Drawable |在直播间展示的购物车图标。 |


<span id="65eb7338"></span>
### setShopCardItemImageCorner

设置商品卡片项背景的圆角。

```java
public void setShopCardItemImageCorner(int mShopCardItemImageCorner)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mShopCardItemImageCorner |Integer |商品卡片项背景的圆角。 |


<span id="8a715680"></span>
### setShoppingCardDialogHeight

设置商品卡片弹窗的高度。

```java
public void setShoppingCardDialogHeight(int shoppingCardDialogHeight)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardDialogHeight |Integer |商品卡片弹窗的高度。该值不能为负数。默认情况下，高度为屏幕高度的 0.73 倍。单位：dp。 |


<span id="d2c8b7e7"></span>
### setShoppingCardDialogBackgroundColor

设置商品卡片弹窗的背景色。

```java
public void setShoppingCardDialogBackgroundColor(int shoppingCardDialogBackgroundColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardDialogBackgroundColor |Integer |商品卡片弹窗的背景颜色。 |


<span id="4112416e"></span>
### setShoppingCardTabFontStyle

设置商品卡片菜单栏的字体。

```java
public void setShoppingCardTabFontStyle(Typeface shoppingCardTabFontStyle)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardTabFontStyle |Typeface |商品卡片菜单栏的字体。 |


<span id="6c2bb529"></span>
### setShoppingCardTitleFontStyle

设置商品名称的字体。

```java
public void setShoppingCardTitleFontStyle(Typeface shoppingCardTitleFontStyle)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardTitleFontStyle |Typeface |商品名称的字体。 |


<span id="ee5486a7"></span>
### setShoppingCardTitleFontSize

设置商品名称的字体大小。

```java
public void setShoppingCardTitleFontSize(int shoppingCardTitleFontSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardTitleFontSize |Integer |商品名称的字体大小。单位：sp。 |


<span id="44b490a3"></span>
### setShoppingCardTitleFontColor

设置商品名称的字体颜色。

```java
public void setShoppingCardTitleFontColor(int shoppingCardTitleFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardTitleFontColor |Integer |商品名称的颜色。 |


<span id="9f848956"></span>
### setShoppingCardHighLightFontStyle

设置零售价的字体。

```java
public void setShoppingCardHighLightFontStyle(Typeface shoppingCardHighLightFontStyle)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardHighLightFontStyle |Typeface |刊例价的字体。 |


<span id="ab1031d9"></span>
### setShoppingCardHighLightFontSize

设置零售价的字体大小。

```java
public void setShoppingCardHighLightFontSize(int shoppingCardHighLightFontSize)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardHighLightFontSize |Integer |刊例价的字体大小。单位：sp。 |


<span id="18b68aa4"></span>
### setShoppingCardHighLightFontColor

设置零售价的字体颜色。

```java
public void setShoppingCardHighLightFontColor(int shoppingCardHighLightFontColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardHighLightFontColor |Integer |刊例价的颜色。 |


<span id="4a00b94d"></span>
### setProductOriginalPriceShowStrikethrough

设置是否在刊例价上显示删除线。

```Java
public void setProductOriginalPriceShowStrikethrough(boolean productOriginalPriceShowStrikethrough)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|productOriginalPriceShowStrikethrough |Boolean |是否在刊例价上显示删除线。默认值：`false`。可选值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="78f83141"></span>
### setShoppingCardBackgroundColor

设置商品卡片的背景色。

```java
public void setShoppingCardBackgroundColor(int shoppingCardBackgroundColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shoppingCardBackgroundColor |Integer |商品卡片的背景颜色。 |


<span id="e7f49df1"></span>
### setEnableDirectUrl

设置是否启用商品的直达链接。

```java
public void setEnableDirectUrl(boolean mEnableDirectUrl) {
    this.mEnableDirectUrl = mEnableDirectUrl;
}
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mEnableDirectUrl |Boolean |是否启用商品的直达链接。可选值：<br><br><br>* `true`：若在 BytePlus Live 控制台配置了直达链接，则优先使用直达链接。<br><br>* `false`：使用商品链接。 |


<span id="5b643189"></span>
## 商品浮窗

商品浮窗是以悬浮图标形式展示的商品卡片。

<span id="b6d0c80f"></span>
### setFloatingShoppingCardBuyBtn

设置商品浮窗的按钮。

```java
public void setFloatingShoppingCardBuyBtn(Drawable floatingShoppingCardBuyBtn)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatingShoppingCardBuyBtn |Drawable |商品浮窗的按钮。 |


<span id="191d8368"></span>
### setFloatingShopCardBtnText

设置商品浮窗按钮的文本。

```typescript
public void setFloatingShopCardBtnText(String mFloatingShopCardBtnText)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatingShopCardBtnText |String |商品浮窗的按钮文本。默认情况下，使用 BytePlus Live 控制台配置的商品刊例价。如设置，则使用参数值。 |


<span id="9f41e9e3"></span>
### setFloatingShoppingCardLayoutParams

设置商品浮窗的默认位置。

```Java
public void setFloatingShoppingCardLayoutParams(SimpleLayoutParams floatingShoppingCardLayoutParams)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatingShoppingCardLayoutParams |SimpleLayoutParams |商品浮窗的默认位置。有关配置详情，请参见[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e4a2c940)。 |


<span id="f9c4dc83"></span>
### setFloatShoppingCardMovable

设置是否允许观众拖动商品浮窗。

```Java
public void setFloatShoppingCardMovable(boolean FloatShoppingCardMovable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|FloatShoppingCardMovable |Boolean |是否允许观众拖动商品浮窗。默认值：`false`。有效值：<br><br><br>* `true`：允许。<br><br>* `false`：不允许。 |


<span id="3c19c5d6"></span>
### setFloatShopCardCorner

设置商品浮窗的外部圆角。

```java
public void setFloatShopCardCorner(int mFloatShopCardCorner)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatShopCardCorner |Integer |商品浮窗的外部圆角。内部图片的圆角会自动适配外部圆角。 |


<span id="1b9eeb2d"></span>
### setEnableFloatShopCardView

设置是否在直播间显示商品浮窗。

```Java
public void setEnableFloatShopCardView(boolean enableFloatShopCardView) {
    this.enableFloatShopCardView = enableFloatShopCardView;
}
```


**参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|enableFloatShopCardView |Boolean |是否允许显示商品浮窗。默认值：`true`。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="fe186922"></span>
## 直播间中的URL跳转


* 默认情况下，SDK会在观众点击菜单下的商品卡片、商品浮窗、主播账号的头像或名称、页头广告、页中广告、浮标广告或评论区URL后，将观众跳转到WebView或外部浏览器。如需实现自定义跳转，可以调用[setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#be1306ce)监听点击事件，并根据检测到的点击事件实现自定义跳转。

* 如果以自定义模式登录直播间的观众在评论区点击用户昵称，SDK不会有默认跳转行为。必须调用[setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#be1306ce)监听点击事件，并根据检测到的点击事件实现自定义跳转。


<span id="be1306ce"></span>
### setRedirectPageListener

设置直播间内链接的点击事件监听器。设置后，观众点击上述链接时，SDK会触发相应的点击事件。需要根据点击事件实现自定义跳转。

```java
public void setRedirectPageListener(RedirectPageListener mRedirectPageListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mRedirectPageListener |[RedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#f163f66b) |直播间内链接的点击事件监听器。 |


**示例代码**

```Java
CustomSettings.Holder.mSettings.setRedirectPageListener(new RedirectPageListener() {
    /*****@paramliveActivity 直播间的Activity。*@paramredirectInfo 跳转所需的信息。*@return是否拦截SDK的默认跳转行为。true：拦截。SDK不再执行默认跳转行为。false：不拦截。SDK继续执行默认跳转行为。*/
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
                    
                    // Display the SDK's internal WebViewDialog.也可以使用自定义Dialog。
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
## 直播间状态

<span id="8d1bd70f"></span>
### setLiveRoomStatusListener

设置直播间状态监听器。回调信息请参见[LiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#1c2e9aff)。

```java
public void setLiveRoomStatusListener(LiveRoomStatusListener mLiveRoomStatusListener)
```



|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLiveRoomStatusListener |LiveRoomStatusListener |直播间状态监听器。 |


<span id="59235a7d"></span>
### setLiveRoomActionListener

设置完整直播间的退出事件监听器。设置后，观众点击退出按钮或实体返回键退出完整直播间时，SDK会通知`LiveRoomActionListener`点击事件，不执行默认点击行为。回调信息请参见[LiveRoomActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#1d31736d)。

```java
public void setLiveRoomActionListener(LiveRoomActionListener liveRoomActionListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|liveRoomActionListener |LiveRoomActionListener |完整直播间的退出事件监听器。 |


<span id="6ae57c28"></span>
## 抽奖

<span id="329545cb"></span>
### setFloatAwardListener

设置抽奖图标的监听器。回调信息请参见[FloatingAwardView.Listener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#f36aa242)。

```java
public void setFloatAwardListener(FloatingAwardView.Listener mFloatAwardListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mFloatAwardListener |FloatingAwardView.Listener |抽奖图标的监听器。 |


<span id="b0aec866"></span>
### setNeedFillAwardInfo

设置观众中奖后是否需要完善个人信息。

```java
public void setNeedFillAwardInfo(boolean mNeedFillAwardInfo)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNeedFillAwardInfo |Boolean |观众中奖后是否需要完善个人信息。默认值：`true`。有效值：<br><br><br>* `true`：观众需要完善个人信息。<br><br>* `false`：观众无需完善个人信息。 |


<span id="a247b2a2"></span>
## 互动工具

<span id="d680233d"></span>
### setFloatInteractToolLayoutParams

设置完整互动工具图标组的默认位置。完整互动工具图标组包含观看页上显示的所有互动工具图标。

```Java
public void setFloatInteractToolLayoutParams(SimpleLayoutParams floatInteractToolLayoutParams)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|floatInteractToolLayoutParams |SimpleLayoutParams |完整互动工具图标的默认位置。有关配置详情，请参见[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e4a2c940)。 |


<span id="3d641a87"></span>
### setFloatInteractToolMovable

设置是否允许观众拖动完整互动工具图标组。完整互动工具图标组包含观看页上显示的所有互动工具图标。

```Java
public void setFloatInteractToolMovable(boolean FloatInteractToolMovable)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|FloatInteractToolMovable |Boolean |是否允许观众拖动完整互动工具图标。默认值：`true`。有效值：<br><br><br>* `true`：允许。<br><br>* `false`：不允许。 |


<span id="d49d3e3f"></span>
### setVotePeopleCountVisible

设置是否显示参与投票的观众人数。

```Java
public void setVotePeopleCountVisible(boolean visible)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|visible |Boolean |是否显示参与投票的观众人数。默认值：`true`。有效值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="dcf1c092"></span>
## 其他

<span id="360e675a"></span>
### setPortraitExitIconPosition

设置直播间竖屏模式下退出图标的位置。

```java
public void setPortraitExitIconPosition(boolean mPortraitExitIconPosition)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPortraitExitIconPosition |Boolean |竖屏模式下直播间退出图标的位置。<br><br><br>* `true`：直播间右侧。<br><br>* `false`：直播间左侧。 |


<span id="6c8a8268"></span>
### setLandScapeExitIconPosition

设置直播间横屏模式下退出图标的位置。

```java
public void setLandScapeExitIconPosition(boolean mLandScapeExitIconPosition)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mLandScapeExitIconPosition |Boolean |横屏模式下直播间退出图标的位置。<br><br><br>* `true`：直播间右侧。<br><br>* `false`：直播间左侧。 |


<span id="313cdccf"></span>
### setCommentLinkToWebView

设置观众点击链接后内容是否在当前直播间页面显示。

```java
public void setCommentLinkToWebView(boolean mCommentLinkToWebView)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mCommentLinkToWebView |Boolean |观众点击链接后内容是否在当前直播间页面显示。有效值：<br><br><br>* `true`：在当前直播间页面显示。<br><br>* `false`：在新页面显示。 |


<span id="7ba2e7be"></span>
### setExitRoomIcon

设置直播间退出图标。

```java
public void setExitRoomIcon(Drawable exitRoomIcon)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|exitRoomIcon |Drawable |退出直播间的图标。 |


<span id="6f30af5f"></span>
### setPageBackGroundColor

设置直播间的背景色。

```java
public void setPageBackGroundColor(int mPageBackGroundColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mPageBackGroundColor |Integer |直播间的背景色。 |


<span id="9565823b"></span>
### setTransitionPage

设置直播间竖屏模式下的加载页。建议使用黑色背景的图片。

```java
public void setTransitionPage(Drawable transitionPage)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|transitionPage |Drawable |竖屏模式下直播间的加载页。 |


<span id="ad65c19c"></span>
### setCustomLoginListener

在认证模式为公开时，设置登录自有账号系统的监听器。有关回调信息，请参见[CustomLoginListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#75007939)。

```java
public void setCustomLoginListener(CustomLoginListener mCustomLoginListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mCustomLoginListener |CustomLoginListener |当认证模式为公开时，用于登录自有账号系统的监听器。 |


<span id="4bec9c3c"></span>
### setBookSuccessText

设置直播流预约成功时的提示文本。

```java
public void setBookSuccessText(String bookSuccessText)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|bookSuccessText |String |直播流预约成功的提示文本。 |


<span id="70e35b57"></span>
### setBookFailText

设置直播流预约失败时的提示文本。

```java
public void setBookFailText(String bookFailText)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|bookFailText |String |直播流预约失败的提示文本。 |


<span id="af612d85"></span>
### setActivityBottomNavBarColor

设置直播间显示时系统底部导航栏的背景颜色。

```Java
public void setActivityBottomNavBarColor(int activityBottomNavBarColor)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityBottomNavBarColor |Integer |直播间展示时系统底部导航栏的背景色。默认颜色为纯黑（`#000000`）。 |


<span id="7b592acf"></span>
### setShareListener

设置在完整直播间点击分享图标的监听器。设置后，SDK 在观众点击完整直播间的分享图标时，会通知`ShareListener`监听器该点击事件，并不会执行默认点击行为。有关回调信息，请参见[ShareListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#2a6e0df9)。

```Java
public void setShareListener(ShareListener shareListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shareListener |[ShareListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#2a6e0df9) |完整直播间中点击分享图标的监听器。 |


<span id="278b0202"></span>
### setPortraitRoomClearScreenEnable

设置是否启用竖屏模式下直播间的清屏功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">清屏功能仅支持竖屏模式下的直播间。</div>


```Java
public void setPortraitRoomClearScreenEnable(boolean portraitRoomClearScreenEnable)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|portraitRoomClearScreenEnable |Boolean |是否启用竖屏模式下直播间的清屏功能。默认值：`true`。有效值：<br><br><br>* `true`：启用。观众可通过右滑或点击更多图标（...）\> **清屏**来清屏。<br><br>* `false`：禁用。 |


<span id="28b8fb22"></span>
### setShowCloseButtonWhenClearingScreen

设置清屏时是否显示关闭直播间的图标。

```Java
public void setShowCloseButtonWhenClearingScreen(boolean showCloseButtonWhenClearingScreen)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|showCloseButtonWhenClearingScreen |Boolean |清屏过程中是否显示关闭直播间的图标。默认值：`false`。有效值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="ba44eae4"></span>
### setShowRetryPageWhenJoinRoomFail

设置完整直播间页面初始化失败时是否显示重试页面。

```Java
public void setShowRetryPageWhenJoinRoomFail(boolean showRetryPageWhenJoinRoomFail)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|showRetryPageWhenJoinRoomFail |Boolean |完整直播间页面初始化失败时是否显示重试页。默认值：`true`。有效值：<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |


<span id="b29215e9"></span>
### setActivityBookListener

设置直播流预约的监听器。有关回调信息，请参见[ActivityBookListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#2d2129c0)。

```Java
public void setActivityBookListener(ActivityBookListener listener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|listener |ActivityBookListener |直播流预约的监听器。 |


<span id="d240e1b4"></span>
### setCustomLanguageStringListener

设置自定义系统文本的监听器。有关回调信息，请参见[CustomLanguageStringListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#c5d14099)。

```Java
public void setCustomLanguageStringListener(CustomLanguageStringListener mCustomLanguageStringListener) 
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mCustomLanguageStringListener |CustomLanguageStringListener |自定义系统文本的监听器。 |


**示例代码**

以下示例代码在观看页语言为英文时，将`key`为`more`的文本修改为`123`。

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

在认证模式为公开时，设置观众进入直播间的默认昵称。

```Java
public void setPublicCommentNickName(String publicRegisterNickName, PublicNickNameRegisterListener nameRegisterListener)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|publicRegisterNickName |String |昵称。若为空，则不执行任何操作。 |
|nameRegisterListener |PublicNickNameRegisterListener |直播间认证模式为公开时，昵称注册结果的回调类。该参数可为 null。更多信息请参见 [PublicNickNameRegisterListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#192a9ac2)。 |


<span id="9fa8eed2"></span>
### setShowPortraitRoomTopShadow

设置竖屏模式下直播间顶部是否显示渐变遮罩。

```Java
public void setShowPortraitRoomTopShadow(boolean showPortraitRoomTopShadow)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|showPortraitRoomTopShadow |Boolean |竖屏模式下是否在直播间顶部显示渐变遮罩。默认值：`true`。有效值：<br><br><br>* `true`：显示。若视频背景为白色，显示渐变遮罩可提升直播间顶部白色文本的可见性。<br><br>* `false`：不显示。 |


<span id="543e5973"></span>
### setBdlExternalReportConfiguration

设置数据上报配置

```Java
public void setBdlExternalReportConfiguration(BDLExternalReportConfiguration bdlExternalReportConfiguration)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|bdlExternalReportConfiguration |BDLExternalReportConfiguration |数据上报配置。更多信息请参见 [BDLExternalReportConfiguration](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#446d9b7a)。 |
