---
title: "Inter-application access within the cluster"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Intra-cluster-access-between-applications"
---

This document primarily describes how applications within the same cluster in VKE can communicate with each other to meet communication requirements.

<span id=".5qaC6L-w"></span>
## Overview

<span id=".6ZuG576k5YaFLXBvZC3nmoTorr_pl67pl67popg="></span>
### Access issues for Pods in the cluster

Once a workload is created, it runs across multiple Pods. Because Pods have autoscaling capabilities, accessing them presents the following challenges:


* Pods can be deleted and recreated at any time by controllers such as Deployment, so the result of accessing a Pod is unpredictable.

* The IP address of a Pod is allocated only after the Pod starts, so the IP address is not known before startup and therefore cannot be used to access the Pod.

* The IP addresses allocated to Pods are internal cluster IP addresses, which are typically private IP addresses and cannot be accessed directly. In addition, there can be multiple replica Pods under the same workload, and each Pod has a different IP address. Therefore, directly accessing the application through the Pod's IP address can result in single\-point performance and failure issues.


<span id=".6YCa6L-HLXNlcnZpY2Ut6Kej5YazLXBvZC3nmoTorr_pl67pl67popg="></span>
### Resolve Pod access issues using Service

In Kubernetes, the Service object is used to resolve the above Pod access issue.


* When a Service is created, the system assigns a fixed IP address (ClusterIP) to the Service. Users can access the Service by connecting to this ClusterIP.

* A Service selects Pods using Labels and forwards user traffic to the Pods. Additionally, a Service can also provide load balancing for Pods.


<span id=".c2VydmljZS3nmoTorr_pl67mlrnlvI8="></span>
### Service access methods

<span id=".6ZuG576k5YaF6K6_6Zeu77yIY2x1c3Rlcmlw77yJ"></span>
#### ClusterIP

ClusterIP refers to exposing a workload so that it can be accessed by other workloads within the same cluster. Access is available through the cluster's internal domain name.

For example, when you create a Service named nginx with port 8080, you can access the Service from within the cluster directly using **nginx:8080**, which in turn allows access to the backend Pod.

<span id=".6IqC54K556uv5Y-j6K6_6Zeu77yIbm9kZXBvcnTvvIk="></span>
#### Accessible through NodePort

Node access refers to opening a static port on each node's IP address to expose the Service externally through that static port. Other applications within the cluster can access the Service by sending a request to **NodeIP:NodePort**.

<span id=".6LSf6L295Z2H6KGh77yIbG9hZGJhbGFuY2Vy77yJ"></span>
#### LoadBalancer

A Service of the LoadBalancer type is essentially an extension of the NodePort type. When you access the Service through the LoadBalancer, the Service forwards the request to the node's NodePort. Load balancing has been implemented, providing higher reliability assurance.

<span id="headless-service"></span>
#### Headless Service

In microservices scenarios, when neither load balancing nor a Service IP is required and direct access to a Pod is needed. You can create a Headless Service by setting the value of Cluster IP (`spec.clusterIP`) to `"None"`.

A Headless Service does not create a ClusterIP for the Service. When a DNS query is made, it returns the DNS records for all Pods, allowing access to the IP addresses of all Pods. making it possible to connect to pods directly.

The following table shows the main differences between ClusterIP and headless services.


|**Change item** |**ClusterIP** |**Headless Service** |
|---|---|---|
|ClusterIP |Yes. |none. |
|DNS resolution for services |The ClusterIPs of Services will be returned as results. |IPs of all pods will be returned as results. |
|Accessed by other applications |Services are the farest destinations that other applications can see. The iptables will be working as a load balancer to determine which pod the traffic is further forwarded to. |Pods can be directly accessed through IPs. |
|Application scenarios |Where services are required to provide load balancing for pods. |* Where direct connections to pods are required. For example, Kafka pods deployed in a cluster need to be accessed directly by clients.<br><br>* Where the clients provide load balancing. For example, when deploying two MySQL instances in a cluster, the client is responsible for handling load balancing requests, so there is no need to use Service as a proxy in this scenario. |


<span id=".6K6_6Zeu5pa55byP5a-55q-U"></span>
### Comparison of access methods


|**Access methods** |**Public content** |**Descriptions** |
|---|---|---|
|ClusterIP |`spec.clusterIp:spec.ports[*].port` |This Service can only be accessed from within the cluster. Can be accessed through its `spec.clusterIp` port. If `spec.ports[*].targetPort` is set, traffic will be routed from the port to targetPort. The ClusterIP obtained during invocation: `kubectl get services` is the IP allocated to the Service within the cluster. |
|NodePort |* `NodeIP:spec.ports[*].nodePort`<br><br>* `spec.clusterIp:spec.ports[*].port` |If this Service is accessed via the NodePort using the external IP of a node, the request will be routed to `spec.clusterIp:spec.ports[*].port`, and then to `spec.ports[*].targetPort` if it is set. You can also access this Service in the same way as ClusterIP. NodeIP is the external IP address of the node. Cannot access the Service from `<ClusterIP>:spec.ports[*].nodePort`. |
|LoadBalancer |* `spec.loadBalancerIp:spec.ports[*].port`<br><br>* `<NodeIP>:spec.ports[*].nodePort`<br><br>* `spec.clusterIp:spec.ports[*].port` |You can access this Service through the IP address of the LoadBalancer. The Service routes requests to the NodePort, which then routes them to the ClusterIP port. Users can access this Service in the same way as they access a NodePort or ClusterIP Service. |


