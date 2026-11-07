---
title: "Set remaining amount alert"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/set-remaining-amount-alert"
---

<span id="okd8JHld"></span>
# Set remaining amount alert

You can set up remaining amount alert notifications on the [Savings plans page of the Billing Center](https://console.byteplus.com/finance/saving-plan).

<span id="nfmzGaT3"></span>
# Alert rules


1. For diminishing savings plans, the platform sends a notification when the remaining amount is below the threshold.

2. For periodic savings plans, if the commitment term is yearly/monthly/daily, a notification will be sent once per commitment term when the remaining amount is below the threshold. For those commitment terms are hourly, the notification is not supported.

3. The alert is turned on by default after purchasing, and the threshold is set to 20 percent.Notifications will no longer be sent after closing. You can goto the [Message Center](https://console.byteplus.com/message/setting) to set up receiving channels (message type is 'Billing Notifications').

4. If a new purchase, modification, or unsubscription changes the total amount of savings plans,the system will reset the remaining amount alert (the threshold ratio remains the same).


<span id="pBUtOpF5"></span>
# Operating steps


1. Open the [Savings Plans](https://console.byteplus.com/finance/saving-plan) page and click the 'Set alert' button.

2. Select product and configuration name requiring setup. Set the alert status to 'Enabled' (blue indicates enabled, gray indicates disabled). The default threshold ratio is 20%, adjustable between 5% and 50% as needed (in 5% increments).

3. You may also choose to perform batch settings by enabling/disabling 'Manage quota alerts in bulk' and configuring the 'Set quota threshold percentage in bulk' value. This will apply to all products and configurations without requiring individual adjustments.

4. After completing the settings, click 'OK' to finalize the changes; clicking 'Cancel' will discard the modifications.
