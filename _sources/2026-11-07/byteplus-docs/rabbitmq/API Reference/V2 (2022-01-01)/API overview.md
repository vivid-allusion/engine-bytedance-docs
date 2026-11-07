---
title: "API overview"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/API_overview"
---

<span id="3b8441d9"></span>
## Resource check


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/rabbitmq/DescribeRegions_-_Query_available_Region_list) |Call the DescribeRegions API to view the list of Regions. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/rabbitmq/DescribeAvailabilityZones_-_View_the_availability_zone_list) |Call the DescribeAvailabilityZones interface to view the list of availability zones. |


<span id="60005359"></span>
## Instance lifecycle


|API |Description |
|---|---|
|[CreateInstance](https://docs.byteplus.com/en/docs/rabbitmq/Create_Instance_-_Create_instance) |Call CreateInstance to create a Message Queue for RabbitMQ instance. |
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/rabbitmq/ModifyInstanceSpec_-_Modify_instance_specification) |Call the ModifyInstanceSpec API to change the instance's computing specs, storage specification, and partition upgrades. |
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/rabbitmq/ModifyInstanceChargeType_-_change_billing_method) |Call the ModifyInstanceChargeType API to change the instance billing method. |
|[DeleteInstance](https://docs.byteplus.com/en/docs/rabbitmq/DeleteInstance_-_Delete_instance) |Call DeleteInstance to release the pay\-as\-you\-go instance. |


<span id="e99c2adf"></span>
## Instance management


|API |Description |
|---|---|
|[DescribeInstances](https://docs.byteplus.com/en/docs/rabbitmq/DescribeInstances_-_Get_the_current_instances_list) |Call the DescribeInstances API to get the instances list under the current account. |
|[DescribeInstanceDetail](https://docs.byteplus.com/en/docs/rabbitmq/DescribeInstanceDetail_-_Query_instance_details) |Call the DescribeInstanceDetail API to view the details of the specified instance. |
|[ModifyInstanceAttributes](https://docs.byteplus.com/en/docs/rabbitmq/ModifyInstanceAttributes_-_Modify_instance_information) |Call the ModifyInstanceAttributes API to modify the instance name, description, and other instance information. |
|[ModifyUserPassword](https://docs.byteplus.com/en/docs/rabbitmq/ModifyUserPassword_-_Modify_Username_and_Password) |Call ModifyUserPassword to reset the administrator password for RabbitMQ instance Web UI. |
|[RestartInstance](https://docs.byteplus.com/en/docs/rabbitmq/RestartInstance_-_Restart_instance) |Call the RestartInstance API to restart the instance. |


<span id="01a24bc1"></span>
## Network management


|API |Description |
|---|---|
|[CreatePublicAddress](https://docs.byteplus.com/en/docs/rabbitmq/CreatePublicAddress_-_Enable_public_network_access) |Call the CreatePublicAddress API to enable public network access for the RabbitMQ instance. |
|[DeletePublicAddress](https://docs.byteplus.com/en/docs/rabbitmq/DeletePublicAddress_-_Disable_public_network_access) |Call the DeletePublicAddress API to disable public network access for the RabbitMQ instance. |


<span id="0d46345e"></span>
## Extension management


|API |Description |
|---|---|
|[DescribePlugins](https://docs.byteplus.com/en/docs/rabbitmq/DescribePlugins_-_Query_instance_extension_status) |Call the DescribePlugins interface to query the list of extensions for a specified instance. |
|[ModifyPlugin](https://docs.byteplus.com/en/docs/rabbitmq/ModifyPlugin_-_modify_extension_instance_status) |Call the ModifyPlugin interface to enable or disable an extension. |


<span id="c5a4d15f"></span>
## Tag management


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/rabbitmq/AddTagsToResource_-_Add_instance_tags) |Call the AddTagsToResource API to add user tags to one or more resources. |
|[DescribeTagsByResource](https://docs.byteplus.com/en/docs/rabbitmq/DescribeTagsByResource_-_Batch_query_instance_tags) |Call the DescribeTagsByResource API to query resources with bound tags. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/rabbitmq/RemoveTagsFromResource_-_Unbind_instance_tags) |Call the RemoveTagsFromResource API to remove user tags from one or more resources. |
