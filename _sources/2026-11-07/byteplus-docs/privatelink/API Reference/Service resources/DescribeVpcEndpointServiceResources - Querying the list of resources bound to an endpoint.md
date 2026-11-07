---
title: "DescribeVpcEndpointServiceResources - Querying the list of resources bound to an endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceResources"
---

Call the DescribeVpcEndpointServiceResources API to query the service resources bound to a specified endpoint service.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointServiceResources&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|o59bYi">必选</span> `Example: DescribeVpcEndpointServiceResources`

Action to execute. Set the value to **DescribeVpcEndpointServiceResources**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|BjEQ7Y">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple"> String </span><span data-api-tag="require|2jiPp_">必选</span>`Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer </span>`optional` `Example: 10`

The number of entries per page in a pagination query. Maximum: 100. Default: 10.



**ZoneId ** <span data-label="purple"> String </span>`optional` `Example: cn-guangzhou-a`

ID of the Availability Zone where the service resource provides its service.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is not supported when querying service resources of the RDS type.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**PageNumber ** <span data-label="purple"> Integer  </span>`optional` `Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 10`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple"> Integer </span>`optional` `Example: 2`

Total number of qualified service resources that meet the conditions.



**Resources ** <span data-label="purple"> Object[] </span>`optional` `Example value: -`

Details of the service resource.


**ResourceId ** <span data-label="purple"> String  </span>`optional` `Example: clb-bp1o94dp5i6ea****`

Service resource ID.



**ResourceType ** <span data-label="purple"> String </span>`optional` `Example: CLB`

Service resource type.


* CLB: Classic Load Balancer.

* ALB: Application Load Balancer.

* RDSMySQL: Cloud Database MySQL Edition.



**ZoneId ** <span data-label="purple"> String </span>`optional` `Example: cn-guangzhou-a`

ID of the Availability Zone to which the service resource belongs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter returns a null value when the ResourceType parameter returns <strong>RDSMySQL</strong>.</div>




**ResourceAutoAllocated ** <span data-label="purple"> Object[] </span>`optional` `Example: --`

Details about the auto\-assign of the service resource.


**AutoAllocatedEnabled ** <span data-label="purple"> Boolean </span>`optional` `Example: true`

Enable Auto\-assign.


* true: Yes

* false: No



**ZoneId ** <span data-label="purple"> String </span>`optional` `Example: cn-guangzhou-a`

Availability zone ID.





<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeVpcEndpointServiceResources&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
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
        "Action": "DescribeVpcEndpointServiceResources",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "Resources": [
            {
                "ZoneId": "cn-guangzhou-a",
                "ResourceId": "clb-bp1o94dp5i6ea****",
                "ResourceType": "CLB",
                "ResourceAutoAllocated": [
                    {
                        "ZoneId": "cn-guangzhou-a",
                        "AutoAllocatedEnabled": true
                    }
                ]
            }
        ],
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
|400 |ErrInterfaceNotSupportedResourceType |The Interface does not support the resource type. |The endpoint service API does not support this service resource type. |
|400 |InvalidZoneID.Malformed |The specified ZoneID is malformed. |The specified ZoneID parameter format is invalid. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
