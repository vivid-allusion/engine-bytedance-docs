---
title: "CreateNatGateway - Creating a NAT gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/CreateNatGateway"
---

Call the CreateNatGateway API to create a Network Address Translation (NAT) gateway instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* A single Virtual Private Cloud (VPC) can have a maximum of 3 NAT gateways.

* You can call [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress) to associate an elastic IP address (EIP) with a NAT gateway.

* A single NAT gateway can have a maximum of 10 associated EIPs by default. If the default quota for associating EIPs is insufficient, go to BytePlus Quota Center to increase the corresponding quota.

* For other tag actions, see TagResources, UntagResources, and ListTagsForResources.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateNatGateway&groupName=NAT%E7%BD%91%E5%85%B3&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|82qfuO">必选</span> `Example: CreateNatGateway`

The action that you want to perform. Value: CreateNatGateway.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|EthpGu">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**BillingType ** <span data-label="purple">integer </span>`optional` `Example: 1`

The metering method of the NAT Gateway. Values:


* 1: Subscription.

* 2 (default): Pay\-by\-Specification.

* 3: Pay\-by\-CU.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When NetworkType is set to "intranet", this parameter only supports and must be set to "3".</div>




**NatGatewayName ** <span data-label="purple">string </span>`optional` `Example: nat-01`

The name of the NAT gateway.


* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters. If left blank, this parameter defaults to the NAT gateway ID.



**Description ** <span data-label="purple">string </span>`optional` `Example: This is a NAT`

Description of the NAT gateway.


* Must start with a letter, Chinese character, or number.

* May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters. If left blank, this parameter defaults to an empty string.



**Spec ** <span data-label="purple">string </span>`optional` `Example: Small`

The specification of the NAT gateway.


* Small (default)

* Medium.

* Large.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not supported when BillingType is set to "3".</div>




**PeriodUnit ** <span data-label="purple">string </span>`optional` `Example: Month`

The unit of purchase duration for Subscription NAT gateways. Default: Month.


* Month

* Year.



**Period ** <span data-label="purple">integer </span>`optional` `Example: 3`

The purchased duration for the Subscription NAT gateway. Default: 1.


* When PeriodUnit is set to "Month", the valid values of Period are 1–9, 12, 24, and 36.

* When PeriodUnit is set to "Year", the valid values of Period are 1–3.



**ClientToken ** <span data-label="purple">string </span>`optional` `Example: 333456899ff****`

Ensure the request idempotency. You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs. Values:


* Must not exceed 64 ASCII characters.



**Tags.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: key1`

The custom tag key of the NAT gateway.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag keys with ampersands (&). Must not start with volc: regardless of case.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@). If a tag key starts or ends with spaces, the system automatically deletes the space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`optional` `Example: value1`

The custom tag value of the NAT gateway.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with spaces, the system automatically deletes the space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide this parameter, provide Tags.N.Key first.</div>




**NetworkType ** <span data-label="purple">string </span>`optional` `Example: internet`

The type of the NAT gateway. Values:


* internet (default): Internet NAT Gateway.

* intranet: VPC NAT Gateway.



**DirectMode ** <span data-label="purple">boolean </span>`optional` `Example: true`

The direct mode for the NAT gateway. Values:


* true (default): Direct NAT Gateway.

* false: Non\-direct NAT Gateway.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: Project_1`

The name of the project to which the NAT gateway belongs. If left blank, this parameter defaults to the default project.



**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|ehXzCI">必选</span> `Example: vpc-2feypfmenesqo59gp67yz****`

The ID of the VPC where the NAT gateway resides.



**SubnetId ** <span data-label="purple">string </span>`optional` `Example: subnet-2feypga30rgg059gp67ag****`

ID of the subnet where the NAT gateway is located.


* The subnet to be specified must be a subnet of the VPC specified in VpcId.

* The subnet contains at least one available private IP. The network interface automatically generated by the system for the NAT Gateway will occupy one private IP address in that subnet.

* The subnet's availability zone must have NAT Gateway resources deployed. You can call DescribeSubnets to query the availability zones of subnets under the VPC. You can also call [ListNatGatewayAvailableZones](https://docs.byteplus.com/en/docs/natgateway/ListNatGatewayAvailableZones) to query the availability zones where NAT gateway resources are located in the current region. The availability zone where the subnet is located is used as the primary availability zone of the NAT gateway, and the system will automatically associate a secondary availability zone for it. If the primary availability zone experiences a failure, the NAT Gateway will automatically fail over to the secondary availability zone.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp686****`

