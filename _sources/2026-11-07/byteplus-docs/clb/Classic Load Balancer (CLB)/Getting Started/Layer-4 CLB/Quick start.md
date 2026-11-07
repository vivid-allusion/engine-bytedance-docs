---
title: "Quick start"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-01"
---

<span id=".5Zy65pmv5Li-5L6L"></span>
## Scenario examples

This topic describes how to quickly configure a Layer\-4 Classic Load Balancer (CLB) instance with access request distribution capabilities. After configuration, the CLB instance listens to requests on TCP port 80, and the Elastic Compute Service instances in the backend server group provide services through TCP port 80.

Layer\-4 CLB is applicable for scenarios with a large amount of application access requests. Access requests can be distributed to multiple backend servers for processing through CLB. After the health check feature is enabled, CLB can automatically identify abnormal backend servers and distribute access requests to normal backend servers, avoiding single points of failure (SPOFs) and improving application availability.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Before configuring the CLB instance, you need to prepare the following:


* Prepare a VPC environment: The CLB instance should be in the same VPC as the backend servers providing services. When creating a VPC, it is recommended to select a region geographically closest to the source clients to reduce latency and improve download speed. You can see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC) to create a new VPC.

* Build your backend server environment within the VPC: create two Elastic Compute Service instances and deploy the services for external access. For detailed steps, see [Purchasing Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [Deploying Backend Services](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).

* Complete the CLB instance Type and specification planning: It is recommended to see Product Type and specification selection based on the actual business scenario and business volume.Product

* Ensure that the security group attached to the ECS instance has opened the service ports (TCP port 80) and allowed the CLB health check CIDR block: see Configuring backend server security group.


<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures

The configuration process for Layer\-4 CLB services is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84666d21154393b2a6f70608f866b704.png) </span>


1. Create CLB instance: Create a CLB instance based on the actual business scenario and business volume.

2. [Configure the backend server group](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-03): create the backend server group and add backend servers that provide the actual services.

3. [Create listener](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-04): add a listener to the CLB instance and associate it with the backend server group.

4. Verification: Verify that the configured CLB can correctly forward access requests to the backend server.
