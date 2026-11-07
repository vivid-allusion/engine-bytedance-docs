---
title: "New feature release notes"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/New_feature_release_notes"
---

This topic lists product feature updates and related documentation for Table Storage for HBase.

<span id="tddIig7Y"></span>
## September 2026


|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Thrift service optimization and billing initiation<br><br>&nbsp;<br><br> |HBase has completed the Thrift service upgrade. The new high\-availability Thrift supports flexible configuration of Thrift Server node specifications and quantities, and is billed based on the selected configuration. After high\-availability Thrift is launched, applying for the legacy Thrift2 connection address is no longer supported. Instances with the legacy Thrift2 already enabled can continue to use it free of charge or upgrade to high\-availability Thrift. After the upgrade, you only need to update the connection address in your application configuration; the original access method remains unchanged. |September 21, 2026<br><br> |All<br><br> |* [Enabling or disabling high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address)<br><br>* [Changing high-availability Thrift Server configurations](https://docs.byteplus.com/en/docs/HBase/Changing_high-availability_Thrift_Server_configurations)<br><br>* [Upgrading to high-availability Thrift connection address](https://docs.byteplus.com/en/docs/HBase/Upgrading_to_high-availability_Thrift_connection_address) |


<span id="ZXKo6ERs"></span>
## July 2026


|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Offline 4 C 16 GiB specification<br><br> |HBase has discontinued the 4 C 16 GiB node specification, which is not recommended for use in production environments. If you have special requirements, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for application to use them. |July 21, 2026 |All |[Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications)<br><br> |


<span id="0FypeVbh"></span>
## March 2026


|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Supports setting maintenance window for instances |After setting the maintenance window for instance, some operations on the instance can be performed within these periods. |March 10, 2026 |All |[Configuring maintenance window](https://docs.byteplus.com/en/docs/HBase/Configuring_maintenance_window) |
|Added operation and maintenance events |The operation and maintenance events section displays all operation and maintenance events scheduled to be executed within the maintenance window under the specified region of the target account. Events with a status of "waiting for execution" can be canceled or their execution time modified in the event list. |March 10, 2026 |All |[Viewing operation and maintenance events](https://docs.byteplus.com/en/docs/HBase/Viewing_operation_and_maintenance_events) |
|Support disabling DDL function |To ensure the stability of HBase instance table structures and prevent accidental or erroneous DDL operations on tables, HBase provides a function to disable DDL. Enabling this function will prevent any DDL operations on the instance's tables. |March 10, 2026 |All |[Disable DDL](https://docs.byteplus.com/en/docs/HBase/Disable_DDL) |
|Offline sales specifications |HBase has taken offline some node specifications that are not recommended for production environments (2 C 4 GiB, 4 C 8 GiB, 8 C 16 GiB, 8 C 32 GiB). If you have special requirements, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for application to use them. |March 10, 2026 |All |[Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications) |
|China (Beijing), China (Shanghai), and China (Guangzhou) regions officially available<br><br> |The Table Storage for HBase officially is available for sale in the China (Beijing), China (Shanghai), and China (Guangzhou) regions starting from Beijing time on March 10, 2026.<br><br> |&nbsp;<br><br>March 10, 2026 |* China (Beijing)<br><br>* China (Shanghai)<br><br>* China (Guangzhou)<br><br><br> |[Service endpoint](https://docs.byteplus.com/en/docs/HBase/Request_structure#.5pyN5Yqh5Zyw5Z2A)<br><br> |


<span id="ZxGkDdKN"></span>
## December 2025


|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Add more monitoring metrics<br><br> |HBase adds QPS and latency monitoring metrics for Get, Scan, Put, and BatchPut requests at the instance and RegionServer levels, providing more comprehensive data support to help you better understand database performance and manage and plan resources in a timely manner. |December 4, 2025 |All<br><br> |[Monitoring metrics](https://docs.byteplus.com/en/docs/HBase/Monitoring_metrics) |
|Optimization of monitoring metric names |The instance level **QPS** metric has been optimized to **Read QPS**, and the RegionServer level **QPS** and **TPS** metrics have been optimized to **Read QPS** and **Write QPS**. |December 4, 2025 |All ||


<span id="BtYqZKdL"></span>
## November 2025


|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Support yearly or monthly subscription billing method |Yearly or monthly subscription is a billing method that requires paying up front when you create a new instance. When buying HBase instances, subscription is more cost\-effective than pay\-as\-you\-go billing. |November 5, 2025 |Asia Pacific (Johor) |[Yearly or monthly subscription](https://docs.byteplus.com/en/docs/HBase/Yearly_or_monthly_subscription) |
|Support hot and cold data separation<br><br> |HBase provides Capacity storage as a cold storage medium, supporting the separation of hot and cold storage for data in a table column family based on data write time. By using different storage media, storage costs can be effectively reduced. |November 5, 2025 |Asia Pacific (Johor) |[About hot and cold data separation](https://docs.byteplus.com/en/docs/HBase/About_hot_and_cold_data_separation) |
|Support index management<br><br>&nbsp;<br><br> |HBase index management integrates Table Storage for HBase with Cloud Search services, providing multi\-dimensional indexing capabilities. This feature caters to various data types and query requirements, accelerating data queries.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, the index management feature is in gray\-scale release. If you need to use it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> and contact technical support to apply for usage.</div><br> |November 5, 2025 |Asia Pacific (Johor) |[Index overview](https://docs.byteplus.com/en/docs/HBase/Index_overview) |


<span id="8QRf19mS"></span>
## September 2025


|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Product released |Table Storage for HBase is released in beta stage for the first time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, the Table Storage for HBase is in gray\-scale release. If you need to use it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> and contact technical support to apply for usage.</div><br> |September 19, 2025 |All |[Table Storage for HBase](https://docs.byteplus.com/en/docs/HBase/About_Table_Storage_for_HBase) |
