---
title: "MySQL database bidirectional synchronization"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/MySQL_database_bidirectional_synchronization"
---

Database Transmission Service (DTS) supports MySQL database bidirectional synchronization. MySQL database bidirectional synchronization applies to multiple application scenarios, such as multi\-site high availability (unitization) and cross\-region data disaster recovery.

<span id="qonUuQ4j"></span>
## Bidirectional synchronization topology


|**Topology type** |**Topology diagram** |**Features** |
|---|---|---|
|**Single\-write and multi\-read** |<div style="text-align: center"><br><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34dc90911db16003fa6561f4b988143b.png" /></div><br><br><br> |The key features for the single\-write and multi\-read architecture are as follows.<br><br><br>* The primary region is responsible for write services and asynchronously synchronizes the written data to other secondary regions.<br><br>* The secondary region provides read services. If there is data in a secondary region that needs to be written, it must be written through the primary region.<br><br>* The single\-write and multi\-read architecture is not suitable for services that are highly sensitive to reads and writes. Cross\-region data transmission faces numerous issues and influencing factors, which can easily lead to latency. For businesses with high requirements for data read consistency, it is recommended to implement a cross\-region callback mechanism in the primary region.<br><br><br> |
|**Multi\-write and multi\-read**<br><br> |<div style="text-align: center"><br><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_188d9e29ab84f5171b348e7d9e672d42.png" /></div><br><br><br> |The key features for the multi\-write and multi\-read architecture are as follows.<br><br><br>* It supports multi\-region write and uses the data synchronization topology link for level\-by\-level synchronization.<br><br><br>The overall data latency is related to the complexity of the topology. The more complex the topology, the greater the latency.<br><br><br>* The system adopts a unitized read/write mode. In general scenarios, business operations perform read and write activities within their local region, achieving a closed loop of read\-write operations within the unit module. To avoid cross\-region reads after local writes, data updated in other regions will be synchronized to the associated region through the synchronization link.<br><br>* The business side needs to allocate traffic to different regions according to specific <rules\> (such as user ID distribution). You should avoid updating the same element in multiple regions. Accessing the same element needs to be routed to the corresponding unit.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The multi\-write and multi\-read topology requires unitization transformation of businesses. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/MySQL_database_bidirectional_synchronization#bX2McxRc">Business unit splitting</a>.</div><br> |


<span id="6qbWia40"></span>
## Conflict resolution strategy


|**Conflict resolution strategy** |**Description** |**Recommendation level** |
|---|---|---|
|**Conflict overwrite** |When source end data conflicts with destination data, the data from the source end overwrites the data from the destination.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In most cases, the data obtained by selecting conflict overwrite is the data that the business wants, but there are also special cases. For example, in the bidirectional synchronization scenario of A and B, if the time A writes data is t1, and the time B writes data is t2 (t1 is later than t2), in the reverse link scenario of A, when the data of B is transmitted to A, it will overwrite the data written by A after t1.</div><br> |Recommended first |
|**Ignore on conflict** |When the source end data conflicts with the destination data, ignore the conflict, and the source end and the destination write data respectively.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Conflict ignore will cause data inconsistency between the source end and the destination.</div><br> |Not recommended |
|**Abort on conflict** |When data conflicts occur between the source and target ends, you need to manually modify the conflict data; otherwise, the migration or synchronization task will pause and report an error.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When a data conflict occurs, the data synchronization will pause. You need to manually resolve the conflict data, and the business verification passed before you can continue the migration or synchronization task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">In this scenario, data consistency can be ensured, but the task pause will occur. Assume that an accident occurs in a certain end in an extreme scenario, and all subsequent data cannot be accessed.</div><br> |Recommended only in the test environment |


<span id="RJoGMagq"></span>
## Bidirectional synchronization process

<span id="shfzcazr"></span>
## Create a MySQL bidirectional synchronization task

<span id="dR666CTl"></span>
### Precautions


* In bidirectional synchronization of MySQL, do not perform DDL operations simultaneously on both the source and target database, or the synchronization task may fail. Bidirectional synchronization tasks only support synchronizing DDL operations from the forward task to the target database, and currently do not support synchronizing DDL from the reverse task. If you need to synchronize DDL operations from the reverse task, you can first [adjust the DDL synchronization direction of the bidirectional synchronization task](https://docs.byteplus.com/en/docs/DTS/Reversing_the_DDL_synchronization_direction_of_the_bidirectional_synchronization_task) and then perform the DDL operations to ensure data consistency.

* To ensure data consistency, it is recommended that rows with the same primary key value be updated in only one instance. If updated simultaneously, the system will handle it according to the primary key conflict handling method selected when configuring the data synchronization task.

* In a bidirectional synchronization topology, you need to configure both a forward synchronization task and a reverse synchronization task separately. For configuration methods, refer to [Configuring a forward task](https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization) and [Configuring a reverse task](https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization).

* When performing OnlineDDL, forward compatibility must be ensured. For example, do not modify field types or reduce fields, as this may cause synchronization interruptions or data inconsistency. The forward\-compatible table structure DDL list includes: create table, add column, modify column (increase field length), create index, and drop index.

* It is not recommended to use public networks for bidirectional synchronization, as they are prone to performance bottlenecks.


<span id="6ZFhmOt7"></span>
### Step 1: Create a synchronization task

You can select the corresponding reference documentation based on your source and target database types to create a data synchronization task.

When creating a bidirectional synchronization task, select **Bidirectional synchronization** as the synchronization topology. For more information, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).


