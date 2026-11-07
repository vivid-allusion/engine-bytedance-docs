---
title: "Input variable"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Input-variables"
---

An input variable is an input argument of a module. You can declare input variables using the keyword "variable." After declaring input variables, you can modify configurations without changing the source code.

<span id=".5aOw5piO6L6T5YWl5Y-Y6YeP"></span>
## Declaring input variables

For Terraform, input variables are declared in `variables.tf` file. Example settings:

```Plain Text
variable "vpc_id" {
  type        = string
  description = "id of vpc"
}

variable "zone_id" {
  type    = string
  default = "cn-beijing-a"
}
```



* Name of the input variable:

   After the keyword "variable," the input variable’s name must be unique among all variables in the same module. The name of the variable can be any valid identifier except reserved keywords, which include:

   ```Plain Text
   source    version    providers    count    for_each    lifecycle    depends_on    locals
   ```
   

* Arguments in a variable block:

   * type: the variable type, which defaults to string. For more information on other variable types, refer to [Argument types](https://docs.byteplus.com/en/docs/tf/Basic-syntax#参数类型).

      The following example demonstrates how to declare variables of complex types:

      ```Plain Text
      variable "security_group_ids" {
        type    = list(string)
        default = ["sg-13f5gejti0pvk3n6nu503****"]
      }
      
      variable "volumes" {
        type = list(object({
          volume_type = string
          size = number
          delete_with_instance = bool
        }))
        default = [{
          volume_type = PTSSD
          size = 50
          delete_with_instance = true
        }]
      }
      ```
      

   * description: the variable description.

   * default: the default variable value. Variables with a default value are optional.

   * validation: a block used for specifying custom validation rules for the variable. This is available only in Terraform 0.13.0 or later. Example:

      ```Plain Text
      variable "ecs_instance_password" {
          type        = string
          description = "The password for ecs user to log in."
      
          validation {
            condition     = length(var.ecs_instance_password)>=8
            error_message = "The password is too short."
          }
      }
      ```
      

      `condition` is a boolean expression. You can use the `can` function to detect whether the expression reports an error. Example:

      ```Plain Text
      variable "ecs_instance_name" {
          type        = string
          description = "This name of ecs instance."
      
          validation {
      # If regex(...) fails, error_message is returned. An error message must start with an uppercase letter and end with a period ( . ) or question mark ( ? ).
            condition     = can(regex("([a-zA-Z])", var.ecs_instance_name))
            error_message = "Incorrect instance name. Please check whether it contains upper and lower case letters."
          }
      }
      ```
      


<span id=".5byV55So6L6T5YWl5Y-Y6YeP"></span>
## Referencing input variables

When referencing input variables, the format is: var.<variable name\>, only supported within the module that declares the variable. Example settings:

```Plain Text
# Define a variable in variables.tf file.
variable "vpc_cidr" {
  type        = string
  description = "the CIDR of VPC"
}

# Use the variable in main.tf file.
resource "byteplus_vpc" "foo" {
    vpc_name = "my_vpc"
    cidr_block = var.vpc_cidr
}
```


<span id=".6K6-572u6L6T5YWl5Y-Y6YeP"></span>
## Setting input variables

You can set input variables in the following three ways.

<span id=".6YCa6L-HLXZhcuiuvue9rg=="></span>
### Setting input variables using `-var`

Add `-var` in the "terraform plan" or "terraform apply" command line. You can use `-var` in the command more than once. Example:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Do not leave any spaces between the variable name and the equal sign.</div>


```Plain Text
terraform apply -var='vpc_cidr=172.20.0.0/16'
terraform apply -var='vpc_name=my_vpc' -var='vpc_cidr=172.20.0.0/16'
terraform apply -var='dns_servers = ["8.8.8.8","114.114.114.114"]'
```


<span id=".6YCa6L-H5Y-Y6YeP5a6a5LmJ5paH5Lu2KC50ZnZhcnMp6K6-572u"></span>
### Setting input variables using a variable defining file (.tfvars)

If you use many variables in your configuration, set their names and values in a variable defining file, then use `-var-file` to specify the file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To improve readability and avoid character escaping issues, we recommend that you use a variable defining file to set variables of complex types.</div>


Example settings:

```Plain Text
terraform apply -var-file="test.tfvars"
```


The example of a variable defining file is as follows:

```Plain Text
vpc_name = "my_vpc"
vpc_cidr = "172.20.0.0/16"
dns_servers = [
    "8.8.8.8",
    "114.114.114.114",
]
```


Terraform automatically loads variable defining files with specific names. Example:


* Files whose name is `terraform.tfvars` or `terraform.tfvars.json`

* Files whose name ends with `.auto.tfvars` or `.auto.tfvars.json`

   For files whose name ends with `.json`, you must use JSON objects. Example:

   ```Plain Text
   {
       "vpc_name": "my_vpc"
       "dns_servers": ["8.8.8.8", "114.114.114.114"]
   }
   ```
   


<span id=".6YCa6L-H546v5aKD5Y-Y6YeP6K6-572u"></span>
### Setting input variables using environment variables

Use environment variables prefixed with "TF_VAR_" to set input variables. This can be useful when running Terraform in automation, or when running a sequence of Terraform commands in succession with the same variables.

```Plain Text
$ export TF_VAR_vpc_name=my_vpc
$ export TF_VAR_dns_servers='["8.8.8.8", "114.114.114.114"]'
$ terraform plan
...
```


<span id=".5Y-Y6YeP5LyY5YWI57qn"></span>
### Variable priorities

You can freely combine the three methods of setting variables as needed. When a conflict occurs, the following rules are applied:


* If you set multiple values for a variable, Terraform uses the last value.

* Terraform loads variables in the following order of priorities, from the highest priority to the lowest priority:

   1. `-var`, `-var-file`

   2. `*.auto.tfvars` and `*.auto.tfvars.json` files

   3. `terraform.tfvars` and `terraform.tfvars.json` files

   4. environment variables
