---
title: "Health check exception troubleshooting guide"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Troubleshooting-health-check-exceptions"
---

This topic introduces possible causes and detailed steps for handling backend server health check status exceptions, guiding you to locate and resolve the issues.

<span id=".5aSE55CG5q2l6aqk"></span>
## Handling steps

<span id="H0FKYU2n"></span>
### Check CLB configuration


* Verify that the backend server port configuration matches the actual service port.

   On the Server Group tab of the Classic Load Balancer (CLB) details page, view the port of the target backend server. If it is inconsistent with the actual service port, modify it to match the actual service port.

* Verify the health check path configuration is correct.

   The health check path is a relative path. For example, if the access link is http://www.example.com/test/, the health check path should be set to /test/. For detailed steps, see [Editing the health check](https://docs.byteplus.com/en/docs/clb/Editing-health-check).

   On the Listener tab of the Layer\-7 CLB details page, click Actions \> Edit health check on the right side of the target listener to modify the health check path.


<span id=".5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo6YWN572u"></span>
### Backend server configuration check


* Check whether the security group of the backend server allows access for the 100.64.0.0/10 CIDR block.

   If not allowed, add an inbound rule to the security group of the backend server to allow the 100.64.0.0/10 CIDR block. For detailed steps, see [Configuring the backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

* Check the backend server firewall configuration.

   The backend server firewall is disabled by default. If enabled, ensure the firewall inbound rules allow the 100.64.0.0/10 CIDR block.

* Check the backend server route configuration.

   Check whether the internal route of the backend server has been manually modified, and run the following command to check the default route of the primary network interface (for example, eth0):

   `route -n`

   The normal output is shown in the following figure:

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/f2172ba558a240ff8365976257b1e8d9.png) </span>

   If the default route is missing or does not point to the gateway of the VPC subnet where the backend server is located, modify the default route configuration.

* Check whether the backend server can provide service normally.

   On the client, run the ping command to check the connectivity.

* Check the backend server load.

   View the backend server load. If the load is high, slow connection response causes response timeout, leading to Health Check failure, and the backend server status shows as exception. No action is needed at this time; it will recover automatically when the load decreases.


<span id=".5qOA5p-l5ZCO56uv5pyN5Yqh6YWN572u"></span>
### Check backend service configuration


* Check if the Layer\-7 Health Check backend service forbids empty Host access.

   In the Layer\-7 Health Check configuration, the Health check domain name is optional. If the Health check domain name is not configured, the system defaults to the intranet IP Address with an empty Host. If the backend service forbids empty Host access, it may cause Health Check failure.

* Check whether the backend service for the layer 7 health check forbids GET or HEAD requests.

   Currently, layer 7 health checks use GET or HEAD requests to probe backend hosts. If the configured health check method is forbidden by the backend service, the health check will fail.

* Check if the backend service's listening port is on 0.0.0.0.

   After logging into the Elastic Compute Service (ECS), select the appropriate command to view based on the ECS operating system. If the corresponding backend service's listening port is not open on 0.0.0.0, it may cause the health check to fail.

   * For Linux\-based ECS: netstat \-antup

      For example, the image below shows that the backend service listens on port 80 using the TCP protocol type on 0.0.0.0.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0c6dc89b45f730d931c3d61d535fa8a1.png) </span>

   * For Windows\-based ECS: netstat \-ano

      For example, the image below shows that the backend service listens on port 135 using the TCP protocol type on 0.0.0.0.


&nbsp;
