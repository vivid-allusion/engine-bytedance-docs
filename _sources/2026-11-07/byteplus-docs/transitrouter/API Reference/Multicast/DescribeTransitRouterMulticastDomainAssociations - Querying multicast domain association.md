---
title: "DescribeTransitRouterMulticastDomainAssociations - Querying multicast domain association"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomainAssociations"
---

Call the DescribeTransitRouterMulticastDomainAssociations API to query the association information about multicast domains that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterMulticastDomainAssociations&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|ownjLP">必选</span> `Example: DescribeTransitRouterMulticastDomainAssociations`

The interface name. The current API name is `DescribeTransitRouterMulticastDomainAssociations`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|eUunxK">必选</span>`Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterMulticastDomainId** <span data-label="purple">String</span> <span data-api-tag="require|4H6rgT">必选</span> `Example: tr-md-hy13n2l4c6c0v****`

The ID of the multicast domain. You can call [DescribeTransitRouterMulticastDomains](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains) to obtain the ID of the multicast domain.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You must specify at least one of: this parameter, <code>TransitRouterAttachmentId</code>, or <code>ResourceId</code>.</div>




**TransitRouterAttachmentId** <span data-label="purple">String</span> <span data-api-tag="require|VHCP07">必选</span> `Example: tr-attach-a*******`

The ID of the network instance attachment. You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You must specify at least one of: this parameter, <code>TransitRouterMulticastDomainId</code> or <code>ResourceId</code>.</div>




**SubnetIds.N** <span data-label="purple">String</span> <span data-api-tag="require|Uyqxwa">必选</span> `Example: subnet-123456`

ID of the subnet.


* N represents the sequence number of a subnet ID, ranging from 1 to 100.

* Separate multiple subnet IDs with ampersands (&).



**ResourceType** <span data-label="purple">String</span> <span data-api-tag="require|LbhJrf">必选</span> `Example: VPC`

The network instance type. Values:


* VPC: Virtual Private Cloud.



**ResourceId** <span data-label="purple">String</span> <span data-api-tag="require|CVdiDK">必选</span> `Example: vpc-bp1aevy8sofi8mh1****`

The network instance ID. You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to get the ID of the VPC instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You must specify at least one of: this parameter, <code>TransitRouterAttachmentId</code>, or <code>TransitRouterMulticastDomainId</code>.</div>




**PageNumber** <span data-label="purple">Integer</span> <span data-api-tag="require|3rYHvb">必选</span> `Example: 1`

The page number of the list. Default: 1.



**PageSize** <span data-label="purple">Integer</span> <span data-api-tag="require|FI4AhE">必选</span> `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterMulticastDomainAssociations ** <span data-label="purple"> Object[]  </span>`Example: -`

Detailed association of multicast domains that meet the conditions.


**TransitRouterMulticastDomainId ** <span data-label="purple"> String  </span>`Example: tr-md-3t6b1n60vg4jks0txrs8****`

The ID of the multicast domain.



**TransitRouterAttachmentId ** <span data-label="purple"> String  </span>`Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.



**SubnetId** <span data-label="purple">String</span> `Example: subnet-at6avgks2l454****`

Subnet ID.



**ResourceType** <span data-label="purple">String</span> `Example: VPC`

Type of the network instance attachment.


* VPC: Virtual Private Cloud.



**CreationTime ** <span data-label="purple"> String  </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the multicast domain is created.



**UpdateTime ** <span data-label="purple"> String  </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the multicast domain is last modified.



**Status ** <span data-label="purple"> String </span>`Example: Available`

Status of the multicast domain.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**ResourceId ** <span data-label="purple"> String  </span>`Example: vpc-bp15zckdt37pq72zv****`

The ID of the multicast resource.




**PageSize ** <span data-label="purple"> Integer  </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer</span> `Example: 1`

The current page number.



**TotalCount ** <span data-label="purple"> Integer  </span>`Example: 1`

Total number of multicast domains that meet the condition.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterMulticastDomainAssociations&Version=2020-04-01 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T122234Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterMulticastDomainAssociations",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1,
        "TransitRouterMulticastDomainAssociations": [
            {
                "Status": "Available",
                "SubnetId": "subnet-at6avgks2l454****",
                "ResourceId": "vpc-bp15zckdt37pq72zv****",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "ResourceType": "VPC",
                "TransitRouterAttachmentId": "tr-attach-13n2l4c****",
                "TransitRouterMulticastDomainId": "tr-md-3t6b1n60vg4jks0txrs8****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
