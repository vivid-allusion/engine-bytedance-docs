---
title: "API changelog"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/API_changelog"
---

This article summarizes the changes to the NDB for MySQL API.

<span id="v1（2022-01-01）"></span>
## v1（2022\-01\-01）

<span id="nBAaoX5N"></span>
### July 2026


|API |Release date |Change log |Related functions |
|---|---|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpoint) |July 30, 2026 |Added the request parameter `ConnectionPool`. |[Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool) |
|[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint) ||Added the request parameter `ConnectionPool`. ||
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint) ||Added the `ConnectionPool` parameter to the EndpointObject response parameter. ||
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) ||Added the `ConnectionPool` parameter to the EndpointObject response parameter. ||
|[ModifyConnectionPersistence](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyConnectionPersistence) ||Add an API. |[Connection persistence](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_persistence) |
|[CreateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateAllowList)<br><br> ||Add the request parameters `SecurityGroupBindInfos` and `UserAllowList`. |Added support for binding security groups to an allowlist. For details, refer to [Synchronizing security group](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Synchronizing_security_group). |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyAllowList) ||Add the request parameters `SecurityGroupBindInfos` and `UserAllowList`. ||
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowListDetail) ||Add the response parameters `SecurityGroupBindInfos` and `UserAllowList`. ||


<span id="IEpQpKnn"></span>
### June 2026


|API |Release date |Change log |Related functions |
|---|---|---|---|
|[ModifyDBInstanceStorageType](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceStorageType?_vtm_=a106466.b106468.0_0.0_0.0.18_7636664361964570175) |June 1, 2026 |New API.<br><br> |Added an intelligent compression storage type. For details, refer to [Product specification](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). |
|[CreateDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance) ||Added the request parameter `StorageType`.<br><br> ||
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) ||* Added the request parameter `StorageType`.<br><br>* Added the `StorageType` parameter to the `InstanceObject` structure in the response. ||
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) ||Added the `CompressedStorageUsedGiB` and `StorageType` parameters to the InstanceDetailObject structure in the response. ||
|[DescribeStoragePayablePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeStoragePayablePrice) ||Added the value `CompressClusterpool` to the request parameter StorageTypes.<br><br> ||
|[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstancePriceDetail)<br><br> ||Added the request parameter `StorageType`.<br><br> ||
|[DescribeExistDBInstancePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeExistDBInstancePrice)<br><br> ||* Added `ModifyDBInstanceStorageType` to the UserAction request parameter.<br><br>* Added the `StorageType` parameter to the InstanceInfo structure.<br><br><br> ||
|[RestoreToNewInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreToNewInstance) ||Added the `StorageType` request parameter. ||


<span id="3dOZA7ZX"></span>
### March 2026


|API |Release date |Change log |Related functions |
|---|---|---|---|
|[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyParameterTemplate) |March 23, 2026 |Added a new interface. |[Editing parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_parameter_template) |
|[CopyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CopyParameterTemplate) ||New API. |[Copying parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Copying_parameter_template) |


<span id="BdA1tn6A"></span>
###
