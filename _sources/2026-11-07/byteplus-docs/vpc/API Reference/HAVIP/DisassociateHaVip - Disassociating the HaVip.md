---
title: "DisassociateHaVip - Disassociating the HaVip"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DisassociateHaVip"
---

Call the DisassociateHaVip API to detach the High\-Availability Virtual IP Address (HAVIP) from the Elastic Compute Service instance or network interface.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisassociateHaVip&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|ee4Yhv">必选</span> `Example value: DisassociateHaVip`

The interface name. The current API name is `DisassociateHaVip`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|HkaCvI">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**HaVipId ** <span data-label="purple"> String  </span><span data-api-tag="require|faI152">必选</span> `Example: havip-2zeo05qre24nhrqpy****`

The ID of the HAVIP to be unbound.

You can call the [DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) API to query the ID of the High\-Availability Virtual IP.



**InstanceType ** <span data-label="purple"> String </span>`optional` `Example value: EcsInstance`

The instance type from which to unbind the HAVIP.


* EcsInstance: Elastic Compute Service instance

* NetworkInterface: Network interface



**InstanceId ** <span data-label="purple"> String  </span><span data-api-tag="require|bj6apF">必选</span> `Example: i-faf344422ffsfad****`

The ID of the instance from which to unbind the HAVIP.

You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) or [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the ECS instance ID or the network interface ID.



**ClientToken ** <span data-label="purple">String</span> `optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example: 473469C7-AA6F-4DC5-B3DB-A3DC0DE3****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DisassociateHaVip&Version=2020-04-01&HaVipId=havip-2zeo05qre24nhrqpy****&InstanceId=i-faf344422ffsfad****&InstanceType=EcsInstance HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3****",
        "Action": "DisassociateHaVip",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidHaVip.InstanceMismatch |The specified HaVip and instance are not associated. |The specified HAVIP and instance are not bound. |
|400 |InvalidHaVip.InvalidStatus |The specified HaVip is not in the correct status for the request. |The specified High\-Availability Virtual IP Address is in a state that cannot respond to this request. |
|400 |InvalidHaVip.NotSupport |The specified HaVip does not support this operation |The specified HAVIP does not support this operation. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|404 |InvalidHaVip.NotFound |The specified HaVip does not exist. |The specified High\-Availability Virtual IP Address does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
