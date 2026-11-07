---
title: "CreateDBInstance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/createdbinstance"
---

Call the CreateDBInstance API to create a MongoDB instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBInstance&serviceCode=mongodb&version=2022-01-01&groupName=实例管理)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



ZoneId****<span data-label="purple"></span><span data-api-tag="require|XH1p-z">必选</span>`  String   Sample value: cn-beijing-a`

The ID of the instance's availability zone.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones">DescribeAvailabilityZones</a> API to view the availability zone information, including availability zone IDs, for all MongoDB instances that can be created under the current account.</div>


* <div data-tips="true" data-tips-type="default">If you need to deploy a new instance across multiple availability zones, you can pass three availability zone IDs simultaneously, separated by commas (,). For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/feature-introduction">Multi\-availability\-zone disaster recovery solution</a>.</div>




**VpcId**<span data-label="purple">  String </span><span data-api-tag="require|OTB72a">必选</span>`  Sample value: vpc-rs5811nceqyov0x58x458x4`

Virtual Private Cloud ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> API to query the list of all Virtual Private Clouds under the current account, including the Virtual Private Cloud ID.</div>




**Subnet ID ** <span data-label="purple"> String</span><span data-api-tag="require|7VrRza">必选</span> ` Sample value: subnet-274c1ohtlim0w7fap8sna8sna`

Subnet ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> API to query subnet list information under the specified Virtual Private Cloud, including Subnet ID.</div>




**DBEngine ** <span data-label="purple"> String  </span>`Optional` `Sample value: MongoDB`

Database engine. The value is fixed to `MongoDB`.



**DBEngineVersion ** <span data-label="purple"> String  </span>`Optional` `Sample value: MongoDB_5_0`

Database engine version. The valid values are as follows:


* `MongoDB_4_0` (Default): MongoDB 4.0.

* `MongoDB_4_2`: MongoDB 4.2.

* `MongoDB_4_4`: MongoDB 4.4.

* `MongoDB_5_0`: MongoDB 5.0.

* `MongoDB_6_0`: MongoDB 6.0.

* `MongoDB_7_0`: MongoDB 7.0.

* `MongoDB_8_0`: MongoDB 8.0.

* `MongoDB_8_3`: MongoDB 8.3.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details about MongoDB versions, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/version_introduction">Version introduction</a>.</div>




**InstanceType ** <span data-label="purple"> String  </span>`Optional` `Sample value: ReplicaSet`

The available instance types for MongoDB are as follows:


* `ReplicaSet` (Default): Replica set.

* `ShardedCluster`: Sharding cluster.



**NodeSpec** <span data-label="purple"> String</span><span data-api-tag="require|nqcOkd">必选</span>  `Sample value: mongo.2c4g`

Specification code of the instance. Among them:


* When the instance type is a replica set (i.e., `InstanceType` is `ReplicaSet`), this parameter indicates the compute node specification of the replica set instance.

* When the instance type is a sharding cluster (i.e., `InstanceType` is `ShardedCluster`), this parameter indicates the Shard node specification.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describenodespecs">DescribeNodeSpecs</a> API to view instance specification information, including the specification code.</div>




**NodeNumber ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 3`

Number of nodes, where:


* When the instance type is a replica set (i.e., `InstanceType` is `ReplicaSet`), this parameter indicates the number of compute nodes for the replica set instance.

* When the instance type is a sharding cluster (i.e., `InstanceType` takes the value of `ShardedCluster`), this parameter indicates the number of nodes in each Shard.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, each replica set instance and each Shard only supports 3 nodes, with the value fixed at <code>3</code>.</div>




**MongosNodeSpec ** <span data-label="purple"> String  </span>`Optional` `Sample value: mongo.mongos.2c4g`

Specification code of the Mongos node in the sharding cluster.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This parameter is required when the instance type is a sharding cluster (i.e., <code>InstanceType</code> is set to <code>ShardedCluster</code>).</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describenodespecs">DescribeNodeSpecs</a> API to view instance specification information for sharding clusters, including the spec code.</div>




**MongosNodeNumber ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 2`

Number of Mongos nodes in the sharding cluster. Value range: 2 to 32.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is required when the instance type is a sharding cluster (i.e., when <code>InstanceType</code> is set to <code>ShardedCluster</code>).</div>




