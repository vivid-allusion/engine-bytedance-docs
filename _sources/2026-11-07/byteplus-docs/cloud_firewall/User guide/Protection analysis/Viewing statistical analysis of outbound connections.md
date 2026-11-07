---
title: "Viewing statistical analysis of outbound connections"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Viewing_statistical_analysis_of_outbound_connections"
---

An outbound connection occurs when your host accesses an external domain or IP address. Once activated, Cloud Firewall's outbound connection analysis actively monitors the outbound connections of your hosts and detects potentially malicious activities. With the insights provided by Cloud Firewall, you can take appropriate measures, such as restricting outbound connections and blocking IP addresses, to prevent servers from becoming part of a botnet or engaging in external attacks or internal intrusions.

<span id="Prerequisites"></span>
## Prerequisites

You have enabled the firewall for the relevant assets. For more information about how to enable the firewall for an asset, refer to [Enabling the internet firewall](https://docs.byteplus.com/en/docs/99/1249437).

<span id="viewing-statistical-analysis-of-accessed-domains"></span>
## Viewing statistical analysis of accessed domains

**Outbound domains** are external domains that are accessed by your hosts. You can view the total number of accessed domains, their traffic size, and their access count on the **Outbound domains** page.


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Protection analysis** ＞ **Outbound analysis**.

3. Click the **Outbound domains** tab to view the details of the accessed external domains. You can filter the information to display by asset and time.

   * Overview: Displays the total number of accessed domains and the number of those that pose a risk.

   * Outbound connection domain TOP5: Displays the top 5 most accessed domains and their access counts.

   * Outbound connection domain lists: Displays the details of the accessed domains. You can filter the list by domain.

      
      |**Parameter** |**Description** |
      |---|---|
      |Domain name |Displays information of the accessed domain. It can be the domain of the website or an IP address associated with that domain. |
      |My assets |Displays the information of the host asset that initiates the outbound connection, including its IP address and name. |
      |Access times |Displays the number of times the asset under the current account accessed the domain. |
      |Access time |Displays the first and the last time when the asset accessed the domain. |
      |Actions |Click **Details** to view the traffic logs of the asset. |
      


<span id="Accessed IP addresses"></span>
## Viewing statistical analysis of accessed IP addresses

**Outbound IP** Address are external IP addresses that are accessed by your hosts. You can view the total number of accessed IP addresses, their port, and their access count on the **Outbound IP** page.


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Protection analysis** ＞ **Outbound analysis**.

3. Click the **Outbound IP** tab to view the details of the accessed IP addresses. You can filter the information to display by asset and time.

   * Overview: Displays the total number of accessed IP addresses and the number of those that pose a risk.

   * Outbound IP address TOP5: Displays the top 5 most accessed IP addresses and their access counts.

   * Outbound IP address lists: Displays the details of the IP addresses. You can filter the list by domain.

      
      |**Parameter** |**Description** |
      |---|---|
      |Outbound IP address |IP address of the accessed destination. |
      |External port |Port of the accessed destination. |
      |My assets |Displays the information of the host asset that initiates the outbound connection, including its IP address and name. |
      |Access times |Displays the number of times the asset under the current account accessed the domain. |
      |Access time |Displays the first and the last time when the asset accessed the domain. |
      |Actions |Click **Details** to view the traffic logs of the asset. |
