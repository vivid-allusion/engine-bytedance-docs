---
title: "Instance edition"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Instance_type"
---

  CR provides both Standard Edition and Micro Edition specifications. You can select the appropriate instance type based on business scale, performance requirements, and usage scenarios.

&nbsp;


|**Instance edition** |**Role** |**Application scenario** |
|---|---|---|
|Standard Edition Standard instance |A full\-featured managed image service for enterprise\-level production environments, providing exclusive data storage, exclusive Registry services, and comprehensive security management capabilities. |Medium and large enterprises, multi\-team collaboration, large\-scale container cluster image distribution, and production environments with strict performance and SLA requirements. |
|Micro Edition Standard instance |A lightweight image hosting service for micro enterprises and individual developers, providing basic image push and pull capabilities. |Scenarios for individual developers, startup teams, development and test environments, and cost\-sensitive scenarios with small image volumes. |


<span id="qhMQ9nxB"></span>
## Feature comparison

For specific quota limits of each instance type (such as the number of namespaces, number of OCI artifact repositories, concurrent push/pull QPS, and more), see [product features](https://docs.byteplus.com/en/docs/cr/features?lang=en).

<span id="oILLvjSF"></span>
## Instance upgrade path

CR supports upgrading from Micro Edition to Standard Edition to meet performance expansion needs after business growth.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Instance upgrade is an irreversible action; Standard Edition cannot be downgraded to Micro Edition.</div>


* <div data-tips="true" data-tips-type="warning">There will be a brief service interruption during the upgrade process (typically lasting several minutes), so it is recommended to perform the upgrade during off\-peak business hours.</div>




|**Upgrade path** |**Data processing** |**Description** |
|---|---|---|
|Standard instance (Micro Edition) → Standard instance (Standard Edition) |Automatic data migration. |After upgrading, obtain dedicated resources, VPC access, P2P acceleration, and other enterprise\-level capabilities. Image data is automatically retained. For details, see [Upgrade Micro Edition instance to Standard Edition instance](https://docs.byteplus.com/en/docs/cr/Upgrade_a_Micro_Edition_instance_to_a_Standard_Edition_instance). |
