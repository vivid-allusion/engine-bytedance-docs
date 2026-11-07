---
title: "QueryDataMigrateTask - query migration task"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/QueryDataMigrateTask_-_query_migration_task"
---

Call the QueryDataMigrateTask API to query migration tasks.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Below are the unique request parameters for this API and some common parameters For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|k7pIL3">必选</span> `Example: QueryDataMigrateTask`

Operation to be performed: QueryDataMigrateTask.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VIzTPm">必选</span> `Example value: 2018-01-01`

API version. Value: 2018\-01\-01.



**TaskID ** <span data-label="purple">long </span><span data-api-tag="require|Y8c7Gg">必选</span> `Example: 298686`

Task ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the ListDataMigrateTask API to query the task ID.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Below are the unique response parameters for this API For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CreateTime ** <span data-label="purple">string </span>`Example value: 2024-05-14 19:20:39`

Time when the task is created.



**TaskID ** <span data-label="purple">long </span>`Example: 298686`

Task ID.



**TaskStatus** <span data-label="purple">string</span> `Example value: Success`

The task status includes the following options:


* `Preparing`: The task is being prepared.

* `Transferring`: The task is in progress.

* `Suspended`: The task is paused.

* `Success`: The task completed successfully.

* `Stopping`: The task is stopping.

* `Stopped`: The task has been stopped.

* `Failure`: The task has failed.

* `ResultGenerating`: Generate task results.



**BasicConfig ** <span data-label="purple">object </span>`Example: -`

Basic task configuration.


**TaskName ** <span data-label="purple">string </span>`Example value: test`

Name of the migration task.



**Bandwidth ** <span data-label="purple">integer </span>`Example value: 200000`

The default bandwidth for migration tasks, measured in Byte/s.



**FailedNumToAbort ** <span data-label="purple">integer </span>`Example value: 2`

Specifies the number of consecutive failed objects allowed in migration tasks.



**EnableRangeCheck ** <span data-label="purple">boolean </span>`Example value: true`

If you enable sampling verification, DMS will retrieve 100 bytes from each object on the source side and 100 corresponding bytes from the target side to verify data consistency between source and target. The options are as follows:


* `true`: Enable sampling verification.

* `false`: Disable sampling verification.



**OverwritePolicy ** <span data-label="purple">string </span>`Example value: Force`

Migration task overwrite policy. Value details are as follows:


* `Force`: For files with the same name, always overwrite the destination with the source without any checks.

* `None`: For files with the same name, always skip without any checks.

* `LastModify`: When files with the same name exist on both the source and destination, the overwrite decision is made based on the lastmodify field (last modified time). Overwriting occurs only if the file on the source has a later last modified time than the file on the destination.



**SourceType ** <span data-label="purple">string </span>`Example value: StorageTypeObject`

Type of source data, with the following options:


* `StorageTypeObject`: The source type is object storage.

* `StorageTypeUrl`: The source type is a URL list.



**StorageClass ** <span data-label="purple">string </span>`Example value: Standard`

The storage type of the migrated object at the target, with the options explained below:


* `Standard`: Standard Storage.

* `InheritSource`: Inherit source storage type.

* `Ia`: Infrequent Access Storage.

* `ArchiveFr`: Archive Flashback Storage.

* `IntelligentTiering`: Intelligent Tiering Storage.

* `ColdArchive`: Cold Archive Storage.

* `Archive`: Archive.

* `DeepColdArchive`: Deep Cold Archive




**AdvanceConfig ** <span data-label="purple">object </span>`Example: -`

Advanced task configuration.


**PrivateLink ** <span data-label="purple">object </span>`Example: -`

Network configuration for direct connect tasks.


**VpcID ** <span data-label="purple">string </span>`Example: vpc-3ewj81jek8l4w70o42vd****`

Private network ID.



**SubnetID ** <span data-label="purple">string </span>`Example value: subnet-36stxciqoo6ww383g0x25****`

Subnet ID in the private network.



**SecurityGroupIDs ** <span data-label="purple">string[] </span>`Example value: sg-3rfeg3y7jccg016nf3p9v****`

Security group IDs in the private network.



**IdcIP ** <span data-label="purple">string </span>`Example: 192.168.0.0`

Data center IPv4 address.



**IdcPort ** <span data-label="purple">integer </span>`Example value: 8008`

Port number of the data center's IPv4 address.



**ENIRole ** <span data-label="purple">string </span>`Example: DMSEniCtlRole`

Name of the delegated authorization role for the user's virtual NIC. When creating a shuttle in DMS, this role is required to obtain related permissions.




