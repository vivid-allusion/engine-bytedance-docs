---
title: "TVUSinglePlayerView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvusingleplayerview-zh-TW"
---

TVUSinglePlayerView 是一個可自訂的視圖元件，用於影片播放。本 API 參考詳細說明所有可用於控制播放器的成員函式。內容涵蓋初始化、基本播放控制（播放、暫停）、狀態取得（可播放狀態、卡頓）、版面配置與解析度管理，以及針對 VOD（快進、播放速度）和直播（刷新、切線）的專屬控制。

<span id="ef40d04f"></span>
## 成員函式

<span id="bf477a17"></span>
### Init

呼叫 `init` 方法以取得 `InitConfig` 參數，並初始化自訂播放器的 `TVUSinglePlayerView` 實例。

```Java
public void init(InitConfig config)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|config |[InitConfig](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#142a3b71) |自定義播放器的初始化配置。 |


<span id="615a183b"></span>
### refreshLive

刷新目前的直播串流。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值為 `2` 時，可呼叫此方法。

```Java
public void refreshLive()
```


<span id="1be9767d"></span>
### play

播放影片。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值不為 `0` 時，可呼叫此方法。

```java
public void play()
```


<span id="c5ee7ddf"></span>
### pause

暫停影片。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值不為 `0` 時，可呼叫此方法。

```java
public void pause()
```


<span id="4d7c8619"></span>
### isPlaying

取得影片是否正在播放。

```java
public boolean isPlaying()
```


**回傳值**


* `true`：影片正在播放。

* `false`：影片未在播放。


<span id="3a0455cd"></span>
### getPlayableStatus

取得資源目前的可播放狀態。

```java
public int getPlayableStatus()
```


**回傳值**


* `0`：無可播放資源，因此無法呼叫 [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#1be9767d) 方法。

* `1`：隨選視訊（VOD）影片可播放。可呼叫 [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#1be9767d) 方法播放影片。

* `2`：直播串流可播放。可呼叫 [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#1be9767d) 方法播放影片。


<span id="04ae6102"></span>
### isStalling

檢查影片播放是否卡頓。

```java
public boolean isStalling()
```


**回傳值**


* `true`：影片正在卡頓。

* `false`：影片未卡頓。


<span id="34c994a8"></span>
### setPlayerLayoutMode

設定影片縮放模式。

```java
public void setPlayerLayoutMode(int playerLayoutMode)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|playerLayoutMode |整數 |視頻縮放模式。可選值：<br><br><br>* `0`：`ImageAspectFit`。將視頻縮放以適應播放器邊界，並保持原始寬高比。視頻的一個維度會與播放器對應維度相同，另一個維度會被縮小，若寬高比不同則會出現黑邊或白邊。<br><br>* `1`：`ImageToFill`。用視頻填滿播放器。視頻的寬高比可能會被改變。<br><br>* `2`：`ImageAspectFill`。將視頻縮放以填滿播放器邊界，並保持原始寬高比。若視頻寬高比與播放器不一致，則會裁切視頻以適應。 |


<span id="944e752b"></span>
### getResolutions

取得目前支援的解析度列表。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值不為 `0` 時，可呼叫此方法。

```java
public String[] getResolutions()
```


**回傳值**

一個字串陣列，代表目前支援的解析度。

<span id="87d359b1"></span>
### getCurResolution

取得目前選擇的解析度。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值不為 `0` 時，可呼叫此方法。

```java
public String getCurResolution()
```


**回傳值**

一個字串，代表目前選擇的解析度。

<span id="39974b24"></span>
### setCurResolution

設定目前影片的解析度。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值不為 `0` 時，可呼叫此方法。

