---
title: "Implementing picture-in-picture (PiP) mode in mobile apps"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/implementing-picture-in-picture-mode-in-mobile-apps"
---

This topic introduces how to implement PiP mode in your mobile apps when using SaaS or Web Viewer SDK version 1.1.3 and above. When viewers leave the viewing page, such as opening a new page or switching the viewing page to the background, they can watch the live stream or Video on Demand (VOD) content in PiP mode.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This solution aims to establish a communication mechanism between the Web and Native, requiring the Native integration partners to have certain development capabilities to enable communication and adjust the size of the WebView window.</div>


* <div data-tips="true" data-tips-type="warning">The term Native refers to mobile apps, and this term will be used to refer to mobile apps hereafter.</div>



<span id="273e6353"></span>
## Effect demonstration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/057444bd81da44ea816ab6c5b248cb77~tplv-goo7wpa0wc-image.image) </span>

<span id="9c1162c8"></span>
## Solution introduction

As a Native integration partner, you can use WebView in your app to open the H5 page of the live room and adjust the size of the WebView window as needed. Additionally, you can use `JsBridge` to communicate with the H5 page (Web end), and use the `postMessage` method to enable data transmission and interaction.

<span id="131d1327"></span>
## Prerequisites

On the Android side, you must implement the `invokeNative` method yourself to enable the Web to send messages to the Native.

<span id="23d000da"></span>
## Detailed process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6a2ccd6184a4fb4a3e63df4ab6e6bcf~tplv-goo7wpa0wc-image.image) </span>


1. A viewer visits the viewing page, and then the Native detects the Web’s `INIT_FINISH` event, indicating that the `JSBridge` has completed loading.

2. Upon detecting the Web’s `CREATE_PLAYER` event, the Native confirms that the player has been created, and knows whether the live room is in Live status and in portrait mode.

3. When the viewer leaves the viewing page, the Native needs to implement entering PiP mode and send the `ENTER_MINI_WINDOW` event to the Web.

4. Upon detecting the Native’s `ENTER_MINI_WINDOW` event, the Web displays the player in full\-screen within the PiP mode window.

5. The Native needs to implement exiting PiP mode and send the `EXIT_MINI_WINDOW` event to the Web in the following situations. Upon detecting the Native’s `EXIT_MINI_WINDOW` event, the Web exits the full\-screen of the player and returns to the viewing page.

   * The viewer returns to the viewing page by tapping the PiP mode window or in other ways.

   * The live room status changes or the viewer switches the live source, the Native detects the Web's `DESTROY_PLAYER` event, indicating the player has been destroyed.

6. (Optional) If there are playing issues in the WebView, the Native can:

   * Send the `PLAY` event to the Web when the playing is paused in the WebView. Upon detecting this event, the Web can play live stream or VOD content.

   * Send the `STOP_PLAY` event to the Web during playing in the WebView. Upon detecting this event, the Web can pause the live stream or VOD content.


For more information about related events, see [Events](https://docs.byteplus.com/docs/byteplus-livesaas/implementing-picture-in-picture-mode-in-mobile-apps#b73988d7).

<span id="fcb271db"></span>
## Appendix

<span id="57969dbc"></span>
### Signaling definitions

Both the Native and Web must follow the following signaling definitions to enable two\-way communication.

```TypeScript
// Message types used in communication.
export interface IMessage {
  eventKey: number; // Message type.
  info?: any; // (Optional) Additional information.
}

// Defines the message sent by Web to the Native.
export enum Web2NativeMessageEvent {
  /** JsBridge loading is complete. */
  INIT_FINISH = 10001,
  /** The player is created. */
  CREATE_PLAYER = 11000,
  /** The player is destroyed. */
  DESTROY_PLAYER,
}

// Defines the message sent by Native to the Web.
export enum Native2WebMessageEvent {
  /** Enter PiP mode. */
  ENTER_MINI_WINDOW = 21000,
  /** Exit PiP mode. */
  EXIT_MINI_WINDOW,
}

// Defines the event triggered when the player is created.
export interface IMsgCreatePlayer {
  isPortrait: boolean; // Whether the live room is in portrait mode.
  isLive: boolean; // Whether the live room is in Live status.
}
```


<span id="72ece41d"></span>
### `JsBridge` interaction process

`JSBridge` is a bridge between the Native and Web, serving as a medium for two\-way communication.

BytePlus Live injects the global variable `window.ByteLiveJsBridge` into the `window`, including the following APIs:


* `nativeCallBack`: The Native calls `window.ByteLiveJsBridge.nativeCallBack` to send messages to the Web.

* `invokeNative`: The Web calls this API to send messages to the Native.


<span id="b73988d7"></span>
### Events

<span id="36dec7d6"></span>
#### Web events listened to by the Native

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



|**Event** |**Key** |**Description** |
|---|---|---|
|INIT_FINISH |10001 |The event triggered when JsBridge loading is complete. |
|CREATE_PLAYER |11000 |The event triggered when the player is created.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After this event is triggered, you can use the <code>info</code> parameter to get whether the live room is in Live status and in portrait mode.</div><br> |
|DESTROY_PLAYER |11001 |The event triggered when the player is destroyed. |


<span id="6d361e2e"></span>
#### Events sent by Native to the Web

```TypeScript
// The event to enter PiP mode.
window.ByteLiveJsBridge.nativeCallBack({
  eventKey: 21000   
})
```



|**Event** |**Key** |**Description** |
|---|---|---|
|ENTER_MINI_WINDOW |21000 |The event to enter PiP mode. |
|EXIT_MINI_WINDOW |21001 |The event to exit PiP mode. |
|STOP_PLAY |21002 |The event to pause playing. |
|START_PLAY |21003 |The event to resume playing and exit PiP mode. |
|PLAY |21004 |The event to play live stream or VoD content. |
