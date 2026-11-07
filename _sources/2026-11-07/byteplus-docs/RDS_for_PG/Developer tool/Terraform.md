---
title: "Terraform"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/terraform"
---

<span id=".5YWz5LqOIFRlcnJhZm9ybQ=="></span>
## About Terraform

Terraform is an open\-source IT infrastructure orchestration tool that enables you to define infrastructures and applications using configuration files. With Terraform, you can easily orchestrate BytePlus RDS for PostgreSQL resources, including creating, managing, maintaining, and version controlling them.

<span id=".5Lqn5ZOB6K6h6LS5"></span>
## Product billing

Terraform is currently available for free.

<span id=".VGVycmFmb3JtIOaUr-aMgeeahOWKn-iDvQ=="></span>
## Functions supported by Terraform

The following table lists the functions and corresponding resources that Terraform provides for RDS for PostgreSQL.


|Feature |User guide |
|---|---|
|Create instance, delete instance, modify the instance name, change the instance configuration (scale or change node specifications, excluding adding or deleting read\-only nodes), modify instance parameters, bind or remove tags for the instance. |Refer to [volcengine_rds_postgresql_instance](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_instance). |
|Add or remove read\-only nodes for a specified instance. |Refer to [volcengine_rds_postgresql_instance_readonly_node](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_instance_readonly_node). |
|Create or delete databases for a specified instance. |Refer to [volcengine_rds_postgresql_database](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_database). |
|Create account, delete account, modify account privileges, or reset account password for the specified instance. |Refer to [volcengine_rds_postgresql_account](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_account). |
|Create, delete, or modify the owner of a schema for the specified instance. |Refer to [volcengine_rds_postgresql_schema](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_schema). |
|Query the account information of the specified instance. |Refer to [volcengine_rds_postgresql_accounts](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_postgresql_accounts). |
|Query the database information of a specified instance. |Refer to [volcengine_rds_postgresql_databases](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_postgresql_databases). |
|Query the list of instances or the details of the specified instance. |Refer to [volcengine_rds_postgresql_instances](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_postgresql_instances). |
|Query the schema information of the specified instance. |Refer to [volcengine_rds_postgresql_schemas](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_postgresql_schemas). |
|Create an allowlist, delete an allowlist. |Refer to [volcengine_rds_postgresql_allowlist](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_allowlist). |
|Associate or disassociate an allowlist for the specified instance. |Refer to [volcengine_rds_postgresql_allowlist_associate](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_postgresql_allowlist_associate). |
|Query allowlists. |Refer to [volcengine_rds_postgresql_allowlists](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_postgresql_allowlists). |


<span id=".5a6J6KOFIFRlcnJhZm9ybQ=="></span>
## Install Terraform

Using Terraform to orchestrate resources of the cloud database PostgreSQL edition requires installing Terraform and Provider volcengine version 0.0.139 or later.


* For more information about installing Terraform, refer to [Installing Terraform](https://docs.byteplus.com/en/docs/tf/Installing-Terraform).

* For more information about installing Provider volcengine, refer to [Installing Provider volcengine](https://docs.byteplus.com/en/docs/tf/Installing-Terraform).


<span id=".5L2_55SoIFRlcnJhZm9ybQ=="></span>
## Use Terraform

For more information about using Terraform, refer to [Using Terraform](https://docs.byteplus.com/en/docs/tf/Terraform-Tool-Guide).

<span id=".5L2_55So56S65L6L"></span>
### Examples


* Create a PostgreSQL instance with the specification shown in the table below. The code is as follows:

   
   |Instance attibutes |Configuration value |
   |---|---|
   |Instance name |acc\-test\-1 |
   |Instance compatible version |PostgreSQL_12 |
   |Instance specification |rds.postgres.1c2g |
   |Storage space |40 |
   |Virtual private cloud |acc\-test\-project1 |
   |Subnet |acc\-subnet\-test\-2 |
   |Billing method |PostPaid |
   |Project |default |
   |Tag |The tag key is tagkey and the tag value is tagvalue. |
   |Instance parameters |Set two parameters for the instance:<br><br><br>* Set the parameter `auto_explain.log_analyze` to `off`.<br><br>* Set the parameter `auto_explain.log_format` to `text`. |
   

   ```json
   data "volcengine_zones" "foo" {
   }
   
   resource "volcengine_vpc" "foo" {
     vpc_name   = "acc-test-project1"
     cidr_block = "172.16.0.0/16"
   }
   
   resource "volcengine_subnet" "foo" {
     subnet_name = "acc-subnet-test-2"
     cidr_block  = "172.16.0.0/24"
     zone_id     = data.volcengine_zones.foo.zones[0].id
     vpc_id      = volcengine_vpc.foo.id
   }
   
   
   resource "volcengine_rds_postgresql_instance" "foo" {
     db_engine_version = "PostgreSQL_12"
     node_spec         = "rds.postgres.1c2g"
     primary_zone_id   = data.volcengine_zones.foo.zones[0].id
     secondary_zone_id = data.volcengine_zones.foo.zones[0].id
     storage_space     = 40
     subnet_id         = volcengine_subnet.foo.id
     instance_name     = "acc-test-1"
     charge_info {
       charge_type = "PostPaid"
     }
     project_name = "default"
     tags {
       key   = "tagkey"
       value = "tagvalue"
     }
     parameters {
       name  = "auto_explain.log_analyze"
       value = "off"
     }
     parameters {
       name  = "auto_explain.log_format"
       value = "text"
     }
   }
   ```
   

* Create a high\-privilege account Account_super and a normal account Account_normal for the instance postgres\-95472335\*\*\*\*, with passwords 93c@\*\*\*\*\*!ab12 and 9wc@\*\*\*\*\*b12 respectively, and grant the normal account Account_normal the permissions of `Inherit`, `Login`, and `CreateDB`. The code is as follows: The code is as follows:

   ```json
   resource "volcengine_rds_postgresql_account" "foo" {
     account_name     = "Account_super"
     account_password = "93c@*****!ab12"
     account_type     = "Super"
     instance_id      = "postgres-95472335****"
   }
   
   resource "volcengine_rds_postgresql_account" "foo1" {
     account_name       = "Account_normal"
     account_password   = "9wc@****b12"
     account_type       = "Normal"
     instance_id        = "postgres-95472335****"
     account_privileges = "Inherit,Login,CreateDB"
   }
   ```
