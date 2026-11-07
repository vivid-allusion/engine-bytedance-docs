---
title: "Configure Cerebro private network address public network resolution"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_private_network_address_public_network_resolution"
---

The Cloud Search service supports enabling public network resolution for Cerebro private network addresses to meet users' special scenarios such as development and testing in non\-production environments. After enabling public network resolution, users can access via private network addresses through dedicated lines.

<span id="degRlvZ9"></span>
## Precautions


* Due to the complexity of the public network environment, the accuracy and timeliness of domain name resolution cannot be guaranteed; therefore, enabling public network resolution is limited to non\-production environments only. For production environments, it is strongly recommended to use the DNS Forward solution.

* After enabling public network resolution successfully, wait 1 minute before using the resolved Cerebro address.


<span id="nhvylCYs"></span>
## Enable public network resolution


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **Cerebro**, then click **Enable public resolution of private address** next to the **Private network access address**.

4. In the **enable public network resolution** dialog, review the precautions, confirm, and then click **OK**.


<span id="Wajugewa"></span>
## Disable public network resolution

Considering the complexity of the public network environment, it is recommended to disable the visual tool’s public network resolution as soon as possible after enabling public network resolution and completing dedicated line access requirements.


5. Log on to the [Cloud Search console](https://console.byteplus.com/es).

6. In the top navigation bar, select the target project and region.

7. In the left navigation bar, select **Cerebro**, then click **Disable public resolution of private address** after the **Private network access address**.

8. In the confirmation dialog for disabling public network resolution, click **OK**.
