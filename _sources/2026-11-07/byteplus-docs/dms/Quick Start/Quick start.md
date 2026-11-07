---
title: "Quick start"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Quick_start1"
---

This article introduces the prerequisites and migration process for using the Data Migration Service, helping you quickly get started with the service.

<span id="4d67e7b2"></span>
## Preconditions

Before using the Data Migration Service, please make sure you have registered a BytePlus account and completed the enterprise certification. For specific steps, please refer to [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

<span id="3ea63b32"></span>
## Usage process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dac53a2dfe7f4573a31c4217611d5a5c~tplv-goo7wpa0wc-image.image) </span>


|Steps |Explanation |
|---|---|
|1. Confirm source information |Before migrating data, you need to confirm the following information based on the source class:<br><br><br>* **source type** is **URL list**: ** ** I need to confirm the URL of the file to be migrated.<br><br>* **source type** is **object storage**: ** ** Need to confirm the data source type, AKSK, source bucket name, source region, and endpoint. |
|2. (Optional) Create destination bucket |After confirming the source information, you need to create an object storage TOS as the destination. For the creation steps, please refer to [Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket)。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to migrate data to an existing bucket, you can skip this step.</div><br> |
|3. Create migration task |After confirming the source and destination information, you can create a migration task. For detailed steps, please refer to [Create a migration task](https://docs.byteplus.com/docs/dms/Create-a-migration-task). |
|4. View migration results |After the migration task is successfully created, the data migration process will begin. For detailed steps on how to view the migration results, please refer to [View migration results](https://docs.byteplus.com/docs/dms/View-migration-results). |
