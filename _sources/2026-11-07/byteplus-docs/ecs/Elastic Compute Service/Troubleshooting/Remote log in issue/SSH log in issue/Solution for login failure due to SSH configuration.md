---
title: "Solution for login failure due to SSH configuration"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_SSH_Configuration_Issues_Causing_Log_In_Failures"
---

This topic describes how to troubleshoot and resolve SSH login failures on Linux instances caused by improper SSH configurations or system parameter settings. These issues include SSH access permission exceptions, missing critical SSH files or directories, SSH login errors, and unrunning service processes in the instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you modify the configuration or data of an instance, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) first to improve fault tolerance and ensure data security.

<span id=".U1NI6K6_6Zeu5p2D6ZmQ5byC5bi4"></span>
## SSH access permission exceptions

If you cannot log in to a Linux instance due to abnormal SSH access permission configurations such as insufficient access permissions, you can resolve the issue by performing the following operations.


1. Enter the Linux operating system in single\-user mode. For more information, see [Entering single-user mode](https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode).

2. Execute the following command to reset the permissions of the `/var/empty/sshd` directory.

   ```Plain Text
   chmod 711 /var/empty/sshd
   ```
   

3. Restart the instance to make the configuration take effect.


<span id=".U1NI5YWz6ZSu5paH5Lu25oiW55uu5b2V5Lii5aSx"></span>
## Missing critical SSH files or directories

If critical files or directories required for SSH access are missing, such as the `sshd_config` configuration file, you may be unable to log in to the Linux instance. You can resolve the issue by performing the following operations.


1. Enter the Linux operating system in single\-user mode. For more information, see [Entering single-user mode](https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode).

2. Execute the following command to check whether the `sshd_config` configuration file exists.

   ```Plain Text
   ll /etc/ssh/sshd_config
   ```
   

3. (Optional) If the `sshd_config` configuration file exists, skip this step. If the `sshd_config` configuration file does not exist, nor do you have a previously backed up sshd_config.bak file, perform the following operations:

   1. Execute the following command to reinstall the openssh\-server service.

      * Debian system: `sudo apt-get install --reinstall openssh-server`

      * CentOS system: `yum reinstall openssh-server`

   2. Restart the instance to make the configuration take effect.


<span id=".U1NI55m75b2V5oql6ZSZ"></span>
## SSH login errors

When the root user attempts to log in to a Linux ECS instance with the correct password by using a local SSH client, the `Permission denied, please try again` error message is displayed. You can resolve the issue by performing the following operations.

> Two possible causes for this issue exist. One is that root user login is disabled on the ECS instance, and the other is that the SELinux service is enabled on the Linux system, which prevents both root users and ordinary users from logging in.


<span id=".56aB5q2icm9vdOeUqOaIt-eZu-W9leW8lei1t-eahOmXrumimA=="></span>
### Issue arising from prohibited root user login


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the `PermitRootLogin` or `PasswordAuthentication` configuration.

   ```Plain Text
   cat /etc/ssh/sshd_config
   ```
   

