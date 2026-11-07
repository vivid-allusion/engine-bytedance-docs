---
title: "Constraints and limits"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/constraints_and_limits"
---

This topic describes the usage constraints of MySQL instances.

|Constraint |Description |
|---|---|
|Instance parameter |Instance parameters are modified via the console or API. However, only certain parameters can be modified to ensure security and stability. For more information, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters). |
|Database account privileges |Root privileges are not provided. |
|Account privileges |If there are still uncleared MySQL resources under the account, you cannot remove MySQL permissions from the account in access control. |
|Database creation |You can create a database via the command line, but you cannot perform database authorization and deletion operations in the console if the database name contains special characters other than underscores (_) or hyphens (\-), such as `!@#$%^&*()+=`. |
|Database backup |Physical backup is supported via the console or API only. |
|Database recovery |Physical recovery is supported via the console or API only. |
|Database replication |MySQL provides a primary\-secondary replication architecture. In a double\-node instance, the secondary node is not directly accessible by users. You can add 10 read\-only nodes, and the data on each node is exactly the same as the primary node. In multi\-node instance types, the secondary nodes are accessible. The instance can have up to 8 secondary nodes, and the data on each secondary node is exactly the same as that on the primary node.<br><br>> **warning**<br><br><br><br>* > For multi\-node instances, it is recommended to reserve an independent secondary node that does not carry business, so that it can be switched to the primary node if necessary. RDS for MySQL assumes no responsibility if the primary node switch fails because an independent secondary node was not set up.<br><br><br>* > Single\-node instances do not have a primary\-secondary replication structure.<br> |
|Instance restart |Instances are restarted via the console or API only. Single node instances only support force restart. |
|Database version |MySQL 5.7, MySQL 8.0, and MySQL 8.4 versions are supported. |
|Storage engine |MyISAM engine, Memory engine, or Archive engine are not supported.<br><br>> **tip**<br><br><br>> If you specify the storage engine as MyISAM, Memory, or Archive when creating a table, or set the default storage engine to MyISAM, Memory, or Archive, RDS for MySQL automatically converts the storage engine to InnoDB. For details about the automatic conversion, refer to [Automatic conversion of storage engines to InnoDB](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Automatically_converts_storage_engine_to_InnoDB).<br> |
|Database access |If the instance does not allow Internet access, it must be in the same VPC as the ECS instance to allow mutual access. The default port of the instance is 3306, which can be modified. For more details, refer to [Modifying address prefix and port](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_address_prefix_and_port). |
|Database plugins |Keyring_file, rpl_semi_sync_slave, rpl_semi_sync_master, rpl_semi_sync_replica, and rpl_semi_sync_source are required plugins for RDS for MySQL and cannot be uninstalled. |
|Single\-table size limit |The effective maximum size of a single table is typically constrained by the operating system's file size limit rather than MySQL's internal mechanisms. Due to some metadata overhead, the maximum size of a single table in ApsaraDB RDS for MySQL is slightly less than 16 TB. |
|Deployment |The server where the instance is deployed is not visible to users. Applications can only access the database through an IP address and domain name. |
