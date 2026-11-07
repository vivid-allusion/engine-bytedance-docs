---
title: "Import container clusters"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Import_container_cluster"
---

To create an Upstream of the container service type, you must import the Vital Kubernetes Engine (VKE) cluster in advance and use it as the Upstream Source for the gateway, so that the gateway can obtain the list of Services in the cluster. This article describes how to import a cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The API Gateway instance has been created. For detailed instructions, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The pending connection cluster has been created, and the deployment of workload and service has been completed. For details, refer to [Use Vital Kubernetes Engine through the console](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console).

* The cluster to be connected has generated a KubeConfig for private access, and the KubeConfig is within its valid period. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* The APIG instance must be in the same VPC as the cluster.

* An APIG instance supports importing up to 3 clusters.

* When an API Gateway adds multiple Flannel clusters as upstream sources, the Pod CIDRs of the Flannel clusters must belong to the same subnet and must be consistent with the Pod CIDR subnet configured when creating the gateway instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance in **Instance Management**, click **Import container cluster**.

4. On the cluster list page, click **Import cluster**.

5. On the Import cluster page, enter the configuration information as required.

   
   |Parameter |Description |
   |---|---|
   |K8S cluster |Select the specific cluster to connect to.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only clusters that are in the same VPC as the APIG instance can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only clusters with Running status can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For Flannel clusters, the Pod CIDR of the selected cluster must be consistent with the Pod CIDR block chosen when creating the gateway instance.</div><br> |
   |Route synchronization |Configure whether to enable the route synchronization feature.<br><br>After enabling route synchronization, the API Gateway will automatically listen for changes in Ingress resources and apply the relevant configuration. It will convert the Ingress resources into services, custom domain names, routes, upstreams, and other resources, and merge them into the current gateway. For a detailed introduction, refer to [Ingress route synchronization](https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization). |
   

6. Click **Confirm** to complete the cluster import.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Cluster route synchronization](https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization)

* [Create Upstream service type for Vital Kubernetes Engine](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream)
