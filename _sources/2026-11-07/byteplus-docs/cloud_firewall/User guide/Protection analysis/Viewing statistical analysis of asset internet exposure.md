---
title: "Viewing statistical analysis of asset internet exposure"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Viewing-statistical-analysis-of-Internet-exposure"
---

Cloud Firewall's internet exposure analysis for assets presents information about assets that are exposed to the internet and their exposed ports, helping you promptly detect and address asset exposure issues and mitigate security risks.

<span id="Prerequisites"></span>
## Prerequisites

You have enabled the firewall for the relevant assets. For more information about how to enable the firewall for an asset, refer to [Enabling internet firewall](https://docs.byteplus.com/docs/cloud_firewall/Enabling-Internet-firewall).

<span id="7a3949b6"></span>
## Steps


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Protection analysis** ＞ **Internet exposure analysis**.

3. You can view the details of internet exposure of your assets and filter the information to display by asset and time.

   * Risk statistics

      * Source IP TOP 5: Displays the IP addresses of sources that access your cloud assets most frequently. You can sort them in ascending or descending order by access count.

      * Opening port TOP 5: Displays the ports that are exposed to the internet most frequently. You can sort them in ascending or descending order by the number of involved assets.

   * Analysis details: The analysis detail list displays the details of your assets' exposure to the internet.

      
      |**Parameter** |**Description** |
      |---|---|
      |Asset |IP address and name of the asset with exposed ports. |
      |Opening port |All of the asset's ports that are exposed to the internet. |
      |Opening protocol |The protocols used for the exposed ports. |
      |Source |IP addresses of the sources that accessed the asset through the internet. |
      |Action |Click **Details** to view the log details. |
