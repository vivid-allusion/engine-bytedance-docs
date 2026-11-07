---
title: "NodePort"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/NodePort"
---

NodePort exposes a service by opening a static port on the IP of every node in the cluster. This topic describes how to configure a NodePort service.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When you create a NodePort service in a cluster, the system opens a static port on the IP of every node. Other applications can then access the service by sending requests to `Node_IP:Node_Port`.

The IP address of a node can be either private or public. Therefore, NodePort services can be made available internally or externally.

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
      |Annotation |It refers to annotations in Kubernetes. Click **Add annotation** to add one to the service by creating a key\-value pair. |
      

   * **Access configuration**

      
      |Parameter |Description |
      |---|---|
      |Access type |Select an access type for the service. In this case, select **NodePort**. |
      |Communication Protocol |[[Beta - Apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)]  IPv4 and IPv6 protocols can be configured with different options to cover specific scenarios. The options include:<br><br><br>* **IPv4**: IPv4 addresses only.<br><br>* **IPv6**: IPv6 addresses only.<br><br>* **IPv4&IPv6**: Both protocols are allowed, but the IPv4 addresses will be used by default.<br><br>* **IPv6&IPv4**: Both protocols are allowed, but the IPv6 addresses will be used by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details about how to create IPv4/IPv6 clusters, see <a href="https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE">Creating IPv4/IPv6 clusters with VKE</a>.</div><br> |
      |Port mapping |Configure a port mapping rule:<br><br><br>* **Name**: enter a name for the port mapping between the service and container.<br><br>* **Service level port**: Enter a port through which the service will be accessed. Duplicate ports are not allowed for services using the same protocol.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In clusters using the VPC\-CNI network model, duplicate ports are not allowed for services even across different protocols. That is, no services can share the same port number regardless of whether they use TCP or UDP.</div><br><br><br><br>* **Protocol**: select a protocol for the service. Currently, available protocols include **TCP** and **UDP**.<br><br>* **Node port**: the port exposed on the node, which can be an integer from 30000 to 32767. A port will be allocated automatically by the system if you leave it empty.<br><br>* **Container port**: the port of the container, which is a port number through which the deployment provides services externally. e.g., the default port number for Nginx is 80. |
      |Label selector |Services are bound to back\-end pods through label selectors.<br><br><br>* **Add new**: Specify the label of the Deployment to which the service will be bound.<br><br>* **Associated workload**: Select the Deployment to bind the service to. Currently, Deployment, StatefulSet, and DaemonSet are supported.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not bind NodePort services to workloads deployed on Vital Container Instances.</div><br> |
      |External traffic policy |The policies that the service will use to forward inbound traffic: <br><br><br>* **Cluster**: traffic is forwarded evenly to each pod of the workload.<br><br>* **Local**: traffic can only be forwarded to the local pods on the current node, which may cause unbalanced traffic distribution. However, the source IPs can be retained. |
      |Session persistence |Whether to enable session persistence.<br><br><br>* Disabled by default.<br><br>* Check **Configure timeout** to enable session persistence and set its duration. The service ensures requests from the same IP are forwarded to a single backend server. We recommend setting a timeout longer than 120 seconds. |
      

5. Click **Confirm** to finish the configuration.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5Yib5bu6"></span>
### Creating via kubectl command line

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Make sure the following requirements are met before getting started:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool is installed on your computer. For details, please see <a href="https://kubernetes.io/docs/tasks/tools/">Installation and settings of kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">Successfully connected to the target cluster with kubectl. For details, please see<a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connect to a cluster</a>.</div>


1. A YAML file for creating the service. The following code is the content of a sample YAML file named `service-demo.yaml`:

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: service-demo # Service name.
   spec:
     selector:
       app: nginx # Bind the service to backend pods via a label selector.
     ports:
     - name: rule #The name of the port mapping rule.
       protocol: TCP # service protocol, which can either be TCP or UDP.
       port: 80 # Service port.
       nodePort: 30000 # NodePort, which can be an integer from 30000 to 32767.
       targetPort: 80 # Container port, a port number or port name through which the Deployment provides service, e.g., the default port number for Nginx is 80.
     type: NodePort # Service type.
   ```
   

2. Execute the following command to create a service.

   ```bash
   kubectl apply -f service-demo.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result checking

<span id=".5p-l55yL5pyN5Yqh"></span>
### Viewing services

The service you created can be found in the service list.

If you did not specify a NodePort when creating a service, the system will allocate one for the service. You can click the service name to go to the Overview tab, and scroll to the **Port mapping** section to view the port number in the Container port column. 

<span id=".6K6_6Zeu5pyN5Yqh"></span>
### Access services

Any successfully created service can be accessed through `any node IP and node port` within the same VPC or by any container in the cluster. It can also be accessed through a public IP if the node has one.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0499ce4c79933b2487654a350952456.png) </span>
