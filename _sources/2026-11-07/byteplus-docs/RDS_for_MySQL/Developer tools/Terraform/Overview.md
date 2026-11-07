---
title: "Overview"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_terraform"
---

This article describes the resources that you can manage and use for RDS for MySQL with Terraform.

<span id="关于-terraform"></span>
## About Terraform

Terraform is an open\-source IT infrastructure automation and orchestration tool that allows you to efficiently configure and manage cloud infrastructure resources. Volcengine provides developer tools based on the open\-source Terraform to help you securely and efficiently preview, configure, and manage your cloud infrastructure and resources. For more information, refer to [Terraform](https://www.volcengine.com/docs/tf/What-is-Terraform).

<span id="terraform-的优势"></span>
## Advantages of Terraform


* Infrastructure as code: use an advanced configuration syntax to describe and codify your infrastructure. By controlling the versions of resources defined in Terraform, your cloud resources become controllable, manageable, and traceable.

* Automated infrastructure management: Terraform configuration templates support planning and automatic execution. They also save the state of your infrastructure resources, preventing the complexity and errors associated with manual operations.

* Reduced handover costs: use Terraform to facilitate the handover of O&M tasks, reducing issues such as information loss and wasted cloud resources that can occur during handovers.


<span id="云数据库-mysql-版支持通过-terraform-管理的资源"></span>
## RDS for MySQL resources managed by Terraform

MySQL supports managing the following Resources and Data Sources with Terraform.


* Resources

   
   |Resource |description |
   |---|---|
   |[volcengine_rds_mysql_instance](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_instance) |Create instance, delete instance, modify instance name, modify instance configuration (scale an instance or change the node specification, excluding adding or deleting read\-only nodes), modify instance parameter, and bind or remove tags for an instance. |
   |[volcengine_rds_mysql_database](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_database) |Manage the databases for a specified instance. |
   |[volcengine_rds_mysql_account](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_account) |Manage accounts for a specified instance, such as creating an account, deleting an account, modifying account permissions, or resetting an account password. |
   |[volcengine_rds_mysql_allowlist](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_allowlist) |Manage allowlists for MySQL, such as creating and deleting allowlists. |
   |[volcengine_rds_mysql_allowlist_associate](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_allowlist_associate) |Associate or disassociate an allowlist for an instance. |
   |[volcengine_rds_mysql_backup](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_backup) |Manage backups for a specified instance. |
   |[volcengine_rds_mysql_backup_policy](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_backup_policy) |Manage the backup policy for a specified instance. |
   |[volcengine_rds_mysql_endpoint](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_endpoint) |Manages the connection endpoint of a specified instance. |
   |[volcengine_rds_mysql_endpoint_public_address](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_endpoint_public_address) |Enable or disable public network access for a specified connection endpoint of an instance. |
   |[volcengine_rds_mysql_instance_readonly_node](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_instance_readonly_node) |Add or delete a read\-only node for a specified instance. |
   |[volcengine_rds_mysql_parameter_template](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/resources/rds_mysql_parameter_template) |Manage parameter templates for MySQL. |
   

* Data Source

   
   |Resource |description |
   |---|---|
   |[volcengine_rds_mysql_accounts](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_accounts) |Query account information for a specified instance. |
   |[volcengine_rds_mysql_allowlists](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_allowlists) |Retrieve the list of allowlists or the allowlists for a specified instance. |
   |[volcengine_rds_mysql_backups](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_backups) |Queries the backup list of a specified instance. |
   |[volcengine_rds_mysql_databases](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_databases) |Query the list of databases for a specified instance or the detailed information for a specified database. |
   |[volcengine_rds_mysql_endpoints](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_endpoints) |View the endpoints for a specified instance or the details of a specified connection endpoint. |
   |[volcengine_rds_mysql_instance_specs](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_instance_specs) |View the list of instance specifications for MySQL. |
   |[volcengine_rds_mysql_instances](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_instances) |View the list of instances or the details of a specified instance. |
   |[volcengine_rds_mysql_parameter_templates](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_parameter_templates) |Retrieve the list of MySQL parameter templates. |
   |[volcengine_rds_mysql_regions](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_regions) |View the list of regions that provide MySQL service. |
   |[volcengine_rds_mysql_zones](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs/data-sources/rds_mysql_zones) |Queries the list of availability zones in a specified region. |
   


For more information, refer to the official [Terraform Registry](https://registry.terraform.io/providers/volcengine/volcengine/latest/docs).
