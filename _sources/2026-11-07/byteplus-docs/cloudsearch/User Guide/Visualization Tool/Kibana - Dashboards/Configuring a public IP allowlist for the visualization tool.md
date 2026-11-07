---
title: "Configuring a public IP allowlist for the visualization tool"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/public-IPallowlist-for-tool"
---

Once public network access is enabled for the visualization tool, the tool can be accessed by all internet devices by default. We recommend that you configure a public IP allowlist to restrict access to the visualization tool from public IP addresses.

<span id="c8bffa69"></span>
## Before you begin

Enable public network access to the visualization tool. For more information, refer to [Enabling public network access for Kibana](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool).

<span id="471886ab"></span>
## Configuring a public IP allowlist


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. On the **Instances** page, click the name of the instance.

4. In **Instance management \>**  **Visulization configuration**, click **IP allowlist** **configuration** on the right side of **Public network access address**.

5. In the **IP allowlist** **configuration** dialog box, add the IP addresses that you want to allow to access the visualization tool, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring an IP allowlist, pay attention to the following points:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cerebro and Kibana/Dashboards share the same IP allowlist. When you add or delete IP address entries to or from the IP allowlist, the operation takes effect on both Cerebro and Kibana/Dashboards.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An IP allowlist can contain IP address entries in a single IP address format or in CIDR block notation, such as 192.168.0.1 or 192.168.0.0/24. Multiple IP address entries are separated with commas (,).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An IP allowlist can contain up to 300 IP address entries.   </div>
   

6. View the operation progress.

   Return to the instance list page, and find that the instance status is **Updating**. If the status changes to **Running**, it indicates that the IP allowlist is configured successfully. At this point, only IP addresses in the allowlist can access the visualization tool.


<span id="7b581d4b"></span>
## Modifying the public IP allowlist

To modify the IP allowlist, navigate to the **IP allowlist** **configuration** dialog box and add or delete IP address entries as needed.
