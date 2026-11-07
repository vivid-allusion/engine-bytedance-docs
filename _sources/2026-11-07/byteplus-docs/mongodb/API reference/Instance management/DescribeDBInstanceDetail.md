---
title: "DescribeDBInstanceDetail"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail"
---

Call the DescribeDBInstanceDetail API to query the detailed information of the target MongoDB instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceDetail&serviceCode=mongodb&version=2022-01-01&groupName=实例管理)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**InstanceId**<span data-label="purple">String</span><span data-api-tag="require|VkQI4Q">必选</span> `Sample value: mongo-shard-3d7141824182`

Instance ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances">DescribeDBInstances</a> API to query basic information of all MongoDB instances in the target region, including the instance ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**DBInstance ** <span data-label="purple"> Object  </span>`Sample value:`

Instance details list.


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




**ConfigServers ** <span data-label="purple"> Object[]</span>

List of information about ConfigServers.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances support returning this parameter</div>



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



**DBEngine ** <span data-label="purple"> String  </span>`Sample value: MongoDB`

Database engine. The value is fixed to `MongoDB`.



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



**Nodes ** <span data-label="purple"> Object[]</span>

Information list of nodes in a replica set instance or nodes in a sharding cluster Shard.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only supported in replica set instances or sharding cluster Shards.</div>



**NodeDelayTime ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Primary\-secondary delay time. Unit: milliseconds (ms).



**NodeId ** <span data-label="purple"> String  </span>`Sample value: mongo-replica-c70a99ee****-0`

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




**NodeSpec ** <span data-label="purple"> String  </span>`Sample value: mongo.2c4g`

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

The state of the node in the replica set, with data sourced from MongoDB's `rs.status().members[].stateStr`.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">For more information about replica set member states, see <a href="https://www.mongodb.com/docs/manual/reference/replica-states/">Replica Set Member States</a>.</div>





**Mongos ** <span data-label="purple"> Object[]</span>

List of Mongos information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances support returning this parameter</div>



**MongosNodeId ** <span data-label="purple"> String  </span>`Sample value: mongo-shard-011d2479****-0`

The Mongos node ID.



**NodeSpec ** <span data-label="purple"> String  </span>`Sample value: mongo.mongos.2c4g`

Node specification.



**NodeStatus ** <span data-label="purple"> String </span>`Sample value: Running`

Node status.



**TotalMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 4`

Total memory. Unit: GiB.



**TotalvCPU ** <span data-label="purple"> Double  </span>`Sample value: 2`

Total number of cores.



**UsedMemoryGB ** <span data-label="purple"> Double </span>`Sample value: 0.09878921508789062`

Used memory. Unit: GiB.



**UsedvCPU ** <span data-label="purple"> Double  </span>`Sample value: 0.002623241`

Used vCPUs.



**ZoneId ** <span data-label="purple"> String </span>`Sample value: cn-beijing-a`

Availability Zone ID of the current node.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your instance is deployed with multiple availability zones, the availability zones where different role nodes are located will be different. For more details about multi\-availability zone deployment, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/feature-introduction">Multi\-availability zone disaster recovery solution</a>.</div>





**MongosId ** <span data-label="purple"> String  </span>`Sample value: mongo-shard-011d2479****`

Mongos ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances can return this parameter.</div>




**ReclaimTime ** <span data-label="purple"> String  </span>`Sample value: 2022-03-26T03:45:28Z`

The scheduled reclaim time of the instance (UTC).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for Subscription instances.</div>




**Shards ** <span data-label="purple"> Object[]</span>

List of Shards information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only sharding cluster instances support returning this parameter.</div>



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

The state of the node in the replica set, with data sourced from MongoDB's `rs.status().members[].stateStr`.

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




**MaintenanceTime ** <span data-label="purple"> String</span>

Maintenance period



**BackupVersion ** <span data-label="purple"> String</span>

Backup version



**MongoClusterVersion ** <span data-label="purple"> String</span>

mgc version



**MongotInfos ** <span data-label="purple"> Object[]</span>

Mongot node information.


**ShardId ** <span data-label="purple"> String </span>`Sample value: mongo-shard-011d2479****-s0`

Shard node ID.

<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">This parameter is only returned for sharding cluster instances.</div>




**NodeInfos ** <span data-label="purple"> Object[]  </span>`Example value: -`

Details of the Mongot node.


**NodeId ** <span data-label="purple"> String  </span>`Example value: mongo-mongot-011d2479****-node-0`

Node ID.



**ZoneId ** <span data-label="purple"> String  </span>`Sample value: cn-beijing-a`

Availability Zone ID of the node.



**NodeSpec ** <span data-label="purple"> String</span>

Node specifications



**UsedvCPU ** <span data-label="purple"> Double  </span>`Sample value: 0.00256789`

Number of CPU cores used by the node.



**TotalvCPU ** <span data-label="purple"> Double  </span>`Sample value: 2`

Total node core count.



**UsedMemoryGB ** <span data-label="purple"> Double  </span>`Example value: 0.33296966552734375`

Used memory of the node, in GiB.



**TotalMemoryGB ** <span data-label="purple"> Double  </span>`Sample value: 4`

Total memory of the node, in GiB.



**UsedStorageGB ** <span data-label="purple"> Double  </span>`Sample value: 1.56789`

Node storage used, in GiB.



**TotalStorageGB ** <span data-label="purple"> Double  </span>`Sample value: 20`

Node total storage space, in GiB.





**MongotEnable ** <span data-label="purple"> Boolean</span>

Indicates whether Mongot is enabled.




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
