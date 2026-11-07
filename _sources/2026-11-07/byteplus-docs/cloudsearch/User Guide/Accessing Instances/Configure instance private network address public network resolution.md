---
title: "Configure instance private network address public network resolution"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/enabling-DNS"
---

Cloud Search supports enabling public network resolution for the instance’s private network address to meet special scenarios such as development and testing in non\-production environments. After enabling public network resolution, users can access the instance’s private network address via dedicated lines.

<span id="9907abf8"></span>
## Precautions


* Due to the complexity of the public network environment, domain name resolution accuracy and timeliness cannot be guaranteed. Therefore, public network resolution is only allowed in non\-production environments. For production environments, using the DNS Forward solution is strongly recommended.

* After successfully enabling public network resolution for the instance’s private network address, please wait 1 minute before using the resolved instance address.

* Considering the complexity of the public network environment, it is recommended to disable public resolution of the instance’s private network address as soon as possible after enabling it and completing the dedicated line access requirements.


<span id="95eb952e"></span>
## Enable public network resolution


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Basic information** in the left navigation bar, then click **Enable public resolution of private address** after **Instance private network address** in the **Service access** section.

5. In the **Enable public network resolution** dialog, review the precautions, then click **OK** to confirm.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After enabling public network resolution, you can view the progress of enabling public resolution of the instance’s private network address. <strong>Refresh</strong> the page, the instance status shows as <strong>Updating</strong>. When the status shows <strong>Running</strong>, it means public resolution of the private network address is enabled successfully.   </div>
   

<span id="05197c86"></span>
## Disable public network resolution


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Basic information** in the left navigation bar, then click **Disable public resolution of private address** after **Instance private network address** in the **Service access** section.

5. In the **Confirm disable public network analysis** dialog, click **OK**.

6. View the progress of disabling public resolution of the instance's private network address.

   Refresh the page; the instance status shows as **Updating**. When the status shows **Running**, the private network address public resolution has been disabled successfully.
