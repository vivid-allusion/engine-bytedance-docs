---
title: "Common concepts"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Common_concepts"
---

This document summarizes the common concepts and data models of Table Storage for HBase instances.

<span id=".5bi455So5qaC5b-1"></span>
## Common concepts


|Concepts |Description |
|---|---|
|Region |The geographical location of the data. Refer to [Service endpoint](https://docs.byteplus.com/en/docs/HBase/Request_structure#.5pyN5Yqh5Zyw5Z2A) for regions where HBase is available. |
|Availability zone |Abbreviated as AZ. Each region has multiple isolated areas called availability zones. |
|Instance |The basic unit for managing cloud resources in HBase. Instance performance varies with its specifications, such as the number of CPU cores and memory size. For more information about HBase instance specifications, see [Product specifications](https://docs.byteplus.com/en/docs/HBase/Product_specifications). |
|Master node |HBase HMaster is deployed on master nodes. HMaster manages and coordinates HRegionServers, and handles CRUD operations for tables. By default, each HBase instance is created with two master nodes (one primary and one standby). |
|Region Server Node |A Region Server node stores and manages HRegions and provides read and write services for table data. Each HBase instance can have 2 to 100 Region Server nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In HBase, tables are partitioned by row into multiple HRegions. An HRegion is the smallest unit of distributed storage and load balancing, and different HRegions can be distributed on different HRegionServers.</div><br> |
|ZK connection address |Table Storage for HBase instances provide a ZK connection address by default. You can use the Java API to access an HBase instance directly through the ZK connection address. For more information, see [Connecting to the instance using the Java API](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_Java_API_1). |
|High\-availability Thrift connection address |Table Storage for HBase supports multi\-language access through Thrift, including Python, Go, and PHP. The supported Thrift protocol version is Thrift2. For details, see [Access an HBase instance from a Python program using a Thrift2 address](https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Python_program_using_a_Thrift2_address). |
|Virtual private cloud |A Virtual Private Cloud (VPC), is an isolated network environment with higher security and performance than those of the traditional classic network. |
|Internal Address |HBase instances provide a private IP address by default, which allows direct access from an ECS instance within the same VPC. |
|Public network address |You can apply for a public IP address for your HBase instance to allow access from devices outside the VPC. For details, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access). |


<span id=".5pWw5o2u5qih5Z6L"></span>
## Data model


|Concepts |Description |
|---|---|
|Namespace |A namespace is a logical grouping of tables, similar to a database in RDS. It is used to categorize tables by business.<br><br>Table Storage for HBase defines two namespaces by default: `hbase` and `default`. The `hbase` namespace stores internal system tables, and the `default` namespace stores tables created without a specified namespace. |
|Row Key |An HBase table consists of column families. Each row in the table is uniquely identified by a row key. |
|Column Family |An HBase table consists of several column families, each of which contains multiple columns. All columns in a column family are prefixed with the name of that column family. For example, columns `cf:col1` and `cf:col2` both belong to the `cf` column family.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum number of versions for a column family in an HBase instance is an integer ranging from 1 to 2,147,483,647. If not set, the default value is 1.</div><br> |
|Column Qualifier |A column qualifier can be understood as an attribute of a column. For example, the column qualifiers for the columns `cf:col1` and `cf:col2` are `col1` and `col2`, respectively. |
|Column |A column in HBase consists of a column family and a column qualifier, separated by a colon (`:`), for example, `cf:col1` is a complete column name. |
|Timestamp |When you update data in an HBase table, old versions are not deleted. Instead, the system automatically adds a timestamp to each new entry to identify different versions of the data. |
|Cell |A Cell is a storage unit identified by a Row Key and a Column. Each Cell contains multiple versions of the same data, distinguished by a Timestamp. |
