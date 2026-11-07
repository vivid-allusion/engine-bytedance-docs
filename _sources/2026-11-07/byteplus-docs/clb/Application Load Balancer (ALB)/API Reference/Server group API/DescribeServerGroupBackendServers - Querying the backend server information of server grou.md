---
title: "DescribeServerGroupBackendServers - Querying the backend server information of server groups"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeServerGroupBackendServers"
---

Call the DescribeServerGroupBackendServers API to query the backend server information of a server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 200 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeServerGroupBackendServers&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|gKgmME">必选</span> `Example: DescribeServerGroupBackendServers`

Action to execute. Set the value to DescribeServerGroupBackendServers.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|hHr0O6">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">string </span><span data-api-tag="require|3XtbvS">必选</span> `Example: rsp-bp1o94dp5i6ea****`

ID of the backend server group.



**InstanceIds.N ** <span data-label="purple">string[] </span>`optional` `Example: InstanceIds.1=i-3tkuehz8oa3vj0wz****`

ID of the backend server instance.


* Parameter \- N: Indicates the serial number of the backend server. Value range: 1\-20.

* Separate multiple IDs with ampersands (&).


Parameter description:


* When the backend server is ECS, the parameter value is the ECS ID.

* When the backend server is a secondary network interface, the parameter value is the secondary network interface ID.

* When the backend server is an IP address, the parameter value is the IP address. You can also use the `Ips.N` parameter to specify IP type backend servers.



**Ips.N ** <span data-label="purple">string[] </span>`optional` `Example: Ips.1=192.168.1.10`

Private IP address of the backend server.

Parameter \- N: Indicates the serial number of the backend server. Value range: 1\-20.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 10`

The number of rows per page for paginated queries.


* Value range: 1\-100. Default value: 10.

* When you specify only PageSize but not PageNumber, data from page 1 is returned. When you specify only PageNumber but not PageSize, 10 entries from the specified page are returned. However, if there is no data on the specified page, an empty result is returned. When neither PageSize nor PageNumber is specified, 10 entries from page 1 are returned.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">integer </span>`Example: 50`

Total number of eligible backend servers.



**Servers ** <span data-label="purple">object[] </span>`Example: -`

Information of the backend server.


**ServerId ** <span data-label="purple">string </span>`Example: rs-3cig8e5o0kxs06c6rrsqn****`

Backend server ID.



**InstanceId ** <span data-label="purple">string </span>`Example: i-3tkuehz8oa3vj0wz****`

ID of the ECS instance or network interface.



**Type ** <span data-label="purple">string </span>`Example: ecs`

Backend server instance type.


* ecs: Elastic Compute Service instance.

* eni: Secondary network interface.

* ip: IP address (valid only for IP type server groups).



**RemoteEnabled ** <span data-label="purple">string </span>`Example: on`

Enable the remote IP feature. When the backend server instance type is IP address (i.e., Type takes the value ip), this field is valid.


* on: Enable.

* off: Disable.



**Weight ** <span data-label="purple">integer </span>`Example: 100`

Weight of the backend server.



**Ip ** <span data-label="purple">string </span>`Example: 192.XX.XX.2`

Private IP address of the backend server.



**Port ** <span data-label="purple">integer </span>`Example: 88`

Port number on which the backend server receives requests.



**Description ** <span data-label="purple">string </span>`Example: This is a backend server`

Description of the backend server.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeServerGroupBackendServers&ServerGroupId=rsp-bp1o94dp5i6ea****&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021081716563****2252431000306F1F2",
        "Action": "DescribeServerGroupBackendServers",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210817165634****252431000306F1F2",
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1,
        "Servers": [
            {
                "ServerId": "rs-3ciw6son****46c6rrtl3tpi3",
                "InstanceId": "i-3tli51pv****j0wuvaeh",
                "Type": "ecs",
                "Weight": 100,
                "Ip": "172.**.**.242",
                "Port": 1,
                "Description": "test"
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
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.BackendServer |You've reached the limit on the number of backend servers that you can operate at a time. |The maximum number of backend servers that can be operated on in a single request has been reached. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
