---
title: "Guide for IAM users to use certificate center"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/iam-user-guide"
---

To ensure the security of your BytePlus account, we recommend that you use Identity and Access Management (IAM) to create independent IAM users for different members of your organization and grant them different permissions to achieve separation of powers. This article takes BytePlus Certificate Center as an example to introduce how to create and authorize IAM users, so that different members of the organization can safely and conveniently access and manage SSL certificates.

<span id="prerequisites"></span>
## Prerequisites

Before you begin, make sure you have a BytePlus main account. The main account is the account you registered with BytePlus and has full access to all resources. In daily operations, we strongly recommend that you use IAM users for resource management to reduce the risk of main account key leakage.

Identity and Access Management (IAM) is a core security service provided by BytePlus to help you securely manage access to BytePlus resources. Through IAM, you can centrally manage users, permissions, and resources to achieve fine\-grained permission control.

<span id="steps"></span>
## Steps

<span id="step-1-main-account-create-an-iam-user"></span>
### Step 1: (Main account) Create an IAM user


1. Log in to the [BytePlus IAM console](https://console.byteplus.com/iam/identitymanage/user) with your main account.

2. In the left navigation pane, choose **User management** \> **User**.

3. On the user list page, click **Create new user**.

4. Complete the **Create user** configuration wizard.


<span id="configuration-wizard-description"></span>
#### Configuration wizard description

In the configuration wizard, you need to complete the following settings:


1. **Basic information settings**

   * **Username**: Set a unique username for the IAM user.

   * **Access method**: Select **Console access** or **Programmatic access** as needed.

      * **Console access**: Allows users to log in to the BytePlus console with a username and password.

      * **Programmatic access**: Allows users to access BytePlus resources through API calls.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e22bd94ab8725ec97f5014e4e3cdda59.png) </span>#{style="margin: 0"}#

2. **Permission settings**

   Select **Add permissions directly**, then search for and select system managed policies related to BytePlus Certificate Center. System managed policies are a set of predefined permission collections by BytePlus that can meet common authorization needs.

   
   |System managed policy |Description |Recommended scenario |
   |---|---|---|
   |`SSLFullAccess` |Grants the user full management permissions for the SSL certificate service. |Allows IAM users to perform all certificate operations, including purchasing, requesting, downloading, and deploying. |
   |`SSLReadOnly` |Grants the user read\-only management permissions for the SSL certificate service. |Allows IAM users to view the certificate list and details. |
   

3. **Review**

   After confirming that the information is correct, click **Next**.

4. **Done**

   Complete the creation.


After successful creation, you can see the newly created IAM user in the user list.

<span id="step-2-iam-user-accesses-byteplus-certificate-center"></span>
### Step 2: IAM user accesses BytePlus Certificate Center

IAM users can log in to the BytePlus console in the following two ways:


* **Dedicated login link**: You can get a dedicated login link for IAM users from the **Users** page of the IAM console. After accessing this link, users only need to enter their username and password to log in.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_40ea7da0f44b3c5df79c2a08d9bc9bb6.png) </span>#{style="margin: 0"}#

* **Universal login link**: When users visit the [universal login page](https://console.byteplus.com/auth/login/), they need to select **IAM user** and enter the main account name, IAM username, and password.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_43db7fea7a45bb0c526f97cad63c6beb.png) </span>#{style="margin: 0"}#


After successful login, IAM users can access the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center/ssl/overview) and view and manage SSL certificates according to the granted permissions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To adjust the permissions of an IAM user, please log in to the <a href="https://console.byteplus.com/iam/">IAM console</a> with your main account to operate.</div>


<span id="more-information"></span>
## More information

<span id="authorize-for-deploy"></span>
### Authorize IAM users for certificate deployment

If an IAM user needs to perform certificate deployment operations, in addition to the `SSLFullAccess` permission, you also need to grant the user the following permissions:


1. **Permission to complete cross\-service access authorization**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To deploy a certificate to a cloud service through the <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-deploy-certificate-to-byteplus-cdn">Certificate deployment</a> function, you must first complete cross\-service access authorization. Cross\-service access authorization is a one\-time operation used to allow BytePlus Certificate Center to access resources of other cloud services (such as CDN, ALB, etc.).   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you <strong>use the main account</strong> to complete this operation. You can also grant corresponding permissions to IAM users to allow them to complete this operation.   </div>
   

   To allow IAM users to complete cross\-service access authorization, grant the required permissions to the IAM user in the following ways:

   * **Method 1 (not recommended)** : Grant the user the `IAMFullAccess` policy. This policy grants full management permissions for Identity and Access Management (IAM), and the permission scope is wide. It is recommended that you use it with caution.

   * **Method 2 (recommended)** : Create a customer managed policy that includes the `"iam:GetRole", "iam:CreateRole", "iam:AttachRolePolicy"` operations and grant it to the IAM user. For specific operations, see [Creating a user custom policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy) and [Editing a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).

      Policy example:

      ```json
      {
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "iam:GetRole",
              "iam:CreateRole",
              "iam:AttachRolePolicy"
            ],
            "Resource": [
              "*"
            ]
          }
        ]
      }
      ```
      

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ced1e5c270a534fc441d1d3fa054138e.png) </span>#{style="margin: 0"}#

2. **Operation permissions for the target cloud service**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">IAM users can only deploy certificates to resources for which they have management permissions. Therefore, to allow IAM users to deploy certificates, you must ensure that the IAM user has resource management permissions for the target cloud service.   </div>
   

   Taking CDN as an example, if the IAM user already has full management permissions for the target cloud service (such as `CDNFullAccess`), no additional authorization is required. Otherwise, you can authorize the user in one of the following two ways:

   * **Method 1**: Grant the user the `SSLAccessCDNRolePolicy` system managed policy, which allows the IAM user to deploy certificates to all CDN domain names.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_61b5d2370c4dca4c9d571be974d62429.png) </span>#{style="margin: 0"}#

   * **Method 2**: Copy the `SSLAccessCDNRolePolicy` policy to create a customer managed policy, change the value of the `Resource` field to the specified CDN domain name resource identifier (TRN), and then grant the customer managed policy to the user. In this way, the user can only deploy certificates to the specified CDN domain name. For more information about TRN, see [What is the policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax).

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2c7542b92bdfe16851ea8f3dc27c7a31.png) </span>#{style="margin: 0"}#
