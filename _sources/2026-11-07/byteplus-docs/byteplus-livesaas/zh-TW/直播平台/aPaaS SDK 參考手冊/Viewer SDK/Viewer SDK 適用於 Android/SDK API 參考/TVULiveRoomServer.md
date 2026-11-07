---
title: "TVULiveRoomServer"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvuliveroomserver-zh-TW"
---

當需要獨立整合直播間組件時所使用的類別。

```java
public class TVULiveRoomServer
```


<span id="c1c46f81"></span>
## 成員函式

<span id="d7e92e4f"></span>
### TVULiveRoomServer

建立一個`TVULiveRoomServer`實例。

```java
public TVULiveRoomServer(Context context, long activityId, String token, int serverType)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |
|activityId |Long |要加入的直播間活動 ID。可透過呼叫[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW)或[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW)取得 ID。 |
|token |String |加入直播間所需的授權 token。可透過呼叫[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)取得 token。 |
|serverType |Integer |直播間類型。<br><br>預設值：`SERVER_TYPE_LIVEROOM`。<br><br><br>* SERVER_TYPE_LIVEROOM(1)：橫屏全功能直播間，可綁定聊天組件、自訂播放器及其他直播間組件。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">TVULiveRoomServer 實例為單例模式，表示同一時間只能存在一個實例。若要建立新實例，必須先銷毀目前的實例。   </div><br>   <br><br>* SERVER_TYPE_PORTRAIT_LIVEROOM(2)：直屏全功能直播間，可綁定聊天組件、自訂播放器及其他直播間組件。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>TVULiveRoomServer</code> 實例以單例形式存在，任何時刻僅能有一個實例。若需要新實例，必須先銷毀現有實例。   </div><br>   <br><br>* SERVER_TYPE_SINGLE(3)：自訂播放器直播間，只能綁定自訂播放器組件。同時支援多個實例，可在自有頁面上顯示多個自訂播放器。 |


**回傳值**

`TVULiveRoomServer`實例。

<span id="e5275d46"></span>
### setPlayerView

設定一個`PlayerView`實例，並綁定至`TVULiveRoomServer`實例。

```java
public void setPlayerView(PlayerView playerView)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|playerView |PlayerView |綁定至`TVULiveRoomServer`實例的[PlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/playerview-zh-TW)實例。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必於呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a>前先呼叫此方法。</div>


<span id="3068420a"></span>
### setRoomAuthMode

設定直播間的驗證模式。

```java
public void setRoomAuthMode(TVULiveRoom.TVURoomAuthMode roomAuthMode)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|roomAuthMode |TVURoomAuthMode |直播間的驗證模式，可為`PUBLIC`或`CUSTOM`，取決於傳入[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)的`mode`值。<br><br><br>* PUBLIC：若 mode 值為 1，請將參數值設為 PUBLIC。觀眾以訪客身份加入直播間。在需要用戶資訊的情境下（例如點擊評論文字框或點讚評論），必須輸入暱稱以完成訪客註冊。<br><br>* CUSTOM：若 mode 值為 2，請將參數值設為 CUSTOM。觀眾會使用您應用程式中的用戶帳號加入直播間，並可直接發送及點讚評論。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之前先呼叫此方法。</div>


<span id="fd188940"></span>
### setListener

設定直播間的監聽器。

```java
public void setListener(ITVULiveRoomServerListener tVULiveRoomListener)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|tVULiveRoomListener |ITVULiveRoomServerListener |直播間的監聽器，包含與直播間初始化及狀態變更相關的回呼。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之前先呼叫此方法。</div>


<span id="6f796abf"></span>
### start

啟動直播間。呼叫此方法後，TVULiveRoomServer 實例會呼叫後端 API 進行驗證並取得直播間資料。成功呼叫此方法後，會初始化本地直播間資料。

```java
public void start()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若不再需要直播間，可呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#9a50d0bb">closeRoom</a> 方法來銷毀目前的直播間並釋放資源。</div>


<span id="187fb8f6"></span>
### play

播放影片。

```java
public void play()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之後且在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#9a50d0bb">closeRoom</a> 之前呼叫此方法。</div>


<span id="a4751de2"></span>
### pause

暫停影片。

```java
public void pause()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之後且在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#9a50d0bb">closeRoom</a> 之前呼叫此方法。</div>


<span id="fab7b98f"></span>
### onPause#{#onPause}#

暫停影片。此方法適用於直播間的 Activity 移至背景時。

```java
public void onPause()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之後且在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#9a50d0bb">closeRoom</a> 之前呼叫此方法。</div>


<span id="0e000da9"></span>
### onResume#{#onResume}#

恢復播放影片。此方法適用於直播間的 Activity 回到前景時。

```java
public void onResume()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之後且在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#9a50d0bb">closeRoom</a> 之前呼叫此方法。</div>


<span id="c789dd75"></span>
### pausePollingData

成功初始化後，TVULiveRoomServer 實例會定期輪詢 BytePlus Live 控制台以更新直播間狀態（例如：直播、回放、預覽或已結束）。若不希望 TVULiveRoomServer 實例從控制台輪詢直播間狀態，可使用此方法暫停輪詢。

```java
public void pausePollingData()
```


<span id="09a0d1e2"></span>
### continuePollingData

指示 TVULiveRoomServer 實例恢復從控制台輪詢直播間狀態。

```java
public void continuePollingData()
```


<span id="9a50d0bb"></span>
### closeRoom

銷毀目前的直播間。

```java
public void closeRoom()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">請務必在呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#6f796abf">start</a> 之後呼叫此方法。</div>


* <div data-tips="true" data-tips-type="tip">呼叫此方法後，請勿在 TVULiveRoomServer 實例上呼叫任何其他方法。呼叫此方法後，可以將 TVULiveRoomServer 實例設為 null。</div>



<span id="82e33355"></span>
### getCommentDataManager

取得直播間訊息列表的 CommentDataManager。

```Java
public CommentDataManager getCommentDataManager()
```


**回傳值**


|類型 |說明 |
|---|---|
|CommentDataManager |直播間訊息列表的管理類別。如需更多資訊，請參閱 [CommentDataManager](https://docs.byteplus.com/docs/byteplus-livesaas/commentdatamanager-zh-TW)。 |


<span id="2323d292"></span>
### getDynamicSettings

取得直播間的 DynamicCustomSettings。可於觀眾進入直播間前或後呼叫此方法，以自訂直播間相關設定。

```Java
public DynamicCustomSettings getDynamicSettings()
```


**回傳值**

`DynamicCustomSettings`實例。欲了解更多資訊，請參閱[DynamicCustomSettings](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-TW)。
