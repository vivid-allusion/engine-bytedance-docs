---
title: "Enabling the multiqueue feature for network interfaces"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enabling-network-interface-queues"
---

This topic describes how to enable the multiqueue feature for primary and secondary network interfaces associated with ECS instances.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

The multiqueue feature can distribute network interrupts of an instance across multiple CPUs. This improves network performance and response speed. Additionally, the multiqueue feature can mitigate performance degradation due to the bottleneck where one vCPU handles all network interrupts.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

The network interface multiqueue automatic configuration tool adjust\-nic\-queue currently supports only the following images:


|Operating systems |Operating system version |
|---|---|
|veLinux |* veLinux 1.0 64 bit<br><br>* veLinux 1.0 CentOS compatible version 64 bit<br><br>* veLinux 2.0 64 bit |
|CentOS |* CentOS Stream 9 64 bit<br><br>* CentOS 8.3 64 bit<br><br>* CentOS 7.x 64 bit |
|RHEL |* RHEL 9.3 64 bit<br><br>* RHEL 9.2 64 bit<br><br>* RHEL 8.8 64 bit<br><br>* RHEL 7.8 64 bit |
|Debian |* 64\-bit Debian 9<br><br>* 64\-bit Debian 10<br><br>* Debian 11 64 bit |
|Ubuntu |* Ubuntu 16.04 64 bit<br><br>* Ubuntu 18.04 64 bit<br><br>* Ubuntu 20.04 64 bit<br><br>* Ubuntu 22.04 64 bit<br><br>* Ubuntu 24.04 64 bit |
|Rocky Linux |Rocky Linux 8.5 64 bit |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YCa6L-H5bel5YW36Ieq5Yqo5byA5ZCv"></span>
### Automatically enable multiqueue via the tool


1. Log in to an ECS instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check whether the network interface supports the multiqueue feature and the number of enabled queues.

   > Replace `eth0` with the name of the target network interface.   
   

   ```Plain Text
   ethtool -l eth0
   ```
   

   For example:

   > In the command output, if the `Combined` parameter values under `Pre-set maximums` and `Current hardware settings`​ are the same, it means that the multiqueue is enabled for the network interface. And no further actions are required.   
   

3. Execute the following commands to configure the extra\-tools software source or download and install the package.



<Tabs>
<Tab zoneid="JzQl2BmPvU" title="veLinux">
<TabTitle>veLinux</TabTitle>

* veLinux 1.0

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/velinux/ orion main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/velinux/GPG-KEY-system | apt-key add -
   ```
   

* veLinux 2.0

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/velinux/ lyra main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/velinux/GPG-KEY-system | apt-key add -
   ```
   

* veLinux 1.0 CentOS Compatible

   ```Plain Text
   echo -e '[extra-tools]\nname= extra-tools\nbaseurl=http://mirrors.ivolces.com/extra-tools/centos/7/rpms/\nenabled=1\ngpgcheck=0' >> /etc/yum.repos.d/extra-tools.repo
   ```
   


</Tab>
<Tab zoneid="Gn7fYdni92" title="CentOS">
<TabTitle>CentOS</TabTitle>

* CentOS 7.x

   ```Plain Text
   echo -e '[extra-tools]\nname= extra-tools\nbaseurl=http://mirrors.ivolces.com/extra-tools/centos/7/rpms/\nenabled=1\ngpgcheck=0' >> /etc/yum.repos.d/extra-tools.repo
   ```
   

* CentOS 8.3

   ```Plain Text
   echo -e '[extra-tools]\nname= extra-tools\nbaseurl=http://mirrors.ivolces.com/extra-tools/centos/8/rpms/\nenabled=1\ngpgcheck=0' >> /etc/yum.repos.d/extra-tools.repo
   ```
   

* CentOS Stream 9

   ```Plain Text
   echo -e '[extra-tools]\nname= extra-tools\nbaseurl=http://mirrors.ivolces.com/extra-tools/centos/9/rpms/\nenabled=1\ngpgcheck=0' >> /etc/yum.repos.d/extra-tools.repo
   ```
   


</Tab>
<Tab zoneid="r55rETz6yE" title="RHEL">
<TabTitle>RHEL</TabTitle>

* RHEL 7.8

   ```Plain Text
   wget http://mirrors.ivolces.com/extra-tools/centos/7/rpms/adjust-nic-queue-1.0.6-1.ve.noarch.rpm
   ```
   

* RHEL 8.8

   ```Plain Text
   wget http://mirrors.ivolces.com/extra-tools/centos/8/rpms/adjust-nic-queue-1.0.6-1.ve.noarch.rpm
   ```
   

* RHEL 9.2 / RHEL 9.3

   ```Plain Text
   wget http://mirrors.ivolces.com/extra-tools/centos/9/rpms/adjust-nic-queue-1.0.6-1.ve2.noarch.rpm
   ```
   


