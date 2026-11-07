---
title: "Features overview"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Features_overview"
---

This article summarizes the features supported by NDB for MySQL instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the table, ✔️ indicates the feature is supported by the corresponding instance version, and ❌ indicates it is not supported.</div>



|Type |Function |Compatible with MySQL 8.0 |Compatible with MySQL 5.7 |
|---|---|---|---|
|||3.0.\*.\* |2.0.\*.\* |
|Managing instances |[Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) |✔️ |✔️ |
||[Changing instance configuration](https://www.byteplus.com/en/docs/NDB_for_MySQL/Changing_instance_configuration) |✔️ |✔️ |
||[Switching to primary node](https://www.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node) |✔️ |✔️ |
||[Exporting instance list](https://www.byteplus.com/en/docs/NDB_for_MySQL/Exporting_instance_list) |✔️ |✔️ |
||[Restarting instances](https://www.byteplus.com/en/docs/NDB_for_MySQL/Restarting_instances) |✔️ |✔️ |
||[Deleting or unsubscribing an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Deleting_or_unsubscribing_an_instance) |✔️ |✔️ |
||[Managing tags](https://www.byteplus.com/en/docs/NDB_for_MySQL/Managing_tags) |✔️ |✔️ |
||[Configuring maintenance window](https://www.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window) |✔️ |✔️ |
||[Read/Write separation](https://www.byteplus.com/en/docs/NDB_for_MySQL/Read_write_splitting) |✔️ |✔️ |
||[Instance deletion protection](https://www.byteplus.com/en/docs/NDB_for_MySQL/Instance_deletion_protection) |✔️ |✔️ |
||[Connection persistence](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_persistence) |✔️ |✔️ |
|Managing connections |[Connecting to an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Connecting_to_an_instance_1) |✔️ |✔️ |
||[Viewing instance topology](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_instance_topology) |✔️ |✔️ |
||[View access address](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_connection_endpoints) |✔️ |✔️ |
||[Enabling or disabling public network access](https://www.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_access) |✔️ |✔️ |
||[Managing connection endpoints](https://www.byteplus.com/en/docs/NDB_for_MySQL/Managing_connection_endpoints) |✔️ |✔️ |
||[Enabling or disabling public network resolution](https://www.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_resolution) |✔️ |✔️ |
||[Modifying address prefix and port](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_address_prefix_and_port) |✔️ |✔️ |
||[Modifying VPC and subnet](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_VPC_and_subnet) |✔️ |✔️ |
|Managing databases |[Creating database](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_database) |✔️ |✔️ |
||[Deleting a database](https://www.byteplus.com/en/docs/NDB_for_MySQL/Deleting_a_database) |✔️ |✔️ |
||[Modifying database description](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_database_description) |✔️ |✔️ |
|Account and access authorization |[Creating and deleting accounts](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts) |✔️ |✔️ |
||[Reset standard account permissions](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_normal_account_permissions) |✔️ |✔️ |
||[Resetting super account permissions](https://www.byteplus.com/en/docs/NDB_for_MySQL/Resetting_super_account_permissions) |✔️ |✔️ |
||[Changing account password](https://www.byteplus.com/en/docs/NDB_for_MySQL/Changing_account_password) |✔️ |✔️ |
||[Modifying account description](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_account_description) |✔️ |✔️ |
||[Sub-user project management](https://www.byteplus.com/en/docs/6357/1276595) |✔️ |✔️ |
|Managing data security |[Viewing allowlist information](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_allowlist_information) |✔️ |✔️ |
||[Creating an allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist) |✔️ |✔️ |
||[Modifying an allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist) |✔️ |✔️ |
||[Associating allowlist and instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Associating_allowlist_and_instance) |✔️ |✔️ |
||[Disassociating instance and allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Disassociating_instance_and_allowlist) |✔️ |✔️ |
||[Deleting an allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Deleting_an_allowlist) |✔️ |✔️ |
||[Copying an allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Copying_an_allowlist) |✔️ |✔️ |
||[Synchronizing security group](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Synchronizing_security_group) |✔️ |✔️ |
|Backup recovery |[Set automatic backup policy](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_basic_backup_policies) |✔️ |✔️ |
||[Create backup manually](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_data_backup_manually) |✔️ |✔️ |
||[Deleting data backup files](https://www.byteplus.com/en/docs/NDB_for_MySQL/Deleting_data_backup_files) |✔️ |✔️ |
||[Recovering to the new instance from a backup set](https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_to_the_new_instance_from_a_backup_set) |✔️ |✔️ |
||[Recovering to the new instance by time point](https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_to_the_new_instance_by_time_point) |✔️ |✔️ |
||[Recovering database and table from a backup set](https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_database_and_table_by_backup_set) |✔️ |❌ |
||[Recovering database and table by time point](https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_database_and_table_by_time_point) |✔️ |❌ |
||[Managing backups of deleted instances](https://www.byteplus.com/en/docs/NDB_for_MySQL/Backups_of_deleted_instances) |✔️ |✔️ |
|Monitoring and alerts |[Monitoring metrics](https://www.byteplus.com/en/docs/NDB_for_MySQL/Monitoring_metrics) |✔️ |✔️ |
||[Viewing monitoring information](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_monitoring_information) |✔️ |✔️ |
||[Creating alert policies](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_alert_policies) |✔️ |✔️ |
|Managing parameters |[Modifying parameters](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters) |✔️ |✔️ |
||[Viewing parameter modification history](https://www.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec) |✔️ |✔️ |
||[Creating a parameter template](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_parameter_template) |✔️ |✔️ |
||[Apply parameter template](https://www.byteplus.com/en/docs/NDB_for_MySQL/Apply_parameter_template) |✔️ |✔️ |
||[Deleting a parameter template](https://www.byteplus.com/en/docs/NDB_for_MySQL/Deleting_a_parameter_template) |✔️ |✔️ |
||[Exporting parameters as a template](https://www.byteplus.com/en/docs/NDB_for_MySQL/Exporting_parameters_as_a_template) |✔️ |✔️ |
|Task center |[Viewing task list](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_task_list) |✔️ |✔️ |
|Planned events |[Viewing event list](https://www.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list) |✔️ |✔️ |
||[Modifying event execution time](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_event_execution_time) |✔️ |✔️ |
||[Cancelling the scheduled events](https://www.byteplus.com/en/docs/NDB_for_MySQL/Cancelling_the_scheduled_events) |✔️ |✔️ |
