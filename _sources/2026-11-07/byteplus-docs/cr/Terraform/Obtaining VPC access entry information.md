---
title: "Obtaining VPC access entry information"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Obtain_VPC_access_point_information"
---

This topic describes how to use Terraform to obtain VPC access entry information.

## Prerequisites

You have completed the preparations for using Terraform in CR. For operation details, see [Preparations](https://docs.byteplus.com/en/docs/cr/Preparation?lang=en).

## Procedure

1. Log in to the terminal where Terraform is installed.

2. Create a folder and a configuration file named `main.tf` in it.

   ```java
   variable "common" {
     type = object({
       registry  = string
       region    = string
     })
     default = {
     #  Instance name
       registry  = "****"
     #  Instance region
       region    = "cn-guangzhou"
     }
   }
   provider "volcengine" {
     #  Access key
     access_key = "AKLT****" 
     #  Secret key
     secret_key = "WmpW****"  
     region = var.common.region
   }
   
   data "volcengine_cr_vpc_endpoints" "status_null" {
     registry    = var.common.registry
     output_file = "status_null"
   }
   
   data "volcengine_cr_vpc_endpoints" "status_one" {
     registry    = var.common.registry
     statuses    = ["Enabled"]
     output_file = "status_one"
   }
   
   data "volcengine_cr_vpc_endpoints" "status_two" {
     registry    = var.common.registry
     statuses    = ["Enabled", "Enabling"]
     output_file = "status_two"
   }
   
   data "volcengine_cr_vpc_endpoints" "status_all" {
     registry    = var.common.registry
     statuses    = ["Enabled", "Enabling", "Disabling", "Failed"]
     output_file = "status_all"
   }
   ```

3. Initialize the Terraform environment.

   ```bash
   terraform init
   ```

4. Perform resource planning.

   ```bash
   terraform plan
   ```

5. Obtain VPC access entry information.

   ```bash
   terraform apply -auto-approve
   ```

## Results

After completion, you can view the target VPC access address information in the `status_all` file.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a11b3a236aa2d5c8e200eeaee13d21bb.png)
