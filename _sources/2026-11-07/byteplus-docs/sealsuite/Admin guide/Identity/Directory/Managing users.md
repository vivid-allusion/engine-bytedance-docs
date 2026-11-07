---
title: "Managing users"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-members"
---

To effectively manage your organization's users throughout their entire lifecycle within SealSuite, this guide provides step\-by\-step instructions. You will learn how to add new users individually or in bulk, view their details, send activation invitations, and manage their accounts by changing departments, resetting passwords, or processing resignations. The methods described apply specifically to organizations where user information is manually managed in the SealSuite Admin Console.

# Precautions

* If your enterprise's organizational structure is built using a third\-party data import method, it is advised to keep user information updated in the third\-party system and sync this data source regularly in the SealSuite Admin Console.

* To perform other operations during a directory sync, you must first stop the sync. It helps prevent the incremental data from the third\-party data source from syncing to the SealSuite Admin Console. Please proceed with caution. For more information on importing from third\-party data sources, please refer to [Setting up account systems and identity authentication](https://docs.byteplus.com/docs/sealsuite/docs-managing-account-settings).

# Use case description

This section outlines how to manage user information throughout the employee lifecycle, from onboarding to offboarding:

1. You can add and view user information. For specific operations, please refer to the following:

   * **Add department users**: Add users to designated departments and facilitate the addition or batch import of user information individually or in groups.

   * **View user information**: Access the information of an individual user or retrieve details for a group of users simultaneously.

2. You can configure the policy for the user account activation invitation. For specific operations, please refer to the following:

   * **Activate a single user account**: Set up the policy for individual user activation invitations.

   * **Batch activation of user accounts**: Set up the sending policy for users in bulk.

3. You can manage existing user accounts. For specific operations, please refer to the following:

   * **Change user department**: Transfer a user to a different department individually or in batches.

   * **Lock User**: Lock the specified user's account.

   * **Reset account password**: Reset the specified user's password.

   * **Process user resignations**: Process resignations for individual users or in batches

# Add users under department

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Select the specified department in the department structure list on the left.

4. Add a user in the department area on the right.

   * Method One: Add user information individually

      Click **Add User**, then complete the following configurations in the **Add User** dialog box and click **Confirm**.

      |**Configuration Item** |**Description** |
      |---|---|
      |**Name** |Set the user name. |
      |**User ID** |User ID refers to the user's unique Identifier. If you leave this field blank, SealSuite will automatically generate a User ID. |
      |**Department** |Select the user's department. |
      |**Direct Manager** |Select the direct manager of the user. |
      |**Email** |Set the user's email address. |
      |**Phone number** |Set the user's phone number. |
      |**Role** |Select the user's role. |
      |**Account Effective Date** |Set the account effective date. The system automatically sets the time to the present but allows for changes. |
      |**Account expiration date** |Set when the account expires. At that time, SealSuite automatically disables the account, blocks login, and revokes all access permissions. The date can be set manually by an administrator, calculated by a security policy, or set to follow the employee’s departure time by default. |
      |**Departure initiation time** |Records the specific time when the offboarding process officially begins. Depending on how the process is initiated, it triggers different account statuses:<br><br><br>* **Scenario 1**: Initiated by the employee. The status changes to **To be offboarded**, and the account remains active until its expiration date.<br><br>* **Scenario 2**: Initiated by an administrator. The status immediately changes to **Offboarded**, and account permissions expire instantly. |
      |**Departure time** |Sets the date on which the employee’s employment officially ends for legal or contractual purposes. This data can be automatically synchronized from upstream HR systems or manually entered by an administrator. |
      |**Individual Status** |Select a user's status: **Active**, **To be offboarded**, or **Offboarded**. |
      |**Advanced Properties** |Set the advanced properties of the user's account. |
      |**Activation Notification Setting** |Choose whether to send activation information, with options to **Send Now**, **Send Later**, and **Do Not Send**. Configuration Instructions for each method are as follows:<br><br><br>* **Send Now**: After selecting **Send Now**, you must continue to configure the method of sending invitations, with options to choose either **SMS** or **Email**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet configured a gateway, click **Configure SMS Gateway** or **Configure Mail Gateway** to set one up.<br>   <br><br>   * **SMS**: SealSuite will send an SMS containing account activation information.<br><br>   * **Email**: SealSuite will send an email containing account activation information.<br><br>* **Send Later**: After selecting **Send Later**, you need to continue to configure the method of sending invitations, with options to choose either **SMS** or **Email**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **SMS**: SealSuite will send an SMS containing account activation information. After selecting **SMS**, you need to continue to configure the following fields:<br><br>      * **Mobile number**: Fill in the phone number to receive the account activation information.<br><br>      * **Send activation at**: Supports selection of **8:00 on account effective date** or **Custom date & time**.<br><br>   * **Email**: SealSuite will send an email containing account activation information. After selecting **Email**, you need to continue to configure the following fields:<br><br>      * **Email**: Fill in the email address to receive the account activation information.<br><br>      * **Send activation at**: Supports selection of **8:00 on account effective date** (UTC+8) or **Custom date & time** (UTC+8).<br><br>* **Do Not Send**: After selecting **Do Not Send**, the following impacts will occur:<br><br>   * (UTC+8) Users who fail to activate their SealSuite account on time will be unable to access related features of SealSuite.<br><br>   * The administrator must then export the initial password and either notify the user to activate their account or resend the activation notification from the user details page. |

   * Method Two: Batch import user information

      1. Click **Import/Export**.

      2. Select **Import** from the dropdown menu

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d74db590ee544d029b1bb0f53bcb8276~tplv-goo7wpa0wc-topic.webp)

      3. On the **Batch Import** page, download the **Excel template**.

      4. Open the **Excel template** locally, enter the user information, and save it.

      5. Return to the SealSuite Admin Console, on the **Batch Import** page, upload the locally edited **Excel template**.

      6. Configure the settings for sending user account activation information, and click **Confirm**.

         |**Configuration Item** |**Description** |
         |---|---|
         |**Activation Notification Setting** |Choose whether to send the activation message; supports choosing **Send Now**, **Send Later**, and **Do Not Send**. Configuration Instructions for different methods are as follows:<br><br><br>* **Send Now**: After selecting **Send Now**, you must continue to configure the method of sending invitations, with options to choose either **SMS** or **Email**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **SMS**: SealSuite will send an SMS containing account activation information.<br><br>   * **Email**: SealSuite will send an email containing account activation information.<br><br>* **Send Later**: After selecting **Send Later**, you need to continue to configure the **Invitation method** and **Send activation at**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **Invitation method**: You can choose **SMS** or **Email**.<br><br>      * **SMS**: SealSuite will send an SMS containing account activation information.<br><br>      * **Email**: SealSuite will send an email containing account activation information.<br><br>   * **Send activation at**: Supports selection of **8:00 on account effective date** (UTC+8) or **Custom date & time** (UTC+8).<br><br>* **Do Not Send**: After selecting **Do Not Send**, the following impacts will occur.<br><br>   * Users who fail to activate their SealSuite account on time will be unable to access related features of SealSuite.<br><br>   * The administrator needs to export the initial password and either remind the user offline to activate it or resend the activation notification on the user details page. |

