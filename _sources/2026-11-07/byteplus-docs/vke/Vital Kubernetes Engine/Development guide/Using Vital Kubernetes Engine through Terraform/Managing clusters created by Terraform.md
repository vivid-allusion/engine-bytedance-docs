---
title: "Managing clusters created by Terraform"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-clusters-created-using-Terraform"
---

This topic describes how to create clusters using Terraform and manage such clusters.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Before managing VKE clusters with Terraform, follow the steps below to install Terraform.


1. Download and install the desired version from the official Terraform website. For details, see [Terraform documentation](https://www.terraform.io/downloads).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the Terraform version is not lower than v0.13. You can run the <code>terraform version</code> command to query the version.   </div>
   

2. Configure BytePlus account information in Terraform.

   1. Create environment variables to store authentication credentials.

      ```bash
      export BYTEPLUS_ACCESS_KEY="AK************"
      export BYTEPLUS_SECRET_KEY="************"
      export BYTEPLUS_REGION="ap-southeast-1"
      ```
      

      The following table describes the parameters.

      
      |Parameter |Description |
      |---|---|
      |BYTEPLUS_ACCESS_KEY |The AK of your Byteplus root user. For instructions on obtaining the SK, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |BYTEPLUS_SECRET_KEY |The SK of your Byteplus root user. For instructions on obtaining the SK, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |BYTEPLUS_REGION |The region where the VKE cluster is located. For the regions supported by VKE, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |
      

   2. Specify the provider section of the configuration file.

      ```bash
      provider "byteplus" {
        access_key = "AK************"
        secret_key = "************"
        session_token = "sts token"
        region = "ap-southeast-1"
      }
      ```
      

      The following table describes the parameters.

      
      |Parameter |Description |
      |---|---|
      |access_key |The AK of your Byteplus root user. For instructions on obtaining the AK, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |secret_key |The SK of your Byteplus root user. For instructions on obtaining the SK, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |session_token |(Optional) The security token for role assumption, which can be obtained by calling the [AssumeRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole) API. |
      |region |The region where the VKE cluster is located. Specify the same value as the value of the **BYTEPLUS_REGION** parameter configured in the previous step. |
      


<span id=".5Yib5bu66ZuG576k"></span>
## Creating a cluster


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
     access_key = "**********"
     secret_key = "**********" 
     region = "ap-southeast-1" # The Region where the VKE application is located.
     endpoint = "open.ap-southeast-1.byteplusapi.com"
   }
   
   
   #Create a Virtual Private Cloud (VPC)
   resource "byteplus_vpc" "vke-tf-vpc" {
     vpc_name    = "vke-tf-vpc" # The name of the VPC.
     cidr_block  = "172.16.0.0/16" # The Classless Inter-Domain Routing (CIDR) block of the VPC.
   }
   
   #Create a Virtual Switch (VSW)
   resource "byteplus_subnet" "vke-tf-vsw" {
     subnet_name = "vke-tf-vsw-1" # The subnet name of the VSW.
     cidr_block  = "172.16.0.0/24" # The CIDR block of the VSW.
     zone_id     = "ap-southeast-1a" # The Availability Zone of the VSW.
     vpc_id      = byteplus_vpc.vke-tf-vpc.id # The ID of the VPC to which the VSW belongs.
   }
   
   #Create a VKE cluster
   resource "byteplus_vke_cluster" "vke-tf-test" {
     name                = "tf-created-vke" # The name of the cluster.
     kubernetes_version  = "1.24" # The Kubernetes version of the cluster. The version number only supports the x.y format rather than x.y.z.
     # For more information on Kubernetes versions that VKE supports, refer to https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes.
     description         = "vke created by tf" # The description of the cluster.
     delete_protection_enabled = true # Whether to enable Delete Protection. true: enable; false: disable.
     cluster_config {
       subnet_ids = [byteplus_subnet.vke-tf-vsw.id] # The subnet ID of the cluster.
       api_server_public_access_enabled = true # Whether to enable Public access to API Server. true: enable; false: disable.
       #Configure the Elastic IP Address (EIP) billing method and bandwidth for the API Server
       api_server_public_access_config {
         public_access_network_config {
           billing_type    = "PostPaidByTraffic" # The EIP billing method. PostPaidByTraffic: the pay-as-you-go billing method based on the actual traffic; PostPaidByBandwidth: the pay-as-you-go billing method based on the maximum bandwidth.
           bandwidth       = 10 # The maximum EIP bandwidth. The range of valid values for PostPaidByTraffic is 1 to 200. The range of valid values for PostPaidByBandwidth is 1 to 500.
         }
       }
       resource_public_access_default_enabled = true # Whether to enable internet-facing access. true: enable; false: disable.
     }
     pods_config {
       pod_network_mode = "VpcCniShared"  # The container network mode. VpcCniShared: the VPC-CNI network model; Flannel: the Flannel network model.
       #When the network model is Flannel, flannel_config takes effect.
       flannel_config {
         pod_cidrs = ["192.168.0.0/20"]  # The Pod CIDR of the Flannel container network.
         max_pods_per_node = 64  # The maximum number of single-node pod instances in the Flannel container network. Valid values: 64, 16, 32, 128, and 256.
       }
       #When the network model is VpcCniShared, vpc_cni_config takes effect.
       vpc_cni_config {
         subnet_ids = [byteplus_subnet.vke-tf-vsw.id]  # The pod subnet ID of the VPC-CNI container network.
       }
     }
     #Configure a CIDR for Services in the cluster
     services_config {
       service_cidrsv4 = ["192.168.16.0/24"]  # The CIDR that Services in the cluster use.
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
   

   The expected result is as follows.

   ```bash
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # byteplus_subnet.vke-tf-vsw will be created
     + resource "byteplus_subnet" "vke-tf-vsw" {
         + cidr_block      = "172.16.0.0/24"
         + creation_time   = (known after apply)
         + enable_ipv6     = (known after apply)
         + id              = (known after apply)
         + ipv6_cidr_block = (known after apply)
         + status          = (known after apply)
         + subnet_name     = "vke-tf-vsw-1"
         + vpc_id          = (known after apply)
         + zone_id         = "ap-southeast-1a"
       }
   
     # byteplus_vke_addon.fo1 will be created
     + resource "byteplus_vke_addon" "fo1" {
         + cluster_id       = (known after apply)
         + config           = (known after apply)
         + deploy_mode      = (known after apply)
         + deploy_node_type = "VirtualNode"
         + id               = (known after apply)
         + name             = "vci-virtual-kubelet"
         + version          = (known after apply)
       }
   ....
   ```
   

4. Creates a cluster.

   ```bash
   terraform apply
   ```
   

   The expected result is as follows.

   ```bash
   Plan: 21 to add, 0 to change, 0 to destroy.
   
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value:
   ```
   

   You can log in to the [VKE console](https://console.byteplus.com/vke) to view the created cluster.


<span id=".5pu05paw6ZuG576k"></span>
## Updating a cluster

Follow the steps below to use Terraform to update a cluster created by Terraform.


1. Update the `main.tf` file and set the **delete_protection_enabled** field to **false** to disable cluster deletion protection.

   ```bash
   ...
     description         = "vke created by tf"
     delete_protection_enabled = false
     cluster_config {
   ...
   ```
   

2. Update cluster configurations.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Because the field for updating the cluster configuration is not a ForceNew field, resources will not be deleted and recreated.   </div>
   

   ```bash
   terraform apply
   ```
   

   The expected result is as follows.

   ```bash
   ...
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     ~ update in-place
   Terraform will perform the following actions:
   ...
   Plan: 0 to add, 1 to change, 0 to destroy.
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
     Enter a value: yes
   ...
   Apply complete! Resources: 0 added, 1 changed, 0 destroyed. 
   ```
   


<span id=".5Yig6Zmk6ZuG576k"></span>
## Deleting a cluster

Follow the steps below to use Terraform to delete a cluster created by Terraform.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you delete a cluster by using Terraform, all cluster\-associated resources except subscription worker nodes will be automatically released. Exercise caution when you perform this operation.</div>



1. Update the `main.tf` file and set the **delete_protection_enabled** field to **false** to disable cluster deletion protection.

   ```bash
   ...
     description         = "vke created by tf"
     delete_protection_enabled = false
     cluster_config {
   ...
   ```
   

2. Delete the target cluster and associated resources, such as CLB resources used by the cluster API Server.

   ```bash
   terraform destroy
   ```
   

   The expected result is as follows.

   ```bash
   ...
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     ~ update in-place
   
   Terraform will perform the following actions:
   ...
   Do you really want to destroy all resources?
     Terraform will destroy all your managed infrastructure, as shown above.
     There is no undo. Only 'yes' will be accepted to confirm.
   
     Enter a value: yes
   ...
   Destroy complete! Resources: 3 destroyed.
   ```
