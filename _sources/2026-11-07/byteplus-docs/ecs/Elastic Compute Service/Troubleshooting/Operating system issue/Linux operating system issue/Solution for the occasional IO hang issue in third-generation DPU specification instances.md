---
title: "Solution for the occasional IO hang issue in third-generation DPU specification instances caused by operating system kernel issues"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/blk-none"
---

<span id="6JR1fk2k"></span>
## Issue description

The third\-generation DPU specification instances (for example, General\-purpose g3a/g3i, Compute\-optimized c3a/c3i, Memory\-optimized r3a/r3i) experience IO hang issues, where the disk mounted on the instance encounters IO operations that remain suspended or stagnant for a long time, leading to slow or even unresponsive system performance.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

Due to the different configurations of operating system kernels, certain kernel versions may cause third\-generation DPU specification instances (for example, General\-purpose g3a/g3i, Compute\-optimized c3a/c3i, Memory\-optimized r3a/r3i) to encounter various IO hang issues.


* **Older kernel version of the operating system**

   For operating systems with lower kernel versions (e.g., CentOS 7.x, Ubuntu 16.04, Ubuntu 18.04, Debian 9), under high IO merging and deep queue scenarios, virtio_blk defects may be triggered, posing a low risk of IO hang issues. [Solutions](https://docs.byteplus.com/en/docs/ecs/blk-none#SQUm2GMR).

* **Mutual blocking between WBT and block\-core**

   Using certain kernel versions of veLinux, CentOS, and Ubuntu operating systems in high\-load scenarios may trigger kernel timing exception issues, further causing mutual blockage between WBT (Writeback Threads) and block\-core, leading to IO hang issues. [Solutions](https://docs.byteplus.com/en/docs/ecs/blk-none#aKrXCWiM).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use VNC to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance">log in to the target instance</a> and execute the <code>dmesg -T</code> command. If the highlighted content in the red box as shown below appears in the output, it indicates that the IO hang issue of your instance is caused by mutual blocking between WBT and block\-core.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46791d0f98990990186ac742544111e9.png" width="425px" />   </div>
   

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

<span id="SQUm2GMR"></span>
### The operating system kernel version is outdated.

The blk\-none tool provided by the platform sets the disk scheduling algorithm to `none` or `noop` based on the disk type of your instance to prevent such issues.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2.  **(Optional)**  Manually adjust the disk scheduling algorithm to temporarily resolve the issue.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are temporarily unable to restart the instance due to business constraints, you can follow the instructions in this step to resolve the issue temporarily. However, the configuration becomes invalid after the instance restarts.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you can restart the instance, you can skip this step and proceed to Step 3 where you can use the blk\-none tool to persistently resolve the issue.   </div>
   

   1. Execute the following command to view disk information.

      ```Bash
      lsblk
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8950aaf3526c718465c989910cdf5b63.png) </span>

   2. Manually configure the scheduling algorithm for each disk.

      > Replace `<vdx>` in the command with the actual disk name obtained from the query in the previous step, for example, vda.      
      

      ```Bash
      echo "none" > /sys/block/<vdx>/queue/scheduler
      ```
      

3. Install the blk\-none tool to resolve the issue persistently.

   1. Execute the following command to install the blk\-none tool.

      * Installation over the BytePlus private network

         * **CentOS 7.x**

            ```Plain Text
            wget http://mirrors.ivolces.com/extra-tools/centos/7/rpms/blk-none-v1.0.1-1.ve1.x86_64.rpm
            yum install ./blk-none-v1.0.1-1.ve1.x86_64.rpm        
            ```
            

         * **Ubuntu 16.04/Ubuntu 18.04/Debian 9**

            ```Bash
            wget http://mirrors.ivolces.com/extra-tools/ubuntu/pool/main/b/blk-none/blk-none_1.0.1_amd64.deb
            apt install ./blk-none_1.0.1_amd64.deb  
            ```
            

      * Installation over the Internet

         * **CentOS 7.x**

            ```Bash
            wget https://blk-none.tos-cn-beijing.volces.com/blk-none-v1.0.1-1.ve1.x86_64.rpm
            yum install ./blk-none-v1.0.1-1.ve1.x86_64.rpm        
            ```
            

         * **Ubuntu 16.04/Ubuntu 18.04/Debian 9**

            ```Bash
            wget https://blk-none.tos-cn-beijing.volces.com/blk-none_1.0.1_amd64.deb
            apt install ./blk-none_1.0.1_amd64.deb  
            ```
            

   2. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances). The tool will take effect automatically and complete the configuration adjustments once the instance starts.

      > After the tool takes effect, you do not need to restart the instance again when you mount a new data volume. The tool will automatically adjust the configuration for the new data volume.      
      

<span id="aKrXCWiM"></span>
### Mutual blocking between WBT and block\-core

The platform provides you with bytedance\-iohung\-tools, which detects whether the current operating system has an IO hang issue. If such an issue exists, the tool will attempt to avoid IO hang caused by WBT by modifying the `wbt_lat_usec` parameter.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The bytedance\-iohung\-tools tool is currently only supported on the following operating systems:</div>


<div data-tips="true" data-tips-type="default">
|Operating systems |Versions |Kernel version |
|---|---|---|
|veLinux |* veLinux 1.0 64 bit<br><br>* veLinux 1.0 CentOS compatible version 64 bit |4.10.x ≤ kernel version ≤ 6.8.x |
|CentOS |* CentOS 8.3 64 bit<br><br>* CentOS Stream 8 64 bit ||
|Ubuntu |* Ubuntu 16.04 64 bit<br><br>* Ubuntu 18.04 64 bit<br><br>* Ubuntu 20.04 64 bit<br><br>* Ubuntu 22.04 64 bit<br><br>* Ubuntu 24.04 64 bit ||
|Debian |* Debian 10 64 bit<br><br>* Debian 11 64 bit ||
</div>



1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. Execute the following command to configure the extra\-tools software repository.

   
   <Tabs>
   <Tab zoneid="PHjHY7uAEN" title="veLinux">
   <TabTitle>veLinux</TabTitle>
   
   * **veLinux 1.0**
   
      ```Bash
      wget -O - https://mirrors.ivolces.com/extra-tools/velinux/GPG-KEY-system | apt-key add -
      cat << EOF > /etc/apt/sources.list.d/extra-tools.list
      deb https://mirrors.ivolces.com/extra-tools/velinux orion main
      EOF
      ```
      
   
   * **veLinux 1.0 CentOS Compatible**
   
      ```Bash
      cat << EOF > /etc/yum.repos.d/extra-tools.repo
      [extra-tools]
      name=extra-tools
      baseurl=https://mirrors.ivolces.com/extra-tools/velinux-centos/1/rpm
      gpgcheck=1
      gpgkey=https://mirrors.ivolces.com/extra-tools/velinux-centos/GPG-KEY-system
      EOF
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="tGxFtHtVYY" title="CentOS">
   <TabTitle>CentOS</TabTitle>
   
   **CentOS 8.3/CentOS Stream 8**
   
   ```Bash
   cat << EOF > /etc/yum.repos.d/extra-tools.repo
   [extra-tools]
   name=extra-tools
   baseurl=https://mirrors.ivolces.com/extra-tools/centos/8/rpms
   gpgcheck=1
   gpgkey=https://mirrors.ivolces.com/extra-tools/centos/GPG-KEY-system
   EOF
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="uGzdGs5mQz" title="Ubuntu">
   <TabTitle>Ubuntu</TabTitle>
   
   * **Ubuntu 16.04**
   
      ```Bash
      wget -O - https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
      cat << EOF > /etc/apt/sources.list.d/extra-tools.list
      deb https://mirrors.ivolces.com/extra-tools/ubuntu xenial main
      EOF
      ```
      
   
   * **Ubuntu 18.04**
   
      ```Bash
      wget -O - https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
      cat << EOF > /etc/apt/sources.list.d/extra-tools.list
      deb https://mirrors.ivolces.com/extra-tools/ubuntu bionic main
      EOF
      ```
      
   
   * **Ubuntu 20.04**
   
      ```Bash
      wget -O - https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | apt-key add -
      cat << EOF > /etc/apt/sources.list.d/extra-tools.list
      deb https://mirrors.ivolces.com/extra-tools/ubuntu focal main
      EOF
      ```
      
   
   * **Ubuntu 22.04**
   
      ```Bash
      wget -qO- https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/keyrings/extra-tools.gpg
      echo "deb [signed-by=/etc/apt/keyrings/extra-tools.gpg] https://mirrors.ivolces.com/extra-tools/ubuntu jammy main" | sudo tee /etc/apt/sources.list.d/extra-tools.list
      ```
      
   
   * **Ubuntu** ** 24.04**
   
      ```Bash
      wget -qO- https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/keyrings/extra-tools.gpg
      echo "deb [signed-by=/etc/apt/keyrings/extra-tools.gpg] https://mirrors.ivolces.com/extra-tools/ubuntu noble main" | sudo tee /etc/apt/sources.list.d/extra-tools.list
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="lf1e7s8Det" title="Debian">
   <TabTitle>Debian</TabTitle>
   
   * **Debian 10**
   
      ```Bash
      wget -O - https://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | apt-key add -
      cat << EOF > /etc/apt/sources.list.d/extra-tools.list && apt-get update
      deb https://mirrors.ivolces.com/extra-tools/debian buster main
      EOF
      ```
      
   
   * **Debian 11**
   
      ```Bash
      wget -O - https://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | apt-key add -
      cat << EOF > /etc/apt/sources.list.d/extra-tools.list && apt-get update
      deb https://mirrors.ivolces.com/extra-tools/debian bullseye main
      EOF
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. Execute the following commands to update the software repository.

   * **veLinux/Ubuntu/Debian**

      ```Bash
      apt-get update
      ```
      

   * **veLinux CentOS compatible version/CentOS/CentOS Stream**

      ```Bash
      yum makecache
      ```
      

4. Run the following command to install the bytedance\-iohung\-tools tool.

   * **veLinux/Ubuntu/Debian**

      ```Bash
      apt-get install -y bytedance-os-assistants
      ```
      

   * **veLinux CentOS Compatible version/CentOS/CentOS Stream**

      ```Bash
      yum install -y bytedance-os-assistants
      ```
      

5. Execute the following command to check the tool operating status.

   ```Bash
   systemctl status bytedance-iohung-tools.service
   ```
   

   If there is output, it indicates that the tool is installed and functioning properly.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ece33c7685bd546eae7e42231a17111e.png) </span>

6.  **(Optional)**  You can also execute the following command as needed to delete the installed bytedance\-iohung\-tools tool.

   * **veLinux/Ubuntu**

      ```Bash
      apt-get remove -y bytedance-os-assistants
      ```
      

   * **veLinux CentOS compatible version/CentOS/CentOS Stream**

      ```Bash
      yum remove -y bytedance-os-assistants
      ```
