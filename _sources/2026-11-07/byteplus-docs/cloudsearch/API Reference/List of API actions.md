---
title: "List of API actions"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/List-API"
---

This topic introduces the API actions available for Cloud Search.

<span id="实例信息"></span>
## Instance information


|**Action** |**Description** |
|---|---|
|[DescribeZones](https://docs.byteplus.com/en/docs/cloudsearch/DescribeZones) |Call DescribeZones to query the Availability Zones where Cloud Search is available in a specified Region. |
|[DescribeInstance](https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstance) |Call DescribeInstance to query the configuration details of a specified instance. |
|[DescribeInstances](https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstances) |Call DescribeInstances to query Cloud Search instances and their configuration details. |
|[DescribeInstanceNodes](https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstanceNodes) |Call DescribeInstanceNodes to query detailed information on member nodes of a specified instance, such as the node type, running status, and resource configurations. |
|[DescribeInstancePlugins](https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstancePlugins) |Call DescribeInstancePlugins to query the plug\-ins that are installed on a specified instance. |
|[DescribeNodeAvailableSpecs](https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecs) |Call DescribeNodeAvailableSpecs to query the available node types, instance types, and storage specifications as well as the billing configuration code. |


<span id="实例管理"></span>
## Instance management


|**Action** |**Description** |
|---|---|
|[CreateInstance](https://docs.byteplus.com/en/docs/cloudsearch/CreateInstance) |Call CreateInstance to create an instance. When you call this action, you must also confirm the order information on BytePlus in the browser to start the instance creation. |
|[CreateInstanceInOneStep](https://docs.byteplus.com/en/docs/cloudsearch/CreateInstanceInOneStep) |Call CreateInstanceInOneStep to create an instance in one step. |
|[RenameInstance](https://docs.byteplus.com/en/docs/cloudsearch/RenameInstance) |Call RenameInstance to rename an instance. |
|[ReleaseInstance](https://docs.byteplus.com/en/docs/cloudsearch/ReleaseInstance) |Call ReleaseInstance to delete or release an instance. |
|[RestartInstance](https://docs.byteplus.com/en/docs/cloudsearch/RestartInstance) |Call RestartInstance to restart all member nodes in an instance. |
|[RestartNode](https://docs.byteplus.com/en/docs/cloudsearch/RestartNode) |Call RestartNode to restart a specified member node in an instance. |
|[ResetAdminPassword](https://docs.byteplus.com/en/docs/cloudsearch/ResetAdminPassword) |Call ResetAdminPassword to reset the password of the administrator account (admin) for an instance. |
|[ModifyMaintenanceSetting](https://docs.byteplus.com/en/docs/cloudsearch/ModifyMaintenanceSetting) |Call ModifyMaintenanceSetting to change the maintenance window and days for an instance. |
|[ModifyDeletionProtection](https://docs.byteplus.com/en/docs/cloudsearch/ModifyDeletionProtection) |Call ModifyDeletionProtection to enable or disable the deletion protection feature for an instance. |
|[ModifyNodeSpecInOneStep](https://docs.byteplus.com/en/docs/cloudsearch/ModifyNodeSpecInOneStep) |Call ModifyNodeSpecInOneStep to upgrade or downgrade the node configurations of an instance in one step. |
|[ModifyIpAllowlist](https://docs.byteplus.com/en/docs/cloudsearch/ModifyIpAllowlist) |Call ModifyIpAllowlist to configure an IP allowlist for accessing an instance or Kibana. |
|[ModifyChargeCode](https://docs.byteplus.com/en/docs/cloudsearch/ModifyChargeCode) |Call ModifyChargeCode to change the billing method of an instance from pay\-as\-you\-go to subscription. |
