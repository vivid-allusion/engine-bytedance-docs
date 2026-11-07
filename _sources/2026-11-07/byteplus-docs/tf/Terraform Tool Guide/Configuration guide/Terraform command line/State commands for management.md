---
title: "State commands for management"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/State-commands-for-management"
---

Terraform stores resource information such as resource state and attributes in the `terraform.tfstate` file. You can use the `terraform state` commands to manage the `state` file.

<span id="terraform state list"></span>
## terraform state list

Used for listing all resources in the `state` file. The output format is <RESOURCE_TYPE\>.<RESOURCE_NAME\>.

```Plain Text
$ terraform state list
byteplus_vpc.foo
```


<span id="terraform state show"></span>
## terraform state show

Used for displaying all attributes of a specific resource. The command format is `terraform state show <RESOURCE_TYPE>.<RESOURCE_NAME>`.

```Plain Text
$terraform state show byteplus_vpc.foo
# byteplus_vpc.foo:
resource "byteplus_vpc" "foo" {
    account_id            = "XXXXXX"
    associate_cens        = []
    auxiliary_cidr_blocks = []
    cidr_block            = "172.16.0.0/16"
    creation_time         = "2022-04-02T16:02:40+08:00"
    dns_servers           = [
        "114.114.114.114",
        "8.8.8.8",
    ]
    id                    = "vpc-mjhlf3gs61hc5smt1ajya7ct"
    nat_gateway_ids       = []
    route_table_ids       = [
        "vtb-mjhlf5fta3gg5smt1ambg5j3",
    ]
    security_group_ids    = [
        "sg-mjhlf9dvi7eo5smt1aucvf7z",
    ]
    status                = "Available"
    subnet_ids            = []
    update_time           = "2022-04-02T16:02:41+08:00"
    vpc_id                = "vpc-mjhlf3gs61hc5smt1ajya7ct"
    vpc_name              = "tf-test-2"
}
```


<span id="terraform state rm"></span>
## terraform state rm

Used for removing a specific resource from the `state` file without deleting the resource. The command format is `terraform state rm <RESOURCE_TYPE>.<RESOURCE_NAME>`.

```Plain Text
$terraform state rm byteplus_vpc.foo
Removed byteplus_vpc.foo
Successfully removed 1 resource instance(s).
```


<span id="terraform state mv"></span>
## terraform state mv

Used for changing the name of a specific resource or the path where a specific resource resides.


* Changing a resource name: The command is `terraform state mv <RESOURCE_TYPE>.<OLD_RESOURCE_NAME> <RESOURCE_TYPE>.<NEW_RESOURCE_NAME>`.

   ```Plain Text
   $terraform state mv byteplus_vpc.foo byteplus_vpc.test
   Move "byteplus_vpc.foo" to "byteplus_vpc.test"
   Successfully moved 1 object(s).
   ```
   

* Changing a resource path: You can move a resource from the `state` file to which it belongs to another `state` file while changing the resource name. The command is `terraform state mv -state-out=RELATIVE/ABSOLUTE_STATE_FILE_PATH <RESOURCE_TYPE>.<OLD_RESOURCE_NAME> <RESOURCE_TYPE>.<NEW_RESOURCE_NAME>`. Example settings:

   ```Plain Text
   $terraform state mv -state-out=../vpc/terraform.tfstate  byteplus_vpc.foo byteplus_vpc.test
   Move "byteplus_vpc.foo" to "byteplus_vpc.test"
   Successfully moved 1 object(s).
   ```
