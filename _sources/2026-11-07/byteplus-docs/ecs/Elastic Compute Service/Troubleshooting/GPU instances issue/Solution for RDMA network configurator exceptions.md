---
title: "Solution for RDMA network configurator exceptions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_RDMA_Network_Configurator_Not_Running_Normally"
---

This topic describes how to troubleshoot RDMA network configurator exceptions.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance). 

2. Confirm whether the service status of `rdma-agent.service` is `active (exited)`. For more information about RDMA Agent, refer to [Installing RDMA Agent in HPC-optimized instances](https://docs.byteplus.com/en/docs/gpu/Installing_RDMA_Agent_in_HPC-optimized_instances?lang=zh).

   ```Plain Text
   systemctl status rdma-agent.service
   ```
   

   A sample of normal output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa3ba0674f505edfbb569594a166d6b2.png) </span>

3. Perform the following operations when the service status is not `active (exited)`:

   1. Check whether your instance supports RDMA. The rdma\-agent.service service is required only when the instance supports RDMA.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only HPC\-optimized instances support RDMA. For more information, see<a href="https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h"> HPC\-optimized instances</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the instance does not support RDMA network, it is considered normal for the <code>rdma-agent.service</code> service to have an abnormal status or not exist.      </div>
      

   2. If your instance supports RDMA network, execute the following command to restart the service.

      ```Plain Text
      systemctl restart rdma-agent.service        
      ```
      

   3. After the service is restarted, execute the following command again to check whether the service status is `active (exited)`.

      ```Plain Text
      systemctl status rdma-agent.service
      ```
      

   4. To obtain technical support when the method described in this topic does not resolve your issue, contact your account manager.
