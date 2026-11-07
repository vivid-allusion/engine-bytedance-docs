---
title: "Creating users"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-user"
---

A user is the identity carrier within the user pool, representing a natural person or service account that can log in to the system. In the user pool, you can manage individual users in a granular manner. Through the user's basic information, authentication status, and other attributes, you can centrally manage identities and their lifecycles.

## Prerequisites

A user pool has been created. For related operations, see [Creating user pools](https://docs.byteplus.com/en/docs/agentkit/create-user-pool).

## Create a single user

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management". On the page that appears, click the name of the target user pool.

3. On the user pool details page, switch to the "User" tab and click "Manage users".

4. Under the "Users" tab, click "Create User" and configure the user\-related parameters.

   |**Parameter** |**Description** |
   |---|---|
   |Username |Customize the username according to the naming rules prompted in the console. This name is the **unique identifier of the user**. |
   |Email |Set the user's email address for login or receiving notifications. Email format requirements:<br><br><br>* Must conform to the standard email format (for example, `xxx@example.com`).<br><br>* Other requirements are subject to the instructions displayed in the console.<br><br><br>Checking "Email verified" indicates that the email address has already been verified and does not require the user to confirm again.<br><br>> **warning**<br><br><br>> Whether the email is required depends on the user pool login attributes configured for [user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool).<br> |
   |Mobile number |Set the user's phone number for login or receiving verification codes. Mobile number format requirements:<br><br><br>* Must include the international country calling code, for example, `+86xxxxxxxx`.<br><br>* Must conform to the E.164 international number format (for example, a mobile number in the Chinese mainland is 11 digits) and contain no spaces or special characters.<br><br><br>Checking "Mobile number verified" indicates that the phone number has already been verified and does not require the user to confirm again.<br><br>> **warning**<br><br><br>> Whether the mobile number is required depends on the user pool login attributes configured for [user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool).<br> |
   |Temporary password |Set an initial password for the user according to the instructions displayed in the console. Users usually need to change this password after logging in for the first time. |
   |Additional attributes |Add custom additional attributes for the user. For example, Name, Gender, and Birthday.<br><br>Click "Add key\-value pair" to add a new attribute. Each attribute contains a **Key** and a **Value**. |
   |User metadata |A JSON\-format field for storing additional user information, supporting business\-specific customization, for example:`{"Department":"Finance"}`. |

5. Click "Confirm" to complete the creation.

## Importing users in batches

To batch create users, you can use the batch import feature.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management". On the page that appears, click the name of the target user pool.

3. On the user pool details page, switch to the "User" tab and click "Manage users".

4. Under the "Users" tab, click "Batch Import".

5. Select "Mobile number" or "Email" as needed, and then download the corresponding CSV template to your local device.

   > **tip**

   > The **Unique identifier policy** in the figure below is only used for information import matching and does not affect the employee login method.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc153e7881f113b44169941cc4be8a8c.png)

6. Open the downloaded template file and enter user information according to the column requirements of the template (such as `username`, `email`, `phone_number`, and `password`).

7. Upload the completed CSV file to the console. The system will validate the file. If `Data validation succeeded` is displayed, the file has been uploaded successfully.

   > **warning**

   * > Only `.csv` format files are supported for upload.

   * > Only a single file can be uploaded.

   * > The file size must not exceed 10 MB.

   * > Common reasons for import failure include: duplicate username/email/mobile number, password not meeting the policy, and incorrect CSV file format. Please read the error report carefully, correct the issues, and re\-upload.

## Manage users by department

After successfully creating users, you can create departments for them and manage users by department (or sub\-department) dimension.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management". On the page that appears, click the name of the target user pool.

3. On the user pool details page, switch to the "User" tab and click "Manage users".

4. Switch to the "Departments" tab to manage the user's departments.

   **Create departments**

1. Click "Create department".

   2. Configure the department\-related parameters.

      |**Parameter** |**Description** |
      |---|---|
      |Department name |Customize the department name, for example, `R&D department`. |
      |Parent department |If the department is not a top\-level department, you can associate it with a top\-level department.<br><br>This is an example of adding a top\-level department, so you can leave this field empty. |
      |External ID |Customize the department ID corresponding to the identity source, for example, `dept_rd`. When a user logs in from an external provider such as Feishu or DingTalk, the external ID is used to match local departments with third\-party ones.<br><br>> **warning**<br><br><br>> The external ID is the only credential for department synchronization and association between this system and external identity sources, and it cannot be modified after the department is created.<br> |

   3. Click "Confirm" to complete the creation.

   **Batch import departments**

