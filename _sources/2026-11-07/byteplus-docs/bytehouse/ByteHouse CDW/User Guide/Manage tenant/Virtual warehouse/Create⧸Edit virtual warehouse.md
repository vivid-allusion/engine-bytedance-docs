---
title: "Create⧸Edit virtual warehouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-edit-virtual-warehouse"
---

The virtual warehouse (VW) is ByteHouse's compute resource. You can create virtual warehouses with specified configurations as needed to provide sufficient resources for various data operations. This tutorial explains how to create and edit virtual warehouses, and how to set default virtual warehouses, default write virtual warehouses, and database\-level write virtual warehouses.

<span id="f8bb49e5"></span>
## Usage restrictions


* The usage restrictions for the virtual warehouse type feature are as follows:

   * This feature is in Beta. To use it, submit a ticket or contact the ByteHouse team to request whitelist access.

   * Ensure that your ByteHouse engine version is v2.3.1 or higher. You can log in to the ByteHouse Cloud Data Warehouse Console, click the **Tenant management** at the top, and view your engine version on the **Basic information** page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48e6361f21d64da3b4c1276d1a5f98c3~tplv-goo7wpa0wc-image.image) </span>

* The load elasticity feature is in Beta. To use it, submit a ticket or contact the ByteHouse team to request whitelist access.


<span id="0557445e"></span>
## Create virtual warehouse


1. On the ByteHouse console, click the **Virtual warehouse** tab.

2. Click the  **+ Virtual warehouse** button in the upper right corner.

