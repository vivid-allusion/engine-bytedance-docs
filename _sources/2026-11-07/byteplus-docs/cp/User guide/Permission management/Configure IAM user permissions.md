---
title: "Configure IAM user permissions"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configure_IAM_user_permissions"
---

Code Pipeline supports multi\-user collaboration on Code Pipeline resources by authorizing IAM users (also known as sub\-users) to meet the need for multi\-user collaborative operation of Code Pipeline resources. This document mainly describes the steps for authorizing IAM users to use the Code Pipeline product.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* Identity and Access Management:  [Identity and Access Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3) (IAM) is the permission management system provided by BytePlus for customers, used to control the access permissions of different identities to cloud resources.

* BytePlus account (root user): Refers to a user identity generated through the BytePlus official website or an authorized channel, uniquely identified by account ID and name. The BytePlus root user is the owner of Cloud Service resources and serves as the principal for resource measurement and billing. By default, the root user has all permissions for the Code Pipeline Product.

* IAM user: An identity created by an enterprise customer for each user of cloud resources, also referred to as an IAM user. An IAM user is typically associated with an employee within an enterprise or an application. An IAM user belongs to a BytePlus root user. A BytePlus root user can have multiple IAM users. The combination of the BytePlus root user ID and the IAM user name serves as the unique identifier. IAM users only have permission to use Cloud Service resources. The IAM user needs the BytePlus root user to configure the system default policy of the Code Pipeline Product for them.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Account has completed real\-name authentication. For details, refer to  [Real-name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The IAM user has been created. For detailed instructions, refer to  [User management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Identity and Access Management (IAM) Console](https://console.byteplus.com/iam).

2. In the left navigation bar, select **Identity Management \> Users**.

3. In the **User list**, select the username for which you need to set permission, then click **Manage** under the corresponding **Actions** column.

4. On the **user details** page, under the **Permission \> Global Permission** tab, click **add permission**.

5. In the search box of the **Add Permission** panel, enter `CP` to search for the system preset policies for the Code Pipeline Product.

   
   |Policy name |Policy description |
   |---|---|
   |CPAdminAccess |The Code Pipeline administrator policy is recommended for enterprise administrators or project managers.<br><br><br>* Application delivery: Supports creating applications and viewing the application list.<br><br>* Other modules: Full read\-write permission. |
   |CPMemberAccess |The Code Pipeline workspace member policy is recommended for personnel engaged in project development or operations.<br><br><br>* Workspace resources: The application delivery module supports creating new applications and viewing the list of applications; other modules have full read and write permissions.<br><br>* Workspace: Read\-only permission; editing the workspace is not supported.<br><br>* Resources outside the workspace: read\-only permission. |
   |CPReadOnlyAccess |The Code Pipeline read\-only policy only allows viewing the contents of each module in Code Pipeline. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The application delivery module provides fine\-grained permission control capabilities. The operation permissions for each application are managed independently by the application delivery module.   </div>
   

6. According to actual requirements, check the target policy, click **confirm**, and add the permission policy for the Code Pipeline Product to the IAM user.
