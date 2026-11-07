---
title: "Obtaining temporary keys for logging into instances"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Obtain_a_temporary_key_for_a_login_instance"
---

This topic describes how to use Terraform to create a temporary key for a CR Standard Edition instance. After obtaining the temporary key, you can log in to the instance and push or pull images into the instance.

> **tip**

> Temporary keys are valid for one hour. If a key expires, execute the key creation command again to create a new one.

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
           registry  = "enterprise-1" 
           # Instance region
           region    = "cn-guangzhou" 
         }
       }
       
       provider "volcengine" {
         # Access key
         access_key = "AKAPO****" 
         # Secret key
         secret_key = "WXpre****'" 
         region = var.common.region
       }
       
       # Query token
       data "volcengine_cr_authorization_tokens" "label" {
         registry    = var.common.registry
         output_file = "token"
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

5. Create the temporary key.

   ```bash
   terraform apply -auto-approve
   ```

6. In the current directory, view the temporary key for logging in to the CR Standard Edition instance.

   ```bash
   cat token
   ```

## What to do next

After obtaining the temporary key, you can log in to the instance and push or pull images in it. For detailed steps, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images-in-an-enterprise-instance).
