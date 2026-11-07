---
title: "Guidance for using KubeRay to manage RayClusters across different namespaces"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Guidance_for_using_KubeRay_to_manage_RayClusters_across_different_namespaces"
---

This document describes how to configure KubeRay to manage RayClusters in VKE.

For EMR On VKE version 3.17.0 and later, when deploying Ray services, the KubeRay Operator by default supports managing RayCluster resources in all namespaces within the VKE cluster.

For EMR On VKE versions earlier than 3.17.0, the KubeRay Operator by default can only manage RayCluster resources in its own namespace. To enable the KubeRay Operator to manage RayCluster resources across different namespaces, refer to the following instructions.

This document describes how to configure KubeRay to manage RayClusters in VKE.

<span id="cf46302f"></span>
## Important notes


* Ensure that when there are multiple KubeRay Operators in the same VKE cluster, the namespaces monitored by each KubeRay Operator do not overlap.

* If multiple KubeRay Operators in the same VKE cluster monitor the same namespace, when performing RayCluster resource operations in that namespace, the event will be executed by multiple KubeRay Operators simultaneously, which may cause conflicts. Conflicts can be avoided by configuring monitoring parameters:

   * For clusters of EMR version 3.17.0 and above, in **Service Management\> Service Parameters**, modify the kuberay\-operator\-values.yaml file and set the `watch_namespace` parameter to specify multiple namespaces to monitor, separated by commas.

   * For clusters of EMR versions earlier than 3.17.0, follow these steps: In the VKE console, edit the YAML file of the KubeRayOperator resource, and in args, add multiple namespaces to monitor (separated by commas) to the `--watch-namespace` parameter; when creating RayCluster, use a public repository image.


<span id="f2af3c78"></span>
## **Prerequisites**

An EMR On VKE cluster of a version earlier than 3.17.0 has been created, and Ray services have been deployed.

<span id="dde8525a"></span>
## Procedure


1. Log in to the [VKE console](https://console.volcengine.com/vke/).

2. Under **Cluster \> Cluster Name \> Workloads \> Stateless Workloads**, select the corresponding namespace and locate the KubeRay Operator resource.

3. Click **Actions \> Edit YAML**.

4. Locate the `args` field. If it contains the `--watch-namespace` key\-value pair, delete it (see the figure below).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a8aa049acd847bebb7f2251c1f6653d~tplv-goo7wpa0wc-image.image) </span>

5. Click **Confirm** to apply the changes.
