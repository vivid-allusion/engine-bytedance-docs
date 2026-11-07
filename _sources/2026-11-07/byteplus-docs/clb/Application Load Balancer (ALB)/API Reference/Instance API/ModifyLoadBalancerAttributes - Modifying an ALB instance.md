---
title: "ModifyLoadBalancerAttributes - Modifying an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-ModifyLoadBalancerAttributes"
---

Call the ModifyLoadBalancerAttributes API to modify the ALB instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Submit up to 10 API requests per second.

* If the following optional parameters are not configured, the existing configurations will be preserved.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyLoadBalancerAttributes&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|FtGcs5">必选</span> `Example: ModifyLoadBalancerAttributes`

Action to execute. Set the value to ModifyLoadBalancerAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|qZGIzC">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**Description ** <span data-label="purple">string </span>`optional` `Example: This is an ALB instance`

Description of the ALB instance.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 255 characters.



**DeleteProtection ** <span data-label="purple">string </span>`optional` `Example: off`

ALB delete protection feature.


* off: Disable.

* on: Enable.



**LoadBalancerName ** <span data-label="purple">string </span>`optional` `Example: alb-test1`

Name of the ALB instance.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.



**WafProtectionEnabled ** <span data-label="purple">string </span>`optional` `Example: off`

WAF protection switch.


* off: Disable.

* on: Enable.



**WafInstanceId ** <span data-label="purple">string </span>`optional` `Example: waf-14ca6f67c33c09****`

The ID of the WAF security protection instance bound to the ALB instance.



**WafProtectedDomain ** <span data-label="purple">string </span>`optional` `Example: www.test.com`

WAF protection domain name.


* When WafProtectionEnabled is set to on, this parameter is optional; when it is set to off, this parameter is invalid.

* Supports exact domain names and wildcard domain names.



**GlobalAccelerator.AcceleratorId ** <span data-label="purple">string </span>`optional` `Example: accinstance-VYjG****`

Global accelerator ID.



**GlobalAccelerator.AcceleratorListenerId ** <span data-label="purple">string </span>`optional` `Example: listener-rrhN7WbeeYo****`

The ID of the global accelerator listener.



**GlobalAccelerator.EndpointGroupId** <span data-label="purple">string</span> `optional` `Example: endpointgroup-NoT****`

ID of the endpoint group.



**GlobalAccelerator.Weight ** <span data-label="purple">integer </span>`optional` `Example: 100`

Traffic distribution weight of the endpoint. Value range: 1\-100.



**ModificationProtectionReason ** <span data-label="purple">string </span>`optional` `Example: This is modification protection`

Fill in the reason for enabling instance modification protection.


* Must start with a letter or Chinese character and may include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Length limit: 0 to 128 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The value of the <code>ModificationProtectionReason</code> parameter is valid only when the <code>ModificationProtectionStatus</code> parameter is set to <code>ConsoleProtection</code>.</div>


* <div data-tips="true" data-tips-type="tip">When the <code>ModificationProtectionStatus</code> parameter is set to <code>NonProtection</code>, any previously configured value of the <code>ModificationProtectionReason</code> parameter will be cleared.</div>




**ModificationProtectionStatus ** <span data-label="purple">string </span>`optional` `Example: NonProtection`

Enable instance modification protection feature. Valid values:


* NonProtection: Disable.

* ConsoleProtection: Enable. After enabling this, you cannot modify the instance configuration through the ALB console; you can only modify the instance configuration by calling the API.



**ProxyProtocolEnabled ** <span data-label="purple">string </span>`optional` `Example: off`

ALB supports the Proxy Protocol and can record the client's real IP address.


* off: Disable Proxy protocol.

* on: Enable Proxy protocol.



**LoadBalancerId ** <span data-label="purple">string </span><span data-api-tag="require|IaVMLZ">必选</span> `Example: alb-bp1b6c719dfa08ex****`

ALB instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifyLoadBalancerAttributes&Version=2020-04-01&Description=test&LoadBalancerId=alb-bp1b6c719dfa08ex****&LoadBalancerName=lb1 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyLoadBalancerAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidDeleteProtection.Malformed |The specified DeleteProtection is malformed. |The specified DeleteProtection parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |InvalidWafProtectionEnabled.Malformed |The specified WafProtectionEnabled is malformed. |The specified WafProtectionEnabled parameter format is invalid. |
|400 |InvalidWafInstanceId.Malformed |The specified WafInstanceId is malformed. |The specified WafInstanceId parameter format is invalid. |
|400 |InvalidWafProtectedDomain.Malformed |The specified WafProtectedDomain is malformed. |The specified WafProtectedDomain parameter format is invalid. |
|400 |LimitExceed.WafProtectedDomain |You've reached the limit on the number of domain you can associate with the waf instance. |The maximum number of protection domain names that can be added to a single WAF instance has been reached. |
|400 |OperationFailed.QueryWafService |The request on the specified resource failed due to the query on WAF Service failed. |The request to operate on this resource failed because the WAF request failed. |
|400 |OperationDenied.WafProtectionOnLocalZoneNotSupported |The request on the specified LoadBalancer is denied due to the LoadBalancer with WAF Protection is not allowed to be deployed on local zone. |Because WAF security protection can only be enabled on ALB instances deployed in standard availability zones, the operation request for this ALB instance is rejected. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|409 |InvalidWafProtectedDomain.Conflict |The specified WafProtectedDomain already exists. |The specified WAF protection domain already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
