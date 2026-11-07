---
title: "CSAI integration overview"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai_integration_overview"
---

This guide provides a comprehensive overview of the Client\-Side Ad Insertion (CSAI) solution for VideoOne\-based Short Drama applications. By integrating the BytePlus MediaAds SDK and Google IMA SDK, you can monetize your content with In\-stream Ads alongside or as an alternative to the Paywall/Unlock model.

<span id="fb9bc419"></span>
## Key features


* **Diverse Ad formats**: Supports Pre\-roll, Mid\-roll, and Post\-roll ads.

* **Flexible scheduling**: Configure ads using VAST tag URLs and precise time offsets.

* **Player agnostic**: Compatible with `TTVideoEngine` and custom players via the `ContentPlayer` interface.

* **Seamless experience**: Automatically manages content pausing/resuming and ad skip logic.

* **Anti\-Bypass**: Automatically plays the most recent missed ad break if a user seeks past one or more ad offsets, preventing intentional ad skipping.

* **Frequency control**: Ensures each mid\-roll ad spot triggers only once per session for a balanced user experience.


<span id="aa76cfc7"></span>
## Monetization rules


* **Drama series level**: A single drama series can use **either** the Paywall/Unlock model **or** the In\-stream Ads model, but not both simultaneously.

* **App level**: You can apply different monetization models to different drama series within the same application.


<span id="43918d44"></span>
## Experience the Demo

Download the latest [VideoOne Demo](https://docs.byteplus.com/en/docs/byteplus-vos/docs-byteplus-videoone-demo-app_1) (v5.4.0 or above) to experience the In\-stream Ads capability firsthand.

<span id="e2257056"></span>
## Integration guides

Select your platform to start the integration:


* [CSAI integration for Android](https://docs.byteplus.com/docs/byteplus-vos/csai_integration_for_android)

* [CSAI integration for iOS](https://docs.byteplus.com/docs/byteplus-vos/csai_integration_for_ios)
