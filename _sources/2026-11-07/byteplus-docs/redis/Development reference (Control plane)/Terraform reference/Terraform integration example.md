---
title: "Terraform integration example"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/terraform_integration_example"
---

This topic takes creating Redis instances through Terraform as an example to introduce how to install and use Terraform.

## Precautions

* The root account of BytePlus has all permissions for resources. Once it is leaked, you will face significant risks. It is recommended that you use IAM user and create a separate AK/SK for this IAM user to use Redis\-related resources. For detailed steps, see [Create sub-user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) and [Managing access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* Authorize IAM user with permissions related to Redis cloud services, such as RedisFullAccess (full management permissions for Redis in cache database), VPCFullAccess (full management permissions for Virtual Private Cloud (VPC), etc. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).

* Some resources included in the examples in this article incur certain fees (such as the cost of creating a new Redis instance). When you no longer need to manage resources through Terraform, release the resources in a timely manner using [terraform destroy](https://docs.byteplus.com/en/docs/tf/Basic-commands) command.

## Procedure

### Step 1: Install Terraform and configure environment variables

1. You can download and install the required version from the Terraform website. For specific procedures, refer to [Terraform official documentation](https://www.terraform.io/downloads).

   > **tip**

   > Ensure that the installed Terraform version is not lower than v0.13. You can check the version information by running the `terraform version` command after successful installation.

2. Under the file directory of the Terraform project, create a configuration file named main.tf and configure the information of the Provider (service provider) in the file, including the source and version of the Provider.

   > **tip**

   > You can get the `version` information from the [Terraform\-BytePlus](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest) pages. For more information about the Provider, refer to [Providers](https://docs.byteplus.com/en/docs/tf/Provider).

   ```Plain Text
   terraform {
     required_providers {
       byteplus = {
         source = "byteplus-sdk/byteplus"
         version = "0.0.22"
       }
     }
   }
   
   provider "byteplus" {
     enable_standard_endpoint = true
     standard_endpoint_suffix = "byteplusapi.com.cn"
   }
   ```

3. Execute the following command in the command line to create environment variables to store authentication information.

   Temporary environment variables configured using the export command are only valid for the current session. The configured environment variables will be lost after the session exits. If you need to retain environment variables permanently, you can configure the export command in the startup configuration file of the corresponding operating system.

   ```Bash
   export BYTEPLUS_ACCESS_KEY="AK************"
   export BYTEPLUS_SECRET_KEY="************"
   export BYTEPLUS_REGION="cn-beijing"
   ```

   The parameter descriptions are shown in the following table.

   |Parameters |Description |
   |---|---|
   |`BYTEPLUS_ACCESS_KEY` |The AccessKey ID (AK) of your BytePlus account. For specific procedures, refer to [Managing access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
   |`BYTEPLUS_SECRET_KEY` |Secret Access Key (SK) for your BytePlus account. For specific procedures, refer to [Managing access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
   |`BYTEPLUS_REGION` |Regions where Redis resources need to be used. For more details about the regions where Cache for Redis is available, refer to [Service endpoints](https://docs.byteplus.com/en/docs/redis/request-structure). |

### Step 2: Write template

Enter the file directory of the Terraform project and open the main.tf file created in step 1 to edit, append the following content to the file to create a Redis instance with the following configuration:

* Database version number: 5.0.

* Available memory: 8 GiB (i.e. 8192 MiB).

* Number of shards: 2.

* Number of nodes in each shard: 3.

* Use multi\-availability\-zone deployment in the China (Beijing) region, where the primary node is deployed in availability zone A, and the two secondary nodes are both in availability zone B.

* Associate `department:game` and `owner:Mary` two tags.

The code example is as follows.

> **tip**

> For the configuration details of the resource type used in the code below, refer to [byteplus_redis_instance](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/redis_instance).

```Bash
# query available zones in current region
data "byteplus_zones" "foo" {
}

# create vpc
resource "byteplus_vpc" "foo" {
  vpc_name     = "tf-test-vpc-mary"
  cidr_block   = "172.16.0.0/16"
  dns_servers  = ["114.114.114.114", "8.8.8.8"]
  project_name = "default"
}

# create subnet
resource "byteplus_subnet" "foo" {
  subnet_name = "tf-test-subnet-mary"
  cidr_block  = "172.16.0.0/24"
  zone_id     = data.byteplus_zones.foo.zones[0].id
  vpc_id      = byteplus_vpc.foo.id
}

# create redis instance
resource "byteplus_redis_instance" "foo" {
  instance_name       = "tf-test-redis-mary"
  sharded_cluster     = 1
  password            = "Test@pWd"
  node_number         = 3
  shard_capacity      = 8192
  shard_number        = 2
  engine_version      = "5.0"
  subnet_id           = byteplus_subnet.foo.id
  deletion_protection = "disabled"
  charge_type         = "PostPaid"
  port                = 6391
  project_name        = "default"
  tags {
    key   = "department"
    value = "game"
  }
  tags {
    key   = "owner"
    value = "Mary"
  }
  multi_az = "enabled"
  configure_nodes {
    az = "cn-beijing-a"
  }
  configure_nodes {
    az = "cn-beijing-c"
  }
  configure_nodes {
    az = "cn-beijing-c"
  }
}
```

### Step 3: Run template

1. In the directory where the main.tf file is located, execute the following command to initialize and load the module.

   ```Bash
   terraform init
   ```

   Examples of expected back results are as follows.

   ```Bash
   Initializing the backend...
   Initializing provider plugins...
   - Finding byteplus-sdk/byteplus versions matching "0.0.22"...
   - Installing byteplus-sdk/byteplus v0.0.22...
   - Installed byteplus-sdk/byteplus v0.0.22 (self-signed, key ID ****)
   Partner and community providers are signed by their developers.
   ......
   
   Terraform has been successfully initialized!
   
   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure. All Terraform commands
   should now work.
   
   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```

2. Execute the following command to verify that the template syntax is correct.

   ```Bash
   terraform validate
   ```

   Examples of expected back results are as follows.

   ```Bash
   Success! The configuration is valid.
   ```

3. Execute the following command to create an execution plan.

   ```Bash
   terraform plan
   ```

   Examples of expected back results are as follows.

   ```Bash
   data.byteplus_zones.foo: Reading...
   data.byteplus_zones.foo: Read complete after 1s [id=****]
   
   Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
     + create
   
   Terraform will perform the following actions:
   
     # byteplus_redis_instance.foo will be created
     + resource "byteplus_redis_instance" "foo" {
         + additional_bandwidth  = (known after apply)
         + addr_type             = (known after apply)
         + backup_active         = (known after apply)
         + backup_hour           = (known after apply)
         + backup_period         = (known after apply)
         + backup_point_name     = (known after apply)
         + charge_type           = "PostPaid"
         + create_backup         = false
         + deletion_protection   = "disabled"
         + engine_version        = "5.0"
         + id                    = (known after apply)
         + instance_name         = "tf-test-redis-mary"
         + max_connections       = (known after apply)
         + multi_az              = "enabled"
         + new_address_prefix    = (known after apply)
         + new_port              = (known after apply)
         + node_number           = 3
         + password              = (sensitive value)
         + port                  = 6391
         + project_name          = "default"
         + shard_capacity        = 8192
         + shard_number          = 2
         + sharded_cluster       = 1
         + subnet_id             = (known after apply)
         + time_scope            = (known after apply)
         + upgrade_region_domain = (known after apply)
         + vpc_auth_mode         = "close"
   
         + configure_nodes {
             + az = "ap-southeast-1a"
           }
         + configure_nodes {
             + az = "ap-southeast-1c"
           }
         + configure_nodes {
             + az = "ap-southeast-1c"
           }
   
         + tags {
             + key   = "department"
             + value = "game"
           }
         + tags {
             + key   = "owner"
             + value = "Mary"
           }
       }
   
     # byteplus_subnet.foo will be created
     + resource "byteplus_subnet" "foo" {
         + cidr_block      = "172.16.0.0/24"
         + creation_time   = (known after apply)
         + enable_ipv6     = (known after apply)
         + id              = (known after apply)
         + ipv6_cidr_block = (known after apply)
         + status          = (known after apply)
         + subnet_name     = "tf-test-subnet-mary"
         + vpc_id          = (known after apply)
         + zone_id         = "ap-southeast-1a"
       }
   
     # byteplus_vpc.foo will be created
     + resource "byteplus_vpc" "foo" {
         + account_id            = (known after apply)
         + associate_cens        = (known after apply)
         + auxiliary_cidr_blocks = (known after apply)
         + cidr_block            = "172.16.0.0/16"
         + creation_time         = (known after apply)
         + dns_servers           = [
             + "8.8.8.8",
           ]
         + enable_ipv6           = (known after apply)
         + id                    = (known after apply)
         + ipv6_cidr_block       = (known after apply)
         + nat_gateway_ids       = (known after apply)
         + project_name          = "default"
         + route_table_ids       = (known after apply)
         + security_group_ids    = (known after apply)
         + status                = (known after apply)
         + subnet_ids            = (known after apply)
         + update_time           = (known after apply)
         + vpc_id                = (known after apply)
         + vpc_name              = "tf-test-vpc-mary"
       }
   
   Plan: 3 to add, 0 to change, 0 to destroy.
   
   ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   
   Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
   ```

4. Execute the following command to deploy the template.

   ```Bash
   terraform apply
   ```

   Some examples of back results are as follows.

   ```Bash
   Plan: 3 to add, 0 to change, 0 to destroy.
   
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.
   
     Enter a value: 
   ```

   At this point, you need to enter `yes` to change resources.

   An example of the result of back after entering `yes` is as follows.

   ```Bash
   byteplus_vpc.foo: Creating...
   byteplus_vpc.foo: Creation complete after 4s [id=vpc-q6m5vtvmywao1ntgts3x****]
   byteplus_subnet.foo: Creating...
   byteplus_subnet.foo: Creation complete after 4s [id=subnet-q6m5x96fwbnk1ntgtrl6****]
   byteplus_redis_instance.foo: Creating...
   byteplus_redis_instance.foo: Still creating... [00m10s elapsed]
   ...
   byteplus_redis_instance.foo: Still creating... [02m50s elapsed]
   byteplus_redis_instance.foo: Creation complete after 2m52s [id=redis-mlrf55x69pfgz****]
   
   Apply complete! Resources: 3 added, 0 changed, 0 destroyed.
   ```

5. Once created, you can view the newly created instance via OpenAPI or the Redis console. For specific procedures, refer to [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) and [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

## Relevant documents

* [Terraform syntax guide](https://docs.byteplus.com/en/docs/tf/Syntax-guide)

* [Terraform configuration guide](https://docs.byteplus.com/en/docs/tf/Configuration-guide)

* [Terraform command line](https://docs.byteplus.com/en/docs/tf/Terraform-command-line)
