---
title: "DescribeDBInstances"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbinstances"
---

Call the DescribeDBInstances API to query the basic information of the MongoDB instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you do not provide any parameters, it defaults to returning a list of all MongoDB instances under your current account.</div>


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstances&serviceCode=mongodb&version=2022-01-01&groupName=实例管理)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**ZoneId ** <span data-label="purple"> String  </span>`Optional` `Sample value: cn-beijing-a`

Availability zone ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones">DescribeAvailabilityZones</a> API to query all availability zone information for a MongoDB instance, including the availability zone ID.</div>




**InstanceId ** <span data-label="purple"> String </span>`Optional` `Sample value: mongo-replica-e405f8e2f8e2`

Instance ID.



**InstanceName ** <span data-label="purple"> String  </span>`Optional` `Sample value: test_mongo`

Instance name.



**InstanceType ** <span data-label="purple"> String  </span>`Optional` `Sample value: ReplicaSet`

The instance type for MongoDB. Valid values are:


* `ReplicaSet`: replica set.

* `ShardedCluster`: sharding cluster.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left empty, a list of all types of MongoDB instances under the current account is returned by default.</div>




**InstanceStatus ** <span data-label="purple"> String </span>`Optional` `Sample value: Running`

Instance status. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).



**DBEngine ** <span data-label="purple"> String  </span>`Optional` `Sample value: MongoDB`

Database engine. The value is fixed to `MongoDB`.



**DBEngineVersion ** <span data-label="purple"> String  </span>`Optional` `Sample value: MongoDB_5_0`

Database engine version, with the following valid values:


* `MongoDB_4_0`: MongoDB 4.0.

* `MongoDB_4_2`: MongoDB 4.2.

* `MongoDB_4_4`: MongoDB 4.4.

* `MongoDB_5_0`: MongoDB 5.0.

* `MongoDB_6_0`: MongoDB 6.0.

* `MongoDB_7_0`: MongoDB 7.0.

* `MongoDB_8_0`: MongoDB 8.0.

* `MongoDB_8_3`: MongoDB 8.3.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left empty, it defaults to returning all versions of MongoDB Instances under the current account. For more details about MongoDB versions, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/version_introduction">Version introduction</a>.</div>




**CreateStartTime ** <span data-label="purple"> String  </span>`Optional` `Sample value: 2022-03-15T03:50:00Z`

Instance creation start time. Format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).



**CreateEndTime ** <span data-label="purple"> String  </span>`Optional` `Sample value: 2022-03-15T04:00:00Z`

The end time of instance creation. Format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).



**UpdateStartTime ** <span data-label="purple"> String  </span>`Optional` `Sample value: 2022-03-19T03:45:00Z`

The start time of the instance update. Format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).



**UpdateEndTime ** <span data-label="purple"> String </span>`Optional` `Sample value: 2022-03-19T04:00:00Z`

The end time of the instance update. Format is *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).



**VpcId ** <span data-label="purple"> String  </span>`Optional` `Sample value: vpc-2743n1ihbxla87fap8tap8tap`

The Virtual Private Cloud (VPC) ID that the instance belongs to.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> API to query the list of all Virtual Private Clouds under the current account, including their Virtual Private Cloud IDs.</div>




**PageNumber ** <span data-label="purple"> Integer </span>`Optional` `Sample value: 1`

Page number of the instance list; default value is 1. The value ranges from 1 to the maximum value of the Integer data type.



**PageSize** <span data-label="purple">Integer</span> `Optional` `Sample value: 10`

The number of records per page. The value range is 1 to 1,000, and the default value is 10.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Specifies the name of the project to which the instance belongs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left empty, instances will not be filtered by project name.</div>




**FilterByTags ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value:`

An array of tag key\-value pairs for querying and filtering.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is left empty, tags will not be used for filtering.</div>


* <div data-tips="true" data-tips-type="default">When multiple tags are provided for filtering, the conditions between them are <strong>OR</strong> relationships.</div>




**Key**<span data-label="purple">  String </span><span data-api-tag="require|bBHwOs">必选</span>`  Sample value: instancetype`

The tag key for querying and filtering.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To query and filter instances using tags, the tag key (<code>Key</code>) is required.</div>




**Values ** <span data-label="purple"> String[] </span>`Optional` `Sample value: ["replica"]`

Tag values corresponding to the tag key used for query filtering.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left blank, no restrictions are placed on tag values, and all instances associated with the specified tag key will be filtered.</div>





**TagFilters ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value:`

