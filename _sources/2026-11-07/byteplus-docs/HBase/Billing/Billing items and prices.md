---
title: "Billing items and prices"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Billing_items_and_prices"
---

This article describes the billing items and pricing details for Table Storage for HBase.

<span id=".6K6h6LS56aG5"></span>
## Billing items

The following items are billed when you use HBase instances.


|Billing Item |Billing method |
|---|---|
|Compute node |Pay\-as\-you\-go (postpaid) and subscription (prepaid) plans are available. Charges are based on node specifications and usage duration. |
|Storage space |Pay\-as\-you\-go (postpaid) and subscription (prepaid) billing, based on the amount of data stored and the duration of storage. |
|Capacity Storage |Pay\-as\-you\-go (postpaid) and subscription (prepaid) billing, based on the amount of data stored and the duration of storage. |


<span id=".5Lu35qC86KGo"></span>
## Pricing


* **Compute Node Pricing**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The prices in the following table are for a single compute node.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The prices do not differentiate between Master and Region Server nodes. Nodes with the same specifications have the same price.   </div>
   

   
   |Spec Code |CPU and Memory |Pay\-as\-you\-go（USD/node/hour） |||Subscription（USD/node/month） |
   |---|---|---|---|---|---|
   |||**China (Hong Kong)**  |**Asia Pacific (Johor)**  |Asia Pacific (Jakarta) |**Asia Pacific (Johor)**  |
   |hbase.x1.4xlarge |16C32GiB |0.711824851 |0.623461564 |0.751097946 |299.2615506 |
   |hbase.x2.4xlarge |16C64GiB |1.033737798 |0.941058926 |1.033737798 |451.7082843 |
   |hbase.x1.8xlarge |32C64GiB |1.423654018 |1.246923128 |1.502200446 |598.5231012 |
   

* **Storage space**

   
   |Specification type |Pay\-as\-you\-go（USD/GiB/hour） |||Pay\-as\-you\-go（USD/GiB/month） |
   |---|---|---|---|---|
   ||**China (Hong Kong)**  |**Asia Pacific (Johor)**  |Asia Pacific (Jakarta) |**Asia Pacific (Johor)**  |
   |HDD file storage |0.000208333 |0.0003125 |0.000208333 |0.15 |
   |SSD file storage |0.000892857 |0.0009375 |0.000892857 |0.45 |
   |Capacity Storage |0.00003869 |0.000040476 |0.00003869 |0.02 |
   


<span id=".5Lu35qC86K6h566X5YWs5byP"></span>
## Pricing formula


* **Pay\-as\-you\-go**

   Hourly pay\-as\-you\-go price = Compute node fees + Storage space fees = (Master node spec unit price × Number of nodes + Region Server node spec unit price × Number of nodes) + Storage space unit price × Storage space size

* **Yearly or monthly subscription**

   One\-time prepaid price = compute node cost + storage cost = ((Master node specification monthly price per node × number of nodes + Region Server node specification monthly price per node × number of nodes) + storage space monthly price per node × storage space size × number of months
