---
title: "Mounting a file system"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Mounting-a-file-system"
---

This topic takes the CentOS system instance as an example to introduce the operation steps for mounting a file system on an ECS instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The FileNAS service has been created. For specific steps, please refer to [Creating a file system](https://docs.byteplus.com/docs/nas/Creating-a-file-system).

* The mount point has been created. For specific steps, please refer to [Managing mount points](https://docs.byteplus.com/docs/nas/Managing-mount-points).

* An ECS instance with the same VPC as the FileNAS service has been created. For specific steps, please refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For optimal performance, it is recommended to have FileNAS and ECS instances in the same availability zone.   </div>
   

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* For optimal performance, it is recommended to choose the appropriate NFS version based on the file system type. When using the extreme file system, NFSv3 protocol is recommended, while NFSv4.0 and NFSv4.1 protocols are not recommended.

* NFS v4.0 supports file locks, including range locks. If you need to have multiple Linux instances simultaneously modify the content of a file, you can use the NFS V4.0 protocol.


<span id=".5omL5Yqo5oyC6L295paH5Lu257O757uf"></span>
## Manually mount the file system.


1. To log in to an ECS instance that requires mounting a file system, please refer to [Using the console to log on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Choose the appropriate command to install the NFS client based on different operating systems.

   * CentOS, Redhat, Aliyun Linux Operating System

      ```Plain
        sudo yum install nfs-utils
      ```
      

   * Ubuntu or Debian Operating System

      ```Plain
      sudo apt-get update
      ```
      

      ```JSON
      sudo apt-get install nfs-common
      ```
      

3. Execute the following command to create the target path to be mounted.

   ```Plain
   mkdir <target directory to be mounted>
   ```
   

   In this topic, the localdir folder is used as an example.

   ```Plain
   mkdir /localdir
   ```
   

4. Choose the appropriate command to mount the file system based on different protocol versions.

   You can log on to the [FileNAS console](https://console.byteplus.com/filenas), go to the Mount Point page, and view and copy the corresponding mount command. After copying the mount command, you need to enter `<mount address>` at the end of the command. For example, if the mount address in this article is `/localdir`, you need to enter `/localdir` at the end of the command.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please be aware of avoiding mounting the file system to the <code>/tmp</code> directory. In some operating system environments, there is an automatic cleaning mechanism that may result in file loss.   </div>
   

   * NFS V3

      ```Plain
      mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <mount point address>:/ <directory to be mounted>  
      ```
      

   * NFS V4.0

      ```Plain
      mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <mount point address>:/ <directory to be mounted>   
      ```
      

      NFS V3 Example commands are as follows.

      ```Plain
      mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport apse1a03854ca4aebd8.vpc-22qcdcj9zcu0wds3n8bu****.nas.ibytepluses.com:/enas-apse1a03854ca4a**** /localdir   
      ```
      

5. Execute the following command to view the mounted file systems.

&nbsp;

   ```Plain
   mount -l 
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also use the df command to view the capacity information of this file system.   </div>
   

<span id=".6Ieq5Yqo5oyC6L295paH5Lu257O757uf"></span>
## Automatically mount file system

You can configure the command to automatically mount the NAS file system in the files of the ECS instance, so that the file system can be automatically mounted after the ECS instance restarts, avoiding issues such as loss of mount information.

**Automatic Mounting Method Explanation**


* Add the mounting command in the `/etc/fstab` configuration file: If the file system is deleted or the configured mounting command is incorrect, there may be a risk of failure to start for ECS instances of certain operating systems.

* Add the mounting command in the `/etc/rc.local` configuration file: If the file system is deleted or the configured mounting command is incorrect, it will not affect the operation of the ECS instance.


<span id=".5pa55rOV5LiA77ya5ZyoLWV0Yy1mc3RhYi3phY3nva7mlofku7bkuK3mt7vliqDmjILovb3lkb3ku6Q="></span>
### Method 1: Add the mount command in the /etc/fstab configuration file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">If your operating system is CentOS 6.x, please execute the following command first to ensure that the netfs service starts automatically at boot.</div>


   <div data-tips="true" data-tips-type="tip">   ```Plain
   chkconfig netfs on 
   ```
      </div>
   

* <div data-tips="true" data-tips-type="tip">If your operating system is Ubuntu, please execute the following commands first.</div>


   <div data-tips="true" data-tips-type="tip">   ```Plain
   [ ! -f /etc/rc.local ] && echo '#!/bin/bash' > /etc/rc.local; echo "mount -a -t nfs" >> /etc/rc.local; chmod +x /etc/rc.local
   ```
      </div>
   


<span id=".5pON5L2c5q2l6aqk"></span>
#### **Procedure**


1. Add the mount command in the `/etc/fstab` configuration file.

   The mounting command instructions for different protocol versions are as follows:

   * NFS V3

      ```Plain
      <mount point address>:/ <directory to be mounted>  nfs  vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport,_netdev 0 0  
      ```
      

   * NFS V4.0

      ```Plain
      <mount point address>:/ <directory to be mounted> nfs  vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport,_netdev 0 0   
      ```
      

      NFS V3 example command is as follows:

      ```Plain
      apse1a03854ca4a****.vpc-22qcdcj9zcu0wds3n8bu****.nas.ibytepluses.com:/enas-apse1a03854ca4a**** /localdir nfs -o vers=3,nolock,proto=tcp,noresvport,_netdev 0 0   
      ```
      

2. After restarting the ECS instance, the file system will be automatically mounted.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before restarting the ECS instance, please ensure that the file system can be mounted correctly. Mounting failure may cause the ECS instance to fail to start. You can use the <code>mount -a</code> command to check if the mounting command is correct. After executing the <code>mount -a</code> command, execute <code>df -h</code> to check. If the file system has been successfully mounted, it means that the mounting command is correct. You can restart the ECS instance to automatically mount the file system.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your ECS instance fails to start due to mounting failure, you can enter single\-user mode during system startup, delete the mounting commands in the <code>/etc/fstab</code> configuration file, and then restart the host.   </div>
   


<span id=".5pa55rOV5LqM77ya5ZyoLWV0Yy1yYy1sb2NhbC3phY3nva7mlofku7bkuK3mt7vliqDmjILovb3lkb3ku6Q="></span>
### Method 2: Add the mounting command to the /etc/rc.local configuration file.


1. Execute the following command to add execute permission to the `/etc/rc.local` file.

   ```Plain
   [ ! -f /etc/rc.local ] && echo '#!/bin/bash' > /etc/rc.local; chmod +x /etc/rc.local  
   ```
   

2. At the end of the `/etc/rc.local` file, add the mount commands that need to be executed.

   The instructions for mounting commands of different protocol versions are as follows.

   * NFS V3

      ```Plain
      mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <mount point address>:/ <directory to be mounted>   
      ```
      

   * NFS V4.0

      ```Plain
      mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <mount point address>:/ <directory to be mounted>
      ```
      

      NFS V3 example command is as follows:

      ```Plain
      mount -t nfs -o vers=3,nolock,proto=tcp,noresvport apse1a03854ca4a****.vpc-22qcdcj9zcu0wds3n8bu****.nas.ibytepluses.com:/enas-apse1a03854ca4a**** /localdir   
      ```
      

3. After restarting the ECS instance, the file system will be automatically mounted.
