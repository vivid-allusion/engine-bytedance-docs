---
title: "Billing conversion"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Switching-billing-methods"
---

The VPN gateway features billing conversion. You can directly convert a Pay\-as\-you\-go VPN gateway to a Subscription VPN gateway without affecting the other configuration of the VPN gateway and the connectivity of IPsec\-VPN connection.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* When modifying the billing methods of the VPN gateway, it is not supported to simultaneously modify the Bandwidth, IPsec\-VPN connection capability, SSL\-VPN connection capability, and other configurations. To modify the VPN gateway configuration, see [Modifying configuration for a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations).

* The VPN gateway to be changed is neither suspended nor banned. VPN gateways that are already suspended or banned are not supported for metering method change.


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* Only the VPN gateway supports metering method change; IPsec\-VPN connection does not.

* For VPN gateway billing conversion, only converting from Pay\-as\-you\-go to Subscription is supported. Conversion from Subscription to Pay\-as\-you\-go is not supported.

* After the billing conversion for VPN gateway is completed, the start time of the billing cycle for the new billing method (Subscription) is the creation time of the billing conversion order.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click **Convert to Subscription** in the **Actions** column to the right of the target VPN gateway.

4. Select the specific number of months for purchasing a subscription. You can check **Automatic renewal** as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If automatic renewal is enabled, the renewal length is one month and the number of renewals is unlimited. You can manually disable automatic renewal or visit <strong>the Billing center</strong> to modify the number of renewals. For detailed actions, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules">Automatic renewal</a>. For VPN gateways that you rely on for the long term, we recommend checking Automatic renewal to prevent any disruption when they expire.   </div>
   

5. Follow the console guidance to review and accept the legal terms.

6. Click **Confirm order**. After successful payment, the metering method change will be completed.
