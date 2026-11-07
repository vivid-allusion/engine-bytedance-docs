---
title: "Create an Upstream container service type"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream"
---

API Gateway supports connecting to BytePlus Vital Kubernetes Engine (VKE), abstracting the Kubernetes Service under the VKE cluster as an Upstream, which serves as the backend for gateway routing. Applicable to scenarios where businesses adopt VKE deployment and wish to release their services through a gateway. This article explains how to create a VKE\-type Upstream.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The API Gateway instance has been created. For specific operations, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The cluster to be connected has been added as an Upstream source. For specific operations, refer to [Import VKE cluster](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

API Gateway instance and Vital Kubernetes Engine cluster must be in the same VPC.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance in **Instance Management**, click **Upstream List**.

4. On the Upstream list page, click **Create Upstream**.

5. On the Create Upstream page, fill in the parameter information as required.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Upstream name |Customize the Upstream Name. The Upstream Name must be unique within the same Instance. |
      

   * **Backend configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Choose the backend service type that Upstream connects to. In this scenario, **Vital Kubernetes Engine** is used. The API Gateway automatically aggregates all Namespaces, Services, and Ports with the same name across all clusters in the upstream source, and treats them as a single application.<br><br><br>* **Namespace**: Choose the namespace where the target Kubernetes Service is located.<br><br>* **Service name**: Choose the target Kubernetes Service name.<br><br>* **Port**: Choose the port exposed by the target Kubernetes Service. |
      |Protocol |Choose protocol type. Support **HTTP1.1**, **HTTP2**, and **HTTP2/GRPC**. |
      |TLS Settings |Configure TLS.<br><br><br>* **Disable TLS**: The gateway accesses the Backend Upstream using the HTTP Protocol.<br><br>* **Unidirectional TLS**: The gateway accesses the Backend Upstream using the HTTPS protocol, which requires selecting the corresponding certificate. |
      |Load balancing algorithm |Configure a load balancing algorithm.<br><br><br>* **Poll**: (Default) Assign all requests to pods associated with the Kubernetes Service in turn, suitable for scenes with the same pod instance type.<br><br>* **Random**: Requests are randomly allocated to pods.<br><br>* **Least connections**: Allocate requests to the Pod currently processing the fewest requests.<br><br>* **Consistent hashing**: Load balancing based on header/querystring information ensures that, when the number of backend services remains unchanged, users carrying the same information can consistently access the same Pod. Click **Enable overload protection**, set **load threshold**, and enable instance overload protection. Once enabled, if an instance's active request count exceeds the threshold based on the average active request count, the instance will not be selected even if it is matched by the hash value. |
      |Service circuit breaking |Configuration for whether to enable circuit breaking.<br><br>Once enabled, the API Gateway can improve the routing hit rate by setting a circuit breaker, without consuming additional traffic. For details, see [Circuit breaking policies](https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy). |
      |Warm up time |When the load balancing algorithm is configured as **Round robin** or **Minimum number of connections**, configuration is supported.<br><br>Configure the warm\-up time for backend services. The value must be in integer format and in the range from 1 up to but not including 10000. Unit: seconds. |
      

6. Click **Confirm**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Security group configuration


* When the API Gateway connects to a VPC\-CNI cluster, allow actions are enabled by default, so there is no need to perform allow actions.

* When the API Gateway connects to a Flannel cluster, you need to open the APIG security group (named `apig-sg-<accountID>`) for all nodes in the Flannel cluster to be connected, ensuring that the gateway can access resources in the cluster without issues. All nodes in Vital Kubernetes Engine are associated with the default security group named `<Cluster ID>-common`. You only need to add an inbound rule to the default security group to allow the APIG security group. The specific operations are as follows:

   1. Log in to the [Vital Kubernetes Engine console](https://console.byteplus.com/vke), select **Cluster** in the navigation bar on the left, click the target Flannel cluster on the cluster list page, and enter the current cluster management page.

   2. In the left navigation bar, select **Node**. On the node list page, click any node name to go to the details page for the selected node.

   3. In the Basic information region, locate the Vital Kubernetes Engine default security group named `<cluster ID>-common`, and click to open this security group.

   4. Switch to the **Access Rules** tab, and in the **Inbound Rules** region, click **Add rule**.

   5. In the **Add Inbound Rule** dialog box, configure APIG security group information as required. Parameters not mentioned in the table remain at the default configuration.

      
      |Parameter |Description |
      |---|---|
      |Protocol |Choose ALL, allow access to all communication protocols. |
      |Source address |Select **Security group**, then choose the APIG security group named `apig-sg-<accountID>`. |
      

   6. Click **Confirm**.
