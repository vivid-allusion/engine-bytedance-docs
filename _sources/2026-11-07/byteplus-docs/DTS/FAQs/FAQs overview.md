---
title: "FAQs overview"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Overview"
---

This topic describes common issues and solutions that you may encounter when using Database Transmission Service (DTS). If the problem you encounter is not included in this topic, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical staff for assistance.

<span id="H8h6c4PF"></span>
## Common general questions


* [Common FAQs for using Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/which_databases_does_DTS_currently_support)

* [Common issues about billing method and overdue payments](https://docs.byteplus.com/en/docs/DTS/What_billing_methods_does_Database_Transmission_)

* [Common issues about access security and business impact](https://docs.byteplus.com/en/docs/DTS/will_the_data_in_the_source_database_be_deleted_when_using_DTS_for_data_migration)

* [When does the incremental phase start after the full migration phase is complete? Does the incremental task end automatically?](https://docs.byteplus.com/en/docs/DTS/why_does_the_incremental_data_migration_task_keep_running_and_never_end)

* [During task execution, can the system automatically handle new tables or schema changes added at the source end?](https://docs.byteplus.com/en/docs/DTS/Can_newly_added_tables_)

* [How to handle data conflict and primary key conflict?](https://docs.byteplus.com/en/docs/DTS/What_if_a_data_conflict_occurs)

* [Why are some migration types not visible on the Task progress tab?](https://docs.byteplus.com/en/docs/DTS/why_are_some_migration_types_not_displayed_under_the_migration_progress_tab)

* [How to set the definer of a database object after the MySQL structural migration is complete?](https://docs.byteplus.com/en/docs/DTS/How_to_set_the_DEFINER_of_database_objects_during_MySQL_schema_migration_or_initialization)

* [Common issues in data verification tasks](https://docs.byteplus.com/en/docs/DTS/Why_do_some_data_verification_tasks)

* [What are the possible causes of task delay?](https://docs.byteplus.com/en/docs/DTS/what_are_the_possible_reasons_for_task_delays_during_data_migration_or_synchronization_tasks)

* [How to obtain the instance's GTID_EXECUTED?](https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance)

* [Do I need to rename the table when migrating data within the same instance and synchronizing data from table A to table B?](https://docs.byteplus.com/en/docs/DTS/do_I_need_to_rename_the_table_)

* [Why is the key to data in the JSON type field not order-preserving?](https://docs.byteplus.com/en/docs/DTS/why_is_the_key_to_data_in_)

* [Why is the number of data rows inconsistent with the Binlog Event during data subscription?](https://docs.byteplus.com/en/docs/DTS/why_is_the_number_of_data_rows_inconsistent)

* [What to do when encountering data dispersion and large page holes after synchronization?](https://docs.byteplus.com/en/docs/DTS/What_should_we_do_if_we_encounter_data_fragmentation)

* [How can RDS for MySQL instances achieve data disaster recovery?](https://docs.byteplus.com/en/docs/DTS/How_can_RDS_for_MySQL)

* [How to quickly complete the migration or synchronization of MySQL data?](https://docs.byteplus.com/en/docs/DTS/How_to_quickly_complete_the_migration)

* [Why are there bandwidth alarms during the data migration or data synchronization process?](https://docs.byteplus.com/en/docs/DTS/Why_are_there_bandwidth_alarms)

* [How to rename and display fields after synchronizing table A to table B?](https://docs.byteplus.com/en/docs/DTS/How_to_display_the_field_named)

* [What if the subscription task fails when subscribing messages to Message Queue for Kafka?](https://docs.byteplus.com/en/docs/DTS/What_if_the_subscription_task_fails)

* [How to migrate data from the third-party MySQL to BytePlus RDS for MySQL?](https://docs.byteplus.com/en/docs/DTS/How_to_migrate_data_from)

* [I encountered an error when configuring the timestamp to start synchronization. How should I handle it?](https://docs.byteplus.com/en/docs/DTS/I_encountered_an_error_when)

* [When calling the CreateTransmissionTask API to create a PostgreSQL data migration task, how should I handle an error?](https://docs.byteplus.com/en/docs/DTS/When_calling_the_CreateTransmissionTas)

* [Does DTS support synchronizing data from read-only nodes of the source MongoDB database?](https://docs.byteplus.com/en/docs/DTS/Does_DTS_support_synchronizing)

* [How to implement incremental migration when the source database is a single node MongoDB instance?](https://docs.byteplus.com/en/docs/DTS/how_to_perform_incremental_migration_or_incremental_synchronization)

* [How to clean orphaned documents in MongoDB (sharding cluster architecture)?](https://docs.byteplus.com/en/docs/DTS/how-to-clean-orphaned-documents-in-MongoDB-sharding-cluster-architecture)

* [Is it supported to change the link specifications of data migration?](https://docs.byteplus.com/en/docs/DTS/can_I_change_the_link_specification_for_data_migration)

* [Why is the post-schema migration not started, yet the status is shown as "Complete"?](https://docs.byteplus.com/en/docs/DTS/Why_is_the_post-schema)

* [Why does the task status remain unchanged after the task is terminated and deleted?](https://docs.byteplus.com/en/docs/DTS/why_does)

* [What if an error occurs when connecting to an instance while creating a data transmission task?](https://docs.byteplus.com/en/docs/DTS/what_if_an_error)

* [Redis FAQ](https://docs.byteplus.com/en/docs/DTS/How_can_I_migrate_data_from_a_Redis_database)


<span id="sqv0ybGt"></span>
## **Common pre\-check errors**


* [Error source database parameters gtid_mode inconsistent with expectations, expectations are: ON, but set to: OFF, how to do?](https://docs.byteplus.com/en/docs/DTS/Error_source_database_parameters_gtid_mode)

* [What causes the check for the database connection and structure wildcard rules to fail?](https://docs.byteplus.com/en/docs/DTS/Wwhat_causes_the_check_for_the_database_connection)

* [Why does the pre-check still fail after adding all custom privileges to the ordinary database account?](https://docs.byteplus.com/en/docs/DTS/why_does_pre-check_fail_after_I_added_all_custom_permissions_to_general_account)


<span id="Vvz87Lpr"></span>
## **Troubleshooting**


* [What if the network environment is unstable during data transmission over express networks?](https://docs.byteplus.com/en/docs/DTS/What_if_the_network_environment_is_unstable_during_data_transmission_over_express_)

* [What causes a task to fail during execution?](https://docs.byteplus.com/en/docs/DTS/what_are_the_reasons_for_task_execution_failures_during_the_task_execution_process)

* [Guide to troubleshooting data consistency abnormalities in migration and synchronization](https://docs.byteplus.com/en/docs/DTS/why_are_data_on_source_and_target_instances_inconsistent_during_migration_or_sync_tasks)

* [How to ensure immediate effectiveness after enabling the Binlog parameter on the MySQL source database?](https://docs.byteplus.com/en/docs/DTS/how_can_I_bring_parameter_format_immediately_effective)

* [Error 4109 (HY000): Failed to generate invisible primary key. What to do?](https://docs.byteplus.com/en/docs/DTS/Error_4109_HY000_)

* [How to resolve the error: err[Error 1273 (HY000): Unknown collation: 'utf8mb4_0900_ai_ci']?](https://docs.byteplus.com/en/docs/DTS/what_should_I_do_if_an_authentication_failure_error_occurs)

* [What if you encounter the error described in this topic when performing data synchronization from MySQL to ElasticSearch?](https://docs.byteplus.com/en/docs/DTS/What_if_you_encounter_the_error_described_in_this_topic_when_performing_)

* [Why is a heartbeat table needed when enabling millisecond-level latency monitoring?](https://docs.byteplus.com/en/docs/DTS/Why_is_a_heartbeat_table_required_when_enabling_millisecond-level_latency_monitoring)

* [Why does the destination's disk usage exceed the source's after full migration?](https://docs.byteplus.com/en/docs/DTS/After_the_PostgreSQL_type_of_migration_task_is_complete)

* [Guide to troubleshooting performance abnormalities during migration and synchronization](https://docs.byteplus.com/en/docs/DTS/What_if_migration_or_synchronization_is_slow_)

* [Why does the progress of full migration or full initialization remain stalled for a long time?](https://docs.byteplus.com/en/docs/DTS/why_is_there_no_progress_in_the_full_initialization_task_during_data_synchronization)

* [What should I do if I encounter the error error 1054 (42s22): unknown column 'my_row_id' in 'field list' when synchronizing data from MySQL 8.0 to 5.7?](https://docs.byteplus.com/en/docs/DTS/What_should_I_do_if_I)
