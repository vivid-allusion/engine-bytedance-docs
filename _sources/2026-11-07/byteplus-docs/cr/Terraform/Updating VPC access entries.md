---
title: "Updating VPC access entries"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Update_VPC_entry_point"
---

This topic describes how to use Terraform to update VPC access entries.

## Prerequisites

* You have completed the preparations for using Terraform in CR. For operation details, see [Preparations](https://docs.byteplus.com/en/docs/cr/Preparation?lang=en).

* Obtain VPC\-related parameter information.

   |Parameter |Description |
   |---|---|
   |vpcid |The ID of the VPC to add or retain. For example, `vpc-13g1chlhy0d8g3n6nu4gc****`. To view the VPC ID, see [Viewing details of a VPC](https://docs.byteplus.com/en/docs/vpc/Viewing-details-of-a-VPC). |
   |subid |The ID of the VPC subnet. For example, `subnet-13fw7xf83jim83n6nu4ce****`. Log in to the [Subnet console](https://console.byteplus.com/vpc/subnet) to view the target subnet ID. |

## Procedure

> **warning**

> During this operation, specify the complete list of VPC IDs. Terraform will use the VPC IDs defined in the `main.tf` configuration file to replace the existing VPC endpoint configuration.

> For example, if you have added VPC\-A, but only enter the IDs of VPC\-B and VPC\-C in the `main.tf` configuration file for this update. After the operation succeeds, the VPC\-A access entry will be removed, and the VPC\-B and VPC\-C access entries will be added.

1. Log in to the terminal where Terraform is installed.

2. Create a folder and a configuration file named `main.tf` in it.

   ```go
   variable "common" {
     type = object({
       registry = string
       region   = string
       vpcid    = string
       subid    = string
       vpcid2   = string
       subid2   = string
   #   To cover three or more VPCs, add VPC and subnet parameters as needed.
   #   vpcid3   = string
   #   subid3   = string
     })
     default = {
       # Instance name
       registry = "***test"
       # Region where the instance is deployed
       region   = "cn-beijing"
       # ID of the VPC to be covered
       vpcid    = "vpc-mjaw2apyzx8g5smt1a5d****"
       # ID of the subnet associated with the VPC to be covered
       subid    = "subnet-rr10v9czmlfkv0x58yy****"
       vpcid2   = "vpc-rs5zapo0osu8v0x58o9****"
       subid2   = "subnet-13fw7xf83jim83n6nu4ce****"
   #   To cover three or more VPCs, configure the corresponding VPC IDs and subnet IDs as needed.
   #   vpcid3   = "vpc-13fw35b36rc3k3n6nu5ft****"
   #   subid3   = "subnet-mj7fzyemvhfk5smt1be1****"
     }
   }
   
   provider "volcengine" {
     # AK of the BytePlus account
     access_key = "AKLT****"
     # SK of the BytePlus account
     secret_key = "WmpW****"
     region     = var.common.region
   }
   
   resource "volcengine_cr_vpc_endpoint" "label" {
     registry = var.common.registry
   
     vpcs {
       vpc_id    = var.common.vpcid
       subnet_id = var.common.subid
     }
   
     vpcs {
       vpc_id    = var.common.vpcid2
       subnet_id = var.common.subid2
     }
   
   # To cover three or more VPCs, add more parameters as needed.
   # vpcs {
   #   vpc_id    = var.common.vpcid3
   #   subnet_id = var.common.subid3
   # }
   }
   ```

3. Initialize the Terraform environment.

   ```bash
   terraform init
   ```

4. Update the VPC configuration.

   ```bash
   terraform import volcengine_cr_vpc_endpoint.label crVpcEndpoint:***test
   ```

   > **tip**

   > Replace `***test` (the example name in this topic) after `crVpcEndpoint` with the name of your instance.

5. Perform resource planning.

   ```bash
   terraform plan
   ```

6. Update VPC access endpoint information.

   ```bash
   terraform apply -auto-approve
   ```

## Results

After the operation is complete, you can view the updated VPC endpoint information in the VPC list on the console.
