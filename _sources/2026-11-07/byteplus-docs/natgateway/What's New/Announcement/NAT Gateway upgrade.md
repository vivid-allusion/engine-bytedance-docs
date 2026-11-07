---
title: "NAT Gateway upgrade"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/NAT_Gateway_upgrade"
---

Dear BytePlus users, to further enhance network performance, the BytePlus NAT Gateway service will undergo a progressive underlying architecture upgrade starting from **November 5, 2025 (UTC+8)** . After the upgrade, NAT Gateway will deliver **higher stability, greater resource elasticity**, and **stronger security capabilities,**  continuing to offer you a stable and high\-quality network service.

<span id="wm51SlO8"></span>
## Upgrade notes


* This upgrade covers **Internet NAT Gateway** and **VPC NAT Gateway** in all released regions.

* This is **an online hot upgrade**, ensuring zero impact on the availability and network connectivity of your existing NAT gateways. We will perform the upgrade on existing instances progressively in the background. You will receive an advance notification with the specific schedule via internal message. Please check your inbox for this update.

* Your NAT gateway's configuration and billing will stay the same after the upgrade. No action is needed on your part.

* The Pay\-by\-specification/Subscription instances do not feature auto\-scaling. To enable elasticity, please select Pay\-by\-CU for billing.


<span id="VETJkM1u"></span>
## Feature upgrade

With the upgraded NAT Gateway, you'll benefit from the following improvements:


* **Elastic architecture**

   Built on distributed elastic architecture, the NAT gateway dynamically adjusts capacity based on traffic, delivering consistent performance and reliability during peak periods. New instances support Pay\-by\-CU, achieving higher resource utilization and cost transparency.

* **Flexible management**

   Internet NAT Gateway features a new IP assignment mode, allowing each elastic IP address (EIP) to be configured with a separate private address, easily adapting to complex network architectures. Additionally, it supports configuring smart scheduling for gateway traffic and setting limits on metrics such as bandwidth and max connections per IP, enabling precise cost and performance control.

* **Security Audit**

   Internet NAT Gateway supports session logging. After enabling, SNAT session information is automatically delivered to Torch Log Service (TLS) for security analysis and compliance auditing.

* **Traffic Control**

   The system will automatically enable the network ACL traffic control function for your newly created instances. Subnet ACL rules will apply to inbound and outbound traffic of the NAT gateway, enabling traffic access governance and security protection.


<span id="XGj4IBO5"></span>
## Contact us

For any questions, please [submit a ticket](https://console.byteplus.com/workorder/create) or contact your account manager.
