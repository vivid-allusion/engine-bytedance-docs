---
title: "ModifyNetworkLoadBalancerAccessLog - Configuring an access log"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAccessLog"
---

Call the ModifyNetworkLoadBalancerAccessLog API to configure access logs.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNetworkLoadBalancerAccessLog&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|irQgTK">必选</span> `Example: ModifyNetworkLoadBalancerAccessLog`

Action to execute. Set the value to ModifyNetworkLoadBalancerAccessLog.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|RysrXC">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|gmqG7t">必选</span> `Example: nlb-bp1o94dp5i6ea****`

The ID of the NLB instance.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.



**AccessLogEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Enable access log.


* true: Yes

* false: No



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: fc6953c1-fe50-43aa-9d26-c1e0a207****`

The ID of the log project.



**TopicName ** <span data-label="purple">String </span>`optional` `Example: 74936ae4-bbd6-41de-a0d2-ed156203****`

The ID of the log topic.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202409295332201042142000A01EA****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyNetworkLoadBalancerAccessLog&Version=2020-04-01&LoadBalancerId=nlb-bp1o94dp5i6ea****&AccessLogEnabled=true&ProjectName=fc6953c1-fe50-43aa-9d26-c1e0a207****&TopicName=74936ae4-bbd6-41de-a0d2-ed156203**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNetworkLoadBalancerAccessLog",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202409295332201042142000A01EA****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidAccessLogEnabled.Malformed |The specified AccessLogEnabled is malformed. |The specified AccessLogEnabled parameter format is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified load balancer cannot respond to this request due to its billing status. |
|400 |InvalidProjectName.AccessLogEnabledMismatch |The specified ProjectName is not matched with AccessLogEnabled. |The specified ProjectName does not match AccessLogEnabled. |
|400 |InvalidProjectName.UsedInOtherService |The specified Project has been used in other service. |The specified Project is already in use by another cloud service. |
|400 |InvalidSite.NotSupportEnableAccessLog |The specified site does not support enable access log. |The access log is not enabled in the specified account's home region. |
|400 |InvalidTopicName.AccessLogEnabledMismatch |The specified TopicName is not matched with AccessLogEnabled. |The specified TopicName does not match AccessLogEnabled. |
|400 |InvalidTopicName.UsedInOtherService |The specified Topic has been used in other service. |The specified Topic is already in use by another cloud service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |ServiceRoleForNLBLogDelivery.NotFound |ServiceRoleForNLBLogDelivery does not exist. |The NLB log delivery service role does not exist. |
|409 |InvalidTLSOperation.Conflict |Interaction with TLS services has resource conflict. |A resource conflict occurred during the interaction with the TLS service. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
