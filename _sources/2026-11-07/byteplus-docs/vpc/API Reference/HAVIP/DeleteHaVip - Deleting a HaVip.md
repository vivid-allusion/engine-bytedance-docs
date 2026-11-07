---
title: "DeleteHaVip - Deleting a HaVip"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteHaVip"
---

Call the DeleteHaVip API to delete the specified high\-availability virtual IP address (HAVIP).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteHaVip&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|uEm3dv">必选</span> `Example value: DeleteHaVip`

The interface name. The current API name is `DeleteHaVip`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|9Ue-yx">必选</span>`Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**HaVipId ** <span data-label="purple"> String </span><span data-api-tag="require|8jOG3u">必选</span> `Example value: havip-2zeo05qre24nhrqpy****`

The ID of the High\-Availability Virtual IP Address to be deleted.

You can call the [DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) API to query the ID of the High\-Availability Virtual IP Address.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: F3CD6886-D8D0-4FEE-B93E-1B732396****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteHaVip&Version=2020-04-01&HaVipId=havip-2zeo05qre24nhrqpy**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B732396C8****",
        "Action": "DeleteHaVip",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B732396C8****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidHaVip.InUse |The specified HaVip is in use. If you are trying to delete this HaVip, ensure that it is disassociated with elastic IP. |The specified High\-Availability Virtual IP Address is currently in use. If you attempt to delete this HAVIP, please first disassociate it from any Elastic IP (EIP). |
|400 |InvalidHaVip.InUse |The specified HaVip is in use. If you are trying to delete this HaVip, ensure that it is not referenced by route entry. |The specified High\-Availability Virtual IP Address is currently in use. If you attempt to delete this HAVIP, please first remove it from all routing entries. |
|400 |InvalidHaVip.InvalidStatus |The specified HaVip is not in the correct status for the request. |The specified high availability virtual IP address is in a status that cannot respond to this request. |
|400 |InvalidHaVip.NotSupport |The specified HaVip does not support this operation |The specified HAVIP does not support this operation. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified elastic network interface does not exist. |
|404 |InvalidHaVip.NotFound |The specified HaVip does not exist. |The specified high\-availability virtual IP does not exist. |
