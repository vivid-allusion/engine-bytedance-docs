---
title: "Instance disk expansion"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Instance_disk_expansion"
---

This article describes how to expand the disk capacity of an EMR EMR Serverless OLAP cluster to meet business needs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The operation entry and key points for the FE node and BE node are similar. This article uses the FE node as an example to demonstrate the operation details.</div>


<span id="_1-前提条件"></span>
# prerequisites


* An EMR EMR Serverless OLAP instance has been created, and the instance status is **Running.** 

* Your Volcano Engine account balance is sufficient.


<span id="_2-扩容-be-节点的磁盘容量"></span>
# Expand disk capacity

<span id="bffaf47f"></span>
## Operation entry

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/840c527e9c8a4aa99e175ce0be9d429a~tplv-goo7wpa0wc-image.image) </span>


1. Go to the EMR EMR Serverless OLAP instance details page.

   1. Log in to the [EMR Serverless OLAP console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage).

   2. In the top menu bar, select the region and project as needed.

   3. Click the instance name of the target instance.

2. In the FE Details/BE details area of Storage Specifications, click the Expansion button.


<span id="06820c85"></span>
## Configuration details


1. In the storage expansion window, set the storage size for the corresponding node and expand it to meet business needs. After the pre\-check passes, select the checkbox to agree to the EMR service terms, then click the **Confirm** button. Wait for the instance status to change from **Changing** to **Running**, indicating that the node disk expansion was successful.

2. If the payment type is **Subscription**, after clicking **Confirm**, you will be redirected to the order confirmation and payment page. After the order is confirmed and payment is completed, click **Go to console** to return to the console.

   Wait for the instance status to change from **Changing** to **Running**, indicating that the node expansion was successful.
