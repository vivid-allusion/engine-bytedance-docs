---
title: "Autoplay Configuration Guide"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/Autoplay_Configuration_Guide"
---

This document describes how to implement video autoplay using the Web Player SDK (VePlayer). It covers configuration methods, compatibility strategies across major browsers and WebView environments, and fallback handling. The goal is to help you achieve a stable autoplay experience across multiple platforms.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="f443dd0b"></span>
## Feature Overview

Autoplay allows video playback to begin automatically when the page loads, without user interaction. However, autoplay behavior is subject to browser\-specific policies. Conditions such as muted playback or prior user interaction may be required.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to these restrictions, autoplay may be blocked on certain devices or browsers. We recommend designing your application with user experience in mind and avoiding forced autoplay.</div>


<span id="前提条件"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="配置自动播放"></span>
## 1. Configuring Autoplay

VePlayer supports autoplay through the `autoplay` configuration option. For detailed configuration options, refer to [LiveVePlayerOptions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423). Autoplay success depends on whether the current environment satisfies browser autoplay policies.

<span id="浏览器环境"></span>
### In Browser Environments

In standard web browsers, autoplay will succeed if **any** of the following conditions are met:


|Condition Category |Description |
|---|---|
|Muted Playback |The video is muted (`muted: true`) or has volume set to 0. This is the most reliable way to enable autoplay. |
|User Interaction |Autoplay is allowed after the user interacts with the page (click, scroll, keyboard input, etc.). |
|Site Whitelist |Browsers may grant autoplay permission to sites based on user engagement history. |
|User Settings |Some browsers allow users to manually grant autoplay permission for specific sites. |
|Delegated Permissions |If the video is embedded in an `<iframe>` and the top\-level page has autoplay permission, the permission can be delegated to the iframe. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details, see the autoplay policies of <a href="https://www.chromium.org/audio-video/autoplay/">Google Chrome</a> and <a href="https://webkit.org/blog/7734/auto-play-policy-changes-for-macos/">WebKit</a>.</div>


<span id="WebView 环境"></span>
### In WebView Environments

Autoplay in embedded browsers like WebView may require additional configuration.

<span id="Android WebView"></span>
#### Android WebView

By default, Android WebView **blocks unmuted autoplay**. It is recommended to configure VePlayer for **muted autoplay** as shown below:

```javascript
VePlayer.createLivePlayer({
    autoplay: { muted: true }
}).then(function(veplayer) {
    // Player instance
});
```


To allow unmuted autoplay (not recommended unless carefully evaluated), set [setMediaPlaybackRequiresUserGesture](https://developer.android.com/reference/android/webkit/WebSettings.html#setMediaPlaybackRequiresUserGesture(boolean)) to `false`:

```java
myWebView.getSettings().setMediaPlaybackRequiresUserGesture(false);
```


<span id="iOS WebView"></span>
#### iOS WebView

iOS WebView also blocks autoplay of videos with sound by default. Use muted autoplay:

```javascript
VePlayer.createLivePlayer({
    autoplay: { muted: true }
}).then(function(veplayer) {
    // Player instance
});
```


To allow unmuted autoplay, set [mediaTypesRequiringUserActionForPlayback](https://developer.apple.com/documentation/webkit/wkwebviewconfiguration/1851524-mediatypesrequiringuseractionfor) to `NO`:

```objectivec
[self.webView mediaTypesRequiringUserActionForPlayback:NO];
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Autoplay may be blocked when iOS devices are in Low Power Mode.</div>


<span id="微信内置浏览器环境"></span>
### 2. Detecting Autoplay Success

Due to the complexity of browser policies, it’s important to programmatically verify whether autoplay has succeeded.

<span id="方法一：监听 play() 方法的 Promise 返回"></span>
### Method 1: Use the `play()` Promise

Calling `veplayer.play()` returns a Promise object.


* **Resolved:**  Playback started successfully.

* **Rejected with** **`NotAllowedError`** **:**  Playback was blocked by the browser due to autoplay restrictions.


Example:

```javascript
let startPlayPromise = veplayer.play();

if (startPlayPromise !== undefined) {
  startPlayPromise
    .catch(error => {
      if (error.name === "NotAllowedError") {
        // Autoplay was blocked by the browser
        // You can retry playback with muted audio, or prompt the user to click a play button
      } else {
        // Other playback-related errors occurred
      }
    })
    .then(() => {
      // Playback started successfully
      // Continue with any post-playback logic here
    });
}
```


<span id="方法二：监听 AUTOPLAY_PREVENTED 事件"></span>
### Method 2: Listen for the `AUTOPLAY_PREVENTED` Event

The Web Player SDK emits an `AUTOPLAY_PREVENTED` event when autoplay is blocked by the browser. You can handle this event to implement fallback logic.

Example:

```javascript
VePlayer.createLivePlayer({
  autoplay: { muted: false }
}).then(function (veplayer) {
  // Listen for autoplay prevention event
  veplayer.on(VePlayer.live.Events.AUTOPLAY_PREVENTED, () => {
    console.log('Autoplay was blocked by the browser');
    // Add fallback logic here, such as prompting the user to tap a play button
  });
});
```
