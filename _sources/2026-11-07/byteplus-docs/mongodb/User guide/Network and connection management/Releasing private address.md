---
title: "Releasing private address"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/release-private-address"
---

This topic describes how to release private address of MongoDB instance via the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Instance type must be **Sharding cluster**. For more details about sharding cluster instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E).

* You have successfully applied for a private address. For specific procedures, refer to [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address).

* For a sharding cluster MongoDB instance, before releasing the private address for a Shard or a ConfigServer node, you need to release the public address of the corresponding node first. For specific procedures, refer to [Releasing public address](https://docs.byteplus.com/en/docs/mongodb/release-public-address).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only supports releasing the private network addresses of Shard or ConfigServer nodes in MongoDB sharding cluster instances.

* The private network addresses of replica set instances or Mongos nodes in sharding cluster instances are provided by default and cannot be released.

* After you release the private address, addresses of shards or all ConfigServer nodes (three nodes by default) are also released. The released addresses cannot be used to connect to the corresponding shards or nodes. Proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **Sharding instances**.

4. On the target instance type list page, click the name of the target instance.

5. On the **Connectivity** tab, perform corresponding operations based on the node type of the private network address.

   * **Releasing private address of shard**

      In the **Connect to Shard** area, locate the private address of the target shard and click **Release private network address**.

   * **Releasing private address of ConfigServer**

      In the **Connect to ConfigServer** area, click **Release private network address** next to the private address.

6. In the pop\-up dialog box, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) |Call the DescribeDBEndpoint API to query address information in target instance. |
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/deletedbendpoint) |Call the DeleteDBEndpoint API to delete specified address in target MongoDB instance. |
