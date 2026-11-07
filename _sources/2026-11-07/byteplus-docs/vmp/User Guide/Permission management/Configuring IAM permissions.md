---
title: "Configuring IAM permissions"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Configuring-IAM-permissions"
---

Before you manage the resources of Vital Managed Service for Prometheus (VMP) by using an Identity and Access Management (IAM) user, you need to attach a policy to the IAM user.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An IAM user is created. 

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [IAM console](https://console.byteplus.com/iam).

2. In the left navigation bar, click **User management** \> **User**.

3. In the user list, find the target IAM user and click **Authorize** in the **Actions** column.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57092906f50d1a5b51201e358954b9bd.png) </span>


|Parameter |Description |
|---|---|
|Identity |Check information of the user that you want to authorize. |
|Policy |Select policies as needed. For a list of system\-managed VMP policies, see [Permission overview](https://docs.byteplus.com/en/docs/vmp/Permission-overview).<br><br>You can filter policies by policy type, service, policy name, or policy description. We recommend that you filter system\-managed VMP policies by selecting **vmp** from the **Service** drop\-down list. |
|Limit to project resources |Specify whether to limit the authorization only to resources within the specified projects. <br><br><br>* **No** (default): does not grant permissions by project. When you select this option, authorization takes effect globally.<br><br>* **Yes**: grants permissions by project. When you select this option, you need to specify projects to which the authorization applies.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only certain resources in VMP support project\-level access control. If you want to assign read\-only or full access to a specific project, you need to choose the corresponding policy and the project. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Configuring_project-level_permissions">Configuring project\-level permissions</a>.</div><br> |



4. Click **Submit** to attach the permission policies related to the VMP resources to the IAM user.