# View user information

1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, go to **Identity** \> **Directory**.

3. Select a department from the hierarchy list on the left.

4. You can view member information individually or export data in bulk for offline review.

   * Option 1: View an individual member's details

      1. Locate the target member and click their name. A details drawer will expand from the right.

      2. Switch between the following tabs to view specific information.

         * **General**: View or edit the member's profile, such as mobile number, email, and roles.

            > **说明**

            > To protect privacy, the middle four digits of the mobile number are masked by default. Click the **Eye** icon to reveal the full number. This action is recorded in the audit logs.

         * **Permission**: View the member's application and resource permissions. The tabs available depend on the features activated for your organization. Select a tab to review the corresponding permissions.

            * **SSO**: View the names and URLs of applications the member can access through single sign\-on.

            * **Web application**: View the Zero Trust Web applications the member is authorized to access.

            * **VPN**: View the member's VPN resource permissions, including resource addresses, authorization methods, expiration dates, authorization status, and policy names. Filter the list to find a resource, then click **Details** to view its associated access policies. For instructions, see [View employee VPN resource access permissions](https://docs.byteplus.com/en/docs/sealsuite/docs-managing-access-control-rules_2#employee-vpn-resource-permissions).

         * **Devices**: View all devices currently logged in with this account. You can manually sign out any device by clicking the **Offline** button in the **Action** column to terminate its session.

         * **Attribute update log**: Review the change history of core attributes (e.g., Member ID, Name, Mobile, and Email). You can filter logs by attribute category, source, or time range.

   * Option 2: View and export members in bulk

      1. On the **Directory** page, click **Import/Export**.

      2. Select **Export** from the dropdown menu.

      3. In the **Select Export Scope** step, configure the following settings and click **Next Step**.

         * Select one or more account statuses.

         * Set the account effective date range.

         * Select departments and members.

      4. In the **Select fields** step, check the attributes you want to export and click **Next Step**.

         The list includes any **Custom Fields** you have defined. To learn how to manage these, see [Configuring custom attributes](https://docs.byteplus.com/docs/sealsuite/docs-configuring-custom-attributes).

      5. Choose your preferred file format (**CSV** or **Excel**).

      6. Click **Export** to generate and download the file.

# Activate user account

## Activate a single user account

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Select the specified department in the department structure list on the left.

4. Identify members within the department and set up the activation policy for user accounts using any of the following methods.

   * Method One: Set up the account activation strategy on the user details page

      1. Click on the specified user's name, then on the right side, click the **General** tab. In the upper right corner of the page, click the **SMS Invitation** button.

      2. On the **SMS Invitation** page, configure the activation strategy for the user's account, and click **Confirm**.

         |**Configuration Item** |**Description** |
         |---|---|
         |**Activation Notification Setting** |Choose whether to send activation information, with options to **Send Now**, **Send Later**, and **Do Not Send**. Configuration Instructions for each method are as follows:<br><br><br>* **Send Now**: After selecting **Send Now**, you must continue to configure the method of sending invitations, with options to choose either **SMS** or **Email**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **SMS**: SealSuite will send account activation information to the specified phone number via SMS.<br><br>   * **Email**: SealSuite will send the activation information for your account to the designated email address.<br><br>* **Send Later**: After selecting **Send Later**, you need to continue to configure the method of sending invitations, with options to choose either **SMS** or **Email**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **SMS**: SealSuite will send an SMS containing account activation information. After selecting **SMS**, you need to continue to configure the following fields.<br><br>      * **Mobile number**: The field is pre\-filled with the designated user's phone number, but still editable.<br><br>      * **Send activation at**: Supports selection of **8:00 on account effective date** (UTC+8) or **Custom date & time** (UTC+8).<br><br>   * **Email**: SealSuite will send an email containing account activation information. After selecting **Email**, you need to continue to configure the following fields:<br><br>      * **Email**: The email field is pre\-populated with the specified user's email address, but it can be edited if necessary.<br><br>      * **Send activation at**: Supports selection of **8:00 on account effective date** or **Custom date & time**.<br><br>* **Do Not Send**: After selecting **Do Not Send**, the following impacts will occur:<br><br>   * (UTC+8) Users who fail to activate their SealSuite account on time will be unable to access related features of SealSuite.<br><br>   * The administrator needs to export the initial password and either remind the user offline to activate it or resend the activation notification on the user details page. |

   * Method Two: Set up the account activation strategy in the member list

      1. Click **Action** on the right side of the target member column, then select **SMS Invitation**.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c0ce7a399fd482da4e9ce6e67b8d6b5~tplv-goo7wpa0wc-topic.webp)

      2. On the **SMS Invitation** page, follow the configuration instructions in Method One, and click **Confirm**.

