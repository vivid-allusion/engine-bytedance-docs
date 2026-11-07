---
title: "Command line overview"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Command-line-overview"
---

This topic introduces some common Terraform commands. You can run the `terraform` command to view the full command list or run the `terraform -h` or `terraform --help` command to obtain all usages. Example: As shown in the following figure:

```Plain Text
$ terraform
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.
...

$ terraform init -h
Usage: terraform init [options] [DIR]

  Initialize a new or existing Terraform working directory by creating
  initial files, loading any remote state, downloading modules, etc.

  This is the first command that should be run for any new or existing
  Terraform configuration per machine. This sets up all the local data
  necessary to run Terraform that is typically not committed to version
  control.
...
```
