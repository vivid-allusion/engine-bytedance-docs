---
title: "Overview"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/terraform_overview"
---

Cache for Redis supports creating, managing, and maintaining related resources through Terraform tools. This topic describes Terraform's support for managing Redis resources.

<span id="cLzZ524M"></span>
## Terraform introduction

Terraform is an open\-source IT infrastructure orchestration tool that supports the use of configuration files to define infrastructure or applications. With Terraform, you can easily orchestrate BytePlus cloud resources, such as creating, managing, and maintaining them, and performing version control on them. For more details, refer to [What is Terraform](https://docs.byteplus.com/en/docs/tf/What-is-Terraform).

<span id="UhtAeYgi"></span>
## Redis resources supported by Terraform

Cache for Redis supports managing the following resources through Terraform.


<Tabs>
<Tab zoneid="H1QZUJSjtl" title="Resource">
<TabTitle>Resource</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/tf/Configuration-guide">Resource</a> is the most important element in Teraform, declared with the keyword <code>resource</code>.</div>



|Resource item |Description |
|---|---|
|[byteplus_redis_instance](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_instance) |Instance lifecycle management, such as creating and deleting instances, changing instance specification configurations, modifying instance names, parameters, billing methods, tag information, etc. |
|[byteplus_redis_instance_state](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_instance_state) |Instance status management, mainly used for restarting instances. |
|[byteplus_redis_allow_list](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_allow_list) |Allowlist management, such as creating, modifying, and deleting allowlists. |
|[byteplus_redis_allow_list_associate](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_allow_list_associate) |Allowlist association management, such as associating and disassociating instances with allowlists. |
|[byteplus_redis_backup](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_backup) |Data backup management, such as creating and downloading backups, modifying backup policies. |
|[byteplus_redis_continuous_backup](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_continuous_backup) |Data flashback function management, mainly used for enabling or disabling the data flashback function. |
|[byteplus_redis_backup_restore](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_backup_restore) |Data recovery management, mainly used for restoring data from backup sets to the original Redis instance. |
|[byteplus_redis_account](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_account) |Account management, such as creating, modifying, and deleting accounts. |
|[byteplus_redis_endpoint](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_endpoint) |Connection address management, such as creating and deleting connection addresses, enabling or disabling password\-free access. |
|[byteplus_redis_parameter_group](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_parameter_group) |Parameter template management, such as creating, modifying, and deleting parameter templates. |





</Tab>
<Tab zoneid="nmK8EvDK1A" title="Data Sources">
<TabTitle>Data Sources</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/tf/Data-Sources">Data Source</a> is a special resource, used to query the properties and information of existing resources, declared by keyword <code>data</code>.</div>



|Resource item |Description |
|---|---|
|[byteplus_redis_regions](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_regions) |Query the list of regions that support Redis cloud services. |
|[byteplus_redis_zones](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_zones) |Query the list of availability zones in a specified region. |
|[byteplus_redis_instance_specs](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_instance_specs) |Query the list of Redis instance specifications. |
|[byteplus_redis_instances](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_instances) |Query the list of instances or the detailed information of a specified instance. |
|[byteplus_redis_allow_lists](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_allow_lists) |Query the list of allowlists or the list of allowlists associated with a specified instance. |
|[byteplus_redis_backups](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_backups) |Query information such as the backup list, backup policy, and backup download address of a specified instance. |
|[byteplus_redis_pitr_time_periods](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_pitr_time_periods) |Query the supported recoverable time period when restoring data by point\-in\-time for a specified instance. |
|[byteplus_redis_accounts](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_accounts) |Query the list of accounts of a specified instance. |
|[byteplus_redis_planned_events](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_planned_events) |Query the list of scheduled events of a specified instance. |
|[byteplus_redis_big_keys](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_big_keys) |Query the list of big keys of a specified instance. |
|[byteplus_redis_parameter_groups](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/redis_parameter_groups) |Query the list of parameter templates of a specified instance. |





</Tab>
</Tabs>
