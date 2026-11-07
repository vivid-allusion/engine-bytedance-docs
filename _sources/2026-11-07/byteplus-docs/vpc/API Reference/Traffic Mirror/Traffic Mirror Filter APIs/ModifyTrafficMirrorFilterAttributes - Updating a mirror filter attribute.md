---
title: "ModifyTrafficMirrorFilterAttributes - Updating a mirror filter attribute"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterAttributes"
---

Call the ModifyTrafficMirrorFilterAttributes API to modify the traffic mirror filter.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Following optional parameters retain their existing configurations if not explicitly specified.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTrafficMirrorFilterAttributes&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|S19tRF">必选</span> `Example value: ModifyTrafficMirrorFilterAttributes`

The interface name. The current API name is `ModifyTrafficMirrorFilterAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|sk5Mnp">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TrafficMirrorFilterId ** <span data-label="purple"> String </span><span data-api-tag="require|qUMjuk">必选</span> `Example value: tmf-bp1opxu1zkhn00123****`

ID of the traffic mirror filter.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the traffic mirror filter ID.



**TrafficMirrorFilterName ** <span data-label="purple"> String </span>`optional` `Example value: TM_Filter_1`

Name of the traffic mirror filter.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).



**Description ** <span data-label="purple">String </span>`optional` `Example value: TM_Filter_1_Description`

Description of the traffic mirror filter.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTrafficMirrorFilterAttributes&Version=2020-04-01&TrafficMirrorFilterId=tmf-bp1opxu1zkhn00123****&TrafficMirrorFilterName=TM_Filter_1 HTTP/1.1
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
        "Action": "ModifyTrafficMirrorFilterAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTrafficMirrorFilter.InvalidStatus |The specified traffic mirror filter is not in the correct status for the request. |The specified traffic mirror filter is in a state that cannot process this request. |
|404 |InvalidTrafficMirrorFilter.NotFound |The specified traffic mirror filter does not exist. |The specified traffic mirror filter does not exist. |
