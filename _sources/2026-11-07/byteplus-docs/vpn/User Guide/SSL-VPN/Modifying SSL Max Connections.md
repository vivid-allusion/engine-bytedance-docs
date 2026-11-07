---
title: "Modifying SSL Max Connections"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Modifying-the-maximum-number-of-SSL-connections"
---

This topic describes how to modify SSL Max Connections for a VPN gateway. You can adjust this specification based on your business requirements.

<span id=".5pON5L2c6ZmQ5Yi2"></span>
## Limits


* Make sure that the VPN gateway to be modified is in normal status (not expired or suspended) and has no unpaid orders.

* After you modify SSL Max Connections of the VPN gateway, the new specification takes effect immediately. The fee displayed during the modification is the difference between the fee for the new specification and the amount already paid.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Modifying SSL Max Connections may disconnect existing SSL VPN connections. We recommend that you perform this action during off\-peak hours.</strong></div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select a target region and project.

3. Click Modify configuration in Actions column on the right side of the target VPN gateway, or click Modify in Feature configuration column of the target VPN gateway.

4. Enter the Modify VPN gateway configuration page, modify SSL Max Connections for the VPN gateway as needed, and consult and confirm the Legal as guided by the console.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure that the IP quantity under the client IP pool mask in the SSL server created by this VPN gateway is greater than 4 times the modified SSL Max Connections.   </div>
   

5. Click Confirm order to jump to the payment platform for payment. After successful payment, the VPN gateway configuration change is completed. Click Next step to follow the prompts to complete the action.

   After successful payment, the new specification takes effect immediately. In rare cases, there may be a delay in activation due to the network or other causes. Wait patiently for a few minutes. If the change is still not effective, [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=3&Service=VPN&FlowKey=NGhBLLYotsiBMSgHMvCt) to contact the O&M administrator for assistance. The platform will charge or refund based on the actual difference between the new and old configurations. Refer to the Confirm order information page for accurate details.

   * If the payable amount is positive, such as ¥100, it indicates a payment of USD 100. Please follow the platform prompts for payment.

   * If the payable amount is negative, such as \-¥100, it indicates a refund of USD 100. This refund will be credited to your account balance upon order completion.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes): Modify a VPN gateway.
