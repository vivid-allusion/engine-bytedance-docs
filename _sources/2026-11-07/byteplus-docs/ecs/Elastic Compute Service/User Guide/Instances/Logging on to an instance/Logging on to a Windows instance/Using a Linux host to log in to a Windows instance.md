---
title: "Using a Linux host to log in to a Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-a-Linux-host-to-log-on-to-a-Windows-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic describes how to log in to a Windows instance on the cloud when your local host runs the Linux operating system.


|Local host OS |ECS instance OS |Login tool on local host |Login authentication method |
|---|---|---|---|
|Linux |Windows |rdesktop, which uses RDP (Remote Desktop Protocol) |Password |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance you log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance is [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), and can communicate with the Internet.

* If you need data transfer, refer to [Uploading a file from an local Linux system to a Windows ECS instance by using RDP](https://docs.byteplus.com/en/docs/ecs/Using-RDP-to-upload-files-from-a-local-Linux-to-a-Windows-instance).


<span id=".5a-G56CB55m75b2V5q2l6aqk"></span>
## Procedure (password)


1. [Install a visual interface](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux) on your local Linux computer.

2. Refer to [Uploading a file from a local Linux system to a Windows ECS instance by using RDP > Install rdesktop](https://docs.byteplus.com/en/docs/ecs/Using-RDP-to-upload-files-from-a-local-Linux-to-a-Windows-instance#.5a6J6KOFLXJkZXNrdG9w) and use your local browser to download and install rdesktop.

3. Run the following command to log in to the Windows instance.

   `rdesktop -u Administrator -p password XX.XX.XX.XX`

   
   |Argument |Description |
   |---|---|
   |\-u |The username of the Windows ECS instance. |
   |\-p |The password for the username of the Windows ECS instance. |
   |IP address |The EIP address of the Windows ECS instance. |
