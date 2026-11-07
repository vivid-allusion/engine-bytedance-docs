---
title: "Provider"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Provider"
---

A Terraform configuration file ends with .tf and consists of providers, [Resources](https://docs.byteplus.com/en/docs/tf/Resource), [Data Sources](https://docs.byteplus.com/en/docs/tf/Data-Sources), and [variables](https://docs.byteplus.com/en/docs/tf/Variables).

A provider is used for specifying a service provider. You can declare a provider using the keyword "provider."

<span id=".5oyH5a6a5rqQ5ZKM54mI5pys"></span>
## Specifying a source and a version

For Terraform 0.13 or later, you can use required_providers to specify the source and version of providers. Example:

```Plain Text
terraform {
  required_providers {
    byteplus = {
      source = "byteplus/byteplus"
      version = "1.0.0"
    }
  }
  required_version = ">= 0.13"
}
```


<span id=".5Yib5bu6UHJvdmlkZXLlnZc="></span>
## Creating provider blocks

You can use provider blocks to create multiple configurations. The default block is unique and uses the identifier "provider" while non\-default blocks use the identifier "alias." To manage resources in different Regions, you must declare multiple provider blocks. The following example demonstrates how to declare the BytePlus providers of the China (Beijing) (cn\-beijing) and China (Shanghai) (cn\-nantong) Regions and how to add an alias for the provider of the China (Shanghai) Region:

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


<span id=".6YCJ5oupUHJvdmlkZXLlnZc="></span>
## Selecting a provider block

When you select a non\-default block, the format is <provider name\>.<alias\>. As shown in the following example, the selected provider is `byteplus.ntcc`:

```Plain Text
resource "byteplus_vpc" "foo" {
  provider = byteplus.ntcc
  vpc_name = "tf-test-2"
  cidr_block = "172.16.0.0/16"
```