**ShardNumber ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 3`

The number of Shard shards in the sharding cluster. Value range: 2 to 32.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is required when the instance type is a sharding cluster (i.e., when <code>InstanceType</code> is set to <code>ShardedCluster</code>).</div>




**StorageSpaceGB** <span data-label="purple"> Integer</span><span data-api-tag="require|QI--Xh">必选</span>   `Sample value: 100`

The total storage space of the replica set instance, or the storage space of a single Shard in the sharding cluster, in GiB, with a step size of 10.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If the instance type is a sharded cluster (i.e., <code>InstanceType</code> is <code>ShardedCluster</code>), the total capacity of the entire instance after successful creation is the storage space of a single Shard multiplied by the number of Shards.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describenodespecs">DescribeNodeSpecs</a> API to view the specification information of MongoDB instances, including the storage space specifications supported by different nodes.</div>




**ConfigServerNodeSpec ** <span data-label="purple"> String  </span>`Optional` `Sample value: mongo.config.2c4g`

The ConfigServer node specification code in a sharding cluster. The default value is `mongo.config.2c4g`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This parameter takes effect only when the instance type is a sharding cluster (i.e., the <code>InstanceType</code> value is <code>ShardedCluster</code>).</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describenodespecs">DescribeNodeSpecs</a> API to view instance specification information for sharding clusters, including spec codes.</div>




**ConfigServerStorageSpaceGB ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 200`

Storage space for ConfigServer in a sharding cluster. Unit: GiB. Step size is 10, default value: 20.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This parameter takes effect only when the instance type is a sharding cluster (i.e., <code>InstanceType</code> is <code>ShardedCluster</code>).</div>


* <div data-tips="true" data-tips-type="default">Different node specifications support different maximum storage spaces. Call the <a href="https://docs.byteplus.com/en/docs/mongodb/describenodespecs">DescribeNodeSpecs</a> API to view MongoDB instance specification information, including the storage space specifications supported by different nodes.</div>




**SuperAccountName ** <span data-label="purple"> String  </span>`Optional` `Sample value: root`

Database account name. Currently, only super administrator accounts can be set during instance creation, and the account name is fixed as `root`.



**SuperAccountPassword ** <span data-label="purple"> String  </span>`Optional` `Sample value: Password123`

The password for the root account. The password must meet the following conditions:


* Can only contain uppercase and lowercase letters, numbers, and the following special characters `_#!@$%^&*()+=-`.

* The length is 8 to 32 characters.

* Must contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.

* Weak passwords that are easily cracked are not allowed (such as `Admin@123`).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is left blank, no password will be set for the root account. The system will automatically generate a password for the root account to ensure instance access security.</div>


* <div data-tips="true" data-tips-type="default">You can also modify the root account password after instance creation using the <a href="https://docs.byteplus.com/en/docs/mongodb/resetdbaccount">ResetDBAccount</a> API.</div>


* <div data-tips="true" data-tips-type="default">If you use special characters in the password, you might need to escape them when connecting to the instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf">Special characters requiring escaping</a>.</div>


* <div data-tips="true" data-tips-type="default">For details on weak passwords prohibited in MongoDB, refer to <a href="https://docs.byteplus.com/en/docs/6447/71101%E5%BC%B1%E5%AF%86%E7%A0%81%E5%88%97%E8%A1%A8">Weak password list</a>.</div>




**InstanceName ** <span data-label="purple"> String  </span>`Optional` `Sample value: test_mongo`

Instance name. The name must meet the following requirements:


* It cannot start with a number or hyphen (\-).

* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).

* The length should be 2 to 64 characters.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is left blank, the instance ID will be used as the instance name by default.</div>


* <div data-tips="true" data-tips-type="default">You can customize the instance name as needed; uniqueness is not required for instance names.</div>


* <div data-tips="true" data-tips-type="default">If you have set instance name and purchased multiple instances simultaneously, the system will append a number to the end of the instance name according to corresponding rules for differentiation. For more details, refer to the rules for <strong>Instance names</strong> in the parameter configuration table <a href="https://docs.byteplus.com/en/docs/mongodb/create-instance#.5pON5L2c5q2l6aqk">Create instance</a>.</div>




