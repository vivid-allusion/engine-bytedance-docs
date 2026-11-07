---
title: "Grant push and pull permissions for images in the specified namespace"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/grant-permissions-to-push-and-pull-images-from-a-specific-namespace"
---

In practice, based on the principle of least privilege, you often need to restrict permissions of IAM users within a specific project. For example, you may need to allow a user to push images only to a specified CR namespace. This topic describes how to grant project\-level permissions that allow an IAM user to push images to a specific namespace.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

Add push permissions for images in instance `instance-a` and namespace `library` to IAM user `cr-demo`, as well as permissions for project `cr-demo-project`.

After authorization completes, the IAM user can pull all image instances in the namespace and query namespace information and all image instances under it via OpenAPI.

In this example, the authorization involves two custom policies:


* The required policy `custom-cr` for accessing CR services. It allows role\- and instance\-related actions: `SetUser`, `GetUser`, and `ListRegistries`.

   ```json
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "cr:GetUser",
           "cr:SetUser",
           "cr:ListRegistries"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   

* Project policy `custom-cr-for-project` in this scenario: policy for pushing images in the specified namespace (for example: instance `instance-a`, namespace `library`).

   ```json
   {
     "Statement": [
         {
         "Effect": "Allow",
         "Action": [
             "cr:List*",
             "cr:Get*",
             "cr:Pull*",
             "cr:Push*"
         ],
         "Resource": [
           "trn:cr:*:*:instance/instance-a", 
           "trn:cr:*:*:repository/instance-a/library", 
           "trn:cr:*:*:repository/instance-a/library/*"
         ]
       }
     ]
   }
   ```
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A project has been created based on the business scenario. For operating details, see [Organization Setup](https://docs.byteplus.com/en/docs/organization/OrganizationSetup). In this example, the project name is `cr-demo-project`.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".56ys5LiA5q2l77ya5Yib5bu65bm25re75Yqg5YWo5bGA5o6I5p2D"></span>
### Step 1: Create and attach the global policy


1. Log in to the [IAM console ](https://console.byteplus.com/iam/overview/).

2. In the left navigation bar, click **Policy Management**.

3. On the ** Policy Management ** page, click ** Create Policy**.

4. In the **Create Policy** dialog box, create a policy named `custom-cr` with the sample code below.

   ```json
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "cr:GetUser",
           "cr:SetUser",
           "cr:ListRegistries"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   

5. Click **Submit** to complete creation.

6. On the creation success page, click **Add authorization**.

7. Select the target IAM user `cr-demo`.


8. Click **Confirm** to complete the configuration

<span id=".56ys5LqM5q2l77ya5Yib5bu65bm25re75Yqg6aG555uu5p2D6ZmQ"></span>
### Step 2: Create a policy and grant project\-specific permissions

Grant the user CR read and write permissions for a specific project (cr\-demo\-project in this example) by attaching the `custom-cr-for-project policy` at the project level.


1. Log in to the [IAM console ](https://console.byteplus.com/iam/overview/).

2. In the left navigation bar, click **Policy Management**.

3. On the ** Policy Management ** page, click ** Create Policy**.

4. In the **Create Policy ** dialog box, create a policy named `custom-cr-for-project `with the sample code below.

   ```json
   {
     "Statement": [
         {
         "Effect": "Allow",
         "Action": [
             "cr:List*",
             "cr:Get*",
             "cr:Pull*",
             "cr:Push*"
         ],
         "Resource": [
           "trn:cr:*:*:instance/instance-a", 
           "trn:cr:*:*:repository/instance-a/library", 
           "trn:cr:*:*:repository/instance-a/library/*"
         ]
       }
     ]
   }
   ```
   

5. Click **Submit** to complete creation.

6. On the creation success page, click **Add authorization**.

7. Select the `custom-cr-for-project` policy and the `cr-demo-project` project.

8. Click **Confirm** to complete authorization.
