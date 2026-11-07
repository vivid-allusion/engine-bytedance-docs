---
title: "VCI preparations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-preparations"
---

This topic describes the necessary preparations before using Vital Container Instance (VCI).

<span id=".5q2l6aqk5LiAOuazqOWGjCBWb2xjYW5vIEVuZ2luZSA="></span>
## Step 1: Register a BytePlus account

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have already registered a BytePlus account, skip this step.</div>



1. Go to the [BytePlus console](https://console.byteplus.com/auth/login) and click **Sign up now**.

2. Set your account information as prompted. For more information, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

3. Complete enterprise real\-name authentication for your account. For more information, refer to [Identity authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, only users who have completed enterprise real\-name authentication can use Vital Kubernetes Engine (VKE) and VCI.   </div>
   

<span id=".5q2l6aqk5LqMOuWFheWAvOi0puaItw=="></span>
## Step 2: Add funds to your account

Ensure that the balance of your BytePlus account is greater than or equal to USD 0 after deducting coupons.

<span id=".5q2l6aqk5LiJOuW8gOmAmuWuueWZqOacjeWKoeadg-mZkA=="></span>
## Step 3: Apply for VKE permissions


1. Log in to the [Vital Kubernetes Engine (VKE) console](https://console.byteplus.com/vke).

2. Apply for VKE console permissions as prompted.


<span id=".5q2l6aqk5ZubOijlj6_pgIkp5Yib5bu65ZKM5o6I5p2DLWlhbS3nlKjmiLc="></span>
## (Optional) Step 4: Create and authorize IAM users

By default, the main BytePlus account has all VKE permissions. If you want multiple users to collaboratively manage the resources within your account, you must create Identity and Access Management (IAM) users and grant them appropriate roles and permissions.


1. Log in to the [IAM console](https://console.byteplus.com/iam/).

2. According to the instructions in [Creating users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) and [attaching access policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management), create an IAM user and attach necessary policies as listed below.

   For more information on policies and their configurations, refer to [Authorization management](https://docs.byteplus.com/en/docs/vke/Authorization-overview).

   
   |Policy |Description |
   |---|---|
   |VKEFullAccess |This policy grants full read and write permissions on VKE, including full read and write access to ECS, Load Balancer, VPC, and NAT Gateway. |
   |VKEInnerFullAccess |This policy grants full read and write permissions on the internal resources of VKE. |
   |VKEReadOnlyAccess |This policy grants read\-only permissions on VKE. |
   |VKEInnerReadOnlyAccess |This policy grants read\-only permissions on the internal resources of VKE. |
   


<span id=".5q2l6aqk5LqUOijlj6_pgIkp6YWN572uLWlhbS3nlKjmiLfnmoQtcmJhYy3mnYPpmZA="></span>
## (Optional) Step 5: Configure RBAC permissions for IAM users

VKE offers the role\-based access control (RBAC) authorization feature to meet the fine\-grained resource access control needs of enterprise users. After granting permissions to IAM users, you can configure RBAC permissions for them.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Authorizations** \> **User authorization**. Find the IAM user for which you want to configure RBAC permissions. Click **Add authorization** in the **Actions** column.

3. On the **Create user authorization** page, grant the appropriate permissions to the user. Click **Create**.


<span id=".5q2l6aqk5YWtOuWIm-W7uuengeaciee9kee7nA=="></span>
## Step 6: Create a VPC

A virtual private cloud (VPC) offers an isolated, self\-configured, and managed virtual network environment for clusters.


1. Log in to the [VPC console](https://console.byteplus.com/vpc).

2. In the top menu bar, select the region closest to your application.

3. In the left navigation bar, click **VPC**, and click **Create VPC**.

4. Configure the VPC and subnet parameters as prompted. For more information on the parameters, refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id=".5q2l6aqk5LiDOuS4iuS8oOmVnOWDjw=="></span>
## Step 7: Upload images

VKE allows you to use container images in BytePlus Container Registry (CR) or third\-party image registries. Before using VKE, ensure that images have been uploaded to the image registry.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">In this example, an Nginx application is deployed. You need to upload the Nginx image to CR and set the image type to <strong>Public</strong> in advance. For more information, refer to <a href="https://docs.byteplus.com/en/docs/cr/push-and-pull-images">Pushing and pulling images</a>.</div>
