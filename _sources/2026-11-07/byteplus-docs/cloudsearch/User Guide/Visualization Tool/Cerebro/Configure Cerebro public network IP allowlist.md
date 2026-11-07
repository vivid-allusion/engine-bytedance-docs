---
title: "Configure Cerebro public network IP allowlist"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/public-IPallowlist-Cerebro"
---

After enabling public network access for the visualization tool, all public network devices can access it by default. It is recommended to configure the public network IP allowlist to restrict access to authorized public IP addresses

<span id="14bb8dc0"></span>
## Precautions

When configuring the IP allowlist, you can set it as a single IP address or an IP subnet. Pay attention to the format requirements:


* IP address format: It must be a valid IPv4 address, consisting of four integers from 0 to 255 separated by dots.

* CIDR subnet: It should follow the standard format, with matching IP and mask.

   * The IP address part must be the network address, which is the first address in the subnet; all host bits must be zero.

   * The network prefix length ranges from `0 to 32`. `/0` is valid, representing the entire IPv4 address space (`0.0.0.0/0`); `/32` represents a single host address.

   * Reserved IP ranges, such as the loopback address 127.0.0.0/8, must not be used.

   * Do not configure as 0.0.0.0/x.

   
   |**Example of a valid CIDR notation** |**Example of an invalid CIDR notation** |
   |---|---|
   |* 192.168.0.0/24: Correct Class C network address<br><br>* 10.0.0.0/8: Correct Class A network address<br><br>* 172.16.0.0/12: Correct Class B network address |* 192.168.1.1/24: Not a network address (the last octet is not 0)<br><br>* 192.168.0.0/33: Invalid prefix length (exceeds 32)<br><br>* 256.0.0.0/24: Invalid IP address (the first octet exceeds 255)<br><br>* 192.168.01.0/24: Format error (leading zero in the third octet) |
   


<span id="c5021c88"></span>
## Configure public network IP allowlist


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation pane, select **Instance management \> Visulization configuration**, then click **IP allowlist configuration** after the **Public access address** on the **Cerebro** card .

5. In the **IP allowlist configuration** dialog, add the IP addresses that need continued access to the visualization tool, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring the IP allowlist, note the following:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cerebro and Kibana/Dashboards share the same IP allowlist configuration; adding or deleting entries affects both simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The IP allowlist supports single IP addresses or IP subnet ranges, separated by English commas.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The allowlist supports up to 300 IP addresses and subnets.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using CIDR subnets, use the standard format where the IP and mask correspond. For detailed format requirements, see <a href="https://docs.byteplus.com/docs/cloudsearch/public-IPallowlist-Cerebro#14bb8dc0">Precautions</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">e.g., <code>192.168.0.0/16</code>; entering <code>192.168.1.0/16</code> is incorrect.   </div>
   

6. View IP allowlist configuration progress.

   Return to the Instances page, and the instance status shows as **Updating**. When the status shows **Running**, the IP allowlist configuration is successful. Only IP addresses added to the allowlist can access the visualization tool.
