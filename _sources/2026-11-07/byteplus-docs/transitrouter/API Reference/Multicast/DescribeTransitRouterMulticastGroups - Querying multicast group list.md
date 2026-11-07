---
title: "DescribeTransitRouterMulticastGroups - Querying multicast group list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastGroups"
---

Call the DescribeTransitRouterMulticastGroups API to query the multicast sources and multicast members in the specified multicast domain.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterMulticastGroups&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|k13vpd">必选</span> `Example: DescribeTransitRouterMulticastGroups`

The interface name. The current API name is `DescribeTransitRouterMulticastGroups`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|UJLmY8">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterMulticastDomainId ** <span data-label="purple">String </span><span data-api-tag="require|3eKuOS">必选</span> `Example value: tr-md-hy13n2l4c6c0v****`

The ID of the multicast domain. You can call [DescribeTransitRouterMulticastDomains](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains) to obtain the multicast domain ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You must specify at least one of: this parameter, <code>TransitRouterMulticastDomainId</code> or <code>ResourceId</code>.</div>




**GroupIpAddress ** <span data-label="purple">String </span><span data-api-tag="require|EsQJND">必选</span> `Example: 224.0.1.0`

IP address of the multicast group. Value range: 224.0.1.0\-239.255.255.254.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|3xJhj6">必选</span> `Example value: tr-attach-a*******`

The ID of the network instance attachment. You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.



**ResourceType ** <span data-label="purple">String </span><span data-api-tag="require|7S4h8S">必选</span> `Example value: VPC`

The type of the multicast resource.


* VPC: Virtual Private Cloud.



**ResourceId ** <span data-label="purple">String </span><span data-api-tag="require|xiA947">必选</span> `Example value: vpc-bp1aevy8sofi8mh1****`

The ID of the multicast resource. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to obtain the VPC ID.



**SubnetIds.N ** <span data-label="purple">String </span><span data-api-tag="require|Yks7bj">必选</span> `Example value: subnet-123456`

ID of the subnet.


* N represents the serial number of the subnet ID, ranging from 1 to 100.

* Separate multiple subnet IDs with ampersands (&).



**NetworkInterfaceIds.N ** <span data-label="purple">String </span><span data-api-tag="require|WHv5dy">必选</span> `Example value: eni-123456`

Network Interface ID.


* N represents the serial number of the network interface ID, with a value range of 1 to 100.

* Separate multiple network interface IDs with ampersands (&).



**IsGroupSource ** <span data-label="purple">Boolean </span><span data-api-tag="require|XwiL6s">必选</span> `Example value: true`

Whether to query the multicast source.


* true: Yes.

* false: No.



**IsGroupMember ** <span data-label="purple">Boolean </span><span data-api-tag="require|wOMn5b">必选</span> `Example value: true`

Describe whether to query multicast members.


* true: Yes.

* false: No.



**SourceType ** <span data-label="purple">String </span><span data-api-tag="require|xkrzLq">必选</span> `Example value: Static`

The type of the multicast source.


* Static: Static multicast source, indicating to specify the multicast source manually.



**MemberType ** <span data-label="purple">String </span><span data-api-tag="require|IIrzAa">必选</span> `Example value: Static`

The type of the multicast member.


* Static: Static multicast member, indicating that multicast member is manually specified.



**PageNumber ** <span data-label="purple">Integer </span><span data-api-tag="require|MGaozK">必选</span> `Example value: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span><span data-api-tag="require|xhnCVY">必选</span> `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterMulticastGroups ** <span data-label="purple">Object[] </span>`Example value: -`

Resource information about qualified multicast groups.


**CreationTime ** <span data-label="purple">String </span>`Example value: 2021-04-09T08:36:47+08:00`

The time when the multicast group is created.



**UpdateTime ** <span data-label="purple">String </span>`Example value: 2021-04-10T09:18:28+08:00`

The time when the multicast group is last operated.



**Status ** <span data-label="purple">String </span>`Example value: Available`

Status of the multicast resource.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**TransitRouterMulticastDomainId ** <span data-label="purple">String </span>`Example: tr-md-3t6b1n60vg4jks0txrs8****`

The ID of the multicast domain.



**GroupIpAddress ** <span data-label="purple">String </span>`Example value: 224.0.1.0`

IP address of the multicast group.



**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-16b4ks6wd****`

The ID of the network instance attachment.



**ResourceType ** <span data-label="purple">String </span>`Example value: VPC`

The network instance type.


* VPC: Virtual Private Cloud.



**ResourceId ** <span data-label="purple">String </span>`Example value: vpc-bp1aevy8sofi8mh1****`

The network instance ID.



**SubnetId ** <span data-label="purple">String </span>`Example value: subnet-1wdfv3tfh6****`

ID of the subnet.



**NetworkInterfaceId ** <span data-label="purple">String </span>`Example value: eni-wsdfgg5wrf****`

Network Interface ID.



**GroupSource ** <span data-label="purple">Boolean </span>`Example value: true`

Describe whether the current multicast resource is a multicast source.


* true: Yes.

* false: No.



**GroupMember ** <span data-label="purple">Boolean </span>`Example value: true`

Describe whether the current multicast resource is a multicast member.


* true: Yes.

* false: No.



**SourceType ** <span data-label="purple">String </span>`Example value: Static`

The type of the multicast source.


* Static: Static multicast source, indicating to specify the multicast source manually.



**MemberType ** <span data-label="purple">String </span>`Example value: Static`

The type of the multicast member.


* Static: Static multicast member, indicating that multicast member is manually specified.



**TransitRouterId ** <span data-label="purple">String </span>`Example value: tr-1aadrf4cgh****`

The ID of the Transit Router (TR) instance.




**PageNumber ** <span data-label="purple">Integer </span>`Example value: 1`

The page number of the current multicast group list returned, indicating pagination information of the query results.



**PageSize ** <span data-label="purple">Integer </span>`Example value: 10`

Number of multicast groups displayed per page.



**TotalCount ** <span data-label="purple">Integer </span>`Example value: 2`

The total number of qualified multicast group resources.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterMulticastGroups&Version=2020-04-01 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T122158Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterMulticastGroups",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 2,
        "TransitRouterMulticastGroups": [
            {
                "Status": "Available",
                "SubnetId": "subnet-1wdfv3tfh6****",
                "MemberType": "Static",
                "ResourceId": "vpc-bp1aevy8sofi8mh1****",
                "SourceType": "Static",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "GroupMember": true,
                "GroupSource": true,
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "ResourceType": "VPC",
                "GroupIpAddress": "224.0.1.0",
                "TransitRouterId": "tr-1aadrf4cgh****",
                "NetworkInterfaceId": "eni-wsdfgg5wrf****",
                "TransitRouterAttachmentId": "tr-attach-16b4ks6wd****",
                "TransitRouterMulticastDomainId": "tr-md-3t6b1n60vg4jks0txrs8****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
