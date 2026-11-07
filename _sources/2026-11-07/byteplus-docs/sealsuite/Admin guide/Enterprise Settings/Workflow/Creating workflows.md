---
title: "Creating workflows"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/creating-workflows"
---

The Workflow module allows you to create automated tasks that streamline administrative processes, reduce manual errors, and ensure consistent enforcement of your business rules.

<span id="7927b3f7"></span>
# How It Works

The Workflow module is an enterprise\-grade solution for automating complex operational tasks. It provides a centralized platform to create, monitor, and manage workflows and their associated data, bringing transparency and efficiency to your business processes.

By building automated task flows, you can simplify day\-to\-day operations, minimize human error, and boost productivity. The module tracks every workflow execution, providing detailed run logs and real\-time analytics to help you identify bottlenecks and opportunities for improvement.

<span id="7946bb6c"></span>
# Common Use Cases

SealSuite provides a variety of workflow templates to address common business needs. Key scenarios include:


* **Employee Lifecycle Management:**  Automate the entire identity and access lifecycle, from onboarding a new hire to offboarding a departing employee, ensuring timely and compliant HR processes.

* **Bulk Account Management:**  Use workflows to bulk\-lock user accounts during temporary leaves of absence (e.g., long\-term vacation, training) to prevent unauthorized access. For departing employees, workflows can bulk\-delete accounts and automatically clean up associated data based on your retention policies.

* **Self\-Service Access Requests:**  Empower employees to request access to applications and resources through a self\-service portal, reducing the burden on your IT department.



|**Workflow Template** |**Use Case** |
|---|---|
|**Application Access Approval** |Allows users without permission to request access to an application that is scoped to "specific users." |
|**Application Autofill Password Approval** |Allows users to request access to the credentials for a specific Password Vaulting application. |
|**VPN Resource Access Approval** |Allows users to request access to specific VPN network resources (URLs or IPs) for themselves or others. |
|**File Sharing Whitelist Approval** |Allows users to request a temporary exception when a file transfer is blocked by a DLP policy. |
|**Removable Device Whitelist Approval** |Allows users to request read\-only or read/write access for a specific external device. |
|**Desktop Application Whitelist Approval** |Allows users to request an exception when a file transfer is blocked by a channel control (DLP) policy. |
|**DLP Evidence Request** |Allows users to request access to the forensic evidence (file and screenshot) associated with a specific DLP alert ID. |
|**Administrator Access Approval** |Allows users to request an administrator role and management scope for a temporary period. |
|**User Role Request Approval** |Allows users to request assignment to a static role for themselves or others. |
|**Expiration Reminder of Dumb Terminals** |Automatically notifies the device owner or an administrator when a dumb terminal's access is about to expire. |


<span id="0b7098f7"></span>
# How to Create a New Workflow


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Workflow**.

3. In the top\-right corner, click  **+ Add New Workflow**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0179ab080ef4279b8f9b71ee82b3096~tplv-goo7wpa0wc-image.image) </span>

4. Select a template that matches your use case and click **Confirm**.

5. Follow the steps in the workflow builder.

   The example below uses the "**Onboarding New Hire**" template, but the process is similar for all templates.

   1. **Configure Basic Information:** 

      
      |**Parameter** |**Description** |
      |---|---|
      |**Workflow name** |A descriptive name for the workflow. |
      |**Workflow description** |A brief summary of what the workflow does. |
      |**Trigger Event** |The event that starts the workflow. This is pre\-defined by the template and cannot be changed (e.g., "A new account is created"). |
      |**Workflow scope** |Define which users this workflow applies to using conditions based on **Department**, **Role**, or **User Custom Attributes**. |
      

   2. **Configure Tasks:**  Define the actions the workflow will perform.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Configure User Roles** |Automatically assign roles to the new user. Click **Edit** to select the roles. |
      |**Generate Wi\-Fi Account and Password** |Automatically create Wi\-Fi credentials for the new user. |
      |**Add New Task(s)**  |Click this to add custom steps to your workflow, such as sending a notification via **Email** or a **Third\-Party IM Bot**. |
      

   3. **Review and Submit:**  Confirm your configuration and click **Submit** to activate the workflow.

