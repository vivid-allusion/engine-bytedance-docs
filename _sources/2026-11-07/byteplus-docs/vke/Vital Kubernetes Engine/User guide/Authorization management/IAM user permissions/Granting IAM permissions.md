---
title: "Granting IAM permissions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions"
---

Before you use IAM users to manage VKE resources, you need to attach policies to IAM users. You can attach system preset policies and user\-defined policies to IAM identities, including IAM users, IAM user groups, and IAM roles.

This topic provides an example of how to grant permissions to IAM users. The permissions configuration methods for other IAM identities are similar.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

IAM users have been created.  For detailed operations, see [User management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

<span id=".5YWz6IGU57O757uf6aKE6K6-562W55Wl"></span>
## Attaching system\-preset policies

IAM provides system\-preset policies. You can directly attach system preset policies related to VKE to IAM users.


1. Log in to the [IAM console.](https://console.byteplus.com/iam)

2. In the left navigation bar, click **User management** \> **User**.

3. On the User page, find the name of the user to whom you want to grant permissions and click **Authorize** in the **Actions** column.

5. On the **Add authorization** page, select **vke** from the **Service** drop\-down list in the **Policy** section. For the descriptions of the system preset policies related to VKE, see [System preset policies](https://docs.byteplus.com/en/docs/vke/Authorization-overview).

6. You can select the checkboxes before the policy names based on your business requirements and then click **Submit** to attach permission policies for VKE resources to the IAM user.


<span id=".5YWz6IGU55So5oi36Ieq5a6a5LmJ562W55Wl"></span>
## Attaching user\-defined policies

If the system preset policies related to VKE do not meet your authorization requirements, you can create custom policies and attach them to target users, user groups, or roles.  For related operations, see [Creating policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy) and [IAM authorization best practices](https://docs.byteplus.com/en/docs/vke/IAM-based-authorization-best-practices).

For the VKE resource actions that can be included in a custom policy, see [Actions](https://docs.byteplus.com/en/docs/vke/Authorization-overview). For access permissions on cloud service resources required by VKE, see [Introduction to the VKE service-linked role](https://docs.byteplus.com/en/docs/vke/Service-linked-roles-for-Vital-Kubernetes-Engine). For VKE\-related conditions, see [Service-specific condition keys and custom policies](https://docs.byteplus.com/en/docs/vke/Service_condition_keywords_and_custom_policies).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Custom ‌IAM policies do not automatically update with product API changes. When the service adds, modifies, or deprecates APIs or Actions, you need to evaluate and update custom policies manually. Otherwise, the following issues may occur:</div>



* <div data-tips="true" data-tips-type="warning">Feature unavailability (new Actions are not added to the policy, resulting in authorization failure)</div>


* <div data-tips="true" data-tips-type="warning">Permission redundancy (deprecated Actions are not removed promptly, resulting in unnecessary permissions)</div>