**Count ** <span data-label="purple"> Integer </span>`Optional` `Sample value: 1`

The number of instances to create. The value must be a positive integer greater than or equal to 1. The default value is 1.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Each root account of BytePlus can purchase a maximum of 30 MongoDB instances by default in each region. Therefore, when calling this API to create instances in batches, a maximum of 30 instances can be created each time by default. If you need to adjust the quota to purchase more instances, please go to the <strong>Quota center</strong> to submit a <a href="https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=MongoDB_ToB">Quota application</a>.</div>


* <div data-tips="true" data-tips-type="default">If you have set instance name and purchased multiple instances simultaneously, the system will append a number to the end of the instance name according to corresponding rules for differentiation. For more details, refer to the rules for <strong>Instance names</strong> in the parameter configuration table <a href="https://docs.byteplus.com/en/docs/mongodb/create-instance#.5pON5L2c5q2l6aqk">Create instance</a>.</div>




**ChargeType ** <span data-label="purple"> String  </span>`Optional` `Sample value: Prepaid`

Instance billing types are as follows:


* `PostPaid` (default): Pay\-as\-you\-go (also known as Postpaid).

* `Prepaid`: Subscription (also known as Prepaid).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information on billing types, see <a href="https://docs.byteplus.com/en/docs/mongodb/billing-method">Billing method</a>.</div>




**AutoRenew ** <span data-label="purple"> Boolean  </span>`Optional` `Sample value: false`

Whether to enable automatic renewal, the value range is as follows:


* `false` (Default): do not enable automatic renewal.

* `true`: enable automatic renewal.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is required when the value of <code>ChargeType</code> is <code>Prepaid</code>.</div>




**PeriodUnit ** <span data-label="purple"> String  </span>`Optional` `Sample value: Year`

Specifies whether the subscription instance is yearly or monthly. The values are as follows:


* `Year`: Yearly subscription.

* `Month`: Monthly subscription.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When <code>ChargeType</code> is <code>Prepaid</code>, this parameter is required.</div>




**Period ** <span data-label="purple"> Integer </span>`Optional` `Sample value: 1`

The purchase duration for Subscription instances, where:


* When `PeriodUnit` is `Year`, `Period` ranges from 1 to 3.

* When `PeriodUnit` is `Month`, `Period` ranges from 1 to 9.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> is <code>Prepaid</code>.</div>




**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Select the project to which the instance belongs. If this parameter is left blank, new instances will be added to the default project by default.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources. For more details, refer to <a href="https://docs.byteplus.com/en/docs/6649/94333">Resource management</a>.</div>




**Tags ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value: `

An array object of tag keys and tag values to be bound.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left empty, the new instance will not be bound to any tags.</div>



**Key**<span data-label="purple"></span><span data-api-tag="require|ESc9ez">必选</span>`  String   Sample value: instancetype`

The tag key to be associated.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. If the tag value is not provided, the tag value for the corresponding tag key will be empty.</div>


* <div data-tips="true" data-tips-type="default">Supports passing in multiple sets of tag key\-value pairs at once. Multiple sets of tag key\-value pairs are separated by commas (,). You can specify up to 20 sets of tag key\-value pairs at a time.</div>


* <div data-tips="true" data-tips-type="default">Each instance can be associated with up to 50 tags. Tag keys must comply with the setting rules. For details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.</div>




**Value ** <span data-label="purple"> String  </span>`Optional` `Sample value: replica`

The tag value corresponding to the tag to be bound.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When associating tags with an instance, the tag key is required, while the tag value is optional. Leaving the tag value blank means the tag value for the corresponding tag key is empty.</div>


* <div data-tips="true" data-tips-type="default">Supports passing in multiple sets of tag key\-value pairs at once. Multiple sets of tag key\-value pairs are separated by commas (,). You can specify up to 20 sets of tag key\-value pairs at a time.</div>


* <div data-tips="true" data-tips-type="default">Each instance can be associated with up to 50 tags. Tag keys must comply with the setting rules. For details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.</div>





**AllowListIds ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: [ "acl-cq014ioqkm9zt5j****", "acl-cq015pp15v8buvl****" ]`

