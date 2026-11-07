---
title: "Creating an RDS for MySQL instance with Terraform"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_terraform"
---

The process of using Terraform revolves around the `main.tf` file, and you can manage and orchestrate resources by appending content to the `main.tf` file. This article describes the procedure for creating an RDS for MySQL instance with Terraform.

<span id="前提条件"></span>
## Required

You have installed Terraform by referring to [Install Terraform](https://www.volcengine.com/docs/6313/424647).

<span id="操作步骤"></span>
## Procedure


1. Create a folder and a configuration file named `main.tf` in the folder.

   ```python
   data "volcengine_zones" "foo" {
   }
   
   resource "volcengine_vpc" "foo" {
     vpc_name   = "vpc-test"
     cidr_block = "172.16.0.0/16"
   }
   
   resource "volcengine_subnet" "foo" {
     subnet_name = "subnet-test"
     cidr_block  = "172.16.0.0/24"
     zone_id     = data.volcengine_zones.foo.zones[0].id
     vpc_id      = volcengine_vpc.foo.id
   }
   
   resource "volcengine_rds_mysql_instance" "foo" {
     db_engine_version      = "MySQL_5_7"
     node_spec              = "rds.mysql.1c2g"
     primary_zone_id        = data.volcengine_zones.foo.zones[0].id
     secondary_zone_id      = data.volcengine_zones.foo.zones[0].id
     storage_space          = 80
     subnet_id              = volcengine_subnet.foo.id
     instance_name          = "mysql-test"
     lower_case_table_names = "1"
   
     charge_info {
       charge_type = "PostPaid"
     }
   
     parameters {
       parameter_name  = "auto_increment_increment"
       parameter_value = "2"
     }
     parameters {
       parameter_name  = "auto_increment_offset"
       parameter_value = "5"
     }
   
     project_name = "default"
     tags {
       key   = "k1"
       value = "v1"
     }
   }
   ```
   

2. Initialize the Terraform running environment.

   ```bash
   terraform init
   ```
   

3. The expected output is as follows.

   ```sql
   Initializing the backend...
   Initializing provider plugins...
   - Finding latest version of hashicorp/volcengine...
   - Installing hashicorp/volcengine v0.0.1...
   - Installed hashicorp/volcengine v0.0.1 (unauthenticated)
   Terraform has created a lock file .terraform.lock.hcl to record the provider
   selections it made above. Include this file in your version control repository
   so that Terraform can guarantee to make the same selections by default when
   you run "terraform init" in the future.
   
   ....
   
   Terraform has been successfully initialized!
   
   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure. All Terraform commands
   should now work.
   
   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```
   

4. Create a resource plan.

   ```bash
   terraform plan
   ```
   

5. The expected execution result is as follows.

   ```markdown
   data.volcengine_zones.foo: Reading...
   data.volcengine_zones.foo: Read complete after 0s [id=1581253418]
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # volcengine_rds_mysql_instance.foo will be created
     + resource "volcengine_rds_mysql_instance" "foo" {
         + allow_list_ids              = (known after apply)
         + allow_list_version          = (known after apply)
         + backup_use                  = (known after apply)
         + binlog_dump                 = (known after apply)
         + charge_detail               = (known after apply)
         + connection_pool_type        = (known after apply)
         + create_time                 = (known after apply)
         + data_sync_mode              = (known after apply)
         + db_engine_version           = "MySQL_5_7"
         + db_proxy_status             = (known after apply)
         + db_time_zone                = (known after apply)
         + endpoints                   = (known after apply)
         + feature_states              = (known after apply)
         + global_read_only            = (known after apply)
         + id                          = (known after apply)
         + instance_id                 = (known after apply)
         + instance_name               = "mysql-test"
         + instance_status             = (known after apply)
         + lower_case_table_names      = "1"
         + memory                      = (known after apply)
         + node_cpu_used_percentage    = (known after apply)
         + node_memory_used_percentage = (known after apply)
         + node_number                 = (known after apply)
         + node_space_used_percentage  = (known after apply)
         + node_spec                   = "rds.mysql.1c2g"
         + nodes                       = (known after apply)
         + primary_zone_id             = "cn-nanjing-bbit-a"
         + project_name                = "default"
         + region_id                   = (known after apply)
         + secondary_zone_id           = "cn-nanjing-bbit-a"
         + storage_space               = 80
         + storage_type                = (known after apply)
         + storage_use                 = (known after apply)
         + subnet_id                   = (known after apply)
         + time_zone                   = (known after apply)
         + update_time                 = (known after apply)
         + v_cpu                       = (known after apply)
         + vpc_id                      = (known after apply)
         + zone_id                     = (known after apply)
         + zone_ids                    = (known after apply)
   
         + charge_info {
             + auto_renew  = (known after apply)
             + charge_type = "PostPaid"
             + period      = (known after apply)
             + period_unit = (known after apply)
           }
   
         + maintenance_window (known after apply)
   
         + parameters {
             + parameter_name  = "auto_increment_increment"
             + parameter_value = "2"
           }
         + parameters {
             + parameter_name  = "auto_increment_offset"
             + parameter_value = "5"
           }
   
         + tags {
             + key   = "k1"
             + value = "v1"
           }
       }
   
     # volcengine_subnet.foo will be created
     + resource "volcengine_subnet" "foo" {
         + cidr_block      = "172.16.0.0/24"
         + creation_time   = (known after apply)
         + enable_ipv6     = (known after apply)
         + id              = (known after apply)
         + ipv6_cidr_block = (known after apply)
         + status          = (known after apply)
         + subnet_name     = "subnet-test"
         + vpc_id          = (known after apply)
         + zone_id         = "cn-nanjing-bbit-a"
       }
   
     # volcengine_vpc.foo will be created
     + resource "volcengine_vpc" "foo" {
         + account_id            = (known after apply)
         + associate_cens        = (known after apply)
         + auxiliary_cidr_blocks = (known after apply)
         + cidr_block            = "172.16.0.0/16"
         + creation_time         = (known after apply)
         + enable_ipv6           = (known after apply)
         + id                    = (known after apply)
         + ipv6_cidr_block       = (known after apply)
         + nat_gateway_ids       = (known after apply)
         + project_name          = (known after apply)
         + route_table_ids       = (known after apply)
         + security_group_ids    = (known after apply)
         + status                = (known after apply)
         + subnet_ids            = (known after apply)
         + update_time           = (known after apply)
         + vpc_id                = (known after apply)
         + vpc_name              = "vpc-test"
       }
   
   Plan: 3 to add, 0 to change, 0 to destroy.
   ```
   

6. Create instance

   ```sql
   terraform apply
   ```
   

7. The expected execution result is as follows.

   ```sql
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   ...
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value: yes
   
   volcengine_vpc.foo: Creating...
   volcengine_vpc.foo: Creation complete after 2s [id=vpc-1mvxn32380dtsj63v3yfw33z]
   volcengine_subnet.foo: Creating...
   volcengine_subnet.foo: Creation complete after 2s [id=subnet-24mnjbs2fdvy84acvz77vfbeb]
   volcengine_rds_mysql_instance.foo: Creating...
   ...
   Apply complete! Resources: 3 added, 0 changed, 0 destroyed.
   ```
