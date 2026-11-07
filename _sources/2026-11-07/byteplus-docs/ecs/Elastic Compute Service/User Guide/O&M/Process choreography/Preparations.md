---
title: "Preparations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Preparation"
---

When using the orchestration service for the first time, you need to create a role (CustomRoleForOOS) for your account that is granted with read/write access to your ECS resources. This role has all default permissions offered by the orchestration service, helping you avoid any permission issues while using the service. For more information about roles, see [Role management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-roles).

<span id="kUbhyYcO"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Orchestration".

3. On the "Create role request" page, confirm the scope of permissions involved for the role, and then click the "Create now" button. The system will automatically complete the authorization process, and subsequent operation orchestration actions will default to being authorized and executed via this role (CustomRoleForOOS).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Cross\-service access is performed by using IAM roles. An IAM role is granted permissions to access specific cloud resources, and the current service can assume this role to access resources of other cloud services. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Overview-3">IAM</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After successful authorization, the role will appear in the role list of Identity and Access Management (IAM). Deleting the role will result in cross\-service access failures. Therefore, perform this operation with caution.   </div>
