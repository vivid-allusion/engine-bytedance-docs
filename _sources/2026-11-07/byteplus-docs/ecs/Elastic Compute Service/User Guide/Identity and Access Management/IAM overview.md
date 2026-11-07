---
title: "IAM overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-3"
---

Identity and Access Management (IAM) is a free service that the platform provides to users. It is a permission management system that controls access to cloud resources by different identities, enables delegated permission management, improves management efficiency, and reduces the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

To use cloud resources, you need to first [register an account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). After registration, you obtain an account that is referred to as "Root Account". **By default, the root user has full administrative permissions over all resources under it.** 

Using only the root account to manage resources may cause the following issues:


* Multiple users use the same root user, and you cannot identify the actual user.

* The root account has extensive permissions, so any leak would have severe consequences.

* Using the root account directly for O&M tasks involves higher risks.


You can avoid the above issues by using IAM features. You can create IAM users, user groups, and roles under the root account. New IAM users, user groups, and roles have no permissions initially. You can grant them appropriate permissions based on actual needs to achieve multi\-identity management and granular permission control. For more features, refer to [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

<span id=".SUFN55u45YWz5LuL57uN"></span>
## IAM\-related information


|Introduction |Detailed description |Related documents |
|---|---|---|
|IAM usage process |IAM user: You can authorize IAM users directly or authorize them by adding them to a user group. |[Creating users and authorizing them](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) |
||IAM role: You can associate the ECS service role with an instance to obtain temporary access credentials for other cloud resources. |[Authorizing ECS to access other cloud resources based on instance IAM roles](https://docs.byteplus.com/en/docs/ecs/Authorize_ECS_to_access_other_cloud_resources_based_on_instance_IAM_roles) |
|IAM policy overview |A policy is a set of permissions described using a syntax structure.<br><br><br>* Policy type: IAM supports two types of policies: **system default policies** and **custom policies**.<br><br>* Policy syntax structure: IAM policies follow a fixed syntax format, allowing you to create diversified and customized IAM policies as needed.<br><br>* Policy scope: IAM policies support two scopes: **global permissions** and **project\-level permissions**. |* [IAM policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax)<br><br>* [ECS IAM policy types](https://docs.byteplus.com/en/docs/ecs/Accessing-resources-with-Identity-and-Access-Management) |
