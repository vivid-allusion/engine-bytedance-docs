---
title: "Creating an Internet Tunnel Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating-an-Internet-Tunnel-gateway"
---

An Internet Tunnel (IT) Gateway allows an on\-premises data center to access the Internet directly via a Direct Connect (DC) Connection. This topic describes how to create an IT Gateway.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Internet Tunnel Gateway console](https://console.byteplus.com/dc/InternetTunnelGateway).

2. In the top menu bar, select your target region.

3. Click **Create IT Gateway**.

4. Configure parameters for the IT Gateway based on the table below.

   
   |Parameter |Notes |Sample value |
   |---|---|---|
   |Region |Select the region to which the IT Gateway belongs. It is fixed to the current region. To modify the region, exit the creation page and reselect.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select the appropriate region based on your requirements. If the region you select does not support Internet Tunnel, it will automatically redirect to the DC Connection list after selecting the region.</div><br> |China (Beijing) |
   |Name |Set the name for the IT Gateway. |Tunnel\-internet |
   |IPv6 |Specify whether to enable IPv6. Once enabled, it cannot be disabled.<br><br><br>* This parameter appears only after enabling IPv6 for Internet Tunnel.<br><br>* If the IT Gateway does not have IPv6 enabled, its associated IT Virtual Interface also cannot use IPv6.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Internet Tunnel supports only IPv4 by default. IPv6 is currently in the beta stage and is available only after activation. Contact your account manager if needed.</div><br> |Enable |
   

5. Click **Create** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create IT Bandwidth](https://docs.byteplus.com/en/docs/directconnect/Creating-the-internet-bandwidth): Create an IT Bandwidth under an IT Gateway. Adding an IT Gateway to IT Bandwidth enables the data center accesses the Internet via the Internet Tunnel.

* [Create an IT Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-an-Internet-Tunnel-virtual-interface): Create an IT Virtual Interface to connect an IT Gateway with a DC Connection.

* [Apply for an IT Public IP and add it to IT Bandwidth](https://docs.byteplus.com/en/docs/directconnect/Applying-for-an-Internet-Tunnel-address): Apply for an IT Public IP Address to access the Internet, and add this IP to the IT Bandwidth.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateInternetTunnelGateway](https://docs.byteplus.com/en/docs/directconnect/CreateInternetTunnelGateway): Create a new IT Gateway.
