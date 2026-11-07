---
title: "mSettings"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings-zh-TW"
---

本主題說明各種自訂方法。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">SDK自訂設定優先於在BytePlus Live主控台或透過呼叫伺服器端OpenAPI所設定的自訂配置。例如，若同時使用SDK的<code>setThumbIcon</code>方法與BytePlus Live主控台自訂直播間按讚圖示，則觀看頁面會顯示由<code>setThumbIcon</code>方法自訂的圖示。</div>


* <div data-tips="true" data-tips-type="tip">本主題中的所有方法必須在觀眾進入直播間前呼叫。</div>



<span id="c84ea727"></span>
## 播放器

<span id="14c1fc92"></span>
### setPlayerLayoutMode

設定橫屏直播間的影片縮放模式。

```java
public void setPlayerLayoutMode(int playerLayoutMode)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|playerLayoutMode |整數 |橫式直播間的影片縮放模式。預設值：`0`。<br><br><br>* `0`：`ImageAspectFit`。填滿播放器並保持影片的長寬比。影片的寬度或高度會填滿播放器的寬度或高度。若影片長寬比與播放器不同，影片會縮放以適應，且不會裁切內容。<br><br>* `1`：`ImageToFill`。以影片填滿播放器。影片的長寬比可能會被改變。<br><br>* `2`：`ImageAspectFill`。填滿播放器並保持影片的長寬比。影片的寬度填滿播放器的寬度，影片的高度填滿播放器的高度。若影片長寬比與播放器不同，影片會裁切以適應。 |


<span id="bcd1844b"></span>
### setPortraitPlayerLayoutMode

設定直屏直播間的影片縮放模式。

```java
public void setPortraitPlayerLayoutMode(int playerLayoutMode)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|playerLayoutMode |整數 |直向模式下直播間的影片縮放模式。預設值：`2`。<br><br><br>* `0`：`ImageAspectFit`。填滿播放器並保持影片的長寬比。影片的寬度或高度會填滿播放器的寬度或高度。若影片的長寬比與播放器不同，影片會等比例縮放以適應，內容不會被裁切。<br><br>* `1`：`ImageToFill`。以影片填滿播放器。影片的長寬比可能會被改變。<br><br>* `2`：`ImageAspectFill`。填滿播放器並保持影片的長寬比。影片的寬度會填滿播放器的寬度，高度會填滿播放器的高度。若影片的長寬比與播放器不同，影片會被裁切以適應。 |


<span id="9b743f4d"></span>
### setPeopleCountFontStyle

設定人氣標籤文字的字型。

