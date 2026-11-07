---
title: "Backend"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Backend"
---

After you create or modify a resource through Terraform, the resource state and attributes are stored in the `terraform.tfstate` file in the current directory. This file is a map where Terraform stores resource attributes. You can run the `terraform show` command to read the file and view the resource state and attributes.

After you run the `terraform plan/apply` command, Terraform verifies whether the pending changes are consistent with the `terraform.tfstate` file. If the `tfstate` file is corrupted or deleted, Terraform deems that the resources managed by the file are modified or removed and rebuilds the resources according to the pending changes. In this case, if the actual resources still exist, resources are created repetitively or unsuccessfully. If the actual resource still exists at this time, it will cause duplicate create or create of the resource to fail.

When different teams maintain the same set of resources, multiple copies of the resource configuration file and the` tfstate` file are required. This increases code maintenance costs.

A backend is an element that Terraform uses to achieve remote storage. It allows you to store the `tfstate` file in a remote service such as AWS S3, HashiCorp Consul, and etcd. This separates code management from file management and increases management flexibility. To use backends, you must declare nested backend blocks and specify tags of specific backend types. Backend is implemented by declaring backend nested blocks and specifying different [Backend Type](https://developer.hashicorp.com/terraform/language/backend) tags.

<span id=".5L2_55SoUzMgQmFja2VuZA=="></span>
## Using an S3 backend

Torch Object Storage (TOS) provides an interface compatible with AWS S3, and the S3 backend supports custom endpoints. You can use the S3 backend to store the `tfstate` file in a TOS bucket.

The procedure is as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In this mode, you must use the S3 domain name of TOS in the format of <code>https://tos-s3-${region}.bytepluses.com</code>. For example, <code>https://tos-s3-ap-southeast-1.bytepluses.com</code>.</div>


* <div data-tips="true" data-tips-type="tip">Terraform has made changes to the relevant arguments of the backend since version 1.6.x. The following examples will give the argument configuration of the new version and the old version before 1.5.x, respectively.</div>


1. Declare a nested backend block in the terraform block.

   ```Plain Text
   terraform {
       required_version = "< 1.6.0"
       
   backend "s3" {
   bucket   = "backend-test" #The bucket name.
   key      = "backend-test/terraform.tfstate" #The object name.
   region   = "cn-beijing" #The Region where the bucket resides.
   endpoint = "https://tos-s3-ap-southeast-1.bytepluses.com" # The S3 domain name of TOS.
   
   skip_region_validation      = true
   skip_metadata_api_check     = true
   skip_credentials_validation = true
     }
   }
   
   terraform {
   required_version = ">= 0.13"
   
   backend "s3" {
   bucket   = "backend-test" #The bucket name.
   key      = "backend-test/terraform.tfstate" #The object name.
   region   = "cn-beijing" #The Region where the bucket resides.
       endpoints = {
   endpoint = "https://tos-s3-ap-southeast-1.bytepluses.com" # The S3 domain name of TOS.
       }
   
   skip_region_validation      = true
   skip_metadata_api_check     = true
   skip_credentials_validation = true
       skip_requesting_account_id  = true
       skip_s3_checksum            = true
     }
   }
   ```
   

2. Define the following environment variables: AccessKey ID and AccessKey secret.

   ```Plain Text
   $ export AWS_ACCESS_KEY_ID="******"
   $ export AWS_SECRET_ACCESS_KEY="******"
   ```
   

3. Run the `terraform init` command.

   ```Plain Text
   terraform init
   2022/04/13 12:18:02 [WARN] Log levels other than TRACE are currently unreliable, and are supported only for backward compatibility.
   Use TF_LOG=TRACE to see Terraform's internal logs.
    ----
   
   Initializing the backend...
   
   Initializing provider plugins...
   
   Terraform has been successfully initialized!
   
   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure.  All Terraform commands
   should now work.
   
   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the working directory has been initialized and the backend configuration has been changed, you need to re\-execute the init command and add the relevant argument:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">terraform init \-reconfigure re \- configures the backend and ignores any existing state files.    </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Terraform init \-migrate\-state re \- configures the backend and attempts to automatically migrate the existing state files.   </div>
