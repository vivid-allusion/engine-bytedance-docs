---
title: "Quick start"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-01"
---

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

This topic introduces how to quickly configure Layer\-7 Classic Load Balancer (CLB) services. After configuration, the Layer\-7 CLB instance listens to requests from HTTPS protocol on port 443, and Elastic Compute Service instances in backend server groups group01 and group02 provide services for different applications through HTTPS port 443 respectively.

Layer\-7 CLB is applicable to scenarios where different applications provide services for entities beyond the local VPC through the same domain name, and access requests from different applications are distributed to different backend server groups for processing based on the CLB forwarding rules. Only HTTP and HTTPS protocol listeners support forwarding rules configuration. If your application requires higher security, use HTTPS protocol; otherwise, HTTP protocol is sufficient.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Before configuring the CLB instance, prepare the following items:


* Prepare a VPC environment: The CLB instance and backend servers providing services must be in the same VPC. When creating a VPC, choose a region geographically closest to the source clients to reduce latency and improve download speed. You can see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC) to create a new VPC.

* Build your backend server environment within this VPC: create 2 Elastic Compute Service instances and deploy services to provide external access. For detailed operations, see [Purchasing Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [Building backend services](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).

* Complete the CLB instance Type and specification planning: It is recommended to see Product Type and specification selection based on the actual business scenario and business volume.Product

* Ensure the security group attached to the Elastic Compute Service instance has opened the service port (TCP port 443): See [Configuring backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

* Prepare a certificate: Upload your server certificate to the CLB console for HTTPS protocol authentication. For detailed operations, see Creating a certificate.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Make sure the domain name in the certificate matches the domain name used by the business; the example domain here is <code>www.test.com</code>.   </div>
   

<span id=".5pON5L2c5rWB56iL"></span>
## Procedures

The operation procedure for Layer\-7 CLB is shown as follows.


1. Create a CLB instance: Create a CLB instance based on actual business scenarios and volume.

2. [Create backend server groups](https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-03): Create two backend server groups and add backend servers that provide actual services to each group.

3. [Create listener](https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-04): Add a listener to the instance and associate the certificate and the default server group.

4. [Configure forwarding rules](https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-05): Configure forwarding rules to route requests from different services to corresponding backend server groups for processing.

5. Verification of CLB service: Verify that the CLB can forward access requests to the corresponding backend servers based on the forwarding rules.
