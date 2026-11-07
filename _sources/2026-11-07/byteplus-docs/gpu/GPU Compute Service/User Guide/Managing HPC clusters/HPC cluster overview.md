---
title: "HPC cluster overview"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/HPC-cluster-overview"
---

<span id=".5LuA5LmI5piv6auY5oCn6IO96K6h566X6ZuG576k"></span>
## What is an HPC cluster

A High Performance Computing (HPC) Cluster is a clustered computing environment designed for large\-scale computational tasks. It typically comprises a large number of compute nodes interconnected via a high\-speed RDMA (Remote Direct Memory Access) network, which work together to handle complex computational tasks. An HPC cluster can provide powerful computing capabilities, large memory, high\-speed storage, and a high\-speed network to meet the requirements of compute\-intensive, data\-intensive, or combined workloads.

In HPC clusters, compute tasks are assigned to compute nodes for parallel processing. A compute node is a single compute unit in the cluster, typically a server or computer, responsible for executing specific compute tasks. This enables full utilization of the computing capabilities of multiple nodes, accelerating computations and improving efficiency.

You can use the HPC cluster feature provided by the platform to logically isolate HPC\-optimized instances (compute nodes). Instances within the same cluster are interconnected through the RDMA network, while instances in different clusters are isolated from each other on the RDMA network.

<span id=".5Lia5Yqh54m554K5"></span>
## Business features


* Powerful computing capability: An HPC cluster composed of a large number of compute nodes provides powerful compute resources for large\-scale and complex compute tasks.

* Efficiency: In an HPC cluster, computing tasks can be completed efficiently via parallel computing and distributed processing, thereby enhancing work efficiency.

* Supported large memory and high\-speed storage: This helps handling large amounts of data and high\-speed data transmission.

* Scalability: Compute nodes can be flexibly added or deleted based on your needs. This helps handling compute tasks of different scales.

* Wide applicability: Scientific computing, machine learning, data analytics and other scenarios.


<span id=".5bqU55So5Zy65pmv"></span>
## Applicable scenarios

HPC clusters are typically used to handle tasks that require a large amount of computing resources and high\-speed data transfer. For example, scientific computing, engineering simulation, weather forecasting, financial analysis, and artificial intelligence training.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


|Feature |Document |
|---|---|
|Compute nodes that can be added to HPC clusters |[HPC-optimized](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types) |
|Creating HPC\-optimized instances and adding them to HPC clusters |[Purchasing HPC-optimized instances](https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances) |
|Creating HPC clusters when no HPC cluster is available |[Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters) |
|How to add compute nodes to HPC clusters |[Expanding HPC clusters](https://docs.byteplus.com/en/docs/gpu/Scaling-up-HPC-clusters) |
|Deleting HPC clusters that are no longer in use |[Deleting HPC clusters](https://docs.byteplus.com/en/docs/gpu/Deleting-HPC-clusters) |
