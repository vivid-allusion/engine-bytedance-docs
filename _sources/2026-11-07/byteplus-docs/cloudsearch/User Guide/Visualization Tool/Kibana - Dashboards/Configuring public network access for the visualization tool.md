---
title: "Configuring public network access for the visualization tool"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool"
---

Cloud Search allows you to enable public network access to the visualization tool for instance. By default, public network access to the visualization tool is disabled.

This topic describes how to enable and disable public network access.

<span id="ae1f24d5"></span>
## Precautions


* There are two methods to enable public network access. One is that the system automatically allocates public access with exclusive bandwidth according to the public bandwidth you set, and the other is that you bind an existing elastic IP. The two methods are billed differently, as explained below:

   * For billing of public network access with exclusive bandwidth allocated by the system, refer to [Billable Items](https://docs.byteplus.com/docs/cloudsearch/billing-items).

   * Bind an elastic IP to the instance, and the cost is charged by the EIP. For billing details, refer to [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* When the public network access is enabled for the visualization tool, all public network devices are allowed to access the visualization tool by default. It is recommended that you configure a public IP allowlist for the visualization tool to restrict the public IP addresses that can access the visualization tool. For details, refer to [Configuring a public IP allowlist for the visualization tool](https://docs.byteplus.com/docs/cloudsearch/public-IPallowlist-for-tool).

* Cerebro and Kibana/Dashboards share elastic IP, enabling or disabling public access is effective for both.


<span id="85b5bf40"></span>
## Enabling public network access


1. Log on to the [Cloud Search console](https://console.volcengine.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the instance.

4. On the left navigation bar, select **Instance Management \> Visualization configuration**, then \*\*\*\* enable **Public network access**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ac9c68d94794e9a9c78deebb468aa59~tplv-goo7wpa0wc-image.image) </span>

5. Select the method for configuring public network access.

   * Exclusive bandwidth allocated by the system: Select **default**, then set the public bandwidth of the instance, read and check the relevant protocol, and then click **OK**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Access to Kibana/Dashboards may be slow if bandwidth is less than 5 Mbps. Therefore, 5 Mbps or more is recommended.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23b57f69830e444bbbca2369c955dc99~tplv-goo7wpa0wc-image.image) </span>

   * Elastic IP: Select **User\-defined**, then bind the target elastic IP and click **OK**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be24a6f25e744e37a4fad12b1ec55d0a~tplv-goo7wpa0wc-image.image) </span>

6. View the operation progress.

   Return to the **Instances** page and view the desired instance. When instance status changes from **Updating** to **Running**, it means that the operation is successful.


<span id="fd165d4c"></span>
## Changing bandwidth configuration

If the visualization tool uses the exclusive bandwidth allocated by the system for public network access, you can change the public network bandwidth according to your business needs.


1. Log on to [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Visualization configuration**, and then click **Change bandwidth configuration** behind **Public network access**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb9918f7253345ce92224f4ccbc86def~tplv-goo7wpa0wc-image.image) </span>

5. On the **Change bandwidth configuration** page, set the public network bandwidth of the visualization tool, read and check the relevant terms of service, and then click **Confirm order**.


<span id="1762afa5"></span>
## Disabling public network access

We recommend that you disable public network access to the visualization tool as soon as possible when internet devices outside the virtual private cloud (VPC) no longer require access to the tool.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once public network access is disabled, clients can no longer access the visualization tool using the public domain name and port. To avoid business interruptions, make sure that your business does not rely on the public endpoint before disabling public network access.</div>



1. Log on to the [Cloud Search console](https://console.volcengine.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Visualization configuration**.

5. Disable public network access.

   * Exclusive bandwidth allocated by the system: Turn off the switch for \*\*\*\* **Public network access**.

   * Elastic IP: Click **Disable public access** button.

6. In the pop\-up dialog box, review the note for disabling public network access, and then click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the visualization tool is bound to an Elastic IP (EIP), the unbound EIP continues to be retained and charged when you disable public access. Release the EIP by yourself.   </div>
