---
title: "Viewing asset risk information"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Viewing-asset-risk-information"
---

To effectively evaluate and manage the security posture of your network, you can use the asset risk information page. This guide provides detailed instructions on how to view the risk status, security scores, and alert details for all your assets, and explains the methods for handling identified risks.

<span id="ef174f45"></span>
## Handling method descriptions

You can handle asset risks using the following two methods:


* Manual handling: Follow the handling suggestions to resolve the alert, then mark it as handled.

* Add to allowlist: Add the source and destination IP addresses and destination port to the allowlist. After successful configuration, the traffic from the source IP address to the destination IP address and port won't be inspected. Once you add an alert to the allowlist, you can go to **System settings** \> **Allowlist configuration** page to view the added records.


<span id="c9a6a250"></span>
## Risk level descriptions

Asset risk levels are calculated based on factors such as the attack chains, volume, types, and directions of unresolved security alerts from the past 7 days. A lower asset score indicates a more severely compromised host that requires immediate attention.

Different asset security scores correspond to different risk levels. For more information, refer to the table below.


|Score |Level |
|---|---|
|100 |Security |
|75–99 |Low risk |
|50–74 |Moderate risk |
|25–49 |High risk |
|0–24 |Fatal |


<span id="297331e5"></span>
## Prerequisites

Risk detection is already enabled for your assets.

<span id="048c3277"></span>
## Procedure


1. Log in to the NDR console.

2. Select **Threat center** \> **Asset perspective** on the left side of the page.

3. View asset risk information.

   
   |**Parameter** |**Description** |
   |---|---|
   |Asset IP address / instance name |The public IP address and instance name of the asset. |
   |Risk level / score |The current risk level and security score of the asset. It changes dynamically with time and alerts. |
   |Threat detected |Security alerts that occurred on the asset in the last 7 days. |
   |Time of last alert |The time when the last alert occurred on this asset. |
   

4. Click on the asset IP address to open the risky asset details page.

   You can review an overview of security alerts for the asset and handle them.

   * Basic information: Including asset IP address, instance name, risk level, and the number of risky ports.

   * Alert trend: Trend of the number of alerts that occurred on the asset in the last 7 days.

   * Alerts and risks \- Security alerts: Alerts are grouped by alert type and asset IP address. You can view the numbers of alerts of different types that occurred on the assets.

      
      |**Parameter** |**Description** |
      |---|---|
      |Time of last alert |Displays the time of last occurrence of this alert type. Alerts can be sorted by time. |
      |Threat type |Threat name of the security alert. |
      |Attack direction |Including inbound and outbound directions. Inbound attacks are initiated by external attackers against your cloud assets over the internet and often represent entry points for an attack. Outbound attacks are suspicious connections initiated from your cloud assets, often indicating a virus infection or compromise. |
      |Risk level |Displays the risk levels of different alert types, including fatal, high\-risk, medium\-risk, and low\-risk levels. Alerts can be filtered by risk level. |
      |Number of times handled / total number of alerts |The total number of alerts of this type and the number that have been handled. |
      |Handled status |* Not handled: None of the alerts of this type have been handled.<br><br>* Handling: Some, but not all, alerts of this type have been handled.<br><br>* Handled: All alerts of this type have been handled. |
      |Action |Click **Process** to handle the related alerts. |
      

   * Alerts and risks \- Risky ports: Displays all the risky ports of the asset. Exposing high\-risk ports to external access can create an entry point for attacks. Therefore, block unnecessary ports using a cloud firewall or security group to reduce the risk of intrusion.

      
      |**Parameter** |**Description** |
      |---|---|
      |Risky port |The port number that has a security risk. |
      |Suggested fix |The suggested fix provided by NDR. If the recommendation is to close the port, block it promptly using a cloud firewall or a security group. |
      |Protocol |The protocol supported by this port. |
      |Port service |The service provided by this port. |
      |Exploited |Indicates whether this port is under attack. If it has been exploited, it may become an entry point of attacks. |
      |Action |If you need the risky port for external services, add it to the allowlist, and NDR will then stop inspecting traffic to the port. |
