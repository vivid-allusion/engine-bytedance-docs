---
title: "IAM overview"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Permission-overview"
---

Identity and Access Management (IAM) is a free permission management service provided by the platform for customers. It is used to control the access permissions of different identities on cloud resources. This enables decentralized resource management, improves management efficiency, and reduces information leakage risks. Before you manage the resources of Vital Managed Service for Prometheus (VMP) by using an Identity and Access Management (IAM) user, you need to attach a policy to the IAM user.

<span id="rCYTcfTV"></span>
## Reasons for using IAM

Before using cloud resources, you need to first [create an account](https://docs.byteplus.com/en/docs/6261/64925). After the account is created, you will obtain an account, which is the "root user". **The root user has full management permissions on all resources within the account by default**.

The following issues may arise when you only use the root user to manage resources:


* Multiple people share the root user for operations, making it impossible to distinguish individual users.

* The root user has broad permissions, which can cause a severe impact if leaked.

* Using the root user for O&M operations poses high risks.


IAM helps avoid the preceding issues. You can create IAM users, user groups, and roles within the root user. Newly created IAM users, user groups, and roles have no permissions by default. You can grant appropriate permissions as needed, enabling multi‑identity management and fine‑grained permission control. For more features, see [Product introduction](https://docs.byteplus.com/en/docs/6257/64959).

<span id="tZAl9Vy6"></span>
## Introduction to IAM


|Introduction |Description |Related document |
|---|---|---|
|IAM\-related concepts |Permission management with IAM involves many technical terms, such as IAM identities (users, user groups, and roles), policies, and single sign\-on (SSO). |[Basic concepts](https://docs.byteplus.com/en/docs/6257/64963) |
|IAM constraints |IAM resources are subject to quotas. If the quota is exceeded, new resources cannot be created. |[Limits](https://docs.byteplus.com/en/docs/6257/1285191) |
|IAM usage process |You can directly attach policies to IAM users or grant permissions by adding IAM users to user groups. |* [Create a user and grant permissions](https://docs.byteplus.com/en/docs/6257/94013)<br><br>* [Grant permissions to a user to manage API access keys](https://docs.byteplus.com/en/docs/6257/1319865) |
|IAM policy overview |A policy is a set of permissions described using a specific syntax structure.<br><br><br>* Policy types: IAM supports **system preset policies** and **custom policies**.<br><br>* Policy syntax: IAM policies have a fixed syntax structure. You can create richer and more diverse policies as needed.<br><br>* Policy effective scope: IAM policies can take effect at the **global level** or the **project level**. |* [IAM policy syntax](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [System preset policies](https://docs.byteplus.com/en/docs/vmp/Permission-overview?TagIDs=2,143&lang=en#f4x7e18O) |


<span id="f4x7e18O"></span>
## System preset policies

VMP provides six preset policies listed in the following table for you to directly authorize IAM users.


|**Policy** |**Description** |Project\-level authorization |
|---|---|---|
|VMPFullAccess |The VMP full management permission. |Supported |
|VMPReadOnlyAccess |The VMP read\-only access permission. |Supported |
|VMPRemoteWriteAccess |The VMP data write permission. |Supported |
|VMPQueryAccess |The VMP data query permission. |Supported |
|VMPCommonFullAccess |Read and write access to generic VMP resources. |Not supported |
|VMPCommonReadonlyAccess |Read\-only access to generic VMP resources. |Not supported |


<span id="D6m9Zud1"></span>
##
