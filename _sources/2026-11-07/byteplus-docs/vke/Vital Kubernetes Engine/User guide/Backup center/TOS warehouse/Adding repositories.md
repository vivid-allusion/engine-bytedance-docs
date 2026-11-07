---
title: "Adding repositories"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Add_warehouse"
---

VKE supports adding  TOS buckets to the backup center as warehouses. This topic describes how to add a warehouse.

<span id="SU6ljfGU"></span>
## Usage limits

Currently, only BytePlus TOS can be added as a warehouse.

<span id="0u1haTge"></span>
## Prerequisites

A BytePlus TOS bucket has already been created, and the relevant TOS connection and bucket information has been obtained.

<span id="vR87YZzz"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, choose **Backup center \> TOS warehouse** to enter the TOS warehouse page.

3. Click **Add warehouse** and specify warehouse\-related parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Warehouse type |Select the type of warehouse. You can select **BytePlus TOS**. |
   |Warehouse name |Specify a name for the warehouse. |
   |Region ID |Select the region where the target TOS bucket resides. |
   |Bucket name |Select the target TOS bucket. If no TOS bucket is available, click **Create TOS bucket** to create one. |
   |Bucket subdirectory |Enter a bucket subdirectory that meets your requirements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The subdirectory cannot contain "restores" or "backups", and cannot begin or end with the forward slash (/).</div><br> |
   |Access Key ID |Set the access key ID for accessing TOS. It must match the existing bucket name. Otherwise, the connection will fail. |
   |Secret Access Key |Set the secret access key for accessing TOS. It must match the existing bucket name. Otherwise, the connection will fail. |
   

4. After the repository is configured, the system will automatically check whether the TOS warehouse can be accessed as expected.

   * If the connection to the TOS warehouse fails, check the storage configuration.

   * If nothing is wrong, click **Confirm** to complete the configuration.
