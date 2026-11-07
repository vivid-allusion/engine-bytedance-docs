---
title: "DeleteCenServiceRouteEntry - delete a specified cloud service access route"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DeleteCenServiceRouteEntry"
---

Call the DeleteCenServiceRouteEntry interface to delete a specified cloud service access route.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCenServiceRouteEntry&groupName=%E4%BA%91%E6%9C%8D%E5%8A%A1%E8%AE%BF%E9%97%AE&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|prd45I">必选</span> `example value: DeleteCenServiceRouteEntry`

The action to perform, value: DeleteCenServiceRouteEntry.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|cTGqGm">必选</span> `Example value: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) interface to get the CEN instance ID.



**DestinationCidrBlock ** <span data-label="purple">string </span><span data-api-tag="require|stPvMZ">必选</span> `Example value: 100.XX.XX.0/24`

The deployed address of the cloud service must belong to `100.64.0.0/10` or `fd00:64::/32` CIDR block.



**ServiceRegionId ** <span data-label="purple">string </span><span data-api-tag="require|Uy8JLZ">必选</span> `Example value: cn-beijing`

The Region of cloud service.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteCenServiceRouteEntry&Version=2020-04-01&CenId=cen-2nim00ybaylts7trquyzt****&DestinationCidrBlock=100.XX.XX.0%2F24&ServiceRegionId=cn-beijing HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082549Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151638470091802381035CD819",
    "Action": "DeleteCenServiceRouteEntry",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|404 |InvalidServiceRouteEntry.NotFound |The specified service route entry does not exist. |The specified cloud service access route does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified Cloud Enterprise Network (CEN) instance is in a state that cannot respond to this request. Try again later. |
|409 |InvalidServiceRouteEntry.InvalidStatus |The specified CEN service route is not in the correct status for the request. |The specified Cloud Service route is in a state that cannot respond to this request. Try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
