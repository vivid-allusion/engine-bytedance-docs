---
title: "Managing node pools created via Terraform"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-NodePools-created-using-Terraform"
---

After you create a cluster by using Terraform, you can continue to use Terraform to manage the cluster. For example, you can create custom node pools within the cluster, scale out custom node pools, and delete custom node pools.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A cluster has been created by using Terraform. For details, see [Managing clusters created using Terraform](https://docs.byteplus.com/en/docs/vke/Managing-clusters-created-using-Terraform).

<span id=".5re75Yqg6Ieq5a6a5LmJ6IqC54K55rGg"></span>
## Creating custom node pools

To create a custom node pool within a cluster by using Terraform, follow these steps.


1. Create a folder and a configuration file named `main.tf` within it.

   ```bash
   terraform {
     required_providers {
       byteplus = {
         source = "byteplus-sdk/byteplus"
         version = "0.0.12" # Get the version information from the official website of Terraform (https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest).
       }
     }
   }
   
   provider "byteplus" {
     access_key = "**********"  # The AccessKey ID of the BytePlus account.
     secret_key = "**********"  # The AccessKey secret of the BytePlus account.
     region = "ap-southeast-1"  # The Region where the VKE application is located.
     endpoint = "open.ap-southeast-1.byteplusapi.com"
   }
   
   data "byteplus_vke_clusters" "default" {
     name_regex = "tf-created-vke"  # The name of the cluster to which the node pool created through Terraform belongs.
   }
   
   resource "byteplus_vke_node_pool" "node-pool-test" {
     cluster_id = data.byteplus_vke_clusters.default.clusters[0].id
     name = "demo"  # The name of the custom node pool.
     node_config {
       instance_type_ids = ["ecs.g3il.large"]  # The specification of the Elastic Compute Service (ECS) instance to which the node corresponds.
       subnet_ids = ["subnet-rrmacgc4b37kv******"]  # The ID of the subnet to which the network of the node belongs.
       security {
         login {
           password = "*******"  # The access method of the node, that is, a root user login password. The password is Base64-encoded.
         }
       }
       #The system volume. Select a node type that supports mounting to the system volume of the specified type.
       system_volume {
         type = "ESSD_PL0"  # The type of the volume. PTSSD (to be out of support soon): performance type SSD volume; ESSD_PL0: PL0 Enhance SSD volume; ESSD_FlexPL: PL1 Enhance SSD volume.
         size = 40  # The volume capacity. Unit: GiB. The PTSSD volume capacity ranges from 40 to 500. The ESSD_PL0 or ESSD_FlexPL volume capacity ranges from 40 to 2048.
       }
   
       #After the system volume setting, the first data volume is mounted to /mnt/vdb. The /var/lib/containerd and /var/lib/kubelet directories are mounted too.
       #If you set a custom mount target, the first data volume is mounted to the custom mount target. The /var/lib/containerd and /var/lib/kubelet directories are mounted too.
       additional_container_storage_enabled = true
       #The data volumes. Select a node type that supports mounting to a data volume of the specified type. A custom mount target can be configured.
       data_volumes  {
         type = "ESSD_PL0"  # The type of the volume. PTSSD (to be out of support soon): performance type SSD volume; ESSD_PL0: PL0 Enhance SSD volume; ESSD_FlexPL: PL1 Enhance SSD volume.
         size = 50  # The volume capacity. Unit: GiB. The PTSSD volume capacity ranges from 40 to 500. The ESSD_PL0 or ESSD_FlexPL volume capacity ranges from 40 to 2048.
       }
       data_volumes  {
         type = "ESSD_PL0"
         size = 50
       }
       ecs_tags {   #The tags associated with the ECS instances corresponding to the nodes. The labels are used to search and manage ECS instances.
         key = "ecs_k1"
         value = "ecs_v1"
       }
     }
     auto_scaling {
       enabled = false  # Whether to enable auto scaling for the node pool. true: enable; false: disable.
       max_replicas = 5  # The maximum number of nodes in the node pool.
       min_replicas = 0  # The minimum number of nodes in the node pool.
       desired_replicas = 0  # The desired number of nodes in the node pool.
       priority = 15  # The priority, which only takes effect in priority-based algorithms.
     }
     kubernetes_config {
       #Configure the node label
       labels {
         key = "aaa"
         value ="bbb"
       }
       cordon = false  # Whether to cordon a node. true: cordon; false: not cordon.
     }
     tags {  #The custom label of the node pool
       key = "k1"
       value = "v1"
     }
   }
   ```
   

2. Initialize the Terraform environment.

   ```bash
   terraform init
   ```
   

3. Perform resource planning.

   ```bash
   terraform plan
   ```
   

4. Creating the custom node pool.

   ```bash
   terraform apply
   ```
   

   The expected result is as follows.

   ```bash
   ...
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```
   

   You can view the created custom node pool in the [VKE console](https://console.byteplus.com/vke).


<span id=".6IqC54K55rGg5omp5a656IqC54K5"></span>
## Increasing or decreasing the number of nodes

To scale a node pool created through Terraform, follow the steps below:


1. Set **auto_scaling.desired_replicas** in the `main.tf` file to a value between **max_replicas** and **min_replicas**.

   ```bash
     auto_scaling {
       enabled = false
       max_replicas = 5
       min_replicas = 0
       desired_replicas = 2 # The manually set number of nodes to which you want to scale the node pool.
       priority = 15
     }
   ```
   

2. Run the scaling command.

   ```bash
   terraform apply
   ```
   

   You can check the nodes in the cluster after scaling in the [VKE console](https://console.byteplus.com/vke).


<span id=".5Yig6Zmk6Ieq5a6a5LmJ6IqC54K55rGg"></span>
## Deleting custom node pools

To delete a node pool created through Terraform, follow the steps below:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When deleting a custom node pool using Terraform, you cannot retain worker nodes in the node pool. All non\-subscription worker nodes will be automatically released. Exercise caution when you perform this operation.</div>


Run the following command to delete the custom node pool.

```bash
terraform destroy
```


The expected results are as follows:

```bash
...
Destroy complete! Resources: 1 destroyed.
```
