---
title: "ModifyHaVipAttributes - Modifying a HaVip"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyHaVipAttributes"
---

Call the ModifyHaVipAttributes API to modify the name and description of the high\-availability virtual IP address (HAVIP).

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Following optional parameters retain their existing configurations if not explicitly specified.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyHaVipAttributes&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|PRmTAQ">必选</span> `Example value: ModifyHaVipAttributes`

The interface name. Current API name is `ModifyHaVipAttributes`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|EpEoAI">必选</span> `Example value: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**HaVipId ** <span data-label="purple"> String  </span><span data-api-tag="require|z4VIt4">必选</span> `Example value: havip-2zeo05qre24nhrqp****`

ID of the HAVIP to modify.

You can call the [DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) API to query the ID of the High\-Availability Virtual IP Address.



**HaVipName ** <span data-label="purple"> String </span>`optional` `Example value: havip-1`

Name of HAVIP.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).



**Description ** <span data-label="purple"> String </span>`optional` `Example value: This is my HaVip.`

Description of HAVIP.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: F3CD6886-D8D0-4FEE-B93E-1B732396****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyHaVipAttributes&Version=2020-04-01&HaVipId=havip-2zeo05qre24nhrqp****&Description=This is my HaVip.&HaVipName=havip-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyHaVipAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B732396****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidHaVip.InvalidStatus |The specified HaVip is not in the correct status for the request. |The specified HAVIP is in a state that cannot respond to this request. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|404 |InvalidHaVip.NotFound |The specified HaVip does not exist. |The specified HAVIP does not exist. |
