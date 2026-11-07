---
title: "Managing existing clusters by using Terraform"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Terraform-to-manage-existing-clusters"
---

This topic describes how to use Terraform to manage existing clusters that were not created by Terraform.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VKE cluster has been created by using the console or by calling the API. For details, see [Creating a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster) and [CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster).

* Terraform has been installed. For details, see [Preparations](https://docs.byteplus.com/en/docs/vke/Managing-clusters-created-using-Terraform#.5YeG5aSH5bel5L2c).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Create a folder and a configuration file named `main.tf` in the folder.

   ```bash
   terraform {
     required_providers {
       byteplus = {
         source = "byteplus-sdk/byteplus"
         version = "0.0.12"  # Get the version information from the official website of Terraform (https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest).
       }
     }
   }
   
   provider "byteplus" {
     access_key = "**********" # The AccessKey ID of the BytePlus account.
     secret_key = "**********" # The AccessKey secret of the BytePlus account.
     region = "ap-southeast-1" # The Region where the VKE application is located.
   }
   
   resource "byteplus_vke_cluster" "vke-tf-test" {
   }
   ```
   

2. Initialize the Terraform environment.

   ```bash
   terraform init
   ```
   

3. Import the cluster.

   ```bash
   terraform import byteplus_vke_cluster.vke-tf-test ccdk7omvqtofl********
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>ccdk7omvqtofl********</code> part is the ID of the cluster to be imported. You can query the cluster ID on the <strong>Basic information</strong> page of the cluster overview page in the VKE console.   </div>
   

   The expected result is as follows.

   ```bash
   byteplus_vke_cluster.vke-tf-test: Importing from ID "..."...
   byteplus_vke_cluster.vke-tf-test: Import prepared!
     Prepared byteplus_vke_cluster for import
   byteplus_vke_cluster.vke-tf-test: Refreshing state... [id=...]
   Import successful!
   The resources that were imported are shown above. These resources are now in
   your Terraform state and will henceforth be managed by Terraform.
   ```
   

   The `terraform.tfstate` file holds information about the imported cluster. An example is shown below:

   ```bash
   {
     "version": 4,
     "terraform_version": "1.2.9",
     "serial": 1,
     "outputs": {},
     "resources": [
       {
         "mode": "managed",
         "type": "byteplus_vke_cluster",
         "name": "vke-tf-test",
   ...
       }
     ]
   }
   ```
   

4. Complete the required and matching fields in the `main.tf` file based on the `terraform.tfstate` file.

   The following code snippet provides an example. For details on required fields, see the [Provider documentation on the Terraform official website](https://github.com/byteplus-sdk/terraform-provider-byteplus).

   ```bash
   resource "byteplus_vke_cluster" "vke-tf-test" {
     name                = "***"
     cluster_config {
       subnet_ids = [
                         "subnet-rrmacce22z9c***********",
                         "subnet-rrmacgc4b37k***********"
                    ]
       }
     pods_config {
       pod_network_mode = "VpcCniShared"
       vpc_cni_config {
         subnet_ids = [
                         "subnet-rrmacce22z9***********",
                         "subnet-rrmacgc4b37***********"
                    ]
       }
     }
     services_config {
       service_cidrsv4 = ["192.168.**.0/**"]
     }
   }    
   ```
   

5. Perform resource planning.

   ```bash
   terraform plan
   ```
   

   The expected result is as follows.

   ```bash
   ...
   No changes. Your infrastructure matches the configuration.
   
   Terraform has compared your real infrastructure against your configuration and found no
   differences, so no changes are needed.
   ```
