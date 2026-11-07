---
title: "Transferring files from local Linux or macOS system to Linux instance (via SCP)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-SCP-to-upload-files-from-a-local-Linux-or-MacOS-to-a-Linux-instance"
---

If your local computer is running the Linux or macOS operating system, you can use SCP to transfer files to a Linux ECS instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The Linux ECS instance must meet the following requirements:


* [An EIP is associated with the ECS instance](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), enabling the ECS instance to connect to the Internet.

* The instance is in the **Running** status.

* An inbound rule is added to the security group of the instance to allow inbound traffic on port 22. For detailed steps, refer to [Changing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* Operating system of the local computer: CentOS 7.6.

* Operating system of the ECS instance: CentOS 7.6.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload a file


1. Obtain the EIP of the Linux ECS instance.

2. Execute the following command on your local computer to upload a file to the Linux ECS instance.

   ```Bash
   scp Local file path Username of the ECS instance@EIP of the ECS instance:Path of the uploaded file on the ECS instance
   ```
   

   For example, you can execute the following command to upload the local file /home/test.txt to the corresponding directory on the ECS instance whose EIP is 10.x.x.x:

   ```Bash
   scp /home/test.txt root@10.x.x.x:/home/
   ```
   

3. Enter the login password as prompted, and then complete the file upload. If you forget your password, reset the password by referring to [Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords).

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/986aea4553914be78b114f4fd9d843d2.png) </span>


<span id=".5LiL6L295paH5Lu2"></span>
### Download a file


1. Execute the following command on the local computer to download a file from the ECS instance to the local computer.

   ```Bash
   scp Username of the ECS instance@EIP of the ECS instance:Path to the file on the ECS instance Path to the downloaded file on the local computer
   ```
   

   For example, you can execute the following command to download the file /home/test.txt from the ECS instance whose EIP is 10.x.x.x to the local /home/ directory:

   ```Bash
   scp root@10.x.x.x:/home/test.txt /home/
   ```
   

2. Enter the login password as prompted, and then download the file.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/ca82b895861e4a52919fefc7009c4cb3.png) </span>
