---
title: "DescribeVpcEndpointServicePermissions - Querying the list of allowlist accounts for an endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicePermissions"
---

Call the DescribeVpcEndpointServicePermissions API to query the authorized allowlist accounts for a specified endpoint service.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointServicePermissions&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|Nygz0Y">必选</span> `Example: DescribeVpcEndpointServicePermissions`

Action to execute. Set the value to **DescribeVpcEndpointServicePermissions**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|oPGzb7">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple"> String </span><span data-api-tag="require|12unJ5">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to obtain the ID of the Endpoint service.



**PermitAccountId ** <span data-label="purple"> String  </span>`optional` `Example: 2100000000`

Account ID of the allowlist.

You can call the DescribeVpcEndpoints API to query the ID of the account to which the endpoint belongs.



**PageNumber ** <span data-label="purple"> Integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 10`

The number of entries per page in a pagination query. Maximum: 100. Default: 10.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer </span>`optional` `Example: 10`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple"> Integer </span>`optional` `Example: 2`

The total number of authorized allowlist accounts that meet the conditions.



**Permissions ** <span data-label="purple"> Object[] </span>`optional` `Example: -`

The detailed information of the authorized allowlist accounts.


**PermitAccountId ** <span data-label="purple"> String  </span>`optional` `Example: 2100000000`

The ID of an authorized allowlist account.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeVpcEndpointServicePermissions&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcEndpointServicePermissions",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "Permissions": [
            {
                "PermitAccountId": "2100000000"
            }
        ],
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format of specified pagination parameter is invalid. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