**RenameSetting ** <span data-label="purple">object </span>`Example: -`

Object rename settings.


**Pattern ** <span data-label="purple">string </span>`Example value: ^`

Renamed regular expression rule.



**ReplaceStr ** <span data-label="purple">string </span>`Example value: prefix-path/`

Target string to replace.




**IncreaseSetting ** <span data-label="purple">object </span>`Example value: -`

Incremental migration settings.


**Times ** <span data-label="purple">integer </span>`Example: 1`

Number of times incremental migration is performed after completing the stock migration (i.e., first migration)



**Interval ** <span data-label="purple">integer </span>`Example: 2`

Interval for incremental migration tasks, indicating how often an incremental migration starts. The unit is hours.




**TimeBandwidthSetting ** <span data-label="purple">object[] </span>`Example value: -`

Time\-based bandwidth control configuration.


**Start ** <span data-label="purple">integer </span>`Example value: 1`

Flow control start time.



**End ** <span data-label="purple">integer </span>`Example value: 3`

Flow control end time.



**Bandwidth ** <span data-label="purple">long </span>`Example: 100`

Rate limit in bytes per second (Byte/s).





**Source ** <span data-label="purple">object </span>`Example: -`

Task source configuration.


**ObjectSourceConfig ** <span data-label="purple">object </span>`Example: -`

Source data object storage access configuration.


**BucketAccessConfig ** <span data-label="purple">object </span>`Example value: -`

Access configuration for the bucket containing the object


**AK ** <span data-label="purple">string </span>`Example value: AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****`

AccessKey ID for accessing object storage.



**SK ** <span data-label="purple">string </span>`Example value: T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TW****`

AccessKey Secret for accessing Object Storage.



**BucketName ** <span data-label="purple">string </span>`Example value: test`

Bucket name.



**RoleTrn ** <span data-label="purple">string </span>`Example value: trn:iam::2100xxxx4:role/dms_role`

RoleTrn used for cross\-service authorization.



**Vendor ** <span data-label="purple">string </span>`Example value: StorageVendorTOS`

Source data provider. Value details are as follows:


* `StorageVendorTOS`: Object Storage \- BytePlus

* `StorageVendorS3`: Other S3 protocol storage

* `StorageVendorOBS`: Huawei Cloud

* `StorageVendorCOS`: Tencent Cloud

* `StorageVendorOSS`: Alibaba Cloud

* `StorageVendorKodo`: Qiniu Cloud

* `StorageVendorKs3`: Kingsoft Cloud

* `StorageVendorGCS`: Google Cloud

* `StorageVendorURLAtEndPoint`: Indicates that when the source data is a URL list, use the download address to get the file list.



**Region ** <span data-label="purple">string </span>`Example value: cn-beijing`

The region where the bucket is located.



**Endpoint ** <span data-label="purple">string </span>`Example value: dms.cn-beijing.byteplusapi.com.cn`

The access domain name for object storage, excluding the bucket name.




**PrefixList ** <span data-label="purple">string[] </span>`Example value: prefix`

List of prefixes to migrate.



**PrefixListFile ** <span data-label="purple">string </span>`Example: https://test.dms.cn-beijing.byteplusapi.com.cn/excel.txt`

Access link for the prefix list file to be migrated.



**KeyListFile ** <span data-label="purple">string </span>`Example value: https://test.dms.cn-beijing.byteplusapi.com.cn/data.txt`

Access link to the list of objects to be migrated.



**ScanWithDelimiter ** <span data-label="purple">boolean </span>`Example value: true`

Indicate whether the source carries a delimiter. The options are as follows:


* `true`: List with delimiter. TOS can access files across multi\-level directories in the source bucket and ensures the integrity of files migrated to TOS.

* `false`: List without delimiter. File migration speed is faster, but if the source object storage enables bucket acceleration or similar scenarios, some files may not be fully migrated to TOS.



**StartTime ** <span data-label="purple">string </span>`Example: "2024-09-03 14:26:57"`

Select files for migration by specifying a date; only files created or modified after this date will be migrated.



**IsExcluded ** <span data-label="purple">boolean </span>`Example: false`

Used to specify objects to exclude from migration. Must be used with PrefixList or PrefixListFile; otherwise, it is invalid.

After specifying objects with PrefixList or PrefixListFile, migration behavior varies based on the value of IsExcluded. Value description:


* `true`: Enables exclusion. After this is enabled, DMS will exclude objects specified by PrefixList or PrefixListFile and migrate only the remaining objects.