This field has been deprecated and is no longer in use. We recommend using the `FilterByTags` field for tag filtering.


**Key**<span data-label="purple">  String</span><span data-api-tag="require|wdAGWr">必选</span>  ` Sample value: instancetype`

This field is deprecated. We recommend using the `FilterByTags` field for tag filtering.



**Value ** <span data-label="purple"> String </span>`Optional` `Sample value: replica`

This field has been deprecated and is no longer used. We recommend using the `FilterByTags` field for tag filtering.




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Total ** <span data-label="purple"> Integer </span>`Sample value: 1`

The number of all instances.



**DBInstances ** <span data-label="purple"> Object[]  </span>`Sample value:`

List of basic instance information.


**AutoRenew ** <span data-label="purple"> Boolean  </span>`Sample value: false`

Whether automatic renewal is enabled for the subscription instance. The value range is as follows:


* `false`: Not enabled.

* `true`: Enabled.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only subscription instances support returning this parameter.</div>




**ChargeStatus ** <span data-label="purple"> String  </span>`Sample value: Normal`

Instance billing status. The valid values are as follows:


* `Normal`: Normal.

* `WaitingPaid`: Waiting for payment.

* `ChangingPayType`: Updating billing type.

* `Renewing`: Renewing.

* `Overdue`: Expired.

* `Owing`: Overdue.

* `Unsubscribing`: In progress.



**ChargeType ** <span data-label="purple"> String  </span>`Sample value: Prepaid`

Instance billing type. Valid values are as follows:


* `Prepaid`: Subscription (also known as prepaid).

* `PostPaid`: Pay\-as\-you\-go (also known as postpaid).



**ClosedTime ** <span data-label="purple"> String  </span>`Sample value: 2022-03-19T04:00:00Z`

Scheduled shutdown time (UTC).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for Subscription instances.</div>




**ConfigServers ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of ConfigServers information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for sharding cluster instances.</div>



**ConfigServerNodeId ** <span data-label="purple"> String  </span>`Sample value: mongo-shard-3d714182****-config-0`

The node ID of the ConfigServer.



**NodeRole ** <span data-label="purple"> String </span>`Sample value: Primary`

Node role, with values as follows:


* `Primary`: Primary node

* `Secondary`: secondary node.

* `Hidden`: hidden node.



**NodeStatus ** <span data-label="purple"> String </span>`Sample value: Running`

Node status.



**TotalMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 4`

Total memory. Unit: GiB.



**TotalvCPU ** <span data-label="purple"> Double  </span>`Sample value: 2`

Total number of cores.



**UsedMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 0.33296966552734375`

Used memory. Unit: GiB.



**UsedvCPU ** <span data-label="purple"> Double </span>`Sample value: 0.004654006`

Used cores.



**ZoneId ** <span data-label="purple"> String  </span>`Sample value: cn-beijing-a`

Availability Zone ID of the current node.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your instance is deployed with multiple availability zones, the availability zones where different role nodes are located will be different. For more details about multi\-availability zone deployment, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/feature-introduction">Multi\-availability zone disaster recovery solution</a>.</div>




**RsMemberState ** <span data-label="purple"> String  </span>`Sample value: PRIMARY`

The state of the node in the replica set, with data sourced from MongoDB's `rs.status().members[].stateStr`.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">For more information about replica set node states, see <a href="https://www.mongodb.com/docs/manual/reference/replica-states/">Replica Set Member States</a>.</div>





**ConfigServersId ** <span data-label="purple"> String  </span>`Sample value: mongo-shard-fa8cd21d****-config`

ConfigServer ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances support returning this parameter</div>




**CreateTime ** <span data-label="purple"> String  </span>`Sample value: 2022-03-15T03:57:15Z`

