---
title: "ClusterIP"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ClusterIP"
---

ClusterIP allows workloads to be exposed to other workloads within the same cluster through services. This topic describes how to configure a ClusterIP service.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When creating a ClusterIP service in a cluster, the system generates an internal domain name for the service in the format of `service-name.namespace.svc.cluster.local:port`. For example, after you create a service named nginx with port 80 in the default namespace, you can access the service and its backend pods within the cluster by using `nginx:80` or `nginx.default:80`.

If you want to directly connect to pods instead of communicating through the load balancer and service IP, you can create a headless service. A headless service does not have a ClusterIP. When DNS queries are performed inside the cluster, DNS records for all pods are returned, so you can directly access the IP addresses of all pods.

The following table shows the main differences between ClusterIP and headless services.


|**Item** |**ClusterIP** |**Headless Service** |
|---|---|---|
|ClusterIP |Yes |None |
|DNS resolution for services |The ClusterIPs of Services will be returned as results. |IPs of all pods will be returned as results. |
|Accessed by other applications |Services are the farthest destinations that other applications can see. The iptables acts as a load balancer to determine which pod the traffic is further forwarded to. |Pods can be directly accessed through IPs. |
|Application scenarios |Where services are required to provide load balancing for pods. |* Where direct connections to pods are required. For example, Kafka pods deployed in a cluster need to be accessed directly by clients.<br><br>* Scenarios where clients handle load balancing. For example, when two applications are deployed in a cluster and the clients handle load\-balancing requests themselves, no proxy service is needed. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Deployments have been created. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment), [Creating StatefulSets](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet), and [Creating DaemonSets](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only Deployment, StatefulSet, and DaemonSet are supported.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YCa6L-H5o6n5Yi25Y-w5Yib5bu6"></span>
### Creating via console


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. Click **Cluster** in the left navigation bar.

3. On the cluster list page, click the name of the cluster in which you want to create services.

4. On the cluster management page, select **Services and Ingresses** \> **Service** in the left navigation bar, then click **Create Service**.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Name |Enter a name for the service. Make sure the name is unique under the same namespace. |
      |Namespace |Select the namespace to which the service belongs. It is recommended that you select the namespace created by yourself or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Label |Click **Add new** to add labels to the service. Labels are used to define various attributes of services, facilitating batch filtering and other operations. |
      |Annotation |It is an annotation in Kubernetes. Click **Add annotation** to add one for the service by creating a key\-value pair. |
      

   * **Access configuration**

      
      |Parameter |Description |
      |---|---|
      |Access type |Select an access type for the service. In this case, select **ClusterIP**. |
      |Communication protocol |[[beta·apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)]  IPv4 and IPv6 protocols can be configured with different options to cover specific scenarios. The options include:<br><br><br>* **IPv4**: IPv4 addresses only.<br><br>* **IPv6**: IPv6 addresses only.<br><br>* **IPv4&IPv6**: Both protocols are allowed, but the IPv4 addresses will be used by default.<br><br>* **IPv6&IPv4**: Both protocols are allowed, but the IPv6 addresses will be used by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details about how to create IPv4/IPv6 clusters, see <a href="https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE">Create IPv4/IPv6 clusters with VKE</a>.</div><br> |
      |Port mapping |Create a port mapping:<br><br><br>* **Name**: Enter a name for the port mapping between the service and container.<br><br>* **Service level port**: Enter a port used to access the service. Duplicate ports are not allowed for services using the same protocol.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In clusters using the VPC\-CNI network model, duplicate ports are not allowed for services even across different protocols. That is, no services can share the same port number regardless of whether they use TCP or UDP.</div><br><br><br><br>* **Protocol**: Select a protocol for the service. Available protocols include **TCP** and **UDP**.<br><br>* **Container port**: Specify the port of the container, which is a port number through which the deployment provides services externally. e.g., the default port number for Nginx is 80. |
      |Label selector |Services are bound to back\-end pods through label selectors.<br><br><br>* **Add new**: add the label of the Deployment to which the service will be bound. You can find deployment labels by clicking **Workload** in the left navigation bar of the cluster management page.<br><br>* **Associated workload**: Select the deployment to which the service will be bound. Currently, only Deployment, StatefulSet, and DaemonSet are supported. |
      |Session persistence |Whether to enable session persistence.<br><br><br>* Disabled by default.<br><br>* Check **Configure timeout** to enable session persistence and set its duration. The service will forward all requests from the same IP to a single backend server. We recommend setting a timeout longer than 120 seconds.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Headless services do not support session persistence and the timeout setting will not take effect.</div><br> |
      

5. Click **Confirm** to finish the configuration.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5Yib5bu6"></span>
### Creating via kubectl command line

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Make sure the following requirements are met before getting started:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool is installed on your computer. For details, please see <a href="https://kubernetes.io/docs/tasks/tools/">Installation and settings of kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">Successfully connected to the target cluster with kubectl. For details, please see<a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connect to a cluster</a>.</div>


1. Create a YAML file for the service.The following code is the content of a sample YAML file named `service-demo.yaml`:

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: service-demo # Service name.
   spec:
     selector:
       app: nginx # Bind the service to backend pods via a label selector.
     ipFamilyPolicy: PreferDualStack  # Preferred protocol stack SingleStack means only one protocol stack is applied, PreferDualStack means two protocol stacks can be applied simultaneously.
     ipFamilies: # The communication protocols actually used. Single-stack can have IPv4 and IPv6 as the options; dual-stack can have IPv4&IPv6 and IPv6&IPv4 as the options.
     - IPv6
     - IPv4
     ports:
     - name: rule #The name of the port mapping rule.
       protocol: TCP # service protocol, which can either be TCP or UDP.
       port: 8080 # Service port.
       targetPort: 80 # Container port, a port number or port name through which the deployment provides service, e.g., the default port number for Nginx is 80.
     type: ClusterIP # Service type.
   ```
   

2. Execute the following command to create a service.

   ```bash
   kubectl apply -f service-demo.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result checking

<span id=".5p-l55yL5pyN5Yqh"></span>
### Viewing the services

The service you created successfully can be found in the service list, which displays cluster IPs (i.e. ClusterIP) and internal endpoints (i.e., internal domain names)

<span id=".6K6_6Zeu5pyN5Yqh"></span>
### Testing the connections to services

You can access the service in several ways as described below:


* Accessing the service using `ClusterIP:Port`.

* Accessing the service using `service-demo:80` within the same namespace.

* Accessing the service in another namespace using `service-demo.default:80`
