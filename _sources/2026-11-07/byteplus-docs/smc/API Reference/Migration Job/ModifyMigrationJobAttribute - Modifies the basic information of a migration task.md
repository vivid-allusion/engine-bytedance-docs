---
title: "ModifyMigrationJobAttribute - Modifies the basic information of a migration task"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/ModifyMigrationJobAttribute"
---

Call the ModifyMigrationJobAttribute operation to modify the basic information of a migration task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, if you do not pass in optional parameters, the original configuration is retained.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyMigrationJobAttribute&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|26qdOM">必选</span> `Sample value: ModifyMigrationJobAttribute`

The operation that you want to perform. Valid value: ModifyMigrationJobAttribute.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|8YFL5m">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**NetworkTransitionMode ** <span data-label="purple">string </span>`Optional` `Sample value: PublicNetwork`

The network transfer mode. Value:


* PublicNetwork: Public network.

* VPC: VPC.



**Bandwidth ** <span data-label="purple">integer </span>`Optional` `Sample value: 0`

The network transfer bandwidth. Unit: Mbps. The minimum value (default) is `0`, which means throttling is disabled.



**MigrationJobDescription ** <span data-label="purple">string </span>`Optional` `Sample value: Migrate local virtual machine`

The task description.


* Start with a letter or a Chinese character only.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an empty string is passed in, the original description information will be cleared.</div>




**MigrationJobId ** <span data-label="purple">string </span><span data-api-tag="require|BEcZSw">必选</span> `Sample value: job-3tiegs1y963vj0****`

The migration task ID. You can call the [DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) operation to query and obtain the migration task ID.



**MigrationJobName ** <span data-label="purple">string </span>`Optional` `Sample value: VM migration to ECS`

The task name.


* Start with a letter or Chinese.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MigrationJobId ** <span data-label="purple">string </span>`Sample value: job-3tiegs1y963vj0****`

The migration task ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyMigrationJobAttribute&Version=2020-04-01&MigrationJobId=job-3tiegs1y963vj0****&MigrationJobName=VMtoECS HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202306021637410F150D*****",
    "Action": "ModifyMigrationJobAttribute",
    "Version": "2020-04-01",
    "Service": "smc",
    "Region": "cn-beijing"
  },
  "Result": {
    "MigrationJobId": "job-3tiegs1y963vj0******"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDestinationTypeForOperate.Unsupported |The specified migration job destination type does not support operate. |The type of the specified migration task does not support this operation. |
|400 |InvalidJobStateForOperate.Unsupported |The specified migration job state not support operate. |The status of the specified migration task does not support this operation. |
|400 |InvalidMigrationJobDescription.Malformed |The specified MigrationJobDescription is malformed. |The specified MigrationJobDescription value is invalid. |
|400 |InvalidMigrationJobName.Malformed |The specified MigrationJobName is malformed. |The specified MigrationJobName value is invalid. |
|400 |InvalidNetworkTransitionMode.Malformed |The specified migration job network transition mode is malformed. |The network transfer type of the specified migration task is invalid. |
|400 |LimitExceeded.MinimumBandwidth |The number of specified Bandwidth exceeds the minimum limit. |The value specified for Bandwidth is below the lower limit. |
|400 |MissingParameter.MigrationJobId |The required parameter MigrationJobId is not supplied. |The MigrationJobId parameter cannot be empty. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|404 |InvalidMigrationJob.NotFound |The specified migration job does not exist. |The specified migration task does not exist. |
|404 |InvalidSourceTransferEip.NotFound |The specified source instance does not associate eip. |No EIP is associated with the specified source instance. |
|404 |InvalidSourceTransferPrivateIp.NotFound |The specified source instance private ip does not exist. |The specified source instance does not have a private IP address. |
|404 |InvalidTransferEip.NotFound |The specified destination instance does not associate eip. |No EIP is associated with the specified target instance. |
|412 |OperationDenied.AgentNeedUpgrade |The specified migration agent need upgrade |Upgrade the migration Agent. |
