---
title: "ListMirrorSrcRule"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listmirrorsrcrule"
---

Query the list of image mirror source rules (mirroring\-based back\-to\-origin rules) in a specified VOD space. The `Id` parameter can be used to precisely query a specific rule.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListMirrorSrcRule&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListMirrorSrcRule` |The API action. For the current API, the value is `ListMirrorSrcRule`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |Yes |`my-space` |The name of the space to query for mirror source rules. |
|Id |String |No |`06d0499eedf84f4e9b4064442fc59993` |The ID of the image source rule. If not provided, all rules under this space will be returned. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Rule |Array of [MirrorSrcRule](https://docs.byteplus.com/en/docs/25/47190#mirrorsrcrule) |`-` |The list of mirror source rules, each containing details about the rule's configuration and conditions. |


#{.custom\-md\-table\-4}#

<span id="mirrorsrcrule"></span>
### MirrorSrcRule


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |String |`06d0499eedf84f4e9b4064442fc59993` |The ID of the mirror source rule. |
|Enabled |Boolean |`true` |Whether the mirror source rule is enabled. |
|Condition |Object of [MirrorSrcCondition](https://docs.byteplus.com/en/docs/25/47190#mirrorsrccondition) |`-` |The conditions that trigger the mirror source rule. |
|CreatedAt |Long |`1747908332` |The timestamp when the mirror source rule was created, represented in Unix epoch time format. |
|UpdatedAt |Long |`1747908332` |The timestamp when the mirror source rule was last updated, represented in Unix epoch time format. |
|OriginType |Integer |`1` |The type of the origin station, with the following possible values. This field is required when creating a new rule.<br><br><br>* `1`: Amazon S3. |
|PublicSource |Object of [PublicSourceConf](https://docs.byteplus.com/en/docs/25/47190#publicsourceconf) |`-` |The third\-party source station information. This field is required when creating a new rule. |


#{.custom\-md\-table\-4}#

<span id="mirrorsrccondition"></span>
### MirrorSrcCondition


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AllowHost |Array of String |`["abc.test.com"]` |The domain names of the VOD cover images. Multiple domain names are allowed for a single rule, but each domain name can only be associated with one rule. This field is required when creating a new rule. |
|KeyPrefix |String |`a/b` |The prefix of the image file being accessed. |
|KeySuffix |String |`.jpeg` |The suffix of the image file being accessed. |


#{.custom\-md\-table\-4}#

<span id="publicsourceconf"></span>
### PublicSourceConf


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|S3 |Object of [MirrorSrcS3Conf](https://docs.byteplus.com/en/docs/25/47190#mirrorsrcs3conf) |`-` |The S3 bucket configuration for the third\-party source station. |


#{.custom\-md\-table\-4}#

<span id="mirrorsrcs3conf"></span>
### MirrorSrcS3Conf


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Bucket |String |`test-bucket` |The S3 bucket name. |
|Region |String |`ap-southeast-1` |The S3 region. |
|Endpoint |String |`s3.ap-southeast-1.amazonaws.com` |The S3 endpoint. |
|AccessKey |String |`AK******************` |The S3 access key. |
|SecretKey |String |`*****` |The S3 secret key. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListMirrorSrcRule&Version=2023-07-01&SpaceName=my-space&Id=06d0499eedf84f4e9b4064442fc59993
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListMirrorSrcRule",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-07-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Rule": [
            {
                "Id": "06d0499eedf84f4e9b4064442fc59993",
                "Enabled": true,
                "Condition": {
                    "AllowHost": [
                        "abc.test.com"
                    ],
                    "KeyPrefix": "a/b",
                    "KeySuffix": ".jpeg"
                },
                "CreatedAt": 1747908332,
                "UpdatedAt": 1747908332,
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
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
