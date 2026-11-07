---
title: "Configuring public network access to Cerebro"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/public-access-Cerebro"
---

Public network access is disabled by default in Cloud Search. If you want to access the visualization tool Cerebro over the internet, enable public network access to Cerebro first.

This topic describes how to enable and disable public network access.

<span id="注意事项"></span>
## Precautions


* There are two methods to enable public network access. One is that the system automatically allocates public access with exclusive bandwidth according to the public bandwidth you set, and the other is that you bind an existing elastic IP. The two methods are billed differently, as explained below:

   * For billing of public network access with exclusive bandwidth allocated by the system, refer to [Billable Items](https://docs.byteplus.com/docs/cloudsearch/billing-items).

   * Bind an elastic IP to the instance, and the cost is charged by the EIP. For billing details, refer to [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* When the public network access is enabled for the visualization tool, all public network devices are allowed to access the visualization tool by default. It is recommended that you configure a public IP allowlist for the visualization tool to restrict the public IP addresses that can access the visualization tool. For details, refer to [Configuring a public IP allowlist for Cerebro](https://docs.byteplus.com/docs/cloudsearch/public-IPallowlist-Cerebro).

* Cerebro and Kibana/Dashboards share the public IP, enabling or disabling public access is effective for both.


<span id="开启公网访问"></span>
## Enabling public network access


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the instance.

4. On the left navigation bar, select **Instance Management \> Visualization configuration**, then \*\*\*\* enable **Public network access** on the **Cerebro** card.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/766576c914a44626aafc3777290659ca~tplv-goo7wpa0wc-image.image) </span>

5. Select the method for configuring public network access.

   * Exclusive bandwidth allocated by the system: Select **default**, then set the public bandwidth of the instance, read and check the relevant protocol, and then click **OK**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Access to Cerebro may be slow if bandwidth is less than 5 Mbps, 5 Mbps or more is recommended.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b134690e6cbd45f3bd5e93e37dfc8000~tplv-goo7wpa0wc-image.image) </span>

   * Elastic IP: Select **User\-defined**, then bind the target elastic IP and click **OK**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7cc3699ba7342269ea51248f7dbecd3~tplv-goo7wpa0wc-image.image) </span>

6. View the operation progress.

   Return to the **Instances** page and view the desired instance. When instance status changes from **Updating** to **Running**, it means that the operation is successful.


<span id="0d4619c3"></span>
## Changing bandwidth configuration

You can change the public bandwidth of the visualization tool according to your business needs.


1. Log on to [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Visualization configuration**, and then click **Change bandwidth configuration** behind **Public network access** on the Cerebro card.

5. On the **Change bandwidth configuration** page, set the public network bandwidth of the visualization tool, read and check the relevant protocol, and then click **Confirm order**.


<span id="关闭公网访问"></span>
## Disabling public network access

We recommend that you disable public network access to a visualization tool as soon as possible when internet devices outside the virtual private cloud (VPC) no longer require access to the tool.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once public network access is disabled, clients can no longer access the visualization tool using the public domain name and port number. To avoid business interruptions, make sure that your business does not rely on the public endpoint before disabling public network access.</div>



1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Visualization configuration**.

5. Disable public network access.

   * Exclusive bandwidth allocated by the system: Turn off the switch for \*\*\*\* **Public network access**.

   * Elastic IP: Click **Disable public access** button.

6. In the pop\-up dialog box, review the note for disabling public network access, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the visualization tool is bound to an Elastic IP (EIP), the unbound EIP continues to be retained and charged when you disable public access. Release the EIP by yourself.   </div>
