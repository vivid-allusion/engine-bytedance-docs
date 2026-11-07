---
title: "Manage container clusters"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Manage_Container_Cluster"
---

You can view, edit, and disassociate imported VKE cluster information. This article introduces operations related to managing VKE cluster information.

<span id=".5p-l55yLIFZLRSDpm4bnvqTkv6Hmga8="></span>
## View VKE cluster information

You can navigate to the corresponding VKE cluster page to view detailed information about the cluster.


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. After selecting the target instance in **Instance Management**, click **Import Kubernetes cluster**.

3. In the cluster list, click the target cluster name to navigate to the corresponding VKE cluster page.

   You can view detailed information about the VKE cluster.


<span id=".57yW6L6RIFZLRSDpm4bnvqTlpIfms6jlj4rot6_nlLHlkIzmraXphY3nva4="></span>
## Edit VKE cluster remarks and the route synchronization configuration

Supports modifying the remarks of imported VKE clusters and the configuration of the route synchronization feature.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you turn off route synchronization, the API Gateway will stop listening to Ingress resources and delete the custom domain names, routes, and upstream resources that were synchronized from Ingress. Caution: Please proceed with caution!</div>



1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. After selecting the target instance in **Instance management**, click **Import container cluster**.

3. In the cluster list, select the target cluster, and click **Edit** in the **Actions** column.

4. Modify the relevant information as needed. Once the modification is complete, click **Confirm**.


<span id=".6Kej57uR5bey5a-85YWlIFZLRSDpm4bnvqQ="></span>
## Disassociate imported VKE clusters

Delete the VKE cluster information of the APIG instance that has already been imported from the gateway.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">The disassociate action will delete the VKE cluster information from the gateway, and the gateway will no longer be able to obtain service information from the cluster.</div>


* <div data-tips="true" data-tips-type="danger">After disassociating, the API Gateway will stop listening to Ingress resources and will delete custom domain names, routes, and Upstream resources synchronized from Ingress. Please proceed with caution!</div>


* <div data-tips="true" data-tips-type="danger">After disassociation, your Upstream may become abnormal. Please proceed with caution!</div>


1. Log in to APIG console.

2. After selecting the target instance in **Instance management**, click **Associated kubernetes**.

3. In the cluster list, select the target cluster, and click **Unbind** in the **Actions** column.

4. In the pop\-up secondary confirmation dialog, click **Unbind**.