3. In the \*\*Create virtual warehouse \*\*dialog, select the payment type and virtual warehouse specifications, then set the related parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Users who activated ByteHouse Cloud Data Warehouse Service in May 2024 or later must select the type of virtual warehouse when creating it.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Users who activated ByteHouse Cloud Data Warehouse Service in April 2024 or earlier will have the virtual warehouse created automatically based on the type selected when creating the service.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c4f42eba98f435190e30a53ca50065b~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter items |Parameter description |
   |---|---|
   |Specifications |Virtual warehouse specifications. Virtual warehouses of different specifications have different prices. You can select one according to your needs. You can view the specifications and pricing of the virtual warehouse on the interface, or refer to [Computational resources](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing#cadb49e9). |
   |Virtual warehouse name |You can customize virtual warehouse name, but this name cannot be changed once created. Naming rules are as follows:<br><br><br>* It should start with a lowercase letter.<br><br>* It should consist of lowercase letters and numbers.<br><br>* You can use a single underline to connect the name.<br><br>* Up to 31 characters. |
   |Virtual warehouse description |It provides a custom description for the virtual warehouse to facilitate future distinction and use. |
   |Auto resume/suspend |* Auto resume: The system defaults to auto resume enabled. Once enabled, you do not need to manually start the virtual warehouse and can send requests to activate computing resources and perform queries. After enabling auto resume, the first time query takes longer (10 to 30 seconds). You can configure it according to business needs.<br><br>* Auto suspend: When enabled, if unused within the set interval, the virtual warehouse automatically shuts down to reduce resource costs.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To set a virtual warehouse as the default write virtual warehouse for an exclusive Server, you need to disable the group’s auto start and stop settings.</div><br> |
   |Virtual warehouse type |Supported types for the virtual warehouse. A virtual warehouse can be configured as OLAP or ELT.<br><br><br>* **OLAP**: This type is optimized for high concurrency and low latency OLAP queries and supports complex SQL queries and interactive analysis.<br><br>* **ELT**: This type is suitable for long\-running batch processes, applied in scenarios such as bulk data import, cleaning, and large\-scale offline computing. For more details about ELT, refer to [ELT Support](https://docs.byteplus.com/docs/bytehouse/docs-elt-support).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, existing virtual warehouses are all OLAP types. You can refer to <a href="https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f">Edit virtual warehouse configuration</a> and switch types as needed.</div><br> |
   |Advanced Configuration |**Advanced features**: It supports enabling advanced features like full text search, GIS, and vector search.<br><br><br>* **Full Text Search**: It allows preprocessing documents and saving indexes for faster future searches. For function details, see [Full-text search ](https://docs.byteplus.com/docs/bytehouse/full_text_search).<br><br>* **GIS**: This function provides high\-performance GIS geospatial analysis capabilities, offering high\-performance geographic data analysis services for scenarios like location insights and user segmentation. For function details, see [GIS spatiotemporal analysis](https://docs.byteplus.com/docs/bytehouse/gis-spatiotemporal-analysis).<br><br>* **VectorSearch**: Vector search offers management and similarity query functions for vector data, enhancing retrieval performance by supporting various common approximate nearest neighbor (ANN) algorithms to handle unstructured data. For function details, see [Enable vector search](https://docs.byteplus.com/docs/bytehouse/vector-retrieval). |
   ||**Local disk**: This function caches cold data from object storage to increase data hot\-read probability, targeting high\-performance, high QPS scenarios to improve your query efficiency.<br><br>You can enable the virtual warehouse local disk feature as needed, starting from 100 GB. For specifications and pricing of the local disk, please refer to [Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache). |
   ||**Load Elasticity**: Load elasticity is the auto\-scaling feature of the virtual warehouse that dynamically allocates elastic resources and adjusts specifications automatically based on preset policies to adapt to workload fluctuations. You can set the load elasticity policy for the virtual warehouse as needed. The system automatically scales according to the set thresholds. For detailed introduction to load elasticity, see [Load elasticity](https://docs.byteplus.com/docs/bytehouse/docs-virtual-warehouses#8ad22697).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Load elasticity is not supported below the L specification. Before use, ensure your virtual warehouse specification is L or higher.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Virtual warehouse local disk scales proportionally with the basic resources of the virtual warehouse. When the virtual warehouse elastically expands, the local disk scales proportionally with the elastic resources; when the virtual warehouse elastically shrinks, the local disk deletes the cache of the corresponding compute nodes. The expanded elastic cache will be billed separately on a pay\-as\-you\-go basis.</div><br> |
   

4. After configuration, click **Proceed to order**, and the system will automatically create and start the virtual warehouse. You can check its status in the virtual warehouse list. When the virtual warehouse status is **Running**, it indicates the virtual warehouse was created successfully.

   After creation, set the default virtual warehouse resources for the current environment and user to ensure normal data operations. For operation details, see [Set the default write virtual warehouse](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#e4ec3478) and [Set user parameters](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#08d78c94).


<span id="220e473b"></span>
## **Edit** virtual warehouse

<span id="0ec4ad8c"></span>
### Change billing method

You can refer to [Virtual warehouse specification change](https://docs.byteplus.com/docs/bytehouse/virtual-warehouse-specification-change) to change the billing method.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Changing the billing method only affects the virtual warehouse’s basic resources. Elastic resources allocated by load elasticity will still be charged on a pay\-as\-you\-go basis.</div>


<span id="2c35e58f"></span>
### Edit virtual warehouse configuration


1. In the virtual warehouse list, click the **Edit** button in the Actions column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f7e562646344e99bc585b6794e2ca38~tplv-goo7wpa0wc-image.image) </span>

2. On the edit page, adjust the virtual warehouse specifications, description, auto resume/suspend, virtual warehouse type, advanced features, virtual warehouse local disk, and load elasticity as needed. After adjusting virtual warehouse specifications, local disk, advanced features, and load elasticity, costs will change and display on the page in real time. Please monitor cost changes.

   For virtual warehouse specifications, you can refer to [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm). In Cloud Monitor, view the overall resource utilization to judge if you need to adjust the virtual warehouse specifications.

   If you disable elastic resources for a virtual warehouse while editing it, the system waits for running tasks to finish before terminating the corresponding elastic resources.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7b6d03f831e4886954fe9bf8696a770~tplv-goo7wpa0wc-image.image) </span>

3. After adjustment, click **Confirm**. The system updates the configuration automatically. When the status bar of the virtual warehouse list changes from **Pending** to **Running**, it means the configuration adjustment is complete. You can verify success by reviewing the parameters.


<span id="ea65d64c"></span>
## View virtual warehouse monitoring

After creating a virtual warehouse, you can view the monitoring metric data of the virtual warehouse on **Tenant management** \> **Cloud monitor** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb1bc002cd643a8bd5da34325c88b66~tplv-goo7wpa0wc-image.image) </span>

For details about the currently supported virtual warehouse monitoring metrics and operation guidelines for creating monitoring and alarms via BytePlus Cloud Monitor, please refer to [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm).