Instance creation time (UTC).



**DBEngineVersion ** <span data-label="purple"> String  </span>`Sample value: MongoDB_5_0`

Database engine version. For more details about MongoDB versions, refer to [Version introduction](https://docs.byteplus.com/en/docs/mongodb/version_introduction).



**DBEngineVersionStr ** <span data-label="purple"> String  </span>`Sample value: MongoDB 5.0`

The string of the database engine version.



**ExpiredTime ** <span data-label="purple"> String  </span>`Sample value: 22022-03-19T03:45:28Z`

Instance expiration time (UTC).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for subscription instances.</div>




**InstanceId ** <span data-label="purple"> String  </span>`Sample value: mongo-replica-9b3f8fb9****`

Instance ID.



**InstanceName ** <span data-label="purple"> String  </span>`Sample value: test-mongo`

Instance name.



**InstanceStatus ** <span data-label="purple"> String  </span>`Sample value: Running`

Instance status. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).



**InstanceType ** <span data-label="purple"> String  </span>`Sample value: ReplicaSet`

The instance types for MongoDB are as follows:


* `ReplicaSet`: replica set.

* `ShardedCluster`: sharding cluster.



**MongosId ** <span data-label="purple"> String  </span>`Sample value: mongo-shard-011d2479****`

Mongos ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances can return this parameter.</div>




**ReclaimTime ** <span data-label="purple"> String  </span>`Sample value: 2022-03-26T03:45:28Z`

The scheduled reclaim time of the instance (UTC).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for subscription instances.</div>




**Shards ** <span data-label="purple"> Object[]  </span>`Sample value: -`

Shards information list

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances support returning this parameter</div>



**Nodes ** <span data-label="purple"> Object[]</span>

Information list of nodes in the Shard.


**NodeDelayTime ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Primary\-secondary delay time. Unit: milliseconds (ms).



**NodeId ** <span data-label="purple"> String  </span>`Sample value: mongo-shard-011d2479****-s1-0`

Node ID.



**NodeRole ** <span data-label="purple"> String </span>`Sample value: Primary`

Node role, with values as follows:


* `Primary`: Primary node

* `Secondary`: secondary node.

* `Hidden`: Hidden node.

* `ReadOnly`: Read\-only node

   <div data-tips="true" data-tips-type="default">Description   </div>
   

* <div data-tips="true" data-tips-type="default">Read\-only nodes are only supported by Shard nodes in replica set instances and sharding cluster instances.</div>


* <div data-tips="true" data-tips-type="default">Only when read\-only nodes are present in the instance will relevant information about the <code>ReadOnly</code> node be returned. For more information about read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div>




**NodeSpec ** <span data-label="purple"> String  </span>`Sample value: mongo.shard.2c4g`

Node specification.



**NodeStatus ** <span data-label="purple"> String </span>`Sample value: Running`

Node status.



**TotalMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 4`

Total memory. Unit: GiB.



**TotalStorageGB ** <span data-label="purple"> Double  </span>`Sample value: 20`

The node's total storage space. Unit: GiB.



**TotalvCPU ** <span data-label="purple"> Double  </span>`Sample value: 2`

Total number of cores.



**UsedMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 0.4655952453613281`

Used memory. Unit: GiB.



**UsedStorageGB ** <span data-label="purple"> Double  </span>`Sample value: 0.9955019280314445`

The storage space used by this node. Unit: GiB.



**UsedvCPU ** <span data-label="purple"> Double  </span>`Sample value: 0.003100326`

Used vCPUs.



**ZoneId ** <span data-label="purple"> String  </span>`Sample value: cn-beijing-a`

Availability Zone ID of the current node.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your instance is deployed with multiple availability zones, the availability zones where different role nodes are located will be different. For more details about multi\-availability zone deployment, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/feature-introduction">Multi\-availability zone disaster recovery solution</a>.</div>




**RsMemberState ** <span data-label="purple"> String  </span>`Sample value: PRIMARY`

The status of the node in the replica set, with data sourced from MongoDB's `rs.status().members[].stateStr`.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">For more information about replica set member states, see <a href="https://www.mongodb.com/docs/manual/reference/replica-states/">Replica Set Member States</a>.</div>





