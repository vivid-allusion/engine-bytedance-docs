---
title: "How to resolve the issue of being unable to remotely log in to the instance via SSH after upgrading OpenSSL"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/unable_to_log_in_via_SSH_remotely_after_upgrading_OpenSSL"
---

<span id="LZ2OMKhq"></span>
## Issue description

After OpenSSL of the operating system is upgraded to the latest version, remote login to the ECS instance by using the ECS Terminal or SSH command fails.

<span id="0zdqdZkj"></span>
## Causes

This may be because SSH relies on certain features provided by an older version of OpenSSL. The upgraded OpenSSL version is incompatible with the installed SSH, preventing remote login to the ECS instance by using the ECS terminal or SSH command.

<span id="LnyhkFjK"></span>
## Solutions

You can upgrade SSH to the latest version to resolve the version incompatibility between OpenSSL and SSH.


1. [Use VNC to log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your ECS instance uses key pair login, we recommend that you reset it to password login. <a href="https://docs.byteplus.com/en/docs/ecs/Resetting-passwords">Learn more</a>.   </div>
   

2. Check whether the SSH and OpenSSL versions are compatible.

   
   <Tabs>
   <Tab zoneid="bbr3WC3RCu" title="Check based on the SSH version">
   <TabTitle>Check based on the SSH version</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   ssh -V
   ```
   
   
   If the following output is displayed, your SSH is incompatible with the upgraded OpenSSL version. We recommend that you upgrade SSH to the latest version according to the following instructions. 
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e7fe9d8e7ffa1553f969fda54040c75.png) </span>
   
   
   </Tab>
   <Tab zoneid="GWkeFbu9da" title="Check based on system logs">
   <TabTitle>Check based on system logs</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   tail -f /var/log/messages
   ```
   
   
   If the following output is displayed, your SSH is incompatible with the upgraded OpenSSL version. We recommend that you upgrade SSH to the latest version according to the following instructions. 
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9894784043a4c2926959157b738ffa69.png) </span>
   
   
   </Tab>
   </Tabs>
   

3. Execute the following command to upgrade `openssh-server` to the latest version.

   
   <Tabs>
   <Tab zoneid="T2T7QmVY" title="CentOS, RHEL, Rocky Linux, and AlmaLinux series">
   <TabTitle>CentOS, RHEL, Rocky Linux, and AlmaLinux series</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   yum install openssh-server -y
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="T1OUCPpO" title="Ubuntu and Debian series">
   <TabTitle>Ubuntu and Debian series</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   apt-get install openssh-server -y
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="fYgfc8If" title="SUSE and OpenSUSE series">
   <TabTitle>SUSE and OpenSUSE series</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   zypper install -y openssh-server
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="bXGjcAJy" title="Fedora series">
   <TabTitle>Fedora series</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   dnf install openssh-server -y
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

4. Execute the following command to restart the SSH service.

   ```Plain Text
   systemctl restart sshd
   ```
   

5. Use the [ECS terminal](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or SSH command to check whether you can log in to the target instance as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c48af4cb420d367256ce828d9ad72ee6.png) </span>
