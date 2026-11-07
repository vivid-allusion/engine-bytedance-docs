---
title: "Transferring files from local Windows system to ECS instance (via FTP)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-FTP-to-upload-files-to-a-Windows-instance"
---

This topic describes how to transfer files from a local computer running Windows to an ECS instance by using the FTP service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The FTP service is set up on the ECS instance.


* For information about how to set up the FTP service on a Linux ECS instance, see [Setting up FTP sites (Linux)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Linux).

* For information about how to set up the FTP service on a Windows ECS instance, see [Setting up FTP sites (Windows)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Windows).


<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* Operating system of the local computer: In the example provided in this topic, a BytePlus ECS instance with a Windows Server 2019 image is used as the local computer.

* FileZilla: 3.56.0


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6L-e5o6l5LqR5pyN5Yqh5Zmo6L-c56iL56uZ54K5"></span>
### Connect to the remote ECS site


1. Download and install [FileZilla](https://www.filezilla.cn/download/client) on the local computer.

2. Double\-click FileZilla to open the client.

3. In the FileZilla window, enter the following information and click "Quickconnect".

   * Host: The EIP of the ECS instance.

   * Username: The FTP user account configured when you set up the FTP service. In the example provided in this topic, "ftptest" is used as the username.

   * Password: The FTP user password configured when you set up the FTP service.

   * Port: The default FTP listening port is 21.

   When you connect to the remote ECS instance, you can view the files stored on the ECS instance.


<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload a file

In the pane below "Local site" on the left side of FileZilla, right\-click the file that you want to upload, and select "Upload" to upload the file to the ECS instance.

<span id=".5LiL6L295paH5Lu2"></span>
### Download a file

In the lower pane below "Remote site" on the right side of FileZilla, right\-click the file that you want to download, and select "Download" to download the file from the ECS instance to your local computer.
