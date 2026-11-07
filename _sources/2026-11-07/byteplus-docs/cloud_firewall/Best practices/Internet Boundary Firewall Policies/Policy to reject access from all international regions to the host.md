---
title: "Policy to reject access from all international regions to the host"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Policy_to_reject_access_from_all_international_regions_to_the_host"
---

This article describes how to configure ingress policy settings, allowing only domestic internet IPs to access cloud services.


---



<span id="e3b57b67"></span>
# Example scenario

The EIP bound to ECS (host) is `180.100.1.1/32`, and it is necessary to reject all access from international regions. By default, the cloud firewall allows all traffic when no policies are configured, so in this scenario, a high\-priority policy to block access from international region IPs needs to be configured.

<span id="40a9f6af"></span>
# Steps


1. Log in to [the cloud firewall console](https://console.byteplus.com/firewall/overview).

2. **Add blocking policy**

   1. In the left navigation bar, select **Access Control \> Internet Boundary**. On the **Inbound Rules** tab, click **Add**.

   2. Add a high\-priority blocking policy to block traffic from international region IPs to this host.



|**Configuration item** |**Configuration description** |**Configuration parameters** |
|---|---|---|
|**Rule priority** |Select the priority of this strategy; here, choose the highest priority. After configuration is complete, you can also click **move** in the access control policy list to customize the strategy priority adjustment.<br><br><br>* **Highest priority**: refers to the highest priority at which the access control policy takes effect, taking effect first.<br><br>* **Lowest priority**: refers to the lowest priority at which the access control policy takes effect, taking effect last. |Highest priority |
|**Access source type** |You need to select the access source type and enter the access source address according to the access source type. Here select **Region** type and enter **International Region**, blocking the international region from accessing host `180.100.1.1/32`.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **Address Book** type, you need to create an IP address book in advance.<br><br>* When selecting **Region** type, you need to select the region where the source address is located. Select domestic areas or international areas. |Region |
|**Access source** ||International region |
|**Access purpose type** |You need to select the type of access purpose and input the access purpose address according to it. Select IP type here and enter `180.100.1.1/32`.<br><br><br>* When selecting **IP** type, you need to enter an IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting the **address book** type, you need to create the IP address book in advance. |IP |
|**Access purpose** ||180.100.1.1/32 |
|**Protocol type** |Transmission layer protocol type, supports setting to: **TCP**, **UDP**, **ICMP**, **ANY**. If unsure about the specific agreement, you can choose **ANY.**  |ANY |
|**Action** |Set the traffic release status for matching success in this policy.<br><br><br>* **Permit**: Allow this traffic, access control logs will not be recorded, only traffic logs will be recorded.<br><br>* **Block**: Intercept this traffic, block logs will be recorded in the access control logs.<br><br>* **Monitor**: Allow this traffic. Block logs will be recorded in the access control logs. |Block |
|**Description** |Input the current strategy content and usage scenarios. Facilitates your identification and application of the address book. | |
|**Policy switch** |Set the policy switch. If you did not enable the strategy when creating it, you can enable the strategy in the strategy list. |Keep it enabled |