## Activate user accounts in bulk

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Click the **Bulk Activation** button in the top\-right corner of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5801b398c1124ec5932954a2774d2819~tplv-goo7wpa0wc-topic.webp)

4. In the **Bulk Activation** dialog box, complete the following configuration, and click **Confirm**.

   |**Configuration Item** |**Description** |
   |---|---|
   |**Select scope** |Select the scope for this activation policy. You can apply it to **specific members** or **entire departments**. |
   |**Activation Notification Setting** |Set up the activation information sending strategy, with options to **Send Now** or **Send Later**.<br><br><br>* **Send Now**: After selecting **Send Now**, you must continue to configure the method of sending invitations, with options to choose either **SMS** or **Email**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **SMS**: SealSuite will send an SMS containing account activation information.<br><br>   * **Email**: SealSuite will send an email containing account activation information.<br><br>* **Send Later**: After selecting **Send Later**, you need to continue to configure the **Invitation method** and **Send activation at**.<br><br>   > **说明**<br>   <br><br>   > You need to configure the corresponding SMS gateway or email gateway to send activation information. If you have not yet completed the configuration, click **Configure SMS Gateway** or **Configure Mail Gateway** to complete configuration.<br>   <br><br>   * **Invitation method**: Supports **SMS** and **Email** options.<br><br>      * **SMS**: SealSuite will send an SMS containing account activation information.<br><br>      * **Email**: SealSuite will send an email containing account activation information.<br><br>   * **Send activation at**: Supports selection of **8:00 on account effective date** (UTC+8) or **Custom date & time** (UTC+8). |

