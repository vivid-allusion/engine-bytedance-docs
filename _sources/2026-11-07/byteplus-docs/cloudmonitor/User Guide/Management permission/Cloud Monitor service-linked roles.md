---
title: "Cloud Monitor service-linked roles"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Cloud_Monitor_service-linked_roles"
---

In some scenarios, Cloud Monitor must access other cloud services. These permissions are granted through service\-associated roles.

<span id="033d96b0"></span>
## Application scenarios


* When Cloud Monitor automatically installs the host monitoring add\-on, access permissions on Elastic Compute Service (ECS) need to be obtained through a service\-associated role.

* When you use the log monitoring feature, you need to grant read permissions on Torch Log Service (TLS) by using a service\-associated role.

* When you use the alerting feature of Cloud Monitor, you need to grant query permissions on other cloud service instances by using a service\-associated role.


<span id="0066b186"></span>
## Permission description

The following table describes the permissions of Cloud Monitor service\-associated roles.


|Role Name |Role Description |
|---|---|
|ServiceRoleForCM |The role is used by Cloud Monitor to access the resources of other cloud services. |
|ServiceRolePolicyForVolcECS |This role provides the cross\-service association policy between Cloud Monitor and ECS. |
