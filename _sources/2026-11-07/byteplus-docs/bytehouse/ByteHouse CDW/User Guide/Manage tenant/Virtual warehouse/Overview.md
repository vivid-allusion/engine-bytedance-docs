---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-virtual-warehouses"
---

This tutorial introduces the functional definition, core advantages, and usage guidelines of ByteHouse Cloud Data Warehouse Edition's (ByteHouse CDW) virtual warehouse.

<span id="86b4241f"></span>
# Overview

The virtual warehouse (VW) is a cluster of compute resources in ByteHouse that provides core resources such as CPU, memory, and temporary storage. It offers stable computing power support for various data operations to run users' SQL queries and write tasks, including:


* Running SQL statements that require compute resources (such as retrieving rows from tables and views), covering both short\-term and long\-term query scenarios.

* Performing DML operations, such as:

   * Row\-level operations like deleting, inserting, and updating data in tables;

   * Data flow operations that load data into tables or export data from tables.


The virtual warehouse offers isolated and elastic compute resources. Different virtual warehouses operate independently without interference, suitable for multi\-tenant and multi\-business workload scenarios.


* Isolated computation: ByteHouse supports providing independent compute resources for different users or workloads to prevent resource contention.

* Elastic scaling: Virtual warehouses can dynamically increase or decrease compute nodes based on the load to optimize cost and performance.


<span id="1f411c1f"></span>
# Core advantages

ByteHouse virtual warehouses have the following advantages:


* **Resource isolation and read\-write separation**: ByteHouse virtual warehousesupports read\-write separation, assigning data import and query operations to different virtual warehouses. It also enables resource isolation among different departments and business queries to prevent interference and improve stability.

* **Elastic scaling and cost optimization**: The virtual warehouse scales elastically according to business needs, reducing resource waste while ensuring performance, achieving cost control and maximizing resource utilization.

* **Supports OLAP and ELT\-type virtual warehouses**: You can choose the type as needed and flexibly customize parameters based on business scenarios. This meets OLAP analytical performance optimization requirements and supports ELT task stability in batch processing scenarios.

* **Custom virtual warehouse parameters**: ByteHouse provides fixed parameter templates for virtual warehouses, supports parameter configuration to improve data warehouse performance, and allows adding custom SQL parameters to better meet specific business needs.

* **Fine\-grained access control**: ByteHouse supports fine\-grained access control over virtual warehouse resources to meet resource usage permission management requirements for different roles.

