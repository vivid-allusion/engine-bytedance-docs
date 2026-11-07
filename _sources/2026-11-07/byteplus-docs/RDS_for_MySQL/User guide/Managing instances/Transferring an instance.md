---
title: "Transferring an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Transfering_instance"
---

This topic describes how to transfer an instance between accounts.

<span id="Z4hogdcG"></span>
## Background

It is common to assign resources to different business entities at various business stages. RDS for MySQL allows you to transfer an instance from one account to another without changing its ownership, ensuring business continuity and management flexibility.

<span id="lA7GIE6O"></span>
## Use cases

Only enterprise\-certified accounts can use the resource transfer feature. The initiating and receiving accounts must be certified under the same entity. Individually certified accounts do not support resource transfer. They can neither initiate a transfer nor receive transferred resources.

<span id="GLwFEdUY"></span>
## Limitation


* This function is currently in invitation\-only testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

* MySQL 8.4 instances do not support transferring an instance.


<span id="qs5pzE8y"></span>
## Rules

When a resource transfer is initiated, the system validates the initiating and receiving accounts, as well as the instance to be transferred. The following table describes the specific validation rules.


* Account validation rules


For details about account validation rules, refer to [Resource transfer rules](https://docs.byteplus.com/en/docs/byteplus-platform/Resource_Transfer?lang=en#qnCtE39S).


* Instance validation rules

   * The instance state must be **Running**.

   * The instance must be configured with a virtual private cloud and a subnet in an **Available** state. Refer to [Modifying instance network configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_instance_network_configuration) to make necessary adjustments to the instance network configuration. The account that receives the transferred resources must have an available virtual private cloud and subnet for the instance to be transferred.

   * Public network access for the instance is disabled. Refer to [Enabling or disabling public network access](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access) to configure public network access for the instance.

   * The instance is not connected via PrivateLink.

   * No blue\-green deployment has been created for the instance. Refer to [Deleting a blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Delete_a_blue-green_deployment) to configure blue\-green deployment for the instance.

   * No disaster recovery deployment has been created for the instance. Refer to [Switching a disaster recovery instance to a primary instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Switching_a_disaster_recovery_instance_to_a_primary_instance) to configure disaster recovery deployment for the instance.

   * Transparent data encryption is disabled for the instance. Refer to [Configuring TDE](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_tde) to configure transparent data encryption for the instance.

   * The instance is not in a temporary upgrade period. Refer to [Temporary upgrade](https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade?lang=en#.5rOo5oSP5LqL6aG5) to adjust the temporary upgrade of the instance.

   * The instance has no pending operation and maintenance events. Refer to [Executing an operation and maintenance event in advance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Executing_an_operation_and_maintenance_event_in_advance) to run the events for the instance ahead of schedule.


<span id="VkoapuZy"></span>
## Precautions

After an instance is transferred, the following instance configurations change:


* Connection diagnosis result: Diagnosis information for private network connections is cleared.

* Affiliated project: The instance is assigned to the **default** (default project).

* Tags: The associated tags are removed.

* Monitoring policy for the instance: If a monitoring policy is configured for the instance in Database Workshop, you need to reconfigure it in Database Workshop after the resource transfer.


<span id="W7wj5cku"></span>
## Risks and procedures

For details about the risks and procedures of resource transfer, refer to [Resource transfer](https://docs.byteplus.com/en/docs/byteplus-platform/Resource_Transfer?lang=en).
