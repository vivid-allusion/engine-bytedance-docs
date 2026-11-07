---
title: "Workload overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Workload-overview"
---

In Kubernetes, a workload is an abstract model representing a group of pods (a group of containers). It can refer to any of the service entities, such as Deployment, StatefulSet, DaemonSet, Job, and CronJob. A workload is also known as a pod controller, which ensures that an expected number of pods of the desired type are running. Vital Kubernetes Engine (VKE) is built on native Kubernetes capabilities and supports full lifecycle management of container workloads.

<span id=".5a655Zmo57uE5ZKM5bel5L2c6LSf6L29"></span>
## Pods and workloads

A pod is the smallest deployable computing unit in Kubernetes. A pod encapsulates one or more containers, storage resources (volume), an independent network IP address, and policies for managing and controlling how containers run.

A workload is used for managing pods. A workload can manage one or more pods, and supports multi\-version management, rolling updates, and automatic recovery capabilities. You can use workloads and pod templates to create pods that meet your business requirements.

<span id=".5peg54q25oCB5bel5L2c6LSf6L29"></span>
## Deployments

A Deployment can contain one or more pod replicas, each with the same role. The system automatically distributes requests among the multiple pod replicas in the Deployment.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8c42935419bd0f70da56d31b1fa71b6b.png) </span>

A Deployment integrates the functionalities of deployment, rolling updates, replica creation, and rollback and enables unattended operations. This significantly reduces the complexity and operational risks during the deployment process. A Deployment is commonly used to deploy stateless applications. Compared to stateful applications, Deployments can enable automated and flexible scaling.

<span id=".5pyJ54q25oCB5bel5L2c6LSf6L29"></span>
## StatefulSets

Similar to Deployments, StatefulSets manage application deployment and scaling. Additionally, StatefulSets provide persistent storage and stable network identifiers for pods, enabling the deployment of stateful services such as databases, caches, and similar applications.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a256eb5c62ff297d3fe2b1c2375e2d35.png) </span>

<span id=".5a6I5oqk6L-b56iL"></span>
## DaemonSets

A DaemonSet ensures that all (or some) Nodes run a copy of a pod. When nodes are added to the cluster, pods are added to them. When nodes are removed from the cluster, those pods will be reclaimed. Deleting a DaemonSet will delete all pods that it created. DaemonSets are node\-specific. If a node becomes unavailable, the pods are not recreated on other nodes.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_fc3439bd636f7b2daf72c480db7774e4.png) </span>

DaemonSet is applicable to foundational system\-level applications such as log collection and resource monitoring. These applications need to run on every node and do not require many instances.

<span id=".5Lu75Yqh5ZKM5a6a5pe25Lu75Yqh"></span>
## Jobs and CronJobs

Jobs and CronJobs manage batch processing of short\-lived one\-off tasks, executing them only once. They ensure the successful completion of one or more pods in batch jobs. Jobs and CronJobs are applicable to one\-off tasks, such as those in continuous integration.


* Job: Controls batch jobs. Pods managed by a Job will automatically exit (and the pods will be deleted automatically) once they successfully complete the task as per the specified settings.

* CronJob: A CronJob is a time\-based Job, similar to a Crontab expression on a Linux system, that runs the specified Job at the specified intervals.


<span id=".5bel5L2c6LSf6L2955Sf5ZG95ZGo5pyf6K-05piO"></span>
## Workload lifecycle description


|Status |Description |
|---|---|
|Ready |When replicas are in the Ready state, the workload is in this state.<br><br>The **Ready n/n** displayed on the console indicates **Number of Ready replicas / Total number of replicas**. |
|Updated |When replicas are in the Update status, the workload is in this state, which indicates that the replicas have completed the update. |
|Available |When replicas are in the Available state, the workload is in this state, which indicates that the replicas within the workload are running normally. |
|Active |When replicas are in the Active state (the replicas are running normally and have not been suspended), the workload enters this status. |
|Succeeded |When replicas are in the Succeeded state, the workload is in this state. This state only appears in Job and CronJob workloads. |
|Fail |When replicas are in the Failed state, the workload is in this state. |
