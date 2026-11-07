---
title: "AddDomainToScheduler"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-adddomaintoscheduler"
---

This interface is used to add the domain to the VOD CDN service by selecting the domain type and the origin type in the specified space.

<span id="requirements"></span>
## Requirements


* Prerequisite: You need to call the [StartDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startdomain) interface to enable the domain and add the domain to the video on demand scheduling before it can be played.

* Data latency: Takes effect within 5 minutes.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=AddDomainToScheduler&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`AddDomainToScheduler` |The API action. For the current API, the value is `AddDomainToScheduler`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Space](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus VOD console.<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|DomainType |String |Yes |`play` |The domain type. The values are as follows:<br><br><br>* `play`: The play domain.<br><br>* `image`: The cover domain. |
|Domain |String |Yes |`example.vod.com` |The domain name. You can obtain the list of all domain names under the current space account through the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface. The rules for the domain names are as follows:<br><br><br>* Supports precise domain names.<br><br>* Does not support adding wildcard domain names, such as `*.vod.com`.<br><br>* Does not support uppercase.<br><br>* Does not support duplicate domain names. |
|SourceStationType |Integer |Yes |`1` |The type of the origin site. The values are as follows:<br><br><br>* `1`: The VOD origin site.<br><br>* `2`: The custom origin site. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=AddDomainToScheduler&Version=2023-01-01&SpaceName=test&DomainType=play&Domain=example.vod.com&SourceStationType=1
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "AddDomainToScheduler",
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
