---
title: "Managing instances"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Managing_Instances"
---

You can view the information about or delete your created APIG instances. This topic describes APIG instance management operations.

<span id=".5p-l55yL5a6e5L6L"></span>
## View instances

You can view the basic information of a gateway instance and manage the associated services, Upstreams, and Upstream source information about the instance.


1. Log in to [APIG console](https://console.byteplus.com/veapig). Select the target region in the top navigation bar.

2. In the left navigation pane, select **Instance management**, and then click the name of the target instance to enter the instance overview page.

   You can view the basic information of the target instance, and manage the services, Upstreams, and Upstream source information about the instance.


<span id=".5Yig6Zmk5a6e5L6L"></span>
## Delete an instance

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Before deleting an instance, you need to clear all of its resources, including services, Upstreams, and the Upstream source information.</div>


* <div data-tips="true" data-tips-type="danger">After you delete the instance, it cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="danger">After you delete the instance, the automatically created log topic in API Gateway will not be deleted. You can go to the TLS console to delete the log topic as needed.</div>


1. Log in to [APIG console](https://console.byteplus.com/veapig). Select the target region in the top navigation bar.

2. On the **Instance management** page, find the instance to be deleted and click **Delete ** in the **Actions** column.

3. In the pop\-up box, click **Confirm** to delete the instance.


<span id=".5Y-Y5pu06YWN572u"></span>
## Change configurations

You can change the configurations of an instance, including the node specification and the number of nodes.


1. Log in to [APIG console](https://console.byteplus.com/veapig). Select the target region in the top navigation bar.

2. On the **Instance management** page, find the instance whose configurations need to change and click **Upgrade** in the **Actions** column.

3. In the "Upgrade" section, modify the node specifications, number of nodes, and CLB specifications, and then click  **"Confirm changes"** .

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Changing the specifications of an APIG instance takes about 3 to 4 minutes. During this period, you cannot perform any operation on the instance in the console.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For instances with two or more nodes, a rolling update is performed on each node, and data is synchronized automatically to ensure near\-lossless upgrades.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you perform upgrades during off\-peak hours to avoid impacts on your business.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, you can only change the specifications of an APIG instance.  If you have additional change requirements, such as a bandwidth limit, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170&FlowKey=DhvSFwiOSXyEVSlGZJXx">submit a ticket</a>.   </div>
   


<span id="oTOyp85S"></span>
## Enable Gzip response compression

API Gateway supports Gzip response compression. Before forwarding a backend response to the client, the gateway can automatically perform lossless Gzip compression on the response body. For workloads with large response payloads, uncompressed data generates more outbound traffic on the gateway and increases traffic costs. You can enable Gzip response compression to compress response bodies and effectively reduce traffic costs. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>[Beta · apply for trial]</strong>: This feature is currently in Beta. To use this feature, contact your account manager.</div>


* <div data-tips="true" data-tips-type="warning">Enabling Gzip response compression may increase CPU usage on the gateway.</div>


1. Log in to [APIG console](https://console.byteplus.com/veapig). Select the target region in the top navigation bar.

2. In the left navigation pane, select **Instance management**, and then click the name of the target instance to enter the instance overview page.

3. In the **gzip response compression** area, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_145d7d9f719eef5b2200c18b51be9cd1.png) </span> next to the target label.

4. In the **Edit gzip response compression **  dialog box, enable Gzip response compression.

5. Click **Confirm** to finish.
