---
title: "ModifyCenAttributes - Modify the specified Cloud Enterprise Network instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/ModifyCenAttributes"
---

Call the ModifyCenAttributes interface to update the Cloud Enterprise Network instance information.

<span id=".5L2_55So6K-05piO"></span>
## Notes

Following optional parameters retain their existing configurations if not explicitly specified.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyCenAttributes&groupName=%E4%BA%91%E4%BC%81%E4%B8%9A%E7%BD%91%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|3zcWzV">必选</span> `example value: ModifyCenAttributes`

The action to perform. Value: ModifyCenAttributes.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**CenName ** <span data-label="purple">string </span>`optional` `Example value: cen-test`

Name of the CEN instance.


* The name must start with a letter, number, or Chinese character. It may contain letters, numbers, Chinese characters, periods ( . ), underscores ( _ ), and hyphens ( \- ).

* Must be 1 to 128 characters.



**Description ** <span data-label="purple">string </span>`optional` `Example: ThisIsASampleDescription`

Description of the CEN instance.


* The description must start with a letter, number, or Chinese character. It may contain letters, numbers, Chinese characters, and the following special characters: half\-width commas ( , ), half\-width periods ( . ), underscores ( _ ), spaces, equal signs ( = ), hyphens ( \- ), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Must be 0 to 255 characters.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|GWQYM0">必选</span> `Example value: cen-7qthudw0ll6jmc****`

ID of the CEN instance.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) interface to query the CEN instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifyCenAttributes&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083942Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151650051591860442139DB41D",
    "Action": "ModifyCenAttributes",
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
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified Cloud Enterprise Network (CEN) instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified Cloud Enterprise Network (CEN) instance state cannot respond to this request. Try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
