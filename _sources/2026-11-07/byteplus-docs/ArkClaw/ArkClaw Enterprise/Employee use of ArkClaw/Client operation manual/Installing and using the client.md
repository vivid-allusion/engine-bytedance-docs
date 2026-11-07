---
title: "Installing and using the client"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Installing_and_using_the_client"
---

The ArkClaw client is a desktop client that allows you to access and use ArkClaw on local devices. The client is compatible with Windows and macOS, and supports file upload, download, deletion, and other operations in the local environment, helping you manage local files and interact with ArkClaw more efficiently.

## Prerequisites

* **You have access to ArkClaw**. If you have no permission to use ArkClaw, contact your administrator to grant permissions.

* **You have obtained the ArkClaw login link**. If you have not obtained the ArkClaw login link, contact your administrator to obtain it. For information about how to obtain the link, see [Viewing space configurations](https://docs.byteplus.com/en/docs/ArkClaw/Space_information#ftsmTKKb).

* **You have ** [applied for an ArkClaw instance](https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_?lang=en) **.**

## Step 1: Download and install the client

1. Download the client.

   > If your enterprise administrator has already provided you with an installation package download link, skip this step and proceed to installation.

   1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

   2. Click the "Download client" button in the upper\-right corner of the page. The system will automatically download the installation package for your operating system.

2. Install the client.

   **macOS**

1. Locate the downloaded `.dmg` installer on your computer and double\-click to open it.

   2. In the installation window that appears, drag the **ArkClaw** application to the **Applications** folder.

   3. Open the **Applications** folder, locate **ArkClaw**, and double\-click it to start the client.

   4. If a security prompt appears, follow the on\-screen instructions to confirm and proceed.

      > If macOS restricts the application from launching due to security policy, confirm in the system dialog box to open it, or go to **System Settings** to allow the application to run.

   **Windows**

1. Locate the downloaded .exe installer on your computer and double\-click to run it.

   2. Follow the installation wizard to install the client.

   3. Once the installation is complete, launch the client by double\-clicking the desktop shortcut or clicking **ArkClaw** in the **Start menu**.

## Step 2: Log in to the ArkClaw client

1. Open the ArkClaw client, enter the **ArkClaw login link**, and click "Bind enterprise employee login link" **.**

2. On the displayed page, click the "Try now" button.

3. In the browser link that opens, click "Open ArkClaw" to log in to the ArkClaw client.

4. After you log in successfully, you can use ArkClaw in the client.

> **tip**

> The ArkClaw client and the web version differ in the features they support. Refer to what is actually displayed in the ArkClaw client as the definitive reference.

* > [Complete web capabilities](https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_usage_overview)

* > [Client operation manual](https://docs.byteplus.com/en/docs/ArkClaw/Client_operation_manual)

## Step 3 (Optional): Access local computer files

If you want to access and operate local files in Cloud assistant mode, use "Device management" to authorize the device and configure local file permissions for the current instance. In the "Device management" section, you can also view the authorization status of the current device, handle pending authorization requests for local device access, and manage ArkClaw's access to local files after authorization is complete.

### 1. Device authorization

1. Switch to the target ArkClaw.

2. Click the "Enter project space \> Add project \> Pair" button at the bottom of the chat box.

   > This step does not actually add a project. It only navigates to the device authorization page.

3. In the **Pending local authorization request** section **,**  verify that the device information is correct, and click "Click to authorize and enable read\-write access to local computer files" **.**

4. In the dialog box that appears, click "Authorize" to authorize the local device.

   > This operation authorizes only the current device. The local capability plugin now handles command approval, so you do not need to modify the OpenClaw gateway configuration. The instance does not restart for this reason. Keep the ArkClaw client and this page open until the authorization is complete.

5. After authorization is complete, the current device is ready for file operations only when the page shows the "The local device is connected" message and the device status is both **Authorized** and **Online**.

   Next to the device name, you can also place the pointer over the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3a89182fd7d53afdd5d5f45cfeba21b8.png) icon to view detailed information about the local device.

### 2. Configure local file permissions

Local file permissions limit the scope of local files that ArkClaw can access. Only authorized directories can be used for file read\-write operations in the current conversation. Commands are executed within a restricted sandbox. If permissions are insufficient, related operations will be directly denied.

* **Global default permission**: The fallback permission configuration that applies to all sessions not associated with any project space. Conversations initiated directly in ArkClaw follow this permission setting by default.

* **Project permission**: A permission configuration set separately for sessions associated with a specific project space. Conversations initiated within a project space follow this permission setting and are not affected by the global default.

**Global default permission**

Applies to sessions not associated with a project space. Commands are executed under this setting for all conversations without an associated project.

**Procedure**

On the **File permissions** tab, select a permission mode from the drop\-down list to the right of Global default module.

|**Permission mode** |**Description** |
|---|---|
|Read\-only |All files are read\-only. Modifying, adding, or deleting files is not allowed. Directories cannot be added manually in this mode. |
|Full access |Provides read\-write access to all files on the device, with no per\-directory authorization required. Suitable for scenarios with low data sensitivity where quick access to all local files is needed. Enable this mode only when you trust the current task.<br><br>> **warning**<br><br><br>> When "Full access" is selected, terminal commands generated by ArkClaw are allowed directly (the "Deny" or "Require confirmation" rule configured on the "Device management" page still applies).<br> |
|Custom |This mode follows the principle of least privilege and provides precise control using a directory allowlist. Only authorized directories and their subdirectories support file reads and writes, and operations in unauthorized directories are blocked and rejected. For details, refer to [Managing local file access permissions](https://docs.byteplus.com/en/docs/ArkClaw/Managing_local_file_access_permissions). |

**Project permission**

Applies to scenarios where permissions need to be configured separately for individual project spaces. Each project can be configured independently without affecting others.

1. In the left navigation pane, click the "Initiate Task" button to go back to the ArkClaw conversation page.

2. Click "Enter project space \> Add project" below the ArkClaw input box, and select the local folder you want to allow ArkClaw to access.

3. After the project is added, click the "Request approval mode \> Current file system permission for sessions: xxxx" button at the bottom of the chat box.

4. In the target project configuration section, set the file system permissions for sessions of the current project.

   |**Permission mode** |**Description** |
   |---|---|
   |Workspace write permission |The default mode that grants read\-write access to the current project workspace directly, without the need to manually add a directory. |
   |Read\-only |All files are read\-only. Modifying, adding, or deleting files is not allowed. Directories cannot be added manually in this mode. |
   |Full access |Provides read\-write access to all files on the device, with no per\-directory authorization required. Suitable for scenarios with low data sensitivity where quick access to all local files is needed. Enable this mode only when you trust the current task.<br><br>> **warning**<br><br><br>> When "Full access" is selected, terminal commands generated by ArkClaw are allowed directly (the "Deny" or "Require confirmation" rule configured on the "Device management" page still applies).<br> |
   |Custom permissions |This mode follows the principle of least privilege and provides precise control using a directory allowlist. Only authorized directories and their subdirectories support file reads and writes, and operations in unauthorized directories are blocked and rejected. For details, refer to [Managing local file access permissions](https://docs.byteplus.com/en/docs/ArkClaw/Managing_local_file_access_permissions). |

### 3. (Optional) Configure the permission mode for ArkClaw to execute terminal commands on your local device

When executing terminal commands locally, ArkClaw supports flexible permission control through command approval modes. You can choose to confirm each execution manually, grant full access directly, or automatically execute commands based on preset rules, meeting different security and efficiency requirements.

1. Click the "Request approval mode" button at the bottom of the chat box.

2. In the drop\-down list, select the permission mode for ArkClaw to execute terminal commands on the local device.

   * **Request approval mode (default)** : A confirmation prompt appears before each terminal command is executed locally.

   * **Intelligent approval mode**: Automatically identifies high\-risk commands and requests approval only when necessary.

   * **Full access**: Grants unrestricted access to the file system and command execution. Enable this mode only when you trust the current task.

### 4. Work with local files using the desktop client

After adding a project and obtaining read\-write permissions for local files, you can work with local files in your conversations.

> **tip**

> If the "**Local file read\-write access is temporarily unavailable**" message appears, click "Fix now" and retry the operation after the fix is complete.

1. Click the "New conversation" button next to the target project name.

2. In the conversation input box for the target project, start a conversation task.

   Example: Generate a ranking of the top 10 movies of 2025 on my desktop.
