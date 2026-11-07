---
title: "How do I fix the \"AccessDenied,Code:403\" error when performing operations on cluster resources?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-resolve-the-AccessDenied-Code_403-error-when-operating-cluster-resources"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description


* Case 1

   When I log in as an IAM user and perform operations on cluster resources (for example, nodes) on the cluster configuration page, the system displays the **Not authorized yet** message. The error message is `AccessDenied,Code:403`.

* Case 2

   When I use an IAM user to deploy the ebs add\-on, the system displays the `need bind ecs with assume role name` error.


<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The account you are using has not been granted RBAC authorization for this cluster and therefore does not have permission to manage the relevant cluster resources. A BytePlus root user or IAM user, by default, only has administrator permissions for clusters that they create. To perform operations on clusters created by other accounts, you need RBAC authorization.

For RBAC details, see [Authorization overview](https://docs.byteplus.com/en/docs/vke/Authorization-overview).

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution


1. Log in to the [VKE console](https://console.byteplus.com/vke) using a cluster administrator account.

2. In the left navigation bar, click **Authorizations** \> **User authorization**.

3. On the **User authorization management** page, click **Create user authorization**.

4. On the **Create user authorization** page, select the username to be authorized (the IAM user) and configure RBAC permissions for the IAM user as needed.

   
   |Parameters |Description |
   |---|---|
   |User  |In the **All users** list, select the check boxes in front of the usernames to configure the same RBAC permissions for the selected IAM users. |
   |Permissions |Select the cluster and namespace to be authorized, and specify the role for the users. In this example, select **Cluster administrator**. |
   

5. Click **Create** to complete IAM user authorization.
