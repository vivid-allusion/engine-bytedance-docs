---
title: "Mapping between S3 and TOS during data migration"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Mapping-between-S3-and-TOS-during-data-migration"
---

When creating a migration task, if the **File storage method** is set to **Keep original stored properties**, the file storage type in TOS will be set according to the corresponding relationship between S3 and TOS. This topic introduces the corresponding relationship between S3 and TOS when migrating data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">注意</div>



* <div data-tips="true" data-tips-type="warning">This topic only describes the correspondence between S3 and TOS when the <strong>File storage method</strong> is set to <strong>Keep original stored properties</strong> during data migration. For the correspondence between S3 and TOS storage types when calling the S3 interface, please refer to <a href="https://docs.byteplus.com/en/docs/tos/docs-compatibility-with-amazon-s3">Compatibility with Amazon S3</a>.</div>


* <div data-tips="true" data-tips-type="warning">The functionality of preserving the original storage attributes during data migration is designed according to the supported S3 storage types. Therefore, when migrating from other cloud vendors, the corresponding relationship between the storage types used by them and TOS storage types needs to be referenced against their relationship with S3. If there is no corresponding relationship, the migration will default to the standard storage layer of TOS.</div>




|**AWS** **S3** |**TOS** |
|---|---|
|* STANDARD<br><br>* REDUCED_REDUNDANCY<br><br>* OUTPOSTS |STANDARD: Standard Storage |
|* STANDARD_IA<br><br>* ONEZONE_IA |IA: Infrequent Access Storage |
|INTELLIGENT_TIERING |INTELLIGENT_TIERING: Intelligent Tiered Storage |
|GLACIER_IR |ARCHIVE_FR: Flashback Archive |
|GLACIER |ARCHIVE: Archive Storage |
|DEEP_ARCHIVE |COLD_ARCHIVE: Cold Archive Storage |
