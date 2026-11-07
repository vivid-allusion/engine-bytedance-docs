---
title: "Configuring multi-user login in Windows 2019 instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configure_multi-user_log_in_in_Windows_2019_operating_system_instance"
---

Windows Server operating system supports the multi\-user login feature, which allows multiple users to simultaneously connect to a server through Remote Desktop Protocol (RDP). Each user has a separate session environment, enabling them to run different applications and tasks without mutual interference.

<span id="ocIUxQTw"></span>
## Applicable scenarios


* **Remote office and collaboration**

   Team members can log in to the server remotely at the same time to access its resources, applications, or development environments. This helps distributed teams collaborate on tasks hosted on the same server.

* **Virtual Desktop Infrastructure (VDI)** 

   It provides a unified desktop experience for multiple users while reducing the cost of virtualization solutions.

* **Testing and training environments**

   Developers and testers can log in to the server simultaneously for project development, debugging, and other tasks.


<span id="9jdylAP2"></span>
## Usage notes


* The inbound rules of the ECS instance's security group allow TCP traffic on port `3389`. [Learn more](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).

* The ECS instance has been [associated with an Elastic IP (EIP)](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* Ensure that the ECS instance has sufficient bandwidth to prevent lagging or login failures caused by high load from concurrent operations by multiple users.


<span id="h6e8uRHE"></span>
## Procedure

Taking Windows Server 2019 as an example, this section introduces the procedure for configuring multi\-user login. Please refer to the actual operating system path for your setup.

<span id="c5zrTygl"></span>
### Step 1: Install the Remote Desktop Services (RDS) role


1.  [Log in to the target server](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon and select "Server Manager".

3. In the left directory tree, select "Dashboard" and click the "Quick Start \> Add Roles and Features" button.

4. Read the precautions and click the "Next Page" button.

5. Select "Role\-based or feature\-based installation" and click the "Next Page" button.

6. Select "Select server from server pool" and check the current server, then click the "Next Page" button.

7. In the "Roles" list, check "Remote Desktop Services," keep the other content unchanged, and click the "Next Page" button.

8. In "Remote Desktop Services," click the "Next Page" button.

9. Keep the configuration in the "Features" list unchanged and click the "Next Page" button.

10. In the left directory tree, select "Role Services", and then select "Remote Desktop Session Host" and "Remote Desktop Licensing" in the list.

   > If a pop\-up window appears prompting you to add features when you check the services, click "Add Features".   
   

11. After confirming that the installation content is correct, click the "Install" button.

12. After the installation is complete, click the "Close" button and [restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances).


<span id="1T2O19fn"></span>
### Step 2: Enable multi\-user login


1. [Log in to the target server](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon, and then select "Windows System \> Run".

3. Input `gpedit.msc` in the dialog box, press Enter to open the Local Group Policy Editor.

4. In the left directory tree, select "Computer Configuration \> Administrative Templates \> Windows Components \> Remote Desktop Services \> Remote Desktop Session Host \> Connections" and complete the following configuration.

   * **Allow users to remotely connect via the Remote Desktop Services image**

      1. Right\-click "Allow users to remotely connect by using Remote Desktop Services," and select "Edit".

      2. Select "Enabled".

      3. Click "Apply" and then "Confirm" to complete the configuration.

   * **Limit the number of connections**

      1. Right\-click "Limit the number of connections" and select "Edit".

      2. Select "Enabled" and configure the maximum number of allowed remote connections.

      3. Click the "Apply" button, then click "OK" to complete the configuration.

   * **Restrict Remote Desktop Service users to individual remote desktops**

      1. Right\-click "Restrict Remote Desktop Service users to individual remote desktops" and select "edit".

      2. Select "Enabled" or "Disabled" as required.

         * **Enable:**  Users can only have one active remote desktop session. Example:

            User A has already logged in to the server via Remote Desktop. When attempting to log in from another device, the system will not create a new session.

         * **Disabled:**  Users can establish multiple independent Remote Desktop Protocol (RDP) sessions simultaneously through multiple clients, with each session having its own desktop environment and processes.

            User A has already logged into the server via Remote Desktop. When logging in again from another device, the system will create a new session.

      3. Click the "Apply" button, then click "OK" to complete the configuration.

5. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to make the policy take effect.


<span id="bkCQ3E46"></span>
### Step 3: Configure the firewall


1. [Log in to the target server](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon, right\-click "Windows PowerShell" in the "Windows PowerShell" directory, and select "More \> Run as administrator."

3. Run the following command in PowerShell to ensure that the instance's internal firewall opens port `3389` for RDP traffic.

   ```PowerShell
   New-NetFirewallRule -DisplayName "Allow RDP" -Direction Inbound -Protocol TCP -LocalPort 3389 -Action Allow
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a22a35eb3f732ce5ee8bdd40ac17c772.png) </span>


<span id="3daDvX0l"></span>
### Step 4: Assign user permissions

You need to add the users who log in to the server via Remote Desktop to the Remote Desktop user group.


1. [Log in to the target server](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon, and then select "Windows System \> Run".

3. In the dialog box, `input lusrmgr.msc`, and press Enter to open the Local Group Policy Editor.

4.  **(Optional)**  You can create a new user as needed for remote server login.

   1. Select "User" in the directory tree on the left.

   2. Click on the blank area of the user module, and select "New User".

   3. After filling in the new user's name, login password, and other configurations, click the "Create" button to complete the actions.

5. Assign user permissions.

   1. Select "Group" in the directory tree on the left.

   2. Right\-click "Remote Desktop Users" and select "Add to Group".

   3. Click the "Add..." button.

   4. Click the "Advanced" button.

   5. Click the "Find Now" button, select the target user who needs to remotely log in to this server, and click the "OK" button.

   6. Click the "OK" button to save the selection.

   7. Click "Apply" and then the "OK" button in sequence to complete the actions.


<span id="r1choZVe"></span>
## Subsequent operations

<span id="N0oqTTRG"></span>
### Remotely log in to the ECS instance

From a local PC with internet access, use the newly added remote login user to access the ECS instance through various tools. [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

<span id="bnDQt2t8"></span>
### Manage Remote Desktop permission

The grace period for Remote Desktop licensing is 120 days. If you do not activate the ECS instance with a valid license within this period, the multi\-user login feature becomes unavailable. You can:


* [Apply for a Remote Desktop license](https://docs.byteplus.com/en/docs/ecs/Apply_for_Remote_Desktop_authorization_licenses_and_activate_the_Elastic_Compute_Service), and then activate the ECS instance to continue using the multi\-user login feature.

* [Remove Remote Desktop Services](https://docs.byteplus.com/en/docs/ecs/Solution_for_Remote_Login_Failure_of_ECS_Instances_with_Windows_Operating_System) and stop using the multi\-user login feature.
