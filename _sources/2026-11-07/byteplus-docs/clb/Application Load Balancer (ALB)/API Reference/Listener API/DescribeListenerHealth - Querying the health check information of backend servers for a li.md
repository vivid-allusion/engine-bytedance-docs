---
title: "DescribeListenerHealth - Querying the health check information of backend servers for a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeListenerHealth"
---

Call the DescribeListenerHealth API query the health check information of backend servers associated with the specified listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeListenerHealth&groupName=%E7%9B%91%E5%90%AC%E5%99%A8&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Pkip5v">必选</span> `Example: DescribeListenerHealth`

Action to execute. Set the value to DescribeListenerHealth.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|lPXBOO">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ListenerIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|gqIMlB">必选</span> `Example: ListenerIds.1=lsn-abc*****&ListenerIds.2=lsn-def*******`

Listener ID.


* Parameter \- N: Represents the serial number of the listener, with a value range of 1 to 10.

* Separate listener IDs with ampersands (&).



**OnlyUnHealthy** <span data-label="purple">boolean</span> `optional` `Example: true`

Only return information about backend servers with a health check status of "exception". Valid values:


* false

* true



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: default`

The project name that the listener belongs to.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



**TotalCount ** <span data-label="purple">integer </span>`Example: 26`

The total number of listeners queried in this request.



**Listeners ** <span data-label="purple">object[] </span>`Example: -`

Listener list.


**ListenerId ** <span data-label="purple">string </span>`Example: lsn-12344***765`

Listener ID.



**Results ** <span data-label="purple">object[] </span>`Example: -`

Details of exception servers.


**ServerId ** <span data-label="purple">string </span>`Example: rs-123****654`

Backend server ID.



**InstanceId ** <span data-label="purple">string </span>`Example: i-123****765`

ID of the ECS instance or network interface.



**Type ** <span data-label="purple">string </span>`Example: esc`

Type of backend server.


* ecs: Elastic Compute Service (ECS).

* eni: Network interface.



**Ip ** <span data-label="purple">string </span>`Example: 192.168.0.1`

The IP address of the backend server.



**Port ** <span data-label="purple">integer </span>`Example: 443`

Port number of the backend server.



**RuleNumber ** <span data-label="purple">integer </span>`Example: 12`

Number of forwarding rules associated with the backend server.



**ServerGroupId ** <span data-label="purple">string </span>`Example: rsp-123****765`

ID of the server group to which the backend server belongs.



**ServerGroupName ** <span data-label="purple">string </span>`Example: server group 1`

Name of the server group to which the backend server belongs.



**Status ** <span data-label="purple">string </span>`Example: Down`

Status of the backend server.


* Up: Normal.

* Down: Abnormal




**Status ** <span data-label="purple">string </span>`Example: Active`

Listener status.


* Active: Normal.

* Error: Exception exists.

* NoTarget: No target.

* Disabled: Not enabled.



**TotalBackendServerCount ** <span data-label="purple">integer </span>`Example: 50`

The total number of backend servers under the listener.



**UnHealthyCount ** <span data-label="purple">integer </span>`Example: 3`

The total number of backend servers with an **Exception** health check status.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeListenerHealth&Version=2020-04-01&ListenerIds.1=lsn-123***765&OnlyUnHealthy=true HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021122917************14702044B16",
        "Action": "DescribeListenerHealth",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Listeners": [
            {
                "ListenerId": "lsn-123****7654",
                "TotalCount": 1,
                "UnHealthyCount": 1,
                "Status": "Error",
                "Results": [
                    {
                        "ServerId": "rs-3ciw6son****46c6rrtl3tpi3",
                        "InstanceId": "i-3tli51pv****j0wuvaeh",
                        "ServerGroupId": "rsp-2fe5fl3****405oxruwbagicr",
                        "Type": "ecs",
                        "Ip": "172.16.1.242",
                        "Port": 1,
                        "RuleNumber": 1,
                        "Status": "Down"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.Listener |You've reached the limit on the number of listeners that you can operate at a time. |The maximum number of listeners that can be operated on in a single request has been reached. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
