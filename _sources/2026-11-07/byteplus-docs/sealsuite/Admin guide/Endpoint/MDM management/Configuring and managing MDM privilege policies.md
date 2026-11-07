---
title: "Configuring and managing MDM privilege policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-and-managing-mdm-privilege-policies"
---

To enforce the Principle of Least Privilege and enhance endpoint security, use the Privilege Management feature in SealSuite MDM for granular control over local accounts. This guide provides comprehensive instructions on creating and deploying privilege policies, configuring self\-service elevation workflows for users, and auditing all elevation events for compliance.

<span id="adb8926c"></span>
## Feature Overview

Privilege Management in SealSuite MDM allows organizations to exercise granular control over local login accounts on endpoint devices. By adhering to the **Principle of Least Privilege (PoLP)** , administrators can assign specific permission levels to different users or devices, ensuring that only authorized personnel can perform sensitive system\-level operations.

Key capabilities include:


* **Access Restriction**: Prevent unauthorized changes to system settings.

* **App Permission Governance**: Centrally manage application access to hardware and data, such as cameras, microphones, and contacts.

* **Administrator Control**: Reclaim local administrator rights from standard users while providing a secure path for temporary elevation.


<span id="d9ede397"></span>
## Adding a Privilege Policy

Follow these steps to create and deploy a new privilege policy for Windows or macOS devices.


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Privileges**.

3. Click  **+ Add Privilege Policy** and select either **macOS** or **Windows**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bcf49dc0fdb4220b688c3bcbd4411cb~tplv-goo7wpa0wc-image.image) </span>

4. Configure the parameters based on the table below:

   
   |Section |Parameter |Required |Description |
   |---|---|---|---|
   |**General** |**Name** |Yes |A unique identifier (up to 50 characters). |
   ||**Description** |No |Brief notes regarding the policy's purpose. |
   |**Privilege Policy Configuration** |**Administrative Permission Removal** |No |Enable this to remove local administrator privileges from users. Specify an **Admin allowlist** for accounts that should retain permanent admin access. |
   ||**Defined Rules** |No |(**Windows Only**) Define specific processes (via Path, Publisher, or Hash) that are automatically granted elevation within a set time window. |
   ||**Self\-Service Elevation** |No |(**Windows Only**) Allows users to manually request temporary admin rights for specific tasks. |
   ||**Preset Reasons** |No |(**Windows Only**) Create a list of reasons (e.g., "Install/Uninstall Software") for users to select when requesting elevation. |
   ||**Forcing users to add reasons for privilege elevations.**  |No |(**Windows Only**) If enabled, users must provide a detailed text description before they can submit an elevation request. |
   ||**Placeholder for Client Pop\-up Reason Input** |No |(**Windows Only**) Customize the hint text shown in the client's elevation dialog (e.g., "Please explain why this software is required"). |
   |**Scope** |**Assignments** |Yes |Select users (by Department/Role) or devices (by Group/ID). |
   ||**Exclude object** |No |Specify users or devices that should be exempt from this policy. |
   

5. Click **Save** to keep as a draft, or click **Deploy** to activate the policy immediately.


<span id="35d95aa9"></span>
## Managing Privilege Policies

Administrators can monitor and maintain active policies to ensure they remain aligned with organizational security standards.

<span id="bf7bd56b"></span>
### 1. Monitoring Policy Status


1. Navigate to the **Policies** tab.

2. Filter by **OS**, **Name**, or **Status** (Enabled/Disabled).

3. Click **View** (available for "Deployed" policies) to access:

   * **Deployment Status**: Real\-time compliance data for all target devices. You can **Refresh** for the latest data or **Export** the device list.

   * **Configuration Info**: A summary of all active rules within the policy.


<span id="f6e68422"></span>
### 2. Modifying and Deleting Policies


* **Edit**: Click **Edit** to adjust rules or scopes.

   * *Scope Logic*: If the scope expands, new devices receive the policy immediately. If the scope shrinks, devices removed from the scope will retain their previous state until the policy is manually revoked or updated.

* **Delete**: To delete a policy, you must first change its status to **Inactive** (Revoke). Click **Delete** in the action column to remove the record permanently.


<span id="5575e6fe"></span>
## Executing Elevation on Windows

When a Windows user needs to perform a task requiring higher permissions (such as installing software or modifying system files), they can utilize the **Self\-Service Elevation** workflow.

<span id="e63b8fb5"></span>
### User Workflow


1. On the Windows device, locate the application that requires admin rights.

2. Right\-click the application icon and select **Elevation Run** (or "Run with Elevated Privileges") from the context menu.

3. In the pop\-up dialog, select a reason from the dropdown and provide any mandatory justification.

4. Click **Elevation Run** to execute the application with administrative privileges.

   * *Note: If a "Default Elevation Rule" exists for the app, the user will not see a pop\-up and the app will elevate silently.* 


<span id="0d0b76e1"></span>
## Auditing Elevation Logs

Auditing elevation events is critical for monitoring security compliance and identifying potential unauthorized activity.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0eea2ed718749a5b6441b491b1375bc~tplv-goo7wpa0wc-image.image) </span>


1. Navigate to **Endpoint** \> **MDM** \> **Privileges** \> **Elevation Records**.

2. Filter the logs by **OS**, **Elevation type** (Default Rule vs. Self\-Service), **Date Range**, or **Policy Name**.

3. Click **View** on a specific log entry to see detailed information, including the specific process elevated and the user's justification.

4. Click **Export** to download the logs as a `.csv` file for external reporting or forensic analysis.
