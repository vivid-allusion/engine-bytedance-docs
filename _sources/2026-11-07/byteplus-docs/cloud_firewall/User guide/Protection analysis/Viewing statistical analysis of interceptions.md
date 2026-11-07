---
title: "Viewing statistical analysis of interceptions"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Viewing_statistical_analysis_of_interceptions"
---

On the **Interception analysis** page in Cloud Firewall, you can find details of all the intercepted outbound and inbound traffic. With this information, you can further find, from the related logs, source IP addresses, source ports, destination IP addresses, destination ports, protocols, and other information.

<span id="Prerequisites"></span>
## Prerequisites


* You have enabled the firewall for the relevant assets. For more information about how to enable the firewall for an asset, refer to Enabling the internet firewall.

* You have configured access control policies for inbound or outbound traffic. For more information about how to configure an access control policy, refer to Configuring an internal firewall access policy.


<span id="cb423beb"></span>
## Viewing statistical analysis of interceptions of inbound traffic


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Protection analysis** \> **Interception analysis.** 

3. Click the **Inbound** tab to view the details of intercepted inbound traffic. You can filter the information by asset, time, and risk level.

   * **Blocked external IP address TOP5**: The top 5 most intercepted external IP addresses.

   * **Protected assets TOP5**: The top 5 most frequently accessed internal assets by external IP addresses.

   * **Rule hits TOP5**: The top 5 most\-hit policies, excluding those that have been deleted.

   * **Blocked times**: A chart displays trends in the interceptions of external IP addresses by Cloud Firewall.


<span id="8f5e30b5"></span>
## Viewing statistical analysis of interceptions of outbound traffic


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Protection analysis**  **\> Interception analysis**.

3. Click the **Outbound** tab to view the details of intercepted outbound traffic. You can filter the information by asset, time, and risk level.

   * **Unexpected IP TOP5**: The top 5 most accessed external IP addresses.

   * **Source asset TOP5**: The top 5 internal assets with the most outbound connections.

   * **Rule hits TOP5**: The top 5 most\-hit policies, excluding those that have been deleted.

   * **Blocked times**: A chart displays trends in the interceptions of outbound connections from internal assets by Cloud Firewall.


<span id="068531b0"></span>
## Optional action

Hover the cursor over the trend chart to view details of the interception counts. Click **Details** to view the corresponding logs.
