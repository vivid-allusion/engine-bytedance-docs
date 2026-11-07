---
title: "CreateFlowLog - Creating a VPC flow log"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateFlowLog"
---

Call the CreateFlowLog API to create a flow log.

## Instructions

* A single user in a single region can create up to 10 VPC flow logs.

* CreateFlowLog is an asynchronous API. When a request ID is returned, the system is still creating in the background. You can call [DescribeFlowLogs](https://docs.byteplus.com/en/docs/vpc/DescribeFlowLogs) to view the status of flow logs. Creating indicates that the flow log is being created, and Active indicates that the creation is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateFlowLog&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateFlowLog`

Interface name. The current API name is `CreateFlowLog`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**FlowLogName ** String必选 `Example: FlowLog-1`

The name of the flow log.

* Must be 1 to 128 characters in length.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the flow log instance ID.

**Description ** String`optional` `Example: FlowLog_VPC`

Description of the flow log.

* Must be 0 to 255 characters.

* If left blank, the parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), half\-width periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**ResourceType ** String必选 `Example: vpc`

The resource type from which to collect traffic. Valid values:

* vpc: Virtual Private Cloud.

* subnet: Subnet.

* eni: Network Interface.

**ResourceId ** String必选 `Example: vpc-123456****`

The ID of the resource from which to collect traffic. Provide the ID of the corresponding resource type based on the parameter passed for `ResourceType`.

**TrafficType ** String必选 `Example: All`

The type of traffic to collect. Valid values:

* All: Total traffic.

* Allow: Traffic permitted by the network ACL and security group.

* Drop: Traffic denied by the network ACL and security group.

**LogProjectName ** String必选 `Example: flowlog-project-1`

Name of the flow log project.

* The name can only contain lowercase letters, numbers, and hyphens (\-).

* It must start and end with a lowercase letter or a number.

* The name must be 3 to 63 characters in length.

> **tip**

> The system searches for an existing Log Project by name; if none is found, a new one is created.

**LogTopicName ** String必选 `Example: flowlog-topic-1`

Name of the flow log topic. The following requirements must be met.

* Only lowercase English letters, numbers, and hyphens (\-) are supported

* It must start and end with a lowercase letter or a number.

* Must be 3 to 63 characters.

> **tip**

> The system searches for an existing Log Topic by name; if none is found, a new one is created.

**AggregationInterval ** Integer`optional` `Example: 10`

Sampling interval of the flow log. Values:

* 1: 1 minute.

* 5: 5 minutes.

* 10 (default): 10 minutes.

**EnableIndex ** Boolean`optional` `Example: true`

Whether to configure the index automatically. Indexes are used for searching and analyzing data. Flow Logs must be configured with indexes before you can perform search and analysis.

* true: Yes.

* false (default): No.

**ProjectName ** String`optional` `Example: default`

Name of the flow log project. If left blank, it defaults to the default project.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N specifies the serial number of the tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands ( & ).

* Cannot start with `volc:` or `sys:` in any case form.

* It can be 1 to 128 characters in length. It may contain characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N represents the serial number of the tag value. Valid range: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include multilingual characters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.

> **tip**

> If this parameter is provided, you must first provide `Tags.N.Key`.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

**TrafficPath.N ** String`optional` `Example: NatGW`

Identifies the path by which traffic reaches the destination. Valid values:

* All (default): All traffic except the scenarios below.

* NatGW: Traffic through the NAT Gateway.

* Ipv4GW: Traffic accessing the internet through an EIP (including via IPv4 gateway).

* Ipv6GW: Traffic accessing the internet through an IPv6 gateway.

* VpnGW: Traffic through the VPN gateway.

* GWLBEndpoint: Traffic through the Gateway Load Balancer Endpoint.

* TransitRouter: Traffic through a Transit Router (TR), including traffic destined for VPCs in the same region, VPCs in cross\-regions, Direct Connect gateways, and other resources via TR.

* CEN: Traffic through Cloud Enterprise Network (CEN), including traffic destined for VPCs in the same region, VPCs in cross\-regions, Direct Connect (DC) Gateways, and other resources via CEN.

* IntraRegionVpcPeeringConnection: Traffic through a same\-region Peering Connection.

