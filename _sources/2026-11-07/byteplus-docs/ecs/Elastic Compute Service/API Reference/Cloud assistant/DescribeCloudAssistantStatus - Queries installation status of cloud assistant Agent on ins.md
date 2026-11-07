---
title: "DescribeCloudAssistantStatus - Queries installation status of cloud assistant Agent on instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus"
---

Call the DescribeCloudAssistantStatus operation to query the installation status of the cloud assistant Agent on one or multiple instances.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCloudAssistantStatus&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|mwDAN6">必选</span> `Sample value: DescribeCloudAssistantStatus`

The action that you want to perform. Value: DescribeCloudAssistantStatus.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ppLVWm">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: InstanceIds.1=i-sdvgs****`

The instance ID. A maximum of 100 instance IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query and obtain the instance ID.


* Argument \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with &.



**OSType** <span data-label="purple">string</span> `Optional` `Sample value: linux`

The operating system type. Value:


* linux: The instance runs on the Linux operating system.

* windows: The instance runs on the Windows operating system.



**ClientVersion** <span data-label="purple">string</span> `Optional` `Sample value: v1.9.0`

The Agent version.



**Status** <span data-label="purple">string</span> `Optional` `Sample value: Running`

The Agent status. Valid values:


* Running: The Agent is running.

* Updating: The Agent is being upgraded.

* Error: An error occurred.

* Lost: Heartbeat times out.

* ReadyReboot: To be restarted.

* InstallFailed: Installation failure.

* Uninstalling: The Agent is being uninstalled.

* Initializing: The Agent is being initialized.



**PageNumber** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber** <span data-label="purple">integer</span> `Sample value: 1`

The current page number.



**PageSize** <span data-label="purple">integer</span> `Sample value: 10`

The number of entries returned on each page in a pagination query.



**TotalCount** <span data-label="purple">integer</span> `Sample value: 100`

The total number of instances with Agent installed.



**Instances** <span data-label="purple">object[]</span> `Sample value: --`

The information about instances that meet the conditions.


**InstanceId** <span data-label="purple">string</span> `Sample value: i-yci89z1gpml8j1\*\*\*\*`

The instance ID.



**InstanceName** <span data-label="purple">string</span> `Sample value: instance-3`

The instance name.



**OSType** <span data-label="purple">string</span> `Sample value: linux`

The operating system type.



**OSVersion** <span data-label="purple">string</span> `Sample value: CentOS 7.9 64 bit`

The operating system version.



**HostName** <span data-label="purple">string</span> `Sample value: iv-yci89z1gpml8j1\*\*\*\*`

The host name.



**LastHeartbeatTime** <span data-label="purple">string</span> `Sample value: 2023-07-01T09:00:45Z`

The time the last heartbeat packet is received (last online time).



**Status** <span data-label="purple">string</span> `Sample value: Running`

The Agent status.



**ClientVersion** <span data-label="purple">string</span> `Sample value: v1.1.0`

The Agent version.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Version=2020-04-01&Action=DescribeCloudAssistantStatus HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202408201648201****",
        "Action": "DescribeCloudAssistantStatus",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageSize": 10,
        "PageNumber": 1,
        "TotalCount": 1,
        "Instances": [
            {
                "InstanceId": "i-ycgk0k*****",
                "InstanceName": "",
                "OSType": "linux",
                "OSVersion": "5.14****",
                "HostName": "",
                "ClientVersion": "v1.9.0",
                "LastHeartbeatTime": "2024-08-20T12:18:56Z",
                "Status": "Running"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |InvalidOSType.Malformed |The specified OSType is malformed. |The specified operating system type is invalid. |
|400 |InvalidStatus.Malformed |The specified Status is malformed. |The specified Agent status is invalid. |
|400 |InvalidClientVersion.Malformed |The specified ClientVersion is malformed. |The specified Agent version is invalid. |
|400 |LimitExceeded.MaximumInstanceIds |The specified InstanceIds exceeds the limit. |The number of instances exceeds the limit. |
|400 |InvalidRegion |Service [ecs] is not available in region [ap\-guangzhou]. |The specified region is invalid |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
