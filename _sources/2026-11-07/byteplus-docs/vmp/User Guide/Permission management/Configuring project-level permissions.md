---
title: "Configuring project-level permissions"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Configuring_project-level_permissions"
---

Project\-level authorization grants access only to resources within the specified projects. This topic describes how to grant a user read\-only or full access to Vital Managed Service for Prometheus (VMP) resources of specific projects.

<span id="bHcHT0R0"></span>
## Background

Currently, only certain resources in VMP support project\-level access control. For a list of system policies related to VMP, see [IAM overview](https://docs.byteplus.com/en/docs/vmp/Permission-overview). If you want to assign read\-only or full access to a specific project, choose the corresponding policy and the project. Otherwise, you may get many permission errors, which can affect your experience with using this service.

<span id="oMuihIQ8"></span>
## Prerequisites

An IAM user has been created.

<span id="9cAGuZAC"></span>
## Operating instructions

When configuring project‑level permissions on VMP for a specific IAM user, you need to grant both the corresponding global common resource permissions and the specified project‑level permissions at the same time. This prevents frequent console errors caused by missing common permissions, affecting the user experience.

Configure permissions based on the permission requirements of the IAM user in the target project:


* Read‑only access: Grant read‑only permissions on VMP to the IAM user. Use this policy only to view monitoring data and resource information. For details, see [Scenario 1: read-only access to projects](https://docs.byteplus.com/en/docs/vmp/Configuring_project-level_permissions?TagIDs=2,143&lang=en#Mmh427p6).

* Full access: Grant full permissions on VMP to the IAM user. Use this policy when you need to create, modify, or delete related resources. For details, see [Scenario 2: full access to projects](https://docs.byteplus.com/en/docs/vmp/Configuring_project-level_permissions?TagIDs=2,143&lang=en#JW2Vjsfz).


<span id="xFjwKQtZ"></span>
## Procedure

<span id="Mmh427p6"></span>
### Scenario 1: read\-only access to projects


1. Log in to the [IAM console](https://console.byteplus.com/iam). 

2. In the left navigation pane, click **User management** \> **User**.

3. In the user list****, find the target IAM user and click **Authorize** in the **Actions** column.

4. Add `VMPCommonReadonlyAccess` as a global policy. Click **Submit**.

5. Limit `VMPReadOnlyAccess` to the desired projects. Click **Submit**.


&nbsp;

<span id="JW2Vjsfz"></span>
### Scenario 2: full access to projects


1. Log in to the [IAM console](https://console.byteplus.com/iam). 

2. In the left navigation pane, click **User management** \> **User**.

3. In the user list****, find the target IAM user and click **Authorize** in the **Actions** column.

4. Add `VMPCommonFullAccess` as a global policy. Click **Submit**.

5. Limit `VMPFullAccess` to the desired projects. Click **Submit**.


<span id="mNOB2EZz"></span>
## Validate results

Log in to the VMP console by using the IAM user that you authorized. If you can access an authorized project and fail to access an unauthorized project with a permission error, the authorization is successful.
