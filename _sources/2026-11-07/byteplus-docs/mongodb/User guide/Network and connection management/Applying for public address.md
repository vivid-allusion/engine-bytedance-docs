---
title: "Applying for public address"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address"
---

You can apply for a public address for the MongoDB instance on the console, so that devices outside the VPC can access the MongoDB instance. This topic describes how to apply for a public address for a MongoDB instance.

<span id="B6dzkJJi"></span>
## Prerequisite


* When applying for a public address, associate an elastic IP address (EIP) first. You must apply for an EIP. For details, refer to [Applying for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP). In addition, you can flexibly adjust the EIP bandwidth based on your business needs. The bandwidth modification will take effect immediately. For details, refer to [Modifying the maximum bandwidth](https://www.volcengine.com/docs/6402/67956?lang=en).

* For a sharding cluster MongoDB instance, you need to apply for a private address for the node before applying for a public address for a shard or a ConfigServer node. For specific procedures, refer to [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address).

* If you use an IAM user to apply for a public address, you need to configure the permission policies `EIPReadOnlyAccess` and `EIPFullAccess` for the IAM user. For policy configuration methods, refer to [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).


<span id="kOIOcSMT"></span>
## Precautions

Internet connections involve potential security risks. If devices outside the VPC do not need to access the MongoDB instance, promptly release the public address. For specific procedures, refer to [Releasing public address](https://docs.byteplus.com/en/docs/mongodb/release-public-address).

<span id="fGh5HlPJ"></span>
## Billing information


* To enable Internet access, you must associate an EIP, and you are billing for the EIP. For more details, refer to [EIP billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* If your account is in arrears for more than 2 hours, the Pay\-as\-you\-go EIP will enter the **Closed** status, stopping services and automatically disassociating from resources. If your MongoDB instance is associated with a Pay\-as\-you\-go EIP, you should pay close attention to your account balance and recharge in time when your balance is low, so that the public address of the instance will not be unavailable due to arrears. For more details, refer to [EIP arrears](https://docs.byteplus.com/en/docs/eip/Arrears).


<span id="NIvGDXY0"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. Under the **Connectivity** tab, complete the corresponding operations based on your instance or address type.

   
   <Tabs>
   <Tab zoneid="KL4elJ0L" title="Replica set instance">
   <TabTitle>Replica set instance</TabTitle>
   
   
   |Connection address type |Procedure |
   |---|---|
   |Primary\-secondary nodes |1. In the **Public network access** area, click **Apply for public network address** on the right side of **Public network address of primary\-secondary nodes**.<br><br>2. In the pop\-up panel, select the EIP to be associated with and click **OK**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Need to select 2 EIPs at the same time.</div><br> |
   |Read\-only node |1. Locate the target read\-only node in the single\-node address table and click **Apply for public network address**.<br><br>2. In the pop\-up panel, select the EIP to be associated with and click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only need to select 1 EIP.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only when there are read\-only nodes in the instance will the connection address information of the read\-only nodes be displayed. For more information about read\-only nodes, refer to <a href="https://www.volcengine.com/docs/6447/1149751">Managing read\-only nodes</a>.</div><br> |
   
   
   
   
   
   </Tab>
   <Tab zoneid="pYXwUzew" title="Sharding cluster instance">
   <TabTitle>Sharding cluster instance</TabTitle>
   
   
   |Connection address type |Procedure |
   |---|---|
   |Connect to Mongos |1. Locate the target node in the Mongos single\-node address table and click **Apply for public network address**.<br><br>2. In the pop\-up panel, select the EIP to be associated with and click **OK**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only need to select 1 EIP.</div><br> |
   |Connect to Shard |1. Locate the target shard in the shard address table and click **Apply for public network address**.<br><br>2. In the pop\-up panel, select the EIP to be associated with and click **OK**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Need to select 2 EIPs at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have not applied for a private address for the target shard, you cannot apply for a public address. To apply for a private address, refer to <a href="https://www.volcengine.com/docs/6447/104730">Applying for private address</a>.</div><br> |
   |Connect to ConfigServer |1. Click **Apply for public network address**.<br><br>2. In the pop\-up panel, select the EIP to be associated with and click **OK**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Need to select 2 EIPs at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have not applied for a private address for the ConfigServer, you cannot apply for a public address. To apply for a private address, refer to <a href="https://www.volcengine.com/docs/6447/104730">Applying for private address</a>.</div><br> |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="UCMcDyL4"></span>
## Subsequent operations


* After the application is approved, you need to add the IP address of the client device to the IP allowlist of the instance. For specific procedures, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist).

* You can use the new public address to connect to the MongoDB instance. For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell).

* MongoDB supports modifying connection addresses. You can modify the domain name of a public address after enabling public access. For specific procedures, refer to [Modifying connection address](https://docs.byteplus.com/en/docs/mongodb/modify-connection-address).


<span id="I3KJhFLN"></span>
## Relevant APIs


|API |Description |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/createdbendpoint) |Call the CreateDBEndpoint API to create a connection address for the target MongoDB instance. |
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) |Call the DescribeDBEndpoint API to query address information in target instance. |
