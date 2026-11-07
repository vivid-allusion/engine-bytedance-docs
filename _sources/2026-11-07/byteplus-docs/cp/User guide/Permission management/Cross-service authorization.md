---
title: "Cross-service authorization"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Cross-service_authorization"
---

Code Pipeline calls other BytePlus services through cross\-service authorization. To connect normally to other services required by BytePlus, you must complete cross\-service authorization. Create cross\-service authorization

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The following are scenarios that may currently involve cross\-service authorization:


* When pushing images to the image repository service, Code Pipeline must obtain permission for Actions on the image repository service.

* When integrating a deploy resource that uses Vital Kubernetes Engine clusters, Code Pipeline must obtain Vital Kubernetes Engine Actions permission.

* When integrating deploy resources that use distributed cloud\-native platform clusters, Code Pipeline must obtain permission for Actions on the distributed cloud\-native platform.


<span id="e0oMxU6D"></span>
## Prerequisites

The account has the IAMFullAccess permission. You can grant the IAMFullAccess permission to an IAM user via the BytePlus root user. For specific operations, refer to [Editing a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

Each BytePlus root user only needs to be authorized once.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. When a feature involves cross\-service authorization but authorization has not been granted, the system will automatically display an authorization confirmation dialog.

3. Click **Authorize** to go to the cross\-service access request page.

4. Read the associate policy and trust relationship, confirm, and then click **Authorize now**.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After successful authorization, the role ServiceRoleForCP will appear in the Identity and Access Management role list. Deleting a role will make cross\-service access unavailable. Please proceed with caution.</div>
