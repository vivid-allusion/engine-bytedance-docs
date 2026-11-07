---
title: "Scale out and upgrade instance nodes"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Scale_out_and_upgrade_instance_nodes"
---

This article describes how to perform configuration upgrades and capacity expansion for the nodes of an EMR Serverless OLAP instance to meet business requirements.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The operation entry points and key aspects of FE nodes and BE nodes are similar. This article uses FE nodes as an example to show operation details.</div>


<span id="_1-前提条件"></span>
# Prerequisites


* An EMR Serverless OLAP instance has been created, and the instance status is **Running.** 

* Your Volcano Engine account balance is sufficient.


<span id="266e437b"></span>
# Steps

<span id="caacf094"></span>
## Entry point

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/446b6f03540b4b20924a3677de1f86c2~tplv-goo7wpa0wc-image.image) </span>


1. Go to the EMR Serverless OLAP instance details page.

   1. Log in to [EMR Serverless OLAP Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage).

   2. In the top menu bar, select the region and project as needed.

   3. Click the **instance name** of the target instance to enter the instance details page.

2. In the Node specifications and Number of nodes areas of the corresponding node, click the Upgrade and Expansion buttons to access the configuration upgrade and expansion interface.


<span id="7779ffae"></span>
## Node configuration upgrade


1. Go to the EMR Serverless OLAP instance details page, and in the Node specifications area of the corresponding node, click the Upgrade button.

2. In the **Instance configuration upgrade** window, select Target FE Specifications\*\*.\*\* Currently, 8CU, 16CU, and 32CU are supported. After the pre\-check passes, check to agree to the EMR Service Terms, then click the **Confirm** button. Wait for the instance status to change from **Changing** to **Running**, indicating that the node configuration upgrade was successful.

3. If the payment type is Subscription, clicking **Confirm** will redirect to the order confirmation and payment page. After the order is confirmed and payment is completed, click **Go to Console** to return to the console.

   Wait for the instance status to change from **Changing** to **Running**, indicating that the node configuration upgrade was successful.


<span id="_2-扩容be节点"></span>
## Node expansion


1. Go to the EMR Serverless OLAP instance details page, and in the Number of nodes area of the corresponding node, click the **Expansion** button.

2. In the instance scaling window, set Number of FE nodes. After the pre\-check passes, check to agree to the Service Terms, then click the **Confirm** button. Wait for the instance status to change from **Changing** to **Running**, indicating that the node expansion was successful.

3. If the payment type is Subscription, clicking **Confirm** will redirect to the order confirmation and payment page. After the order is confirmed and payment is completed, click **Go to Console** to return to the console.

   Wait for the instance status to change from **Changing** to **Running**, indicating that the node expansion was successful.
