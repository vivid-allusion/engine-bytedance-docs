---
title: "Policy that only allows the host to access specified domain names (outbound direction)"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Policies_allowing_only_the_host_to_access_a_specified_domain"
---

This article describes how to configure outbound policy settings, allowing only the business to access the domain `console.volcengine.com`.


---



<span id="deb908ca"></span>
# Example scenario

The EIP bound to the ECS (host) is `180.100.1.1/32`, and it is necessary to set it so that the host can only access the domain `console.volcengine.com`. Cloud firewall allows all traffic by default when no policies are configured, so in this scenario, it is necessary to configure 2 access policies. One is a high\-priority allow policy, permitting the host to access the domain `console.volcengine.com`; the other is a low\-priority deny policy, blocking all outbound traffic from the host.

<span id="f6144bef"></span>
# Procedure


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. **Add Allow Policy**:

   1. In the left navigation bar, select **Access Control \> Internet Boundary**. On the **Outbound Rules** tab, click **Add.** 

   2. Add a high\-priority allow rule to allow this host to access traffic to the domain `console.volcengine.com`.



|**Configuration item** |**Configuration description** |**Configuration parameter** |
|---|---|---|
|**Rule priority** |Select the priority of this policy, here choose the highest priority. After configuration, you can also click **Move** in the access control policy list to customize the priority of the policy.<br><br><br>* **Highest priority**: Refers to the highest priority at which the access control policy takes effect, taking effect first.<br><br>* **Lowest priority**: Refers to the lowest priority at which the access control policy takes effect, taking effect last. |Highest priority |
|**Access source type** |You need to select the access source type and enter the access source address based on the access source type. Select IP type here and enter `180.100.1.1/32`, host `180.100.1.1/32` can access external domain names.<br><br><br>* When selecting **IP** type, you need to enter an IP address or an IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create an IP address book in advance. |IP |
|**Access Source** ||180.100.1.1/32 |
|**Access purpose type** |You need to select the destination type of access and enter the access destination address based on the destination type. Select the domain `type` and enter <a i=1\>console.volcengine.com</a\>. The host can access this domain.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **domain** type, you need to enter the destination domain address.<br><br>   * You can enter a single domain `example.com`, wildcard domain `*.example.com`, multi\-level domain `example1.example2.com`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please do not enter protocol content such as http(s).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The principle of domain access empty policy is based on the Host information in HTTP protocol data and the Server Name information in the Client Hello of HTTPS protocol data packets to obtain domain data for matching control. If your business traffic packets do not contain these two fields, the domain policy cannot take effect.   </div><br>   <br><br>* When selecting **address book** type, you need to create an IP address book in advance.<br><br>* When selecting **region** type, you need to choose the region where the source address is located. Optional Chinese regions or international regions. |Domain name. |
|**Access Destination** ||console.volcengine.com |
|**Protocol type** |The transport layer protocol type and domain access control policy only apply to **HTTP** and **HTTPS** protocols, so the default setting is **TCP** protocol. |TCP |
|**Destination port type** |Set the destination port type and destination port. Select port 0/65535 or 80, 443 here.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Domain access control policy only takes effect for <strong>HTTP</strong> and <strong>HTTPS</strong> protocols, please ensure the protocol corresponding to the destination port is HTTP or <strong>HTTPS</strong> protocol.</div><br><br><br>* When selecting **port** type, you need to enter the port or port range, such as 22, 80/88, 0/65535.<br><br>* **Address book**: When selecting **address book** type, you need to create the port address book in advance. |Port |
|**Destination Port** ||0/65535 |
|**Action** |Set the release status of successfully matched traffic in this policy.<br><br><br>* **Release**: Release this traffic, access control logs will not be recorded, only traffic logs will be recorded.<br><br>* **Block**: Intercept this traffic, and block logs will be recorded in the access control logs.<br><br>* **Observe**: Release this traffic. Block logs will be recorded in the access control logs. |Release |
|**Description** |Enter the current policy content and usage scenarios. Facilitate your identification and application of the address book. |Domain Whitelisting Policy for console.volcengine.com |
|**Policy switch** |Set the Policy switch. If you did not enable the policy when creating it, you can turn on the policy in the policy list. |Keep it enabled |



3. **Add Block Policy**:

   1. In the left navigation bar, select **Access Control \> Internet Boundary**. In the **Outbound Rules** tab, click **Add.** 

   2. Add a low\-priority block rule to block all traffic from this host to the external network.

   
   |**Configuration item** |**Configuration Parameter** |
   |---|---|
   |**Rule priority** |Lowest priority |
   |**Access source type** |IP |
   |**Access source** |180.100.1.1/32 |
   |**Access purpose type** |IP |
   |**Access destination** |0.0.0.0/0 |
   |**Protocol type** |ANY |
   |**Action** |Block |
   |**Description** |Prohibit active access to the public network. |
   |**Policy switch** |Keep it enabled |
