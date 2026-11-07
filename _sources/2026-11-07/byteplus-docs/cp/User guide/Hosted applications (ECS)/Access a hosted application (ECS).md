---
title: "Access a hosted application (ECS)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Access_a_hosted_application_ECS"
---

Managed applications (ECS) support configuring public or internal load balancing as the traffic entry point. This document describes how to configure it.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The managed application (ECS) has been created and deployed. For detailed actions, see [Create and deploy a managed application (ECS)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_ECS).

* The load balancer instance has been created. The load balancer instance and the ECS instance to be deployed must be in the same VPC. For detailed instructions, see [Create a load balancing instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to access the current workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the application management page, select the target hosted application, click the application card, and go to the basic information tab for the current application.

3. Switch to the **application orchestration** tab, and in the **access method settings** section, configure the application's access method. The following access methods are supported. Please select as needed.


<span id=".5re75Yqg6LSf6L295Z2H6KGh77yI5YWs572R77yJ"></span>
### Add a public load balancer

Add a public load balancer to the application to enable other applications to access the current application via the public network.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure that the security group associated with the ECS instance allows traffic to the host ports that the application listens on; otherwise, the application cannot be accessed from the public network.</div>



1. Click **Add load balancing (public network)** , and configure the relevant information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Cloud Load Balancer (CLB) |Select the target CLB instance |
   |Scheduling algorithms |Rules for configuring listener request forwarding.<br><br><br>* **Weighted Round Robin**: traffic is forwarded based on weight values. The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>* **Weighted Least Connection**: traffic is forwarded first to the backend with the smallest real\-time ratio of connections to weight.<br><br>* **Source Hashing**: traffic is always forwarded to a single backend server if the hash of the source IP remains unchanged. |
   |Port mapping |Configure port mapping rules. Configuration of multiple port mappings is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple port mappings are commonly used in scenarios where an application defines multiple ports to distinguish different functionalities. For example, one port is used for business access, while another port is used for debugging.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding multiple port mappings, service ports must not be duplicated.</div><br><br><br>* **Service port**: Specifies the front\-end port of the public\-facing load balancer. This port is used to access the application and can be set to any value from 1 to 65535.<br><br>* **Protocol**: Select a communication protocol. Supports **TCP** and **UDP** protocols.<br><br>* **Host port**: The port that a process listens on, usually defined by the program. For example, a web application uses port 8080 by default. |
   

2. Click **OK**. The system will start to create a public load balancer access address.


<span id=".5re75Yqg6LSf6L295Z2H6KGh77yI5YaF572R77yJ"></span>
### Add load balancing (internal network)

Add an internal load balancer to the application to enable other applications within the same VPC to access it.


1. Click **Add Load Balancer (Internal)** , and configure the relevant information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |CLB load balancer |Select the target CLB instance. |
   |Scheduling algorithms |Rules for specifying how a listener forwards requests.<br><br><br>* **Weighted Round Robin**: traffic is forwarded based on weight values. The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>* **Weighted Least Connection**: traffic is forwarded first to the backend with the smallest real\-time ratio of connections to weight.<br><br>* **Source Hashing**: traffic is always forwarded to a single backend server if the hash of the source IP remains unchanged. |
   |Port mapping |Configure port mapping rules. Supports configuration of multiple port mappings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple port mappings are commonly used in scenarios where an application defines several ports to distinguish different functionalities. For example: one port is used for service access, while another is used for debugging.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you add multiple port mappings, service ports must not be duplicated.</div><br><br><br>* **Service port**: Defines the frontend port for public network load balancing. Access to the application is provided through this port, and it can be set within the range of 1 to 65535.<br><br>* **Protocol**: Select a communication protocol. **TCP** and **UDP** protocols are supported.<br><br>* **Host port**: The port that a process listens on, usually defined by the program. For example, the Web application uses port 8080 by default. |
   

2. Click **OK**, and the system will begin to create the internal load balancing access address.
