---
title: "DescribeFailoverJobs - Querying the list of failure drill tasks"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeFailoverJobs"
---

Call the DescribeFailoverJobs API to query failure drill tasks that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeFailoverJobs&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|wRNgXg">必选</span>`Example: DescribeFailoverJobs`

The interface name. The current API name is `DescribeFailoverJobs`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|oqFPNz">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**JobIds.N ** <span data-label="purple">String </span>`optional` `Example: foj-1234***`

The ID of the health check probe.


* N represents the sequence number of a failure drill task ID. You can call up to 100 IDs per request.

* Separate multiple failure drill task IDs with ampersands (&).



**JobName ** <span data-label="purple">String </span>`optional` `Example: FailoverJob-01`

The name of the failure drill task.



**JobType ** <span data-label="purple">String </span>`optional` `Example: dcc`

The type of the target to be drilled for the failure drill task. Values:


* dcc: Direct Connect (DC) Connection.

* bgp: BGP Peer.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If left blank or set to 0, it defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

The total number of failure drill tasks meeting the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**FailoverJobs** <span data-label="purple">Object[]</span> `Example: -`

The details of the failure drill task.


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



**ObjectCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of failure drill target resources.



**Objects ** <span data-label="purple">Object[] </span>`Example: -`

The details of the failure drill target resource.


**ObjectId** <span data-label="purple">String</span> `Example: dcc-d012mga***`

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
GET /?Action=DescribeFailoverJobs&Version=2020-04-01&JobName=FailoverJob-01 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeFailoverJobs",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "FailoverJobs": [
            {
                "JobId": "foj-1234****",
                "JobName": "FailoverJob-01",
                "JobType": "dcc",
                "Objects": [
                    {
                        "PeerIp": "192.XX.XX.1/24",
                        "LocalIp": "192.XX.XX.2/24",
                        "ObjectId": "dcc-d012mga***",
                        "ConnectionType": "SharedConnection",
                        "VirtualInterfaceId": "dcv-7qth0ll6jmc****",
                        "VirtualInterfaceName": "dcv-01",
                        "DirectConnectConnectionName": "dcc-01"
                    }
                ],
                "AccountId": "20000***",
                "CreatedAt": "2025-07-03 10:48:21",
                "JobStatus": "starting",
                "JobStopAt": "2025-07-03 10:58:21",
                "JobStartAt": "2025-07-03 10:48:21",
                "Description": "This is a FailoverJob",
                "JobDuration": 10,
                "ObjectCount": 2,
                "JobTotalTime": 600
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.FailoverJobId |You've reached the limit on the number of failover job IDs that you can describe. |You have reached the maximum number of failure drill tasks that can be queried. |
|403 |Forbidden |You are not authorized to perform operations on the specified shared connection. |No permission to perform actions on the specified Shared Line. |
|403 |InvalidDirectConnectVirtualInterface.CrossAccountForbidden |You are not authorized to allocate the specified virtual interface to other account. |No permission to share the specified DC Virtual Interface with another account. |
|403 |InvalidFailoverJob.Forbidden |You are not authorized to perform failover job operations on the specified account. |No permission to perform failure drill task actions on the specified account. |
