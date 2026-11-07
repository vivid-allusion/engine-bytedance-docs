---
title: "Using Terraform"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/using_terraform"
---

The Terraform process is centered on the `main.tf` file, and the management and orchestration of resources are realized by adding corresponding content to the `main.tf` file. This topic gives an example of creating an RDS for MySQL instance.

<span id="procedure"></span>
## Procedure


1. Here we use creating an RDS for MySQL instance as an example. The following content is added to the file `main.tf`, and you must modify the parameter content, where my\-instance\-0 represents the resource name.

   ```xml
   resource "volcengine_rds_instance_v2" "my-instance-0" {
     db_engine_version = "MySQL_5_7"
     instance_type     = "HA"
     node_info {
       node_type = "Primary"
       node_spec = "rds.mysql.1c2g"
       zone_id   = "cn-beijing-a"
     }
     node_info {
       node_type = "Secondary"
       node_spec = "rds.mysql.1c2g"
       zone_id   = "cn-beijing-a"
     }
     storage_type           = "LocalSSD"
     storage_space          = 100
     vpc_id                 = "vpc-xxx"
     subnet_id              = "subnet-xxx"
     charge_info {
       charge_type = "PostPaid"
     }
   }
   ```
   

2. Enter the directory where `main.tf` is located, and run the following command at the endpoint to view the execution plan. After execution of `terraform plan`, the relevant information of the instance to be created is displayed in the endpoint, as shown below.

   ```bash
   # volcengine_rds_instance_v2.my-instance-0 will be created
   + resource "volcengine_rds_instance_v2" "my-instance-0" {
       + connection_info   = (known after apply)
       + db_engine_version = "MySQL_5_7"
       + id                = (known after apply)
       + instance_type     = "HA"
       + storage_space     = 100
       + storage_type      = "LocalSSD"
       + subnet_id         = "subnet-rrzzs6dzof0gv0x58bh****"
       + vpc_id            = "vpc-13g2qkkzntfy83n6nu4z1****"
   
       + charge_info {
           + auto_renew  = (known after apply)
           + charge_type = "PostPaid"
           + period      = (known after apply)
           + period_unit = (known after apply)
         }
   
       + node_info {
           + node_id   = (known after apply)
           + node_spec = "rds.mysql.1c2g"
           + node_type = "Primary"
           + zone_id   = "cn-beijing-a"
         }
       + node_info {
           + node_id   = (known after apply)
           + node_spec = "rds.mysql.1c2g"
           + node_type = "Secondary"
           + zone_id   = "cn-beijing-a"
         }
     }
   
   Plan: 1 to add, 0 to change, 1 to destroy.
   ```
   

3. Run the following command to apply the execution plan.

   ```plain
   terraform apply
   ```
   

   After execution, a confirmation message is displayed in the endpoint. Enter 'Yes' to confirm execution, or enter other content to cancel the execution plan.

   ```plain
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value:
   ```
   

   Enter 'Yes' to start the execution plan. After execution, the following prompt message appears in the endpoint.

   ```shell
   $ terraform apply
   
   ...
   
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value: yes
     
   ...
     
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```
   


<span id="relevant-documents"></span>
## Relevant documents


* 

*
