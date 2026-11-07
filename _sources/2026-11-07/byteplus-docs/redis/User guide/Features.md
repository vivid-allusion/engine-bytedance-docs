---
title: "Features"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/features"
---

This topic summarizes the features supported by various instance types of Cache for Redis for your reference.

> **tip**

> In the following tables, ✔️ indicates that the corresponding instance type supports this feature, while ❌ indicates that it does not.

* > Direct connection mode is only available when the database version is Redis 7.0 and shard cluster is not enabled. The direct connection feature without shard cluster enabled is currently an allowlist feature. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to apply.

## Instance management

|Feature |Type of instance architecture ||||||
|---|---|---|---|---|---|---|
||Primary\-secondary instance |||Single\-node instance |||
||Sharding cluster enabled |Sharding cluster disabled ||Sharding cluster enabled |Sharding cluster disabled ||
|||**Proxy mode** |**Direct connection mode** ||**Proxy mode** |**Direct connection mode** |
|[Purchasing instance with same configuration](https://docs.byteplus.com/en/docs/redis/purchase-same-config-instance) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Restart instance](https://docs.byteplus.com/en/docs/redis/restart-instance) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Restarting proxy node](https://docs.byteplus.com/en/docs/redis/restart-proxy-node) |✔️ |✔️ |❌ |✔️ |✔️ |❌ |
|[Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Deleting pay-as-you-go instance](https://docs.byteplus.com/en/docs/redis/delete-instance) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Unsubscribing from yearly or monthly subscription instance](https://docs.byteplus.com/en/docs/redis/unsubscribe-instance) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Modifying maintenance periods in batches](https://docs.byteplus.com/en/docs/redis/modifying_maintainable_periods_in_batches) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Exporting instance list](https://docs.byteplus.com/en/docs/redis/export-instance-list) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Task management](https://docs.byteplus.com/en/docs/redis/task-management) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Upgrading minor version](https://docs.byteplus.com/en/docs/redis/upgrade-minor-version) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |
|[Setting query result cache](https://docs.byteplus.com/en/docs/redis/set_query_result_cache) |✔️ |✔️ |✔️ |✔️ |✔️ |✔️ |

## High availability

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||**Primary\-secondary instance** ||**Single\-node instance** ||
||**Sharding cluster enabled** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster disabled** |
|[Failover](https://docs.byteplus.com/en/docs/redis/failover) |✔️ |✔️ |❌ |❌ |
|[Executing failover manually](https://docs.byteplus.com/en/docs/redis/switch-primary-node-manually) |✔️ |✔️ |❌ |❌ |
|[Deploying in multiple availability zones](https://docs.byteplus.com/en/docs/redis/deploy-multi-az) |✔️ |✔️ |❌ |❌ |
|[Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az) |✔️ |✔️ |✔️ |✔️ |

## Changing instance configuration

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||**Primary\-secondary instance** ||**Single\-node instance** ||
||**Sharding cluster enabled** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster disabled** |
|[Modifying number of nodes](https://docs.byteplus.com/en/docs/redis/modify-node-number) |✔️ |✔️ |❌ |❌ |
|[Modifying number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number) |✔️ |❌ |✔️ |❌ |
|[Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec) |✔️ |✔️ |✔️ |✔️ |
|[Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config) |❌ |✔️ |❌ |✔️ |
|[Switching to primary-secondary instance](https://docs.byteplus.com/en/docs/redis/switch_to_high_availability_instance) |❌ |❌ |✔️ |✔️ |

## Billing management

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Automatic and manual renewal](https://docs.byteplus.com/en/docs/redis/automatic-manual-renewal) |✔️ |✔️ |✔️ |✔️ |
|[Switching to subscription](https://docs.byteplus.com/en/docs/redis/switch-to-subscription) |✔️ |✔️ |✔️ |✔️ |
|[Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/redis/switch-to-pay-as-you-go) |✔️ |✔️ |✔️ |✔️ |

## Tag management

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Associating or adding tag](https://docs.byteplus.com/en/docs/redis/associate-tag) |✔️ |✔️ |✔️ |✔️ |
|[Filtering instances by tag](https://docs.byteplus.com/en/docs/redis/filter-by-tag) |✔️ |✔️ |✔️ |✔️ |
|[Disassociating or deleting tag](https://docs.byteplus.com/en/docs/redis/disassociate-tag) |✔️ |✔️ |✔️ |✔️ |

## Network connection management

|Feature |Type of instance architecture ||||||
|---|---|---|---|---|---|---|
||Primary\-secondary instance |||Single\-node instance |||
||Sharding cluster enabled |Sharding cluster disabled ||Sharding cluster enabled |Sharding cluster disabled ||
|||**Proxy mode** |**Direct connection mode** ||**Proxy mode** |**Direct connection mode** |
|[Enabling proxy connection private network access](https://docs.byteplus.com/en/docs/redis/Enabling_or_disabling_private_network_access) |❌ |❌ |✔️ |❌ |❌ |✔️ |
|[Disabling proxy connection private network access](https://docs.byteplus.com/en/docs/redis/Enabling_or_disabling_private_network_access?lang=en) |❌ |✔️ (When direct connection mode is enabled) |✔️ (When proxy connection mode is enabled) |❌ |✔️ (When direct connection mode is enabled) |✔️ (When proxy connection mode is enabled) |
|[Turn on direct private network access](https://docs.byteplus.com/en/docs/redis/Enabling_or_disabling_private_network_access?lang=en) |❌ |✔️ |❌ |❌ |✔️ |❌ |
|[Disabling direct connection private network access](https://docs.byteplus.com/en/docs/redis/Enabling_or_disabling_private_network_access?lang=en) |❌ |✔️ (When proxy connection mode is enabled) |❌ (When direct connection mode is enabled) |❌ |✔️ (When proxy connection mode is enabled) |❌ (When direct connection mode is enabled) |
|[Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address) |✔️ |✔️ | |✔️ |✔️ | |
|[Releasing public network access](https://docs.byteplus.com/en/docs/redis/release-public-address) |✔️ |✔️ | |✔️ |✔️ | |
|[Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) |✔️ |❌ | |✔️ |❌ | |
|[Releasing direct connection address](https://docs.byteplus.com/en/docs/redis/release-direct-connection-address) |✔️ |❌ | |✔️ |❌ | |
|[Modifying VPC or subnet](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet) |✔️ |✔️ | |✔️ |✔️ | |
|[Modifying maximum connections](https://docs.byteplus.com/en/docs/redis/modify-max-conn-number) |✔️ |✔️ | |✔️ |✔️ | |
|[Modifying connection address](https://docs.byteplus.com/en/docs/redis/modify-address) |✔️ |✔️ | |✔️ |✔️ | |
|[Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port) |✔️ |✔️ | |✔️ |✔️ | |
|[Upgrading domain suffix](https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix) |✔️ |✔️ | |✔️ |✔️ | |
|[Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth) |✔️ |✔️ | |✔️ |✔️ | |
|[Password-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access) |✔️ |✔️ | |✔️ |✔️ | |
|[Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/redis/set-public-network-resolution) |✔️ |✔️ | |✔️ |✔️ | |
|[Connection diagnostics](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics) |✔️ |✔️ | |✔️ |✔️ | |
|[Connecting to instance via private address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address) |✔️ |✔️ | |✔️ |✔️ | |
|[Connecting to instance via public address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address) |✔️ |✔️ | |✔️ |✔️ | |
|[Connecting to instance via direct connection address](https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address) |✔️ |❌ | |✔️ |❌ | |
|[Connecting to instance via client application](https://docs.byteplus.com/en/docs/redis/connect-instance-via-client) |✔️ |✔️ | |✔️ |✔️ | |
|[Connecting to instance via Redis-cli](https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli) |✔️ |✔️ | |✔️ |✔️ | |
|[Connecting to instance via DBW](https://docs.byteplus.com/en/docs/redis/connecting_to_an_instance_via_dbw) |✔️ |✔️ | |✔️ |✔️ | |

## Account and access authorization

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Creating role](https://docs.byteplus.com/en/docs/redis/create-role) |✔️ |✔️ |✔️ |✔️ |
|[Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account) |✔️ |✔️ |✔️ |✔️ |
|[Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password) |✔️ |✔️ |✔️ |✔️ |
|[Cross-service access authorization](https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization) |✔️ |✔️ |✔️ |✔️ |
|[Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers) |✔️ |✔️ |✔️ |✔️ |

## Data security

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Editing allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Copying allowlist](https://docs.byteplus.com/en/docs/redis/copying_a_allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Associating instances and allowlists](https://docs.byteplus.com/en/docs/redis/associate-allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/redis/disassociate-allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Copying allowlist](https://docs.byteplus.com/en/docs/redis/copying_a_allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Deleting allowlist](https://docs.byteplus.com/en/docs/redis/delete-allowlist) |✔️ |✔️ |✔️ |✔️ |
|[Synchronizing security group](https://docs.byteplus.com/en/docs/redis/synchronizing_the_security_group) |✔️ |✔️ |✔️ |✔️ |
|[Setting SSL encryption](https://docs.byteplus.com/en/docs/redis/setup-ssl) |✔️ |✔️ |✔️ |✔️ |
|[Clearing data](https://docs.byteplus.com/en/docs/redis/clear-data) |✔️ |✔️ |✔️ |✔️ |
|[Connecting to Redis from client via SSL encryption](https://docs.byteplus.com/en/docs/redis/connect-redis-from-client-via-ssl) |✔️ |✔️ |✔️ |✔️ |

## Monitoring and alerts

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data) |✔️ |✔️ |✔️ |✔️ |
|[Viewing monitoring dashboard](https://docs.byteplus.com/en/docs/redis/view-monitoring-dashboard) |✔️ |✔️ |✔️ |✔️ |
|[Setting alerts](https://docs.byteplus.com/en/docs/redis/set-alert) |✔️ |✔️ |✔️ |✔️ |
|[Event monitoring](https://docs.byteplus.com/en/docs/redis/event-monitoring) |✔️ |✔️ |✔️ |✔️ |

## Backup and recovery

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Modifying automatic backup strategy](https://docs.byteplus.com/en/docs/redis/automatic-backup) |✔️ |✔️ |❌ |❌ |
|[Modifying automatic backup settings in batches](https://docs.byteplus.com/en/docs/redis/batch-modify-automatic-backup) |✔️ |✔️ |❌ |❌ |
|[Modifying data flashback strategy](https://docs.byteplus.com/en/docs/redis/set-data-flashback) |✔️ |✔️ |❌ |❌ |
|[Manual backup](https://docs.byteplus.com/en/docs/redis/manual-backup) |✔️ |✔️ |❌ |❌ |
|[Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup) |✔️ |✔️ |❌ |❌ |
|[Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files) |✔️ |✔️ |❌ |❌ |
|[Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name) |✔️ |✔️ |❌ |❌ |
|[Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set) |✔️ |✔️ |❌ |❌ |
|[Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point) |✔️ |✔️ |❌ |❌ |
|[Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance) |✔️ |✔️ |❌ |❌ |

## Parameter management

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter) |✔️ |✔️ |✔️ |✔️ |
|[Viewing parameter modification history](https://docs.byteplus.com/en/docs/redis/view-parameter-modification-history) |✔️ |✔️ |✔️ |✔️ |
|[Creating parameter template](https://docs.byteplus.com/en/docs/redis/create-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Applying parameter template](https://docs.byteplus.com/en/docs/redis/apply-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Applying parameter template in batches](https://docs.byteplus.com/en/docs/redis/batch-apply-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Editing parameter template](https://docs.byteplus.com/en/docs/redis/edit-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Copying parameter template](https://docs.byteplus.com/en/docs/redis/copy-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Exporting as parameter template](https://docs.byteplus.com/en/docs/redis/export-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Exporting parameter list from parameter template](https://docs.byteplus.com/en/docs/redis/export-parameter-list-from-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Deleting parameter template](https://docs.byteplus.com/en/docs/redis/delete-parameter-template) |✔️ |✔️ |✔️ |✔️ |
|[Adjusting frequency of Redis scheduled tasks](https://docs.byteplus.com/en/docs/redis/set-hz) |✔️ |✔️ |✔️ |✔️ |
|[Limiting output buffer size for publish-subscribe client](https://docs.byteplus.com/en/docs/redis/set-client-output-buffer-pubsub) |✔️ |✔️ |✔️ |✔️ |
|[Adjusting slow log parameters](https://docs.byteplus.com/en/docs/redis/adjust-slow-log-parameters) |✔️ |✔️ |✔️ |✔️ |
|[Setting key eviction policy](https://docs.byteplus.com/en/docs/redis/set-maxmemory-policy) |✔️ |✔️ |✔️ |✔️ |

## Event management

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Viewing planned event](https://docs.byteplus.com/en/docs/redis/manage-planned-event) |✔️ |✔️ |✔️ |✔️ |
|[Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time) |✔️ |✔️ |✔️ |✔️ |
|[Executing planned event](https://docs.byteplus.com/en/docs/redis/execute-planned-event) |✔️ |✔️ |✔️ |✔️ |
|[Canceling planned event](https://docs.byteplus.com/en/docs/redis/cancel-planned-event) |✔️ |✔️ |✔️ |✔️ |

## Performance analysis

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) |✔️ |✔️ |✔️ |✔️ |
|[Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis) |✔️ |✔️ |✔️ |✔️ |
|[Creating RDB analysis task](https://docs.byteplus.com/en/docs/redis/create-rdb-analysis-task) |✔️ |✔️ |❌ |❌ |
|[Viewing RDB analysis task](https://docs.byteplus.com/en/docs/redis/view-rdb-analysis-task) |✔️ |✔️ |❌ |❌ |
|[Deleting RDB analysis task](https://docs.byteplus.com/en/docs/redis/delete-rdb-analysis-task) |✔️ |✔️ |❌ |❌ |
|[Instance sessions](https://docs.byteplus.com/en/docs/redis/instance-session) |✔️ |✔️ |✔️ |✔️ |
|[Clearing expired key](https://docs.byteplus.com/en/docs/redis/clear_expired_key) |✔️ |✔️ |✔️ |✔️ |
|[Canceling expired key clear task](https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task) |✔️ |✔️ |✔️ |✔️ |
|[Slot distribution view](https://docs.byteplus.com/en/docs/redis/Slot_distribution_view) |✔️ |✔️ |✔️ |✔️ |

## Log management

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Querying slow log](https://docs.byteplus.com/en/docs/redis/query-slow-log) |✔️ |✔️ |✔️ |✔️ |
|[Exporting slow log](https://docs.byteplus.com/en/docs/redis/export-slow-log) |✔️ |✔️ |✔️ |✔️ |
|[Querying fatlog](https://docs.byteplus.com/en/docs/redis/query-fat-log) |✔️ |✔️ |✔️ |✔️ |
|[Exporting fatlog](https://docs.byteplus.com/en/docs/redis/export-fat-log) |✔️ |✔️ |✔️ |✔️ |

## Kernel features

|Feature |Type of instance architecture ||||
|---|---|---|---|---|
||Primary\-secondary instance ||Single\-node instance ||
||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting) |✔️ |✔️ |❌ |❌ |
|[Setting read local node only](https://docs.byteplus.com/en/docs/redis/read-local-node-only) |✔️ |✔️ |❌ |❌ |
|[Configuring password-free command execution in Sentinel mode](https://docs.byteplus.com/en/docs/redis/password-free_execution_in_sentinel_mode) |✔️ |✔️ |✔️ |✔️ |
