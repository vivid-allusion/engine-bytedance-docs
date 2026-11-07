---
title: "UntagNLBResources - Deleting a custom tag from NLB resources"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/UntagNLBResources"
---

You can call the UntagNLBResources API to delete custom tags from NLB resources.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagNLBResources&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|PsoV3J">必选</span> `Example: UntagNLBResources`

Action to execute. Set the value to UntagNLBResources.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|1fw7Yf">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ResourceType ** <span data-label="purple">String </span><span data-api-tag="require|D4pkxw">必选</span> `Example: nlb`

The resource type. Valid values:


* nlb: NLB instance.

* nlb_listener: Listener.

* nlb_servergroup: Server group.

* nlb_security_policy: TLS custom security policy.



**ResourceIds.N ** <span data-label="purple">String </span><span data-api-tag="require|yShPR3">必选</span> `Example: nlb-273sdsdswrfdp8u2j****`

The resource ID.


* Parameter \- N: Represents the serial number of the resource ID, ranging from 1 to 20.

* Separate multiple resource IDs with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers">DescribeNetworkLoadBalancers</a> API to query the ID of the NLB instance.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners">DescribeNLBListeners</a> API to query the ID of the listener.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups">DescribeNLBServerGroups</a> API to query the ID of the server group.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies">DescribeNLBSecurityPolicies</a> API to query the ID of the TLS custom security policy.</div>




**TagKeys.N ** <span data-label="purple">String </span><span data-api-tag="require|6c3VVY">必选</span> `Example: k1`

The key of the custom tag to be deleted. Must not start or end with a space.


* Parameter \- N specifies the serial number of the tag key. The value ranges from 1 to 20.

* Separate multiple tag keys with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the specified <code>TagKeys.N</code> does not exist or are already unbound, the operation returns success by default without reporting an error.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=UntagNLBResources&Version=2020-04-01&ResourceType=nlb&ResourceIds.1=nlb-273sdsdswrfdp8u2j****&TagKeys.1=k1 HTTP/1.1
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
        "Action": "UntagNLBResources",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
