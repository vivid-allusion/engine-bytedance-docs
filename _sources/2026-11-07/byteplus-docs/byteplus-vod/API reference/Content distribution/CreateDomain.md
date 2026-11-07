---
title: "CreateDomain"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-createdomain"
---

This interface is used to select the domain category and origin type, and create a domain under the specified space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=CreateDomain&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateDomain` |The API action. For the current API, the value is `CreateDomain`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test-space` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Space](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus VOD console.<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|DomainType |String |Yes |`play` |Domain category. The values are as follows:<br><br><br>* `play`: The play domain.<br><br>* `image`: The cover domain. |
|Domain |String |Yes |`example.test.com` |The domain name. The domain name rules are as follows:<br><br><br>* Supports exact domain names.<br><br>* Does not support adding wildcard domains, such as `*.vod.com`.<br><br>* Does not support uppercase.<br><br>* Does not support duplicate domain names. |
|SourceStationType |Integer |Yes |`2` |The type of the origin server. The values are as follows:<br><br><br>* `1`: The VOD origin server.<br><br>* `2`: The custom origin server. |
|SourceStationAddressType |Integer |No |`1` |The origin site address type. The values are as follows:<br><br><br>* `1`: Domain type origin.<br><br>* `2`: IP type origin.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <code>SourceStationType</code> parameter value is 2 (custom origin acceleration domain), this parameter is required.</div><br> |
|Origins |String |No |`www.test.com` |The list of origin sites. Multiple entries should be separated by commas.<br><br><br>* For the domain type origin: Only one is allowed.<br><br>* For the IP type origin: No more than 10 are allowed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <code>SourceStationType</code> parameter is set to <code>2</code> (custom origin acceleration domain), this parameter is mandatory.</div><br> |
|Area |String |Yes |`cn` |The acceleration region. Supported values:<br><br><br>* `cn`: Chinese mainland.<br><br>* `overseas`: Non\-Chinese mainland.<br><br>* `global`: Global. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=CreateDomain&Version=2023-01-01&SpaceName=test-space&DomainType=play&Domain=example.test.com&SourceStationType=2&Area=cn
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateDomain",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|403 |RequestForbidden.AccessIsRestricted |\- |The account access is restricted. |


#{.custom\-md\-table\-4}#

&nbsp;
