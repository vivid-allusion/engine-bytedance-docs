---
title: "CreateDataMigrateTask - Create migration task"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/CreateDataMigrateTask_-_Create_migration_task"
---

Call the CreateDataMigrateTask API to create a migration task.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters and some common parameters for this API are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|wQJKd6">必选</span> `Example: CreateDataMigrateTask`

Operation to perform: CreateDataMigrateTask.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Z3uBUQ">必选</span> `Example value: 2018-01-01`

API version: 2018\-01\-01.



**BasicConfig** <span data-label="purple">object</span> <span data-api-tag="require|vWkJbP">必选</span></a\> `Example: -`

Basic migration task configuration.


**TaskName ** <span data-label="purple">string </span><span data-api-tag="require|RBRPnb">必选</span> `Example: dms`

Name of the migration task.



**FailedNumToAbort**<span data-label="purple">integer</span>`Optional Example: 2`

The number of objects allowed to continuously fail migration tasks. Valid values: [\-1, +∞). \-1 indicates no limit; the default value is 20.



**EnableRangeCheck ** <span data-label="purple">boolean </span>`Optional` `Example value: true`

Enable sampling verification to have DMS retrieve 100 bytes from each object on both the source and target ends, then check for consistency between them. The options are as follows:


* `true`: Enable sampling verification.

* `false`: Disable sampling verification.

   The default value is `false`.



**OverwritePolicy ** <span data-label="purple">string </span><span data-api-tag="require|ukUboT">必选</span> `Example: Force`

Migration task overwrite policy; value descriptions are as follows:


* `Force`: For files with the same name, overwrite the target directly with the source without any validation.

* `None`: For files with the same name, skip directly without any validation.

* `LastModify`: When files with the same name exist at the source and target, use the lastmodify field (last modified time) to determine whether to overwrite. Overwrite only if the source file's last modified time is later than the target file's last modified time.



**SourceType ** <span data-label="purple">string </span><span data-api-tag="require|7CA2Ya">必选</span> `Example: StorageTypeObject`

Source data types are described as follows:


* `StorageTypeObject`: The source data type is object storage.

* `StorageTypeUrl`: The source data type is a URL list.



**StorageClass ** <span data-label="purple">string </span><span data-api-tag="require|E9X4nU">必选</span> `Example: Standard`

The storage type for migrated objects on the target, as described below:


* `Standard`: Standard Storage

* `InheritSource`: Inherit source storage type

* `Ia`: Infrequent Access Storage

* `ArchiveFr`: Flashback Archive Storage

* `IntelligentTiering`: Intelligent Tiering Storage

* `ColdArchive`: Cold Archive Storage

* `Archive`: Archive Storage

* `DeepColdArchive`: Deep Cold Archive



**ObjectMigrationPolicy ** <span data-label="purple">object </span>`Optional`

Migration policy


**SyncAcl ** <span data-label="purple">boolean </span>Optional

Migrate object ACL



**SyncTag ** <span data-label="purple">boolean </span>`Optional`

Whether to migrate object tags



**SyncSymlink ** <span data-label="purple">boolean </span>`Optional`

Whether to migrate the Symlink object




**OfflineMigrationPolicy ** <span data-label="purple">object </span>`Optional`

Offline migration configuration


**Source ** <span data-label="purple">string</span><span data-api-tag="require|Eb6QIG">必选</span>

Source bucket type



**Target ** <span data-label="purple">string</span><span data-api-tag="require|Gbqwc1">必选</span>

Target bucket type




**Bandwidth ** <span data-label="purple">long </span>`Optional` `Example value: 200000`

The default bandwidth of the migration task, in bytes per second. The default value is 1073741824.




**AdvanceConfig ** <span data-label="purple">object </span>`Optional` `Example: -`

Advanced configuration for migration tasks.


**PrivateLink ** <span data-label="purple">object </span>`Optional` `Example: -`

Network configuration for data migration using a dedicated connection.


**VpcID ** <span data-label="purple">string </span><span data-api-tag="require|NMDJqB">必选</span> `Example: vpc-3ewj81jek8l4w70o42vd****`

Private network ID.



**SubnetID ** <span data-label="purple">string </span><span data-api-tag="require|SWl3pI">必选</span> `Example value: subnet-36stxciqoo6ww383g0x25****`

Subnet ID in the private network.



**SecurityGroupIDs ** <span data-label="purple">string[] </span><span data-api-tag="require|ba4iBc">必选</span> `Example: sg-3rfeg3y7jccg016nf3p9v****`

