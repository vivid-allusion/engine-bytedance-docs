---
title: "DescribePrivateEgressEndpoints - Listing private egress endpoints"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribePrivateEgressEndpoints"
---

Call the DescribePrivateEgressEndpoints API to query the endpoint list of a private network egress.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePrivateEgressEndpoints&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|OXBeN9">必选</span> `Example: DescribePrivateEgressEndpoints`

The action to perform. Value: **DescribePrivateEgressEndpoints**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|qjvrt2">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PrivateEgressId ** <span data-label="purple"> String </span><span data-api-tag="require|JxXJjo">必选</span> `Example: pre-p6q7r8s9t0****`

The ID of the private network egress.



**PrivateEgressEndpointIds.N ** <span data-label="purple"> String </span>`optional` `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the private egress endpoint.


* N represents the sequence number of a private egress endpoint ID. Valid values: 1\-100.

* Separate multiple private egress endpoint IDs with ampersands (&).



**PageNumber ** <span data-label="purple"> Integer </span>`optional` `Example: 1`

The page number of the list.


* If not specified, the value defaults to 1.

* Minimum: 1.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 20`

The number of entries per page in a pagination query.


* Valid values: 1\-100.

* If not specified, the value defaults to 20.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AsyncTaskId ** <span data-label="purple"> String </span>`Example: asynctask-13f0odozfrdvk3n6nu41l****`

The ID of the asynchronous task.



**PageNumber ** <span data-label="purple"> Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer </span>`Example: 10`

The number of entries per page.



**PrivateEgressEndpoints ** <span data-label="purple"> Object[] </span>`Example: --`

The information about the private egress endpoint.


**VpcId ** <span data-label="purple"> String  </span>`Example: vpc-bp1b1llp3ve5yze****`

The ID of your VPC.



**Status ** <span data-label="purple"> String </span>`Example: Available`

The status of the endpoint.


* Creating

* Available

* Pending

* Deleting



**CreateTime ** <span data-label="purple"> String </span>`Example: 2026-08-18 15:19:00`

The time when the private egress endpoint is created.



**UpdateTime ** <span data-label="purple"> String  </span>`Example: 2026-08-18 15:19:00`

The time when the private egress endpoint is updated.



**EndpointIps ** <span data-label="purple"> String[]  </span>`Example: ["192.168.0.2","192.168.0.3","192.168.0.4",192.168.0.5",192.168.0.6","192.168.0.7"]`

The list of endpoints IPs.



**ZoneMappings ** <span data-label="purple"> Object[] </span>`Example: --`

The mapping between the availability zone and the subnet.


**ZoneId ** <span data-label="purple"> String </span>`Example: cn-beijing-a`

The ID of the availability zone.



**SubnetId ** <span data-label="purple"> String </span>`Example: subnet-bp1nhbnpv2blyz8dl****`

The ID of the subnet.




**SpaceNetworkId ** <span data-label="purple"> String </span>`Example: csn-3hxxy2a53tce81wincnyu****`

The space network ID.



**PrivateEgressId ** <span data-label="purple"> String </span>`Example: pre-p6q7r8s9t0****`

The ID of the private network egress.



**DestinationCidrs ** <span data-label="purple"> String[]  </span>`Example: ["192.168.0.0/16"]`

The CIDR blocks of enterprise services that can be accessed by the Claw instance over the private network.



**SecurityGroupIds ** <span data-label="purple"> String[] </span>`Example: ["sg-bp1fg655nh68xyz9****"]`

The security group ID.



**AppPrivateAccessEnabled ** <span data-label="purple"> Boolean </span>`Example: false`

Describe whether the private access to apps feature is enabled.


* true

* false



**PrivateEgressEndpointId ** <span data-label="purple"> String </span>`Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the private egress endpoint.




**RequestId ** <span data-label="purple"> String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



**TotalCount ** <span data-label="purple"> Integer </span>`Example: 2`

The total number of private egress endpoints matching the specified conditions.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=DescribePrivateEgressEndpoints&Version=2020-04-01&PrivateEgressId=pre-p6q7r8s9t0****&PrivateEgressEndpointIds.1=ep-273yuq6q7bgn47fap8squ****&PageNumber=1&PageSize=20
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePrivateEgressEndpoints",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AsyncTaskId": "asynctask-13f0odozfrdvk3n6nu41l****",
        "PageNumber": 1,
        "PageSize": 10,
        "PrivateEgressEndpoints": [
            {
                "VpcId": "vpc-bp1b1llp3ve5yze****",
                "Status": "Available",
                "CreateTime": "2026-08-18 15:19:00",
                "UpdateTime": "2026-08-18 15:19:00",
                "EndpointIps": [
                    ""
                ],
                "ZoneMappings": [
                    {
                        "ZoneId": "cn-beijing-a",
                        "SubnetId": "subnet-bp1nhbnpv2blyz8dl****"
                    }
                ],
                "SpaceNetworkId": "csn-3hxxy2a53tce81wincnyu****",
                "PrivateEgressId": "pre-p6q7r8s9t0****",
                "DestinationCidrs": [
                    "192.168.0.0/16"
                ],
                "SecurityGroupIds": [
                    "sg-bp1fg655nh68xyz9****"
                ],
                "AppPrivateAccessEnabled": true,
                "PrivateEgressEndpointId": "ep-273yuq6q7bgn47fap8squ****"
            }
        ],
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no service\-specific error codes. For more details, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).
