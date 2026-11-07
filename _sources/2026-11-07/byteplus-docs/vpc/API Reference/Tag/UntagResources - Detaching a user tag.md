---
title: "UntagResources - Detaching a user tag"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/UntagResources"
---

Call the UntagResources API to detach user tags from resources.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Tags exist only in association with a resource. When a tag is disassociated from all its bound resources, it is automatically deleted.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|OtgJYM">必选</span> `Example value: UntagResources`

The interface name. The current API name is `UntagResources`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|TGBNP1">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**ResourceType ** <span data-label="purple"> String </span><span data-api-tag="require|jg8hN-">必选</span> `Example value: vpc`

The resource type. Values:


* vpc: Virtual Private Cloud.

* subnet: Subnet.

* eni: Network interface.

* securitygroup: Security group.

* havip: High\-Availability Virtual IP Address.

* routetable: Route table.

* networkacl: Network Access Control List.

* flowlog: Flow log.

* trafficmirrortarget: Traffic mirror target.

* trafficmirrorfilter: Traffic mirror filter.

* trafficmirrorsession: Traffic mirror session.

* eip: EIP.

* bandwidthpackage: Bandwidth package.

* ngw: NAT gateway.

* vpngateway: VPN gateway.

* directconnectconnection: DC connection.

* directconnectgateway: DC gateway.

* directconnectvirtualinterface: DC Virtual Interface.



**ResourceIds.N ** <span data-label="purple"> String  </span><span data-api-tag="require|hteBrO">必选</span> `Example value: vpc-273w3e33y2y9s7fap8u2j****`

The resource ID.


* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).



**TagKeys.N ** <span data-label="purple"> String  </span><span data-api-tag="require|bnK500">必选</span> `Example value: k1`

The tag key of the custom tag to be deleted.


* Parameter \- N: Represents the serial number of a Tag key. A maximum of 20 IDs can be specified per single API call.

* Separate multiple tag keys with ampersands (&).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=vpc&ResourceIds.1=vpc-273w3e33y2y9s7fap8u2j****&ResourceIds.2=vpc-bp15zckdt37pq72zv****&TagKeys.1=k1&TagKeys.2=k2 HTTP/1.1
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
        "Action": "UntagResources",
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


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidResourceType.NotFound |The specified resource type does not exist. |The specified resource type does not exist. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
