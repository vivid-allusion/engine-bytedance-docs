---
title: "Specification type"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/storage_type"
---

Document Database for MongoDB provides two architectures: replica set and sharding cluster. Instances for each architecture support various storage types and specification configurations, allowing flexible selection to meet your requirements for different performance, capacity needs, and application scenarios. This topic describes the details of different storage types and specification types.

<span id="7fikGhkr"></span>
## Specification type

Document Database for MongoDB supports two storage types: FlexPL volumes and local disks. For architecture features, performance comparison, and selection recommendations of each storage type, see [Storage types](https://docs.byteplus.com/en/docs/mongodb/Storage_type?lang=en). Different storage types support different node specification types. The table below summarizes the details of each MongoDB specification type.


|Storage types |**Specification type** |**Description** |**Applicable scenarios** |**Specification type chart** |
|---|---|---|---|---|
|Local disk |General specification |It has independent memory and storage space but shares CPU and I/O resources with other general instances on the same physical machine. This maximizes utilization through resource reuse, offering high cost\-effectiveness. |Ideal for application scenarios that prioritize cost\-effectiveness but have lower peak performance requirements. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2821d678681d7ec4042ef794f46a342f.png) </span> |
|FlexPL ****volume |Dedicated specification |Exclusively use allocated memory, storage, CPU, and I/O, ensuring no resource contention.<br><br>Compared to local disk instances, volume instances are not affected by other instances on the physical machine, ensuring long\-term stable performance. |Application scenarios with higher performance requirements for database computing power and networking, such as finance, e\-commerce, government services, and large\-scale internet businesses.<br><br> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_450b2baf4db5ec93a522af877e4538e9.png) </span> |


<span id="30XHj8B2"></span>
## Limits


* Currently, **FlexPL volumes** are in gray\-scale release and are only available in **China (Guangzhou)** , **China (Beijing)** , and **China (Shanghai)** . Specifically, China (Shanghai) supports multi\-availability zone deployment, while China (Guangzhou) and China (Beijing) only support single\-availability zone deployment. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to apply for usage.

* FlexPL volumes currently only support dedicated specifications.

* FlexPL volumes currently support up to MongoDB 8.0.

* FlexPL volumes do not support the retrieval features (mongot) provided by MongoDB 8.3 and later versions. To use vector search or full\-text search, select local disks and [submit a ticket](https://console.byteplus.com/workorder/create/) to request enablement.

* When modifying instance specifications, only scaling up or down between instance specifications of the same type is supported. Switching between instances of different storage types or different specification types is not currently supported. For more details on instance modification, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/mongodb/solutions-for-spec-modification).

* FlexPL volume instances do not support storage space reduction.


<span id="vUH7iYcC"></span>
## Specification performance and billing

For details on specification performance, and billing of various instance types, refer to [Instance specifications](https://docs.byteplus.com/en/docs/mongodb/instance_spec) and [Billing items and prices](https://docs.byteplus.com/en/docs/mongodb/billing-item-price).

<span id="MJFqLCk5"></span>
## Usage

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The usage scenarios for different instance specification types are similar. You can choose the desired instance specification type based on your business needs in the following scenarios:</div>



* <div data-tips="true" data-tips-type="default">Creating instance</div>


* <div data-tips="true" data-tips-type="default">Restore to new instance by backup file</div>


* <div data-tips="true" data-tips-type="default">Restore to new instance by point in time</div>


* <div data-tips="true" data-tips-type="default">Recovery from deleted instance</div>


1. Log on to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. According to your use case, enter the **Create instance** or **Recovery instance** page by referring to instructions on [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance), [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file), [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) or [Recovery from deleted instance](https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance), and set the parameters for the **Storage type** and **Node specification** following the steps below:

   1. For the storage type, select **local disk** or **FlexPL** based on your business needs.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e174cb90b5da46027d027651e60a4bd0.png) </span>

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For more details on volumes, refer to <a href="https://docs.byteplus.com/en/docs/26444/701062">Volume specifications</a>.      </div>
      

   3. In the node specification table for the selected specification type, select the desired node specifications.

4. After setting the **Node specification** parameters, refer to the creating instance or recovery instance operation guide to set other parameters for the instance and complete the instance purchase.


<span id="ISlx10A2"></span>
## View specification type

You can log in to the[ MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb), and in the **Configuration area** under the **Summary** tab, view the instance's **Specification type** information. For more details, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06e4ab85d6b8a082f01f6bf408b52fba.png) </span>

&nbsp;
