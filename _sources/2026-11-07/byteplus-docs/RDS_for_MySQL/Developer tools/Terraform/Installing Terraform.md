---
title: "Installing Terraform"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/installing_terraform"
---

This document describes how to install Terraform as a preparatory step to manage RDS for MySQL resources.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Download and install the required version from the official Terraform website. For details, refer to the [official Terraform documentation](https://www.terraform.io/downloads).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the installed Terraform version is v0.13 or later. You can view the version information with the <code>terraform version</code> command.   </div>
   

2. Configure the Volcengine Account information in Terraform.

   1. Create environment variables to store authentication information.

      ```bash
      export VOLCENGINE_ACCESS_KEY="AK************"
      export VOLCENGINE_SECRET_KEY="************"
      export VOLCENGINE_REGION="cn-beijing"
      ```
      

      The parameter description is provided in the table below.

      
      |Parameter |description |
      |---|---|
      |VOLCENGINE_ACCESS_KEY |The AccessKey ID (AK) of your Volcengine Account. To obtain it, refer to [User guide for access keys](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key). |
      |VOLCENGINE_SECRET_KEY |The Secret Access Key (SK) of your Volcengine Account. To obtain it, refer to [User guide for access keys](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key). |
      |VOLCENGINE_REGION |The Region where your MySQL business is located. For the Regions and RegionIDs supported by RDS for MySQL, refer to [Regions and availability zones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/request_structure_1#.6K-35rGC5pa55rOV). |
      

   2. Specify the authentication information in the provider section of the configuration file.

      ```bash
      provider "volcengine" {
        access_key = "AK************"
        secret_key = "************"
        session_token = "sts token"
        region = "cn-beijing"
      }
      ```
      

      The parameters are described in the following table.

      
      |Parameter |description |
      |---|---|
      |access_key |The AccessKey ID (AK) of your Volcengine Account. To obtain it, refer to [User guide for access keys](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key). |
      |secret_key |The Secret Access Key (SK) for your BytePlus Account. To obtain it, refer to [User guide for access keys](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key). |
      |session_token |Optional parameter. The security token for role assumption, which you can obtain by calling the [AssumeRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole) API. |
      |region |The Region where your MySQL service is located. Must be consistent with the VOLCENGINE_REGION Parameter Value in the previous step. |
