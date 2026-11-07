---
title: "Configuring Internet DNS Lookup for the visualization tool"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/enabling-DNS-tool"
---

Cloud Search allows you to enable Internet DNS Lookup for the private endpoint of the visualization tool. This feature is applicable to development and testing in non\-production environments. Once Internet DNS Lookup is enabled, you can access the visualization tool using the private endpoint over a leased line.

<span id="6089064b"></span>
## Precautions


* Due to the complexity of the internet, we cannot guarantee the accuracy and timeliness of domain name resolution. Therefore, enable Internet DNS Lookup only in **non\-production environments**. We strongly recommend that you use the DNS Forward solution in production environments.

* After enabling Internet DNS Lookup for the private endpoint of the visualization tool, wait for 1 minute before using the resolved endpoint to access the visualization tool.

* Cerebro and Kibana/Dashboards share the Internet DNS Lookup setting. When you enable or disable Internet DNS Lookup, the operation takes effect on both Cerebro and Kibana/Dashboards.


<span id="ef806187"></span>
## Enabling Internet DNS Lookup


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. On the **Instances** page, click the name of the instance.

4. In **Instance management \>**  **Visulization configuration**, click **Enable private network address public network resolution** on the right side of **Private network access address**.

5. In the **Enable public network resolution** dialog box, read and confirm the precautions, then click **OK**.


<span id="67faac34"></span>
## Disabling Internet DNS Lookup

We recommend that you disable Internet DNS Lookup for the visualization tool as soon as possible if you no longer require access to the tool by using the private endpoint over a leased line, due to the complexity of the internet environment.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. In **Instance management \>**  **Visulization configuration**, click **Disable private network address public network resolution** on the right side of **Private network access address**.

4. In the confirmation dialog box, click **OK**.
