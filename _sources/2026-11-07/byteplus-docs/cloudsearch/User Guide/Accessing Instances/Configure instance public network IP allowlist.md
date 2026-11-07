---
title: "Configure instance public network IP allowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/public-IPallowlist-for-instance"
---

When enabling public network access for a Cloud Search service instance, it already includes the action to configure the public IP allowlist. This allows you to specify the public IP addresses permitted to access the instance. You can reconfigure the public IP allowlist as needed later. This topic explains how to configure the instance public network IP allowlist.

<span id="463eb5c9"></span>
## Precautions

When configuring the IP allowlist, you can specify a single IP address or an IP network segment. Please follow the format requirements below:


* IP address format: Must be a valid IPv4 address consisting of four integers from 0 to 255, separated by periods (.).

* CIDR segment: Must be in standard format, with the IP and mask matching.

   * The IP part must be the network address, the first address in the subnet; all host bits must be zero.

   * The network prefix length range is `0~32`. `/0` is valid, representing the entire IPv4 address space (`0.0.0.0/0`); `/32` denotes a single host address.

   * Reserved IP ranges such as the loopback address `127.0.0.0/8` are not allowed.

   * Configuration with `0.0.0.0/x` is not allowed.

   
   |**Examples of valid CIDR notation** |**Examples of invalid CIDR notation** |
   |---|---|
   |* 192.168.0.0/24: correct Class C network address;<br><br>* 10.0.0.0/8: correct Class A network address;<br><br>* 172.16.0.0/12: correct Class B network address. |* 192.168.1.1/24: not a network address (last octet is not 0);<br><br>* 192.168.0.0/33: invalid prefix length (exceeds 32);<br><br>* 256.0.0.0/24: invalid IP address (the first octet exceeds 255);<br><br>* 192.168.01.0/24: incorrect format (leading zero in the third octet). |
   


<span id="fc05c619"></span>
## Configure public network IP allowlist


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Basic information** in the left navigation pane, then click **IP allowlist configuration** after the **Instance public network access address** in the **Service access** section.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">IP allowlist configuration is only available when public network access is enabled for the instance, restricting which public devices can access the instance.   </div>
   

5. In the **IP allowlist configuration** dialog, add the IP addresses that need continued access to the instance, then click **OK**.

6. Check the progress of instance IP allowlist configuration.

   Return to the Instances page, where the instance status shows as **Updating**. When the status shows **Running**, the IP allowlist configuration is successful. Only IP addresses added to the allowlist can access the instance.