Allowlist ID list. New instances will be associated with the specified allowlist.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describeallowlists">DescribeAllowLists</a> API to query all IP allowlist information within the specified region under the current account, including allowlist ID information.</div>


* <div data-tips="true" data-tips-type="default">Each instance can be associated with a maximum of 100 allowlists. A maximum of 100 allowlists can be associated at a time.</div>




**NodeAvailabilityZone ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value:`

Add read\-only node information, including the availability zone and quantity of the read\-only nodes.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Leaving this parameter empty indicates that no read\-only nodes will be added to the instance. For more information about read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div>



**ZoneId**  <span data-label="purple">String</span><span data-api-tag="require|eAezFa">必选</span> `  Sample value: cn-beijing-a`

Availability zone of the read\-only node.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The availability zone of the read\-only node must be a subset of the instance's availability zone.</div>




**NodeNumber**<span data-label="purple">  Integer</span><span data-api-tag="require|9H2TmP">必选</span>  `Sample value: 1`

The number of read\-only nodes to be added in the current availability zone. Currently, only replica set instances and Shard shards in sharding cluster instances support adding read\-only nodes. Among them:


* When the instance type is a replica set (i.e., `InstanceType` is `ReplicaSet`), this value indicates the total number of read\-only nodes in a single replica set instance. Each replica set instance supports adding a maximum of 5 read\-only nodes.

* When the instance type is a sharding cluster (i.e., `InstanceType` is `ShardedCluster`), this value indicates the number of read\-only nodes in each Shard. Each Shard supports a maximum of 5 read\-only nodes.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div>





**Port ** <span data-label="purple"> String </span>`Optional` `Sample value: 3717`

Set the port number for the private network address of the new instance. The value range is 1000\-65535.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is left blank, the instance's private network address defaults to port 3717.</div>


* <div data-tips="true" data-tips-type="default">After the instance is created successfully, you can also modify the port number of the connection address using the <a href="https://docs.byteplus.com/en/docs/mongodb/modifydbendpointport">ModifyDBEndpointPort</a> API. For more details on modifying the port number, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modifying_ports">Modifying port</a>.</div>




**MongotSpec ** <span data-label="purple"> Object  </span>`Optional` `Sample: -`

The specification list for Mongot nodes.


**Zx ** <span data-label="purple"> Object  </span>`Optional`

Detailed configuration information for the Mongot node, including the specification code, number of nodes in each availability zone, and storage space.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">DBEngineVersion is set to <code>MongoDB_8_3</code></div>


<div data-tips="true" data-tips-type="default">this parameter is required.</div>



**Spec ** <span data-label="purple"> String  </span>`Optional` `Sample: mongo.mongot.2c4g`

Specification code for Mongot nodes. For values, see [Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification).

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">Only when DBEngineVersion is set to <code>MongoDB_8_3</code></div>


<div data-tips="true" data-tips-type="default">this parameter is required.</div>




**AzNums ** <span data-label="purple"> Object[]  </span>`Optional`

Specify the number of Mongot nodes deployed in each availability zone.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">Only when <code>DBEngineVersion</code> is <code>MongoDB_8_3</code></div>


<div data-tips="true" data-tips-type="default">this parameter is required.</div>



**Az ** <span data-label="purple"> String </span>`Optional` `Sample: cn-beijing-a`

Specify the Availability Zone ID for deploying Mongot nodes.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <code>DescribeAvailabilityZones</code> API to view availability zone information for all creatable MongoDB instances under the current account, including availability zone IDs.</div>




**Nums ** <span data-label="purple"> Integer  </span>`Optional` `Sample: 1`

Specify the number of Mongot nodes deployed in the corresponding availability zone.




**StorageGB ** <span data-label="purple"> Integer </span>`Optional` `Sample: 200`

Storage space for Mongot nodes. Unit: GiB. Step: 10.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">Only when <code>DBEngineVersion</code> is <code>MongoDB_8_3</code></div>


<div data-tips="true" data-tips-type="default">, this parameter is required.</div>






<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**InstanceId ** <span data-label="purple"> String  </span>`Sample value: mongo-replica-e405f8e2f8e2`

Instance ID of the new instance.



**OrderNO ** <span data-label="purple"> String  </span>`Sample value: Order7076626359344174417`

Order ID.



**EventID ** <span data-label="purple"> String  </span>`Sample:`





<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LIDE="></span>
### Sample request 1

Create one replica set instance (including 3 nodes by default), with the following configuration:


* Database version: MongoDB 5.0

* Node specification: 2 cores 4 GiB.

* Storage space: 30 GiB.

* Associate two tags: `instancetype` and `chargetype`.

* Use a multi\-AZ deployment method, where Availability Zone A is the primary availability zone, and B and C are secondary availability zones.

* Associate with two allowlists: `acl-cq014ioqkm9zt5j****` and `acl-cq015pp15v8buvl****`.

* Read\-only nodes: Add one read\-only node to Availability Zone A and one to B.


```JSON
POST https://mongodb.cn-beijing.byteplusapi.com.cn/?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Host: mongodb.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ZoneId": "cn-beijing-a,cn-beijing-b,cn-beijing-c",
    "DBEngineVersion": "MongoDB_5_0",
    "NodeSpec": "mongo.2c4g",
    "StorageSpaceGB": 30,
    "VpcId": "vpc-13f24t16guqdc3n6nu4k5u4k5",
    "SubnetId": "subnet-rr96lovl7f28v0x58tv58tv",
    "InstanceName": "api_test_replica",
    "Tags": [
        {
            "Key": "instancetype",
            "Value": "replica"
        },
        {
            "Key": "chargetype",
            "Value": "postpaid"
        }
    ],
    "AllowListIds": [
        "acl-cq014ioqkm9zt5j****",
        "acl-cq015pp15v8buvl****"
    ],
    "NodeAvailabilityZone": [
        {
            "ZoneId": "cn-beijing-a",
            "NodeNumber": 1
        },
        {
            "ZoneId": "cn-beijing-b",
            "NodeNumber": 1
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6LIDE="></span>
### Sample response 1

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202202241620210102121020921E081E08",
        "Action": "CreateDBInstance",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mongo-replica-e405f8e2f8e2",
        "OrderNO": "Order7076626359344174417"
    }
}
```


<span id=".6K-35rGC56S65L6LIDI="></span>
### Sample request 2

Create one sharding cluster instance with the following configuration:


* Database version: MongoDB 5.0

* Using a single availability zone deployment, all instance nodes are deployed in Availability Zone A.

* Mongos

   * Node specification: 2 cores 4GiB.

   * Number of nodes: 2.

* Shard

   * Number of shards: 2.

   * Nodes per shard: Each shard includes 3 nodes by default.

   * Node specification: 2 cores 4GiB.

   * Storage space: 30GiB.

   * Read\-only node: Add 1 read\-only node in Availability Zone A.

* ConfigServer

   * Node specification: 2 cores 4GiB.

   * Node count: 3 nodes are included by default.

   * Storage space: 30GiB.


```JSON
POST https://mongodb.cn-beijing.byteplusapi.com.cn/?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Host: mongodb.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ZoneId":"cn-beijing-a",
    "DBEngineVersion": "MongoDB_5_0",
    "NodeSpec":"mongo.shard.2c4g",
    "StorageSpaceGB":30,
    "VpcId":"vpc-13f24t16guqdc3n6nu4k5u4k5",
    "SubnetId":"subnet-rr96lovl7f28v0x58tv58tv",
    "InstanceName":"api_test_shard",
    "MongosNodeSpec":"mongo.mongos.2c4g",
    "InstanceType":"ShardedCluster",
    "ShardNumber":2,
    "MongosNodeNumber":2,
	"ConfigNodeSpec":"mongo.config.2c4g",
	"ConfigStorageSpaceGB":30,
    "NodeAvailabilityZone":[
        {
            "ZoneId":"cn-beijing-a",
            "NodeNumber":1
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6LIDI="></span>
### Response example 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202202241620210102121020921E081E08",
        "Action": "CreateDBInstance",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "cn-beijing"
    },
 "Result": {
     "InstanceId": "mongo-shard-fc1c77c377c3",
     "OrderNO": "Order7076626387340174017"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/mongodb/error-code).
