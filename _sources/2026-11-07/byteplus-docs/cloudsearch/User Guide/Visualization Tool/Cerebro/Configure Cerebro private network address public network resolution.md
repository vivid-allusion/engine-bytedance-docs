---
title: "Configure Cerebro private network address public network resolution"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configuring-DNS-Cerebro"
---

Cloud Search supports enabling public network resolution for the private network address of visualization tools to meet development and testing needs in non\-production environments. After enabling public network resolution, users can access the private network address via dedicated lines.

<span id="e15e89ac"></span>
## Precautions


* Due to the complexity of the public network environment, accuracy and timeliness of domain name resolution cannot be guaranteed. Therefore, public network resolution is limited to non\-production environments. For production environments, it is strongly recommended to use the DNS Forward solution.

* Cerebro and Kibana/Dashboards share one public network resolution. Enabling or disabling public network resolution applies to both simultaneously.

* After successfully enabling public network resolution, wait 1 minute before using the resolved visualization tool address.


<span id="cbb3ef35"></span>
## Enable public network resolution


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation pane, select **Instance management \> Visulization configuration**, then on the **Cerebro** card, click **Enable public resolution of private address** behind the **Private network access address**.

5. In the **Enable public network resolution** dialog, review the precautions, confirm, and then click **OK**.


<span id="2615de8c"></span>
## Disable public network resolution

Considering the complexity of the public network environment, it is recommended to disable the public network resolution of the visualization tool as soon as possible after enabling it and completing the dedicated line access requirements.


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. At the top navigation bar, select the region where the target instance is located.

3. On the **Instances** page, click the target instance name.

4. In the left navigation pane, select **Instance management \> Visulization configuration**, then on the **Cerebro** card, click **Disable public resolution of private address** behind the **Private network access address**.

5. In the **Confirm disable public network resolution** dialog, click **OK**.
