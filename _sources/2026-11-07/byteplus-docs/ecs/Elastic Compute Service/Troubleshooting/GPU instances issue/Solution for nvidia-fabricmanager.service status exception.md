---
title: "Solution for nvidia-fabricmanager.service status exception"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_nvidia_fabricmanager_service_status_exception"
---

This topic mainly describes how to troubleshoot the "nvidia\-fabricmanager.service" exception when you use a GPU instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to[ Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance). 

2. Execute the following command to confirm whether the `nvidia-fabricmanager` service status is `active (running)`.

   ```Plain Text
   systemctl status nvidia-fabricmanager.service
   ```
   

   A sample of normal output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68b938b3f3fe28ced541ae140e9f3e64.png) </span>

3. If the service is not in `active (running)` status, perform the following operations:

   1. Confirm whether the instance needs the `nvidia-fabricmanager.service` service.

      Only for HPC\-optimized instances, the `nvidia-fabricmanager.service` service is needed. In instances of other types, it is considered normal for the `nvidia-fabricmanager` service to have an abnormal status or to be absent. 

   2. Confirm whether the version of `nvidia-fabricmanager.service` service matches that of the instance driver.

      1. Execute the following command to view the service version.

         ```Plain Text
         /usr/bin/nv-fabricmanager -v
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fdc5c62cf5bac6a2853d24c3b67ba262.png) </span>

      2. Execute the following command to view the driver version.

         ```Plain Text
         nvidia-smi
         ```
         

      3. Check whether the versions of the two match each other.

         * To start the service successfully, make sure the two versions match.

         * If the versions match, execute the following command to restart and then check the service status.

            ```Plain Text
            systemctl restart nvidia-fabricmanager.service 
            ```
            

      4. To obtain support when the method described in this topic does not resolve the exception,  contact your account manager.
