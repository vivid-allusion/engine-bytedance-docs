---
title: "Product specification family"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/product-specification-family"
---

This topic describes the instance specification families of RDS for SQL Server, including **General Specifications** and **Exclusive Specifications**.

<span id="instance-specification-family"></span>
## Instance specification family


|**Specification family** |**Specification type** |Description |**Usage scenario** |
|---|---|---|---|
|**General Specifications** |**General Type II** |* General specification instances have completely exclusive CPU and memory resources, and their performance is stable for a long time without being affected by other instances on the physical machine. However, there is a difference in the CPU memory ratio of general specifications and exclusive specifications, please refer to the actual situation.<br><br>* General specification instances improve utilization through resource reuse, thus achieving cost\-effective results. |General specification instances are suitable for cost\-effective scenarios with low cost, high availability, high performance, and large memory. |
|||||
|**Exclusive Specifications** |**Exclusive Type II** |* Exclusive specification instances have fully exclusive CPU and memory resources, and their performance is stable for a long time without being affected by other instances on the physical machine. However, there is a difference in the proportion of CPU memory between exclusive specifications and general specifications, please refer to the actual situation.<br><br>* The top configuration of the exclusive specification instance is the exclusive TCE\-metal type, also known as the exclusive host type, which completely monopolizes all the resources of a TCE\-metal. |Exclusive specification instances perform better and more stably, and are suitable for business scenarios with database\-based systems, such as finance, e\-commerce, government affairs, and large and medium\-sized Internet services. |
|||||


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">RDS for SQL Server supports the creation of BYOL specification instances, which is currently a whitelisted feature. If you need to use it, you can <a href="https://console.byteplus.com/workorder/create">Submit a work order</a> to contact technical support.</div>


<span id="instance-spec-list"></span>
## Instance spec list

For details on the specifications, CPU, memory, and storage space for the primary instances supported by RDS for SQL Server instances, see the [Primary instance specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification).

<span id="cost"></span>
## Cost

The cost of different instance specification families varies, please refer to the actual situation, you can also refer to the [Billing items and price](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/charge-items-and-price) to view the price information of each specification.
