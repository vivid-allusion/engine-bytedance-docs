---
title: "Relay"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1"
---

The relaying service allows you to pull content from existing videos or live streams and push it to destination addresses. It can push content to both non\-third\-party and third\-party addresses.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/65bc807-relay_pricing.jpeg) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pulling content from existing videos or live streams is regarded as playing the content, and the third\-party source from which you pull the content might charge you playback fees.</div>



* **Relay to non\-third\-party addresses**: Non\-third\-party addresses use domain names that are added to your account (excluding deleted ones) and have the correct CNAME records configured. You are billed based on the relaying duration if you relay to non\-third\-party addresses. Apart from relaying fees, you also need to pay live\-streaming service fees if the audience pulls the content from the address.

* **Relay to third\-party addresses**: Third\-party addresses use domain names that are not added to your account. You are billed based on the **sum** of relaying duration fee and third\-party relaying bandwidth fee if you relay to third\-party addresses.


<span id="Bill by relaying duration"></span>
## Bill by relaying duration

If you relay to non\-third\-party addresses, the relaying fees are calculated by multiplying the relay task duration by the unit price.

<span id="Pricing"></span>
### Pricing

The unit price is 0.0003 USD/Minute.

<span id="Billing cycle"></span>
### Billing cycle

Billing by relaying duration supports both daily and monthly pay\-as\-you\-go.

<span id="Billing example"></span>
### Billing example

User A started two relay tasks on November 1st.


* Task 1 lasted from 9:00 to 11:00 on November 1st, totaling 120 minutes, which were included in the relay duration of November 1st.

* Task 2 lasted from 23:00, November 1st to 1:00, November 2nd. The first 60 minutes were included in the relay duration of November 1st and the remaining 60 minutes were included in the relay duration of November 2nd.


The relaying fees generated on November 1st would be 0.0003 × (120 + 60) = 0.054 USD.

<span id="Bill by third-party relaying bandwidth"></span>
## Bill by third\-party relaying bandwidth

If you relay to third\-party addresses, apart from being billed by relaying duration, you are also billed by third\-party relaying bandwidth, which is the peak bandwidth consumed when BytePlus MediaLive pushes the content to third\-party addresses.

<span id="Pricing"></span>
### Pricing

The unit price is 1 USD/Mbps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The conversion factor for units of bandwidth is 1,000. For example, 1 Gbps = 1,000 Mbps.</div>


<span id="Billing cycle"></span>
### Billing cycle

Bill by third\-party relaying bandwidth supports both daily and monthly pay\-as\-you\-go.

<span id="Billing example"></span>
### Billing example

User A started two relay tasks on November 1st, both of which pushed the stream to third\-party addresses.


* Task 1 lasted from 9:00 to 11:00, totaling 120 minutes. The peak bandwidth for this period was 500 Mbps.

* Task 2 lasted from 19:00 to 20:00, totaling 60 minutes. The peak bandwidth for this period was 1 Gbps.


The relaying duration was 120 + 60 = 180 minutes, and the peak bandwidth of the day was 1 Gbps, which equals 1,000 Mbps. The relaying fees on November 1st would be 0.0003×180+1×1,000 = 1,000.054 USD.
