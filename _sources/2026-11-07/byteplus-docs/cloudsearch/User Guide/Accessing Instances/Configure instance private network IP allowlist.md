---
title: "Configure instance private network IP allowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/IPallowlist-for-instance"
---

Instance supports private network access by default, allowing all devices within the same VPC environment to access the instance. It is recommended to configure a private IP allowlist for the instance to restrict access to specified private IP addresses.

<span id="d0bb6c27"></span>
## Precautions

When configuring the IP allowlist, you can specify a single IP address or an IP network segment. Please follow the format requirements below:


* IP address format: Must be a valid IPv4 address consisting of four integers from 0 to 255, separated by periods (.).

* CIDR segment: Must be in standard format, with the IP and mask matching.

   * The IP address must be a network address, which is the first address in the subnet; all host bits must be zero.

   * The network prefix length range is `0~32`. `/0` is valid and represents the entire IPv4 address space (0.0.0.0/0); `/32` represents a single host address.

   * Reserved IP ranges such as the loopback address 127.0.0.0/8 must not be used.

   * Configuration as 0.0.0.0/x is not allowed.

   
   |**Examples of valid CIDR notation** |**Examples of invalid CIDR notation** |
   |---|---|
   |* 192.168.0.0/24: correct Class C network address;<br><br>* 10.0.0.0/8: correct Class A network address;<br><br>* 172.16.0.0/12: correct Class B network address. |* 192.168.1.1/24: not a network address (the last octet is not 0);<br><br>* 192.168.0.0/33: invalid prefix length (exceeds 32);<br><br>* 256.0.0.0/24: invalid IP address (the first octet exceeds 255);<br><br>* 192.168.01.0/24: format error (the third octet has a leading zero). |
   


<span id="8a210def"></span>
## configure private network IP allowlist


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation, select **Basic information**, then click **IP allowlist configuration** after **Instance private network access address** in the **Service access** section.

5. In the **IP allowlist configuration** dialog, add the private network IP addresses that need access to the instance, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please note the following when configuring the IP allowlist:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">All groups can upload up to 300 IP addresses or IP subnets in total.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">127.0.0.1 means blocking all IPv4 addresses, and 0.0.0.0/0 means allowing all IPv4 addresses to access.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For security reasons, it is not recommended to configure access for all IP addresses.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using CIDR blocks, they must follow standard format, with IP and mask matching. For detailed format requirements, refer to the <a href="https://docs.byteplus.com/docs/cloudsearch/IPallowlist-for-instance#d0bb6c27">Precautions</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, <code>192.168.0.0/16</code>; entering <code>192.168.1.0/16</code> is incorrect.   </div>
   

6. Check the progress of instance IP allowlist configuration.

   Return to the Instances page, where the instance status shows as **Updating**. When the status shows **Running**, the IP allowlist configuration is successful. Only IP addresses added to the allowlist can access the instance.
