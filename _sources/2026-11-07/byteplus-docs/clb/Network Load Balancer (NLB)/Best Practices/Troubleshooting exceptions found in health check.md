---
title: "Troubleshooting exceptions found in health check"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Troubleshooting-exceptions-found-in-health-check"
---

This article describes the possible causes and detailed troubleshooting procedures when the health check status of a backend server is abnormal.

<span id=".5q2l6aqk5LiA77ya5qOA5p-l6LSf6L295Z2H6KGh6YWN572u"></span>
## Step 1: Check the CLB configuration


* Confirm that the port of the backend server is consistent with the actual service port.

   On the **backend server** tab of the Server Group details page, view the port of the target backend server. If it is inconsistent with the actual service port, modify it to match the actual service port.

* When the health check protocol is HTTP, confirm that the health check configuration is correct.

   On the **Overview** tab of the server group details page, view the health check configuration. If the configuration is incorrect, click the **Edit health check** button in the upper\-right corner of the page to modify the health check path.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The health check path is a relative path. For example, if the link is <code>http://www.example.com/test/</code>, set the health check path to <code>/test/</code>.   </div>
   

<span id=".5q2l6aqk5LqM77ya5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo6YWN572u"></span>
## Step 2: Check the configuration of the backend server


* Check whether the security group associated with the backend server has allowed the health check CIDR block (the CIDR block of the NLB instance's subnet).

   If not, refer to [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL) to allow the CIDR block of all subnets of the NLB instance.

* Check the firewall configuration of the backend server.

   The internal firewall of the backend server is disabled by default. If the firewall is enabled, ensure that the health check CIDR block is allowed in the inbound rule of the firewall. For detailed firewall configuration steps, refer to [Windows firewall configuration](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.d2luZG93c-mYsueBq-WimQ==) or [Linux firewall configuration](https://developer.volcengine.com/articles/7270815826700140600).

* Check the route configuration of the backend server.

   Check whether the internal route of the backend server has been manually modified, and run the following command to check the default route of the primary network interface (for example, eth0):

   `route -n`

   Normally, the output should be as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f082770bded2b6c676694d874c367ac6.png) </span>

   If the first default route is not found in the route configuration, or if the default route does not point to the gateway of the VPC subnet where the backend server is located, modify the default route configuration.

* Check whether the backend server can provide services normally.

   On the client, run the `ping` command to check the connectivity.

* Check the load of the backend server.

   Check the load of the backend server. When the load is heavy and the connection response speed is slow, response timeout may occur. That is, the health check fails, and the backend server status is displayed as **abnormal**. In this case, you do not need to take any actions, and the backend server status will automatically return to normal after the load decreases.


<span id=".5q2l6aqk5LiJ77ya5qOA5p-l5ZCO56uv5pyN5Yqh6YWN572u"></span>
## Step 3: Check the backend service configuration


* Check whether the backend service listening port is open on `0.0.0.0`.

   Log into the ECS, and select an appropriate command based on the operating system of the ECS to check the configuration of the listening port. If the listening port of the corresponding backend service is closed on `0.0.0.0`, the health check may fail.

   * For Linux\-based Elastic Compute Service (ECS): `netstat -antup`

      The figure below indicates that the TCP listening port 80 of the backend service is open on `0.0.0.0`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08c03420cef43785463a6b19b8bbd9a2.png) </span>

   * For Windows\-based Elastic Compute Service (ECS): `netstat -ano`

      The figure below indicates that the TCP listening port 135 of the backend service is open on `0.0.0.0`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bc42cd88b4b052df30fc7e454e007ca.png) </span>