6. (Optional) You can enable or disable any workflow from the main workflow list at any time using the toggle switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab4c7cbca78944daa880bed0fe9a95b4~tplv-goo7wpa0wc-image.image) </span>


<span id="83247d38"></span>
# Understanding Key Workflow Templates

While all workflows share common elements like a name, scope, and approval nodes, each template has unique parameters tailored to its specific purpose. This section details the key settings for the most important workflow templates.

<span id="0b63e812"></span>
## 1. Application Access Approval

**Purpose:**  Allows users to request access to applications they are not currently authorized to use.

This workflow is typically used for applications where Authorization is set to  **"Restricted"**  and the  **"Allow employees to apply"**  option is turned on.

**Unique Configuration:** 


|**Parameter** |**Description** |
|---|---|
|**Request target type** |Configure who can make requests: for **themselves**, for **their entire department**, or **others**. |
|**Target Applications** |Define which applications this workflow applies to.<br><br><br>* **All:**  The workflow will apply to all current and future applications that have access requests enabled.<br><br>* **Selected:**  Select the individual applications that should use this workflow for access requests. |
|**Request Approval: Approver Type** |In addition to standard approver types, this template includes:<br><br>&nbsp;<br><br>\* **Application Owner:**  Assigns the approval task to the designated administrator(s) of the requested application. |
|**Additional Tasks** |This template supports integration with **Feishu**/**Lark Approvals**, allowing approvers to manage requests directly within /FeishuLark. |


<span id="3e3c9107"></span>
## 2. File Sharing, Desktop Application, and Removable Device Whitelist Requests

**Purpose:**  Allows users to request a temporary exception when a Data Loss Prevention (DLP) policy blocks a file transfer, the use of a specific application channel, or a removable device.

> These three templates share a nearly identical configuration.


**Unique Configuration:** 


|**Parameter** |**Description** |
|---|---|
|**Request target type** |Configure who can make requests: for **themselves** or **others**. |
|**Use existing event id** |Determines how users submit requests.<br><br><br>* **Yes:**  Requires the user to provide the **Alert ID** from their client's Alert Center. This automatically links the request to the specific blocked event, providing the approver with full context (e.g., the exact file and channel).<br><br>* **No:**  Requires the user to manually upload the file and specify the channel they wish to use, as there is no associated alert. |
|**Source Channel** (For File Sharing) |Define the specific data transfer channels (e.g., USB, Slack, Email) that users can request an exception for. |


<span id="7048e629"></span>
## 3. DLP Evidence Request

**Purpose:**  Allows a user to request access to the forensic evidence (the original file and a screenshot) associated with a DLP alert that they triggered.

**Unique Configuration:** 

This workflow uses a standard approval process. Its uniqueness lies in its trigger and outcome.


* **Trigger:**  The user must submit a request with a valid **DLP Alert ID**.

* **Outcome:**  Upon approval, the system automatically grants the user temporary access to download the forensic files associated with that specific alert directly from the request ticket details.


<span id="e533aa53"></span>
## 4. VPN Resource Access Approval

**Purpose:**  Allows users to request access to specific VPN network resources (URLs or IPs) that they are currently denied access to.

**Unique Configuration:** 


|**Parameter** |**Description** |
|---|---|
|**Request target type** |Configure who can make requests: for **themselves**, for **their entire department**, or **others**. |
|**Request Approval: Approver Type** |This template uses standard approver types like **Role Group** (e.g., IT Admins) or **Appointed User**. |
|**Additional Tasks** |Supports integration with **Feishu (Lark) Approvals**. |


<span id="6d73c0a4"></span>
## 5. Bulk User Account Lock

**Purpose:**  Automates the locking of multiple user accounts based on a schedule or manual trigger. This is useful for managing users on extended leave.

**Unique Configuration:** 


|**Parameter** |**Description** |
|---|---|
|**Trigger Method** |Choose how the workflow is initiated.<br><br><br>* **Manual:**  An administrator must manually run the workflow from the Admin Console.<br><br>* **Scheduled:**  The workflow runs automatically based on a defined start time, end time, and frequency. |
|**Workflow Scope** |**Crucial:**  The users defined in this scope will have their accounts **locked** when the workflow runs. **Use extreme caution when scoping by department.**  |
|**Lock User Account** |The core action is **Account Lock**, which is automatic and requires no configuration. |


<span id="082466e4"></span>
## 6. Expiration Reminder of Dumb Terminals

**Purpose:**  Automatically sends a notification to the device owner or an administrator before a dumb terminal's access is scheduled to expire.

**Unique Configuration:** 


|**Parameter** |**Description** |
|---|---|
|**Trigger Event** |The workflow is triggered a specified number of days **before the expiration date** of a dumb terminal. You can configure this lead time (default: 7 days). |
|**Workflow Scope** |Define which dumb terminals this workflow applies to by selecting their **device type** or specific **dumb terminals**. |
|**Primary Task** |The main task is **Send User Notification**, which sends a customizable alert to the device's registered owner via Email or a Third\-Party IM Bot. You can also add a secondary task to notify an administrator. |


<span id="fa31a150"></span>
## **7. Request macOS Administrator Privileges**

This workflow template allows macOS users to request temporary local administrator privileges via a self\-service process. Once approved, SealSuite automatically grants administrative rights to the user's device for a specified duration and revokes them immediately upon expiration. This balances operational flexibility for power users with the security principle of least privilege.

<span id="73298c3d"></span>
### Prerequisites & Constraints


* **Client Version**: Supported on SealSuite macOS client version **3.2.14** or higher.

* **Single Instance Policy**: Only **one** "Request macOS Administrator Privileges" workflow can be active at a time. This workflow maps directly to the unique "Request Admin Privileges" entry in the client's **Toolbox**.


<span id="6650712c"></span>
### Configuration Parameters


|**Section** |**Parameter** |**Description** |
|---|---|---|
|**Basic Info** |**Workflow name** |Enter a clear, descriptive name for the workflow. |
||**Workflow description** |Briefly explain the purpose of this workflow (e.g., "Temporary admin access for software installation"). |
||**Trigger Event** |Fixed as **The user submits a request for macOS admin privileges ticket**. This cannot be modified. |
||**Request form setup** |* **Request target type**: Limited to **Self** (users can only request privileges for their own devices).<br><br>* **Authorization time**: Set the maximum time the admin rights will remain active (Default: 600 seconds). Privileges are automatically revoked once the timer expires. |
||**Workflow scope** |Define which users will see the "Request Admin Privileges" option in their SealSuite client **Toolbox**. You can set criteria based on departments, roles, or specific user attributes using AND/OR logic. |
|**Configure Tasks** |**Request approval** |Define the approval logic for the request.<br><br><br>* **Approcal stage name**: Customize how this stage appears in the workflow (e.g., "IT Manager Approval").<br><br>* **Approval Type**: Choose **Manual**, **Auto\-Approve**, or **Auto\-Reject**.<br><br>* **Approval result notification**: (Optional) Configure email or IM bot alerts to notify the applicant of the approval result. |
||**Grant Privileges** |**Automatic Task**: No manual configuration required. SealSuite automatically executes the command to elevate the user to a local admin once the request is approved. |
||**Additional Tasks** |(Optional) Add extra steps such as:<br><br><br>* **Multi\-stage Approvals**: Add more approval nodes.<br><br>* **Third\-party Integration**: Sync approval with **Lark (Feishu) Approval**.<br><br>* **CC Notifications**: Send "view\-only" copies of the request to specific admins, the user’s direct manager, or other stakeholders for audit purposes. |


<span id="1b8b2cf2"></span>
### User Experience

Once the workflow is enabled, eligible users will see the **Request Admin Privileges** option in their SealSuite client's **Toolbox**. After submitting a request and receiving approval, the user’s local account is temporarily added to the administrators' group.