* InterRegionVpcPeeringConnection: Traffic through a cross\-region Peering Connection.

* DirectExchangeGateway: Traffic through a Direct Exchange Gateway.

**FlowLogVersion ** Integer`optional` `Example: 1`

Version of the VPC flow log.

* 1: Version 1.

* 2: Version 2.

* 3: Version 3.

* 4: Version 4.

If not provided, the system automatically assigns a random version.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**FlowLogId ** String`Example: fl-123456****`

Flow Log ID.

**Version ** Integer`Example: 3`

Version of the VPC flow log.

* 1: Version 1.

* 2: Version 2.

* 3: Version 3.

* 4: Version 4.

## Request example

```json
GET /?Action=CreateFlowLog&Version=2020-04-01&FlowLogName=FlowLog-1&Description=FlowLog_VPC&ResourceType=vpc&ResourceId=vpc-123456****&TrafficType=All&LogProjectName=flowlog-project-1&LogTopicName=flowlog-topic-1&AggregationInterval=10 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateFlowLog",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "FlowLogId": "fl-123456****",
        "RequestId": "2021062415303301022514515207C4****",
        "Version": 3
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidFlowLog.CloudProfileNotAvailable |The cloud profile is not available in this region. |The account system in the current region is temporarily unavailable. |
|400 |InvalidFlowLog.InvalidVersion |The version is not invalid. |Setting to this version is not supported. |
|400 |InvalidFlowLog.TlsNotSupport |The specified account is not supported by TLS service in this region. |TLS is not supported for the current account in this region. |
|400 |InvalidFlowLog.TrafficPathNotSupported |The specified flow log does not support traffic path updates. |The current version of the specified flow log does not support modifying path filter parameters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and try again. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified ClientToken is invalid. It cannot exceed 64 ASCII characters. |
|400 |InvalidParameter.FlowLogAggregationInterval |The specified aggregation interval is invalid. |The specified flow log sampling interval parameter is invalid. |
|400 |InvalidParameter.FlowLogInvalidResource |The specified resource is not allowed to be bound to a flow log. |The specified resource cannot be bound to a Flow Log due to type restrictions. |
|400 |InvalidParameter.FlowLogResourceAlreadyBound |The specified resource is already bound to a flow log. |The specified resource is already bound to a Flow Log. |
|400 |InvalidParameter.FlowLogTrafficPath |The specified traffic path is invalid. |The specified flow log path filter parameter is invalid. |
|400 |InvalidParameter.FlowLogTrafficType |The specified traffic type is invalid. |The specified traffic collection type parameter is invalid. |
|400 |InvalidParameter.TLSTopicExisted |The specified topic name already exists. |The specified log topic name exists and cannot be created. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |LimitExceeded.TLSProject |You've reached the limit on the number of TLS project per region that you can create. |Reached the maximum TLS log projects that you can create in a single region under the current account. |
|400 |LimitExceeded.TLSTopic |You've reached the limit on the number of TLS topics per project that you can create. |You have reached the maximum number of topics that you can create under a single TLS log project for the current account. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |The maximum tags that you can operate in a single request have been reached. |
|400 |MainAccountNotSupportPaypal |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The postpaid product in this order does not support PayPal payment. Please contact the root user to add another payment method. |
|400 |NotPaymentQualified |Your account has not passed the payment qualified yet. |Your account payment verification failed. |
|400 |NotSupportPaypal |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The postpaid product in this order does not support PayPal payment. Please add another payment method. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The request to operate on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The request on the specified instance is denied because the account is in arrears. |
|401 |InvalidOperation.NoPermission |The current service is not allowed to do this operation. |The current service is not authorized. |
|403 |Forbidden.PurchaseLimited |The account is not authorized to purchase the resource. |This account does not have permission to purchase resources. |
|403 |Forbidden.ShareENI |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface in shared subnet does not support this operation. |No permission to perform actions on the specified Elastic Network Interface (ENI). This operation is not supported for the specified ENI in a shared subnet. |
|403 |InvalidFlowLog.TlsAccessDenied |TLS service access denied. |The current account has not activated the TLS. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|404 |QuotaExceeded.FlowLog |Flow log number exceeded quota. |The number of Flow Logs exceeds the quota limit. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
