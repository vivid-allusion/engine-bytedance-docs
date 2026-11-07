---
title: "SDK licenses"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-licenses"
---

To integrate BytePlus MediaLive SDKs, you need a license to manage feature access. This topic details the available license types for client SDKs and the Player SDK for Web, and their respective pricing to help you select the most appropriate and cost\-effective option for your project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to get a license, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management">Getting your SDK license</a>.</div>


<span id="74ff77ba"></span>
## Pricing

<span id="9a8326b3"></span>
### Client SDKs

The billing of client SDKs, namely SDKs for Android, iOS, React Native, and Flutter, consists of the following two parts.


|Type |Description |
|---|---|
|BytePlus MediaLive SDK license fees |The license fees for BytePlus MediaLive client SDKs. |
|[Other cloud service fees](https://docs.byteplus.com/docs/byteplus-media-live/docs-other-cloud-service-fees) |Fees generated when using BytePlus MediaLive SDKs in conjunction with other products such as BytePlus RTC and BytePlus Effects SDK. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The premium license was upgraded on January 9, 2026. From that date, if you need to renew the license, refer to the following table for the latest features supported by each license type. For more information about this upgrade, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/announcement_on_the_upgrade_of_the_client_sdk_premium_license">Announcement on the upgrade of the client SDK premium license</a>.</div>



|License Type |Validity Period |Acquisition Method |Price (USD) |Description |
|---|---|---|---|---|
|Basic |1 year |Make a purchase |2,860 |You can use all the basic features, such as playing RTMP and HLS streams, using the TCP and TLS protocols, starting or stopping playback, and muted playback. |
|||Bind a live\-stream traffic pack of 100 TB or larger |0 ||
|Premium |1 year |Make a purchase |28,600 |You can use all the basic features, as well as the following features. For more information on the differences among the SDKs, see [SDK introduction](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction).<br><br><br>* QUIC protocol<br><br>* Playing RTM streams<br><br>* Playing CMAF streams (currently only available for the SDK for Android)<br><br>* Low\-latency FLV stream pulling<br><br>* SEI message transmission<br><br>* H.265 hardware and software decoding<br><br>* H.266 software decoding (currently only available for the SDK for Android)<br><br>* Adaptive Bitrate (ABR) streaming<br><br>* Commercial DRM (Digital Rights Management)<br><br>* Super\-resolution (SR)<br><br>* Video sharpening<br><br>* Primary/backup stream switching |
|Trial |1 month |Apply for the license through the console |0 |You can use premium license features during the trial. |


<span id="0c916d6b"></span>
### Player SDK for Web


|License Type |Validity Period |Acquisition Method |Price (USD) |Description |
|---|---|---|---|---|
|Basic |1 year |Make a purchase |0 |You can use all the basic features, such as stream pulling and statistics. |
|Premium |1 year |Make a purchase |8,300 |You can use all the basic features, as well as the following features:<br><br><br>* [ABR streaming](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr)<br><br>* [Adaptive buffer strategy](https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy)<br><br>* [Low-latency FLV stream pulling](https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web)<br><br>* [Playing RTM streams](https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration) |
|Trial |1 month |Apply for the license through the console |0 |You can use premium license features during the trial. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus also offers a powerful, AI\-friendly video player solution that supports AI\-powered features such as video summarization and object recognition, enabling an intelligent client\-side viewing experience. You can <a href="https://demo.byteplus.com/aiexp/demo/ai-player">try the demo</a> and contact us for more information about integration and billing.</div>


<span id="55ec08cd"></span>
## Calculating validity periods

The validity period calculation rule depends on the type of operation.

<span id="1216336d"></span>
### Upgrading a trial license

This operation applies when you upgrade a trial license to a basic or premium license.


* **Rule:**  The new one\-year validity period starts **immediately** upon upgrade. Any remaining time on the trial license will be lost.

* **Example:** 

   * **Trial license starts**: May 10, 2026, 10:00

   * **Trial license expires**: June 10, 2026, 10:00

   * **Upgrade to a basic license**: May 30, 2026, 11:00

   * **New basic license starts**: May 30, 2026, 11:00

   * **New basic license expires**: May 30, 2027, 11:00


<span id="c766097e"></span>
### Renewing a license

This operation applies when you renew a basic or premium license.


* **Rule**: The validity period is extended by **adding one year to the current license's original expiration date**. Your remaining validity period is preserved.

* **Example**:

   * **Original basic license starts**: May 12, 2026, 10:00

   * **Original basic license expires**: May 12, 2027, 10:00

   * **Renew a basic license**: October 9, 2026, 11:00

   * **New basic license expires**: May 12, 2028, 10:00


<span id="be926f57"></span>
## Notes


* A license's validity period begins only when the license is bound to your SDK application. The trial license is valid for one month from the binding date, and the basic or premium license is valid for one year from the binding date.

* You can renew a basic or premium license before or after its expiration. A basic license can only be renewed as a basic license, and a premium license as a premium license.

* The trial license cannot be renewed. Instead, you can upgrade it to a basic or premium license.

* You cannot bind a basic, premium, or trial license to multiple package names for Android apps (PackageName), bundle IDs for iOS apps (BundleID), or wildcard domains for Web apps. If you have multiple apps, you must use multiple licenses.

* If you get a license by binding a live\-stream traffic pack of 100 TB or larger, the license's validity period remains unaffected by the resource pack. In other words, if the traffic in a resource pack is used up before the license expires, or if you unsubscribe from or receive a refund for the pack, you can continue to use the SDK as long as the license remains valid.