<span id=".5L2_55So5o-Q56S6"></span>
### Note


* Unless absolutely necessary, do not specify hostPort for a Pod. When binding a Pod to a hostPort, each `<hostIP, hostPort, protocol>` combination must be unique, so hostPort restricts the number of locations where the Pod can be scheduled. If neither hostIP nor Protocol is explicitly specified, Kubernetes uses `0.0.0.0` as the default hostIP and TCP as the default Protocol.

* If you only need to access a port for debugging, you can use apiserver proxy or kubectl port\-forward.

* If you explicitly need to expose Pod ports on the node, please consider using a NodePort Service before using hostPort.

* Avoid using hostNetwork; the reason is the same as for hostPort.

* When kube\-proxy load balancing is not required, use headless services (with ClusterIP set to None) to facilitate service discovery.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you need to access workloads across VPCs, you must connect different VPC networks using methods such as peering connections.

<span id=".6YWN572u6ZuG576k5YaF6K6_6Zeu77yIY2x1c3Rlcmlw77yJ"></span>
## Configure ClusterIP access

<span id=".6YWN572u5YmN5qOA5p-l"></span>
### Pre\-configuration checks


* After creating clusters and nodes, ensure that they are operating properly. For detailed operations, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Upload the application image to the Container Registry. For detailed operations, refer to [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".6YWN572u5q2l6aqk"></span>
### Configuration steps

Take stateless workload (Deployment) as an example. For detailed procedure and parameter descriptions, refer to [ClusterIP](https://docs.byteplus.com/en/docs/vke/ClusterIP).


1. Go to the VKE console, select **Cluster** \> **Workload** \> **Deployment**, and create a workload.

2. Select the newly created workload in the **Access method** tab. Select **Service**, and click **Create Service**.

3. Go to the Service configuration page and configure the basic information for the Service.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |Name |The name of the Service to configure. |
   |Namespance |Configure the namespace for the Service. By default, this example uses the same namespace as the Deployment. |
   |Label |Click **Add new** to add labels to the service. Labels are used to define various attributes of service, facilitating batch filtering and other operations. |
   |Annotation |It is the annotation in Kubernetes. Click **Add annotation** to add an annotation for the service by creating a key\-value pair. |
   

4. Configure the access type. In this example, select **ClusterIP**.

5. Configure **Port mapping**. Configure the Service ports, container ports, and protocol separately.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |Name |Specify the name for the mapping from Service port to container port. |
   |Service ports |Configure the ports through which the Service provides services to external clients. Duplicate ports are not allowed for services running on the same protocol. |
   |Protocol |Select the protocol for the port based on the service protocol type. Currently, available protocols include TCP and UDP. |
   |Container ports |Configure the container port through which the workload provides Service externally. For example, Nginx uses port 80 by default. |
   

6. Configure the label selector. Service uses labels to forward traffic.

7. (Optional) Configure session persistence, set the timeout period, and after a timeout, handle according to the parameters.

8. Click **Confirm** to complete the configuration.


<span id=".5qOA5p-l57uT5p6c"></span>
### Inspection results

Log in to other nodes in the cluster, use `the cluster IP and service port` to access the exposed workload, and confirm that the access is successful (using nginx as an example).

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_fd79830f364963f09006fa2727b88637.png) </span>

<span id=".6YWN572u6IqC54K556uv5Y-j6K6_6Zeu77yIbm9kZXBvcnTvvIk="></span>
## Configure NodePort access

<span id=".6YWN572u5YmN5qOA5p-l"></span>
### Pre\-configuration check


* After creating clusters and nodes, ensure clusters and nodes operate normally. For detailed operations, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Upload the application image to the Container Registry. For detailed instructions, refer to [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".6YWN572u5q2l6aqk"></span>
### Configuration steps

For example, consider a stateless workload (Deployment). For detailed procedures and parameter descriptions, refer to [NodePort](https://docs.byteplus.com/en/docs/vke/NodePort).


1. Go to the VKE console, select **cluster** \> **workload** \> **Deployment**, and create a workload.

2. Select the newly created workload on the **Access Method** tab. Select **Service**, click **Create Service**.

3. Go to the Service configuration page and configure the basic information for the Service.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |Name |Configure the name of the service. |
   |Namespance |Configure the namespace for the Service. By default, this example uses the same namespace as the Deployment. |
   |Label |Click **Add new** to add labels to the service. Labels are used to define various attributes of service, facilitating batch filtering and other operations. |
   |Annotation |It is the annotation in Kubernetes. Click **Add annotation** to add an annotation for the service by creating a key\-value pair. |
   

4. Configure the access type. In this example, select **NodePort**.

5. Configure port mapping. Configure the node port, Service port, container port, and protocol separately.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |Name |Configure the name for the mapping from the Service port to the container port. |
   |Service port |Configure the ports through which the Service provides services externally. Duplicate ports are not allowed for services running on the same protocol. |
   |Protocol |Select the port protocol based on the type of business protocol. Currently, available protocols include TCP and UDP. |
   |Node port |That is, NodePort. You can specify a particular port, or leave it blank. When a specific value is not provided, the system automatically allocates a port. |
   |Container port |Configure the container port through which the workload provides services externally. For example, nginx uses port 80 by default. |
   

6. Configure a label selector Associate workloads through labels.

7. Optional: Configure session persistence and the timeout period. After the timeout period, process as specified by the configured parameters.

8. Click **Confirm** to complete the configuration.


<span id=".5qOA5p-l57uT5p6c"></span>
### Inspection results

Log in to other nodes in the cluster, use `node IP + node port` to access the exposed workload, and confirm that access is successful (using nginx as an example).

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3b3a19086cd451a94c8a058d0c17f2be.png) </span>

<span id=".6YWN572u6LSf6L295Z2H6KGh77yIbG9hZGJhbGFuY2Vy77yJ"></span>
## Configure LoadBalancer

<span id=".6YWN572u5YmN5qOA5p-l"></span>
### Pre\-configuration check


* After creating clusters and nodes, ensure that they are operating normally. For detailed operations, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Upload the application image to the Container Registry. For detailed instructions, refer to [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".6YWN572u5q2l6aqk"></span>
### Configuration steps

Take stateless workload (Deployment) as an example. For detailed procedures and parameter descriptions, refer to [LoadBalancer](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console).


1. Open the VKE console, select **cluster** \> **workload** \> **Deployment**, and create a stateless workload.

2. Select the newly created workload in the **Access method** tab. Select **Service**, and click **Create Service**.

3. Go to the service configuration page and configure the basic information for the Service.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |Name |Configure the name of the Service. |
   |Namespance |Configure the namespace of a Service. By default, this example uses the same namespace as the Deployment. |
   |Label |Click **Add new** to add labels to the service. Labels are used to define various attributes of service, facilitating batch filtering and other operations. |
   |Annotation |It is the annotation in Kubernetes. Click **Add annotation** to add an annotation for the service by creating a key\-value pair. |
   

4. Configure the access type. In this example, select **LoadBalancer**.

5. (Optional) Configure LB\-to\-pod direct access mode. This mode refers to the direct connection between CLB and Pod, bypassing Kube\-proxy, and enabling the use of advanced CLB capabilities such as health checks. This parameter is supported only in VPC\-CNI networks.

6. Configure **a LoadBalancer**. Select **Private network access** and **Automatic creation** from the dropdown menu. Select subnet and instance specification based on actual requirements.

7. Configure listener scheduling algorithms, supporting **weighted round robin (WRR)** , **weighted least connections (WLC)** , and **source address hash (SH)** .

   
   |Algorithm |**Descriptions** |
   |---|---|
   |Weighted round robin (WRR) |Traffic is distributed based on weight values, and backend servers with higher weights are polled more frequently, resulting in a higher probability of being selected. |
   |Weighted least connection (WLC) |Prioritize distributing traffic to the backend with the smallest ratio of current connections to weight. |
   |Source address hash (SH) |Consistent hashing based on the source IP address ensures that requests from the same source address are routed to the same backend server. |
   

8. (Optional) Select as needed whether to enable health checks. This example does not configure a health check.

9. Configure port mapping.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |Name |The name of the port mapping configuration. |
   |Service port |Configure the ports through which the Service provides external access. Ports for the same protocol must not be duplicated. |
   |Protocol |Select the port protocol based on the business protocol type. Currently supports the TCP and UDP protocols |
   |Container port |Configure the container port. This port is used by the workload to provide service externally. For example, the port for Nginx is port 80. |
   

10. Configure the label selector. It is associated with workloads via labels.

11. Optional: Configure session persistence and the timeout period. After a timeout occurs, handle according to the configured parameters.

12. Click **Confirm** to complete the configuration.


<span id=".5qOA5p-l57uT5p6c"></span>
### Inspection results

Log in to other nodes in the cluster, and use `the LoadBalancer external endpoint IP and port number` to access the exposed workload.

After successful access, the following is displayed (nginx is used as an example in this case).

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_88006dcdb4c5f4be55dd7fe83b006a7f.png) </span>
