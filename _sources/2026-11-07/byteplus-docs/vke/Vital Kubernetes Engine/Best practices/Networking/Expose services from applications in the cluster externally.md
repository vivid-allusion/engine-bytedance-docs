---
title: "Expose services from applications in the cluster externally"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Exposing-applications-in-clusters"
---

This document mainly describes how applications in a VKE cluster expose Services to external networks to enable public users to access the applications.

<span id=".5qaC6L-w"></span>
## Overview

Workloads in the cluster can provide services to public network users in two ways: through Service (LoadBalancer) and Ingress.


|**Service exposure methods** |**Descriptions** |
|---|---|
|Service（LoadBalancer） |Provides Layer 4 network services externally, based on the TCP and UDP protocols. |
|ingress |The system provides Layer 7 network services to external clients based on the HTTP and HTTPS protocols. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details, refer to <a href="https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_overview">LoadBalancer Service overview</a> and <a href="https://docs.byteplus.com/en/docs/vke/Ingress-overview">Ingress overview</a>.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

When exposing a Service (LoadBalancer) to external networks, you must configure a load balancer in **Public NAT for internet endpoint** mode. For details, refer to [Create a LoadBalancer Service through the console](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console).

<span id=".6YWN572uLXNlcnZpY2Ut5a-55aSW5pq06Zyy5pyN5Yqh"></span>
## Configure a Service for external access

<span id=".6YWN572u5YmN5qOA5p-l"></span>
### Pre\-configuration checks


* After creating clusters and nodes, ensure that clusters and nodes are functioning properly. For detailed operations, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Upload the application image to the Container Registry. For detailed instructions, refer to [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".6YWN572u5q2l6aqk"></span>
### Configuration steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article uses the creation of a stateless workload (Deployment) as an example.</div>



1. Log in to [the VKE console](https://console.byteplus.com/vke), and click **cluster** in the left navigation bar.

2. On the **cluster** page, find the target cluster and click the cluster name.

3. On the cluster management page, select **Workload** \> **Deployment** from the left navigation bar to create a Deployment. For detailed instructions, refer to [Create Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

4. After the Deployment is created successfully, click the name to enter the **Deployment details page**.

5. Select the **Access Method** \> **Service** tab, and click **Create Service**.

6. Configure service parameters. Some parameter configurations in this example are shown below. For the remaining parameter configurations, please refer to the content in [LoadBalancer](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console) and configure them according to your actual requirements.

   
   |**Configuration Item** |**Configuration description** |
   |---|---|
   |**Configurations for access** ||
   |Access type |Service access type. In this example, **LoadBalancer** is selected, which means that applications in the cluster can be accessed from the public network via an elastic load balancer (Public NAT for internet endpoint). |
   |LB\-to\-pod direct access mode |Only clusters using the VPC\-CNI network model support this parameter. This feature is disabled by default. When enabled, it directly associates Pods as the backend for the LoadBalancer, bypassing Kube\-proxy processing and allowing the use of advanced capabilities such as CLB health checks.<br><br>Configure as needed. The default values can be used for this example. |
   |Load balancer |Configure the LoadBalancer for the Service. In this example, select **Public NAT for internet endpoint** and **automatic creation**. |
   |label selector |The stateless workload created in step 3 above has already been associated here, so no configuration is required.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the stateless workload you created in Step 3 is deployed using VCI, only access via <strong>LB\-to\-pod direct access mode</strong> is supported. The system will automatically enable the <strong>LB\-to\-pod direct access mode</strong> switch, which cannot be disabled.</div><br> |
   

7. Click **Confirm** to complete the configuration.


<span id=".5qOA5p-l57uT5p6c"></span>
### Inspection results

Log in to the browser on a PC with public NAT for internet endpoint permission, and access the exposed workload using `public IP address and service port number`. In this example, nginx is used; the content shown in the following image is returned, indicating that access was successful.

<span id=".6YWN572uLWluZ3Jlc3Mt5a-55aSW5pq06Zyy5pyN5Yqh"></span>
## Configure Ingress to expose Service externally

<span id=".6YWN572u5YmN5qOA5p-l"></span>
### Pre\-configuration check


* Once clusters and nodes have been created, ensure that they are functioning properly. For detailed operations, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Upload the application image to the Container Registry. For detailed operations, refer to [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".6YWN572u5q2l6aqk"></span>
### Configuration steps


1. Log in to the [VKE console](https://console.byteplus.com/vke), and in the left navigation pane, click **Cluster**.

2. On the **cluster** page, locate the target cluster and click the cluster name.

3. In the left navigation bar of the cluster management page, select **Workload** \> **Deployment**, then create a Deployment. For detailed operations, refer to [Create a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

4. After the Deployment is created successfully, click the name to enter the **Deployment details page**.

5. Select the **Access method** \> **Ingress** tab, and click **Create Ingress**.

6. Configure Ingress parameter. Some parameter configurations in this example are shown below. For the remaining parameter configurations, refer to the content in [Configure Nginx Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-Nginx-Ingress-in-the-console) and configure them as needed.

7. Configure the Ingress parameters according to actual requirements. For detailed operation, refer to [Ingress](https://docs.byteplus.com/en/docs/vke/Ingresses).

8. Click **Add** to complete the configuration.


<span id=".5qOA5p-l57uT5p6c"></span>
### Inspection results

On a PC with Public NAT for internet endpoint permission, use `domain name + path` to access the exposed workload (application). A response similar to the one shown below will be returned, indicating that access was successful and that different paths accessed different applications.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_faefb3b749ea90dae387a3df9462ed47.png) </span>
