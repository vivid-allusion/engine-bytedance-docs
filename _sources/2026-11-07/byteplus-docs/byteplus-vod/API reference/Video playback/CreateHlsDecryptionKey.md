---
title: "CreateHlsDecryptionKey"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/createhlsdecryptionkey"
---

Call `CreateHlsDecryptionKey` to create the HLS standard encryption key.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=CreateHlsDecryptionKey&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateHlsDecryptionKey` |The API action. For the current API, the value is `CreateHlsDecryptionKey`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |No |`test` |The space name. You can call [ListSpace](https://www.volcengine.com/docs/4/107686)t o obtain information about all the spaces under the current account. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Ak |String |`68270ce05***7a7d6e4592b60052559a` |The key ID |
|IsBase64 |Boolean |`false` |Indicates whether the `SecretKey` has been encoded using Base64. If `true`, the `SecretKey`is already Base64\-encoded; otherwise, it is in plaintext. |
|KeyFormat |String |`binary` |Specifies the format of the real key. The supported formats are as follows.<br><br><br>* `binary`: the binary key;<br><br>* Default: the string. |
|SecretKey |String |`e9655b6b8***46f19dcda614ae0959df` |The plaintext key |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=CreateHlsDecryptionKey&Version=2023-07-01&SpaceName=test
```


<span id="Sample response"></span>
### Sample response

```json
{
    "Result": {
        "Ak": "68270ce05***7a7d6e4592b60052559a",
        "IsBase64": false,
        "KeyFormat": "binary",
        "SecretKey": "e9655b6b8***46f19dcda614ae0959df"
    },
    "ResponseMetadata": {
        "Action": "CreateHlsDecryptionKey",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-07-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
