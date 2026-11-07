---
title: "DescribeTransitRouterTrafficQosMarkingEntries - Querying the list of traffic marking entries"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingEntries"
---

Call the DescribeTransitRouterTrafficQosMarkingEntries API to query the marking entries in a traffic marking policy that meet the specified conditions.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterTrafficQosMarkingEntries&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|6MEZQv">必选</span> `Example: DescribeTransitRouterTrafficQosMarkingEntries`

The interface name. The current API name is `DescribeTransitRouterTrafficQosMarkingEntries`.



**Version ** <span data-label="purple">String</span> <span data-api-tag="require|xlfX3v">必选</span>`Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageNumber** <span data-label="purple">Integer</span> <span data-api-tag="require|Ql11L4">必选</span> `Example: 1`

The page number of the list. Default: 1.



**PageSize** <span data-label="purple">Integer</span> <span data-api-tag="require|KN9dAs">必选</span> `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterTrafficQosMarkingPolicyId** <span data-label="purple">String</span> <span data-api-tag="require|LWFF0r">必选</span> `Example: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy. You can call the [DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) API to obtain the ID of the traffic marking policy.



**TransitRouterTrafficQosMarkingEntryIds.N** <span data-label="purple">String</span> <span data-api-tag="require|DRckmV">必选</span> `Example: tr-tme-1i5i8khf9m58gae5kcx6****`

ID of the marking entry.


* N represents the serial number of the marking entry, ranging from 1 to 100.

* Separate multiple marking entry IDs with ampersands (&).



**TransitRouterTrafficQosMarkingEntryName** <span data-label="purple">String</span> <span data-api-tag="require|6wJfJC">必选</span> `Example: tme-02`

Name of the traffic marking entry.



**Protocol** <span data-label="purple">String</span> <span data-api-tag="require|6FfsJf">必选</span> `Example: udp`

Protocol type.


* tcp: Transmission Control Protocol

* udp: User Datagram Protocol

* gre: Generic Routing Encapsulation​​

* icmp: Internet Control Message Protocol

* icmpv6: Internet Control Message Protocol version 6

* all: All protocols.



**SourceCidrBlock** <span data-label="purple">String</span> <span data-api-tag="require|tHDQXY">必选</span> `Example: 192.168.XX.XX/24`

The CIDR block of the source IP address.



**DestinationCidrBlock** <span data-label="purple">String</span> <span data-api-tag="require|dk7ttl">必选</span> `Example: 192.168.XX.XX/24`

The CIDR block of the destination IP address.



**MatchDscp** <span data-label="purple">Integer</span> <span data-api-tag="require|JHv5Lu">必选</span> `Example: 1`

The DSCP carried within the traffic packet.



**RemarkingDscp** <span data-label="purple">Integer</span> <span data-api-tag="require|r83i5w">必选</span> `Example: 1`f

The retagged DSCP of the traffic packet.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterTrafficQosMarkingEntries ** <span data-label="purple"> Object[]  </span>`Example: --`

Details of qualified traffic marking entries.


**Description ** <span data-label="purple"> String </span>`Example: This traffic qos marking entry is used for test.`

The description of the marking entry.



**TransitRouterTrafficQosMarkingEntryName ** <span data-label="purple"> String </span>`Example: tme-02`

Name of the marking entry.



**Status ** <span data-label="purple"> String  </span>`Example: Available`

Status of the marking entry.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**UpdateTime ** <span data-label="purple">String</span> `Example: 2021-04-10T09:18:28+08:00`

The time when the marking entry is recently updated.



**CreationTime ** <span data-label="purple"> String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the marking entry is created.



**TransitRouterTrafficQosMarkingEntryId ** <span data-label="purple"> String  </span>`Example: tr-tme-1i5i8khf9m58gae5kcx6****`

ID of the marking entry.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple"> String  </span>`Example: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy.



**Priority ** <span data-label="purple"> Integer  </span>`Example: 100`

Priority of the marking entry.



**Protocol ** <span data-label="purple"> String </span>`Example: udp`

The network protocol of the marking entry.


* tcp: Transmission Control Protocol

* udp: User Datagram Protocol

* gre: Generic Routing Encapsulation​​

* icmp: Internet Control Message Protocol

* icmpv6: Internet Control Message Protocol version 6

* all: All protocols.



**SourceCidrBlock ** <span data-label="purple"> String </span>`Example: 192.168.XX.XX/24`

Source CIDR block of the marking entry.



**DestinationCidrBlock ** <span data-label="purple"> String </span>`Example: 192.168.XX.XX/24`

Destination CIDR block of the marking entry.



**SourcePortStart ** <span data-label="purple"> Integer  </span>`Example: 1`

Start value of the marking entry's source port range. \-1 indicates no port restriction.



**SourcePortEnd ** <span data-label="purple"> Integer </span>`Example: 1`

End value of the marking entry's source port range. \-1 indicates no port restriction.



**DestinationPortStart ** <span data-label="purple"> Integer </span>`Example: 1`

Start value of the marking entry's destination port range. \-1 indicates no port restriction.



**DestinationPortEnd ** <span data-label="purple"> Integer  </span>`Example: 1`

End value of the marking entry's destination port range. \-1 indicates no port restriction.



**MatchDscp ** <span data-label="purple"> Integer  </span>`Example: 1`

The DSCP that the marking entry should match.



**Remarking DSCP ** <span data-label="purple"> Integer </span>`Example: 1`

Remarking DSCP after the business traffic successfully matches a marking entry.




**PageSize ** <span data-label="purple"> Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple"> Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple"> Integer  </span>`Example: 2`

The total number of qualified traffic marking entries.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterTrafficQosMarkingEntries&Version=2020-04-01&TransitRouterTrafficQosMarkingPolicyId=tr-tmp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250722T130405Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250722/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202507222104102120121940138D7345",
    "Action": "DescribeTransitRouterTrafficQosMarkingEntries",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterTrafficQosMarkingEntries": [
      {
        "Description": "This traffic qos marking entry is used for test.",
        "TransitRouterTrafficQosMarkingEntryName": "tme-02",
        "Status": "Available",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "TransitRouterTrafficQosMarkingEntryId": "tr-tme-1i5i8khf9m58gae5kcx6****",
        "TransitRouterTrafficQosMarkingPolicyId": "tr-tmp-hy13n2l4c6c0v****",
        "Priority": 100,
        "Protocol": "udp",
        "SourceCidrBlock": "192.168.XX.XX/24",
        "DestinationCidrBlock": "192.168.XX.XX/24",
        "SourcePortStart": 1,
        "SourcePortEnd": 1,
        "DestinationPortStart": 1,
        "DestinationPortEnd": 1,
        "MatchDscp": 1,
        "RemarkingDscp": 1
      }
    ],
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 2
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
