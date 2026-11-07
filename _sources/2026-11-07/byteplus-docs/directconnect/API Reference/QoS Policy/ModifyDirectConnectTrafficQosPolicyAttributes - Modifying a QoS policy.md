---
title: "ModifyDirectConnectTrafficQosPolicyAttributes - Modifying a QoS policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosPolicyAttributes"
---

Call ModifyDirectConnectTrafficQosPolicyAttributes to modify a QoS policy.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You can call this API, and specify AddInstanceIds.N to associate a DC Connection with the QoS policy, and RemoveInstanceIds.N to disassociate associated DC Connections.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectTrafficQosPolicyAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|jX7Bng">必选</span> `Example: ModifyDirectConnectTrafficQosPolicyAttributes`

The interface name. The current API name is `ModifyDirectConnectTrafficQosPolicyAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|VeB8uv">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|Iy2Sr6">必选</span> `Example: dcq-123456`

The ID of the QoS Policy.



**DirectConnectTrafficQosPolicyName ** <span data-label="purple">String </span>`optional` `Example: dcq-name`

The name of the QoS policy.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, the original configuration remains.



**Description ** <span data-label="purple">String </span>`optional` `Example: dcq-describe`

The description of the QoS policy.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, the original configuration remains.



**AddInstanceIds.N ** <span data-label="purple">String </span>`optional` `Example: dcc-ojk17q****`

The ID of the DC Connection with which the QoS policy is to be associated.


* N represents the sequence number of a DC Connection ID.

* Separate multiple IDs with ampersands (&).

* If left blank, the original configuration remains.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A QoS policy can be associated only with DC Connections, not with Shared Lines.</div>




**RemoveInstanceIds.N ** <span data-label="purple">String </span>`optional` `Example: dcc-jjfftzh4b****`

The ID of the DC Connection from which the QoS policy is to be disassociated.


* N represents the sequence number of a DC Connection ID.

* Separate multiple IDs with ampersands (&).

* If left blank, the original configuration remains.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectTrafficQosPolicyAttributes&Version=2020-04-01&DirectConnectTrafficQosPolicyId=dcq-123456&DirectConnectTrafficQosPolicyName=dcq-name&Description=dcq-describe&AddInstanceIds.1=dcc-ojk17q****&RemoveInstanceIds.1=dcc-jjfftzh4b**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241107160027257DCF867CC69261****",
        "Action": "ModifyDirectConnectTrafficQosPolicyAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20241107160027257DCF867CC69261****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosPolicy.ConflictQos |The specified direct connect connection has associate with other traffic qos policy. |The specified DC Connection is already associated with a QoS policy. Duplicate association is not supported. |
|400 |InvalidDirectConnectTrafficQosPolicy.DirectConnectConnectionWithDifferentQos |In the direct connect gateway with multiple direct connect connections scene, it is not supported to associate with different qos policy in all direct connect connections. |When multiple DC Connections are associated with the same DC Gateway, all DC Connections must have the same QoS Policy. |
|400 |InvalidDirectConnectTrafficQosPolicy.DirectConnectConnectionWithSharedVif |It is not supported to associate the qos policy for direct connect connection associated with shared direct connect virtual interfaces. |The DC Connection associated with a Shared Virtual Interface does not support associating QoS policies. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosPolicy.MisMatchQos |The specified direct connect connection doesn't associate with the specified traffic qos policy. |The specified QoS policy is not associated with the DC Connection. Disassociation is not supported. |
|400 |InvalidDirectConnectTrafficQosPolicy.SameDirectConnectConnectionUnsupported |It is not supported to associate and disassociate the same direct connect connection to the specified traffic qos policy. |A DC Connection does not support simultaneous QoS policy association and disassociation. |
|400 |InvalidDirectConnectTrafficQosPolicy.SharedConnectionUnsupported |It is not supported to associate the shared direct connect connection to the specified traffic qos policy. |Shared Lines does not support associating QoS policies. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|403 |InvalidDirectConnectTrafficQosPolicy.SharedDirectConnectConnectionForbidden |You are not authorized to associate the specified traffic qos policy with direct connect connection with shared connection. |No permission to associate a QoS policy with a Direct Connect (DC) Connection that already hosts a Shared Line. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|404 |InvalidDirectConnectTrafficQosPolicy.NotFound |The specified direct connect traffic qos policy does not exist. |The specified QoS policy does not exist. |
