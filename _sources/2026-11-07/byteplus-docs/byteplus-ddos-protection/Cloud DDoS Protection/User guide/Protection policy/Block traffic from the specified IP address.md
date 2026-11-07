---
title: "Block traffic from the specified IP address"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Block_traffic_from_the_specified_IP_address"
---

The IP blocklist is an access control feature for DDoS protection that allows you to block traffic from specific IP addresses, providing precise control over your traffic sources. It is particularly useful for proactively blocking known malicious IPs or for emergency response during an active DDoS attack. This document will guide you through the steps to configure IP blocklists in the DDoS protection system.

<span id="54e0c52d"></span>
## **Applicable scenarios**


* **Blocking attack sources**: Add the IP addresses of known malicious attackers to the blocklist to deny them access.

* **Emergency blocking**: During a DDoS attack, block the IP addresses that are the source of the attack traffic.


<span id="9089e55b"></span>
## **Important notes**


* **Trigger mechanism**: When the Cloud DDoS Protection instance detects an attack, it intercepts request traffic from any IP address on the blocklist.

* **Execution priority**: Cloud DDoS Protection first applies the IP allowlist policy when detecting traffic, followed by the IP blocklist policy. If an IP address is simultaneously added to both the IP allowlist and the IP blocklist, Cloud DDoS Protection will apply the allowlist rule first to ensure that access requests from that IP address are allowed.

* **IP address limits per rule group**:

   
   |Rule type |Maximum number of IPv4 addresses |Maximum number of IPv6 addresses |
   |---|---|---|
   |IP allowlist |1000 |20 |
   |IP blocklist |1000 |20 |
   


<span id="42d26a35"></span>
## Prerequisites

You have purchased and activated the Cloud DDoS Protection service. For instructions, see [Step 1: Create a Cloud DDoS Protection instance](https://docs.byteplus.com/docs/byteplus-ddos-protection/Get_started_with_Cloud_DDoS_Protection#f147827f).

<span id="8cb9dc21"></span>
## Steps


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select  **Cloud DDoS Protection** ** \> ** **Protection policy**.

3. From the protection policy list, find your target rule group. To open its settings, click the rule group's name or click **Set rules** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d4128bdd43940f5ab94402e70d5f3a0) </span>


&nbsp;


&nbsp;

4. Select **IP blocklist**, and click ** Add IP Blocklist**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8589c31e5158483a91c29d7291a47f78) </span>

5. Enter the IP addresses or CIDR blocks to block.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This feature supports IPv4 and IPv6 addresses.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Separate multiple IP addresses or CIDR blocks with spaces or line breaks.   </div>
   

   The following are formatting examples:

   * Single IP address: `192.0.2.1` or `2001:db8:85a3::8a2e:370:7334`

   * Single CIDR block: `192.168.1.1/24` or `2001:db8:85a3::/48`

   * Multiple IP addresses/CIDR blocks:

      ```Bash
      # Separate with spaces
      192.168.1.1 192.168.1.2
      
      # Separate with line breaks
      192.168.1.1
      192.168.1.2
      ```
      

6. Click **OK**.


<span id="8bb27d27"></span>
## Related operations


* **Download**: Select the target blocklist, then click the download icon above the list to save the list as a `CSV` file.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/de4364ac1e4a43d8b2c3c109afe2ac5c) </span>

* **Delete**: Select the target blocklist, then click **Batch delete** below the list.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend downloading a backup before deletion.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d9ae3ea834284439b66cfefddd9da646) </span>
