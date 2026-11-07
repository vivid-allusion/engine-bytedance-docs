---
title: "DescribeFailoverJobAttributes - Querying a failure drill task"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeFailoverJobAttributes"
---

Call the DescribeFailoverJobAttributes API to query the details of a specified failure drill task.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeFailoverJobAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|WGDuTU">必选</span> `Example: DescribeFailoverJobAttributes`

The interface name. The current API name is `DescribeFailoverJobAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|K3MQNl">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**JobID ** <span data-label="purple">String </span><span data-api-tag="require|MxjzLB">必选</span> `Example: foj-1234***`

The ID of the failure drill task.

You can call the [DescribeFailoverJobs](https://docs.byteplus.com/en/docs/directconnect/DescribeFailoverJobs) API to query the ID of the failure drill task.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">String </span>`Example: 20000***`

The account ID of the user.



**CreatedAt ** <span data-label="purple">String </span>`Example: 2025-07-03 10:48:21`

The time when the failure drill task is created.



**Description ** <span data-label="purple">String </span>`Example: This is a FailoverJob`

The description of the failure drill task.



**JobDuration ** <span data-label="purple">Integer </span>`Example: 10`

The duration of the failure drill. Unit: minutes.



**JobId ** <span data-label="purple">String </span>`Example: foj-1234****`

The ID of the failure drill task.



**JobName ** <span data-label="purple">String </span>`Example: FailoverJob-01`

The name of the failure drill task.



**JobStartAt ** <span data-label="purple">String </span>`Example: 2025-07-03 10:48:21`

The time when the failure drill task starts. Returns `-` if the task is not started.



**JobStatus ** <span data-label="purple">String </span>`Example: starting`

The status of the failure drill task.


* creating: The task is being created.

* updating: The task is being updated.

* prepare: The task is not started.

* starting: The task is starting.

* running: The task is running.

* stopping: The task is terminating.

* completed: The task is completed.

* deleting: The task is being deleted.



**JobStopAt ** <span data-label="purple">String </span>`Example: 2025-07-03 10:58:21`

The time when the failure drill task is completed. Returns `-` if the task has not completed.



**JobTotalTime ** <span data-label="purple">Integer </span>`Example: 600`

The actual total running duration of the failure drill task. Unit: seconds. Returns "0" if the task has not completed.



**JobType ** <span data-label="purple">String </span>`Example: dcc`

The type of the task.


* dcc: Direct Connect (DC) Connection.

* bgp: BGP Peer.



**ObjectCount ** <span data-label="purple">Integer </span>`Example: 1`

The total number of failure drill target resources.



**Objects ** <span data-label="purple">Object[] </span>`Example: -`

The details of the failure drill target resource.


**ObjectId ** <span data-label="purple">String </span>`Example: dcc-d012mga***`

The ID of the failure drill target resource.



**DirectConnectConnectionName ** <span data-label="purple">String </span>`Example: dcc-01`

Name of the DC Connection.



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-7qth0ll6jmc****`

ID of the DC Virtual interface.



**VirtualInterfaceName ** <span data-label="purple">String </span>`Example: dcv-01`

Name of the DC Virtual interface.



**PeerIp ** <span data-label="purple">String </span>`Example: 192.XX.XX.1/24`

Your gateway peer IP address.



**LocalIp ** <span data-label="purple">String </span>`Example: 192.XX.XX.2/24`

Cloud gateway peer IP address.



**ConnectionType ** <span data-label="purple">String </span>`Example: SharedConnection`

Type of the DC Connection.


* SharedConnection: Shared Line.

* DedicatedConnection: Dedicated Line.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeFailoverJobAttributes&Version=2020-04-01&JobID=foj-1234*** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20211222112033010224****",
        "Action": "DescribeFailoverJobAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RequestId": "20211222112033010224****",
        "AccountId": "20000***",
        "CreatedAt": "2025-07-03 10:48:21",
        "Description": "This is a FailoverJob",
        "JobDuration":10,
        "JobId":"foj-1234****",
        "JobName":"FailoverJob-01",
        "JobStartAt":"2025-07-03 10:48:21",
        "JobStatus":"starting",
        "JobStopAt":"2025-07-03 10:58:21",
        "JobTotalTime":"600",
        "JobType":"dcc",
        "ObjectCount":"1",
            "Object":{
                [
                 "ObjectId":"dcc-d012mga***", 
                 "DirectConnectConnectionName":"dcc-01",
                 "ConnectConnectionType":"DedicatedConnection"
                     ]
              }
          }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidFailoverJob.IsNull |The failover job does not exist. |The failure drill task does not exist. |
|403 |Forbidden |You are not authorized to perform operations on the specified shared connection. |No permission to perform actions on the specified Shared Line. |
|403 |InvalidDirectConnectVirtualInterface.CrossAccountForbidden |You are not authorized to allocate the specified virtual interface to other account. |No permission to share the specified DC Virtual Interface with another account. |
|403 |InvalidFailoverJob.Forbidden |You are not authorized to perform failover job operations on the specified account. |No permission to perform failure drill task actions on the specified account. |
|500 |InvalidFailoverJob.Forbidden |You are not authorized to perform failover job operations on the specified account. |No permission to perform failure drill task actions on the specified account. |
