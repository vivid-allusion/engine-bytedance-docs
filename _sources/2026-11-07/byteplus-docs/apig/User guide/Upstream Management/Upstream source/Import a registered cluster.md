---
title: "Import a registered cluster"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Import_a_registered_cluster"
---

The API gateway supports the registered cluster feature based on Vital Kubernetes Engine, allowing you to import multi\-cloud clusters into an API gateway instance and use them as upstream sources. This enables the gateway to obtain the list of Services within each cluster. Implement multi\-cloud and multi\-cluster management features. This article introduces how to import registered clusters.

<span id="8ciP19WW"></span>
## Background information

Vital Kubernetes Engine supports the registered cluster feature, allowing you to connect to and manage standard Kubernetes clusters across different regions and infrastructures. The management scope includes local clusters, third\-party public cloud clusters, IDC self\-built clusters, edge clusters, and other Kubernetes clusters that comply with CNCF (Cloud Native Computing Foundation) standards, such as Alibaba Cloud ACK, Tencent Cloud TKE, Huawei Cloud CCE, Google Cloud GKE, Amazon EKS, Baidu Cloud CCE, and Custom Cluster.

Registered clusters allow users to flexibly integrate and manage Kubernetes clusters across any region or infrastructure, providing centralized management and operation and maintenance controls. This eliminates the need for business teams to directly interface with multiple clouds, streamlining management. For more details about registered clusters, refer to [the Registered cluster overview](https://docs.byteplus.com/en/docs/vke/Registered_cluster_overview).

The API gateway enables multi\-cluster management by connecting to the cluster registration feature. Provides a managed cloud\-native gateway feature for multi\-cloud and multi\-cluster environments, delivering highly available and scalable Ingress traffic management. Service resources in the cluster can be added as Upstreams for the API gateway, with support for configuring routing weights. Meets the requirements for business release, canary release, and similar scenarios in multi\-cloud disaster recovery.

Importing registered clusters into the API gateway mainly involves the following scenarios:


* Connect to multiple managed clusters in different VPCs within the same region of BytePlus.

* Connect to multiple managed clusters of BytePlus in different regions.

* Connect to clusters from multiple cloud providers.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The API gateway can connect to multiple managed clusters within the same region and VPC on BytePlus by using the import managed cluster feature. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Import_container_cluster">Import a container cluster</a>.</div>


<span id="lXYEuGkn"></span>
## Prerequisites


* The API Gateway instance has been created. For detailed instructions, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* Network connectivity and cluster import have been completed in the Vital Kubernetes Engine console. For more information, refer to [Register an existing cluster via the proxy method](https://docs.byteplus.com/en/docs/vke/Register_the_cluster_by_proxy).

   * If the cluster to be imported is a VKE cluster from another region of BytePlus, network connectivity is supported via [Cloud Enterprise Network](https://docs.byteplus.com/en/docs/cen/Product-Overview-01).

   * If the cluster to be imported is not a VKE cluster (such as clusters from other cloud providers or self\-managed clusters), you can establish network connectivity via Direct Connect.

* Workloads and Services have been deployed in clusters pending connection.


<span id="0KKxQX1E"></span>
## Limit


* Gateway instances must reside in the same VPC as the imported cluster.

* The supported version range for imported Kubernetes clusters is: **v1.24.x ~ v1.31.x**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more restrictions on cluster import, refer to <a href="https://docs.byteplus.com/en/docs/vke/Register_the_cluster_by_proxy">Registering existing clusters through proxy</a>.</div>


<span id="f4CpkLh7"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance in **Instance Management**, click **Import container cluster**.

4. On the cluster list page, click **Import cluster**.

5. On the import cluster page, select Import Registered Cluster.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Instance |Select the instance for which to import cluster information. |
   |Notes/comments |Enter remarks for the current cluster. This field can be left blank. |
   |K8s cluster |Select the specific import cluster to connect to.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can only select clusters that are in the same VPC as the gateway instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only clusters in the running state can be selected.</div><br> |
   |Route synchronization |Configure whether to enable the route synchronization feature.<br><br>After route synchronization is enabled, the API Gateway automatically listens for changes in Ingress resources, applies the relevant configurations, and maps the Ingress resources to Services, custom domains, routes, Upstreams, and other resources, which are then merged into the current gateway. For a detailed introduction, refer to [Ingress route synchronization](https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization). |
   

6. Click **OK** to complete the cluster import.


<span id="0PQQLwai"></span>
## Result validation

After the cluster is imported, check the status of the imported cluster in the **Cluster list**. When the status shows **Import successful**, the cluster has been imported successfully.

<span id="0PQQLwai"></span>
## What to do next


* [Cluster routing synchronizations](https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization)

* [Create an upstream of the Vital Kubernetes Engine type](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream)
