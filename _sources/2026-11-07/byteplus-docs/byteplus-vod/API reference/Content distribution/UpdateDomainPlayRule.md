---
title: "UpdateDomainPlayRule"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatedomainplayrule"
---

This interface is used to set the distribution rules for the domain name in the specified space.

<span id="requirements"></span>
## Requirements

Data delay: Effective within 5 minutes.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateDomainPlayRule&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateDomainPlayRule` |The API action. For the current API, the value is `UpdateDomainPlayRule`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The space name. You can call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|DefaultDomain |String |Yes |`example.vod.com` |The default domain name. You can obtain the list of all domain names under the current space account through the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface. The rules for the domain name are as follows:<br><br><br>* Supports precise domain names.<br><br>* Does not support adding wildcard domain names, such as `*.vod.com`.<br><br>* Does not support uppercase.<br><br>* Does not support duplicate domain names. |
|PlayRule |Integer |Yes |`1` |The mode category. The values are as follows:<br><br><br>* `0`: Random mode.<br><br>* `1`: Default domain name mode. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateDomainPlayRule&Version=2023-01-01&SpaceName=test&DefaultDomain=example.vod.com&PlayRule=1
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateDomainPlayRule",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
