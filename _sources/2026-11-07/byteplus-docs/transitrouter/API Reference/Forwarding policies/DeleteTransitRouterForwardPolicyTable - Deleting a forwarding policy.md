---
title: "DeleteTransitRouterForwardPolicyTable - Deleting a forwarding policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterForwardPolicyTable"
---

Call the DeleteTransitRouterForwardPolicyTable API to delete the specified forwarding policy.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterForwardPolicyTable&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|hJR1RP">必选</span> `Example value: DeleteTransitRouterForwardPolicyTable`

The interface name. The current API name is `DeleteTransitRouterForwardPolicyTable`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|4qNtFg">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterForwardPolicyTableId** <span data-label="purple">String</span> <span data-api-tag="require|2wfhYD">必选</span> `Example value: tr-fpt-hy13n2l4c6c0v****`

ID of the forwarding policy. You can call the [DescribeTransitRouterForwardPolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyTables) API to get the ID of the forwarding policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterForwardPolicyTable&Version=2020-04-01&TransitRouterForwardPolicyTableId=tr-fpt-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T034154Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2025081511415821005306422424B45D",
        "Action": "DeleteTransitRouterForwardPolicyTable",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterForwardPolicyTable.InvalidStatus |The specified Transit Router forward policy table is not in the correct status for the request. |The specified forwarding policy cannot respond to this request due to its status. |
|400 |InvalidTransitRouterForwardPolicyTable.WithAssociation |The specified forward policy table has been used by Transit Router attachments, and cannot be deleted. |The specified TR forwarding policy is in use by a network instance attachment and cannot be deleted. |
|400 |InvalidTransitRouterForwardPolicyTable.WithForwardPolicyEntry |The specified forward policy table has configured entries, and cannot be deleted. |The specified TR forwarding policy has configured policy entries and cannot be deleted. |
|404 |InvalidTransitRouterForwardPolicyTable.NotFound |The specified Transit Router forward policy table does not exist. |The specified forwarding policy does not exist. |
