---
title: "Solution for SSH start failure"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_SSHD_Not_Starting"
---

This topic describes how to troubleshoot and resolve the issue where the SSH service fails to start even though no error messages are displayed when you use the service or systemctl command to start it in a Linux instance environment.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## **Causes**

This issue is usually caused by an abnormal configuration of the PATH environment variable or the removal of files related to the SSH package.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check whether the environment variable configuration is specified as expected.

   ```Plain Text
   echo $PATH
   ```
   

   * Normally, information similar to the following is returned. This value is the default value of the PATH environment variable.

      ```Plain Text
      /usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
      ```
      

   * If other information (not the default value) is returned, the environment variable is altered from its default. Execute the following command to reset the environment variable.

      ```Plain Text
      export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
      ```
      

3. Execute the following command to find and confirm the path of the SSHD program. Then, determine whether files related to the SSH software package are removed.

   ```Plain Text
   find / -name sshd
   ```
   

   * If the output shows information similar to the following, the default path of the SSHD program exists (the files exist). Skip the subsequent operations.

      ```Plain Text
      /usr/sbin/sshd
      ```
      

   * If no similar information is returned after you execute the `find / -name sshd` command, the files do not exist. Continue with the subsequent operations.

      1. Execute the following command to reinstall the SSH package.

      ```Plain Text
      yum install -y openssh
      ```
      

      2. Execute the following command to restart the SSH service.

      ```Plain Text
      systemctl restart sshd.service
      ```
      

      3. Execute the following command to view the SSH service status.

         ```Plain Text
         systemctl status sshd.service
         ```
         

         If the following output is displayed, the SSH service is running.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b835aa435417b6ff1e52357b0d8029b.png) </span>
