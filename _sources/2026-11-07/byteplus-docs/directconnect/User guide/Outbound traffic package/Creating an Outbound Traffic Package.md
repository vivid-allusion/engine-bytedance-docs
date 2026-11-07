---
title: "Creating an Outbound Traffic Package"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating_an_Outbound_Traffic_Package"
---

<span id="OF8Xo0AR"></span>
## Prerequisites


* You have completed real\-name authentication for your account before purchasing resources related to Direct Connect (DC).

* The total value of your account balance (i.e., cash balance) and coupons applicable to DC Gateway must be no less than USD 0. You can recharge your account in advance. 


<span id="GJnC10SH"></span>
## Procedure


1. Log in to the [Outbound Traffic Package console](https://console.byteplus.com/dc/OutboundTrafficPacket).

2. In the top menu bar, select your target region.

3. Click **Create Outbound Traffic Package** and configure the related parameters.

   
   |Parameter |Notes |Example value |
   |---|---|---|
   |Specification |Traffic quota of the Traffic Package. Different validity periods correspond to different specifications. See [Unit prices](https://docs.byteplus.com/en/docs/directconnect/Outbound_Traffic_Package_overview#khaSF9IA) for details. |10 TB |
   |Belongs to Project |Select a project to which the outbound traffic package belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/bandwidthpackage/Managing-projects). To change the project after creation, see [Transfer resource in project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management). |default |
   |Tag |Add one or more custom tags to outbound traffic packages as needed.<br><br>A tag consists of the tag key (Key) and the tag value (Value), and is used to tag the outbound traffic packages for classification and search. For more information, see [Tag management](https://docs.byteplus.com/en/docs/bandwidthpackage/Managing-tags). |dcwg:v1 |
   |Valid period |Currently the outbound traffic package supports only a validity period of one month. |1 month |
   |Effective time |Select a way to effect the outbound traffic package:<br><br><br>* Instant effect (default): Take effect immediately after purchase.<br><br>* Effect at specified time: Take effect at the specified time after purchase. |Effective immediately |
   |Quantity |Quantity of outbound traffic packages that you can purchase. You can apply for up to 99 packages in a single request. |1 |
   

4. Follow the console guidance to review and accept Legal. Click **Buy now**.

5. After confirming the order is correct, click **Next**.

6. Select a payment method and click **Pay ** to complete the action **.** 


<span id="D404F74V"></span>
## Related actions

[Unsubscribe an outbound traffic package](https://docs.byteplus.com/en/docs/directconnect/Managing_an_outbound_traffic_package): Only packages unused within 7 days support unsubscription.
