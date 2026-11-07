---
title: "Time shifting"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-time-shifting"
---

The time\-shifting feature allows your viewers to replay any streamed content. When using this feature, you may incur the following fees:


* **Live\-streaming service fee**: When the viewer replays the time\-shifting content, there will be live\-streaming service fees. Refer to [Live-streaming service fees](https://docs.byteplus.com/en/byteplus-media-live/docs/live-streaming-service-fees) for billing details.

* **Storage fee**:

   * If you use **Torch Object Storage (TOS)**  to store time\-shifting content, then the storage fee is charged by TOS.

   * If you use **Storage Space** service ([contact technical support](https://console.byteplus.com/workorder/create) to enable it) to store time\-shifting content, you will be charged based on the following rates.


This section explains how storage fees are calculated:

<span id="3ad1f46b"></span>
## Pricing

The unit price is 0.0008 USD/GB/Day.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Recording and time\-shifting content share the same recording task, so the fee is charged only once.</div>


* <div data-tips="true" data-tips-type="tip">The conversion factor for units of storage is 1,024. For example, 1 GB = 1024 MB.</div>



<span id="130a66d6"></span>
## Billing cycle

Daily pay\-as\-you\-go.

<span id="4e081e71"></span>
## Billing details

Storage fees are calculated by multiplying your daily storage usage by the unit price.

BytePlus MediaLive records the storage usage at 00:00:00 of the next day as the usage for the previous day. For example, if you have 500 GB of time\-shifting content stored at 00:00:00 on January 2nd, this is counted as your storage usage for January 1st.

<span id="299e3ecb"></span>
## Billing example

User A stored 1,000 GB of time\-shifting content on January 1st. On January 2nd, 300 GB of new files were added and 200 GB of old files were removed.

The total storage fee for January 2nd is: (1,000 GB + 300 GB \- 200 GB) × 0.0008 USD/GB/Day = 0.88 USD.