5. In the **Bulk Activation** dialog box, ensure the information is accurate, and click **Confirm**.

# Manage existing user accounts

## Change user department

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Select the specified department in the department structure list on the left.

4. Find members within the department and change their departments through any of the following methods.

   * Method One: Adjust user department

      On the right side of the designated member column, click **Action**, then click **Change Department**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa71d4f68a014d79a08ba464d8fee2d0~tplv-goo7wpa0wc-topic.webp)

   * Method Two: Adjust the department for multiple members simultaneously

      In the member list, select the checkboxes next to the members who require a department change, then click **Change Department**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd1de371f36408d88aa5d1c2079247c~tplv-goo7wpa0wc-topic.webp)

## Lock user account

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Select the specified department in the department structure list on the left.

4. To lock a department member's account, locate the desired member, click on **Action** to the right of their name, and then select **Lock**.

   If a user is logged into SealSuite when their account is locked, they will be immediately logged out and prevented from further use of the account. At this point, if you click **Action** on the right side of the member again, only the **Restore use** button will be available. When a user with a locked account attempts to log in to the SealSuite client, an error message is displayed.

## Reset account password

Reset the member account password to a randomly generated initial password. After resetting the password, users who attempt to log in to SealSuite will be automatically logged out and must manually log in again using the new password.

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Select the specified department in the department structure list on the left.

4. To reset a department member's password, locate the member in the department list, click on **Action** to the right of their name, and then select **Reset Password**.

## Manage user resignation

Before processing a member's resignation, it's important to familiarize yourself with the following information:

* Source of user resignation information: SealSuite or third\-party software (such as LDAP, Lark, Workday).

   * If the resignation originates from SealSuite, please refer to this chapter to manage the resignation process within the SealSuite Admin Console.

   * If the resignation originates from third\-party software, you should sync it with the SealSuite Admin Console. If SealSuite does not directly receive the resignation information, the resigned user will still appear as available on SealSuite.

      * Lark: user resignation.

      * DingTalk: User resignation in contacts.

* Network access upon resignation: When a user resigns, the SealSuite Admin Console automatically disconnects the user's devices from both Wi\-Fi and wired networks.

* Data relating to resigned users cannot be altered: Once a user resigns, their user information in the Admin Console becomes uneditable and is only accessible for viewing.

* Interaction between resigned users and third parties immediately ceases: After a user resigns, all communication through short messaging service, email, and IM notification with third parties will immediately cease.

1. Log in to the SealSuite Admin Console.

2. Select **Identity** \> **Directory** in the left navigation bar.

3. Select the specified department in the department structure list on the left.

4. Identify the member who needs to depart from the department and facilitate their resignation through any of the following methods.

   * Method One: User resignation for a specified member

      On the right side of the specified member's column, click **Action**, and then click **User Resignation**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a16d584cfdf4afa9f2942c1124fd438~tplv-goo7wpa0wc-topic.webp)

   * Method Two: Batch user resignation

      Select the checkbox next to each member requiring resignation, then click **User Resignation** located at the bottom of the member list.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8387cd9cda5b4b84a851826582e2dcbc~tplv-goo7wpa0wc-topic.webp)

   > **说明**

   > After a user resignation, you can view and manage resigned members on the **Manage Terminated Employees** page. For specific information, please refer to [Managing resigned members](https://docs.byteplus.com/docs/sealsuite/docs-managing-resigned-members).