**ShardId ** <span data-label="purple"> String </span>`Sample value: mongo-shard-011d2479****-s0`

The ID of the Shard node.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for sharding cluster instances.</div>





**ProjectName ** <span data-label="purple"> String  </span>`Sample value: default`

The name of the project to which the instance belongs.



**SubnetId ** <span data-label="purple"> String  </span>`Sample value: subnet-2743n265pa8zk7fap8st3****`

The subnet ID of the instance.



**Tags ** <span data-label="purple"> Object[]  </span>`Sample value: -`

Information about tags associated with the instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for instances that have tags associated.</div>



**Key ** <span data-label="purple"> String  </span>`Sample value: instancetype`

The tag key bound to the current instance.



**Value ** <span data-label="purple"> String  </span>`Sample value: replica`

The tag value of the tags associated with the current instance.




**UpdateTime ** <span data-label="purple"> String  </span>`Sample value: 2022-03-19T03:45:28Z`

The update time of the instance (UTC).



**VpcId ** <span data-label="purple"> String  </span>`Sample value: vpc-3tfam26vmy3v****`

The ID of the instance's virtual private cloud.



**ZoneId ** <span data-label="purple"> String  </span>`Sample value: cn-beijing-a`

The Availability Zone ID of the instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your instance is deployed in multiple availability zones, the availability zone information for all nodes will also be displayed. For more details about multi\-zone deployment, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/feature-introduction">multi\-zone Zone\-disaster recovery solution</a>.</div>




**StorageType ** <span data-label="purple"> String  </span>`Sample value: LocalSSD`

The storage type of the instance. Currently, only local SSDs (i.e., `LocalSSD`) are supported for storage.



**PrivateEndpoint ** <span data-label="purple"> String  </span>`Sample value: mongodb://:@mongoshard3d714182\\*\\*\\*\\*0.mongodb.ivolces.com:3717,mongoshard3d714182\\*\\*\\*\\*1.mongodb.ivolces.com:3717,mongoshard3d714182\\*\\*\\*\\*2.mongodb.ivolces.com:3717/?authSource=admin&retryWrites=true`

String information of the instance's private network address.



**ReadOnlyNodeNumber ** <span data-label="purple"> Integer  </span>`Sample value: 3`

Number of read\-only nodes in the instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><code>0</code> indicates that no read\-only nodes have been added to the current instance.</div>


* <div data-tips="true" data-tips-type="default">For sharding cluster instances, this parameter's value represents the total number of read\-only nodes across all Shard shards within the instance. For more details on read\-only node feature introduction and limits, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes">MongoDB read\-only nodes</a>.</div>




**MongotInfos ** <span data-label="purple"> Object[]</span>

Mongot node information.


**ShardId ** <span data-label="purple"> String </span>`Sample value: mongo-shard-011d2479****-s0`

Shard node ID.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for sharding cluster instances.</div>




**NodeInfos ** <span data-label="purple"> Object[]  </span>`Example value: -`

Details of the Mongot node.


**NodeId ** <span data-label="purple"> String  </span>`Sample value: mongo-mongot-011d2479****-node-0`

Node ID.



**ZoneId ** <span data-label="purple"> String  </span>`Sample value: cn-beijing-a`

Availability Zone ID of the node.



**NodeSpec ** <span data-label="purple"> String</span>

Node specification



**UsedvCPU ** <span data-label="purple"> Double  </span>`Example value: 0.00256789`

Number of CPU cores used by the node.



**TotalvCPU ** <span data-label="purple"> Double  </span>`Sample value: 2`

Total node core count.



**UsedMemoryGB ** <span data-label="purple"> Double  </span>`Example value: 0.33296966552734375`

Used memory of the node, in GiB.



**TotalMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 4`

Total memory of the node, in GiB.



**UsedStorageGB ** <span data-label="purple"> Double  </span>`Example value: 1.56789`

Node storage used, in GiB.



**TotalStorageGB ** <span data-label="purple"> Double  </span>`Sample value: 20`

Node total storage space, in GiB.





**MongotEnable ** <span data-label="purple"> Boolean</span>

Indicates whether Mongot is enabled.



**BackupVersion ** <span data-label="purple"> String</span>

Backup version



**MaintenanceTime ** <span data-label="purple"> String</span>

Maintenance period



**MongoClusterVersion ** <span data-label="purple"> String</span>

mgc version




<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LIDE="></span>
### Sample request 1

Query details of pay\-as\-you\-go sharding cluster instances.

```JSON
POST https://mongodb.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceDetail&Version=2022-01-01 HTTP/1.1
Host: mongodb.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-3d7141824182"
}
```


<span id=".6L-U5Zue56S65L6LIDE="></span>
### Sample response 1

Sample response for a pay\-as\-you\-go sharding cluster instance. The following example only shows partial node information of the instance. The actual returned data is subject to the result of the API call.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260722165540B81A1414CCB9269A4B3D-24057c",
        "Action": "DescribeDBInstanceDetail",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "cn-guilin-boe"
    },
    "Result": {
        "DBInstance": {
            "AutoRenew": false,
            "BackupVersion": "25.12.2",
            "ChargeStatus": "Normal",
            "ChargeType": "PostPaid",
            "ClosedTime": "",
            "CreateTime": "2026-07-20T12:06:02Z",
            "DBEngine": "MongoDB",
            "DBEngineVersion": "MongoDB_8_3",
            "DBEngineVersionStr": "MongoDB 8.3",
            "InstanceId": "mongo-replica-49d441f6xxxx",
            "InstanceName": "test-83",
            "InstanceStatus": "Running",
            "InstanceType": "ReplicaSet",
            "MaintenanceTime": "18:00Z-22:00Z",
            "MongoClusterVersion": "6.6.1",
            "MongotEnable": true,
            "MongotInfos": [
                {
                    "NodeInfos": [
                        {
                            "NodeId": "mongo-replica-49d441f6387f-mongot-cn-guilin-c-0",
                            "NodeSpec": "mongo.mongot.2c4g",
                            "TotalMemoryGB": 4,
                            "TotalStorageGB": 200,
                            "TotalvCPU": 2,
                            "UsedMemoryGB": 0.9510612487792969,
                            "UsedStorageGB": 57.73587917815894,
                            "UsedvCPU": 0.17534521141611104,
                            "ZoneId": "cn-guilin-c"
                        },
                        {
                            "NodeId": "mongo-replica-49d441f6387f-mongot-cn-guilin-c-1",
                            "NodeSpec": "mongo.mongot.2c4g",
                            "TotalMemoryGB": 4,
                            "TotalStorageGB": 200,
                            "TotalvCPU": 2,
                            "UsedMemoryGB": 1.0714073181152344,
                            "UsedStorageGB": 57.712479719892144,
                            "UsedvCPU": 0.183387033451654,
                            "ZoneId": "cn-guilin-c"
                        }
                    ],
                    "ShardId": "mongo-replica-49d441f6387f"
                }
            ],
            "NetworkType": "Private",
            "Nodes": [
                {
                    "Cluster": "mix-azc-database",
                    "NodeDelayTime": 0,
                    "NodeId": "mongo-replica-49d441f6387f-0",
                    "NodeRole": "Primary",
                    "NodeSpec": "mongo.2c4g",
                    "NodeStatus": "Running",
                    "RsMemberState": "PRIMARY",
                    "TotalMemoryGB": 4,
                    "TotalStorageGB": 200,
                    "TotalvCPU": 2,
                    "UsedMemoryGB": 1.4145698547363281,
                    "UsedStorageGB": 1.535832087509334,
                    "UsedvCPU": 0.02365425482349663,
                    "ZoneId": "cn-guilin-c"
                },
                {
                    "Cluster": "mix-azc-database",
                    "NodeDelayTime": 0,
                    "NodeId": "mongo-replica-49d441f6387f-1",
                    "NodeRole": "Secondary",
                    "NodeSpec": "mongo.2c4g",
                    "NodeStatus": "Running",
                    "RsMemberState": "SECONDARY",
                    "TotalMemoryGB": 4,
                    "TotalStorageGB": 200,
                    "TotalvCPU": 2,
                    "UsedMemoryGB": 1.5751991271972656,
                    "UsedStorageGB": 1.5077232401818037,
                    "UsedvCPU": 0.031676946309643704,
                    "ZoneId": "cn-guilin-c"
                },
                {
                    "Cluster": "mix-azc-database",
                    "NodeDelayTime": 0,
                    "NodeId": "mongo-replica-49d441f6387f-2",
                    "NodeRole": "Hidden",
                    "NodeSpec": "mongo.2c4g",
                    "NodeStatus": "Running",
                    "RsMemberState": "SECONDARY",
                    "TotalMemoryGB": 4,
                    "TotalStorageGB": 200,
                    "TotalvCPU": 2,
                    "UsedMemoryGB": 1.5390701293945312,
                    "UsedStorageGB": 1.473611656576395,
                    "UsedvCPU": 0.021968421217316177,
                    "ZoneId": "cn-guilin-c"
                }
            ],
            "PrivateEndpoint": "mongodb://\u003cuser\u003e:\u003cpassword\u003e@mongoreplica49d441f6387f0.mongodb-boe.ivolces.com:3717,mongoreplica49d441f6387f1.mongodb-boe.ivolces.com:3717/?authSource=admin\u0026replicaSet=rs-mongo-replica-49d441f6387f\u0026retryWrites=true",
            "ProjectName": "default",
            "ReadOnlyNodeNumber": 0,
            "ReclaimTime": "",
            "SpecType": "GENERAL",
            "StorageType": "LocalSSD",
            "SubnetId": "subnet-1el48uidyuku81jcpwich01b3",
            "Tags": [
                {
                    "Key": "sys:tag:createdBy",
                    "Value": "Root:2100001228"
                }
            ],
            "Tenant": "2100001228",
            "UpdateTime": "2026-07-21T03:39:43Z",
            "VpcId": "vpc-1elkrq4tg3ta81jcpwjx5j6s4",
            "ZoneId": "cn-guilin-c"
        }
    }
}
```


