---
title: "DeleteTrafficMirrorFilter - Deleting a filter instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilter"
---

Call the DeleteTrafficMirrorFilter API to delete the Traffic Mirror Filter.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The traffic mirror filter is not associated with any traffic mirror session. If already associated, [Delete Traffic Mirror Session](https://docs.byteplus.com/en/docs/vpc/Managing-traffic-mirror-filter#.5Yig6Zmk562b6YCJ5p2h5Lu2).

* DeleteTrafficMirrorFilter is an asynchronous API; when a request ID is returned, the system is still configuring in the background. You can call [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to check the filter status. Deleting indicates deletion in progress; Query failed means deletion is complete.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTrafficMirrorFilter&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|7FWgR8">必选</span> `Example value: DeleteTrafficMirrorFilter`

The interface name. The current API name is `DeleteTrafficMirrorFilter`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|VoC1kQ">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TrafficMirrorFilterId ** <span data-label="purple"> String </span><span data-api-tag="require|GNLNkn">必选</span> `Example value: tmf-bp1opxu1zkhn00123****`

ID of the Traffic Mirror Filter.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the Traffic Mirror Filter ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteTrafficMirrorFilter&Version=2020-04-01&TrafficMirrorFilterId=tmf-bp1opxu1zkhn00123**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteTrafficMirrorFilter",
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
|400 |InvalidTrafficMirrorFilter.InUse |The specified traffic mirror filter is in use. |The specified Traffic Mirror Filter is currently in use. |
|404 |InvalidTrafficMirrorFilter.NotFound |The specified traffic mirror filter does not exist. |The specified Traffic Mirror Filter does not exist. |