|**Source database type** |**Source database version** |**Synchronization type** |**Target database type** |**Configuration documents** |
|---|---|---|---|---|
|BytePlus RDS for MySQL |* MySQL 5.7<br><br>* MySQL 8.0 |* Full initialization<br><br>* Incremental synchronization<br><br>* Schema initialization<br><br><br> |MySQL |* [Synchronizing to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_mysql_rdsmysql)<br><br>* [Synchronizing to BytePlus NDB for MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_veDB_for_MySQL)<br><br>* [Synchronizing to MySQL connected over public network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_public_network_rdsmysql)<br><br>* [Synchronizing to MySQL connected over express network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_express_network_rdsmysql) |
|BytePlus NDB for MySQL |MySQL 8.0 ||MySQL |* [Synchronizing to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_RDS_for_MySQL)<br><br>* [Synchronizing to BytePlus NDB for MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_veDB_for_MySQL)<br><br>* [Synchronizing to MySQL connected over public network](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_MySQL_connected_over_public_network)<br><br>* [Synchronizing to MySQL connected over express network](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_MySQL_connected_over_express_network) |
|MySQL connected over public network |* MySQL 5.5<br><br>* MySQL 5.6<br><br>* MySQL 5.7<br><br>* MySQL 8.0 ||MySQL<br><br> |* [Synchronizing to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_mysql_publicmysql)<br><br>* [Synchronizing to BytePlus NDB for MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_veDB_for_MySQL)<br><br>* [Synchronizing to MySQL connected over public network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_public_network_publicmysql)<br><br>* [Synchronizing to MySQL connected over express network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_express_network_publicmysql) |
|MySQL connected over express network<br><br> |* MySQL 5.6<br><br>* MySQL 5.7<br><br>* MySQL 8.0 ||MySQL |* [Synchronizing to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_mysql_expressmysql)<br><br>* [Synchronizing to BytePlus NDB for MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_veDB_for_MySQL)<br><br>* [Synchronizing to MySQL connected over public network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_public_network_expressmysql)<br><br>* [Synchronizing to MySQL connected over express network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_express_network_expressmysql) |


<span id="myWvbDHy"></span>
### Step 2: Configure forward synchronization

After the bidirectional synchronization task is created, you can configure the data forward synchronization task via DTS. For more information, please refer to [Configuring forward synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization).

<span id="GBcSO7eS"></span>
### Step 3: Configure reverse synchronization

You can configure the reverse synchronization task after the forward synchronization task enters the incremental synchronization phase. For the configuration method, refer to [Configuring reverse synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization).

<span id="WUNAXMkX"></span>
## Traffic cutover


1. Before performing any traffic cutover, a bidirectional link must be established. Do not start, stop, or create DTS links during traffic cutover, as this may increase the complexity of the switchover and make the process uncontrollable.

2. During traffic cutover, write operations on the source end must be disabled to prevent concurrent business writes on both ends of the link at the same time.


<span id="S3v56pjD"></span>
### Unidirectional traffic cutover


|**Normal cutover process** |**Abnormal cutover process** |
|---|---|
|1. Confirm that the DTS latency is within 1 second.<br><br>2. Disable writes on the source DB and confirm that DTS has no replication delay.<br><br>3. Enable writes on the target DB. |1. Based on the DTS delay, decide whether to perform traffic cutover (prioritizing availability or accepting minor data inconsistency).<br><br>2. Enable writes on the target DB. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b16671ab06b792913bf0eef734d36e85.png) </span>

<span id="lpyFPBDm"></span>
### Bidirectional traffic cutover


