---
title: "Transferring files from local Windows system to Windows instance (MSTSC)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-MSTSC-to-upload-files-from-a-local-Windows-to-a-Windows-instance"
---

If your local computer is running the Windows operating system, you can use the built\-in Windows remote desktop connection tool called MSTSC to transfer files to a Windows ECS instance.

<span id=".5YWz5LqOTVNUU0M="></span>
## About MSTSC

Microsoft Terminal Services Client (MSTSC) is a remote desktop connection component provided by Microsoft. It can be used to remotely connect to a terminal server or other remote computers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An ECS instance [is associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), enabling the ECS instance to connect to the Internet.

* The ECS instance is in the **Running** status.


<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* Operating system of the local computer: Windows Server 2019.

* Operating system of the ECS instance: Windows Server 2019.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. On the local computer, click "Start" to open the "Start" window, and then click "Remote Desktop Connection".

2. In the "Remote Desktop Connection" window, click "Show Options" in the lower left corner.

3. On the "General" tab, enter the EIP and username of the ECS instance.

   * Computer: Enter the EIP of the ECS instance.

   * User name: Enter the username of the Windows ECS instance, which is "Administrator".

4. Select the "Local Resources" tab, and click "More".

5. In the pop\-up "Local devices and resources" window, select "Drives", select the local hard disk where the files to be uploaded to the Windows ECS instance are located, and then click "OK".

6. After the configuration is complete, click "Connect" and enter the password for logging in to the ECS instance as prompted. If you forget your password, reset the password by referring to [Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords).

7. After the local computer is connected to the ECS instance, click "Start \> File Explorer" on the Windows ECS instance, select "This PC," and then view the shared folder.

8. Double\-click to open the shared folder, then copy the files to be uploaded into the Windows ECS instance to finish uploading.


<span id=".5LiL6L295paH5Lu2"></span>
### Download files

To download files from a Windows ECS instance to your local computer, you can copy the required files from the Windows ECS instance to the shared folder by referring to the upload operation.
