---
title: "CreateSessionLog - Creating a NAT session log"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/CreateSessionLog"
---

Call the CreateSessionLog API to create a NAT session log.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateSessionLog&groupName=NAT%E4%BC%9A%E8%AF%9D%E6%97%A5%E5%BF%97&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ksDhYK">必选</span> `Example: CreateSessionLog`

The action that you want to perform. Value: CreateSessionLog.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|KLz0ir">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|1IRGPn">必选</span> `Example: ngw-123456****`

The NAT instance ID in the session log for retrieving log information

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) API to query the NAT gateway ID.



**SessionLogName ** <span data-label="purple">string </span>`optional` `Example: ngw-SessionLog`

The name of the session log.


* Must start with a letter, number or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.



**Description ** <span data-label="purple">string </span>`optional` `Example: this is log`

The description of the session log.


* Must start with a letter, number or Chinese character. May include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 255 characters in length.

* If left blank, this parameter defaults to an empty string.



**TlsProjectName ** <span data-label="purple">string </span><span data-api-tag="require|cXDEC2">必选</span> `Example: TLS-project`

The name of the log project.


* May include lowercase letters, numbers, and hyphens (\-).

* Must start and end with a lowercase letter or a number.

* Must be 3 to 63 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a log project with the specified name does not exist in Torch Log Service (TLS), it will be created automatically.</div>




**TlsTopicName ** <span data-label="purple">string </span><span data-api-tag="require|l8DIHl">必选</span>`Example: TLS-topic`

The name of the log topic.


* May include lowercase letters, numbers, and hyphens (\-).

* Must start or end with a lowercase letter or a number.

* Must be 3 to 63 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a log topic with the specified name does not exist in the log project, it will be created automatically.</div>




**EnableTlsTopicIndex ** <span data-label="purple">boolean </span>`optional` `Example: false`

Specify whether to enable log index. Values:


* true: Yes.

* false (default): No.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**SessionLogId ** <span data-label="purple">string </span>`Example: nsl-273w1s2v5xnuo7fap8t8****`

The ID of the NAT session log instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateSessionLog&Version=2020-04-01&SessionLogName=ngw-SessionLog&NatGatewayId=ngw-123456****&TlsProjectName=TLS-project&TlsTopicName=TLS-topic HTTP/1.1
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
        "Action": "CreateSessionLog",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "SessionLogId": "nsl-273w1s2v5xnuo7fap8t8****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidSessionLog.InvalidNatArch |The specified NAT gateway is not in the correct arch for the request. |The specified NAT gateway cannot respond to this request. |
|400 |InvalidSessionLog.InvalidNatGateway |The specified NAT gateway already has a session log instance. |The specified NAT gateway already has a session log instance. |
|400 |InvalidSessionLog.NotSupport |The specified region does not support nat session log. |The NAT session log feature is not supported in this specified region. |
|400 |InvalidParameter.TlsTopicTaggedByOtherService |The specified tls topic already tagged by other service. |The specified TLS log topic for the NAT session log is already associated with the tag from other, non\-NAT services. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|401 |InvalidOperation.NoPermission |The current service is not allowed to do this operation. |The current service is not authorized. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
