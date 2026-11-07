---
title: "Creating HPC clusters"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

Before you create HPC\-optimized instances, you need to first create an HPC cluster. Subsequently, you can deploy new HPC\-optimized instances in this cluster. However, you are not allowed to add existing ECS instances to the cluster.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HPC Cluster console](https://console.byteplus.com/ecs/hpcCluster). 

2. In the top menu bar, select the project and region.

3. Click the "Create HPC cluster" button. Configure the parameters described in the following table.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |Region and AZ |Intranets in different regions are completely isolated. We recommend that you select a region that is closest to your business to reduce network latency and improve access speed.<br><br>An availability zone is a physical area with an isolated power grid and network in the same region. To ensure RDMA network connectivity among instances within a cluster, make sure availability zones of the cluster and the instances are the same. |China North 2 (Beijing) availability zone A |
   |Name |Enter the name of the HPC cluster. |HPC\-Cluster 01 |
   |Cluster properties |Select the cluster property that matches the instances.<br><br><br>* RoCE: RoCE (RDMA over Converged Ethernet) is an Ethernet\-based RDMA network protocol that offers high performance and cost\-effectiveness. After creating the HPC cluster, you can only add instances configured with the RoCE RDMA network architecture to it.<br><br>* InfiniBand: A network communication protocol specifically designed for remote direct memory access (RDMA). It features high throughput and low latency. After creating the HPC cluster, you can only add instances configured with the InfiniBand RDMA network architecture to it.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For HPC\-optimized ecs.hpcpni3h.42xlarge, you are required to select the InfiniBand cluster. And for instances of other HPC\-optimized types, you are required to select the RoCE cluster.</div><br> |RoCE |
   |Project |A project is a collection of resources. You can add the new HPC cluster to a project and manage it centrally at the project level, which helps keep resources independent and maintain data security. For more information on projects, refer to [Managing projects](https://docs.byteplus.com/en/docs/ecs/Managing-projects).<br><br><br>* By default, instances are associated with the default project. Each instance can only belong to one project.<br><br>* After you select a project, only users that have permissions on the project can use the created HPC cluster. <br><br>* If you select a specific project in the top navigation bar when entering the creation page, the newly created HPC cluster can only be associated with that project. To associate it with another project, switch the project in the top navigation bar to "All Resources" or the target project.<br><br>* If no projects are available, you can click the "Create project" button to create one. After you create a project, return to this page to select the new project. |default |
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources.<br><br>Click the "+ Add tags" button, and select an existing tag or enter a new tag to associate it with the HPC cluster. For more information, please refer to [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can associate up to 20 tags per request, and associate up to 50 tags with one resource.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the tag key to be associated with the instance overlaps with an existing one, the new tag value will override the original. Please proceed with caution.</div><br> |Key1:Value1 |
   

3. Click the "Create" button to complete creation.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After the HPC cluster is created, you can view the availability zone of the cluster on the HPC Cluster page or details page.

> HPC clusters and the instances deployed within them are displayed by specific project. If no matching resources are found, switch the project in the top menu bar to "All Resources" or the target project.
