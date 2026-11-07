---
title: "Setting up FTP sites (Ubuntu 22.04)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Setting_up_FTP_sites_Ubuntu"
---

FTP is an application\-layer protocol used for file transfer between a client and a server over a computer network. Typically, it operates on two ports: 20 and 21. This topic describes how to set up an FTP site on a Ubuntu 22.04 instance.

<span id="mUY6ko2i"></span>
## Prerequisites


* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [associated an EIP with it](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The ECS instance status is **Running**.


<span id="vIXEeTuT"></span>
## Software version


* Linux operating system: This topic uses Ubuntu 22.04 as an example.

* Client operating system: This topic uses macOS Sequoia 15.6.1 as an example.

* vsftpd: This topic uses vsftpd 3.0.2 as an example.


<span id="4nctarXp"></span>
## Procedure

<span id="S6GoVvdE"></span>
### Step 1: Install vsftpd


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. Execute the following commands to install vsftpd.

   ```Bash
   sudo apt-get update
   sudo apt-get -y install vsftpd
   ```
   

   3. Execute the following command to specify that the vsftpd automatically starts upon instance startup.

   ```Plain Text
   systemctl enable vsftpd
   ```
   

4. Execute the following command to start the FTP service.

   ```Plain Text
   systemctl start vsftpd
   ```
   

5. Execute the following command to check whether the service is started.

   ```Plain Text
   netstat -antup | grep vsftpd
   ```
   

   If the following output is displayed, the vsftpd service is started.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25a19c3b34045005caab2bd23bae92db.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">vsftpd allows anonymous access by default. The default FTP server path for anonymous users is /var/ftp/pub. Anonymous users only have view permissions—they cannot create, delete, or modify files or directories.   </div>
   

<span id="6lDFtz3X"></span>
### Step 2: Configure vsftpd


1. Execute the following command to back up the vsftpd configuration file.

   ```Bash
   sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.bak
   ```
   

2. Modify the vsftpd configuration file.

   1. Execute the following command to open the vsftpd configuration file.

      ```Bash
      sudo vim /etc/vsftpd.conf
      ```
      

   2. Press the `i `key to enter edit mode. Enable IPv4 socket listening, and disable IPv6 socket listening.

      ```Plain Text
      listen=YES
      listen_ipv6=NO
      ```
      

   3. Modify the FTP access permissions to allow only local users to access FTP and disable anonymous access.

      ```Plain Text
      anonymous_enable=NO
      local_enable=YES
      ```
      

   4. Modify the following configuration to enable file uploads.

      ```Plain Text
      write_enable=YES
      ```
      

   5. Remove the comment symbol `# `at the beginning of the following configuration lines. This allows you to restrict FTP user directory access using chroot jails and configure which files FTP service users can access.

      ```Plain Text
      chroot_local_user=YES
      chroot_list_enable=YES
      chroot_list_file=/etc/vsftpd.chroot_list
      ```
      

   6. Add FTP service directory configuration and enable write permissions for users in the mounted chroot (root directory change) environment.

      ```Plain Text
      local_root=/home/ftp  
      allow_writeable_chroot=YES
      ```
      

   7. Add the following configuration as needed to set FTP to active mode or passive mode.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Due to firewall settings on most clients and other factors, the active mode may cause issues. We recommend using <strong>passive mode </strong>to set up an FTP service.      </div>
      

      * Active mode

         ```Plain Text
         port_enable=YES
         ```
         

      * Passive mode

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code><PUBLIC_IP></code> with the actual public IP address of the server hosting the FTP site.         </div>
         

         ```Plain Text
         pasv_enable=YES
         pasv_min_port=35000
         pasv_max_port=40000
         pasv_address=<PUBLIC_IP>
         ```
         

   8. Press the `esc `key to exit edit mode, enter `:wq`, and press the Enter key to save the changes and exit the configuration file.

3. Create a chroot_list file, and add the list of exception usernames to the file.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Users in an exception list are not restricted to their home directories and can access other directories.   </div>
   

   1. Execute the following command to create the chroot_list file.

      ```Bash
      sudo vim /etc/vsftpd.chroot_list
      ```
      

   2. Press `i` to enter edit mode and enter the exception user list.

   2. Press `Esc` to exit the edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to restart vsftpd for the configuration to take effect.

   ```Bash
   sudo systemctl restart vsftpd
   ```
   


<span id="LOeirBvm"></span>
### Step 3: Configure user directory


1. After you install vsftpd, a default passwordless user named `ftp` is created. Execute the following command to modify the password.

   ```Bash
   sudo passwd ftp
   ```
   

   If the following output is displayed, the login password for user `ftp` is modified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0e0994bd44194657ecbaee02b87cbda.png) </span>

2. Execute the following command to ensure that the shell of user `ftp` is included in the /etc/shells file.

   ```Bash
   SHELL_TO_CHECK=$(getent passwd ftp | cut -d: -f7) && (grep -q "^$SHELL_TO_CHECK$" /etc/shells || echo "$SHELL_TO_CHECK" >> /etc/shells)
   ```
   

3. Execute the following command to add the user `ftp` to the vsftpd list of users allowed to log in.

   ```Bash
   echo "ftp" | sudo tee -a /etc/vsftpd.userlist
   ```
   

4. Execute the following command to create the FTP file directory.

   ```Bash
   sudo mkdir /home/ftp
   ```
   

5. Execute the following command to grant permissions for the FTP file directory.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, read, write, and full control permissions on the folder are granted. Modify the corresponding permissions as needed.   </div>
   

   ```Bash
   sudo chmod 777 /home/ftp
   ```
   


<span id="pDVw5vYl"></span>
### Step 4: Configure security group

After the FTP site is set up, add rules to the inbound direction of the instance security group and allow the following FTP ports. For detailed steps, refer to [Changing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


|FTP usage mode |Direction |Protocol type |Port range |Source address |
|---|---|---|---|---|
|Active mode |Inbound |TCP |20/21 |0.0.0.0/0 |
|Passive mode |Inbound |TCP |Port 21, and all ports between the values of parameters `pasv_min_port` and `pasv_max_port`, which are defined in the /etc/vsftpd/vsftpd.conf configuration file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To adjust the passive mode port range, refer to<a href="https://docs.byteplus.com/en/docs/ecs/FTP_site_setup_FAQ#SOZBk7kM"> configuration recommendations</a>. This topic uses the range<code> 35000-40000</code> as an example.</div><br> |0.0.0.0/0 |


<span id="CikZCnqO"></span>
### Step 5: Client test

You can verify the FTP service using FTP client software, a browser, a file explorer, or other tools. This topic uses MacOS Finder as an example.


1. Open Finder and select "Go \> Connect to Server" in the top menu bar.

2. Enter `ftp://ECS instance EIP:21` and click the "Connect" button.

3. In the pop\-up login window, confirm the FTP server information and click the "Connect" button.

4. Enter the FTP username and password that have been set, and then click "Connect". After the connection succeeds, you can view the files in the specified directory on the FTP server.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Since macOS "Finder" does not support uploading files to an FTP server, you can download third\-party software like FileZilla to transfer files.   </div>
