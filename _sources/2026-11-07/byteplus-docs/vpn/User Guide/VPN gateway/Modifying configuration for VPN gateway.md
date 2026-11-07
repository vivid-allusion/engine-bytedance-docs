---
title: "Modifying configuration for VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations"
---

This topic describes how to modify the Bandwidth, connection capability, and other configurations of a VPN gateway. If the current Bandwidth, connection capability, or SSL Max Connections of the VPN gateway no longer meet your business needs, you can modify its configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>This notice is very important. Ignoring it may impact your business: Make sure to thoroughly read all the contents in </strong><a href="https://docs.byteplus.com/en/docs/vpn/Upgrade-and-downgrade"><strong>Specification change</strong></a><strong> before changing the VPN gateway configuration. You should fully assess the impact on your business, and choose an appropriate time to perform the actions.</strong></div>


<span id=".5L-u5pS56YWN572u5L-h5oGv"></span>
## Modify configuration


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click **Modify configuration** in the **Actions** column on the right side of the  target VPN gateway.

4. Change the VPN gateway configuration according to your actual needs.

   
   |Parameter |Description |
   |---|---|
   |Bandwidth |Select a Bandwidth that suits your business requirements. |
   |IPsec\-VPN capability |Adjust the status of the IPsec\-VPN capability. Once this capability is enabled, the VPN gateway supports IPsec\-VPN connections.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Dual\-tunnel VPN gateways currently do not support disabling IPsec\-VPN capability.</div><br> |
   |SSL\-VPN capability |Adjust the status of SSL Max Connections. Once enabled, this VPN gateway supports SSL\-VPN.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Dual\-tunnel VPN gateways do not support SSL\-VPN capability.</div><br> |
   |SSL Max Connections |This argument appears only if you enable the SSL\-VPN capability. Select the maximum number of clients that an SSL\-VPN connection can connect at the same time. **Ensure that the number of IPs under the client IP pool mask in the SSL server created by this VPN gateway is greater than four times the modified SSL Max Connections**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Modifying SSL Max Connections may disconnect existing SSL\-VPN connections in a few seconds. We recommend that you perform this action during off\-peak hours.</div><br> |
   |Agreement |Follow the console guidance to review and accept the legal terms. |
   

5. Complete the modification. Click **Submit**, and follow the prompts on the interface to complete the operation.

   * Pay\-as\-you\-go: Click **Confirm order** to complete the VPN gateway configuration modification.

   * Subscription: Click **Confirm order** to redirect to the payment platform. After successful payment, the VPN gateway configuration change is completed.

      If the modification does not take effect in 1 minute, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=3&Service=VPN&FlowKey=NGhBLLYotsiBMSgHMvCt).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The platform will charge or refund based on the actual difference between the new and old configurations. Please refer to the Confirm order information page for accurate details.</div>



* <div data-tips="true" data-tips-type="tip">If the payable amount is positive, such as ¥100, it indicates a payment of USD 100. Please follow the platform prompts for payment.</div>


* <div data-tips="true" data-tips-type="tip">If the payable amount is negative, such as \-¥100, it indicates a refund of USD 100. This refund will be credited to your account balance upon order completion.</div>



<span id=".5re75YqgQkdQIEFTTg=="></span>
## Add BGP ASN


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. In the VPN gateway list, click the edit icon in BGP ASN column of target VPN gateway.

4. Type the ASN of the VPN gateway in the text box and click Save to complete the modification.

   * Only VPN gateways without a configured BGP ASN can add a BGP ASN. Modifications on BGP ASN are not supported for configured VPN gateways.

   * The valid range for BGP ASN is: 64512 to 65534, and 4200000000 to 4294967294.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes): Modify attributes for a VPN gateway.
