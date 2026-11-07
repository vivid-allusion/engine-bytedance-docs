---
title: "CreateDirectConnectConnectionOrder - Creating a payment order for a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectConnectionOrder"
---

Call CreateDirectConnectConnectionOrder to create a payment order for a Direct Connect (DC) Connection resource.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API can only be called to create a payment order for a DC Connection that is in the "Pending payment" status.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectConnectionOrder&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|EJdxrN">必选</span> `Example: CreateDirectConnectConnectionOrder`

The interface name. The current API name is `CreateDirectConnectConnectionOrder`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|y0ZrzA">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|rW6lKz">必选</span> `Example: dcc-8njk2nl32bd232b****`

The ID of the DC Connection. You can call [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) to query the DC Connection ID.



**PeriodUnit ** <span data-label="purple">String </span>`optional` `Example: Month`

The purchased duration unit of the port resource for the DC Connection.


* Month (default): Subscribing by month.

* Year: Subscribing by year.



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The purchased duration of the port resource for the DC Connection.


* If `PeriodUnit` is set to `Year`, valid values for this parameter are 1, 2, and 3.

* If `PeriodUnit` is set to `Month`, valid values for this parameter are 1 through 11.

* If not specified, it defaults to 1.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-BHLJK9832544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderNumber ** <span data-label="purple">String </span>`Example: Order71606759118820*****`

The order number.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectConnectionOrder&Version=2020-04-01&DirectConnectConnectionId=dcc-8njk2nl32bd232b****&Period=1&PeriodUnit=Month' HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20220627103212010225145152058*****",
        "Action": "CreateDirectConnectConnectionOrder",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220627103212010225145152058*****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |The creation of the configuration order failed. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|404 |InvalidEip.GetInstanceDetail |Get instance detail failed. |Failed to obtain instance information. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