Security group ID in private network.



**IdcIP ** <span data-label="purple">string </span><span data-api-tag="require|xvzkUK">必选</span> `Example: 192.168.0.0`

IPv4 address of the data center.



**IdcPort ** <span data-label="purple">integer </span><span data-api-tag="require|0q8Yut">必选</span> `Example: 8008`

Port number for the IPv4 address of the data center.



**ENIRole** <span data-label="purple">string</span> <span data-api-tag="require|Nim5Rw">必选</span> `Example value: DMSEniCtlRole`

Name of the delegated role for the user's virtual network card. DMS requires this role to obtain necessary permissions when creating a shuttle.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you create a DMS dedicated line task in the console, the DMSEniCtlRole role is automatically created. It is recommended to create the dedicated line task in the console first; otherwise, you need to manually create this role.</div>





**RenameSetting ** <span data-label="purple">object </span>`Optional Example: -`

Object renaming configuration.


**Pattern ** <span data-label="purple">string </span><span data-api-tag="require|kOKsQ3">必选</span> `Example: ^`

Regular expression rule for renaming.



**ReplaceStr ** <span data-label="purple">string </span><span data-api-tag="require|lA3pAd">必选</span> `Example: prefix-path/`

Target string to be replaced.




**IncreaseSetting** <span data-label="purple">object</span> `Optional` `Example value: -`

Incremental migration configuration.


**Times ** <span data-label="purple">integer </span><span data-api-tag="require|0PtPw2">必选</span> `Example value: 1`

After the initial migration is completed, set the number of incremental migrations. Only supports integers from 1 to 100.



**Interval ** <span data-label="purple">integer </span><span data-api-tag="require|3CrSJ7">必选</span> `Example value: 3600`

Incremental migration interval, which is the time between each incremental migration task. The unit is seconds, and only integers in the range 3600 to 86400 are supported.




**TimeBandwidthSetting ** <span data-label="purple">object[] </span>`Optional` `Example: -`

Configure time\-based flow control.


**Start ** <span data-label="purple">integer </span><span data-api-tag="require|QbzKME">必选</span> `Example value: 23`

The start time for traffic control, ranging from 0 to 23.



**End ** <span data-label="purple">integer </span><span data-api-tag="require|cHiiSt">必选</span> `Example value: 2`

Flow control end time. The value can range from 1 to 24.



**Bandwidth ** <span data-label="purple">long </span><span data-api-tag="require|zfQ8x1">必选</span> `Example value: 100`

Flow control rate, unit: Byte/s.





**Source ** <span data-label="purple">object </span><span data-api-tag="require|EM9gjn">必选</span> `Example value: -`

Migration task source configuration.


**ObjectSourceConfig ** <span data-label="purple">object </span>`Optional` `Example: -`

Access configuration for object storage as the source data source.


**BucketAccessConfig ** <span data-label="purple">object </span><span data-api-tag="require|6jTtTW">必选</span> `Example: -`

Access configuration for the bucket where the object is stored.


**AK**<span data-label="purple">string</span>`Optional Example: AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****`

AccessKey ID for accessing object storage.



**SK ** <span data-label="purple">string </span>`optional` `Example value: T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TW****`

AccessKey Secret for accessing object storage.



**BucketName ** <span data-label="purple">string </span><span data-api-tag="require|yPQGUD">必选</span> `Example: test`

Bucket name.



**RoleTrn ** <span data-label="purple">string </span>`Optional` `Example: trn:iam::210015****:role/dms_role`

RoleTrn used for cross\-service authorization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After setting RoleTrn, you do not need to set AK or SK information. With your authorization, DMS can directly access the bucket list and files.</div>




**Vendor**<span data-label="purple">string</span><span data-api-tag="require|kSB7Ox">必选</span>`Example value: StorageVendorTOS`

Source data source. Details are as follows:


* `StorageVendorTOS`: Object Storage \- BytePlus

* `StorageVendorS3`: Other S3 protocol storage

* `StorageVendorOBS`: Huawei Cloud

* `StorageVendorCOS`: Tencent Cloud

* `StorageVendorOSS`: Alibaba Cloud

* `StorageVendorKodo`: Qiniu Cloud

* `StorageVendorKs3`: Kingsoft Cloud

* `StorageVendorGCS`: Google Cloud

* `StorageVendorURLAtEndPoint`: When the source data is a list of URLs, select this option to use the download address to retrieve the file list.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a migration task using the CreateDataMigrateTask API, only one URL list file upload method is supported—the download address.</div>