* `false`: Disables exclusion. DMS will migrate the objects specified by PrefixList or PrefixListFile.




**UrlSourceConfig ** <span data-label="purple">object </span>`Example value: -`

Access configuration for URL list as a data source.


**IsUrlTryRangeGet ** <span data-label="purple">boolean </span>`Example value: true`

Enable range\-get migration. Details are as follows:


* `true`: Enable range\-get migration. When enabled, DMS supports migration using breakpoint resume, allowing interrupted file transfers due to network issues to restart from the breakpoint rather than from the beginning. This avoids extra data usage and reduces costs.

* `false`: Do not enable range\-get migration.



**BucketAccessConfig ** <span data-label="purple">object </span>`Example value: -`

Access configuration for the bucket storing the URL list file.


**AK ** <span data-label="purple">string </span>`Example value: AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****`

AccessKey ID for accessing object storage.



**SK ** <span data-label="purple">string </span>`Example value: T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TW****`

AccessKey Secret for accessing object storage.



**BucketName ** <span data-label="purple">string </span>`Example value: test`

The name of the bucket.



**RoleTrn ** <span data-label="purple">string </span>`Example value: trn:iam::2100xxxx4:role/dms_role`

RoleTrn used for cross\-service authorization.



**Vendor ** <span data-label="purple">string </span>`Example value: StorageVendorTOS`

Source data selection. The values are as follows:


* `StorageVendorTOS`: Object Storage \- BytePlus

* `StorageVendorS3`: Other S3 protocol storage

* `StorageVendorOBS`: Huawei Cloud

* `StorageVendorCOS`: Tencent Cloud

* `StorageVendorOSS`: Alibaba Cloud

* `StorageVendorKodo`: Qiniu Cloud

* `StorageVendorKs3`: Kingsoft Cloud

* `StorageVendorGCS`: Google Cloud

* `StorageVendorURLAtEndPoint`: Used to obtain a file list using download links when the source data is a URL list.



**Region ** <span data-label="purple">string </span>`Example value: cn-beijing`

The region where the bucket is located.



**Endpoint ** <span data-label="purple">string </span>`Example value: dms.cn-beijing.byteplusapi.com.cn`

Access domain name for object storage, excluding bucket name.




**UrlListName ** <span data-label="purple">string </span>`Example: data.txt`

Name of the URL list.



**UrlListLink ** <span data-label="purple">string </span>`Example value: https://test.dms.cn-beijing.byteplusapi.com.cn/data.txt`

Public access link for the URL list.





**Target ** <span data-label="purple">object </span>`Example: -`

Target configuration for the task.


**AK ** <span data-label="purple">string </span>`Example value: AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****`

AccessKey ID for accessing Object Storage.



**SK ** <span data-label="purple">string </span>`Example: T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TW****`

AccessKey Secret for accessing object storage.



**BucketName ** <span data-label="purple">string </span>`Example value: test`

The name of the bucket.



**RoleTrn ** <span data-label="purple">string </span>`Example: trn:iam::2100xxxx4:role/dms_role`

RoleTrn used for cross\-service authorization.



**Vendor ** <span data-label="purple">string </span>`Example: StorageVendorTOS`

Source data source. Description:


* `StorageVendorTOS`: Object Storage \- BytePlus

* `StorageVendorS3`: Other S3 protocol storage

* `StorageVendorOBS`: Huawei Cloud

* `StorageVendorCOS`: Tencent Cloud

* `StorageVendorOSS`: Alibaba Cloud

* `StorageVendorKodo`: Qiniu Cloud

* `StorageVendorKs3`: Kingsoft Cloud

* `StorageVendorGCS`: Google Cloud

* `StorageVendorURLAtEndPoint`: When the source data is a URL list, use the download URL to get the file list.



**Region ** <span data-label="purple">string </span>`Example value: cn-beijing`

The region where the bucket is located.



**Endpoint ** <span data-label="purple">string </span>`Example value: dms.cn-beijing.byteplusapi.com.cn`

The access domain name for Object Storage, excluding the bucket name.




**TaskProgress ** <span data-label="purple">object </span>`Example: -`

Task migration progress.


**FailedBytes ** <span data-label="purple">long </span>`Example value: 0`

Number of bytes failed to migrate.



**FailedObjects ** <span data-label="purple">long </span>`Example: 0`

Number of failed objects during migration.



**RemainingBytes ** <span data-label="purple">long </span>`Example value: 0`

Bytes not migrated.



**RemainingObjects ** <span data-label="purple">long </span>`Example value: 0`

Number of objects not migrated.



