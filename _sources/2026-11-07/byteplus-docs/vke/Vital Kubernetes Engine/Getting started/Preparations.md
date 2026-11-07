---
title: "Preparations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Preparations"
---

This topic describes the preparations you need to complete before getting started with VKE.

<span id=".5q2l6aqk5LiA77ya5rOo5YaM54Gr5bGx5byV5pOO"></span>
## Step 1: Create a BytePlus root user

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Skip this step if you already have a BytePlus account.</div>



1. Go to the [BytePlus console](https://console.byteplus.com/auth/login/) and click **Sign up now**.

2. Finish registration as prompted on the page.  For details, see [How to register accounts](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

   After registration, click **Go to the login page** to log in to the BytePlus console.

3. Finish identity authentication.   For details, see [Identity authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).


<span id=".5q2l6aqk5LqM77ya5YWF5YC86LSm5oi3"></span>
## Step 2: Top up your account


* Ensure that your BytePlus account balance is not zero when vouchers are excluded. For details, see [Billing center](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

* Pay\-as\-you\-go cloud resources can be created only if your account balance is not zero when vouchers are excluded.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Creating a VKE cluster may incur fees for cloud infrastructure resources such as Load Balancer, NAT Gateway, EIP, and EBS instances. You can view the actual billing by checking the <strong>Configuration fee</strong> field at the bottom of the cluster creation page. For details on billing models and fees for cloud infrastructure, see <a href="https://docs.byteplus.com/en/docs/vke/Billing">Product billing</a>.</div>


<span id=".5q2l6aqk5LiJ77ya5byA6YCa5a655Zmo5pyN5Yqh5p2D6ZmQ"></span>
## Step 3: Apply for VKE permissions


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. Follow the prompts on the page to apply for permissions to use the VKE console.


<span id=".5q2l6aqk5Zub77ya77yI5Y-v6YCJ77yJ5Yib5bu65ZKM5o6I5p2DLWlhbS3nlKjmiLc="></span>
## Step 4: (Optional) Create and authorize IAM users

By default, a BytePlus root user has full access to VKE products. To allow other users to collaboratively manage resources within your account, you need to create IAM users and grant them the appropriate roles and permissions.


1. Log in to the [IAM console](https://console.byteplus.com/iam/overview/).

2.  According to the instructions in [Creating users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) and [Attaching access policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management), create an IAM user and attach necessary policies as listed below.

   For more details about policies, see [Authorization overview](https://docs.byteplus.com/en/docs/vke/Authorization-overview).

   
   |Policy |Description |
   |---|---|
   |VKEFullAccess |This policy allows full read and write access to VKE, including ECS, Load Balancer, VPC, and NAT Gateway. |
   |VKEInnerFullAccess |This policy allows internal read and write access to VKE. |
   |VKEReadOnlyAccess |This policy allows read\-only access to VKE. |
   |VKEInnerReadOnlyAccess |This policy allows internal read\-only access to VKE. |
   |BillingCenterPayOrderAccess |This policy grants payment permission for the cost center and PayOrder permission for OpenAPI access. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Starting from August 31, 2025, all IAM users (even those with <strong>FullAccess</strong> permission) must have <strong>BillingCenterPayOrderAccess</strong> permission to apply for prepaid resources. Otherwise, order payment cannot be completed.   </div>
   

<span id=".5q2l6aqk5LqU77ya77yI5Y-v6YCJ77yJ6YWN572uLXJiYWMt5p2D6ZmQ"></span>
## Step 5: (Optional) Configure RBAC permissions

VKE provides RBAC (Role\-Based Access Control) to meet requirements for fine\-grained resource access control in enterprises. You can configure RBAC for existing IAM users.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VKE can also provide RBAC for IAM roles. In this topic, the IAM user created in step 4 above will be taken as an example to introduce how to configure RBAC for a user under the root account. For more details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions">Configuring RBAC</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Authorizations** \> **User authorization**. Find the IAM user who requires RBAC, and click **Add authorization** in the **Actions ** column.

3. On the **Create user authentication** page, finish configurations and click **Confirm** to save changes.


<span id=".5q2l6aqk5YWt77ya5Yib5bu656eB5pyJ572R57uc"></span>
## Step 6: Create a VPC

VPC is an isolated, user\-configurable, and manageable private network environment for clusters on VKE.


1. Log in to the [VPC Console](https://console.byteplus.com/vpc).

2. In the top navigation bar, select the region closest to your business.

3. In the left navigation bar, click **VPC**, and then click **Create VPC**.

4. Configure the VPC and subnet parameters as prompted on the page. For details of the parameters, see [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this quick start, the following network resources are created: a VPC named <strong>demo\-vpc</strong> and two subnets (<strong>demo\-vpc\-subnetA</strong> and <strong>demo\-vpc\-subnetB</strong>) within this VPC.   </div>
   

<span id=".5q2l6aqk5LiD77ya5LiK5Lyg6ZWc5YOP"></span>
## Step 7: Upload an image

VKE supports using images from both the BytePlus CR and third\-party container registries. Make sure that images are already uploaded to a container registry before you get started with VKE.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic provides an example of how to deploy an Nginx application. You can use the sample image provided in this topic, or upload your own Nginx image to CR. For details, see <a href="https://docs.byteplus.com/en/docs/cr/push-and-pull-images">Pushing and pulling images</a>.</div>
