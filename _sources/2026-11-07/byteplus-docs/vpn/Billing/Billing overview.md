---
title: "Billing overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Billing-overview"
---

VPN Connect supports two types of connections: IPsec\-VPN and SSL\-VPN. They differ in resources, billing items, and metering methods. Choose the one you need.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923) for your account before purchasing VPN Connect\-related resources.

* To purchase Pay\-as\-you\-go products, ensure that the total value of both the [available balance](https://docs.byteplus.com/en/docs/6269/100429) in your account and the coupon applicable to this product is not less than USD 100.00. The available balance is not less than USD 0.00. To recharge your account, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".6K6h6LS56aG56K-05piO"></span>
## Billing items


|Billing items |Metering method |Billed instance |Description |
|---|---|---|---|
|IPsec\-VPN instances |* Subscription<br><br>* Pay\-as\-you\-go (specification\-based) |VPN gateway |Enabling IPsec\-VPN for a VPN gateway incurs the IPsec\-VPN instance fee on the VPN gateway side. |
|SSL\-VPN instances |* Subscription<br><br>* Pay\-as\-you\-go (specification\-based) |VPN gateway |The VPN gateway enables SSL connection capability and charges the SSL\-VPN instance fee on the VPN gateway side. |
|VPN gateway bandwidth fee |* Subscription<br><br>* Pay\-as\-you\-go (specification\-based) |VPN gateway |Using a VPN gateway, bandwidth fees are charged on the gateway side. |
|SSL specification fee |* Subscription<br><br>* Pay\-as\-you\-go (specification\-based) |VPN gateway |When enabling SSL\-VPN for a VPN gateway, you need to specify the SSL Max Connections. This incurs the SSL specification fee on the VPN gateway side. |
|IPsec\-VPN instance fee |Pay\-as\-you\-go |IPsec\-VPN connection |Associating IPsec\-VPN connections to a TR incurs the IPsec instance fee on the IPsec\-VPN connection side. |
|IPsec traffic fee |Pay\-as\-you\-go |IPsec\-VPN connection |Associating IPsec\-VPN connections to a TR incurs the IPsec traffic fee on the IPsec\-VPN connection side. |
|TR attachment fee |Pay\-as\-you\-go |Transit Router |Associating IPsec\-VPN connections with a Transit Router (TR) incurs the TR attachment fee on the TR side. |
|TR traffic processing fee |Pay\-as\-you\-go |Transit Router |Associating IPsec\-VPN connections to a TR incurs the TR traffic processing fee on the TR side. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic focuses on the billing of VPN gateways and IPsec\-VPN connections. For more information on TR billing, see <a href="https://docs.byteplus.com/en/docs/83472/1223945">Transit Router Billing</a>.</div>


<span id=".5LiN5ZCM572R57uc6L-e5o6l5pa55byP6K6h6LS56K-05piO"></span>
## Billing descriptions for different network connections


|Connection type |Associatable resource |Connection capability of VPN gateway |Billing item |Description |
|---|---|---|---|---|
|IPsec\-VPN |Associate IPsec\-VPN connections to a VPN gateway |Only IPsec\-VPN is enabled |* IPsec\-VPN instances<br><br>* VPN gateway bandwidth fee |Associating IPsec\-VPN connections to a VPN gateway. The IPsec\-VPN instance fee and the VPN gateway bandwidth fee are incurred on the VPN gateway side, while the IPsec\-VPN connection side is exempt. |
|||Both IPsec\-VPN and SSL\-VPN are enabled |* IPsec\-VPN instances<br><br>* SSL\-VPN instances<br><br>* SSL specification fee<br><br>* VPN gateway bandwidth fee ||
||Attach IPsec\-VPN connections to a TR |Not involving VPN gateway |* IPsec\-VPN instance fee<br><br>* IPsec traffic fee<br><br>* Transit Router (TR) attachment fee<br><br>* TR traffic processing fee |* The IPsec instance fee and the IPsec traffic fee are incurred by the IPsec\-VPN connection, and the TR attachment fee and the TR traffic processing fee are incurred by the TR.<br><br>* This article focuses on the fees incurred by the IPsec\-VPN connection. |
|SSL\-VPN |Associate an SSL server to a VPN gateway |Only SSL\-VPN enabled |* SSL\-VPN instances<br><br>* SSL specification fee<br><br>* VPN gateway bandwidth fee |Associating an SSL server to a VPN gateway incurs the SSL\-VPN instance fee and the VPN gateway bandwidth fee on the VPN gateway side. Additionally, the SSL specification fee is charged according to the SSL Max Connections you specified. |
|||Both SSL\-VPN and IPsec\-VPN are enabled |* SSL\-VPN instances<br><br>* IPsec\-VPN instances<br><br>* SSL specification fee<br><br>* VPN gateway bandwidth fee ||


<span id=".6K6h6LS55paH5qGj6K-05piO"></span>
## Billing documentation


|Billing documentation |Description |
|---|---|
|[Billing for VPN gateway](https://docs.byteplus.com/en/docs/vpn/VPN-gateway-billing) |This topic describesbilling details of the VPN gateway, including billing items, metering methods, unit prices, billing formulas, and billing examples. |
|[Billing for IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/IPsec-VPN-connection-billing) |This topic describesbilling details of the IPsec\-VPN connection, including billing items, metering methods, unit prices, billing formulas, and billing examples. |
|[Specification change](https://docs.byteplus.com/en/docs/vpn/Upgrade-and-downgrade) |This topic describesthe procedures and limits when modifying VPN gateway configurations, including bandwidth, connections, and others. |
|[Expiration](https://docs.byteplus.com/en/docs/vpn/Expiration) |This topic outlines next steps for subscribed resources after expiration:<br><br>\- Resource status at different post\-expiration times<br><br>\- Unsubscription types (pre\- or post\-expiration) and corresponding actions<br><br>\- Renewal types (manual or automatic) and related actions<br><br> |
|[Arrears](https://docs.byteplus.com/en/docs/vpn/Arrears) |This topic describeshow the status of a resource in pay\-as\-you\-go mode changes and what limits are imposed on the resource after an overdue payment. |
