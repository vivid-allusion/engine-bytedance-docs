---
title: "Transferring files from local Linux system to Windows instance (via RDP)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-RDP-to-upload-files-from-a-local-Linux-to-a-Windows-instance"
---

If your local computer is running the Linux operating system, you can transfer files to a Windows ECS instance by using RDP.

<span id=".5YWz5LqOUkRQ"></span>
## About RDP

rdesktop is a Linux\-based client program that supports Windows Remote Desktop connections. It enables remote access to Windows desktops from Linux systems, uses the Remote Desktop Protocol (RDP), and is compatible with multiple versions.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Local computer:

   * The Linux operating system is used.

   * A [visual interface](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux) is installed. Otherwise, rdesktop cannot be used.

* ECS instance:

   * The Windows operating system is used.

   * The instance is in the **Running** status.

   * [An EIP is associated with the instance](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), enabling the instance to connect to the Internet.

   * An inbound rule is added to the security group of the instance to allow inbound traffic on port 3389. For detailed steps, refer to [Changing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).

   * RDP is enabled. For more information, see [Enabling RDP on Windows ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-RDP-to-upload-files-from-a-local-Linux-to-a-Windows-instance#.d2luZG93c-S6keacjeWKoeWZqOW8gOWQr3JkcA==).


<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* Operating system of the local computer: CentOS 8.3.

* Operating system of the ECS instance: Windows Server 2016.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5a6J6KOFIHJkZXNrdG9w"></span>
### Install rdesktop


1. Execute the following command on the local computer to install rdesktop from the software repository.

   `yum install rdesktop`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are unable to install rdesktop from the software repository, you can go to the <a href="http://www.rdesktop.org/">rdesktop official website</a> to download it, and then execute the <code>wget</code> command to download and install it.   </div>
   

   > Execute the `wget` command to download and install rdesktop.   
   

   ```Plain Text
   yum install libX11-devel openssl-devel -y
   wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.6/rdesktop-1.8.6.tar.gz
   tar xvzf rdesktop-1.8.6.tar.gz
   cd rdesktop-1.8.6/
   ./configure --disable-credssp --disable-smartcard
   make 
   make install
   ```
   

2. After the installation is complete, you can execute the following command to check whether the installation is successful.

   `rdesktop`

   > If the rdesktop version number is displayed, the installation is successful.

   > <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_440d8bbf74dee0f31bddbb7ef1c8cc72.jpg) </span>   
   

<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload a file


1. Execute the following command on your local computer to specify the folder that you want to upload to the ECS instance.

   `rdesktop EIP of the ECS instance -u Username of the ECS instance -p Login password of the ECS instance -r disk:Specified shared folder name=Local folder path`

   * EIP of the ECS instance.

   * Username of the ECS instance: The username is "Administrator" for a Windows instance.

   * Login password of the ECS instance: The password corresponding to the username of the ECS instance. If you forget your password, [reset the password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords).

   For example, you can execute the following command to share the /home folder of the local computer with the specified ECS instance, and rename the shared folder to share.

   ```Bash
   rdesktop 10.x.x.x -u Administrator -p yourpassword -r disk:share=/home
   ```
   

2. After the local computer is connected to the remote ECS instance, access the Windows ECS instance. Click "Start \> File Explorer", select "This PC" on the "File" page, and view the shared folder.

3. Double\-click to open the shared folder, and copy the local file that you want to upload to another volume on the Windows ECS instance. The file upload operation is finished.


<span id=".5LiL6L295paH5Lu2"></span>
### Download a file

To download files from an ECS instance to your local computer, you can copy the required files from the Windows ECS instance to the shared folder by referring to the upload operation.

<span id=".6ZmE5b2V"></span>
## Appendix

<span id=".V2luZG93c-S6keacjeWKoeWZqOW8gOWQr1JEUA=="></span>
### Enable RDP on the Windows ECS instance


1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Select "This PC \> Properties", and click "Advanced system settings".

3. Select the "Remote" tab, confirm that "Allow remote connections to this computer" is selected, and select "Allow connections only from computers running Remote Desktop with Network Level Authentication (recommended)" based on your needs.
