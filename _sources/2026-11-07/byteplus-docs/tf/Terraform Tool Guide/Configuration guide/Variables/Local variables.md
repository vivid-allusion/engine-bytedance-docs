---
title: "Local variables"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Local-variables"
---

A local variable is a temporary variable in a module. Local variables are used in scenarios where the same value or expression is repetitively defined in the configuration. They help reduce code redundancy and are easy to modify. Local variables are confined to the module where they are declared. You can declare a local variable using the keyword "local." Local variables are confined to the module where they are declared. You can declare a local variable using the keyword "local."

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use local variables appropriately. Excessive use of local variables makes the code difficult to understand and maintain because numerous actual variable values are hidden.</div>


<span id=".5aOw5piO5pys5Zyw5Y-Y6YeP"></span>
## Declaring local variables

For Terraform, output variables are declared in the `variables.tf` file. Example: Example settings:

```Plain Text
locals {
  vpc_name = "tf-test-vpc"
}
```


In addition to setting local variables to character and number constants, you can also use input variables, resource attributes, or references and expression results of other local variables:

```Plain Text
locals {
  dns_servers = concat(byteplus_vpc.foo1.dns_servers, byteplus_vpc.foo2.dns_servers)
}

locals {
  common_names = {
    name = local.vpc_name
  }
}
```


<span id=".5byV55So5pys5Zyw5Y-Y6YeP"></span>
## Referencing local variables

When referencing local variables, the format is: local.<variable name\>. Example settings:

```Plain Text
resource "byteplus_vpc" "foo" {
  ...
  vpc_name = local.vpc_name
  dns_servers = local.dns_servers
}
```
