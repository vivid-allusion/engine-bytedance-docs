---
title: "DescribeMigrationSystemSupportTypes - Queries the target operating systems that the source system supports for migration"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/DescribeMigrationSystemSupportTypes"
---

Call the DescribeMigrationSystemSupportTypes operation to query the target operating systems that the operating system of the source server supports for migration.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeMigrationSystemSupportTypes&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ARtWjL">必选</span> `Sample value: DescribeMigrationSystemSupportTypes`

The operation that you want to perform. Valid value: DescribeMigrationSystemSupportTypes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|iwfJpc">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**OS ** <span data-label="purple">string </span><span data-api-tag="require|Mtx66y">必选</span> `Sample value: Linux`

The type of the source server operating system. Value:


* Linux

* Windows



**Platform ** <span data-label="purple">string </span><span data-api-tag="require|n8wRpL">必选</span> `Sample value: CentOS`

The operating system platform. Value:


* CentOS



**PlatformVersion ** <span data-label="purple">string </span><span data-api-tag="require|GASZtW">必选</span> `Sample value: 7.1`

The operating system version number. Example:


* 7.1: The CentOS 7.1 operating system.

* Stream 8: The CentOS Stream 8 operating system.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the migration source belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is empty, the project is default.</div>


* <div data-tips="true" data-tips-type="tip">Make sure that the account calling the operation has permission to use the specified project.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TargetOSInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The information of the target operating system supported for migration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is empty, the source server does not support operating system migration.</div>



**OS ** <span data-label="purple">string </span>`Sample value: Linux`

The type of the target operating system supported for migration.



**OSName ** <span data-label="purple">string </span>`Sample value: VeLinux10Centos`

The operating system name. Value:


* VeLinux20Centos: veLinux 2.0 CentOS Compatible.

* VeLinux10Centos: veLinux 1.0 CentOS Compatible.



**Platform ** <span data-label="purple">string </span>`Sample value: veLinux`

The target operating system platform supported for migration. Value:


* veLinux



**PlatformVersion ** <span data-label="purple">string </span>`Sample value: 1.0 CentOS Compatible`

The version number of the target operating system supported for migration. Value:


* 2.0 CentOS Compatible: veLinux 2.0 CentOS Compatible.

* 1.0 CentOS Compatible: veLinux 1.0 CentOS Compatible.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeMigrationSystemSupportTypes&Version=2020-04-01&OS=Linux&Platform=CentOS&PlatformVersion=7.1 HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240711164806E040245*****",
        "Action": "DescribeMigrationSystemSupportTypes",
        "Version": "2020-04-01",
        "Service": "smc",
        "Region": "cn-beijing"
    },
    "Result": {
        "TargetOSInfos": [
            {
                "OS": "Linux",
                "Platform": "veLinux",
                "PlatformVersion": "1.0 CentOS Compatible",
                "OSName": "VeLinux10Centos"
            },
            {
                "OS": "Linux",
                "Platform": "veLinux",
                "PlatformVersion": "2.0 CentOS Compatible",
                "OSName": "VeLinux20Centos"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |MissingParameter.OS |The required parameter OS is not supplied. |The OS parameter cannot be empty. |
|400 |MissingParameter.Platform |The required parameter Platform is not supplied. |The Platform parameter cannot be empty. |
|400 |MissingParameter.PlatformVersion |The required parameter PlatformVersion is not supplied. |The PlatformVersion parameter cannot be empty. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested operation does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
