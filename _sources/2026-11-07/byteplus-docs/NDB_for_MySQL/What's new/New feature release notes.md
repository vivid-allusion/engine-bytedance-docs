---
title: "New feature release notes"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/New_feature_release_notes"
---

This topic lists product feature updates and related documentation for NDB for MySQL.

## October 2026

|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Support parameter template comparison<br><br> |Support comparing parameter configurations of different parameter templates and displaying parameter differences. |October 15, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Compare parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Compare_parameter_template) |
|Add more modifiable parameters |More modifiable parameters are added so that you can flexibly adjust parameter configurations based on your business needs. |October 15, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |* [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_8_0)<br><br>* [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_5_7) |
|Optimize configuration change capabilities |Instances with general\-purpose specifications can be scaled up or down without restarting the instance when specific conditions are met. This effectively improves configuration change efficiency and reduces the impact of configuration changes on instances. |October 15, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |* [Changing node specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications)<br><br>* [Enabling fast specification change](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Enabling_fast_specification_change) |
|Add more monitoring metrics |A monitoring metric for prepaid storage usage is added to help you stay informed about storage capacity usage and plan storage resources accordingly. |October 15, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Monitoring metrics](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Monitoring_metrics)<br><br> |
|DescribeStoragePayablePrice: Add subscription storage price query |The DescribeStoragePayablePrice API now supports querying subscription storage prices. When calling the API, you can query the price of pay\-as\-you\-go or subscription storage based on the billing method. |October 15, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[DescribeStoragePayablePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeStoragePayablePrice)<br><br> |

## July 2026

|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Supports associating security groups with allowlists<br><br> |It supports associating allowlists with ECS security groups. After associating a security group, all IP addresses under the corresponding security group can be imported into the allowlist. |July 30, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |* [Creating an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist)<br><br>* [Modifying an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist)<br><br>* [Synchronizing security group](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Synchronizing_security_group) |
|Support connection pooling |NDB for MySQL supports session\-level connection pooling and transaction\-level connection pooling, which can effectively reduce the database load pressure caused by a large number of connections.<br><br>> **Tip**<br><br><br>> This feature is in gray\-scale release. If you need to use it, [submit a ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.<br> |July 30, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool)<br><br> |
|Support connection persistent<br><br> |The connection persistent feature ensures that the connection will not be actively disconnected during operation, thereby improving the stability of the business system.<br><br>> **Tip**<br><br><br>> This feature is in gray\-scale release. If you need to use it, [submit a ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.<br> |July 30, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong)<br><br> |[Connection persistence](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_persistence) |
|Add modifiable parameters |Add the modifiable parameters innodb_open_files and open_files_limit to control the maximum number of files that the InnoDB storage engine can open at one time. |July 30, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |* [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_8_0)<br><br>* [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_5_7) |
|Supports for Statement Outline<br><br> |Supports Statement Outline, which associates an SQL execution plan with an SQL query template. This allows users to fix the query plan without modifying the SQL, avoiding stability risks caused by unexpected changes in the execution plan. |July 8, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Statement Outline](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Statement_Outline) |

## June 2026

|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Added compressed storage type<br><br> |NDB for MySQL has launched a new intelligent compression storage type that employs intelligent compression algorithm technology to reduce the storage cost per unit of data capacity while keeping performance impact within controllable limits. |June 30, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications) |
|Supports modification of VPC and subnet |Supports modifying an instance's VPC and subnet after the instance is successfully created.<br><br>> **tip**<br><br><br>> This feature is in gray\-scale release. If you need to use it, [submit a ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.<br> |June 1, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Modifying VPC and subnet](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_VPC_and_subnet)<br><br> |
|Allowlist optimization<br><br> |Optimizes allowlist display and supports one\-click copying of all IP addresses.<br><br> |June 1, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Viewing allowlist information](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_allowlist_information) |
|Connection address prefix rule update |The connection address prefix rule has been updated with a new restriction: the ID of another instance is prohibited from being used as a prefix.<br><br> |June 1, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Modifying address prefix and port](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_address_prefix_and_port) |

## March 2026

|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Support system parameter templates |NDB for MySQL provides a default parameter template for each database engine version, which includes all parameters and default parameter values supported by the version. The parameters in the system template are a collection of parameters for all kernel versions. When applying a parameter template, parameters unsupported by the instance's kernel version are automatically ignored. |March 23, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Viewing parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_template) |
|Supports copying and editing parameter templates |NDB for MySQL provides the ability to copy and edit parameter templates. You can quickly create the new template by copying the existing one and then editing it as needed. |March 23, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |* [Editing parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_parameter_template)<br><br>* [Copying parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Copying_parameter_template) |

## January 2026

|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Support yearly or monthly subscription billing method<br><br> |Yearly or monthly subscription is a billing method that requires paying up front when you create a new instance. When buying instances, subscription is more cost\-effective than pay\-as\-you\-go billing. |January 22, 2026 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[Yearly or monthly subscription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Yearly_or_monthly_subscription) |

## July 2025

|**Feature** |**Description** |**Release time** |**Release region** |**Related documents** |
|---|---|---|---|---|
|Product released |NDB for MySQL first public release. |July 23, 2025 |Asia Pacific (Johor)、Asia Pacific (Jakarta)、China (Hong Kong) |[About NDB for MySQL](https://docs.byteplus.com/en/docs/NDB_for_MySQL/About_NDB_for_MySQL) |
