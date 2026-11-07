---
title: "Other commands"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Other-commands"
---

<span id="terraform validate"></span>
## terraform validate

Used for quickly detecting syntax errors in configuration files. This command eliminates the need to run the `terraform plan/apply` command to identify error locations and causes.


* If no error is detected, the output is as follows:

   ```Plain Text
   $ terraform validate
   Success! The configuration is valid.
   ```
   

* If any errors are detected, the output is as follows:

   ```Plain Text
   $ terraform validate
   Error: Missing required argument
   
     on main.tf line 1, in resource "byteplus_vpc" "foo":
      1: resource "byteplus_vpc" "foo" {
   
   The argument "cidr_block" is required, but no definition was found.
   
   
   Error: Unsupported argument
   
     on main.tf line 3, in resource "byteplus_vpc" "foo":
      3:   cidr = "172.16.0.0/16"
   
   An argument named "cidr" is not expected here. Did you mean "id"?
   ```
   


<span id="terraform fmt"></span>
## terraform fmt

Used for formatting all `.tf` files in the current directory and its subdirectories for a unified coding style.

<span id="terraform graph"></span>
## terraform graph

Used for outputting visualized dependency relationships between resources in DOT format according to configuration files and execution plans.

```Plain Text
$ terraform graph
digraph {
        compound = "true"
        newrank = "true"
        subgraph "root" {
                "[root] provider.byteplus" [label = "provider.byteplus", shape = "diamond"]
                "[root] byteplus_security_group.foo1" [label = "byteplus_security_group.foo1", shape = "box"]
                "[root] byteplus_subnet.foo1" [label = "byteplus_subnet.foo1", shape = "box"]
                "[root] byteplus_subnet.foo2" [label = "byteplus_subnet.foo2", shape = "box"]
                "[root] byteplus_vpc.foo" [label = "byteplus_vpc.foo", shape = "box"]
                "[root] meta.count-boundary (EachMode fixup)" -> "[root] byteplus_security_group.foo1"
                "[root] provider.byteplus (close)" -> "[root] byteplus_security_group.foo1"
                "[root] root" -> "[root] meta.count-boundary (EachMode fixup)"
                "[root] root" -> "[root] provider.byteplus (close)"
                "[root] byteplus_security_group.foo1" -> "[root] byteplus_subnet.foo1"
                "[root] byteplus_security_group.foo1" -> "[root] byteplus_subnet.foo2"
                "[root] byteplus_subnet.foo1" -> "[root] byteplus_vpc.foo"
                "[root] byteplus_subnet.foo2" -> "[root] byteplus_vpc.foo"
                "[root] byteplus_vpc.foo" -> "[root] provider.byteplus"
        }
}
```


You can run the `dot` command to visualize the output result into a graph:

```Plain Text
$ Install graphviz according to the operating system.
$ terraform graph | dot -Tsvg > test.svg
```


<span id="terraform import"></span>
## terraform import

Used for importing existing resources into the `state` file. The command is `terraform import <RESOURCE_TYPE>.<RESOURCE_NAME> <RESOURCE_ID>`.

```Plain Text
$ terraform import byteplus_vpc.foo vpc-mjhlf3gs61hc5smt1ajya7ct
byteplus_vpc.foo: Importing from ID "vpc-mjhlf3gs61hc5smt1ajya7ct"...
byteplus_vpc.foo: Import prepared!
  Prepared byteplus_vpc for import
byteplus_vpc.foo: Refreshing state... [id=vpc-mjhlf3gs61hc5smt1ajya7ct]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.
```


<span id="terraform taint"></span>
## terraform taint

Used for manually marking a resource as tainted. When you run the `terraform apply` command after marking the resource, Terraform deletes and rebuilds the resource. The command is terraform taint <RESOURCE_TYPE\>.<RESOURCE_NAME\>.

```Plain Text
$ terraform taint byteplus_subnet.foo
Resource instance byteplus_subnet.foo has been marked as tainted.
```


If you run the `terraform show` command after marking the resource as tainted, you can find the state of the resource becomes tainted:

```Plain Text
$ terraform show
...
# byteplus_subnet.foo: (tainted)
resource "byteplus_subnet" "foo" {
  ...
}
```


<span id="terraform untaint"></span>
## terraform untaint

Used for manually changing the state of a resource from tainted to normal. This command reverses the action of the `terraform taint` command. The command is terraform untaint `<RESOURCE_TYPE>.<RESOURCE_NAME>`.

```Plain Text
$ terraform untaint byteplus_subnet.foo
Resource instance byteplus_subnet.foo has been successfully untainted.
```


<span id="terraform console"></span>
## terraform console

Used for opening the interactive console where you can try and test expressions and built\-in functions.

```Plain Text
$ terraform console
> length("Hello,world!")
12
```