**Region ** <span data-label="purple">string </span><span data-api-tag="require|qLnfOd">必选</span> `Example value: cn-beijing`

Region where the bucket is located.



**Endpoint ** <span data-label="purple">string </span><span data-api-tag="require|quchu4">必选</span> `Example value: dms.cn-beijing.byteplusapi.com.cn`

The access domain for object storage, excluding the bucket name.




**PrefixList ** <span data-label="purple">string[] </span>`Optional` `Example value: [prefix1,prefix2]`

List of prefixes to migrate. Separate multiple prefixes with commas.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>PrefixList</code>, <code>PrefixListFile</code>, and <code>KeyListFile</code> specify the files to migrate. You only need to set one of these parameters.</div>




**PrefixListFile ** <span data-label="purple">string </span>`Optional` `Example: https://test.dms.cn-beijing.byteplusapi.com.cn/excel.txt`

Specify the access link for the prefix list file to be migrated.



**KeyListFile** <span data-label="purple">string</span> `Optional` `Example: https://test.dms.cn-beijing.byteplusapi.com.cn/data.txt`

Access link to the list of objects to be migrated.



**ScanWithDelimiter ** <span data-label="purple">boolean </span>`Optional` `Example: true`

Indicates whether the source uses delimiters when listing objects. The options are as follows:


* `true`: Enables delimiter listing. DMS can retrieve files from multi\-level directories in the source bucket, ensuring complete file migration to TOS.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you use delimiter listing, set the migration range to include (set <code>IsExcluded</code> to <code>false</code>) and specify the migration range with a prefix (by setting the <code>PrefixList</code> parameter or the <code>PrefixListFile</code> parameter), the prefix must end with a forward slash (/).   </div>
   

* `false`: Does not use delimiter listing. Migration will be faster, but in scenarios such as bucket acceleration on the source, migrating to TOS may result in incomplete files.



**StartTime ** <span data-label="purple">string </span>`Optional` `Example value: "2024-09-03 14:26:57"`

Specify the migration files by date. Only files created or modified after the specified date will be migrated.



**IsExcluded ** <span data-label="purple">boolean </span><span data-api-tag="require|qMiYSg">必选</span> `Example value: true`

Specifies objects to exclude from migration. Must be used with PrefixList or PrefixListFile; otherwise, it is invalid.

After specifying objects using PrefixList or PrefixListFile, different values for IsExcluded result in different migration operations. The options are as follows:


* `true`: Excludes specified objects. When enabled, DMS will exclude the objects listed in PrefixList or PrefixListFile and only migrate the remaining objects.

* `false`: Does not exclude objects. DMS will migrate the objects specified in PrefixList or PrefixListFile.




**UrlSourceConfig ** <span data-label="purple">object </span>`Optional` `Example value: -`

Access configuration for URL list data sources at the source side.


**IsUrlTryRangeGet ** <span data-label="purple">boolean </span>`Optional` `Example: false`

Enable range\-get migration as described below:


* `true`: Enable range\-get migration. When enabled, DMS supports breakpoint resume for file migration. If file transmission is interrupted due to network fluctuations, DMS restarts transmission from the breakpoint, avoiding extra traffic from retransmitting files from the beginning and reducing costs.

* `false`: Do not enable range\-get migration.



**BucketAccessConfig** <span data-label="purple">object</span> `Optional` `Example: -`

Configuration for accessing the bucket containing the URL list file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>BucketAccessConfig</code> and <code>UrlListName</code> are used to specify the bucket and list file name for selecting the URL file list, so both <code>BucketAccessConfig</code> and <code>UrlListName</code> must be set.</div>



**AK ** <span data-label="purple">string </span>`Optional` `Example value: AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****`

AccessKey ID for object storage access.



**SK**<span data-label="purple">string</span>`Optional Example: T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TW****`

AccessKey Secret for accessing object storage.



**BucketName ** <span data-label="purple">string </span><span data-api-tag="require|u8cofI">必选</span> `Example value: test`

Bucket name.



**RoleTrn ** <span data-label="purple">string </span>`Optional` `Example: trn:iam::210015****:role/dms_role`

RoleTrn for cross\-service authorization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After setting RoleTrn, you do not need to set AK or SK information. Once authorized, DMS can directly access bucket lists and files.</div>




**Vendor** <span data-label="purple">string</span> <span data-api-tag="require|jC49MU">必选</span>`Example: StorageVendorTOS`

Source data source options:


* `StorageVendorTOS`: Object Storage \- BytePlus

* `StorageVendorS3`: Other S3 protocol storage

