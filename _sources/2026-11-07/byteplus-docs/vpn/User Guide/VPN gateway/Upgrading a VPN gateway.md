---
title: "Upgrading a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway"
---

The VPN gateway supports self\-service upgrades. After a new version is released, you can choose an inactive time based on your situation to perform a self\-service VPN gateway upgrade. After the upgrade, the VPN gateway updates to the latest version, allowing you to experience more new features.

<span id=".5Y2H57qn6K-05piO"></span>
## Upgrade description


* Upgrading the major version of a VPN gateway (such as from 4.0 to 5.0) takes approximately 10 minutes. During the upgrade, the VPN gateway will not provide services and existing connections will be interrupted. It is recommended that you upgrade during off\-peak hours.

* If a minor version is released, the system automatically updates the previous VPN gateway version (such as 5.0) to the latest version (such as 5.1). The upgrade process does not affect your business.

* The tunnel mode of the VPN gateway remains unchanged before and after the upgrade.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click on the name of the target VPN gateway to enter the details page.

4. In the prompt box, click **Upgrade now**.

   * If there is no prompt similar to the image below, it means the current version is the latest and does not require an upgrade.

   * VPN gateways with versions that are too low do not support the upgrade operation. To use the latest VPN gateway features, delete and recreate the VPN gateway.

5. In the pop\-up prompt dialog box, assess the potential impact of the upgrade and click **Upgrade now** to start the upgrade.

   The upgrade takes some time, wait patiently.
