---
title: "Configuring route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configuring-routes"
---

<span id=".6YWN572uVlBO572R5YWz6Lev55Sx"></span>
## Configure route for VPN gateway


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project and region.

3. Click the name of target VPN gateway to go to the details page.

4. Select the **Routing information** tab and click **Add route**.

5. Refer to the table below to complete the route information.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Type the private CIDR block of the on\-premises data center. |192.168.0.0/24 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select the IPsec\-VPN connection created in the previous phase. |IPsecVPN\-test |
   

6. Click **OK** to complete adding the route entry.

   After the route entry is added, the platform automatically publishes the route to the system route table of the VPC associated with the VPN gateway.


<span id=".6YWN572u5pys5Zyw572R5YWz6Lev55Sx"></span>
## Configure route for on\-premises gateway

Configure the Sangfor firewall in the data center to establish communication with the cloud. For procedure, see [Configuring the Sangfor firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Sangfor_firewall).

Now, you have completed all configurations for the VPN Connect.

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

[Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity)
