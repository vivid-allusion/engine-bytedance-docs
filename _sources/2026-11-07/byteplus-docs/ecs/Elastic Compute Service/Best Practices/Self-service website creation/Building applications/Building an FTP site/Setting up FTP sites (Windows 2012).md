---
title: "Setting up FTP sites (Windows 2012)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Setting_up_FTP_sites_Windows_2012"
---

FTP is an application\-layer protocol used for file transfer between a client and a server over a computer network. Typically, it operates on two ports: 20 and 21. This topic describes how to set up an FTP site on a Windows Server 2012 R2 instance.

<span id="xJIUMcPf"></span>
## Prerequisites


* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [associated an EIP with it](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The ECS instance status is **Running**.


<span id="19ZDVBYC"></span>
## Software version


* Windows operating system: This topic uses Windows Server 2012 R2 as an example.

* IIS: Web server. This topic uses IIS 8 as an example.

* Client operating system: This topic uses macOS Sequoia 15.6.1 as an example.


<span id="It5YMf4v"></span>
## Procedure

<span id="6SrCsH6j"></span>
### Step 1: Install the FTP service in IIS


1. Log in to [ECS console](https://console.byteplus.com/ecs/instance).

2. On the server desktop, click "Start" in the lower left corner, and select "Server Manager".

3. In the directory tree on the left, select "Dashboard" and click "Add roles and features".

4. In the "Add Roles and Features Wizard" window that pops up, click "Next" to enter the "Select installation type" interface.

5. In the "Select installation type" interface, select "Role\-based or feature\-based installation", and click "Next".

6. On the "Select destination server" page, keep the default settings and click "Next".

7. In the "Select server roles" interface, select "Web Server (IIS)". Then, in the pop\-up window, click "Add Features".

8. Continue clicking "Next" until you reach the "Select role services" interface.

9. In the "Select role services" interface, check "FTP Service" and "FTP Extensibility", and click "Next".

10. Confirm the installation information and click the "Install" button.

11. After installation is complete, click the "Close" button to quit the page.


<span id="PlYXUb1B"></span>
### Step 2: Create an FTP username and password

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Create a Windows username and password for FTP use. If you need access as an anonymous user, skip this step.</div>



1. In the "Server Manager" window, select "Tools \> Computer Management" from the navigation bar in the upper right corner to open the "Computer Management" window.

2. In the left navigation pane, select "System Tools \> Local Users and Groups \> Users".

3. In the "Actions" module on the right, click "More Actions \> New User...".

4. On the "New User" interface, set the username and password as instructed below. Then, click the "Create" button to complete the operation.

   * User name: This topic uses "`ftptest`" as an example.

   * Password: Set a password based on password requirements.

   * Password never expires: Select this option as needed. In the example provided in this topic, this option is selected.


<span id="31puGVTs"></span>
### Step 3: Set shared folder permissions


1. Click "Start \> File Explorer" and select "This PC" in the left directory tree.

2. Double\-click "Windows 2012r2 (C:)" to enter the C drive.

3. Right\-click a blank area and select "New \> Folder" to create an FTP shared folder. This topic uses the name `test` as an example.

4. Right\-click the "test" folder and select "Properties".

5. Select the "Security" tab and click the "Edit" button.

6. On the pop\-up "Permissions for test" page, click the "Add" button.

7. In the pop\-up dialog box, enter the object name (here, the FTP user `ftptest` created in Step 2 is used as an example), and click the "Check Names" button.

8. Confirm the name, and then click the "OK" button.

9. In the "Permissions for test" window, grant permissions to "ftptest" as needed, and click "Apply" and "OK" in sequence.

   In the example provided in this topic, all permissions are granted.

9. In the "test Properties" window, click the "OK" button to complete the configuration.


<span id="VlLk5710"></span>
### Step 4: Add an FTP site


1. In the upper right corner of the "Server Manager" window, select "Tools \> Internet Information Services (IIS) Manager".

2. Click the expand button to the left of the hostname. In the pop\-up window, you will be prompted "Whether to start using the Microsoft Web platform to maintain links with the latest web platform components?". In the example provided in this topic, the "Cancel" option is selected to skip configuring this option.

3. Select "Sites" in the right directory tree, and click the "Add FTP Site" button in the left "Actions" module.

3. In the pop\-up window, enter the FTP site name, select the physical path of the shared folder, and click "Next".

   In the example provided in this topic, `ftpserver` is used as the FTP site name, and `C:\test `configured in Step 3 as the physical path.

4. On the "Binding and SSL Settings" interface, configure relevant settings as needed, and then click "Next".

   * **Binding**: The IP address defaults to **All unassigned**, and the port to **21 ** (the default FTP port number). You can also set a port number manually.

   * **SSL**: Select this option as needed. In the example provided in this topic, **No SSL** is selected.

      * **No SSL**: SSL encryption is not required.

      * **Allow SSL**: An FTP server is allowed to support non\-SSL and SSL connections between the FTP server and clients.

      * **Require SSL**: SSL encryption is required for communications between the FTP server and clients.

         If you select "Allow SSL" or "Require SSL", you can choose an existing SSL certificate in the "SSL Certificate" section. Or, refer to steps for [creating server certificates](https://docs.byteplus.com/en/docs/ecs/FTP_site_setup_FAQ#ftxfQcdZ) to create one.

5. On the "Authentication and Authorization Information" interface, configure relevant settings, and then click the "Finish" button.

   * **Authentication**: Select an identity authentication method. This topic uses "Basic" as an example.

      * **Anonymous**: Allows any user to access content with an anonymous username (anonymous) or an FTP username.

      * **Basic**: Requires a user to provide a valid username and password to access content. Because basic authentication transmits passwords in an unencrypted form over the network, use this authentication method only when you know the connection between clients and the FTP server is secure (such as via the Secure Sockets Layer, SSL).

   * **Authorization**: Select a method from the "Allowed access to" dropdown list. In the example provided in this topic, "Allowed access to" is set to "Specified users", and the user is specified as "ftptest".

      * **All users**: All users can access content.

      * **Anonymous users**: Anonymous users can access content.

      * **Specified roles or user groups**: Only members belonging to the specified roles or user groups can access content. After selecting this option, you need to specify the role or user group.

      * **Specified users**: Only specified users can access content. After selecting this option, you need to specify the username.

   * **Permissions**: Grant permissions for authorized users. In the example provided in this topic, **Read** and **Write** permissions are granted.

      * **Read**: Allows authorized users to read content from the directory.

      * **Write**: Allows authorized users to write to the directory.

6. Configure the firewall for the FTP site.

   1. Select the FTP site you created in the directory tree on the left side of IIS Manager. This topic uses `ftpserver` as an example.

   2. Select the "FTP Firewall Support" feature and click the "Enable feature" button in the "Actions" module on the right.

   3. In the text box under "External IP address of Firewall", enter the Windows instance EIP.

      Log in to the [ECS console](https://console.byteplus.com/ecs/instance), and view the EIP of the corresponding ECS instance in the Instances list.

   4. In the "Actions" column on the right side of the page, click "Apply". Then, in the pop\-up window, click "OK".


<span id="Jmys7ATC"></span>
### Step 5: Configure the security group and firewall

After the FTP site is set up, add rules to the inbound direction of the instance security group and allow the following FTP ports. For detailed steps, refer to [Changing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


* **Configure the instance security group**

   Add an inbound rule to the security group of the Windows instance to allow traffic on port 21 and port range 1024 – 65535.

   
   |FTP usage mode |Direction |Protocol type |Port range |Source address |
   |---|---|---|---|---|
   |Active mode |Inbound |TCP |20/21 |0.0.0.0/0 |
   |Passive mode |Inbound |TCP |Port 21 and ports 1024–65535<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To adjust the passive mode port range, refer to <a href="https://docs.byteplus.com/en/docs/ecs/FTP_site_setup_FAQ#SOZBk7kM">configuration recommendations</a>. This topic uses the range <code>1024-65535</code> as an example.</div><br> |0.0.0.0/0 |
   

* **Configure the instance firewall**

   Follow the guide in the ["Configure port rules for the firewall"](https://docs.byteplus.com/en/docs/ecs/Security-FAQs) section to create inbound rules in your instance and allow TCP ports 20, 21, and 1024–65535 as needed. For more firewall settings, refer to [Microsoft official documents](https://docs.microsoft.com/en-us/previous-versions/orphan-topics/ws.11/hh831655%28v=ws.11%29?redirectedfrom=MSDN#Step4).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>1024–65535</code> with the actual passive mode port range.   </div>
   

<span id="EmlOBGTs"></span>
### Step 6: Test the client

You can verify the FTP service using FTP client software, a browser, a file explorer, or other tools. This topic uses MacOS Finder as an example.


1. Open Finder and select "Go \> Connect to Server" in the top menu bar.

2. Enter` ftp://ECS instance EIP:21` and click the "Connect" button.

3. In the pop\-up login window, confirm the FTP server information and click the "Connect" button.

4. Enter the FTP username and password that have been set, and then click "Connect". After the connection succeeds, you can view a file in the specified directory on the FTP server.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since macOS "Finder" does not support uploading files to an FTP server, you can download third\-party software like FileZilla to transfer files.</div>