<span id=".6K-35rGC56S65L6LIDI="></span>
### Sample request 2

Query details of a Subscription replica set instance.

```JSON
POST https://mongodb.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceDetail&Version=2022-01-01 HTTP/1.1
Host: mongodb.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-c70a99ee99ee"
}
```


<span id=".6L-U5Zue56S65L6LIDI="></span>
### Response example 2

Sample response for a subscription replica set instance. The following example only shows partial node information of the instance. The actual returned data is subject to the result of the API call.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260722171217F545F2157F3E6A87395E-fcb9ab",
        "Action": "DescribeDBInstanceDetail",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "cn-guilin-boe"
    },
    "Result": {
        "DBInstance": {
            "AutoRenew": false,
            "BackupVersion": "25.12.2",
            "ChargeStatus": "Normal",
            "ChargeType": "Prepaid",
            "ClosedTime": "2026-08-23T04:00:00Z",
            "CreateTime": "2026-07-22T09:06:15Z",
            "DBEngine": "MongoDB",
            "DBEngineVersion": "MongoDB_8_3",
            "DBEngineVersionStr": "MongoDB 8.3",
            "ExpiredTime": "2026-08-22T15:59:59Z",
            "InstanceId": "mongo-replica-fbe4cdd7xxxx",
            "InstanceName": "lwy",
            "InstanceStatus": "Running",
            "InstanceType": "ReplicaSet",
            "MaintenanceTime": "18:00Z-22:00Z",
            "MongoClusterVersion": "6.6.1",
            "MongotEnable": true,
            "MongotInfos": [
                {
                    "NodeInfos": [
                        {
                            "NodeId": "mongo-replica-fbe4cdd7de82-mongot-cn-guilin-c-0",
                            "NodeSpec": "mongo.mongot.2c4g",
                            "TotalMemoryGB": 4,
                            "TotalStorageGB": 100,
                            "TotalvCPU": 2,
                            "UsedMemoryGB": 0.22394943237304688,
                            "UsedStorageGB": 0.00039912760257720947,
                            "UsedvCPU": 0.025126908079432367,
                            "ZoneId": "cn-guilin-c"
                        },
                        {
                            "NodeId": "mongo-replica-fbe4cdd7de82-mongot-cn-guilin-c-1",
                            "NodeSpec": "mongo.mongot.2c4g",
                            "TotalMemoryGB": 4,
                            "TotalStorageGB": 100,
                            "TotalvCPU": 2,
                            "UsedMemoryGB": 0.24459457397460938,
                            "UsedStorageGB": 0.0004052901640534401,
                            "UsedvCPU": 0.022484653968326006,
                            "ZoneId": "cn-guilin-c"
                        }
                    ],
                    "ShardId": "mongo-replica-fbe4cdd7de82"
                }
            ],
            "NetworkType": "Private",
            "Nodes": [
                {
                    "Cluster": "mix-azc-database",
                    "NodeDelayTime": 0,
                    "NodeId": "mongo-replica-fbe4cdd7de82-0",
                    "NodeRole": "Primary",
                    "NodeSpec": "mongo.2c4g",
                    "NodeStatus": "Running",
                    "RsMemberState": "PRIMARY",
                    "TotalMemoryGB": 4,
                    "TotalStorageGB": 100,
                    "TotalvCPU": 2,
                    "UsedMemoryGB": 0.16679763793945312,
                    "UsedStorageGB": 0.19842858891934156,
                    "UsedvCPU": 0.020273914465585765,
                    "ZoneId": "cn-guilin-c"
                },
                {
                    "Cluster": "mix-azc-database",
                    "NodeDelayTime": 0,
                    "NodeId": "mongo-replica-fbe4cdd7de82-1",
                    "NodeRole": "Secondary",
                    "NodeSpec": "mongo.2c4g",
                    "NodeStatus": "Running",
                    "RsMemberState": "SECONDARY",
                    "TotalMemoryGB": 4,
                    "TotalStorageGB": 100,
                    "TotalvCPU": 2,
                    "UsedMemoryGB": 0.17724609375,
                    "UsedStorageGB": 0.19857225101441145,
                    "UsedvCPU": 0.021979507733426294,
                    "ZoneId": "cn-guilin-c"
                },
                {
                    "Cluster": "mix-azc-database",
                    "NodeDelayTime": 0,
                    "NodeId": "mongo-replica-fbe4cdd7de82-2",
                    "NodeRole": "Hidden",
                    "NodeSpec": "mongo.2c4g",
                    "NodeStatus": "Running",
                    "RsMemberState": "SECONDARY",
                    "TotalMemoryGB": 4,
                    "TotalStorageGB": 100,
                    "TotalvCPU": 2,
                    "UsedMemoryGB": 0.18416976928710938,
                    "UsedStorageGB": 0.19868833664804697,
                    "UsedvCPU": 0.019592978678410478,
                    "ZoneId": "cn-guilin-c"
                }
            ],
            "PrivateEndpoint": "mongodb://\u003cuser\u003e:\u003cpassword\u003e@mongoreplicafbe4cdd7de820.mongodb-boe.ivolces.com:3717,mongoreplicafbe4cdd7de821.mongodb-boe.ivolces.com:3717/?authSource=admin\u0026replicaSet=rs-mongo-replica-fbe4cdd7de82\u0026retryWrites=true",
            "ProjectName": "default",
            "ReadOnlyNodeNumber": 0,
            "ReclaimTime": "2026-08-29T15:59:59Z",
            "SpecType": "GENERAL",
            "StorageType": "LocalSSD",
            "SubnetId": "subnet-1el48uidyuku81jcpwich01b3",
            "Tags": [
                {
                    "Key": "sys:tag:createdBy",
                    "Value": "Root:2100001228"
                }
            ],
            "Tenant": "2100001228",
            "UpdateTime": "2026-07-22T09:09:55Z",
            "VpcId": "vpc-1elkrq4tg3ta81jcpwjx5j6s4",
            "ZoneId": "cn-guilin-c"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/mongodb/error-code).
