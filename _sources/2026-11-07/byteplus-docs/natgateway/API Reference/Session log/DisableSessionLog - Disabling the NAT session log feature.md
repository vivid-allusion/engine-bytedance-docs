---
title: "DisableSessionLog - Disabling the NAT session log feature"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DisableSessionLog"
---

Call the DisableSessionLog API to disable the session log feature for the NAT instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DisableSessionLog&groupName=NAT%E4%BC%9A%E8%AF%9D%E6%97%A5%E5%BF%97&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|1T2irx">必选</span> `Example: DisableSessionLog`

The action that you want to perform. Value: DisableSessionLog.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|chsdLS">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**SessionLogId ** <span data-label="purple">string </span><span data-api-tag="require|JaTD89">必选</span> `Example: nsl-273w1s2v5xnuo7fap8t8****`

The ID of the session log.

You can call the [DescribeSessionLogs](https://docs.byteplus.com/en/docs/natgateway/DescribeSessionLogs) API to query the session log ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DisableSessionLog&Version=2020-04-01&SessionLogId=nsl-273w1s2v5xnuo7fap8t8**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DisableSessionLog",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidSessionLog.InvalidStatus |The specified session log instance is not in the correct status for the request. |The specified NAT session log instance cannot respond to this request due to its status. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|404 |InvalidSessionLog.NotFound |The specified session log instance does not exist. |The current NAT session log instance does not exist. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
