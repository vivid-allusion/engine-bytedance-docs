---
title: "User Synchronization Settings"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/User-Synchronization-Settings"
---

# Use Cases

When initializing your enterprise identities in the cloud, you must use your identity management platform as the identity source and import employee identities into Cloud Identity Center.

Cloud Identity Center supports **Lark** as an enterprise identity source, allowing you to import employee identities and synchronize identity information with one click.

## Prerequisites

1. You have activated Cloud Identity Center. [Activate Cloud Identity Center](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/ServiceOpen/).

2. You have an enterprise identity management platform, such as an independent Lark tenant, and you either have administrator permissions for the Lark tenant or can work with a Lark tenant administrator to configure user synchronization.

3. You are signed in with an administrator account for the enterprise organization. This can be the root user or an IAM user with the required permissions.

## Procedure

1. Sign in to the BytePlus console and go to the [User Synchronization Settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/) page.

2. Click **Configure Identity Source** and select **Lark**.

3. On the **Configure User Synchronization** page, first ensure that the BytePlus app has been installed in your enterprise's Lark tenant:

   1. Preparation: Use the Lark mobile app to scan the QR code with a Lark administrator account, or go directly to the [BytePlus app in the Lark App Directory](https://app.larksuite.com/app/cli_aa28992c4c78de14) to download and install the **BytePlus app for Lark**.

> **Note:**  The app must be installed by a Lark administrator.

   2. The tenant binding operation after installation does not have to be performed by a Lark administrator. However, a Lark user must be signed in through the browser, and that user must be included in the BytePlus app's availability scope. A Lark administrator can go to the [Lark Admin Console](https://www.larksuite.com/admin/), choose **Workplace \> App Management \> BytePlus \> Available Members**, and then review or configure the available\-member scope.

   3. The available\-member scope selected during app installation defines the range of employee directory data that you authorize for synchronization to BytePlus.

   4. After confirming that the BytePlus app has been installed, click **Confirm App Activation and Bind Lark Tenant**. During the redirect process, sign in or scan the QR code using a Lark administrator account to authorize access. After a successful sign\-in, you are automatically redirected to BytePlus Cloud Identity Center to continue with the next step.

4. In the **User Synchronization Configuration** step, you can view the binding between the Lark tenant and the Cloud Identity Center instance. **Verify that the binding is correct.**  If it is not, return to the previous step and bind the tenant again. After verifying the binding, configure and review the mappings between the user information fields in Cloud Identity Center and the employee information fields in Lark under **Field Synchronization Details**. Here, you can map the username and display name synchronized to Cloud Identity Center to the corresponding Lark user fields.

   1. **Username:**  The unique identifier of a user in Cloud Identity Center. It must be unique across the entire Cloud Identity Center instance. In subsequent steps, the username is also used as the IAM username when configuring multi\-account SSO and creating IAM users in each account. We recommend selecting a Lark user field that uniquely identifies an employee. Supported fields include name, user_id, union_id, email, mobile, employee_no, and enterprise_email.

   2. **Display name:**  Additional readable information used to identify a user in Cloud Identity Center. Select a field that is easy to understand. Supported fields include name, en_name, nickname, email, enterprise_email, and mobile.

5. When the configuration is complete, click **Complete**. The identity source is added successfully. On the identity source synchronization success page, go to **User Synchronization Settings** and click **Enable Incremental Identity Synchronization** or **Manually Trigger Synchronization**.

   1. **Enable Incremental Identity Synchronization:**  Cloud Identity Center performs a full import of user identity information from the accessible portion of the Lark directory. It then begins synchronizing employee onboarding, offboarding, transfer, and other changes from Lark to Cloud Identity Center in real time. Synchronization continues until you disable incremental identity synchronization.

   2. **Manually Trigger Synchronization:**  Cloud Identity Center performs a full import of user identity information from the accessible portion of the Lark directory, but it does not perform real\-time synchronization or any additional full synchronization. No further synchronization occurs until you enable incremental identity synchronization or manually trigger synchronization again.

## Next Steps

Users synchronized from Lark can scan a QR code with Lark to sign in directly to the BytePlus website. They can also sign in through the standalone sign\-in portal provided by Cloud Identity Center. For configuration instructions, see [Configure User Sign-in Methods](https://docs.byteplus.com/en/docs/CloudIdentity/User-login-settings).

After users have been created, if you do not need to configure the standalone portal sign\-in method, proceed to [Configure User Access Authorization](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-user-based-access-authorization) and  [Configure Role Access Authorization](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-role-based-access-authorization).

## FAQ

#### How do I synchronize only part of the enterprise directory?

When installing the **BytePlus** app from the Lark App Directory, you can select the range of employees that you authorize for synchronization to BytePlus. Under **Installation Scope**, specify **Selected Members** to synchronize only those users to BytePlus.

If the app has already been installed, or if you want to change the installation and synchronization scope later, sign in to the [Lark Admin Console](https://www.larksuite.com/admin/) as a Lark tenant administrator. Go to **Workplace \> App Management**, find the BytePlus app, and adjust the **Available Members** scope.

> **Note:**  If user synchronization has already been configured and you change the synchronized directory scope in the Lark Admin Console, go to the [BytePlus console](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/) to process the data that has already been synchronized.

#### Why do I receive an authorization failure message when binding Lark?

During the binding process, scan the QR code and sign in with a Lark administrator account to bind your enterprise's Lark tenant to the Cloud Identity Center instance. If an authorization failure message appears after you scan the QR code and are redirected back to Cloud Identity Center, try the following solutions:

1. Contact your enterprise's Lark administrator and verify that the BytePlus app from the Lark App Directory has been installed in your Lark tenant and updated to use the latest permissions. If the app is not installed, install it. If its permissions are outdated, go to the [Lark Admin Console](https://www.larksuite.com/admin/), choose **Workplace \> App Management**, find the BytePlus app, and update its authorization under app permissions.

2. Contact your enterprise's Lark administrator and verify that the Lark user who scanned the QR code is included in the BytePlus app's available\-member scope. Only available members of the app can authorize synchronization of the enterprise directory to BytePlus.