* `StorageVendorOBS`: Huawei Cloud

* `StorageVendorCOS`: Tencent Cloud

* `StorageVendorOSS`: Alibaba Cloud

* `StorageVendorKodo`: Qiniu Cloud

* `StorageVendorKs3`: Kingsoft Cloud

* `StorageVendorGCS`: Google Cloud

* `StorageVendorURLAtEndPoint`: When the source data is a URL list, select this option to use download links for retrieving the file list.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a migration task with the CreateDataMigrateTask API, only one URL list upload method is supported: via download links.</div>




**Region** <span data-label="purple">string</span> <span data-api-tag="require|8pJV0i">必选</span> `Example value: cn-beijing`

The region where the bucket is located.



**Endpoint**<span data-label="purple">string</span><span data-api-tag="require|Ouz4Rs">必选</span>` Example: dms.cn-beijing.byteplusapi.com.cn`

Access domain name for object storage, excluding the bucket name.




**UrlListName ** <span data-label="purple">string </span>`Optional` `Example value: data.txt`

Name of the URL list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Either <code>UrlListLink</code> or <code>UrlListName</code> can be set; do not configure both parameters.</div>




**UrlListLink ** <span data-label="purple">string </span>`Optional` `Example value: https://test.dms.cn-beijing.byteplusapi.com.cn/data.txt`

Public access link for the URL list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Choose either <code>UrlListLink</code> or <code>UrlListName</code>; you do not need to set both.</div>






**Target ** <span data-label="purple">object </span><span data-api-tag="require|AxhES6">必选</span> `Example value: -`

Migration task target configuration.


**AK ** <span data-label="purple">string </span>`Optional` `Example: AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****`

AccessKey ID used to access the target object storage.



**SK** <span data-label="purple">string</span> `Optional` `Example: T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TW****`

AccessKey Secret used to access the target object storage



**BucketName ** <span data-label="purple">string </span><span data-api-tag="require|1rqeU0">必选</span> `Example: data`

Target bucket name.



**RoleTrn ** <span data-label="purple">string </span>`Optional` `Example value: trn:iam::2100xxxx4:role/dms_role`

RoleTrn used for cross\-service authorization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After setting <code>RoleTrn</code>, you do not need to configure AK or SK information. With your authorization, DMS can directly read bucket lists and files.</div>





&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

Only the unique return parameters for this API are listed below. For more details, see [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Task ID ** <span data-label="purple">long </span>`Example: 298686`

Task ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=CreateDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20240513T062624Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240513/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
    "BasicConfig":
    {
        "OverwritePolicy": "Force",
        "SourceType": "StorageTypeObject",
        "StorageClass": "Standard",
        "TaskName": "test1"
    },
    "Source":
    {
        "ObjectSourceConfig":
        {
            "BucketAccessConfig":
            {
                "AK": "AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****",
                "BucketName": "data",
                "Endpoint": "http://dms.cn-beijing.byteplusapi.com.cn",
                "Region": "cn-beijing",
                "SK": "T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TWpNME0y****",
                "Vendor": "StorageVendorTOS"
            }
        }
    },
    "Target":
    {
        "AK": "AKLTM2NlN2E5Yzg2ZDhkNDBjMGIzZGU3MDllMzE4NzU****",
        "BucketName": "bucketname",
        "SK": "T1RkbVpHTmlNakl3TWpobE5EVmlObUkzTURrMU16STNZakF4TWpNME0y****"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024051314263307210712807736****",
    "Action": "CreateDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {
    "TaskID": 298686
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The table below lists error codes related to API business logic. For public error codes, refer to the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |Invalid Parameter. |Invalid parameter. |
|400 |InvalidTaskName |Task name must contain 3\-32 letters, numbers, and dash (\-), and cannot start or end with dash (\-). |Invalid task name. |
|400 |InvalidParameterAssumeRole |Assume role check failed, illegal trn. |Invalid Roletrn. |
|400 |InvalidParameterTooManyPrefix |Up to prefixes num. |The number of prefixes exceeds the limit. |
|405 |InvalidStorageType |Not support this source type. |This source type is not supported. |
|408 |CreateDataMigrateTaskTimeout |Wait creating task timeout. |Task creation timed out. |
|409 |TaskNameExists |Task name already exists, please select another task name. |Duplicate task name. |
|429 |TaskLimitExceed |The number of tasks exceeds the upper limit. |The number of tasks exceeds the limit. |
|500 |InnerDBAccessErr |Access DB failed. |Internal error. |
