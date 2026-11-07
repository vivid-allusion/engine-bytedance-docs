---
title: "Using a Windows host to log in to a Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Windows-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic describes how to log in to a Windows instance on the cloud when your local host runs the Windows operating system.


|Local Host OS |ECS Instance OS |Local Host Login Tool |Login Authentication Method |
|---|---|---|---|
|Windows |Windows |MSTSC, a remote desktop login tool |Password |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance you log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance is [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), and can communicate with the Internet.

* If you need data transfer, refer to [Uploading a file from an local Windows system to a Windows ECS instance by using MSTSC](https://docs.byteplus.com/en/docs/ecs/Using-MSTSC-to-upload-files-from-a-local-Windows-to-a-Windows-instance).


<span id=".5a-G56CB55m75b2V5q2l6aqk"></span>
## Procedure (password)


1. On your local host, choose "Start \> Search" and search for Remote Desktop.

2. Open Remote Desktop Connection, click the "Show Options" button, and enter the login information of the target Windows ECS instance.

   
   |Information |Description |
   |---|---|
   |Computer |Enter the EIP address of the Windows instance on the cloud. |
   |Username |Enter the username of the Windows instance on the cloud. |
   |Allow me to save credentials |If you do not want to manually enter the username and password for the next login, select "Allow me to save credentials". |
   

3. Click the "Connect" button and enter the password for the Windows ECS instance on the cloud to log in.
