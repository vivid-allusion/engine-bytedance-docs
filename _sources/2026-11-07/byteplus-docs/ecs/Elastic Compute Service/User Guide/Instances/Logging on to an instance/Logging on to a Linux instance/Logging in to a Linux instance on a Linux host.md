---
title: "Logging in to a Linux instance on a Linux host"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-a-Linux-host-to-log-on-to-a-Linux-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic describes how to log in to a Linux ECS instance when your local host runs a Linux operating system.


|Operating system of the local host |Operating system of ECS instance |Login tool on local host |Login authentication method |
|---|---|---|---|
|Linux |Linux |SSH command |Password and key |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance you log to in meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance is[ associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), and can communicate with the Internet.

* If you need data transfer, refer to [Transferring files from a local Linux or macOS system to a Linux instance (SCP)](https://docs.byteplus.com/en/docs/ecs/Using-SCP-to-upload-files-from-a-local-Linux-or-MacOS-to-a-Linux-instance).


<span id=".55m75b2V5q2l6aqk"></span>
## Login procedure


<Tabs>
<Tab zoneid="jScnMYoOZl" title="Password login">
<TabTitle>Password login</TabTitle>

1. Run the following SSH command.

   ```Plain Text
   ssh <The username of the Linux ECS instance>@<The EIP address of the Linux ECS instance>
   ```
   

2. Enter the login password that matches the Linux instance username, and then press Enter to log in to the Linux ECS instance.


</Tab>
<Tab zoneid="jr5fjDTfG0" title="Key login">
<TabTitle>Key login</TabTitle>

1. Run the following command to make the private key file readable by the currently logged\-in user.

   ```Plain Text
   chmod 400 <The storage path of the .pem private key file on the local host>
   ```
   

2. Run the following command to log in to the ECS instance.

   ```Plain Text
   ssh -i <The storage path of the .pem private key file on the local host> <The username of the Linux ECS instance>@<The EIP address of the Linux ECS instance>
   ```
   

3. Press the `Enter` key to log in to the ECS instance.


</Tab>
</Tabs>
