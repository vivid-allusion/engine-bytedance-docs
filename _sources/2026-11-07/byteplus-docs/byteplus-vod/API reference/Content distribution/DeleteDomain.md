---
title: "DeleteDomain"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deletedomain"
---

This interface is used to delete specified domains under different types within the designated space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteDomain&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteDomain` |The API action. For the current API, the value is `DeleteDomain`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Space](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus VOD console.<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|DomainType |String |Yes |`play` |The domain type. The values are as follows:<br><br><br>* `play`: The play domain.<br><br>* `image`: The cover domain. |
|Domain |String |Yes |`example.vod.com` |The domain name. You can obtain the list of all domain names under the current space account through the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface. The rules for the domain name are as follows:<br><br><br>* Supports exact domain names.<br><br>* Does not support adding wildcard domain names, such as `*.vod.com`.<br><br>* Does not support uppercase.<br><br>* Does not support duplicate domain names. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DeleteDomain&Version=2023-01-01&SpaceName=test&DomainType=play&Domain=example.vod.com
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteDomain",
        "Version": "2023-01-01",
        "Service": "vod",
        "Region": "ap-singapore-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
