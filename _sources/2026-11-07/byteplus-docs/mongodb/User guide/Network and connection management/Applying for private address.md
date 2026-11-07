---
title: "Applying for private address"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/apply-private-address"
---

Document Database for MongoDB provides a default private network address and supports applying for additional private network addresses. This topic describes how to apply for a private address for a MongoDB instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Instance type must be **Sharding cluster**. For more details about sharding cluster instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can only apply for separate private network addresses for Shard and ConfigServer nodes in MongoDB sharding cluster instances.

* Replica set instances and Mongos nodes in sharding cluster instances have private network addresses by default and do not require additional applications.

* Document Database for MongoDB sharding clusters support 2 to 32 shards, and you can apply for one private network address for each shard.

* After applying for private network address, the system automatically creates connection addresses for target shards and all ConfigServer nodes (three nodes by default).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **Sharding instances**.

4. On the target instance type list page, click the name of the target instance.

5. On the instance details page, click on the **Connectivity** tab.

6. On the **Connectivity** tab, perform corresponding operations based on the node type of the private network address.

   * **Applying for private address of shard**

      In the **Connect to Shard** area, click **Apply for private address** next to the target shard.

   * **Applying for private address of ConfigServer**

      In the **Connect to ConfigServer** area, click **Apply for private address**.

7. In the pop\-up dialog box, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) |Call the DescribeDBEndpoint API to query address information in target instance. |
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/createdbendpoint) |Call the CreateDBEndpoint API to create a connection address for the target MongoDB instance. |
