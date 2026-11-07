---
title: "Change the instance specification"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Change_instance_specification"
---

You can change the Dedicated instance specification based on your business requirements. Serverless instances do not require specification changes; they automatically adjust the instance specification based on actual load. This topic describes how to change instance specification.

<span id="KFCp8VFg"></span>
## Prerequisites

A dedicated instance has been created and is in **Running** status. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

<span id="0M30Ibgr"></span>
## Precautions


* Downgrading the specification may cause insufficient resources, resulting in cluster unavailability or high availability failure. Proceed with caution.

* Instances with elastic scaling enabled do not support manual specification changes. For details, see [Elastic scaling](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Elastic_scaling).


<span id="Nem7LrkT"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region where you want to create an instance.

3. Select the **Dedicated** tab, then go to the target instance’s **Change specification** page. You can enter the Upgrade page by any of the following methods:

   * Click **Change specification** in the **Actions** column of the target instance.

   * Click the target instance name to enter the details page, then click **Change specification** at the top right of the page.

4. In the pop\-up dialog box, confirm the information, and click **OK**.

5. On the **Change specification**, view the current specification of the instance, adjust the configurations below as needed, then click **Confirm order**.

   
   |Parameter |Description |
   |---|---|
   |Deployment mode |Select the instance deployment mode. Valid values are as follows:<br><br><br>* Single\-AZ deployment: reduces network latency and improves access speed.<br><br>* Two availability zones deployed: cross\-AZ deployment improves availability, with possible network latency of 2–3 ms.<br><br>* Three availability zones deployed: deployment across three availability zones further improves availability, with possible network latency of 2–3 ms.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of availability zones cannot be reduced during specification changes.</div><br> |
   |Availability zone |Select the availability zones for instance deployment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The original availability zones cannot be removed during specification changes.</div><br> |
   |Service nodes<br><br> |Select the specifications and quantities for each service node.<br><br><br>* You can select different specifications for different nodes. For more information, see [Product specifications](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications).<br><br>* The number of supported nodes for each type varies depending on whether high availability is enabled. The number of nodes must be a multiple of the number of availability zones. You can configure up to 20 index nodes and 200 compute nodes. |
   |Index/Compute node |* The resource model cannot be changed after instance creation.<br><br>* Select CU type, specifications, and quantity for index and compute nodes.<br><br>   * Setting CU type is supported only when GPU usage is enabled.<br><br>   * The CU type supports **Capacity** and **Performance**.<br><br>   * For detailed information about available specifications for index nodes and compute nodes, see [Product specifications](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications).<br><br>   * The number of index and compute nodes supported varies by deployment mode. The number of nodes must be an integer multiple of the number of availability zones. You can configure up to 20 index nodes and 200 compute nodes. |
   

6. Complete the following steps according to the instance’s billing type.

   * Pay\-as\-you\-go

      On the **Confirm order** page, review the order details, read and check the service terms, then click **Buy now**.

   * Subscription

      1. On the **Confirm order** page, review the order details, read and check the service terms, then click **Buy now**.

      2. On the **Confirm order information** page, review the order details again, then click **Next**.

      3. On the **Submit payment information** page, confirm the payment details, choose the payment method, then click **Proceed to payment**.
