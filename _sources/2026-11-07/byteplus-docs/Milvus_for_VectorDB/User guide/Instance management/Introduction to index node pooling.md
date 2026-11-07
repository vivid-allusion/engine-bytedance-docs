---
title: "Introduction to index node pooling"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Introduction_to_index_node_pooling"
---

<span id="rSMn4ZTo"></span>
## **Feature overview**

Index pooling is a platform\-provided capability for hosting index building resources. Once enabled, users no longer need to deploy and manage index nodes separately within the cluster. All index building tasks are scheduled to the shared resource pool provided by the platform, delivering ready\-to\-use index building capability. By enabling index pooling when creating a Dedicated instance, index nodes are decoupled from the cluster and centrally managed by the platform with pay\-as\-you\-go billing. This reduces operational complexity, improves resource utilization, and lowers overall costs.

<span id="bwaBroeU"></span>
## **Core capabilities**


* No deployment required: no need to manually create or maintain index nodes.

* Resource pooling: multi\-tenant resource sharing improves overall utilization.

* Elastic scheduling: dynamically allocates computing resources based on index task load.

* Operation simplification: platform unified responsibility for node health checks and scaling.


<span id="7wxWBU0P"></span>
## **Applicable scenarios**

The index node pooling feature applies to the following scenarios:


* Low or medium write frequency with infrequent index building triggers.

* Reducing resource costs and avoiding node idling.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The unit price for index node pooling is twice that of the non\-pooling mode. Therefore, enabling index pooling lowers costs when index node usage is below 50%. When index node usage exceeds 50%, enabling index pooling is not recommended.   </div>
   

* No need for custom specifications or exclusive resources for index nodes.


<span id="NIRi8YPh"></span>
## **Usage**

When creating a Dedicated instance, turn on the **index pooling** switch to use this feature. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

After turning on:


* You do not need to configure the index node specification or quantity.

* The index build tasks automatically schedule execution to the platform’s unified resource pool.


<span id="rxQ36FIv"></span>
## **Billing instruction**


* Billing method: cumulative CU billed hourly. Details are available in [Product billing](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_billing).

* Billing features: charges apply only for computing resources used in actual index building, with no cost for idle resources.


<span id="6eFfh9Ma"></span>
## Feature comparison


|**Item** |**Non\-pooling mode** |**Pooling mode** |
|---|---|---|
|Index node deployment |Self\-built within cluster |Platform unified management |
|Resource usage |Exclusive resource |Shared resource pool |
|Billing method |Charged by node specification |Cumulative CU per hour |
|O&M complexity |Node status requires monitoring |No perception required |


<span id="uDTrDghU"></span>
## **Precautions**


* Pooling mode and non\-pooling mode clusters do not support mutual conversion at this time.

* The execution time of index building tasks may be affected by the overall load of the resource pool.

* Custom index node specifications or exclusive resources are not supported.

* For scenarios with high concurrent writes or frequent index builds, it is recommended to consider using the default mode (non\-pooling).
