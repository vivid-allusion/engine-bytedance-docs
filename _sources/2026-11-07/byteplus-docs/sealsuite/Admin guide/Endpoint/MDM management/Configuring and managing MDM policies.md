---
title: "Configuring and managing MDM policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-and-managing-mdm-policies"
---

To centrally manage and secure your organization's mobile devices, you can use SealSuite's Mobile Device Management (MDM) feature. This guide provides instructions on creating policy files, enrolling clients (with a specific focus on macOS), and performing lifecycle management tasks such as modifying, updating, and deleting policies.

<span id="02667f18"></span>
## Feature Overview

Mobile Device Management (MDM) is an enterprise\-grade technology used to monitor, manage, and secure mobile devices such as smartphones, tablets, and laptops. SealSuite’s MDM module provides a variety of built\-in policies, including password enforcement, screen saver settings, and guest account management. By leveraging MDM, enterprises can ensure device and data security while improving operational productivity and compliance.

<span id="8e39d7b3"></span>
## Operational Workflow

To ensure MDM is successfully implemented and managed within your organization, follow these steps:


1. **Create Policy Files**: Define specific management rules in a new policy file. See [Adding Policy Files](https://docs.byteplus.com/docs/sealsuite/configuring-and-managing-mdm-policies#9cd148ae).

2. **macOS Client Enrollment**: Unlike other platforms, macOS requires the installation of a configuration profile. Once enrolled, device status is visible in the Admin Console. See [macOS Client Enrollment](https://docs.byteplus.com/docs/sealsuite/configuring-and-managing-mdm-policies#59a9e5ed).

3. **Manage Existing Policies**: Perform maintenance tasks such as searching, modifying, or deleting policies.

   * **Query Policy Info**: View policy details and deployment range.

   * **Modify Configuration**: Adjust policy items based on updated security requirements.

   * **Update Policy Status**: Enable or disable policies to control their real\-time enforcement.

   * **Delete Policy Files**: Remove obsolete policies.


<span id="9cd148ae"></span>
## Adding Policy Files

To deploy security rules, you must create a policy file and associate it with target employees or devices. Once a policy is successfully deployed, eligible users will be prompted to install the necessary configuration on their SealSuite clients.


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Policies**.

3. Click  **+**  **Add Policy File** in the top right corner and select the target operating system: **Windows**, **macOS**, **Linux**, or **iOS/iPadOS**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9262a53aa954504a7c898b72b573ee0~tplv-goo7wpa0wc-image.image) </span>

4. Configure the parameters based on the table below:

   
   |Configuration |Description |
   |---|---|
   |**General Info** |* **Policy Name** (Required): A unique identifier for the policy (up to 50 characters).<br><br>* **Description** (Optional): Administrative notes for the policy. |
   |**Policy Configuration** |1. Click  **+ Add Policies**.<br><br>2. In the pop\-up, check the specific rules you wish to enforce (e.g., Password policy, Screen lock) and click **Confirm**.<br><br>3. Configure the specific values for each selected item as prompted. |
   |**Assignments** |Specify the target audience by selecting one or more **Users** (Department/Role) or **Devices** (Group/ID). |
   |**Exclude Object** |Define exceptions to the assignment scope.<br><br><br>1. Toggle the **Exclusion Objects** switch.<br><br>2. Click **Add Exclusion Objects** to specify users or devices that should be exempt from this policy. |
   

5. (Optional) Review the selected policy items. You can enable, disable, or remove specific items as needed.

6. Click **Save** to keep the policy as a draft, or click **Deploy** to activate it immediately.


<span id="59a9e5ed"></span>
## macOS Client Enrollment

Once a policy is deployed, users on macOS must install a configuration profile. When a user logs into the SealSuite client (version 3.0.2 or higher) and is within the MDM authorization scope, they will be prompted to enroll.


* **Platform Note**: Only macOS requires manual profile installation. Windows and Linux clients are managed automatically upon login.

* **Conflicts**: If a macOS device is linked to Apple Business Manager (ABM) or has an existing MDM profile from another vendor or SealSuite tenant, the user must manually remove the old profile before enrolling.


<span id="d1daa101"></span>
### Enrollment Procedure


1. After the user logs in to the client, a "Configuration Profile Check" window appears. Click **Install Now**.

2. In the system **Profiles** dialog, click **Install** for the **Enrollment Profile**.

3. Click **Enroll** in the confirmation dialog.

4. Enter the local administrator password and click **Enroll** to complete the MDM registration.


<span id="730a53ce"></span>
## Managing Policy Files

You can perform lifecycle operations on existing policies to adapt to changing business needs.

<span id="96abfdd1"></span>
### 1. Viewing Policy Information


1. Go to **Endpoint** \> **MDM** \> **Policies**.

2. Use the search bar to filter by:

   * **OS**: Windows, macOS, Linux, or iOS/iPadOS.

   * **Name/Description**: Keyword search.

   * **Status**: Active or Inactive.

3. Click **View** on a target policy to see:

   * **Deployment Status**: A breakdown of devices and their current compliance state. You can **Refresh** for real\-time data or **Export** the device list.

   * **Configuration Info**: The specific rules enforced by the policy and the Configuration Profile ID.


<span id="c3129fbb"></span>
### 2. Modifying Policy Configurations


1. Click **Edit** on the target policy in the list.

2. Adjust basic information, policy items, or assignment scopes.

3. Click **Deploy** to push the updates.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Impact of Modifications:</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>Unchanged Scope</strong>: All endpoints are redeployed with the new policy, overwriting the previous version.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Expanded Scope</strong>: Existing endpoints are updated; new endpoints receive the policy for the first time.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Narrowed Scope</strong>: Endpoints remaining in scope are updated.</div>



<span id="e651c280"></span>
### 3. Updating Policy Status

You can toggle a policy's active state. When a policy is changed to **Revoke Deployment**, monitoring and enforcement stop, and the policy is removed from endpoints. For example, revoking a "USB Disable" policy will immediately restore USB access to the 100 targeted devices.


1. In the **Policies** list, locate the **Effective** **Status** column.

2. Click the toggle switch to enable or disable the policy.


<span id="ae5cd2a8"></span>
### 4. Deleting Policy Files


* **Risk**: Deletion removes the policy and related detection tasks from the console but does not guarantee the policy is revoked from the endpoint.

* **Best Practice**: Change the policy status to **Revoke Deployment** first. Confirm that all endpoints have successfully revoked the policy (visible in **Endpoint Details**) before performing the final deletion. You can view the specific MDM policy status on the Endpoint Details page; for more information, see [Managing endpoint devices](https://docs.byteplus.com/docs/sealsuite/docs-viewing-device-information).

1. In the **Policies** list, locate the target policy.

2. If the status is "Active," click the toggle to revoke it first.

3. Click **Delete** in the Action column.