* **Flexible specification selection**: You can select virtual warehouses of XS, S, M, L, or XL specifications based on demand. After creation, you can manually adjust the virtual warehouse specification based on actual CPU or memory load, referring to [Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#b8abd1e8). If the current cluster performance does not meet your requirements, you can contact [ByteHouse](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000067) through a ticket to customize the virtual warehouse configuration.


<span id="37dd54eb"></span>
# Core features

<span id="b97ae460"></span>
## Automatic resume and suspend

The ByteHouse CDW virtual warehouse supports an automatic resume\-suspend policy to help you save resource costs. When the virtual warehouse remains idle beyond the set period, the automatic resume\-suspend function shuts down the cluster automatically. No fees are incurred while the virtual warehouse is off, saving costs and avoiding unnecessary resource waste during low workload periods. When you have query demands, sending a query request automatically starts the virtual warehouse to activate computing resources and process the query. This mode flexibly adjusts resource usage based on actual workload, optimizing costs.

<span id="a3438358"></span>
## Read\-write separation

ByteHouse natively supports storage\-compute separation. Write and background tasks use write\-dedicated virtual warehouses, while front\-end queries use read\-dedicated virtual warehouses. Read and write jobs do not interfere, suitable for read\-write intensive business.


* Write: ByteHouse supports assigning a dedicated virtual warehouse to handle write tasks, ensuring real\-time data updates and accuracy. Write tasks usually require high data consistency and reliability, so dedicated computing resources are needed to ensure efficient execution.

* Read: ByteHouse supports assigning a dedicated virtual warehouse to handle query tasks to meet a large number of concurrent query requests. Query tasks often demand fast response times and accurate data. Dedicated computing resources provide faster query speeds and more stable service quality.


<span id="f06d0e9b"></span>
## Scheduled elasticity

ByteHouse supports flexible scheduling of virtual warehouse scaling policies based on business needs. You can use [Cron Task Center](https://docs.byteplus.com/docs/bytehouse/docs-cron-task) to set a time period, and the system automatically triggers elastic scaling according to the schedule to match query traffic and workloads at different times. You can plan compute resource expansion or reduction times in advance based on business needs and resource usage forecasts to ensure efficient resource use and timely response.

With ByteHouse's scheduled elasticity, you gain the following benefits:


* **Cost optimization**: ByteHouse automatically reduces resource scale during low business periods to significantly lower compute costs.

* **Automated operations**: ByteHouse can help you achieve intelligent resource scheduling and configuration adjustments without relying on external tools or manual intervention, improving operational efficiency.


<span id="8ad22697"></span>
## Load elasticity

Load elasticity means ByteHouse virtual warehouses support automatic scaling. For L size and above virtual warehouses, elastic resources are dynamically allocated and adjusted automatically based on preset policies to match business load fluctuations. Elastic resources are billed based on actual usage.

You can refer to the operations in [Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse) to activate load elasticity. After activation, the virtual warehouse consists of **basic resources** and **elastic resources**. When CPU or memory metrics reach the set threshold, the system automatically scales elastic resources. The triggers are as follows:


* **Scaling up trigger**: When the average value of either CPU or memory metrics exceeds the threshold (80% or 90%) for 5 consecutive periods (each period is 1 minute, total 5 minutes), the system automatically scales up.

* **Scaling down trigger**: After scaling up elastic resources, when the average value of either CPU or memory metrics falls below the threshold (40%) for 5 consecutive periods, the system automatically scales down.


During scaling, load elasticity uses a stepwise adjustment strategy, scaling elastic resources up or down by one size at a time:


* Scaling up range is up to 3 sizes above the basic resources. For example, if the basic resource size is L, elastic resources can be scaled up gradually to L, XL, and 2XL sizes.

* When scaling down, elastic resources reduce stepwise from the current highest size to zero, which means elastic resources are turned off.

* When the specifications of the base resources for a virtual warehouse are adjusted, the elastic resources will automatically adapt to the latest base resource specifications in the next expansion cycle and perform scaling operations according to the new range. If the expanded virtual warehouse resources still do not meet your business needs and you need to increase elastic resources to higher specifications, you can first refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#9fe625be) to upgrade the base resource specifications.


The following table uses a virtual warehouse with base resources of L specification as an example to demonstrate the load elasticity feature:


* **Trigger condition**:

   * Scale up: CPU/memory load exceeds 80% and lasts for 5 consecutive periods.

   * Scale down: CPU/memory load falls below 40% and lasts for 5 consecutive periods.

* **Scale\-up process**:

   * If the CPU load of the L\-specification virtual warehouse exceeds the set threshold of 80% for 5 consecutive periods (T\-1 to T\-5), the system will scale up in a laddered manner in the T\-6 period, first scaling up elastic resources by 1 specification (i.e., L→L+L).

   * If the CPU load in the next 5 periods (T\-7 to T\-11) still exceeds the threshold, the system will scale up to a higher specification in the T\-12 period (i.e., L+L→L+XL).

   * If the CPU load in the following 5 periods (T\-13 to T\-17) continues to exceed the threshold, the system will further scale up in the T\-18 period (i.e., L+XL→L+2XL), reaching the maximum scale of 2XL with no further scaling.

   * If the current computing group resources still cannot meet your business needs, you can refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#9fe625be) to adjust the base resource specifications first. The elastic resources will automatically adapt to the latest base resource specifications and continue to expand in the next scaling cycle.

   
   |Time |CPU Load |Memory Load |Basic Resources |Elastic Resources |Scale Up or Down |
   |---|---|---|---|---|---|
   |T\-0 |10% |30% |L |*  |No scaling up |
   |T\-1 |85% |30% |L |*  |No scaling up |
   |T\-2 |85% |30% |L |*  |No scaling up |
   |T\-3 |85% |30% |L |*  |No scaling up |
   |T\-4 |85% |30% |L |*  |No scaling up |
   |T\-5 |85% |30% |L |*  |No scaling up |
   |T\-6 |85% |30% |L |L |Expand to L |
   |T\-7 |85% |30% |L |L |No scaling up |
   |T\-8 |85% |40% |L |L |No scaling up |
   |T\-9 |85% |40% |L |L |No scaling up |
   |T\-10 |85% |40% |L |L |No scaling up |
   |T\-11 |85% |40% |L |L |No scaling up |
   |T\-12 |85% |40% |L |XL |Expand to XL |
   |T\-13 |85% |40% |L |XL |No scaling up |
   |T\-14 |85% |40% |L |XL |No scaling up |
   |T\-15 |85% |40% |L |XL |No scaling up |
   |T\-16 |85% |40% |L |XL |No scaling up |
   |T\-17 |85% |40% |L |XL |No scaling up |
   |T\-18 |85% |40% |L |2XL |Expand to 2XL |
   

* **Scale\-down process**:

   * During low business load periods, if the CPU load remains below the set threshold of 40% for 5 consecutive cycles (T\-1 to T\-5), the system will scale down stepwise from the current maximum specification (2XL) in cycle T\-6, first shrinking the elastic resources by one specification (i.e., L+2XL → L+XL).

   * If the CPU load remains below the threshold in the next 5 cycles (T\-7 to T\-11), the system will further scale down to a lower specification in cycle T\-12 (i.e., L+XL → L+L).

   * If the CPU load still remains below the threshold in the following 5 cycles (T\-13 to T\-17), the system will continue to shrink in cycle T\-18 (i.e., L+L → L). At this point, elastic resources will be zero, and the computing group will only retain the base resources without further scaling down.

   
   |Time |CPU Load |Memory Load |Basic Resources |Elastic Resources |Scale Up or Down |
   |---|---|---|---|---|---|
   |T\-0 |60% |60% |L |2XL |No scaling down |
   |T\-1 |30% |40% |L |2XL |No scaling down |
   |T\-2 |30% |40% |L |2XL |No scaling down |
   |T\-3 |30% |40% |L |2XL |No scaling down |
   |T\-4 |30% |40% |L |2XL |No scaling down |
   |T\-5 |30% |40% |L |2XL |No scaling down |
   |T\-6 |30% |40% |L |XL |Scale down to XL |
   |T\-7 |30% |40% |L |XL |No scaling down |
   |T\-8 |30% |40% |L |XL |No scaling down |
   |T\-9 |30% |40% |L |XL |No scaling down |
   |T\-10 |30% |40% |L |XL |No scaling down |
   |T\-11 |30% |40% |L |XL |No scaling down |
   |T\-12 |30% |40% |L |L |Scale down to L |
   |T\-13 |30% |40% |L |L |No scaling down |
   |T\-14 |30% |40% |L |L |No scaling down |
   |T\-15 |30% |40% |L |L |No scaling down |
   |T\-16 |30% |40% |L |L |No scaling down |
   |T\-17 |30% |40% |L |L |No scaling down |
   |T\-18 |30% |40% |L |*  |Shut down elastic resources |
   


<span id="214f4373"></span>
# Computing Group Usage Guide


* Computing Group Billing Rules:

   * [Specifications and pricing](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing)

   * [Virtual warehouse specification change](https://docs.byteplus.com/docs/bytehouse/virtual-warehouse-specification-change)

* Computing Group Usage:

   * [Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse)

   * [Manage parameters](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters)

   * [Start⧸Stop virtual warehouse](https://docs.byteplus.com/docs/bytehouse/start-stop-virtual-warehouse)

   * [Delete virtual warehouse](https://docs.byteplus.com/docs/bytehouse/delete-virtual-warehouse)