**NotExistBytes ** <span data-label="purple">long </span>`Example: 0`

Number of non\-existent bytes, indicating the bytes deleted from the source during migration.



**NotExistObjectCount ** <span data-label="purple">long </span>`Example: 0`

Number of non\-existent objects, meaning the number of objects deleted from the source during migration.



**SkipBytes ** <span data-label="purple">long </span>`Example value: 0`

Skipped bytes. DMS skips objects in Archive, Cold Archive, and Deep Cold Archive. If the overwrite policy is set to not overwrite, DMS also skips files with the same name. Skipped bytes refers to the total number of bytes for all objects skipped during migration.



**SkipObjectCount ** <span data-label="purple">long </span>`Example value: 0`

Skipped objects. DMS skips objects in Archive, Cold Archive, and Deep Cold Archive. If the overwrite policy is set to not overwrite, DMS also skips files with the same name. Skipped objects refers to the total number of objects skipped during migration.



**TotalBytes ** <span data-label="purple">long </span>`Example value: 5357251`

Total number of bytes.



**TotalObjects ** <span data-label="purple">long </span>Example value: 10003

Total number of objects.



**TransferredBytes ** <span data-label="purple">long </span>Example value: 5357251

Number of bytes transferred successfully.



**TransferredObjects ** <span data-label="purple">long </span>`Example value: 10003`

Number of objects migrated successfully.



**TransferBytesSpeed ** <span data-label="purple">long </span>Example value: 100

Average migration bandwidth.



**TransferCountSpeed ** <span data-label="purple">long </span>`Example: 100`

Average migration QPS.




**TaskReport ** <span data-label="purple">object </span>`Example value: -`

Migration report.


**SuccessListName ** <span data-label="purple">string </span>`Example value: dms-210006****-514-1715685639_lsource_dest_success`

Name of the list of successfully migrated objects.



**FailedListName ** <span data-label="purple">string </span>`Example value: dms-210006****-514-1715685639_source_dest_failed`

Name of the migration failed object list.



**ReportName ** <span data-label="purple">string </span>`Example: dms-210006****-514-1715685639_lsource_dest_report.pdf`

Name of the migration report.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=QueryDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20240513T123200Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240513/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "TaskID": 298686
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```text
{
  "ResponseMetadata": {
    "RequestId": "2024051320320615823222506938****",
    "Action": "QueryDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {
        "AdvanceConfig": {},
        "BasicConfig": {
            "Bandwidth": 1073741824,
            "EnableRangeCheck": false,
            "FailedNumToAbort": 20,
            "OverwritePolicy": "None",
            "SourceType": "StorageTypeObject",
            "StorageClass": "Standard",
            "TaskName": "test"
        },
        "CreateTime": "2024-05-14 19:20:39",
        "Source": {
            "ObjectSourceConfig": {
                "BucketAccessConfig": {
                    "AK": "AKLTZjl****jMGM4ZWE4MTQwMzgzY2Y",
                    "BucketName": "source",
                    "Endpoint": "http://dms.cn-beijing.byteplusapi.com.cn",
                    "Region": "cn-beijing",
                    "RoleTrn": "",
                    "Vendor": "StorageVendorS3"
                },
                "KeyListFile": "",
                "PrefixListFile": "",
                "ScanWithDelimiter": false
            }
        },
        "Target": {
            "AK": "AKLTZjl****jMGM4ZWE4MTQwMzgzY2Y",
            "BucketName": "dest",
            "RoleTrn": ""
        },
        "TaskID": 84,
        "TaskProgress": {
            "FailedBytes": 0,
            "FailedObjects": 0,
            "NotExistBytes": 0,
            "NotExistObjectCount": 0,
            "RemainingBytes": 0,
            "RemainingObjects": 0,
            "SkipBytes": 5357251,
            "SkipObjectCount": 10003,
            "TotalBytes": 5357251,
            "TotalObjects": 10003,
            "TransferBytesSpeed": 0,
            "TransferCountSpeed": 0,
            "TransferredBytes": 0,
            "TransferredObjects": 0
        },
        "TaskReport": {
            "FailedListName": "dms-210006****-514-1715685639_source_dest_failed",
            "ReportName": "dms-210006****-514-1715685639_lsource_dest_report.pdf",
            "SuccessListName": "dms-210006****-514-1715685639_lsource_dest_success"
        },
        "TaskStatus": "Success"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the error codes related to business logic for this API. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error codes |Error message |Description |
|---|---|---|---|
|404 |TaskNotFound |TaskNotFound |The task does not exist. |