|**Normal cutover process** |**Abnormal cutover process** |
|---|---|
|1. Confirm that the DTS latency is within 1 second.<br><br>2. Disable writes on the source DB and confirm that DTS has no replication delay.<br><br>3. Enable writes on the target DB.<br><br>4. For bidirectional synchronization, perform traffic cutovers in batches by user (Dual writes are generally cut over by user to ensure that the same user does not write on both sides at the same time).<br><br>   1. Close the traffic write route of the user on the source end (User write will fail briefly).<br><br>   2. Wait a few seconds, and the wait time is greater than the DTS delay time.<br><br>   3. Change the user's traffic route on the Source end to the target DB. |1. **Fault occurs**<br><br>   * Network anomalies or datacenter failures in Region A result in a small backlog of data not being synchronized to Region B.<br><br>   * The business traffic of the source computer room drops, but not necessarily to 0.<br><br>2. **Determine whether to switch traffic**<br><br>   1. Detects DTS latency, and DTS returns the latency status at the time of network disconnection.<br><br>   2. Determine whether too much data is accumulated based on the latency status, and decide whether to perform an emergency traffic cutover.<br><br>3. **Traffic cutover process**<br><br>   1. Disable writes on the source DB If the network is unreachable and disabling writes on the source DB fails, consider skipping this step (in which case the service can not be written).<br><br>   2. Enable write restrictions for specific applications at the destination, such as order locking. For example, orders created in Region A should be prevented from triggering duplicate payment or shipment actions in Region B after traffic cutover.<br><br>   3. Switch writes to Region B.<br><br>   4. Check the application load and business success rate in Region B to determine if recovery is needed. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13e6b761e2bd553638f233b9505e2437.png) </span>

&nbsp;

<span id="RHufQzzK"></span>
## Appendix

<span id="bX2McxRc"></span>
### Business unit splitting

Unitization refers to dividing businesses into small business units according to specific dimensions. Each unit covers all the services required by the business and can independently process the entire business process. Each unit stores only a portion of the data, and the complete dataset is formed by integrating the data from all units. A "unit" can be migrated as a relatively independent entity or partially deployed to a different geographical location.


* The unitization of business components should adhere to the following principles to avoid data conflicts.

   * The use of database auto\-increment IDs is prohibited. Third\-party ID generators should be adopted instead.

   * It should be ensured that the data of each business unit is mutually independent, with minimal or no overlap.

* A bidirectional link should be established from the read\-write nodes at both ends, which may affect the read and write performance of the business.


<span id="zwaGIl2j"></span>
#### Business unitization background


|**Existing pain points** |**After business unitization** |
|---|---|
|Database connection bottleneck |Database connections are extremely valuable resources. After business unitization, data reads and writes within each unit form an internal closed loop, which helps reduce database connections. |
|Computer room latency |If unitization is well implemented, meaning that business access is strictly confined within its own unit. Data read/write in each unit is an intranet self\-closed loop, without cross\-computer room calls. |
|Traffic entry |Users are routed by the routing gateway, and each time they request the data center where they are located. For example, if a user is in center A, after unitization, user A's requests will be routed to center A and not to center B. The entire link, from ingress traffic to distributed services, eliminates single points of failure. |
|Data conflict |Users are grouped according to a rule, and each group of users can only write data to the specified data center. This is equivalent to binding users to the data center, which ensures that data from different user groups does not conflict before bidirectional synchronization. |


<span id="h5Qla9T3"></span>
#### Business unitization solution


|**Solution** |**Business scenario** |**Business unitization analysis** |
|---|---|---|
|Solution 1 |A customer is a logistics provider that provides logistics services for multiple e\-commerce platforms such as taobao and jd.com. The key table, order table, and outline fields of its business are as follows.<br><br><br>* Order ID (OrderID)<br><br>* Order source (Platform)<br><br>* Logistics address (Address) |The customer stores orders from Taobao in Database A and orders from JD.com in Database B. In this case, a bidirectional synchronization link can be established between Database A and Database B. Since order changes (INSERT/UPDATE/DELETE) from Taobao originate solely from Database A, and order changes from JD.com originate solely from Database B, the data is naturally partitioned by "order source," preventing data conflicts. |
|Solution 2 |A customer is a C‑end fitness app. Due to its massive user base, the customer uses Database A and Database B to store user data. The key fields of its User table are shown below.<br><br><br>* User ID (UserID)<br><br>* User information (UserInfo) |* The user ID is a 32\-bit string (containing only lowercase letters). The customer performs write partitioning operations at their user traffic entry. If the UserID starts with a to n, it is written to database A; if it starts with o to z, it is written to database B. At this time, a bidirectional synchronization link can be established to ensure that full user data can be read from either database A or database B.<br><br>* Given that user data starting with a to n will only be written to database A, and user data starting with o to z will only be written to database B, there will be no conflict in this bidirectional synchronization link. |
|Solution 3<br><br> |A customer, an international B2B SaaS provider, writes data for domestic tenants to the CN database and data for international tenants to the US database. The tenant table is roughly as follows.<br><br><br>* Tenant ID (TenantID)<br><br>* Tenant name (TenantName)<br><br>* Tenant data (Data) |* Customers can use DTS to establish a bidirectional synchronization link between the CN and US regions, ensuring that full data can be retrieved when reading from either database. In other words, read operations fetch the full data, while write operations are differentiated accordingly.<br><br>* Since data is written to CN or US entirely based on the tenant ID partition, no conflicts will occur. |
