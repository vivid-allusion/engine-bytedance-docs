---
title: "Overview of large-scale cluster management"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Overview_of_large-scale_cluster_management"
---

This topic provides a complete set of suggestions and guidelines for setting up large\-scale clusters in VKE. We recommend following these suggestions to ensure large\-scale workloads run stably within Kubernetes SLOs and to fully leverage the high\-performance features of VKE.

<span id="ASuu0UJp"></span>
## What is a large\-scale cluster

In most cases, if a cluster has more than 500 nodes or more than 10,000 Pods, it is considered a large\-scale cluster. You need to plan your cluster based on the suggestions in this topic to ensure the stable operation of the cluster.

<span id="tn7wqzAF"></span>
## How to use this topic

Before you plan and create a VKE cluster, we recommend first determining the key parameters of your workloads (such as the expected number of services and required computing resources) and mapping them to the core resources of the Kubernetes cluster (such as Nodes, Pods, and Services). Based on this information, you can refer to the suggestions in this topic in a more targeted manner.

This topic summarizes the stability practices for large\-scale clusters into the following three topics, which cover the three key stages: cluster creation, usage, and subsequent operations.


* [Large-scale cluster version and configuration](https://docs.byteplus.com/en/docs/vke/Large-scale_cluster_version_and_configuration) (focusing on the cluster creation stage): Describes how to select appropriate Kubernetes versions, network models (VPC\-CNI), and add\-on settings for large\-scale clusters. Appropriate initial settings are the foundation of stable cluster operation. This topic helps you make key decisions before creating a cluster.

* [Large-scale cluster limits and suggestions](https://docs.byteplus.com/en/docs/vke/Large-scale_cluster_limits_and_suggestions) (focusing on the usage stage): Provides a detailed list of known limits of VKE and Kubernetes in large\-scale scenarios and best practices to avoid these limits. This helps you design an architecture that can scale smoothly during usage.

* [Large-scale cluster O&M guarantee](https://docs.byteplus.com/en/docs/vke/Large-scale-cluster-OM-guarantee) (focusing on the O&M stage): Focuses on the daily O&M of large\-scale clusters, which involves monitoring and alerting configuration as well as resource quota management. This ensures high availability of large\-scale clusters.


The preceding scalability suggestions apply to all modes of VKE, including scenarios where managed node pools and VCI workloads are deployed together. For workloads deployed through VCI, some suggestions involving node management may not be applicable. Refer to the specific topic for details.

<span id="Ou5BCZln"></span>
## About ultra\-large\-scale clusters

To create an ultra\-large\-scale cluster with more than 5,000 nodes or more than 150,000 Pods, contact the VKE team through the [ticket system](https://console.byteplus.com/workorder/create) or your dedicated solution architect. We will provide you with targeted architecture reviews, parameter tuning, and dedicated support to ensure the stable operation of your ultra\-large\-scale cluster.