```java
public void setCurResolution(String resolution)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|resolution |字串 |解析度。 |


<span id="5741df2b"></span>
### getCurVodPlayTime

取得目前 VOD 影片的播放時間，單位為毫秒（ms）。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值為 `1` 時，可呼叫此方法。

```java
public int getCurVodPlayTime()
```


**回傳值**

目前 VOD 影片的播放進度。

<span id="73d37e7d"></span>
### seekVodTime

跳至目前 VOD 影片指定的播放進度。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值為 `1` 時，可呼叫此方法。

```java
public void seekVodTime(int timeInMills, SeekCompletionListener listener)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|timeInMills |整數 |當前 VOD 視頻的指定播放進度。單位：ms。 |
|listener |[SeekCompletionListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#a24195f6) |定位操作完成時觸發的回調。 |


<span id="708726e4"></span>
### getCurVodDuration

取得目前 VOD 影片的總時長。單位為 ms。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值為 `1` 時，可呼叫此方法。

```Java
public int getCurVodDuration()
```


**回傳值**

目前 VOD 影片的總時長。

<span id="13db6157"></span>
### getCurVodPlaySpeed

取得目前 VOD 影片的播放速度。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值為 `1` 時，可呼叫此方法。

```Java
public float getCurVodPlaySpeed()
```


**回傳值**

目前 VOD 影片的播放速度。此值為浮點數，範圍為 (0,2]。

若無 VOD 影片正在播放，則回傳 `-1`。

<span id="83257226"></span>
### setMute

設定是否將影片靜音。

```java
public void setMute(boolean isMute)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|isMute |布林值 |指定是否靜音視頻。預設為 `false`。<br><br><br>* `true`：靜音。<br><br>* `false`：不靜音。 |


<span id="d5db245a"></span>
### setVodLoop

設定是否循環播放 VOD 影片。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的回傳值為 `1` 時，可呼叫此方法。

```java
public void setVodLoop(boolean isLoop)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|isLoop |布林值 |是否循環播放 VOD 視頻。可選值：<br><br><br>* `true`：循環播放<br><br>* `false`：不循環播放。 |


<span id="8c9860a0"></span>
### setVodPlaySpeed

設定 VOD 視頻的播放速度。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的返回值為 `1` 時，可以調用此方法。

```java
public void setVodPlaySpeed(float playSpeed)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|playSpeed |浮點數 |播放速度。取值範圍：(0,2] |


<span id="b16ac95d"></span>
### setInBackground

當所屬頁面進入或退出後台時通知播放器。

```Java
public void setInBackground(boolean inBackground)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|inBackground |布林值 |包含自訂播放器的頁面是否在背景中運行。有效值：<br><br><br>* `true`：在背景中。<br><br>* `false`：在前景中。 |


<span id="b025f007"></span>
### getLiveRoomStatus

獲取直播間狀態。

```Java
public int getLiveRoomStatus()
```


**返回值**


* `0`：由於 `TVULiveRoomServer` 實例尚未啟動，無法獲取狀態。

* `1`：直播中。

* `2`：預覽中。

* `3`：回放中。

* `4`：已結束。


<span id="0afd14cd"></span>
### getCurVodVid

獲取當前 VOD 視頻的視頻 ID（Vid）。此方法適用於有多個回放的直播間。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的返回值為 `1` 時，可以調用此方法。

```Java
public String getCurVodVid()
```


**返回值**

當前 VOD 視頻的 Vid。若未播放 VOD 視頻，則返回空字串。

<span id="d6b57534"></span>
### getCurReplayList

獲取當前回放列表。此方法適用於有多個回放的直播間。當 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#3a0455cd) 的返回值為 `1` 且 [getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#b025f007) 的返回值為 `3` 時，可以調用此方法。

```Java
public List<Replay> getCurReplayList()
```


**返回值**

當前回放列表。若直播間無回放，則返回空列表。

<span id="5cee58ed"></span>
### getCurLiveLineId

獲取當前直播源 ID。此方法適用於有多個直播源的直播間。當 [getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#b025f007) 的返回值為 `1` 時，可以調用此方法。

```Java
public long getCurLiveLineId()
```


**返回值**

當前直播源 ID。若 [getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#b025f007) 的返回值不為 `1`，則返回 `0`。

<span id="54d87f03"></span>
### getCurLiveLineList

獲取當前直播源列表。此方法適用於有多個直播源的直播間。當 [getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#b025f007) 的返回值為 `1` 時，可以調用此方法。

```Java
public List<PullStreamUrl> getCurLiveLineList() 
```


**返回值**

當前直播源列表。若 [getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#b025f007) 的返回值不為 `1`，則返回空列表。

<span id="f66fc68c"></span>
### setCoverImageContainerVisibility

設定直播間封面圖片容器的可見性。

```Java
public void setCoverImageContainerVisibility(int visibility)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|visibility |整數 |直播間封面圖片容器的可見性。預設值：[ ](https://developer.android.com/reference/android/view/View#VISIBLE)[View.VISIBLE](https://developer.android.com/reference/android/view/View#VISIBLE)。 |
