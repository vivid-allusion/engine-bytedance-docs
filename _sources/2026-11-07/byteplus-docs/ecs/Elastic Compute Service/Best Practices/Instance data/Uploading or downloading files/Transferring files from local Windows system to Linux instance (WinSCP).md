---
title: "Transferring files from local Windows system to Linux instance (WinSCP)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-WinSCP-to-upload-files-from-a-local-Windows-to-a-Linux-instance"
---

If your local computer is running the Windows operating system, you can use WinSCP to transfer files to a Linux instance.

<span id=".5YWz5LqOIFdpblNDUA=="></span>
## About WinSCP

WinSCP is an open\-source graphical SFTP client that uses SSH and runs on the Windows environment. WinSCP also supports the SCP protocol. It can securely copy files between local and remote computers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Local computer:

   * The Windows operating system is used.

   * The WinSCP client is downloaded and installed. You can obtain the latest version from the [official website](https://winscp.net/eng/docs/lang:chs).

* ECS instance:

   * The Linux operating system is used.

   * The instance is in the **Running** status.

   * [An EIP is associated with the instance](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), enabling the instance to connect to the Internet.

   * An inbound rule is added to the security group of the instance to allow inbound traffic on port 22. For detailed steps, refer to [Changing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* Operating system of the local computer: Windows Server 2019.

* Operating system of the ECS instance: CentOS 8.3.

* WinSCP version: 5.19.2 (build 11614).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload a file


1. Double\-click to open WinSCP on your local computer. The "Log in" dialog box is displayed.

2. Fill in the relevant information for the new site (ECS instance).

   * Protocol (optional): Enter SFTP or SCP.

   * Hostname: Enter the EIP of the ECS instance.

   * Port: The default value is 22.

   * Username: The system username of the ECS instance. For Linux systems, the username is root.

   * Password: The password corresponding to the username of the ECS instance. If you forget your password, reset the password by referring to [Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords).

3. Click "Log in" to enter the WinSCP file transfer interface. The file directory of the local computer is displayed in the left pane of the interface, while the file directory of the ECS instance is displayed in the right pane.

4. In the right pane of the WinSCP file transfer interface, select the directory where you want to store the uploaded files, such as "/root/".

   In the left pane of the WinSCP file transfer interface, select the directory containing the files that you want to upload, such as "C:\Users\Administrator\Downloads\", and select a file you want to upload.

5. In the left pane of the WinSCP file transfer interface, click the "Upload" button.

6. Confirm the file you want to transfer and other related information, and click the "OK" button to upload the file.


<span id=".5LiL6L295paH5Lu2"></span>
### Download a file


1. In the left pane of the WinSCP file transfer interface, select the directory where you want to store the downloaded file, such as "C:\Users\Administrator\Downloads\".

   In the right pane of the WinSCP file transfer interface, select the directory on the ECS instance from which you want to download a file, such as "/root/". Select the file you want to download.

2. In the right pane of the WinSCP file transfer interface, click the "Download" button.

3. Confirm the file you want to transfer and other related information, and click the "OK" button to download the file.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results

The uploaded/downloaded file is displayed in the specified directory of the right/left pane in the WinSCP file transfer interface.
