---
title: "Granting project-specific permissions"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/grant-project-permissions"
---

Before associating a CR repository namespace with a project, you need to grant the specified permissions for the target user. This topic describes how to grant project\-specific permissions.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Before associating a CR namespace with a project, you need to grant the following permissions to the user.


* **Global permission**: Attach the `CRReadOnlyAccess` policy.

* **Project permission**: Attach a project\-specific policy based on your needs. In this example, the `CRFullAccess` policy that allows CR read and write access is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A project has been created based on the business scenario. For operating details, see [Organization Setup](https://docs.byteplus.com/en/docs/organization/OrganizationSetup). In this example, the project name is `cr-demo-project`.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".56ys5LiA5q2l77ya5re75YqgIENSUmVhZE9ubHlBY2Nlc3Mg562W55Wl"></span>
### Step 1: Attach the CRReadOnlyAccess policy


1. Log in to the [IAM console](https://console.byteplus.com/iam).

2. In the left navigation bar, click **Permission policy**.

3. On the **Permission policy** page, search `CRReadOnlyAccess`.

4. Click **Authorization** in the **Actions** column.

5. In the **Identity** section, select the user, user group, or role to be authorized.

6. Click **Submit** to complete the authorization.


&nbsp;

<span id=".56ys5LqM5q2l77ya5re75Yqg6aG555uu5p2D6ZmQ"></span>
### Step 2: Grant project\-specific permissions

Grant the user CR read and write permissions for a specific project (cr\-demo\-project in this example) by attaching the `CRFullAccess` policy at the project level.


1. Log in to the [IAM console](https://console.byteplus.com/iam).

2. In the left navigation bar, select **User management** and **User** in sequence.

3. Click the target user name (in this example, it is `cr-demo`) to enter the user detail page.

4. On the **User detail** page, select **Policy** \> **Authorize**.

5. Select the `CRFullAccess` policy and the target project.

6. Click **Confirm** to complete authorization.
