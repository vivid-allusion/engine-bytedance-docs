---
title: "CreateFailoverJob - Creating a failure drill task"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateFailoverJob"
---

Call the CreateFailoverJob API to create a failure drill task.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateFailoverJob&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|bPlvIo">必选</span> `Example: CreateFailoverJob`

The interface name. The current API name is `CreateFailoverJob`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|jLZaiS">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**JobName ** <span data-label="purple">String </span>`optional` `Example: FailoverJob-01`

The name of the failure drill task.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-). Cannot start with http:// or https://.

* If you do not provide this parameter or leave it empty, it defaults to the ID of the failure drill task.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a FailoverJob`

The description of the failure drill task.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**JobType ** <span data-label="purple">String </span><span data-api-tag="require|DwBdNH">必选</span> `Example: dcc`

The type of the target to be drilled for the failure drill task. Values:


* dcc: Direct Connect (DC) Connection.

* bgp: BGP Peer.



**JobDuration ** <span data-label="purple">Integer </span><span data-api-tag="require|byqCNF">必选</span> `Example: 10`

The duration of the failure drill. Value range: 1\-4320. Unit: minutes.



**JobAct ** <span data-label="purple">String </span>`optional` `Example: start`

Specify whether to start the failure drill immediately. Values:


* start: Yes.

* null (default): No.



**Objects.N.ObjectId ** <span data-label="purple">String </span>`optional` `Example: dcc-d012mga***`

The resource ID of the target to be drilled. Values:


* The ID of the DC Connection. This parameter must be set to the DC Connection ID when `JobType` is `dcc`. You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.

* The ID of the BGP Peer. This parameter must be set to the BGP Peer ID when `JobType` is `bgp`. You can call the [DescribeBgpPeers](https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeers) API to query the BGP Peer ID.



**Objects.N.DirectConnectConnectionName ** <span data-label="purple">String </span>`Optional` `Example: dcc-01`

The name of the DC Connection. This parameter is configurable only if `JobType` is set to `dcc`.

You can call the [DescribeDirectConnectConnectionAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionAttributes) API to query the name of the DC Connection.



**Objects.N.ConnectionType ** <span data-label="purple">String </span>`optional` `Example: DedicatedConnection`

The type of the DC Connection. This parameter is configured only if `JobType` is set to `dcc`. Values:


* SharedConnection: Shared Line.

* DedicatedConnection: Dedicated Line.



**Objects.N.VirtualInterfaceId ** <span data-label="purple">String </span>`optional Example: dcv-7qth0ll6jmc****`

The ID of the DC Virtual Interface associated with the BGP Peer. This parameter is configurable only if `JobType` is set to `bgp`.

You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the ID of the DC Virtual Interface.



**Objects.N.VirtualInterfaceName ** <span data-label="purple">String </span>`optional` `Example: DCv-01`

The name of the DC Virtual Interface associated with the BGP peer. This parameter is configurable only if `JobType` is set to `bgp`.

You can call [DescribeDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaceAttributes) to query the name of the DC Virtual Interface.



**Objects.N.PeerIP ** <span data-label="purple">String </span>`optional` `Example: 192.XXX.XXX.1/24`

Your gateway peer IP of the DC Virtual Interface. This parameter is configurable only if `JobType` is set to `bgp`.

You can call [DescribeDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaceAttributes) to query the IP address of the DC Virtual Interface.



**Objects.N.LocalIP ** <span data-label="purple">String </span>`optional` `Example: 192.XXX.XXX.1/24`

Cloud gateway peer IP of the DC Virtual Interface. This parameter is configurable only if `JobType` is set to `bgp`.

You can call [DescribeDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaceAttributes) to query the IP address of the DC Virtual Interface.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**JobId ** <span data-label="purple">String </span>`Example: foj-1234***`

The ID of the failure drill task.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateFailoverJob&Version=2020-04-01&JobType=dcc&JobDuration=10&Objects.1.ObjectId=dcc-d012mga*** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateFailoverJob",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "DirectConnectHealthCheckId": "foj-1234***"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidFailoverJob.BGPStatusDown |The BGP session status is down, so it cannot be used in failover job. |A BGP session in the Down status cannot be referenced by a failure drill task. |
|400 |InvalidFailoverJob.DCCTypeShared |The direct connect connection is shared, so it cannot be used in failover job. |Failure drill tasks cannot reference a Shared Line. |
|400 |InvalidFailoverJob.InvalidAct |The failover job action is invalid. |The action to perform on the failure drill task is invalid. |
|400 |InvalidFailoverJob.InvalidDuration |The failover job duration is invalid. |The duration specified for the failure drill task is invalid. It must be greater than 1 minute and less than 72 hours. |
|400 |InvalidFailoverJob.InvalidType |The failover job type is invalid. |The task type for the failure drill to be created is not supported. |
|400 |InvalidFailoverJob.ObjectInUse |The object has already been used by another job. |The target instance already exists in another failure drill task and cannot be referenced again. |
|400 |InvalidFailoverJob.ObjectsInvalid |At least one object instance should be included. |At least one instance must be included. |
|400 |InvalidFailoverJob.OnlyOneBeRunning |Only one failover job is allowed to be started under each account. |Only one failure drill task per account can be in the running status at a time. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |QuotaExceeded.FailoverJob |You've reached the limit on the number of failover jobs that you can use. |You have reached the maximum number of failure drill tasks that can be created. |
|400 |QuotaExceeded.FailoverJobObject |You've reached the limit on the number of failover job for the object that can be used. |You have reached the maximum number of target instances allowed per failure drill task. |
|403 |Forbidden |You are not authorized to perform operations on the specified shared connection. |No permission to perform actions on the specified Shared Line. |
|403 |InvalidDirectConnectVirtualInterface.CrossAccountForbidden |You are not authorized to allocate the specified virtual interface to other account. |No permission to share the specified DC Virtual Interface with another account. |
|403 |InvalidFailoverJob.Forbidden |You are not authorized to perform failover job operations on the specified account. |No permission to perform failure drill task actions on the specified account. |
|404 |InvalidBgpPeer.NotFound |The specified BGP peer does not exist. |The specified BGP Peer does not exist. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
