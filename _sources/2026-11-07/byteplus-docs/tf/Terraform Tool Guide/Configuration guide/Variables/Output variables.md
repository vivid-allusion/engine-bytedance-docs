---
title: "Output variables"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Output-variables"
---

An output variable is a return value of a module for offering information. You can declare output variables using the keyword "output."

<span id=".5aOw5piO6L6T5Ye65Y-Y6YeP"></span>
## Declaring output variables

According to Terraform conventions, output variables are usually declared in the `variables.tf` file. Example settings:

```Plain Text
output "ecs_private_address" {
  value       = byteplus_ecs_instance.foo.network_interfaces[0].primary_ip_address
  description = "The private IP address of ECS"
}
```



* The name of the output variable:

   After the keyword "output" is the name of the output variable, and this name must be a valid identifier.

* Arguments in an output block:

   * value: the output variable value, which is required. You can use any valid expressions.

   * description: the output variable description.

   * sensitive: the mark for specifying whether to hide the value of the output variable. Example: Example settings:

      ```Plain Text
      output "vpc_id" {
          value       = byteplus_vpc.foo.id
          description = "Check out ID of byteplus VPC."
          sensitive   = true
      }
      ```
      

   * depends_on: Specifies the dependency relationship of output variables. But output variables are just a method of converting data, and generally do not need to set dependencies with other resources or data.


<span id=".5p-l55yL6L6T5Ye65Y-Y6YeP"></span>
## Viewing output variables

Run the `terraform apply` or `terraform output` command to view output variables. Alternatively, assign the values of the child module to the parent module.

For hidden variables, view them in the following ways:


* Output variable values are stored in the `state` file. You can view them if you have permission to access the `state` file.

* If the output variable values of a child module are called by the parent module, you can view the values by outputting them or referencing the resources through the parent module.
