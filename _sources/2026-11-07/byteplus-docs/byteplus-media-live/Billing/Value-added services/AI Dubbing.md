---
title: "AI Dubbing"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing"
---

The AI Dubbing feature integrates advanced technologies such as the Doubao simultaneous interpretation model, multilingual subtitles, voice cloning, and lip sync. This feature can process the human voice in your live stream audio into multilingual content, effectively enhancing the audience's viewing experience in noisy or muted environments, or in cross\-language scenarios, and helping your content reach a broader global audience. This topic introduces the pricing and billing rules for the AI Dubbing feature to help you estimate costs and manage your budget.

<span id="73674ed5"></span>
## Pricing

The unit price for AI Dubbing depends on the features you enable in the task. The system will bill based on the feature with the highest unit price among those you enable. Fees will not be combined. For example, if you enable subtitle translation or source subtitles (lower unit price) and dubbed audio (higher unit price) at the same time, the entire task will be billed uniformly at the unit price for dubbed audio.

The unit prices for each feature are as follows.


|Feature (sorted by unit price from high to low) |Unit price (USD/minute) |
|---|---|
|Lip sync |0.2990 |
|Dubbed audio |0.1118 |
|Subtitle translation or source subtitles only |0.013 |


Based on the above\-mentioned table, you can determine the final unit price using the following rules:


* If the enabled features include lip sync, the unit price is 0.2990 USD per minute.

* If the enabled features do not include lip sync but include dubbed audio, the unit price is 0.1118 USD per minute.

* If the enabled features only include subtitle translation or source subtitles, the unit price is 0.013 USD per minute.


<span id="0a1c92d9"></span>
## Billing rules


* **Billing basis**

   AI Dubbing is billed based on the task's **actual stream push duration**.

   **Example**: You create a task with a relay duration (task's start to end time) of 3 days. If, during these 3 days, the actual stream push duration each day is only 8 hours, the system will ultimately charge for 24 hours (3 days × 8 hours per day).

* **Billing starts and stops**

   Billing starts when the task begins pushing the stream and stops when the task ends pushing the stream.

   * **For demos**

      * **Billing starts**: When you choose the **Web push**, **Upload video**, or **Online address** method to begin the experience.

      * **Billing stops**: When you stop the experience.

   * **For tasks**

      * **Billing starts**: When the task successfully pushes the translated content to your push stream address.

      * **Billing stops**: When the stream pushed to the push stream address is interrupted due to reasons such as task ending, source stream disconnection, and stream pull failure.

* **Detailed rules**

   
   |Item |Description |
   |---|---|
   |Billing formula |AI Dubbing fee = Task's stream push duration (minutes) × unit price (USD/minute) |
   |Measurement method |Accumulated based on the task's actual stream push duration. |
   |Billing cycle |The default billing cycle is daily pay\-as\-you\-go. Fees generated each day will be billed and deducted on the following day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To change the billing cycle to monthly pay\-as\-you\-go, please contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a>.</div><br> |
   


<span id="54385633"></span>
## Billing example

Assume the following scenario:


* **January 1**: Use the **Upload video** method to experience the AI Dubbing demo. Enable **subtitle translation** and **dubbed audio** features, with a total stream push duration of 10 minutes.

* **January 2**: Create a task and enable **subtitle translation**, **dubbed audio**, and **lip sync** features, with a total stream push duration of 200 minutes.


The AI Dubbing fees for these two days are calculated as follows:


* **January 1**

   * **Billing analysis**: Among the features enabled, **dubbed audio** has the highest unit price (0.1118 USD/minute), so the entire task is billed at this unit price.

   * **Fee calculation**: 10 minutes × 0.1118 USD/minute = **1.118 USD**

* **January 2**

   * **Billing analysis**: Among the features enabled, **lip sync** has the highest unit price (0.2990 USD/minute), so the entire task is billed at this unit price.

   * **Fee calculation**: 200 minutes × 0.2990 USD/minute = **59.8 USD**


These two fees will be reflected and deducted in the bills for January 2 and January 3, respectively.
