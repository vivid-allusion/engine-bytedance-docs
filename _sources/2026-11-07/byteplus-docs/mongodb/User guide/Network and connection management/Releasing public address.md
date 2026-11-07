---
title: "Releasing public address"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/release-public-address"
---

When devices outside the Virtual Private Cloud (VPC) do not need to access a MongoDB instance, release the public address in time. This topic introduces how to release a public address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

You have applied for the public address for instance. For more information about how to apply for a public address, refer to [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

To ensure the security of database data, after releasing the public network address, it is recommended that you delete the relevant public network IP address in the IP whitelist in a timely manner. For more information about how to set IP allowlists, refer to [Editing allowlist](https://docs.byteplus.com/en/docs/mongodb/edit-allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. On the **Connectivity** tab, perform corresponding operations based on the instance or address type.

   
   <Tabs>
   <Tab zoneid="RfzFU561eR" title="Replica set instance">
   <TabTitle>Replica set instance</TabTitle>
   
   
   |**Connection address type** |Procedure |
   |---|---|
   |Public address for primary and secondary nodes<br><br> |1. In the **Public network access** pane, click **Release public network address** next to the **Public address for primary and secondary nodes**.<br><br>2. In the pop\-up panel, click **OK**. |
   |Public address for read\-only nodes |1. In the single\-node address table, locate the target read\-only node and click **Release public network address**.<br><br>2. In the pop\-up panel, click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only when there are read\-only nodes in the instance will the connection address information of the read\-only nodes be displayed. For more information about read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">Managing read\-only nodes</a>.</div><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="XqEFh73pRQ" title="Sharding cluster instance">
   <TabTitle>Sharding cluster instance</TabTitle>
   
   
   |**Connection address type** |Procedure |
   |---|---|
   |Connect to Mongos |1. Locate the target node in the single\-node address table of Mongos and click **Release public network address** next to the public address.<br><br>2. In the pop\-up panel, click **OK**. |
   |Connect to Shard |1. Locate the target shard in the sharding address table, and click **Release public network address** next to the public address.<br><br>2. In the pop\-up panel, click **OK**. |
   |Connect to ConfigServer |1. Click **Release public network address** next to the public address.<br><br>2. In the pop\-up panel, click **OK**. |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) |Call the DescribeDBEndpoint API to query address information for target instance. |
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/deletedbendpoint) |Call the DeleteDBEndpoint API to delete specified address in target MongoDB instance. |
