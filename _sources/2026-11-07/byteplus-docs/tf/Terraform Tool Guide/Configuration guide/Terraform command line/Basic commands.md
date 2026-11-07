---
title: "Basic commands"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Basic-commands"
---

<span id="terraform init"></span>
## terraform init

Used for initializing working directories, including loading provider, backend, and module blocks. You can run this command repetitively in the same working directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Running <code>terraform init -upgrade=true</code> command updates providers and modules.</div>


```Plain Text
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of byteplus/byteplus...
- Installing byteplus/byteplus v1.0.0...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgardes to new major versions that may contain breaking
changes, we recommend adding version constraints in a required_providers block
in your configuration, with the constraint strings suggested below.

* byteplus/byteplus: version = "~> 1.0.0"

Terraform has been successfully initialized!
```


<span id="terraform plan"></span>
## terraform plan

Used for creating preparatory plans. Before running the `terraform apply` command, you must run this command to preview the pending changes and verify whether they are as expected. That is, whether the attributes of the cloud resources differ from those in the state file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, this command first updates resource attributes from the remote. When there are many resources, the operation may take a long time. You can execute <code>terraform plan -refresh=false</code> to disable updates.</div>


If Terraform detects differences, it outputs the differences:

```Plain Text
$ terraform plan
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or state storage.
...
Plan: 1 to add, 0 to change, 1 to destroy.
...
```


If Terraform does not detect any differences, it outputs the following information:

```Plain Text
$ terraform plan
...
No changes. Infrastructure is up-to-date.

This means that Terraform did not detect ant differences between your
configuration and real physical resources that exist. As a result, no
actions need to be performed.
```


<span id="terraform apply"></span>
## terraform apply

Used for creating or modifying resources. Before executing actions, a human\-computer interaction is required to confirm resource creation and modification. You can run `terraform apply -auto-approve` to skip human\-computer interaction and directly execute.

```Plain Text
$ terraform apply
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
Terraform will perform the following action:
...
Plan: 1 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.
  Enter a value:
```


This command saves its running result to the terraform.tfstate file and displays the output variables of resources. Example:

```Plain Text
Apply complete! Resources: 1 to add, 0 to change, 1 to destroy.

Outputs:

vpc_id = vpc-12323204
```


<span id="terraform destroy"></span>
## terraform destroy

Used for deleting resources. Before executing actions, a human\-computer interaction is required to confirm resource deletion. You can run `terraform destroy -auto-approve` to skip human\-computer interaction and directly delete resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, the <code>terraform destroy</code> command deletes all resources in the current module. Proceed with caution.</div>


```Plain Text
$ terraform destroy -auto-approve
...
Destroy complete! Resources: 1 destroyed.
```


To delete a specific resource, use the following format: \-target=<RESOURCE_TYPE\>.<RESOURCE_NAME\>.

```Plain Text
$ terraform destroy -target=byteplus_subnet.foo
An execution plan has been generated and is show below.
Resource actions are indicated with the following symbols:
  - destroy
Terraform will perform the following actions:
  # byteplus_subnet.foo will be destroyed
  - resource "byteplus_subnet" "foo" {
    ...
  }
Plan: 0 to add, 0 to change, 1 to destroy.
...
Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.
  Enter a value:
```


<span id="terraform refresh"></span>
## terraform refresh

Used for refreshing the configurations of the `state` file. After you run this command, it calls the remote API to obtain the latest data and writes the results to the `state` file.

<span id="terraform show"></span>
## terraform show

Used for displaying all managed resources and their attribute values in the `state` file.

<span id="terraform output"></span>
## terraform output

Used for displaying the output variables in the current configuration. This command outputs the output variables defined in the configuration one by one. The format is OUTPUT_VARIABLE_NAME = OUTPUT_VARIABLE_VALUE.
