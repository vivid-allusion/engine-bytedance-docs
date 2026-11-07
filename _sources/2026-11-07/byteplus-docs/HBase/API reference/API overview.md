---
title: "API overview"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/API_overview"
---

This document lists the APIs provided by Table Storage for HBase.

<span id=".5Zyw5Z-f5ZKM5Y-v55So5Yy6"></span>
## Regions and Zones


|API |Note |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/HBase/DescribeRegions) |Call the DescribeRegions API to query information about available regions for HBase. |
|[DescribeZones](https://docs.byteplus.com/en/docs/HBase/DescribeZones) |Call the DescribeZones API to query information about availability zone resources for HBase in a specified region. |


<span id=".5a6e5L6L566h55CG"></span>
## Instance Management


|API |Description |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/HBase/CreateDBInstance) |Call the CreateDBInstance API to create an HBase instance. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances) |Call the DescribeDBInstances API to retrieve the list of HBase instances. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/HBase/DescribeDBInstanceDetail) |Call the DescribeDBInstanceDetail API to query the details of a specified instance. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/HBase/RestartDBInstance) |Call the RestartDBInstance API to restart a specified instance. |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceName) |Use the ModifyDBInstanceName API to change an instance name. |
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/HBase/DeleteDBInstance) |Call the DeleteDBInstance API to delete a specified instance. |
|[ModifyInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/HBase/ModifyInstanceDeletionProtectionPolicy) |Call the ModifyInstanceDeletionProtectionPolicy API to enable or disable instance deletion protection. |
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/HBase/ModifyInstanceChargeType) |Use the ModifyInstanceChargeType API to change the billing method of an instance from pay\-as\-you\-go to subscription. |


<span id=".5Y-Y5pu05a6e5L6L6YWN572u"></span>
## Modify Instance Configuration


|API |Note |
|---|---|
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceSpec) |Call the ModifyDBInstanceSpec API to modify the specifications of a specified instance. |
|[ModifyRSNodeCount](https://docs.byteplus.com/en/docs/HBase/ModifyRSNodeCount) |Call the ModifyRSNodeCount API to modify the number of RegionServer nodes for an instance. |
|[ModifyDBInstanceStorageCapacity](https://docs.byteplus.com/en/docs/HBase/ModifyDBInstanceStorageCapacity) |Call the ModifyDBInstanceStorageCapacity API to modify the storage capacity of an instance. |


<span id=".5qCH562-566h55CG"></span>
## Tag Management


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/HBase/AddTagsToResource) |Call the AddTagsToResource API to add tags to a specified instance. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/HBase/RemoveTagsFromResource) |Call the RemoveTagsFromResource API to unbind tags from a specified instance. |
|[DescribeTagsByResource](https://docs.byteplus.com/en/docs/HBase/DescribeTagsByResource) |Call the DescribeTagsByResource API to retrieve information about tags bound to an instance. |


<span id=".6L-e5o6l566h55CG"></span>
## Connectivity


|API |Description |
|---|---|
|[StartThrift2](https://docs.byteplus.com/en/docs/HBase/StartThrift2) |Call the StartThrift2 API to request the private network connection address of Thrift2 for the specified instance. |
|[StopThrift2](https://docs.byteplus.com/en/docs/HBase/StopThrift2) |Call the StopThrift2 API to delete the Thrift2 private endpoint of a specified instance. |
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/HBase/CreateDBEndpoint) |Call the CreateDBEndpoint API to enable public access for a specified connection address. |
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/HBase/DeleteDBEndpoint) |Call the DeleteDBEndpoint API to disable public access for a specified endpoint. |


<span id=".6LSm5Y-3566h55CG"></span>
## Accounts


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/HBase/CreateDBAccount) |Call the CreateDBAccount API to create a database account for an HBase instance. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/HBase/DescribeDBAccounts) |Call the DescribeDBAccounts API to retrieve the database account information of an HBase instance. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/HBase/ResetDBAccount) |Call the ResetDBAccount API to modify the database account password for an HBase instance. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/HBase/DeleteDBAccount) |Call the DeleteDBAccount API to delete a database account of an HBase instance. |


<span id=".55m95ZCN5Y2V566h55CG"></span>
## Allowlist Management


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/HBase/CreateAllowList) |Call the CreateAllowList API to create a new IP allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists) |Call the DescribeAllowLists API to retrieve all IP allowlist information for the current account in a specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/HBase/DescribeAllowListDetail) |Call the DescribeAllowListDetail API to query the details of a specified allowlist, including IP addresses and associated instance details. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/HBase/ModifyAllowList) |Call the ModifyAllowList API to modify the information of a specified allowlist, such as its name and IP addresses. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/HBase/AssociateAllowList) |Call the AssociateAllowList API to associate a target instance with a specified allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/HBase/DisassociateAllowList) |Call the DisassociateAllowList API to disassociate a target instance from a specified allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/HBase/DeleteAllowList) |Call the DeleteAllowList API to delete the specified allowlist. |
