---
title: "AddCallbackSubscription"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-addcallbacksubscription"
---

This interface is used to add the callback subscription address.

<span id="usage-scenario"></span>
## Usage scenario

For a list of VOD callback mechanisms and events, see [Event Notification](https://docs.byteplus.com/en/docs/byteplus-vod/docs-callback-notification).

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=AddCallbackSubscription&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`AddCallbackSubscription` |The API action. For the current API, the value is `AddCallbackSubscription`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The Video on Demand (VOD) space name. The space name can be obtained in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD control panel [Spaces](https://console.byteplus.com/vodpaas/overview/).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|Url |String |Yes |`https://example.com` |Subscribe to the URL to which the BytePlus VOD server sends the callback.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The URL must begin with <code>http://</code> or <code>https://</code>.</div><br> |
|ContentType |String |No |`application/octet-stream` |The content type of the subscription address. Supported values:<br><br><br>* (Default) `application/octet-stream`<br><br>* `application/json` |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=AddCallbackSubscription&Version=2023-01-01&SpaceName=test&Url=https://example.com&ContentType=application/octet-stream
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "AddCallbackSubscription",
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
