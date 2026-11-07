---
title: "What is Server Migration Center?"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/What-is-Server-Migration-Center"
---

Server Migration Center (SMC) is a server migration platform provided by the cloud platform. You can use SMC to migrate your on\-premises servers, virtual machines, cloud servers from other cloud platforms (such as Alibaba Cloud, Huawei Cloud, and Tencent Cloud), or other types of servers to the cloud platform. Migrating to the cloud platform addresses issues such as limited existing resources, inability to meet business requirements, and poor scalability.

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Concept |Description |
|---|---|
|Migration source (or source server) |Refers to the data center servers, virtual machines, cloud servers from other cloud platforms, or other types of servers to be migrated. |
|Client |The server migration tool Agent is used to collect migration source information and synchronize it to Server Migration Center. |
|Migration template |A tool used to specify configurations such as type, volumes, and network for the target ECS instance in a templated manner. During the migration process, SMC automatically creates the target instance based on the migration template. This reduces resource waste caused by caused by creating the target instance in advance. |
|Migration task |After migration source information is imported, the SMC console automatically generates migration source records. You can create migration tasks for the migration sources and start the tasks to perform migrations in the SMC console. |
|Target instance |When you create a migration task, you need to select an ECS instance as the target instance. After migration, data from the source server will overwrite the data in the system volume and data volumes of the target instance. |
|Server migration |A one\-click feature that migrates data from your source servers (such as self\-built data center servers, on\-premises virtual machines, and instances from other cloud providers) to ECS instances or custom images of the platform. |
|Operating system migration |A feature that allows you to replace the operating system of an ECS instance on the platform without stopping the instance. Data in the system volume will not be lost after replacement by using this feature. |
