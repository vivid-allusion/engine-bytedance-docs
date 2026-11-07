---
title: "Managing existing nodes in a custom node pool by using Terraform"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Terraform-to-managing-existing-nodes-in-a-custom-node-pool"
---

This topic describes how to add nodes to or remove nodes from a custom node pool by using Terraform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created by using Terraform. For details, see [Managing clusters created with Terraform](https://docs.byteplus.com/en/docs/vke/Managing-clusters-created-using-Terraform).

* A node pool has been created by using Terraform. For details, see [Creating custom node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools-created-using-Terraform#.5re75Yqg6Ieq5a6a5LmJ6IqC54K55rGg).

* There are ECS instances that can be added. For details, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id="limits"></span>
## Limit

When you add an existing ECS instance to a custom node pool:


* The custom node pool must meet the following requirements:

   * The **autoscaler** is not enabled for the node pool.

   * The current node pool status is **running**.

   * The current node pool billing mode is **Pay\-as\-you\-go** or **Subscription**.

* For ECS instances, the following conditions need to be met:

   * Running in the same VPC as the current cluster.

   * Be under the same project as the target node pool.

   * The instance is not in a scaling group of any cluster or autoscaler service.

   * The instance only has one network interface card.

   * The system volume of the instance has a `capacity` ≥ (`image size configured for the target node pool` + `10 GiB`).

   * The data volumes of the instance must include the data volumes specified for mounting in the target node pool, and the volume type and size must be exactly the same.


<span id=".5Yib5bu66buY6K6k6IqC54K55rGg5bm25re75Yqg5bey5pyJ6IqC54K5"></span>
## Adding existing nodes to a custom node pool

Follow the steps below to add an ECS instance to a custom node pool by using Terraform.


1. Create a folder and a configuration file named `main.tf` in the folder.

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
     region = "ap-southeast-1" # The Region where the VKE application is located.
   }
   data "byteplus_vke_clusters" "default" {
     name_regex = "tf-created-vke"  # The name of the cluster to which the node created through Terraform belongs.
   }
   resource "byteplus_vke_node_pool" "node-pool-test" {
     cluster_id = data.byteplus_vke_clusters.default.clusters[0].id
     name = "demo"  # The name of the custom node pool.
     instance_ids = ["i-ydazicr0n4yg********"]  # The ID of the existing node, that is, the ID of an Elastic Compute Service (ECS) instance.
     keep_instance_name = true  # Whether to retain the name of the ECS instance. true: retain the name; false: rename the ECS instance after it is added to the cluster.
     node_config {
       instance_type_ids = ["ecs.g3il.large"]  # The specification of the Elastic Compute Service (ECS) instance to which the node corresponds.
       subnet_ids = ["subnet-rrmacgc4b37kv******"]  # The ID of the subnet to which the network of the node belongs.
       security {
         login {
           password = "*******"  # The access method of the node, that is, a root user login password. The password is Base64-encoded.
         }
       }
       # The system volume. Select a node type that supports mounting to the system volume of the specified type.
       system_volume {
         type = "ESSD_PL0"  # The type of the volume. PTSSD (to be out of support soon): performance type SSD volume; ESSD_PL0: PL0 Enhance SSD volume; ESSD_FlexPL: PL1 Enhance SSD volume.
         size = 40  # The volume capacity. Unit: GiB. The PTSSD volume capacity ranges from 40 to 500. The ESSD_PL0 or ESSD_FlexPL volume capacity ranges from 40 to 2048.
       }
       # After the system volume setting, the first data volume is mounted to /mnt/vdb. The /var/lib/containerd and /var/lib/kubelet directories are mounted too.
       # If you set a custom mount target, the first data volume is mounted to the custom mount target. The /var/lib/containerd and /var/lib/kubelet directories are mounted too.
       additional_container_storage_enabled = true    
       # The data volumes. Select a node type that supports mounting to a data volume of the specified type. A custom mount target can be configured.
       data_volumes  {
         type = "ESSD_PL0"  # The type of the volume. PTSSD (to be out of support soon): performance type SSD volume; ESSD_PL0: PL0 Enhance SSD volume; ESSD_FlexPL: PL1 Enhance SSD volume.
         size = 50     # The volume capacity. Unit: GiB. The PTSSD volume capacity ranges from 40 to 500. The ESSD_PL0 or ESSD_FlexPL volume capacity ranges from 40 to 2048.
       }
       data_volumes  {
         type = "ESSD_PL0"
         size = 50
       }
       ecs_tags {      # The tags associated with the ECS instances corresponding to the nodes. The labels are used to search and manage ECS instances.
         key = "ecs_k1"
         value = "ecs_v1"
       }
     }
     kubernetes_config {
       # Configure the node label
       labels {
         key = "aaa"
         value ="bbb"
       }
       cordon = false  # Whether to cordon a node. true: cordon; false: not cordon.
     }
     tags {            # The custom label of the node pool
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
   

4. Add the existing instance to the custom node pool.

   ```bash
   terraform apply
   ```
   

   You can also log in to the [VKE console](https://console.byteplus.com/vke) to view the node added to the custom node pool.


<span id=".5LuO6buY6K6k6IqC54K55rGg5Lit56e76Zmk6IqC54K5"></span>
## Removing a node from a custom node pool

You can follow the steps below to use Terraform to remove an existing node you added before from the custom node pool.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Regardless of whether the billing method for the existing node to be removed is subscription or pay\-as\-you\-go, this action will not release the node. You can release the node in the ECS console. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">Deleting instances</a>.</div>



1. Remove the target ECS instance ID from the `instance_ids` parameter under the `byteplus_vke_node_pool` in the `main.tf` file.

   ```bash
   ...
   resource "byteplus_vke_node_pool" "node-pool-test" {
     cluster_id = data.byteplus_vke_clusters.default.clusters[0].id
     name = "demo"
     instance_ids = ["i-ydazicr0n4yg********"]  # Remove the target ECS instance ID from this parameter (including "").
   ...
   }
   ```
   

2. Run the command to remove the node.

   ```bash
   terraform apply
   ```
   

   You can check whether the node has been removed from the target custom node pool in the [VKE console](https://console.byteplus.com/vke).
