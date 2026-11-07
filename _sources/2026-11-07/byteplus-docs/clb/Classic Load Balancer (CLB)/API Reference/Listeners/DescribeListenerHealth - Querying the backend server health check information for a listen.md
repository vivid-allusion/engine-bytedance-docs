---
title: "DescribeListenerHealth - Querying the backend server health check information for a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeListenerHealth"
---

Call the DescribeListenerHealth API to query the health check information of backend servers associated with the specified listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeListenerHealth&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|A0FacW">必选</span> `Example: DescribeListenerHealth`

Action to execute. Set the value to **DescribeListenerHealth**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|2HijT2">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|eKh9oW">必选</span> `Example: lsn-2fek3rgsxhrsw5oxruwec****` 

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to query the listener ID.



**OnlyUnHealthy ** <span data-label="purple">String </span>`optional` `Example: true`

Specifies whether to return only information about backend server groups with a health check status of "abnormal".

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Returns only information about "abnormal" backend server groups.

* false: Returns information about backend server groups in all states.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of rows per page for paginated queries. Valid range: 1\-100. Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 50`

Total number of eligible backend servers.



**UnHealthyCount ** <span data-label="purple">Integer </span>`Example: 3`

The total number of eligible backend servers with a health check status of "abnormal".



**Status ** <span data-label="purple">String </span>`Example: Active`

Status of the listener's health check.


* Active: Normal.

* Error: Exception.

* Disabled: Indicates that health checks are not enabled.

* NoTarget: Indicates that no backend servers are configured.



**Results ** <span data-label="purple">Object[] </span>`Example: -`

Detailed information about the eligible backend servers.


**ServerId ** <span data-label="purple">String </span>`Example: rs-2fel9yaoyv75s5oxruux5****`

Backend server ID.



**Type ** <span data-label="purple">String </span>`Example: ecs`

Type of backend server.


* ecs: Elastic Compute Service (ECS).

* eni: Network interface.



**InstanceId ** <span data-label="purple">String </span>`Example: i-3tm18xqalm4e8i4q****`

ID of the ECS instance or network interface.



**Ip ** <span data-label="purple">String </span>`Example: 192.XX.XX.8`

The IP address of the backend server.



**Port ** <span data-label="purple">Integer </span>`Example: 443`

Port number of the backend server.



**RuleNumber ** <span data-label="purple">Integer </span>`Example: 12`

Number of forwarding rules associated with the backend server. For TCP/UDP listeners, the return value is 0.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

ID of the server group to which the backend server belongs.



**Status ** <span data-label="purple">String </span>`Example: Down`

Status of the backend server.


* Up: Normal.

* Down: Abnormal



**UpdatedAt ** <span data-label="purple">String </span>`Example: 2019-04-23T01:37:38Z`

Update time of the backend server.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeListenerHealth&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&OnlyUnHealthy=true&PageNumber=1&PageSize=20
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeListenerHealth",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "20210811152539010225146063030****",
        "Results": [
            {
                "Ip": "192.XX.XX.8",
                "Port": 443,
                "Type": "ecs",
                "Status": "Down",
                "ServerId": "rs-2fel9yaoyv75s5oxruux5****",
                "UpdatedAt": "2019-04-23T01:37:38Z",
                "InstanceId": "i-3tm18xqalm4e8i4q****",
                "RuleNumber": 12,
                "ServerGroupId": "rsp-bp1o94dp5i6ea****"
            }
        ],
        "Status": "Active",
        "TotalCount": 50,
        "UnHealthyCount": 3
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidPageNumber.Malformed |The specified PageNumber is malformed. |The specified PageNumber format is invalid. |
|400 |InvalidPageSize.Malformed |The specified PageSize is malformed. |The specified PageSize parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
