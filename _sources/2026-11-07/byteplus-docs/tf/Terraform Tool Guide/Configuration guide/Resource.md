---
title: "Resource"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Resource"
---

A resource is an important element for Terraform. You can declare a resource using the keyword "resource."

<span id=".5YWz6IGU6LWE5rqQ"></span>
## Associating a resource

Each Cloud Service has one or more resources attached to it. For example, byteplus_ecs_instance represents an Elastic Compute Service (ECS), and byteplus_eip_address represents an Elastic IP (EIP). Using byteplus_eip_associate, you can assign an Elastic IP (EIP) to an Elastic Compute Service (ECS). Example settings:

```Plain Text
resource "byteplus_ecs_instance" "foo" {
  ...
}

resource "byteplus_eip_address" "foo" {
  ...
}

resource "byteplus_eip_associate" "foo" {
  allocation_id = byteplus_eip_address.foo.id
  instance_id = byteplus_ecs_instance.foo.id
  instance_type = "EcsInstance"
}
```


<span id=".5byV55So6LWE5rqQ"></span>
## Referencing a resource

When referencing the attribute of a resource, the format is: <Type\>.<Name\>.<attribute\>. For example, when referencing a byteplus_ecs_instance resource named "foo," the example is as follows:

```Plain Text
# The ID of the instance
> byteplus_ecs_instance.foo.id
i-mizl7m1kqccg5smt1bdp****

# The security group of the first network interface of the instance
> byteplus_ecs_instance.foo.network_interfaces[0].security_group_ids
 ["sg-13f5gejti0pvk3n6nu503****"]

# The IP address of the first network interface of the instance
> byteplus_ecs_instance.foo.network_interfaces[0].primary_ip_address
172.XX.XX.20

# The IP addresses of all network interfaces of the instance
> byteplus_ecs_instance.foo.network_interfaces[*].primary_ip_address
["172.XX.XX.20", "172.XX.XX.20"]
```
