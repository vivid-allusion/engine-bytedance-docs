---
title: "TVULiveRoom"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW"
---

用於整合全功能直播間的類別，包含進入與離開直播間等功能。

```java
public class com.bytedance.live.sdk.player.TVULiveRoom
```


<span id="d6403c6d"></span>
## 成員函式

<span id="b20db0d1"></span>
### joinLiveRoom

進入全功能直播間。

```java
public static void joinLiveRoom(final Context context, JoinRoomConfig joinRoomConfig)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |
|joinRoomConfig |JoinRoomConfig |進入全功能直播間所需的配置。詳情請參見[JoinRoomConfig](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#4530ad0e)。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在調用此方法前，可調用<code>CustomSettings.Holder.mSettings</code>中的方法自訂直播間。詳情請參見<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW">mSettings</a>。</div>


<span id="9fab7a9d"></span>
### leaveLiveRoom

離開直播間並銷毀當前浮窗。

```java
public static void leaveLiveRoom(final Context context)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在調用此方法前先調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="e8fc71ab"></span>
### destroyFloatWindow

銷毀當前浮窗及其播放資源。建議在調用[setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#8d1bd70f)方法並檢測到直播間已被銷毀後，再調用此方法。

```java
public static void destroyFloatWindow()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在調用此方法前先調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="f974fe00"></span>
### manualClickFloatWindow

模擬手動點擊當前浮窗。

```java
public static void manualClickFloatWindow()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在調用此方法前先調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="0f1507fb"></span>
### manualClickFloatWindowExitBtn

模擬手動點擊當前浮窗的退出按鈕。

```java
public static void manualClickFloatWindowExitBtn()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在調用此方法前先調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="44c0414d"></span>
### manualClickLiveRoomExitBtn

模擬手動點擊直播間的退出按鈕。此操作會觸發與觀眾點擊直播間退出按鈕相同的行為。

```java
public static void manualClickLiveRoomExitBtn(final Context context)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在調用此方法前先調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="5984565f"></span>
### clearCache

清除觀眾當前裝置上 SDK 的所有本地快取。本地快取包括：


* 提醒彈窗的記錄。清除快取後，觀眾再次進入直播間時會再次看到彈窗。

* 當驗證模式為公開時，系統行事曆中的直播預約記錄。清除快取後，**預約**按鈕會恢復為**立即預約**，但系統行事曆中的事件仍會保留。

* 隨選視訊（VOD）影片播放進度的記錄。清除快取後，觀眾再次進入直播間時，VOD 影片將從頭開始播放。


```java
public static void clearCache(Context context)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |


<span id="0a6ab44b"></span>
### getCookieId

取得 SDK 本地產生的裝置 ID（`deviceId`）。每個裝置都有唯一的裝置 ID，可用於日誌查詢。

```java
public static String getCookieId(Context context)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |


**回傳值**

本地產生的裝置 ID（`deviceId`）。

<span id="8982a31c"></span>
### showFloatPermissionDialogInLiveRoom

在全功能直播間中顯示浮窗權限請求對話框。此方法僅在全功能直播間頁面處於活動狀態時生效。

```Java
public static void showFloatPermissionDialogInLiveRoom(final Context context)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |
