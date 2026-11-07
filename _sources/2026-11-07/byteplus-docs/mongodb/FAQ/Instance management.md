---
title: "Instance management"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/instance-management-faq"
---

This topic summarizes the instance management FAQs for Document Database for MongoDB.

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5ZKMLW1vbmdvZGIt5pyJ5LuA5LmI5YWz57O777yf"></span>
### What are the differences between Document Database for MongoDB and open\-source MongoDB?

Document Database for MongoDB is an online cloud database service that is fully compatible with the MongoDB protocol and offers high availability and high performance. It supports most open\-source MongoDB command operations and can establish connections with any MongoDB\-compatible client for data storage or to perform corresponding database operations. For more information about Document Database for MongoDB, refer to [About Document Database for MongoDB](https://docs.byteplus.com/en/docs/mongodb/about-mongodb).

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5o-Q5L6b5L2V56eN5a6e5L6L6KeE5qC877yf"></span>
### What instance specifications does Document Database for MongoDB provide?

Document Database for MongoDB provides two types of architectures: replica set and sharding cluster. The instances for each architecture come in a variety of specifications and configurations, which can be flexibly selected to meet different performance requirements, capacity needs, and application scenarios. For more details, refer to [Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification).

<span id=".5Zyo5ZCM5LiA6LSm5Y-355qE5ZCM5LiA5Zyw5Z-f5LiL77yM5piv5ZCm5pSv5oyB6K6-572u5ZCM5ZCN55qE5a6e5L6L77yf"></span>
### Is it supported to configure instances with same name under same account and region?

Yes. Document Database for MongoDB uses the instance ID as the unique identifier for instances. Each instance randomly generates a unique instance ID upon creation. The instance name is optional. If left blank, the instance ID is used as the default name for the instance. You can also customize the instance name as needed. For more details, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

<span id=".5pyA5aSa5pSv5oyB5Yib5bu65aSa5bCR5Liq5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5a6e5L6L77yf"></span>
### How many Document Database for MongoDB instances can be created?

Document Database for MongoDB supports batch instance creation, allowing up to 10 instances to be created simultaneously each time. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each root account of BytePlus can purchase a maximum of 30 MongoDB instances by default in each region. If you need to adjust the quota to purchase more instances, please go to the <strong>Quota center</strong> to submit a <a href="https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=MongoDB_ToB">Quota application</a>.</div>


<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5pSv5oyB5ZOq5Lqb5pWw5o2u5bqT54mI5pys77yf"></span>
### Which database versions does Document Database for MongoDB support?

Document Database for MongoDB currently supports MongoDB  4.2, 4.4, 5.0, 6.0, 7.0. We recommend using clients that match the corresponding database version for access. You can download clients for various languages from [MongoDB Drivers](https://docs.mongodb.org/ecosystem/drivers/).

<span id=".5aaC5L2V5p-l55yLLW1vbmdvZGIt5a6e5L6L5L2_55So55qE5pWw5o2u5bqT54mI5pys77yf"></span>
### How to view the database version used by MongoDB instance?

You can view the database version used by MongoDB instance via following steps.


1. Connect to MongoDB instance via Mongo shell. For specific procedures, refer to [Connecting to instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

2. Execute the following command to view the database version.

   ```JavaScript
   db.version()
   ```
   


<span id=".5aaC5L2V5Y2H57qnLW1vbmdvZGIt5a6e5L6L55qE5pWw5o2u5bqT54mI5pys77yM5L6L5aaC5LuOLW1vbmdvZGItNS0wLeeJiOacrOWNh-e6p-WIsC1tb25nb2RiLTYtMC3niYjmnKzvvJ8="></span>
### How to upgrade the database version for MongoDB instance, for example, from MongoDB 5.0 to 6.0?

Direct upgrade of the MongoDB database version (such as from MongoDB 5.0 to MongoDB 6.0) is not supported for now. However, you can achieve this by creating a new instance with a higher version and replacing the original lower version instance with it. The specific procedures are as follows:


1. Create a new instance with higher version (e.g., MongoDB 6.0). For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

2. Migrate the original lower version instance (such as MongoDB 5.0) to the new higher version instance (such as MongoDB 6.0) using Database Transmission Service (DTS). For specific procedures, refer to [Migrating from BytePlus MongoDB to BytePlus MongoDB](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_documentdb_for_mongodb_mongodb).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about MongoDB versions, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/version_introduction">Version introduction</a>.</div>


<span id=".5aaC5L2V5bCG5a6e5L6L5LuO5Ymv5pys6ZuG5Y2H57qn5Li65YiG54mH6ZuG576k77yf"></span>
### How to upgrade instance from replica set to sharding cluster?

Currently, directly upgrading instance from replica set to sharding cluster architecture is not supported. However, you can achieve this by creating a new instance and replacing the old one with the new one. The specific procedures are as follows:


1. Create a new sharding cluster instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

2. Migrate data of replica set instance to new sharding cluster instance with Database Transmission Service (DTS). For specific procedures, refer to [Migrating from BytePlus MongoDB to BytePlus MongoDB](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_documentdb_for_mongodb_mongodb).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details on instance architecture, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E">Product architecture</a>.</div>


<span id=".5Li65LuA5LmI5ZyoLW1vbmdvZGIt5o6n5Yi25Y-w5LiK55yL5LiN6KeB5oiR5Yia5Yib5bu65oiQ5Yqf55qE5a6e5L6L77yf"></span>
### Why can't I see the instance I just created on the MongoDB console?

Maybe because the project of the new instance created by you is different from the project you choose to enter on the console.

When viewing an instance on the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb/list), specify the project and region of the target instance first. You can select the project and region of the instance from the drop\-down list of projects and regions in the upper\-right corner of the console.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_933c65ae386d71ed6e8fa594c1c1aa0a.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information on how to specify the project of instance when creating it, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/create-instance">Creating instance</a>.</div>


* <div data-tips="true" data-tips-type="tip">You can also change the project of the instance after it is created. For specific procedures for modifying projects, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project">Editing project</a>.</div>



<span id=".5Li65LuA5LmI5aSH5Lu95paH5Lu25YiX6KGo5Lit5bGV56S655qE5pWw5o2u5aSH5Lu95paH5Lu277yM5q-U5a6e6ZmF5LiL6L295LiL5p2l55qE5aSH5Lu95paH5Lu25pu05aSn77yf"></span>
### Why is the data backup file displayed in backup file list larger than actually downloaded backup file?

The **data backups** of MongoDB are stored in TOS in the form of shard. The backup file size displayed in the backup file list on the MongoDB console is the size of the **uncompressed** backup data. After you click **Obtain backup file**, the system will first compress the backup file stored in TOS and then provide it for download, so the size of the downloaded file is the **compressed** file size.

Therefore, for data backup files, you will notice that the backup file size displayed on the console (uncompressed) is larger than the data backup file size you downloaded (compressed). Examples are as follows:


* Uncompressed data backup file size

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46fb58cd3c80c389bc98189d63a3d50b.png) </span>

* Compressed data backup file size

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5c58ef1c3970e1caf80411992ea555f.png) </span>


For specific procedures on how to get and download backup files, refer to [Managing backup files](https://docs.byteplus.com/en/docs/mongodb/manage-backup-file).

<span id=".5L-u5pS55LqG56eB5pyJ572R57uc5omA5bGe6aG555uu5ZCO77yM5Li65L2V5Yib5bu6LW1vbmdvZGIt5a6e5L6L5pe25om-5LiN5Yiw6K-l56eB5pyJ572R57uc5LiL55qE5a2Q572R5LqG77yf"></span>
### Why can't the subnets under this private network be found when creating MongoDB instance after modifying the project to which a private network belongs?

You can specify a project when you create a VPC, but you cannot specify a project when you create a subnet, which is by default under the same project as the VPC to which it belongs. The project changes of the VPC and the subnet are independent, that is, modifying the project to which the VPC belongs will not modify the project of the subnet under the current VPC at the same time. For more details, refer to [Managing projects](https://docs.byteplus.com/en/docs/vpc/Managing-projects).

Therefore, if the project to which a VPC belongs is modified, you also need to change the project of the subnets under the VPC accordingly to ensure the consistency of the projects to which they belong. Otherwise, when a subuser with non\-global privileges creates a cloud resource (such as Document Database for MongoDB), it will not be able to select a subnet or anomalies will be reported. For specific procedures for modifying projects, refer to [Editing project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).

<span id=".5pS25Yiw5a6e5L6LLW9wbG9nLeS_neeVmeeql-i_h-Wwj-eahOS6i-S7tuebkeaOp-WRiuitpuWQjuivpeWmguS9leWkhOeQhu-8nw=="></span>
### What should be done after receiving event monitoring alarm for the oplog window being insufficient?

The oplog (`operations log`) of Document Database for MongoDB stores all document modification operations in the database and is used for primary\-secondary replication between nodes. The default size of the oplog for Document Database for MongoDB (that is, the parameter value of `replication.oplogSizeMB`) is **10% of the maximum available storage space of the instance** (for example, if the maximum available storage space of the instance is 20 GiB, then the corresponding oplog size is 2 GiB), and the oplog size will be automatically adjusted as the disk is expanded.

The oplog retention window (also known as oplog available time) is the time difference between the oldest oplog and the newest oplog in the oplog record table. Primary\-secondary replication depends on this oplog window. Only when the expected oplog record is found in the oplog window of the synchronization source can the slave node synchronize normally. If the oplog available time is too short, then the number of oplog records that can be retained is limited. In scenarios such as increased master\-slave replication latency and slave library reconstruction, the risk of master\-slave replication failure due to the lack of required oplog will increase, which will in turn affect instance availability and data reliability.

Therefore, when the oplog available time of an instance is insufficient, you will receive an alarm message for the insufficient oplog retention window in [Event monitoring](https://docs.byteplus.com/en/docs/mongodb/event-monitoring). After receiving this event monitoring alarm, you need to appropriately adjust the parameter value of `replication.oplogSizeMB` of the instance. You can **estimate** the recommended value of the `replication.oplogSizeMB` parameter according to the following calculation formula.


<Tabs>
<Tab zoneid="xk5sHrbZlx" title="Calculation formula">
<TabTitle>Calculation formula</TabTitle>

<div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Description</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">To ensure instance performance, it is recommended that the oplog size not exceed 30% of the maximum available storage space of the instance. If the required oplog size exceeds this value, it is recommended to expand the storage space of the instance For the specific procedures on instance configuration change, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec">Modifying replica set instance specification</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/change-sharding-cluster-config">Modifying sharding cluster instance configuration</a>.</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">To set the parameter <code>replication.oplogSizeMB</code>, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter">Modifying instance parameter</a>. For more details on the settings of oplog\-related parameters, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/guide-to-set-oplog-related-parameters">Guide to setting oplog\-related parameters</a>.</div>



Recommended value of `replication.oplogSizeMB` = Current value of `replication.oplogSizeMB` × recommended adjustment factor.

You can estimate the recommended adjustment factor based on the following information:

= Recommended oplog availability time ÷ Actual oplog availability time

= (Current data volume of instance ÷ Common synchronization rate of primary\-secondary replication) ÷ Actual oplog availability time.

The description of each calculation item in the above formula is shown in the table below.


|Calculation item |Description |
|---|---|
|Current data volume of instance |You can estimate the current data volume of the instance by the **Total used data disk space** of the primary node on the replica set instance or the sum of the **Total used data disk space** of the primary nodes of each Shard in the sharded cluster instance.<br><br>You can view the monitoring indicator of the **Total used data disk space** of the instance on the MongoDB console. For specific procedures, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data). |
|Common synchronization rate of primary\-secondary replication |The primary\-secondary replication sync rate indicates the amount of data that primary and secondary nodes can synchronize per hour. Typically, the data synchronization rate during primary\-secondary replication is approximately 50 GiB/hour. |
|Oplog available time |You can view the monitoring indicator of the **Oplog available time** of the instance on the MongoDB console. For specific procedures, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data). |





</Tab>
<Tab zoneid="hrUw1f0p64" title="Calculation example">
<TabTitle>Calculation example</TabTitle>

Suppose there is a MongoDB replica set instance, and the relevant information of the instance is as follows:


* Current data volume of instance: 500 GiB.

* Actual oplog availability time: 4 hours.

* Current value of `replication.oplogSizeMB`: Dynamically determined. Given that the instance's maximum available storage space is 1000 GiB, the current value of the `replication.oplogSizeMB` parameter is 1000 GiB × 10% = 100 GiB.


Then, when the instance receives the event monitoring alarm of too small oplog retention window, the recommended adjustment factor can be roughly estimated as: 500 GiB ÷ 50 GiB/hour ÷ 4 hours = 2.5.

Therefore, the recommended value of `replication.oplogSizeMB` is 2.5 × 100 GiB = 250 GiB. That is, it is recommended that you adjust the parameter value of `replication.oplogSizeMB` to 250 GiB.


</Tab>
</Tabs>
