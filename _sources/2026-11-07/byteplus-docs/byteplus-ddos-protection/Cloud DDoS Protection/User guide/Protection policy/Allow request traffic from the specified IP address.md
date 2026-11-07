---
title: "Allow request traffic from the specified IP address"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Allow_request_traffic_from_the_specified_IP_address"
---

To ensure traffic from trusted sources is always allowed and not mistakenly blocked by security policies, you can configure an IP allowlist for your Cloud DDoS Protection instance. This guide provides step\-by\-step instructions on adding specific IP addresses or CIDR blocks to the allowlist, ensuring stable access for internal services, administrators, or authorized proxy services.

<span id="54e0c52d"></span>
## **Applicable scenarios**


* **Authorize internal access**: Allow access from static IP addresses used by your corporate intranet, VPN, or administrators to ensure reliable connectivity.

* **Allow traffic from proxy services**: In scenarios that use proxy services like a CDN, add the proxy service's IP addresses to the allowlist to ensure uninterrupted service and prevent them from being incorrectly blocked by security policies.


<span id="9089e55b"></span>
## **Notifications**


* **Execution priority**: Cloud DDoS Protection first evaluates the IP allowlist policy when processing traffic, followed by the IP blocklist policy. If an IP address is on both the allowlist and the blocklist, the allowlist rule takes precedence, and traffic from that IP is allowed.

* **IP address limits per rule group** 

   
   |Rule type |Maximum number of IPv4 addresses |Maximum number of IPv6 addresses |
   |---|---|---|
   |IP allowlist |1000 |20 |
   |IP blocklist |1000 |20 |
   


<span id="42d26a35"></span>
## Prerequisites

You have purchased and activated the Cloud DDoS Protection service. For instructions, refer to [Step 1: Create a Cloud DDoS Protection instance](https://docs.byteplus.com/docs/byteplus-ddos-protection/Get_started_with_Cloud_DDoS_Protection#f147827f).

<span id="89158056"></span>
## **Steps**


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select  **Cloud DDoS Protection** ** \> ** **Protection policy**.

3. From the protection policy list, find your target rule group. To open its settings, click the rule group's name or click **Set rules** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d4128bdd43940f5ab94402e70d5f3a0) </span>


&nbsp;


&nbsp;

4. Select **IP allowlist** and click **Add IP allowlist**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2674b14028d248f18e480098510b72f6) </span>

5. Enter the IP addresses or CIDR blocks to allow.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The allowlist supports both IPv4 and IPv6 addresses.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Separate multiple IP addresses or CIDR blocks with spaces or line breaks.   </div>
   

   The following are formatting examples:

   * Single IP address: `192.168.1.1` or `2001:db8:85a3::8a2e:370:7334`

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


<span id="8cb9dc21"></span>
## Related operations


* **Download**: Select one or more entries in the allowlist, then click the download icon to export them as a `CSV` file.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/22f9c273fd3447b1b84fecfa22da7a77) </span>

* **Delete**: Select the IP addresses to delete, and then click **Batch Delete** below the list.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend downloading a backup before deleting the entries.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/19a9b744f56441aaa95535d409590968) </span>


&nbsp;

&nbsp;
