---
title: "Transferring files from local Linux system to ECS instance (FTP)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-FTP-to-upload-files-to-a-Linux-instance"
---

This topic describes how to transfer files from a local computer running Linux to an ECS instance by using the FTP service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The FTP service is set up on the ECS instance.


* For information about how to set up the FTP service on a Linux ECS instance, see [Setting up FTP sites (Linux)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Linux).

* For information about how to set up the FTP service on a Windows ECS instance, see [Setting up FTP sites (Windows)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Windows).


<span id=".6L2v5Lu254mI5pys"></span>
## Software version

Operating system of the local computer: CentOS 8.3.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6L-e5o6l5LqR5pyN5Yqh5Zmo6L-c56iL56uZ54K5"></span>
### Connect to the remote ECS instance.


1. Execute the following command on the local computer to install FTP.

   `yum -y install ftp`

2. Execute the following command to connect to the ECS instance, and enter the username and password of the FTP service as prompted.

   `ftp EIP of the ECS instance`

   If the following output is displayed, the connection is successful.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/af49c2075c2541ef8553078fa63418db.png) </span>


<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload a file

Execute the following command to upload a file from your local computer to the ECS instance.

`put local-file [remote-file]`

For example, you can execute the following command to upload the local upload.txt file to the ECS instance.

`put /home/upload.txt upload.txt`

If the following output is displayed, the file is uploaded.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/6370344a76354562ab35e839636da0a2.png) </span>

<span id=".5LiL6L295paH5Lu2"></span>
### Download a file

Execute the following command to download a file from the ECS instance to the local computer.

`get [remote-file] [local-file]`

For example, you can execute the following command to download the download.txt file from the ECS instance to the local computer.

`get download.txt /home/download.txt`

If the following output is displayed, the file is downloaded.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/c3909ee56bb047be9821255e028250e7.png) </span>
