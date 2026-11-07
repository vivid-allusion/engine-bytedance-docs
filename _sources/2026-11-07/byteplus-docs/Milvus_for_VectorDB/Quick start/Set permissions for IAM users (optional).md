---
title: "Set permissions for IAM users (optional)"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Set_permissions_for_IAM_users_optional"
---

Each root account can create multiple IAM users and assign different permissions to each, managing access to cloud resources for different identities under the account. This topic describes how to authorize IAM users to use Milvus for VectorDB.

<span id="HuoaJoA3"></span>
## Applicable scenarios

**Independent resource management scenarios**: You can create different IAM users for different businesses, and access resources belonging to each business through these IAM users.

**Security scenarios**: You can use the AK and SK of IAM users to call OpenAPIs, preventing the risk of leaking the AK and SK of the root user.

<span id="UBSugo8K"></span>
## Background

<span id="ypjjLg1k"></span>
### Policies

A policy describes permissions. IAM users, user groups, or roles must be granted permissions through associated policies. For IAM users using Milvus, system preset policies or user\-defined policies can be added as needed.


* System preset policy

   
   |**Related service** |**Policy name** |**Policy type** |**Description** |
   |---|---|---|---|
   |Milvus for VectorDB |MilvusFullAccess |System preset policy |Full management access to Milvus for VectorDB. After you add this permission, users have<br><br>read and write permissions for Milvus for VectorDB within the policy scope, such as creating, deleting, and modifying instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If users only have this permission, they cannot use Milvus instances to their full functionality. To use VPC features, you need VPCFullAccess or VPCReadOnlyAccess permissions. To use alerts and monitoring, you need CloudMonitorFullAccess or CloudMonitorReadOnlyAccess permissions.</div><br> |
   ||MilvusReadOnlyAccess |System preset policy |Read\-only access to Milvus for VectorDB. After you add this permission, users can view Milvus instances within the policy scope. |
   |VPC |VPCFullAccess |System preset policy |Full management permissions for the VPC. After you add this permission, users can read and write VPCs within the policy scope, such as creating VPCs and associating Milvus instances with VPCs or subnets. |
   ||VPCReadOnlyAccess |System preset policy |Read\-only access to the VPC. After you add this permission, users can view the VPC and subnet information of the Milvus instances within the policy scope. |
   |CloudMonitor |CloudMonitorFullAccess |System preset policy |Full management permission for CloudMonitor. After you add this permission, users will have read and write access to monitoring alerts of the Milvus instances within the policy scope, such as viewing monitoring data and adding alarm policies for instances. |
   ||CloudMonitorReadOnlyAccess |System preset policy |Read\-only access permission for CloudMonitor. After you add this permission, users can view the monitoring data of Milvus instances within the policy's scope.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If an IAM user wants to view monitoring information, this permission must be added globally to the IAM user.</div><br> |
   

* User\-defined policies: In addition to authorizing IAM users with the system preset policies listed in the table above, you can also define more specific control policies through user\-defined policies.


<span id="qMl4IT5t"></span>
### Scope of application

After selecting a policy, you can assign its scope to the user as needed.


* **Global**: The permission policy applies to all projects within the account, including future projects.

* **Project**: The permission policy applies within the specified project.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The policies MilvusFullAccess and MilvusReadOnlyAccess for Milvus for VectorDB support only the <strong>Global</strong> scope configuration.</div>
