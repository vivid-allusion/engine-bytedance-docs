---
title: "SetMirrorSrcRule"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-setmirrorsrcrule"
---

Create or update the image mirror source rule (mirroring\-based back\-to\-origin rule) for a BytePlus VOD space. By configuring a mirroring back\-origin rule, when a requested resource is not found, the system will automatically retrieve the resource from the specified origin server and store it in the current service. Subsequent requests can then be served directly from BytePlus VOD service.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=SetMirrorSrcRule&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`SetMirrorSrcRule` |The API action. For the current API, the value is `SetMirrorSrcRule`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |Yes |`my-sapce` |The VOD space name. |
|Id |String |No |`06d0499eedf84f4e9b4064442fc59993` |The ID of the mirror source rule. If not provided, a new rule will be created. If provided, the existing rule with the specified ID will be updated. |
|MirrorSrcRule |Object of [MirrorSrcRule](https://docs.byteplus.com/en/docs/25/47189#mirrorsrcrule) |Yes |`-` |The mirror source rule configuration. |


#{.custom\-md\-table\-5}#

<span id="mirrorsrcrule"></span>
### MirrorSrcRule


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enabled |Boolean |No |`true` |Whether the mirror source rule is enabled. |
|Condition |Object of [MirrorSrcCondition](https://docs.byteplus.com/en/docs/25/47189#mirrorsrccondition) |No |`-` |The conditions that trigger the mirror source rule. |
|OriginType |Integer |No |`1` |The type of the origin station, with the following possible values. This field is required when creating a new rule.<br><br><br>* `1`: Amazon S3. |
|PublicSource |Object of [PublicSourceConf](https://docs.byteplus.com/en/docs/25/47189#publicsourceconf) |No |`-` |The third\-party source station information. This field is required when creating a new rule. |


#{.custom\-md\-table\-5}#

<span id="mirrorsrccondition"></span>
### MirrorSrcCondition


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AllowHost |Array of String |No |`["abc.test.com"]` |The domain names of the VOD cover images. Multiple domain names are allowed for a single rule, but each domain name can only be associated with one rule. This field is required when creating a new rule. |
|KeyPrefix |String |No |`a/b` |The prefix of the image file being accessed. |
|KeySuffix |String |No |`.jpeg` |The suffix of the image file being accessed. |


#{.custom\-md\-table\-5}#

<span id="publicsourceconf"></span>
### PublicSourceConf


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|S3 |Object of [MirrorSrcS3Conf](https://docs.byteplus.com/en/docs/25/47189#mirrorsrcs3conf) |No |`-` |The S3 bucket configuration for the third\-party source station. |


#{.custom\-md\-table\-5}#

<span id="mirrorsrcs3conf"></span>
### MirrorSrcS3Conf


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Bucket |String |No |`test-bucket` |The S3 bucket name. |
|Region |String |No |`ap-southeast-1` |The S3 region. |
|Endpoint |String |No |`s3.ap-southeast-1.amazonaws.com` |The S3 endpoint. |
|AccessKey |String |No |`AK******************` |The S3 access key. |
|SecretKey |String |No |`*****` |The S3 secret key. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |String |`06d0499eedf84f4e9b4064442fc59993` |The ID of the mirror source rule. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=SetMirrorSrcRule&Version=2023-07-01
{
    "SpaceName": "my-sapce",
    "Id": "06d0499eedf84f4e9b4064442fc59993",
    "MirrorSrcRule": {
        "Enabled": true,
        "Condition": {
            "AllowHost": [
                "abc.test.com"
            ],
            "KeyPrefix": "a/b",
            "KeySuffix": ".jpeg"
        },
        "OriginType": 1,
        "PublicSource": {
            "S3": {
                "Bucket": "test-bucket",
                "Region": "ap-southeast-1",
                "Endpoint": "s3.ap-southeast-1.amazonaws.com",
                "AccessKey": "AK******************",
                "SecretKey": "*****"
            }
        }
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "SetMirrorSrcRule",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-07-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Id": "06d0499eedf84f4e9b4064442fc59993"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