</Tab>
<Tab zoneid="C6lqHhqe9E" title="Debian">
<TabTitle>Debian</TabTitle>

* Debian 9

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/debian/ stretch main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | apt-key add -
   ```
   

* Debian 10

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/debian/ buster main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | apt-key add -
   ```
   

* Debian 11

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/debian/ bullseye main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | apt-key add -
   ```
   


</Tab>
<Tab zoneid="JNiyirw2kL" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

* Ubuntu 16.04

   ```Plain Text
   echo 'deb [arch=amd64] http://mirrors.ivolces.com/extra-tools/ubuntu/ xenial main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
   ```
   

* Ubuntu 18.04

   ```Plain Text
   echo 'deb [arch=amd64] http://mirrors.ivolces.com/extra-tools/ubuntu/ bionic main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
   ```
   

* Ubuntu 20.04

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/ubuntu/ focal main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
   ```
   

* Ubuntu 22.04

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/ubuntu/ jammy main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
   ```
   

* Ubuntu 24.04

   ```Plain Text
   echo 'deb http://mirrors.ivolces.com/extra-tools/ubuntu/ noble main' >> /etc/apt/sources.list.d/extra-tools.list
   wget -O - http://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
   ```
   


</Tab>
<Tab zoneid="jLFrIsGfdK" title="Rocky Linux">
<TabTitle>Rocky Linux</TabTitle>

Rocky Linux 8.5

```Plain Text
echo -e '[extra-tools]\nname= extra-tools\nbaseurl=http://mirrors.ivolces.com/extra-tools/rockylinux/8.5/rpms/\nenabled=1\ngpgcheck=0' >> /etc/yum.repos.d/extra-tools.repo
```



</Tab>
</Tabs>



4. Execute the following commands to install the network interface multiqueue automatic configuration tool (adjust\-nic\-queue).



<Tabs>
<Tab zoneid="KhTU3mbLEx" title="veLinux 1.0 CentOS Compatible/CentOS/Rocky Linux">
<TabTitle>veLinux 1.0 CentOS Compatible/CentOS/Rocky Linux</TabTitle>

```Plain Text
yum makecache
yum install -y adjust-nic-queue
```



</Tab>
<Tab zoneid="e9f281BEMi" title="RHEL">
<TabTitle>RHEL</TabTitle>

* RHEL 7.8 / RHEL 8.8

   ```Plain Text
   rpm -ivh adjust-nic-queue-1.0.6-1.ve.noarch.rpm
   ```
   

* RHEL 9.2 / RHEL 9.3

   ```Plain Text
   rpm -ivh adjust-nic-queue-1.0.6-1.ve2.noarch.rpm
   ```
   


</Tab>
<Tab zoneid="lREvtHQ0xb" title="veLinux 1.0 & 2.0/Debian/Ubuntu">
<TabTitle>veLinux 1.0 & 2.0/Debian/Ubuntu</TabTitle>

```Plain Text
apt-get update
apt-get install -y adjust-nic-queue
```



</Tab>
</Tabs>



5. After being installed, adjust\-nic\-queue automatically enables multiqueue for the primary and secondary network interfaces associated with the instance.

   > If you associate a new secondary network interface after installing the tool, restart the instance. This allows the tool to automatically enable the multiqueue feature of the new network interface when the instance restarts.   
   

6. Execute the following command to verify whether you enable the multiqueue feature.

   > Replace `eth0` with the name of the target network interface.   
   

   ```Plain Text
   ethtool -l eth0
   ```
   

   If the output appears as shown below, the multiqueue is enabled for the network interface `eth0`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e52bf93a48b8d68429c149ddcbc50582.png) </span>


<span id=".5omL5Yqo5byA5ZCv"></span>
### Manually enable multiqueue


1. Log in to an ECS instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check whether the network interface supports the multiqueue feature and the number of enabled queues.

   > Replace `eth0` in the command with the name of the target network interface.   
   

   ```Plain Text
   ethtool -l eth0
   ```
   

   For example:

   > In the command output, if the `Combined` parameter value is the same under `Pre-set maximums` and `Current hardware settings`, it means that the multiqueue is enabled for the network interface. And no further actions are required.   
   

3. Execute the following command to manually adjust the queue count for the primary or secondary network interface to the maximum value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>eth0</code> in the command with the name of the target primary or secondary network interface.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>4</code> in the command with the maximum number of queues supported by the network interface.   </div>
   

   ```Plain Text
   ethtool -L eth0 combined 4
   ```
   

4. Execute the following command to verify whether you enable the multiqueue feature.

   > Replace `eth0` with the name of the target network interface.   
   

   ```Plain Text
   ethtool -l eth0
   ```
   

   If the output appears as shown below, the multiqueue is enabled for the network interface `eth0`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e52bf93a48b8d68429c149ddcbc50582.png) </span>
