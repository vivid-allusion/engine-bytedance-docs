---
title: "Read-only overview"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/read-only-overview"
---

Read\-only instances are primarily used to offload the read pressure of the master instance. When there are a large number of read requests in the database, and the master instance cannot meet the pressure of a large number of read and write requests at the same time, you can create a read\-only instance for the master instance, thereby reducing the read pressure of the master instance and improving the overall processing power of the system. This article introduces the application scenarios of the read\-only instance, matters needing attention, and the difference and comparison between the main instances.

<span id="billing"></span>
## Billing

The billing method, lifecycle, etc. of the read\-only instance are consistent with the billing of the primary instance. For more information about billing, see [Product Billing](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/price-overview).

<span id="application-scenario"></span>
## application scenario

Read\-only instances are often used in high\-concurrency, large\-data read scenarios, such as:


* **Big data analytics**

   When faced with complex query and reporting scenarios, it usually requires a large amount of computing resources, which may affect the performance of the master instance database.

* **Highly concurrent reads**

   In the face of applications with very frequent read requests, read\-only instances can be used to share the read pressure of the main instance and improve the throughput of the system.

* **load balance**

   In the case of multiple read\-only instances, load balancing technology can be used to distribute read requests to different read\-only instances to further improve the processing power of the system.

* **report generation**

   Report generation usually requires a large number of read operations to the database, and using read\-only instances can reduce the performance impact of the primary instance.


<span id="precautions"></span>
## Precautions


* An instance can create up to 5 read\-only instances, and multiple read\-only instances under the master instance are independent of each other and do not affect each other.

* The time to create a read\-only instance is proportional to the amount of data and I/O of the master instance, so you need to evaluate and optimize the amount of data and I/O performance of the master instance before creating a read\-only instance to reduce the time it takes to create a read\-only instance to impact the performance of the master instance.

* The master instance in a read\-only instance change or change does not support the creation of new read\-only instances. The master instance in a read\-only instance change does not support modifying the configuration of the master instance.

* Only creating a read\-only instance on the master instance of the cluster version is supported, and switching the master instance to a read\-only instance is not supported.

* The data of the read\-only instance is replicated and synchronized from the data of the primary instance, and filtering of certain data is not supported.

* Function\-related notes:

   * Backup and recovery management: Since the primary instance has been backed up, backup settings and backup and recovery operations for read\-only instances are not supported.

   * Log management: Slow logging that starts read\-only instances is not supported.


<span id="the-difference-between-a-read-only-instance-and-a-master-instance"></span>
## The difference between a read\-only instance and a master instance

A read\-only instance and a primary instance are two different types of database instances. The main instance is used to handle read and write operations and is responsible for writing and reading data; the read\-only instance is used to read data, improve the reading performance of the database, and can be used as a backup and disaster recovery scheme for the main instance. The main differences between them are shown in the following table.


|**module** |**read\-only instance** |**master instance** |
|---|---|---|
|**function** |* A read\-only instance is a copy of the primary instance and can only be used to read data. Write operations are not supported.<br><br>* When a read\-only instance is deleted, no backup is performed. |* The main instance is the main database instance that mainly handles read and write operations, and can perform data addition, deletion, modification and search operations.<br><br>* When a primary instance is deleted, a final backup is retained. |
|**data synchronization** |The read\-only instance synchronizes data through the data replication function of the primary instance, so there may be some latency. |The master instance is responsible for synchronizing data to all read\-only instances to ensure data consistency. |
|**access load** |Read\-only instances can share the read requests of the primary instance, improving the read performance of the database. |The master instance is responsible for handling all read and write requests and bears the main access load. |
|**connection management** |Cloud Database SQL Server provides two connection address access management read\-only instances:<br><br><br>* The system provides a single read\-only cluster connection address for multiple read\-only instances by default.<br><br>* The system provides a read\-only node connection address for each read\-only instance individually. |The system provides a connection address for the master instance to access the administrative SQL Server instance. |
|**availability** |Primary and read\-only instances can be deployed in different Availability Zones to improve the availability and disaster tolerance of the database. ||


<span id="faq"></span>
## FAQ

<span id="does-read-only-instance-data-synchronization-affect-the-performance-of-the-primary-instance"></span>
### Does read\-only instance data synchronization affect the performance of the primary instance?


* When creating a read\-only instance: If the database & table volume in the primary instance is large, the CPU, memory, and I/O resources of the primary instance may be affected during the read\-only instance creation phase.

* Read\-only instance runtime: Data synchronization of a read\-only instance can affect the performance of the primary instance, but usually to a lesser extent. As the master instance performs a data write operation, changes to the data are logged to a binary log and then sent to the read\-only instance, which synchronizes the data by reading the log. This process requires relatively little CPU, memory, and I/O resources for the primary instance.


Under normal circumstances, the data synchronization of a read\-only instance has a relatively small impact on the performance of the primary instance, but when the write operations of the primary instance are very frequent or the number of read\-only instances is very large, then data synchronization may have a significant impact on the performance of the primary instance. Therefore, when using read\-only instances, it is necessary to reasonably configure the number of read\-only instances according to the actual business requirements and system environment, so as to achieve the best performance and cost effect.

<span id="how-to-determine-how-many-read-only-instances-need-to-be-created-to-ensure-the-optimal-performance-of-the-system"></span>
### How to determine how many read\-only instances need to be created to ensure the optimal performance of the system?

Determining how many read\-only instances need to be configured to ensure optimal system performance depends primarily on the following factors:


* **read load**

   When your application has a large number of read operations and the primary instance cannot handle these read requests, you need to configure multiple read\-only instances to share the read load.

* **performance monitoring**

   You can understand the CPU, memory, and I/O resource usage of a master instance by monitoring its performance. If the resource usage of the primary instance remains high, you need to configure a read\-only instance to share the load.

* **business requirement**

   Determine the number of read\-only instances based on business requirements. For example, when you need to perform operations such as big data analytics or report generation, you need to configure multiple read\-only instances to provide sufficient computing resources.

* **Cost Considerations**

   The cost of configuring multiple read\-only instances also increases, so the number of read\-only instances needs to be determined according to your budget.


How many read\-only instances to create requires a combination of factors such as read load, performance monitoring, business requirements, and cost considerations. If you are unsure how many read\-only instances you need to create, you can start by creating a small number of read\-only instances and gradually adjust them based on actual performance and load.

<span id="when-do-you-need-to-increase-the-configuration-of-a-primary-instance-rather-than-just-a-read-only-instance"></span>
### When do you need to increase the configuration of a primary instance rather than just a read\-only instance?

Whether you need to increase the configuration of the master instance depends on the actual load, resource usage, and business requirements. You usually need to add a master instance configuration instead of just a read\-only instance in the following cases:


* **High write load**

   Read\-only instances are primarily used to handle read requests, and when your application has a large number of write requests, simply increasing the number of read\-only instances may not significantly improve system performance. In this case, you need to increase the configuration of the primary instance, such as CPU, memory, or storage space, to improve write performance.

* **Insufficient primary instance resources**

   If the CPU, memory, or I/O resource usage of the primary instance remains high, you need to increase the configuration of the primary instance to provide more resources to handle requests.

* **data synchronization delay**

   If the data synchronization delay of the read\-only instance is large, it may affect the accuracy of the read request. In this case, increasing the configuration of the master instance helps to improve the speed of data synchronization, thereby reducing the delay in data synchronization.

* **business requirement**

   According to the specific business requirements, the configuration of the master instance is increased as needed. For example, when you need to perform operations such as big data processing or real\-time analysis, you need a more powerful master instance to provide sufficient computing resources.