1. Click "Import department".

   2. View the "Dataset format description" and download the spreadsheet template.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44f20d09b1acacf582298d292efd2a60.png)

   3. Open the downloaded template file and fill in the department information according to the column requirements in the template.

   4. Upload the completed CSV file to the console. The system will validate the file. If `Data validation succeeded` is displayed, the file has been uploaded successfully.

      > **warning**

      * > Only `.csv` format files can be uploaded.

      * > Only a single file can be uploaded.

      * > The file size cannot exceed 2 MB.

      * > If the upload fails, update the `.csv` file according to the system prompt and upload it again.

   **Add sub-department**

1. Find the target department in the department list. Click "Add sub\-department" in the "Actions" column on the right to add a sub\-department to the target department.

   2. Configure the relevant parameters for the sub\-department and click the "Confirm" button to complete adding the sub\-department. The parameter configuration is the same as that for **Creating department** in this topic.

   **Add employees**

1. Find the target department in the department list, and click "Add employee" in the "Actions" column on the right to add employees to the target department.

   2. In the pop\-up dialog box, select the target employees and click "Confirm addition" to complete the operation.

   **Edit department information**

Find the target department in the department list, click "`...` \> Edit" in the "Actions" column on the right to update the department information. Currently, only the department name, parent department, and department description can be modified. Updating the external ID is not supported.

   **Delete departments**

Find the target department in the department list, click "`...` \> Delete department" in the "Actions" column to delete the current department.

   > **warning**

   * > After the department is deleted, the department data cannot be recovered, and the employees in the current department no longer belong to the department.

   * > If the department has sub\-departments, all sub\-departments must be deleted before deleting the department itself.

   * > The operation of deleting a department does not delete department members.

## Manage users by user group dimension

After successfully creating users, you can create user groups for them and manage users by user group dimension.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management". On the page that appears, click the name of the target user pool.

3. On the user pool details page, switch to the "User" tab and click "Manage users".

4. Switch to the "User group" tab to manage the user's user groups.

   **Create user group**

1. Click "Create user group".

   2. Configure the department\-related parameters.

      |**Parameter** |**Description** |
      |---|---|
      |Term |Customize the user group name, for example `R&D department administrator`.<br><br>> **tip**<br><br><br>> The user group name cannot be modified after it is created.<br> |
      |Associate IAM role |Enter the TRN of the IAM role to associate the IAM role with the entire user group. All permissions on the role will be granted to all members of the group at once. For IAM role\-related operations and permission configuration, see [Role management](https://docs.byteplus.com/en/docs/iam/role-management).<br><br><br>* The IAM role TRN format is `trn:iam::${AccountId}:role/${RoleName}`.<br><br>* After members of the user group log in, the associated IAM role is included in the ID Token with the field `identity_userpool_preferred_role`. |

   3. Click "Confirm" to complete the creation.

   **Manage members**

1. Find the target user group in the department list, and click "Manage members" in the "Actions" column on the right to add or remove members for the target user group.

   2. Add or remove members as needed in the panel provided by the system.

   **Edit user group information**

Find the target user group in the user group list, and click "Edit" in the "Actions" column on the right to update the user group information. Currently, only the user group description and the associated IAM role can be modified. Updating the user group name is not supported.

   **Delete user group**

Find the target user group in the user group list, and click "Delete" in the "Actions" column on the right to delete the current user group.

   > **tip**

   > Deleting a user group does not delete members. However, the members no longer belong to the user group.

## Other operations

After successfully creating a user, you can view, edit, or delete users.

* **View**: The user list displays the basic profiles and account statuses of all users in the current user pool, including key information such as username, user ID, name, email, and the last login method. It is suitable for quickly searching and locating target users when verifying user identities, troubleshooting login anomalies, counting account scale, or assisting users in recovering their accounts.

* **Edit**: Click "Edit" in the "Actions" column of the user list to modify the user's email, mobile number, additional attributes, and user status (Enabled/Disabled). You can also manually mark the user's email or mobile number as "Verified" here.

* **Delete**: Click "Delete" in the "Actions" column of the user list. This is an irreversible action. The user's personal information and all associated sessions will be permanently deleted.
