---
title: "Configuring route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configure_routing"
---

After completing the attachment configuration, you also need to configure routes on the Transit Router (TR) to forward traffic between the on\-premises data center and the IPsec\-VPN connection. This example demonstrates how to configure a static route. For more routing capabilities, see [List of routing features](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx6IO95Yqb)

<span id="AzWq2YQc"></span>
## Configure a static route


1. Log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. Select the **Route Table** tab, select the target route table, and then select the **Route entry** tab.

4. Click **Create static route**, and configure the static route based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Route name |Name of the static route to be created. |Static Route\-IPsecVPN\-test |
   |Destination CIDR |Type the private CIDR block of the on\-premises data center. |192.168.0.0/24 |
   |Blackhole routing |Specify whether the static route to be created is a blackhole route.<br><br><br>* Yes: All traffic pointing to this route will be discarded.<br><br>* No: All traffic pointing to this route will be forwarded to the next hop. This option requires you to specify the next hop for this route. |No |
   |Next Hop type |Select the next hop for this static route. Options: Intra\-region attachment and Inter\-region attachment. |Intra\-region attachment |
   |Next Hop |Select the IPsec\-VPN connection created in the previous phase. |IPsecVPN\-test |
   

6. Click **Create** to complete the action.

   After the route is added, the platform automatically publishes this route to the TR's system route table.


<span id="AzWq2YQc"></span>
## Configure rotue for on\-premises gateway

Configure the Sangfor firewall in the data center to establish communication with the cloud. For procedure, see [Configuring the Sangfor firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Sangfor_firewall).

Now, you have completed all configurations for the VPN Connect.

<span id="ftmdZFSF"></span>
## What to do next

[Test connectivity](https://docs.byteplus.com/en/docs/vpn/Test_connectivity)