```java
public void setPeopleCountFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|typeface |Typeface |人氣標籤文字的字型。 |


<span id="d55a37d1"></span>
### setPeopleCountFontSize

設定人氣標籤文字的字體大小。

```Java
public void setPeopleCountFontSize(int peopleCountFontSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|peopleCountFontSiz |Integer |人氣標籤文字的字體大小。單位：sp。 |


<span id="08753ee9"></span>
### setPeopleCountTextColor

設定人氣標籤文字的顏色。

```Java
public void setPeopleCountTextColor(int peopleCountTextColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|peopleCountTextColor |Integer |人氣標籤文字的顏色。 |


<span id="351984cc"></span>
### setPeopleCountIconDrawable

設定人氣圖示。

```java
public void setPeopleCountIconDrawable(Drawable drawable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|drawable |Drawable |人氣圖示。 |


<span id="3fecc7b5"></span>
### setPlayerThemeColor

設定播放器主題色，即倍速按鈕、進度條及解析度按鈕的顏色。

```java
public void setPlayerThemeColor(int playerThemeColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|playerThemeColor |Integer |播放器主題色，即倍速按鈕、進度條和畫質按鈕的顏色。 |


<span id="45fcf8aa"></span>
### setRoomStatusTextTipFontSize

設定直播間狀態文字的字體大小。

```java
public void setRoomStatusTextTipFontSize(int roomStatusTextTipFontSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|roomStatusTextTipFontSize |Integer |直播間狀態文字的字體大小。單位：sp。 |


<span id="a38c2a91"></span>
### setRoomStatusTextTipCenterOffset

設定直播間狀態文字相對於播放器中心的垂直偏移量。

```java
public void setRoomStatusTextTipCenterOffset(int roomStatusTextTipCenterOffset)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|roomStatusTextTipCenterOffset |Integer |直播間狀態文字相對於播放器中心的垂直偏移量。單位：dp。 |


<span id="0e07387a"></span>
### setRoomStatusTextTipRadius

設定直播間狀態文字背景的圓角。

```java
public void setRoomStatusTextTipRadius(int roomStatusTextTipRadius)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|roomStatusTextTipRadius |Integer |直播間狀態文字背景的圓角。單位：dp。 |


<span id="3aaaec13"></span>
### setRoomStatusTextTipHorizontalPadding

設定直播間狀態文字的水平邊距。

```java
public void setRoomStatusTextTipHorizontalPadding(int roomStatusTextTipHorizontalPadding)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|roomStatusTextTipHorizontalPadding |Integer |直播間狀態文字的水平內邊距。此值不可為負數。單位：dp。 |


<span id="eb9159a4"></span>
### setRoomStatusTextTipVerticalPadding

設定直播間狀態文字的垂直邊距。

```java
public void setRoomStatusTextTipVerticalPadding(int roomStatusTextTipVerticalPadding)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|roomStatusTextTipVerticalPadding |Integer |直播間狀態文字的垂直內邊距。此值不可為負數。單位：dp。 |


<span id="3da839f7"></span>
### setPlayerTimeColor

設定隨選視訊（VOD）影片的時間顏色。

```java
public void setPlayerTimeColor(int playerTimeColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|playerTimeColor |Integer |點播影片的時間顏色。 |


<span id="de7e091f"></span>
### setFullScreenIcon

設定全螢幕圖示。

```java
public void setFullScreenIcon(Drawable fullScreenIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|fullScreenIcon |Drawable |全螢幕圖示。 |


<span id="c53da99c"></span>
### setSmallScreenIcon

設定退出全螢幕圖示。

```java
public void setSmallScreenIcon(Drawable smallScreenIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|smallScreenIcon |Drawable |退出全螢幕圖示。 |


<span id="10d1e9a9"></span>
### setLiveRefreshIcon

設定播放器左下角於**Live**狀態時顯示的刷新圖示。

```java
public void setLiveRefreshIcon(Drawable liveRefreshIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|liveRefreshIcon |Drawable |在**Live**狀態下，播放器左下角顯示的刷新圖示。 |


<span id="fea0b7ee"></span>
### setPlayerStartIcon

設定播放器左下角顯示的播放圖示。

```java
public void setPlayerStartIcon(Drawable playerStartIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|playerStartIcon |Drawable |播放器左下角顯示的播放圖示。 |


<span id="741fd598"></span>
### setPlayerPauseIcon

設定播放器左下角顯示的暫停圖示。

```java
public void setPlayerPauseIcon(Drawable playerPauseIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|playerPauseIcon |Drawable |播放器左下角顯示的暫停圖示。 |


<span id="b9f9855e"></span>
### setPlayerPausedCenterIcon

設定播放器中央顯示的暫停狀態圖示。

```java
public void setPlayerPausedCenterIcon(Drawable playerPausedCenterIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|playerPausedCenterIcon |Drawable |播放器中央顯示的暫停狀態圖示。 |


<span id="4c0db46f"></span>
### setCustomLiveName

設定直播間名稱。

```java
public void setCustomLiveName(String customLiveName)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|customLiveName |String |直播間名稱。設定後，傳入的名稱將優先使用。若傳入空字串，則名稱將隱藏。 |


<span id="f1b19520"></span>
### setSpeedSettingDialogAutoClose

設定觀眾選擇倍速時，倍速選擇對話框是否自動關閉。

```java
public void setSpeedSettingDialogAutoClose(boolean speedSettingDialogAutoClose)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|speedSettingDialogAutoClose |Boolean |觀眾選擇倍速時，倍速選擇對話框是否自動關閉。預設值：`false`。<br><br><br>* `true`：自動關閉。<br><br>* `false`：不自動關閉。 |


<span id="d34e9355"></span>
### setResolutionSettingDialogAutoClose

設定觀眾選擇解析度時，解析度選擇對話框是否自動關閉。

```java
public void setResolutionSettingDialogAutoClose(boolean resolutionSettingDialogAutoClose)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|resolutionSettingDialogAutoClose |Boolean |觀眾選擇畫質時，畫質選擇對話框是否自動關閉。預設值：`false`。<br><br><br>* `true`：自動關閉。<br><br>* `false`：不自動關閉。 |


<span id="1df9583d"></span>
### setSimpleControlBar

設定橫屏直播間是否啟用簡易控制列。簡易控制列不包含倍速及解析度選擇按鈕。

```java
public void setSimpleControlBar(boolean mSimpleControlBar)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mSimpleControlBar |Boolean |是否啟用橫屏直播間的簡易控制條。<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |


<span id="958af3e1"></span>
### setReplayTipText

設定回放重播按鈕的文字。

```java
public void setReplayTipText(String mReplayTipText)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mReplayTipText |String |回放重播按鈕的文字。 |


<span id="f77abe2b"></span>
### setLiveAutoPlay

設定是否自動播放直播影片。

```java
public void setLiveAutoPlay(boolean mLiveAutoPlay)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mLiveAutoPlay |Boolean |是否自動播放直播視頻。<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |


<span id="102e91a5"></span>
### setPlayBackAutoPlay

設定橫屏直播間是否自動播放回放。

```java
public void setPlayBackAutoPlay(boolean mPlayBackAutoPlay)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mPlayBackAutoPlay |Boolean |橫屏直播間下是否自動播放回放。<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |


<span id="a7710614"></span>
### setPortraitPlayBackAutoPlay

設定直屏直播間是否自動播放回放。

```java
public void setPortraitPlayBackAutoPlay(boolean mPortraitPlayBackAutoPlay)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mPortraitPlayBackAutoPlay |Boolean |直屏直播間下是否自動播放回放。<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |


<span id="f630c72c"></span>
### setForceShowAutoPlay

設定橫屏直播間是否自動播放預覽。

```java
public void setForceShowAutoPlay(boolean mForceShowAutoPlay)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mForceShowAutoPlay |Boolean |橫屏直播間下是否自動播放預覽。<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |


<span id="28a79c72"></span>
### setPortraitForceShowAutoPlay

設定直屏直播間是否自動播放預覽。

```java
public void setPortraitForceShowAutoPlay(boolean mPortraitForceShowAutoPlay)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mPortraitForceShowAutoPlay |Boolean |直屏直播間下是否自動播放預覽。<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |


<span id="c0b34f9b"></span>
### setPlayBackLoop

設定橫屏直播間是否自動循環播放回放。

```java
public void setPlayBackLoop(boolean mIsPlayBackLoop)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mIsPlayBackLoop |Boolean |橫屏直播間下是否自動循環播放回放。<br><br><br>* `true`：自動循環播放。<br><br>* `false`：不自動循環播放。 |


<span id="311325a4"></span>
### setPortraitPlayBackLoop

設定直屏直播間是否自動循環播放回放。

```java
public void setPortraitPlayBackLoop(boolean mIsPortraitPlayBackLoop)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mIsPortraitPlayBackLoop |Boolean |直屏直播間下是否自動循環播放回放。<br><br><br>* `true`：自動循環播放。<br><br>* `false`：不自動循環播放。 |


<span id="2a2cd31c"></span>
### setForceShowLoop

設定橫屏直播間是否自動循環播放預覽。

```java
public void setForceShowLoop(boolean mIsForceShowLoop)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mIsForceShowLoop |Boolean |橫屏直播間下是否自動循環播放預覽。<br><br><br>* `true`：自動循環播放。<br><br>* `false`：不自動循環播放。 |


<span id="f32e4191"></span>
### setPortraitForceShowLoop

設定當直播間處於直式模式時，是否自動循環預覽。

```java
public void setPortraitForceShowLoop(boolean mIsPortraitForceShowLoop)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mIsPortraitForceShowLoop |Boolean |直屏直播間下是否自動循環播放預覽。<br><br><br>* `true`：自動循環播放。<br><br>* `false`：不自動循環播放。 |


<span id="937879b8"></span>
### setVodAutoContinuePlayback

設定是否啟用 VOD 視頻的自動斷點續播功能。

```java
public void setVodAutoContinuePlayback(boolean isVodAutoContinuePlayback)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|isVodAutoContinuePlayback |Boolean |是否啟用 VOD 視頻的自動斷點續播。預設值：`true`。<br><br><br>* `true`：啟用自動斷點續播。當觀眾退出並重新進入直播間時，VOD 視頻會自動從斷點繼續播放。<br><br>* `false`：停用自動斷點續播。 |


<span id="3884d8f7"></span>
### setVodAutoSeekTipTextVisible

設定 VOD 視頻自動斷點續播時是否顯示提示。

```java
public void setVodAutoSeekTipTextVisible(boolean mVodAutoSeekTipTextVisible)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mVodAutoSeekTipTextVisible |Boolean |VOD 視頻自動斷點續播時是否顯示提示。預設值：`true`。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="355c7e9b"></span>
### setVodAutoSeekTipTextSize

設定 VOD 視頻自動斷點續播提示的字體大小。

```java
public void setVodAutoSeekTipTextSize(float mVodAutoSeekTipTextSize)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mVodAutoSeekTipTextSize |float |VOD 視頻自動斷點續播提示的字體大小。預設值：`11`。單位：sp。 |


<span id="05c5b49f"></span>
### setEnterFullScreenEnable

設定觀眾是否可以進入全螢幕模式。

```Java
public void setEnterFullScreenEnable(boolean enterFullScreenEnable)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|enterFullScreenEnable |Boolean |觀眾是否可進入全螢幕模式。預設值：`true`。<br><br><br>* `true`：觀眾可進入全螢幕模式。播放器中會顯示全螢幕按鈕。當原始視頻流的寬度大於高度時，無論是直播還是 VOD 視頻，在直屏直播間或橫屏直播間都會顯示全螢幕按鈕。<br><br>* `false`：觀眾不可進入全螢幕模式。播放器中不顯示全螢幕按鈕。 |


<span id="1909af7e"></span>
### setNeedAutoDemote

設定直播過程中遇到網路延遲時，是否支援自動降級或提供提示。

```Java
public void setNeedAutoDemote(boolean needAutoDemote)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|needAutoDemote |Boolean |直播過程中出現網路卡頓時，是否支援自動降級或給出提示。預設值：`true`。<br><br><br>* `true`：<br><br>   * 若 [setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall) 參數值為 `true`，則會直接在主備流間切換。<br><br>   * 若 [setBackupDowngradeWhenStall](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setbackupdowngradewhenstall) 參數值為 `false`，在智慧模式下，會自動降級至較低解析度。若在最低解析度下仍發生卡頓，則切換主串流與備份串流。在非智慧模式下，會向觀眾提供提示，詢問是否切換至較低解析度，讓他們依需求選擇。若觀眾切換至最低解析度後仍發生卡頓，則切換主串流與備份串流。<br><br>* `false`：在智慧模式下，不會自動降級。在非智慧模式下，不會通知觀眾切換至較低解析度。 |


<span id="8c5dc53a"></span>
### setBackupDowngradeWhenStall

設定直播過程中發生卡頓時，是否直接切換主備流。

```Java
public void setBackupDowngradeWhenStall(boolean backupDowngradeWhenStall)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|backupDowngradeWhenStall |boolean |直播過程中發生卡頓時，是否直接切換主串流與備份串流。預設值：`false`。此方法僅在 [setNeedAutoDemote](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setneedautodemote) 參數值為 `true` 時生效。<br><br><br>* `true`：直接切換主串流與備份串流。<br><br>* `false`：在智慧模式下，自動降級至較低解析度。若在最低解析度下仍發生卡頓，則切換主串流與備份串流。在非智慧模式下，會向觀眾提供提示，詢問是否切換至較低解析度，讓他們依需求選擇。若觀眾切換至最低解析度後仍發生卡頓，則切換主串流與備份串流。 |


<span id="6fafa479"></span>
### setEnableShowPortraitRoomTopArea

設定直式直播間是否顯示整個頂部區域，包括右上角的關閉按鈕、主播帳號資訊、人氣數，以及多模式切換按鈕。

```Java
public void setEnableShowPortraitRoomTopArea(boolean enableShowPortraitRoomTopArea)
```


**參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|enableShowPortraitRoomTopArea |Boolean |是否顯示直式直播間的整個頂部區域。預設值：`true`。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="a208dfb2"></span>
### addChildViewInLinearLayout

在直播間指定位置插入自訂浮動 View。

```Java
public void addChildViewInLinearLayout(View childView, int location, boolean isLastChild, CustomSize customSize)
```


**參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|childView |View |要插入的自訂 View。 |
|location |int |指定插入位置。預設值：。<br><br><br>* `ADD_CHILD_VIEW_LEFT_TOP`：將 View 插入至左上角。<br><br>* `ADD_CHILD_VIEW_RIGHT_TOP`：將 View 插入至右上角。<br><br>* `ADD_CHILD_VIEW_RIGHT_BOTTOM`：將 View 插入至右下角。 |
|isLastChild |Boolean |目前的 View 是否為最後一個子 View。預設值：。<br><br><br>* `true`：此 View 為最後一個 View。<br><br>* `false`：此 View 不是最後一個 View。 |
|customSize |CustomSize |自訂 View 的尺寸。預設值：。 |


<span id="2d369486"></span>
## 選單

<span id="d0e012ac"></span>
### setMenuTabBackgroundDrawable

設定橫式直播間選單列的背景。

```java
public void setMenuTabBackgroundDrawable(Drawable drawable)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|drawable |Drawable |橫式直播間選單列的背景。 |


<span id="53ea42b5"></span>
### setMenuFontColor

設定選單列中選單項目被選取或未選取時的文字顏色。

```java
public void setMenuFontColor(new Pair<>(unSelectedColor,selectedColor))
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|unSelectedColor |Integer |橫式直播間選單列未選中選單項目的文字顏色。 |
|selectedColor |Integer |橫式直播間選單列選中選單項目的文字顏色。 |


<span id="b7289d01"></span>
### setMenuFontStyle

設定選單列的字體。

```java
public void setMenuFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |選單列的字型。 |


<span id="04b74c84"></span>
### setLandMenuFlowingTagColor

設定橫式直播間選單列中選取項目的指示顏色。

```java
public void setLandMenuFlowingTagColor(int landMenuFlowingTagColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|landMenuFlowingTagColor |Integer |橫式直播間選單列選中選單項目的指示器顏色。預設值：`0xFF3370FF`。 |


<span id="15c8126e"></span>
### setMenuDialogFlowingTagColor

設定直式直播間選單列中嵌入連結及圖文選單項目被選取時的指示顏色。

```Java
public void  setMenuDialogFlowingTagColor(int menuDialogFlowingTagColor) 
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|menuDialogFlowingTagColor |Integer |直式直播間嵌入連結及圖文選單列選中選單項目的指示器顏色。預設值：`0xFF161823`。 |


<span id="34aaada2"></span>
### setImageEmbeddedWebUrlsIcon

設定直式直播間嵌入連結選單的圖示。

```Java
public void setImageEmbeddedWebUrlsIcon(Drawable imageEmbeddedWebUrlsIcon)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|imageEmbeddedWebUrlsIcon |Drawable |直式直播間嵌入連結選單的圖示。 |


<span id="ea75f056"></span>
### setMenuDialogTabFontSize

設定嵌入連結及圖文選單標題的字體大小。

```Java
public void setMenuDialogTabFontSize(int menuDialogTabFontSize)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|menuDialogTabFontSize |Integer |嵌入連結及圖文選單標題的字型大小。單位：sp。 |


<span id="26a3e658"></span>
### setMenuDialogTabSelectedFontColor

設定嵌入連結及圖文選單標題被選取時的文字顏色。

```java
public void setMenuDialogTabSelectedFontColor(int menuDialogTabSelectedFontColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|menuDialogTabSelectedFontColor |Integer |嵌入式連結與圖形選單被選取時的標題文字顏色。預設值：`0xFF161823`。 |


<span id="6c07f026"></span>
### setMenuDialogTabUnSelectedFontColor

設定嵌入連結及圖文選單標題未選取時的文字顏色。

```java
public void setMenuDialogTabUnSelectedFontColor(int menuDialogTabUnSelectedFontColor) 
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|menuDialogTabUnSelectedFontColor |整數 |嵌入式連結與圖形選單未被選取時的標題文字顏色。預設值：`0xFF161823`。 |


<span id="6bc0db40"></span>
## 留言

<span id="fe61f617"></span>
### setNoCommentIconDrawable

設定留言區無留言時顯示的佔位圖示。

```java
public void setNoCommentIconDrawable(Drawable drawable)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|drawable |Drawable |評論區無評論時顯示的佔位圖示。 |


<span id="7a4995ea"></span>
### setCommentNicknameFontStyle

設定非主播暱稱的字體。

```java
public void setCommentNicknameFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |非主播暱稱的字體。 |


<span id="44c1830f"></span>
### setCommentNicknameFontColor

設定非主播暱稱的顏色。

```java
public void setCommentNicknameFontColor(int commentNicknameFontColor)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|commentNicknameFontColor |整數 |非主播暱稱的顏色。 |


<span id="2885642f"></span>
### setCommentNicknameFontSize

設定非主播暱稱的字體大小。

```Java
public void setCommentNicknameFontSize(int commentNicknameFontSize)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|commentNicknameFontSize |整數 |非主播暱稱的字體大小。單位：sp。 |


<span id="910f28cf"></span>
### setCommentContentFontColor

設定非主播留言內容的文字顏色。

```java
public void setCommentContentFontColor(int commentContentFontColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|commentContentFontColor |整數 |非主播評論的文字顏色。 |


<span id="d73603d2"></span>
### setCommentLinkColor

設定留言連結的顏色。

```java
public void setCommentLinkColor(int mCommentLinkColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mCommentLinkColor |整數 |評論連結的顏色。 |


<span id="4d6e871a"></span>
### setAudienceCommentLinkClickable

設定非主播留言中的連結是否可點擊。

```java
public void setAudienceCommentLinkClickable(boolean mAudienceCommentLinkClickable)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mAudienceCommentLinkClickable |布林值 |非主播評論中的連結是否可點擊。如需自訂觀眾點擊評論連結時的操作，請參見[setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#be1306ce)。<br><br><br>* `true`：可點擊。<br><br>* `false`：不可點擊。 |


<span id="7975da1e"></span>
### setCommentContentFontStyle

設定非主播留言內容的字體。

```java
public void setCommentContentFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |非主播評論的字體。 |


<span id="a6dabe5a"></span>
### setCommentContentFontSize

設定非主播留言內容的字體大小。

```Kotlin
public void setCommentContentFontSize(int commentContentFontSize)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|commentContentFontSize |整數 |非主播評論的字體大小。單位：sp。 |


<span id="032f1ab3"></span>
### setHostTagFontStyle

設定主播標籤的字體。

```java
public void setHostTagFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |主播標籤的字體。 |


<span id="3e4dfbf9"></span>
### setHostTagFontSize

設定主播標籤的字體大小。

```Java
public void setHostTagFontSize(int hostTagFontSize)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|hostTagFontSize |整數 |主播標籤的字體大小。單位：sp。 |


<span id="158d5023"></span>
### setTopCommentTagFontStyle

設定置頂標籤的字體。

```java
public void setTopCommentTagFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |置頂標籤的字體。 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自版本 1.51.0 起不再支援此方法。</div>


<span id="52954629"></span>
### setTopCommentFontStyle

設定置頂內容的字體。

```java
public void setTopCommentFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |置頂內容的字體。 |


<span id="262969ee"></span>
### setTopCommentFontColor

設定置頂內容的文字顏色。

```java
public void setTopCommentFontColor(int topCommentFontColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|topCommentFontColor |整數 |置頂內容的文字顏色。 |


<span id="261f08a4"></span>
### setTopCommentRowCount

設定置頂留言顯示的最大行數。

```java
public void setTopCommentRowCount(int count)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|count |整數 |置頂評論顯示的最大行數。預設值：`1`。 |


<span id="70a0fcb1"></span>
### setTopCommentDialogTitleAtStart

設定是否將置頂內容詳情對話框的標題顯示於最左側。

```java
public void setTopCommentDialogTitleAtStart(boolean mTopCommentDialogAtStart)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mTopCommentDialogAtStart |布林值 |置頂內容詳情對話框的標題是否顯示於最左側。<br><br><br>* `true`：於最左側。<br><br>* `false`：不在最左側。 |


<span id="4338c1b2"></span>
### setPortraitCommentAreaHeight

設定直式模式下直播間留言區的高度。

```java
public void setPortraitCommentAreaHeight(int mPortraitCommentAreaHeight)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mPortraitCommentAreaHeight |整數 |直式直播間評論區的高度。此值不可為負數。預設值：`194`。單位：dp。 |


<span id="748d2665"></span>
### setPortraitCommentLineCount

設定直式模式下直播間每則留言顯示的最大行數。

```java
public void setPortraitCommentLineCount(int mPortraitCommentLineCount)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mPortraitCommentLineCount |整數 |直式直播間每則評論顯示的最大行數。 |


<span id="a2aac31c"></span>
### setCommentEditViewHintTextColor

設定留言輸入框佔位文字的顏色。

```java
public void setCommentEditViewHintTextColor(int color)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|color |整數 |評論輸入框佔位文字的顏色。預設值：`0xB3FFFFFF` |


<span id="bab9d110"></span>
### setCommentEditViewTextColor

設定留言輸入框中輸入文字的顏色。

```java
public void setCommentEditViewTextColor(int mCommentEditViewTextColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mCommentEditViewTextColor |整數 |評論輸入框中輸入文字的顏色。預設值：`0xFF000000`。 |


<span id="425e8f28"></span>
### setCommentIntervalTip

設定留言間隔提示的內容。

```java
public void setCommentIntervalTip(String tip)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|tip |字串 |評論間隔提示的內容。 |


<span id="175601a7"></span>
### setCommentIntervalFontStyle

設定留言間隔提示內容的字型。

```java
public void setCommentIntervalFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|typeface |Typeface |評論間隔提示內容的字體。 |


<span id="2b82be95"></span>
### setCommentItemBgColor

設定歡迎訊息、進場訊息及非主持人留言的背景顏色。

```java
public void setCommentItemBgColor(int commentItemBgColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|commentItemBgColor |整數 |歡迎訊息、進入訊息及非主播評論的背景顏色。預設值：`#33000000`。 |


<span id="ff6e1afe"></span>
### setPullCommentCount

設定每次拉取的留言數量。

```java
public void setPullCommentCount(int count)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|count |整數 |每次拉取的評論數量。 |


<span id="ad021546"></span>
### setPullHistoryCommentTotalCount

設定可拉取的歷史留言總數。

```java
public void setPullHistoryCommentTotalCount(int count)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|count |整數 |可拉取的歷史評論總數。 |


<span id="075b7249"></span>
### setThumbIcon

設定直播間按讚的圖示。

```java
public void setThumbIcon(Drawable drawable)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|drawable |Drawable |直播間點讚圖示。 |


<span id="40624408"></span>
### setJoinRoomMsgNicknameColor

設定直播間進場訊息中暱稱的文字顏色。

```java
public void setJoinRoomMsgNicknameColor(int mJoinRoomMsgNicknameColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mJoinRoomMsgNicknameColor |整數 |直播間進入訊息中暱稱的文字顏色。 |


<span id="5488ff75"></span>
### setJoinRoomMsgContentColor

設定直播間進場訊息內容的文字顏色。

```java
public void setJoinRoomMsgContentColor(int mJoinRoomMsgContentColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mJoinRoomMsgContentColor |整數 |直播間進入訊息內容的文字顏色。 |


<span id="b006f58b"></span>
### setWelcomeMsgFontColor

設定直播間歡迎訊息的文字顏色。

```java
public void setWelcomeMsgFontColor(int mWelcomeMsgFontColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mWelcomeMsgFontColor |整數 |直播間歡迎訊息的文字顏色 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 1.53.0 版本起不再支援此方法。請改用 <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setsystemcommentcolor">setSystemCommentColor</a> 方法。</div>


<span id="c5541059"></span>
### setLandscapeCommentShouldShowAvatar

設定橫式模式下直播間留言區是否顯示用戶頭像。

呼叫 [setHostDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#3dc09158) 設定主持人預設頭像，並呼叫 [setCommentDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#a8949de3) 設定非主持人預設頭像。自訂模式（當 `roomAuthMode` 為 CUSTOM）下，可呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) 傳入指定用戶的頭像網址。

```java
public void setLandscapeCommentShouldShowAvatar(boolean landscapeCommentShouldShowAvatar)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|landscapeCommentShouldShowAvatar |布林值 |橫屏模式下，是否在直播間評論區顯示用戶頭像。預設值：`true`。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="f68ed0e2"></span>
### setPortraitCommentShouldShowAvatar

設定直式模式下直播間留言區是否顯示用戶頭像。

呼叫 [setHostDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#3dc09158) 設定主持人預設頭像，並呼叫 [setCommentDefaultAvatar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#a8949de3) 設定非主持人預設頭像。自訂模式（當 `roomAuthMode` 為 CUSTOM）下，可呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) 傳入指定用戶的頭像網址。

```java
public void setPortraitCommentShouldShowAvatar(boolean portraitCommentShouldShowAvatar)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|portraitCommentShouldShowAvatar |布林值 |直屏模式下，是否在直播間評論區顯示用戶頭像。預設值：`false`。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="3dc09158"></span>
### setHostDefaultAvatar

設定留言區主持人的預設頭像。

```java
public void setHostDefaultAvatar(Drawable hostDefaultAvatar)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|hostDefaultAvatar |Drawable |評論區中主播的預設頭像。 |


<span id="a8949de3"></span>
### setCommentDefaultAvatar

設定留言區非主持人的預設頭像。設定後，此頭像將顯示於每則非主持人留言前方。

```java
public void setCommentDefaultAvatar(Drawable commentDefaultAvatar)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|commentDefaultAvatar |Drawable |評論區中非主播的預設頭像。 |


<span id="3c5e004d"></span>
### setThumbFloatingDrawableListener

設定觀眾按讚直播間後顯示的浮動動畫圖示監聽器。回調資訊請參見 [ITVUMultipleDrawableListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#7929f65e)。

```java
public void setThumbFloatingDrawableListener(ITVUMultipleDrawableListener listener)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|listener |ITVUMultipleDrawableListener |觀眾點讚直播間後顯示的浮動動畫圖示監聽器。 |


<span id="3822d4b1"></span>
### setHostCommentColor

設定主持人留言的文字顏色。

```Java
public void setHostCommentColor(int hostCommentColor)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|hostCommentColor |整數 |主播評論的文字顏色。 |


<span id="ac731a87"></span>
### setHostCommentBackgroundColor

設定主持人留言的背景顏色。

```Java
public void setHostCommentBackgroundColor(int hostCommentBackgroundColor)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|hostCommentBackgroundColor |整數 |主播評論的背景顏色。 |


<span id="9169ea51"></span>
### setHostTagFontColor

設定主持人標籤的顏色。

```Java
public void setHostTagFontColor(int hostTagFontColor) 
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|hostTagFontColor |整數 |主播標籤的顏色。 |


<span id="f7ccfd88"></span>
### setHostCommentFontSize

設定主持人留言的字型大小。

```Java
public void setHostCommentFontSize(int mHostCommentFontSize)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|mHostCommentFontSize |整數 |主播評論的字體大小。單位：sp。 |


<span id="68c26a6c"></span>
### setHostCommentFontStyle

設定主持人留言的字型。

```Java
public void setHostCommentFontStyle(Typeface hostCommentFontStyle)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|hostCommentFontStyle |Typeface |主播評論的字體樣式。 |


<span id="c30d44f3"></span>
### setSystemCommentTagFontStyle

設定直式模式下直播間描述標籤及歡迎訊息標籤的字型。

```Java
public void setSystemCommentTagFontStyle(Typeface systemCommentTagFontStyle)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|systemCommentTagFontStyle |Typeface |直屏模式下直播間描述與歡迎訊息標籤的字體樣式。 |


<span id="1de92ebe"></span>
### setSystemCommentTagFontSize

設定直式模式下直播間描述標籤及歡迎訊息標籤的字型大小。

```Java
public void setSystemCommentTagFontSize(int systemCommentTagFontSize
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|systemCommentTagFontSize |整數 |直屏模式下直播間描述與歡迎訊息標籤的字體大小。單位：sp。 |


<span id="d5b319a2"></span>
### setSystemCommentTagFontColor

設定直式模式下直播間描述標籤及歡迎訊息標籤的顏色。

```Java
public void setSystemCommentTagFontColor(int systemCommentTagFontColor)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|systemCommentTagFontColor |整數 |直屏模式下直播間描述與歡迎訊息標籤的顏色。 |


<span id="06ae9e64"></span>
### setSystemCommentFontStyle

設定直式模式下直播間描述與歡迎訊息的主體字型。

```Java
public void setSystemCommentFontStyle(Typeface systemCommentFontStyle)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|systemCommentFontStyle |Typeface |直屏模式下直播間描述與歡迎訊息主體的字體樣式。 |


<span id="599c655a"></span>
### setSystemCommentFontSize

設定直式模式下直播間描述與歡迎訊息的主體字體大小。

```Java
public void setSystemCommentFontSize(int systemCommentFontSize)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|systemCommentFontSize |整數 |直屏模式下直播間描述與歡迎訊息主體的字體大小。單位：sp。 |


<span id="c7606a4c"></span>
### setSystemCommentColor

設定直式模式下直播間描述與歡迎訊息的主體文字顏色。

```Java
public void setSystemCommentColor(int systemCommentColor)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|systemCommentColor |整數 |直屏模式下直播間描述與歡迎訊息主體的文字顏色。 |


<span id="931a0bba"></span>
### setCommentItemSpacing

設定相鄰評論之間的間距。

```Java
public void setCommentItemSpacing(int mDistanceBetweenCommentItem
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|mDistanceBetweenCommentItem |整數 |相鄰評論項之間的間距。預設值：`6`。單位：dp。 |


<span id="5f9f91d5"></span>
### setRoomCommentListViewBottomMargin

設定評論列表底部與評論輸入框頂部之間的間距。

```Java
public void setRoomCommentListViewBottomMargin(int roomCommentListViewBottomMargin)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|roomCommentListViewBottomMargin |整數 |評論列表底部與評論輸入框頂部之間的間距。預設值：`0`。單位：dp。 |


<span id="08f729f4"></span>
### setCommentListPullToRefreshColor

設定下拉刷新元件的內容顏色，例如`↓ 拉取更多評論`。

```Java
public void setCommentListPullToRefreshColor(int mCommentListPullToRefreshColor)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|mCommentListPullToRefreshColor |整數 |下拉刷新元件的內容顏色，例如 `↓ 下拉載入更多評論`。 |


<span id="a60099d7"></span>
### setCommentLikedIcon

設定評論已按讚時的讚圖示。

```Java
public void setCommentLikedIcon(BDThemeIconModel commentLikedIcon) {
    mCommentLikedIcon = commentLikedIcon;
}
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|commentLikedIcon |BDThemeIconModel |按鈕資訊。更多資訊請參見 [BDThemeIconModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#56a27a1b)。 |


<span id="166c853b"></span>
### setCommentLikeIcon

設定評論尚未按讚時的讚圖示。

```Java
public void setCommentLikeIcon(BDThemeIconModel commentLikeIcon) {
    mCommentLikeIcon = commentLikeIcon;
}
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|commentLikeIcon |BDThemeIconModel |按鈕資訊。更多資訊請參見 [BDThemeIconModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#56a27a1b)。 |


<span id="542ef80d"></span>
### setCommentInputCountLimit

設定評論輸入框允許輸入的最大字數。

```Java
public void setCommentInputCountLimit(int commentInputCountLimit)
```


**輸入參數**


|名稱 |型別 |描述 |
|---|---|---|
|commentInputCountLimit |整數 |評論輸入框允許的最大字元數。預設值：`200`。 |


<span id="ea9bfd75"></span>
### setCommentCustomListener

設定直播間評論的自訂監聽器。

```Java
public void setCommentCustomizeListener(CommentCustomizeListener commentCustomizeListener)
```


**輸入參數**


|**名稱** |**型別** |**描述** |
|---|---|---|
|commentCustomizeListener |CommentCustomizeListener |直播間評論的自訂監聽器。更多資訊請參見 [CommentCustomizeListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#2c977992)。 |


**範例程式碼**

以下範例程式碼將文字評論中的`123`顏色變更為黃色，並將笑臉表情符號替換為其他圖片。

```Java
settings.setCommentCustomizeListener((commentModel, commentConfigModel, uiConfigModel, languageManager, spannableStringBuilder, textView) -> {
    boolean presenter = commentModel.isPresenter(); // 判斷評論是否由主播發送。
    boolean lightTheme = uiConfigModel.isLightTheme(); // 判斷主題是否為非深色模式。
    LanguageManager.LANGUAGE currentLanguage = languageManager.getCurrentLanguage();// 獲取直播間當前選擇的語言。
    
    String s = spannableStringBuilder.toString();
    
    // 將評論文字中的「123」變更為黃色。
    if (s.contains("123")) {
        spannableStringBuilder.setSpan(new ForegroundColorSpan(Color.YELLOW),
                s.indexOf("123"), s.indexOf("123") + 3, Spannable.SPAN_INCLUSIVE_EXCLUSIVE);
    }
    
    // 將笑臉表情替換為其他圖片。
    if (s.contains("[Smile]")) {
        spannableStringBuilder.setSpan(new GlideImageSpan(textView, "https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/055f8e4f26c04fd39aa3a3935a43866e~tplv-goo7wpa0wc-image.image"),
                s.indexOf("[Smile]"), s.indexOf("[Smile]") + "[Smile]".length(), Spannable.SPAN_INCLUSIVE_EXCLUSIVE);
    }
    // 重設 textView 以套用變更。
    textView.setText(spannableStringBuilder);
});
```


<span id="8b6e0523"></span>
### setTopCommentViewCornerRadius

設定置頂評論背景的圓角半徑。

```Java
public void setTopCommentViewCornerRadius(int topCommentViewCornerRadius)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentViewCornerRadius |int |置頂評論背景的圓角半徑。預設值：`8`。單位：dp。 |


<span id="115fbc19"></span>
### setTopCommentBackgroundWidthFitContent

設定置頂評論背景寬度是否隨內容寬度調整。

```Java
public void setTopCommentBackgroundWidthFitContent(boolean topCommentBackgroundWidthFitContent)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentBackgroundWidthFitContent |boolean |置頂評論背景的寬度是否隨內容寬度自動調整。預設值：`false`。有效值：<br><br><br>* `true`：置頂評論背景的寬度隨內容寬度自動調整。<br><br>* `false`：置頂評論背景的寬度為固定值。 |


<span id="36d938dc"></span>
### setTopCommentNicknameColor

設定置頂評論暱稱的顏色。

```Java
public void setTopCommentNicknameColor(int topCommentNicknameColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentNicknameColor |int |置頂評論暱稱的顏色。 |


<span id="e85f2897"></span>
### setTopCommentNicknameFontSize

設定置頂評論暱稱的字體大小。

```Java
public void setTopCommentNicknameFontSize(int topCommentNicknameFontSize)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentNicknameFontSize |int |置頂評論暱稱的字體大小。單位：sp。 |


<span id="9891737b"></span>
### setTopCommentNicknameFontStyle

設定置頂評論暱稱的字型。

```Java
public void setTopCommentNicknameFontStyle(Typeface topCommentNicknameFontStyle)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentNicknameFontStyle |Typeface |置頂評論暱稱的字體。 |


<span id="826adc59"></span>
### setTopCommentContentLineSpacingExtra

設定置頂評論內容的行距。

```Java
public void setTopCommentContentLineSpacingExtra(int topCommentContentLineSpacingExtra)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentContentLineSpacingExtra |int |置頂評論內容的行距。單位：dp。 |


<span id="452857ff"></span>
### setTopCommentTagColor

設定置頂評論暱稱左側垂直線的顏色。

```Java
public void setTopCommentTagColor(int topCommentTagColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentTagColor |int |置頂評論中暱稱左側垂直線的顏色。 |


<span id="b5661b0f"></span>
### setTopCommentBackgroundColor

設定置頂評論的背景顏色。

```Java
public void setTopCommentBackgroundColor(int topCommentBackgroundColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|topCommentBackgroundColor |int |置頂評論的背景顏色。 |


<span id="5fc5536f"></span>
### setPopupInputBoxPromptTextColor

設定評論輸入框處於編輯狀態（即鍵盤彈出時）的佔位文字顏色。

```Java
public void setPopupInputBoxPromptTextColor(int popupInputBoxPromptTextColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|popupInputBoxPromptTextColor |int |評論輸入框於編輯狀態（即鍵盤彈出時）的佔位文字顏色。 |


<span id="a128a852"></span>
### setPopupInputBoxTextColor

設定評論輸入框處於編輯狀態（即鍵盤彈出時）已輸入文字的顏色。

```Java
public void setPopupInputBoxTextColor(int popupInputBoxTextColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|popupInputBoxTextColor |int |評論輸入框於編輯狀態（即鍵盤彈出時）已輸入文字的顏色。 |


<span id="e349d9b3"></span>
### setInputBoxPromptTextColor

設定評論輸入框處於非編輯狀態（即鍵盤未彈出時）的佔位文字顏色。

```Java
public void setInputBoxPromptTextColor(int inputBoxPromptTextColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|inputBoxPromptTextColor |int |評論輸入框於非編輯狀態（即鍵盤未彈出時）的佔位文字顏色。 |


<span id="bb581984"></span>
### setInputBoxTextColor

設定評論輸入框處於非編輯狀態（即鍵盤未彈出時）已輸入文字的顏色。

```Java
public void setInputBoxTextColor(int inputBoxTextColor)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|inputBoxTextColor |int |評論輸入框於非編輯狀態（即鍵盤未彈出時）已輸入文字的顏色。 |


<span id="40f70e3f"></span>
### setInputBoxCornerRadius

設定評論輸入框處於非編輯狀態（即鍵盤未彈出時）的圓角半徑。

```Java
public void setInputBoxCornerRadius(int inputBoxCornerRadius)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|inputBoxCornerRadius |int |評論輸入框於非編輯狀態（即鍵盤未彈出時）的圓角半徑。預設值：`19`。單位：dp。 |


<span id="992d58e3"></span>
### setCommentCellCornerRadius

設定評論單元格的圓角半徑。

```Java
public void setCommentCellCornerRadius(int commentCellCornerRadius)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|commentCellCornerRadius |int |評論單元格的圓角半徑。預設值：`12`。單位：dp。 |


<span id="016961d8"></span>
### setCommentContentLineSpacingExtra

設定評論內容的行距。

```Java
public void setCommentContentLineSpacingExtra(int commentContentLineSpacingExtra)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|commentContentLineSpacingExtra |int |評論內容的行距。單位：dp。 |


<span id="2a63cdb6"></span>
### setFunctionEntranceButtonCornerRadius

設定直播間右下角功能入口按鈕（如購物車、互動工具按鈕）的圓角半徑。

```Java
public void setFunctionEntranceButtonCornerRadius(int functionEntranceButtonCornerRadius)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|functionEntranceButtonCornerRadius |int |直播間右下角功能入口按鈕（如購物車、互動工具按鈕等）的圓角半徑。預設值：`18`。單位：dp。 |


<span id="a75bf5dd"></span>
## 註冊對話框

<span id="de14983a"></span>
### setNicknameDialogHeadFontStyle

設定標題字型。

```java
public void setNicknameDialogHeadFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|typeface |Typeface |標題的字體。 |


<span id="8dee7093"></span>
### setNicknameDialogEditTextFontStyle

設定文字框內文字的字型。

```java
public void setNicknameDialogEditTextFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|typeface |Typeface |輸入框中文字的字體。 |


<span id="31291001"></span>
### setNicknameDialogHintText

設定文字框內的佔位文字。

```java
public void setNicknameDialogHintText(String tip)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|tip |String |輸入框中的佔位文字。 |


<span id="902a970a"></span>
### setNicknameDialogButtonColor

設定確認按鈕的背景顏色。

```java
public void setNicknameDialogButtonColor(int color)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|color |Integer |確認按鈕的背景顏色。 |


<span id="719a810a"></span>
### setNicknameDialogButtonTextFontStyle

設定確認按鈕的字型。

```java
public void setNicknameDialogButtonTextFontStyle(Typeface typeface)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|typeface |Typeface |確認按鈕的字體。 |


<span id="f2244eec"></span>
### setNicknameDialogCloseButtonIconDrawable

設定關閉圖示。

```java
public void setNicknameDialogCloseButtonIconDrawable(Drawable drawable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|drawable |Drawable |關閉圖示。 |


<span id="83ccfbdf"></span>
## 圖形

<span id="7aea6698"></span>
### setRichTextPadding

設定圖形區域的上、下、左、右邊距。

```java
public void setRichTextPadding(int padding)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|padding |Integer |圖文區域的上、下、左、右邊距。該值不可為負數。單位：dp。 |


<span id="bfdcd525"></span>
### setImageTextContentColor

設定圖形內容的文字顏色。

```java
public void setImageTextContentColor(int mImageTextContentColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mImageTextContentColor |Integer |圖文內容的文字顏色。<br><br>若值為`0`或為空，則使用伺服器返回的文字顏色。 |


<span id="5bf1f53a"></span>
## 廣告

<span id="f6305e09"></span>
### setPageCenterAdRatio

設定頁面內廣告的寬高比。

```java
public void setPageCenterAdRatio(float pageCenterAdRatio)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|pageCenterAdRatio |float |頁面內廣告的寬高比。 |


<span id="50a8bd40"></span>
### setCenterAdStrokeColor

設定頁面內廣告的邊框顏色。

```java
public void setCenterAdStrokeColor(int centerAdStrokeColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|centerAdStrokeColor |Integer |頁面內廣告的邊框顏色。 |


<span id="1be75c00"></span>
### setCenterAdRadius

設定頁面內廣告的圓角。

```java
public void setCenterAdRadius(int centerAdRadius)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|centerAdRadius |Integer |頁面內廣告的圓角。 |


<span id="314388e8"></span>
### setCenterAdRotationInterval

設定頁面內廣告的輪播速度。

```java
public void setCenterAdRotationInterval(int centerAdRotationInterval)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|centerAdRotationInterval |Integer |頁面內廣告的輪播速度，具體指輪播向右滑動的頻率。單位：毫秒（ms）。 |


<span id="1448f45f"></span>
### setFloatAdLayoutParams

設定浮動廣告的預設位置。

```Java
public void setFloatAdLayoutParams(SimpleLayoutParams floatAdLayoutParams)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatAdLayoutParams |SimpleLayoutParams |浮動廣告的預設位置。有關配置詳情，請參見[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e4a2c940)。 |


<span id="039e38e4"></span>
### setFloatAdSize

設定浮動廣告的尺寸。

```Java
public void setFloatAdSize(CustomSize floatAdSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatAdSize |CustomSize |浮動廣告的尺寸。有關配置詳情，請參見[CustomSize](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#38b050a5)。 |


<span id="a252408c"></span>
### setFloatAdMovable

設定是否允許觀眾拖曳浮動廣告。

```Java
public void setFloatAdMovable(boolean FloatAdMovable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|FloatAdMovable |Boolean |是否允許觀眾拖曳浮動廣告。預設值：`false`。有效值：<br><br><br>* `true`：允許。<br><br>* `false`：不允許。 |


<span id="845b7139"></span>
### setFloatAdShowBounds

設定浮動廣告是否顯示白色邊框與背景。

```Java
public void setFloatAdShowBounds(boolean floatAdShowBounds)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatAdShowBounds |Boolean |浮動廣告是否顯示白色邊框和背景。預設值：`true`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="de9bce95"></span>
### **setShowPageHeaderImage**

設定是否顯示頁首圖片。

```Java
  public void setShowPageHeaderImage(boolean show)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|show |Boolean |是否顯示標頭圖片。預設值：`true`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="c2532e01"></span>
### **setShowPageCenterAd**

設定是否顯示頁面內廣告。

```Java
  public void setShowPageCenterAd(boolean show)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|show |Boolean |是否顯示頁面內廣告。預設值：`true`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="3a79a1ea"></span>
## 播放器網路狀態變化

<span id="83c1947d"></span>
### setShowNonWiFiToast

設定是否顯示行動數據使用提示。

```java
public void setShowNonWiFiToast(boolean mShowNonWiFiToast)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mShowNonWiFiToast |Boolean |是否顯示使用行動數據的提示。預設值：`true`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="6a5da8bd"></span>
### setLandNonWifiToastCount

設定橫屏直播間行動數據使用提示文字出現的次數。

```java
public void setLandNonWifiToastCount(int mNonWifiToastCount)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNonWifiToastCount |Integer |橫屏直播間中，使用行動數據提示文字出現的次數。預設值：`1`。<br><br><br>* `-1`：每次都顯示提示。<br><br>* `0`：不顯示提示。<br><br>* `≥ 1`：顯示 1 次或多次提示。 |


<span id="fe25a490"></span>
### setRetryBtnBackgroundColor

設定橫屏直播間**重試**按鈕的背景顏色。

```java
public void setRetryBtnBackgroundColor(int btnBackGround)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|btnBackGround |Integer |橫屏直播間中**Retry**按鈕的背景顏色。 |


<span id="80e7d2c4"></span>
### setPorRetryBtnBackgroundColor

設定直屏直播間**重試**按鈕的背景顏色。

```java
public void setPorRetryBtnBackgroundColor(int btnBackGround)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|btnBackGround |Integer |直屏直播間中**Retry**按鈕的背景顏色。 |


<span id="61f1657e"></span>
### setLandscapeRetryBtnCornerRadius

設定橫屏直播間**重試**按鈕的圓角。

```java
public void setLandscapeRetryBtnCornerRadius(float btnCorner)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|btnCorner |Float |橫屏直播間中**Retry**按鈕的圓角。 |


<span id="031c6eb4"></span>
### setPortraitRetryBtnCornerRadius

設定直屏直播間**重試**按鈕的圓角。

```java
public void setPortraitRetryBtnCornerRadius(float btnCorner)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|btnCorner |Float |直屏直播間中**Retry**按鈕的圓角。 |


<span id="e1e44fa2"></span>
### setNetErrorBtn

設定網路錯誤提示的按鈕文字。

```java
public void setNetErrorBtn(String mNetErrorBut)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNetErrorBut |String |網路錯誤提示的按鈕文字。 |


<span id="0e34b2ee"></span>
### setNonWIFIBtn

設定非 Wi\-Fi 狀態下的按鈕文字。

```java
public void setNonWIFIBtn(String mNonWIFIBut)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNonWIFIBut |String |非 Wi\-Fi 狀態下的按鈕文字。 |


<span id="4161f237"></span>
### setNetErrorText

設定網路錯誤提示的文字內容。

```java
public void setNetErrorText(String mNetErrorText)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNetErrorText |String |網路錯誤提示的文字內容。 |


<span id="bdd6dcee"></span>
### setNonWIFIText

設定非 Wi\-Fi 狀態下的提示文字。

```java
public void setNonWIFIText(String mNonWIFIText)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNonWIFIText |String |非 Wi\-Fi 狀態下的提示文字。 |


<span id="9dc535c9"></span>
### setNetWorkChangeTextColor

設定行動數據使用提示文字的顏色。

```java
public void setNetWorkChangeTextColor(int mNetWorkChangeTextColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNetWorkChangeTextColor |Integer |使用行動數據提示文字的顏色。預設顏色為白色。 |


<span id="f1bb9981"></span>
### setLoadingDrawable

設定橫屏直播間的加載圖示。

```java
public void setLoadingDrawable(Drawable mLoadingDrawable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mLoadingDrawable |Drawable |橫屏直播間的加載圖示。 |


<span id="c55cac87"></span>
### setPorLoadingDrawable

設定直屏直播間的加載圖示。

```java
public void setPorLoadingDrawable(Drawable mLoadingDrawable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mLoadingDrawable |Drawable |直屏直播間的加載圖示。 |


<span id="14848730"></span>
### setLoadingDrawableSize

設定橫屏直播間加載圖示的尺寸。

```java
public void setLoadingDrawableSize(int size)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|size |Integer |橫屏直播間加載圖示的尺寸。 |


<span id="e0017ed2"></span>
### setPorLoadingDrawableSize

設定直屏直播間加載圖示的尺寸。

```java
public void setPorLoadingDrawableSize(int size)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|size |Integer |直屏直播間加載圖示的尺寸。 |


<span id="dfb9b61c"></span>
## 主播帳號

<span id="b7619504"></span>
### setAccountImageSize

設定主播帳號的大頭貼尺寸。

```java
public void setAccountImageSize(int mAccountImageSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mAccountImageSize |Integer |主播帳號的頭像尺寸。 |


<span id="fb45e202"></span>
### setAccountViewColor

設定主播帳號的背景顏色。

```java
public void setAccountViewColor(int mAccountViewColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mAccountViewColor |Integer |主播帳號的背景顏色。 |


<span id="f44e96b4"></span>
### setAccountFontSize

設定主播帳號的字型大小。

```java
public void setAccountFontSize(int mAccountFontSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mAccountFontSize |Integer |主播帳號的字體大小。單位：sp。 |


<span id="59f6d2ac"></span>
### setAccountFontColor

設定主播帳號的文字顏色。

```java
public void setAccountFontColor(int accountFontColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|accountFontColor |Integer |主播帳號的文字顏色 |


<span id="d5a89797"></span>
## 浮動視窗

浮動視窗即子母畫面（PiP）視窗。

<span id="17b259a9"></span>
### setOpenLiveFloatWindow

設定是否啟用直播浮動視窗，即是否支援以 PiP 模式顯示直播畫面。

```java
public void setOpenLiveFloatWindow(boolean mOpenFloatWindow)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mOpenFloatWindow |Boolean |是否啟用直播浮動視窗。預設值：`true`。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |


<span id="afd1a6ca"></span>
### setOpenVodFloatWindow

設定是否啟用 VOD 視頻的浮動視窗，即是否支援在 PiP 模式下顯示預覽或播放。

```java
public void setOpenVodFloatWindow(boolean mOpenFloatWindow)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mOpenFloatWindow |Boolean |是否啟用 VOD 視頻的浮動視窗。預設值：`true`。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |


<span id="ef659165"></span>
### setFloatWindowBorderWidth

設定浮動視窗的邊框寬度。

```java
public void setFloatWindowBorderWidth(int mFloatWindowBorderWidth)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatWindowBorderWidth |Integer |浮動視窗的邊框寬度。此值不可為負數。單位：dp。 |


<span id="1aef7bd9"></span>
### setFloatWindowBorderColor

設定浮動視窗的邊框顏色。

```java
public void setFloatWindowBorderColor(int mFloatWindowBorderColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatWindowBorderColor |Integer |浮動視窗的邊框顏色。 |


<span id="1ef9f97b"></span>
### setFloatWindowExitBtn

設定浮動視窗的關閉圖示。

```java
public void setFloatWindowExitBtn(Drawable mFloatWindowExitBtn)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatWindowExitBtn |Drawable |浮動視窗的關閉圖示。 |


<span id="9a3a861e"></span>
### setFloatWindowCorner

設定浮動視窗的圓角。

```java
public void setFloatWindowCorner(float mFloatWindowCorner)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatWindowCorner |Float |浮動視窗的圓角。 |


<span id="644b100e"></span>
### setFloatViewActionListener

設定浮動視窗或其關閉圖示的點擊事件監聽器。設定後，當觀眾點擊浮動視窗或其關閉圖示時，SDK 會通知 `FloatViewActionListener` 點擊事件，但不會執行預設的點擊行為。有關回調資訊，請參見 [FloatViewActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#379862a5)。

```java
public void setFloatViewActionListener(FloatViewActionListener floatViewActionListener)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatViewActionListener |FloatViewActionListener |浮動視窗或其關閉圖示的點擊事件監聽器。 |


<span id="f8150cf4"></span>
### setPauseOnLockScreenInMiniWindow

設定 PiP 視窗在螢幕鎖定時是否暫停播放視頻。

```Java
public void setPauseOnLockScreenInMiniWindow(boolean pauseOnLockScreenInMiniWindow)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|pauseOnLockScreenInMiniWindow |boolean |當螢幕鎖定時，PiP 視窗是否暫停播放影片。預設值為 `false`。有效值：<br><br><br>* `true`：暫停播放影片。<br><br>* `false`：繼續播放影片。 |


<span id="dab5088d"></span>
## 多語言

<span id="e3daaa52"></span>
### setLanguageType

設定所需的語言類型。預設支援所有語言（簡體中文、繁體中文、英文和日文）。此設定僅適用於以下自訂文字。若要設定觀看頁面的語言，請呼叫 [setPreferLanguage](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#0fee5955) 方法。


* 評論間隔提醒文字

* 重播按鈕文字

* 直播間使用行動數據的提示文字

* 網路斷線按鈕文字

* 網路斷線提示文字


```java
public void setLanguageType(LanguageManager.LANGUAGE[] mLanguageType)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mLanguageType |LanguageManager.LANGUAGE[] |所需的語言類型。 |


要在直播間實現多語言自訂文字，需先傳入所需語言類型的陣列，然後依陣列索引順序以「|」分隔自訂文字。以下範例程式碼自訂重播按鈕的文字。

```java
LanguageManager.LANGUAGE[] mLanguageType = {LanguageManager.LANGUAGE.ZH_HANS, LanguageManager.LANGUAGE.EN
        , LanguageManager.LANGUAGE.JA, LanguageManager.LANGUAGE.ZH_HANT};
        
settings.setLanguageType(mLanguageType);

settings.setReplayTipText("重新观看|Watch again|もう一度見る|重新觀看");
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 1.52.1 版本起，此方法不再支援。</div>


<span id="9b8a2dce"></span>
### setMultiLanguageIcon

設定切換語言的圖示。

```java
public void setMultiLanguageIcon(Drawable mMultiLanguageIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mMultiLanguageIcon |Drawable |切換語言的圖示。 |


<span id="f7139b44"></span>
### setLanguageListener

設定切換語言的監聽器。有關回調資訊，請參見 [LanguageListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#76956141)。

```java
public void setLanguageListener(LanguageListener mLanguageListener)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mLanguageListener |LanguageListener |切換語言的監聽器。 |


<span id="0fee5955"></span>
### setPreferLanguage

設定觀看頁面的偏好語言。

```java
public void setPreferLanguage(LanguageManager.LANGUAGE mPreferLanguage)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mPreferLanguage |LanguageManager.LANGUAGE |觀看頁面的偏好語言。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅對 BytePlus Live 控制台已啟用的語言生效。</div><br> |


<span id="c37c04d4"></span>
## 商品卡片

<span id="b4177ecc"></span>
### setShowGoodsCount

設定是否顯示商品卡片總數。

```java
public void setShowGoodsCount(boolean mShowGoodsCount)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mShowGoodsCount |Boolean |是否顯示商品卡片的總數。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="f13496d0"></span>
### setShoppingCardIcon

設定直播間顯示的購物車圖示。

```java
public void setShoppingCardIcon(Drawable shoppingCardIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardIcon |Drawable |直播間顯示的購物車圖示。 |


<span id="65eb7338"></span>
### setShopCardItemImageCorner

設定商品卡片項目背景的圓角。

```java
public void setShopCardItemImageCorner(int mShopCardItemImageCorner)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mShopCardItemImageCorner |Integer |商品卡片項目背景的圓角。 |


<span id="8a715680"></span>
### setShoppingCardDialogHeight

設定商品卡片對話框的高度。

```java
public void setShoppingCardDialogHeight(int shoppingCardDialogHeight)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardDialogHeight |Integer |商品卡片對話框的高度。此值不可為負數。預設情況下，高度為螢幕高度的 0.73 倍。單位：dp。 |


<span id="d2c8b7e7"></span>
### setShoppingCardDialogBackgroundColor

設定商品卡片對話框的背景顏色。

```java
public void setShoppingCardDialogBackgroundColor(int shoppingCardDialogBackgroundColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardDialogBackgroundColor |Integer |商品卡片對話框的背景顏色。 |


<span id="4112416e"></span>
### setShoppingCardTabFontStyle

設定商品卡片選單列的字型。

```java
public void setShoppingCardTabFontStyle(Typeface shoppingCardTabFontStyle)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardTabFontStyle |Typeface |商品卡片選單列的字體。 |


<span id="6c2bb529"></span>
### setShoppingCardTitleFontStyle

設定商品名稱的字型。

```java
public void setShoppingCardTitleFontStyle(Typeface shoppingCardTitleFontStyle)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardTitleFontStyle |Typeface |商品名稱的字體。 |


<span id="ee5486a7"></span>
### setShoppingCardTitleFontSize

設定商品名稱的字型大小。

```java
public void setShoppingCardTitleFontSize(int shoppingCardTitleFontSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardTitleFontSize |Integer |商品名稱的字型大小。單位：sp。 |


<span id="44b490a3"></span>
### setShoppingCardTitleFontColor

設定商品名稱的顏色。

```java
public void setShoppingCardTitleFontColor(int shoppingCardTitleFontColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardTitleFontColor |Integer |商品名稱的顏色。 |


<span id="9f848956"></span>
### setShoppingCardHighLightFontStyle

設定零售價格的字型。

```java
public void setShoppingCardHighLightFontStyle(Typeface shoppingCardHighLightFontStyle)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardHighLightFontStyle |Typeface |零售價的字體。 |


<span id="ab1031d9"></span>
### setShoppingCardHighLightFontSize

設定零售價格的字型大小。

```java
public void setShoppingCardHighLightFontSize(int shoppingCardHighLightFontSize)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardHighLightFontSize |Integer |零售價的字型大小。單位：sp。 |


<span id="18b68aa4"></span>
### setShoppingCardHighLightFontColor

設定零售價格的顏色。

```java
public void setShoppingCardHighLightFontColor(int shoppingCardHighLightFontColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardHighLightFontColor |Integer |零售價的顏色。 |


<span id="4a00b94d"></span>
### setProductOriginalPriceShowStrikethrough

設定是否在標價上顯示刪除線。

```Java
public void setProductOriginalPriceShowStrikethrough(boolean productOriginalPriceShowStrikethrough)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|productOriginalPriceShowStrikethrough |Boolean |是否在標價上顯示刪除線。預設值：`false`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="78f83141"></span>
### setShoppingCardBackgroundColor

設定商品卡片的背景顏色。

```java
public void setShoppingCardBackgroundColor(int shoppingCardBackgroundColor)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|shoppingCardBackgroundColor |Integer |商品卡片的背景顏色。 |


<span id="e7f49df1"></span>
### setEnableDirectUrl

設定是否啟用商品的直接 URL。

```java
public void setEnableDirectUrl(boolean mEnableDirectUrl) {
    this.mEnableDirectUrl = mEnableDirectUrl;
}
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mEnableDirectUrl |Boolean |是否啟用商品的直達連結。有效值：<br><br><br>* `true`：若在 BytePlus Live 控制台已配置直達連結，則優先使用直達連結。<br><br>* `false`：使用商品連結。 |


<span id="5b643189"></span>
## 浮動商品卡片

浮動商品卡片是以浮動圖示形式顯示的商品卡片。

<span id="b6d0c80f"></span>
### setFloatingShoppingCardBuyBtn

設定浮動商品卡片的按鈕。

```java
public void setFloatingShoppingCardBuyBtn(Drawable floatingShoppingCardBuyBtn)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatingShoppingCardBuyBtn |Drawable |浮動商品卡片的按鈕。 |


<span id="191d8368"></span>
### setFloatingShopCardBtnText

設定浮動商品卡片的按鈕文字。

```typescript
public void setFloatingShopCardBtnText(String mFloatingShopCardBtnText)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatingShopCardBtnText |String |浮動商品卡片的按鈕文字。預設情況下，使用 BytePlus Live 控制台配置的商品零售價。設定後，將使用該參數值。 |


<span id="9f41e9e3"></span>
### setFloatingShoppingCardLayoutParams

設定浮動商品卡片的預設位置。

```Java
public void setFloatingShoppingCardLayoutParams(SimpleLayoutParams floatingShoppingCardLayoutParams)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatingShoppingCardLayoutParams |SimpleLayoutParams |浮動商品卡片的預設位置。有關配置詳情，請參閱[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e4a2c940)。 |


<span id="f9c4dc83"></span>
### setFloatShoppingCardMovable

設定是否允許觀眾拖曳浮動商品卡片。

```Java
public void setFloatShoppingCardMovable(boolean FloatShoppingCardMovable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|FloatShoppingCardMovable |Boolean |是否允許觀眾拖曳浮動商品卡片。預設值：`false`。有效值：<br><br><br>* `true`：允許。<br><br>* `false`：不允許。 |


<span id="3c19c5d6"></span>
### setFloatShopCardCorner

設定浮動商品卡片的外部圓角。

```java
public void setFloatShopCardCorner(int mFloatShopCardCorner)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatShopCardCorner |Integer |浮動商品卡片的外部圓角。內部圖片的圓角會自動適應外部圓角。 |


<span id="1b9eeb2d"></span>
### setEnableFloatShopCardView

設定是否在直播間顯示浮動商品卡片。

```Java
public void setEnableFloatShopCardView(boolean enableFloatShopCardView) {
    this.enableFloatShopCardView = enableFloatShopCardView;
}
```


**參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|enableFloatShopCardView |Boolean |是否允許顯示浮動商品卡片。預設值：`true`。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="fe186922"></span>
## 直播間的 URL 重定向


* 預設情況下，SDK 會在觀眾點擊菜單下的商品卡片、浮動商品卡片、主帳號頭像或名稱、標頭廣告、頁內廣告、浮動廣告或評論區 URL 後，將觀眾重定向至 WebView 或外部瀏覽器。若要實現自訂重定向，可呼叫 [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#be1306ce) 來監聽點擊事件，並根據偵測到的點擊事件實現自訂重定向。

* 若觀眾以自訂模式登入直播間並點擊評論區的用戶暱稱時，SDK 不會有預設重定向行為。必須呼叫 [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#be1306ce) 來監聽點擊事件，並根據偵測到的點擊事件實現自訂重定向。


<span id="be1306ce"></span>
### setRedirectPageListener

設定直播間內連結的點擊事件監聽器。設定後，當觀眾點擊上述連結時，SDK 會觸發對應的點擊事件。需根據點擊事件實現自訂重定向。

```java
public void setRedirectPageListener(RedirectPageListener mRedirectPageListener)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mRedirectPageListener |[RedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#f163f66b) |直播間內鏈接的點擊事件監聽器。 |


**範例程式碼**

```Java
CustomSettings.Holder.mSettings.setRedirectPageListener(new RedirectPageListener() {
    /*****@paramliveActivity 直播間的 Activity。*@paramredirectInfo 跳轉所需的資訊。*@return是否攔截 SDK 的預設跳轉行為。true：攔截。SDK 不再執行預設跳轉行為。false：不攔截。SDK 繼續執行預設跳轉行為。*/
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
                    
                    // Display the SDK's internal WebViewDialog.也可以使用自定義 Dialog。
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
## 直播間狀態

<span id="8d1bd70f"></span>
### setLiveRoomStatusListener

設定直播間狀態監聽器。回調資訊請參見 [LiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#1c2e9aff)。

```java
public void setLiveRoomStatusListener(LiveRoomStatusListener mLiveRoomStatusListener)
```



|**名稱** |**類型** |**說明** |
|---|---|---|
|mLiveRoomStatusListener |LiveRoomStatusListener |直播間狀態監聽器。 |


<span id="59235a7d"></span>
### setLiveRoomActionListener

設定全功能直播間的退出事件監聽器。設定後，當觀眾點擊退出按鈕或實體返回鍵退出全功能直播間時，SDK 會通知 `LiveRoomActionListener` 點擊事件，且不執行預設點擊行為。回調資訊請參見 [LiveRoomActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#1d31736d)。

```java
public void setLiveRoomActionListener(LiveRoomActionListener liveRoomActionListener)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|liveRoomActionListener |LiveRoomActionListener |全功能直播間的退出事件監聽器。 |


<span id="6ae57c28"></span>
## 抽獎

<span id="329545cb"></span>
### setFloatAwardListener

設定抽獎圖示的監聽器。回調資訊請參見 [FloatingAwardView.Listener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#f36aa242)。

```java
public void setFloatAwardListener(FloatingAwardView.Listener mFloatAwardListener)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mFloatAwardListener |FloatingAwardView.Listener |抽獎圖示監聽器。 |


<span id="b0aec866"></span>
### setNeedFillAwardInfo

設定觀眾中獎後是否需要更新個人資訊。

```java
public void setNeedFillAwardInfo(boolean mNeedFillAwardInfo)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNeedFillAwardInfo |Boolean |觀眾中獎後是否需要更新個人資訊。預設值：`true`。有效值：<br><br><br>* `true`：觀眾需要更新個人資訊。<br><br>* `false`：觀眾不需要更新個人資訊。 |


<span id="a247b2a2"></span>
## 互動工具

<span id="d680233d"></span>
### setFloatInteractToolLayoutParams

設定完整互動工具圖示組的預設位置。完整互動工具圖示組包含所有在觀看頁面顯示的互動工具圖示。

```Java
public void setFloatInteractToolLayoutParams(SimpleLayoutParams floatInteractToolLayoutParams)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|floatInteractToolLayoutParams |SimpleLayoutParams |互動工具圖示組的預設位置。有關配置詳情，請參閱[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e4a2c940)。 |


<span id="3d641a87"></span>
### setFloatInteractToolMovable

設定是否允許觀眾拖曳完整互動工具圖示組。完整互動工具圖示組包含所有在觀看頁面顯示的互動工具圖示。

```Java
public void setFloatInteractToolMovable(boolean FloatInteractToolMovable)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|FloatInteractToolMovable |Boolean |是否允許觀眾拖曳互動工具圖示組。預設值：`true`。有效值：<br><br><br>* `true`：允許。<br><br>* `false`：不允許。 |


<span id="d49d3e3f"></span>
### setVotePeopleCountVisible

設定是否顯示參與投票的觀眾人數。

```Java
public void setVotePeopleCountVisible(boolean visible)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|visible |Boolean |是否顯示參與投票的觀眾人數。預設值：`true`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="dcf1c092"></span>
## 其他

<span id="360e675a"></span>
### setPortraitExitIconPosition

設定直播間直式模式下退出圖示的位置。

```java
public void setPortraitExitIconPosition(boolean mPortraitExitIconPosition)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mPortraitExitIconPosition |Boolean |直播間直式模式下退出圖示的位置。<br><br><br>* `true`：直播間右側。<br><br>* `false`：直播間左側。 |


<span id="6c8a8268"></span>
### setLandScapeExitIconPosition

設定直播間橫式模式下退出圖示的位置。

```java
public void setLandScapeExitIconPosition(boolean mLandScapeExitIconPosition)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mLandScapeExitIconPosition |Boolean |直播間橫式模式下退出圖示的位置。<br><br><br>* `true`：直播間右側。<br><br>* `false`：直播間左側。 |


<span id="313cdccf"></span>
### setCommentLinkToWebView

設定觀眾點擊連結後，內容是否顯示於當前直播間頁面。

```java
public void setCommentLinkToWebView(boolean mCommentLinkToWebView)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mCommentLinkToWebView |Boolean |觀眾點擊連結後，內容是否顯示於當前直播間頁面。有效值：<br><br><br>* `true`：顯示於當前直播間頁面。<br><br>* `false`：顯示於新頁面。 |


<span id="7ba2e7be"></span>
### setExitRoomIcon

設定退出直播間的圖示。

```java
public void setExitRoomIcon(Drawable exitRoomIcon)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|exitRoomIcon |Drawable |退出直播間的圖示。 |


<span id="6f30af5f"></span>
### setPageBackGroundColor

設定直播間的背景顏色。

```java
public void setPageBackGroundColor(int mPageBackGroundColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mPageBackGroundColor |Integer |直播間的背景顏色。 |


<span id="9565823b"></span>
### setTransitionPage

設定直播間直式模式的載入頁面。建議使用黑色背景的圖片。

```java
public void setTransitionPage(Drawable transitionPage)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|transitionPage |Drawable |直播間直屏模式下的加載頁面。 |


<span id="ad65c19c"></span>
### setCustomLoginListener

在驗證模式為公開時，設定登入自有帳號系統的監聽器。有關回呼資訊，請參閱[CustomLoginListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#75007939)。

```java
public void setCustomLoginListener(CustomLoginListener mCustomLoginListener)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mCustomLoginListener |CustomLoginListener |當認證模式為公開時，用於登入自有帳號系統的監聽器。 |


<span id="4bec9c3c"></span>
### setBookSuccessText

設定直播預約成功時的提示文字。

```java
public void setBookSuccessText(String bookSuccessText)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|bookSuccessText |String |直播預約成功時的提示文字。 |


<span id="70e35b57"></span>
### setBookFailText

設定直播預約失敗時的提示文字。

```java
public void setBookFailText(String bookFailText)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|bookFailText |String |直播預約失敗時的提示文字。 |


<span id="af612d85"></span>
### setActivityBottomNavBarColor

設定直播間顯示時，系統底部導航列的背景顏色。

```Java
public void setActivityBottomNavBarColor(int activityBottomNavBarColor)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|activityBottomNavBarColor |Integer |直播間顯示時，系統底部導航欄的背景顏色。預設顏色為純黑（`#000000`）。 |


<span id="7b592acf"></span>
### setShareListener

設定在全功能直播間點擊分享圖示時的監聽器。設定後，當觀眾在全功能直播間點擊分享圖示時，SDK會通知`ShareListener`該點擊事件，並不執行預設的點擊行為。有關回呼資訊，請參閱[ShareListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#2a6e0df9)。

```Java
public void setShareListener(ShareListener shareListener)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|shareListener |[ShareListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#2a6e0df9) |在全功能直播間點擊分享圖示時的監聽器。 |


<span id="278b0202"></span>
### setPortraitRoomClearScreenEnable

設定是否啟用直式直播間的清屏功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">清屏功能僅支援直屏直播間。</div>


```Java
public void setPortraitRoomClearScreenEnable(boolean portraitRoomClearScreenEnable)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|portraitRoomClearScreenEnable |Boolean |是否啟用直屏直播間的清屏功能。預設值：`true`。有效值：<br><br><br>* `true`：啟用。觀眾可向右滑動或點擊更多圖示（...）\> **清屏**來清除畫面。<br><br>* `false`：停用。 |


<span id="28b8fb22"></span>
### setShowCloseButtonWhenClearingScreen

設定清屏時是否顯示關閉直播間的圖示。

```Java
public void setShowCloseButtonWhenClearingScreen(boolean showCloseButtonWhenClearingScreen)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|showCloseButtonWhenClearingScreen |Boolean |清屏時是否顯示關閉直播間的圖示。預設值：`false`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="ba44eae4"></span>
### setShowRetryPageWhenJoinRoomFail

設定全功能直播間頁面初始化失敗時是否顯示重試頁面。

```Java
public void setShowRetryPageWhenJoinRoomFail(boolean showRetryPageWhenJoinRoomFail)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|showRetryPageWhenJoinRoomFail |Boolean |全功能直播間頁面初始化失敗時是否顯示重試頁面。預設值：`true`。有效值：<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |


<span id="b29215e9"></span>
### setActivityBookListener

設定直播預約的監聽器。有關回呼資訊，請參閱[ActivityBookListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#2d2129c0)。

```Java
public void setActivityBookListener(ActivityBookListener listener)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|listener |ActivityBookListener |直播預約的監聽器。 |


<span id="d240e1b4"></span>
### setCustomLanguageStringListener

設定自訂系統文字的監聽器。有關回呼資訊，請參閱[CustomLanguageStringListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#c5d14099)。

```Java
public void setCustomLanguageStringListener(CustomLanguageStringListener mCustomLanguageStringListener) 
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|mCustomLanguageStringListener |CustomLanguageStringListener |自定義系統文字的監聽器。 |


**範例程式碼**

以下範例程式碼會在觀看頁語言為英文時，將`key` `more`的文字變更為`123`。

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

在驗證模式為公開時，設定進入直播間觀眾的預設暱稱。

```Java
public void setPublicCommentNickName(String publicRegisterNickName, PublicNickNameRegisterListener nameRegisterListener)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|publicRegisterNickName |String |暱稱。若為空，則不執行任何操作。 |
|nameRegisterListener |PublicNickNameRegisterListener |當直播間認證模式為公開時，暱稱註冊結果的回調類。此參數可為 null。更多資訊請參見[PublicNickNameRegisterListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#192a9ac2)。 |


<span id="9fa8eed2"></span>
### setShowPortraitRoomTopShadow

設定直式直播間頂部是否顯示漸層覆蓋。

```Java
public void setShowPortraitRoomTopShadow(boolean showPortraitRoomTopShadow)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|showPortraitRoomTopShadow |Boolean |直屏直播間頂部是否顯示漸層覆蓋。預設值：`true`。有效值：<br><br><br>* `true`：顯示。若你的影片背景為白色，顯示漸層覆蓋可讓直播間頂部的白色文字更清晰。<br><br>* `false`：不顯示。 |


<span id="543e5973"></span>
### setBdlExternalReportConfiguration

設定資料報告配置

```Java
public void setBdlExternalReportConfiguration(BDLExternalReportConfiguration bdlExternalReportConfiguration)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|bdlExternalReportConfiguration |BDLExternalReportConfiguration |數據報告配置。更多資訊請參見[BDLExternalReportConfiguration](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#446d9b7a)。 |
