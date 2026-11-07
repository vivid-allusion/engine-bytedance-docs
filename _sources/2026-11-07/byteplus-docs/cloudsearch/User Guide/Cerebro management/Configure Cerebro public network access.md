---
title: "Configure Cerebro public network access"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_public_network_access"
---

Cloud Search disables public network access by default. To access the visualization tool Cerebro via public network, you need to enable public network access first. This topic explains how to configure Cerebro public network access.

<span id="wn6Hild8"></span>
## Precautions


* To enable public network access for the instance, you need to associate an existing Elastic IP (EIP). Charges are billed by EIP. For billing details, refer to [EIP billing overview.](https://docs.byteplus.com/en/docs/eip/Billing-overview)

* Monitor the expiration time of the EIP. If it expires without renewal, the public domain name will become unavailable.

* When Cerebro enables public network access, the IP allowlist automatically includes `127.0.0.1`, blocking all public IPs from accessing it. If you need normal use, modify the IP allowlist configuration after enabling public network access. For detailed steps, refer to [Configure Cerebro public network IP allowlist](https://docs.byteplus.com/en/docs/cloudsearch/public-IPallowlist-Cerebro).


<span id="vJTcNIJu"></span>
## Enable public network access


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **Cerebro**, then turn on **Public network access** in the **access information** area.

4. On the **Enable public network access** panel, select the EIP to associate, then click **OK**.


<span id="vaihgrtz"></span>
## Disable public network access

After disabling public network access for Cerebro, clients can no longer access Cerebro through the original public access address. Make sure your business does not use the public address to access Cerebro to avoid unnecessary losses.


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **Cerebro**, then turn off **Public network access** in the **access information** area.

4. In the pop\-up dialog box, review the precautions for disabling public network access, then click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After disabling public network access, the disassociated EIP will remain and incur charges. Release the EIP resource on your own. For more information, see <a href="https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP">Release EIP</a>.   </div>
