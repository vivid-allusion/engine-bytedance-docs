---
title: "Configuring a fee payer"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Configuring_a_fee_payer"
---

<span id="bbde7454"></span>
## Scenarios

By default, the network instance attachment fee is charged to the account that owns the network instance. In cross\-account scenarios (where the network instance and Transit Router (TR) belong to different accounts), you can configure a fee payer to have the attachment fee charged to the account that owns the TR instance.

<span id="6bfa4c99"></span>
## Instructions


* You can only configure a fee payer for TR instances within my account. If a TR instance is shared from another account, contact the resource owner (the account that owns the TR instance) to configure it.

* The fee payer configuration takes effect only on newly created network instance attachments. Existing attachments retain their original fee payer settings. To apply the new fee payer to existing attachments, you must delete and [recreate them](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc).


<span id="6f796966"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select the target project and region.

3. Click the name of the target TR instance.

4. Click **Configure fee payer** at the top right of the instance details page.

5. In the pop\-up Configure fee payer dialog box, modify the fee payer.

   * Network instance account: The fee for the cross\-account network instance attachment is charged to the account that owns the network instance.

   * TR owner account: The fee for the cross\-account network instance attachment is charged to the account that owns the TR instance.

6. Click **OK** to complete the action.


<span id="e3b6f843"></span>
### Related documentation

[ModifyTransitRouterAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterAttributes): Modify the fee payer of the network instance attachment.
