---
title: "Adding the CIDR block of the DTS server"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server"
---

When using Database Transmission Service (DTS) for data transmission, if the database instance is built via BytePlus ECS and the public network, or uses a Virtual Private Cloud (VPC) for data migration, synchronization, or subscription, and the target instance has access restrictions configured, you must first add the DTS server's CIDR block to the allowlist or security group of the corresponding database instance. This is to allow normal access by DTS. Otherwise, task creation for the DTS may fail.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Background**


* Access method: DTS supports three ways to access databases: **BytePlus**, **Public network**, and **Express network**. When creating a data transmission task, the access method depends on the combination of task type, database type, source database, and target database, as follows:

   * BytePlus instance: If you create instances in the BytePlus console, such as RDS for MySQL or Cache for Redis, it is recommended to select the BytePlus as the **Access method** when creating the database transmission service.

   * VPC: If you transmit data through VPN or a dedicated line, it is recommended to select VPC as the **Access method** when creating the data transmission task.

   * Public network: If transmitting data from other cloud vendors, select Public network as the **Access method** when creating the database.

* Adding method: If the source or target end uses the BytePlus access method, the system will bind an allowlist starting with `dts` to the instance by default when creating the database transmission service. If the source or target end uses other access methods, you need to manually add the DTS server CIDR block to the security group or allowlist before creating the data transmission task. For details, refer to [Adding the CIDR block](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server#.5re75YqgLWlwLeWcsOWdgOautQ==).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If the source or target endpoint of the DTS is accessed via a **Public IP address**, add all IPs and CIDR blocks of the DTS servers in the corresponding regions to the allowlist or security group of the database instance when using DTS for the first time or upon receiving a DTS allowlist expansion notification.

* Ensure that all IPs and CIDR blocks of the DTS for the corresponding regions have been added to the allowlists or security groups of both the source and target endpoints of DTS. It is critical to add the complete set of IPs during configuration. Otherwise, after DTS task disaster recovery, new nodes may be unable to connect to the database instance, potentially causing task delays or interruptions.

* Manually adding CIDR blocks of DTS servers may pose security risks. Using this product indicates you understand and acknowledge potential security risks and need to implement basic security measures, including but not limited to strengthening account password complexity, limiting open ports for each subnet, using authentication method communication for internal APIs, regularly reviewing and restricting unnecessary subnets, or accessing it via intranet (**VPC**).

* Do not apply the allowlisted IPs or security group IPs added for DTS to non\-DTS business needs. Task failures caused by this issue are not covered under the SLA of Database Transmission Service (DTS).


<span id=".5re75YqgLWlwLeWcsOWdgOautQ=="></span>
## **Add the CIDR block**

If your instance is connected to Database Transmission Service (DTS) through a **Public network ** or ** Express network**, you need to manually add the IP addresses of DTS servers in the corresponding regions to the allowlist or security group of your database.


1. Confirm whether the DTS server CIDR block to be added is for the source end or the target end.

2. Confirm the region to which the DTS server CIDR block to be obtained belongs.

   
   |**Task type** |**Add the database instance of the CIDR block** |**Require adding the region where the CIDR block of the DTS server belongs** |
   |---|---|---|
   |Data migration |Source database |Region where the target database is located |
   ||Target database |Region where the target database is located |
   |Data subscription |Source database |Region where the target database is located |
   |Data synchronization |Source database |Region where the target database is located |
   ||Target database |Region where the target database is located |
   

3. Check the DTS server CIDR block to add according to the region of the database instance. For more information on the CIDR block of DTS servers, refer to [CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server#.ZHRzLeacjeWKoeWZqOeahC1pcC3lnLDlnYDmrrU=)..

4. Add the queried CIDR block to the allowlist or security group rules.


<span id=".ZHRzLeacjeWKoeWZqOeahC1pcC3lnLDlnYDmrrU="></span>
## CIDR block of the DTS server

To enable DTS to access instances connected through self\-managed over a public network or VPC, add the corresponding subnet to the database's allowlist or security group based on the following prompts.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the DTS transmission task completes or is released, it is recommended to delete the added DTS server IP addresses or CIDR blocks from the instance to prevent DTS from continuing to access the database instance.</div>


<span id=".5YWs572R6Ieq5bu6"></span>
### Connected over public network

When your instance is connected over public network, the subnet CIDR blocks for such connections will vary across different regions. For details, refer to the following table.


|**Region** |**Access method** |
|---|---|
||Public network |
|**China (Guangzhou)**  |221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27 |
|**China (Shanghai)**  ||
|**China (Beijing)**  ||
|**China (Hong Kong)**  |101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27 |
|**Asia Pacific (Johor)**  ||
|**Asia Pacific (Jakarta)**  |221.194.189.0/27,157.148.90.32/27 |


<span id=".5LiT5pyJ572R57uc"></span>
### VPC

When your instance connects via the VPC, the subnet of the VPC must communicate with the source or target database. To allow DTS to access instances in the VPC normally, add the subnet CIDR block to the source or target database allowlist or security group rules.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

Refer to the following documents for creating BytePlus data migration, synchronization, and subscription tasks:


* [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions)

* [Synchronization solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions)

* [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions)
