---
title: "Install terraform"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/install-terraform"
---

This article describes how to install Terraform.

<span id="download-terraform"></span>
## Download Terraform

Terraform is published as a binary executable, you simply download Terraform and add the Terraform executable directory to the system environment variables PATH.


1. Log in to [Terraform official website](https://www.terraform.io/downloads.html) or enter the [download page](https://releases.hashicorp.com/terraform/), it is recommended to use 0.13.x or higher version to download the installation package of the corresponding operating system.

2. Unzip the installation package and add the terraform executable directory to the system environment variables PATH.

3. Execute the following command to verify that the configuration path is correct:

   ```json
   terraform
   ```
   

   Expected output:

   ```plain
   Usage: terraform [-version] [-help] <command> [args] 
   ....
   ```
