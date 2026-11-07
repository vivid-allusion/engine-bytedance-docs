---
title: "IAM user permission management"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/iam_user_permission_management"
---

After successfully creating an IAM user, you need to grant the IAM user permission to access Database Transmission Service (DTS) when they require it. This topic describes the steps to authorize a subuser to access DTS.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* A BytePlus account has been registered with real name authentication completed. For more information, refer to [Create account](https://docs.byteplus.com/en/docs/6261/64925) and [Verify account](https://docs.byteplus.com/en/docs/6261/64935).

* A created user is an IAM user. For more information, refer to [User management](https://docs.byteplus.com/en/docs/6257/64977).


<span id=".5Z-65pys5qaC5b-1"></span>
## **Basic concepts**


* IAM: Identity and Access Management (IAM) is a permission management system used to control access permissions of different identities to cloud resources. For details, refer to [what is IAM?](https://docs.byteplus.com/en/docs/6257/64959)

* Account: Also known as the root user, is the owner of cloud service resources and the subject of resource metering and billing. The root user has all permissions under the account by default.

* User: Also known as an IAM user, is an identity in IAM created by an Account or a user with permissions. After a user is granted permissions (Policy), they can log on to the console or use the Access Key to call APIs to access cloud resources.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [lAM](https://console.byteplus.com/iam/identitymanage/user) console using the root user.

2. In the left navigation bar, click **User**.

3. On the **User** page, select the target IAM user.

4. On the **User details** page, click **Permissions**.

5. On the **Permissions** tab, assign specified permissions to IAM users as needed:

   * **Global authorization**

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If IAM users need to create tasks in DTS, you must grant them global authorization. Otherwise, they can not create DTS tasks.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After granting global authorization, IAM users will have permissions across all projects.      </div>
      

      1. In the **Global authorization** pane, click **Add permissions**.

      2. In the **Add permissions** panel, select the following permission policies.

         * `DTSFullAccess`: represents full management permissions for DTS.

         * `IAMReadOnlyAccess`: represents read\-only access to IAM.

      3. Click **OK**.

   * **Project authorization**

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If IAM users do not need to create tasks in DTS, you can assign them minimal permissions, granting only the rights needed to execute certain tasks without additional permissions.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After granting permissions for the specified project, the IAM user will have permissions only under the authorized project.      </div>
      

      1. In the **Project authorization** pane, click **Add permissions**.

      2. In the ** Add permissions** panel, select the following permission policies.

         * `DTSFullAccess`: represents full management permissions for DTS.

         * `IAMReadOnlyAccess`: represents read\-only access to IAM.

      3. Select the target project from the **Scope of effect** drop\-down list.

      4. Click **OK**.
