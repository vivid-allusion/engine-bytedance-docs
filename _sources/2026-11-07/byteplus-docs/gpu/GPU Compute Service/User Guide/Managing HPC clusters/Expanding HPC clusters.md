---
title: "Expanding HPC clusters"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Scaling-up-HPC-clusters"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can expand an HPC cluster at any time as needed by adding newly purchased HPC\-optimized instances to it.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* Within the same cluster, only ECS instances within the same availability zone can be added. Therefore, when scaling up the cluster, the existing availability zone of ECS instances will automatically be inherited and can not be modified.

* HPC Cluster and the instances within the cluster do not have an association with the VPC. Instances meeting the conditions and belonging to different VPCs can be added to the same cluster.

* If the target instance type within the availability zone associated with the cluster is sold out, the expansion operation is not supported.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [HPC Cluster console](https://console.byteplus.com/ecs/hpcCluster). 

2. In the top menu bar, select the region and project of the target cluster.

3. Click the "Expansion" button in the "Actions" column of the target cluster to enter the Create Instances page.

4. You can refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to complete the operation.
