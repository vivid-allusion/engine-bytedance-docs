---
title: "Managing existing nodes in the default node pool by using Terraform"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Terraform-to-add-existing-nodes-to-a-cluster"
---

This topic describes how to create a default node pool in a cluster created using Terraform, and how to add existing nodes to or remove existing nodes from the default node pool.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created by using Terraform. For details, see [Managing clusters created using Terraform](https://docs.byteplus.com/en/docs/vke/Managing-clusters-created-using-Terraform).

* You have available ECS instances in the same VPC as the cluster. For details, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5Yib5bu66buY6K6k6IqC54K55rGg5bm25re75Yqg5bey5pyJ6IqC54K5"></span>
## Creating a default node pool and adding existing nodes to the default node pool

To create a default node pool using Terraform and add existing nodes to the default node pool, follow the steps below.


1. Create a folder and a configuration file named `main.tf` in it.

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
     endpoint = "open.ap-southeast-1.byteplusapi.com"
   }
   
   data "byteplus_vke_clusters" "default" {
     name_regex = "tf-created-vke"  # The name of the cluster to which the node created through Terraform belongs.
   }
   
   #Creating a default node pool and adding an existing node
   resource "byteplus_vke_default_node_pool" "vke_test" {
     cluster_id = data.byteplus_vke_clusters.default.clusters[0].id
     node_config {
       security {
         login {
           password = "*****"  # The access method of the node, that is, a root user login password. The password is Base64-encoded.
         }
       }
     }
     instances {
       instance_id = "i-ybwgrtud6d********"  # The ID of the existing node, that is, the ID of an Elastic Compute Service (ECS) instance.
       keep_instance_name = true  # Whether to retain the name of the ECS instance. true: retain the name; false: rename the ECS instance after it is added to the cluster.
       additional_container_storage_enabled = true  # Whether to format the data volume and mount the formatted data volume to the storage directories of containers and images. true: yes; false: no.
       container_storage_path = "/dev/vdb"  # Specify the directory to which you want to mount the data volume.
     }
     instances {
       instance_id = "i-ybwgqqpjav********"
       keep_instance_name = true
       additional_container_storage_enabled = true
       container_storage_path = "/dev/vdb"
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
   

4. Create a default node pool and add existing nodes to the default node pool.

   ```bash
   terraform apply
   ```
   

   You can also check the existing nodes in the default node pool `vke-default-nodepool` in the [VKE console](https://console.byteplus.com/vke).


<span id=".5LuO6buY6K6k6IqC54K55rGg5Lit56e76Zmk6IqC54K5"></span>
## Removing nodes from the default node pool

To remove a previously added node from the default node pool using Terraform, follow these steps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Regardless of whether the billing method for the existing node to be removed is subscription or pay\-as\-you\-go, this action will not release the node. You can release the node in the ECS console. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">Deleting instances</a>.</div>



1. Delete the content of the **instances** field from the `main.tf` file.

   ```bash
     ...
     #instances {
     #  instance_id = "i-ybwgqqpjav********"
     #  keep_instance_name = true
     #  additional_container_storage_enabled = true
     #  container_storage_path = "/dev/vdb"
     #}
     ...
   ```
   

2. Run the command to remove the node.

   ```bash
   terraform apply
   ```
   

   You can check whether the node has been removed from the default node pool in the [VKE console](https://console.byteplus.com/vke).
