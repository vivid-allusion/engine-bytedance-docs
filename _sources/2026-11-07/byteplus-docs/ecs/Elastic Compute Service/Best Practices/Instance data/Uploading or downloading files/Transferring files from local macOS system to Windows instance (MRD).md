---
title: "Transferring files from local macOS system to Windows instance (MRD)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-MRD-to-upload-file-from-a-local-MacOS-to-a-Windows-instance"
---

If your local computer is running the macOS operating system, you can transfer files to a Windows ECS instance by using MRD.

<span id=".5YWz5LqOTVJE"></span>
## About MRD

Microsoft Remote Desktop (MRD) is a remote desktop client developed by Microsoft for macOS. You can use and control remote Windows applications, resources, and desktops from your macOS computer.

MRD is applicable to Windows Server 2019 and Windows Server 2016.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Local computer:

   * The macOS operating system is used.

   * The MRD client is downloaded and installed. Microsoft has officially discontinued providing download links for the MRD client. You can click [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) to download and use the Beta version.

* ECS instance:

   * The Windows operating system is used.

   * The instance is in the **Running** status.

   * [An EIP is associated with the ECS instance](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), enabling the ECS instance to connect to the Internet.

   * An inbound rule is added to the security group of the instance to allow inbound traffic on port 3389. For more information, see [Modifying security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* Operating system of the local computer: In the example provided in this topic, macOS Big Sur 11.6 is used.

* Operating system of the ECS instance: In the example provided in this topic, Windows Server 2019 is used.

* MRD version: Version 10.6.8 (1914).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload a file


1. Start the MRD client on the local computer.

2. Click the "Add PC" button.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/7546e09ac49a4261a37a798b036227b4.png) </span>

3. In the pop\-up "Add PC" window, perform the following steps to configure the login information.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/d050a7333f7f49938056b29103a8ba4f.png) </span>

   1. PC name: Enter the EIP of the ECS instance.

   2. User account: In the drop\-down list, select "Add User Account...".

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/6c6d3b1118884e0084bd3b8bd2f78c47.png) </span>

   3. In the "Add a User Account" dialog box, enter the ECS instance username "Administrator" and password. Then, click "Add". If you forget your password, reset the password by referring to [Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords).

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/3f459590531a472c87c35786a4b4f415.png) </span>

   4. Click "Folders" and select the folder that you want to upload on your local computer.

   5. Click the ➕ icon in the lower left corner, and select the folder that you want to upload in the pop\-up window.

   6. Click "Add" to finish adding the remote server.

4. Double\-click the added server.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/182a5887aa01423993a6a249819cdbb8.png) </span>

5. Confirm the login information and click "Continue" to log in.

6. After the local computer is connected to the ECS instance, click "Start \> File Explorer" on the Windows ECS instance, select "This PC," and then view the shared folder.

7. Double\-click to open the shared folder, then copy the files to be uploaded into the Windows ECS instance to finish uploading.


<span id=".5LiL6L295paH5Lu2"></span>
### Download a file

To download files from a Windows ECS instance to your local computer, you can copy the required files from the Windows ECS instance to the shared folder by referring to the upload operation.
