---
title: "Granting full management permissions of a specific namespace"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Grant_all_management_permissions_to_the_specified_namespace"
---

This topic describes how to grant users management permissions of a specified CR namespace.

<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios

In daily development, namespaces are often used to differentiate business resources. Similarly, you may need to manage resource access permissions based on namespaces.

You can use the BytePlus project management feature to add members from different business teams to different projects, and then attach policies granting namespace access to the projects.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".56ys5LiA5q2l77ya5Yib5bu66aG555uu5bm26YWN572u5p2D6ZmQ"></span>
### Step 1: Create a project and configure permissions

First, create a project and attach the `CRFullAccess` policy to it to grant users full CR management access.


1. Log in to the [IAM console](https://console.byteplus.com/iam/overview/) for creating the project. For operating details, see [Organization Setup](https://docs.byteplus.com/en/docs/organization/OrganizationSetup). In this example, the project name is `cr-namespace`.

2. Under the **Permission policy** tab, click **Authorize**.

3. Configure the project policy.

   1. For the **Select identity** step, select the target user or role for authorization.

   2. For the **Authorize** step, select `CRFullAccess`.

   3. Then, confirm the changes as prompted and complete the policy configuration.


<span id=".56ys5LqM5q2l77ya5YWz6IGU6ZWc5YOP5LuT5bqT5ZG95ZCN56m66Ze0"></span>
### Step 2: Associate the CR namespace

To complete the authorization, you need to associate the created `cr-namespace` project with the target namespace.


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **List of instances**. In the **List of instances** area, find the instance for which you need to modify namespace resources, and click **Enter instance**.

4. On the instance page, in the left navigation bar, click **Namespace**.

5. On the **Namespace** page, find the target namespace and click` ...` in the **Actions** column. Then, select **Modify**.

6. Under the **Associated project** section, select the created project. In this example, the project is `cr-namespace`.

7. Click **Confirm** to complete the modification.
