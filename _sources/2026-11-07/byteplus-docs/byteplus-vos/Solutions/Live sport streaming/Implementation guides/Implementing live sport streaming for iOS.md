---
title: "Implementing live sport streaming for iOS"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-ios"
---

This guide describes how to implement a sports live\-viewing experience on iOS using the BytePlus MediaLive SDK. You will learn how to initialize the live player, pull a stream over a low\-latency protocol, switch camera angles and quality, and layer interactive features on top of playback.

<span id="lsi-env"></span>
## Environmental requirements


* Xcode 16 or higher. We recommend using the latest version of Xcode for optimal performance.

* A physical device that runs iOS 13 or higher.


<span id="lsi-prereq"></span>
## Prerequisites


* A valid [BytePlus account](http://console.byteplus.com/) with [BytePlus MediaLive](https://console.byteplus.com/live) activated.

* Complete the [basic setup for Live stream](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started):

   * Obtain a BytePlus MediaLive SDK license.

      * For detailed instructions on how to acquire the license, see [Accessing your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license).

      * To learn more about choosing the right license type for your needs, refer to [SDK introduction](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction).


<span id="lsi-version"></span>
## Version requirements


* To access the **live stream pulling** feature, you must use the BytePlus MediaLive SDK. Remember to choose the correct SDK on the [Client SDK components](https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination) page.


<span id="lsi-integrate"></span>
## Integrate the SDK

Add the `TTSDKFramework` pull subspec to your `Podfile`:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To get the latest version number, see <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">Client SDK components</a>.</div>


```Ruby
$TT_SDK_VERSION = '1.50.200.2-premium'
pod 'TTSDKFramework', $TT_SDK_VERSION, :subspecs => ['LivePull-RTS']
```


Then run `pod install`.

<span id="lsi-impl"></span>
## Implementation

<span id="lsi-player"></span>
### Step 1: Create the player

Create a live player instance using the BytePlus MediaLive SDK and set up its delegate to receive playback callbacks.

```Swift
let player = TVLManager(type: VeLivePlayerTypeOwn)
```


<span id="lsi-pull"></span>
### Step 2: Pull the stream

Configure the pull URL for the selected camera and quality, then start playback. To use low\-latency FLV, enable the low\-latency FLV option before playback.

<span id="lsi-switch"></span>
### Step 3: Switch camera angle and quality

When the viewer selects a different camera or quality tier, re\-bind the player to the corresponding pull URL. When multiple protocols or quality tiers are available for the same source, choose the URL that matches the viewer's selection.

<span id="lsi-interact"></span>
### Step 4: Add interactive features

Layer interactive UI (gifts, comments and bullet comments, and likes) on top of the playback view, and provide a landscape mode for fullscreen viewing.

<span id="lsi-code"></span>
## Sample code

Refer to the demo source code to integrate this feature into your app.


* iOS: [LiveSportStreaming](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/LiveSportStreaming)
