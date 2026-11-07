---
title: "Features"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/feature_overview"
---

This topic describes the features supported by RDS for MySQL.

> **tip**

* > Slow log, Audit log and SQl throttling are are only available to enterprise users.

* > Instances with a storage type of Cloud ESSD FlexPL, Cloud ESSD PL0 or High performance cloud disk are currently available only in the following regions. The available regions and their Region IDs are as follows:

International regions:

，ap\-southeast\-1

* > The following functions are currently invited to test. If you want to use them, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178) to apply.

   * > Modifying specifications temporarily

|<br>**Scope**<br> |<br>**Feature**<br> |<br>**Local disk instance**<br> ||<br>**Cloud disk instance**<br> |||
|---|---|---|---|---|---|---|
|||<br>**Double node**<br> |<br>**Multiple node**<br> |<br>**Single node**<br> |<br>**Double node**<br> |<br>**Multiple node**<br> |
|Managing instances |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) |Support ||Support |||
||[Dedicated type](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications) |Support ||Not support |||
||[General type](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications) |Support ||Support |||
||[Change specification ](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification) |Support ||Support |||
||[Change instance storage space](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification) |Support<br><br> ||Support<br><br>> Description<br><br><br>> Reducing the storage space of a cloud disk instance is not currently supported.<br> |||
||[Change instance storage type](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification) |Not support ||Support<br><br>> **tip**<br><br><br>> The storage type can be changed from PL0 cloud disk to FlexPL cloud disk. Changing from FlexPL cloud disk to PL0 cloud disk is not supported.<br> |||
||[Add node](https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_nodes) |Support ||Not support |Support ||
||[Delete node](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_nodes) |Support ||Not support |Support ||
||[Modifying specifications temporarily](https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade) |Support ||Support |||
||[Changing instance type](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_instance_type) |Support ||Support |Support ||
||[Modify data synchronization method](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_sync_mode) |Support ||Not support |Support ||
||[Migrate nodes to other availability zones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/availability_zone_migration) |Support ||Not support |Support ||
||[Restart instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance) |Support ||Support |||
||[Upgrade instance kernel minor version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version) |Support ||Not support |||
||[Upgrade instance database major version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instances_database_major_version) |Support ||Support |||
||[Delete or unsubscribe an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_or_unsubscribing_an_instance) |Support ||Support |||
||[Exporting instance list](https://docs.byteplus.com/en/docs/RDS_for_MySQL/exporting_an_instance_list) |Support ||Support |||
||[Stopping and starting an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/stopping_and_starting_an_instance) |Support ||Support |||
||[Set instance deletion protection](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Setting_instance_deletion_protection) |Support ||Support |||
||[Creat a same instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_the_same_instance_configuration) |Support ||Support |||
||[Set maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period) |Support ||Support |||
||[Add tag](https://docs.byteplus.com/en/docs/RDS_for_MySQL/managing_tags) |Support ||Support |||
||[Creating a blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment) |Support ||Support |||
|Billing management |[Switch to subscription](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_to_yearly_or_monthly_subscription) |Support ||Support |||
||[Switch to Pay-as-you-go](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_to_pay-as-you-go) |Support ||Support |||
|Manage connections<br><br> |[Enable database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent) |Support ||Support |||
||[Changing the proxy configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_agent_configurations) |Support ||Support |||
||Connecting to instances via [client side programs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_client_application) or [command line](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_command_line) |Support ||Support |||
||[Connect an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_command_line) |Support ||Support |||
||[Create endpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_connection_endpoints) |Support ||Not support |Support ||
||[View connection endpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_connection_endpoints) |Support ||Support |||
||[Modifing an endpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints) |Support ||Support |||
||[Deleting connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_connection_endpoints) |Support ||Not support |Support ||
||[Connect to the database via public network](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access) |Support ||Support |||
||[Enable Read/Write separation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting) |Support ||Not support |Support ||
||[Set read-only latency threshold](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints) |Support ||Not support |Support ||
||[Configure read/Write separation threshold](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints) |Support ||Not support |Support ||
||[Enable global read-only](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting) |Support ||Support |||
||[Switch connection pool mode](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_connection_pool_mode) |Support ||Not support |Support ||
||[Set replication delay of read-only node](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_delayed_replication_for_read-only_nodes) |Support ||Not support |Support ||
||[Public network resolution](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_public_network_resolution) |Support ||Support |||
||[Overload protection](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_overload_protection) |Support ||Not support |Support ||
||[Transaction splitting](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Transaction_splitting) |Support ||Not support |Support ||
||[Connection diagnosis](https://docs.byteplus.com/en/docs/RDS_for_MySQL/diagnosing_connections) |Support ||Support |||
||[Modify instance network configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_instance_network_configuration) |Support ||Support |||
||[Modify the prefix and port of connection address](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_address_prefix_and_port) |Support ||Support |||
|Managing accounts |[Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account) |Support ||Support |||
||[Reset password](https://docs.byteplus.com/en/docs/RDS_for_MySQL/resetting_an_account_password) |Support ||Support |||
||[Modifying account permissions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions) |Support ||Support |||
||[Deleting an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yig6Zmk6LSm5Y-3) |Support ||Support |||
|Managing databases |[Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database) |Support ||Support |||
||[Delete a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_a_database) |Support ||Support |||
|Backups |[Modify backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies) |Support ||Support |||
||[Physical data backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup) |Support ||Not support |||
||[Logical data backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup) |Support ||Not support |||
||[Snapshot backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup) |Not support ||Support |||
||[High frequency backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies) |Support ||Support |||
||[Physical backup encryption](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies) |Support ||Not support |||
||[Download data backup files](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_data_backup_files) |Support ||Not support |||
||[Delete manual backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_deleting_data_backup_files) |Support ||Support |||
||[Create a binlog backup manually](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_backing_up_binlog) |Support ||Support |||
||[Download binlog backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backups) |Support ||Support |||
||Recovering to the a new instance from [a backup set](https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_to_the_new_instance_from_a_backup_set) or [by time point](https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_to_the_new_instance_by_time_point) |Support ||Support |||
||Recovering to the orginal instance from [a backup set](https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_to_the_source_instance_from_a_backup_set) or [by time point](https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_to_the_source_instance_by_time_point) |Support ||Support |||
||[Batch rollback](https://docs.byteplus.com/en/docs/RDS_for_MySQL/batch_rollback) |Support ||Support |||
|Service availability |[Switch primary nodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_primary_nodes) |Support ||Not support |Support ||
|Logs |[View the switchover log and error log](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_and_downloading_logs) |Support ||Support<br><br>> **tip**<br><br><br>> Does not support viewing switchover logs.<br> |Support ||
|Security management |[Allowlist management](https://docs.byteplus.com/en/docs/RDS_for_MySQL/managing_allowlists) |Support ||Support |||
||[Configuring TDE](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_tde) |Support ||Support |||
||[Configure SSL encryption](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_ssl_encryption) |Support ||Support |||
|Managing parameters |[Modify parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters) |Support ||Support |||
||[View records of parameter modification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_parameter_modification_history) |Support ||Support |||
||[Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters) |Support ||Support |||
||[Manage parameter templates](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template) |Support ||Support |||
||[Apply parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/applying_a_parameter_template) |Support ||Support |||
||[Export as a template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/exporting_parameters_as_a_template) |Support ||Support |||
||[Compare parameter](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Comparing_parameter_between_instances) |Support ||Support |||
||[View node difference parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_instance_node_parameter_differences) |Support ||Not support |Support ||
||[Compare parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Comparing_parameter_templates) |Support ||Support |||
|Monitoring |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics) |Support ||Support |||
||[View monitoring information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_monitoring_information) |Support ||Support<br><br>> **tip**<br><br><br><br>* > Deployment and proxy monitoring are not supported.<br><br><br>* > Monitoring by node is not supported.<br> |Support ||
||[Set alert policies](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_alert_policies) |Support ||Support |||
||[Creating event policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_event_policy) |Support ||Support |||
|Online DDL |[Create an online DDL task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_online_ddl_task) |Support ||Support |||
|Database Workshop |[Database Workshop](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Database_Workshop) provides slow log analysis, audit log, limited viewership of SQL, work order, database inspection and automatic operation and maintenance for RDS for MySQL. |Support ||Support<br><br>> **tip**<br><br><br>> The automatic operation and maintenance rules for configuring automatic specification volume expansion and contraction for cloud disk instances are not supported for the time being.<br> |||
|Task center |[View a task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_a_task) |Support ||Support |||
||[Executing a task in advance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Executing_tasks_in_advance) |Support ||Support |||
||[Modify execution time of task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task) |Support ||Support |||
||[Cancelling a task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/cancelling_a_task) |Support ||Support |||
|Operation and maintenance event |[View an event](https://docs.byteplus.com/en/docs/RDS_for_MySQL/view_operation_and_maintenance_events) |Support ||Support |||
||[Executing an operation and maintenance event in advance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Executing_an_operation_and_maintenance_event_in_advance) |Support ||Support |||
||[Modify the switching time of operation and maintenance event](https://docs.byteplus.com/en/docs/RDS_for_MySQL/postponing_operation_and_maintenance_events) |Support ||Support |||
|Backups of deleted instances |[Change backup retention policy of the deleted instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_retention_policy_for_deleted_instances_backups) |Support ||Support |||
||[Download backups of deleted instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Downloading_backups_of_deleted_instances) |Support ||Support |||
||[Rebuild or destroy an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilding_an_instance) |Support ||Support |||
||[Clean backups of deleted instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Clearing_backups_of_deleted_instances) |Support ||Support |||
||[Renewal](https://docs.byteplus.com/en/docs/RDS_for_MySQL/unlocking_an_instance_by_renewal) |Support ||Support |||
