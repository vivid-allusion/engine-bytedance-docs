---
title: "DescribeVpcEndpoints - Querying the endpoint list"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints"
---

Call the DescribeVpcEndpoints API to query the list of endpoints that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpoints&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|C4XRDT">必选</span> `Example: DescribeVpcEndpoints`

Action to execute. Set the value to **DescribeVpcEndpoints**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|UIrScG">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of rows per page for paginated queries. Maximum: 100. Default: 10.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the endpoint belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC ID.



**ServiceId ** <span data-label="purple">String </span>`optional` `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**ServiceName ** <span data-label="purple">String </span>`optional` `Example: com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****`

Endpoint service name. Format: com.volces.privatelink. *<regionID\>* . *<endpointserviceID\>* .



**EndpointIds.N ** <span data-label="purple">String </span>`optional` `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.


* N: Represents the serial number of the endpoint ID, ranging from 1 to 100.

* Separate multiple endpoint IDs with ampersands (&).



**EndpointName ** <span data-label="purple">String </span>`optional` `Example: endpoint-01`

The name of the endpoint.



**Status ** <span data-label="purple">String </span>`optional` `Example: Available`

Status of the endpoint.


* Creating

* Pending: Modifying configuration.

* Available: Available for use.

* Deleting: In the deleting process.



**ConnectionStatus ** <span data-label="purple">String </span>`optional` `Example: Connected`

The connection status between the endpoint and the endpoint service.


* PendingAcceptance: Waiting for connection

* Connecting

* Connected

* Disconnecting

* Rejected: Connection denied.

* Failed: Connection failed.

* PartialFailed: Partial connection failure.

* ServiceDeleted: The service has been deleted.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Project to which the endpoint belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns interface endpoints tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns interface endpoints that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is passed in, TagFilters.N.Key must be passed in first.</div>


<div data-tips="true" data-tips-type="tip">Passing an empty string queries for interface endpoints with an empty tag value.</div>




**ServiceRegion ** <span data-label="purple">String </span>`optional` `Example: cn-beijing`

The region to which the endpoint service belongs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The number of rows on the current page.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of qualified endpoints.



**Endpoints ** <span data-label="purple">Object[] </span>`Example: -`

Details of the endpoint.


**Endpoint ID** <span data-label="purple">String</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.



**EndpointName ** <span data-label="purple">String </span>`Example: endpoint-01`

The name of the endpoint.



**EndpointType ** <span data-label="purple">String </span>`Example: Interface`

Endpoint type.


* Interface: Interface endpoint.



**IpAddressVersions** <span data-label="purple">String[]</span> `Example: ipv4`

IP protocol type of the endpoint.


* If the return value contains only **ipv4**, it means the endpoint is of the IPv4 type.

* If the return value contains both **ipv4** and **ipv6**, it means the endpoint is of the dual\-stack type.



**Payer ** <span data-label="purple">String </span>`Example: Endpoint`

The account that pays for PrivateLink.


* Endpoint: Endpoint account.

* EndpointService: Endpoint service account.



**EndpointDomain ** <span data-label="purple">String </span>`Example: ep-273yuq6q7bgn47fap8squ****.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com`

Domain name of the endpoint.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the endpoint.


* Creating

* Pending: Modifying configuration.

* Available: Available for use.

* Deleting: In the deleting process.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

Whether the endpoint is locked.


* Normal

* FinancialLocked: Being locked.



**ConnectionStatus ** <span data-label="purple">String </span>`Example: Connecting`

Status of the endpoint connection.


* PendingAcceptance: Waiting for connection

* Connecting

* Connected

* Disconnecting

* Rejected: Connection denied.

* Failed: Connection failed.

* PartialFailed: Partial connection failure.

* ServiceDeleted: The service has been deleted.



**Bps ** <span data-label="purple">Integer </span>`Example: 1000`

The maximum bandwidth of the endpoint connection, measured in Mbps.



**EndpointZoneNums** <span data-label="purple">Integer</span> `Example: 2`

Number of endpoint availability zone.



**Description ** <span data-label="purple">String </span>`Example: endpoint service`

The description of the endpoint.



**ServiceId** <span data-label="purple">String</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.



**ServiceName ** <span data-label="purple">String </span>`Example: com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****`

Endpoint service name.



**ServiceManaged ** <span data-label="purple">Boolean </span>`Example: false`

Indicates whether this is a managed endpoint.


* false: Non\-managed endpoint.

* true: Managed endpoint.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the endpoint belongs.



**PrivateDNSEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Whether private DNS name is enabled for the endpoint.


* false: Disabled.

* true: Enabled.



**PrivateDNSName ** <span data-label="purple">String </span>`Example: www.example.com`

Private DNS name of the endpoint.

This parameter returns empty when the `PrivateDNSEnabled` parameter returns **false**.



**CreationTime** <span data-label="purple">String</span> `Example: 2021-07-20T03:32:32+08:00`

The creation time of the endpoint.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-07-20T03:32:32+08:00`

Last operation time of the endpoint.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-08-20T03:32:32+08:00`

Deletion time of the endpoint.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the endpoint belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the endpoint.


**Key ** <span data-label="purple">String </span>`Example: k1`

Tag key of the endpoint tag.



**Value ** <span data-label="purple">String </span>`Example: v1`

Tag value of the endpoint tag.




**ServiceRegion ** <span data-label="purple">String </span>`Example: cn-beijing`

The region to which the endpoint service belongs.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeVpcEndpoints&Version=2020-04-01&EndpointName=endpoint-01 HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "Action": "DescribeVpcEndpoints",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "PageNumber": 1,
        "PageSize": 10,  
        "TotalCount": 2,
        "Endpoints": [
            {
                "EndpointId": "ep-273yuq6q7bgn47fap8squ****",
                "EndpointName": "endpoint-01",
                "EndpointType": "Interface",
                "IpAddressVersions": [
                    "ipv4",
                    "ipv6"
                ],
                "Payer": "Endpoint",
                "EndpointDomain": "ep-273yuq6q7bgn47fap8squ****.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com",
                "Status": "Available"
                "BusinessStatus": "Normal",
                "ConnectionStatus": "Connecting",
                "Description": "",
                "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****",
                "ServiceName": "com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****",
                "VpcId": "vpc-bp15zkdt37pq72zv****",
                "PrivateDNSEnabled": false,
                "PrivateDNSName": "",
                "CreationTime": "2021-07-20T03:32:32+08:00",
                "UpdateTime": "2021-07-20T03:32:32+08:00",
                "DeletedTime": "2021-08-20T03:32:32+08:00",
                "ProjectName": "default",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    },
                    {
                        "Key": "k2",
                        "Value": "v2"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.EndpointNumber |You've reached the limit on the number of endpoints that you can operate. |The quota for the number of endpoints that can be operated on in a single request has been reached. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |InvalidParameter.BatchQueryForFuzzySearch |Batch query parameters and precise search parameters are passed in at the same time. |Batch query parameters and exact search parameters cannot be passed simultaneously. |
|400 |LimitExceed.EndpointServices |You've reached the limit on the number of EndpointServices that you can operate. |The quota for the number of endpoint services that can be operated on in a single request has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
