---
title: "在行動應用程式中實現子母畫面（PiP）模式"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/zai-hang-dong-ying-yong-cheng-shi-zhong-shi-xian-z-zh-TW"
---

為了讓觀眾在離開主觀看頁面時，仍能持續關注直播或點播（VOD）內容，您可以實現子母畫面（PiP）模式。本指南為行動應用程式開發者提供說明，指導如何透過建立原生應用與網頁內容之間的通訊橋樑，啟用 Web Viewer SDK（v1.1.3 及以上版本）的 PiP 功能。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">本方案旨在建立 Web 與 Native 之間的通訊機制，要求 Native 整合合作夥伴具備一定的開發能力，以實現通訊並調整 WebView 視窗的大小。</div>


* <div data-tips="true" data-tips-type="warning">在本文檔中，<em>Native</em> 指的是行動應用程式。</div>



<span id="273e6353"></span>
## 演示

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/057444bd81da44ea816ab6c5b248cb77~tplv-goo7wpa0wc-image.image) </span>

<span id="9c1162c8"></span>
## 方案介紹

作為原生應用整合夥伴，您可以在應用程式中使用 WebView 開啟直播間的 H5 頁面，並根據需要調整 WebView 視窗的大小。此外，您可以使用`JSBridge`與 H5 頁面（網頁端）進行通訊，並利用`postMessage`方法實現資料傳輸與互動。

<span id="131d1327"></span>
## 前置條件

在 Android 端，您必須自行實作`invokeNative`方法，以便 Web 能向 Native 傳送訊息。

<span id="23d000da"></span>
## 詳細流程

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6a2ccd6184a4fb4a3e63df4ab6e6bcf~tplv-goo7wpa0wc-image.image) </span>


1. 觀眾進入觀看頁面後，原生應用會偵測到網頁元件的`INIT_FINISH`事件，表示`JSBridge`已載入完成。

2. 當偵測到網頁元件的`CREATE_PLAYER`事件時，原生應用確認播放器已建立，並接收串流是否為直播以及直播間是否為直式模式的資訊。

3. 當觀眾離開觀看頁面時，原生應用必須進入 PiP 模式，並向網頁元件發送`ENTER_MINI_WINDOW`事件。

4. 當偵測到 Native 的`ENTER_MINI_WINDOW`事件時，Web 會在 PiP 模式視窗中全螢幕顯示播放器。

5. Native 需在下列情境下實作退出 PiP 模式，並向 Web 發送`EXIT_MINI_WINDOW`事件。當偵測到 Native 的`EXIT_MINI_WINDOW`事件時，Web 會退出播放器的全螢幕，並返回觀看頁面。

   * 觀眾返回觀看頁面，例如點擊 PiP 視窗。

   * 若直播間狀態變更或觀眾切換直播來源，原生應用會偵測到網頁元件的`DESTROY_PLAYER`事件，表示播放器已被銷毀。

6. （可選）若 WebView 中出現播放問題，原生應用可：

   * 當 WebView 播放暫停時，向 Web 發送`PLAY`事件。Web 偵測到此事件後，可播放直播或點播內容。

   * WebView 播放過程中，向 Web 發送`STOP_PLAY`事件。Web 偵測到此事件後，可暫停直播或點播內容。


如需更多相關事件資訊，請參閱[事件](https://docs.byteplus.com/docs/byteplus-livesaas/zai-hang-dong-ying-yong-cheng-shi-zhong-shi-xian-z-zh-TW#b73988d7)。

<span id="fcb271db"></span>
## 附錄

<span id="57969dbc"></span>
### 訊號定義

Native 與 Web 必須遵循以下訊號定義，以實現雙向通訊。

```TypeScript
// Message types used in communication.
export interface IMessage {
  eventKey: number; // Message type.
  info?: any; // (Optional) Additional information.
}

// Defines messages sent from the web component to the native app.
export enum Web2NativeMessageEvent {
  /** JsBridge loading is complete.*/
  INIT_FINISH = 10001,
  /** The player is created.*/
  CREATE_PLAYER = 11000,
  /** The player is destroyed.*/
  DESTROY_PLAYER,
}

// Defines the message sent by Native to the Web.
export enum Native2WebMessageEvent {
  /** Enter PiP mode.*/
  ENTER_MINI_WINDOW = 21000,
  /** Exit PiP mode.*/
  EXIT_MINI_WINDOW,
}

// Defines the event triggered when the player is created.
export interface IMsgCreatePlayer {
  isPortrait: boolean; // Whether the live room is in portrait mode.
  isLive: boolean; // Whether the live room is in Live status.
}
```


<span id="72ece41d"></span>
### `JsBridge` 互動流程

`JSBridge` 作為原生應用與網頁元件之間的橋樑，實現雙向通訊。

BytePlus Live 會將全域變數`window.ByteLiveJsBridge`注入至`window`，包含以下 API：


* `nativeCallBack`：Native 端呼叫`window.ByteLiveJsBridge.nativeCallBack`向 Web 傳送訊息。

* `invokeNative`：Web 端呼叫此 API 向 Native 傳送訊息。


<span id="b73988d7"></span>
### 事件

<span id="36dec7d6"></span>
#### 網頁元件發送給原生應用的事件

```TypeScript
// The event triggered when the player is created.
window.ByteLiveJsBridge.invokeNative({
  eventKey:11000,
  info: {
     isPortrait: true, // The live room is in portrait mode.
     isLive: true, // The live room is in the Live status.
  }
)
```



|**事件** |**鍵值** |**描述** |
|---|---|---|
|INIT_FINISH |10001 |JsBridge 載入完成時觸發的事件。 |
|CREATE_PLAYER |11000 |播放器建立時觸發的事件。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此事件觸發後，可透過 <code>info</code> 參數獲取直播間是否為 Live 狀態及是否為直向模式。</div><br> |
|DESTROY_PLAYER |11001 |播放器銷毀時觸發的事件。 |


<span id="6d361e2e"></span>
#### Native 發送給 Web 的事件

```TypeScript
// The event to enter PiP mode.
window.ByteLiveJsBridge.nativeCallBack({
  eventKey: 21000   
})
```



|**事件** |**鍵值** |**描述** |
|---|---|---|
|ENTER_MINI_WINDOW |21000 |進入 PiP 模式的事件。 |
|EXIT_MINI_WINDOW |21001 |離開 PiP 模式的事件。 |
|STOP_PLAY |21002 |暫停播放的事件。 |
|START_PLAY |21003 |恢復播放並離開 PiP 模式的事件。 |
|PLAY |21004 |播放直播流或 VoD 內容的事件。 |