3. If the `PermitRootLogin` and `PasswordAuthentication` parameters are set to `no`, root user login and password\-based login are prohibited. Continue with the following operation. Otherwise, skip this subsection and follow the instructions in [Issue caused by the SELinux service](https://docs.byteplus.com/en/docs/ecs/Solution_for_SSH_Configuration_Issues_Causing_Log_In_Failures#.c2VsaW51eOacjeWKoeW8lei1t-eahOmXrumimA==) to troubleshoot and resolve the issue.

4. Modify the `PermitRootLogin` and `PasswordAuthentication` parameters.

   1. Execute the following command to open the SSH configuration file.

      ```Plain Text
      vi /etc/ssh/sshd_config
      ```
      

   2. Modify the values for the `PermitRootLogin` and `PasswordAuthentication` parameters.

      * To enable root user login, set the `PermitRootLogin` parameter to `yes`.

      * To use password\-based login, set the `PasswordAuthentication` parameter to `yes`.

   3. Press the "Esc" key and enter `:wq` to save the modifications.

5. Execute the following command to restart the SSH service for the modifications to take effect.

   ```Plain Text
   systemctl restart sshd.service
   ```
   


<span id=".U0VMaW51eOacjeWKoeW8lei1t-eahOmXrumimA=="></span>
### Issue caused by the SELinux service

You can temporarily or permanently disable the SELinux service based on your needs to resolve SSH connection issues.

**Step 1: Check SELinux service status**


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current SELinux service status.

   ```Plain Text
   /usr/sbin/sestatus -v
   ```
   

3. Information similar to the following is displayed:

   ```Plain Text
   SELinux status:       enabled
   ```
   

   ```Plain Text
   SELinux status:       disabled
   ```
   

   * enabled: The SELinux service is enabled.

   * disabled: The SELinux service is disabled.


**Step 2: Disable the SELinux service**

You can disable the SELinux service either temporarily or permanently based on your specific needs. A temporary disablement of SELinux is not persistent. The service will automatically re\-enable itself once the instance restarts.


* **Temporarily disable the SELinux service**

   Execute the following command to temporarily disable SELinux.

   ```Plain Text
   setenforce 0
   ```
   

* **Permanently disable the SELinux service**:

   1. Execute the following command to permanently disable the SELinux service.

      ```Plain Text
      vim /etc/selinux/config
      
      SELINUX=disabled
      ```
      

   2. Enter `:wq` to save the modification.

   3. Restart the instance to make the configuration take effect.


<span id=".5pyN5Yqh6L-b56iL5pyq5aSE5LqO6L-Q6KGM5Lit"></span>
## Unrunning service processes

When the service process is not running (not in the listening state), you may be unable to access the Linux instance. This issue can be resolved by starting common services. In the example provided in this section, CentOS 7 is used.

<span id=".5pON5L2c6K-05piO"></span>
### Usage note

The following table lists common services in Linux instances and the impact when the services are not running.


|**Service name** |**Description** |**Default listening port** |**Impact when not running** |
|---|---|---|---|
|SSH |Remote connection |22 |SSH remote connection failure |
|Web |Website service |80 (HTTP) and 443 (HTTPS) |Website access failure |
|MySQL |MySQL database |3306 |Database access failure |


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check the port listening status of the target service.

   ```Plain Text
   netstat -ntlp | grep [$Port]
   ```
   

   > [$Port] refers to the port that the target service listens on. Use the port you are actually using. If you have modified the default port of the target service, replace it with the modified port number.   
   

   * If the target port information is returned and the listening status is **LISTEN**, the target service is running and there is no need to start it. Skip the following steps.

   * If there is no response, that is, the port of the target service is not in listening state, perform the following operations.

3. Execute the following command to start the target service.

   ```Plain Text
   systemctl start [$Service]
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">[$Service] refers to the name of the target service. Use the name of the service you are actually using.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to start the SSH service, the service name is <code>sshd</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To start a third\-party service, such as "Nginx", "Tomcat", or "MySQL", refer to the official website of the third\-party service to obtain the corresponding start command.   </div>
   

   * If there is no response, the command is executed as expected. In this case, skip the following steps.

   * If an error is returned, resolve the issue by referring to the error message, and then continue with the following operations.

4. Execute the following command to check the status of the target service.

   ```Plain Text
   systemctl status [$Service]
   ```
   

5. If information similar to the following is displayed, the target service is in **running** state.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8220f91dda06fce4783b99e51b1dba3.png) </span>

   > In the example provided in this section, the SSH service is used. Refer to your actual response.   
   

6. Execute the following command to check the port listening status of the target service.

   ```Plain Text
   netstat -ntlp | grep [$Port]
   ```
   

7. If information similar to the following is displayed, the port of the target service is in listening state, that is, the target service is running.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_431df377215b5e9e900d7f94fb6cefa4.png) </span>
