---
title: "Volume instance specifications"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/volume_instance_spec"
---

This topic describes the volume instance specifications supported by BytePlus Document Database for MongoDB.

## Precautions

* Currently, instances with volumes storage type only support dedicated specification node. For more details, see [Specification types](https://docs.byteplus.com/en/docs/mongodb/storage_type).

* To use FlexPL volume, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

## Compute node specifications

> **tip**

* > The node type in replica set instances is Mongod. Each replica set instance is currently fixed at 3 nodes and cannot be changed.

* > Each sharding cluster instance can contain 2~32 Mongos nodes and 2~32 shards (each shard contains 3 nodes).

* > The recommended number of connections in the table below refers to the recommended number of connections for a single node. You can also modify the number of connections for a single node by using the `net.maxIncomingConnections` parameter. For more information about the `net.maxIncomingConnections` parameter, refer to [Supported parameters](https://docs.byteplus.com/en/docs/mongodb/supported-parameter). For parameter modification methods, refer to [Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter).

### Replica set instance

|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.vm.ded.2c4g |2 cores 4 GiB |2000 |
|mongo.vm.ded.4c8g |4 cores 8 GiB |4000 |
|mongo.vm.ded.4c16g |4 cores 16 GiB |6000 |
|mongo.vm.ded.4c32g |4 cores 32 GiB |8000 |
|mongo.vm.ded.8c16g |8 cores 16 GiB |16000 |
|mongo.vm.ded.8c32g |8 cores 32 GiB |16000 |
|mongo.vm.ded.8c64g |8 cores 64 GiB |16000 |
|mongo.vm.ded.16c32g |16 cores 32 GiB |24000 |
|mongo.vm.ded.16c64g |16 cores 64 GiB |24000 |
|mongo.vm.ded.16c128g |16 cores 128 GiB |24000 |
|mongo.vm.ded.32c64g |32 cores 64 GiB |24000 |
|mongo.vm.ded.32c128g |32 cores 128 GiB |42000 |
|mongo.vm.ded.32c256g |32 cores 256 GiB |42000 |
|mongo.vm.ded.64c128g |64 cores 128 GiB |64000 |

### **Sharding cluster instance**

**Mongos**

|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.mongos.ded.2c4g |2 cores 4 GiB |2000 |
|mongo.mongos.ded.4c8g |4 cores 8 GiB |4000 |
|mongo.mongos.ded.4c16g |4 cores 16 GiB |6000 |
|mongo.mongos.ded.4c32g |4 cores 32 GiB |8000 |
|mongo.mongos.ded.8c16g |8 cores 16 GiB |16000 |
|mongo.mongos.ded.8c32g |8 cores 32 GiB |16000 |
|mongo.mongos.ded.8c64g |8 cores 64 GiB |16000 |
|mongo.mongos.ded.16c32g |16 cores 32 GiB |24000 |
|mongo.mongos.ded.16c64g |16 cores 64 GiB |24000 |
|mongo.mongos.ded.16c128g |16 cores 128 GiB |24000 |
|mongo.mongos.ded.32c64g |32 cores 64 GiB |24000 |
|mongo.mongos.ded.32c128g |32 cores 128 GiB |42000 |
|mongo.mongos.ded.32c256g |32 cores 256 GiB |42000 |
|mongo.mongos.ded.64c128g |64 cores 128 GiB |64000 |

**Shard**

|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.mongos.ded.2c4g |2 cores 4 GiB |2000 |
|mongo.mongos.ded.4c8g |4 cores 8 GiB |4000 |
|mongo.mongos.ded.4c16g |4 cores 16 GiB |6000 |
|mongo.mongos.ded.4c32g |4 cores 32 GiB |8000 |
|mongo.mongos.ded.8c16g |8 cores 16 GiB |16000 |
|mongo.mongos.ded.8c32g |8 cores 32 GiB |16000 |
|mongo.mongos.ded.8c64g |8 cores 64 GiB |16000 |
|mongo.mongos.ded.16c32g |16 cores 32 GiB |24000 |
|mongo.mongos.ded.16c64g |16 cores 64 GiB |24000 |
|mongo.mongos.ded.16c128g |16 cores 128 GiB |24000 |
|mongo.mongos.ded.32c64g |32 cores 64 GiB |24000 |
|mongo.mongos.ded.32c128g |32 cores 128 GiB |42000 |
|mongo.mongos.ded.32c256g |32 cores 256 GiB |42000 |
|mongo.mongos.ded.64c128g |64 cores 128 GiB |64000 |

**ConfigServer**

|Specification code |CPU and memory |Recommended number of connections |
|---|---|---|
|mongo.config.ded.2c4g |2 cores 4 GiB |2000 |
|mongo.config.ded.4c8g |4 cores 8 GiB |4000 |
|mongo.config.ded.4c16g |4 cores 16 GiB |6000 |
|mongo.config.ded.4c32g |4 cores 32 GiB |8000 |
|mongo.config.ded.8c16g |8 cores 16 GiB |16000 |
|mongo.config.ded.8c32g |8 cores 32 GiB |16000 |
|mongo.config.ded.8c64g |8 cores 64 GiB |16000 |
|mongo.config.ded.16c32g |16 cores 32 GiB |24000 |
|mongo.config.ded.16c64g |16 cores 64 GiB |24000 |

## Storage specifications

The storage space for Document Database for MongoDB instances is divided into single\-shard or single\-node storage, and maximum available storage.

### Single\-shard or single\-node storage

This refers to the replica set storage space specifications selected when purchasing an instance, or the storage space specifications of Shard and ConfigServer nodes in a sharding cluster instance.

The storage range supported by MongoDB Volumes instances is shown in the following table.

|Instance (or component) type ||Specification code |Storage range |
|---|---|---|---|
|Replica set instance ||mongo.essdflexpl |The storage range supported by all node specifications is: 20 GiB ~ 16000 GiB. |
|Sharding cluster instance |Shard |||
||ConfigServer node |||

### Maximum available storage

It refers to the disk space available for storing business data. You can view the instance's maximum available storage space information on the instance information page. For specific procedures, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance).

The calculation method of maximum available storage capacity varies with the instance type. The specific calculation method is shown in the table below.

|Instance type |Replica set |Sharding cluster |
|---|---|---|
|Maximum available storage |Single node storage specification |Number of shards x Single\-shard storage + ConfigServer storage |
