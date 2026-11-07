---
title: "Verifying the CLB service"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-06"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

This topic introduces how to verify that the Layer\-7 Classic Load Balancer (CLB) service can provide ACTIVE service.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. View and record the EIP of the CLB instance on the CLB Instances page.

2. Add the following domain name mapping in the local PC's hosts file to map the domain name `www.test.com` to the CLB's EIP.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8adfedf3f2ac924e072b9fe572d1b1af.png) </span>

3. In the local PC's command line window, run the following command to check if the domain mapping succeeded.

   `ping www.test.com`

   If ping responds successfully, it means the domain mapping succeeded.

4. Use the local browser to access `https://www.test.com/ECS01` and `https://www.test.com/ECS02` respectively. If the interface sequentially displays the backend service pages deployed in backend server groups group01 and group02, it indicates that the Layer\-7 CLB can forward different business requests to backend servers based on different forwarding rules normally.
