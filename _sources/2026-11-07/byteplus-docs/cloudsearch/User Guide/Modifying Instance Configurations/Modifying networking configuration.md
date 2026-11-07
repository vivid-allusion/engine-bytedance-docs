---
title: "Modifying networking configuration"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/modify-network-configuration"
---

This topic describes how to modify the private network and subnet configuration of an existing instance in case of network adjustment and insufficient number of IPs.

<span id="6165539a"></span>
## Precautions

Modifying the configurations of private network and subnet will result in change of network connection accessing the instance, namely access via public and private network domain name should be resolved to a new IP address. Since browsers, applications, operating systems, and DNS servers may cache the results of DNS resolution, the new IP address cannot be detected in time. Therefore, network change of Cloud Search instance will lead to minutes or even hours of disruption to instance access from visualization tools (Kibana, Cerebro, etc.) as well as the online read/write of applications.

Please proceed with caution when modifying the instance network configuration. If it is determined that this operation needs to be performed, it is recommended to operate during off\-peak hours.

In order to reduce service interruption time due to network change, optimization solutions for different cloud service scenarios and clients are described in [Optimization solution for network change](https://docs.byteplus.com/en/docs/cloudsearch/Network-change-optimization). Please perform the optimization operation based on your actual business scenario.

<span id="255cb583"></span>
## Prerequisites


* The instance status is running.

* The desired VPC and subnet are pre\-configured. For more information, please see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).


<span id="c0705e0c"></span>
## Modifying Private Network


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Basic information**, and click the edit icon of **private network** in **Service access**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a815063968b43cc877ccab4b0d91800~tplv-goo7wpa0wc-image.image) </span>

5. On the pop\-up page of modifying network information, choose the desired private network and subnet from the dropdown list, and then click **OK**.


If an EIP is not associated, the page is displayed as below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/154a0420d559420a82b27d77b0354e27~tplv-goo7wpa0wc-image.image) </span>

If an EIP is associated, the page is displayed as below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83868cca5a3b4c4bbd45a1fcd75778e7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Here you can either modify private network and subnet at the same time, or only modify subnet.</div>


* <div data-tips="true" data-tips-type="tip">If public network access is enabled for instance, Kibana or Dashboards, a new EIP should be configured accordingly and the former EIP will be released automatically.</div>


6. On the confirm page, review the prompt information, and click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5bc12ef78db45ddbf38fee4f56b9d2e~tplv-goo7wpa0wc-image.image) </span>


7. Check the modification progress.


Switch to **Instances** page and view the modified instance. When the status is changed from updating to running, it means that the modification is successful.

<span id="01aa205c"></span>
## Modifying Subnet


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Basic information**, and click the edit icon of **Subnet** in **Service access**.

5. On the pop\-up page of modifying network information, choose the desired subnet from the dropdown list, and then click **OK**.


If an EIP is not associated, the page is displayed as below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2efee6237c0643c7a7fc86a73a22a208~tplv-goo7wpa0wc-image.image) </span>

If an EIP is associated, the page is displayed as below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b27461f77fb4088add27d4e7e01fbed~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Here you can only modify subnet.</div>



<div data-tips="true" data-tips-type="tip">If public network access is enabled for instance, Kibana or Dashboards, a new EIP should be configured accordingly and the former EIP will be released automatically.</div>



6. On the confirm page, review the prompt information, and click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5bc12ef78db45ddbf38fee4f56b9d2e~tplv-goo7wpa0wc-image.image) </span>


7. Check the modification progress.


Switch to **Instances** page and view the modified instance. When the status is changed from updating to running, it means that the modification is successful.
