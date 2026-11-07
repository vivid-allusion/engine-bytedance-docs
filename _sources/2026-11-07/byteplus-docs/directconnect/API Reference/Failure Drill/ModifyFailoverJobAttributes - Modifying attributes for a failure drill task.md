---
title: "ModifyFailoverJobAttributes - Modifying attributes for a failure drill task"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyFailoverJobAttributes"
---

Call ModifyFailoverJobAttributes to modify a specified failure drill task.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If you do not configure the following optional parameters, their current values remain unchanged.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyFailoverJobAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|vywgzU">必选</span> `Example: ModifyFailoverJobAttributes`

The interface name. The current API name is `ModifyFailoverJobAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|7s8kwi">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**JobId ** <span data-label="purple">String </span><span data-api-tag="require|oxYJ2T">必选</span>`Example: foj-1234***`

The ID of the failure drill task.



**Description ** <span data-label="purple">String </span>`Optional` `Example: This is a FailoverJob`

The description of the failure drill task.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.



**JobName ** <span data-label="purple">String </span>`optional` `Example: FailoverJob-01`

The name of the failure drill task.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-). Must not start with http:// or https://.



**JobAct ** <span data-label="purple">String </span>`optional` `Example: start`

The action to perform on the failure drill task. Values:


* update: Updates the task (including the information of associated target resources).

* start: Start the failure drill task.

* stop: Terminate the failure drill task. The associated target resources are released at this time.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>JobAct</code> is set to <code>stop</code>, all parameters except <code>AccountID</code> and <code>JobID</code> are optional.</div>




**JobType ** <span data-label="purple">String </span>`optional` `Example: dcc`

The type of the target to be drilled for the failure drill task. Values:


* dcc: Direct Connect (DC) Connection.

* bgp: BGP Peer.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The value of <code>JobType</code> cannot be changed.</div>




**JobDuration ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The duration of the failure drill. Unit: minutes.

Only failure drill tasks that have not started support modifying this parameter. You can call the [DescribeFailoverJobAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyFailoverJobAttributes) API to query `JobStatus` for the failure drill task status.



**Objects.N.ObjectId ** <span data-label="purple">String </span>`optional` `Example: dcc-d012mga***`

The resource ID of the target to be drilled. Values:


* The ID of the DC Connection. This parameter must be set to the DC Connection ID when `JobType` is `dcc`.

   You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.

* The ID of the BGP Peer. This parameter must be set to the BGP Peer ID when `JobType` is `bgp`.

   You can call the [DescribeBgpPeers](https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeers) API to query the BGP Peer ID.



**Objects.N.DirectConnectConnectionName ** <span data-label="purple">String </span>`optional` `Example: dcc-01`

The name of the DC Connection. This parameter is configurable only if `JobType` is set to `dcc`.

You can call the [DescribeDirectConnectConnectionAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionAttributes) API to query the name of the DC Connection.



**Objects.N.ConnectionType ** <span data-label="purple">String </span>`optional` `Example: DedicatedConnection`

The type of the DC Connection. This parameter is configured only if `JobType` is set to `dcc`. Values:


* SharedConnection: Shared Line.

* DedicatedConnection: Dedicated Line.



**Objects.N.VirtualInterfaceId** <span data-label="purple">String</span> `optional` `Example: dcv-7qth0ll6jmc****`

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

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyFailoverJobAttributes&Version=2020-04-01&JobId=foj-1234***&JobAct=stop HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "ModifyFailoverJobAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidAccountFailoverJob.IsNull |The failover job does not exist for the account. |The failure drill task does not exist under this account. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidFailoverJob.BGPStatusDown |The BGP session status is down, so it cannot be used in failover job. |A BGP session in the Down status cannot be referenced by a failure drill task. |
|400 |InvalidFailoverJob.DCCTypeShared |The direct connect connection is shared, so it cannot be used in failover job. |Failure drill tasks cannot reference a Shared Line. |
|400 |InvalidFailoverJob.InvalidAct |The failover job action is invalid. |The action to perform on the failure drill task is invalid. |
|400 |InvalidFailoverJob.InvalidDuration |The failover job duration is invalid. |The duration specified for the failure drill task is invalid. It must be greater than 1 minute and less than 72 hours. |
|400 |InvalidFailoverJob.InvalidStatus |The specified failover job is not in the correct status for the request. |The specified failover drill task cannot respond to this request due to its status. |
|400 |InvalidFailoverJob.InvalidType |The failover job type is invalid. |The task type for the failure drill to be created is not supported. |
|400 |InvalidFailoverJob.IsNull |The failover job does not exist. |The failure drill task does not exist. |
|400 |InvalidFailoverJob.ObjectInUse |The object has already been used by another job. |The target instance already exists in another failure drill task and cannot be referenced again. |
|400 |InvalidFailoverJob.ObjectsInvalid |At least one object instance should be included. |At least one instance must be included. |
|400 |InvalidFailoverJob.OnlyOneBeRunning |Only one failover job is allowed to be started under each account. |Only one failure drill task per account can be in the running status at a time. |
|400 |InvalidFailoverJob.StatusIsCompleted |The status of the object is completed, so no operations are permitted. |The failure drill task is completed and cannot be operated on. |
|400 |InvalidFailoverJob.StatusIsRunning |The status of the object is running, so no operations are permitted. |The failure drill task is running and cannot be operated on. |
|400 |InvalidFailoverJobAdd.TypeIsNull |The added object must specify the failover job type. |You must specify the failure drill task type when adding a target instance. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |QuotaExceeded.FailoverJob |You've reached the limit on the number of failover jobs that you can use. |You have reached the maximum number of failure drill tasks that can be created. |
|400 |QuotaExceeded.FailoverJobObject |You've reached the limit on the number of failover job for the object that can be used. |You have reached the maximum number of target instances allowed per failure drill task. |
|403 |Forbidden |You are not authorized to perform operations on the specified shared connection. |No permission to perform actions on the specified Shared Line. |
|403 |InvalidDirectConnectVirtualInterface.CrossAccountForbidden |You are not authorized to allocate the specified virtual interface to other account. |No permission to share the specified DC Virtual Interface with another account. |
|403 |InvalidFailoverJob.Forbidden |You are not authorized to perform failover job operations on the specified account. |No permission to perform failure drill task actions on the specified account. |
|404 |InvalidBgpPeer.NotFound |The specified BGP peer does not exist. |The specified BGP Peer does not exist. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
