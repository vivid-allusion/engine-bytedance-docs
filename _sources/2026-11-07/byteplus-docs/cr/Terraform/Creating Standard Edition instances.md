---
title: "Creating Standard Edition instances"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Creating_a_Standard_Edition_Instance"
---

This topic describes how to use Terraform to create a CR Standard Edition instance.

## Prerequisites

You have completed the preparations for using Terraform in CR. For operation details, see [Preparations](https://docs.byteplus.com/en/docs/cr/Preparation?lang=en).

## Procedure

1. Log in to the terminal where Terraform is installed.

2. Create a folder and a configuration file named `main.tf` in it.

   ```bash
       variable "common" {
         type = object({
           registry  = string
           region    = string
         })
         default = {
           # Instance name
           registry  = "{your_instance_name}" 
           # Instance region
           region    = "cn-guangzhou" 
         }
       }
       
       provider "volcengine" {
         # Access key
         access_key = "AKLT****" 
         # Secret key
         secret_key = "WTJG****"  
         region = var.common.region
       }
       
       resource "volcengine_cr_registry" "label" {
         name   = var.common.registry
         delete_immediately=false
         # Instance password
         password = "{your_password}"
       }
       
       output "create_registry" {
         value = volcengine_cr_registry.label
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

5. Create an instance and set the instance password.

   > **warning**

   > You need to run this command twice: once to create the instance and to set the password.

   ```bash
   terraform apply -auto-approve
   ```

## Results

After execution is complete, log in to the console to view the created instance.
