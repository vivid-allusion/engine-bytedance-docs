---
title: "Use terraform"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/use-terraform"
---

The process of using Terraform is carried out around the `main.tf` file, and the management and arrangement of resources are realized by appending the corresponding content in the `main.tf` file. This article illustrates creating a RDS for SQL Server instance as an example.

<span id="use-example"></span>
## use example


1. To create a RDS for SQL Server instance, for example, append the following content to the `main.tf` file, the parameter content needs to be modified by yourself, where `my-instance-0` represents the resource name.

   ```bash
   resource "volcengine_rds_mssql_instance" "my-instance-0" { 
    
     db_engine_version = "SQLServer_2019_Std" 
     instance_type = "HA" 
     subnet_id = ["subnet-****"] 
     node_spec = "rds.mssql.se.ha.d4.4c16g" 
     storage_space = 100 
     super_account_password = "Test@****" 
     instance_name = "Na****" 
     
     charge_info { 
       charge_type="PostPaid" 
     } 
   }
   ```
   

2. Go to the directory where the `main.tf` is located and execute the following command at the end point to view the execution plan. After the `terraform plan` is executed, information about the instance to be created is displayed in the end point, as shown below.

   ```bash
   # [volcengine_rds_mssql_instance.my](http://volcengine_rds_mssql_instance.my)-instance-0 will be created 
   + resource "volcengine_rds_mssql_instance" "my-instance-0" { 
       + db_engine_version      = "SQLServer_2019_Std" 
       + id                     = (known after apply) 
       + instance_name          = "Na****" 
       + instance_type          = "HA" 
       + node_spec              = "rds.mssql.se.ha.d4.4c16g" 
       + project_name           = (known after apply) 
       + storage_space          = 100 
       + subnet_id              = [ 
           + "subnet-****", 
         ] 
       + super_account_password = (sensitive value) 
   
       + charge_info { 
           + auto_renew           = (known after apply) 
           + charge_end_time      = (known after apply) 
           + charge_start_time    = (known after apply) 
           + charge_status        = (known after apply) 
           + charge_type          = "PostPaid" 
           + overdue_reclaim_time = (known after apply) 
           + overdue_time         = (known after apply) 
           + period               = (known after apply) 
         } 
     } 
   
   Plan: 1 to add, 0 to change, 0 to destroy.
   ```
   

3. Execute the following command to execute the app plan.

   ```json
   terraform apply
   ```
   

   After execution, a confirmation message is displayed in the end point. If execution is confirmed, enter yes; enter something else to cancel the execution plan.

   ```plain
   Do you want to perform these actions? 
     Terraform will perform the actions described above. 
     Only 'yes' will be accepted to approve. 
     Enter a value:
   ```
   

   After entering yes, the execution plan starts. After execution, the end point will have the following prompt message.

   ```plain
   $ terraform apply 
   ... 
   Do you want to perform these actions? 
     Terraform will perform the actions described above. 
     Only 'yes' will be accepted to approve. 
     Enter a value: yes 
   
   ... 
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```
