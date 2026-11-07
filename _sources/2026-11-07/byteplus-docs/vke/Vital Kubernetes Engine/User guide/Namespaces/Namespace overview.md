---
title: "Namespace overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Namespace-overview"
---

In Kubernetes, namespaces provide a mechanism to divide resources within the same cluster into mutually isolated groups. You can create multiple namespaces with different names in a cluster, and data in different namespaces is isolated from each other.

In scenarios involving multiple teams or projects, namespaces are used to isolate and partition cluster resources.

<span id=".5ZG95ZCN56m66Ze05YiG57G7"></span>
## Namespace classification

A cluster consists of two types of namespaces: the system namespace and the user\-defined namespace.


* System namespace:

   The cluster automatically creates system namespaces by default when it starts.

   
   |**Namespace name** |**Description** |
   |---|---|
   |default |The default namespace of a cluster. Objects without specified namespaces are deployed in this namespace. |
   |kube\-public |The namespace  that can be read by all users, including unauthenticated users, and is used to deploy public add\-ons, container templates, and other public resources. |
   |kube\-system |The namespace used by objects created by the Kubernetes system. |
   |kube\-node\-lease |The Lease objects that are associated with each node. They are periodically updated by the nodes. During the lease period, the control plane can detect node heartbeats to determine whether a node has failed. |
   

* User\-defined namespace:

   You can create custom namespaces based on your business requirements, such as namespaces named after development, test, and production environments.


<span id=".5ZG95ZCN56m66Ze05YiS5YiG5a6e6Le1"></span>
## Namespace partitioning practices


* By team:

   Create namespaces for independent projects or teams to facilitate subsequent management of team permissions and resource quotas at the namespace level.

* By environment:

   The release of an application typically involves the development environment, testing environment, and production environment. An application in different environments is generally similar. You can isolate environments by using namespaces to ensure that the application in each environment is independently maintained without mutual interference.

* By application:

   If you have created multiple applications, you can group workloads based on their relationships, deploy them in different namespaces, and manage them in batches.


<span id="vJ0NT6RI"></span>
## Resource management

VKE allows you to specify ResourceQuotas and LimitRanges at the namespace level.


|Dimension |[Specifying ResourceQuotas](https://docs.byteplus.com/en/docs/vke/Setting-ResourceQuotas) |[Specifying LimitRanges](https://docs.byteplus.com/en/docs/vke/Setting-LimitRanges) |
|---|---|---|
|Scope of control |The entire namespace. |A single Container/Pod in a namespace. |
|Content of control |The requests, upper limits, or quantity of total resources. |The minimum, maximum, or default value of a single resource. |
|Management method |After different namespaces are allocated to different users or teams, the cluster administrator can create a ResourceQuota for each namespace. When users or teams create objects in a namespace, the system tracks resource usage to ensure quotas are not exceeded. If an object creation request that will cause the quota to be exceeded is initiated, the request will be denied. |After the cluster administrator sets a LimitRange in a namespace, when users create resources such as Pods and Containers in the namespace, the admission controller (LimitRanger) sets default values and upper limits for Pods or Containers without specified resource requirements. If the resource request for creation or update violates the LimitRange restrictions, the request will be denied. |
|Application scenarios |* Cluster resource sharing among multiple teams: ResourceQuotas can limit the cluster resource quotas that are available to namespaces associated with different teams or projects.<br><br>* Resource usage by environment: ResourceQuotas allocate resource usage quotas for different environments, such as test and production environments.<br><br>* Resource budget management: ResourceQuotas set different resource budgets for different projects to ensure appropriate resource allocation. |* Preventing resource monopoly: LimitRanges prevent a single business from monopolizing cluster resources, such as CPU and memory.<br><br>* Appropriate resource allocation: Limited resources are appropriately allocated to each business namespace to maximize resource utilization.<br><br>* Default resource limits: For objects without resource limits configured, you can use a LimitRange to define request and limit values for resources such as CPU and memory, thereby restricting the amount of resources the objects can use. |
