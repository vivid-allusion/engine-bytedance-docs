---
title: "DescribeDirectConnectAccessPoints - Querying information about DC access points."
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints"
---

Call DescribeDirectConnectAccessPoints to query information about Direct Connect (DC) access points.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectAccessPoints&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|4JkjtB">必选</span> `Example: DescribeDirectConnectAccessPoints`

The interface name. The current API name is `DescribeDirectConnectAccessPoints`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|OhZ6Cd">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectAccessPointIds.N ** <span data-label="purple">String </span>`optional` `Example: ap-cn-shanghai-***-A`

The ID of the DC access point to be queried.


* N represents the sequence number of a DC access point ID. You can call a maximum of 100 IDs per request.

* Separate multiple IDs with ampersands (&).

* If not provided, the information about all access points is queried by default.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number for pagination query.


* Set this parameter to a non\-negative integer.

* If left blank or set to 0, it defaults to 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

Total number of the qualified DC access points.



**DirectConnectAccessPoints ** <span data-label="purple">Object[] </span>`Example: -`

The details of the DC access point.


**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the DC access point.


* Available

* Unavailable



**Location ** <span data-label="purple">String </span>`Example: Wanguo, Langfang City, Hebei Province`

The physical location of the DC access point.



**Description ** <span data-label="purple">String </span>`Example: China Mobile access point`

The description of the DC access point.



**LineOperators ** <span data-label="purple">String[] </span>`Example: ChinaTelecom`

The line operator who supports the DC access point.


* ChinaTelecom: China Telecom

* ChinaMobile: China Mobile

* ChinaUnicom: China Unicom

* ChinaOther: Other line operators in China with the corresponding telecommunications business operating license.



**DirectConnectAccessPointId ** <span data-label="purple">String </span>`Example: ap-cn-shanghai-***-A`

The ID of the DC access point.



**DirectConnectAccessPointName ** <span data-label="purple">String </span>`Example: LFWG`

The name of the DC access point.



**DirectConnectAccessPointAlias ** <span data-label="purple">String </span>`Example: AP-LangFangWanGuo`

The English name of the DC access point location.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectAccessPoints&Version=2020-04-01&PageNumber=1&PageSize=20&DirectConnectAccessPointIds=ap-cn-beijing-*** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectAccessPoints",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectAccessPoints": [
            {
                "Status": "Available",
                "Location": "Wanguo, Langfang City, Hebei Province",
                "Description": "China Mobile access point",
                "LineOperators": [
                    "ChinaTelecom"
                ],
                "DirectConnectAccessPointId": "ap-cn-shanghai-***-A",
                "DirectConnectAccessPointName": "LFWG",
                "DirectConnectAccessPointAlias": "AP-LangFangWanGuo"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.DirectConnectAccessPointId |You've reached the limit on the number of direct connect access point IDs that you can describe. |You have reached the maximum number of DC access points that can be queried. |
