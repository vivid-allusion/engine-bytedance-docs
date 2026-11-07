---
title: "Preparations"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Preparation"
---

This topic describes the preparations you need to complete before using Terraform to manage CR resources.

## Background

Terraform is an open\-source Infrastructure as Code (IaC) tool that supports managing cloud resources through declarative configuration files. BytePlus CR provides a Terraform Provider plugin. You can use Terraform to automatically create and manage CR instances and related resources.

## Application scenarios

* You need to create and manage CR instances in batches via code.

* You need to incorporate CR resources into IaC for unified management.

* You need to automatically create CR infrastructure within CI/CD pipelines.

## Procedure

### Step 1: Install Terraform

Install [Terraform](https://releases.hashicorp.com/terraform/) v0.12.31 or a later version. After the installation, you can run the following command to view the version information:

```Bash
terraform version
```

### Step 2: Configure the BytePlus Provider plugin

Add the terraform\-provider\-volcengine file to the `~/.terraform.d/plugins/darwin_amd64` directory and grant execute permission:

[terraform-provider-volcengine](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_152a6ab4928cd168bf3f0fb95d74a45f)

```Bash
chmod 755 ~/.terraform.d/plugins/darwin_amd64/terraform-provider-volcengine
```

### Step 3: Obtain account key and region information

You have obtained the key of your BytePlus account and the information about the region where the target instance is located.

|**Parameter** |**Description** |
|---|---|
|access_key | The AccessKey ID (AK) of your BytePlus account. For how to obtain it, see [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |
|secret_key |The Secret Access Key (SK) of your BytePlus account. For how to obtain it, see [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |
|region |The Region where your CR business is located. For example, `cn-guangzhou`. |

##
