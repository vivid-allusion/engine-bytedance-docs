---
title: "Modules"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Modules"
---

A Terraform configuration file typically consists of multiple [resources](https://docs.byteplus.com/en/docs/tf/Resource), [data sources](https://docs.byteplus.com/en/docs/tf/Data-Sources), and [variables](https://docs.byteplus.com/en/docs/tf/Variables). Modules help simplify configurations and reduce maintenance complexity. You can declare a module using the keyword "module."

A module is equivalent to a Terraform module that encapsulates and abstracts multiple resources.

<span id=".6LCD55SobW9kdWxl5qih5Z2X"></span>
## Calling a module

Specify the call path in the configuration file. Example:

```Plain Text
module "child_module" {
  source = "./child"
  ...
}
```



* Module block name:

   The block name after the keyword "module." The name must be a valid identifier.

* Arguments in a module block:

   * source: the source path that contains the module configuration file. This argument is required.

      
      |Source Path Type |explain |Example Value |
      |---|---|---|
      |Local path |Must start with ./ or ../. |source = "./child"<br><br>source = "../parent" |
      |GitHub |Support using the HTTPS protocol. |source = "github.com/terraform\-xxx\-modules/terraform\-xxx\-vpc.git" |
      ||Support using the SSH protocol. |source = "git@github.com:terraform\-xxx\-modules/terraform\-xxx\-vpc.git" |
      ||Require the `ref` argument in the path to specify a branch or version. |source = "github.com/terraform\-xxx\-modules/terraform\-xxx\-vpc.git?ref=v1.0.0" |
      |Common Git repository |Must start with git::, support using the HTTPS or SSH protocol, and support specifying a branch or version. |* source = "git::ssh://username@example.com/storage.git"<br><br>* source = "git::https://example.com/vpc.git?ref=v1.2.0" |
      

   * Other arguments.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After adding a module block, you must run the <code>terraform init</code> command to save a replica of the module code to the working directory.</div>


* <div data-tips="true" data-tips-type="tip">After modifying or deleting a module block, you must run the <code>terraform init</code> command again to update corresponding configurations.</div>



<span id=".6K6_6Zeu5qih5Z2X55qE6L6T5Ye65Y-Y6YeP"></span>
## Accessing the output variables of a module

As a module block encapsulates and abstracts resources, direct access to resource attributes defined in the module block is not possible. You can only access output variables defined in a module block in the format of module.< MODULE NAME \>.< OUTPUT NAME \>.

The following uses a local source path as an example to introduce how to access the output variables of a module block:


1. In the working directory `./modules/vpc`, declare a module block, create a virtual private cloud (VPC), and output the VPC ID. For more information on declaration methods, refer to [Variables](https://docs.byteplus.com/en/docs/tf/Variables).

   ```Plain Text
   variable "cidr" {
     type    = string
     default = "172.20.0.0/16"
   }
   
   resource "byteplus_vpc" "foo" {
     name = "tf_vpc_test"
     cidr = var.cidr
   }
   
   output "vpc_id" {
     value = byteplus_vpc.foo.id
   }
   ```
   

2. In the working directory, call the module and add a subnet to the VPC. In this case, module.vpc.vpc_id is the value of `vpc_id`.

   ```Plain Text
   module "vpc" {
     source = "./modules/vpc"
   }
   
   resource "byteplus_subnet" "default" {
     subnet_name = "tf_subnet_test"
     cidr_block = "172.20.1.0/24"
     zone_id = "cn-beijing-a"
     vpc_id  = module.vpc.vpc_id
   }
   ```
