---
title: "Mounting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_NFS"
---

This topic demonstrates how to mount a file system on an ECS instance, using CentOS as an example.

<span id="8AntxWbD"></span>
## Prerequisites


* You have created an EFS file system. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

* You have created a mount target. For instructions, see [Creating a mount target](https://docs.byteplus.com/en/docs/nas/efs_Managing_mount_targets#ZRe0cMNq).

* You have created an ECS instance within the same VPC as the EFS file system. For instructions, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For optimal performance, deploy your file system and ECS instance in the same availability zone.   </div>
   

<span id="AukgSUJg"></span>
## Caution

EFS file systems support both the NFSv4.1 and NFSv3 protocols.

<span id="cSumlOGw"></span>
## Steps


1. [Use the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Choose the right NFS client installation command for your operating system.

   
   <Tabs>
   <Tab zoneid="GX9wGubJkP" title="CentOS, Redhat, and Aliyun Linux">
   <TabTitle>CentOS, Redhat, and Aliyun Linux</TabTitle>
   
   ```Plain Text
   sudo yum install nfs-utils
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="t7yKFfOXGh" title="Ubuntu or Debian">
   <TabTitle>Ubuntu or Debian</TabTitle>
   
   ```Plain Text
   sudo apt-get update
   ```
   
   
   ```Plain Text
   sudo apt-get install nfs-common
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. Run this command to create the mount directory.

   ```Plain Text
   mkdir <mount directory>
   ```
   

   Example: `/localdir`.

   ```Plain Text
   mkdir /localdir
   ```
   

4. Run this command to mount the file system with the NFSv4.1 protocol.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/efs">EFS console</a> and go to the Mount Target page to view and copy the mount command. Append <code><mount directory></code> after the mount command. For example, the mount directory in this topic is <code>/localdir</code>, so you need to append <code>/localdir</code> after the mount command.   </div>
   

   ```Plain Text
   mount -t nfs -o vers=4.1,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <mount target domain name>:/ <mount directory>
   ```
   

   Example command:

   ```Plain Text
   mount -t nfs -o vers=4.1,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport cnbjf0baf17f****.3jhhzmexcmiv43pncmfwo****.efs.ivolces.com:/ /localdir 
   ```
   

5. Run the following command to view the mounted file system.

   ```Plain Text
   mount -l
   ```
   

   If the following output is returned, the file system has been mounted successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe79e382a58eecf35b206fa936635b23.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also use the <code>df</code> command to check the capacity information of the file system.   </div>
