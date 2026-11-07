---
title: "Granting permissions to an IAM user"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Granting_permissions_to_an_IAM_user"
---

Before you manage cloud services by using Cloud Monitor, you need to attach the corresponding permission policies to Identity and Access Management (IAM) users.

<span id="f387b3db"></span>
## Prerequisites

An IAM user has been created. 

<span id="11b8a6fe"></span>
## Granting permissions to an IAM user


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user). 

2. In the left navigation bar, click **User management** \> **User**.

3. In the **user list**, find the target IAM user and click **Authorize** in the **Actions** column.

   * **Policy**: Click the **Service** drop\-down box to select Volc_Observe and search for system preset policies or custom policies related to Cloud Monitor. Select the check box before the name of the target policy based on your business requirements. 

      
      |Policy Name |Description |
      |---|---|
      |CloudMonitorFullAccess |The full management permission on Cloud Monitor. |
      |CloudMonitorReadOnlyAccess |The read\-only access permission on Cloud Monitor. |
      |CloudMonitorDashboardComponentAccess |The dashboard add\-on permission on Cloud Monitor. This policy allows the IAM user to view monitoring dashboards provided by Cloud Monitor in the consoles of other services.<br><br><br>* If you want to view the monitoring dashboards of instances in the console of other services, you need to attach this policy to the IAM user.<br><br>* If you want to view the monitoring dashboards of instances both in the console of other services and the Cloud Monitor console, you need to attach this policy and the CloudMonitorReadOnlyAccess policy to the IAM user. |
      

   * **Limit to project resources**: Specify whether the IAM user is authorized to only access resources within a project.

      * **No**: (Default) When you select this option, the authorization is globally effective.

      * **Yes**: When you select this option, you need to configure a project and the authorization takes effect only within the project.

4. Click **Submit** to attach the permission policies related to the Cloud Monitor resources to the IAM user.
