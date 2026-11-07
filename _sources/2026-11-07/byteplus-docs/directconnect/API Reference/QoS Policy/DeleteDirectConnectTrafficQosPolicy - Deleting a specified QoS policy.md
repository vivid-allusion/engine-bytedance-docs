---
title: "DeleteDirectConnectTrafficQosPolicy - Deleting a specified QoS policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosPolicy"
---

Call DeleteDirectConnectTrafficQosPolicy to delete a specified QoS policy.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

The QoS policy to be deleted is not associated with any Direct Connect (DC) Connections, and contains no traffic queues other than the default queue (named **Default**). If present, first disassociate all DC Connections associated with the QoS policy and delete the traffic queues before deleting the QoS policy. You can call [ModifyDirectConnectTrafficQosPolicyAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosPolicyAttributes) to disassociate the DC Connection and [DeleteDirectConnectTrafficQosQueue](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosQueue) to delete the traffic queue.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectTrafficQosPolicy&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|evK3lV">必选</span> `Example: DeleteDirectConnectTrafficQosPolicy`

The interface name. The current API name is `DeleteDirectConnectTrafficQosPolicy`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|6BEMTy">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|iZ7jzx">必选</span> `Example: dcq-a2du7fojk17****`

The ID of the QoS policy to be deleted.

You can call the [DescribeDirectConnectTrafficQosPolicies](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosPolicies) API to query the QoS policy ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectTrafficQosPolicy&Version=2020-04-01&DirectConnectTrafficQosPolicyId=dcq-2fezrjmq3vif459gp67**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202411071550407A413E6A9D8BD4****",
        "Action": "DeleteDirectConnectTrafficQosPolicy",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202411071550407A413E6A9D8BD4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosPolicy.WithAssociation |The specified traffic qos policy is in use. If you are trying to delete the traffic qos policy, ensure that its associated direct connect connections have been detached. |The specified QoS policy is in use. Before attempting to delete a QoS policy, ensure all associated DC Connections have been disassociated. |
|400 |InvalidDirectConnectTrafficQosPolicy.WithTrafficQosQueue |The specified traffic qos policy is in use. If you are trying to delete the traffic qos policy, ensure that its traffic qos queues have been deleted. |The specified QoS policy is in use. Before attempting to delete a QoS policy, ensure all associated traffic queues have been deleted. |
|400 |QuotaExceeded.DcTrafficQosPolicy |You've reached the limit on the number of traffic qos policies that you can create. |You have reached the maximum number of QoS policies that can be created. |
|404 |InvalidDirectConnectTrafficQosPolicy.NotFound |The specified direct connect traffic qos policy does not exist. |The specified QoS policy does not exist. |
