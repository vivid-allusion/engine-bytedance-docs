---
title: "Metadata"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Metadata"
---

Metadata is built\-in meta\-arguments in Terraform that can be used in [Provider](https://docs.byteplus.com/en/docs/tf/Provider), [Resource](https://docs.byteplus.com/en/docs/tf/Resource), and [Data Sources](https://docs.byteplus.com/en/docs/tf/Data-Sources) blocks.

This topic introduces meta\-arguments supported by resource blocks, including their functions.


* depends_on: specifies the dependencies of a resource.

* count: creates multiple resources with identical configurations.

* for_each: creates multiple resources based on maps and string sets.

* provider: selects non\-default providers.

* lifecycle: customizes the lifecycle of a resource.


<span id="depends_on"></span>
## depends_on

A Terraform configuration file may contain multiple resources. The dependency relationships between resources can be automatically inferred through the resource reference logic. A Terraform configuration file may contain multiple resources. The dependency relationships between resources can be automatically inferred through the resource reference logic. However, for invisible resource dependency relationships, you must use depends_on to create explicit dependencies. The depends_on meta\-argument can change the order of resource creation or execution, ensuring that a resource is processed after the resources it depends on.

The depends_on expression is a list of dependency resource addresses. The following example demonstrates how to create a virtual private cloud (VPC), subnet, and security group in series while ensuring the security group is created after the subnet:

```Plain Text
resource "byteplus_vpc" "vpc" {
  ...
}
#The subnet is created in series after the VPC.
resource "byteplus_subnet" "subnet" {
  vpc_id = byteplus_vpc.id
  ...
}
#The security group is created after the subnet. If you do not use depends_on, the subnet and the security group are created in parallel.
resource "byteplus_security_group" "sg" {
  depends_on = [byteplus_subnet.subnet]
  vpc_id = byteplus_vpc.id
  ...
}
```


<span id="count"></span>
## count

By default, you can configure up to one [Resource](https://docs.byteplus.com/en/docs/tf/Resource) in a resource block. If you use multiple independent resource blocks to create identical resources, the code becomes redundant and hard to maintain. In this case, you can use the count or for_each meta\-argument to manage multiple identical resources in one resource block.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot use both count and for_each in the same resource block.</div>



* <div data-tips="true" data-tips-type="tip">If the arguments of the resources are mostly or entirely identical, we recommend that you use the count argument.</div>


* <div data-tips="true" data-tips-type="tip">If the arguments of the resources require different values that cannot be derived from integers, we recommend that you use the for_each argument.</div>



The following example demonstrates how to create three volumes with identical configurations:

```Plain Text
resource "byteplus_volume" "foo" {
  count = 3

  volume_name = "terraform-test"
  zone_id = "cn-beijing-a"
  volume_type = "PTSSD"
  kind = "data"
  size = 40
}
```


If you have a uniqueness requirement for certain resource arguments, you can use the `count.index` attribute for differentiation, starting the count from 0. Assume there are two VPCs created, named tf_vpc_0 and tf_vpc_1, example settings:

```Plain Text
resource "byteplus_vpc" "vpcs" {
  count = 2
  vpc_name  = "tf_vpc_${count.index}"
  cidr_block  = "172.20.0.0/16"
}
```


Based on the above example, if you want to assign different masks to different VPCs, you can declare a string list to store VPC mask values and use `count.index` to access list elements. Example settings:

```Plain Text
variable "name_list" {
  type    = list(string)
  default = ["tf_vpc_test1", "tf_vpc_test2"]
}
variable "cidr_list" {
  type    = list(string)
  default = ["172.20.0.0/16", "172.21.0.0/16"]
}

resource "byteplus_vpc" "vpcs" {
  count = 2
  vpc_name  = var.name_list[count.index]
  cidr_block  = var.cidr_list[count.index]
}
```


When accessing resources created by count, the index value needs to be used, with the format: <Resource Type\>.<Name\>[index value]. Example settings:

```Plain Text
# Access the first VPC.
> byteplus_vpc.vpcs[0]

# Access the ID of the first VPC.
> byteplus_vpc.vpcs[0].id

# Access the IDs of all VPCs.
> byteplus_vpc.vpcs[*].id
```


<span id="for_each"></span>
## for_each

The for_each and count meta\-arguments are similar. The difference is that for_each maps values to corresponding attributes in the format of key\-value pairs or string sets.


* Key\-value pairs: Use `each.key` and `each.value` to access keys and values.

   For example, when creating VPCs, the key\-value pairs in `for_each` allow flexible configuration of VPC names and masks.

   ```Plain Text
   resource "byteplus_vpc" "vpc" {
     for_each = {
       tf_vpc_test1 = "172.20.0.0/16"
       tf_vpc_test2 = "172.21.0.0/16"
     }
   
     vpc_name = each.key
     cidr_block = each.value
   }
   ```
   

* String set: `each.key` is equivalent to `each.value`. Use `each.key` for uniformity. Additionally, you can use `toset()` to convert a defined list:

   ```Plain Text
   # to_set list => set
   resource "byteplus_security_group" "sg" {
     for_each = toset(["tf_sg_test1", "tf_sg_test2"])
     name     = each.key
   }
   
   # Define for_each through a variable.
   variable "sg_name" {
     type = set(string)
   }
   resource "byteplus_security_group" "sg" {
     for_each = var.sg_name
     name     = each.key
   }
   ```
   


When you access resources created by for_each, the format is <RESOURCE_TYPE\>.<NAME\>.[KEY_NAME]. Example: Example settings:

```Plain Text
# Access tf_vpc_test1.
> byteplus_vpc.vpcs["tf_vpc_test1"]

# Access the ID of tf_vpc_test1.
> byteplus_vpc.vpcs["tf_vpc_test1"].id
```


<span id="provider"></span>
## provider

You can use the provider block to create multiple configurations. The default block is unique and identified by "provider", while other non\-default blocks are identified by "alias". To manage resources in different Regions, you must declare multiple provider blocks. The following example demonstrates how to declare the BytePlus providers of the China (Beijing) (cn\-beijing) and China (Shanghai) (cn\-nantong) Regions and how to add an alias for the provider of the China (Shanghai) Region:

```Plain Text
provider "byteplus" {
  region = "cn-beijing"
  ...
}

provider "byteplus" {
  alias  = "ntcc"
  region = "cn-nantong"
  ...
}
```


When selecting a non\-default block, the format is <PROVIDER_NAME\>.<ALIAS\>. As shown below, the selected provider is byteplus.ntcc:

```Plain Text
resource "byteplus_vpc" "foo" {
  provider = byteplus.ntcc
  vpc_name = "tf-test-2"
  cidr_block = "172.16.0.0/16"
```


<span id="lifecycle"></span>
## lifecycle

Every resource instance experiences three stages throughout its lifecycle: creation, updating, and deletion. The lifecycle meta\-argument can change resource lifecycle processes and supports the following arguments:


* create_before_destroy

   By default, when updating an unchangeable resource argument, Terraform deletes the existing instance before creating a new instance based on the newly configured argument for replacement. If you set the create_before_destroy argument to `true`, Terraform creates a new instance before deleting the existing instance to avoid business disruption. Example settings:

   ```Plain Text
   lifecycle {
     create_before_destroy = true
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you use create_before_destroy, the new and old instances exist at the same time. Learn about whether a resource instance name must be unique or has other limits in advance.   </div>
   

* prevent_destroy

   If you want to prevent resource deletion actions, you can set the prevent_destroy argument to `true` to prevent accidental operations. If you want to delete this resource normally, simply remove the prevent_destroy argument and then perform the delete action.

   ```Plain Text
   lifecycle {
     prevent_destroy = true
   }
   ```
   

* ignore_changes

   By default, when executing the `terraform plan/apply` command, differences between cloud resource attributes and local resource blocks are automatically detected, and any inconsistencies will be updated or rebuilt to match the configuration. If you do not want automatic detection, you can use ignore_changes to ignore certain arguments.

   The value of ignore_changes can be a relative address list of attributes, and for Map and List types, the index notation can also be used, For example, tags["Name"], list[0].

   * When ignoring one or more arguments, you need to specify the argument name. The example is as follows, indicating to ignore `instance_name`:

      ```Plain Text
      resource "byteplus_ecs_instance" "foo" {
        ...
        lifecycle {
          ignore_changes = [
            instance_name,
          ]
        }
      }
      ```
      

   * If you need to ignore all arguments, you can use the keyword `all`, as shown in the example below:

      ```Plain Text
      resource "byteplus_ecs_instance" "foo" {
        ...
        lifecycle {
          ignore_changes = all
        }
      }
      ```