The instance ID of the NAT gateway.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateNatGateway&Version=2020-04-01&VpcId=vpc-2feypfmenesqo59gp67yz****&SubnetId=subnet-2feypga30rgg059gp67ag****&Spec=Small HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateNatGateway",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "NatGatewayId": "ngw-2feq5xhimd88w59gp686****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |QuotaExceeded.SecurityGroup |Security group number exceeded quota. |You have reached the maximum number of security groups that you can create in a region under the current account. |
|400 |QuotaExceeded.RouteEntry |Route entry of a route table number exceeded quota. |You have reached the maximum of route entries that you can create in a route table. |
|400 |QuotaExceeded.NatGateway |NAT gateways number of the VPC exceeded quota. |You have reached the maximum number of NAT gateways that you can create for a single VPC. |
|400 |QuotaExceeded.Eni |ENI number exceeded quota. |You have reached the maximum number of network interfaces that you can create in a region under the current account. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |InvalidZone.NotSupported |The specified Availability Zone does not support Nat Gateways. |The availability zone where the specified subnet is located does not have NAT gateway resources deployed. |
|400 |InvalidYearPeriod.Malformed |The specified yearly period is malformed. Yearly period only supports 1~3. |The specified subscription duration in years is invalid. The valid values for subscription duration in years are 1 to 3. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified billing method is invalid. |
|400 |InvalidMonthPeriod.Malformed |The specified monthly period is malformed. Monthly period only supports 1~9, 12, 24, 36. |The specified subscription duration in months is invalid. The valid values for subscription duration in months are 1 to 9, 12, 24, and 36. |
|400 |InvalidNatGateway.NoSubnetInVpc |The specified VPC has no subnet. NAT gateway cannot be created. |No subnets exist in the specified VPC. Therefore, the NAT gateway cannot be created. |
|400 |InvalidNatGatewayDefaultRoute.Conflict |A default route already exists in specified VPC, NAT gateway cannot be created. |A default route exists in the specified VPC. Therefore, the NAT gateway cannot be created. |
|400 |InvalidNatGatewaySpec.Malformed |The specified NAT spec is malformed. |The specified NAT gateway specification is not supported. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of the specified ClientToken is invalid. A parameter must not exceed 64 ASCII characters. |
|400 |InvalidPeriodUnit.Malformed |The specified period unit is malformed. Pre billing period unit can only be Month or Year. |The specified unit for the subscription duration is invalid. The subscription duration unit must be Month or Year. |
|400 |InvalidSubnet.VpcMismatch |The specified subnet is not in the specified VPC. |The specified subnet is not within the specified VPC. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidNatGateway.PreOrder |Create preorder for nat gateway failed. |Failed to create the configuration order for the NAT gateway. |
|400 |InvalidNatGatewayNetworkType.Malformed |The specified network type of NAT gateway is malformed. |The network type of the specified NAT gateway is invalid. |
|400 |QuotaExceeded.NatIp |NAT IPs number of the cidr exceeded quota. |You have reached the maximum number of NAT IP addresses that you can create in a CIDR block. |
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidNatGateway.IPv4GatewayAttached |The specified VPC has been attached to IPv4 gateway, direct mode NAT gateway cannot be created. |The specified VPC has an IPv4 gateway associated. Therefore, the NAT gateway in direct mode cannot be created. |
|400 |InvalidNatGateway.UnSupportLocalZone |The current type of NAT instance is not supported in local zones. |This region does not support the current type of NAT instances. |
|400 |InvalidNatGateway.NoSubnetInRegion |The specified region has no available subnet. NAT gateway cannot be created. |No available subnet in the specified region. |
|400 |InvalidSubnet.IPv4Disabled |IPv4 has been disabled for the specified subnet. |IPv4 has been disabled for the specified subnet. |
|403 |Forbidden |You are not authorized to create or update an extra large NAT gateway. |No permission to create or modify super large NAT gateways. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidProject.NotFound |The specified project does not exist. |The specified project does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified Virtual Private Cloud (VPC) does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|412 |InvalidNatGateway.CreateEniFailed |The specified nat gateway create eni failed. |Failed to create the network interface for the NAT gateway. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
