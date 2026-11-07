---
title: "Install Terraform"
product: "Terraform"
product_code: "tf"
section: "Document"
source: "https://docs.byteplus.com/en/docs/tf/Installing-Terraform"
---

This article introduces the installation configuration of Terraform and uses the creation of a Virtual Private Cloud (VPC) as an example to explain how to use Terraform.

<span id=".5q2l6aqk5LiA77ya5a6J6KOFVGVycmFmb3Jt"></span>
## Step 1: Install Terraform

Terraform is released as an executable binary file. You can download Terraform and add the directory of the Terraform executable file to the system environment variable PATH.


1. Log on to the [Terraform official website](https://www.terraform.io/downloads.html) or go to the [download page](https://releases.hashicorp.com/terraform/) to download an installation package corresponding to your operating system. It is recommended to use version 0.13.x or later.

2. Uncompress the installation package, then add the directory of the Terraform executable file to the system environment variable PATH.

3. Run the following command in the command line to verify whether the configuration path is correct

   `terraform`

   If the following output is displayed, it indicates that the configuration is correct and Terraform can run properly.

   ```Plain Text
   Usage: terraform [-version] [-help] <command> [args]
   
   ....
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yid5aeL5YyW5L2_55So546v5aKD"></span>
## Step 2: Initialize the environment that you want to use


1. Terraform allows you to orchestrate multiple cloud resources listed in [Supported Cloud Services](https://docs.byteplus.com/en/docs/tf/Supported-cloud-services). Before using Terraform to manage cloud resources, you must obtain the AccessKey ID and AccessKey secret.

4. Create a text file named `main.tf` in any directory you want.

5. Edit the `main.tf` file to set provider information. To obtain the `version`, go to the [Terraform official website](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs). The content to add is as follows:

   ```Plain Text
   terraform {
     required_providers {
       byteplus = {
         source = "byteplus-sdk/byteplus"
         version = "0.0.129"
       }
     }
   }
   ```
   

4. Edit the `main.tf` file to add access credentials. You can set access credentials in the following two ways:

   1. Method 1: using **static credentials**. Add an AccessKey ID and AccessKey secret to the Terraform configuration file. If you use the role assumption mode of your account, you can also add SessionToken. The content to add is as follows:

      ```Plain Text
      provider "byteplus" {
        access_key = "AK**************"
        secret_key = "****************"
        region = "cn-beijing"
        
      }
      ```
      

      * access_key: **required**. It specifies the AccessKey ID. 

      * secret_key: **required**, it specifies the AccessKey secret, that is, SK. 

      * region: **required**, it specifies the zone where you can create and manage resources. You can [click here](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones) to query the supported zones.

      * session_token: **optional**. It specifies the security token for role assumption. 

   2. Method 2: **using environment variables.**  Add the following information to environment variables for authentication and authorization:

      ```Plain Text
      export BYTEPLUS_ACCESS_KEY=AK**************
      export BYTEPLUS_SECRET_KEY=****************
      export BYTEPLUS_REGION=cn-beijing
      ```
      

      * BYTEPLUS_ACCESS_KEY: **required**, specifies the Key ID, that is, AK. 

      * BYTEPLUS_SECRET_KEY: **required**. It specifies the access key (AK), that is the SK. 

      * BYTEPLUS_REGION: **required**. It specifies the region where you need to create and manage resources. You can [click here](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones) to query the regions supported.

      * BYTEPLUS_SESSION_TOKEN: **optional**. It specifies the security token for role assumption. 


<span id=".5q2l6aqk5LiJ77ya5L2_55SoVGVycmFmb3Jt5Yib5bu654Gr5bGx5byV5pOOVlBD"></span>
## Step 3: Use Terraform to create a Virtual Private Cloud (VPC)

The following example demonstrates how to use Terraform to create a Virtual Private Cloud (VPC).


1. Edit [the environment that you want to use](https://docs.byteplus.com/en/docs/tf/Installing-Terraform#.5q2l6aqk5LqM77ya5Yid5aeL5YyW5L2_55So546v5aKD) in Step 2 and complete the `main.tf` file. Add the following information to configure the provider and create a Virtual Private Cloud (VPC). The content to add is as follows:

   ```Plain Text
   #Create vpc
   resource "byteplus_vpc" "this" {
     vpc_name = "tf-test-1"
     cidr_block = "172.16.0.0/16"
   }
   ```
   

2. Navigate to the directory where `main.tf` is located and execute the following command to initialize.

   `terraform init`

   The output is as follows. Please note that when you run it for the first time, the provider will be downloaded and installed.

   ```Plain Text
   Initializing the backend...
   
   Initializing provider plugins...
   
   Terraform has been successfully initialized!
   
   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure.  All Terraform commands
   should now work.
   
   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```
   

3. Execute the following command to <view\> the execution plan.

   `terraform plan`

   The output is as follows, showing the resources to be created.

   ```Plain Text
   An execution plan has been generated and is shown below.
   Resource actions are indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # bytelus_vpc.foo will be created
     + resource "byteplus_vpc" "foo" {
         + account_id            = (known after apply)
         + associate_cens        = (known after apply)
         + auxiliary_cidr_blocks = (known after apply)
         + cidr_block            = "172.16.0.0/16"
         + creation_time         = (known after apply)
         + id                    = (known after apply)
         + nat_gateway_ids       = (known after apply)
         + route_table_ids       = (known after apply)
         + security_group_ids    = (known after apply)
         + status                = (known after apply)
         + subnet_ids            = (known after apply)
         + update_time           = (known after apply)
         + vpc_id                = (known after apply)
         + vpc_name              = "tf-test-2"
       }
   
   Plan: 1 to add, 0 to change, 0 to destroy.
   
   ------------------------------------------------------------------------
   
   Note: You didn't specify an "-out" parameter to save this plan, so Terraform
   can't guarantee that exactly these actions will be performed if
   "terraform apply" is subsequently run.
   ```
   

4. Execute the following command to create resources.

   `terraform apply`

   Enter `yes` as prompted. As shown in the output, a VPC named terraform_vpc has been created. You can also log in to the Virtual Private Cloud console to view whether the resource has been created.

   ```Plain Text
   An execution plan has been generated and is shown below.
   Resource actions are indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # byteplus_vpc.foo will be created
     + resource "byteplus_vpc" "foo" {
         + account_id            = (known after apply)
         + associate_cens        = (known after apply)
         + auxiliary_cidr_blocks = (known after apply)
         + cidr_block            = "172.16.0.0/16"
         + creation_time         = (known after apply)
         + id                    = (known after apply)
         + nat_gateway_ids       = (known after apply)
         + route_table_ids       = (known after apply)
         + security_group_ids    = (known after apply)
         + status                = (known after apply)
         + subnet_ids            = (known after apply)
         + update_time           = (known after apply)
         + vpc_id                = (known after apply)
         + vpc_name              = "tf-test-2"
       }
   
   Plan: 1 to add, 0 to change, 0 to destroy.
   
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value: yes
   
   byteplus_vpc_vpc.foo: Creating...
   byteplus_vpc_vpc.foo: Creation complete after 2s [id=vpc-13f4ryf7v2cxs3n6nu5ho4l2u]
   
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```
