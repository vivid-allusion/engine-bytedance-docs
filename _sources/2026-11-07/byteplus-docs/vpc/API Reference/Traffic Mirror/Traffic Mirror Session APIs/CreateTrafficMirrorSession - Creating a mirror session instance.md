---
title: "CreateTrafficMirrorSession - Creating a mirror session instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorSession"
---

Call the CreateTrafficMirrorSession API to create a Mirror Session.

## Instructions

* After a mirror session is created, Traffic Mirror starts being billed. If the mirror site is a secondary Network Interface (ENI), billing continues normally even if the secondary ENI is detached from its Elastic Compute Service (ECS) instance.

* CreateTrafficMirrorSession is an asynchronous API; when a request ID is returned, the system is still creating in the background. You can call [DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) to check the mirror session status: Creating means in progress, Active means creation is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTrafficMirrorSession&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateTrafficMirrorSession`

The interface name. The current API name is `CreateTrafficMirrorSession`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorSessionName ** String`optional` `Example: TM_Session_1`

Name of the traffic mirror session.

* Must be 1 to 128 characters.

* The name must start with a letter, Chinese character, or number. It may contain periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the ID of the Traffic Mirror Session.

**Description ** String`optional` `Example: TM_Session_1_Description`

Description of the traffic mirror session.

* If left blank, this defaults to an empty string.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**NetworkInterfaceId ** String必选`Example: eni-bp1fgnh68xyz9****`

ENI ID of the mirror site.

Currently, only primary ENIs or secondary ENIs already attached to an ECS instance are supported.

You can call [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query ENIs that meet the conditions.

**TrafficMirrorTargetId ** String必选 `Example: tmt-35bvae1r7rv283dy2w2ll****`

Mirror target ID.

You can call the [DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) API to query the mirror target ID.

**Priority ** Integer必选 `Example: 1`

The priority of the mirror session ranges from **1** to **32766**.

A lower priority value indicates higher precedence. The priorities of mirror sessions created by the same account in the same region must be unique.

**VirtualNetworkId ** Integer`optional` `Example: 2`

VNI of Traffic Mirror Session. Used for the mirror target to distinguish traffic from different mirror sessions.

* Value range: **1**~**16777215.**

* If not specified, one is assigned randomly.

**PacketLength ** Integer`optional` `Example: 1450`

Data packet size of the traffic mirror session. The minimum range is 64 bytes, and the recommended range is 64 to 1450 bytes. The default is 1500 bytes.

> If the set packet size is ≤ the MTU of the mirror site or \> 1450, some packets may be truncated and the truncated content discarded. To ensure packets are not truncated, it is recommended to set the ENI's MTU value according to the following relationship:

> The MTU of the mirror site ≤ the packet size set in the mirror session ≤ the MTU of the Mirror Target \- 50, and the packet size set in the mirror session must be ≤ 1450.

**TrafficMirrorFilterId ** String必选 `Example: tmf-bp1opxu1zkhn00123****`

ID of the traffic mirror filter.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the traffic mirror filter ID.

**ProjectName ** String`optional` `Example: default`

Name of the project to which the Traffic Mirror Session belongs. If left blank, it defaults to the default project.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N represents the serial number of the tag key. Valid range: 1–50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters in various languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Tag keys of the same resource must be unique.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the user tag.

* N represents the serial number of the tag value. Valid range: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include multilingual characters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.

> **tip**

> To provide this parameter, provide `TagFilters.N.Key` first.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

**Enabled ** Boolean`optional` `Example: true`

Start traffic mirror session.

* true (default): Start.

* false: Do not start.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**TrafficMirrorSessionId ** String`Example: tms-j6cmls82xnc86vtpe****`

The ID of the Traffic Mirror Session.

## Request example

```json
GET /?Action=CreateTrafficMirrorSession&Version=2020-04-01&TrafficMirrorSessionName=TM_Session_1&NetworkInterfaceId=eni-bp1fgnh68xyz9****&TrafficMirrorTargetId=tmt-35bvae1r7rv283dy2w2ll****&Priority=1&TrafficMirrorFilterId=tmf-bp1opxu1zkhn00123**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateTrafficMirrorSession",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TrafficMirrorSessionId": "tms-j6cmls82xnc86vtpe****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description cannot exceed 255 characters. |
|400 |InvalidEni.IPv4Disabled |IPv4 has been disabled for the specified ENI. |IPv4 has been disabled for the specified ENI. |
|400 |InvalidEni.InstanceMismatch |The specified elastic network interface is not attached to the specified instance. |The specified ENI is not bound to the ECS instance. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of ENI cannot process this request. |
|400 |InvalidInstanceSpecification.Malformed |The specified instance does not currently support traffic mirror. |The specified instance does not currently support Traffic Mirror. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidPacketLength.Malformed |The specified MTU is malformed. |The specified MTU is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of the specified ClientToken is invalid. It cannot exceed 64 ASCII characters. |
|400 |InvalidParameter.NetworkInterfaceId |The network interface must not be the source and the target of traffic mirror sessions at the same time. |An ENI cannot serve as both the source and destination of a traffic mirror session simultaneously. |
|400 |InvalidPriority.Malformed |The specified priority is malformed. |The specified priority is invalid. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidTrafficMirrorFilter.InvalidStatus |The specified traffic mirror filter is not in the correct status for the request. |The specified traffic mirror filter is in a state that cannot process this request. |
|400 |InvalidTrafficMirrorTarget.InvalidInstance |The specified traffic mirror target has an invalid instance for the request. |The instance associated with the specified traffic mirror target cannot process this request. |
|400 |InvalidTrafficMirrorTarget.InvalidStatus |The specified traffic mirror target is not in the correct status for the request. |The specified traffic mirror target is in a state that cannot respond to the request. |
|400 |InvalidVirtualNetworkId.Malformed |The specified VNI is malformed. |The specified VNI is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that you can operate per request. |
|400 |MainAccountNotSupportPaypal |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The postpaid product in this order does not support PayPal payment. Please contact the root user to add another payment method. |
|400 |NotPaymentQualified |Your account has not passed the payment qualified yet. |Your account payment verification failed. |
|400 |NotSupportPaypal |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Add other payment methods. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |QuotaExceeded.TrafficMirrorFilterSession |You've reached the limit on the number of traffic mirror sessions per filter that you can create. |The maximum number of mirror sessions that can be associated with each mirror filter has been reached. |
|400 |QuotaExceeded.TrafficMirrorSession |You've reached the limit on the number of traffic mirror sessions that you can create. |The maximum number of traffic mirror sessions that can be created has been reached. |
|400 |QuotaExceeded.TrafficMirrorSourceSession |You've reached the limit on the number of traffic mirror sessions per source that you can create. |The maximum number of mirror sessions that can be associated with each mirror site has been reached. |
|400 |QuotaExceeded.TrafficMirrorTargetSession |You've reached the limit on the number of traffic mirror sessions per target that you can create. |The maximum number of mirror sessions that can be associated with each mirror target has been reached. |
|400 |QuotaExceeded.TrafficMirrorTargetSource |You've reached the limit on the number of traffic mirror sources per target that you can create. |The maximum number of mirror sites that can be associated with each mirror target has been reached. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The request to operate on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The request on the specified instance is denied because the account is in arrears. |
|403 |Forbidden.PurchaseLimited |The account is not authorized to purchase the resource. |This account does not have permission to purchase resources. |
|403 |Forbidden.ShareENI |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface in shared subnet does not support this operation. |No permission to perform actions on the specified ENI. This operation is not supported for the specified ENI in a shared subnet. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified ENI. The specified ENI is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidNetworkInterfaceId.NotFound |The specified traffic mirror source network interface does not exist. |The specified traffic mirror site does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidTrafficMirrorFilter.NotFound |The specified traffic mirror filter does not exist. |The specified Traffic Mirror Filter does not exist. |
|404 |InvalidTrafficMirrorTarget.NotFound |The specified traffic mirror target does not exist. |The specified traffic mirror target does not exist. |
|409 |InvalidTrafficMirrorSessionPriority.Conflict |The specified priority conflicts with another in your traffic mirror session. |The specified mirror session has a priority conflict with another session under its parent traffic mirror session. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
|429 |RateLimited |Too many requests, please try again later. |Too many requests, try again later. |
