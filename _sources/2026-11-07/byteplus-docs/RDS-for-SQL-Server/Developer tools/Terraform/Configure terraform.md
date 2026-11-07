---
title: "Configure terraform"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/configure-terraform"
---

This article describes the steps to configure Terraform.

<span id="prerequisite"></span>
## prerequisite


* Terraform is installed. For details, see Installing Terraform.

* Acquired AK/SK. For details, please refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).


<span id="operation-steps"></span>
## Operation steps


1. Create a text file named `main.tf` in any directory.

2. Edit `main.tf` file:

   1. Set the Provider information and add the following:

      The version information can be obtained from the [Terraform](https://registry.terraform.io/providers/volcengine/volcengine/latest) website.

      ```plain
      terraform { 
        required_providers { 
          volcengine = { 
            source = "volcengine/volcengine" 
            version = "0.0.138" 
          } 
        } 
      }
      ```
      

   2. Add access credential information. You can set access credential information in two ways:

      * Method 1: **Static credentials (Static credentials)** , that is, add AK/SK information in the Terraform configuration file, if you use the role\-playing mode of the account, you can also add SessionToken, add the following content:

         ```plain
         provider "volcengine" { 
           access_key = "AK**************" 
           secret_key = "****************" 
           region = "cn-beijing" 
         }
         ```
         

      * Method 2: **environment variables (Environment variables)** . You can add the following information to environment variables for authentication:

         ```plain
         export VOLCENGINE_ACCESS_KEY=AK************** 
         export VOLCENGINE_SECRET_KEY=**************** 
         export VOLCENGINE_REGION=cn-beijing
         ```
